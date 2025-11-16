# 18 – Manual de Usuario AUMA  
Versión 1.0

---

# 1. Introducción

Este manual guía al **usuario final** en el uso del e-commerce AUMA, abarcando:

- Navegación general  
- Búsqueda y visualización de productos  
- Uso del carrito  
- Finalización de compra  
- Funciones adicionales (si tiene cuenta)  
- Funcionalidades del panel administrador  

---

# 2. Manual para Clientes / Visitantes

## 2.1 Ingreso al sitio

1. Abrir el navegador.  
2. Ingresar a la URL de AUMA.  
3. El usuario verá la **home** con productos y accesos al catálogo.

---

# 3. Navegación del Catálogo

### 3.1 Ver catálogo completo  
- Acceder mediante el menú **Catálogo**.  
- Se muestran todas las velas disponibles.

### 3.2 Filtrar productos  
El usuario puede filtrar por:

- Categoría  
- Línea  
- Tamaño  
- Fragancia (filtro opcional)  

### 3.3 Ver detalle de producto  
Al hacer clic en una card se abre:

- Nombre del producto  
- Descripción  
- Tamaño y tipo de recipiente  
- Línea y categoría  
- Lista de **fragancias disponibles**  
  - Si una fragancia está sin stock → aparece en gris y no es seleccionable  
- Precio  
- Botón **Agregar al carrito**

---

# 4. Carrito de Compras

## 4.1 Agregar al carrito  
1. Elegir fragancia.  
2. Seleccionar cantidad.  
3. Presionar **Agregar al carrito**.  

El carrito se actualiza automáticamente.

---

## 4.2 Ver carrito  
El usuario accede al ícono del carrito:

En esta vista puede:

- Ver todos los ítems  
- Cambiar la cantidad  
- Eliminar un producto  
- Ver el total  
- Continuar al Checkout  

---

# 5. Proceso de Checkout

1. Revisar el carrito.  
2. Presionar **Finalizar Compra**.  
3. Completar datos:  
   - Nombre  
   - Email  
   - Dirección (opcional en MVP)  
4. Confirmar pedido.  
5. Es redirigido a la pasarela de pago (una vez implementada).  

---

# 6. Confirmación de Pedido

Al finalizar la compra:

- Se muestra una página de **confirmación**.  
- Una vez implementados los pagos reales, se enviará un estado actualizado según el webhook.  

---

# 7. Funciones para Cliente Registrado (futuro)

- Iniciar sesión / cerrar sesión  
- Ver historial de pedidos  
- Guardar datos de entrega  
- Realizar recompras más rápido  

---

# 8. Manual para Administradores

El admin es el responsable de gestionar el catálogo desde una vista privada.

## 8.1 Iniciar sesión (post-MVP)
- Acceso mediante un login protegido por Cognito.

---

## 8.2 Panel principal
En el panel el admin puede ver:

- Lista de productos  
- Lista de variantes  
- Tabla de pedidos  

---

## 8.3 Gestión de Productos (ABM)

### Crear producto
1. Ir a **Productos → Crear nuevo**.  
2. Completar:  
   - Nombre comercial  
   - Línea  
   - Categoría  
   - Tipo de recipiente  
   - Volumen  
   - Descripción  
3. Guardar.

### Editar producto
- Seleccionar un producto y ajustar datos.

### Eliminar producto
- Opción *Eliminar* → el producto deja de estar disponible.

---

## 8.4 Gestión de Variantes

- Crear variantes con fragancia + precio + stock  
- Editar stock  
- Deshabilitar variante sin eliminarla  

---

## 8.5 Gestión de Pedidos

- Cambiar estado: pendiente → pagado → completado  
- Ver detalle del pedido  
- Filtrar por estado  

---

# 9. Conclusión

Este manual cubre todas las acciones esperadas del usuario y del administrador para operar la plataforma AUMA de manera adecuada.

---
