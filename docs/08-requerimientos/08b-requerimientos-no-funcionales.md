# 08b – Requerimientos No Funcionales (RNF)  
Versión 1.0

---

# 1. Introducción

Este documento lista los **Requerimientos No Funcionales (RNF)** del sistema AUMA.  
Los RNF describen las cualidades, restricciones y comportamientos esperados del sistema, más allá de sus funciones específicas.

---

# 2. Requerimientos No Funcionales

## 2.1. Usabilidad

### RNF-01  
La interfaz debe ser intuitiva, clara y visualmente coherente con la identidad de AUMA.

### RNF-02  
El catálogo, carrito y checkout deben ser completamente responsivos.

---

## 2.2. Rendimiento

### RNF-03  
Las vistas deben cargar en menos de 3 segundos bajo condiciones normales.

### RNF-04  
Las operaciones de API deben ejecutarse en menos de 500 ms.

---

## 2.3. Seguridad

### RNF-05  
Las contraseñas deben gestionarse exclusivamente mediante Amazon Cognito.

### RNF-06  
El panel admin debe requerir autenticación y autorización estricta.

### RNF-07  
Los datos sensibles deben almacenarse cifrados o no almacenarse.

---

## 2.4. Confiabilidad

### RNF-08  
La integridad de datos debe estar garantizada mediante DynamoDB y validaciones internas.

### RNF-09  
Las confirmaciones de pago solo deben considerarse válidas mediante webhook oficial.

---

## 2.5. Mantenibilidad

### RNF-10  
El sistema debe seguir buenas prácticas de código y estructura clara de carpetas.

### RNF-11  
El código debe estar modularizado para facilitar cambios futuros.

---

## 2.6. Portabilidad

### RNF-12  
El frontend debe ser compatible con los principales navegadores modernos.

### RNF-13  
La infraestructura debe poder migrarse entre regiones AWS si es necesario.

---

# 3. Conclusión

Este documento establece los estándares de calidad que deben cumplirse durante el desarrollo y despliegue del e-commerce AUMA.

