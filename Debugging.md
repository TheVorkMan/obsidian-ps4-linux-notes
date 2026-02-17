### Max kernel logs
```bash
loglevel=8 drm.debug=0x1ff amdgpu.debug=0x1ff
```
### DXVK Logs
```bash
export DXVK_LOG_LEVEL=debug
export DXVK_LOG_PATH=~/dxvk_logs
ls ~/dxvk_logs
```
## Dmesg
```bash
dmesg -w
```

## Journalctl
```bash
journalctl -b -f
```
## Klog
https://consolemods.org/wiki/PS4:FAQ#How_can_I_get_Klogs?
