# ScriptFTPSSH

### Con este script automatizo la creación de usuarios con acceso a ftp, ssh, etc..

#### A destacar que tanto este script como todos los demás están hechos por funciones

El primer paso, es pedir por pantalla el nombre de usuario a crear

```bash
echo "Introduce el nombre de un usuario existente"
read usu
```
Defino las variables UID(ID de usuario) y GID(ID de grupo) con un número elevado, para que no se repitan a la hora de crear los usarios

```bash
let UID=2000
let GID=2000
```

Compruebo que el usuario existe

```bash
comprobar=`grep $usu /etc/passwd`
```

Con una sentencia IF, si el usuario existe le doy acceso a los servicios, sino muestro un mensaje de error

```bash
if [ $comprobar ];
then
   sudo mkdir /srv/ftp_$usu
   sudo chmod 777 /srv/ftp_$usu
   
   sudo ftpasswd --passwd --name=$usu --uid=$(($UID+1)) --gid=$(($GID+1)) --home /srv/ftp_$usu --shell /bin/false
else
  echo "ERROR. El usuario no existe"
fi
```

Así quedaría el script implementado en la función:

![image](https://user-images.githubusercontent.com/91189372/221452605-634d6168-42ce-4728-97e4-bcbc13401098.png)

