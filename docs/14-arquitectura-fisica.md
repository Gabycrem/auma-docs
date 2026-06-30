---
title: Arquitectura Física e Infraestructura AWS
document: arquitectura-fisica
category: architecture
domain: infrastructure
version: "2.0"
status: vigente

owner: AUMA Studio
author: Nazarena Macre

repository: auma-docs
project: auma

created: 2026-06-28
last_updated: 2026-06-29

language: es-AR

audience:

- developers
- management
- ai-agent

tags:

- arquitectura-fisica
- infraestructura
- aws
- serverless
- cloud

related_documents:

- 10-arquitectura.md
- 15-plan-despliegue.md
- 17-mantenimiento-sla-monitoreo.md
- 19-manual-tecnico.md

references: []

description: >
    Documenta la arquitectura física, infraestructura cloud y servicios AWS
    previstos para implementar el sistema e-commerce AUMA.
---

```md
# Arquitectura Física e Infraestructura AWS

Versión 2.0

---

# 1. Introducción

## 1.1 Propósito

Este documento describe la arquitectura física e infraestructura prevista para la implementación del sistema **AUMA**, detallando los servicios cloud, componentes de infraestructura, distribución de recursos y estrategias de despliegue adoptadas para el proyecto.

Su propósito es documentar la organización física del sistema, facilitando su implementación, mantenimiento y evolución.

## 1.2 Alcance

Este documento abarca:

- la infraestructura cloud utilizada por el proyecto;
- los servicios de infraestructura y su función;
- la distribución de componentes físicos;
- la estrategia de seguridad de la infraestructura;
- la disponibilidad y escalabilidad de la plataforma;
- la distribución geográfica de los recursos;
- el flujo físico de una solicitud a través de la infraestructura.

La arquitectura lógica del sistema se documenta en:

[`10-arquitectura.md`](10-arquitectura.md)

La implementación técnica del sistema se documenta en:

[`19-manual-tecnico.md`](19-manual-tecnico.md)

> **Nota**
>
> Esta documentación refleja la infraestructura prevista para el proyecto durante su etapa de diseño.
>
> A medida que el sistema evolucione hacia su implementación, este documento deberá actualizarse para reflejar la infraestructura efectivamente utilizada.

---

# 2. Objetivos de la Arquitectura Física
La infraestructura de AUMA fue diseñada con los siguientes objetivos:

- desplegar un sistema completo sin administrar servidores propios;
- minimizar los costos operativos mediante una arquitectura serverless;
- garantizar alta disponibilidad y escalabilidad automática;
- desacoplar los distintos componentes del sistema;
- facilitar el despliegue continuo a partir del repositorio del proyecto;
- permitir la evolución incremental de la infraestructura acompañando el roadmap del sistema.

---

# 3. Infraestructura General

## 3.1 Descripción

La infraestructura física de AUMA se implementa sobre una arquitectura **cloud serverless** basada en servicios administrados de AWS.

La solución fue diseñada para minimizar la complejidad operativa, reducir costos de mantenimiento y aprovechar las capacidades de escalabilidad automática proporcionadas por la plataforma.

Cada componente de la infraestructura cumple una función específica dentro del sistema y se integra con el resto mediante servicios administrados.

## 3.2 Diagrama de infraestructura

```mermaid
flowchart TD

    Usuario[Usuario / Web]

    Amplify[AWS Amplify Hosting]

    APIGateway[AWS API Gateway]

    Lambda[AWS Lambda]

    DynamoDB[Amazon DynamoDB]

    CloudWatch[AWS CloudWatch]

    Pago[Pasarela de Pago]

    Usuario --> Amplify
    Amplify --> APIGateway
    APIGateway --> Lambda
    Lambda --> DynamoDB
    Lambda --> CloudWatch

    Pago --> APIGateway
````

## 3.3 Características

La infraestructura presenta las siguientes características:

* Arquitectura completamente basada en servicios administrados.
* Infraestructura serverless sin administración de servidores.
* Escalabilidad automática según la demanda.
* Alta disponibilidad proporcionada por la plataforma cloud.
* Componentes desacoplados mediante servicios independientes.
* Integración nativa entre los servicios utilizados.
* Preparada para incorporar nuevos componentes sin afectar la infraestructura existente.

---

# 4. Componentes de Infraestructura

## 4.1 Frontend

### AWS Amplify Hosting

El frontend del sistema se aloja mediante **AWS Amplify Hosting**, servicio encargado de publicar la aplicación React y gestionar su despliegue.

Responsabilidades principales:

- alojamiento de la aplicación SPA;
- despliegue automático desde GitHub;
- distribución mediante CDN;
- gestión automática de certificados HTTPS;
- redirecciones para aplicaciones SPA.

**Motivos de selección**

- integración nativa con GitHub;
- despliegue continuo simplificado;
- infraestructura totalmente administrada;
- bajo costo operativo.

---

## 4.2 Backend

### AWS API Gateway

La API REST del sistema se expone mediante **AWS API Gateway**, actuando como punto de entrada para todas las solicitudes provenientes del frontend.

Principales responsabilidades:

- recepción de solicitudes HTTP;
- enrutamiento hacia funciones AWS Lambda;
- configuración de CORS;
- limitación de solicitudes (Rate Limiting);
- registro de accesos.

### AWS Lambda

La lógica de negocio del sistema se implementa mediante funciones **AWS Lambda**, organizadas por dominio funcional.

Funciones previstas:

- gestión de productos;
- gestión de variantes;
- administración de pedidos;
- administración del catálogo;
- procesamiento de webhooks.

**Ventajas**

- ejecución bajo demanda;
- escalabilidad automática;
- pago por consumo;
- ausencia de administración de servidores.

---

## 4.3 Persistencia

### Amazon DynamoDB

La persistencia del sistema se implementa mediante **Amazon DynamoDB**, base de datos NoSQL administrada.

La infraestructura contempla las siguientes entidades principales:

- Productos;
- VariantesProducto;
- Categorias;
- LineasProducto;
- Recipientes;
- Fragancias;
- Clientes;
- Pedidos;
- ItemsPedido.

La estrategia de modelado y persistencia se documenta en:

[`09-modelado-sistema.md`](09-modelado-sistema.md)

---

## 4.4 Servicios complementarios

La infraestructura incorpora servicios adicionales que complementan el funcionamiento del sistema.

### AWS IAM

Responsable de la gestión de permisos y políticas de acceso entre los distintos servicios.

Se aplica el principio de **mínimo privilegio**, garantizando que cada componente disponga únicamente de los permisos estrictamente necesarios.

### AWS CloudWatch

Servicio destinado al monitoreo de la infraestructura.

Permite:

- registro de logs;
- recopilación de métricas;
- supervisión del rendimiento;
- generación de alertas.

### Pasarela de Pago

Durante el MVP el proceso de pago será simulado.

En etapas posteriores se prevé la integración con una pasarela de pagos externa mediante Webhooks para automatizar la confirmación de pagos y la actualización del estado de los pedidos.

---

# 5. Seguridad de Infraestructura

## 5.1 Gestión de identidades

La infraestructura utiliza **AWS IAM** para administrar los permisos de acceso entre los distintos servicios que componen el sistema.

Los principales roles previstos son:

| Rol | Responsabilidad |
|------|-----------------|
| LambdaExecutionRole | Acceso a DynamoDB y CloudWatch. |
| AmplifyServiceRole | Despliegue automático del frontend desde GitHub. |
| APIGatewayInvokeRole | Ejecución de funciones AWS Lambda. |

La configuración de permisos sigue el **principio de mínimo privilegio**, garantizando que cada servicio únicamente pueda acceder a los recursos estrictamente necesarios para cumplir su función.

---

## 5.2 Seguridad de red

La infraestructura contempla las siguientes medidas de seguridad:

- comunicación cifrada mediante HTTPS;
- configuración de CORS para restringir el acceso a la API;
- limitación de solicitudes (Rate Limiting);
- validación de solicitudes recibidas por la API;
- protección de los Webhooks mediante validación de origen y firma cuando corresponda.

---

## 5.3 Gestión de secretos

Las credenciales, claves de acceso y demás información sensible deberán administrarse mediante los mecanismos seguros proporcionados por AWS.

Las credenciales no deberán almacenarse en el código fuente ni en el repositorio del proyecto.

---

# 6. Disponibilidad y Escalabilidad

La infraestructura física de AUMA fue diseñada para aprovechar las capacidades de escalabilidad y alta disponibilidad proporcionadas por los servicios administrados de AWS.

Las principales características son:

- escalabilidad automática de los servicios serverless;
- alta disponibilidad mediante infraestructura administrada;
- tolerancia a fallos proporcionada por la plataforma cloud;
- ausencia de administración manual de servidores;
- crecimiento de la infraestructura según la demanda del sistema.

La estrategia adoptada permite acompañar el crecimiento del proyecto sin requerir modificaciones significativas en la arquitectura física.

---

# 7. Monitoreo y Observabilidad

La infraestructura incorpora mecanismos de monitoreo que permiten supervisar el comportamiento del sistema y detectar posibles incidentes.

Las capacidades previstas incluyen:

- registro centralizado de logs;
- recopilación de métricas de infraestructura;
- monitoreo del rendimiento de los servicios;
- generación de alertas ante fallos;
- auditoría de eventos relevantes.

El servicio principal utilizado para estas tareas es **AWS CloudWatch**, complementado por las herramientas de monitoreo propias de los servicios administrados cuando corresponda.

---

# 8. Distribución Geográfica

La infraestructura se implementará inicialmente en la región:

- **us-east-1 (Norte de Virginia)**

La selección de esta región responde a criterios de disponibilidad, costos y compatibilidad con los servicios utilizados por el proyecto.

Los servicios administrados empleados distribuyen automáticamente los recursos entre múltiples Zonas de Disponibilidad (Availability Zones), proporcionando redundancia y alta disponibilidad sin requerir configuraciones adicionales.

Servicios con distribución multi-AZ:

- AWS Amplify Hosting;
- AWS API Gateway;
- AWS Lambda;
- Amazon DynamoDB.

---

# 9. Flujo de Infraestructura

El recorrido físico de una solicitud dentro de la infraestructura de AUMA se desarrolla de la siguiente manera:

1. El usuario accede a la aplicación web publicada mediante **AWS Amplify Hosting**.
2. El contenido estático es distribuido a través de la infraestructura CDN asociada al servicio.
3. El frontend realiza solicitudes HTTP hacia **AWS API Gateway**.
4. API Gateway enruta las solicitudes hacia las funciones **AWS Lambda** correspondientes.
5. Las funciones Lambda ejecutan la lógica de negocio y acceden a **Amazon DynamoDB** cuando es necesario consultar o persistir información.
6. Los eventos de ejecución, métricas y registros son enviados a **AWS CloudWatch** para su monitoreo.
7. En etapas posteriores al MVP, la pasarela de pago notificará el resultado de las transacciones mediante un Webhook que será procesado por la infraestructura del sistema.

---

# 10. Documentos Relacionados

La arquitectura física del sistema se complementa con los siguientes documentos del proyecto:

- [`10-arquitectura.md`](10-arquitectura.md)
- [`09-modelado-sistema.md`](09-modelado-sistema.md)
- [`15-plan-despliegue.md`](15-plan-despliegue.md)
- [`17-mantenimiento-sla-monitoreo.md`](17-mantenimiento-sla-monitoreo.md)
- [`19-manual-tecnico.md`](19-manual-tecnico.md)

---

# 11. Autoría

Este documento forma parte de la documentación oficial del proyecto **AUMA**, desarrollado por **Gabycrem Software** bajo la metodología **Gabycrem Engineering**.

## Organización

Gabycrem Software

## Proyecto

AUMA

## Autora

Nazarena Macre

## Portafolio profesional

GitHub: https://github.com/Gabycrem

LinkedIn: https://www.linkedin.com/in/macrenazarena/

---

<div align="center">

`Siempre construyendo, siempre aprendiendo. — GABYCREM®`

</div>

---

# 12. Historial de cambios

| Versión | Fecha | Cambio | Autor |
|----------|------------|--------------------------------------------------------------|----------------|
| 2.0 | 2026-06-29 | Adaptación del documento al estándar Gabycrem Engineering. | Nazarena Macre |
| 1.0 | 2025-11-28 | Creación del documento. | Nazarena Macre |