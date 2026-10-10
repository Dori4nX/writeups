# TryHackMe

Laboratorios realizados en TryHackMe.

Cada máquina incluye un writeup con los hallazgos, los aprendizajes y las medidas de seguridad relacionadas.

---

# Máquinas

---

## 🔴 Internal

**Sistema:** Linux<br>
**Dificultad:** Difícil

**Técnicas y conceptos:**

- RCE autenticada editando `footer.php` en WordPress (reverse shell)
- Pivoting a Jenkins interno con Chisel
- RCE con Groovy en la Script Console de Jenkins
- Escalada a root mediante credenciales expuestas

[➡️ Ver writeup](Internal/Internal.md)

---
## 🟡 Mr Robot CTF

**Sistema:** Linux<br>
**Dificultad:** Media

**Técnicas y conceptos:**

- Enumeración con Gobuster y credenciales expuestas en `license.txt`
- RCE autenticada editando `footer.php` en WordPress (reverse shell)
- Crackeo del hash MD5 con John the Ripper
- Escalada de privilegios mediante Nmap con SUID

[➡️ Ver writeup](MrRobotCTF/Mr%20Robot%20CTF.md)

---
