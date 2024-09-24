# Modulo Para Servir

Este documento describe los modelos utilizados en la aplicación Condevuelta, proporcionando detalles sobre sus campos, relaciones y funciones.

### 1. Modelo `Locacion`

El modelo `Locacion` representa una ubicación específica que puede asociarse a comercios.

- **Campos:**
  - `nombre`: Nombre de la locación (único).
  - `direccion`: Dirección de la locación.
  - `descripcion`: Descripción opcional de la locación.
  - `created_at`: Fecha de creación del registro.
  - `updated_at`: Fecha de última actualización.

- **Métodos:**
  - `__str__()`: Retorna una representación en cadena de la locación, combinando su nombre y dirección.

### 2. Modelo `Comercio`

El modelo `Comercio` representa un comercio asociado a una locación.

- **Campos:**
  - `locacion`: Relación con la locación correspondiente.
  - `nombre`: Nombre del comercio.
  - `descripcion`: Descripción opcional del comercio.
  - `created_at`: Fecha de creación del registro.
  - `updated_at`: Fecha de última actualización.

- **Métodos:**
  - `__str__()`: Retorna una cadena con el nombre del comercio y su locación.
  - `get_ultima_entrega()`: Devuelve la última entrega asociada al comercio.

- **Meta:**
  - `unique_together = ('locacion', 'nombre')`: Unicidad combinada de locación y nombre.

### 3. Modelo `Implemento`

El modelo `Implemento` describe los implementos que pueden estar en el inventario.

- **Campos:**
  - `nombre`: Nombre del implemento (único).
  - `tipo`: Tipo de implemento (utensilio o loza).
  - `descripcion`: Descripción opcional.
  - `created_at`: Fecha de creación.
  - `updated_at`: Fecha de última actualización.

- **Métodos:**
  - `__str__()`: Retorna el nombre del implemento.

### 4. Modelo `Stock`

El modelo `Stock` gestiona el inventario de implementos en una locación específica.

- **Campos:**
  - `location`: Relación uno a uno con una locación.
  - `created_at`: Fecha de creación del registro.
  - `updated_at`: Fecha de última actualización.

- **Métodos:**
  - `__str__()`: Retorna una cadena que describe el stock de la locación.

### 5. Modelo `ImplementoStock`

El modelo `ImplementoStock` gestiona los implementos dentro de un stock específico.

- **Campos:**
  - `stock`: Relación con un registro de stock.
  - `implemento`: Relación con un implemento.
  - `cantidad`: Cantidad de implementos en stock.
  - `creado_por`: Usuario que creó el registro.
  - `actualizado_por`: Usuario que actualizó el registro.
  - `created_at`: Fecha de creación.
  - `updated_at`: Fecha de última actualización.

- **Meta:**
  - `unique_together = ('stock', 'implemento')`: Garantiza la unicidad combinada.

- **Métodos:**
  - `__str__()`: Devuelve una cadena que describe el implemento y su cantidad en stock.

### 6. Modelo `EstadoInventario`

El modelo `EstadoInventario` mantiene registros de los estados de inventario en una locación.

- **Campos:**
  - `autor`: Nombre del autor del registro.
  - `nombre`: Nombre único generado automáticamente.
  - `location`: Relación con una locación.
  - `created_at`: Fecha de creación.
  - `updated_at`: Fecha de última actualización.

- **Métodos:**
  - `save()`: Genera un nombre único si no existe al guardar.
  - `__str__()`: Retorna el nombre del registro.

### 7. Modelo `ImplementoInventario`

El modelo `ImplementoInventario` relaciona implementos con un estado de inventario.

- **Campos:**
  - `inventario`: Relación con un estado de inventario.
  - `implemento`: Relación con un implemento.
  - `cantidad`: Cantidad de implementos en el inventario.

- **Métodos:**
  - `__str__()`: Retorna una cadena que describe el implemento, su cantidad y el inventario.

### 8. Modelo `Entrega`

El modelo `Entrega` documenta entregas realizadas a una locación o comercio.

- **Campos:**
  - `autor`: Nombre del autor de la entrega.
  - `locacion`: Relación con la locación.
  - `comercio`: Relación opcional con un comercio.
  - `nombre`: Nombre único generado automáticamente.
  - `created_at`: Fecha de creación.
  - `updated_at`: Fecha de última actualización.

- **Métodos:**
  - `save()`: Genera un nombre único si no existe al guardar.
  - `__str__()`: Retorna una descripción de la entrega, incluyendo comercio y fecha.

### 9. Modelo `ImplementoEntrega`

El modelo `ImplementoEntrega` gestiona los implementos entregados en una entrega específica.

- **Campos:**
  - `entrega`: Relación con una entrega.
  - `implemento`: Relación con un implemento.
  - `cantidad`: Cantidad de implementos entregados.

- **Métodos:**
  - `__str__()`: Retorna una cadena que describe el implemento y la cantidad entregada.

### 10. Modelo `Actividad`

El modelo `Actividad` registra actividades realizadas por los usuarios en el sistema.

- **Campos:**
  - `usuario`: Nombre del usuario que realizó la actividad.
  - `accion`: Descripción de la acción realizada.
  - `fecha`: Fecha en la que se realizó la acción.
  - `modulo`: Módulo donde ocurrió la acción (`stock`, `inventario`, `entregas`).
  - `identificador`: Identificador opcional de la acción.

- **Métodos:**
  - `__str__()`: Retorna una cadena describiendo la actividad realizada, el usuario y el módulo involucrado.



