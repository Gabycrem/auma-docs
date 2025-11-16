# 17 – Plan de Mantenimiento, SLA y Monitoreo  
Versión 1.0

---

# 1. Introducción

Este documento detalla el **plan de mantenimiento**, los **acuerdos de nivel de servicio (SLA)** y las **estrategias de monitoreo** implementadas para el sistema AUMA.

El objetivo es asegurar que la plataforma:

- funcione correctamente en todo momento,  
- sea estable y escalable,  
- minimice interrupciones,  
- cuente con detección temprana de fallas,  
- mantenga integridad y seguridad en los datos.  

---

# 2. Objetivos del mantenimiento

- Mantener la disponibilidad del sistema.  
- Realizar correcciones y ajustes mínimos post-producción.  
- Asegurar la continuidad del negocio.  
- Mantener la infraestructura AWS al día.  
- Prevenir incidentes futuros.  

---

# 3. Tipos de mantenimiento

## 3.1 Mantenimiento Correctivo
Acciones realizadas para corregir errores detectados en producción:

- Fallas en lambdas  
- Errores en endpoints  
- Respuestas HTTP incorrectas  
- Paginas del frontend que no cargan  
- Problemas de stock o actualización en DynamoDB  

Se aplica **inmediatamente** después de detectar una falla.

---

## 3.2 Mantenimiento Preventivo
Acciones periódicas para evitar incidentes:

- Revisión de logs en CloudWatch  
- Limpieza de recursos innecesarios  
- Actualización de dependencias del frontend/backend  
- Validación de roles IAM  
- Revisión del consumo de DynamoDB (RCU/WCU)  
- Chequeo de reglas de CORS y seguridad  

Frecuencia sugerida: **1 vez por mes**

---

## 3.3 Mantenimiento Evolutivo
Modificaciones para mejorar o actualizar el sistema:

- Nuevas variantes de producto  
- Mejoras en panel admin  
- Cambios en UI/UX  
- Nuevos endpoints  
- Optimizaciones de performance  

Este tipo de mantenimiento se planifica según el roadmap del proyecto.

---

# 4. SLA – Acuerdos de Nivel de Servicio

Los SLA establecen los niveles mínimos de calidad esperados para la plataforma.

## 4.1 Disponibilidad del sistema

| Componente | SLA Esperado |
|-----------|---------------|
| Amplify Hosting | 99.9% |
| API Gateway | 99.95% |
| AWS Lambda | 99.95% |
| DynamoDB | 99.999% (multi-AZ) |

La infraestructura serverless garantiza disponibilidad sin intervención manual.

---

## 4.2 Tiempos de respuesta

| Acción | Tiempo promedio |
|--------|-----------------|
| Llamada a API Gateway | 50–200 ms |
| Ejecución Lambda | 20–150 ms |
| Query DynamoDB | 1–10 ms |

---

## 4.3 Tiempos de resolución de incidentes

| Severidad | Descripción | Tiempo estimado |
|----------|-------------|-----------------|
| Alta | Falla que impide compras o rompe API | < 4 horas |
| Media | Error en funciones no críticas | < 24 horas |
| Baja | Ajustes estéticos, texto, UX | < 72 horas |

---

# 5. Monitoreo del sistema

La plataforma utiliza principalmente **AWS CloudWatch** para supervisión en tiempo real.

## 5.1 Monitoreo de AWS Lambda

- Invocaciones por minuto  
- Duración promedio  
- Errores por función  
- Timeouts  
- Logs de ejecución  

Alarmas sugeridas:

- Error rate > 5%  
- Duration > 2 seconds  
- Timeouts recurrentes  

---

## 5.2 Monitoreo API Gateway

- Errores 4xx  
- Errores 5xx  
- Latencia  
- Throughput  

Alarmas sugeridas:

- Latencia > 800ms  
- Errores 5xx > 10 por minuto  

---

## 5.3 Monitoreo DynamoDB

- Consumo de lectura (RCU)  
- Consumo de escritura (WCU)  
- Uso de índices  
- Errores de throttling  

Alarmas sugeridas:

- ThrottlingDetected >= 1  
- Consumo > 80% del provisionado  

---

## 5.4 Monitoreo del Frontend (Amplify)

- Logs de build  
- Fallas de despliegue  
- Errores de cache  
- Disponibilidad del CDN  

---

# 6. Plan de respaldo (Backup)

DynamoDB ofrece backups automáticos:

## 6.1 Backups Continuos (PITR)
- Permiten recuperar la base a cualquier punto de los últimos 35 días.  
- Recomendado para producción.  
- Sin afectar performance.  

## 6.2 Backups Manuales
- Para hitos importantes (antes de cambios grandes).  
- Guardados sin vencimiento.  

---

# 7. Plan de recuperación ante desastres (DR – Disaster Recovery)

## 7.1 Escenarios contemplados

- Caída de API Gateway  
- Fallas masivas en una Lambda  
- Error humano en base de datos  
- Caída regional en AWS (muy improbable)  

## 7.2 Estrategias

- DynamoDB multi-AZ con replicación automática  
- Amplify Hosting con CDN global  
- Lambdas desplegadas en múltiples AZ  
- Rollback inmediato de versiones en Amplify  
- Restauración de DynamoDB mediante PITR  

Tiempo estimado de recuperación: **< 20 minutos**

---

# 8. Registro y gestión de incidentes

Incidencias documentadas en **GitHub Issues**:

Cada issue debe incluir:

- Fecha  
- Descripción del problema  
- Componente afectado  
- Severidad  
- Logs adjuntos (CloudWatch)  
- Pasos para reproducir  
- Solución aplicada  
- Estado (Nuevo / En análisis / Resuelto / Cerrado)

---

# 9. Tareas periódicas sugeridas

## Mensuales
- Limpiar funciones Lambda obsoletas  
- Revisar costos en Cost Explorer  
- Actualizar dependencias NPM  
- Revisar IAM Roles  
- Validar alertas de CloudWatch  
- Test manual del checkout local  

## Trimestrales
- Revisar roadmap y plan de releases  
- Evaluar optimizaciones de catálogo  
- Actualizar documentación técnica  

---

# 10. Conclusión

El plan de mantenimiento, SLA y monitoreo asegura que la plataforma AUMA permanezca:

- estable  
- escalable  
- segura  
- mantenible  
- lista para crecer  

Este documento será actualizado en función de la evolución del proyecto y nuevas necesidades operativas.

---
