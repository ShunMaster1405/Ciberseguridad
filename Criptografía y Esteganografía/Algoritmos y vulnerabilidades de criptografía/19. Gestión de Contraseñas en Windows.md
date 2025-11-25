## Introducción

Windows utiliza diversos mecanismos para gestionar y almacenar contraseñas de manera segura.  
Estos sistemas han evolucionado considerablemente desde las primeras versiones del sistema operativo.

---

## Componentes Principales

### Security Accounts Manager (SAM)

- Ubicación: `C:\Windows\System32\config\SAM`
- Función: base de datos que almacena cuentas de usuario locales y sus hashes de contraseñas
- Protección: encriptado con una clave almacenada en el archivo SYSTEM

### Local Security Authority (LSA)

- Propósito: gestiona políticas de seguridad locales y autenticación
- Componentes:
    - **LSASS.exe**: proceso responsable de la autenticación
    - **LSA Secrets**: almacena credenciales de servicios y cuentas de sistema

### Active Directory (AD)

- Función: gestión centralizada de credenciales en entornos empresariales
- Base de datos: `NTDS.dit` contiene todos los objetos del directorio
- Replicación: sincronización entre controladores de dominio

---

## Tipos de Hashes en Windows

### NTLM (NT LAN Manager)

- Algoritmo: MD4
- Formato: 32 caracteres hexadecimales
- Ejemplo: `aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef`
- Características:
    - No utiliza salt
    - Vulnerable a ataques rainbow table
    - Aún utilizado por compatibilidad

### LM Hash (LAN Manager)

- Estado: deprecado desde Windows Vista
- Debilidades:
    - Convierte contraseñas a mayúsculas
    - Divide contraseñas en bloques de 7 caracteres
    - Extremadamente vulnerable

---

## Almacenamiento de Credenciales

### Credential Manager

- Ubicación: Panel de Control → Credential Manager
- Tipos:
    - Windows Credentials
    - Generic Credentials
- Almacenamiento: encriptado con DPAPI

### Data Protection API (DPAPI)

- Función: protege datos sensibles del usuario
- Claves:
    - Master Key: derivada de la contraseña del usuario
    - Backup Key: para recuperación por administradores
- Ubicación: `%APPDATA%\Microsoft\Protect\`

---

## Políticas de Contraseñas

### Configuración Local

```powershell
net accounts
secedit /configure /cfg C:\path\to\security.inf
```

### Group Policy Objects (GPO)

- Ruta: Computer Configuration → Windows Settings → Security Settings → Account Policies
- Opciones principales:
    - Longitud mínima de contraseña
    - Complejidad requerida
    - Historial de contraseñas
    - Tiempo de vida máximo

---

## Herramientas de Extracción

### Mimikatz

- Función: extracción de credenciales desde memoria
- Comandos principales:

```
sekurlsa::logonpasswords
sekurlsa::wdigest
sekurlsa::kerberos
```

### Secretsdump (Impacket)

- Uso: extracción remota de hashes
- Sintaxis:

```bash
secretsdump.py domain/user:password@target
```

---

## Medidas de Protección

### Windows Defender Credential Guard

- Función: protege credenciales usando virtualización
- Requisitos: hardware compatible con HVCI
- Configuración: Group Policy o Registry

### LAPS (Local Administrator Password Solution)

- Propósito: gestión automatizada de contraseñas de administrador local
- Características:
    - Contraseñas únicas por equipo
    - Rotación automática
    - Almacenamiento en Active Directory

---
