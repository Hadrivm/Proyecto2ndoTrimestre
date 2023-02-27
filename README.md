# Proyecto2ndoTrimestre

### Para la realización de esta práctica he necesitado instalar los siguientes servicios:

* Apache 
* Bind
* PHP
* MYSql
* Python

### Se automatizará mediante el uso de scripts: 
* [La creación de usuarios y del directorio correspondiente para el alojamiento web](/ScriptUsuario.md)
* [Host virtual en apache](/ScriptVirtualHost.md)
* [Creación de usuario del sistema para acceso a ftp, ssh, smtp,…](/ScriptFtpSsh.md)
* [Se creará un subdominio en el servidor DNS con las resolución directa e inversa](/ScriptSubdominio.md)
* [Se creará una base de datos además de un usuario con todos los permisos sobre dicha base de datos (ALL PRIVILEGES)](/ScriptBaseDatos.md)
* [Se habilitará la ejecución de aplicaciones Python con el servidor web](/ScriptPython.md)


Una vez finalizado la creación de todos los scripts, creo un menú con bucle CASE donde en función de la opción que elija el usuario podrá realizar una tarea u otra

```bash
echo "-----MENU-----"
echo "-Introduce una opción-"
echo "1. Crear usuarios"
echo "2. Crear virtualhost"
echo "3. Crear subdominio"
echo "4. Crear base de datos"
echo "5. Crear usuarios, ftp, ssh ..."
echo "6. Habilitar aplicaciones python"
echo "7.Salir"
read option

case $option in
  1) user_crear
  ;;
  
  2) host_virtual
  ;;
  
  3) subdominio
  ;;
  
  4) base_datos
  ;;
  
  5) ftp_ssh
  ;;
  
  6) pythonn
  ;;
  
  7) echo "¡Hasta la próxima!"
  ;;
  
  *) echo "ERROR. Opción inválida"
  ;;
esac
```

Así quedaría el menú:

![image](https://user-images.githubusercontent.com/91189372/221453535-f6167255-53e4-491f-94e7-f16e89309196.png)
![image](https://user-images.githubusercontent.com/91189372/221453570-76293339-ada3-4a6a-9006-2c64bb553300.png)




