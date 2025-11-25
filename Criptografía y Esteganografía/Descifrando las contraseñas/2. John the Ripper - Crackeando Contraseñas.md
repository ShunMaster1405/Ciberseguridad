## Introducción a John the Ripper

**John the Ripper** es una herramienta de código abierto diseñada para detectar contraseñas débiles en sistemas Unix.  
Es altamente configurable y soporta múltiples formatos de hash.

---

## Instalación

### En Kali Linux

```bash
john --version
sudo apt update
sudo apt install john-jumbo
```

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install john
```

---

## Uso Básico de John the Ripper

### Sintaxis Básica

```bash
john [opciones] [archivo_hashes]
```

### Primer Ejemplo

```bash
echo "usuario1:$6$salt$hashedpassword" > hashes.txt
john hashes.txt
```

### Mostrar Contraseñas Crackeadas

```bash
john --show hashes.txt
john --show --format=crypt hashes.txt
```

---

## Formatos de Hash Soportados

### Listar Formatos Disponibles

```bash
john --list=formats
```

### Formatos Comunes

```bash
john --format=Raw-MD5 hashes.txt
john --format=Raw-SHA1 hashes.txt
john --format=NT hashes.txt
john --format=DES hashes.txt
```

---

## Tipos de Ataques con John

### Ataque de Diccionario

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --format=Raw-MD5 --wordlist=diccionario.txt hashes.txt
```

### Ataque de Fuerza Bruta

```bash
john --incremental hashes.txt
john --incremental=Lower hashes.txt
```

### Reglas de Mutación

```bash
john --rules --wordlist=diccionario.txt hashes.txt
john --rules=Wordlist --wordlist=diccionario.txt hashes.txt
```

---

## Configuración Avanzada

### Archivo de Configuración

```
/etc/john/john.conf
~/.john/john.conf
```

### Crear Reglas Personalizadas

```conf
[List.Rules:MiRegla]
$[0-9]$[0-9]
c
$!
$@
$#
```

---

## Herramientas Auxiliares

### Unshadow

```bash
unshadow /etc/passwd /etc/shadow > unshadowed.txt
john unshadowed.txt
```

### Zip2john

```bash
zip2john archivo.zip > zip_hash.txt
john zip_hash.txt
```

### Rar2john

```bash
rar2john archivo.rar > rar_hash.txt
john rar_hash.txt
```

---

## Ejemplo Práctico

### Crackear `/etc/shadow`

```bash
john password.txt
john --show password.txt
```

### Uso de Diccionarios

```bash
john --wordlist=passwords.lst password.txt
john --show password.txt
```

### Archivos Comprimidos

```bash
zip2john archivo.zip > hash.txt
john --format=zip --wordlist=/root/password.lst hash.txt
```

---
