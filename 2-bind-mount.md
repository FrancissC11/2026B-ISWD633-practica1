# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
docker run -d --name srv_nginx -p 8080:80 -v C:\Users\FRANCISS\Desktop\nginx\html:/usr/share/nginx/html nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?
Se obtuvo un error 403 Forbidden. Esto pasa debido a que la carpeta html del computador está vacía. Nginx intenta buscar un archivo para mostrar, pero al no encontrar nada y tener deshabilitado el listado de directorios por seguridad, se obtiene un error de accesso denegado.

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo index original que viene por defecto con la imagen queda oculto. Al hacer el bind mount, Docker monta el directorio del host sobre el directorio del contenedor, tapando todo lo que existía previamente en esa ruta de destino. El archivo por defecto no se borra, pero es inaccesible mientras el volumen esté montado.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Al recargar la páginas en tu navegador, el sitio web mostrará el template que se descargó. No es necesario reiniciar el contenedor, porque el bind mount refleja cualquier cambio que haga en el sistema de archivos del host en tiempo real dentro del contenedor. 

### Eliminar el contenedor
docker rm -f srv_nginx

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Una vez se ejecutó de nuevo el comando de creación del contenedor apuntando a la misma ruta del host, el servidor se levantó mostando directamente el template web. Esto demuestra el concepto de la persistencia de datos. 


