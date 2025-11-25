## Fundamentos del Hashing

### Propiedades de las Funciones Hash

1. Determinística: mismo input produce mismo output
2. Rápida: computación eficiente
3. Avalanche Effect: pequeños cambios causan grandes diferencias
4. Irreversible: no se puede obtener el input del output
5. Resistente a colisiones: difícil encontrar dos inputs con mismo hash

#### Ejemplo Práctico de Análisis

```python
import hashlib

def analyze_hash_properties(text):
    algorithms = ['md5', 'sha1', 'sha256', 'sha512']
    results = {}
    for algo in algorithms:
        hash_func = getattr(hashlib, algo)
        hash_value = hash_func(text.encode()).hexdigest()
        results[algo] = {
            'hash': hash_value,
            'length': len(hash_value),
            'bits': len(hash_value) * 4
        }
    return results
```

---

## Análisis de Entropía

### Medición de Entropía

```python
import math
from collections import Counter

def calculate_entropy(data):
    if not data:
        return 0
    counter = Counter(data)
    length = len(data)
    entropy = 0
    for count in counter.values():
        probability = count / length
        entropy -= probability * math.log2(probability)
    return entropy
```

---

## Algoritmos de Encriptación Simétrica

### AES (Advanced Encryption Standard)

```python
from cryptography.fernet import Fernet

def aes_encrypt_decrypt_example():
    key = Fernet.generate_key()
    cipher = Fernet(key)
    plaintext = b"Mensaje secreto"
    ciphertext = cipher.encrypt(plaintext)
    decrypted = cipher.decrypt(ciphertext)
    print(f"Texto original: {plaintext}")
    print(f"Texto encriptado: {ciphertext}")
    print(f"Texto desencriptado: {decrypted}")
```

### DES y Triple DES

```python
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.backends import default_backend
import os

def des_encryption_example():
    key = os.urandom(8)
    iv = os.urandom(8)
    cipher = Cipher(algorithms.TripleDES(key), modes.CBC(iv), backend=default_backend())
    encryptor = cipher.encryptor()
    plaintext = b"Texto de ejemplo para DES"
    pad_length = 8 - (len(plaintext) % 8)
    padded = plaintext + bytes([pad_length] * pad_length)
    ciphertext = encryptor.update(padded) + encryptor.finalize()
    return key, iv, ciphertext
```

---

## Modos de Operación

### ECB (Electronic Codebook)

- Cada bloque se encripta independientemente
- Patrones visibles en datos estructurados
- No recomendado para datos confidenciales

### CBC (Cipher Block Chaining)

- Cada bloque depende del anterior
- Requiere vector de inicialización (IV)
- Mejor que ECB, pero vulnerable a ciertos ataques

### GCM (Galois/Counter Mode)

- Encriptación autenticada
- Proporciona confidencialidad e integridad
- Recomendado para aplicaciones modernas

---

## Análisis de Debilidades

### Identificación de Patrones

```python
def detect_encryption_patterns(ciphertext):
    block_size = 16
    blocks = [ciphertext[i:i+block_size] for i in range(0, len(ciphertext), block_size)]
    unique_blocks = set(blocks)
    return {
        'repeated_blocks': len(blocks) - len(unique_blocks),
        'total_blocks': len(blocks),
        'uniqueness_ratio': len(unique_blocks) / len(blocks)
    }
```

### Análisis de Frecuencia

```python
def frequency_analysis(data):
    frequency = {}
    for byte in data:
        frequency[byte] = frequency.get(byte, 0) + 1
    expected = len(data) / 256
    chi_squared = sum((count - expected) ** 2 / expected for count in frequency.values())
    return {
        'frequency': frequency,
        'chi_squared': chi_squared,
        'randomness_score': chi_squared / len(data)
    }
```

---

## Herramientas de Análisis

### CyberChef

- Herramienta web para análisis y transformación de datos
- Funciones: decodificación, hash, encriptación

### Hashid

```bash
hashid -m hash.txt
hashid -m 5d41402abc4b2a76b9719d911017c592
```

### Hash-identifier

```bash
hash-identifier
```

---
