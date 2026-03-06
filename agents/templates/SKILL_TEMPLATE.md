---
doc_id:      [ECOSISTEMA-SKL-XXX]
title:       [Nombre_Skill] — Skill Spec
version:     1.0
status:      [EN_PRUEBA | Activa | Deprecated]
owner:       [Agente que usa esta skill]
layer:       [agent | shared]
created:     [YYYY-MM-DD]
---

# [Nombre_Skill] v1.0

## Descripción

[Una línea: qué hace esta skill y para qué sirve.]

## Trigger

Esta skill se activa cuando:
- [ ] El humano pide explícitamente: [palabras clave / ejemplos de solicitud]
- [ ] El agente detecta: [condición automática]
- [ ] Se recibe un paquete HERMES de tipo `[type]` con contenido relevante

## Inputs

| Input | Fuente | Obligatorio |
|---|---|---|
| [dato_1] | [de dónde viene] | Sí / No |
| [dato_2] | [de dónde viene] | Sí / No |

## Proceso

1. [Paso 1 — qué hace el agente]
2. [Paso 2 — cómo procesa la información]
3. [Paso 3 — cómo genera el output]

## Output

**Formato:** [Tabla / Narrative / JSON / Markdown / Telegram message]

**Ejemplo de output:**
```
[Pega aquí un ejemplo concreto de lo que entrega esta skill]
```

## Reglas de la Skill

- [Regla 1: qué NUNCA debe hacer esta skill]
- [Regla 2: límites de scope]
- [Regla 3: cómo escala si hay ambigüedad]

## Ley Cero aplicada

[Cómo esta skill respeta el bienestar del humano — ej: "No genera alertas en horario nocturno", "Siempre pregunta antes de ejecutar acciones irreversibles"]

## Integración con otras skills / agentes

| Colabora con | Cómo |
|---|---|
| [Otro agente / skill] | [Para qué interactúan] |

## Métricas de éxito

- [Cómo saber si esta skill funciona bien]
- [Indicador cuantificable si aplica]

## CHANGELOG

### v1.0 — [FECHA]
- Creación inicial de la skill
