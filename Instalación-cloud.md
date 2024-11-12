# Instalación de OwnCloud

Para instalar la cloud necsitamos descargar el archivo que he dejado en el README

### Instalamos la versión 7.4 de PHP en el sistema operativo Ubuntu 24.04

Para instalar correctamente OwnCloud necesitamos la versión 7.4 de PHP, para  instalar en nuestro sistema debemos poner los siguientes comandos en la terminal:

Actualizamos las listaqs de paquetes y actualizamos todos los paquetes del sistema-. 

Instalamos los requisitos previos de PPA:
```bash
sudo apt install software-properties-common -y
```

Instalamos todas las herramientas que necesitamos para trabajar correctaemtne con los archivos personales (PPA).
```bash
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
```

Actualizamos los repositorios:
```bash
sudo apt update
```

Instalamos la libreria de PHP de la versión 7.4
```bash
sudo apt install php7.4 -y
```
```bash
sudo apt install -y php libapache2-mod-php7.4
```

```bash
sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl
```

Seleccionamos la versión de PHP que nosotros queremos:
```bash
sudo update-alternatives --config php
```

Activamos los modulos de apache2 necessarios:
```bash
sudo a2enmod proxy_fcgi setenvif
```

```bash
sudo a2enconf php7.4-fpm
```

Reinicieu l'apache2:
```bash
sudo service apache2 restart
```
