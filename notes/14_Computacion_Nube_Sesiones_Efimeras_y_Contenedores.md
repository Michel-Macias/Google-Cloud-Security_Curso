# ☁️ Computación en la Nube: Sesiones Efímeras, Virtualización y Contenedores

Este documento consolida los conceptos del **Módulo 01** relacionados con la arquitectura computacional en la nube y su impacto directo en la ciberseguridad.

---

## ⏳ 1. Sesiones Efímeras y Recursos de la Nube

En la seguridad tradicional, las sesiones y los servidores tienen tiempos de vida largos (meses o años), lo que da a los atacantes una ventaja para establecer persistencia. La nube introduce el concepto vital de la **Efimeralidad**.

*   **Sesiones Efímeras (Identidad):** En lugar de usar claves estáticas (como contraseñas persistentes o *Service Account Keys* de larga duración), se priorizan las **credenciales de corta duración** (*Short-lived credentials*). Ej: Un token OAuth2 que expira automáticamente en 1 hora. Si este token es interceptado, su ventana de utilidad para el atacante es mínima.
*   **Recursos Efímeros (Infraestructura):** Uso de máquinas virtuales *Spot* (o *Preemptible* en GCP) y contenedores que nacen para una tarea corta y son destruidos posteriormente.
    *   *Ventaja de Seguridad:* Destruye el concepto de "persistencia" del atacante, fundamental en las Amenazas Persistentes Avanzadas (APT). Un atacante no puede instalar un malware residente en un servidor que es destruido y recreado desde cero cada 24 horas.

---

## 🖥️ 2. Virtualización y Máquinas Virtuales (VMs)

La virtualización es el bloque fundacional de la Nube (IaaS). Permite correr múltiples máquinas virtuales sobre un mismo hardware físico, separadas por una capa de software llamada **Hypervisor** (ej. KVM).

*   **Aislamiento de Hardware:** El hypervisor engaña a la VM haciéndole creer que tiene hardware dedicado de forma exclusiva. Si una VM es comprometida, el atacante queda encapsulado en ese entorno (salvo raras vulnerabilidades conocidas como *VM Escape*, las cuales los proveedores suelen parchear de inmediato).
*   **Seguridad Avanzada en VMs de Nube (Ej. Shielded VMs en GCP):**
    *   **Arranque Seguro (Secure Boot):** Verifica criptográficamente que el firmware y el sistema operativo no hayan sido alterados al arrancar, previniendo infecciones de muy bajo nivel (Rootkits o Bootkits).
    *   **vTPM (Virtual Trusted Platform Module):** Protege y aísla en memoria las claves criptográficas y secretos transaccionales.
    *   **Confidential Computing:** Un paradigma superior que cifra los datos no solo en reposo o en tránsito, sino también *en uso* (en la memoria RAM y CPU), protegiéndolos incluso de ataques internos o del propio proveedor de la nube.

---

## 📦 3. Creación de Contenedores

Los contenedores empaquetan una aplicación junto con sus librerías esenciales, corriendo directamente sobre el núcleo (Kernel) del Sistema Operativo anfitrión. Se separan gracias a tecnologías de Linux como `namespaces` (aislamiento de red/procesos) y `cgroups` (límites de CPU/RAM).

*   **Seguridad al Crear Contenedores (Fase Build):**
    *   **Imágenes Mínimas (Distroless / Alpine):** Empaquetar el contenedor con *solo* los binarios necesarios de la aplicación. No se deben incluir shells (`/bin/sh`, `/bin/bash`) ni utilidades como `curl` o `wget`. Si un atacante logra ejecución de código remota (RCE), no tendrá herramientas para descargar su malware o moverse por el sistema.
    *   **Principio de Menor Privilegio (No Root):** Por defecto, los contenedores tienden a correr como administrador (`root`). Dentro del `Dockerfile`, se debe especificar la creación y el uso de un usuario sin privilegios para mitigar el escalado (ej. instrucción `USER appuser`).
    *   **Escaneo de Vulnerabilidades Continuo:** Mandatoriedad de analizar imágenes en artefactos repotisorios (como *Artifact Registry*) buscando vulnerabilidades conocidas (CVEs) antes de permitir su despliegue en clústeres de Producción.

---

## ⚡ 4. Serverless (Cloud Functions / Cloud Run)

*Nota: La perspectiva de casos de uso fue contemplada en la sección introductoria (`13_Casos_Uso...`), pero este pilar es fundamental desde la óptica de seguridad del Módulo 01.*

En el escenario "Sin Servidor", el proveedor de la nube abstrae completamente la infraestructura. Tú solo entregas tu código o tu contenedor; ellos gestionan el hardware, hipervisor, sistema operativo y el *runtime*.

*   **Reducción Drástica de Superficie y Responsabilidad:** La Modelo de Responsabilidad Compartida favorece inmensamente al cliente. Las tareas mundanas pero críticas, como parchear el sistema operativo a las 3:00 AM, pasan a ser carga del proveedor.
*   **Escalado a Cero (Zero Trust Inherent):** Las funciones Serverless solo se encienden al recibir un evento web, un log o una acción concreta. Al no existir un servidor encendido y escuchando el 100% del tiempo en un puerto de red, los escaneos perimetrales tradicionales de los atacantes fracasan; no hay blanco el cual apuntar de forma latente.

---

## 🧠 Reflexión del Mentor

Si analizas todo el **Módulo 01** desde una lente arquitectónica, notarás que la progresión de computación (Máquina Física -> Máquina Virtual -> Contenedor -> Serverless) no trata solo sobre "eficiencia de costos", sino sobre una profunda **Seguridad por Diseño**. 

Por cada peldaño que subimos en esta abstracción tecnológica, te deshaces de responsabilidades operativas riesgosas, acortas los tiempos de vida de los recursos para frustrar a los cibercriminales (la Efimeralidad) e invisibilizas gradualmente tus cargas de trabajo ante el exterior. Como tú y yo venimos del puro *SysAdmin*, es fundamental desaprender el instinto de querer "controlar y parchear a mano" y aprender a confiar en este encapsulamiento automático.
