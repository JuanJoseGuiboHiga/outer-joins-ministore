# MiniStore — Análisis de Inventario y Ventas con Outer JOINs

**Autor:** Juan José Guibo Higa  
**Módulo:** Consultas SQL con Join y Union  

---

### 1. ¿Por qué usaste LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué se perdería si usaras INNER JOIN?

> **Respuesta:**  
> Usé `LEFT JOIN` para conservar todos los registros de la tabla **productos** (catálogo), incluso aquellos que no tienen ventas asociadas. Si hubiera usado `INNER JOIN`, los productos sin ventas se habrían descartado y no podríamos identificar qué productos nunca se vendieron.

---

### 2. ¿Por qué usaste RIGHT JOIN para la Consulta 2? ¿Qué tabla está a la izquierda y cuál a la derecha en tu consulta?

> **Respuesta:**  
> En la consulta, la tabla a la **izquierda** es `productos` y la tabla a la **derecha** es `ventas`.  
> Usé `RIGHT JOIN` para preservar todas las ventas registradas, incluso aquellas que no tienen un `producto_id` existente en el catálogo, permitiendo detectar registros huérfanos.

---

### 3. ¿Qué representan los valores NULL en cada resultado?

> **Respuesta:**  
> Los valores `NULL` indican la ausencia de coincidencia entre ambas tablas según la clave de cruce.

#### Ejemplo — Consulta 1 (LEFT JOIN)
El producto con ID `109` nunca se vendió, por lo que las columnas correspondientes a `ventas` se completan con `NULL`:

| producto_id | nombre             | categoria | precio | venta_id |
|:-----------:|:-------------------|:---------:|:------:|:--------:|
| 109         | Parlante Bluetooth | Audio     | 60.00  | NULL     |

#### Ejemplo — Consulta 2 (RIGHT JOIN)
La venta con ID `10` referencia a un `producto_id` (`999`) que no existe en el catálogo, por lo que los atributos de `productos` se completan con `NULL`:

| producto_id | nombre | categoria | precio | venta_id | producto_id | cliente_id |
|:-----------:|:------:|:---------:|:------:|:--------:|:-----------:|:----------:|
| NULL        | NULL   | NULL      | NULL   | 10       | 999         | 205        |

---

### 4. ¿Cuándo usarías FULL OUTER JOIN en un caso real de negocio?

> **Respuesta:**  
> Usaría `FULL OUTER JOIN` en tareas de **conciliación, auditoría o migración de datos**. Por ejemplo, para auditar discrepancias entre el catálogo de inventario y el registro de ventas: permite identificar en una sola vista tanto productos estancados sin demanda como transacciones con errores de consistencia (ventas de productos no catalogados).
