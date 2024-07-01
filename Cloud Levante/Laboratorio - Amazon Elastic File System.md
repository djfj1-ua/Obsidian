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

+ Details -> Show, en Credentials descarga Download PPK y anota la dirección EC2PublicIP
+ Cierra Credentials
+ Abre PuTTY
+ Elige Session:
	+ En la parte de HostName pega el EC2PublicIP
	+ Ahora selecciona en la consola de EC2 y seleciona Instances
	+ Selecciona la instancia que deseas conectar
	+ En la pestaña *Description*, copia el valor de IPv4 Public IP
+ Vuelve a PuTTY y en Connection expande
+ Selecciona Auth y expande, dale a credentials
+ En private key file for authentication selecciona Browse y abre el archivo labsuser.ppk
+ Dale a accept y conectarte al host
+ Inicia sesion con ec2-user

### Crear un directorio nuevo y montar el sistema de archivos de EFS

+ En SSH crea un nuevo directorio *sudo mkdir efs*.
+ En la consola de administración de AWS, en el menú selecciona EFS.
+ Selecciona el nombre de My First EFS File System
+ En la consola de Amazon EFS, en la esquina superior derecha de la página, selecciona Attach(Adjuntar) para abrir las instrucciones de montaje de Amazon EC2.
+ Copia el comando completo en la sección *Using the NFS client*, el comando debe ser como este: 
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-bce57914.efs.us-west-2.amazonaws.com:/ efs

+ En tu sesión SSH de Linux, monta tu sistema de archivos Amazon EFS de la siguiente forma:
	+ Pegando el comando
	+ Presionando INTRO
+ Obtén un resumen completo del uso de espacio en disco disponible y utilizando ingresando:
	+ *sudo df -hT*

### Examinar el comportamiento de rendimiento del nuevo sistema de archivos de EFS
+ Para examinar las características de rendimiento de escritura del sistema de archivos, escribe lo siguiente:
sudo fio --name=fio-efs --filesize=10G --filename=./efs/fio-efs-test.img --bs=1M --nrfiles=1 --direct=1 --sync=0 --rw=write --iodepth=200 --ioengine=libaio