### DXVK crashes GPU driver (PS4 gets unresponsive)
GPU resets doesn't work - belize thing? Maybe a regression for modern kernels (above 5.4).
~~Debug trigger:~~
~~`sudo cat /sys/kernel/debug/dri/0/amdgpu_gpu_recover`~~
DXVK above 1.10.3 (uses an older Vulkan API) doesn't crash the driver. Use Proton-Sarek.
(performance hit due to an older Vulkan, but what can you do.)
How to reproduce: Install Need for Speed: Most Wanted with Widescreen Fix mod and run it with DXVK 2.6
An example `dmesg` output when driver crashes (with `amdgpu.lockup_timeout=20000 amdgpu.gpu_recovery=0` bootargs set):
```
[  238.672455] amdgpu 0000:00:01.0: amdgpu: Dumping IP State
[  238.672465] amdgpu 0000:00:01.0: amdgpu: Dumping IP State Completed
[  238.672548] amdgpu 0000:00:01.0: amdgpu: [drm] AMDGPU device coredump file has been created
[  238.672552] amdgpu 0000:00:01.0: amdgpu: [drm] Check your /sys/class/drm/card0/device/devcoredump/data
[  238.672556] amdgpu 0000:00:01.0: amdgpu: ring comp_1.1.0 timeout, signaled seq=23, emitted seq=24
[  238.672560] amdgpu 0000:00:01.0: amdgpu: Process information: process speed.exe pid 2260 thread dxvk-submit pid 2303
[  238.672565] amdgpu 0000:00:01.0: amdgpu: GPU recovery disabled.
```
### Linux payload on GoldHEN 2.4b18.8 crashes PS4
@saya0137:
"I had the same problem... I was loading Goldhen, then loading the Pro Linux payload via Netcat on a PC (Binloader).

And at one point on PS4 pro 9.00, I got a black screen and the console shut down immediately... even after 5 consecutive attempts. I then loaded the Pro Linux payload.bin directly using the Lapse Blu-ray exploit, and I was finally able to reload Linux. I then put Goldhen back in the Lapse Blu-ray slot as the first boot device, and loading the Linux payload via Netcat on a PC (Binloader) started working again.

I also had a workaround: load the 9.00 USB exploit, load the Kameleon host, and then boot directly into Linux."