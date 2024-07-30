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

nmap -PS <objetivo>
Identifica los puertos abiertos que tiene una determinada máquina objetivo.

nmap -PS21 <objetivo> -p 21
Comprueba la conexión con la máquina objetivo con el puerto 21(-PS21) y después comprueba si el puerto 21 esta abierto (-p 21).

Puedo especificar más puertos tanto en el -PS (para que compruebe la conexión con esos puertos) o especificar más puertos en el -p (para saber si están abiertos).

Esto también se puede hacer para una red entera, especificando la dirección de red con la máscara (Ej: 192.168.32.0/24).
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
sudo nmap -sS <objetivo>
Realiza un escaneo TCP SYN stealth, comúnmente utilizado para evadir detección.
Deja a medias la comprobación del puerto ya que envia un RST para no hacer tanta interacción con la máquina atacante. Sin 3-Way HandShake completo.
Se puede hacer el escaneo con un rango de máquinas de esta forma:
nmap -sS 192.168.32.125-135 -> Esto realizara el escaneo de las máquinas en ese rango determinado.
nmap -sT <objetivo>
Igual que -sS pero si realiza el 3-Way HandShake completo.
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

### Escaneo con explicación
```sh
nmap --reason <objetivo>
Proporciona una razón de porque los puertos se encuentran en ese estado.
```

[[Ejemplos NMAP]]

### Estado de los puertos

#### Open
Una aplicación está aceptando activamente conexiones TCP, datagramas UDP o asociaciones SCTP en este puerto. Encontrar estos puertos es a menudo el objetivo principal del escaneo de puertos. Las personas preocupadas por la seguridad saben que cada puerto abierto es una vía para un ataque. Los atacantes y los testers de penetración quieren explotar los puertos abiertos, mientras que los administradores intentan cerrarlos o protegerlos con firewalls sin obstaculizar a los usuarios legítimos. Los puertos abiertos también son interesantes para los escaneos no relacionados con la seguridad porque muestran servicios disponibles en la red.

#### Closed
Nmap no puede determinar si el puerto está abierto porque el filtrado de paquetes impide que sus sondeos lleguen al puerto. El filtrado podría ser de un dispositivo de firewall dedicado, reglas de enrutador o software de firewall basado en el host. Estos puertos frustran a los atacantes porque proporcionan muy poca información. A veces responden con mensajes de error ICMP, como el tipo 3 código 13 (destino inalcanzable: comunicación administrativamente prohibida), pero los filtros que simplemente descartan los sondeos sin responder son mucho más comunes. Esto obliga a Nmap a reintentar varias veces por si acaso la sonda se descartó debido a la congestión de la red en lugar del filtrado. Esto ralentiza el escaneo dramáticamente.

#### Unfiltered
El estado sin filtrar (unfiltered) significa que un puerto es accesible, pero Nmap no puede determinar si está abierto o cerrado. Solo el escaneo ACK, que se utiliza para mapear conjuntos de reglas de firewall, clasifica los puertos en este estado. Escanear puertos sin filtrar con otros tipos de escaneo, como el escaneo Window, SYN o FIN, puede ayudar a resolver si el puerto está abierto.

#### Open/filtered
Nmap coloca los puertos en este estado cuando no puede determinar si un puerto está abierto o filtrado. Esto ocurre con tipos de escaneo en los que los puertos abiertos no dan respuesta. La falta de respuesta también podría significar que un filtro de paquetes descartó la sonda o cualquier respuesta que provocó. Por lo tanto, Nmap no sabe con certeza si el puerto está abierto o está siendo filtrado. Los escaneos UDP, de protocolo IP, FIN, NULL y Xmas clasifican los puertos de esta manera.

#### Closed/filtered
Este estado se usa cuando Nmap no puede determinar si un puerto está cerrado o filtrado. Solo se usa para el escaneo IP ID idle.