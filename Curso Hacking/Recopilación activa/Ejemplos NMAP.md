### Ejemplo nmap -sn (ip-objetivo)
#### Ejemplo sin privilegios de administrador

Vamos a probar como funciona el *nmap*, en este caso y para empezar, utilizaremos el comando
```sh
nmap -sn 192.168.32.169
```
Esta ip, es la ip de la máquina windows metasploit3. El resultado del comando es el siguiente: ![[Pasted image 20240721180124.png]]
Donde podemos ver como se ejecuta el programa.
Desde **Wireshark** podemos ver que se han intercambiado ciertos paquetes entre la máquina host (kali linux) a la máquina guest (windows).
![[Pasted image 20240721180845.png]]
Son envios de paquetes TCP SYN al puerto 80 y al puerto 443, para comprobar si estan activos. En este caso, podemos ver en el tercer paquete, que no hay nada corriendo en el puerto 443 y, en el quinto paquete, se ve que si hay algo funcionando en el puerto 80.

#### Ejemplo con privilegios de administrador

Este ejemplo se puede realizar de otra manera menos intrusiva, que es realizando el comando con privilegios de administrador.
```sh
sudo nmap -sn 192.168.32.169
```
Con su respectiva salida por terminal
![[Pasted image 20240721183047.png]]
En este caso, si miramos **Wireshark** nos damos cuenta que solo ha utilizado el protocolo ARP, haciendo así que no se haya establecido una conexión a diferentes puertos. 

El protocolo ARP se utiliza cuando dos máquinas estan dentro de la misma red. Su funcionamiento es el siguiente; la máquina host envia un paquete de difusión a la red local preguntando que dirección *MAC* tiene la dirección *IP* de destino, y recibe un paquete *ARP* de respuesta si la máquina destino existe indicando su dirección *MAC*.
![[Pasted image 20240721183337.png]]
Utilizando permisos de administrador, solo se ha preguntado a un unico puerto por lo que es mucho menos intrusivo.
También es más probable que funcione de esta manera ya que ejecutando el comando sin privilegios de administrador solo se pregunta a los puerto 443 y 80.

### Ejemplo nmap -sn (red-objetivo)

#### Sin privilegios de administrador
Ejecutamos el comando:
```sh
nmap -sn 192.168.32.0/24
```
Es la dirección de red la red local que estamos ut