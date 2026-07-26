# Plantilla de writeup

Esta plantilla sirve como guía para documentar máquinas y laboratorios de forma consistente. Debe utilizarse únicamente con CTF, máquinas propias o sistemas para los que exista autorización explícita.

> **Publicación responsable:** sustituye los campos entre corchetes, elimina las secciones que no sean necesarias y no incluyas flags, credenciales reales, tokens ni otros datos sensibles.

## Información de la máquina

| Campo | Valor |
| --- | --- |
| Máquina | `[Nombre]` |
| Plataforma | `[Plataforma]` |
| Sistema operativo | `[Linux / Windows / Otro]` |
| Dificultad | `[Fácil / Media / Difícil / Sin clasificar]` |
| Fecha de realización | `[AAAA-MM-DD]` |
| Estado | `[Completada / En revisión]` |

## Resumen

Describe brevemente el objetivo del laboratorio, el punto de entrada y la vía de escalada de privilegios. Evita adelantar detalles innecesarios y no incluyas información sensible.

## Cadena de ataque

Resume el recorrido completo en pasos:

1. `[Descubrimiento principal]`
2. `[Vector de acceso inicial]`
3. `[Enumeración interna relevante]`
4. `[Vía de escalada de privilegios]`

## Reconocimiento

Documenta el alcance autorizado, el descubrimiento del objetivo y los comandos relevantes. Incluye solo la salida necesaria y elimina datos sensibles.

```text
[Comando o evidencia relevante]
```

### Tabla de puertos

| Puerto | Protocolo | Servicio | Versión | Observaciones |
| --- | --- | --- | --- | --- |

## Hipótesis iniciales

| Hipótesis | Evidencia | Estado |
| --- | --- | --- |
| `[Posible vector]` | `[Indicio observado]` | `[Pendiente / Confirmada / Descartada]` |

Explica qué líneas de investigación parecen más prometedoras y por qué.

## Enumeración por servicios

### `[Servicio y puerto]`

Documenta:

- Herramientas y comandos utilizados.
- Hallazgos relevantes.
- Interpretación de los resultados.
- Siguiente acción razonada.

Repite este bloque para cada servicio que requiera análisis.

## Explotación

Explica la vulnerabilidad o configuración insegura identificada, los requisitos previos y la forma en que se validó dentro del laboratorio. Distingue con claridad los hechos observados de las hipótesis.

```text
[Prueba o comando sanitizado]
```

## Acceso inicial

Describe cómo se obtuvo el primer acceso, con qué nivel de privilegios y qué evidencia confirmó el resultado. No publiques credenciales, tokens ni flags.

## Estabilización de shell

Indica si fue necesario mejorar la sesión y documenta únicamente los pasos aplicados en el entorno autorizado.

```text
[Comandos utilizados, si procede]
```

## Enumeración interna

Recoge la información relevante obtenida tras el acceso inicial:

- Usuario y grupos.
- Servicios y procesos.
- Permisos y configuraciones.
- Tareas programadas.
- Interfaces y rutas de red.
- Archivos relevantes, siempre sin exponer datos sensibles.

## Escalada de privilegios

Explica el hallazgo, cómo se comprobó y por qué permitió elevar privilegios. Incluye la evidencia mínima necesaria para que el proceso sea reproducible en el laboratorio.

## Caminos descartados

Documenta las pruebas que no funcionaron y el motivo por el que se abandonaron. Esta sección ayuda a conservar el razonamiento y evita repetir intentos sin fundamento.

| Camino | Resultado | Motivo para descartarlo |
| --- | --- | --- |
| `[Prueba realizada]` | `[Resultado]` | `[Conclusión]` |

## Mitigaciones

| Hallazgo | Riesgo | Recomendación |
| --- | --- | --- |
| `[Vulnerabilidad o configuración]` | `[Impacto]` | `[Medida correctiva]` |

Prioriza recomendaciones concretas, realistas y relacionadas con los hallazgos documentados.

## Lecciones aprendidas

- `[Conocimiento consolidado]`
- `[Error o dificultad relevante]`
- `[Mejora para próximos laboratorios]`

## Referencias

- `[Título del recurso](https://example.com)`

Utiliza fuentes oficiales o técnicas fiables y elimina cualquier referencia que no se haya consultado realmente.

## Checklist antes de publicar

- [ ] La práctica procede de un laboratorio, CTF, máquina propia o sistema con autorización explícita.
- [ ] La máquina está completada y los pasos descritos han sido verificados.
- [ ] No se incluyen flags, credenciales reales, tokens, claves ni datos personales.
- [ ] Las direcciones, dominios, capturas y salidas se han revisado y sanitizado cuando es necesario.
- [ ] Se distingue entre hechos, hipótesis y caminos descartados.
- [ ] Los comandos y fragmentos son legibles y tienen contexto suficiente.
- [ ] Todos los enlaces relativos y referencias funcionan.
- [ ] Las tablas y los bloques de código se renderizan correctamente.
- [ ] El texto mantiene un tono profesional y no exagera los conocimientos demostrados.

---

## Versión rápida para máquinas sencillas

Usa esta versión cuando el recorrido sea corto y no necesite todas las secciones anteriores.

### Información

| Campo | Valor |
| --- | --- |
| Máquina | `[Nombre]` |
| Plataforma | `[Plataforma]` |
| Sistema operativo | `[Sistema operativo]` |
| Dificultad | `[Dificultad]` |

### Resumen

`[Objetivo y recorrido en dos o tres frases]`

### Reconocimiento

| Puerto | Servicio | Observaciones |
| --- | --- | --- |

```text
[Comandos y resultados relevantes]
```

### Acceso inicial

`[Vector utilizado y evidencia del acceso]`

### Escalada de privilegios

`[Hallazgo y procedimiento verificado]`

### Mitigaciones

- `[Recomendación principal]`

### Lecciones aprendidas

- `[Aprendizaje principal]`

### Referencias

- `[Recurso consultado](https://example.com)`

Antes de publicar esta versión, aplica el mismo checklist de seguridad y calidad indicado en la plantilla completa.
