# Hydra Cheatsheet Profesional

## Descripción

**Hydra** es una herramienta extremadamente rápida y flexible para realizar ataques de fuerza bruta a diversos servicios de red. Permite atacar una variedad de protocolos y servicios como FTP, SSH, HTTP, IMAP, entre otros, utilizando listas de usuarios y contraseñas.

## Uso Básico

La estructura básica de un comando de **Hydra** es:

```bash
hydra [opciones] [servicio]://[host]
```

- `-l [usuario]`: Define un solo nombre de usuario.
- `-L [lista de usuarios]`: Usa una lista de nombres de usuarios.
- `-p [contraseña]`: Define una sola contraseña.
- `-P [lista de contraseñas]`: Usa una lista de contraseñas.
- `-M [lista de hosts]`: Especifica una lista de múltiples objetivos.
- `-s [puerto]`: Especifica un puerto personalizado (opcional si no es el predeterminado del servicio).
- `-t [número de hilos]`: Define el número de hilos (máximo de conexiones paralelas).
- `-o [archivo.txt]`: Especifica el nombre del archivo donde se guardarán los resultados.

---

## Opciones Comunes

| Opción        | Descripción                                             |
|---------------|--------------------------------------------------------|
| `-l`          | Nombre de usuario único.                               |
| `-L`          | Lista de nombres de usuario.                           |
| `-p`          | Contraseña única.                                      |
| `-P`          | Lista de contraseñas.                                  |
| `-M`          | Lista de múltiples objetivos.                          |
| `-s`          | Puerto específico (si es distinto al predeterminado).  |
| `-t`          | Número de hilos (conexiones paralelas).                |
| `-v / -V / -d`| Verbosidad (-v: verboso, -V: muy verboso, -d: debug). |
| `-o`          | Guardar los resultados en un archivo.                  |
| `-f`          | Detenerse cuando se encuentre la primera contraseña válida. |
| `-6`          | Habilitar ataques sobre IPv6.                          |
| `-C`          | Especifica un archivo con combinaciones `usuario:contraseña`. |

---

## Protocolos Soportados

**Hydra** puede atacar una variedad de servicios como:

- `ftp`
- `ssh`
- `telnet`
- `smtp`
- `http-get` / `http-post`
- `imap`
- `pop3`
- `smb`
- `vnc`
- `ldap`
- `rdp`
- `mssql`
- `mysql`
- `postgres`
- `snmp`
- `redis`
- `sip`
- Y muchos más.

---

## Ejemplos Comunes

### 1. **Ataque FTP con un usuario y lista de contraseñas**

```bash
hydra -l user -P passlist.txt ftp://192.168.0.1 -o resultados_ftp.txt
```

- Ataca un servidor FTP en la IP `192.168.0.1` utilizando el usuario `user` y la lista de contraseñas `passlist.txt`, guardando los resultados en `resultados_ftp.txt`.

### 2. **Ataque IMAP con lista de usuarios y contraseña predeterminada**

```bash
hydra -L userlist.txt -p defaultpw imap://192.168.0.1/PLAIN -o resultados_imap.txt
```

- Usa una lista de usuarios (`userlist.txt`) con la contraseña `defaultpw` para un ataque IMAP a la IP `192.168.0.1`, guardando los resultados en `resultados_imap.txt`.

### 3. **Ataque POP3 seguro con archivo de combinaciones de usuario:contraseña y soporte IPv6**

```bash
hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5 -o resultados_pop3.txt
```

- Ataca un servidor POP3S en la dirección IPv6 `[2001:db8::1]`, puerto `143`, utilizando combinaciones de usuario y contraseña desde el archivo `defaults.txt`, guardando los resultados en `resultados_pop3.txt`.

### 4. **Escaneo de subred para FTP con un usuario y contraseña específicos**

```bash
hydra -l admin -p password ftp://[192.168.0.0/24]/ -o resultados_subred.txt
```

- Escanea todas las direcciones dentro del rango `192.168.0.0/24` (subred local) usando el usuario `admin` y la contraseña `password` para buscar servicios FTP, guardando los resultados en `resultados_subred.txt`.

### 5. **Ataque SSH contra múltiples objetivos con listas de usuarios y contraseñas**

```bash
hydra -L logins.txt -P pws.txt -M targets.txt ssh -o resultados_ssh.txt
```

- Utiliza `logins.txt` para usuarios, `pws.txt` para contraseñas, y `targets.txt` para especificar múltiples IPs o dominios a atacar a través de SSH, guardando los resultados en `resultados_ssh.txt`.

### 6. **Ataque HTTP POST con lista de usuarios y contraseñas**

```bash
hydra -L users.txt -P pass.txt http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect" -t 64 -v -o resultados_http.txt
```

- Realiza un ataque de fuerza bruta a un formulario de login en un sitio web. Usa `users.txt` y `pass.txt` como listas de usuarios y contraseñas. Se busca el mensaje `incorrect` para determinar si el intento falló, guardando los resultados en `resultados_http.txt`.

### 7. **Ataque HTTP GET a una página protegida con autenticación básica**

```bash
hydra -L users.txt -P pass.txt http-get://example.com/protected -o resultados_http_get.txt
```

- Ataque de fuerza bruta sobre una página protegida con autenticación básica en `http-get` con listas de usuarios y contraseñas, guardando los resultados en `resultados_http_get.txt`.

### 8. **Fuerza bruta RDP (Escritorio Remoto)**

```bash
hydra -t 1 -V -f -L users.txt -P passlist.txt rdp://192.168.1.100 -o resultados_rdp.txt
```

- Ataca el servicio de Escritorio Remoto (RDP) en `192.168.1.100` utilizando listas de usuarios y contraseñas, con un solo hilo (`-t 1`) para evitar ser bloqueado rápidamente, guardando los resultados en `resultados_rdp.txt`.

### 9. **Atacando múltiples servicios a la vez**

```bash
hydra -L users.txt -P passlist.txt ftp://192.168.1.10 ssh://192.168.1.11 rdp://192.168.1.12 -o resultados_multi.txt
```

- Ataca múltiples servicios (FTP, SSH, RDP) en diferentes hosts con las mismas listas de usuarios y contraseñas, guardando los resultados en `resultados_multi.txt`.

### 10. **Ataque SSH con rockyou.txt**

```bash
hydra -L users.txt -P /usr/share/wordlists/rockyou.txt 1010.137.76 ssh -o resultados_rockyou.txt
```

- Utiliza una lista de usuarios (`users.txt`) y la famosa wordlist `rockyou.txt` para realizar un ataque de fuerza bruta SSH contra el host `1010.137.76`, guardando los resultados en `resultados_rockyou.txt`.

---

## Consejos Adicionales

- **Hilos y rendimiento:** Ajusta el número de hilos con `-t`. Un valor demasiado alto puede resultar en bloqueos o en la denegación del servicio en el servidor.
  
- **Detener en el primer éxito:** Usa `-f` para que Hydra se detenga después de encontrar una combinación válida de usuario y contraseña.

- **Guardar resultados:** Utiliza `-o resultado.txt` para guardar los resultados exitosos en un archivo de texto.

---

## Fuentes de Documentación

Para más información sobre opciones y ejemplos específicos, consulta la documentación oficial o utiliza el comando:

```bash
hydra -h
```
