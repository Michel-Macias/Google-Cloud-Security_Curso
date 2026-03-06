# 🌐 Módulo 4: Arquitectura de Red Segura (Deep Dive)

## 🎯 Objetivos de Aprendizaje
- Dominar el concepto de **Software Defined Networking (SDN)** en Google Cloud.
- Implementar el principio de mínimo privilegio en el diseño de subredes.
- Diferenciar entre flujos de tráfico internos (PGA) y externos (IAP/Firewall).

---

## 👨‍💻 Escenario
En el Módulo 4, dejamos de ver la nube como un concepto abstracto y empezamos a "tirar cables" virtuales. Como Analista, tu trabajo es asegurar que el tráfico de la base de datos de Cymbal Bank nunca "toque" la internet pública, usando las herramientas nativas de GCP.

---

## 🚀 Parte 1: El Cerebro de la Red (VPC)

### 🔍 Modo Automático vs Custom (Manual)
*   **Auto**: Crea una subred `/20` en cada región. *Riesgo*: Desperdicia IPs y abre puertas innecesarias.
*   **Custom**: Tú defines cada byte. *Recomendado*: Para un Analista, el diseño custom es la primera línea de defensa.

### 🔍 Límites y Cuotas
Por defecto, un proyecto tiene un límite de redes VPC. Esto evita el "Shadow IT" (redes creadas fuera de control).

---

## ⚡ Parte 2: Aislamiento por Segmentación

### 🛡️ Acceso Privado a Google (Private Google Access - PGA)
Esta es una de las funciones más potentes de seguridad en GCP.
- **¿Qué es?**: VMs con IPs privadas pueden llegar a los servicios de Google (Storage, APIs) sin salir a internet.
- **Comando de Auditoría**:
  ```bash
  gcloud compute networks subnets describe [NAME] --region=[REGION]
  # Busca "privateIpGoogleAccess: true"
  ```

---

## 🧠 Reflexión del Mentor
**Si una instancia no tiene IP pública, ¿cómo puede descargar actualizaciones de seguridad de Google?**
> *Respuesta*: Gracias al **Private Google Access**. Como Mentor, te recomiendo activar esto en todas tus subredes de producción. Permite el mantenimiento sin exposición al mundo exterior.

---
*Documento consolidado para el curso de Google Cloud Cybersecurity.*
