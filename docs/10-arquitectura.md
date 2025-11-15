# 10 – Diseño Arquitectónico del Sistema  
Versión 1.0

---

# 1. Introducción

Este documento describe la arquitectura tecnológica del sistema e-commerce AUMA, detallando los componentes frontend, backend, base de datos, seguridad y servicios en la nube.

La solución está diseñada para ser escalable, segura y de bajo costo, utilizando servicios administrados de AWS.

Incluye:

- Arquitectura general  
- Frontend (React + AWS Amplify Hosting)  
- Backend serverless (API Gateway + Lambda)  
- DynamoDB como base de datos  
- Webhooks de pago  
- Seguridad mediante IAM y mejores prácticas  

---

# 2. Arquitectura General del Sistema

El sistema se basa en un enfoque serverless, sin servidores propios, reduciendo costos y mantenimiento.

## 2.1 Diagrama General (Vista de Alto Nivel)

```
       +----------------------+
       |     Cliente Web      |
       | (Navegador/Frontend) |
       +----------+-----------+
                  |
                  v
    +-------------------------------+
    |    AWS Amplify Hosting        |
    |   (Frontend React Build)      |
    +---------------+---------------+
                    |
                    v
        +-------------------------+
        |    API Gateway REST     |
        +-----------+-------------+
                    |
                    v
           +-----------------+
           |   AWS Lambda    |
           | (Funciones API) |
           +-----------------+
                    |
                    v
       +---------------------------+
       |         DynamoDB          |
       | (Tablas: productos,       |
       |  variantes, clientes,     |
       |  pedidos, items)          |
       +---------------------------+

                   +      
                   | Webhook Pago
                   v
           +-------------------+
           | Pasarela de Pago |
           +-------------------+

```
---

# 3. Arquitectura del Frontend

El frontend será una Single Page Application (SPA) construida con:

- React + Vite  
- Componentes reutilizables  
- Consumo de API Gateway  
- Select de fragancias mapeado a VariantesProducto  

El sitio será publicado con AWS Amplify Hosting, con:

- Deploy automático desde GitHub  
- HTTPS habilitado  
- Redirects para todas las rutas (SPA mode)  
- Cache optimizada  

## 3.1 Estructura Lógica del Frontend
```
src/
├── components/
├── pages/
│   ├── Home.jsx
│   ├── Catalogo.jsx
│   ├── Producto.jsx
│   ├── Carrito.jsx
│   ├── Checkout.jsx
│   └── Confirmacion.jsx
├── hooks/
├── services/
│   └── api.js
└── context/
    └── carritoContext.jsx
```

## 3.2 Interacción con Backend

- Las páginas consumen endpoints de API Gateway.  
- El carrito se guarda en Context + localStorage.  
- En la ficha de producto:
  - Se muestra el producto base (tamaño, recipiente, línea, categoría).
  - Se listan las variantes disponibles por fragancia.
  - Variantes con stock 0 aparecen deshabilitadas.

---

# 4. Arquitectura del Backend (Serverless)

El backend utilizará:

- AWS Lambda (Node.js)  
- API Gateway (REST)  
- DynamoDB (base de datos principal)

## 4.1 Diagrama Backend

```
Cliente Web
    |
    v
+----------------+
|  API Gateway   |
+--------+-------+
         |
         v
+--------------------+
|     AWS Lambda     |
|    (controladores) |
+---------+----------+
          |
          v
+--------------------+
|      DynamoDB      |
+--------------------+
```

## 4.2 Endpoints (propuestos)

### Productos
- GET /productos  
- GET /productos/{id}  
- GET /productos/{id}/variantes  

### Pedidos
- POST /pedidos  
- GET /pedidos/{id}  

### Admin
- POST /admin/productos  
- POST /admin/variantes  

### Webhook de Pago
- POST /pagos/webhook  

---

# 5. Arquitectura de Datos

La base se implementará en DynamoDB organizada en tablas independientes.

## 5.1 Tablas Principales

| Tabla             | Descripción                                     |
|-------------------|--------------------------------------------------|
| Productos         | Producto base (tamaño, recipiente, línea…)       |
| VariantesProducto | SKU vendible (producto + fragancia)              |
| Categorias        | Categorías del catálogo                          |
| LineasProducto    | Líneas de colección                              |
| Recipientes       | Tipos de envases                                 |
| Fragancias        | Fragancias disponibles                           |
| Pedidos           | Datos del pedido                                 |
| ItemsPedido       | Ítems del pedido                                 |
| Clientes          | Datos del cliente                                |

## 5.2 Índices recomendados

- GSI1 → productos por categoría  
- GSI2 → productos por línea  
- GSI3 → variantes por idProducto  
- GSI4 → pedidos por idCliente  

---

# 6. Integraciones Externas

## 6.1 Pasarela de Pago (Webhook)

Flujo:

Cliente → Pasarela de Pago → Webhook → API Gateway → Lambda → DynamoDB


El webhook:

- valida firma  
- actualiza estado del pedido  
- registra referencia de pago  
- actualiza stock  
- genera logs  

---

# 7. Seguridad y Permisos

### 7.1 IAM Roles

**LambdaRole**  
- Lectura/escritura DynamoDB  
- Logs CloudWatch  

**AmplifyHostingRole**  
- Deploy automático desde GitHub  

**APIGatewayRole**  
- Permiso para invocar Lambdas  

### 7.2 Seguridad de API

- CORS restringido a dominio AUMA  
- Rate limiting en API Gateway  
- Validación de payload en Lambda  
- MVP sin Cognito (autenticación se agrega post-MVP)

---

# 8. Flujos Críticos del Sistema

## 8.1 Ver producto

Frontend → GET /productos/{id} → Lambda → DynamoDB → Frontend

## 8.2 Agregar al carrito  
Interno del navegador (no usa backend).

## 8.3 Crear pedido

Frontend → POST /pedidos → Lambda → DynamoDB

## 8.4 Confirmación de pago

Pasarela → Webhook → API Gateway → Lambda → DynamoDB


---

# 9. Conclusión

La arquitectura propuesta permite un sistema e-commerce:

- escalable  
- económico  
- seguro  
- fácil de mantener  

Basado 100% en servicios administrados de AWS, sin necesidad de servidores propios.

Este diseño sirve como base para las siguientes etapas:  
implementación del backend, desarrollo del frontend, pruebas y despliegue final.

