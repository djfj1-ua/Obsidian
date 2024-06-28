
### Crear un bucket 

+ En la consola de administración de AWS, en el menú *Services*, elige S3.
+ Elige un nombre para el *bucket*. En la sección *Propiedades del objeto*, selecciona *ACL habilitadas*, luego verifica que *Propietario preferido del bucket* esté seleccionado.
+ Desactiva *Bloquear todo el acceso público*, luego selecciona la casilla que indica *Reconozco que la configuración actual puede dar lugar a que este bucket y los objetos dentro de él se conviertan en públicos*.
+ Crea el bucket.
### Para crear una etiqueta para añadir información adicional a un bucket

+ Selecciona el nombre de un bucket
+ Elige la pestaña *Propiedades*
+ Ve hasta el panel de *Tags*
+ Selecciona *Edit*, y luego elige *Add tag* e ingresa una clave y un valor
+ Guarda los cambios
### Configuración del bucket para el alojamiento de sitios web estáticos

+ En la consola *Propiedades*
+ En *Alojamiento de sitios web estáticos*
+ Elige *Editar*
	+ **Alojamiento web estático:** habilitado,
	+ **Tipo de alojamiento:** elige *Alojar un sitio web estático*
	+ **Documento de índice:** *documento index.html*
	+ **Documento de error:** *documento error.html*
+ Guarda los cambios
+ En el panel *Alojamiento de sitios web estáticos*, selecciona el enlace debajo de *Punto de enlace del sitio web del bucket*.

### Cargar contenido al bucket

+ Elige archivos que quieras subir al bucket.
+ Selecciona el bucket donde quieras subir los archivos y dirígete a la pestaña *Objetos*.
+ Selecciona *Cargar*.
+ Elige *Add files*.
+ Selecciona los archivos que quieras subir.
+ Pincha en *Cargar*.
+ Cierra la ventana.

### Habilitar el acceso a los objetos 

De forma predeterminada, los objetos almacenados en Amazon S3 son privados. Esto garantiza que los datos de tu organización permanecen seguros.

En esta tarea, lograrás que los objetos cargados tengan acceso público.

En primer lugar, confirma que actualmente los objetos sean privados.

Puedes hacer públicos los objetos de Amazon S3 de dos maneras diferentes:
+ Para hacer público un bucket completo o un directorio específico dentro del bucket, utiliza una *política de bucket*.
+ Puedes utilizar una *lista de control de acceso(ACL)* para hacer públicos objetos individuales en un bucket.

En general, es más seguro hacer públicos *objetos individuales* porque esto evita que otro objetos se hagan públicos por accidente. Sin embargo, si sabes que la totalidad del bucket no contiene información confidencial, puedes utilizar una *política de bucket*.

Para configurar los objetos individuales para que que sean accesibles públicamente:
+ Selecciona los objetos que quieras publicar.
+ En el menú *Actions*, elige *Hacer público a través de ACL*.
+ Selecciona *Hacer público*

