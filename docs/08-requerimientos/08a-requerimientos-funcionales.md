# 08a – Requerimientos Funcionales (RF)  
Versión 1.0

---

# 1. Introducción

Este documento lista y estructura los **requerimientos funcionales** del sistema e-commerce AUMA.  
Los RF describen funcionalidades concretas que el sistema debe implementar.

Se organizan por módulos para facilitar su lectura, mantenimiento y trazabilidad.

---

# 2. Requerimientos Funcionales

## 2.1. Módulo de Catálogo

### RF-01  
El sistema debe permitir visualizar un catálogo de productos disponibles.

### RF-02  
El sistema debe permitir filtrar productos por categoría.

### RF-03  
El sistema debe permitir realizar búsquedas por nombre, aroma o palabra clave.

### RF-04  
El sistema debe mostrar el detalle de un producto incluyendo nombre, descripción, aroma, imágenes, precio y stock.

### RF-05  
El administrador debe poder agregar, editar o eliminar productos.

---

## 2.2. Módulo de Carrito y Checkout

### RF-06  
El usuario debe poder agregar productos al carrito.

### RF-07  
El usuario debe poder ajustar cantidades del carrito.

### RF-08  
El usuario debe poder eliminar productos del carrito.

### RF-09  
El sistema debe permitir iniciar un proceso de checkout con resumen del pedido.

### RF-10  
El sistema debe calcular el total del pedido automáticamente.

---

## 2.3. Módulo de Autenticación (Post-MVP)

### RF-11  
El sistema debe permitir el registro mediante Amazon Cognito.

### RF-12  
El sistema debe permitir inicio de sesión de clientes registrados.

### RF-13  
Los usuarios deben poder acceder a su perfil.

### RF-14  
El sistema debe permitir recuperación de contraseña.

---

## 2.4. Módulo de Pedidos

### RF-15  
El sistema debe generar una orden al finalizar el checkout.

### RF-16  
El sistema debe registrar los datos del cliente asociados al pedido.

### RF-17  
El administrador debe poder visualizar todas las órdenes.

### RF-18  
El administrador debe poder modificar el estado de las órdenes.

### RF-19  
El cliente autenticado debe poder ver sus pedidos (futuro).

---

## 2.5. Módulo de Pagos

### RF-20  
El sistema debe integrarse con una pasarela de pagos (Stripe / Mercado Pago).

### RF-21  
El sistema debe recibir confirmación de pago mediante webhook.

### RF-22  
El sistema debe asociar pagos confirmados a las órdenes correspondientes.

---

## 2.6. Módulo de Stock

### RF-23  
El sistema debe descontar stock automáticamente cuando una orden es confirmada.

### RF-24  
El administrador debe poder editar el stock.

### RF-25  
El sistema debe emitir alertas cuando el stock sea bajo.

---

## 2.7. Módulo Administrativo

### RF-26  
El panel admin debe requerir autenticación obligatoria.

### RF-27  
El panel admin debe mostrar estadísticas básicas de ventas.

### RF-28  
El administrador debe poder gestionar categorías de productos.

---

# 3. Conclusión

Este documento define el comportamiento funcional del sistema AUMA y constituye un insumo directo para el diseño, el desarrollo y la validación del e-commerce.

