### Linux payload on GoldHEN 2.4b18.8 crashes PS4
@saya0137:
"I had the same problem... I was loading Goldhen, then loading the Pro Linux payload via Netcat on a PC (Binloader).

And at one point on PS4 pro 9.00, I got a black screen and the console shut down immediately... even after 5 consecutive attempts. I then loaded the Pro Linux payload.bin directly using the Lapse Blu-ray exploit, and I was finally able to reload Linux. I then put Goldhen back in the Lapse Blu-ray slot as the first boot device, and loading the Linux payload via Netcat on a PC (Binloader) started working again.

I also had a workaround: load the 9.00 USB exploit, load the Kameleon host, and then boot directly into Linux."

### GPU resets hangs the PS4
Belize thing? Maybe a regression for modern kernels (above 5.4)
Debug trigger:
`sudo cat /sys/kernel/debug/dri/0/amdgpu_gpu_recover`
Need for Speed: Most Wanted, Sleeping Dogs when used with DXVK trigger GPU reset? Similiar behaviour.