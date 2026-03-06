# ☁️ Los 3 Pilares del Cloud: IaaS, PaaS y SaaS

> **Perfil:** Analista de Seguridad / SysAdmin Linux
> **Objetivo:** Entender la abstracción del servicio y su impacto en la superficie de ataque.

Como SysAdmin, estás acostumbrado a gestionar desde el cable de red hasta la aplicación final. En la nube, delegamos capas de esa pila a Google. Dependiendo de cuánto deleguemos, estaremos en un modelo u otro.

---

## 🏗️ 1. IaaS (Infrastructure as Service)
*   **Enfoque:** "Dame los recursos, yo me encargo del resto".
*   **Ejemplo en GCP:** Compute Engine (VMs).
*   **Analogía SysAdmin:** Es como si alquilaras un servidor en un rack vacío. Google te da la CPU, la RAM y el Disco, pero tú instalas Debian, configuras el `sshd`, aplicas parches al Kernel y gestionas el `iptables`.
*   **Impacto en Seguridad:**
    *   **Control Total:** Tienes control absoluto del sistema operativo.
    *   **Alta Responsabilidad:** Si no actualizas el Kernel y hay un exploit, la culpa es tuya. Es el modelo con mayor superficie de ataque para gestionar.

## 🚀 2. PaaS (Platform as Service)
*   **Enfoque:** "Solo quiero que mi código funcione, olvídate del SO".
*   **Ejemplo en GCP:** Cloud Run, App Engine, Cloud Functions.
*   **Analogía SysAdmin:** Es como usar un servidor que ya viene con todo instalado y optimizado. Tú solo subes tu aplicación (o un contenedor Docker) y Google se encarga de escalar, parchear el sistema operativo subyacente y asegurar el runtime.
*   **Impacto en Seguridad:**
    *   **Superficie Reducida:** No tienes que preocuparte de parches de seguridad del OS. Google lo hace por ti.
    *   **Foco en la App:** Tu mayor riesgo aquí es que tu código tenga vulnerabilidades (ej: inyección SQL) o que los permisos de IAM sean demasiado laxos.

## 📦 3. SaaS (Software as Service)
*   **Enfoque:** "Solo quiero usar la herramienta".
*   **Ejemplo en GCP:** Google Workspace (Gmail, Drive), BigQuery.
*   **Analogía SysAdmin:** Es como usar una aplicación web comercial. No ves el código, no ves el servidor, no ves la base de datos. Solo ves la interfaz de usuario.
*   **Impacto en Seguridad:**
    *   **Responsabilidad Mínima:** Google gestiona casi todo (parches, red, escalado, infraestructura).
    *   **Foco en Identidad y Datos:** Tu único trabajo como Analista aquí es asegurar **quién** entra (IAM/2FA) y **qué** datos suben (Evitar fugas de información).

---

## 📊 Tabla de Abstracción (¿Quién gestiona qué?)

| Componente | On-Premise | IaaS | PaaS | SaaS |
| :--- | :---: | :---: | :---: | :---: |
| **Aplicaciones** | Tú | Tú | Tú | Google |
| **Datos** | Tú | Tú | Tú | Tú |
| **Runtime / Librerías** | Tú | Tú | Google | Google |
| **Middleware / SO** | Tú | Tú | Google | Google |
| **Virtualización** | Tú | Google | Google | Google |
| **Hardware / Red / Almacén** | Tú | Google | Google | Google |

---

## 🧠 Reflexión del Mentor (Perspectiva de Analista)

> [!IMPORTANT]
> **La Paradoja del Control:** Muchos SysAdmins eligen **IaaS** porque "quieren tener el control de todo". Pero en seguridad, tener el control significa tener la **obligación de asegurar**. 
> 
> Como Analista en **Cymbal Bank**, tu recomendación debería ser: *"Usemos PaaS/SaaS siempre que sea posible para reducir nuestra superficie de ataque, y dejemos IaaS solo para aplicaciones legacy que requieran configuraciones de Kernel específicas"*.
>
> **Menos infraestructura que gestionar = Menos huecos por donde entrar.**

---
*Consolidado para el proyecto Google Cloud Security.*
