# 🛍️ Tienda Online - Base de Datos NoSQL (MongoDB)

Este repositorio contiene la estructura y los datos de ejemplo de una base de datos documental MongoDB diseñada para una tienda online de ropa, accesorios y artículos para el hogar.

## 📁 Colecciones incluidas

La base de datos está compuesta por las siguientes colecciones:

### 1. `usuarios`
Contiene la información de los usuarios registrados en la tienda (clientes y administradores).

**Campos principales:**
- `_id`: Identificador único del usuario (ej. `user_1`)
- `nombre`, `email`, `telefono`, `direccion`, `ciudad`, `genero`, `rol`

---

### 2. `productos`
Incluye todos los productos disponibles para la venta.

**Campos principales:**
- `_id`: Identificador del producto (ej. `prod_1`)
- `nombre`, `descripcion`, `precio`, `categoria`, `stock`, `genero`, `tags`

---

### 3. `categorias`
Clasificación general de los productos.

**Campos principales:**
- `_id`: Identificador de la categoría (ej. `cat_1`)
- `nombre`, `descripcion`

---

### 4. `pedidos`
Almacena los pedidos realizados por los clientes.

**Campos principales:**
- `_id`: Identificador del pedido (ej. `pedido_1`)
- `usuario_id`, `fecha`, `estado`, `productos`, `total`, `direccion_envio`, `metodo_pago`

---

### 5. `reseñas`
Contendrá las opiniones de los clientes sobre los productos adquiridos.

---

## 📦 Datos de ejemplo

Cada colección contiene al menos 10 documentos con datos realistas y relacionados entre sí, permitiendo realizar operaciones y consultas útiles para pruebas, desarrollo y análisis de datos.

## 🧪 Consultas en MongoDB
### `1. Buscar usuarios cuyo nombre comienza con "Mar"`
```js
//Filtrar rápidamente nombres similares como "María", "Marcos", "Marcelino".
db.usuarios.find({"nombre":{$regex:"^Mar" , $options: "i"}})
```

### `2. Buscar usuarios con correos que terminan en @gmail.com`
```js
/// Útil para campañas de marketing segmentadas por proveedor de correo.
db.usuarios.find({"email":{$regex:"@gmail.com", $options: "i"}})
```

### `3. Buscar usuarios cuya ciudad contiene “lle”`
```js
///Útil para encontrar usuarios de ciudades como "Valladolid" o "Sevilla" en filtros dinámicos.
db.usuarios.find({"ciudad":{$regex:"lla" , $options:"i"}})
```

### `4. Buscar productos con descripciones que mencionen “algodón”`
```js
///Útil para destacar productos de materiales especificos.
db.productos.find({"descripcion":{$regex:"algod[oó]n", $options:"i"}})
```

### `5. Buscar productos con nombres que contienen "vestido"`
```js
/// Útil para generar categorías de productos segun su nombre.
db.productos.find({"nombre":{$regex:"vestido", $options:"i"}})
```

### `6. Buscar productos etiquetados con tags para el "hogar`
```js
//Útil para filtrar por tags (decoración, algodón, hogar, etc).
db.productos.find({tags:{$regex:"hogar", $options:"i"}})
```

### `7. Buscar productos unisex en tags que contienen “accesorio”`
```js
/// Útil para segmentar productos dependiendo de la necesidad del usuario.
db.productos.find({ genero: "unisex", tags: { $regex: "accesorio", $options: "i" } })

```

### `8. Buscar pedidos con método de pago que contiene “nequi”`
```js
// Útil para analizar el uso de métodos de pago digitales.
db.pedidos.find({ metodo_pago: { $regex: "nequi", $options: "i" } })
```

### `9. Buscar productos con nombre que comience con vocal`
```js
/// Útil para autocompletado y clasificación fonética de productos.
db.productos.find({ nombre: { $regex: "^[AEIOUaeiou]", $options: "i" } })

```

### `10. Buscar productos con nombres que contengan dos palabras`
```js
/// Útil para detectar nombres compuestos y mejorar nomenclatura.
db.productos.find({ nombre: { $regex: "^[A-Za-z]+\\s[A-Za-z]+" } })
```

### `11. Buscar pedidos enviados a direcciones que contengan "Calle"`
```js
/// Útil para detección de ubicaciones urbanas.
db.pedidos.find({ direccion_envio: { $regex: "Calle", $options: "i" } })
```

### `12. Buscar productos con descripción que contiene número`
```js
/// Útil para validar que no se estén usando cantidades arbitrarias.
db.productos.find({ descripcion: { $regex: "\\d+", $options: "i" } })
```

### `13. Buscar pedidos en estado “enviado” o “entregado”`
```js
/// Útil para monitoreo de entregas finalizadas o en proceso
db.pedidos.find({ estado: { $regex: "enviad|entregad", $options: "i" } })
```

### `14. Buscar productos para hombres con tags que contengan "invierno"`
```js
/// Útil para destacar ropa de masculina con un tag en especifico.
db.productos.find({ genero: "masculino", tags: { $regex: "camiseta", $options: "i" } })
```

### `15. Buscar productos con descripción que contenga signo de puntuación`
```js
/// Útil para detectar descripciones bien redactadas.
db.productos.find({ descripcion: { $regex: "[.,!;:]", $options: "i" } })
```

### `16. Buscar categorías con nombres de una sola palabra`
```js
/// Útil para clasificar entre categorías simples y compuestas.
db.categorias.find({ nombre: { $regex: "^[^\\s]+$", $options: "i" } })
```
### `17. Buscar usuarios cuyo nombre tenga acentos`
```js
/// Útil para detección de codificación o correcciones automáticas.
db.usuarios.find({ nombre: { $regex: "[áéíóúÁÉÍÓÚ]", $options: "i" } })
```

### `18. Buscar usuarios con nombre de al menos 3 palabras`
```js
/// Útil para analizar nombres completos y mejorar formularios.
db.usuarios.find({ nombre: { $regex: "^\\w+\\s+\\w+\\s+\\w+", $options: "i" } })
```

### `19. Buscar reseñas que usen la palabra “excelente”`
```js
/// Para destacar buenos comentarios en la tienda.
db.resenas.find({ comentario: { $regex: "excelente", $options: "i" } })
```

### `20. Buscar usuarios con correos empresariales que terminan en “.co”`
```js
/// Segmenta usuarios de empresas colombianas.
db.usuarios.find({ email: { $regex: "\\.co$", $options: "i" } })
```

### `21. Detectar usuarios con correos que no tienen dominio válido (sin @ o sin .)`
```js
/// Para limpiar datos erróneos o mal ingresados.
db.usuarios.find({ email: { $not: { $regex: "@.*\\.", $options: "i" } } })
```

### `22. Comentarios que incluyen palabras como “recomiendo”, “volveré”, “compraría”`
```js
/// Identifica reseñas que refuerzan la lealtad del cliente.
db.resenas.find({ comentario: { $regex: "recomiendo|volver[eé]|comprar[íi]a", $options: "i" } })
```

### `23. Productos que no tienen etiquetas (tags) relacionados con "ropa" o "hogar"`
```js
/// Para identificar productos mal clasificados, sin sector definido o con una categoria que no sean las mencionadas
db.productos.find({ tags: { $not: { $regex: "ropa|hogar", $options: "i" } } })
```

### `24. Buscar usuarios con nombres de más de dos palabras (nombre completo extendido)`
```js
/// Para validar campos de nombre completo.
db.usuarios.find({ nombre: { $regex: "^\\w+\\s\\w+\\s", $options: "i" } })
```

### `25. Buscar reseñas que contengan palabras negativas como “mal”, “defectuoso”, “incompleto”`
```js
/// Detección temprana de problemas en productos o servicio al cliente.
db.resenas.find({ comentario: { $regex: "mal|defectuoso|incompleto", $options: "i" } })
```