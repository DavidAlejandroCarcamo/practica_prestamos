Práctica de Préstamos UNICAH - Odoo 20

Estudiante: David Alejandro Carcamo Espinal
Número de cuenta: 0801200213413
Asignatura: Programación de Negocios
Universidad: Universidad Católica de Honduras

Descripción

Desarrollo de un módulo personalizado en Odoo 20 para administrar el préstamo y devolución de equipos universitarios, como laptops, proyectores y equipos de audio.

Respuestas

Paso 1. Catálogo de equipos

1. ¿Qué pasa con un equipo cuando se desmarca el campo Activo? ¿Por qué es mejor que borrarlo?

El equipo queda archivado y deja de aparecer normalmente en los listados. Es mejor que eliminarlo porque conserva su información y los registros relacionados con él.

2. ¿Para qué sirve copy=False en el campo codigo?

Sirve para evitar que el código de inventario se copie automáticamente cuando duplicamos un equipo, ya que cada equipo debe tener un código único.

Paso 2. Registro de préstamos

1. Este modelo usa _name y _inherit al mismo tiempo. ¿Qué hace cada uno aquí?

_name define el nombre del nuevo modelo prestamo.prestamo, mientras que _inherit permite incorporar las funcionalidades de mail.thread, como el historial de mensajes.

2. ¿Qué hace tracking=True en el campo state?

Permite registrar automáticamente los cambios de estado del préstamo en el historial o chatter, para saber cuándo pasó de Borrador a Prestado o Devuelto.

Paso 3. Equipos del préstamo

1. En fields.One2many("prestamo.linea", "prestamo_id"), ¿qué indica cada parámetro?

prestamo.linea indica el modelo que contiene los equipos asociados al préstamo, y prestamo_id es el campo que relaciona cada línea con su préstamo correspondiente.

2. ¿Qué pasa con las líneas cuando se borra un préstamo? ¿Qué parte del código lo define?

Las líneas asociadas también se eliminan automáticamente. Esto se configura mediante ondelete="cascade" en el campo prestamo_id del modelo prestamo.linea.

Paso 4. Flujo de estados

1. Los botones ya se ocultan según el estado. ¿Por qué los métodos vuelven a validar el estado?

Porque ocultar los botones solamente controla la interfaz. Las validaciones dentro de los métodos impiden ejecutar acciones incorrectas aunque se intenten llamar desde otro lugar del sistema.

2. ¿Qué hace prestamo.linea_ids.equipo_id.write(...)? ¿Por qué no hace falta un for para cada equipo?

Actualiza el estado de todos los equipos relacionados con el préstamo. No necesita un for porque Odoo permite ejecutar write() sobre un conjunto de registros.

Paso 5. Reglas del préstamo

1. El campo equipo_id ya filtra los equipos disponibles. ¿Por qué hace falta el TODO 5?

Porque el filtro solamente limita las opciones que aparecen al seleccionar un equipo. La validación adicional comprueba su disponibilidad justo antes de realizar el préstamo, evitando prestar un equipo que ya no esté disponible.

2. ¿En qué momento se ejecuta un método con @api.constrains? ¿Y la validación de action_prestar?

Los métodos con @api.constrains se ejecutan cuando se crean o modifican registros que incluyen los campos indicados en la restricción. En cambio, las validaciones de action_prestar se ejecutan cuando se intenta realizar la acción de prestar.

Paso 6. Contacto, kanban y búsqueda

1. ¿Qué pasa si arrastra una tarjeta del kanban a otra columna? ¿Por qué?

Cuando la vista permite mover tarjetas, Odoo actualiza el campo estado del equipo según la columna de destino. Esto sucede porque el kanban está agrupado mediante ese campo.

2. El campo prestamo_ids se agregó a res.partner. ¿Se crea una columna nueva en la tabla de contactos? Explique.

No se crea una nueva columna para prestamo_ids, porque es un campo One2many. La relación se establece mediante el campo partner_id, que está almacenado en el modelo de préstamos.

Pasos desarrollados

Catálogo de equipos.

Registro de préstamos.

Equipos del préstamo.

Flujo de estados.

Reglas del préstamo.

Contacto, kanban y búsqueda.

Estado del proyecto

El módulo se instaló en Odoo 20 y se verificó que abre el listado de préstamos, muestra el formulario y permite seleccionar equipos del catálogo.

La integración de la pestaña de préstamos dentro de Contactos quedó pendiente de habilitar por un error de validación de la vista.