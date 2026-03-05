# 🕵️ Auditoría y Detección: El "journalctl" de la Nube

> **Perfil:** Analista de Seguridad / SysAdmin
> **Concepto:** Uso de Cloud Logging y gcloud para detectar incidentes.
> **Módulo 2:** Función de "Detección" y "Respuesta".

Para un SysAdmin Linux, los logs son la verdad absoluta. En GCP, **Cloud Logging** centraliza todo. Aquí tienes cómo usarlo como un verdadero Analista de Seguridad en **Cymbal Bank**.

---

## 🔍 1. Los 3 Logs Críticos
Como Analista, estos son los que debes vigilar:
1.  **Admin Activity Logs:** (Escritura) Quién creó, borró o modificó un recurso. No se pueden desactivar.
2.  **Data Access Logs:** (Lectura) Quién leyó datos sensibles en un Bucket o Base de Datos.
3.  **System Event Logs:** Generados por los sistemas de Google (ej: una VM se reinició por mantenimiento).

---

## 🛠️ 2. Filtros de Detección (Survival Commands)

No uses el buscador de la consola web; usa filtros de `gcloud` para ser más rápido:

### A. Detectar quién borró una instancia
```bash
gcloud logging read "protoPayload.methodName=v1.compute.instances.delete" \
    --format="table(protoPayload.authenticationInfo.principalEmail, timestamp, resource.labels.instance_id)"
```

### B. Buscar cambios en las reglas de Firewall (Microsegmentación rota)
```bash
gcloud logging read "resource.type=gce_firewall_rule AND protoPayload.methodName:patch" \
    --format="yaml(protoPayload.authenticationInfo.principalEmail, protoPayload.request, timestamp)"
```

### C. Errores de Permisos (Posible movimiento lateral o escalada)
Busca denegaciones de acceso (403 Forbidden):
```bash
gcloud logging read "protoPayload.status.code=7" --limit 5
```

---

## 🚨 3. Respuesta ante Incidentes (IR)

Siguiendo el flujo del NIST:
1.  **Identificar:** Recibes una alerta de Security Command Center (SCC).
2.  **Contener:** Si una VM está comprometida, ¡no la borres aún!
    *   **Acción SysAdmin:** Quítale las etiquetas de red para que el firewall la bloquee:
        `gcloud compute instances remove-tags instancia-sospechosa --tags=http-server,https-server`
3.  **Investigar:** Haz un snapshot del disco para análisis forense offline.
4.  **Erradicar:** Borra la VM y despliega una nueva desde una imagen segura (IaC).

---

## 🧠 Reflexión del Mentor

> [!TIP]
> **Logs vs Realidad:** En Linux, un atacante con root puede borrar `/var/log/auth.log`. En la nube, los logs de GCP se guardan fuera de la VM, en una infraestructura que el atacante no puede tocar aunque sea root en tu Linux. Esto hace que el "Forense Cloud" sea mucho más confiable.

> [!IMPORTANT]
> **Estructura el Log:** Acostúmbrate al formato JSON de los logs de GCP. La potencia de `gcloud logging --filter` es superior al `grep` tradicional porque entiende la jerarquía de los datos.

---
*Documento consolidado para el proyecto Google Cloud Security.*
