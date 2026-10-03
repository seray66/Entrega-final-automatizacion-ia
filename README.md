# Ecosistema de Automatización IA Autónomo para Negocios

Proyecto Final — Curso de Automatización IA (CoderHouse)
Autor: Sergio Ayala

## Qué hace

Un cliente potencial escribe un email pidiendo presupuesto o propuesta para automatizar algo en su negocio. El sistema:

1. Detecta el email entrante (Gmail Trigger).
2. Extrae los datos clave del pedido con **Claude Haiku** (nombre, email, necesidad).
3. Consulta el catálogo de servicios en Notion (RAG) y redacta una propuesta comercial personalizada con **Claude Sonnet**.
4. Crea el registro del pedido en Notion, a la espera de aprobación humana (**HITL**).
5. Una vez aprobado manualmente en Notion, envía la propuesta por Gmail al cliente y marca el pedido como enviado.
6. Cualquier falla en los pasos críticos (extracción, redacción, envío) queda registrada en una base de Registro de Errores, sin romper el flujo general.

## Arquitectura

n8n orquesta todo el flujo. Notion es la capa de datos (Pedidos, Catálogo de Servicios, Registro de Errores). Claude Haiku y Sonnet se usan según la complejidad de cada tarea (ver matriz de costos). Gmail es el canal de entrada y salida.

Diagrama completo, estructuras de datos, costos y seguridad están documentados en los PDFs de este repo.

## Entregables (según rúbrica, 20% cada uno)

| # | Entregable | Archivo |
|---|---|---|
| 1 | Diagrama de arquitectura | `Diagrama_Arquitectura.pdf` |
| 2 | Estructuras de datos | `Estructuras_de_Datos.pdf` |
| 3 | Matriz de costos (Haiku vs Sonnet) | `Matriz_Costos.pdf` |
| 4 | Seguridad y resiliencia | `Seguridad_y_Resiliencia.pdf` |
| 5 | Dashboard de control (Notion, público, solo lectura) | [Ver Dashboard](https://leeward-bill-020.notion.site/Dashboard-de-Control-Ecosistema-IA-3ecfb330450080739230d2f19d584926?source=copy_link) |

## Archivos de este repo

- `Diagrama_Arquitectura.pdf`, `Estructuras_de_Datos.pdf`, `Matriz_Costos.pdf`, `Seguridad_y_Resiliencia.pdf` — los 4 documentos de la entrega.
- `workflow/Entrega_Final_Propuestas_Comerciales.json` — export del workflow de n8n (sin credenciales; n8n no exporta esos valores).
- `screenshots/` — evidencia de ejecución: canvas completo, ejecución exitosa, camino infeliz (error controlado), HITL en pausa y dashboard.

## Stack

- **n8n** — orquestación del workflow
- **Notion** — base de datos (Pedidos, Catálogo de Servicios, Registro de Errores) y Dashboard de Control
- **Claude Haiku 4.5** — extracción estructurada de datos del email (tarea simple, bajo costo)
- **Claude Sonnet 4.5** — redacción de la propuesta comercial con selección de servicio vía RAG (tarea compleja)
- **Gmail** — canal de entrada y salida

## Pruebas realizadas

Se documentaron 5+ ejecuciones de prueba, incluyendo al menos 2 caminos infelices deliberados (credencial de Claude rota, campo de destino de Gmail roto) para verificar que el sistema registra el error sin romper el flujo. Detalle completo en `Seguridad_y_Resiliencia.pdf`.
