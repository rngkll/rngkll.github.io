<html><body><p>Revisar project mercury



 



Por necesidades de algunos de los sitios que manejamos en la empresa fue necesario experimentar con varnish ya que en algunos momentos se alcanzan picos en las visitas los cuales causan comportamientos anormales en los servidores, por esto se empieza la implementacion de varnish.



 



Utilizando memcached



Instalar memcached y php5-memcache libmemcached-tools



la configuracion esta en /etc/memcached.conf



reiniciar el servicio memcache ya apache



instalar el modulo de drupal memcache



Para drupal 6



</p><pre><span style="font-size:14px;">$conf['cache_inc'] ='sites/all/modules/memcache/memcache.inc';</span>

</pre>



PAra drupal 7



<pre><span style="font-size:14px;">$conf['cache_backends'][] = 'sites/all/modules/memcache/memcache.inc';

$conf['cache_default_class'] = 'MemCacheDrupal';

$conf['memcache_key_prefix'] = '<strong>something_unique</strong>';</span>



activar el modulo memcache admin para tener acceso a las estadisticas





varnish









</pre>



Se utiliza pressflow para las primeras pruebas ya que esta optimizado para rendimiento.



el comando ab para pruebas de rendimiento



ab -n 5000 -c 50 http://localhost/pressflow6/



para mejorar el rendimiento de php se instala APC



para instalar varnish es recomendado utilizar paquetes precompilados de la distribucion, muchas veces los repositorios tienen una version desactualizada, en el caso de ubuntu se puede agregar el repositio de varnish.



 



<ol>

    <li><code>curl http://repo.varnish-cache.org/debian/GPG-key.txt | apt-key add -</code></li>

    <li><code>echo "deb http://repo.varnish-cache.org/ubuntu/ lucid varnish-3.0" &gt;&gt; /etc/apt/sources.list </code></li>

    <li><code>apt-get update</code></li>

    <li><code>apt-get install varnish</code></li>

</ol>



Luego de instalar varnish es necesario cambiar el puerto en el que escucha apache, esto se hace en el archivo ports.conf y en la declaracion del virtualhost



vamos a pasar a apache a eschar en el puerto 8080 o cualquier otro que se desee, esto se puede verificar con el comando netstat -ln.



por defecto varnish va a escuchar en el puerto 6081, esto se debe de cambiar en el archivo <em>/etc/varnish/default.vcl, </em>se debe pasar al puerto 80.



La terminal de administración del varnish la cual escucha por defecto en el puerto 6082 necesita un secret para poderse conectar.



Se instala el modulo varnish para drupal, este se va a utilizar la terminal de administracion para comunicarse con el varnish.



Se instala el modulo expire de drupal para que este limpie las paginas apropiadas del cache del varnish cuando el contenido cambie.



 



 



 



Referencias



https://www.varnish-cache.org/installation/ubuntu



https://drupal.org/project/varnish



https://drupal.org/project/expire



https://drupal.org/project/esi



 



Herramientas para realizar pruebas



https://jmeter.apache.org/



 



 



Fuentes



http://www.thefanclub.co.za/how-to/how-install-memcached-on-ubuntu-for-drupal</body></html>