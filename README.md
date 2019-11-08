[![](https://cdn.rawgit.com/linuxenko/linuxenko.github.io/master/media/skylake/video-fix.png)](https://cdn.rawgit.com/linuxenko/linuxenko.github.io/master/media/skylake/video-fix.png)

Skylake (Intel HD530/HD520) video fix for Linux<br />

> 00:02.0 VGA compatible controller: Intel Corporation Sky Lake Integrated Graphics (rev 06)

The problem :<br />
 * skype video calls become unusable.<br />
 * blue lines<br />
 * vlc, openshot, skype video always on top<br />
 * video does not resizable<br />
 * etc..<br />


Tested on:  <br />
     * ubuntu trusty tahr ([14.04](https://github.com/linuxenko/ubuntu-skylake-i915-video-fix/issues/21)) <br />
     * ubuntu wily (15.10)  <br />
     * ubuntu xenial (16.04) ([4.3.5 kernel](https://github.com/linuxenko/ubuntu-skylake-i915-video-fix/issues/9))  <br />
     * ubuntu xenial (16.04) (4.6 kernel) <br />
     * ubuntu xenial (16.04) ([4.7.6 kernel](#kern-4.7.6)) <br />
     * deepin linux (15.3) (4.4 kernel)
     
## installation <br />

* Copy 20-intel.conf from repository to /usr/share/X11/xorg.conf.d/20-intel.conf <br />
* Restart / reboot the system <br />

Lazy fix:
```
cd /tmp
wget https://github.com/linuxenko/ubuntu-skylake-i915-video-fix/releases/download/v1/20-intel.conf
sudo cp 20-intel.conf /usr/share/X11/xorg.conf.d/20-intel.conf
```
And restart system then. <br />

### Kernel 4.2.0-x  -  4.3.x issues

 * Very unstable driver when using opengl or playing [games](https://github.com/linuxenko/ubuntu-skylake-i915-video-fix/issues/2).
 * With 4.2 system can stuck even watching youtube videos.

### Kernel - 4.4.x issues

 * Looks like very unstable, sometimes freeze whole system without any reason. I don't use it anymore, 4.3.x is more stable.
 * Monitor flickering at boot time, before it start Xorg server it blinks. (4.4.x only problem)
 * Firefox webgl rendering [crush](https://github.com/linuxenko/ubuntu-skylake-i915-video-fix/issues/4) <br />

> W: Possible missing firmware /lib/firmware/i915/skl_guc_ver4.bin for module i915 [issue](https://github.com/linuxenko/ubuntu-skylake-i915-video-fix/issues/3). <br />

FIX:<br />
 Download and install [firmware](https://01.org/linuxgraphics/downloads/sklgucver43).<br />

```
cd /tmp
wget https://01.org/sites/default/files/downloads/intelr-graphics-linux/sklgucver43.tar.bz2
tar xf sklgucver43.tar.bz2
cd skl_guc_ver4_3/ ; sudo ./install.sh
sudo update-initramfs -u -k all
```

### Kernel - 4.6.X

  * 4.6 kernel from the Ubuntu kernel-ppa/mainline/v4.6-yakkety seems very stable with no system hangs/video freeze.
  * Some graphic glitches remain which are fixed by adding `Option "XVideo" "Disable"` in the `Extensions` Section of your xorg.conf file.
  * Installation:

    * Download and install `linux-headers-4.6.0-xxx_all.deb` , `linux-headers-4.6.0-xxx-generic_xxx_i386/amd64.deb`  
    and `linux-image-4.6.0-xxx-generic_xxx_i386/amd64.deb`
    from [kernel-ppa/mainline/v4.6-yakkety](http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.6-yakkety/)
    * You also might want to prevent Installation of future 4.4 kernel updates  
    with `sudo apt-mark hold linux-image-generic linux-headers-generic`

### Kernel - 4.7.6 <a name="kern-4.7.6"></a>

  * 4.7.6 kernel from kernel-ppa/mainline/v4.7.6/ fixed all issues that I had with video on Ubuntu 16.04.
All other solutions described here didn't work for me.
  * Installation:

    * Download and install `linux-headers-4.7.6-xxx_all.deb` , `linux-headers-4.7.6-xxx-generic_xxx_i386/amd64.deb`
    and `linux-image-4.7.6-xxx-generic_xxx_i386/amd64.deb`
    from [kernel-ppa/mainline/v4.7.6](http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.7.6/)

### Kernel - 4.8 - Ubuntu 16.04.2
   * In Select a cell in LibreOffice does not show boarder and cursor disappears. Script fixes it
   On old PC with Intel Graphics Media Accelerator 4500 (integrated)


## Contribution

 * Testing results and fixes contribution are highly appreciated.
