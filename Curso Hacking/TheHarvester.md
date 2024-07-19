TheHarvester es una herramienta esencial para profesionales de la seguridad y pentesters que necesitan recolectar información detallada sobre un dominio específico. Su capacidad para extraer datos de múltiples fuentes lo convierte en una herramienta poderosa para el reconocimiento pasivo.

Hemos tenido que crear una 'máquina virtual' para utilizar theHarvester 3.2.2 para poder utilizar google y poder almacenar los ficheros en html.

Para cambiar de entorno, hay que ir a la carpeta ~/old_harvester/theHarvester-3.2.2 y ejecutar: *conda activate old_harvester*.

# Optional Arguments

- `-h`, `--help`
  - Show this help message and exit.

- `-d DOMAIN`, `--domain DOMAIN`
  - Company name or domain to search.

- `-l LIMIT`, `--limit LIMIT`
  - Limit the number of search results, default=500.

- `-S START`, `--start START`
  - Start with result number X, default=0.

- `-g`, `--google-dork`
  - Use Google Dorks for Google search.

- `-p`, `--proxies`
  - Use proxies for requests, enter proxies in `proxies.yaml`.

- `-s`, `--shodan`
  - Use Shodan to query discovered hosts.

- `--screenshot SCREENSHOT`
  - Take screenshots of resolved domains, specify output directory: `--screenshot output_directory`.

- `-v`, `--virtual-host`
  - Verify host name via DNS resolution and search for virtual hosts.

- `-e DNS_SERVER`, `--dns-server DNS_SERVER`
  - DNS server to use for lookup.

- `-t DNS_TLD`, `--dns-tld DNS_TLD`
  - Perform a DNS TLD expansion discovery, default False.

- `-r`, `--take-over`
  - Check for takeovers.

- `-n`, `--dns-lookup`
  - Enable DNS server lookup, default False.

- `-c`, `--dns-brute`
  - Perform a DNS brute force on the domain.

- `-f FILENAME`, `--filename FILENAME`
  - Save the results to an HTML and/or XML file.

- `-b SOURCE`, `--source SOURCE`
    `baidu`, `bing`, `bingapi`, `bufferoverun`, `certspotter`, `crtsh`, `dnsdumpster`,
    `duckduckgo`, `exalead`, `github-code`, `google`, `hackertarget`, `hunter`, `intelx`,
    `linkedin`, `linkedin_links`, `netcraft`, `otx`, `pentesttools`, `projectdiscovery`,
    `qwant`, `rapiddns`, `securityTrails`, `spyse`, `sublist3r`, `threatcrowd`, `threatminer`,
    `trello`, `twitter`, `urlscan`, `virustotal`, `yahoo`.

Si aparece el 'error' *substring not found* es que la página a la que estoy referenciando ha bloqueado mi ip por hacer demasiadas peticiones.

Después de realizar algunas peticiones con TheHarvester es posible que os aparezca un error similar al siguiente:

![](https://img-c.udemycdn.com/redactor/raw/article_lecture/2022-05-23_18-30-54-bffa03d329e4e99f17f4ee0de78b1222.png)

Este error nos indica que Google ha bloqueado nuestra dirección IP pública. Lo que quiere decir que no nos deja realizar peticiones a su servicio desde ningún dispositivo que se encuentre dentro de nuestra red local.

Este comportamiento es muy frecuente y también debe tenerse en cuenta para las siguientes herramientas que se presentan en esta sección. Si realizas muchas peticiones automatizadas en poco tiempo a servicio como Google, Bing, Shodan... utilizando herramientas como theHarvester, estos servicios suelen bloquear temporalmente tu dirección IP pública para que no los satures.

Para resolver este problema tienes varias alternativas:

`1.` La más sencilla es esperar un tiempo hasta que el servicio correspondiente (ej. Google) desbloquee tu dirección IP pública. Esto suele tardar unos minutos o, como mucho, unas pocas horas. Probablemente si repites el mismo ejercicio dentro de unos minutos, comprobarás que ya te ha desbloqueado la IP

`2.` La segunda más sencilla es reiniciar tu router. En muchas ocasiones tu proveedor de Internet te asigna una dirección IP pública de manera dinámica, por lo tanto, apagando y encendiendo el router fuerzas a que se te asigne una dirección IP pública nueva que no estará bloqueada. Ten en cuenta que esto depende de tu proveedor de Internet y que no siempre funciona (puedes comprobar cuál es tu dirección IP pública aquí: https://www.whatsmyip.org/)

`3.` Puedes utilizar algún mecanismo de anonimización que te permita conectarte a internet a través de otra región y, por lo tanto, con otra dirección IP pública. El mecanismo más común es utilizar una VPN. Existen muchos servicios de VPN gratuitos, por mi experiencia personal, te recomiendo ProtonVPN. Este servicio tiene una versión gratuita que puedes utilizar. (Para más información sobre privacidad y anonimato te recomiendo mi curso de Udemy: _Curso de Ciberseguridad y Privacidad Online: VPN, Proxy, TOR)_

`4.` Por último, puedes cambiar la fuente en la que realizar la búsqueda y utilizar otras diferentes. Por ejemplo, si te bloquea Google, puedes realizar las peticiones a bing o duckduckgo, para ello utiliza la opción `-b` de theHarvester

Estas serían las opciones más sencillas para resolver el problema. También existirían otras alternativas interesantes un poco más complejas, como, por ejemplo, utilizar un proxy público para la salida a internet o conectarte mediante la red TOR.