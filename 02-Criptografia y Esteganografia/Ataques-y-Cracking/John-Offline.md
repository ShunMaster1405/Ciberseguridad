## Introducción a John the Ripper

### Descripción

John the Ripper es una herramienta de cracking de contraseñas de código abierto, diseñada para detectar contraseñas débiles en sistemas Unix/Linux y Windows.

### Características Principales

- Detección automática de múltiples formatos de hash
- Modos de ataque: diccionario, fuerza bruta, incremental
- Reglas flexibles de modificación de contraseñas
- Multiplataforma: Linux, Windows, macOS

---

## Instalación y Configuración

### Linux (Ubuntu/Debian)

```bash
sudo apt-get install john
git clone https://github.com/openwall/john
cd john/src
make
```

### Archivos de Configuración

- `john.conf`: configuración principal
- `john.pot`: contraseñas crackeadas
- Ubicación: `/etc/john/` o `~/.john/`

---

## Formatos de Hash Soportados

### Sistemas Unix/Linux

- DES: formato tradicional Unix
- MD5: `$1$salt$hash`
- SHA-256: `$5$salt$hash`
- SHA-512: `$6$salt$hash`

### Sistemas Windows

- NTLM: formato moderno
- LM: legacy (desaconsejado)

### Aplicaciones Web

- MySQL
- WordPress: `$P$salt$hash`
- Drupal: `$S$salt$hash`

---

## Modos de Operación

### Modo Single

```bash
john --single hashfile
```

Deriva contraseñas del nombre de usuario.

### Modo Wordlist

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashfile
```

Diccionarios comunes: `rockyou.txt`, `password.lst`, `darkweb2017-top10000.txt`

### Modo Incremental

```bash
john --incremental hashfile
```

Fuerza bruta inteligente con estadísticas de caracteres.

---

## Reglas de Mutación

### Sintaxis Básica

```bash
[List.Rules:Custom]
$[0-9]   # Añadir dígito al final
^[A-Z]   # Capitalizar primera letra
c        # Capitalizar
l        # Minúsculas
u        # Mayúsculas
```

### Reglas Avanzadas

```bash
sa4   # s -> 4
so0   # o -> 0
sa@   # s -> @
csa4$[0-9]   # Capitalizar + s->4 + dígito
```

---

## Ejemplos Prácticos

### Cracking de Shadow File

```bash
sudo unshadow /etc/passwd /etc/shadow > hashes.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --show hashes.txt
```

### Cracking de Hashes NTLM

```bash
echo "user:1001:aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef:::" > ntlm.txt
john --format=nt ntlm.txt
```

### Uso con Reglas Personalizadas

```bash
john --wordlist=passwords.txt --rules=custom hashes.txt
john --wordlist=passwords.txt --rules=Single hashes.txt
```

---

## Optimización y Rendimiento

### Paralelización

```bash
john --fork=4 hashfile
john --node=1/4 hashfile
john --node=2/4 hashfile
```

### Sesiones

```bash
john --session=mysession hashfile
john --restore=mysession
```

---

## Herramientas Auxiliares

### john2hashcat

```bash
john2hashcat.py hashfile > hashcat_format.txt
```

### Estadísticas

```bash
john --status=session_name
john --test
```

---
