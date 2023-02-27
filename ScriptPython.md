# ScriptPython


### Con este scrit autmatizo la habilitación de aplicaciones python bajo apache

#### A destacar que tanto este script como todos los demás están hechos por funciones

Creo el directorio de python, de nombre pythonapp

```bash
sudo mkdir /var/www/pythonapp
```

Creo el fichero de configuración de mi aplicación python

```bash
sudo touch /etc/apache2/sites-available/pythonapp.conf
```


Añado la información correspondiente al fichero pythonapp.conf

```bash
echo
"<VirtualHost *:80>	
        DocumentRoot /var/www/pythonapp
        WSGIDaemonProcess pythonapp user=www-data group=www-data processes=1 threads=5 python-path= /var/www/pythonapp
        WSGIScriptAlias / /var/www/pythonapp/pythonapp.wsgi
        <Directory /var/www/pythonapp >
                WSGIProcessGroup pythonapp 
                WSGIApplicationGroup %{GLOBAL}
                Require all granted
        </Directory>
        ErrorLog /var/log/apache2/pythonapp-error.log
        CustomLog /var/log/apache2/pythonapp-access.log combined
</VirtualHost>" >> /etc/apache2/sites-available/pythonapp.conf
```

Habilito el nuevo fichero de configuración y deshabilito el 000-default.conf

```bash
sudo a2ensite pythonapp.conf
sudo a2dissite 000-default.conf
```

Para aplicar los cambios reinicio el servicio apache 

```bash
sudo service apache2 reload
sudo service apache2 restart
```

Así quedaría el script implementado en la función:

![image](https://user-images.githubusercontent.com/91189372/221451534-364f4497-ff30-45b0-89db-63921eca057f.png)
