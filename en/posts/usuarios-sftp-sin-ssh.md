<!-- 
.. title: Usuarios sftp sin ssh
.. slug: usuarios-sftp-sin-ssh
.. date: 2013-03-15 15:34:28 UTC-06:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

Para evitar que los usuario puedan acceder por medio de ssh pero si tengan acceso sftp al servidor.

## Cambiar el shell del usuario al sftp-server

### Centos 5.7
```
usermod -s  /usr/libexec/openssh/sftp-server username
```
### Debian 6.0
```
usermod -s /usr/lib/sftp-server username
```

## Agregar al archivo /etc/shells

### Centos 5.7
```
/usr/libexec/openssh/sftp-server
```

### Debian 6.0
```
/usr/lib/sftp-server
```
