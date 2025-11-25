## ¿Qué es el Seguimiento de Flujo TCP?

El seguimiento de flujo TCP permite reconstruir una conversación completa entre dos hosts, mostrando todos los datos intercambiados en orden cronológico.

---

## Cómo Seguir un Flujo TCP

### Método 1: Menú Contextual

1. Seleccionar cualquier paquete del flujo TCP
2. Clic derecho
3. **Follow → TCP Stream**

### Método 2: Menú Principal

1. Seleccionar un paquete TCP
2. Ir a **Analyze → Follow → TCP Stream**

### Método 3: Atajo de Teclado

- **Ctrl+Alt+Shift+T** (Windows/Linux)
- **Cmd+Option+Shift+T** (macOS)

---

## Ventana de Seguimiento TCP

### Opciones de Visualización

1. **ASCII**: Texto legible, ideal para protocolos como HTTP/SMTP.
2. **EBCDIC**: Codificación usada en mainframes, poco común hoy.
3. **Hex Dump**: Datos en hexadecimal + ASCII.
4. **C Arrays**: Datos como arrays de C, útil para desarrollo.
5. **Raw**: Datos binarios sin procesar, necesario para extracción de archivos.

### Controles de Dirección

- Entire conversation
- Client → Server
- Server → Client

---

## Análisis de Conversaciones Específicas

### Sesión HTTP

```bash
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0...

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234
```

Información: headers completos, contenido web, cookies, parámetros POST.

### Sesión FTP

```bash
USER anonymous
PASS guest@example.com
230 Login successful
LIST
```

Información: credenciales, comandos, listados, archivos transferidos.

### Sesión SMTP

```bash
EHLO client.example.com
250-PIPELINING
250-SIZE 10240000
```

Información: comandos de autenticación y capacidades del servidor.

---

## Seguimiento de Flujos UDP

Aunque UDP no es orientado a conexión, Wireshark puede seguir flujos UDP.

### Casos de Uso

- DNS
- Streaming de video/audio
- Juegos en línea
- Protocolos IoT

---

## Análisis Avanzado de Flujos

### Estadísticas de Flujo

Ir a **Statistics → Conversations**

- Address A/B
- Port A/B
- Packets
- Bytes
- Duration

### Gráficos de Flujo

Ir a **Statistics → Flow Graph**

- Secuencia temporal
- Direcciones
- Tiempos de respuesta
- Problemas de conectividad

---

## Filtros Relacionados con Flujos

### Filtrar por Flujo Específico

```bash
tcp.stream eq 0
udp.stream eq 0
ip.addr == 192.168.1.100 and ip.addr == 192.168.1.200 and tcp.port == 80
```

### Análisis de Múltiples Flujos

```bash
tcp.stream eq 0 or tcp.stream eq 1
frame.time >= "2023-01-01 10:00:00" and tcp.stream eq 0
tcp.analysis.retransmission or tcp.analysis.duplicate_ack
```

---

## Exportación de Datos de Flujo

### Guardar Conversación Completa

1. Seguir flujo TCP/UDP
2. Seleccionar formato (ASCII, Raw, etc.)
3. Guardar con **Save As**

### Exportar Múltiples Flujos

1. Ir a **File → Export Specified Packets**
2. Aplicar filtros
3. Seleccionar formato
4. Guardar archivo

---

## Casos de Uso Prácticos

### Análisis Forense

- Reconstrucción de navegación web
- Extracción de transferencias FTP

### Análisis de Seguridad

- Detección de exfiltración de datos
- Identificación de comunicaciones maliciosas

### Troubleshooting de Red

- Handshakes TCP fallidos
- Retransmisiones
- Ventanas TCP

---

## Casos de Uso Prácticos

### Análisis Forense

Reconstrucción de Actividad Web:

```bash
# Filtrar actividad HTTP de usuario específico
ip.src == 192.168.1.100 and http

# Seguir flujos para reconstruir navegación
tcp.stream eq 0
```

Análisis de Transferencia de Archivos:

```bash
# Identificar transferencias FTP
ftp-data

# Seguir flujo para extraer archivos
tcp.stream eq 5
```

### Análisis de Seguridad

Detección de Exfiltración de Datos:

```bash
# Buscar conexiones sospechosas
tcp.flags.syn == 1 and ip.dst != 192.168.1.0/24

# Analizar contenido de conexiones externas
tcp.stream eq 10
```

Análisis de Comunicaciones Maliciosas:

```bash
# Buscar tráfico en puertos no estándar
tcp.port > 1024 and tcp.port < 65535

# Seguir flujos sospechosos
tcp.stream eq 15
```

### Troubleshooting de Red

Identificar Problemas de Conectividad:

```bash
# Buscar handshakes TCP fallidos
tcp.flags.syn == 1 and tcp.flags.ack == 0

# Analizar tiempos de respuesta
tcp.analysis.ack_rtt > 1.0
```

Diagnóstico de Rendimiento:

```bash
# Identificar retransmisiones
tcp.analysis.retransmission

# Analizar ventanas TCP
tcp.window_size == 0
```