# ScriptBaseDatos

### En este script automatizo la creación de usuarios con todos los priveligios (ALL PRIVILEGES) con MariaDB

#### A destacar que tanto este script como todos los demás están hechos por funciones

El primer paso es pedir por pantalla que se introduzca un usuario ya existente

```bash
echo "Introduce el nombre de un usuario que ya exista en el sistema"
read usuarioo
```

A continuación, compruebo si este usuario realmente existe

```bash
comprobar=`grep $usuarioo /etc/passwd`
```

Creo un condicional IF, donde si el usuario existe creo la base de datos, sino, muestro un mensaje de error por pantalla

```bash
if [ $comprobar ];
then
    mysql -u root -p -e "CREATE DATABASE $usuarioo;"
    mysql -u root -p -e "GRANT ALL PRIVILEGES ON $usuario.* TO '$usuario'@localhost IDENTIFIED BY 'usuario';"
    mysql -u root -p -e "FLUSH PRIVILEGES;"
else
    echo "ERROR. El usuario no existe"
fi
```

Así quedaría el script implementado en la función:

![image](https://user-images.githubusercontent.com/91189372/221450719-14af533d-cfa1-4b3a-aded-8c96e8d5b4c9.png)
