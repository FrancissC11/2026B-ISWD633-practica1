### MI APRENDIZAJE

Antes de la práctica, el tema de guardar datos en contenedores era pura teoría. Ahora entiendo realmente cómo y cuándo usar los tres tipos de almacenamiento: 
* Los **bind mounts** (vincular carpetas de mi computadora al contenedor).
* Los **volúmenes nombrados** (los que Docker administra por su cuenta).
* Los **volúmenes anónimos**. 

Esto es útil porque ya sé cómo proteger información importante, como bases de datos o archivos de páginas web, asegurando que no se pierdan aunque el contenedor se apague o se borre.

En el proceso me topé con algunos problemas reales. Por ejemplo, olvidé la contraseña de WordPress y comprobé que solo reiniciar el contenedor no servía de nada porque el volumen estaba haciendo su trabajo de persistir los datos. 

Para solucionar esto y evitar chocar con puertos ocupados de ejercicios anteriores, utilicé algunos comandos extra:
* `docker rm -f <nombre_contenedor>`: Para forzar el borrado de contenedores activos.
* `docker volume rm <nombre_volumen>`: Para limpiar los volúmenes y empezar de cero. 
