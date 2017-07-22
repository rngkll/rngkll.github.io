<html><body><p>Para evitar que los usuario puedan acceder por medio de ssh pero si tengan acceso sftp al servidor.</p><h2>Cambiar el shell del usuario al sftp-server</h2><p>Centos 5.7</p><pre>usermod -s  /usr/libexec/openssh/sftp-server username

</pre><p>Debian 6.0</p><pre>usermod -s /usr/lib/sftp-server username

</pre><h2>Agregar al archivo /etc/shells</h2><p>Centos 5.7</p><pre>/usr/libexec/openssh/sftp-server

</pre><p>Debian 6.0</p><pre>/usr/lib/sftp-server

</pre></body></html>