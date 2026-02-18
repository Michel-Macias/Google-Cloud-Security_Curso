# Guía de Supervivencia: Google Cloud CLI (`gcloud`) para SysAdmin Analyst

Esta guía está diseñada para un **SysAdmin Linux** que transiciona a **Analista de Seguridad Cloud**. No es una lista exhaustiva, sino un "Cheat Sheet" táctico enfocado en administración, auditoría y respuesta a incidentes.

## 0. Configuración Inicial (Tu "Login" en la Nube)
Antes de nada, autenticarte y definir tu contexto.

*   `gcloud auth login` -> Inicia sesión vía navegador (OAuth).
*   `gcloud config set project <PROJECT_ID>` -> Define en qué "datacenter virtual" estás trabajando.
*   `gcloud config list` -> **Verifica dónde estás** antes de ejecutar comandos destructivos. ¡Crucial!

---

## 1. Gestión de Identidad y Accesos (IAM) - "El Nuevo Sudo"
Como Analista de Seguridad, IAM es tu prioridad #1. Aquí auditas "quién puede hacer qué".

*   **Listar Políticas:** Ver quién tiene permisos en el proyecto.
    *   `gcloud projects get-iam-policy <PROJECT_ID>`
    *   *Tip SysAdmin:* Salida en JSON/YAML, ideal para pipear a `grep` o herramientas de auditoría.
*   **Añadir un Usuario (Cuidado):**
    *   `gcloud projects add-iam-policy-binding <PROJECT_ID> --member="user:email@example.com" --role="roles/editor"`
*   **Auditar Service Accounts (SA):** Las SA son identidades no humanas (como usuarios de sistema en Linux).
    *   `gcloud iam service-accounts list` -> ¿Ves alguna sospechosa?
    *   `gcloud iam service-accounts keys list --iam-account <SA_EMAIL>` -> ¿Claves antiguas no rotadas? **Vulnerabilidad común.**

---

## 2. Compute Engine (Tus Servidores Linux)
Gestión de ciclo de vida de VMs. Piensa en esto como tu `virt-manager` o `vmware` cli.

*   **Listar Instancias:** Inventario rápido.
    *   `gcloud compute instances list`
*   **SSH Seguro (Sin gestionar claves):** La joya de GCP.
    *   `gcloud compute ssh <INSTANCE_NAME>`
    *   *Por qué:* Google gestiona las claves efímeras por ti. No más `id_rsa` perdidas.
*   **Firewall (VPC):** Tu `iptables` a nivel de red.
    *   `gcloud compute firewall-rules list` -> Revisa puertos expuestos (22, 3389, 80).
    *   `gcloud compute firewall-rules create <NAME> --allow map-tcp:80`

---

## 3. Redes (VPC) - "El Cableado"
Entender la topología de red es vital para la seguridad.

*   **Listar Redes y Subredes:**
    *   `gcloud compute networks list`
    *   `gcloud compute networks subnets list`
*   **Ver Rutas:** ¿Hacia dónde va el tráfico?
    *   `gcloud compute routes list`

---

## 4. Auditoría y Logging (Forensics)
Cuando algo pasa, aquí es donde buscas. Equivalente a `/var/log/*` pero global.

*   **Leer Logs (Cloud Logging):**
    *   `gcloud logging read "resource.type=gce_instance AND severity>=ERROR" --limit 10`
    *   *Uso:* Busca errores en todas tus VMs desde un solo comando.
*   **Actividad Admin (Audit Logs):** ¿Quién borró esa VM?
    *   `gcloud logging read "protoPayload.methodName=v1.compute.instances.delete"`

---

## 5. Almacenamiento (Cloud Storage) - "El Filesystem Global"
Buckets públicos son la causa #1 de fugas de datos.

*   **Listar Buckets:**
    *   `gcloud storage ls`
*   **Ver Permisos (ACLs):** Auditar exposición pública.
    *   `gcloud storage buckets get-iam-policy gs://<BUCKET_NAME>`
*   **Copiar/Sincronizar:** Como `rsync`.
    *   `gcloud storage cp <LOCAL_FILE> gs://<BUCKET_NAME>/`

---

## 💡 Trucos de SysAdmin ("Power User")

1.  **Formato de Salida:** Casi todo comando acepta `--format`.
    *   `--format="json"` -> Para scripts.
    *   `--format="table(name, status, networkInterfaces[0].accessConfigs[0].natIP)"` -> Personaliza tu vista como `ps -eo`.
2.  **Filtros:** No uses `grep` si no es necesario, filtra en origen.
    *   `--filter="status=RUNNING AND zone:us-central1"`
3.  **Configuraciones Múltiples:**
    *   `gcloud config configurations create <NAME>` -> Crea perfiles (e.g., "personal", "trabajo") para no mezclar entornos.

---

> **Nota de Seguridad:** Nunca ejecutes comandos de creación/borrado en producción sin verificar tu proyecto activo con `gcloud config list`.
