¿Por qué usaste LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué se perdería si usaras INNER JOIN? 
Respuesta: Usé LEFT JOIN para conservar todos los registros de la tabla productos (catálogo), incluso aquellos que no tienen ventas asociadas. Si hubiera usado INNER JOIN, los productos sin ventas se habrían descartado y no podríamos identificar qué productos nunca se vendieron.

¿Por qué usaste RIGHT JOIN para la Consulta 2? ¿Qué tabla está a la izquierda y cuál a la derecha en tu consulta?
La tabla a la izquierda es la de productos y la tabla de la derecha es la de ventas, use el RIGHT JOIN para obtener todas las ventas incluso las que no tuvieran asociado un producto_id

¿Qué representan los valores NULL en cada resultado? Explicá con un ejemplo concreto de los datos qué significa que venta_id sea NULL en la Consulta 1 y que producto_id de productos sea NULL en la Consulta 2.

Ejemplo de consulta 1: En este ejemplo el producto con id 109 nunca se vendió, ya que no cuenta con un venta_id relacionado

producto_id |       nombre       | categoria | precio | venta_id
109          Parlante Bluetooth    Audio       60.00     NULL

Ejemplo de consulta 2: En este ejemplo la venta con id 10 tiene un producto_id relacionado que no existe dentro de la tabla productos es por ese motivo que al hacer el RIGHT JOIN se rellena con un valor NULL

producto_id |  nombre | categoria | precio | venta_id | producto_id | cliente_id
NULL           NULL       NULL      NULL     10           999            205

¿Cuándo usarías FULL OUTER JOIN en un caso real de negocio?

Usaría FULL OUTER JOIN en tareas de conciliación, auditoría o migración de datos, por ejemplo para auditar discrepancias entre el catálogo de inventario y el registro de ventas: permite identificar en una sola vista tanto productos estancados sin demanda como transacciones con errores de consistencia (ventas de productos no catalogados)
