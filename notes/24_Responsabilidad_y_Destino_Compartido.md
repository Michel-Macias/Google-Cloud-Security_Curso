# 🤝 Responsabilidad Compartida vs. Destino Compartido

> **Perfil:** Analista de Seguridad / SysAdmin
> **Módulo 2:** El "Contrato de Seguridad" en Cloud.

En **Cymbal Bank**, necesitamos saber dónde termina el trabajo de Google y dónde empieza el nuestro. No hay nada más peligroso que un Analista que cree que "Google ya lo protege todo".

---

## 🏗️ 1. Responsabilidad Compartida (The Rules)

Es el modelo tradicional. Define quién es el dueño de cada capa de seguridad.

| Capa | On-Premise (Tu oficina) | IaaS (Compute Engine) | PaaS (Cloud Run) | SaaS (Gmail/Workspace) |
| :--- | :--- | :--- | :--- | :--- |
| **Hardware / Data Center** | Tú | Google | Google | Google |
| **Red Física / Cables** | Tú | Google | Google | Google |
| **SO (Linux Hardening)** | Tú | **Tú (SysAdmin)** | Google | Google |
| **Config. Firewall (VPC)** | Tú | **Tú (SysAdmin)** | **Compartido** | Google |
| **Acceso / IAM** | Tú | **Tú** | **Tú** | **Tú** |
| **DATOS** | Tú | **Tú** | **Tú** | **Tú** |

> [!IMPORTANT]
> **La Constante:** Los **datos** y el **acceso (IAM)** son SIEMPRE responsabilidad tuya. Google nunca entrará a ver tus datos ni a configurar tus usuarios.

---

## 🚀 2. Destino Compartido (Shared Fate)

Google Cloud ha evolucionado el modelo. Ya no solo te dicen qué es tu problema, actúan como **socios**.

### ¿Cómo nos ayuda Google en el "Destino Compartido"?
1.  **Secure Blueprints:** Guías de configuración "Terraform" ya listas para ser seguras (ej: red para PCI-DSS).
2.  **Risk Protection Program:** Si usas las herramientas de seguridad de Google (como SCC), puedes obtener mejores condiciones en seguros de ciberseguridad.
3.  **Policy Intelligence:** Herramientas que te dicen: *"Oye, este usuario tiene demasiados permisos y no los usa, deberías quitárselos"*.

---

## 🧠 Reflexión del Mentor

> [!TIP]
> **El Gran Error del SysAdmin:** Muchos administradores vienen de redes locales y piensan que con tener una cuenta en GCP ya están protegidos. El **Destino Compartido** es genial, pero si dejas un bucket público con las nóminas de Cymbal Bank, el "destino" será que el banco pierda reputación y tú tengas un problema serio. 
> 
> Google te da las herramientas (Shared Fate), pero tú tienes que apretar el botón (Shared Responsibility).

---
*Consolidado para el proyecto Google Cloud Security.*
