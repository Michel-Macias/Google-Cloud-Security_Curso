# 🛡️ Marco NIST CSF: Controles de Seguridad en Google Cloud

> **Perfil:** Analista de Seguridad Cloud
> **Objetivo:** Implementar Defensa en Profundidad usando estándares globales.
> **Material de Referencia:** Manual de Controles de Seguridad (Google Cloud).

En el rol de **Analista de Seguridad en Cymbal Bank**, no solo tiramos comandos; nos regimos por marcos de trabajo que garantizan que no dejamos ningún flanco abierto. El **NIST Cyber Security Framework (CSF)** es el estándar de oro que Google recomienda seguir.

---

## 🏗️ Las 5 Funciones del NIST CSF

### 1. Identificar (Identificación)
*   **¿Qué es?**: Conocer tus activos. No puedes proteger lo que no sabes que existe.
*   **En GCP**:
    *   Inventario de activos mediante **Cloud Asset Inventory**.
    *   Clasificación de datos críticos (PII de clientes del banco).
    *   Evaluación de riesgos iniciales.

### 2. Proteger (Protección)
*   **¿Qué es?**: Poner "barreras" para evitar ataques.
*   **En GCP**:
    *   **IAM**: Control de acceso granular (Principio de mínimo privilegio).
    *   **VPC Firewalls & Cloud Armor**: Microsegmentación y protección contra DDoS.
    *   **Cloud KMS**: Cifrado de datos en reposo y tránsito.
    *   *Entrenamiento*: Concienciación del staff de Cymbal Bank contra phishing.

### 3. Detectar (Detección)
*   **¿Qué es?**: Vigilar las señales de humo.
*   **En GCP**:
    *   **Security Command Center (SCC)**: Visibilidad centralizada de amenazas.
    *   **Cloud Logging & Monitoring**: Auditoría de logs de acceso (¿Quién hizo qué y cuándo?).
    *   **Intrusion Detection**: Monitoreo de tráfico sospechoso.

### 4. Responder (Respuesta)
*   **¿Qué es?**: Actuar rápido cuando algo huele mal.
*   **En GCP**:
    *   **Automatización**: Usar Cloud Functions o Pub/Sub para aislar una VM comprometida automáticamente.
    *   **Plan de Respuesta**: Procedimientos establecidos para el equipo de Hannah (Incident Response).

### 5. Recuperar (Recuperación)
*   **¿Qué es?**: Volver a la normalidad tras el caos.
*   **En GCP**:
    *   **Alta Disponibilidad**: Replicación multi-zona/región.
    *   **Backups**: Uso de snapshots de disco y Cloud Storage con versionado.
    *   *Objetivo*: Restablecer los servicios del banco con la mínima pérdida de datos (RPO/RTO).

---

## 🧠 Reflexión del Mentor (Perspectiva SysAdmin)

> [!IMPORTANT]
> **Del Rack a la API:** Como SysAdmin tradicional, hacías "Recuperación" cambiando cintas de backup o discos. En Cloud, la "Recuperación" es código (IaC) que despliega una infraestructura idéntica en Australia en minutos si Madrid falla. 
> 
> **Defensa en Profundidad:** El NIST nos enseña que un solo control (ej: una contraseña fuerte) no es suficiente. Necesitamos "Capas de Cebolla". Si el atacante rompe la contraseña (Protección), nuestro SCC debe detectarlo (Detección) y nuestro plan de respuesta debe aislar la cuenta (Respuesta).

---

## 📊 Tarea para tu Portafolio
Relaciona el **Lab 17 (IAP)** con el NIST:
*   **Protección**: Uso de Firewall Regeln e IAP para eliminar IPs públicas.
*   **Identificación**: Uso de etiquetas de red (`target-tags`) para identificar qué recursos reciben tráfico.

---
*Documento consolidado para el curso de Google Cloud Security.*
