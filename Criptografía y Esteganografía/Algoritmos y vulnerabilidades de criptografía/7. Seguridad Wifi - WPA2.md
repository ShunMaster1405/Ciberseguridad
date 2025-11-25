## Introducción

**WPA2 (Wi-Fi Protected Access 2)** es el estándar de seguridad para redes inalámbricas que reemplazó a WEP y WPA.  
Basado en el estándar IEEE 802.11i, proporciona cifrado robusto y autenticación para redes WiFi.

---

## Arquitectura WPA2

### Componentes Principales

**1. Cifrado AES-CCMP**

- Utiliza AES en modo Counter with CBC-MAC Protocol
- Tamaño de bloque: 128 bits
- Proporciona confidencialidad e integridad

**2. Autenticación**

- **WPA2-Personal (PSK)**: clave pre-compartida
- **WPA2-Enterprise (802.1X)**: autenticación por servidor

**3. Gestión de Claves**

- Derivación de claves dinámicas
- Renovación periódica de claves
- Jerarquía de claves robusta

---

## Proceso de Autenticación WPA2

### WPA2-Personal (PSK)

```text
1. Cliente solicita conexión al AP
2. AP envía challenge
3. Cliente deriva claves a partir de PSK
4. Intercambio de 4-way handshake:
   - Mensaje 1: AP → Cliente (ANonce)
   - Mensaje 2: Cliente → AP (SNonce + MIC)
   - Mensaje 3: AP → Cliente (GTK + MIC)
   - Mensaje 4: Cliente → AP (Confirmación)
5. Establecimiento de comunicación cifrada
```

### WPA2-Enterprise (802.1X)

```text
1. Cliente se conecta al AP
2. AP actúa como proxy hacia servidor RADIUS
3. Autenticación EAP (TLS, PEAP, TTLS)
4. Servidor RADIUS valida credenciales
5. Distribución de claves dinámicas
6. Establecimiento de túnel cifrado
```

---

## Jerarquía de Claves WPA2

### Claves Principales

**1. PMK (Pairwise Master Key)**

- WPA2-Personal: `PMK = PBKDF2(passphrase, ssid, 4096, 256)`
- WPA2-Enterprise: derivada del servidor de autenticación

**2. PTK (Pairwise Transient Key)**  
Incluye:

- KCK (Key Confirmation Key)
- KEK (Key Encryption Key)
- TK (Temporal Key)

**3. GTK (Group Temporal Key)**

- Usada para tráfico multicast/broadcast
- Compartida entre clientes
- Renovada periódicamente

---

## Cifrado AES-CCMP

### Características

- Algoritmo: AES en modo Counter with CBC-MAC
- Tamaño de clave: 128 bits
- Autenticación: CBC-MAC
- Integridad: MIC de 64 bits

### Proceso de Cifrado

1. Construcción del nonce
2. Cifrado con AES-CTR
3. Generación de MIC

---

## Configuración Segura WPA2

### Mejores Prácticas

**Contraseña**

- Longitud mínima: 12 caracteres
- Combinar letras, números y símbolos
- Cambiar periódicamente

**Punto de Acceso**

- Ocultar SSID (opcional)
- Deshabilitar WPS
- Actualizar firmware
- Filtrado MAC (opcional)

**Enterprise**

- Certificados válidos en servidor RADIUS
- Métodos EAP seguros (TLS, PEAP)
- Políticas de contraseñas robustas
- Monitoreo de conexiones

---

## Vulnerabilidades y Ataques

### Ataques Conocidos

- **Diccionario**: captura del handshake y prueba de contraseñas comunes
- **KRACK**: reutilización de nonces, mitigado con parches
- **Desautenticación**: forzar reconexión de clientes para capturar handshakes

### Medidas de Protección

- Detección de intrusiones
- Segmentación de red (VLANs, aislamiento)
- Monitoreo continuo

---

## Herramientas de Análisis

### Auditoría

```bash
airmon-ng start wlan0
airodump-ng wlan0mon
aireplay-ng -0 10 -a [BSSID] wlan0mon
aircrack-ng -w wordlist.txt capture.cap
hashcat -m 2500 -a 0 capture.hccapx wordlist.txt
wireshark -i wlan0mon
```

### Laboratorio

```bash
sudo airmon-ng start wlan0
sudo airodump-ng wlan0mon
sudo tcpdump -i wlan0mon
sudo aireplay-ng --test wlan0mon
```

---

## Migración a WPA3

### Diferencias

- SAE (Simultaneous Authentication of Equals)
- Protección contra ataques offline
- Forward Secrecy
- Autenticación mejorada

### Consideraciones

- Compatibilidad con dispositivos legacy
- Configuración dual WPA2/WPA3
- Evaluación de beneficios

---
