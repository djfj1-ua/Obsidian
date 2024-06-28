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

#### Tres enfoques generales para configurar el acceso

Configure la configuración de seguridad apropiada para su caso práctico en el bucket y los objetos.

+ **Configuración de seguridad predeterminada de Amazon S3:** De forma predeterminada, los buckets de Amazon S3 y los objetos almacenados en ellos son privados (están protegidos). Las únicas entidades con acceso a un bucket recién creado sin modificar son el administrador de la cuenta y el usuario raíz de la cuenta de AWS. El propietario del recurso puede otorgar permisos de acceso específicos a otros, pero a quienes no se les haya concedido esos permisos no tendrán acceso.
+ **Desactivado la configuración de seguridad S3:** La mayoría de los casos prácticos , no se requiere acceso público. Con más frecuencia, Amazon S3 se usa para almacenar datos utilizados por una aplicación que se ejecuta fuera de Amazon S3, o para respaldar información confidencial. Para estos casos prácticos comunes, nunca se debe otorgar acceso público a los buckets que contienen los datos.
+ **Configuración de Amazon S3 para proporcionar acceso controlado:** Al usuario A se le otorgó acceso a los objetos en el bucket, pero al Usuario B se le denegó el acceso. Las situaciones de acceso controlado son frecuentes. Las puede configurar el propietario del bucket mediante una o más de las herramientas o las opciones para controlar el acceso a los datos de Amazon S3 que se analizaron anteriormente en este módulo.

#### Cifrado de los objetos en Amazon S3

+ El cifrado codifica los datos con una clave secreta, que los hace ilegibles.
	+ Solo los usuarios que tienen la clave secreta pueden descodificar los datos
	+ Opcionalmente, utilice AWS Key Management Service (AWS KMS) para administrar sus claves de cifrado.
+ Cifrado del lado del servidor
	+ En el bucket, habilite esta función seleccionando la opción Cifrado predeterminado
	+ Amazon S3 cifra los objetos antes de guardar los objetos en el disco y descifra los objetos cuando usted los descarga
+ Cifrado del cliente
	+ Cifre los datos en el lado del cliente y cargue los datos cifrados en Amazon S3
	+ En este caso, usted administra el proceso de cifrado

#### Clases de almacenamiento de Amazon S3 y Amazon S3 Glacier

##### S3 Standard

Ofrece almacenamiento de objetos de de durabilidad, disponibilidad y rendimiento elevados para los datos de acceso frecuente. Debido a que ofrece baja latencia y alto rendimiento, S3 Standard es adecuado para una amplia variedad de casos prácticos, como las aplicaciones en la nube, los sitios web dinámicos, la distribución de contenido, las aplicaciones para dispositivos móviles y videojuegos, y el análisis de big data. Ofrece durabilidad entre un mínimo de tres zonas de disponibilidad.

##### S3 Standard - Acceso poco frecuente (S3 Standard - IA)

Ofrece todos los beneficios de Amazon S3 Standard, pero se ejecuta con un modelo de costos diferentes para almacenar datos de acceso poco frecuente, como imágenes digitales más antiguas o archivos de registro más antiguos. Se aplica una tarifa de almacenamiento mínima de 30 días a todos los datos que se coloquen en él, y también tiene un costo más alto al recuperar los datos desde el almacenamiento de S3 Standard-IA que desde S3 Standard.

##### S3 One Zone - Acceso poco frecuente

Almacena datos en una única zona de disponibilidad. Es ideal para los clientes que desean una opción de menor costo y que no necesitan la disponibilidad y la resiliencia de S3 Standard o S3 Standard - IA. Es una buena opción para almacenar copias de seguridad secundarias de datos en las instalaciones o datos que se puede volver a crear fácilmente. También puede utilizarlo como almacenamiento rentable para los datos que se replican desde otra región de AWS.

##### S3 Intelligent - Tiering

Se diseñó para optimizar los costos mediante la migración automática de los datos al nivel de acceso más rentable sin afectar el rendimiento ni generar una sobrecarga operativa. Por una pequeña tarifa de supervisión y automatización por objeto, Amazon S3 supervisa los patrones de acceso de los objetos en S3 Intelligent - Tiering. Traslada los objetos a los que no se ha accedido durante 30 días consecutivos al nivel de acceso de poco frecuente. Si se accede a un objeto en el nivel de acceso poco frecuente, este se traslada automáticamente al nivel de acceso frecuente. No
hay tarifas por recuperación si se usa S3 Intelligent - Tiering, ni tampoco se cobran tarifas adicionales por organización en niveles cuando los objetos se trasladan de un nivel a otro.

##### Amazon S3 Glacier

Es una clase de almacenamiento segura, duradera y de bajo costo para el archivado de datos. Puede almacenar la cantidad de datos que desee de manera confiable y a precios competitivos o más económicos que las soluciones en las instalaciones. Para mantener los costos bajos, pero adecuados para diferentes necesidades, dispone de tres opciones para recuperar los datos, con diversos plazos de acceso y costos:
+ Las recuperaciones aceleradas suelen estar disponibles en un plazo de 1 a 5 minutos.
+ Las recuperaciones estándar suelen completarse en un plazo de 3 a 5 horas.
+ Las recuperaciones masivas suelen completarse en un plazo de 5 a 12 horas.

**Amazon S3 Glacier Deep Archive** es la clase de almacenamiento de menor costo para Amazon S3. Admite la retención a largo plazo y la preservación digital de datos a los que se podría acceder una o dos veces al año. Los datos se almacenan en un mínimo de tres zonas de disponibilidad geográficamente dispersas, con una protección de 11 nueves de durabilidad y se pueden recuperar en un plazo de 12 horas.

##### Políticas de ciclo de vida de Amazon S3

**Configure una política de ciclo de vida de Amazon S3 para eliminar o mover objetos en función de su antiguedad.***

Puede configurar el ciclo de vida de sus objetos para administrar cómo se almacenan durante su ciclo de vida. La **configuración del ciclo de vida** es un conjunto de reglas que definen acciones que Amazon S3 aplica en un grupo de objetos.

Después de establecer una política de ciclo de vida de S3, los datos se transferirán automáticamente a una clase de almacenamiento distinta sin generar ningún cambio en la aplicación.

Mediante el uso de políticas de ciclo de vida, puede hacer que los datos realicen ciclos a intervalos regulares entre los distintos tipos de almacenamiento de Amazon S3.
Realizar estos ciclos reduce los costos generales porque paga menos por los datos que se vuelven menos importantes con el tiempo. Además de poder establecer reglas del ciclo de vida por objeto , también puede establecer reglas del ciclo de vida por bucket.

##### Costos de Amazon S3

Solo paga por lo que utiliza. Esto incluye lo siguiente:
+ GB de objetos almacenados(al mes). Diferentes precios por región y por clase de almacenamiento.
+ Transferencias salientes a otras regiones o a Internet.
+ PUT, COPY, POST, LIST, GET, SELECT, transición de ciclo de vida, solicitudes de recuperación de datos.

Sin cargos por:
+ Transferencias de datos entrantes de Internet a Amazon S3.
+ Transferencias entre buckets de S3 o de Amazon S3 a cualquier servicio en la misma región de AWS.
+ Transferencia de datos salientes a Amazon CloudFront.
+ Solicitudes DELETE y CANCEL.