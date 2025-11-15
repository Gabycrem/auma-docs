# Funcionalidades – MVP vs Fuera de Alcance  
## Proyecto: AUMA – Tienda Online (MVP)

---

## ✅ 1. Funcionalidades incluidas en el MVP (Sí o sí)

Estas funcionalidades constituyen el Producto Mínimo Viable (MVP) necesario para que la tienda online AUMA funcione, permita validar la experiencia de compra y represente correctamente la identidad de la marca.

### 1.1. Catálogo de Productos
- Ver listado de productos disponibles (velas de cera de soja aromáticas).
- Filtrar por categoría básica.
- Ver detalle completo de un producto:
  - Nombre
  - Aroma
  - Descripción sensorial
  - Formato
  - Precio
  - Imagen del producto

### 1.2. Carrito de Compras
- Agregar productos al carrito desde el catálogo o desde el detalle.
- Visualizar carrito con lista de productos seleccionados.
- Modificar cantidades (opcional).
- Confirmar pedido (checkout simple / simulado).

### 1.3. Órdenes (Checkout Básico)
- Flujo para confirmar pedido.
- Registro básico de la orden (simulado o guardado mínimo).
- Pantalla de confirmación del pedido.

> No se incluye integración con pasarelas de pago.  
> El flujo puede ser simulado.

### 1.4. Autenticación Básica
- Registro de usuario (email + contraseña).
- Inicio de sesión básico.
- Cerrar sesión.

> Solo se utiliza para acceder al panel administrativo.  
> No incluye funcionalidades avanzadas de cuenta.

### 1.5. Panel de Administración (ABM de productos)
- Acceso restringido por autenticación.
- Crear productos.
- Editar productos existentes.
- Eliminar productos.
- Listar productos desde panel interno.

> Panel simple sin roles, estadísticas ni configuraciones avanzadas.

---

## ❌ 2. Funcionalidades fuera de alcance (por ahora)

Estas funcionalidades **NO** se desarrollarán en esta primera versión del proyecto para mantener el MVP simple, alcanzable y orientado a validar la propuesta de AUMA.

### 2.1. Funcionalidades Avanzadas
- Cupones de descuento.
- Wishlist / favoritos.
- Reviews y calificaciones de productos.
- Multi-idioma.
- Comparador de productos.

### 2.2. Checkout y Clientes
- Integración real con Mercado Pago, Stripe, PayPal u otros.
- Cálculo de envíos dinámico.
- Seguimiento de envíos en tiempo real.
- Carrito persistente entre sesiones.
- Múltiples direcciones de envío.
- Gestión avanzada de usuarios (perfiles, historial de compras, recuperación de contraseña avanzada).

### 2.3. Panel Administrativo Avanzado
- Dashboard con estadísticas y métricas.
- Gestión de roles de usuario.
- Editor visual de páginas.
- Gestión de cupones desde el panel.
- Administración de múltiples colecciones o marcas.

### 2.4. Marketing y Automatizaciones
- Emails automáticos (pedido recibido, carrito abandonado, etc.).
- Notificaciones push.
- Campañas automatizadas.

### 2.5. Arquitectura y Escalabilidad Avanzada
- Microservicios.
- API Gateway.
- Bases de datos avanzadas en producción.
- Integración con CRM, ERP u otros sistemas externos.

---

## 🧩 3. Relación con la Visión del Proyecto

Este documento acompaña a la Visión y Alcance del Proyecto definido en el Sprint 0, delimitando **qué se construirá ahora** y **qué se deja para próximas versiones**.

El MVP se enfoca en:
- Validar el flujo de navegación y compra.
- Mostrar el catálogo básico de AUMA.
- Permitir registrar un pedido simple.
- Contar con un panel mínimo para mantener el catálogo.
- Desplegar en AWS usando Amplify con CI/CD.

---

## ✔️ 4. Ubicación Final del Documento

Guardar este archivo en:

