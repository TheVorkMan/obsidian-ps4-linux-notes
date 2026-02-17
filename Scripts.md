## Auto-reconnect DS4 script
```bash
#!/bin/bash


#             C  O  N  F  I  G
#-------------------------------------------
# MAC address of your DualShock 4 controller
DS4_MAC="XX:XX:XX:XX:XX:XX"
# Delay between retries
RETRY_DELAY=3
#-------------------------------------------


# Ensure Bluetooth is powered on
bluetoothctl power on

echo "Resetting previous connection state..."
# Disconnect if connected
bluetoothctl disconnect $DS4_MAC >/dev/null 2>&1
# Remove device from bluetooth cache
bluetoothctl remove $DS4_MAC >/dev/null 2>&1

echo "Starting DS4 auto-connect service..."

is_connected() {
    bluetoothctl info "$DS4_MAC" 2>/dev/null | grep -q "Connected: yes"
}

while true; do
    # Small delay to let stack settle
    sleep 2

    if is_connected; then
        # Controller is connected, nothing to do
        sleep "$CHECK_INTERVAL"
        continue
    fi

    echo "Scanning for controller..."
    bluetoothctl scan on >/dev/null 2>&1 &
    SCAN_PID=$!

    sleep 4

    kill $SCAN_PID >/dev/null 2>&1

    echo "Re-pairing controller..."
    bluetoothctl pair $DS4_MAC
    bluetoothctl trust $DS4_MAC
    bluetoothctl connect $DS4_MAC

    if is_connected; then
        echo "Controller connected successfully!"
        continue
    fi

    echo "Connection failed. Retrying in $RETRY_DELAY seconds..."
    sleep $RETRY_DELAY
done
```
## Patch for disabling sr0 (Blu-Ray drive)
Use this on initramfs you want to patch
```bash
#!/bin/sh
set -e

IN="$1"
OUT="$2"
WORKDIR="initramfs-temp.work"

[ -z "$IN" ] || [ -z "$OUT" ] && {
    echo "usage: $0 input.cpio.gz output.cpio.gz"
    exit 1
}

[ -e "$WORKDIR" ] && {
    echo "$WORKDIR already exists, remove to proceed."
    exit 1
}

mkdir "$WORKDIR"
cd "$WORKDIR"

zcat "../$IN" | cpio -id

PATCH='
# Disabling /dev/sr0 to prevent Blu-Ray Drive from showing up.
if [ -e /sys/block/sr0/device/delete ]; then
    echo 1 > /sys/block/sr0/device/delete
fi
'

awk -v patch="$PATCH" '
{ print }
$0 ~ /^emount[ \t]+\/proc[ \t]+\/sys/ { print patch }
' init > init.new

chmod --reference=init init.new
mv init.new init

find . -print0 \
 | cpio --null -ov --format=newc \
 | gzip -9 > "../$OUT"

rm -rf ./$WORKDIR
echo "Patched successfully."
```
