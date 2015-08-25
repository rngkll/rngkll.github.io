.. title: Using US netflix with roku and openwrt
.. slug: using-us-netflix-with-roku-and-openwrt
.. date: 2014-03-31 17:20:13
.. tags: draft,netflix,openwrt,roku
.. description: 
.. wp-status: draft

<html><body><p>The Roku has no possibility to change the DNS to a specific one, so to use US Netflix with the roku the DNS has to be set in  the router.</p><p>I don't like all my DNS traffic going to a DNS that I don't trust so with options of dnsmasq that comes with openwrt I set DNS Forwardings.</p><p>Be carefull to change x.x.x.x for the ip address of the DNS service you want to use.</p><p>example http://www.unblock-us.com ip 208.122.23.23</p><p>in the file /etc/config/dhcp add the following lines below config dnsmasq.</p><pre>    list server '/netflix.com/x.x.x.x'

    list server '/nflximg.net/x.x.x.x'

    list server '/nflximg.com/x.x.x.x'

    list server '/roku.com/x.x.x.x'

    list server '/mgo-images.com/x.x.x.x'

    list server '/netflix.net/x.x.x.x'



</pre><p>it is necessary to add all that list servers.</p><p>This method could work for any other hardware but I have only tested it in the roku.</p></body></html>
