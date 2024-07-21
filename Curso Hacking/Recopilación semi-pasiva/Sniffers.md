## Definición
Un sniffer es una herramienta que captura y analiza el tráfico de red. Permite a los usuarios interceptar y examinar datos que se transfieren a través de la red en tiempo real. Son utilizados para el diagnóstico de problemas de red, monitoreo de la seguridad, análisis forense y otras aplicaciones relacionadas con la administración de redes y la ciberseguridad.

# Wireshark

## Definición
Wireshark es un analizador de paquetes de red de código abierto que permite capturar y visualizar los datos que se transfieren a través de una red en tiempo real.

## Funcionalidades
- **Captura de Paquetes**: Captura tráfico de red en tiempo real desde múltiples interfaces.
- **Filtrado**: Filtros avanzados para capturar solo el tráfico relevante.
- **Decodificación**: Decodifica más de mil protocolos de red, mostrando los datos en formato legible.
- **Análisis en Tiempo Real y Diferido**: Permite analizar el tráfico en tiempo real o guardar las capturas para un análisis posterior.
- **Estadísticas y Gráficos**: Proporciona estadísticas detalladas y gráficos para visualizar patrones de tráfico.
- **Exportación**: Exporta datos en varios formatos (CSV, XML, JSON, etc.).
- **Seguimiento de Flujos**: Facilita el seguimiento de flujos TCP, UDP y otros tipos de tráfico.
- **Interfaz Gráfica**: Ofrece una interfaz gráfica de usuario (GUI) amigable.

## Opciones
- **Filtros de Captura**: Definen qué paquetes se capturan (e.g., `tcp port 80`).
- **Filtros de Visualización**: Filtran y muestran los paquetes capturados (e.g., `http && ip.addr == 192.168.1.1`).
- **Colores Personalizables**: Destaca diferentes tipos de tráfico utilizando colores.
- **Complementos y Extensiones**: Soporte para plugins que amplían la funcionalidad.

# tcpdump

## Definición
tcpdump es una herramienta de línea de comandos para capturar y analizar tráfico de red. Es poderosa y ligera, ideal para usuarios avanzados y administradores de sistemas.

## Funcionalidades
- **Captura de Paquetes**: Captura tráfico de red en tiempo real.
- **Filtrado de Paquetes**: Usa expresiones de filtrado de Berkeley Packet Filter (BPF) para capturar tráfico específico.
- **Salida Detallada**: Muestra detalles de los paquetes capturados, incluyendo encabezados y datos.
- **Guardado de Capturas**: Guarda capturas en archivos para análisis posterior.
- **Soporte de Protocolos**: Soporte para varios protocolos de red.
- **Interpretación de Protocolo**: Decodifica y muestra información de protocolos comunes.

## Opciones
- **Interfaz**: Especifica la interfaz de red a utilizar (e.g., `tcpdump -i eth0`).
- **Salida a Archivo**: Guarda las capturas en un archivo (e.g., `tcpdump -w capture.pcap`).
- **Lectura de Archivos**: Lee capturas desde un archivo (e.g., `tcpdump -r capture.pcap`).
- **Expresiones de Filtro**: Filtra el tráfico capturado (e.g., `tcpdump 'tcp port 80'`).
- **Número de Paquetes**: Limita el número de paquetes a capturar (e.g., `tcpdump -c 100`).
- **Verbosidad**: Ajusta el nivel de detalle de la salida (e.g., `-v`, `-vv`).

Wireshark y tcpdump son herramientas esenciales para el análisis de tráfico de red, cada una con sus fortalezas específicas: Wireshark con su interfaz gráfica rica en funcionalidades, y tcpdump con su eficiencia y versatilidad en la línea de comandos.
