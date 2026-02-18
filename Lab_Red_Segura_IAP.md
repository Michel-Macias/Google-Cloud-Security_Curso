# Lab Práctico: Despliegue de Red Segura y Bastion Host (SysAdmin Mode)

En este laboratorio vamos a aplicar los conceptos de los **Módulos 1 y 4** para crear una infraestructura que cumpla con los estándares de un Analista de Seguridad.

## 🎯 Escenario del Laboratorio
Vamos a crear una red "Custom" (Personalizada) desde cero, con una subred aislada, y configuraremos un servidor Linux que **no tenga IP pública** (invisible para ataques de internet). Aprenderemos a acceder a él de forma segura.

---

## 🛠️ Requisitos Previos
1.  Haber ejecutado `gcloud auth login` en tu terminal.
2.  Tener un ID de Proyecto de GCP a mano (puedes verlo con `gcloud projects list`).

---

## 🚀 Fase 1: Creación del "Cableado" (VPC y Subred)

Como Analista, siempre huimos del modo "Auto". Queremos control total.

```bash
# 1. Crear la red VPC en modo personalizado
gcloud compute networks create red-segura-lab --subnet-mode=custom

# 2. Crear una subred en Madrid (o la región que prefieras)
# Usaremos el rango 10.10.1.0/24. 
# Activamos '--enable-private-ip-google-access' (Módulo 4 puro!)
gcloud compute networks subnets create subred-segura-madrid \
    --network=red-segura-lab \
    --range=10.10.1.0/24 \
    --region=europe-southwest1 \
    --enable-private-ip-google-access
```

---

## 🛡️ Fase 2: El Firewall (Iptables en la Nube)

Vamos a permitir SSH pero **solo de una forma especial**: a través del proxy de Google (IAP), para no tener que abrir el puerto a todo internet.

```bash
# Crear regla de entrada para IAP (Identity-Aware Proxy)
# IP de Google IAP: 35.235.240.0/20 (Es el rango oficial de Google para este servicio)
gcloud compute firewall-rules create permitir-ssh-iap \
    --network=red-segura-lab \
    --allow=tcp:22 \
    --source-ranges=35.235.240.0/20 \
    --target-tags=permite-ssh
```

---

## 💻 Fase 3: Despliegue del Servidor (Identidad y Confianza)

Ahora desplegamos nuestra VM Linux (Debian/Ubuntu). Fíjate que no le ponemos IP externa (`--no-address`).

```bash
# Crear la instancia de seguridad
gcloud compute instances create servidor-secreto \
    --zone=europe-southwest1-a \
    --network-interface=subnet=subred-segura-madrid,no-address \
    --tags=permite-ssh \
    --image-family=debian-12 \
    --image-project=debian-cloud \
    --metadata=enable-oslogin=TRUE
```

---

## 🕵️ Fase 4: Acceso y Verificación (El Rol del Analista)

Como no tiene IP pública, un `nmap` desde tu casa no verá nada. Usaremos el túnel de Google.

```bash
# Acceder vía túnel IAP
gcloud compute ssh servidor-secreto --tunnel-through-iap --zone=europe-southwest1-a
```

### Una vez dentro de la VM, haz estos checks de SysAdmin:
*   `ip addr` -> Verás que solo tienes la IP `10.10.1.x`.
*   `ping google.com` -> **¡Fallará!** (No tienes salida a internet).
*   *Prueba Maestra:* Intenta usar una API de Google (ej: `gsutil ls`). Funcionará gracias al **Private Google Access** que activamos en la Fase 1, aunque no tengas internet.

---

## 📊 Tarea de Auditoría (Para tu .md de notas)
Después de hacer el lab, ejecuta este comando y guarda la salida. Es lo que presentaría un Analista en un informe:

```bash
gcloud compute firewall-rules describe permitir-ssh-iap --format="yaml(name,allowed,sourceRanges,targetTags)"
```

---

## 🧹 Limpieza (Para no gastar saldo)
Cuando termines, borra todo el laboratorio con un comando:
```bash
gcloud compute networks delete red-segura-lab --quiet
```
