* **Nombre:** Noel Alexander Cárcamo Figueroa
* **Número de cuenta:** 0703200104216
## Respuestas

### Paso 1: Catálogo de equipos
1. **¿Qué pasa con un equipo cuando se desmarca el campo Activo? ¿Por qué es mejor que borrarlo?**
   Odoo lo archiva automáticamente: deja de aparecer en las búsquedas y listas normales sin eliminarse de la base de datos. Es mejor que borrarlo porque conserva la integridad referencial y el historial de préstamos anteriores donde participó ese equipo.
2. **¿Para qué sirve `copy=False` en el campo `codigo`?**
   Evita que al duplicar un registro de equipo desde la interfaz de Odoo se copie el mismo código de inventario, obligando a asignar un código único al nuevo equipo.

### Paso 2: Registro de préstamos
1. **Este modelo usa `_name` y `_inherit` al mismo tiempo. ¿Qué hace cada uno aquí?**
   `_name = "prestamo.prestamo"` crea una tabla nueva e independiente en PostgreSQL para los préstamos, mientras que `_inherit = ["mail.thread"]` le incorpora las funciones y campos de mensajería/auditoría (chatter) sin modificar el modelo original `mail.thread`.
2. **¿Qué hace `tracking=True` en el campo `state`?**
   Registra automáticamente en el chatter cada cambio de valor del estado, mostrando el estado anterior, el nuevo, la fecha/hora y el usuario que realizó la modificación.
