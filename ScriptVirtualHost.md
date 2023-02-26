# ScriptVirtualHost

### En este script pido un usuario existente para crear su virtualhost

#### A destacar que tanto este script como todos los demás están hechos por funciones

Primero pido un usuario por teclado (existente)

```bash
echo "Introduce el usuario para crear su virtual host"
read usuario
```

Compruebo que el usuario existe

```bash
comprobar=`grep $usuario /etc/passwd`
```

Realizo un condicional If, donde si el usuario existe creo su virtual host, sino imprimo un mensaje de error

```bash
if [ $comprobar];
then
  echo "Creando document root"
   sudo mkdir /etc/apache2/sites-available/$usuario.conf
   echo "Creando fichero de configuración"
   echo "<VirtualHost *:80>
          Server Admin admin@$usuario.com
          ServerName $usuario.com
          ServerAlias www.$usuario.com
          DocumentRoot /var/www/html/$usuario
          ErrorLog /var/log/apache2/error.log
          CustomLog /var/log/apache2/acces.log combined
          </VirtualHost>" >> /etc/apache2/sites-available/$usuario.conf
    
    echo "Creando un index.html"
    echo "<p>Dominio: $usuario </p> >> /var/www/html/$usuario/index.html
    echo "<p>INDEX prueba</p> >> /var/www/html/$usuario/index.html
    
    # Después, habilito los servicios de apacho, deshabilito el fichero de configuración por defecto y reinicio los servicios
    
    sudo a2ensite $usuario.conf
    sudo a2dissite 000-default.conf
    sudo service apache2 reload
    sudo service apache2 restart
else
    echo "ERROR. El usuario no existe
fi
```
Así quedaría el script implementado en la función:

![image](https://user-images.githubusercontent.com/91189372/221432521-a462d212-2e21-410f-b48e-6bd0d6175555.png)
![image](https://user-images.githubusercontent.com/91189372/221432555-b1d4a763-9866-460d-9ae4-675cf079d951.png)

