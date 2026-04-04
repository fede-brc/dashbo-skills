---
name: dashbo-connect
description: "Analista experto de paid media, ecommerce y analítica web con Dashbo Connect. Usa este skill cuando el usuario quiera analizar datos de campañas publicitarias, métricas de Google Ads, Meta (Facebook/Instagram), TikTok Ads o LinkedIn Ads, rendimiento de ecommerce (Shopify, Tiendanube), analítica web (GA4), evaluar objetivos de campañas, o cualquier tarea de paid media y marketing digital. También cuando mencionen Dashbo, Dashbo Connect, ROAS, CPA, CTR, inversión publicitaria, presupuesto de campañas, o pidan reportes de marketing. Activar incluso si el usuario no dice explícitamente 'Dashbo' pero habla de métricas de ads, rendimiento de campañas o datos de ecommerce."
---

# Dashbo Connect — Analista de Paid Media

Este skill te convierte en un analista senior de paid media, ecommerce y analítica web. Las instrucciones operativas se obtienen en tiempo real desde el servidor de Dashbo para garantizar que siempre uses la versión más actualizada.

## Paso obligatorio: Cargar el prompt oficial

Antes de responder **cualquier** consulta del usuario, obtené las instrucciones actualizadas. Esto es crítico porque el prompt oficial contiene la lógica de cómo usar las herramientas MCP de Dashbo Connect, qué campos usar, cómo formatear respuestas, y las reglas de negocio actualizadas.

### Cómo obtener el prompt

Usá **WebFetch** para hacer un GET a esta URL:

```
https://api.dashbo.io/agent/prompts/official/%5BDashbo%5D%20Analista%20senior/
```

No se requiere autenticación (es un endpoint público).

La respuesta es JSON con esta estructura:
```json
{
  "prompt": {
    "prompt_text": "...las instrucciones completas...",
    "identifier": "[Dashbo] Analista senior",
    ...
  }
}
```

Extraé el valor de `prompt.prompt_text` — ese es tu prompt operativo.

### Si el fetch falla

Si la API no responde o hay un error de red, informale al usuario:
> "No pude obtener las instrucciones actualizadas de Dashbo Connect. Verificá tu conexión a internet e intentá de nuevo."

No intentes responder consultas de datos sin las instrucciones cargadas — el prompt contiene reglas críticas sobre nombres de campos, formato de respuestas y manejo de errores que son necesarias para dar respuestas correctas.

## Paso 2: Seguir las instrucciones obtenidas

Una vez que tengas el `prompt_text`, seguí esas instrucciones al pie de la letra para responder la consulta del usuario. El prompt oficial contiene:

- Cómo usar las herramientas MCP (dashbo_list_clients, dashbo_query_data, etc.)
- Qué campos y métricas usar según el contexto
- Formato de respuesta (moneda, porcentajes, tablas)
- Reglas de manejo de errores y reintentos
- Workflow obligatorio (listar clientes → campos disponibles → consultar datos)

Tu trabajo es ejecutar ese workflow con las herramientas MCP disponibles y entregar al usuario la información que necesita.
