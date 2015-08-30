.. title: Using US Netflix with roku and openwrt
.. slug: using-us-Netflix-with-roku-and-openwrt
.. date: 2014-03-31 17:20:13
.. tags: draft, Netflix, openwrt, roku
.. description: How to use Netflix from other countries using openwrt and roku. 

The Roku has no possibility to change the DNS to a specific one, so to use US Netflix with the roku the DNS has to be set in the router.

I don't like all my DNS traffic going to a DNS that I don't trust so with options of dnsmasq that comes with openwrt I set DNS Forwardings.

Be carefull to change x.x.x.x for the ip address of the DNS service you want to use.

example http://www.unblock-us.com ip 208.122.23.23 in the file /etc/config/dhcp add the following lines below config dnsmasq.

list server '/netflix.com/x.x.x.x'
list server '/nflximg.net/x.x.x.x'
list server '/nflximg.com/x.x.x.x'
list server '/roku.com/x.x.x.x'
list server '/mgo-images.com/x.x.x.x'
list server '/netflix.net/x.x.x.x'


It is necessary to add all that list servers. This method could work for any other hardware but I have only tested it in the roku.
