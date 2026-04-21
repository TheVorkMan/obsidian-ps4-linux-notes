
## Getting the KLogs
0. Get your PS4 IP Address
1. Load GoldHEN, then enable the "Enable TTY Redirect" from KLog options in GoldHEN settings.
   ![[Pasted image 20260410232405.png]] 
2. Use a separate device to gather the logs.
#### PuTTY for Windows:
0. Enter IP Address of you PS4, enter Port 3232, and choose `Other:`, and in drop down menu choose `Telnet`
   ![[Pasted image 20260421030011.png]]
1. Go to `Logging`
   ![[Pasted image 20260421030019.png]]
2. Create file, and select it here.
   ![[Pasted image 20260421030045.png]]
3. You can also Save sessions - enter the name, and click save 
   ![[Pasted image 20260421030051.png]]
4. After that - you can just click on the Session and `Load` to have everything put up again as it was.
   ![[Pasted image 20260421030608.png]]

#### `nc` on Linux
Or just with`nc -v YOUR_PS4_IP_ADDRESS 3232`

## SSH
This allows you to access console remotely, and also works when GPU driver crashes.
1. Enable `sshd`. It will be also load on every startup
```sh
systemctl enable --now sshd
```
2. Go to `PuTTY` and enter your IP address and port `22` to access it remotely.
   
3. *Or use Linux*, `ssh YOURUSERONPS4@your_ps4_address`
## Journalctl
This will output full journal from the end (`-b`) and follows with the changes (`-f`). 
You can use this with SSH to get logs when GPU driver crashes!
```bash
journalctl -b -f
```

