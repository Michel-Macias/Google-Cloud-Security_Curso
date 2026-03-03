# Resumen de Conceptos Clave: Google Cloud Security (Módulos 1 y 4)

Este documento sintetiza la información clave para un **Analista SysAdmin de Ciberseguridad**, basada en los documentos oficiales de Google Cloud analizados.

---

## 🛡️ Módulo 1: Infraestructura de Confianza (The Foundation)

Google protege la nube desde el silicio hasta la capa de software. Como Analista, debes saber que no heredas "cajas negras", sino una cadena de confianza verificada.

### 1. Seguridad de Hardware y Arranque
*   **Chip Titan:** Hardware diseñado por Google que establece una **Raíz de Confianza (Root of Trust)**. Verifica que el servidor no haya sido manipulado físicamente.
*   **Arranque Seguro (Secure Boot):** Cada componente (firmware, kernel, SO) es verificado criptográficamente antes de ejecutarse. Si algo falla, el servidor no arranca.
*   **Identidad de Bajo Nivel:** Cada servidor tiene su propia identidad criptográfica, lo que impide ataques de suplantación en el centro de datos.

### 2. Modelo de Confianza Cero (Zero Trust)
*   La seguridad no se basa en estar "dentro de la red".
*   Cada comunicación entre servicios (RPC) debe estar **autenticada, autorizada y cifrada** de forma mutua e individual.

### 3. Seguridad Física y Humana
*   **Centros de Datos:** Seguridad multinivel (biometría, detectores de metales, vigilancia 24/7).
*   **Acceso de Ingenieros:** Uso obligatorio de llaves físicas (Security Keys) para prevenir phishing. El acceso a datos de clientes por parte de empleados es casi nulo y siempre auditado.

---

## 🌐 Módulo 4: Redes VPC (Seguridad Lógica)

Aquí es donde tú, como SysAdmin, tienes el control directo. La VPC es un recurso **global** con subredes **regionales**.

### 1. Control de Perímetro y Firewalls
*   **Firewalls Distribuidos:** No son "appliances" centrales; las reglas se aplican directamente a nivel de instancia.
*   **Etiquetas de Red (Network Tags):** Permiten agrupar instancias lógicamente (ej: `web`, `db`) y aplicar reglas a esos grupos sin depender de direcciones IP estáticas.
*   **Denegación por Defecto:** Al crear una red en modo personalizado, todo el tráfico está denegado hasta que tú crees las reglas explícitas.

### 2. Aislamiento y Conectividad Privada
*   **Acceso Privado a Google (Private Google Access):** permite que las máquinas **sin IP pública** se comuniquen con las APIs de Google (Storage, BigQuery, etc.). Esto reduce drásticamente la superficie de ataque.
*   **Modo Personalizado (Custom Mode):** Recomendado para producción. Te permite diseñar el direccionamiento IP de forma que cumpla con el principio de mínimo privilegio.

### 3. Conectividad Híbrida Segura
*   **Cloud VPN:** Tráfico cifrado (IPsec) entre tu oficina y la nube.
*   **Cloud Interconnect:** Conexión directa física para mayor ancho de banda y latencia baja, manteniendo el tráfico fuera de la internet pública.

---

## 💡 Resumen para el Analista
*   **Google se encarga de:** La seguridad física, el hardware, la infraestructura de arranque y el cifrado del disco.
*   **Tú te encargas de:** La gestión de Identidades (IAM), el endurecimiento (hardening) del sistema operativo Linux y la arquitectura de red segura (VPC y Firewalls).
