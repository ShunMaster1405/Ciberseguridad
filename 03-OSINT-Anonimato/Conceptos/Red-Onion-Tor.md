## ¿Qué es Tor?

**Tor** (The Onion Router) es una red de comunicaciones anónimas que permite a los usuarios navegar por internet de forma privada y acceder a la Dark Web.

### Historia

- Origen: desarrollado por la Marina de EE.UU. en los años 90
- Propósito inicial: proteger comunicaciones militares
- Evolución: proyecto de código abierto desde 2006
- Financiamiento: apoyado por organizaciones de derechos humanos

---

## Arquitectura de Tor

### Principio de funcionamiento

```
Usuario → Nodo de Entrada → Nodo Intermedio → Nodo de Salida → Destino
```

### Capas de cifrado

1. Capa 1: cifrado del usuario al nodo de entrada
2. Capa 2: cifrado del nodo de entrada al intermedio
3. Capa 3: cifrado del nodo intermedio al de salida

### Tipos de nodos

- Nodos de Entrada (Entry/Guard): primer punto de conexión
- Nodos Intermedios (Middle): enrutan el tráfico
- Nodos de Salida (Exit): último punto antes del destino

---

## Servicios Ocultos (.onion)

### Características

- Dominio: terminan en `.onion`
- Acceso: solo a través de Tor
- Anonimato: servidor y usuario son anónimos
- Cifrado: extremo a extremo

### Ejemplos legítimos

- Facebook → `facebookcorewwwi.onion`
- ProPublica → `p53lf57qovyuvwsc6xnrppddxpr23otqjafxdnt8i.onion`
- DuckDuckGo → `3g2upl4pq6kufc4m.onion`

---

## Tor Browser

### Características

- Basado en Firefox, modificado para privacidad
- Configuración preestablecida optimizada para Tor
- Actualizaciones automáticas para mantener seguridad
- Extensiones limitadas para prevenir fingerprinting

### Configuraciones de seguridad

- Estándar: navegación normal con protección básica
- Más seguro: desactiva JavaScript en sitios no HTTPS
- Muy seguro: desactiva JavaScript completamente

---

