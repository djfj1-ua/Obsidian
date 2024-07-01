### Crear un grupo de seguridad para acceder al sistema de archivos de EFS

+ Selecciona EC2, a la izquierda selecciona Security Groups
+ Copia el valor de Security group ID
+ Selecciona *Create security group* y configura lo siguiente:
	+ **Security group name:** nombre del grupo de seguridad
	+ **Descripción:** descripción del grupo de seguridad
	+ VPC: Lab VPC
+ En la sección de Inbound rules, selecciona *Add rule* y configura:
	+ **Tipo:** NFS
	+ **Fuente:** Personalizar
	+ **Campo custom**: pega el ID del grupo de seguridad
+ Create security group

### Crear un sistema de archivos de EFS

+ En el menú elige EFS, selecciona *Create File System*
+ En la ventana *create file system*, elige personalizar
+ Paso 1:
	+ Desactiva *Enable automatic backups*
	+ Administración del ciclo de vida: Selecciona ninguno
	+ En la sección tags, configura:
		+ Clave: lo que quieras
		+ Valor: lo que quieras
+ Siguiente
+ En VPC, seleciona Lab VPC
+ Separa el grupo de seguridad predeterminado de cada destino de montaje de la zona de disponibilidad seleccionando la X de verificación de cada grupo de seguridad predeterminado.
+ Adjunta el grupo de seguridad de destino de montaje de EFS a cada destino de montaje de la *zona de disponibilidad*.
+ Seleccionando cada casilla de *Grupo de seguridad*
+ Seleccionando el destino de montaje de EFS
+ Elige siguiente.
+ Siguiente en el paso 3
+ En el paso 4 revisa la configuración y dale a crear.

### Conectarse a la instancia de EC2 mediante SSH

+ Details -> Show, en Credentials descarga Download PP