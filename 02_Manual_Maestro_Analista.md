# manual Maestro: Analista de Seguridad Cloud (Módulos 1, 2 y 4)

Este manual ha sido diseñado específicamente para ti, un **Administrador de Sistemas Linux**, que está cursando el Certificado de Google Cloud Security. Combina la teoría de los documentos técnicos con las lecciones clave de los vídeos del curso, todo en español y adaptado a tu perfil técnico.

---

## 🏛️ Parte 1: La Fundación (Infraestructura de Confianza)

En la nube, no puedes ver ni tocar el servidor físico. Por eso, Google ha construido una "cadena de confianza" que garantiza que el hardware donde corre tu Linux es seguro.

### 1. El Hardware no es "estándar"
Google diseña sus propios centros de datos y chips. El componente estrella es el **Chip Titan**.
*   **¿Qué hace?** Es una "Ancla de Seguridad". Verifica que la placa base y el procesador no han sido manipulados antes de que siquiera se encienda la máquina.
*   **Arranque Seguro (Secure Boot):** Es como una carrera de relevos. El hardware verifica el BIOS; el BIOS verifica el cargador de arranque; el cargador de arranque verifica el Kernel de Linux. Si un eslabón falla, el sistema no arranca.

### 2. Infraestructura Global: Zonas y Regiones
*   **Centro de Datos:** El edificio físico.
*   **Zona:** Un conjunto de uno o más centros de datos (ej: `europe-southwest1-a`).
*   **Región:** Un grupo de zonas conectadas (ej: `europe-southwest1` en Madrid).
*   **Resiliencia y Redundancia:** Como SysAdmin, antes tenías un servidor de backup en la oficina de al lado. Aquí, la **Redundancia** significa copiar tus datos en diferentes "dominios con fallas" (Zonas/Regiones) para que, si un rayo cae en un edificio, tu servicio siga vivo en otro.

---

## ☁️ Parte 2: Modelos de Servicio y Responsabilidad

Este es el concepto más importante para un Analista. Define **quién tiene la culpa** si algo falla.

| Modelo | Definición | Tu responsabilidad (SysAdmin) |
| :--- | :--- | :--- |
| **IaaS** (Instancias GCE) | Google te da el hierro y la red. | **TODO**: Parches de Linux, Apps, Datos, Firewall de la VM. |
| **PaaS** (Cloud Run/App Engine) | Google te da la plataforma para correr tu código. | **Configuración y Datos**: Solo te preocupas de tu app y quién accede. |
| **SaaS** (Gmail/Workspace) | Google te da el software listo. | **Solo los Datos**: Quién entra y qué políticas de acceso tiene. |

> **Principio Clave:** Google protege "La Nube" (hardware, cables). Tú proteges "Lo que hay en la Nube" (tus sistemas operativos, tus usuarios).

---

## 🌐 Parte 3: Redes VPC (Tu Nuevo Data Center Virtual)

Como SysAdmin, tú antes configurabas VLANS y switches. En GCP, todo es **Software Defined Networking (SDN)**.

### 1. El Perímetro Seguro
*   **VPC Global:** Tu red no está atada a un router físico. Es un recurso mundial.
*   **Aislamiento por Subredes:** Aunque la VPC sea global, las subredes son regionales. Úsalas para separar entornos (Prod, Dev, Test).
*   **Acceso Privado a Google:** Visto en los vídeos y PDFs. Permite que tus VMs sin IP de internet se conecten a los servicios de Google. **Esto es oro puro para la seguridad.**

### 2. Firewall: Etiquetas vs IPs
En lugar de recordar que el servidor Web es la `192.168.1.10`, usas **Network Tags**.
*   Creas la etiqueta `web`.
*   Creas la regla de firewall: "Permitir puerto 80 a etiqueta `web`".
*   Esto es **Microsegmentación**. Si una máquina es atacada, el firewall la aislará del resto si no comparten etiquetas.

---

---

## 🛡️ Parte 4: Marcos de Trabajo (NIST CSF y Tríada CIA)

Como Analista, tus decisiones deben basarse en estándares. No protegemos "a ojo", protegemos siguiendo un plan.

### 1. La Tríada CIA (Confidencialidad, Integridad, Disponibilidad)
Es el ABC de la ciberseguridad. Todo control que pongas debe proteger una de estas tres:
*   **Confidencialidad:** Que nadie vea los datos (Cifrado, IAM).
*   **Integridad:** Que nadie los cambie (Hashes, Firmas).
*   **Disponibilidad:** Que el servicio no caiga (Alta Disponibilidad, Backups).

### 2. Marco NIST CSF (Tus 5 mandamientos)
Google recomienda el marco del NIST para organizar tu estrategia:
1.  **Identificar:** Conoce tus activos (Cloud Asset Inventory).
2.  **Proteger:** Pon barreras (Firewalls, IAM).
3.  **Detectar:** Vigila señales (Security Command Center).
4.  **Responder:** Actúa ante incidentes (Automatización de respuesta).
5.  **Recuperar:** Vuelve a la normalidad (Snapshots, Replicación).

### 3. Defensa en Profundidad (Capas de Cebolla)
No confiamos en una sola "muralla". Si el atacante rompe el firewall, se encuentra con IAM. Si rompe IAM, se encuentra con datos cifrados. 
*   **Capas:** Física > Red > Identidad > Cómputo > Datos.
*   Documento detallado: `notes/23_Defensa_en_Profundidad_Cloud.md`.

---

## ⚙️ Parte 5: Conceptos de Negocio para el Analista

---

## 📂 Mapa de Recursos (Docs & Labs)

Tus materiales están en `/docs/` y `/notes/` con nombres descriptivos:
1. **Fundamentos**: `/docs/modulo_1_fundamentos/` (Certificado, Cifrado, Titan).
2. **Redes**: `/docs/modulo_4_redes/` (VPC, gcloud commands).
3. **Casos de Uso**: `/docs/casos_uso/` (Escenario Cymbal Bank).
4. **Laboratorios**: `/labs/` (Guías paso a paso como IAP).
5. **Estrategia y Marcos**:
    * `notes/22_Resumen_NIST_CSF_GCP.md` (Marco NIST).
    * `notes/23_Defensa_en_Profundidad_Cloud.md` (Capas de seguridad).
    * `notes/21_Resumen_Ciberseguridad_M2.md` (C.I.A. y Modelado).

---

## 🚀 Hoja de Ruta Inmediata (Fase de Consolidación)

1.  **Revisar el Resumen**: Lee `notes/Modulo_1_Resumen_Consolidacion.md` para refrescar los conceptos clave de este módulo.
2.  **Laboratorio Red Segura**: Usa el archivo `labs/Lab_Red_Segura_IAP.md`. En él aplicarás el **Acceso Privado a Google** y el **Firewall por Etiquetas**.
3.  **Glosario de Términos**: El glosario centralizado está en `docs/modulo_1_fundamentos/00_Glosario_Terminos.pdf`. Úsalo cada vez que hagamos un lab.

**¿Qué te parece la nueva organización?** He limpiado el ruido de los nombres genéricos de Google para que te sientas como en un entorno de trabajo real de un Analista.
