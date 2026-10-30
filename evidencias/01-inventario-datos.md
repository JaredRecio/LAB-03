# LABORATORIO 3: PRIVACIDAD Y CUMPLIMIENTO
#### Grupo: 4-3
#### Estudiante: Jesús Jared Recio Ozúa

# Actividad 1 — Inventario y finalidad de los datos
| Campo | ¿Es dato personal? | Finalidad | ¿Es necesario? | Nivel de acceso | Retención | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| **id** | No, es un número de control interno que genera el sistema automáticamente. | Ordenar y ubicar de forma rápida cada registro en la base de datos. | Sí, fundamental para llevar una buena organización técnica. | Sistema / Desarrolladores | Todo el tiempo que el sistema esté funcionando | 
| **nombre** | Sí, porque permite saber exactamente de qué persona se trata. | Reconocer al cliente y darle un trato más personalizado. | Sí, indispensable para verificar quién habla al pedir soporte o revisar cuentas. | Soporte / Ventas / Administración | Mientras la cuenta siga abierta + el tiempo que exija la ley | 
| **correo** | Sí, ya que es un canal directo y personal para comunicarse con alguien. | Enviar notificaciones, avisos y dar seguimiento a los reportes de los usuarios. | Sí, es la vía principal para estar en contacto con el cliente. | Soporte / Sistemas | Mientras la cuenta esté activa | 
| **telefono** | Sí, está ligado directamente a una persona física. | Poder llamar o mandar mensajes rápidos cuando se requiera soporte. | No es obligatorio del todo, se puede operar solo con el correo. | Soporte / Logística | Mientras el servicio siga vigente | 
| **rfc** | Sí, combina datos personales y claves de carácter tributario. | Elaborar facturas válidas y cumplir con las normas de hacienda. | Solo si el usuario pide explícitamente una factura de sus compras. | Administración / Contabilidad | 5 años (según las reglas fiscales establecidas) | 
| **edad** | Sí, es un dato demográfico que describe al usuario. | Conocer el perfil de la gente y hacer estadísticas generales. | No es estrictamente obligatorio para el funcionamiento diario. | Analítica | Hasta que el usuario cierre su cuenta | 
| **ciudad** | Sí, indica el lugar general donde vive la persona. | Ver en qué zonas hay más clientes y ajustar los servicios. | No es forzoso, depende de si la empresa vende por regiones. | Analítica / Ventas | Hasta que el usuario cierre su cuenta | 
| **codigo_postal** | Sí, delimita una zona geográfica específica. | Calcular costos de envío o checar si hay cobertura en esa área. | Solo si la empresa realiza entregas físicas a domicilio. | Logística / Facturación | Hasta que termine el proceso de entrega o pedido | 
| **fecha_alta** | No, es solo la marca de tiempo de cuándo se creó el registro. | Tener control interno de cuándo empezó a usar el sistema el usuario. | Sí, útil para métricas internas y revisiones técnicas. | Sistema / Auditoría | Permanente | 

# Actividad 2 — Principio de minimización
1. **¿Todos los campos son necesarios para atención al cliente?** Para nada. A soporte solo le importa cómo te llamas, tu correo y tu teléfono; lo demás está de más para resolver un problema técnico.
2. **¿Por qué soporte necesitaría conocer el RFC?** Únicamente si el cliente tiene un problema directo con su factura o necesita algún trámite fiscal.
3. **¿Necesita conocer la edad?** No, la edad no ayuda en nada a resolver un reporte de soporte.
4. **¿Necesita conocer el código postal?** Solo si el tema de soporte trata sobre envíos físicos o garantías que requieran ir a una zona en particular.
5. **¿Qué principio de privacidad está relacionado con esta decisión?** El **Principio de Minimización**, que nos enseña a pedir y guardar únicamente lo que realmente sirve, evitando acumular información de más.

# Actividad 3 — Separación por finalidad
* **¿Por qué esta información puede ser más apropiada para analítica que entregar directamente la tabla completa de clientes?** Porque cuida la identidad de las personas. En lugar de pasar nombres y correos, se mandan totales y rangos de edades, obteniendo las estadísticas que la empresa necesita sin poner en riesgo la privacidad de nadie.

# Actividad 4 — Control de acceso relacionado con la finalidad
1. **¿Qué información puede consultar el rol?** Solamente la ciudad y los grupos de edad que aparecen resumidos en la vista especial.
2. **¿Puede consultar directamente clientes?** No, tiene prohibido el acceso a la tabla original.
3. **¿Puede obtener nombre, correo y RFC?** No, esos datos ni siquiera existen dentro de la vista que se le asignó.
4. **¿Qué principio de privacidad estás aplicando?** El de generalizar y minimizar los datos.
5. **¿Qué principio de seguridad estás aplicando?** El de **Mínimo Privilegio**, dándole acceso únicamente a lo justo y necesario para trabajar.