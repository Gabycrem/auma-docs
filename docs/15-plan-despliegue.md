# 15 – Plan de Despliegue  
Versión 1.0

---

# 1. Introducción

El objetivo de este documento es describir el **proceso de despliegue completo** del sistema e-commerce AUMA, desde el entorno local del equipo de desarrollo hasta la publicación final en AWS.

Incluye:

- Preparación del entorno  
- Configuración de repositorio  
- Deploy del frontend (Amplify)  
- Deploy del backend (API Gateway + Lambda)  
- Configuración de base de datos (DynamoDB)  
- Integración del webhook (post-MVP)  
- Validaciones antes de producción  
- Procedimiento ante fallas  

---

# 2. Objetivos del despliegue

- Publicar una versión funcional del MVP de AUMA.  
- Automatizar el proceso de publicación con GitHub.  
- Asegurar estabilidad, integridad de datos y correcta operación en AWS.  
- Permitir iteraciones rápidas durante el desarrollo.  

---

# 3. Requisitos previos

Antes de iniciar el despliegue, se deben cumplir:

## 3.1 Requisitos técnicos

- Repositorio GitHub actualizado  
- Proyecto de frontend compilable sin errores (`npm run build`)  
- Código del backend preparado para Lambda (Node.js)  
- Tablas de DynamoDB creadas correctamente  
- Roles IAM configurados (Amplify, LambdaExecutionRole, API Gateway)  
- Archivo `.env` local configurado para desarrollo *pero no subido a GitHub*  

---

# 4. Flujo general del despliegue

Desarrollo → Test local → Push GitHub → Build automático → Deploy AWS Amplify / Lambda → Pruebas en ambiente productivo


---

# 5. Despliegue del Frontend (AWS Amplify Hosting)

El frontend (React + Vite) se publica mediante **AWS Amplify Hosting**.

## 5.1 Pasos del despliegue inicial

1. Ingresar a **AWS Amplify**.  
2. Seleccionar **New App → Host Web App**.  
3. Conectar con **GitHub**.  
4. Elegir el repositorio y la rama (`main`).  
5. Amplify detecta automáticamente:
   - framework: React  
   - comando de build: `npm run build`  
   - comando de install: `npm install`  

## 5.2 Configurar redirects para SPA

Agregar:

Source: </^((?!.).)*$/>
Target: /index.html
Type: 200 (Rewrite)


## 5.3 Deploy automático

Cada vez que se haga **push a main**, Amplify:

1. Construye el front  
2. Genera build optimizado  
3. Despliega en el hosting CDN  

## 5.4 Resultado esperado

- Sitio accesible vía HTTPS  
- Actualización instantánea después de cada deploy  
- Logs de build accesibles desde la consola de Amplify  

---

# 6. Despliegue del Backend (Lambda + API Gateway)

El backend se despliega mediante funciones **AWS Lambda**, expuestas a través de **API Gateway**.

## 6.1 Estructura mínima de cada Lambda

handler.js
package.json
node_modules/


## 6.2 Pasos para crear cada Lambda

1. Abrir Lambda → Create Function  
2. Elegir:
   - Author from scratch  
   - Runtime: Node.js 18+  
   - Role: LambdaExecutionRole  

3. Subir el ZIP del código o conectar AWS SAM/Serverless Framework (opcional).  

## 6.3 Vincular Lambdas con API Gateway

1. Crear API REST  
2. Crear endpoints:
   - /productos  
   - /productos/{id}  
   - /productos/{id}/variantes  
   - /pedidos  
   - /admin/*  
   - /pagos/webhook (post-MVP)

3. Para cada endpoint:
   - Configurar método GET/POST  
   - Integrar con su Lambda  
   - Habilitar CORS para dominio Amplify  

## 6.4 Deploy de API Gateway

1. Actions → Deploy API  
2. Crear stage:
   - `dev`  
   - `prod`  

3. Obtener URL final para usar en frontend.

---

# 7. Configuración de DynamoDB

## 7.1 Crear tablas necesarias

- Productos  
- VariantesProducto  
- Categorias  
- LineasProducto  
- Recipientes  
- Fragancias  
- Pedidos  
- ItemsPedido  
- Clientes  

## 7.2 Crear índices (GSI)

- GSI1: productos por categoría  
- GSI2: productos por línea  
- GSI3: variantes por idProducto  
- GSI4: pedidos por cliente  

## 7.3 Proteger datos

- Lectura/escritura solo desde Lambda Execution Role  
- No exponer DynamoDB directamente a internet  

---

# 8. Integración del webhook de pago (Post-MVP)

Cuando se active:

1. Crear endpoint `/pagos/webhook` en API Gateway.  
2. Configurar Lambda `procesarPago`.  
3. Validar firma con la pasarela.  
4. Actualizar estado del pedido en DynamoDB.  
5. Ajustar stock de variantes.  

---

# 9. Validaciones previas al despliegue final

### 9.1 Frontend

- Build sin warnings severos  
- Navegación SPA OK  
- Carrito funcionando local y en deploy  
- Selector de fragancias funcionando  
- SPA funcionando en rutas directas (gracias a redirect rule)

### 9.2 Backend

- Test de endpoints desde Postman:
  - /productos  
  - /productos/{id}  
  - /variantes  
  - /pedidos  

### 9.3 Base de datos

- Tablas creadas  
- Datos cargados (productos, líneas, fragancias)  
- Variantes listas para test  

---

# 10. Procedimiento ante fallas

### 10.1 Fallas de frontend

- Revisar logs de Amplify (Build details)  
- Verificar errores en `npm run build`  
- Validar que la rama `main` no tenga conflictos  

### 10.2 Fallas de backend

- Revisar CloudWatch Logs para cada Lambda  
- Re-deploy manual desde AWS si es necesario  
- Verificar permisos IAM (errores típicos: `AccessDenied`)  

### 10.3 Fallas en API Gateway

- Verificar que la API esté deployada  
- Revisar CORS  
- Revisar integración con Lambda  

### 10.4 Fallas de DynamoDB

- Validar claves primarias correctas  
- Revisar consumo de RCU/WCU  
- Revisar permisos de Lambda en IAM  

---

# 11. Conclusión

El plan de despliegue descrito permite llevar el sistema AUMA desde desarrollo local hasta un entorno productivo en AWS de forma:

- segura,  
- reproducible,  
- automatizada,  
- escalable,  
- económica.

Este documento servirá como guía operativa para futuros despliegues, mantenimientos y ampliaciones del sistema.

---
