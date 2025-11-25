## Introducción

**AES (Advanced Encryption Standard)** es un algoritmo de cifrado simétrico adoptado por el gobierno de Estados Unidos como estándar de cifrado.  
Reemplazó al DES y es ampliamente utilizado en todo el mundo.

---

## Características Técnicas

### Especificaciones

- Algoritmo: Rijndael
- Tipo: Cifrado de bloque simétrico
- Tamaño de bloque: 128 bits
- Tamaños de clave: 128, 192, 256 bits
- Número de rondas: 10, 12, 14 (según tamaño de clave)

### Operaciones Fundamentales

**1. SubBytes**

- Sustitución no lineal
- Utiliza la S-box
- Proporciona confusión

**2. ShiftRows**

- Desplazamiento cíclico de filas
- Proporciona difusión

**3. MixColumns**

- Transformación lineal de columnas
- Usa aritmética en campos finitos
- Aumenta la difusión

**4. AddRoundKey**

- XOR con la clave de ronda
- Incorpora la clave secreta
- Operación reversible

---

### Proceso de Cifrado AES

```text
AES-128:
1. Expansión de clave
2. Ronda inicial: AddRoundKey
3. 9 rondas principales:
   - SubBytes
   - ShiftRows
   - MixColumns
   - AddRoundKey
4. Ronda final:
   - SubBytes
   - ShiftRows
   - AddRoundKey
```

---

## Modos de Operación AES

### ECB (Electronic Codebook)

- Cada bloque se cifra independientemente
- Patrones visibles en datos similares
- No recomendado para uso general

### CBC (Cipher Block Chaining)

- Cada bloque se XOR con el anterior
- Requiere vector de inicialización (IV)
- Propaga errores

### CFB (Cipher Feedback)

- Convierte cifrado de bloque en flujo
- Permite cifrado de datos menores al bloque
- Propaga errores

### OFB (Output Feedback)

- Genera flujo de claves independiente
- No propaga errores
- Requiere IV único

### CTR (Counter)

- Utiliza contador para generar flujo
- Paralelizable
- Acceso aleatorio a datos

### GCM (Galois/Counter Mode)

- Cifrado autenticado
- Proporciona integridad y autenticación
- Altamente eficiente

---

## Implementación y Optimización

### Implementación por Software

```c
typedef struct {
    uint8_t state[4][4];
    uint8_t key[16];
    uint8_t round_keys[176];
} AES_ctx;

void AES_init(AES_ctx* ctx, const uint8_t* key);
void AES_encrypt(AES_ctx* ctx, uint8_t* data);
void AES_decrypt(AES_ctx* ctx, uint8_t* data);
```

### Optimización por Hardware

- Instrucciones AES-NI en procesadores Intel/AMD
- Aceleración significativa del rendimiento
- Implementaciones dedicadas en FPGA/ASIC

### Implementación Segura

- Protección contra ataques de canal lateral
- Tiempo de ejecución constante
- Gestión segura de claves

---

## Seguridad AES

### Resistencia a Ataques

- Criptoanálisis diferencial: resistente
- Criptoanálisis lineal: resistente
- Fuerza bruta: inviable
- Ataques de canal lateral: requieren mitigación

### Consideraciones de Seguridad

- Uso de claves de longitud adecuada
- Gestión segura de IV
- Protección de claves en memoria
- Validación de entrada

---

## Aplicaciones AES

### Estándares y Protocolos

- WPA2/WPA3 (seguridad inalámbrica)
- IPSec (seguridad de redes)
- SSL/TLS (comunicaciones web)
- SSH (acceso remoto seguro)

### Aplicaciones Comerciales

- Cifrado de discos duros
- Comunicaciones móviles
- Servicios en la nube
- Aplicaciones bancarias

---
