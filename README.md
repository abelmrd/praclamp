# Practica lamp en dos capas
En esta practica separaremos servidor de apache y mysql para dar mayor seguridad y control sobre nuestro entorno de trabajo.

## Primer paso: Vagrant
Generamos un archivo vagrant con vagrant init
Vamos a explicar las lineas que modificamos o añadimos según las necesidades del proyecto


    config.vm.define "serverapache" do |serverapache|

    serverapache.vm.box = "debian/bullseye64"

    serverapache.vm.hostname = "AbelMonApache"

    serverapache.vm.network "public_network"

    serverapache.vm.network "private_network", ip: "192.168.21.21"

    serverapache.vm.synced_folder "./","/vagrant"

    serverapache.vm.provision "shell", path: "scripta.sh"


* Vamos a definir el servidor como "serverapache". 

* Utilizaremos una debian bullseye.
* Le asignamos el nombre al servidor que nos requiere la practica. 
* En este servidor añadimos interfaz pública y privada, ya que requiere salida a exterior y tambien conectarse al equipo MYSQL en red local. Este utimo servidor solo tendrá la red privada, por tanto un único adaptador de red, con una ip local 192.168.21.22 /24 .
* En ambos casos definimos como la carpeta compartida la ruta /vagrant
Para dar un entorno listo para comenzar a configurar aprovisionaremos con dos scripts que previamente hemos hecho para ambas maquinas, al estar en la ruta del vagrant con poner el nombre en el path es suficiente.


## Scripts de aprovisionamiento
```
echo " Actualizamos repositorios y paquetes"

    sudo apt update 
    sudo apt upgrade -y

echo "Instalacion de paquetes LAMP. Apache"
    sudo apt -y install apache2 
    sudo systemctl reload apache2
    sudo apt -y install default-mysql-server

echo " Instalacion de php"
    sudo apt -y install php libapache2-mod-php php-mysql

    #sudo apt -y install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
    #instalamos adminer y lo movemos al www
 sudo wget https://github.com/vrana/adminer/releases/download/v4.8.1/adminer-4.8.1-mysql.php
 sudo find / -type f -name *adminer* -exec mv {} /var/www/adminer.php \; 




echo "Instalamos git"

    sudo apt -y install git
```



[![](https://turismomadrid.es/images/Portada/2017/castillo-mr-nov-art-portada-2018.jpg)](https://www.as.com/)



![Imagen local](https://github.com/abelmrd/repositorio/blob/main/images/867994_1.jpg)
![](images/867994_1.jpg)

[Enlace al archivo nuevo md](https://github.com/abelmrd/repositorio/blob/d178214b8e421dd820c5c8a696b723528a54f429/documento.md)

[Enlace al archivo nuevo md](/documento.md)
