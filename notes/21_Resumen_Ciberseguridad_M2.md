### Informe de Seguridad Informática: Fundamentos y Estrategias de Protección

#### Resumen Ejecutivo

La ciberseguridad se define como el conjunto de técnicas diseñadas para proteger la  **secrecía, integridad y disponibilidad**  de los sistemas informáticos y los datos frente a amenazas externas. En un entorno donde las computadoras operan sin una ética inherente, la seguridad virtual actúa como el equivalente de las cerraduras y las fuerzas de seguridad en el mundo físico.Los pilares fundamentales de una estrategia de seguridad robusta incluyen el  **modelado de amenazas** , la implementación de sistemas de  **autenticación**  multifactorial y un  **control de acceso**  riguroso. Dado que no existe una garantía absoluta de que un software sea inexpugnable debido a errores de implementación, la industria se apoya en la minimización del código, la verificación independiente y el principio de  **aislamiento**  (sandboxing) para mitigar daños cuando ocurre un compromiso inevitable.

#### 1\. Los Objetivos Fundamentales: La Tríada de la Seguridad

La ciberseguridad busca proteger tres propiedades críticas de la información y los sistemas:| Propiedad | Definición | Ejemplo de Ataque || \------ | \------ | \------ || **Secrecía (Confidencialidad)** | Solo las personas autorizadas deben tener acceso a datos específicos. | Filtración de datos (brechas) de tarjetas de crédito. || **Integridad** | Solo las personas autorizadas deben poder modificar sistemas y datos. | Hackers que envían correos suplantando la identidad del usuario. || **Disponibilidad** | Los usuarios autorizados deben tener acceso constante a sus sistemas. | Ataques de Denegación de Servicio (DoS) que saturan un sitio web. |

#### 2\. Modelado de Amenazas y Vectores de Ataque

Antes de implementar medidas técnicas, los expertos deben definir un  **modelo de amenazas** . Este proceso perfila al "enemigo" a un nivel abstracto, evaluando sus capacidades, objetivos y los posibles medios que utilizará, conocidos como  **vectores de ataque** .

* **Dependencia del Contexto:**  La seguridad necesaria varía según el atacante. Proteger una computadora de un compañero de cuarto curioso requiere medidas distintas (como esconderla) que protegerla de un atacante con acceso físico ilimitado y tiempo infinito (que requeriría una caja fuerte).  
* **Supuestos de Seguridad:**  Los arquitectos de seguridad diseñan soluciones bajo ciertos supuestos, como el hecho de que el usuario no revelará voluntariamente sus credenciales.

#### 3\. Autenticación: Verificación de Identidad

La autenticación es el proceso mediante el cual una computadora identifica con quién está interactuando. Se clasifica en tres categorías principales:

##### A. Lo que sabes (Conocimiento)

Es el método más común (nombres de usuario y contraseñas).

* **Vulnerabilidades:**  Ataques de  **fuerza bruta** , donde una computadora prueba todas las combinaciones posibles en fracciones de segundo.  
* **Fortaleza Matemática:**  
* Un PIN de 4 dígitos tiene 10,000 combinaciones.  
* Una contraseña de 8 caracteres complejos tiene más de 600 billones de combinaciones.  
* Una frase de tres palabras aleatorias (ej. "pizza tasty yum") puede ofrecer hasta 1 cuatrillón de combinaciones.

##### B. Lo que tienes (Posesión)

Basado en un token físico o secreto (ej. una llave física o un smartphone).

* **Ventajas:**  Difícil de comprometer de forma remota; requiere presencia física.  
* **Riesgos:**  Pérdida, robo o duplicación física del objeto.

##### C. Lo que eres (Biometría)

Uso de características físicas como huellas dactilares o escaneos de iris.

* **Naturaleza Probabilística:**  A diferencia de los métodos anteriores, que son deterministas (funciona o no funciona), la biometría tiene un margen de error (falsos positivos o negativos).  
* **Limitaciones:**  No se pueden "restablecer" si los datos son robados. Además, investigaciones sugieren que el iris puede falsificarse mediante fotografías de alta resolución.**Recomendación Estratégica:**  Se recomienda el uso de  **autenticación de dos factores (2FA) o multifactor** , ya que es significativamente más difícil para un atacante comprometer dos categorías distintas simultáneamente.

#### 4\. Control de Acceso y Permisos

Una vez autenticado el usuario, el sistema debe determinar sus privilegios mediante Listas de Control de Acceso (ACL).

##### Tipos de Permisos

1. **Lectura (Read):**  Permite ver el contenido del archivo.  
2. **Escritura (Write):**  Permite modificar el contenido.  
3. **Ejecución (Execute):**  Permite correr un archivo como programa.

##### El Modelo Bell-LaPadula

Diseñado originalmente para el Departamento de Defensa de EE. UU., este modelo se basa en dos reglas críticas para evitar filtraciones en organizaciones con niveles de seguridad (Público, Secreto, Top Secret):

* **No leer hacia arriba (No read up):**  Un usuario con nivel "Secreto" no puede leer archivos "Top Secret".  
* **No escribir hacia abajo (No write down):**  Un usuario con nivel "Top Secret" no puede escribir en archivos de nivel "Secreto" o "Público", evitando la filtración accidental de información sensible a niveles inferiores.

#### 5\. Integridad del Sistema y Mitigación de Daños

La seguridad depende de la confianza en el hardware y el software. Sin embargo, no existe forma de garantizar que un sistema sea 100% seguro debido a errores de implementación (bugs).

##### Estrategias de Reducción de Riesgos

* **Minimización de Código:**  Cuanto menos código tenga un sistema, menor es la probabilidad de errores. El objetivo es crear un  **núcleo de seguridad**  o base de computación confiable que sea lo más pequeño posible.  
* **Verificación e Validación Independiente (IV\&V):**  El código de seguridad suele ser de código abierto para que auditores externos y la comunidad identifiquen vulnerabilidades que los autores originales pasaron por alto.  
* **Aislamiento y Sandboxing:**  El principio de aislamiento asume que el compromiso ocurrirá tarde o temprano. Mediante el "sandboxing", las aplicaciones se ejecutan en entornos restringidos. Si una aplicación es comprometida o falla, el daño se limita a su propio "cajón de arena" y no afecta al resto del sistema o a otras  **Máquinas Virtuales**  que corren de forma independiente.

#### Conclusiones Técnicas

La ciberseguridad es una disciplina en constante evolución que requiere un enfoque proactivo. Las medidas críticas inmediatas para cualquier usuario u organización incluyen el fortalecimiento de contraseñas mediante frases memorables largas, la activación de autenticación multifactor y la desconfianza sistemática hacia enlaces en correos electrónicos no solicitados.  
