# 🚀 Check-list de Migración Segura (Responsabilidad Compartida)

> **Perfil:** Analista de Seguridad / Arquitecto Cloud
> **Módulo 2:** Consideraciones críticas antes de mover cargas de trabajo desde On-premise a GCP.

Como parte del equipo de seguridad de **Cymbal Bank**, antes de migrar cualquier servidor Linux heredado a la nube, debemos hacernos estas 5 preguntas tácticas basadas en el modelo de responsabilidad compartida.

---

## 📋 1. ¿Qué controles son MI responsabilidad?
Migrar no significa delegar la seguridad. Debemos catalogar los activos y definir quién gestiona:
*   Identidades (IAM).
*   Reglas de Firewall (VPC).
*   Cifrado a nivel de aplicación.

## 🛡️ 2. ¿Qué ofrece Google para alinearse con mis necesidades?
Debemos revisar el catálogo de seguridad de Google para ver si tienen el control que necesitamos (ej: Cloud Armor si necesitamos protección WAF).

## 🧬 3. ¿Qué controles heredo proactivamente?
Al usar GCP, "heredamos" seguridad por defecto que en on-premise tendríamos que construir:
*   Cifrado de discos en reposo (AES-256).
*   Seguridad física de clase mundial.
*   Infraestructura con Chip Titan.

## ⚖️ 4. ¿Cuáles son nuestras obligaciones de cumplimiento?
Si el banco debe cumplir con **PCI-DSS** o **GDPR (RGPD)**, debemos verificar:
*   En qué **Región** vivirán los datos.
*   Si el CSP (Google) tiene las certificaciones necesarias para auditar esos sistemas.

## 👥 5. ¿Cómo afecta a terceros (Contratistas)?
La migración cambia cómo accedemos. Debemos revisar:
*   Privilegios de acceso para proveedores externos.
*   Cambios en las políticas de privacidad y divulgación de datos.

---

## 🧠 Reflexión del Mentor

> [!IMPORTANT]
> **La Herencia de Seguridad:** Uno de los mayores errores es replicar exactamente lo que tienes en local en la nube. Aprovecha los **controles heredados** (punto 3) para simplificar tu infraestructura. Si Google ya cifra el disco, no necesitas añadir capas de cifrado de software complejas que ya están cubiertas por la plataforma.

---
*Consolidado para el proyecto Google Cloud Security.*
