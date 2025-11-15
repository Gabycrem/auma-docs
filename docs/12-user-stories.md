# 12 – Historias de Usuario  
Versión 2.0

---

# 1. Introducción

Este documento recopila las **historias de usuario del sistema AUMA**, organizadas por roles y clasificadas entre:

- **MVP**: funcionalidades mínimas indispensables para el primer lanzamiento.  
- **Post-MVP**: funcionalidades que corresponden a versiones posteriores.

Las historias siguen el formato:

> “Como [rol], quiero [acción] para [beneficio].”

---

# 2. Roles del sistema

AUMA contempla cuatro roles principales:

1. **Visitante**  
   Usuario no autenticado que navega, consulta productos y puede realizar pedidos sin crear una cuenta.

2. **Cliente registrado** *(Post-MVP)*  
   Usuario autenticado que accede a funciones personalizadas.

3. **Administrador**  
   Usuario con permisos para gestionar catálogo y pedidos.

4. **Sistema externo (Webhook de pago)**  
   Actor automático que notifica el resultado de los pagos.

---

# 3. Historias de Usuario – MVP

## 3.1 Visitante (MVP)

1. **Como visitante, quiero ver el catálogo de productos para conocer la oferta de AUMA.**
2. **Como visitante, quiero filtrar productos por categoría o línea para encontrar lo que me interesa más rápido.**
3. **Como visitante, quiero ver el detalle de un producto para conocer su tamaño, fragancias disponibles y tipo de recipiente.**
4. **Como visitante, quiero seleccionar una fragancia disponible para un producto para elegir la opción exacta que deseo comprar.**
5. **Como visitante, quiero agregar una variante de producto al carrito para iniciar la compra sin registrarme.**
6. **Como visitante, quiero ver mi carrito para revisar los productos agregados.**
7. **Como visitante, quiero modificar las cantidades en el carrito para ajustar mi pedido.**
8. **Como visitante, quiero eliminar ítems del carrito para corregir errores o cambios de intención.**
9. **Como visitante, quiero iniciar el checkout para confirmar mi pedido.**
10. **Como visitante, quiero confirmar el pedido para que AUMA reciba mis datos y mi orden.**
11. **Como visitante, quiero llegar a una pantalla de confirmación después del checkout para asegurarme de que el pedido se generó correctamente.**

---

## 3.2 Administrador (MVP)

1. **Como administrador, quiero crear productos base para mantener actualizado el catálogo.**
2. **Como administrador, quiero editar productos base para corregir información o actualizar datos.**
3. **Como administrador, quiero desactivar productos para evitar mostrar artículos que ya no están disponibles.**
4. **Como administrador, quiero crear variantes de producto para gestionar fragancias, precio y stock.**
5. **Como administrador, quiero editar el stock de una variante para reflejar disponibilidad real.**
6. **Como administrador, quiero ver el listado de pedidos para gestionar el flujo de ventas.**
7. **Como administrador, quiero actualizar el estado de un pedido para avanzar su procesamiento (ej.: recibido, en preparación, listo).**

---

## 3.3 Sistema (Webhook de pago) – MVP Simulado  
*(En MVP se simula el pago, pero igual se registra la historia por consistencia)*

1. **Como sistema, quiero registrar el estado del pedido como “pendiente de pago” para mantener el flujo del checkout.**

---

# 4. Historias de Usuario – Post-MVP

## 4.1 Cliente Registrado (Post-MVP)

1. **Como cliente registrado, quiero crear una cuenta para guardar mis datos y facilitar futuras compras.**
2. **Como cliente registrado, quiero iniciar sesión para acceder a mis pedidos y datos.**
3. **Como cliente registrado, quiero ver mi historial de pedidos para recordar lo que compré.**
4. **Como cliente registrado, quiero actualizar mis datos personales para mantener mi información vigente.**
