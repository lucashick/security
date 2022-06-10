# Recon Pentest Tools

## ASN - Información IP - Whois - DNS

* [Censys](https://censys.io/ipv4)
* [BGP](https://bgp.he.net)
* [Central Ops](https://centralops.net/co/)
* [Robtex](https://www.robtex.com/)
* [DNS Dumpster](https://dnsdumpster.com/)
* [MX Toolbox](https://mxtoolbox.com)
* `dig`

## Escaneo de puertos - red

* Zenmap - nmap
    ```bash
    nmap -T4 -A -v -Pn domain (Intense scan, no ping)
    nmap -f --open -sV domain (Quick scan, open ports)
    nmap -f --script discovery -sV domain
    nmap -f --script intrusive domain
    nmap target -sS -A -PN -sC -sV -vvv -p-65535
    -sS syn scan -A OS + service fingerprint -PN No Ping -sC Scripts -sV versions detection -vvv Verbosity -p-65535 (all ports)
    ```
* [Nmap Online](https://hackertarget.com/nmap-online-port-scanner/)
* [Shodan](https://shodan.io)
* [Nikto](https://github.com/sullo/nikto)
* [HTTProbe](https://github.com/tomnomnom/httprobe)
* SypapsInt
* NetCraft
* Striker

# Certificados

* [CRT](https://crt.sh)
* [SSL Labs](https://www.ssllabs.com)
* ssl-cert  
    ```nmap -sT -p 443 --script ssl-cert domain```
* ssl-enum-ciphers  
	```nmap -sT -p 443 --script ssl-enum-ciphers domain```
* script ssl-dh-params  
	```nmap -sT -p 443 --script ssl-dh-params domain```

## Enumeración de subdominios

* [Sublist3r](https://github.com/aboul3la/Sublist3r)
	```bash
    apt install sublist3r
	sublist3r -d domain -t 3 -e engine
    ```
* [Findomain](https://github.com/Findomain/Findomain)
* Massdns
* knockpy

## Búsqueda de contenido

### Tecnologías utilizadas

* [Wappalyzer](https://www.wappalyzer.com/)
* Cabeceras de la respuestas

### Métodos habilitados

`nmap -sT -p 443 domain --script http-methods`

### Directorios

* [Dirsearch](https://github.com/maurosoria/dirsearch)

### Keys

* [Secretfinder](https://github.com/m4ll0k/SecretFinder)

## Transferencia de zona

`dnsenum dominio`

## DNS Brutting

`dnsrecon -d dominio`   
`dnsmap dominio / dnsmap dominio -w diccionario`   
`dnsenum dominio -f diccionario`

## DNS Caché Snooping

`dnsrecon -t snoop -n servidor_dns -D listado_webs`

## Banner Grabbing

`echo "" | nc -v -n -w 1 IP 21-80`   

## Identificación del CMS

`whatweb -v dominio`   

### Vulnerabilidades y plugins

* BlindElephant: propósito general, contiene listado plugins Dupal y WordPress   
	```BlindElephant -u```   
	```BlindElephant dominio tipo_cms```   
* Nikto: propósito general   
	```nikto -update```   
	```nikto -h dominio```   
* Plecost: especializado en WordPress
* Wpscan: especializado en WordPress
* JoomScan: especializado en Joomla

### [wpscan](https://wpscan.com/wordpress-security-scanner)

* For all plugins with known vulnerabilities:  
    ```wpscan --url example.com -e vp --plugins-detection mixed --api-token YOUR_TOKEN```

* For all plugins in our database (could take a very long time):  
    ```wpscan --url example.com -e ap --plugins-detection mixed --api-token YOUR_TOKEN```

* Password brute force attack:  
    ```wpscan --url example.com -e u --passwords /path/to/password_file.txt```

