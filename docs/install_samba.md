Install Samba Server
--------------------

Download Samba, the public key, and the signature

    wget http://www.samba.org/samba/ftp/samba-latest.tar.gz
    wget http://ftp.samba.org/pub/samba/samba-pubkey.asc
    wget http://ftp.samba.org/pub/samba/samba-latest.tar.asc

Verify the download

    gpg --import samba-pubkey.asc
    gunzip samba-version.tar.gz
    gpg --verify samba-release.tar.asc

Unpack the tarball

    tar xvf samba-version.tar

Installation instructions can be found in the extracted archive at docs
/htmldocs/Samba3-HOWTO/compiling.html The autoconf package also needs to be
installed on Ubuntu (if it has not been already).

To install v3, change dir into `source3/`.

Create the configure script

    sudo ./autogen.sh

Then run it

    sudo ./configure

Compile it

    sudo make

And install it

    sudo make install
