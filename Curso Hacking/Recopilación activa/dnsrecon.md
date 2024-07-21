## Definición
DNSRecon es una herramienta de línea de comandos para la enumeración y recopilación de información sobre servidores DNS. Es utilizada principalmente en el campo de la ciberseguridad para realizar análisis de reconocimiento y auditoría de seguridad.

## Funcionalidades
- **Enumeración de Registros**: Recupera diferentes tipos de registros DNS, incluyendo A, AAAA, CNAME, MX, NS, SOA, TXT y SRV.
- **Transferencia de Zona**: Intenta realizar una transferencia de zona para obtener una copia completa de los registros DNS.
- **Búsqueda de Subdominios**: Identifica subdominios mediante diccionarios predefinidos y búsquedas de fuerza bruta.
- **Recopilación de Información**: Obtiene datos sobre servidores DNS, servidores de correo y otras infraestructuras.
- **Recursividad y Autoridad**: Verifica si los servidores DNS permiten consultas recursivas y si son autoritativos.
- **Búsqueda Inversa**: Realiza búsquedas inversas para obtener nombres de dominio a partir de direcciones IP.
- **GeoIP**: Determina la ubicación geográfica de las direcciones IP asociadas con los registros DNS.
- **Enumeración de Registros SPF y DKIM**: Recupera y analiza registros relacionados con la autenticación del correo electrónico.

## Opciones
- **Enumeración Completa**: `-t std` realiza una enumeración estándar de todos los registros DNS disponibles.
- **Fuerza Bruta de Subdominios**: `-D <diccionario>` utiliza un diccionario para realizar una búsqueda de fuerza bruta de subdominios.
- **Transferencia de Zona**: `-t axfr` intenta una transferencia de zona DNS.
- **Búsqueda Inversa**: `-r <rango>` realiza búsquedas inversas en un rango de IP especificado.
- **Recursividad**: `-t rvl` verifica si los servidores DNS permiten consultas recursivas.
- **GeoIP**: `--geoip` incluye información de ubicación geográfica en los resultados.
- **Registros SPF y DKIM**: `-t tld` recupera y analiza registros SPF y DKIM para dominios de alto nivel.
- **Salida a Archivo**: `-o <archivo>` guarda los resultados en un archivo especificado.
- **Formato de Salida**: `-f <formato>` define el formato de salida (e.g., json, csv).

## Uso Básico
```sh
dnsrecon -d example.com -t std
