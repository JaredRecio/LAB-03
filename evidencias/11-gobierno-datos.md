# LABORATORIO 3: PRIVACIDAD Y CUMPLIMIENTO
#### Grupo: 4-3
#### Estudiante: Jesús Jared Recio Ozúa

# Actividad 11 — Diseñar una matriz de gobierno de datos

| Dato | Finalidad | Responsable | Usuarios autorizados | Protección | Retención | Acción al finalizar |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **nombre** | Identificar al cliente al atender reportes | Atención al cliente | Soporte, DBA, Dirección | Cifrado y control de accesos por roles | Mientras la cuenta esté activa + 1 año | Borrado seguro o desvinculación |
| **correo** | Mandar avisos y estar en contacto | Atención al cliente | Soporte, DBA | Cifrado en tránsito y vistas protegidas | Durante la vigencia de la cuenta | Eliminar de listas de contacto |
| **telefono** | Llamadas rápidas o validación | Atención al cliente | Soporte, DBA | Cifrado y visibilidad limitada | Mientras la cuenta esté activa | Borrado definitivo |
| **rfc** | Hacer facturas válidas | Facturación | Contabilidad, DBA | Cifrado fuerte y acceso muy restringido | 5 años (mandato fiscal) | Depuración y borrado al vencer el plazo |
| **edad** | Sacar estadísticas y perfiles | Analítica | Analítica, DBA | Datos agregados o en rangos | Durante los estudios estadísticos | Resumen anónimo final |
| **ciudad** | Ubicación general y soporte regional | Atención al cliente | Soporte, Logística, DBA | Vistas operativas controladas | Hasta que termine el servicio | Anonimización |
| **codigo_postal** | Calcular envíos y cobertura | Logística | Logística, DBA | Datos seguros para uso logístico | Durante las entregas activas | Limpieza estadística |