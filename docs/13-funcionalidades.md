# 13 – Funcionalidades del Sistema AUMA  
Versión 2.0

---

# 1. Introducción

Este documento describe las funcionalidades del sistema e-commerce AUMA, organizadas en:

- Funcionalidades del MVP  
- Funcionalidades Post-MVP  
- Módulos principales  
- Relación con requerimientos y user stories  

El objetivo es proporcionar una vista funcional clara del sistema, sin entrar en detalle técnico (cubierto en otros documentos).

---

# 2. Módulos principales del sistema

El sistema AUMA se organiza en los siguientes módulos:

1. Catálogo y navegación  
2. Ficha de producto (producto base + variantes)  
3. Carrito de compras  
4. Checkout y generación de pedidos  
5. Gestión de pedidos (admin)  
6. Gestión de catálogo (admin)  
7. Gestión de clientes (básica en MVP, completa en post-MVP)  
8. Webhooks y pagos (simulado en MVP, real en post-MVP)  
9. Autenticación y cuentas (post-MVP)

---

# 3. Funcionalidades del MVP

## 3.1. Catálogo y navegación

**F1 – Ver catálogo**  
El visitante puede ver todos los productos activos.  
Relación con RF: RF-01, RF-02, RF-03  
User stories: V-01

**F2 – Filtrar productos**  
Filtros simples por categoría y línea.  
User stories: V-02

---

## 3.2. Ficha de producto

**F3 – Ver detalle de producto**  
Incluye tamaño, volumen, recipiente, línea, categoría, y descripción.  
User story: V-03

**F4 – Ver fragancias por variante**  
Listar fragancias disponibles y deshabilitar las sin stock.  
User story: V-04

---

## 3.3. Carrito de compras

**F5 – Agregar variante al carrito**  
User story: V-05

**F6 – Ver carrito**  
User story: V-06

**F7 – Modificar cantidades / eliminar ítems**  
User stories: V-07, V-08

---

## 3.4. Checkout y pedidos

**F8 – Iniciar checkout**  
User story: V-09

**F9 – Crear pedido (estado inicial: pendiente)**  
User story: V-10

**F10 – Pantalla de confirmación**  
User story: V-11

---

## 3.5. Gestión de pedidos (Admin)

**F11 – Ver pedidos**  
User story: A-06

**F12 – Cambiar estado de pedido**  
User story: A-07

---

## 3.6. Gestión de catálogo (Admin)

**F13 – Crear producto base**  
User story: A-01

**F14 – Editar producto base**  
User story: A-02

**F15 – Desactivar producto**  
User story: A-03

**F16 – Crear variantes (fragancias, stock y precio)**  
User story: A-04, A-05

---

# 4. Funcionalidades Post-MVP

## 4.1. Autenticación y cuentas

**F17 – Registro de cliente**  
User story: C-01

**F18 – Inicio de sesión**  
User story: C-02

**F19 – Historial de pedidos**  
User story: C-03

---

## 4.2. Pasarela de pago + webhook real

**F20 – Redirección a pasarela de pago**  
User story: S-01

**F21 – Validación de webhook**  
User story: S-02

**F22 – Actualización de estado del pedido**  
User story: S-03

**F23 – Actualización de stock por pago aprobado**  
User story: S-04

---

## 4.3. Funcionalidades avanzadas

**F24 – Wishlist / Favoritos**  
**F25 – Dashboard de estadísticas**  
**F26 – Cupones y promociones**  
**F27 – Envíos avanzados / internacionales**  
**F28 – Multi-idioma**

---

# 5. Relación con otros documentos

- Requerimientos funcionales y no funcionales: docs/08/  
- Historias de usuario: docs/12-user-stories.md  
- Modelado del sistema: docs/09-modelado-sistema.md  
- Arquitectura del sistema: docs/10-arquitectura.md  

---

# 6. Estado del documento

Este documento define el alcance funcional del sistema para el MVP y versiones posteriores.  
Se actualiza con cada nueva iteración del roadmap o sprint planning.
