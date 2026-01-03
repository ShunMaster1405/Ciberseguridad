## Pasos para Capturar Tráfico

### Paso 1: Preparación

1. Ejecutar Wireshark como administrador (Windows) o con permisos apropiados (Linux/macOS)
2. Identificar la interfaz de red correcta
3. Cerrar aplicaciones innecesarias para reducir ruido

---

### Paso 2: Configuración de Captura

1. Seleccionar interfaz:
    
    ```
    Capture → Interfaces → Seleccionar interfaz activa
    ```
    
2. Configurar opciones de captura:
    - **Promiscuous mode**: Activar si se desea capturar todo el tráfico
    - **Buffer size**: Ajustar según la memoria disponible
    - **File options**: Configurar guardado automático

---

### Paso 3: Aplicar Filtros de Captura (Opcional)

Los filtros de captura se aplican durante la captura y utilizan sintaxis **BPF (Berkeley Packet Filter)**:

```bash
# Capturar solo tráfico HTTP
port 80

# Capturar tráfico de/hacia una IP específica
host 192.168.1.100

# Capturar solo tráfico TCP
tcp

# Capturar tráfico de una subred específica
net 192.168.1.0/24

# Capturar tráfico de múltiples puertos
port 80 or port 443 or port 22
```

---

### Paso 4: Iniciar Captura

1. Hacer clic en el botón **Start** o presionar `Ctrl+E`
2. Generar tráfico de red (navegar, enviar emails, etc.)
3. Observar paquetes en tiempo real

---

### Paso 5: Detener Captura

1. Hacer clic en el botón **Stop** o presionar `Ctrl+E`
2. Guardar la captura si es necesario

---

## Filtros de Visualización

Los filtros de visualización se aplican después de la captura y permiten mostrar solo paquetes específicos.

### Filtros Básicos

```bash
http              # Tráfico HTTP
tls               # Tráfico HTTPS
ip.addr == 192.168.1.100
tcp               # Tráfico TCP
udp               # Tráfico UDP
tcp.port == 80    # Puerto específico
dns               # Tráfico DNS
```

---

### Filtros por Dirección IP

```bash
ip.src == 192.168.1.100       # Tráfico desde una IP específica
ip.dst == 192.168.1.100       # Tráfico hacia una IP específica
ip.addr == 192.168.1.0/24     # Tráfico de una subred
!(ip.addr == 192.168.1.100)   # Excluir tráfico de una IP
```

---

### Filtros por Puerto

```bash
tcp.port == 80 or udp.port == 80   # Puerto específico
tcp.srcport == 80                  # Puerto de origen
tcp.dstport == 80                  # Puerto de destino
tcp.port >= 1000 and tcp.port <= 2000   # Rango de puertos
```

---

### Filtros Avanzados

```bash
tcp.flags.syn == 1                 # Paquetes con flags TCP específicos
tcp contains "password"            # Paquetes con payload específico
frame.len > 1000                   # Paquetes de un tamaño específico
http and ip.src == 192.168.1.100   # Combinación de filtros
tcp.port == 80 or tcp.port == 443  # OR lógico
http and tcp.port == 80            # AND lógico
```

---

## Operadores de Filtros

### Operadores de Comparación

- `==` : Igual a
- `!=` : Diferente de
- `>` : Mayor que
- `<` : Menor que
- `>=` : Mayor o igual que
- `<=` : Menor o igual que

### Operadores Lógicos

- `and` : Y lógico
- `or` : O lógico
- `not` o `!` : Negación

### Operadores de Contenido

- `contains` : Contiene
- `matches` : Coincide con expresión regular

---
