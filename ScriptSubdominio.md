# ScriptSubdominio

### En este script automatizo la screación de subdominios

#### A destacar que tanto este script como todos los demás están hechos por funciones

Primero pido un nombre de subdominio por teclado

```bash
echo "Introduce el nombre del subdominio"
read sudbom
```

Establezco la IP del dominio, en mi caso, la IP de mi servidor Ubuntu

```bash
IP=10.4.2.58
```

Creo el fichero de zona para el subdominio

```bash
sudo mkdir /etc/bind/zones/db.$subdom
```

Añado la información necesaria al fichero de zona directa

```bash
echo
"\$TTL 604800
@ IN  SOA ns1.$subdom.  admin.$subdom. (
                5           ; Serial
                604800      ; Refresh
                86400       ; Retry
                2419200     ; Expire
                604800      ; Negative Cache TTL
;
@ IN  NS  ns1.$subdom.
@ IN  A   $IP" >> /etc/bind/zones/db.$subdom
```

Creo el fichero de zona inverso

```bash
sudo mkdir /etc/bind/zones/db.10.4.2
```

Añado la información necesaria dentro del fichero de zona inverso con echo y redirecciono

```bash
echo
"\$TTL 604800
@ IN  SOA ns1.$subdom.  admin.$subdom. (
                5           ; Serial
                604800      ; Refresh
                86400       ; Retry
                2419200     ; Expire
                604800      ; Negative Cache TTL
;
@ IN  NS  ns1.$subdom." >> /etc/bind/zones/db.10.4.2
```

Añado la información tanto de la zona inversa com de la zona directa al fichero named-conf.local

```bash
echo 
" zone \"$sudbom\" {
  type master;
  file \"/etc/bind/zones/db.$subdom\";
};

zone \"2.4.10.in-addr.arpa\" {
  type master;
  file \"/etc/bind/zones/db.10.4.2\";
}; " >> /etc/bind/named-conf.local
```

Finalmente reinicio el servicio bind para aplicar los cambios

```bash
sudo service bind9 restart
```

Así quedaría el script implementado en la función:

![image](https://user-images.githubusercontent.com/91189372/221450130-0be01624-dadb-42c1-a42f-9e41a9361fcf.png)
![image](https://user-images.githubusercontent.com/91189372/221450211-c3df8296-ab0d-417b-85b4-c42f6c5a2525.png)
