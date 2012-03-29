Web Server Development Environment
==================================


Virtual Machine (on VirtualBox)
-------------------------------
### Create Machine
* Use 64 bit Ubuntu if possible (if the host machine is 64 bit)
* Set it up with 600MB memory
* And create an 8GB HDD (flex)

These are the system settings, per tab, on VirtualBox, for this machine.

### System
* 600MB memory
* Shut off absolute pointing device

### Audio
* Disable audio

### Network
* Select bridged adapter
* Advanced::Promiscuous Mode: allow all (requires strong user passwords)

### USB
* Disable USB


Install Ubuntu 10.04.3 Server Edition
-------------------------------------
Download an Ubuntu install disk image (.iso file) for 10.04.3 server edition if
you don't already have it. There is no need to burn an actual CDROM, you can
simply mount the iso image to the CDROM drive on the virtual machine (in the
Storage tab on the machine settings).  Make sure the boot device priority order
is set start with CD/DVD-ROM (in the System tab on the machine settings) and
then start the machine.

### Ubuntu Install Notes
* Partitioning: Guided - use entire disk (no need for Logical Volume Management)
* Use "ubuntu" as the username.
* Create a strong password since the machine is going to make itself available on the Internet.
* Only select the SSH Server software package during installation and leave the rest unchecked.
* Do *not* allow automatic updates.

Let the VM reboot after Ubuntu installation and then log into it.


SSH Setup
---------
While logged into the VM, create the .ssh dir, and get the IP address of the VM
on the local network with

    mkdir ~/.ssh
    hostname -I

With the IP address in hand, you can copy over your private key and ssh config
file used to access GitHub, which will be needed to clone the `web_server`
repository onto the VM.  So, back on your local host machine, use scp to copy
your private key to the VM.

    scp ~/.ssh/$YOUR_KEY* ubuntu@$VM_IP:~/.ssh/
    scp ~/.ssh/config ubuntu@$VM_IP:~/.ssh/

where `$YOUR_KEY` is probably something like `id_rsa` and `$VM_IP` is the IP
address of the VM. Make sure both the private and public keys are copied.


System Setup
------------
After copying your SSH key and config file, log onto the VM in an SSH terminal
from your local host machine.  Then, use wget to grab the toehold script and
bootstrap the production system.

    cd ~
    wget https://github.com/FireworksProject/web_server/raw/master/toehold
    source toehold

That will install git, clone this repository from GitHub, and install the
required Ubuntu packages with apt-get.

When this is done running, restart the machine (to enable the new Linux kernel).

    sudo shutdown -r now


Dotfiles
--------
This step is optional, but really nice to have for development purposes. While logged into the VM do

    cd ~
    git clone git@github.com:FireworksProject/dotfiles.git

Follow the README instructions in the dotfiles repo then:

    source ~/.bashrc

Then, you'll probably want to transfer your .gitconfig file from your local
host machine to the development VM.

    scp username@$HOST_IP:~/.gitconfig ~/

where `$HOST_IP` is the IP address of your local host machine.


Setup the Node.js Stack
-----------------------
Check out the `nodejs.md` docs.


Setup CouchDB
-------------
Check out the `couchdb.md` docs.


Setup the LAMP Stack
--------------------
On the VM do

    bin/setup_LAMP_stack

This will install Apache, MySQL, PHP, and PHPMyAdmin. Along the way it will ask
for a new password for the root MySQL user. A strong password is probably not
needed here, but whatever you choose, make sure to record it and don't lose it.
Also, during PHPMyAdmin setup, choose the Apache server setup option, and then
deny the automatic database setup tool.

After this is all done, point a web browser to
`http://192.168.1.100/phpmyadmin` (where 192.168.1.100 should be replaced with
the IP address of your running VM) and create the MySQL application user in the
privileges tab.  Again, username and password probably does not need to be
strong, but make sure to record it somewhere. This user should have all "data"
and "structure" privileges.

