<!-- 
.. title: Freeswitch in Raspberry Pi
.. slug: freeswitch-in-raspberry-pi
.. date: 2013-07-09 10:23:32 UTC-06:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

# Experiments using raspberry pi

I bought the raspberry pi to use it as a print and scanner server in my house, now I have some more ideas, one is using freeswitch to test voip performance in the rpi.

installing Freeswitch in the rpi.

Pi uses the default Debian image so we need to install Debian dependencies.
```
apt-get install autoconf automake gawk g++ git-core libjpeg62-dev libncurses5-dev libtool make python-dev gawk pkg-config libtiff4-dev libperl-dev libgdbm-dev libdb-dev
```
Change to /usr/local/src and download Freeswitch using git

```
git clone -b v1.2.stable git://git.freeswitch.org/freeswitch.git
git clone git://git.freeswitch.org/freeswitch-contrib.git
git clone git://git.freeswitch.org/freeswitch-sample-configs.git
```
Raspberry Pi has limited resources so I will compile Freeswitch to get a better performance.

##Compiling steps
```
./bootstrap.sh ./configure -C
```
I had some problems when mod_flite enabled, I have a 256mb rpi.

make && make install Now Freeswitch is installed. freeswitch initscript for debian can be found here

# Resources

http://wiki.freeswitch.org/wiki/Installation_Guide
