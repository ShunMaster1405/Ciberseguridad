## Requisitos Previos

### Hardware mínimo

- RAM: 2GB (recomendado 4GB)
- USB: 8GB mínimo (recomendado 16GB)
- Procesador: x86_64 de 64 bits
- BIOS/UEFI: compatible con arranque USB

### Materiales necesarios

- USB confiable (marca reconocida)
- Conexión a internet
- Otro sistema operativo para crear el USB

---

## Descarga y Verificación

### Paso 1: Descargar Tails

- Visitar `https://tails.boum.org/install/`
- Seleccionar versión más reciente
- Descargar archivo ISO y archivo de firma

### Paso 2: Verificar integridad

- Usar herramientas gráficas o PowerShell en Windows
- Confirmar que el hash SHA256 coincide con el oficial

### Paso 3: Verificar autenticidad

- Usar claves públicas oficiales de Tails
- Confirmar firma digital de la ISO

---

## Creación del USB Booteable

### Opción 1: Tails Installer (recomendado)

- Herramienta oficial para Windows
- Seleccionar ISO y USB destino

### Opción 2: Balena Etcher

- Descargar desde `https://www.balena.io/etcher/`
- Seleccionar ISO y USB destino
- Clic en “Flash”

### Opción 3: Rufus

- Útil para BIOS antiguos
- Configuraciones específicas de arranque

---

## Configuración del BIOS/UEFI

### Acceso

- Reiniciar y presionar F2, F12, DEL o ESC
- Desde Windows: Configuración → Recuperación → Reinicio avanzado → Firmware UEFI

### Configuraciones necesarias

- Boot Order: USB primero
- Secure Boot: deshabilitar si es necesario
- Legacy Boot: habilitar en equipos antiguos
- Fast Boot: deshabilitar

### Guardar cambios

- “Save and Exit” o F10

---

## Primer Arranque

### Proceso

1. Insertar USB
2. Reiniciar equipo
3. Seleccionar arranque desde USB
4. Esperar carga del sistema

### Pantalla de bienvenida (Tails Greeter)

- Configurar idioma, teclado y formatos
- Opcional: contraseña admin, spoofing de MAC, configuración de red, Unsafe Browser

### Inicio del sistema

- Clic en “Start Tails”

---

## Configuración Inicial

### Verificar conexión Tor

- Tor Browser abre automáticamente
- Visitar `https://check.torproject.org/`
- Confirmar mensaje de éxito y nueva IP

### Configurar persistencia (opcional)

- Crear volumen persistente desde menú
- Seleccionar datos a guardar (documentos, marcadores, WiFi, software adicional)

### Configurar aplicaciones principales

- Thunderbird: correo seguro
- KeePassXC: gestor de contraseñas
- OnionShare: compartir archivos anónimamente

---

## Uso Seguro de Tails

### Mejores prácticas

- Evitar usuario administrador
- Verificar conexión Tor regularmente
- Mantener actualizado
- Usar solo aplicaciones incluidas
- Trabajar offline para documentos sensibles

### Gestión de archivos

- Temporales: carpeta amnesia (se borran al reiniciar)
- Persistentes: carpeta Persistent (si está configurada)

### Compartir archivos

- Usar OnionShare para enlaces `.onion` temporales

---

## Troubleshooting Común

### Problemas de arranque

- Verificar conexión USB
- Probar puertos USB 2.0
- Deshabilitar Secure Boot
- Actualizar BIOS/UEFI
- Re-formatear USB

### Problemas de red

- Verificar conexión física
- Usar Unsafe Browser en portales cautivos
- Configurar proxy manual
- Reiniciar servicio de red

### Problemas de rendimiento

- Aumentar RAM en VM
- Usar USB 3.0 rápido
- Cerrar apps innecesarias
- Reiniciar regularmente

### Problemas de compatibilidad

- Revisar lista oficial de hardware
- Usar drivers genéricos
- Reportar problemas a la comunidad
- Usar hardware estándar

---
