## Ventana Principal de Wireshark

Cuando abres Wireshark, la interfaz se divide en varias secciones principales:

### 1. Barra de Menú

- **File**: Abrir, guardar, exportar capturas
- **Edit**: Copiar, buscar, preferencias
- **View**: Opciones de visualización
- **Go**: Navegación entre paquetes
- **Capture**: Opciones de captura
- **Analyze**: Herramientas de análisis
- **Statistics**: Estadísticas del tráfico
- **Tools**: Herramientas adicionales
- **Help**: Ayuda y documentación

---

### 2. Barra de Herramientas

- Botones de captura: iniciar, detener, reiniciar
- Botones de navegación: primer, anterior, siguiente, último paquete
- Botones de zoom: ampliar, reducir vista
- Botón de filtros: aplicar filtros de visualización

---

### 3. Barra de Filtros

- Campo de filtro de visualización
- Botón **Apply**: aplicar filtro
- Botón **Clear**: limpiar filtro
- Historial de filtros utilizados anteriormente

---

### 4. Panel de Lista de Paquete

- Muestra todos los paquetes capturados
- Columnas configurables:
    - **No.**: Número de paquete
    - **Time**: Marca de tiempo
    - **Source**: Dirección IP origen
    - **Destination**: Dirección IP destino
    - **Protocol**: Protocolo utilizado
    - **Length**: Longitud del paquete
    - **Info**: Información resumida

---

### 5. Panel de Detalles del Paquete

- Muestra la estructura jerárquica del paquete seleccionado
- Organizado por capas del modelo OSI
- Expandible por secciones

---

### 6. Panel de Bytes

- Muestra el contenido hexadecimal y ASCII del paquete
- Sincronizado con la selección en el panel de detalles
- Permite análisis a nivel de bits

---

## Tipos de Paquetes que se Pueden Capturar

### Protocolos de Capa 2 (Enlace de Datos)

- Ethernet
- Wi-Fi (802.11)
- PPP
- VLAN

### Protocolos de Capa 3 (Red)

- IPv4/IPv6
- ICMP
- ARP
- OSPF, BGP

### Protocolos de Capa 4 (Transporte)

- TCP
- UDP
- SCTP

### Protocolos de Capa 7 (Aplicación)

- HTTP/HTTPS
- FTP
- SMTP/POP3/IMAP
- DNS
- SSH
- Telnet

---

## Configuración de Interfaces

### Selección de Interfaz

1. Ir a **Capture → Interfaces**
2. Seleccionar la interfaz apropiada:
    - Ethernet (tráfico cableado)
    - Wi-Fi (tráfico inalámbrico)
    - Loopback (tráfico local)

---

### Opciones de Captura

- **Promiscuous mode**: Capturar todo el tráfico en el segmento
- **Monitor mode**: Para interfaces Wi-Fi (captura todo el tráfico 802.11)
- **Buffer size**: Tamaño del buffer de captura
- **Capture filter**: Filtrar durante la captura

---
