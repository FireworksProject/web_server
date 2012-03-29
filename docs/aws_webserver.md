Amazon Web Service EC2 Node Deployment
======================================

EC2 Instance From Scratch
-------------------------
How to create a new EC2 image with new OS and software. This is only done when
we need to make software updates, or make architectural changes to the web
server setup.

### Select a fresh Image
Go to [Alestic.com](http://Alestic.com) and select the Ubuntu 10.04 LTS EBS boot image. (currently ami-349b495d)


### Instance settings
* Any availability zone is ok
* Name it "webserver-VERSION" where VERSION is like 2b or something.
* Use the webserver-b1 security group
* Make sure to choose a key which you actually have.


### SSH Login
You'll have to wait for the instane to start, but when it does, you can start
an SSH session. To login to the machine you'll need your access key which
you can use like this:

    ssh -i ~/.ssh/mykey.pem ubuntu@instance.public.domain.com

Where `~/.ssh/mykey.pem` is the location of the access key you are using and
`instance.public.domain.com` is the public domain name of the instance which
you can find on the AWS control panel where you launched the instance.


### Install Git
Git has a lot of uses and is not that big of a dependency, so we install it.

    sudo apt-get install git-core


### Dotfiles
This step is optional, but having our standard set of configuration files on
the machine makes it easier to work with.

    cd ~
    git clone git://github.com/FireworksProject/dotfiles.git

Checkout the README to find out how to initialize the dotfiles repository and
install the configuration files. Once you're done you should re-run the bash
config file with

    source ~/.bashrc

which will cause the new config settings to take effect.


### Install the SysAdmin Scripts
Clone a read-only version of the `web_server` repo:

    cd ~
    git clone git://github.com/FireworksProject/web_server.git


### Update the Ubuntu System
Get the latest packages from Ubuntu and install dependencies with

    ~/web_server/bin/bootstrap_ubuntu

Then restart the machine to get the new kernels and dependencies in place.


### Setup Node.js
See the `nodejs.md` docs.


### Setup CouchDB
See the `couchdb.md` docs.


### Snapshot
