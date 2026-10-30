# Laboratorio 03: Privacidad, cumplimiento y gobierno de los datos
#### Grupo: 4-3
#### Estudiante: Jesús Jared Recio Ozúa

# INFORME FINAL
### 1. Introducción
En este laboratorio, el principal problema abordado fue la privacidad y finalidad de los datos de los clientes. Se analizó qué datos sí son necesarios y por qué siempre se debe tener bien clara cuál es la finalidad de almacenarlos, para después revisar cómo es que se protegerán. También se estudió la importancia de las obligaciones de privacidad y por qué es importante que el DBA sepa identificar las implicaciones técnicas.

### 2. Inventario de datos
| Campo | ¿Es un dato personal? | Clasificación | Finalidad |
| :--- | :--- | :--- | :--- |
| **id** | No | Identificador interno asignado por la BD | Identificar y organizar los registros de clientes |
| **nombre** | Sí | Identificador directo | Identificar al usuario, personalizar la atención y prevenir suplantación |
| **correo** | Sí | Identificador directo (único por persona) | Vía de contacto directo y seguimiento de soporte |
| **telefono** | Sí | Identificador directo (vinculado a una CURP) | Contacto directo para soporte |
| **rfc** | Sí | Dato fiscal identificable (iniciales y fecha de nacimiento) | Facturación y obligaciones tributarias |
| **edad** | Sí | Atributo no identificable por sí solo | Verificar mayoría de edad o fines estadísticos |
| **ciudad** | Sí | Dato de ubicación, no identificable por sí solo | Análisis demográfico y personalización de servicios |
| **codigo_postal** | Sí | Ubicación aproximada; junto con la ciudad es más precisa | Costos de envío, validación de dirección, cobertura del servicio |
| **fecha_alta** | No | Dato de registro del sistema | Registrar cuándo se dio de alta el usuario |

### 3. Finalidades
Los datos personales solo deben utilizarse para la finalidad por la que fueron almacenados. Que la organización ya tenga los datos no significa que pueda usarlos para cualquier otra cosa, ya que cuando se propone una finalidad nueva, como enviar promociones personalizadas según edad, ciudad y comportamiento de compra, se necesita el consentimiento del titular, tanto para usar sus datos con ese fin como para recibir las promociones.
En el inventario de datos de la actividad uno, se asignó una finalidad a cada campo:
* **id:** identificar y organizar los registros de clientes en la base de datos.
* **nombre:** identificar al usuario, verificar su identidad en solicitudes de soporte y prevenir suplantación.
* **correo y teléfono:** contacto directo con el cliente y seguimiento de casos de soporte.
* **rfc:** emisión de facturas y cumplimiento de obligaciones tributarias.
* **edad:** verificar mayoría de edad o fines estadísticos.
* **ciudad y código postal:** análisis demográfico, cobertura del servicio, costos de envío y logística.
* **fecha_alta:** registrar cuándo se dio de alta el usuario, para analítica y auditorías.

### 4. Minimización
El principio de minimización establece que los datos recopilados deben ser adecuados, pertinentes y limitados a lo estrictamente necesario para cumplir la finalidad del servicio.
* **Atención al cliente:** Para gestionar un ticket solo se necesitan el nombre, el correo, el teléfono y, si la empresa lo usa para llevar el registro, el id. El resto de los campos son innecesarios para esa función:
  * **RFC:** solo se requiere si el cliente solicita una factura o un trámite fiscal.
  * **Edad:** no es relevante para resolver un caso de soporte.
  * **Código postal:** depende de si hay envíos físicos, garantías o logística local, de lo contrario no se necesita.
* También eliminaría algunos datos como:
  * **Dirección:** es un dato de ubicación que no se justifica para el negocio.
  * **Fecha de nacimiento:** no se necesita la fecha exacta si se tiene la edad.
  * **Ocupación y estado civil:** no tienen relevancia para la operación ni para la analítica.
  * **Salario:** solo se conservaría si existe una justificación adicional, por ejemplo para estadísticas de ingresos y compras.

Para aplicar privacidad por defecto, la recopilación debe ser mínima, no se debe asumir que el usuario da permiso para finalidades distintas a la principal, y el acceso a datos personales debe limitarse a personal autorizado.

### 5. Control de acceso
Los permisos se otorgan de acuerdo con las funciones de cada área, de forma que cada rol vea únicamente lo que necesita para trabajar.
* **Rol analista:** no tiene permisos sobre la tabla base clientes. Sus privilegios son solo SELECT sobre la vista analítica y USAGE sobre el esquema. La vista no incluye columnas con datos identificables, por lo que desde ese rol es imposible obtener nombre, correo o RFC.
* **Rol de marketing:** no necesita acceso directo a clientes. Se le puede crear otra vista que contenga solo edad, correo y comportamiento de compra, con su propio rol, igual que en el caso del analista.
* **Soporte, facturación y logística:** acceden solo a los campos de su finalidad (por ejemplo, facturación al RFC y soporte a nombre, correo y teléfono).

### 6. Derechos ARCO
Cada derecho tiene implicaciones técnicas para el DBA:
* **Acceso:** Debe poder localizarse toda la información de una persona con una consulta que filtre por un identificador único (id o RFC), como un select que dé los datos del titular utilizando la cláusula where.
* **Rectificación:** El cambio puede verificarse con un SELECT, pero también debe cerrarse la solicitud (por ejemplo, el ticket de soporte donde el cliente pidió la corrección). Debe registrarse quién hizo el cambio, cuándo y por qué. Esta trazabilidad es esencial: si ocurre un error, hay que saber qué falló y quién es responsable de corregirlo.
* **Cancelación:** Eliminar un registro de una tabla no significa que la información haya desaparecido de la organización: pueden quedar copias en respaldos anteriores, réplicas de la base de datos, reportes y archivos. Por eso la eliminación debe contemplar todo el ciclo de vida del dato, incluyendo respaldos. Además, algunos datos (como los fiscales) deben conservarse durante el plazo legal.
* **Oposición:** Oponerse a un uso no implica borrar todos los datos. Debe seguir conservándose lo necesario para soporte y obligaciones fiscales (id, nombre, correo, teléfono y datos fiscales), y dejar de usarse lo asociado a la finalidad a la que el cliente se opuso (por ejemplo, correo y teléfono en listas de promociones, o edad, código postal y ciudad en análisis).

### 7. Retención
El periodo de conservación de los datos no debe fijarse de manera improvisada ni indefinida, porque conservar datos innecesarios contradice la minimización y genera riesgos: problemas legales y, ante un ataque o filtración, un impacto mucho mayor porque se expondría información incluso de personas que ya no tienen relación con la organización.
Para determinar el periodo, la organización debe:
1. Definir qué información se almacena y con qué finalidad.
2. Identificar las leyes y marcos normativos que obligan a conservarla.
3. Documentar la justificación del periodo seleccionado: finalidad, fundamento legal, ciclo de vida del dato, cómo se protegerá mientras se almacene y cómo se eliminará cuando ya no sea necesario.

### 8. Gobierno de datos
| Dato | Finalidad | Responsable | Usuarios autorizados | Protección | Retención | Acción al finalizar |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **nombre** | Identificación del titular para atención de solicitudes y gestión de tickets | Atención al cliente | Atención al cliente, DBA, Dirección | Cifrado en reposo/tránsito, RBAC | Mientras la cuenta esté activa + 1 año | Borrado seguro o desvinculación |
| **correo** | Vía de contacto y notificaciones operativas | Atención al cliente | Atención al cliente, DBA | Cifrado TLS, enmascaramiento en vistas | Durante la vigencia de la cuenta | Eliminar de listas de contacto |
| **telefono** | Verificación de seguridad y contacto directo | Atención al cliente | Atención al cliente, DBA | Cifrado y visibilidad limitada | Mientras la cuenta esté activa | Borrado definitivo |
| **rfc** | Hacer facturas válidas | Facturación | Contabilidad, DBA | Cifrado fuerte y acceso muy restringido | 5 años (mandato fiscal) | Depuración y borrado al vencer el plazo |
| **edad** | Sacar estadísticas y perfiles | Analítica | Analítica, DBA | Datos agregados o en rangos | Durante los estudios estadísticos | Resumen anónimo final |
| **ciudad** | Ubicación general y soporte regional | Atención al cliente | Soporte, Logística, DBA | Vistas operativas controladas | Hasta que termine el servicio | Anonimización |
| **codigo_postal** | Calcular envíos y cobertura | Logística | Logística, DBA | Datos seguros para uso logístico | Durante las entregas activas | Limpieza estadística |

### 9. Evaluación integral
| # | Problema | Principio afectado | Riesgo | Control propuesto |
| :-: | :--- | :--- | :--- | :--- |
| **1** | Analítica consulta directamente la tabla clientes | Responsabilidad / Mínimo Privilegio | Acceso innecesario a datos personales, uso indebido | Control de acceso basado en roles (RBAC) y vistas |
| **2** | Analítica genera estadísticas pero accede a datos identificables | Minimización | Se utilizan más datos de los necesarios | Entregar vistas con datos estrictamente necesarios |
| **3** | Datos conservados por 12 años sin regla de borrado | Limitación del plazo de conservación | Almacenamiento innecesario, mayor superficie de exposición | Definir plazos de conservación y purga |
| **4** | No existe política documentada de retención | Responsabilidad | Incumplimiento normativo | Elaborar y aprobar política formal de retención |
| **5** | Desarrolladores reciben copias completas de producción | Minimización / Confidencialidad | Exposición de datos a personal que no los requiere | Proveer subconjuntos de datos o entornos sintéticos |
| **6** | Copias de desarrollo contienen datos reales | Seguridad / Finalidad | Entornos menos protegidos, mayor riesgo de filtración | Anonimización o enmascaramiento |
| **7** | Marketing usa correos sin evidencia de consentimiento | Consentimiento | Uso para un fin distinto, sanciones y quejas | Registrar y auditar el consentimiento (*opt-in*) |
| **8** | No hay documentación clara de la finalidad de cada dato | Finalidad / Transparencia | No poder justificar por qué se recopila la información | Crear inventario de datos y avisos de privacidad |
| **9** | Todos los datos concentrados en una sola tabla | Seguridad por diseño | Una sola filtración compromete toda la identidad | Arquitectura segregada (operativa, analítica, auditoría) |
| **10** | Sin trazabilidad de quién consulta o copia los datos | Responsabilidad / Seguridad | Imposibilidad de detectar accesos indebidos | Activar bitácoras de auditoría y monitoreo |

### 10. Conclusiones
En este laboratorio aprendí que privacidad, seguridad y administración de bases de datos están estrechamente relacionadas, pero no son lo mismo. La privacidad define qué datos se pueden recopilar, para qué y por cuánto tiempo (finalidad, minimización, consentimiento, retención). La seguridad proporciona los mecanismos para proteger esos datos (mínimo privilegio, cifrado, enmascaramiento, auditoría). La administración de bases de datos es donde ambas se unen: el DBA traduce principios en roles, vistas, banderas de consentimiento, procesos de borrado y bitácoras.
También aprendí que el DBA no puede ni debe decidir solo. Tomar decisiones como definir cuánto tiempo conservar un dato, atender una oposición o eliminar información requiere la participación de las áreas de negocio, el área legal y el titular, y todo debe quedar documentado.
Finalmente, entendí que diseñar con privacidad desde el inicio es más efectivo y económico que corregir después: recopilar lo mínimo, separar los datos por finalidad, limitar los accesos y documentar cada decisión reduce drásticamente el impacto de una brecha.

---

### PREGUNTAS DE REFLEXIÓN
**1. ¿Una base de datos técnicamente segura necesariamente cumple con todos los requisitos de privacidad?**
No, ya que una base de datos puede estar configurada para ser segura a nivel técnico, pero si los datos dentro de ella no se tratan de manera correcta (por ejemplo, si se almacena información excesiva que no es necesaria), no cumple con los principios de privacidad. No se trata solo de configuraciones de seguridad, sino de buenas prácticas de gobierno de datos.

**2. ¿Por qué el principio de mínimo privilegio también contribuye a la privacidad?**
Contribuye porque evita que los datos personales estén expuestos a todas las personas de la organización, permitiendo que únicamente accedan a ellos quienes realmente los necesitan para cumplir con sus funciones laborales.

**3. ¿Por qué el DBA no debería decidir por sí solo la finalidad del tratamiento de los datos?**
Porque el DBA domina la parte técnica (cómo almacenar, proteger y consultar los datos), pero no necesariamente el negocio, las obligaciones legales ni lo que el titular autorizó en el aviso de privacidad.

**4. ¿Por qué los desarrolladores no deberían recibir automáticamente copias completas de bases de datos productivas?**
Porque los desarrolladores no necesitan los datos reales de todos los clientes para programar o probar. Entregar bases productivas reales contradice la minimización y el mínimo privilegio, exponiendo información sensible a personal que no lo requiere.

**5. ¿Por qué una copia utilizada para desarrollo también puede representar un riesgo de privacidad?**
Porque una copia con datos reales sigue conteniendo información personal, pero por lo general se aloja en entornos menos blindados que producción (menores controles, sin auditoría constante y con acceso a más personas), lo que dispara la probabilidad de una filtración.

**6. ¿Por qué la retención debe formar parte del ciclo de vida de los datos?**
Porque los datos no deben existir indefinidamente; tienen un inicio (recolección), un uso, un almacenamiento y un final (eliminación, anonimización o agregación). Si la retención no se define de antemano, los datos se acumulan sin justificación, lo que vulnera la minimización y eleva el riesgo ante incidentes.

**7. ¿Qué relación existe entre privacidad por diseño y diseño de bases de datos?**
La privacidad por diseño implica incorporar la protección de datos desde la concepción del sistema y no como un parche posterior. En las bases de datos se refleja en decisiones estructurales: evitar columnas innecesarias, guardar rangos de edad en lugar de fechas exactas, segregar datos por finalidad, crear vistas y roles desde el inicio, y prever mecanismos de consentimiento y retención.

**8. ¿Qué controles técnicos implementarías para reducir el riesgo de exposición de datos personales?**
Implementaría control de acceso basado en roles (RBAC), vistas limitadas por finalidad, cifrado de datos en reposo y tránsito, enmascaramiento dinámico y seudonimización.

**9. ¿Qué información debería conocer un DBA para responder técnicamente a una solicitud ARCO?**
Debe saber ubicar dónde están los datos del titular, con qué identificador se rastrean, confirmar que la identidad fue validada, identificar qué derecho se ejerce (acceso, rectificación, cancelación u oposición), conocer la finalidad asociada a cada dato y verificar si existe consentimiento registrado.

**10. qué responsabilidades deberían corresponder al DBA, al responsable de privacidad, al área jurídica y al propietario de los datos?**
* **DBA:** Implementar los controles técnicos (roles, vistas, cifrado, bitácoras), ejecutar técnicamente las solicitudes ARCO, respaldar y eliminar de forma segura, y mantener la trazabilidad.
* **Área jurídica:** Identificar las normativas y plazos legales aplicables, validar los periodos de retención y evaluar el riesgo normativo de cada tratamiento.
* **Propietario de los datos (Data Owner):** Definir para qué se requiere cada dato, quiénes deben usarlo, aprobar los accesos de su área y justificar la finalidad y el tiempo de conservación.