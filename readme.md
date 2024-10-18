# P3. Tarefa DIG


### 1-Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)
Fago `dig danielcastelao.org`.
O CNAME ou alias mostra: danielcastelao.org, o IN é clase internet, A é a dirección ip: 178.211.133.37, en QUERY SECTION :
```
;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 20:19:08 CEST 2024
;; MSG SIZE  rcvd: 63

```
ANSWER SECTION:
```
;; ANSWER SECTION:
danielcastelao.org.	304	IN	A	178.211.133.37
```
HEADER
```
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36735
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

```

### 2- Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org 
Na primeira liña:
``` 
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.danielcastelao.org
 
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> moodle.danielcastelao.org
```

No header:
```
www.danielcastelao.org(a):
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45034
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

moodle.danielcastelao.org(b):
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 17928
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
```
AUTHORITY SECTION:
(b):
```
;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300
```
ANSWER QUESTION
(a):
```
;; ANSWER SECTION:
www.danielcastelao.org.	900	IN	A	178.211.133.37
```

### 3- Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?
Con `dig NS wwww.danielcastelao.org`
```
;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300
```
Xa teño o nome dos servidores autoritativos.

Con `dig A + nome do servidor autoritativo`:
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> A ns1.hover.com.
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62750
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ns1.hover.com.			IN	A

;; ANSWER SECTION:
ns1.hover.com.		6425	IN	A	216.40.47.26

;; Query time: 19 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 20:56:06 CEST 2024
;; MSG SIZE  rcvd: 58

```
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> A dnsmaster.hover.com.
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 3739
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;dnsmaster.hover.com.		IN	A

;; ANSWER SECTION:
dnsmaster.hover.com.	900	IN	A	216.40.34.41

;; Query time: 159 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 20:57:06 CEST 2024
;; MSG SIZE  rcvd: 64

```

Suelen ser 2 servidores por temas de geolocalización y de sobrecarga.

### 4- Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.
`dig -x 130.206.164.68` :
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> -x 130.206.164.68
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45793
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;68.164.206.130.in-addr.arpa.	IN	PTR

;; ANSWER SECTION:
68.164.206.130.in-addr.arpa. 7200 IN	PTR	pluto.tlm.unavarra.es.
68.164.206.130.in-addr.arpa. 7200 IN	PTR	s164m68.unavarra.es.

;; Query time: 101 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 20:58:47 CEST 2024
;; MSG SIZE  rcvd: 113

```
`dig -x 8.8.8.8`:
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31753
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.	16477	IN	PTR	dns.google.

;; Query time: 19 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:00:51 CEST 2024
;; MSG SIZE  rcvd: 73

```
`dig -x 34.147.120.111`:
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> -x 34.147.120.111
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49467
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;111.120.147.34.in-addr.arpa.	IN	PTR

;; ANSWER SECTION:
111.120.147.34.in-addr.arpa. 120 IN	PTR	111.120.147.34.bc.googleusercontent.com.

;; Query time: 39 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:03:52 CEST 2024
;; MSG SIZE  rcvd: 109
```



### 5-A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?
Fago `dig localhost`:
```

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> localhost
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 54539
;; flags: qr aa rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;localhost.			IN	A

;; ANSWER SECTION:
localhost.		0	IN	A	127.0.0.1

;; Query time: 1 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:07:54 CEST 2024
;; MSG SIZE  rcvd: 54

```
Agora fago `dig NS 127.0.0.1`, que entendo que debería ser o proveedor de internet: 
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> NS 127.0.0.1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 60847
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;127.0.0.1.			IN	NS

;; AUTHORITY SECTION:
.			86332	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2024101601 1800 900 604800 86400

;; Query time: 37 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:08:06 CEST 2024
;; MSG SIZE  rcvd: 113

```

### 6-Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org. 
Pregúntolle con `dig SOA moodle.danielcastelao.org`
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> SOA moodle.danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 64980
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;moodle.danielcastelao.org.	IN	SOA

;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300

;; Query time: 135 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:12:11 CEST 2024
;; MSG SIZE  rcvd: 113
```
Preguntándolle ao servidor DNS de google:
`dig SOA moodle.danielcastelao.org @8.8.8.8`
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> SOA moodle.danielcastelao.org @8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 7958
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;moodle.danielcastelao.org.	IN	SOA

;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300

;; Query time: 161 msec
;; SERVER: 8.8.8.8#53(8.8.8.8) (UDP)
;; WHEN: Wed Oct 16 21:15:28 CEST 2024
;; MSG SIZE  rcvd: 113

```

### 7-Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?
`dig www.elpais.com`
```

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.elpais.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 44434
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.elpais.com.			IN	A

;; ANSWER SECTION:
www.elpais.com.		10	IN	CNAME	prisa-us-eu.map.fastly.net.
prisa-us-eu.map.fastly.net. 10	IN	A	199.232.194.133
prisa-us-eu.map.fastly.net. 10	IN	A	199.232.198.133

;; Query time: 2 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:22:21 CEST 2024
;; MSG SIZE  rcvd: 115

```
Queda almacenado 10 segundos.

Intento velo con `dig A 127.0.0.1` e obteño o SOA
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> A 127.0.0.1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 11707
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;127.0.0.1.			IN	A

;; AUTHORITY SECTION:
.			86396	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2024101601 1800 900 604800 86400

;; Query time: 38 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:26:29 CEST 2024
;; MSG SIZE  rcvd: 113

```

Agora fago dig ó servidor DNS para saber o TTL:
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> A a.root-servers.net.
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48084
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;a.root-servers.net.		IN	A

;; ANSWER SECTION:
a.root-servers.net.	259190	IN	A	198.41.0.4

;; Query time: 18 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:28:19 CEST 2024
;; MSG SIZE  rcvd: 63

```
259190 segundos.

### 8-Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?

Fixen dous indagación co dig a marca e a w3schools.

O que se mostra son os resultados na terminal para que se vexan as diferencias.
```
luk@luk-VirtualBox:~$ dig www.marca.com

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.marca.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34796
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.marca.com.			IN	A

;; ANSWER SECTION:
www.marca.com.		20	IN	CNAME	unidadeditorial.map.fastly.net.
unidadeditorial.map.fastly.net.	26 IN	A	199.232.197.50
unidadeditorial.map.fastly.net.	26 IN	A	199.232.193.50

;; Query time: 17 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:30:20 CEST 2024
;; MSG SIZE  rcvd: 118

luk@luk-VirtualBox:~$ dig www.w3schools.io

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.w3schools.io
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8259
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.w3schools.io.		IN	A

;; ANSWER SECTION:
www.w3schools.io.	1156	IN	CNAME	www.w3schools.io.cdn.cloudflare.net.
www.w3schools.io.cdn.cloudflare.net. 300 IN A	104.21.14.9
www.w3schools.io.cdn.cloudflare.net. 300 IN A	172.67.133.172

;; Query time: 24 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Oct 16 21:31:04 CEST 2024
;; MSG SIZE  rcvd: 126
```
As diferencias de TTL débense a que unha páxina está constantemente cambiando, polo que non ten sentido ter gardada a mesma información. Unha está actualizándose debido a que é de noticias.

En www.marca.com son de 20 segundos. Na outra é de 1156 segundos.



### 9-Determina o TTL máximo (original) dun nome de dominio.


### 10-Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?
`dig google.es ANY`:
```

luk@luk-VirtualBox:~$ dig google ns any
;; Warning, extra type option

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> google ns any
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31696
;; flags: qr rd ra; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.				IN	ANY

;; ANSWER SECTION:
google.			0	IN	NSEC3PARAM 1 0 1 379B1838B7824DD7
google.			0	IN	RRSIG	NSEC3PARAM 8 1 0 20241107073723 20241016073723 64063 google. HOz45p4J3dskTKAhbcZFxCh4nhLq6vQmr3m7nAIiMZB35Fy3xEB9irIm g9MoO/LrlbuhS6CDE7OIHkCL8BI7YFGQm4qQme055RYL+NOA+ZdOqtoC nVWYGX6KnyEUN4WNKV6dEOIDLhHBoITYdVZ571SrKTjVRTAKn514xfgX mPk=
google.			300	IN	DNSKEY	257 3 8 AwEAAYsyyXIFs0vL26Ot1DUGdX+G/9qD030Ei85Vj27B1mvlDgSeEp5u ckFfRjB3kj1oJDJ6iuEL/5ILXluaQkTap/SI18raPlNufS8ou/JS1vDk JBPVLMxN2Bb7fI7+Y+5hha+bu9k0GkgR1s1nkatsMDFj2eTK/TFkfM05 8aYZ7zew2so7EExMnQYdTZBHzdtcv5/5WhCt169w6dsjSLsSl4VOSoht rPuvakkQm7H7BI8SlqQo5WkDkkmgJsqURb6eTH9zmxqxeoxTgpi/RIeE kIjkHk0eLP/UfFc4yRPFUqZWmDc7UgH5gpM1mkYoHn+30cCBR6dqLWeX 0TS+jOAkcac=
google.			300	IN	DNSKEY	256 3 8 AwEAAYAEIfmF5ubHryDtwfj8W9F0ek7vkKRECKE3o1Ky/ZrZNEjVp+zA 1N/f+yYW+PjioNcPBKGcyfm+se0ByXpF+CqLjOTJOJa9l3YnZ+j7el0F OttjsrN96hBSMX2Wgss3y9RFPe/kc/MTE/QC/4H3PNayCmyZij2pThN4 qpAaBDV5
google.			300	IN	RRSIG	DNSKEY 8 1 300 20241107073723 20241016073723 6125 google. A82BaISOanYcbcFc+r95QQh8h8fRlZoFimSFf57gb+4A7wPMyaoRJPd9 fciJBoJQXc1yqdm39MKsgP4b4FWtJLpx8p1HJftAGy4LIw/D9rs+rASh t5Z7X9Bf8xG2TrH0Q7A1WYWHGOaY+5qRrau+JpKrfYZ/sWG+yYmmIeMz cgNE69XbtqBEPpoJ71LD7/zD36LSB4DWShgRgI8RmchDNEA85Kj0MAo8 S1KcEVvGB9Wo07axH07AnSUiPEHYvSv7byH5lJmSzF0FlC24++5FTzYb 9GX5WBkLiDRdEoH+xVZ6h//XhjN1/HxeF30LgemGBDyrJaR6PYy6jiN4 A0JgBg==
google.			21600	IN	SOA	ns-tld1.charlestonroadregistry.com. cloud-dns-hostmaster.google.com. 1 21600 3600 259200 900
google.			21600	IN	RRSIG	SOA 8 1 21600 20241107073723 20241016073723 64063 google. F6gLwvr+xQzCcmx/5jsJynNev6J2E4f4sdVsl2VTB1VEuJo71ycMJABe 4VPoppOEdTuuv+FoWBJbMGQFNy+64BMJwNfghThLSOfvIa+/0K3b1QC/ gZLrDlOfGJKq555wKHZOmIn4QLW647lGxt+eoiZZPa9AybMNmnRzcchK 9mI=
google.			21600	IN	NS	ns-tld1.charlestonroadregistry.com.
google.			21600	IN	NS	ns-tld5.charlestonroadregistry.com.
google.			21600	IN	NS	ns-tld3.charlestonroadregistry.com.
google.			21600	IN	NS	ns-tld4.charlestonroadregistry.com.
google.			21600	IN	NS	ns-tld2.charlestonroadregistry.com.
google.			21600	IN	RRSIG	NS 8 1 21600 20241107073723 20241016073723 64063 google. TJacAAzlSBVAoIVXHBczJoxfVrTFGMLkIftBijn+EkqYJ6jRG1aK4uC2 es0qhSXtiHRic8gN+kCA/DBgC4NsPlcp/zdmHyueuDduaBaEThAXdozC 9rw3IjuCb9EGBOoo+teH1oRjzxQ4oXqgUoTbRux0So8TgQlIeQs3W9UA Shs=

;; Query time: 129 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (TCP)
;; WHEN: Fri Oct 18 18:32:00 CEST 2024
;; MSG SIZE  rcvd: 1476
```
Non, xa que dependen da carga e do mellor camiño que ten que recorrer a resposta do servidor para obter o mellor resultado.

### 11-Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo

Executei o comando: `dig J.ROOTSERVERS.NET recurse`.
```
luk@luk-VirtualBox:~$ dig J.ROOTSERVERS.NET recurse

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> J.ROOTSERVERS.NET recurse
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29969
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 4

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;J.ROOTSERVERS.NET.		IN	A

;; ANSWER SECTION:
J.ROOTSERVERS.NET.	3382	IN	A	3.33.243.145
J.ROOTSERVERS.NET.	3382	IN	A	15.197.204.56

;; ADDITIONAL SECTION:
J.ROOTSERVERS.NET.	3382	IN	NS	ns2.smartname.com.
J.ROOTSERVERS.NET.	3382	IN	NS	ns1.smartname.com.
J.ROOTSERVERS.NET.	3382	IN	SOA	ns1.smartname.com. dns.jomax.NET. 2023061200 28800 7200 604800 86400

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Oct 18 18:40:07 CEST 2024
;; MSG SIZE  rcvd: 173

;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 46331
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;recurse.			IN	A

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Oct 18 18:40:07 CEST 2024
;; MSG SIZE  rcvd: 36
```



### 12-Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados





### 13-Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org

```
luk@luk-VirtualBox:~$ dig danielcastelao.org

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 4828
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 13

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;danielcastelao.org.		IN	A

;; ANSWER SECTION:
danielcastelao.org.	891	IN	A	178.211.133.37

;; ADDITIONAL SECTION:
danielcastelao.org.	891	IN	MX	130 aspmx4.googlemail.com.             ******************
danielcastelao.org.	891	IN	MX	90 alt1.aspmx.l.google.com.
danielcastelao.org.	891	IN	MX	140 aspmx5.googlemail.com.             ******************
danielcastelao.org.	891	IN	MX	120 aspmx3.googlemail.com.             ******************
danielcastelao.org.	891	IN	MX	110 aspmx2.googlemail.com.             ******************
danielcastelao.org.	891	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300
danielcastelao.org.	891	IN	MX	80 aspmx.l.google.com.
danielcastelao.org.	891	IN	NS	ns1.hover.com.
danielcastelao.org.	891	IN	MX	100 alt2.aspmx.l.google.com.
danielcastelao.org.	891	IN	NS	ns2.hover.com.
danielcastelao.org.	891	IN	TXT	"v=spf1 include:_spf.google.com ~all"
danielcastelao.org.	891	IN	TXT	"google-site-verification=YJ9h1U12oXB6DlEoHxCidyMFdM9H4FH2P1RrcAuDvxc"

;; Query time: 1 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Oct 18 19:01:58 CEST 2024
;; MSG SIZE  rcvd: 459
```




### 14-Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
