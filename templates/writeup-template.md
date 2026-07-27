# Plantilla de writeup

> Uso exclusivo para laboratorios, CTF, máquinas propias o entornos con autorización explícita.

# [Nombre de la máquina]

> **Plataforma:** [DockerLabs / HackTheBox / TryHackMe / Otra]  
> **Dificultad:** [Fácil / Media / Difícil]  
> **Sistema operativo:** [Linux / Windows]  
> **IP objetivo:** [IP]

---

## Resumen

Breve descripción del laboratorio indicando el vector de entrada y la técnica principal utilizada para conseguir privilegios.

Ejemplo:

> Máquina Linux donde se explota una mala configuración de SMB, credenciales débiles y un binario SUID vulnerable para obtener privilegios de root.

---

## Cadena de ataque

```text
Servicio expuesto
      |
      ↓
Vulnerabilidad / mala configuración
      |
      ↓
Acceso inicial
      |
      ↓
Escalada de privilegios
      |
      ↓
Root / Administrator
```

---

# Reconocimiento

## Descubrimiento de puertos

```bash
[comando utilizado]
```

Resultado:

[Captura]

### Servicios encontrados

| Puerto | Servicio | Versión | Observaciones |
|---|---|---|---|
| | | | |

---

# Enumeración

## [Servicio]

Comandos utilizados:

```bash
[comando]
```

Hallazgos:

- [Hallazgo importante]
- [Información obtenida]

Interpretación:

[Explicación breve de por qué este hallazgo es importante]

---

# Explotación

Explicación breve de la vulnerabilidad encontrada y cómo fue aprovechada.

```bash
[comando utilizado]
```

Resultado:

[Captura]

**Vector:** [Vulnerabilidad explotada]

**Resultado:** [Acceso obtenido]

---

# Acceso inicial

Usuario obtenido:

```text
[usuario]
```

Método de acceso:

[Explicación breve]

---

# Estabilización de shell

Si fue necesario mejorar la shell:

```bash
[comandos]
```

---

# Escalada de privilegios

Enumeración realizada:

```bash
[comandos]
```

Hallazgo:

[Explicación del fallo encontrado]

Explotación:

```bash
[comando]
```

Resultado:

[Captura]

**Vector:** [SUID / sudo / permisos / kernel / otro]

**Resultado:** root

---

# Caminos descartados

| Prueba | Resultado | Motivo |
|---|---|---|
| | | |

---

# Mitigaciones

| Hallazgo | Recomendación |
|---|---|
| | |

---

# Lecciones aprendidas

- [Técnica aprendida]
- [Error cometido]
- [Mejora para próximos laboratorios]

---

# Referencias

- [Recurso utilizado]
