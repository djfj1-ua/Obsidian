### Amazon S3

Un servicio de almacenamiento de objetos:
+ Almacena cantidades masivas (ilimitadas) de datos no estructurados.
+ Los archivos de datos se almacenan como objetos en un *bucket* que usted define.
+ 5 TB es el tamaño máximo de archivo de un solo objeto.
+ Todos los objetos tienen una URL única accesible globalmente por REST (espacio de nombres universales).
+ Todos los objetos tienen una *clave*, *ID de versión*, *valor*, *metadatos* y *subrecursos*.

*Amazon S3* es un servicio de almacenamiento de objetos. Le permite almacenar cantidades casi ilimitadas de datos. Los archivos de datos se almacenan como objetos. Coloca los objetos en un *bucket*, que usted define. Cada bucket debe tener un nombre que sea globalmente único entre las regiones. Esto significa que el nombre del *bucket* tiene que ser único entre todas las cuentas de clientes de AWS.

Cada objeto tiene *cinco características* consistentes:
+ Tiene una clave que es el nombre que le asigna a un objeto. La clave del objeto se usa para recuperar el objeto. En la Consola de administración de AWS, puede crear un directorio dentro de un *bucket* y cargar un objeto en ese directorio. Sin embargo, la realidad, Amazon S3 no conoce los directorios, por lo que el valor de clave incluye la ruta completa a la raíz del *bucket*.