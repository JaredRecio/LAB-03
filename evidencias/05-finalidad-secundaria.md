# LABORATORIO 3: PRIVACIDAD Y CUMPLIMIENTO
#### Grupo: 4-3
#### Estudiante: Jesús Jared Recio Ozúa

# Actividad 5 — Analizar una finalidad secundaria
La empresa quiere usar los datos de los clientes para algo nuevo: *“Mandar promociones personalizadas basadas en su edad, ciudad y qué tanto compran.”*

1. **¿El hecho de que la organización ya tenga los datos significa automáticamente que puede utilizarlos para cualquier finalidad?** Claro que no. Tener la información para dar soporte no da permiso de usarla para mandar publicidad; para eso se necesita que el usuario acepte expresamente.
2. **¿Qué preguntas debería realizar la organización antes de implementar este tratamiento?** ¿Le avisamos esto al usuario en el aviso de privacidad?, ¿nos dio su consentimiento consciente?, ¿le damos una forma fácil de decir que no?
3. **¿Qué datos serían realmente necesarios?** Los rangos de edad, la ciudad general y los hábitos de compra resumidos.
4. **¿Necesitaría el área de marketing acceso directo a clientes?** No, marketing debe trabajar con listas limpias o vistas separadas, nunca entrando a las tablas principales con datos completos.
5. **¿Qué controles técnicos podrían limitar la información entregada?** Vistas personalizadas y permisos bien configurados para que solo vean lo autorizado.

# Actividad 6 — Derechos ARCO y la base de datos
* **¿Qué información adicional debería proporcionar la organización además del resultado de esta consulta?** Además de enseñarle al usuario los datos que se encontraron con el filtro de su correo, hay que explicarle de dónde los sacamos, para qué los usamos y cómo puede ejercer el resto de sus derechos.

# Actividad 7 — Derecho de rectificación
1. **¿Cómo podría comprobarse que el cambio fue autorizado?** Pidiendo una validación de identidad segura antes de hacer cualquier modificación en el sistema.
2. **¿Debería registrarse quién realizó el cambio?** Sí, para tener un historial claro y saber quién modificó el registro.
3. **¿Por qué la trazabilidad será importante?** Porque permite seguirle la pista a los cambios, facilitando encontrar el origen de un error o detectar movimientos extraños.