# Proyecto Final - Filtros para imagenes PGM con Apptainer y Docker (para usuarios en otro sistema operativo que no sea Linux o que 
tengan permisos de administrador)

Este repositorio contiene una imagen de contenedor (`.sif`) creada con Apptainer para ejecutar filtros sobre imágenes `.pgm`.

##  Archivos incluidos para ejcutar en Apptainer

 pgm_filters.def
 pgm_filters.sif(aa, ab) _(dividido en partes por límites de GitHub)
Dado que nuestro archivo .sif esta divido, aquí están las recomendaciones para reconstruirlo( no se preocupen, están relativamente fáciles de seguir)

# Instrucciones para recomponer a .sif 

Es fundamental que tengas apptainer instalado, y es el paso 0, hay muchos tutoriales que te pueden ayudar a instalarlo en caso de que no 
lo tengas y no sepas como se hace

Como el archivo `.sif` supera los 100MB, se ha dividido en partes utilizando Split, asi que vamos a reconstruirlo:

# INSTRUCCIONES para correr con Apptainer:

Debes descargar el zip y descomprimirlo en una carpeta que sera la de tu proyecto (solo descomprime el zip descargado, nada mas)

Desde la raíz del proyecto, entra a la carpeta en la que están ubicados pgm_filters_xz_part(aa, ab)

Luego abre un bash, una vez en el bash debes introducir el siguiente comando: (hasta copiado y pegado si quieres)

cat pgm_filters_xz_part_* > pgm_filters.sif.xz 

Tras hacer esto, debes realizar el comando:

xz -d pgm_filters.sif.xz

Luego debes introducir el comando:

apptainer run pgm_filters.sif

Todo esto estando en el bash.

Y ya estaría completo y listo para correr tu programa.

##  Archivos incluidos para ejecutar con Docker
 Dockerfile
 pgm_filters.cpp

# INSTRUCCIONES para correr con Docker:

- Instala Docker Desktop para tu sistema operativo y en Ajustes -> Resources -> File sharing, agrega la ruta de tu carpeta de proyecto 

- Debes descargar el zip y descomprimirlo en la carpeta de tu proyecto, idealmente si estas en tu computador
evita usar una carpeta que tenga backup con OneDrive porque aveces puede generar problemas (solo descomprime el zip descargado, nada mas)

Aqui puedes ignorar los archivos de la parte de Apptainer ( pgm_filters.def y pgm_filters.sif(aa, ab))

- Entra en la carpeta de tu proyecto 

- Luego abre un bash ubicado en tu carpeta y debes ejecutar los siguientes comandos (puedes copiar y pegar pero ten en cuenta que debes completar las
partes como se te indica):

- docker build -t <<nombre que quieras para la imagen de docker>> .   

(Aqui puedes usar como ejemplo el nombre: "pgm_filters", y las << >> no deben ir solo especifican donde y que debes escribir, 
ademas no olvides el "." que es necesario)

- docker run --rm -v "<<Tu ruta interna de la carpeta de tu proyecto>>:/output" <<nombre que pusiste a la imagen de docker>> /output/<<imagen.pgm>> <<filtro>> 

(La ruta interna la obtienes desde tu explorador de archivos y como ejemplo te dejo la que un miembro del grupo ha usado: 
"C:\Users\jujo1\Music\ProgCPP_Proyecto_Final"; continuando con el nombre de la imagen, sera el mismo que usaste en el comando build: "pgm_filters";
luego en imagen.pgm debes escribir el nombre de la imagen que vas a testear sin ningun extra como el .\ que autocompleta el sistema al usar la tecla tab
, como ejemplo de las imagenes que se incluyen en el zip: "baboon.ascii.pgm"; por ultimo, en filtro solo especifica el filtro que deseas usar, las 
opciones son: invert, blur, gaussian3, gaussian5, sharpen, unsharp, edge) -> el ejemplo completo se veria tal que:
<<docker run --rm -v "C:\Users\jujo1\Music\ProgCPP_Proyecto_Final:/output" pgm_filters /output/baboon.ascii.pgm edge>>

- Luego de esto ya deberias ver el mensaje que confirma la creacion de la imagen con el filtro y ademas verla en tu carpeta del proyecto

- Si quieres verla descarga GIMP que es el mejor software para ver este formato de imagen

## Imagenes .pgm incluidas para correr el programa tanto en Apptainer como en Docker
(ascii se refiere al formato P2 y las simplemente .pgm formato P5)
 apollonian_gasket.ascii.pgm
 baboon.ascii.pgm
 balloons.ascii.pgm
 f14.ascii.pgm

 bird.pgm
 coins.pgm
 field.pgm
   