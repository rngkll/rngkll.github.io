<html><body><h2></h2>

Cuando el BBB se conecta por medio de usb, genera una interfaz de red con el ip 192.168.7.1 en la computadora, el BBB va a quedar con el ip 192.168.7.2, para hacer mas facil la configuración cada vez que lo conecto, hice el siguiente script.

<pre>#!/bin/sh



#habilitar forwarding en computadora local

sudo sh -c "echo 1 &gt; /proc/sys/net/ipv4/ip_forward"



#Nateo

sudo /sbin/iptables -t nat -A POSTROUTING -j MASQUERADE



#Agregar el gateway al BBB

ssh root@192.168.7.2 "/sbin/route add default gw 192.168.7.1"



#Agregar DNS

ssh root@192.168.7.2 "echo 'nameserver 8.8.8.8' &gt; /etc/resolv.conf"



#Actualizar la fecha

ssh root@192.168.7.2 "ntpdate pool.ntp.org"





</pre></body></html>