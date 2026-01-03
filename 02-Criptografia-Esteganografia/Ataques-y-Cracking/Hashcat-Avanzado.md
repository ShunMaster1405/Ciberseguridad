## Introducción a Hashcat

**Hashcat** es considerado el "cracker de contraseñas más rápido del mundo".  
Utiliza la potencia de GPU y CPU para crackear hashes de manera extremadamente eficiente.

---

## Instalación

### Kali Linux

```bash
hashcat --version
sudo apt install hashcat
```

### Drivers GPU

```bash
sudo apt install nvidia-driver
sudo apt install mesa-opencl-icd
```

---

## Arquitectura de Hashcat

### Componentes Principales

- Motor de Hash
- Motor de Ataque
- Motor de Reglas
- Motor de Distribución

### Tipos de Hashcat

- hashcat (GPU)
- hashcat-legacy
- hashcat-utils

---

## Modos de Ataque

### Modo 0: Diccionario Directo

```bash
hashcat -m 0 -a 0 hashes.txt wordlist.txt
```

### Modo 1: Combinación

```bash
hashcat -m 0 -a 1 hashes.txt wordlist1.txt wordlist2.txt
```

### Modo 3: Fuerza Bruta

```bash
hashcat -m 0 -a 3 hashes.txt ?a?a?a?a?a?a
```

### Modo 6: Híbrido

```bash
hashcat -m 0 -a 6 hashes.txt wordlist.txt ?d?d?d
```

---

## Tipos de Hash Soportados

### Hashes Comunes

```bash
hashcat -m 0 hashes.txt wordlist.txt      # MD5
hashcat -m 100 hashes.txt wordlist.txt    # SHA-1
hashcat -m 1400 hashes.txt wordlist.txt   # SHA-256
hashcat -m 1000 hashes.txt wordlist.txt   # NTLM
```

### Hashes con Salt

```bash
hashcat -m 10 hashes.txt wordlist.txt     # MD5 con salt
hashcat -m 110 hashes.txt wordlist.txt    # SHA-1 con salt
```

---

## Máscaras y Charsets

### Máscaras Predefinidas

```
?l = letras minúsculas
?u = letras mayúsculas
?d = dígitos
?s = símbolos
?a = todos los anteriores
?b = bytes 0x00-0xff
```

### Ejemplos

```bash
hashcat -m 0 -a 3 hashes.txt ?a?a?a?a?a?a?a?a
hashcat -m 0 -a 3 hashes.txt ?l?l?l?l?d?d?d?d
hashcat -m 0 -a 3 -1 ?l?d Password?1?1?1
```

---

## Reglas de Mutación

### Reglas Básicas

```bash
hashcat -m 0 -a 0 hashes.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule
hashcat -m 0 -a 0 hashes.txt wordlist.txt -r reglas1.rule -r reglas2.rule
```

### Reglas Personalizadas

```bash
:      # No cambio
c      # Capitalizar
u      # Mayúsculas
l      # Minúsculas
$1$2$3 # Agregar 123 al final
^Pass  # Agregar "Pass" al inicio
```

---

## Optimización de Rendimiento

### Configuración GPU

```bash
hashcat -m 0 -a 3 -d 1 hashes.txt ?a?a?a?a?a?a
hashcat -m 0 -a 3 -w 3 hashes.txt ?a?a?a?a?a?a
```

### Sesiones y Checkpoint

```bash
hashcat -m 0 -a 3 --session=misesion hashes.txt ?a?a?a?a?a?a
hashcat --restore --session=misesion
hashcat -m 0 -a 3 --restore-timer=60 hashes.txt ?a?a?a?a?a?a
```

---

## Utilidades de Hashcat

### Hashcat-utils

```bash
hashcat --stdout -a 3 ?l?l?l?l > candidates.txt
combinator wordlist1.txt wordlist2.txt > combined.txt
maskprocessor ?l?l?l?l | head -10
```

### Análisis de Hashes

```bash
hashcat --identify hash.txt
hashcat -b
```

---
