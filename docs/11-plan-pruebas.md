# 11 – Plan de Pruebas  
Versión 1.0

---

# 1. Introducción

El presente documento define el **Plan de Pruebas** del sistema e-commerce AUMA.  
Su objetivo es asegurar que todas las funcionalidades del MVP y componentes asociados operen correctamente antes del despliegue en producción.

Incluye:

- Estrategia general de pruebas  
- Tipos de pruebas aplicadas  
- Casos de prueba por módulo  
- Criterios de aceptación  
- Criterios de entrada y salida  
- Gestión de incidencias  

---

# 2. Estrategia de Pruebas

La estrategia de prueba se basa en validar el funcionamiento del sistema **desde el frontend hacia la base de datos**, cubriendo los flujos críticos definidos en el modelado del sistema.

Se aplicarán los siguientes tipos de prueba:

### 2.1 Pruebas funcionales
Verifican que cada componente cumpla su función según los requerimientos.

Incluyen:

- Catálogo  
- Ficha de producto  
- Carrito  
- Checkout  
- Creación de pedidos  
- Confirmación mediante webhook  

### 2.2 Pruebas de integración
Validan que los componentes funcionen correctamente entre sí:

- Frontend → API Gateway  
- API Gateway → Lambda  
- Lambda → DynamoDB  
- Pasarela de pago → Webhook → Backend  

### 2.3 Pruebas de interfaz (UI/UX)
Comprueban que:

- la navegación sea fluida,  
- elementos estén correctamente visibles,  
- botones e inputs funcionen adecuadamente.

### 2.4 Pruebas de rendimiento (básicas)
Verificación de:

- tiempo de carga del catálogo,  
- latencia de llamadas API,  
- respuesta del backend bajo uso normal.  

### 2.5 Pruebas de seguridad (mínimas para MVP)
- Validación de payload  
- Revisar CORS  
- Asegurar que endpoints protegidos no estén accesibles  

---

# 3. Alcance de las pruebas

El plan cubre todas las funcionalidades core del MVP:

## Incluye:
- Visualización de catálogo  
- Filtros por categoría/línea  
- Ficha de producto + selección de fragancia  
- Carrito de compra  
- Checkout  
- Creación de pedidos  
- Confirmación de pago por webhook  
- Gestión de stock  
- ABM básico de productos (admin)  

## No incluye (fuera de alcance, post-MVP):
- Login/registro Cognito  
- Panel avanzado de reportes  
- Dashboard admin completo  
- Cupones de descuento  
- Programas de fidelización  
- Envíos internacionales  
- Multi-idioma  

---

# 4. Criterios de Entrada

Se podrá iniciar la fase de pruebas cuando:

1. El frontend renderiza catálogo, ficha y carrito sin errores.  
2. La API esté desplegada en API Gateway.  
3. Las funciones Lambda respondan correctamente a peticiones básicas.  
4. Las tablas DynamoDB estén creadas y accesibles.  
5. El webhook tenga endpoint configurado.  

---

# 5. Criterios de Salida

La fase de pruebas se considera aprobada cuando:

- El 100% de los casos de prueba críticos están aprobados.  
- No existan errores de severidad alta pendientes.  
- El checkout genera pedidos correctos.  
- El webhook actualiza correctamente el estado del pedido.  
- El catálogo se muestra sin inconsistencias.  

---

# 6. Casos de Prueba

A continuación se detallan los casos de prueba esenciales del MVP.

---

## 6.1 Catálogo

### CP-01: Visualizar catálogo
| Ítem | Detalle |
|------|---------|
| Objetivo | Verificar que el catálogo cargue correctamente. |
| Precondición | Productos y variantes cargados en BD. |
| Pasos | 1. Ingresar a /catalogo  2. Observar listado |
| Resultado esperado | Se muestran todas las cards de productos. |

### CP-02: Filtros
| Ítem | Detalle |
|------|---------|
| Objetivo | Validar filtros por categoría, línea o recipiente. |
| Resultado esperado | Solo aparecen productos pertenecientes al filtro. |

---

## 6.2 Ficha de Producto

### CP-03: Ver detalle de producto
| Ítem | Detalle |
|------|---------|
| Objetivo | Verificar que la ficha muestre todos los datos. |
| Resultado esperado | Nombre, línea, categoría, recipiente, fragancias, stock. |

### CP-04: Selección de fragancia
| Ítem | Detalle |
|------|---------|
| Objetivo | Validar que el selector muestre fragancias de la variante. |
| Resultado esperado | Fragancias sin stock aparecen deshabilitadas. |

---

## 6.3 Carrito

### CP-05: Agregar al carrito
| Ítem | Detalle |
|------|---------|
| Objetivo | Validar que un producto se agregue correctamente. |
| Resultado esperado | El carrito muestra nombre, fragancia, cantidad, subtotal. |

### CP-06: Modificar cantidades
| Resultado esperado | Total recalculado correctamente. |

### CP-07: Vaciar carrito
| Resultado esperado | El carrito queda en cero. |

---

## 6.4 Checkout

### CP-08: Crear pedido
| Ítem | Detalle |
|------|---------|
| Objetivo | Validar creación del pedido en DynamoDB. |
| Resultado esperado | Pedido con estado “pendiente de pago”. |

### CP-09: Redirección a pasarela de pago
| Resultado esperado | Se abre la pasarela correctamente. |

---

## 6.5 Webhook de Pago

### CP-10: Confirmar pago exitoso
| Ítem | Detalle |
|------|---------|
| Objetivo | Validar funcionamiento del webhook. |
| Resultado esperado | Estado del pedido pasa a “pagado” + stock actualizado. |

### CP-11: Pago rechazado
| Resultado esperado | Estado del pedido pasa a “rechazado”. |

---

## 6.6 Panel Administrador

### CP-12: Crear nuevo producto base
| Resultado esperado | Producto registrado y visible en catálogo. |

### CP-13: Crear variante  
| Resultado esperado | Variante disponible en selector de fragancias. |

---

# 7. Gestión de Incidencias

Las incidencias se registrarán en GitHub Issues con:

- Descripción  
- Pasos para reproducir  
- Resultado actual  
- Resultado esperado  
- Severidad (Alta / Media / Baja)  
- Estado (Nuevo / En análisis / Resuelto / Cerrado)  

---

# 8. Conclusión

El presente plan de pruebas garantiza que el sistema AUMA pueda ser verificado de forma sistemática antes del despliegue, asegurando que los flujos críticos funcionen correctamente y que la experiencia del usuario sea estable.

Con esto queda cubierto el alcance total del MVP a nivel de pruebas funcionales, integración, interfaz, rendimiento básico y validación del proceso de pago mediante webhook.

---
