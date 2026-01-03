## Introducción a los Diccionarios de Contraseñas

Los diccionarios de contraseñas son listas compiladas de contraseñas comunes, palabras del diccionario y patrones utilizados en ataques de fuerza bruta y diccionario.

**Usos principales:**

- Auditorías de seguridad: evaluar la fortaleza de contraseñas organizacionales
- Pentesting: identificar vulnerabilidades en sistemas de autenticación
- Educación: demostrar la importancia de contraseñas seguras

---

## Tipos de Diccionarios

### Diccionarios Base

- Palabras del diccionario en diferentes idiomas
- Nombres propios (personas, lugares, marcas)
- Fechas significativas (años, cumpleaños, aniversarios)

### Diccionarios Especializados

- Contraseñas filtradas en brechas de seguridad
- Patrones específicos de dominios particulares
- Variaciones comunes (ejemplo: `@` por `a`, `3` por `e`)

---

## Herramientas para Crear Diccionarios

### CeWL (Custom Word List Generator)

```bash
cewl -w diccionario.txt -d 2 -m 5 https://ejemplo.com
# -w: archivo de salida
# -d: profundidad de crawling
# -m: longitud mínima de palabra
# -e: incluir direcciones de email
```

### Crunch

```bash
# Generar patrones específicos
crunch 8 8 -t ,,,,,@@@ -o diccionario.txt

# Crear diccionario con caracteres específicos
crunch 6 10 abcdefghijklmnopqrstuvwxyz0123456789 -o passwords.txt
```

---

## Técnicas de Generación

### Mutaciones de Palabras

```python
def generar_mutaciones(palabra):
    mutaciones = []
    sustituciones = {'a': '@', 'e': '3', 'i': '1', 'o': '0', 's': '$'}
    for original, nuevo in sustituciones.items():
        mutaciones.append(palabra.replace(original, nuevo))
    for i in range(100):
        mutaciones.append(palabra + str(i))
    return mutaciones
```

---
