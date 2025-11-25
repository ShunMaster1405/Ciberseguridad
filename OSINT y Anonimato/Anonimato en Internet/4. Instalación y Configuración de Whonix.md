## ¿Qué es Whonix?

**Whonix** es un sistema operativo orientado a la privacidad que consta de dos máquinas virtuales:

- Whonix-Gateway: ejecuta Tor y actúa como puerta de enlace
- Whonix-Workstation: estación de trabajo completamente aislada

### Ventajas

- Aislamiento completo entre red y aplicaciones
- Prevención de leaks (imposible filtrar la IP real)
- Configuración automática de Tor
- Actualizaciones seguras y anónimas

---

## Requisitos del Sistema

### Hardware mínimo

- RAM: 2GB (recomendado 4GB+)
- Almacenamiento: 20GB libres
- Procesador con soporte de virtualización
- VT-x (Intel) o AMD-V habilitado en BIOS

### Software necesario

- Hipervisor: VirtualBox, VMware Workstation o KVM
- Sistema operativo host: Windows, macOS o Linux
- Conexión a internet para descargas y actualizaciones

---

## Instalación Paso a Paso

### Paso 1: Preparación del entorno

- Descargar VirtualBox desde el sitio oficial
- Instalar y reiniciar si es necesario
- Habilitar virtualización en BIOS/UEFI (VT-x, AMD-V)

### Paso 2: Obtener Whonix

- Descargar desde `https://www.whonix.org/download/`
- Obtener Whonix-Gateway y Whonix-Workstation
- Verificar integridad con checksums SHA256

### Paso 3: Importar en VirtualBox

- Abrir VirtualBox → Archivo → Importar servicio virtualizado
- Importar primero Gateway, luego Workstation
- Revisar configuración antes de confirmar

### Paso 4: Configuración de red

- Gateway: Adaptador 1 NAT, Adaptador 2 Red interna “Whonix”
- Workstation: Adaptador 1 Red interna “Whonix” (sin acceso directo a internet)

### Paso 5: Primera ejecución

- Arrancar primero Gateway y esperar configuración de Tor
- Verificar conexión Tor
- Iniciar Workstation y comprobar comunicación interna

---

## Configuración Avanzada

### Gateway

- Acceder a “Tor Control Panel”
- Configurar puertos, bridges (censura), o proxy intermedio

### Workstation

- Actualizar sistema desde terminal o gestor gráfico
- Instalar software adicional vía gestor de paquetes (descarga por Tor)

---

## Integración con Kali Linux

### Método 1: Kali como Workstation personalizada

- Crear VM con Kali Linux
- Configurar red interna “Whonix”
- Proxy manual:
    - HTTP/HTTPS → 10.152.152.10:8118
    - SOCKS → 10.152.152.10:9050

### Método 2: Uso de Proxychains

- Instalar `proxychains4`
- Configurar archivo con:

```
socks5 10.152.152.10 9050
```

- Usar anteponiendo `proxychains4` a los comandos

### Método 3: Configuración global

- Configurar proxy del sistema para usar Gateway de Whonix
- Aplicar a todas las aplicaciones

---

## Verificación y Pruebas

### Pruebas de funcionamiento

- IP: comprobar que sea distinta a la real
- DNS: confirmar que consultas pasan por Tor
- Aplicaciones: verificar que todo el tráfico use Tor
- Aislamiento: Workstation no debe acceder directo a internet

### Herramientas de verificación

- Navegador web (ej. whatismyipaddress.com)
- Herramientas de red
- Logs del sistema

---
