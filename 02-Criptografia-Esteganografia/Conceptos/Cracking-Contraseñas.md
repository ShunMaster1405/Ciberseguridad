## Conceptos Fundamentales

### Definición

El cracking de contraseñas es el proceso de recuperar contraseñas mediante diversos métodos computacionales, aprovechando debilidades en algoritmos de hash o mediante fuerza bruta.

---

## Tipos de Ataques

### Ataque de Diccionario

- Utiliza listas predefinidas de contraseñas comunes
- Rápido para contraseñas comunes
- Inefectivo contra contraseñas únicas

### Ataque de Fuerza Bruta

- Prueba todas las combinaciones posibles
- Garantiza encontrar la contraseña eventualmente
- Tiempo exponencial según la longitud
- Computacionalmente intensivo

### Ataque Híbrido

- Combina diccionario con modificaciones
- Técnicas: añadir números, capitalizar primera letra, reemplazar caracteres (l33t speak)

### Rainbow Tables

- Tablas precomputadas de hashes
- Intercambia espacio de almacenamiento por tiempo
- Inefectivo contra hashes con salt

---

## Factores que Afectan la Velocidad

### Algoritmo de Hash

- Rápidos: MD5, SHA1, NTLM
- Lentos: bcrypt, scrypt, Argon2
- Ejemplo de velocidades:
    - MD5: 50+ billion/sec
    - bcrypt: 50,000/sec

### Hardware

- CPU: múltiples núcleos para paralelización
- GPU: masivamente paralelo para ciertos algoritmos
- RAM: afecta el tamaño de diccionarios cargados

### Optimizaciones

- Reglas de mutación
- Máscaras de patrones
- Distribución en clusters

---

## Complejidad de Contraseñas

### Entropía

Fórmula:  
[ E = \log_2(R^L) ]

- R = rango de caracteres
- L = longitud de contraseña

Ejemplo:

- 8 caracteres alfanuméricos: 47.6 bits
- 12 caracteres con símbolos: 79.2 bits

### Tiempo de Cracking Estimado

```
Tiempo = (R^L) / (2 * velocidad_hash)
```

---

## Técnicas de Defensa

### Password Stretching

- Propósito: hacer más lento el proceso de hash
- Implementaciones: PBKDF2, bcrypt, scrypt, Argon2

### Salt

- Función: prevenir ataques rainbow table
- Implementación: valor aleatorio concatenado con contraseña
- Ejemplo:

```
hash = SHA256(password + salt)
```

---
