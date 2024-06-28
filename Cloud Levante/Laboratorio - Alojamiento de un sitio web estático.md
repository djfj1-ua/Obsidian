
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