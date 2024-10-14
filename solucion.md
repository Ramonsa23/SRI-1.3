# Instalación de zonas secundarias.

### 1.Tomaremos a máquina darthsidious, e configuraremola para ser servidor secundario, tanto da zona primaria de resolución directa como de resolución inversa. Captura os ficheiros de configuración en ambalas dúas máquinas. Fai unha captura onde se vexa o reinicio da máquina darthsidious, no que se vexa no log dos dous equipos e que se fixo a transferencia de zona.
named.conf.local del dns primario:

![imagen](imaxes/img2.png)

named.conf.local del dns secundario:

![imagen](imaxes/img3.png)

Reinicio dns secundario darthsidious:

![imagen](imaxes/img1.png)

cd /var/cache/bind para ver los ficheros que cogió el dns secundario del primario. Lo guarda en formato binario por eso se ve extraño.



### 2.Engade un rexistro tipo A (Chewbacca 192.168.0.28) na zona de resolución directa e tamén na de resolución inversa.  Fai unha captura no momento do reinicio do equipo darthvader, no que se vexa o log dos dous equipos e que se amose que se fixo a transferencia de zona. Adxunta tamén unha captura do ficheiro de zona no servidor secundario.

Cuando hacemos un cambio en dns primario (en el secundario no tocamos), tenemos que aumentar el serial, y es cuando notifica, comprueba ese serial y si es mayor comienza la transferencia de la zona actualizada.

Es importante modificar tanto zona inversa como directa, en caso de que haya cambios.

![imagen](imaxes/img4.png)

### 3.Comproba que o servidor secundario pode resolver ese nome.

### 4.Fai os cambios necesarios para que as trasferencias se fagan de forma segura empregando chaves.  Repite as capturas e vídeos do punto 2, engadindo o rexistro r2d2 (192.168.0.29)

### 6. Pega nesta tarefa o enlace ao teu repo de github

https://github.com/Ramonsa23/SRI-1.1

- git status
- git add .
- git commit -m "Commit 2"
- git push origin main



OJO: Todos los dns secundarios que piden nuevazona, reciben, sin filtrar quien es ni nada. Si no tienen registro NS, no reciben notificaciones,
a no ser que añadamos en el primario also-notify {192.168.20.x}

Por defecto, deja a todos, pero si añadimos en el primario allow-transfer{192.168.20.x} podemos añadir una lista de dnssecundarios que queramos añadir.

