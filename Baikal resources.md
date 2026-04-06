### Links
#### Mesa 25.1.1 (for Baikal)
libdrm 124, mesa 25.1.1 with llvm 19 that works on Baikal. Was compiled by `@deWaardt` 
https://github.com/deWaardt/ps4-baikal-graphics/tree/main.
Compiled for Arch package system, you can install it on other distros by extracting archive and manually replacing library files with root access.
On Arch, you can install them with terminal. Open it up, type `sudo pacman -U` and then select all package files and drag them from file manager to terminal. It will type them after the command.

##### `@deWaardt` quote regarding GPU drivers (can ALSO be applied? to other Soutbridges):
These packages in general work, but there’s still instability.
While you might still have a crash here and there, limiting gtt memory seems to help stability a lot.

To do that, on the fat32 partition of your usb drive (or wherever you keep bzImage):
Make a file `bootargs.txt`, and put in: `amdgpu.gttsize=<the size of the payload you’re using>`

So if you use 2gb payload

`amdgpu.gttsize=2048`

If you’re unsure, use

`andgpu.gttsize=1024`
