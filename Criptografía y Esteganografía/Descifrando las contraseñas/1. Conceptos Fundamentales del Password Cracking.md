## ¿Qué es el Password Cracking?

El **password cracking** es el proceso de recuperar contraseñas desde datos almacenados o transmitidos por un sistema informático.  
Este proceso puede ser realizado por administradores legítimos que han olvidado sus contraseñas o por atacantes maliciosos que buscan acceso no autorizado.

---

## Tipos de Ataques de Contraseñas

### Ataque de Diccionario

- Utiliza una lista predefinida de contraseñas comunes
- Rápido para contraseñas débiles
- Limitado a contraseñas en el diccionario

### Ataque de Fuerza Bruta

- Prueba todas las combinaciones posibles
- Garantiza encontrar la contraseña eventualmente
- Extremadamente lento para contraseñas largas

### Ataque Híbrido

- Combina diccionario con mutaciones
- Ejemplo: `"password"` → `"password123"`, `"Password!"`

### Ataque de Máscara

- Utiliza patrones conocidos
- Ejemplo: `?u?l?l?l?l?d?d?d` (una mayúscula, 4 minúsculas, 3 dígitos)

---

## Tipos de Hashes Comunes

### Hashes de Sistema

- **MD5**: rápido pero inseguro
- **SHA-1**: comprometido, no recomendado
- **SHA-256/SHA-512**: más seguros pero sin salt

### Hashes de Contraseñas

- **bcrypt**: adaptativo, muy seguro
- **scrypt**: resistente a hardware especializado
- **PBKDF2**: estándar, configurable

### Hashes de Sistemas Operativos

- **NTLM**: Windows (vulnerable)
- **LM**: Windows legacy (muy vulnerable)
- **Unix DES**: sistemas Unix antiguos

---

