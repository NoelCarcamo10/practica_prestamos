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

### Paso 3: Equipos del préstamo
1. **En `fields.One2many("prestamo.linea", "prestamo_id")`, ¿qué indica cada parámetro?**
   El primer parámetro (`"prestamo.linea"`) indica el modelo hijo cuyos registros se van a listar, y el segundo (`"prestamo_id"`) indica el campo `Many2one` en ese modelo hijo que apunta hacia el préstamo padre.
2. **¿Qué pasa con las líneas cuando se borra un préstamo? ¿Qué parte del código lo define?**
   Se eliminan automáticamente en cascada junto con el préstamo. Lo define el parámetro `ondelete="cascade"` en el campo `prestamo_id` de `prestamo.linea`.

### Paso 4: Flujo de estados
1. **Los botones ya se ocultan según el estado. ¿Por qué los métodos vuelven a validar el estado?**
   Porque ocultar un botón es solo una regla visual de la interfaz; validar en Python garantiza la seguridad en el servidor ante llamadas por RPC/API, acciones masivas o sesiones simultáneas de dos usuarios.
2. **¿Qué hace `prestamo.linea_ids.equipo_id.write(...)`? ¿Por qué no hace falta un `for` para cada equipo?**
   `prestamo.linea_ids.equipo_id` devuelve un *recordset* con todos los equipos asociados a las líneas del préstamo, y el método `.write()` de Odoo ORM actualiza en lote todos los registros del *recordset* en una sola consulta SQL.
