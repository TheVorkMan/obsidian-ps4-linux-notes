## SSH
This allows you to access console remotely, and also works when GPU driver crashes.
1. Enable `sshd` on your PS4 system. It will be also load on every startup
```sh
sudo systemctl enable --now sshd
```
2. **Windows:** Go to `PuTTY` and enter your IP address and port `22` to access it remotely. Should look like this:
   ![[Pasted image 20260501143308.png]]
   
3. **Linux:** `ssh USERNAME@PS4_IP`
## Journalctl
This will output full journal from the end (`-b`) and follows with the changes (`-f`). 
You can use this with SSH to get logs when GPU driver crashes!
```bash
journalctl -b -f
```
## KLogs
0. Get your PS4 IP Address
1. Load GoldHEN, then enable the "Enable TTY Redirect" from KLog options in GoldHEN settings.
   ![[Pasted image 20260410232405.png]] 
2. Use a separate device to gather the logs.
#### Netcat - Multiplatform
0. **Linux:** Check if `netcat` installed on your distribution.
   **Windows:** Download and install Nmap - https://nmap.org/download.html
1. **Linux:** Go in terminal and execute: `nc -v PS4_IP 3232`
   **Windows:** Go in CMD and execute `ncat -v PS4_IP 3232`
#### PuTTY for Windows:
0. [Download](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), install, and open PuTTY
   Enter IP Address of you PS4, enter Port 3232, and choose `Other:`, and in drop down menu choose `Telnet`
   ![[Pasted image 20260421030011.png]]
1. Go to `Logging`
   ![[Pasted image 20260421030019.png]]
2. Create file, and select it here.
   ![[Pasted image 20260421030045.png]]
3. You can also Save sessions - enter the name, and click save 
   ![[Pasted image 20260421030051.png]]
4. After that - you can just click on the Session and `Load` to have everything put up again as it was.
   ![[Pasted image 20260421030608.png]]
5. Click on `Open` to Open a connection.
