<html><body><h1>Experiments using raspberry pi</h1>



I bought the raspberry pi to use it as a print and scanner server in my house, now I have some more ideas, one is using freeswitch to test voip performance in the rpi.



installing Freeswitch in the rpi.



Pi uses the default Debian image so we need to install Debian dependencies.



<code>apt-get install autoconf automake gawk g++ git-core libjpeg62-dev libncurses5-dev libtool make python-dev gawk pkg-config libtiff4-dev libperl-dev libgdbm-dev libdb-dev</code>



Change to /usr/local/src and download Freeswitch using git



<code>git clone -b v1.2.stable git://git.freeswitch.org/freeswitch.git

git clone git://git.freeswitch.org/freeswitch-contrib.git

git clone git://git.freeswitch.org/freeswitch-sample-configs.git </code>



Raspberry Pi has limited resources so I will compile Freeswitch to get a better performance.



<h2>Compiling steps</h2>



<code>./bootstrap.sh</code> <code>./configure -C</code>



I had some problems when mod_flite enabled, I have a 256mb rpi.



<code>make &amp;&amp; make install</code> Now Freeswitch is installed. freeswitch initscript for debian can be found <a href="http://wiki.freeswitch.org/wiki/Freeswitch_init">here</a>



<h2>Resources</h2>



<em>http://wiki.freeswitch.org/wiki/Installation_Guide</em></body></html>