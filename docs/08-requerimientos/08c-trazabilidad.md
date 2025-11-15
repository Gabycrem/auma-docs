# 08c – Matriz de Trazabilidad  
Versión 1.0

---

# 1. Introducción

La matriz de trazabilidad permite relacionar las **historias de usuario**, los **requerimientos funcionales** y los **componentes del sistema**, asegurando que cada funcionalidad solicitada tenga una implementación asociada.

---

# 2. Matriz de Trazabilidad HU → RF → Componente

| Historia de Usuario | Requerimiento Funcional Asociado | Componente / Módulo |
|---------------------|----------------------------------|---------------------|
| HU-01 Ver catálogo | RF-01, RF-02, RF-03 | Catálogo / Frontend |
| HU-02 Ver detalle de producto | RF-04 | Catálogo / Frontend |
| HU-03 Agregar al carrito | RF-06, RF-07 | Carrito |
| HU-04 Gestionar carrito | RF-07, RF-08, RF-10 | Carrito |
| HU-05 Finalizar compra | RF-09, RF-10, RF-15 | Checkout / Órdenes |
| HU-06 Registrarme | RF-11, RF-12 | Autenticación |
| HU-07 Consultar mis pedidos | RF-19 | Pedidos |
| HU-08 Admin ABM productos | RF-05 | Panel Admin |
| HU-09 Ver órdenes | RF-17, RF-18 | Panel Admin / Pedidos |
| HU-10 Recibir confirmación de pago | RF-20, RF-21, RF-22 | Pagos / Webhooks |

---

# 3. Conclusión

La matriz asegura:
- coherencia entre requerimientos y funcionalidades,  
- cobertura completa de las necesidades,
- trazabilidad del desarrollo y las pruebas.

Este documento se actualizará a medida que evolucionen las historias de usuario o se incorporen nuevas funcionalidades.

