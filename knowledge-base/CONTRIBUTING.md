# Guía de Contribución

Este documento establece las normas para crear y mantener la documentación oficial del proyecto AUMA.

Su objetivo es garantizar consistencia, trazabilidad y facilidad de mantenimiento en toda la Knowledge Base.

---

# Principios

## Una responsabilidad por documento

Cada documento debe responder una única pregunta.

Ejemplo:

* Manual de Marca → ¿Qué representa AUMA?
* Sistema Visual → ¿Cómo se ve AUMA?
* Colección Esencia → ¿Qué es este producto?
* Estrategia de Redes → ¿Cómo se comunica AUMA?

No mezclar responsabilidades.

---

## La documentación es la fuente de verdad

Toda la información oficial debe vivir en un único documento.

No duplicar contenido.

Cuando un documento necesite información existente en otro, deberá utilizar una referencia.

---

## Referencias

Las referencias se escriben utilizando enlaces Markdown relativos.

Ejemplo:

```md
[Manual de Marca](../01-marca/manual-de-marca.md)
```

Nunca utilizar rutas absolutas.

---

## Documentos relacionados

Los documentos relacionados complementan la lectura pero no son dependencias obligatorias.

---

## Front Matter

Todos los documentos deberán utilizar exactamente el mismo Front Matter.

Solo podrán modificarse los valores.

Nunca la estructura.

---

## Estructura

Todos los documentos deberán seguir esta estructura:

* Front Matter
* Título
* Objetivo
* Alcance
* Índice
* Contenido
* Referencias
* Documentos relacionados
* Historial

La estructura de los documentos es obligatoria. El contenido puede evolucionar; la estructura debe permanecer consistente para facilitar la navegación, el mantenimiento y el consumo por herramientas de inteligencia artificial.
---

## Escritura

* Utilizar español (es-AR).
* Mantener un lenguaje claro y objetivo.
* Evitar información duplicada.
* Evitar opiniones personales.
* Escribir pensando en que la documentación será utilizada tanto por personas como por herramientas de IA.

---

## Versionado

Todo cambio significativo deberá reflejarse en el Historial de cambios del documento correspondiente.
