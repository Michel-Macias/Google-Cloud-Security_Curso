# 🏗️ Caso de Uso Real: IaaS (Infrastructure as a Service)

> **Perfil Objetivo:** SysAdmin / Admistrador de Sistemas
> **Propósito:** Profundizar en el modelo IaaS mediante un escenario práctico, técnico y detallado que demuestre el nivel de control y la carga operativa que este modelo exige a un administrador.

En el modelo IaaS, el proveedor de la nube (como Google Cloud) te entrega los recursos fundamentales: cómputo (CPU/RAM virtualizada), almacenamiento en bloque y redes. Como SysAdmin, adquieres el máximo nivel de control posible en la nube, pero a cambio, heredas la máxima responsabilidad operativa y de seguridad sobre el sistema operativo y todo lo que corra sobre él.

---

## 🐧 El Escenario: Despliegue de un Clúster de Base de Datos de Alto Rendimiento con ZFS

**Situación Inicial:**
Tu empresa es una firma de análisis financiero que procesa millones de transacciones por segundo. Han decidido migrar su base de datos principal PostgreSQL a la nube, pero los servicios administrados (PaaS) como Cloud SQL no soportan las configuraciones extremas de optimización que el equipo de bases de datos exige. Necesitan control absoluto a nivel de Kernel y un sistema de archivos especializado (ZFS) para manejar la compresión y las instantáneas (snapshots) en tiempo real.

**Tu Rol como SysAdmin:**
Eres el responsable de diseñar, aprovisionar, configurar y asegurar la infraestructura que soportará esta base de datos crítica.

### 🛠️ Desarrollo de la Implementación en IaaS (Compute Engine)

1.  **Aprovisionamiento Raw (La Infraestructura Base):**
    *   No puedes usar imágenes preconfiguradas estándar. Creas instancias de **Compute Engine (VMs)** seleccionando la familia de máquinas optimizadas para memoria (ej. serie M2 o M3 en GCP) con cientos de Gigabytes de RAM.
    *   Adjuntas discos persistentes SSD de rendimiento extremo (Local SSDs para caché hiper-rápida y Persistent Disk Extreme para almacenamiento persistente).
    *   Diseñas una Red Virtual (VPC) aislada, configurando subredes y reglas de firewall a nivel de puerto (permitiendo solo el tráfico del puerto 5432 desde la subred de aplicaciones).

2.  **Configuración del Sistema Operativo y Kernel:**
    *   Instalas un sistema operativo base libre de bloatware (ej. Ubuntu Server Minimal o Debian).
    *   Como SysAdmin, debes modificar el núcleo (Kernel) de Linux para exprimir el rendimiento. Te conectas por SSH (idealmente a través de IAP - Identity-Aware Proxy para mayor seguridad) y modificas parámetros en `/etc/sysctl.conf`:
        *   `vm.swappiness = 1` (Minimizar el uso de swap para evitar latencia).
        *   `net.core.somaxconn = 65535` (Aumentar el límite de conexiones de red simultáneas).
        *   `kernel.shmmax` (Ajustar la memoria compartida para PostgreSQL).
    *   Instalas y compilas el sistema de archivos **ZFS** desde los repositorios de Linux, formateas los discos adjuntos y montas los puntos (`/var/lib/postgresql`).

3.  **Seguridad y Fortificación (Hardening):**
    *   **Patch Management:** Eres el único responsable de que este servidor reciba los últimos parches de seguridad (CVEs). Si sale una vulnerabilidad grave en `OpenSSH` o en el propio Kernel de Linux, debes planificar una ventana de mantenimiento técnico a las 3:00 AM, actualizar los paquetes (`apt-get upgrade`) y reiniciar los nodos secuencialmente.
    *   **Control de Acceso:** Configuras `fail2ban` o `iptables` a nivel de host para complementar el firewall de la nube, y te aseguras de deshabilitar la autenticación por contraseña (`PasswordAuthentication no` en `sshd_config`), requiriendo llaves criptográficas administradas por OS Login.

### ⚖️ Balance y Valor para el SysAdmin

*   **Lo Positivo (Poder Absoluto):** Has logrado una base de datos más rápida y personalizada que cualquier servicio gestionado genérico. Puedes diagnosticar cuellos de botella utilizando herramientas de bajo nivel como `htop`, `strace`, `iostat` o `tcpdump` directamente en la consola de la máquina.
*   **Lo Negativo (Carga Operativa):** Te has convertido en un esclavo del mantenimiento. Eres responsable del *uptime* del sistema operativo, de la rotación de logs (configurando `logrotate`), de los backups binarios, y de responder a cada alerta de vulnerabilidad de software publicando parches a mano o script.

### 🧠 Reflexión del Mentor
Este escenario demuestra la esencia de **IaaS**: es el paraíso de los verdaderos "picadores de comandos" porque el terminal es tuyo. No hay cajas negras. Sin embargo, para la escala moderna, desplegar infraestructura a este nivel de detalle manual (sin automatización férrea como Ansible o Terraform) es insostenible y peligroso. **IaaS es donde asumes más riesgo, porque cada componente no configurado es una puerta abierta.**
