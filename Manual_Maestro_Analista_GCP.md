# manual Maestro: Analista de Seguridad Cloud (Módulos 1 y 4)

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

## ⚙️ Parte 4: Conceptos de Negocio para el Analista

Un Analista no solo tira comandos, también justifica gastos.
*   **CapEx (Capital Expenditure):** Gastar 20.000€ en servidores físicos que durarán 5 años. (Modelo Local).
*   **OpEx (Operational Expenditure):** Pagar solo por lo que usas cada mes (Modelo Cloud). Como Analista, el OpEx te permite escalar la seguridad cuando hay ataques y reducirla cuando no es necesaria.
*   **DevSecOps:** No es una herramienta, es una cultura. Significa que la **Seguridad** se mete en medio de los Desarrolladores y los de Operaciones (nosotros) desde el primer minuto.

---

## 🚀 Hoja de Ruta Inmediata (Fase de Consolidación)

1.  **Termina tu alta en GCP.**
2.  **Laboratorio Red Segura:** Usa el archivo `Lab_Red_Segura_IAP.md` que te preparé. En él aplicarás el **Acceso Privado a Google** y el **Firewall por Etiquetas**.
3.  **Glosario de Términos:** He visto en el PDF de "Sugerencias" que los glosarios son vitales. Úsalos cada vez que hagamos un lab.

**¿Qué te parece este manual resumido?** Lo tienes guardado en la raíz de tu carpeta como una guía rápida para no tener que volver a los PDFs en inglés cada vez que tengas una duda.
