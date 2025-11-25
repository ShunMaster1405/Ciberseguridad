## Introducción a Certificados Digitales

### Definición

Un certificado digital es un documento electrónico que utiliza criptografía de clave pública para verificar la identidad de una entidad y establecer comunicaciones seguras.

### Propósito Principal

- Autenticación
- Integridad
- No repudio
- Confidencialidad

---

## Estructura de un Certificado X.509

### Componentes Principales

Ejemplo de certificado:

```
Version: 3
Serial Number: 12345678
Signature Algorithm: sha256WithRSAEncryption
Issuer: DigiCert SHA2 Secure Server CA
Validity: Not Before 2024, Not After 2025
Subject: Example Corp, CN=www.example.com
Public Key: RSA 2048 bits
Extensions: Subject Alternative Name (SAN)
```

---

## Campos Importantes

### Issuer (Emisor)

Identifica la Autoridad de Certificación (CA).

### Subject (Sujeto)

Identifica al propietario del certificado.

### Validity (Validez)

Fechas de inicio y expiración.

### Public Key (Clave Pública)

Algoritmos comunes: RSA, ECDSA, DSA.

---

## Autoridades de Certificación (CA)

### Root CA

- Autofirmada
- Almacenada en trust stores

### Intermediate CA

- Firmada por Root CA
- Mayor seguridad

### Issuing CA

- Emite certificados de usuario final

### Cadena de Certificación

```
Root CA
 └── Intermediate CA
      └── End Entity Certificate
```

---

## Tipos de Certificados

### Por Validación

- DV: validación de dominio
- OV: validación de dominio + organización
- EV: validación exhaustiva

### Por Cobertura

- Single Domain
- Wildcard
- Multi-Domain (SAN)

---

## Proceso de Emisión

### Generación de Claves

```bash
openssl genrsa -out private.key 2048
openssl ecparam -genkey -name secp256r1 -out private.key
```

### CSR (Certificate Signing Request)

```bash
openssl req -new -key private.key -out request.csr
```

---

## Revocación de Certificados

### CRL

Lista de certificados revocados.

### OCSP

Verificación en tiempo real.

### OCSP Stapling

Respuesta OCSP adjunta por el servidor.

---

## Gestión de Certificados

### Almacenamiento Seguro

- Claves privadas nunca compartidas
- Permisos restringidos
- Backups encriptados

### Monitoreo

- Alertas de expiración
- Verificación de revocación
- Renovación automatizada

### Herramientas

```bash
openssl x509 -in certificate.crt -text -noout
openssl verify -CAfile ca-bundle.crt certificate.crt
openssl s_client -connect example.com:443 -servername example.com
```

---

## Aplicaciones Prácticas

### SSL/TLS

Cifrado de comunicaciones web.

### Code Signing

Firmar software para verificar integridad.

### Email Security

S/MIME y PGP para correos electrónicos.

---

## Seguridad y Mejores Prácticas

- Usar HSM para claves privadas
- Algoritmos fuertes y claves ≥ 2048 bits
- TLS 1.2+ únicamente
- Certificate Transparency y auditorías periódicas

---
