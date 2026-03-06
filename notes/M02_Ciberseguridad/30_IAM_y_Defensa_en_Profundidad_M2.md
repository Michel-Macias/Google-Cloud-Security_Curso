# 🔐 IAM y su Relación con la Defensa en Profundidad en la Nube

> **Módulo 02:** IAM en la nube y Estrategias Defensivas.
> **Material de Referencia:** Documentación oficial "IAM en la nube" (`IAM_en_la_nube.pdf`).

La transición desde infraestructuras locales (On-Premise) a la arquitectura de Nube Pública ha modificado radicalmente las reglas de combate y diseño en ciberseguridad. En sistemas tradicionales, el cortafuegos (firewall) perimetral y el aislamiento de subredes eran los reyes indiscutibles. En la nube, donde la movilidad es máxima y muchos servicios son expuestos mediante APIs públicas por diseño, **la Identidad se ha convertido en el nuevo y único perímetro real**.

Esta evolución técnica posiciona a la Gestión de Identidad y Accesos (IAM - Identity and Access Management) como el eslabón de control absolutamente vital dentro de la estrategia de **Defensa en Profundidad (Defense in Depth)**. 

---

## 🛡️ ¿Cómo encaja IAM en la Defensa en Profundidad?

El modelo clásico de Defensa en Profundidad dictamina que la ciberseguridad no puede depender de un único punto o barrera de fallo. Se apoya en una superposición de controles técnicos defensivos concéntricos a múltiples niveles (Perímetro, Red, Host, Aplicación y Datos). Las políticas IAM intersectan y gobiernan varias de estas capas neurálgicas de forma simultánea:

1.  **Capa Frontal (El Nuevo Perímetro):** El firewall tradicional no detendrá nunca a un atacante que se presenta con credenciales perfectamente válidas. IAM asume la vanguardia absoluta; si el control de IAM es frágil (ej. contraseñas débiles, ausencia de doble factor de autenticación y asignación de permisos excesivos), el atacante puentea transparentemente toda infraestructura de segmentación de red.
2.  **Capa de Aplicación y Host (Cuentas de Servicio):** Los componentes de software modernos (como máquinas virtuales, Kubernetes o funciones Serverless) no confían en la red, sino que tienen su propia identidad criptográfica administrada por IAM, determinando al detalle atómico qué otros microservicios pueden interrogar.
3.  **Capa del Dato (El Core):** IAM actúa como la última muralla de castillo antes de tocar el dato bruto. Incluso si una máquina virtual IaaS fuera comprometida maliciosamente obteniendo acceso nivel `root`, si la identidad IAM de esa máquina carece de permiso para leer el Bucket S3 / Cloud Storage confidencial, la exfiltración del dato falla inexorablemente.

---

## 👥 Principios de Control de Acceso IAM (Teoría Aplicada)

Para estructurar este anillo defensivo, los CSP (Proveedores de Servicios en la Nube como Google Cloud) operan sobre entidades organizativas estrictas para controlar recursos. 

### 1. Principales (Identidades)
El término agrupa y formaliza a las entidades capaces de consumir permisos y solicitar accesos a recursos. A estos usuarios o aplicaciones se les asignan **Roles** (que son a su vez colecciones predefinidas de distintos **Permisos** p.ej: `storage.objects.get`).

### 2. Grupos de Seguridad: El Estándar de Menor Privilegio
Asignar permisos a usuarios inviduales o singulares dentro de arquitecturas complejas es un antipatrón de diseño de extrema severidad. Se impone el uso innegociable de **Grupos**.
*   **Prevención de Extralimitación (Over-permission):** Los grupos blindan contra errores humanos y solucionan la retención de privilegios cuando empleados cambian de departamento garantizando que sólo un conjunto empaquetado y estricto reciba la menor cantidad de autorizaciones exigidas a la labor actual.
*   **Superficie de Ataque Reducida:** Si se concede algo al individuo fuera de grupo, su eventual exposición arrastra todo el ecosistema con él.

### 3. Cuentas de Servicio (El IAM No Humano)
Las cuentas de servicio son identidades lógicas generadas explícitamente y asociadas a las cargas de trabajo robóticas, microservicios y *PaaS*. 
*   **Aislamiento Lateral:** Limitan catastróficos pivotes maliciosos. Si un atacante compromete a través de un inyección un servidor web (`webapp-service-account`), el atacante asume únicamente el alcance limitado definido por su cuenta de servicio, bloqueándose al instante en la estructura profunda sin impacto del resto del entorno.

---

## 🔗 Federación de Identidades y Confianza (Zero Trust)

La **Federación** es el sistema donde se otorgan y verifican accesos de identidades externas al entorno de nube validando la legitimidad mediante un sistema intermedio de aserción técnica (SSO). Es una piedra de toque técnica sumamente avanzada:

### Usos Prácticos en Defensa
1.  **Federación Humana (SSO de Proveedores o Partners):** Impide las malas praxis derivadas de forzar al equipo externo a crear usuarios locales "huérfanos" (que eventualmente quedarán activos sin despidos reportados o auditoría). Al centralizar credenciales (como los portales "*Iniciar sesión mediante Google* / Microsoft Entra ID") si el socio es despedido desde la central de su propia compañía y la federación se trunca, el acceso local expira sincronizadamente sin intervención del CSP.
2.  **Federación de Identidad por Carga de Trabajo (Workload Federation):** Históricamente las tareas que corrían desde local (On-Premise) subiendo elementos diarios a la nube requerían descargar e instalar largos y exponenciales `.json` (Claves de Servicios RSA generadas) estáticas que los ciberatacantes amaban descubrir. A través de este mecanismo se habilitan interacciones temporales o de corta duración intercambiando los tokens OIDC. Destruye vectores de intrusión suprimiendo la necesidad generalizada y endémica de contar con material sensible por tiempo indefinido.

### MFA sobre Federación
Aplicar Autenticación de Múltiples Factores (MFA) fortifica agresivamente el protocolo a base de obligar a que el robo pasivo o por intrusión social no sea útil si la variable física de token, *smartcard* biométrica no es físicamente robada de manera simultanea para re-autenticarse.

---

## 🧠 Reflexión del Mentor
Un técnico tradicional de ciberespacio gasta todo su tiempo administrando subredes `/24` e inyectando listas negras en los IPS. Hoy, sin desprestigiar a nuestra arquitectura de conectividad, debes entender el peso gravitatorio abisal de esta lección:  **Las políticas y evaluaciones del IAM configuran el armazón atómico, indivisible y fundacional de la Nube Actual**. 
Cualquier falla en los cortafuegos es contingente, pero regalar el Rol `Owner / Propietario` a entidades de grupo generalizado o desactivar MFA es literalmente el prólogo total, irrevocable de cualquier caída de la resiliencia en todo nuestro paradigma de seguridad y su defensa escalonada.
