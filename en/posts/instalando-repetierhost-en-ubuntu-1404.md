<!-- 
.. title: Instalando RepetierHost en Ubuntu 1404
.. slug: instalando-repetierhost-en-ubuntu-1404
.. date: 2014-05-07 10:23:32 UTC-06:00
.. tags: 3dprint printrbot 
.. category: 
.. link: 
.. description: 
.. type: text
-->

# Instalar
1. Para utilizar la printrbot simple estoy utilizando RepetierHost, estos son algunos de los pasos que seguí para poder imprimir.
2. Descargar RepetierHost de http://www.repetier.com/download/
3. Descomprimir y mover la carpeta RepetierHost al lugar donde se desea.

Ej: repetierHostLinux_0_95.tgz
```
tar -xzf repetierHostLinux_0_95.tgz
mv RepetierHost $HOME
```
 
o donde se desea dejar, `cd RepetierHost` y luego ejecutar configureFirst.sh, lo cual les va a instalar las dependencias del sistema.

`./configureFirst.sh`

Si da errores al descargar ExtUtils-ParseXS-3.18_04.tar.gz o parecido

```
Working on SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz
Fetching http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz ... FAIL
! Download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz failed. Retrying ...
! Download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz failed. Retrying ...
! Download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz failed. Retrying ...
! Failed to download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz
! Failed to fetch distribution ExtUtils-ParseXS-3.18_04
--> Working on ./xs
```

es necesario actualizar la linea 127 en Slic3r/Build.PL
y cambiar
```
system $cpanm, 'SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz';
```
por
```
system $cpanm, 'SMUELLER/ExtUtils-ParseXS-3.24.tar.gz';
```
Luego ejecutar de nuevo configureFirst.sh como anteriormente.

van a ver unos errores en las pruebas pero el sistema va a funcionar bien.

Al abrir RepetierHost es necesario como primer paso configurar la impresora, para esto van a "Printer Settings" y utilizan la siguiente configuración

En la pestaña de connection
```
port: /dev/ttyACM0
Baud Rate: 230400
Trasfer Protocol: Autodetect
Reset on Connect: Disabled
Reset on Emergency: Send emergency command and reconnect
En la pestaña Printer
```
Defautl Heated Bed Temperature: 0

En la pestaña Printer Shape
```
X MAx 100
Y Max 100
Print Area Width: 100
Print Area Depth: 100
Print Area Height: 100
```
Cuando tenga mas recomendaciones las agrego, si alguien tiene alguna recomendación se lo agradecería para agregarla.

