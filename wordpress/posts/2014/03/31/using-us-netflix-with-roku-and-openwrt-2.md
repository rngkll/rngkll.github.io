<html><body><h2>First method</h2>



The Roku has no possibility to change the DNS to a specific one, so to use US Netflix with the roku the DNS has to be set in  the router.



I don't like all my DNS traffic going to a DNS that I don't trust so with options of dnsmasq that comes with openwrt I set DNS Forwarding.



Be careful to change x.x.x.x for the ip address of the DNS service you want to use.



example http://www.unblock-us.com ip 208.122.23.23



in the file /etc/config/dhcp add the following lines below config dnsmasq.



<pre>    list server '/netflix.com/x.x.x.x'

    list server '/nflximg.net/x.x.x.x'

    list server '/nflximg.com/x.x.x.x'

    list server '/roku.com/x.x.x.x'

    list server '/mgo-images.com/x.x.x.x'

    list server '/netflix.net/x.x.x.x'

    list server '/netflix.net/x.x.x.x'

    list server '/roku.com/x.x.x.x'

    list server '/scorecardresearch.com/x.x.x.x'</pre>



it is necessary to add all that list servers.



This method could work for any other hardware but I have only tested it in the roku.



<h2>Second method</h2>



at first I was using the first method but I had to keep adding forwarder addresses to the dhcp file.



in "network-&gt;firewall-&gt;custom rules" add the following rules



iptables -t nat -A PREROUTING -i br-lan -s x.x.x.x -p udp --dport 53 -j DNAT --to-destination y.y.y.y:53

#iptables -t nat -A POSTROUTING -j MASQUERADE



where x.x.x.x is the roku or other device you want to use with a specific dns server and y.y.y.y is the address of the specific dns server.</body></html>