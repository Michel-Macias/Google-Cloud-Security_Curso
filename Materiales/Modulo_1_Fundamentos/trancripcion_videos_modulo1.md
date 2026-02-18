00:00  
¡Hola\!  
00:01  
Te damos la bienvenida a la primera etapa del curso de seguridad cibernética en la nube.  
00:05  
Aquí explorarás los principios esenciales de seguridad en la computación en la nube.  
00:09  
Tendrás una descripción general del ciclo de vida de la seguridad e investigarás herramientas de Google Cloud, como la consola y Cloud Shell.  
00:16  
Conocerás DevSecOps, que significa desarrollo, seguridad y operaciones.  
00:22  
Esta metodología integra la seguridad en todo el ciclo de vida del desarrollo de software.  
00:28  
Por el camino, descubrirás cómo trasladar muchas de las habilidades que ya posees al campo de la seguridad en la nube.  
00:34  
Como resolución de problemas, colaboración pensamiento analítico y comunicación.  
00:42  
Uno de los aspectos que más me gusta es que la nube evoluciona junto con las  
00:44  
formas en las que su seguridad puede verse comprometida, por lo que estoy aprendiendo todo el tiempo.  
00:51  
¡Así que empecemos\!  
00:53  
Esta sección del programa es una introducción general a la computación en la nube y la infraestructura de nube.  
00:58  
Examinarás cómo funcionan la virtualización, los contenedores y el almacenamiento en la computación en la nube.  
01:05  
Fortalecerás tus defensas en la nube con controles de seguridad, administración de identidades y accesos, y prácticas de red.  
01:13  
Descubrirás cómo los proveedores de servicios y los usuarios comparten la responsabilidad de la seguridad en modelos como la plataforma como servicio, infraestructura y software.  
01:23  
A continuación, analizarás la automatización en el ciclo de vida de la seguridad.  
01:26  
Aprenderás sobre equipos y flujos de trabajo, el papel de la automatización en las canalizaciones de software y la infraestructura como código.  
01:33  
Además, explorarás la cadena de suministro de software y la importancia de protegerla.  
01:38  
En resumen, explorarás las responsabilidades, habilidades y herramientas de seguridad cibernética en la nube.  
01:45  
Conocerás Google Cloud Shell y agregarás muchas soluciones tecnológicas a tu caja de herramientas de seguridad en la nube.  
01:50  
Estoy aquí para ayudarte en cada paso.  
01:53  
Recurda que tú marcas el ritmo.  
01:56  
Cuando todo esté listo, pasa al siguiente tema.

00:00  
Cuando se aprende una habilidad especial, es útil comprender los conceptos básicos.  
00:03  
En primer lugar, no intentes surfear las olas antes de saber nadar.  
00:07  
Nos sumergiremos primero en los conceptos fundamentales de la computación en la nube, así puedes adquirir  
00:11  
los conocimientos necesarios para tener éxito en este programa y surfear algunas olas en tu futura carrera.  
00:17  
Empezarás con una descripción general de la infraestructura de nube.  
00:20  
Analizarás las estrategias clave a la hora de migrar a la nube.  
00:23  
Revisarás los componentes de la computación en la nube y aprenderás cómo mejora el enfoque tradicional en las instalaciones.  
00:30  
Aprenderás sobre contenedores y sus aplicaciones en la nube, además de cómo ayudan a implementar paquetes de software más ágiles y portátiles.  
00:39  
Por último, verás opciones de almacenamiento en la nube según el tipo de datos.  
00:44  
Cuando tengas todo listo, empezamos.

00:00  
Gracias a la nube, podemos interactuar con los datos casi en cualquier lugar y momento, ya  
00:06  
sea para consultar el clima y ver si necesitamos un abrigo o transmitir nuestro podcast favorito.  
00:10  
Puede parecer magia, pero almacenar tantos datos (y mantenerlos organizados) requiere infraestructura.  
00:16  
Los datos ya existían antes de la nube y debían almacenarse, así que veamos dónde empezamos antes de ver hacia dónde vamos.  
00:24  
Antes, las organizaciones guardaban sus datos en grandes infraestructuras físicas, por lo general, locales.  
00:31  
“Local” hace referencia la infraestructura de tecnología de la información que se encuentra físicamente en el propio centro de datos  
00:40  
u oficina de una organización Es decir, la organización administra sus propios servidores, redes y almacenamiento para ejecutar y almacenar datos.  
00:47  
Ahora bien, la nube usa estas estructuras físicas para ejecutarse.  
00:50  
Toda la información que contiene está alojada en un proveedor de servicios en la nube, conocido como CSP.  
00:56  
Estos proveedores almacenan los recursos de la nube en centros de datos.  
01:00  
Un centro de datos es un edificio físico que almacena servidores, sistemas informáticos y componentes asociados; una ubicación centralizada para incontables datos.  
01:10  
Los servidores de los centros de datos brindan potencia de procesamiento a la nube.  
01:14  
Los cables conectan a las máquinas, y estas a otros centros de datos del área.  
01:19  
Esto se denomina zona.  
01:20  
Una zona es el conjunto de centros de datos de un área.  
01:24  
Una zona puede contener uno o varios centros de datos.  
01:28  
Y una región es un grupo de zonas.  
01:30  
Google Cloud tiene muchas regiones en todo el mundo y sigue creciendo.  
01:34  
Google Cloud llama dominios con fallas a los grupos de zonas y regiones.  
01:38  
Estos dominios son recursos que pueden fallar sin afectar la disponibilidad de los datos.  
01:44  
Incluyen zonas y regiones donde los datos se replican para mejorar la resiliencia.  
01:49  
La resiliencia es la capacidad de prepararse, responder y recuperarse de interrupciones.  
01:55  
Tener los datos en estos dominios es la manera de los proveedores de servicios de proteger los datos de los usuarios.  
02:00  
Veamos un ejemplo: Eres un profesional de seguridad cibernética y tu organización usa recursos en la nube en una zona de la costa de Australia.  
02:09  
Un día estás trabajando y se produce una interrupción de energía en el centro de datos en tu zona.  
02:14  
Pero todo está bien. Tu trabajo está a salvo porque seleccionaste servicios de tu CSP que replican tus recursos en otros dominios con fallas.  
02:23  
Tener varias copias de los datos en distintas ubicaciones para evitar un punto único de fallo se conoce como redundancia.  
02:30  
La redundancia garantiza que tus datos estén disponibles cuando los necesites.  
02:34  
Muy bien, ahora ya sabes dónde se guardan los datos en la nube.  
02:37  
Pero ¿cómo se almacenan?  
02:39  
Y aún más importante, ¿con qué rapidez se puede acceder a los datos almacenados?  
02:43  
Con una cantidad tan grande de información que se genera cada segundo, el acceso rápido es esencial.  
02:49  
Este concepto se denomina latencia.  
02:52  
La latencia es el tiempo que tardan los datos en viajar de una ubicación a otra.  
02:57  
Ya sea desde el dispositivo de un usuario a un servidor en la nube o entre servidores.  
03:02  
Por ejemplo, cuando estás en un sitio web, cuanto menor sea la latencia, más rápido cargará la página web.  
03:07  
Los estudios muestran que el 53% de los usuarios abandonan las páginas que no cargan en tres segundos.  
03:12  
Yo pertenezco a ese 53%, que conste.  
03:16  
Así que los CSP se esfuerzan por ofrecer una baja latencia.  
03:20  
La latencia, redundancia y la infraestructura subyacente tienen el potencial de mejorar de forma significativa el compromiso de una organización con sus usuarios.  
03:29  
Es más, estos beneficios contribuyen a la transformación digital de una organización.  
03:34  
Esta transformación se produce cuando una organización moderniza sus aplicaciones, servicios y relaciones con los clientes con nuevas tecnologías.  
03:42  
La capacidad para escalar y replicar datos globalmente de la nube permite brindar una mejor experiencia del usuario no solo a empleados, sino también a clientes.  
03:51  
Como profesional de seguridad en la nube, será de vital importancia que comprendas cómo funciona la infraestructura de nube.  
03:57  
Una vez que conozcas estos componentes, tu aprendizaje sobre la nube estará en marcha.  
04:02  
Aquí no hay latencia.

00:00  
La nube brinda variedades de infraestructura denominadas modelos de implementación.  
00:04  
Veamos las distintas opciones que tienen los usuarios para aprovechar la potencia de la computación en la nube.  
00:10  
El modelo de implementación es importante para la infraestructura de nube.  
00:13  
Hay tres opciones principales: pública, privada e híbrida.  
00:19  
La nube pública es un modelo que proporciona recursos informáticos, de almacenamiento y de red en Internet  
00:25  
y permite a los usuarios compartir recursos en función de sus necesidades empresariales y objetivos operativos específicos.  
00:32  
Así, la infraestructura y los recursos del CSP se comparten en un entorno multiusuario con otros usuarios.  
00:38  
Un entorno multiusuario es aquel en el que la infraestructura y los recursos de nube se comparten entre usuarios.  
00:45  
Nunca sabes quién comparte tu espacio en el centro de datos.  
00:48  
Aunque compartas recursos, los otros usuarios no pueden acceder a tus datos.  
00:52  
La privacidad es importante.  
00:53  
La nube privada es un modelo en el que todos los recursos de la nube se dedican  
00:58  
a un único usuario u organización y se crean, administran y poseen en centros de datos locales.  
01:05  
Además, se dedican todos los recursos de la nube a un único usuario u organización.  
01:11  
Posee la infraestructura subyacente, en su propio centro de datos, pero usa un CSP.  
01:17  
Como la infraestructura y los recursos están dedicados a este único usuario, la nube privada es un entorno de usuario único.  
01:24  
En este tipo de entorno la infraestructura y los recursos de nube se dedican a un único usuario.  
01:31  
Este modelo es útil para empresas con cuestiones de cumplimiento o reglamentarias.  
01:37  
La nube privada es como ser dueño, y la pública es como alquilar.  
01:42  
Una empresa individual es responsable del mantenimiento y las reparaciones.  
01:46  
El propietario tiene la flexibilidad para renovar o hacer cambios estructurales, como agregar una nueva cocina.  
01:52  
Del mismo modo, en la nube privada la empresa tiene la responsabilidad y el control de los recursos y la infraestructura.  
02:00  
Cuando una empresa alquila oficinas, es probable que deba atenerse al plano acttual y no pueda hacer cambios  
02:05  
estructurales, es la empresa de administración quien se encarga del mantenimiento general, como la electricidad, calefacción y refrigeración.  
02:15  
Tal vez esos gastos estén incluidos en el alquiler, pero la empresa no es responsable del mantenimiento.  
02:20  
Así, en la nube pública, se paga CSP por el uso y mantenimiento de los recursos La nube híbrida es un modelo de nube que combina modelos  
02:26  
públicos y privados para que las organizaciones disfruten tanto de los servicios de la nube como de las funciones de control de los modelos de nube local.  
02:37  
Permiten agregar a la infraestructura local un proveedor de servicios en la nube pública para aumentar la potencia de procesamiento sin agregar gastos del centro de datos.  
02:46  
Como los usuarios eligen la ubicación de sus aplicaciones y del procesamiento, hay grandes ventajas en seguridad y cumplimiento.  
02:54  
Una nube híbrida es como una unidad de almacenamiento que brinda más espacio a las empresas sin que estas deban realizar ampliaciones o traslados.  
03:02  
Como los usuarios consumen cada vez más recursos en la nube, surgió el modelo de implementación de múltiples nubes.  
03:09  
Este modelo es una estrategia en la que usan más de un proveedor de servicios en la nube.  
03:12  
Por ejemplo, se puede usar el servicio Gmail de Google como correo electrónico corporativo y otro proveedor para almacenar datos.  
03:20  
Tanto si tu empresa elige un modelo público, privado, híbrido o de múltiples nubes, todos brindan formas innovadoras de avanzar y proteger los recursos informáticos.

00:00  
Todos los usuarios de computadora, en algún momento, tienen problemas con la velocidad, rendimiento o almacenamiento.  
00:07  
Quizá te compraste una laptop, pero cada vez tarda más en cargarse por falta de espacio en el disco duro.  
00:13  
O quizá tu computadora de escritorio tiene mucha memoria, pero con el tiempo, no puedes agregar la app que quieres porque el equipo no es compatible.  
00:20  
Bueno, la nube puede ayudarte con estas y muchas otras limitaciones relacionadas con el almacenamiento local de tus datos, software y hardware.  
00:28  
Y eso es precisamente lo que exploraremos en este video.  
00:31  
Hablaremos de las cinco ventajas principales de la nube: tiempo de salida al mercado, escalabilidad, colaboración, ahorro de costos y seguridad.  
00:35  
La primera ventaja es el tiempo de salida al mercado.  
00:38  
Tu organización, con computación en la nube, no perderá tiempo, energía, dinero en comprar un hardware, instalarlo, configurarlo o tener un diagnóstico de problemas.  
00:50  
Crear infraestructuras más rápido permite que las nuevas aplicaciones lleguen mucho más rápido a los consumidores.  
00:57  
La segunda ventaja es la escalabilidad.  
01:00  
En un entorno local, el número de dispositivos de almacenamiento varía por la demanda de datos.  
01:06  
El equipo de seguridad agregará dispositivos nuevos que administren los datos crecientes.  
01:10  
Cuando estos dispositivos dejan de ser necesarios, deberá encontrarles otro uso porque no los pueden devolver al proveedor.  
01:17  
Pero con la nube, los recursos se adaptan automáticamente a la carga de trabajo, lo que ahorra tiempo, esfuerzo y dinero.  
01:23  
Al igual que el tiempo de salida al mercado y la escalabilidad pueden reducir gastos, el cambio a la nube en sí mismo también.  
01:31  
Si se usa una solución local, la empresa es responsable del costo del hardware físico, el personal, el centro de datos y las cuotas de mantenimiento y servicio.  
01:43  
Este marco de trabajo se denomina gasto de capital, CapEx.  
01:46  
La nube sigue un modelo de gastos operativos, OpEx.  
01:51  
Con OpEx solo pagas los recursos que usas.  
01:54  
Genial, ¿verdad?  
01:55  
El CSP paga los equipos y espacios físicos, como servidores, dispositivos de red y centros de datos por adelantado.  
02:03  
Y con tantos usuarios, compartir los recursos de la nube reduce el precio para todos.  
02:08  
Veamos la ventaja de una mejor colaboración.  
02:12  
Con la nube, las empresas no necesitan una conexión directa a recursos físicos para acceder a sus datos.  
02:18  
Con solo una conexión a Internet, pueden acceder desde cualquier parte del mundo.  
02:22  
Así, los equipos distribuidos por todo el mundo colaboran de forma fácil y eficaz.  
02:27  
Otra ventaja fundamental es la amplia capacidad de seguridad de la nube.  
02:31  
Y aquí es donde brillan los profesionales de la seguridad cibernética en la nube.  
02:36  
Ellos saben cómo garantizar la integridad, confidencialidad y disponibilidad de datos, infraestructura y aplicaciones basadas en la nube.  
02:44  
Trabajan duro para impedir el acceso no autorizado o la explotación delictiva.  
02:50  
Mantiene los recursos en la nube seguros y protegidos.  
02:53  
La nube ayuda a evitar daños en los recursos y la información de la empresa.  
02:57  
Y previene pérdidas de datos: la redundancia garantiza que la información se replique en los dominios con fallas.  
03:04  
Recuerda que la redundancia es la práctica de distribuir recursos de la nube entre zonas y regiones.  
03:09  
Aunque el uso de la nube tiene muchas ventajas, no es perfecta.  
03:14  
Los profesionales de seguridad cibernética deben reconocer sus limitaciones.  
03:19  
La dependencia de una conexión estable a Internet es fundamental.  
03:23  
En algunos casos, la conexión de red de un CSP puede verse comprometida.  
03:28  
Los usuarios, en consecuencia, esperan más para acceder a sus recursos en la nube.  
03:32  
La buena noticia es que los CSP pueden mitigar el problema con múltiples conexiones a Internet para cada ubicación de la nube.  
03:39  
La tecnología se desarrolla a la velocidad de la luz y la nube ofrece ventajas claves que permiten aprovechar al máximo estas increíbles innovaciones.  
03:48  
Como profesional de seguridad, tu papel será ayudar a tu futuro empleador a avanzar en sus operaciones,  
03:53  
escalar rápido, adaptarse a los cambios del mercado, minimizar costos y aumentar la seguridad de los datos.  
04:00  
Estas son algunas formas de aportar mucho valor a la organización en la que trabajes.

