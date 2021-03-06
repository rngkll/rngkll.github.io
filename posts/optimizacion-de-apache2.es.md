<!-- 
.. title: Optimización de apache2
.. slug: optimizacion-de-apache2
.. date: 2013-10-18 11:16:14 UTC-06:00
.. tags: apache, optimizacion, web, keepalive 
.. category: linux
.. link: 
.. description: 
.. type: text
-->


Primero hay que revisar cuales módulos están cargados, esto se puede hacer con
```
apachectl -M
```

Lo ideal es tener solo los módulos necesarios para que el sitio funcione, la cantidad de módulos influye en e tamaño de cada proceso de apache que se encuentra corriendo.

```
HostnameLookups off
```

Cuando un cliente el accede el servidor web, se crea una bitácora en access.log, si esta directiva esta en On se busca el nombre en el servidor de nombres, aun con un cache de dns esto es muy lento.

Cuando se establece una conexión esta se deja escuchando por un tiempo por si se le hace una nueva petición, en el caso de tener muchos visitantes y dejar la conexiones abiertas por mucho tiempo, se crea un problema, por eso se puede bajar el tiempo para poder servir nuevas peticiones. (Esta altamente ligado al MaxClients).

```
KeepAlive On
KeepAliveTimeout 2
```
Para el momento de calcular MaxClients.

Una buena referencia es MaxClients = (total de memoria)/(promedio de memoria utilizada por cada proceso de apache)

Una buena manera de ver el tamaño de un proceso de apache es con el comando `ps -ylC apache2 --sort:rss`

Con esto se puede ver el tamaño del proceso mas grande de ultimo.

Una suma de la columna del rss nos da un valor del total de memoria que esta usando el proceso, esto puede aumentar porque no todos los procesos tiene el mismo tamaño.

```
ps -ylC apache2 --sort:rss | awk '{SUM += $8 } END {print SUM}'
```

Hay que tomar en cuenta también el resto de procesos del servidor.

Utilizando top y acomodando por rss podemos ver los procesos que están utilizando mas memoria, entre estos deberíamos encontrar los procesos de apache y el o los de la base de datos si es que se tiene una.
