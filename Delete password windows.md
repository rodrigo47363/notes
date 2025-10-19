# 🔐 Windows Local User Password Recovery Guide

![Windows](https://img.shields.io/badge/Windows-0078D6?logo=windows\&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?logo=kalilinux\&logoColor=white)
[![Parrot OS](https://img.shields.io/badge/Parrot_OS-4DBCE9?style=for-the-badge\&logo=parrotos\&logoColor=white)](https://www.parrotsec.org/)
![Security](https://img.shields.io/badge/Security-Professional-orange)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 🌐 Connect With Me

<div align="center">

[![YouTube](https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge\&logo=YouTube\&logoColor=white)](https://youtube.com/@Rodrigo-47363?sub_confirmation=1)
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge\&logo=linkedin\&logoColor=white)](https://linkedin.com/in/rodrigo-v-695728215)
[![HackTheBox](https://img.shields.io/badge/HackTheBox-9FEF00?style=for-the-badge\&logo=hackthebox\&logoColor=black)](https://app.hackthebox.com/profile/2072477)
[![TryHackMe](https://img.shields.io/badge/TryHackMe-212C42?style=for-the-badge\&logo=tryhackme\&logoColor=white)](https://tryhackme.com/p/Rodrigo.47363)
[![ProtonMail](https://img.shields.io/badge/Email-8B89CC?style=for-the-badge\&logo=protonmail\&logoColor=white)](mailto:rodrigovil@proton.me)

</div>

---

## 🔗 Referral Links

[![HackTheBox Referral](https://img.shields.io/badge/Join_HackTheBox-9FEF00?style=for-the-badge\&logo=hackthebox\&logoColor=black)](https://referral.hackthebox.com/mz7ZtlJ)
[![TryHackMe Referral](https://img.shields.io/badge/Join_TryHackMe-212C42?style=for-the-badge\&logo=tryhackme\&logoColor=white)](https://tryhackme.com/signup?referrer=64f0d7665fde58f3ec71379b)

Perfecto, Rodrigo. Para que la sección de **“Support My Work”** se vea más profesional y ordenada en GitHub, podemos mejorar la estructura usando **tarjetas alineadas y centradas**, con íconos y etiquetas claras. También podemos separar los links de dirección de la billetera en un bloque limpio debajo para que no se mezcle con los botones. Aquí te dejo una versión pulida:

---

## 💖 Support My Work

<div align="center">

[![Bitcoin](https://img.shields.io/badge/Bitcoin-F7931A?style=for-the-badge\&logo=bitcoin\&logoColor=white)](bitcoin:bc1qkzmpd0hry99qms7ef23vsyx9vt34pzzaslpp8y)
[![Ethereum](https://img.shields.io/badge/Ethereum-3C3C3D?style=for-the-badge\&logo=ethereum\&logoColor=white)](https://etherscan.io/address/0xB75bC57C54FCBFF139EBF981A596B019C537d018)
[![Solana](https://img.shields.io/badge/Solana-9945FF?style=for-the-badge\&logo=solana\&logoColor=white)](https://solscan.io/address/ELekuGHcmZjhXrtHNqHuu8QmdCZr3oCWtTmu3QUQ5hac)

</div>

<div align="center">

### Wallet Addresses

```text
BTC:  bc1qkzmpd0hry99qms7ef23vsyx9vt34pzzaslpp8y
ETH:  0xB75bC57C54FCBFF139EBF981A596B019C537d018
SOL:  ELekuGHcmZjhXrtHNqHuu8QmdCZr3oCWtTmu3QUQ5hac
```

</div>

---

# 🇺🇸 English Version

## 📌 Table of Contents

* [Professional Guide](#-professional-guide-windows-local-user-password-removal)
* [Method Comparison](#-method-comparison-table)
* Methods

  * [CMD](#1-using-cmd-from-windows)
  * [chntpw](#2-using-chntpw-on-kali-or-parrot-os)
  * [Hiren's BootCD](#3-using-hirens-bootcd-pe)
* [Legal and Ethical Considerations](#-legal-and-ethical-considerations)
* [FAQ](#-frequently-asked-questions)

---

## 🔐 Professional Guide: Windows Local User Password Removal

This repository documents three effective methods to remove or modify local user passwords in Windows systems. Designed for IT technicians, cybersecurity students, and access recovery professionals.
**⚠️ All procedures require legal authorization and proper permissions.**

### 📋 Method Comparison Table

| Method             | Windows 10/11 | Microsoft Accounts | BitLocker                | Admin Rights Required |
| ------------------ | ------------- | ------------------ | ------------------------ | --------------------- |
| **CMD**            | ✅             | ❌                  | N/A                      | ✅                     |
| **chntpw**         | ✅             | ❌                  | ❌                        | ❌                     |
| **Hiren's BootCD** | ✅             | ❌                  | ⚠️ Requires Recovery Key | ❌                     |

---

### 🛠️ Methods

#### 1. Using CMD from Windows

**Requirements:** Administrator access.

**Steps:**

1. Open CMD as administrator (`Win + X` → "Command Prompt (Admin)")
2. List users: `net user`
3. Remove password: `net user username ""`
4. Or set new password: `net user username new_password`
5. Log off and verify access

**Advantages:** Quick and straightforward
**Limitations:** Requires existing administrator access

#### 2. Using chntpw on Kali or Parrot OS

**Requirements:** Bootable USB with Kali Linux or Parrot OS; physical access.

**Steps:**

1. Boot from live USB
2. Mount Windows partition: `sudo mount /dev/sdXn /mnt/windows`
3. Change directory: `cd /mnt/windows/Windows/System32/config`
4. List users: `sudo chntpw -l SAM`
5. Modify user: `sudo chntpw -u username SAM`
6. Select action (`1` clear password, `2` unlock, `3` promote admin)
7. Save changes (`q` then `y`) and reboot

**Advantages:** No pre-existing system access required
**Limitations:** Incompatible with Microsoft accounts and BitLocker

#### 3. Using Hiren's BootCD PE

**Requirements:** Bootable USB with [Hiren's BootCD PE](https://www.hirensbootcd.org); physical access.

**Steps:**

1. Create USB with Rufus
2. Boot computer from USB
3. Launch **NT Password Edit**
4. Load SAM file: `C:\Windows\System32\config\SAM`
5. Select user → "Change Password" → leave blank → "Save Changes"
6. Reboot and verify access

**Advantages:** User-friendly interface
**Limitations:** USB preparation required

---

### ⚠️ Legal and Ethical Considerations

> For educational and authorized recovery purposes only.
> Unauthorized use may violate local or international laws.

### ❓ Frequently Asked Questions

* **Q:** Does this work with Microsoft accounts?
  **A:** No, only local accounts.
* **Q:** What if BitLocker is enabled?
  **A:** You need the recovery key.
* **Q:** Are these changes detectable?
  **A:** Yes, logs may record activity. Document all actions.

---

# 🇪🇸 Versión en Español

## 📌 Tabla de Contenido

* [Guía Profesional](#-guía-profesional-eliminación-de-contraseñas-de-usuario-local-en-windows)
* [Comparativa de Métodos](#-tabla-comparativa-de-métodos)
* Métodos

  * [CMD](#1-usando-cmd-desde-windows)
  * [chntpw](#2-usando-chntpw-en-kali-o-parrot-os)
  * [Hiren's BootCD](#3-usando-hirens-bootcd-pe)
* [Consideraciones Legales](#-consideraciones-legales-y-éticas)
* [Preguntas Frecuentes](#-preguntas-frecuentes)

---

## 🔐 Guía Profesional: Eliminación de Contraseñas de Usuario Local en Windows

Este repositorio documenta tres métodos efectivos para eliminar o modificar contraseñas de usuarios locales en sistemas Windows. Orientado a técnicos de IT, estudiantes de ciberseguridad y profesionales en recuperación de acceso.
**⚠️ Todos los procedimientos requieren autorización legal y permisos adecuados.**

### 📋 Tabla Comparativa de Métodos

| Método             | Windows 10/11 | Cuentas Microsoft | BitLocker                 | Requiere Derechos Admin |
| ------------------ | ------------- | ----------------- | ------------------------- | ----------------------- |
| **CMD**            | ✅             | ❌                 | N/A                       | ✅                       |
| **chntpw**         | ✅             | ❌                 | ❌                         | ❌                       |
| **Hiren's BootCD** | ✅             | ❌                 | ⚠️ Con Clave Recuperación | ❌                       |

---

### 🛠️ Métodos

#### 1. Usando CMD desde Windows

**Requisitos:** Acceso como administrador.

**Pasos:**

1. Abrir CMD como administrador (`Win + X` → "Símbolo del sistema (Administrador)")
2. Listar usuarios: `net user`
3. Eliminar contraseña: `net user nombre_usuario ""`
4. O asignar nueva contraseña: `net user nombre_usuario nueva_contraseña`
5. Cerrar sesión y verificar acceso

**Ventajas:** Rápido y directo
**Limitaciones:** Requiere acceso previo como administrador

#### 2. Usando chntpw en Kali o Parrot OS

**Requisitos:** USB booteable con Kali Linux o Parrot OS; acceso físico.

**Pasos:**

1. Iniciar desde USB live
2. Montar partición de Windows: `sudo mount /dev/sdXn /mnt/windows`
3. Cambiar directorio: `cd /mnt/windows/Windows/System32/config`
4. Listar usuarios: `sudo chntpw -l SAM`
5. Modificar usuario: `sudo chntpw -u nombre_usuario SAM`
6. Seleccionar acción (`1` eliminar contraseña, `2` desbloquear, `3` promover admin)
7. Guardar cambios (`q` luego `y`) y reiniciar

**Ventajas:** No requiere acceso previo al sistema
**Limitaciones:** Incompatible con cuentas Microsoft y BitLocker

#### 3. Usando Hiren's BootCD PE

**Requisitos:** USB booteable con [Hiren's BootCD PE](https://www.hirensbootcd.org); acceso físico.

**Pasos:**

1. Crear USB con Rufus
2. Iniciar desde USB
3. Abrir **NT Password Edit**
4. Cargar archivo SAM: `C:\Windows\System32\config\SAM`
5. Seleccionar usuario → "Change Password" → dejar en blanco → "Save Changes"
6. Reiniciar y verificar acceso

**Ventajas:** Interfaz gráfica amigable
**Limitaciones:** Requiere preparación del USB

---

### ⚠️ Consideraciones Legales y Éticas

> Solo fines educativos y recuperación autorizada.
> El uso no autorizado puede violar leyes locales o internacionales.

### ❓ Preguntas Frecuentes

* **P:** ¿Funciona con cuentas Microsoft?
  **R:** No, solo aplica a cuentas locales.
* **P:** ¿Qué pasa si BitLocker está activado?
  **R:** Necesitas la clave de recuperación.
* **P:** ¿Son detectables estos cambios?
  **R:** Sí, los registros del sistema pueden reflejar la actividad. Documenta siempre tus acciones.

---

## 👨‍💻 Author / Autor

**Rodrigo**
IT Services Specialist, Data Recovery, and Technical Branding
Cybersecurity Student and Open Knowledge Enthusiast

---

## 🤝 Contributions / Contribuciones

Know another secure and legal method? Fork and submit your PR!
¿Conoces otro método seguro y legal? ¡Haz fork y envía tu PR!

*This project aims to document practical solutions for IT professionals / Este proyecto busca documentar soluciones prácticas para profesionales de IT.*

---
