* **Nombre:** Noel Alexander Cárcamo Figueroa
* **Número de cuenta:** 0703200104216
## Respuestas

### Paso 1: Catálogo de equipos
1. **¿Qué pasa con un equipo cuando se desmarca el campo Activo? ¿Por qué es mejor que borrarlo?**
   Odoo lo archiva automáticamente: deja de aparecer en las búsquedas y listas normales sin eliminarse de la base de datos. Es mejor que borrarlo porque conserva la integridad referencial y el historial de préstamos anteriores donde participó ese equipo.
2. **¿Para qué sirve `copy=False` en el campo `codigo`?**
   Evita que al duplicar un registro de equipo desde la interfaz de Odoo se copie el mismo código de inventario, obligando a asignar un código único al nuevo equipo.
