Web Server Development Environment
==================================

Virtual Machine (on VirtualBox)
-------------------------------

### EC2 Specs

* 612mb memory
* 8gb hdd (fixed)

### Network

* Select bridged adapter
* Promiscuous Mode: allow all (requires strong user passwords)


Install Ubuntu 10.04 Server Edition
-----------------------------------

Download an Ubuntu install disk image (.iso file) and simply mount it to the
CDROM drive on the virtual machine.  Make sure the boot device priority order
is set correctly and then start the machine.

### Ubuntu Install Notes

* Partitioning: Guided - use entire disk (no need for Logical Volume Management)
* Use "ubuntu" as the username.
* Create a strong password since the machine is going to make itself available on the Internet.
* Only select the SSH Server software package during installation and leave the rest.


System Setup
------------

Let the VM reboot, shut it down with `sudo shutdown -P now`, and then reset the
boot device priority.  After that, fire up the VM again and connect with an SSH
session from a local terminal.

Use wget to grab the toehold script and bootstrap the system.

    wget https://github.com/FireworksProject/web_server/raw/master/dev_toehold
    HOST_IP=192.168.1.102 HOST_USER=kixx source dev_toehold

That will copy over your SSH keys from the host machine, install git, clone
this repository from GitHub, and install the required Ubuntu packages with
apt-get.
