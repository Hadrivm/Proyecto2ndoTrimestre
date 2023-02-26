# ScriptUsuarios

### Con este script automatizo la creación de usuarios con sus respectivos directorios por defecto

#### A destacar que tanto este script como todos los demás están hechos por funciones

Primer pido por pantalla el nombre del usuario a crear

```bash
echo "Inserta el nombre del usuario a crear"
read user
```

Compruebo que el usuario no exista

```bash
comprobar=`grep "$user" /etc/passwd`
```

Si no existe creo el usuario, su directorio por defecto y un index. Si existe, muestro un mensaje en pantalla de error

```bash
if [ $comprobar];
then
  echo "El usuario $user ya existe"
  clear
  user_crear
else
  useradd -m -d /home/$user $user -s /bin/bash
  passwd $user
  sudo mkdir /var/www/html/$user
  sudo cp /var/www/html/index.html /var/www/html/$user/index.html
fi
```

Así quedaría el script implementado en la función:

![image](https://user-images.githubusercontent.com/91189372/221432636-08fef4d3-7476-4d14-8fd4-a12fc6674a24.png)
