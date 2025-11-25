## Introducción al Ataque de Hashes

El proceso de "romper" un hash consiste en encontrar el valor original (plaintext) que produce un hash específico.  
Este proceso es fundamental en la auditoría de seguridad y el análisis forense.

---

## Tipos de Ataques de Hash

### Ataques de Fuerza Bruta

- Concepto: probar todas las combinaciones posibles
- Ventaja: garantía de éxito eventual
- Desventaja: tiempo computacional extremo

```python
import hashlib, itertools, string

def brute_force_hash(target_hash, max_length=4):
    charset = string.ascii_lowercase + string.digits
    for length in range(1, max_length + 1):
        for attempt in itertools.product(charset, repeat=length):
            password = ''.join(attempt)
            if hashlib.md5(password.encode()).hexdigest() == target_hash:
                return password
    return None
```

---

### Ataques de Diccionario

- Concepto: usar listas de contraseñas comunes
- Ventaja: más rápido que fuerza bruta
- Limitación: solo funciona con contraseñas conocidas

```python
def dictionary_attack(target_hash, dictionary_file):
    with open(dictionary_file, 'r') as f:
        for password in f:
            password = password.strip()
            if hashlib.sha256(password.encode()).hexdigest() == target_hash:
                return password
    return None
```

---

### Ataques Rainbow Tables

- Concepto: tablas precomputadas hash-valor
- Ventaja: intercambio espacio-tiempo
- Desventaja: requiere almacenamiento masivo

---

## Herramientas de Cracking

### Hashcat

```bash
hashcat -m 0 -a 0 hash.txt rockyou.txt
hashcat -m 0 -a 3 hash.txt ?l?l?l?l?d?d?d?d
hashcat -m 0 -a 6 hash.txt rockyou.txt ?d?d?d?d
```

### John the Ripper

```bash
john --wordlist=rockyou.txt hash.txt
john --wordlist=rockyou.txt --rules hash.txt
john --show hash.txt
```

### CrackStation

- Servicio online
- Base de datos con millones de hashes precomputados
- Limitación: dependiente de su base de datos

---

## Algoritmos de Hash Vulnerables

### MD5

- Vulnerabilidad: colisiones conocidas
- Cracking rápido
- Recomendación: no usar para seguridad

```python
import hashlib
def md5_collision_example():
    text1, text2 = "collision1", "collision2"
    hash1 = hashlib.md5(text1.encode()).hexdigest()
    hash2 = hashlib.md5(text2.encode()).hexdigest()
    print(f"{text1} -> {hash1}")
    print(f"{text2} -> {hash2}")
```

### SHA-1

- Estado: criptográficamente roto
- Colisiones demostradas en 2017
- Uso: siendo eliminado gradualmente

### SHA-256

- Estado: actualmente seguro
- Resistencia: no se conocen ataques prácticos
- Uso: ampliamente recomendado

---

## Defensas contra Ataques de Hash

### Salting

```python
import hashlib, os
def hash_with_salt(password):
    salt = os.urandom(32)
    password_hash = hashlib.pbkdf2_hmac('sha256', password.encode('utf-8'), salt, 100000)
    return salt + password_hash
```

### Key Stretching

- Concepto: aumentar el tiempo de cómputo
- Implementación: múltiples iteraciones
- Algoritmos: PBKDF2, bcrypt, scrypt, Argon2

### Pepper

- Concepto: clave secreta adicional
- Almacenamiento: separado de la base de datos
- Beneficio: protección adicional contra dumps de BD

---
