# 🧪 Lab: Despliegue de Red Segura y Bastion Host (IAP)

> **Perfil:** Analista de Seguridad / SysAdmin Cloud
> **Módulos:** 1 (Infraestructura de Confianza) y 4 (Networking)
> **Nivel:** Intermedio

En este laboratorio aplicaremos los principios de **Zero Trust** y **Microsegmentación** para crear una infraestructura invisible desde el internet público.

---

## 🎯 Objetivos
1.  Diseñar una **VPC Custom** (No-Auto) para control total del direccionamiento.
2.  Implementar **Private Google Access** para comunicación segura con APIs.
3.  Configurar un **Firewall defensivo** basado en etiquetas y rangos de confianza.
4.  Desplegar una instancia Linux **sin IP Pública** (Hardened).
5.  Validar el acceso mediante **IAP (Identity-Aware Proxy)**.

---

## 🗺️ Escenario
La empresa **Cymbal Bank** requiere un entorno de gestión para sus bases de datos. El servidor no debe tener exposición directa a internet para prevenir ataques de fuerza bruta al puerto 22. Utilizaremos el túnel de Google como único vector de entrada autorizado.

---

## 🛠️ Requisitos Previos
*   Acceso a proyecto GCP con permisos de `Compute Admin`.
*   Google Cloud SDK (`gcloud`) configurado localmente.
*   ID del proyecto: `gcloud config get-value project`.

---

## 🚀 Fase 1: El Cableado Virtual (VPC)

Como arquitecto de seguridad, evitamos las redes "Default". Queremos segmentación granular.

```bash
# 1. Crear la red VPC en modo personalizado
gcloud compute networks create red-segura-lab --subnet-mode=custom

# 2. Crear subred en Madrid con Private Google Access habilitado
# Note: El acceso privado permite que VMs sin IP pública consuman servicios como Cloud Storage.
gcloud compute networks subnets create subred-segura-madrid \
    --network=red-segura-lab \
    --range=10.10.1.0/24 \
    --region=europe-southwest1 \
    --enable-private-ip-google-access
```

---

## 🛡️ Fase 2: El Firewall (Perímetro Zero Trust)

No abrimos el puerto 22 a `0.0.0.0/0`. Solo permitimos el tráfico que viene desde los proxies internos de Google.

```bash
# Crear regla de entrada para IAP
# Rango oficial de Google IAP: 35.235.240.0/20
gcloud compute firewall-rules create permitir-ssh-iap \
    --network=red-segura-lab \
    --allow=tcp:22 \
    --source-ranges=35.235.240.0/20 \
    --target-tags=permite-ssh \
    --description="Acceso exclusivo via IAP"
```

---

## 💻 Fase 3: Despliegue del Servidor Blindado

Creamos un servidor sin dirección IP externa. El aislamiento es nuestra primera capa de defensa.

```bash
gcloud compute instances create servidor-secreto \
    --zone=europe-southwest1-a \
    --network-interface=subnet=subred-segura-madrid,no-address \
    --tags=permite-ssh \
    --image-family=debian-12 \
    --image-project=debian-cloud \
    --metadata=enable-oslogin=TRUE
```

---

## 🕵️ Fase 4: Acceso y Auditoría

Para entrar al servidor, usaremos una identidad autenticada, no solo una llave SSH.

```bash
# Acceder mediante el túnel IAP
gcloud compute ssh servidor-secreto --tunnel-through-iap --zone=europe-southwest1-a
```

### Checks de Verificación (Dentro de la VM):
1.  **Aislamiento de Red:** `ip addr` (Verás que no hay interfaz con IP pública).
2.  **Tráfico de Salida:** `ping 8.8.8.8` (Debe fallar, garantizando que el servidor no puede ser usado para exfiltración directa).
3.  **API Access:** `gsutil ls` (Debe funcionar gracias al Private Google Access).

---

## 💡 Reflexión del Mentor (Tips de SysAdmin)

> [!TIP]
> **¿Por qué esto es mejor que una VPN?**
> Con IAP no necesitas mantener un túnel VPN complejo. Google verifica la identidad del usuario (IAM) antes de siquiera permitir que el paquete llegue al puerto 22 de tu VM. Es la base de la arquitectura **BeyondCorp**.

> [!WARNING]
> Recuerda que el **Private Google Access** solo funciona para servicios de Google (S3, BigQuery, etc.). Si tu servidor Linux necesita actualizar paquetes vía `apt-get`, necesitarás configurar un **Cloud NAT**.

---

## 📊 Tarea de Cierre: Evidencia
Genera el informe de seguridad de la regla de firewall creada:
```bash
gcloud compute firewall-rules describe permitir-ssh-iap --format="yaml(name,allowed,sourceRanges,targetTags)"
```

---

## 🧹 Limpieza de Recursos
```bash
gcloud compute networks delete red-segura-lab --quiet
```
