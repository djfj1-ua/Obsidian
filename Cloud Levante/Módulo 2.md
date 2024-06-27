## Marco de AWS Well-Architected:

Guía para evaluar las arquitecturas de la nube y orientación para ayudar a implementar diseños. Documenta una serie de preguntas básicas y prácticas recomendadas que le permiten comprender si una arquitectura determinada está bien alienada con las prácticas recomendadas de la nube.
* Excelencia operativa
* Seguridad
* Fiabilidad
* Eficacia del rendimiento
* Optimización de costos
* Sostenibilidad (2021)
### Pilar de seguridad:
* Base de identidad
* Trazabilidad
* Seguridad en todas las capas
* Evaluación de riesgos y estrategias de mitigación
### Pilar de excelencia operativa

Aborda la capacidad de _ejecutar sistemas_ y obtener información sobre sus operaciones para entregar valor empresarial, también la capacidad de mejorar continuamente los procesos y procedimientos de apoyo.

Cuando se diseñe una carga de trabajo para operaciones, se debe saber cómo se implementará, actualizará y operará. Habilite la observación con registros, instrumentación y métricas técnicas y de negocio para que pueda obtener información sobre qué ocurre dentro de su arquitectura.

### Pilar de fiabilidad

Capacidad de un sistema para recuperarse de errores en la infraestructura o interrupciones de servicio y adquirir de manera dinámica recursos de cómputo para satisfacer la demanda, también para mitigar las interrupciones como errores de configuración o problemas transitorios de la red.

### Pilar de eficiencia del rendimiento

**Compatibilidad mecánica**: Ocurre cuando utiliza una herramienta o un sistema con conocimientos sobre cómo funciona mejor. Utilice el enfoque tecnológico que se adapte mejor a lo que intenta lograr. Por ejemplo, tenga en cuenta los patrones de acceso a los datos cuando seleccione los enfoques de la base de datos o de almacenamiento.

### Pilar de optimización de costos

La optimización de costos es un requisito permanente de cualquier buen diseño de arquitectura. Comprender el grado de eficiencia de su arquitectura actual en relación con sus objetivos puede eliminar gastos innecesarios. Considere usar servicios administrados, porque operan a escala de la nube y pueden ofrecer un menor costo por transacción o servicio.

### Pilar de sostenibilidad

* Comprender el impacto
* Establecer objetivos de sostenibilidad
* Maximizar la utilización
* Anticipar y adoptar nuevas ofertas de hardware y software más eficientes
* Reducir el impacto descendente de sus cargas de trabajo en la nube

### La Herramienta de AWS Well-Architected

Es una herramienta de autoservicio que le proporciona acceso bajo demanda a las prácticas recomendadas actuales de AWS.

Permite revisar el estado de las cargas de trabajo y compararlas con las prácticas recomendadas más recientes de AWS en el ámbito de la arquitectura. Le da acceso a los conocimientos y a las prácticas recomendadas que utilizan los arquitectos de AWS, cuando lo necesite.

## Prácticas recomendadas para crear soluciones en AWS

### Compensaciones de diseño
* Evalúe las compensaciones para que pueda seleccionar un enfoque óptimo.
* Algunos ejemplos de compensaciones:
	* Cambiar la consistencia, la durabilidad y el espacio por el tiempo y la latencia para ofrecer un rendimiento más alto.
	* Priorizar la velocidad de comercialización de las funciones nuevas por sobre le costo.
* Basar las decisiones de diseño en datos empíricos.

### 1. Habilite la escalabilidad

Importante habilitar la escalabilidad en todas las capas, si no, podría requerir que el escalado se realice de manera reactiva y manual.

Al **habilitar la escalabilidad**, puede mejorar su diseño para anticipar la necesidad de más capacidad y entregarla antes de que sea demasiado tarde.

Puede utilizar una solución de supervisión como Amazon *CloudWatch* para **detectar si la carga total de toda su flota de servidores alcanzó un umbral especificado**. También se puede diseñar métricas personalizadas basadas en aplicaciones específicas que pueden activar el escalado de recursos que se requiere. 
Cuando se activa una alarma, *Amazon EC2 Auto Scaling* lanza de inmediato una nueva instancia. De este modo, esa instancia está lista antes de que se alcance el máximo de la capacidad, lo que ofrece una experiencia sin interrupciones para los usuarios.
Idealmente, también debe diseñar su sistema para que haga una *reducción horizontal* cuando la **demanda disminuya y usted no ejecute instancias que ya no necesita**.

### 2. Automatice su entorno

**Cuando sea posible, automatice el aprovisionamiento, la terminación y la configuración de recursos

Puede usar herramientas como CloudWatch y Amazon EC2 Auto Scaling para detectar los recursos en mal estado y automatizar el lanzamiento de recursos de reemplazo. También puede recibir notificaciones cuando cambien las asignaciones de recursos.

### 3. Trate los recursos como desechables

**Aproveche la naturaleza de aprovisionamiento dinámico del cómputo en la nube

| Práctica no recomendada                                                                     | Práctica recomendada                                                                                         |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Con el tiempo, servidores distintos terminan teniendo configuraciones diferentes            | Automatice la implementación de recursos nuevos con configuraciones idénticas                                |
| Los recursos se ejecutan cuando no se necesitan                                             | Termine los recursos que no se utilizan                                                                      |
| Las direcciones IP codificadas de manera rígida impiden la flexibilidad                     | Cambien a nuevas direcciones IP de manera automática                                                         |
| Puede ser difícil o inconveniente probar actualizaciones nuevas en hardware que está en uso | Pruebe las actualizaciones en los recursos nuevos, luego, reemplace los recursos viejos por los actualizados |

### 4. Utilice componentes de acoplamiento débil
**Diseñe arquitecturas con componentes independientes

Con el acoplamiento débil, utiliza soluciones administradas como intermediarios entre las capas de su sistema. Con este diseño, el intermediario automáticamente maneja ambos errores y el escalado de los componentes o las capas.

Un equilibrador de carga enruta las solicitudes entre los servidores web y los servidores de aplicaciones. Si un servidor de aplicaciones deja de funcionar, el equilibrador de carga automáticamente comenzará a dirigir todo el tráfico a los dos servidores en buen estado. Dos soluciones primarias para desacoplar los componentes son los equilibradores de carga y las colas de mensajes.

### 5. Diseñe servicios, no servidores

**Use la variedad de servicios de AWS. No limite su infraestructura a servidores.

| Práctica no recomendada                                                                                | Práctica recomendada                                                                                                         |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Las aplicaciones simples se ejecutan en servidores persistentes                                        | Cuando corresponda, considere usar contenedores o una solución sin servidor                                                  |
| Las aplicaciones se comunican directamente entre sí                                                    | Las colas de mensajes manejan la comunicación entre aplicaciones                                                             |
| Los activos web estáticos se almacenan localmente en las instancias                                    | Los activos web estáticos se almacenan de manera externa, como en *Amazon Simple Storage Service* (Amazon S3)                |
| Los servidores backend manejan las autenticación de usuarios y el almacenamiento de estados de usuario | La autenticación de usuarios y el almacenamiento del estado de usuario son manejados por los servicios administrados por AWS |

### 6. Elija la solución de base de datos adecuada

**Adapte la tecnología a la carga de trabajo, no al revés

Aspectos a tener en cuenta:
* Las necesidades de lectura y escritura
* Requisitos de almacenamiento totales
* Tamaño habitual de los objetos y cómo se accede a ellos
* Requisitos de durabilidad
* Requisitos de latencia
* Número máximo de usuarios conectados al mismo tiempo
* Naturaleza de las consultas
* Intensidad necesaria de los controles de integridad

### 7. Evite los punto únicos de error

**Suponga que todo falla. Luego, diseñe en sentido inverso.
Cuando sea posible, use la redundancia para impedir que los puntos únicos hagan fallar un sistema completo

Una forma común de evitar los puntos únicos de error es crear un servidor de base de datos secundario (en espera) y replicar los datos. De este modo, si el servidor de base de datos principal se desconecta, el servidor secundario puede asumir la carga.

### 8. Optimice el costo

**Aproveche la flexibilidad de AWS para aumentar su eficiencia de costos

Aspectos para tener en cuenta:
* ¿Recursos son del tamaño y tipo adecuados?
* ¿Qué métrica debo supervisar?
* ¿Cómo me aseguro de desactivar los recursos que no están en uso?
* ¿Con qué frecuencia necesito usar este recurso?
* ¿Puedo reemplazar cualquiera de mis servidores con servidores administrados?

*Gastos de capital (CapEx)* son fondos que utiliza una empresa para adquirir, actualizar y mantener activos físicos como bienes, edificios industriales o equipos.
Los servicios de AWS usan un modelo de costos de *gastos variables*, lo que significa que solo paga por los servicios individuales que necesita, por el tiempo que los utilice.

### 9. Use el almacenamiento en caché

**El almacenamiento en caché minimiza las operaciones de recuperación de datos redundantes, lo que mejora el rendimiento y el costo

El *almacenamiento en caché* es una técnica para hacer futuras solicitudes con más rapidez y reducir el rendimiento de la red almacenando temporalmente los datos en una ubicación intermedia entre el solicitante y el almacenamiento permanente.

La infraestructura usa *Amazon CloudFront* antes de *Amazon S3* para ofrecer almacenamiento en caché. En esta situación, la solicitud inicial busca el archivo en *Amazon CloudFront*. Si no lo encuentra, *CloudFront* solicita el archivo a *Amazon S3*. Después, *CloudFront* almacena una copia del archivo en una ubicación perimetral cerca del usuario y envía una copia al usuario que hizo la solicitud. Las solicitudes posteriores del archivo se recuperan desde la (ahora más cercana) ubicación perimetral en *CloudFront* en lugar de Amazon S3.
Esto reduce la latencia y el costo porque, después de la primera solicitud, ya no debe pagar por la transferencia del archivo desde *Amazon S3*.

### 10. Proteja la infraestructura completa

**Incorpore seguridad en cada capa de su infraestructura

Aspectos a tener en cuenta:
* Aislar partes de su infraestructura
* Cifrar los datos en tránsito y en reposo
* Aplicar la granularidad del control de acceso, mediante el principio mínimo privilegio
* Utilizar la autenticación multifactor(MFA)
* Utilizar servicios administrados
* Registrar el acceso a recursos
* Automatizar las implementaciones para mantener la coherencia de la seguridad

*Amazon EC2* puede crear grupos de seguridad que le permitan determinar cuáles puertos en sus instancias pueden enviar y recibir tráfico. Los grupos de seguridad también pueden determinar el origen y destino de ese tráfico.

Puede usar grupos de seguridad para reducir la probabilidad de que una amenaza de seguridad en una instancia se propague a todas las demás instancias en su entorno.
Debe tomar precauciones similares con otros servicios. Las maneras específicas de implementar esta práctica recomendada se analizarán durante el curso.

### Pasos a seguir cuando cree soluciones en AWS:

* Habilite la escalabilidad
* Automatice su entorno
* Trate los recursos como desechables
* Utilice componentes de acoplamiento débil
* Diseñe servicios, no servidores
* Elija la solución de base de datos adecuada
* Evite los puntos únicos de error
* Optimice el costo
* Use el almacenamiento en cache
* Proteja la infraestructura completa

## Infraestructura global de AWS

### Regiones de AWS

+ Una región de AWS es una zona geográfica
+ Cada región de AWS consiste en dos o más zonas de disponibilidad
+ La comunicación entre regiones utiliza la infraestructura de red troncal de AWS
+ Usted habilita y controla la replicación de datos entre regiones

Una región de AWS es una ubicación geográfica física con dos o más zonas de disponibilidad. Las zonas de disponibilidad, a su vez, constan de uno o más centros de datos.

Las regiones AWS están conectadas con varios proveedores de servicios a internet (ISP, Internet Service Provider). Las regiones también están conectadas a una red troncal global privada, que proporciona un menos costo y una mayor uniformidad en la latencia de red entre regiones en comparación con la Internet Pública.

Para obtener tolerancia a errores y estabilidad, las regiones están aisladas unas de otras. Los recursos de una región no se replican automáticamente en otras regiones.

### Zonas de disponibilidad de AWS

+ Cada zona de disponibilidad:
	+ Se encuentra conformada por uno o más centros de datos
	+ Está diseñada para el aislamiento de errores
	+ Está interconectada con otras zonas de disponibilidad en una región por medio de enlaces privado de alta velocidad
+ Para algunos servicios, puede elegir la zona de disponibilidad
+ Para lograr resistencia, AWS recomienda la replicación entre zonas de disponibilidad

Es responsabilidad nuestra seleccionar las zonas de disponibilidad donde se encontrarán los sistemas. Los sistemas pueden abarcar varias zonas de disponibilidad. Debe diseñar
los sistemas para que sobrevivan a un error temporal o prolongado de una zona de disponibilidad si ocurre un desastre. La distribución de las aplicaciones en varias zonas de disponibilidad les permite mantenerse resistentes en la mayoría de las situaciones de error, incluidos los desastres naturales o errores de sistema.

### Zonas locales de AWS

+ Le permiten ejecutar partes de las aplicaciones sensibles a la latencia más cerca de los usuarios finales y los recursos en una ubicación geográfica específica
+ Son una extensión de una región de AWS en la que puede usar servicios de AWS en proximidad geográfica de los usuarios finales.
+ Le permiten ubicar servicios de cómputo, almacenamiento, base de datos y otros servicios seleccionados de AWS más cerca de la población, industrias y los centros de TI donde no hay una región en la actualidad.
+ Las administra y reciben soporte de AWS.

### Centros de datos de AWS

+ En los centros de datos se almacenan y se procesan los datos.
+ Un centro de datos suele alojar decenas de miles de servidores.
+ Todos los centros de datos se encuentran en línea y a disposición de los clientes.
+ Equipos de red personalizados de AWS:
	+ Provenientes de varios ODM
	+ Tienen una pila de protocolo de red personalizada
### Puntos de presencia de AWS

Amazon CloudFront utiliza una red global que incluye más de 200 puntos de presencia que se componen de ubicaciones perimetrales y cachés perimetrales regionales.

Las cachés perimetrales regionales se utilizan de forma con Amazon CloudFront. Se utilizan cuando tiene contenido al que no se accede con la frecuencia suficiente para que permanezca en una ubicación perimetral. Las cachés perimetrales regionales absorben este contenido y proporcionan una alternativa a recuperar ese contenido del servidor de origen.

Cuestionario 1:
Pregunta 1:
Pregunta 4: Elastic Load Balancing
Pregunta 5: Activa la automatización para aprovisionar un nuevo servidor
Pregunta 6: usuarios gradualmente
Pregunta 7: cloudfront