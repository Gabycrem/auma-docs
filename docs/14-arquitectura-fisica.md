# 14 – Arquitectura Física e Infraestructura AWS  
Versión 1.0

---

# 1. Introducción

Este documento describe la **arquitectura física, los componentes de infraestructura y los servicios AWS** utilizados para implementar el e-commerce AUMA.

Mientras que el Documento 10 explica la **arquitectura lógica**, este documento detalla la **distribución real en la nube**, los servicios involucrados, sus zonas, relaciones y justificaciones técnicas.

---

# 2. Objetivo de la arquitectura física

- Desplegar un e-commerce completo sin administrar servidores.  
- Minimizar costos gracias al modelo serverless.  
- Garantizar alta disponibilidad y escalabilidad automática.  
- Integrar servicios de AWS de forma segura y desacoplada.  
- Permitir un pipeline de despliegue rápido basado en GitHub.

---

# 3. Servicios AWS utilizados

AUMA se apoya en un conjunto de servicios administrados:

| Servicio AWS        | Descripción breve |
|---------------------|-------------------|
| **Amplify Hosting** | Hosting del frontend (React SPA). |
| **API Gateway**     | Exposición de API REST hacia el frontend. |
| **AWS Lambda**      | Backend serverless para lógica de negocio. |
| **DynamoDB**        | Base de datos NoSQL para productos, variantes y pedidos. |
| **CloudWatch**      | Logs, métricas y monitoreo de Lambdas. |
| **IAM**             | Control de permisos y roles de ejecución. |
| **S3 (estático opcional)** | Almacenamiento de assets o imágenes del catálogo. |
| **Pasarela de Pago externa** | Webhooks de confirmación de pago (post-MVP). |

En futuras fases se podrá integrar:

- **Cognito** (post-MVP): autenticación y manejo de sesiones.  
- **SNS/SES** (post-MVP): notificaciones por email o SMS.  

---

# 4. Diagrama de Arquitectura Física (Vista AWS)

```
                  ┌─────────────────────────┐
                  │      Usuario / Web      │
                  └───────────┬─────────────┘
                              │
                              ▼
             ┌──────────────────────────────────┐
             │       AWS Amplify Hosting        │
             │ (Build + Deploy + HTTPS + CDN)   │
             └───────────┬──────────────────────┘
                         │
                         ▼
                ┌────────────────┐
                │  API Gateway   │
                │ (REST Endpoints) │
                └─────────┬────────┘
                          │
                ┌─────────▼──────────┐
                │    AWS Lambda      │
                │ (Funciones lógica) │
                └─────────┬──────────┘
                          │
                ┌─────────▼──────────┐
                │     DynamoDB       │
                │(Productos/Var/Ped.)│
                └─────────┬──────────┘
                          │
          ┌───────────────▼────────────────┐
          │      CloudWatch Logs & Metrics │
          └────────────────────────────────┘


  ┌───────────────────────────────┐
  │     Pasarela de Pago (EXT)    │
  │ Mercado Pago / Stripe / etc.  │
  └───────────┬───────────────────┘
              │ Webhook (post-MVP)
              ▼
        ┌───────────────┐
        │ API Gateway    │
        │ /pagos/webhook │
        └───────┬───────┘
                ▼
          ┌───────────┐
          │ Lambda     │
          │ (Validación│
          │   y update)│
          └────────────┘
```


---

# 5. Detalle de Componentes

## 5.1 AWS Amplify Hosting (Frontend)

- Aloja el sitio React SPA compilado.  
- Realiza deploy automático desde GitHub.  
- Provee CDN global con CloudFront.  
- Maneja HTTPS automáticamente mediante certificados.  
- Redirecciones configuradas para SPA (rewrites).

**Razones por las que se elige Amplify:**
- Simple, integrado y barato.  
- Deploy automático con un click.  
- Ideal para proyectos serverless.

---

## 5.2 API Gateway (Capa de API REST)

API Gateway expone los endpoints del backend:

- `/productos`
- `/productos/{id}`
- `/productos/{id}/variantes`
- `/pedidos`
- `/pagos/webhook` (post-MVP)
- `/admin/*` (panel de gestión)

**Funciones principales:**

- Peticiones HTTP → Lambdas  
- Validación de payload (opcional)  
- Throttling, rate limiting  
- Logs de acceso  
- CORS para permitir solo dominio de AUMA

---

## 5.3 AWS Lambda (Backend Serverless)

Cada funcionalidad importante se implementa como una Lambda:

- `getProductos`  
- `getProductoById`  
- `getVariantesByProducto`  
- `crearPedido`  
- `listarPedidos`  
- `actualizarEstadoPedido`  
- `crearProducto` (admin)  
- `crearVariante` (admin)  
- `webhookPago` (post-MVP)

**Ventajas:**

- Se ejecuta solo cuando se necesita.  
- Sin servidores ni mantenimiento.  
- Escalado automático.  
- Pago por uso real.  

---

## 5.4 DynamoDB (Base de Datos NoSQL)

Tablas:

- **Productos**  
- **VariantesProducto**  
- **Categorias**  
- **LineasProducto**  
- **Recipientes**  
- **Fragancias**  
- **Clientes**  
- **Pedidos**  
- **ItemsPedido**

Motores de acceso:

- Key-value para búsquedas rápidas  
- Queries por índices secundarios (GSI)  
- Esquema flexible, ideal para variantes por fragancia  

---

## 5.5 IAM (Seguridad y permisos)

Roles principales:

### **LambdaExecutionRole**
- Lectura/escritura DynamoDB  
- Logs en CloudWatch  

### **AmplifyServiceRole**
- Permisos de despliegue desde GitHub  

### **APIGatewayInvokeRole**
- Permiso para ejecutar funciones Lambda  

**Regla principal:**  
> *Principio de mínimo privilegio*  
Cada servicio solo puede hacer lo que estrictamente necesita.

---

## 5.6 CloudWatch (Monitoreo)

- Logs de ejecución de Lambdas  
- Alarmas ante fallas de API  
- Métricas de throughput, errores y latencia  

---

## 5.7 Pasarela de pago (Externa)

En el MVP se simula el pago.  
Post-MVP se integra:

- Mercado Pago, Stripe, o similar  
- Notificaciones por webhook  
- Validación de firma  
- Actualización de estado del pedido  

---

# 6. Arquitectura por Zonas (Regiones y AZs)

Para minimizar costos:

- Región sugerida: **us-east-1** (Virginia)  
- Servicios distribuidos automáticamente entre varias **AZs**:
  - Amplify (CDN global)  
  - API Gateway (multi-AZ)  
  - DynamoDB (multi-AZ, redundante)  
  - Lambda (multi-AZ)  

Alta disponibilidad sin configuración adicional.

---

# 7. Resumen del Flujo Físico Completo

1. El usuario accede a la web → servida por Amplify (CDN).  
2. El frontend realiza llamadas API a API Gateway.  
3. API Gateway invoca Lambdas correspondientes.  
4. Las Lambdas leen/escriben en DynamoDB.  
5. El usuario interactúa con carrito (local en front).  
6. Checkout → pedido en estado “pendiente”.  
7. (Post-MVP) Webhook de pago actualiza estado y stock.  
8. Admin gestiona productos y pedidos mediante endpoints protegidos.

---

# 8. Conclusión

La arquitectura física de AUMA está basada completamente en servicios administrados de AWS.  
Esto permite:

- costos mínimos,  
- escalabilidad automática,  
- cero mantenimiento de servidores,  
- seguridad integrada,  
- despliegue rápido,  
- alta disponibilidad.

Este diseño constituye una base sólida para el crecimiento futuro del e-commerce y soporta sin problemas el roadmap de funcionalidades definido.

---
