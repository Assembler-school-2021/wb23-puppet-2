# wb23-puppet-2

> Pregunta 1 : Parametriza el módulo ntp para usar los servidores ntp de hetzner. Cuando funcione, cambia el scope a common.yaml dado que todos tienen que usar este módulo.

Editamos el fichero /etc/puppet/code/environments/production/hieradata/node/puppet-agent.local.yaml con lo siguiente:
```
---

classes:
   - ntp
   - timezone

timezone::timezone: 'Europe/Madrid'
ntp::servers:
  - "ntp1.hetzner.de"
  - "ntp2.hetzner.com"
  - "ntp3.hetzner.net"
```

Para hacerlo gobal a todos los nodos movemos lo que hay en este fichero al fichero /etc/puppet/code/environments/production/hieradata/common.yaml quedando de esta manera
```
---

classes:
   - common_hosts
   - common_packages
   - ntp
   - timezone

timezone::timezone: 'Europe/Madrid'
ntp::servers:
  - "ntp1.hetzner.de"
  - "ntp2.hetzner.com"
  - "ntp3.hetzner.net"
```

Finalmente ejecuta puppet agent -vt en ambos nodos. Que ha ocurrido?
```
Notice: Location is: developerville
Notice: /Stage[main]/Main/Notify[Location is: developerville]/message: defined 'message' as 'Location is: developerville'
```

> Pregunta 2 : Vamos a cambiar los NTP de devopsville. Crea un nuevo archivo en el lugar adecuado (location) con los valores de los DNS adecuados para devopsville. Finalmente comprueba que todo funciona.

> Pregunta 3 : Ahora que ya eres un experto de puppet, dirígete a puppet forge y busca los módulos necesarios para realizar las siguientes acciones en nuestro stack, Usaremos el agent de webserver. Recuerda subir todo a gitlab y comparte el repo con el usuario @BusyNinja.
> - ntp en todos los servidores con el mismo endpoint, configurado en hiera
> - llaves ssh : añadir las llaves desde hiera
> - php-fpm : configurar el servicio desde hiera
> - webserver : que puedas configurar un virtualhost desde el hiera
> - database : que puedas crear bbdd y users desde el módulo
