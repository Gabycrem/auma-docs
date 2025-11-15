# 07 – Alcance del Proyecto  
Versión 1.0

---

# 1. Introducción

El presente documento define el **alcance del proyecto AUMA**, especificando qué funcionalidades incluirá el sistema en su versión completa, qué entregables formarán parte de cada fase y qué elementos quedan explícitamente fuera del alcance actual.  

Este capítulo es fundamental para orientar el desarrollo, evitar desviaciones y establecer criterios claros para la planificación del MVP y las etapas posteriores.

---

# 2. Objetivo del Proyecto

El objetivo general del proyecto es **desarrollar un sistema e-commerce completo para AUMA**, que permita gestionar productos, ventas, stock, usuarios, pagos y operaciones administrativas de forma automatizada, profesional y escalable.

El sistema deberá:

- digitalizar procesos hoy manuales,  
- facilitar la gestión diaria,  
- mejorar la experiencia del cliente,  
- ofrecer un canal de ventas moderno e independiente de redes sociales,  
- sentar bases sólidas para crecimiento futuro.

---

# 3. Alcance General del Sistema

El proyecto completo incluirá:

## **3.1. Tienda Online (Frontend)**
- Página principal con presentación de marca.  
- Catálogo de productos.  
- Filtros por categoría.  
- Búsqueda interna.  
- Detalle de producto (fotos, descripciones, aroma, precio, stock).  
- Carrito de compras.  
- Checkout.  
- Estado del pedido (futuro).  

---

## **3.2. Backend y Servicios**
- API REST / serverless sobre AWS Lambda.  
- Base de datos NoSQL (DynamoDB).  
- Control de stock automatizado.  
- Gestión de productos y categorías.  
- Gestión de pedidos.  
- Procesamiento de pagos mediante integración (webhooks).  
- Autenticación y autorización con Amazon Cognito.  
- Registro estructurado de usuarios y órdenes.  

---

## **3.3. Panel Administrativo**
- Login de administrador.  
- Alta, baja y modificación de productos.  
- Gestión de imágenes.  
- Control de stock.  
- Consulta de órdenes.  
- Actualización de estado de pedido.  
- Visualización de métricas básicas (ventas, productos vendidos, stock crítico).  

---

## **3.4. Integraciones Externas**
- Pasarela de pagos (Mercado Pago / Stripe).  
- Webhooks para confirmación automática.  
- Posible integración futura con servicios de envío.  

---

## **3.5. Arquitectura y DevOps**
- Hosting con AWS Amplify.  
- Despliegue continuo (CI/CD).  
- Uso de S3 para assets.  
- Logs y monitoreo con CloudWatch.  
- Control de versiones en GitHub.  

---

# 4. Alcance del MVP (Primera Fase)

El MVP se centrará en validar la experiencia de usuario y la identidad digital de AUMA.  

Incluye:

### **4.1. Funcionalidades incluidas**
- Catálogo básico de productos.  
- Detalle de producto.  
- Carrito de compras (con almacenamiento temporal).  
- Flujo de “simular pedido” o checkout básico.  
- Panel admin sencillo para cargar productos (manual).  
- Hosting y deploy en AWS.  
- Estructura inicial de API (mock o versión simplificada).  

### **4.2. Limitaciones del MVP**
- No habrá cupones.  
- No habrá multi-idioma.  
- No habrá usuarios avanzados.  
- No habrá tracking de pedido.  
- El pago puede ser simulado o básico.  
- Reportes mínimos o nulos.  
- Stock administrado manualmente.  

---

# 5. Alcance de Implementaciones Futuras (Post-MVP)

Una vez validado el MVP, se continuarán funcionalidades más avanzadas.

## **5.1. Autenticación avanzada**
- Registro y login real con Amazon Cognito.  
- Perfil del usuario.  
- Recuperación de contraseña.  

## **5.2. Backend completo**
- API real con Lambda + API Gateway.  
- DynamoDB con tablas para usuarios, órdenes y productos.  

## **5.3. Pagos reales**
- Integración con Mercado Pago/Stripe.  
- Webhooks para validar pagos.  
- Estado del pedido automático.  

## **5.4. Panel administrativo completo**
- Reportes básicos.  
- Variantes y categorías avanzadas.  
- Gestión profesional de stock.  

## **5.5. Experiencia del cliente**
- Historial de compras.  
- Seguimiento de pedido.  
- Correos automatizados (notificaciones).  

---

# 6. Fuera de Alcance (hasta nueva versión)

Quedan explícitamente excluidos:

- Multi-idioma.  
- Multi-moneda.  
- Marketplace multi-vendedor.  
- Automatización de marketing (email marketing, flujos, CRM).  
- Dashboard analítico avanzado.  
- Sistema de fidelización / puntos.  
- Envíos internacionales.  
- App móvil nativa.  
- Módulos contables avanzados.

---

# 7. Entregables del Proyecto

## **7.1. Documentación**
- Presentación de la empresa  
- Relevamiento y análisis TGS  
- Requerimientos funcionales y no funcionales  
- Modelado (diagramas)  
- Plan de implementación  

## **7.2. Componentes Técnicos**
- Frontend completo  
- Backend serverless  
- Base de datos  
- Panel admin  
- Integraciones de pago  
- Despliegue en AWS  

---

# 8. Conclusión

El alcance definido permite implementar un sistema capaz de profesionalizar AUMA y acompañar su crecimiento comercial. El MVP establece una base sólida para validar el modelo de negocio digital, mientras que las versiones posteriores ampliarán la funcionalidad hasta completar un e-commerce moderno, seguro y escalable.

Este documento servirá como referencia para la elaboración de los requerimientos y la planificación técnica del proyecto.

---

**Ubicación del archivo:**  
`docs/07-alcance-proyecto.md`

