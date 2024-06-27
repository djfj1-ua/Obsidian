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
+ Los objetos también incluyen un ID de versión. En un *bucket*, una clave y un ID de versión identifican un objeto de forma única.
+ El *valor* del objeto es el contenido real que almacena. Puede ser una secuencia de *bytes*. Los valores del objeto son inmutables, es decir que después de que carga un objeto, no puede modificar el valor. Si desea modificar el objeto, debe hacer un cambio fuera de Amazon S3 y volver a cargar el objeto.
+ Los objetos también incluyen metadatos, que es un conjunto de pares de nombre-valor que puede usar para almacenar información sobre el objeto. Puede asignar metadatos, los que se denominan *metadatos definidos por el usuario*, a sus objetos en Amazon S3. Amazon S3 también asigna metadatos del sistema a estos objetos, que utiliza para administrar objetos.
+ Amazon S3 también usa sobrecursos para almacenar información adicional específica del objeto.
##### Beneficios de Amazon S3
+ Durabilidad
	+ Garantiza que no se pierdan los datos
	+ El almacenamiento de S3 Standard ofrece 11 nueves de durabilidad
+ Disponibilidad
	+ Puede acceder a sus datos cuando lo necesita
	+ La clase de almacenamiento de S3 Standard está diseñada para cuatro nueves de disponibilidad
+ Escalabilidad
	+ Ofrece capacidad prácticamente ilimitada
	+ Cualquier objeto único de 5 TB o menos
+ Seguridad
	+ Ofrece control de acceso detallado
+ Rendimiento
	+ Muchos patrones de diseño lo admiten

Amazon S3 está diseñado para sostener errores de dispositivos simultáneos detectando con rapidez y reparando cualquier redundancia perdida. Amazon S3 también verifica con regularidad la integridad de sus datos mediante sumas de verificación.

#### Protección de buckets y objetos de Amazon S3

Los buckets y objetos que se crean recientemente son privados y están protegidos de forma predeterminada.

Cuándo los casos prácticos deben compartir datos de Amazon S3:
+ Administre y controle el acceso a los datos
+ Siga el principio de mínimo privilegio

Herramientas y opciones para controlar el acceso a los datos de Amazon S3:
+ **Función de bloqueo de acceso público**: Está habilitada en buckets nuevos de forma predeterminada y es fácil de administrar.
+ **Políticas de IAM**: Una buena opción cuando el usuario puede autenticarse mediante IAM,.
+ **Políticas de bucket**: Puede definir el acceso a un objeto o bucket específico.
+ **Listas de control de acceso**(ACL): Un mecanismo de control de acceso heredado.
+ **Puntos de acceso S3**: Puede configurar el acceso con nombres y permisos específicos para cada aplicación.
+ **URL prefirmadas**: Puede conceder acceso limitado a objetos con URL temporales.
+ Comprobación de permisos de bucket de **AWS Trusted Advisor**: una función gratuita.

