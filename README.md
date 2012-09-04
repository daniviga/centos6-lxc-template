centos6-lxc-template
====================

Tools for converting an OpenVZ template into a working CentOS 6 lxc container

How to
-------------

* Download centos-6-x86_64.tar.gz from [http://wiki.openvz.org/Download/template/precreated](http://wiki.openvz.org/Download/template/precreated)
* Exctract it with tar xzps
* Chroot into the container and change the root password  
`chroot /path/to/the/container`  
`passwd root`
* Apply *etc\_lxc\_comp.patch* patch to the rootfs (or edit by hand using files in /etc dir of this repo as templates)
* Create /dev/tty0 and /dev/tty1  
`mknod -m 666 /path/to/the/container/dev/tty0 c 4 0; mknod -m 666 /path/to/the/container/dev/tty1 c 4 1`
* Use provided config and fstab as model. Chnage MAC address and other parameters as you wish.
* Now the container is ready for lxc. Start with lxc-start -n name -d and access it with lxc-console -n name.

Roadmap
-------------
* An automatic script to be used as lxc "template" (i.e. lxc-create -t template) is coming soon
* Testing on other platforms (more host distros and/or i686 arch)

Know issues
-------------
* Work is in progress
* This how-to is intended to be used with lxc userland tools (http://lxc.sourceforge.net/) and is not tested/ready (yet) to be used with libvirt-lxc
* **Running lxc out of SELinux or AppArmor context is not yet 100% safe! Be careful!**
* Tested with CentOS 6.3 64bit on Fedora 17 64bit host with lxc rpms from official Fedora repo (version 0.7.5)