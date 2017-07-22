<html><body><p>Cuando uno quiere hacer una actualización o instalar un paquete en debian o alguna distribución y se encuentra un mensaje similar al siguiente.</p>



<pre>perl: warning: Setting locale failed. <br>perl: warning: Please check that your locale settings:<br> LANGUAGE = "en_US:en",<br> LC_ALL = (unset),<br> LC_TIME = "es_CR.UTF-8",<br> LC_MONETARY = "es_CR.UTF-8",<br> LC_ADDRESS = "es_CR.UTF-8",<br> LC_TELEPHONE = "es_CR.UTF-8",<br> LC_NAME = "es_CR.UTF-8",<br> LC_MEASUREMENT = "es_CR.UTF-8",<br> LC_IDENTIFICATION = "es_CR.UTF-8",<br> LC_NUMERIC = "es_CR.UTF-8",<br> LC_PAPER = "es_CR.UTF-8",<br> LANG = "en_US.UTF-8"<br> are supported and installed on your system.<br>perl: warning: Falling back to the standard locale ("C").<br>locale: Cannot set LC_ALL to default locale: No such file or directory</pre>



Se da porque algún locale no esta definido



se puede arreglar definiendo el locale faltante, como en el siguiente ejemplo



<pre>export LANGUAGE=en_US.UTF-8

export LANG=en_US.UTF-8

export LC_ALL=en_US.UTF-8

locale-gen en_US.UTF-8

dpkg-reconfigure locales</pre>



 



 </body></html>