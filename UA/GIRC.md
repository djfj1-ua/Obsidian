# Práctica 1
## Parte 1
Primero he borrado la VPC que venia por defecto de AWS y he creado la mía propia my-vpc. La red es 192.168.0.0/24 de clase C.![[Pasted image 20250207183611.png]]
Ahora, creare las subredes. Son 2 privadas y una pública. Las subredes tendrán máscara de red de 26 bits para poder crear 4 subredes, de las cuales solo usaremos 3.
![[Pasted image 20250207184440.png]]
Tenemos que crear las 3 instancias EC2, hay que crear una en la subred privada 1, otra en la subred privada 2 y otra en la subred pública. En la instancia de la subred pública hay que habilitar que se genere la ip pública automáticamente.
![[Pasted image 20250213093454.png]]
He accedido a mi maquina de ruter por ssh habilitando el trafico ssh desde mi IP, he ejecutado el comando sudo yum install iptables-services -y para descargar iptables y poder usarlas.
Activo el iptables con los comandos: 
- sudo systemctl enable iptables sudo systemctl start iptables.
He creado el fichero /etc/sysctl.d/custom-ip-forwarding.conf donde he escrito:
- net.ipv4.ip_forward=1 
para hacer persistente el reenvio de IP despues del reinicio. Luego he ejecutado el comando:
- sudo sysctl -p /etc/sysctl.d/custom-ip-forwarding.conf 
para aplicar el archivo de configuracion.
Ejecuto el comando netstat -i para ver las interfaces de red, se puede ver que hay creadas dos interfaces, la eth0 y la loopback.
![[Pasted image 20250213095128.png]]
Ahora hay que configurar la NAT. Para esto ejecuto los siguientes comandos:
- sudo /sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
- sudo /sbin/iptables -F FORWARD
- sudo service iptables save

He configurado los grupos de seguridad de las subredes privadas, para las reglas de entrada y salida he puesto que se admita todo el trafico desde el router.
Para la subred publica, he puesto que permita el acceso desde las subredes privadas y desde internet. Para las reglas de salida, que pueda enviar a las subredes privadas y a internet.

He creado tambien unas tablas de ruta para cada subred. En la tabla de la subred de la red privada A he puesto dos entradas, una para la puerta de enlace por defecto que apunta al router y otra para conectarse a la instancia B que tambien apunta al router. En la tabla de la subred privada B es lo mismo pero para conectarse a la instancia A.
En la tabla del router tiene una entrada solo que es para salir a internet, ya que las redes A y B estan conectadas directamente al router.

Ahora voy a editar los ficheros */etc/hosts* de las 3 instancias para añadir un nombre de dominio a las ips del router, NodeA y NodeB.
![[Pasted image 20250213095400.png]]
Ahora podré usar NodeA en lugar de su IP, también para NodeB.
## Parte 2
1. Para borrar las tablas nat y filter se ejecuta los siguientes comandos:
- sudo iptables -t filter -F -> el -F significa "flush" que hace que se eliminen todas las reglas de la tabla especificada.
- sudo iptables -t nat -F

2. Para establecer por defecto DROP en las reglas de la tabla filter tendremos que realizar los siguientes comandos:
- sudo iptables -t filter -P INPUT DROP
- sudo iptables -t filter -P FORWARD DROP
- sudo iptables -t filter -P OUTPUT DROP

Tuve que permitir el acceso por ssh en la tabla filter para no desconectarme de la instancia con los siguientes comandos: 
- sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
- sudo iptables -A OUTPUT -p tcp --dport 22 -m state --state ESTABLISHED -j ACCEPT

Esto hace que permita las nuevas conexiones y las conexiones ya establecidas por el puerto 22, también permite las respuestas por el puerto 22 de las conexiones ya establecidas.

También añadiré una entrada en la tabla OUTPUT para permitir los mensajes de vuelta para las conexiones por ssh a las máquinas de las redes privadas:
- sudo iptables -I OUTPUT -p tcp --dport 22 -j ACCEPT

Para borrar una entrada de la iptable: 
- sudo iptables -D INPUT <número_de_línea>

Para que las iptables no se reseteen al reiniciar la instancia, ejecutare el siguiente comando:
- sudo service iptables save
Para habilitar el servicio de iptables para que se inicie al arrancar el sistema:
- sudo systemctl enable iptables

1. Ahora hay que permitir las peticiones HTTP que llegan desde NodeA y NodeB que vayan dirigidas a cualquier equipo del exterior:
Hay que crear una regla para permitir el trafico HTTP desde la redA hacia cualquier destino:
- sudo iptables -A FORWARD -p tcp --dport 80 -s 192.168.0.0/26 -j ACCEPT
Y lo mismo para la red B:
- sudo iptables -A FORWARD -p tcp --dport 80 -s 192.168.0.64/26 -j ACCEPT
Hay tambien que permitir las respuestas a estas solicitudes HTTP:
- sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
**Related** sirve para permitir paquetes que no pertenecen directamente a una conexión establecida pero si que esta relacionada con ella.

2. Permitir la comunicación desde el Router y desde el nodo de la red b con un servidor Web escuchando en el Nodo A (Ubuntu 1). Permitir la comunicación también desde el nodo anfitrión.
Primero tendremos que crear en el nodo A un servidor web, he instalado python3 para crear el servidor. He hecho un pequeño index.html:
<html><body><h1>Hola desde mi servidor web con Python!</h1></body></html>
Para poner el servidor en escucha en el puerto 80: 
- sudo python3 -m http.server 80
Para permitir el trafico HTTP desde la red B a la red A:
- sudo iptables -A FORWARD -p tcp -s 192.168.0.64/26 -d NodeA --dport 80 -j ACCEPT
Para permitir tambien el trafico HTTP desde el router:
- sudo iptables -A OUTPUT -p tcp -d NodeA --dport 80 -j ACCEPT

1. Permitir el acceso mediante ping desde las redes A y B al router y viceversa he creado cuatro entradas en la iptable, 2 en OUTPUT y 2 en INPUT:
- sudo iptables -I INPUT -p icmp -s NodeA -j ACCEPT
- sudo iptables -I INPUT -p icmp -s NodeB -j ACCEPT
- sudo iptables -I OUTPUT -p icmp -s NodeA -j ACCEPT
- sudo iptables -I OUTPUT -p icmp -s NodeB -j ACCEPT

2. Permitir el acceso mediante ping desde la red A a la red B y denegar el acceso en sentido contrario. Para denegar el acceso en el sentido B -> A no es necesario hacer nada ya que tiene la politica por defecto drop, para el sentido A -> B:
- sudo iptables -I FORWARD -p icmp -s 192.168.0.0/26(red A) -d 192.168.0.64/26(red B) -j ACCEPT

3. Registrar los log que tengan la cadena /etc/passwd:
- sudo iptables -A INPUT -m string --string "/etc/passwd" --algo bm -j LOG --log-prefix "***** GIRC 2023: GET /ETC/PASSWD ***** "
- sudo iptables -A OUTPUT -m string --string "/etc/passwd" --algo bm -j LOG --log-prefix "***** GIRC 2023: GET /ETC/PASSWD ***** "
- sudo iptables -A FORWARD -m string --string "/etc/passwd" --algo bm -j LOG --log-prefix "***** GIRC 2023: GET /ETC/PASSWD ***** "

4. Registrar los logs del trafico desechado indicando como prefijo una cadena:
- sudo iptables -A INPUT -j LOG --log-prefix "***** GIRC 2023: PRACTICA 1 - DESECHADO ***** " --log-level 4
- sudo iptables -A OUTPUT -j LOG --log-prefix "***** GIRC 2023: PRACTICA 1 - DESECHADO ***** " --log-level 4
- sudo iptables -A FORWARD -j LOG --log-prefix "***** GIRC 2023: PRACTICA 1 - DESECHADO ***** " --log-level 4

No se porque pero se corta la cadena que aparece en el enunciado.
Las iptables del Router quedarían de la siguiente manera:![[Pasted image 20250213101413.png]]