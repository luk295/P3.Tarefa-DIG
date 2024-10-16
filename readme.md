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



### 6-Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org. 

### 7-Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?
### 8-Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?

### 9-Determina o TTL máximo (original) dun nome de dominio.
### 10-Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?

### 11-Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo
### 12-Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados
### 13-Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org
### 14-Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
