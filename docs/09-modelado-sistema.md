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

# 3.3. Descripción de Casos de Uso

## UC1 – Ver Catálogo
**Actor:** Cliente  
**Descripción:** El usuario accede al listado de productos.  
**Flujo principal:**  
1. El usuario ingresa al sitio.  
2. El sistema muestra el catálogo.  

**RF asociados:** RF-01, RF-02, RF-03

---

## UC2 – Ver Detalle de Producto
**Actor:** Cliente  
**Flujo:**  
1. El usuario selecciona un producto.  
2. El sistema muestra la ficha completa.  

**RF asociados:** RF-04

---

## UC3 – Agregar al Carrito
**Actor:** Cliente  
**RF asociados:** RF-06

---

## UC4 – Gestionar Carrito
**Actor:** Cliente  
**RF asociados:** RF-07, RF-08, RF-10

---

## UC5 – Finalizar Compra
**Actor:** Cliente  
**RF asociados:** RF-09, RF-10, RF-15

---

## UC6 – Registrarse (post-MVP)
**Actor:** Cliente  
**RF asociados:** RF-11

---

## UC7 – Iniciar Sesión (post-MVP)
**Actor:** Cliente  
**RF asociados:** RF-12

---

## UC8 – Ver Pedidos (post-MVP)
**Actor:** Cliente registrado  
**RF asociados:** RF-19

---

## UC9 – ABM Productos
**Actor:** Administrador  
**RF asociados:** RF-05

---

## UC10 – Gestionar Pedidos
**Actor:** Administrador  
**RF asociados:** RF-17, RF-18

---

## UC11 – Confirmar Pago (Webhook)
**Actor:** Pasarela de Pago  
**RF asociados:** RF-20, RF-21, RF-22

---

# 4. Diagramas de Flujo de Datos (DFD)

## 4.1. DFD Nivel 0 – Vista General

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
   | 1. Selecciona productos
   v
[Proceso 1: Carrito]
   |
   | 2. Confirma checkout
   v
[Proceso 2: Crear Orden]
   |
   | 3. Genera registro
   v
[BD Pedidos]
   |
   | 4. Redirige a pago
   v
Pasarela de Pago
   |
   | 5. Envía webhook (OK)
   v
[Proceso 3: Confirmar Pago]
   |
   | 6. Actualiza stock
   v
[BD Productos]
```

## 5. Modelo de Datos (DER Lógico)

Basado en DynamoDB (NoSQL), representado con estructura DER para documentación.

```
+-------------+          +------------------+          +-------------+
|  Productos  | 1 ---- * |   ItemsPedido    | * ---- 1 |   Pedidos   |
+-------------+          +------------------+          +-------------+
| idProducto  |          | idItem           |          | idPedido     |
| nombre      |          | idProducto (FK)  |          | idCliente    |
| categoria   |          | cantidad         |          | fecha        |
| precio      |          | subtotal         |          | total        |
| stock       |                                           estado      |
+-------------+                                           pago        +
                                                          +------------+

+-------------+
|  Clientes   |
+-------------+
| idCliente   |
| nombre      |
| email       |
| direccion   |
+-------------+
```
... en proceso
