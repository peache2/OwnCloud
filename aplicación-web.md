# Instalación y configuración de aplicaciones web

Para instalar una aplicación web debemos de bajar el codigo fuente y llevarlo al directorio raiz del servidor de aplicacions, en nuestro caso, `apache2`. Cuando instalemos `apache2` se creara una carpeta a `/var/www/html` donde, per defecto, el servidor web utiliza como directorio raiz.

Entonces, si llevamos nuestra aplicación al directorio `/var/www/html` tendremos acceso a la aplicación mediante la dirección wen `http://localhost`.

## Instalación de apache2, mysql y algunas librerias al contenedor

1. Actualización de la màquina.
```console
sudo apt update
```
```console
sudo apt upgrade
```

2. Instalación del servidor web `apache2`.
```console
sudo apt install -y apache2
```

3. Instalación del servidor de base de datos `mysql-server`.
```console
sudo apt install -y mysql-server
```

4. Instalación de algunas librerias de `php`, el lenguaje principal que utilizan las aplicaciones.
```console
sudo apt install -y php libapache2-mod-php
```
```console
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

5. Reiniciamos el servidor apache2
```console
sudo systemctl restart apache2
```

## Configuración de MySQL
### Accedemos a la consola de MySQL
Desde la terminal donde seguimos en `root` debemos de ejecutar la siguiente comanda:
```console
sudo mysql
```

### Creación de la base de datos:
Una vez dentro de la consola de MySQL ejecutamos las comandas para crear la base de datos. En este caso estamos creando una base de datos con el nombre `bbdd`.

```console
CREATE DATABASE bbdd;
```

### Creación de un usuario
Tenemos en cuenta que se tendra que identificar la IP desde la que se accedera a la base de datos, en este caso, `localhost`.

```console
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

### Damos privilegios al usuari:
```console
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```

### Salimos de la base de datos
```console
exit
```

### Probamos la conexión a la base de datos
Desde la terminal con un usuario que no tiene privilegios hemos de ser capaces de conectar introduciendo la contraseá.

```console
mysql -u usuario -p
```

## Descargamos los ficheros de la aplicación web
Vamos al directorio `/var/www/html` y descomprimimos los ficheros de la aplicació web, heu de substituir `app-web.zip` per el nom del vostre fitxer que heu descarregat amb l'aplicació web i el nom de la carpeta `app-web` per la carpeta que us ha creat, si la vostra instal·lació de linux està en un idioma diferent al català, no tindreu la carpeta `Baixades`, modifiqueu la comanda per adaptarla a les vostrs necessitats.

```console
sudo cp ~/Baixades/app-web.zip /var/www/html
```
Aneu al directori `/var/www/html`
```console
cd /var/www/html
```
Descomprimiu el fitxer que heu baixat
```console
sudo unzip app-web.zip
```
Copieu els fitxers a la carpeta `/var/www/html`, modifiqueu `app-web` pel nom del directori on s'ha descomprimit el vostre arxiu.
```console
sudo cp -R app-web/. /var/www/html
```
Eliminem la carpeta creada quan hem fet l'`unzip`
```console
sudo rm -rf app-web/
```

## Eliminem el fitxer `index.html` de l'`apache2`
```console
sudo rm -rf /var/www/html/index.html
```

## Aplicació de permisos a les nostres aplicacions web
Un cop descomprimits els fitxers de l'aplicació web al directori `/var/www/html`, apliquem els següents permisos al directori `/var/www/html`

```console
cd /var/www/html
```
```console
sudo chmod -R 775 .
```
```console
sudo chown -R usuario:www-data .
```
## Accedim al navegador per veure que tot funciona
Poseu la direcció http://localhost al navegador web i configureu la cloud.

Si tot ha anat bé i heu seguit el manual us apareixerà l'instal·lador de l'aplicació web que heu baixat i us demanarà crear un usuario admin i la informació de la base de dades.

La informació que heu de posar (si no heu modificat la informació del manual) és la següent:

* **usuari:** usuario
* **contrasenya:** password
* **base de dades:** bbdd
* **domini:** localhost
