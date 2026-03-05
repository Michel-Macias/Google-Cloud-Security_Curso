# Plan de Estudio: Analista SysAdmin de Ciberseguridad en GCP

Este plan está diseñado para transformar tus habilidades de SysAdmin Linux en un perfil de **Analista de Seguridad en Cloud (GCP)**, integrando los materiales del curso de Google con habilidades prácticas de Agente y técnicas de Hacking Ético.

## 🎯 Objetivo
Convertirse en un **Cloud Security Analyst** capaz de diseñar, asegurar, monitorizar y auditar infraestructuras en Google Cloud Platform, manteniendo un fuerte enfoque en la administración de sistemas Linux subyacente.

## 📂 Recursos Disponibles
*   **Documentación Organizada:** Ubicada en `/docs/` con nombres descriptivos (Fundamentos, Redes, Casos de Uso).
*   **Guías de Laboratorio:** Centralizadas en `/labs/`.
*   **Mentor Agent:** Asistencia técnica continua enfocada en SysAdmin -> Cloud Security.
*   **Agent Skills:** `file-organizer` (organización), `cisco-lab-formatter` (estética de docs).

---

## 📅 Hoja de Ruta (Progreso Actual: Módulo 2 en curso)

### Fase 1: Fundamentos de Infraestructura Segura (The "Trusted Base") - [TEORÍA COMPLETADA]
**Enfoque:** Entender dónde "viven" tus servidores Linux en la nube y cómo Google protege la capa física y lógica.

*   **Teoría (Finalizada):**
    *   Análisis de Infraestructura Global y Chip Titan.
    *   Modelos de Servicio (IaaS, PaaS, SaaS) y Responsabilidad Compartida.
    *   Gestión de **Almacenamiento Seguro** (Standard, Coldline, etc.).
    *   Seguridad en entornos **Serverless** (BaaS/FaaS).
    *   Resumen consolidado en `notes/Modulo_1_Resumen_Consolidacion.md`.
*   **Práctica (Siguiente paso):**
    *   Configuración de VPCs personalizadas (Uso de Cloud Shell y `gcloud`).



### Fase 2: Gestión de Servidores y Cargas de Trabajo (SysAdmin -> Cloud Admin)
**Enfoque:** Administrar flotas de servidores y contenedores de forma segura.

*   **Skill Integration: `server-management`**
    *   Aplicar la matriz de decisión de "Process Management" a instancias Compute Engine.
    *   Implementar "Monitoring Principles" usando Google Cloud Operations Suite (antes Stackdriver).
*   **Skill Integration: `gcp-cloud-run`**
    *   Aprender a securizar cargas de trabajo Serverless (si vienes de SysAdmin, esto es el siguiente paso lógico hacia DevOps).
    *   Entender la seguridad en el ciclo de vida del contenedor.

### Fase 3: Identidad y Control de Acceso (El nuevo "Perímetro")
**Enfoque:** IAM es el firewall más importante en la nube.

*   **Teoría:**
    *   Entender la jerarquía de recursos (Organización > Carpeta > Proyecto).
    *   Service Accounts vs. User Accounts.
*   **Práctica:**
    *   Auditoría de permisos con `gcloud`.
    *   Implementación de "Least Privilege".

### Fase 4: Operaciones de Seguridad y Respuesta a Incidentes (The Analyst Role)
**Enfoque:** Detectar y responder a amenazas en un contexto organizacional real.

*   **Escenario Cymbal Bank (Tu Rol: Junior Security Analyst):**
    *   **Contexto:** Banco minorista en transformación digital hacia la nube híbrida.
    *   **Equipo:** Javier (CISO), Chloe (Lead), Hank (Architect), Hannah (Incident Response).
    *   **Misión:** Asegurar la adopción de la nube, automatizar con IaC y configurar redes seguras.
    *   Analizar `docs/casos_uso/18_Caso_Uso_Cymbal_Bank.pdf`.
*   **Herramientas:**
    *   Security Command Center (SCC).
    *   Cloud Logging para análisis forense.

### Fase 5: Hacking Ético en Cloud (Red Teaming)
**Enfoque:** Auditar tu propia infraestructura.

*   **Skill Integration: `cloud-penetration-testing`**
    *   **Reconnaissance:** Enumerar recursos públicos y buckets olvidados.
    *   **GCP Enumeration:** Usar `gcloud` para mapear la superficie de ataque.
    *   **Exploitation:** Probar escalada de privilegios en IAM (e.g., permisos `iam.serviceAccounts.actAs`).
    *   **Validación:** Verificar que tus controles de Fase 1-3 detectan estas actividades.

---

## 🛠 Entorno de Laboratorio Recomendado (Setup Inicial)

Para completar este plan, necesito que configuremos tu entorno local (`/home/m1txel/Escritorio/Google Cloud Security`) como un "Centro de Mando".

1.  **Organización de Archivos:** Reestructurar los PDFs por módulos.
2.  **Herramientas CLI:** Verificar instalación de `gcloud` sdk.
3.  **Repo de Notas:** Usar Markdown para documentar cada lab (siguiendo el estilo de tus otros proyectos).

## ✅ Siguientes Pasos Inmediatos
1.  Confirmar si tienes acceso a una cuenta de GCP (Free Tier o Sandbox del curso).
2.  Organizar los PDFs actuales en carpetas (`/docs/module_1`, `/docs/module_4`, etc.) para limpiar el escritorio.
3.  Empezar con el análisis del documento "Infraestructura de confianza".
