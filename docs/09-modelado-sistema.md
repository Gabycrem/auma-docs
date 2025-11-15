# 09 – Modelado del Sistema  
Versión 1.0

---

# 1. Introducción

El presente documento describe el **modelado del sistema e-commerce AUMA**, aplicando diversas técnicas formales de análisis estructural y orientado a objetos.  

Se incluyen:  
- modelo de contexto,  
- diagrama de casos de uso,  
- descripción de casos de uso,  
- diagramas de flujo de datos (DFD),  
- modelo de datos (DER),  
- modelo de clases conceptual.

Este documento permite comprender la estructura, interacciones y comportamiento esperado del sistema previo al diseño y desarrollo.

---

# 2. Modelo de Contexto (Diagrama de Alto Nivel)

El sistema AUMA interactúa con distintos actores externos. Se representa el alcance del sistema como una “caja negra”.

```
                     +----------------------------------+
                     |           SISTEMA AUMA           |
                     |     (E-commerce + Admin)         |
                     +----------------------------------+
                         ^         ^           ^
                         |         |           |
            ----------------    ----------    ----------------
            |   Cliente    |    | Admin |    | Pasarela Pago |
            ----------------    ----------    ----------------
                   |                |                |
       Consulta, compra     Gestión catálogo   Envío confirmación
       estado de pedido      y pedidos         de pago (webhook)
```

# 3. Modelo de Casos de Uso
## 3.1. Actores

- Cliente: usuario que navega el sitio y realiza pedidos.
- Cliente registrado: posee cuenta y puede ver historial.
- Administrador: gestiona catálogo, stock y pedidos.
- Pasarela de pago: sistema externo que envía confirmaciones (webhook).

## 3.2. Diagrama General de Casos de Uso

```
                   SISTEMA AUMA
          ----------------------------------
          |                               |
Cliente --- UC1 Ver catálogo              |
Cliente --- UC2 Ver detalle               |
Cliente --- UC3 Agregar al carrito        |
Cliente --- UC4 Gestionar carrito         |
Cliente --- UC5 Finalizar compra          |
Cliente --- UC6 Registrarse (futuro)      |
Cliente --- UC7 Iniciar sesión (futuro)   |
Cliente --- UC8 Ver pedidos (futuro)      |
                                          |
Administrador --- UC9 ABM Productos       |
Administrador --- UC10 Gestionar pedidos  |
                                          |
Pasarela Pago --- UC11 Confirmar pago     |
          ----------------------------------
```

---

## 3.3. Descripción de Casos de Uso

### UC1 – Ver Catálogo

- **Actor:** Cliente  
- **Descripción:** El usuario accede al listado de productos.  
- **Flujo principal:**
  1. El usuario ingresa al sitio.
  2. El sistema muestra el catálogo de productos disponibles.
- **Requerimientos funcionales asociados:** RF-01, RF-02, RF-03

---

### UC2 – Ver Detalle de Producto

- **Actor:** Cliente  
- **Descripción:** El usuario visualiza la ficha completa de un producto.  
- **Flujo principal:**
  1. El usuario selecciona un producto desde el catálogo.
  2. El sistema muestra la ficha completa del producto con:
     - nombre
     - descripción
     - línea
     - fragancia
     - tamaño (ej. 100 ml, 200 ml)
     - tipo de recipiente (frasco, vaso, tapa madera, etc.)
     - precio
     - stock disponible (o estado “Disponible / Sin stock”).
- **Requerimientos funcionales asociados:** RF-04

---

### UC3 – Agregar al Carrito

- **Actor:** Cliente  
- **Descripción:** El usuario agrega un producto al carrito de compra.  
- **Flujo principal:**
  1. El usuario se encuentra en la ficha de producto.
  2. El usuario selecciona (cuando aplique) la **fragancia** deseada.
  3. El usuario indica la cantidad.
  4. El usuario presiona el botón “Agregar al carrito”.
  5. El sistema agrega el ítem al carrito.
- **Requerimientos funcionales asociados:** RF-06

---

### UC4 – Gestionar Carrito

- **Actor:** Cliente  
- **Descripción:** El usuario revisa y modifica el contenido del carrito.  
- **Flujo principal:**
  1. El usuario accede a la vista “Carrito”.
  2. El sistema muestra el listado de ítems agregados (producto, fragancia, cantidad, subtotal).
  3. El usuario puede:
     - modificar cantidades,
     - eliminar ítems,
     - continuar al checkout.
  4. El sistema recalcula el total del carrito.
- **Requerimientos funcionales asociados:** RF-07, RF-08, RF-10

---

### UC5 – Finalizar Compra

- **Actor:** Cliente  
- **Descripción:** El usuario confirma el pedido y pasa al proceso de pago.  
- **Flujo principal:**
  1. El usuario, desde el carrito, hace clic en “Finalizar compra”.
  2. El sistema solicita los datos necesarios (datos de contacto y/o envío).
  3. El sistema crea el pedido en estado “Pendiente de pago”.
  4. El sistema redirige a la pasarela de pago configurada.
  5. El usuario completa el pago en la pasarela.
- **Requerimientos funcionales asociados:** RF-09, RF-10, RF-15

---

### UC6 – Registrarse (post-MVP)

- **Actor:** Cliente  
- **Descripción:** El usuario crea una cuenta para guardar sus datos y pedidos.  
- **Requerimientos funcionales asociados:** RF-11

---

### UC7 – Iniciar Sesión (post-MVP)

- **Actor:** Cliente  
- **Descripción:** El usuario ingresa con su cuenta previamente registrada.  
- **Requerimientos funcionales asociados:** RF-12

---

### UC8 – Ver Pedidos (post-MVP)

- **Actor:** Cliente registrado  
- **Descripción:** El usuario puede consultar el historial de pedidos.  
- **Requerimientos funcionales asociados:** RF-19

---

### UC9 – ABM Productos

- **Actor:** Administrador  
- **Descripción:** El administrador gestiona el catálogo de productos (altas, bajas, modificaciones).  
- **Requerimientos funcionales asociados:** RF-05

---

### UC10 – Gestionar Pedidos

- **Actor:** Administrador  
- **Descripción:** El administrador visualiza y actualiza el estado de los pedidos.  
- **Requerimientos funcionales asociados:** RF-17, RF-18

---

### UC11 – Confirmar Pago (Webhook)

- **Actor:** Pasarela de Pago  
- **Descripción:** La pasarela de pago notifica el resultado de la transacción mediante un webhook.  
- **Requerimientos funcionales asociados:** RF-20, RF-21, RF-22

---

## 4. Diagramas de Flujo de Datos (DFD)

```
                         +-------------------+
Cliente ----------------> |   E-commerce     |
 (Compra)                |      AUMA         |
                         +-------------------+
                                 |
                                 v
                         [ Base de Datos ]
                                 |
                                 v
                         Pasarela de Pago
                      (confirmación webhook)
```

## 4.2. DFD Nivel 1 – Proceso de Compra

```
Cliente
   |
   | Selecciona productos (catálogo, filtros, fragancia)
   v
[Proceso 1: Carrito]
   |
   | 2. Confirma checkout
   v
[Proceso 2: Crear Orden]
   |
   | 3. Genera registro de pedido
   v
[BD Pedidos]
   |
   | 4. Redirige a pago
   v
Pasarela de Pago
   |
   | 5. Envía webhook (OK / fallo)
   v
[Proceso 3: Confirmar Pago]
   |
   | 6. Actualiza estado de pedido y stock
   v
[BD Productos]
```

# 5. Modelo de Datos (DER Lógico)

> Nota: Aunque la implementación técnica apunte a DynamoDB (NoSQL), se documenta el modelo en formato relacional para dejar claro el **dominio de datos** de AUMA.

## 5.1. Visión general

El modelo separa:

- La **configuración física/comercial del producto base**  
  (tamaño, tipo de recipiente, línea, categoría).
- La **variante específica que el cliente compra**  
  (producto + fragancia + stock + precio).
- Las **entidades de apoyo** para mantener el catálogo flexible:
  categorías, líneas, recipientes, fragancias.

---

## 5.2. Entidades principales

```
+-----------------+         +---------------------+
|   Categorias    |         |      Lineas         |
+-----------------+         +---------------------+
| idCategoria (PK)|         | idLinea (PK)        |
| nombre          |         | nombre              |
| descripcion     |         | descripcion         |
| activa          |         | activa              |
+-----------------+         +---------------------+

+-----------------+         +---------------------+
|   Recipientes   |         |     Fragancias      |
+-----------------+         +---------------------+
| idRecipiente(PK)|         | idFragancia (PK)    |
| nombre          |         | nombre              |
| material        |         | descripcion         |
| color           |         | familiaOlfativa     |
| volumenCc       |         | activa              |
| forma           |         +---------------------+
| descripcion     |
+-----------------+

+---------------------------+
|        Productos          |  (Producto base)
+---------------------------+
| idProducto (PK)           |
| nombreComercial          |  ej: "Vela 100cc en frasco vidrio c/tapa negra"
| descripcion              |
| idCategoria (FK)         |
| idLinea (FK)             |
| idRecipiente (FK)        |
| volumenCc                |
| activo                   |
+---------------------------+
```

Cada Producto representa la combinación física/comercial fija que vas a mostrar como ficha de producto:
por ejemplo, “Vela 100cc en frasco de vidrio con tapa negra”.

## 5.3. Variantes de producto (Producto + Fragancia)

```
+-----------------------------------+
|        VariantesProducto          |  (SKU vendible)
+-----------------------------------+
| idVariante (PK)                   |
| idProducto (FK)                   |
| idFragancia (FK)                  |
| sku                               |
| precioActual                      |
| stockActual                       |
| activo                            |
+-----------------------------------+

```

- Cada fila de VariantesProducto es una combinación concreta de:
  - Producto base (tamaño + recipiente + línea + categoría)
  - Fragancia
- Es lo que realmente se vende y se descuenta en stock.
- En la ficha de producto:
  - Se muestra: Producto
  - El usuario elige la fragancia de un <select> que lista las VariantesProducto asociadas.
  - Las variantes con stockActual = 0 se muestran deshabilitadas / en gris con “sin stock”.
 
## 5.4. Clientes, Pedidos e Ítems

```
+------------------+
|     Clientes     |
+------------------+
| idCliente (PK)   |
| nombre           |
| email            |
| direccion        |
| telefono         |
| creadoEn         |
+------------------+

+------------------------------+
|           Pedidos            |
+------------------------------+
| idPedido (PK)                |
| idCliente (FK, nullable)*    |
| fechaCreacion                |
| total                        |
| estado                       |  ej: 'pendiente', 'pagado', 'cancelado'
| estadoPago                   |  ej: 'pendiente', 'aprobado', 'rechazado'
| origen                       |  ej: 'web'
| referenciaPago               |  id de la pasarela de pago
+------------------------------+

* idCliente puede ser opcional si permitís compras como invitado en el MVP.

+------------------------------+
|         ItemsPedido          |
+------------------------------+
| idItem (PK)                  |
| idPedido (FK)                |
| idVariante (FK)              |
| cantidad                     |
| precioUnitario               |
| subtotal                     |
+------------------------------+

```

## 5.5. Relaciones y cardinalidades (resumen)

- **Categorias 1–N Productos**  
  Una categoría puede tener muchos productos.

- **Lineas 1–N Productos**  
  Una línea (Tradicional, Zodíaco, Primavera, etc.) agrupa varios productos.

- **Recipientes 1–N Productos**  
  Un tipo de recipiente (frasco 100cc tapa negra, vaso 200cc tapa madera, etc.) puede usarse en varios productos.

- **Productos 1–N VariantesProducto**  
  Un producto base puede tener muchas variantes (una por fragancia).

- **Fragancias 1–N VariantesProducto**  
  Una fragancia puede estar asociada a varias configuraciones de producto.

- **Pedidos 1–N ItemsPedido**  
  Un pedido tiene muchos ítems.

- **VariantesProducto 1–N ItemsPedido**  
  Cada ítem del pedido hace referencia a una variante concreta (producto + fragancia).

- **Clientes 1–N Pedidos**  
  Un cliente puede tener varios pedidos históricos.

---

## 5.6. Ejemplo concreto

#### Productos

idProducto = P001
nombreComercial = "Vela 100cc en frasco de vidrio con tapa negra"
idLinea = L-TRADICIONAL
idCategoria = CAT-VELAS
idRecipiente = REC-100-VIDRIO-TAPA-NEGRA


#### Fragancias

idFragancia = F-LEMONGRASS
idFragancia = F-VAINILLA
idFragancia = F-SANDALO


#### VariantesProducto

V001 → P001 + F-LEMONGRASS (stock 10)
V002 → P001 + F-VAINILLA (stock 0) → aparece deshabilitada
V003 → P001 + F-SANDALO (stock 5)


#### ¿Qué ve el usuario en la ficha de producto?

- Información del **producto base**:
  - Descripción  
  - Tamaño  
  - Recipiente  
  - Línea  
  - Categoría  

- **Selector de fragancias**:
  - Lemongrass — *seleccionable*  
  - Vainilla — *sin stock (gris, deshabilitada)*  
  - Sándalo — *seleccionable*  

El usuario elige una fragancia y se mapea directamente a la variante correspondiente.

---
