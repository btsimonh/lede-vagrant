# lede-vagrant
Vagrant files for lede/openwrt dev on ubuntu 16.04 x64

based on base box ubuntu/trusty64
created from the vagrant files from VVV.

provision.sh loads all required lede dependencies, enables samba, and should take you to the point where you can
make menuconfig


This is tested only in my vagrant environment on Windows 10, using virtualbox.
(i ma not have set the base image correctly for other virtualisation suppliers).
Note: on windows, in the past, i have had conflicts between VMware and virtualbox;  
this machine I choose virtualbox because vmware is no longer 'free'.
This SHOULD work with VMWare, but is untested.


Instructions to get building LEDE (openWRT):

Install virtualbox (mine is Version 5.1.6 r110634 (Qt5.5.1))
https://www.virtualbox.org/wiki/Downloads
Install vagrant (mine is 'Installed Version: 1.8.5')
https://www.vagrantup.com/downloads.html
Clone this repo into a folder.
cd to the folder, and run 
vagrant up

what this should do (in theory):
download the base box ubuntu/trusty64
add this VM to virtualbox
run up the VM
Execute provision/provision.sh
	which does:
	everything required to build lede;
	installs all prerequisites
	installes samba, and creates an open share to /home/vagrant/
	retrieves the (trunk?) source from github to /home/vagrant/lede
	
when it's done, you can SSH to localhost:2222 and login with vagrant/vagrant.
Then 
cd lede
make menuconfig
configure the target....
then 
make

(in my test, my target was BTHH5A, and it build with no build errors).



Additional notes:

I use SourceTree from Atlassian; it's a fine GIT GUI for windows.
I added Samba so that i could use my windows GUI git client with the Leda tree.
However, the LEde/OpenWRT tree contains filenames which contain colons 
(something to do with usb....)...  this does not stop you using a windows based git GUI, 
you just have to ignore the files removed/replaced with random filenames.

It would be nice if we could get the Lede source to NOT have filenames which can't be 
represented in windows....  I'll work on that :).

Default configuration:

if you have an existing .config file, you can place this in <root folder>/source/.config
and the provision.sh will copy it to your source folder after getting the Lede sources.


Other Caveats:

Linux & OSX hosts:

Vagrant is available for Linux & OSX,  but there are settings in the vagrant file which 
are specific to these OS which i may not have set - so it would be great if someone more
familiar with Vagrant was to check over the file and correct it...

x64 VM base image & virtualisation:

on 'older' machines (e.g. low end core 2), the processors may not have the CPU virtualisation 
technologies required to run a 64 bit VM.  It should work fine with a 32 bit variety - just change
ubuntu/trusty64 to ubuntu/trusty32 in the vagrant file.  (this is untested).

Other Documentation:

The vagrant file i based this on was a variation of:

https://github.com/Varying-Vagrant-Vagrants/VVV

The VVV readme is worth a read for more mature descriptions of the software and processes involved here.


License: very relaxed....

Original license for VVV:

Copyright / License

VVV is copyright (c) 2014-2016, the contributors of the VVV project under the MIT License.

