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

## What to expect from further development
Right now, we are using solution that hurts GPU (?) on Belize and some changes are necessary.
As @idemetris found out, you can use vanilla Mesa and libdrm, and just patch kernel, with different GPU code for Belize 0x9924 GPU (it's being the Polaris10 instead of Gladius).
Right now, this is doubtable, and testing is being done.
@idemetris:

`Gladius = gfx803`
`You don't need to inject a new variant into the driver`
`Will work 💯 as it is`

`In theory you can use the Polaris firmware blobs as well and all driver capabilities will be open. If those doesn't work you need to disable two specific functions in the driver that sony blobs don't support`

```diff
From 8fe8a46ac4ffbcecdb5ca10f1ad3a09fdf2392a3 Mon Sep 17 00:00:00 2001
From: Demetris Ierokipides <ierokipides.dem@gmail.com>
Date: Sat, 14 Feb 2026 00:54:22 +0200
Subject: [PATCH] Add kernel support for PS4 Pro Gladius GPU (neo)

---
 drivers/gpu/drm/amd/amdgpu/amdgpu_drv.c | 1 +
 1 file changed, 1 insertion(+)

diff --git a/drivers/gpu/drm/amd/amdgpu/amdgpu_drv.c b/drivers/gpu/drm/amd/amdgpu/amdgpu_drv.c
index 7333e1929..0ec9cf05b 100644
--- a/drivers/gpu/drm/amd/amdgpu/amdgpu_drv.c
+++ b/drivers/gpu/drm/amd/amdgpu/amdgpu_drv.c
@@ -2046,6 +2046,7 @@ static const struct pci_device_id pciidlist[] = {
 	{0x1002, 0x67CC, PCI_ANY_ID, PCI_ANY_ID, 0, 0, CHIP_POLARIS10},
 	{0x1002, 0x67CF, PCI_ANY_ID, PCI_ANY_ID, 0, 0, CHIP_POLARIS10},
 	{0x1002, 0x6FDF, PCI_ANY_ID, PCI_ANY_ID, 0, 0, CHIP_POLARIS10},
+	{0x1002, 0x9924, PCI_ANY_ID, PCI_ANY_ID, 0, 0, CHIP_POLARIS10},
 	/* Polaris12 */
 	{0x1002, 0x6980, PCI_ANY_ID, PCI_ANY_ID, 0, 0, CHIP_POLARIS12},
 	{0x1002, 0x6981, PCI_ANY_ID, PCI_ANY_ID, 0, 0, CHIP_POLARIS12},
-- 
2.43.0

```
`this is for 6.18.x lts kernel`