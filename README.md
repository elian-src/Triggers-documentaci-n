# 📘 Documentación: Triggers en Bases de Datos

## 1. ¿Qué es un Trigger?

Un **Trigger** (o **disparador**) es un objeto de base de datos que se asocia a una tabla o vista y se ejecuta automáticamente al ocurrir ciertos eventos como `INSERT`, `UPDATE` o `DELETE`.

---

## 2. ¿Para qué sirve un Trigger?

Un Trigger se utiliza para:

- Automatizar tareas repetitivas.
- Aplicar reglas de negocio.
- Auditar cambios en los datos.
- Validar o modificar datos antes o después de una operación.

---

## 3. ¿Cuándo se puede usar un Trigger?

Se puede usar un Trigger cuando se necesite:

- Garantizar la integridad de los datos.
- Llevar un registro (log) de cambios.
- Sincronizar tablas.
- Prevenir ciertas acciones (por ejemplo, eliminar registros protegidos).

---

## 4. Estructura de un Trigger

```sql
CREATE TRIGGER nombre_del_trigger
{ BEFORE | AFTER } { INSERT | UPDATE | DELETE }
ON nombre_de_la_tabla
FOR EACH ROW
BEGIN
   -- Instrucciones SQL
END;
```

---

## 5. Tipos de Trigger

1. **BEFORE INSERT**  
2. **AFTER INSERT**  
3. **BEFORE UPDATE**  
4. **AFTER UPDATE**  
5. **BEFORE DELETE**  
6. **AFTER DELETE**

---

## 6. ¿Cuándo ejecuta su acción un Trigger?

Un Trigger se ejecuta **automáticamente** cuando se produce el evento al que está vinculado (`INSERT`, `UPDATE` o `DELETE`), **antes o después** de que este se complete, según cómo se haya definido.

---

## 7. Ejemplo de un Trigger

```sql
CREATE TRIGGER log_insert_cliente
AFTER INSERT ON clientes
FOR EACH ROW
BEGIN
  INSERT INTO log_clientes (cliente_id, fecha_insert)
  VALUES (NEW.id, NOW());
END;
```

---

## 8. Trigger en Marketing

En marketing, un "trigger" es un **evento que activa una acción automática**, como enviar un correo electrónico cuando un usuario:

- Se registra en una web.
- Abandona un carrito de compra.
- Cumple años.

Este tipo de triggers forman parte del **marketing automatizado**.

---

## 9. ¿Cómo hacer un Trigger?

Pasos básicos:

1. Identifica la tabla y el evento (`INSERT`, `UPDATE`, `DELETE`).
2. Define si el trigger se ejecutará `BEFORE` o `AFTER`.
3. Escribe la lógica en SQL (dentro del bloque `BEGIN...END`).
4. Usa `NEW` y `OLD` para acceder a los valores de los registros.

---

## 10. Características de un Trigger

- Se ejecutan automáticamente.
- No pueden ser llamados directamente.
- Pueden acceder a los valores antes (`OLD`) y después (`NEW`) del cambio.
- No devuelven resultados.
- Se aplican a nivel de fila (`FOR EACH ROW`) o a nivel de instrucción (según el motor de base de datos).

---

## 11. Desventajas de un Trigger

- **Dificultan la depuración.**
- **Disminuyen el rendimiento** si son mal diseñados.
- **Ocultan lógica de negocio**, haciendo más complejo el mantenimiento.
- **Orden de ejecución impredecible** si hay múltiples triggers del mismo tipo.

---

## 12. Sustitutos de los Triggers en otras bases de datos

- **Procedimientos almacenados**: Se ejecutan manualmente y pueden contener lógica condicional.
- **Funciones definidas por el usuario (UDFs)**: Para validar o transformar datos.
- **ORM Hooks**: En frameworks como Django o Sequelize, se usan métodos como `beforeSave`, `afterCreate`, etc.
- **Middleware/Servicios Backend**: Se puede controlar la lógica directamente en el código de la aplicación.
