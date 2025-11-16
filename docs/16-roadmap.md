# 16 – Roadmap del Proyecto AUMA  
Versión 1.0

---

# 1. Introducción

El objetivo de este documento es presentar el **plan de evolución del sistema AUMA**, organizado en fases que permiten escalar el e-commerce de manera ordenada, segura y rentable.  
El roadmap refleja:

- La visión general del proyecto  
- Las prioridades del MVP  
- Las funcionalidades planificadas para futuras versiones  
- La estrategia de crecimiento del sistema sobre AWS  

Este documento actúa como guía estratégica para el equipo de desarrollo y para la dirección del proyecto.

---

# 2. Objetivos del Roadmap

- Definir una **secuencia lógica** de incorporación de funcionalidades.  
- Asegurar que el producto crezca sin comprometer estabilidad.  
- Priorizar tareas que aportan valor inmediato al usuario.  
- Mantener un equilibrio entre nuevas funciones, mejoras y aspectos técnicos.  

---

# 3. Fases del Roadmap

El proyecto se organiza en **cinco fases**:

1. **MVP – Lanzamiento base en AWS**  
2. **Fase 2 – Integración con pagos reales**  
3. **Fase 3 – Autenticación y módulo de clientes**  
4. **Fase 4 – Panel admin avanzado y analytics**  
5. **Fase 5 – Funcionalidades premium y expansión**

A continuación se detalla cada una.

---

# 4. Fase 1: MVP – Funcionalidades esenciales (Versión 1.0)

> Estado: **En desarrollo / finalización**  
> Objetivo: Publicar la primera versión funcional del e-commerce.

## Incluye:

### 🔹 Frontend
- Catálogo de productos  
- Filtros básicos por categoría y línea  
- Ficha de producto  
- Selector de fragancias (variantes)  
- Carrito local  
- Checkout con datos básicos  
- Pantalla de confirmación  

### 🔹 Backend (Lambda)
- Listado de productos  
- Detalle + variantes  
- Creación de pedidos (estado pendiente)  
- ABM básico de productos y variantes  
- Gestión simple de pedidos (admin)  

### 🔹 Infraestructura
- Frontend en **AWS Amplify Hosting**  
- Backend en **Lambda + API Gateway**  
- Base de datos completa en **DynamoDB**  
- IAM y CloudWatch configurados  

### 🔹 No incluye:
- Pagos reales  
- Autenticación  
- Panel admin avanzado  

---

# 5. Fase 2: Integración de Pagos Reales (Versión 1.1)

> Objetivo: permitir pagos reales y automatizar cambios de estado.

## Funcionalidades:

- Integración con pasarela (Mercado Pago / Stripe).  
- Generación automática de preferencia/checkout.  
- Endpoint `/pagos/webhook` para recibir notificaciones.  
- Validación de firma del webhook.  
- Actualización automática del estado del pedido.  
- Actualización automática del stock.  
- Pantalla de éxito/error según resultado del pago.  

## Impacto técnico:

- Nuevas lambdas → `crearPago`, `procesarWebhook`.  
- Nuevos registros en DynamoDB: referencia de pago.  
- Configuración de CORS / secretos.  

---

# 6. Fase 3: Autenticación y módulo de clientes (Versión 2.0)

> Objetivo: permitir fidelización y compras con cuenta.

## Funcionalidades:

- Registro de usuarios (Cognito)  
- Login / Logout  
- Perfil de cliente  
- Historial de pedidos  
- Datos de envío almacenados  
- Checkout inteligente (autocompleta datos)  

## Beneficios:

- Recompra simple  
- Marketing futuro (emails segmentados)  

---

# 7. Fase 4: Panel Administrativo Avanzado (Versión 2.5)

> Objetivo: mejorar la gestión interna del negocio.

## Funcionalidades:

- Vista administradora mejorada  
- Dashboard de ventas y analytics  
- Reportes de:
  - productos más vendidos
  - ventas por línea/categoría
  - stock proyectado  
- Gestión avanzada de variantes (bulk update)  
- Gestión de usuarios (rol admin)  
- Control de logs y auditoría  

## Mejoras técnicas:

- Amplify o S3 + CloudFront para panel admin separado  
- Endpoints protegidos por API Keys o autorización Cognito  

---

# 8. Fase 5: Expansión y funcionalidades premium (Versión 3.0)

> Objetivo: escalar AUMA y sumar valor agregado al cliente.

## Funcionalidades previstas:

- Wishlist / Favoritos  
- Cupones y descuentos  
- Listas inteligentes (“especiales del mes”)  
- Envíos avanzados (tarifas dinámicas, integración logística)  
- Multi-idioma (ES / EN)  
- Productos digitales / packs especiales  
- Lineas temáticas automáticas (horóscopo, estaciones, etc.)  

## Opciones futuras:
- Aplicación móvil (React Native)  
- Notificaciones push / email marketing  
- Chatbot integrado  
- Segmentación por comportamiento  

---

# 9. Evolución técnica proyectada

Durante la evolución del proyecto, AUMA puede incorporar:

- **Lambdas más modulares** (arquitectura hexagonal)  
- **Sistemas de cache** con DynamoDB Accelerator (DAX)  
- **CI/CD completo** (Amplify + GitHub Actions)  
- **Infra como código** (AWS CDK / Terraform)  
- **Monitoreo avanzado** con CloudWatch Dashboard  

Estas mejoras se incorporan progresivamente según el crecimiento del negocio.

---

# 10. Conclusión

El roadmap presentado organiza la evolución del e-commerce AUMA en fases claras, priorizando:

- valor inmediato,  
- escalabilidad técnica,  
- facilidad de mantenimiento,  
- costos controlados,  
- y crecimiento sostenido sobre la infraestructura AWS.

Este documento guía la continuidad del proyecto y permite planificar iteraciones futuras de forma sólida y estratégica.

---
