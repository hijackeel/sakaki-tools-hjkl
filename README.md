# sakaki-tools-hjkl Gentoo Overlay

Overlay containing [buildkernel-hjkl](https://github.com/hijackeel/buildkernel-hjkl) ebuild, required for the tutorial ["**Sakaki's EFI Install Guide**"](https://wiki.gentoo.org/wiki/Sakaki's_EFI_Install_Guide) on the Gentoo wiki.

## List of ebuilds

* **sys-kernel/buildkernel** [source](https://github.com/hijackeel/buildkernel-hjkl)
  * Provides a script (**buildkernel**(8)) to build a (stub EFI) kernel (with integral initramfs) suitable for booting from a USB key on UEFI BIOS PCs. Automatically sets the necessary kernel configuration parameters, including the command line, and signs the resulting kernel if possible (for secure boot). Has a interactive and non-interactive (batch) mode. Manpages for the script and its configuration file (_/etc/buildkernel.conf_) are included.

## Installation

As of version >= 2.2.16 of Portage, **sakaki-tools-hjkl** is best installed (on Gentoo) via the [new plug-in sync system](https://wiki.gentoo.org/wiki/Project:Portage/Sync).
Full instructions are provided on the [Gentoo wiki](https://wiki.gentoo.org/wiki/Sakaki's_EFI_Install_Guide/Building_the_Gentoo_Base_System_Minus_Kernel#Preparing_to_Run_Parallel_emerges).

The following are short form instructions. If you haven't already installed **git**(1), do so first:

    # emerge --ask --verbose dev-vcs/git 

Next, create a custom `/etc/portage/repos.conf` entry for the **sakaki-tools-hjkl** overlay, so Portage knows what to do. Make sure that `/etc/portage/repos.conf` exists, and is a directory. Then, fire up your favourite editor:

    # vim /etc/portage/repos.conf/sakaki-tools-hjkl.conf

and put the following text in the file:
```
[sakaki-tools-hjkl]
 
# buildkernel-hjkl ebuild for Gentoo on EFI
# Maintainer: hijackeel (hijackeel@posteo.net)
 
location = /usr/local/portage/sakaki-tools-hjkl
sync-type = git
sync-uri = https://github.com/hijackeel/sakaki-tools-hjkl.git
priority = 50
auto-sync = yes
```

Then run:

    # emaint sync --repo sakaki-tools-hjkl

If you are running on the stable branch by default, allow **~amd64** keyword files from this repository. Make sure that `/etc/portage/package.accept_keywords` exists, and is a directory. Then issue:

    # echo "*/*::sakaki-tools-hjkl ~amd64" >> /etc/portage/package.accept_keywords/sakaki-tools-hjkl-repo
    
Now you can install packages from the overlay. For example:

    # emerge --ask --verbose sys-kernel/buildkernel

## Maintainers

* [hijackeel](mailto:hijackeel@posteo.net)
