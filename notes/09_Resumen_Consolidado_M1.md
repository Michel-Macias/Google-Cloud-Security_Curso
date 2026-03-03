# 🧪 Módulo 1: Fundamentos de Infraestructura Segura

## 🎯 Objetivos de Aprendizaje
- Comprender la infraestructura física y lógica de Google Cloud (Trusted Base).
- Identificar beneficios y limitaciones del modelo Cloud frente al local.
- Conocer la sintaxis básica de `gcloud` para la gestión de redes (VPC).

---

## 👨‍💻 Escenario
Como analista de seguridad, tu base es la **Confianza**. Google asume la seguridad física (Centros de Datos, Chip Titan) para que tú te centres en la configuración de identidades y redes. Este resumen consolida los documentos críticos del Módulo 1 para tu transición de SysAdmin Linux a Cloud Security Analyst.

---

## 🏛️ Parte 1: La Fundación (Trusted Infrastructure)

### 🛡️ 1: El Chip Titan
Google diseña sus propias placas base. El **Chip Titan** es la "raíz de confianza" (Hardware Root of Trust) que verifica que el sistema no ha sido comprometido antes de arrancar Linux.

### 🛡️ 2: Redundancia vs Latencia
Para un SysAdmin, la **Región** es tu ubicación (Madrid) y la **Zona** es tu rack o centro de datos redundante.
- **Acción**: Siempre despliega en múltiples zonas para evitar puntos únicos de fallo.

---

## ☁️ Parte 2: El Cambio de Paradigma (Cloud vs Local)

### 🔍 Beneficios Clave
- **Time-to-market**: No esperas meses a que llegue el rack físico.
- **Seguridad por defecto**: Cifrado automático de datos en reposo (AES-256) y en tránsito.

### 🔍 Limitaciones Críticas
- **Pérdida de Control Físico**: Debes confiar en los controles del CSP (Cloud Service Provider).
- **Compliance**: Algunos datos sensibles requieren regiones específicas debido a leyes locales.

---

## ⚡ Parte 3: Gestión vía gcloud (Networking Init)

### 🛠️ Comandos de Supervivencia SysAdmin
| Acción | Comando |
| :--- | :--- |
| **Listar Redes** | `gcloud compute networks list` |
| **Crear Red Segura** | `gcloud compute networks create [NAME] --subnet-mode=custom` |
| **Crear Subred** | `gcloud compute networks subnets create [NAME] --network=[VPC] --region=[REGION] --range=[CIDR]` |

> **Nota del Mentor**: El modo **Custom** es el estándar de seguridad. El modo "Auto" crea subredes en todas las regiones del mundo por defecto, lo que expande innecesariamente tu superficie de ataque.

---

## 🧠 Reflexión del Mentor
**¿Por qué un SysAdmin Linux debería preferir el modo de red "Custom" en lugar de "Auto" en GCP?**
> *Respuesta*: El modo Custom permite el control total sobre los rangos de IP y la segmentación. En seguridad, "menos es más". Solo abrimos las subredes que necesitamos, minimizando los vectores de ataque laterales.

---
*Este material ha sido organizado y consolidado por Antigravity como mentor técnico para el curso de Google Cloud Security.*
