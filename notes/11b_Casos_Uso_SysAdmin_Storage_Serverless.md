# 🏥 Casos de Uso: Almacenamiento y Serverless para el Analista IT

Este documento aplica la teoría de los módulos 10 y 11 del curso a escenarios reales que un **SysAdmin** maneja a diario, transformando tareas manuales en flujos de seguridad cloud.

---

## 💾 Escenario 1: Almacenamiento (Storage Class Strategy)
**Problema**: Tienes 50TB de backups de logs y logs de auditoría (compliance) que debes guardar por 5 años, pero casi nunca los consultas. Mantenerlos en discos estándar es prohibitivo por costes.

| Situación | Clase de Almacenamiento | Configuración de Seguridad |
| :--- | :--- | :--- |
| **Logs de Auditoría (7 años)** | `Archive Storage` | **Bucket Lock**: Impide que incluso tú (el Admin) borres los logs antes de 7 años (WORM). |
| **Recuperación ante Desastres (DR)** | `Nearline Storage` | **Object Versioning**: Si un ransomware cifra tus copias, puedes "volver atrás" en el tiempo. |
| **Repositorio de Scripts/ISOs** | `Standard Storage` | **Uniform Bucket-Level Access**: Asegura que el acceso sea solo vía IAM, no por ACLs antiguas. |

---

## ⚡ Escenario 2: Serverless (Seguridad Automatizada)
**Problema**: En una infraestructura On-Premise, es difícil monitorizar cada archivo que un usuario sube. En GCP, podemos automatizarlo sin servidores dedicados.

### Caso: "La Bóveda de Limpieza Automatizada"
*   **Evento**: Un usuario sube un archivo (ej: un reporte PDF) a un Bucket de Cloud Storage.
*   **Acción (Cloud Function/FaaS)**: Al activarse por la "subida", una pequeña función salta (trigger), escanea el archivo con un motor antivirus o comprueba su hash.
*   **Resultado**:
    *   Si es seguro -> Lo mueve a la carpeta de "Aprobados".
    *   Si es sospechoso -> Lo bloquea, lo mueve a una carpeta de "Cuarentena" y te envía una alerta a tu móvil.
*   **Ventaja SysAdmin**: No tienes una VM encendida 24/7 gastando CPU; solo pagas por los segundos que dura el escaneo.

---

## 🛡️ Escenario 3: "Shadow IT Prevention" (IAM & Serverless)
**Problema**: Un compañero de DevOps crea un Bucket público por error para "probar algo" y olvida cerrarlo.

*   **Implementación**: Una **Cloud Function** monitoriza los cambios de IAM del proyecto.
*   **Reacción**: Si detecta que el miembro `allUsers` (Público) ha sido añadido a un recurso, la función **elimina automáticamente ese permiso** y registra quién hizo el cambio.
*   **Conexión con la teoría**: Aquí aplicamos el "Principio de Mínimo Privilegio" de forma proactiva.

---

## 🧠 Reflexión del Mentor
Como alguien que viene del sector IT, estas herramientas te permiten dejar de ser un "bombero" (apagando fuegos manualmente) para pasar a ser un "arquitecto" (diseñando sistemas que se protegen solos). El **Almacenamiento Archive** es tu seguro de vida para auditorías, y el **Serverless** es tu brazo ejecutor para la seguridad a escala.
