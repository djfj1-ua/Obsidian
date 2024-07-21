## Definición
Nmap (Network Mapper) es una herramienta de código abierto utilizada para la exploración de redes y auditorías de seguridad. Permite descubrir hosts y servicios en una red informática mediante el envío de paquetes y el análisis de sus respuestas.

## Para Qué Sirve
Nmap se utiliza principalmente para:
- **Descubrimiento de Red**: Identificar dispositivos activos en una red.
- **Escaneo de Puertos**: Determinar los puertos abiertos en los dispositivos.
- **Detección de Servicios**: Identificar los servicios que se ejecutan en los puertos abiertos.
- **Detección de SO**: Determinar el sistema operativo y características de los dispositivos.
- **Auditoría de Seguridad**: Identificar vulnerabilidades y configuraciones erróneas en la red.
- **Monitoreo de Red**: Supervisar la disponibilidad y el rendimiento de los servicios de red.

## Funcionalidades
- **Descubrimiento de Hosts**: Identificación de dispositivos activos en una red (ping scan).
- **Escaneo de Puertos**: Detecta puertos abiertos, cerrados y filtrados en un host.
- **Detección de Servicios (Version Detection)**: Identificación de versiones de servicios y aplicaciones en ejecución.
- **Detección de Sistemas Operativos (OS Detection)**: Identificación del sistema operativo del host.
- **Escaneo de Scripts (Nmap Scripting Engine, NSE)**: Utiliza scripts para detectar vulnerabilidades, realizar auditorías y ejecutar tareas avanzadas.
- **Traceroute**: Determina la ruta tomada por los paquetes para llegar al host objetivo.
- **Escaneo de Firewalls**: Identificación de reglas y políticas de cortafuegos.
- **Escaneo de IPv6**: Soporte para escaneo en redes IPv6.
- **Generación de Informes**: Exportación de resultados en varios formatos (XML, HTML, etc.).

## Opciones de Ejecución
### Escaneo Básico
```sh
nmap <objetivo>
Escanea los 1,000 puertos TCP más comunes en el objetivo especificado.
```

### Escaneo de Hosts

```sh
nmap -sn <red>
Realiza un ping scan para descubrir hosts activos en una red.
```

### Escaneo de puertos
```sh
nmap -p <puertos> <objetivo>
Especifica puertos a escanear (e.g., `nmap -p 80,443 <objetivo>`).
```

### Detección de Servicios y Versiones
```sh
nmap -sV <objetivo>
Identifica servicios y versiones en los puertos abiertos.
```

### Detección de Sistemas Operativos
```sh 
nmap -o <objetivo>
Intenta detectar el sistema operativo del host.
```

### Escaneo Silencioso (Stealth Scan)
```sh
nmap -sS <objetivo>
Realiza un escaneo TCP SYN stealth, comúnmente utilizado para evadir detección.
```

### Uso de Nmap Scripting Engine (NSE)
```sh
nmap --script=<script> <objetivo>
Ejecuta scripts NSE específicos para tareas avanzadas (e.g., `nmap --script=vuln <objetivo>`).
```

### Traceroute
```sh
nmap --traceroute <objetivo>
Determina la ruta tomada por los paquetes para llegar al host objetivo.
```

### Escaneo de Red Completa
```sh
nmap -A <objetivo>
Realiza un escaneo completo que incluye detección de servicios, sistema operativo, scripts y traceroute.
```

### Generación de Informes
```sh
nmap -oX <archivo.xml> <objetivo>
Guarda los resultados en formato XML.
```

### Escaneo de Modo Verbose
```sh
nmap -v <objetivo>
Proporciona salida detallada del escaneo.
```

### Ejemplo

Vamos a probar como funciona el *nmap*, en este caso y para empezar, utilizaremos el comando
```sh
nmap -sn 192.168.32.169
```
Esta ip, es la ip de la máquina windows metasploit3. El resultado del comando es el siguiente: ![[Pasted image 20240721180124.png]]
Donde podemos ver como se ejecuta el programa.
Desde **Wireshark** podemos ver que se han intercambiado ciertos paquetes entre la máquina host (kali linux) a la máquina guest (windows).
![[Pasted image 20240721180845.png]]
Son envios de paquetes TCP SYN al puerto 80 y al puerto 443, para comprobar si estan activos. En este caso, podemos ver en el tercer paquete, que no hay nada corriendo en el puerto 443 y, en el quinto paquete, se ve que si hay algo funcionando en el puerto 80.