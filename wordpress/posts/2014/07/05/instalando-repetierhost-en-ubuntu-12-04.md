<html><body><p>Para utilizar la printrbot simple estoy utilizando RepetierHost, estos son algunos de los pasos que seguí para poder imprimir.



Descargar RepetierHost de <a title="repetier.com/download" href="http://www.repetier.com/download/" target="_blank">http://www.repetier.com/download/</a>



Descomprimir y mover la carpeta RepetierHost al lugar donde se desea.



Ej: repetierHostLinux_0_95.tgz



</p><pre>tar -xzf repetierHostLinux_0_95.tgz

mv RepetierHost $HOME</pre>



o donde se desea dejar



<pre><code>cd RepetierHost</code></pre>



ejecutar configureFirst.sh, lo cual les va a instalar las dependencias del sistema.



<pre><code>./configureFirst.sh</code></pre>



si da errores al descargar ExtUtils-ParseXS-3.18_04.tar.gz o parecido



<pre>

Working on SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz

Fetching http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz ... FAIL

! Download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz failed. Retrying ...

! Download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz failed. Retrying ...

! Download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz failed. Retrying ...

! Failed to download http://www.cpan.org/authors/id/S/SM/SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz

! Failed to fetch distribution ExtUtils-ParseXS-3.18_04

--&gt; Working on ./xs

</pre>



es necesario actualizar la linea 127 en Slic3r/Build.PL

y cambiar



system $cpanm, 'SMUELLER/ExtUtils-ParseXS-3.18_04.tar.gz';



por

system $cpanm, 'SMUELLER/ExtUtils-ParseXS-3.24.tar.gz';



Luego ejecutar de nuevo configureFirst.sh como anteriormente.



van a ver unos errores en las pruebas pero el sistema va a funcionar bien.



Al abrir RepetierHost es necesario como primer paso configurar la impresora, para esto van a "Printer Settings" y utilizan la siguiente configuración



En la pestaña de connection



<pre>

port: /dev/ttyACM0



Baud Rate: 230400



Trasfer Protocol: Autodetect



Reset on Connect: Disabled



Reset on Emergency: Send emergency command and reconnect



Receice Cache Size: 63

</pre>



En la pestaña Printer



<pre>

Defautl Heated Bed Temperature: 0

</pre>



En la pestaña Printer Shape



<pre>

X MAx 100



Y Max 100



Print Area Width: 100



Print Area Depth: 100



Print Area Height: 100

</pre>



Cuando tenga mas recomendaciones las agrego, si alguien tiene alguna recomendación se lo agradecería para agregarla.</body></html>