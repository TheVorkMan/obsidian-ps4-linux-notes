### Max kernel logs
`loglevel=8 drm.debug=0x1ff amdgpu.debug=0x1ff`

### Persistent logs
Check:
`ls /var/log/journal`
If none, make:
`sudo mkdir -p /var/log/journal`
`sudo systemctl restart systemd-journald`

`journalctl -b -1 -k`

### netconsole
`nc -klu 6666`
`modprobe netconsole netconsole=@/,@192.168.0.134/6666`

### Enable SysRq
`echo 1 | sudo tee /proc/sys/kernel/sysrq`

### DXVK Logs
`export DXVK_LOG_LEVEL=debug
`export DXVK_LOG_PATH=~/dxvk_logs`

`ls ~/dxvk_logs`
