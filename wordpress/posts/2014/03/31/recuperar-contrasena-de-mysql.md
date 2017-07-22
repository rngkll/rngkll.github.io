<html><body><p>Para "recuperar"  la contraseña de mysql lo primero es detener el servicio.</p><pre>sudo service mysql stop

</pre><p>Luego iniciar mysql con --skip-grant-tables, para evitar que pida contraseña.</p><pre class="terminal">sudo mysqld --skip-grant-tables &amp;

</pre><p>Se inicia sesión como usuario root de mysql</p><p class="terminal">mysql -u root mysql</p><p class="terminal">Con el siguiente comando sustituyendo CONTRASEÑANUEVA por la nueva contraseña.<br><br></p><pre class="terminal">UPDATE user SET Password=PASSWORD('CONTRASEÑANUEVA') WHERE User='root'; FLUSH PRIVILEGES; exit;

</pre><p>Reiniciar el servicio de mysql y listo.</p></body></html>