# Nombre de la máquina

> **Plataforma:**\
> &#x20;**Dificultad:**\
> &#x20;**Sistema operativo:**\
> &#x20;**IP objetivo:** &#x20;

## Resumen

Breve explicación de la máquina, el punto de entrada y la escalada de privilegios.

## Cadena de ataque
```text
Servicio expuesto
    ↓
Vulnerabilidad o mala configuración
    ↓
Acceso como usuario
    ↓
Escalada de privilegios
    ↓
root / SYSTEM

```

## Reconocimiento
```bash
nmap -p- --open -sS --min-rate 5000 -n -Pn <IP> -oG allPorts
nmap -sCV -p<PUERTOS> <IP> -oN targeted

```

| Puerto | Servicio | Versión | Hallazgo |
| ------ | -------- | ------- | -------- |
|        |          |         |          |

## Enumeración
```bash
# Comandos principales utilizados

```

**Hallazgo importante:**

Explica qué encontraste y por qué decidiste investigarlo.

## Explotación
```bash
# Payload, petición o exploit utilizado

```

**Resultado:** acceso obtenido como `<usuario>`.

## Escalada de privilegios
```bash
# Enumeración y comandos principales

```

**Vector:** explica brevemente la configuración vulnerable.

**Resultado:** acceso obtenido como `root` o `SYSTEM`.

## Cadena final
```text
<servicio> → <vulnerabilidad> → <shell> → <escalada> → root/SYSTEM

```

## Aprendizajes

- Técnica nueva aprendida.\
  &#x20;
- Error o bloqueo encontrado.\
  &#x20;
- Qué haría más rápido la próxima vez.\
  &#x20;

## Mitigaciones

- Medida defensiva principal.\
  &#x20;
- Corrección de la mala configuración.\
  &#x20;
- Recomendación adicional.
