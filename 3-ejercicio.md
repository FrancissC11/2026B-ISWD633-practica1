## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
docker network create net-wp

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
Inicialmente, la carpeta se encontró completamente vacía, puesto que el servicio de base de datos aún no había sido inicializado ni había generado su estructura de almacenamiento.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
docker run -d --name mysql_db --network net-wp -v C:\Users\FRANCISS\Desktop\ejercicio3\db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wp_pass mysql:8

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Se observó que el directorio se pobló automáticamente con los archivos de configuración, registros y las estructuras de datos generadas por el motor de MySQL tras su primer arranque.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
docker run -d --name wordpress_web --network net-wp -p 9500:80 -v C:\Users\FRANCISS\Desktop\ejercicio3\www:/var/www/html -e WORDPRESS_DB_HOST=mysql_db -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wp_pass -e WORDPRESS_DB_NAME=wordpress wordpress

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Al eliminar y desplegar nuevamente los contenedores, se comprobó que tanto la personalización de la apariencia como las entradas agregadas en WordPress permanecieron intactas y operativas. El sistema recuperó su estado exacto sin requerir una nueva instalación, comprobando así que la información de la base de datos y los ficheros web persistieron de manera exitosa a través de los volúmenes montados en el directorio del host local.