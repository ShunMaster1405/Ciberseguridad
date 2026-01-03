## Estructura de un Paquete

Cada paquete capturado en Wireshark contiene información organizada por capas:

### Información de Frame (Capa 1)

- Arrival Time: Momento de captura
- Frame Length: Longitud total del frame
- Capture Length: Longitud capturada
- Protocols in frame: Protocolos presentes

---

### Información de Ethernet (Capa 2)

- Destination MAC: Dirección MAC destino
- Source MAC: Dirección MAC origen
- EtherType: Tipo de protocolo de capa superior

---

### Información de IP (Capa 3)

- Version: IPv4 o IPv6
- Header Length: Longitud del header IP
- Type of Service: QoS
- Total Length: Longitud total del paquete
- Identification: Identificador del paquete
- Flags: Fragmentación
- Fragment Offset: Offset de fragmento
- Time to Live: TTL
- Protocol: Protocolo de capa superior
- Header Checksum: Checksum del header
- Source Address: Dirección IP origen
- Destination Address: Dirección IP destino

---

### Información de TCP/UDP (Capa 4)

#### TCP

- Source Port / Destination Port
- Sequence Number / Acknowledgment Number
- Header Length
- Flags: SYN, ACK, FIN, RST, PSH, URG
- Window Size
- Checksum
- Urgent Pointer

#### UDP

- Source Port / Destination Port
- Length
- Checksum

---

## Análisis de Protocolos Específicos

### HTTP

```bash
http.request
http.response
http.request.method == "GET"
http.response.code == 200
http.host == "www.example.com"
http.request.uri contains "/admin"
```

Campos importantes: Request Method, Request URI, HTTP Version, Status Code, Headers.

---

### DNS

```bash
dns.flags.response == 0   # Consultas
dns.flags.response == 1   # Respuestas
dns.qry.type == 1         # A record
dns.qry.name contains "google.com"
```

Campos importantes: Transaction ID, Flags, Question, Answer, Authority, Additional.

---

### TCP

```bash
tcp.flags.syn == 1
tcp.flags.fin == 1
tcp.flags.reset == 1
tcp.analysis.retransmission
tcp.window_size == 0
```

---

## Filtros de Visualización Avanzados

### Filtros por Contenido

```bash
tcp contains "password"
http contains "login"
udp contains "secret"
http.request.uri matches ".*\\.php$"
```

### Filtros por Tiempo

```bash
frame.time >= "2023-01-01 00:00:00" and frame.time <= "2023-01-01 23:59:59"
frame.time_relative >= 0 and frame.time_relative <= 10
```

### Filtros por Análisis TCP

```bash
tcp.analysis.duplicate_ack
tcp.analysis.out_of_order
tcp.analysis.zero_window
tcp.analysis.fast_retransmission
```

---

## Coloreo de Paquetes

Wireshark utiliza colores para identificar diferentes tipos de tráfico:

### Colores Predeterminados

- Verde claro: TCP
- Azul claro: UDP
- Negro: Paquetes con errores
- Amarillo: HTTP
- Púrpura: ICMP
- Gris: ARP

### Personalizar Colores

1. Ir a **View → Coloring Rules**
2. Crear nuevas reglas de color
3. Aplicar filtros específicos

---
