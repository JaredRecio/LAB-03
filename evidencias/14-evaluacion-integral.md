# LABORATORIO 3: PRIVACIDAD Y CUMPLIMIENTO
#### Grupo: 4-3
#### Estudiante: Jesús Jared Recio Ozúa

# Actividad 14 — Escenario integral
| # | Problema | Principio afectado | Riesgo | Control propuesto |
| :-: | :--- | :--- | :--- | :--- |
| 1 | Analítica consulta la tabla completa de clientes | Mínimo Privilegio | Exponer datos personales sin necesidad | Usar vistas con datos resumidos |
| 2 | Uso de datos con nombres y correos para estadísticas | Minimización | Procesar más de lo requerido | Trabajar solo con totales y agregaciones |
| 3 | Datos guardados por 12 años sin regla de borrado | Conservación | Acumular riesgo innecesario | Crear reglas automáticas de retención y purga |
| 4 | No existe una política de retención escrita | Responsabilidad | Incumplir normas de protección | Redactar y aplicar una política formal |
| 5 | Desarrolladores usan copias idénticas a producción | Minimización | Fuga de datos en entornos de prueba | Usar datos falsos o sintéticos en desarrollo |
| 6 | Ambientes de prueba con información real | Seguridad | Mayor vulnerabilidad ante robos de datos | Aplicar enmascaramiento en desarrollo |
| 7 | Marketing manda promos sin permiso de los usuarios | Consentimiento | Multas y molestias por spam | Llevar un registro claro de quién acepta publicidad |
| 8 | No se documenta la finalidad de cada dato | Transparencia | No poder justificar por qué se pide la información | Hacer un inventario de datos y avisos claros |
| 9 | Todo guardado en una sola tabla gigante | Seguridad por diseño | Una filtración tira toda la seguridad | Separar en capas (operativa, analítica y auditoría) |
| 10 | Sin registros de quién consulta qué | Responsabilidad | No poder rastrear accesos extraños | Activar bitácoras de auditoría en la base |