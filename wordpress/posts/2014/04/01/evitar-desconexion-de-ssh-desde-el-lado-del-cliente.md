<html><body><p>Es muy molesto cuando uno esta trabajando por ssh en algún equipo y por un rato no se utiliza la consola, cuando volvemos aparece el una notificación "Connection Timeout".</p><p> </p><p>Para evitar esto es nada mas de agregar unas líneas a la configuración del cliente ssh.</p><p>en el caso de debian o ubuntu.</p><pre>vim /etc/ssh/ssh_config

</pre><p>y se agregan las siguientes líneas<br><br></p><pre>ServerAliveInterval <span class="nu0">30</span>

ServerAliveCountMax <span class="nu0">3</span>

</pre></body></html>