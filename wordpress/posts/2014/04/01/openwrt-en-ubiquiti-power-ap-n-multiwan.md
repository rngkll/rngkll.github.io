<html><body><h2>Instalación de openwrt</h2><h3>Descargar la imagen</h3><p>Como en openwrt.org no existe una imagen hecha específicamente para ese router es necesario utilizar la del Ubiquiti Nanostation M</p><p>http://backfire.openwrt.org/10.03.1/ar71xx/openwrt-ar71xx-ubnt-nano-m-jffs2-factory.bin</p><h3>Cargar por TFTP</h3><h4>Requerimientos</h4><div class="level4"><ul><li class="level1"><div class="li">Cable ethernet entre la computadora y el router</div></li><li class="level1"><div class="li">Configuración de la tarjeta de red: 192.168.1.254/255.255.255.0</div></li><li class="level1"><div class="li">Cliente tftp</div></li><li class="level1"><div class="li">El firmware que se va a cargar</div></li></ul></div><h4>Procedimiento</h4><div class="level4"><ol><li class="level1"><div class="li">Apagar el dispositivo</div></li><li class="level1"><div class="li">Apertar el botón de reset</div></li><li class="level1"><div class="li">Encender el dispositivo</div></li><li class="level1"><div class="li">Liberar el botón cerca de 10 segundos de encender el dispositivo. Los leds empiezan a cambiar.</div></li><li class="level1"><div class="li">hacer ping 192.168.1.20, si funciona estamos listos para cargar la imagen.</div></li><li class="level1"><div class="li">Cargar la imagen por tftp como flash_update (Me parece que en las versiones mas nuevas no es necesario)</div></li></ol><p> </p><pre class="code">tftp 192.168.1.20

tftp&gt; bin

tftp&gt; put imagen.bin flash_update

Sent 1965199 bytes in 28.8 seconds

tftp&gt; quit



</pre><p class="code">En el momento que el equipo reinicia solo va a contestar por el puerto de la WAN, ingresamos a http://192.168.1.1 y cambiamos la contraseña.</p><h3 class="code">Configuración</h3><p class="code">por ssh vamos a editar las interfaces de red en <em> /etc/config/network</em> y sustituimos por lo siguiente.</p><pre>config 'switch' 'eth1'

        option 'enable_vlan' '1'



config 'switch_vlan'

        option 'device' 'eth1'

        option 'vlan' '1'

        option 'ports' '0 1 2 3 4'



config 'interface' 'loopback'

        option 'ifname' 'lo'

        option 'proto' 'static'

        option 'ipaddr' '127.0.0.1'

        option 'netmask' '255.0.0.0'



config 'interface' 'lan'

        option 'ifname' 'eth1'

        option 'type' 'bridge'

        option 'proto' 'static'

        option 'ipaddr' '192.168.1.1'

        option 'netmask' '255.255.255.0'

        option '_orig_ifname' 'eth1'

        option '_orig_bridge' 'true'



config 'interface' 'wan'

        option 'ifname' 'eth0'

        option '_orig_ifname' 'eth0'

        option '_orig_bridge' 'false'

        option 'proto' 'dhcp'

</pre><p>Con esto ya tenemos un router inalámbrico en su configuración normal, de aquí en adelante es jugar con el OpenWRT para poder hacer lo que uno quiera.<br><br></p></div><h3>Multiwan</h3><p>Es necesario instalar los siguientes paquetes:</p><ul><li>luci-app-multiwan</li><li>multiwan</li></ul><p>Para utilizar se tiene que configurar el switch que concentra los 4 puertos para separar uno para utilizarlo como una segunda wan.</p><pre>config 'interface' 'loopback'

    option 'ifname' 'lo'

    option 'proto' 'static'

    option 'ipaddr' '127.0.0.1'

    option 'netmask' '255.0.0.0'



config 'switch' 'eth1'

    option 'enable_vlan' '1'



config 'switch_vlan'

    option 'device' 'eth1'

    option 'vlan' '1'

    option 'vid' '1'

    option 'ports' '0t 1 2 3'



config 'switch_vlan'

    option 'device' 'eth1'

    option 'vlan' '2'

    option 'vid' '2'

    option 'ports' '0t 4'



config 'interface' 'lan'

    option 'ifname' 'eth1.1'

    option 'type' 'bridge'

    option '_orig_ifname' 'eth1'

    option '_orig_bridge' 'true'

    option 'proto' 'static'

    option 'ipaddr' '172.16.1.1'

    option 'netmask' '255.255.255.0'



config 'interface' 'wan'

    option 'ifname' 'eth0'

    option '_orig_ifname' 'eth0'

    option '_orig_bridge' 'false'

    option 'proto' 'dhcp'

    option 'broadcast' '1'



config 'interface' 'wan2'

    option 'ifname' 'eth1.2'

    option '_orig_ifname' 'eth1.2'

    option '_orig_bridge' 'false'

    option 'proto' 'static'

    option 'ipaddr' '192.168.1.3'

    option 'netmask' '255.255.255.0'

    option 'gateway' '192.168.1.1'

    option 'broadcast' '192.168.1.255'

    option 'dns' '200.91.75.5 200.91.75.6'

</pre><p> </p><p>Luego de esto nada mas hay que agregar la nueva interfaz creada a la zona del <strong>wan</strong> del firewall, esto se puede hacer de manera gráfica.</p><p> </p><p>A causa de un pico de voltaje durante una tormenta eléctrica no se va experimentar mas con este router.</p></body></html>