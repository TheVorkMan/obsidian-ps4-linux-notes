#### Here is my saved texts that would be useful for others.

"Tierlist" by @erkki_69_men.com:
![[ps4linux_tierlist.webp]]


@saya0137:
"- Then... the high versions of Mesa on PS4... won't give you much on PS4 Linux...

 OpenGL shows 40% of the register gains included in the bzImage kernel. 
 
 The gains for Vulkan may already be due if you integrate gamer patches into the kernel source before generating your bzImage. 
 
 Mesa 20.0.2 already does a great job, but doesn't have DX11... then from 21.x onwards you can have DX11... and since Mesa 22.1.7... nothing new... but if Linux distributions update, you're forced to use a high version of Mesa to align with the distribution's LLVM version. 
 
 Paradoxically, on Mint they take their time... and you can have Mesa 25 with LLVM 17... the distribution I'm going to release is ready. The links, and the video... I just need to find the time to write the news article... 
 
 One thing to know, Steam has problems after Mesa 24 according to vvsx87... And as for Cemu (Wii U emulator), on Debian/Mint, if you go beyond Mesa 24.1.6 (I don't know about other distributions) there will be artifacts when using Vulkan (no problem with OpenGL 4.6)."


Me:
"DXVK hangs the system, sometimes at some points. Unclear.
NFSMW: windowed mode kinda helps? gamescope delay the hang until you close it and then dmesg start outputing get bridges from ps4 video driver and hang?
Mesa is a piece of quirky shit.
Gamescope has issues?
Steam overlay doesn't work good with wayland when steam client is in big picture and fullscreened.
To compile it, you need to use linux, if ps4 hangs - use different machine, you can compile it with WSL2 btw. Compile mesa-ps4 first, install it, then compile the lib32-mesa-ps4. Use this: https://github.com/DionKill/ps4-video-archlinux
Mesa 25.1 and higher require libdrm 124
It doesn't affect the hanging though I think
Proton Experimental on sleeping dogs has some magical abilities?
Need to test it on debian..."

Dionkill:
"(NFS MW 2005) i think it should work via lutris / bottles, you need to reinstall the game on the system (can't use a preinstalled version for some reason), and you need to use proton 8 or something like that"

Regarding GPU Resets that hang the PS4:
`isaacmv` and `mircoho`
"Do you know if that's a mesa thing or kerel thing?"
"both, if mesa is running well and correctly patched it would not happen, and if kernel 100% right setting for gpu reset, it should work too
On Aeolia no problem though." That means, it's an issue on Belize?

"The 25.1 manjaro doesn't provide ACO nor compatibility with dxvk 2.7"
"is do testing with mesa-25.0.2-rc3"
"25.2 frezzes for me while using dxvk"

