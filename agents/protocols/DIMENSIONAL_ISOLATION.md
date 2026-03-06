# Aislamiento Dimensional — Separar lo Personal de lo Laboral

## El Problema

Cuando construyes un ecosistema de agentes, es tentador tener un solo agente que maneje todo. Pero mezclar datos personales y laborales en un mismo agente crea problemas reales:

- Un agente con acceso a tu salud no debería ver contratos de tu empresa
- Un agente que revisa facturas corporativas no debería conocer tus finanzas personales
- Un contexto demasiado amplio genera respuestas menos precisas y riesgos de privacidad

## La Solución: Dos Dimensiones

Divide tu ecosistema en dos dimensiones aisladas:

```
DIMENSIÓN PERSONAL                    DIMENSIÓN LABORAL
──────────────────                    ─────────────────
Datos sobre ti como persona           Datos sobre tu empresa/trabajo
Salud, finanzas personales            Proyectos, clientes, contratos corp.
Contratos que firmas tú               Obligaciones de la empresa
Bienestar, rutinas                    Operaciones, estrategia

Agentes de esta dimensión:            Agentes de esta dimensión:
- Bienestar personal                  - Estrategia/orquestador
- Legal personal (contratos tuyos)    - Legal corporativo
- Finanzas personales                 - Finanzas empresa
                                      - Seguridad/QA
                                      - Operaciones/Proyectos
```

## Reglas de Aislamiento

1. **Agentes separados para cada dimensión** — no un agente "universal"
2. **Sin memoria compartida** — cada agente de cada dimensión tiene sus propios archivos
3. **El orquestador conoce ambas, pero no cruza datos** sin instrucción explícita del humano
4. **La dimensión personal es más confidencial** — sus datos no salen al bus externo

## Patrón de Simetría

Cuando un rol existe en ambas dimensiones, crea dos agentes paralelos:

| Rol | Dimensión Personal | Dimensión Laboral |
|---|---|---|
| Legal | `Agente-Legal-Personal` | `Agente-Legal-Corp` |
| Finanzas | `Agente-Finanzas-Personal` | `Agente-Finanzas-Corp` |
| Salud/Bienestar | `Agente-Bienestar` | *(no aplica)* |

Cada par:
- Tiene IDs distintos en el protocolo HERMES
- No comparte memoria ni contexto entre sí
- Reporta a namespaces distintos

## En la Práctica

Cuando alguien te pide "¿puedes revisar este contrato?", la pregunta que el orquestador debe resolver es:

> *¿Es un contrato que firma la empresa, o es un contrato que firma la persona?*

Si es la empresa → Agente-Legal-Corp
Si es la persona → Agente-Legal-Personal
Si hay duda → preguntar antes de routear

## Cuándo NO hace falta esta separación

Si eres freelance sin empresa propia, o si tu ecosistema es pequeño y la privacidad no es una preocupación crítica, puedes empezar con agentes únicos. La separación dimensional es más útil cuando:

- Tienes información corporativa sensible (clientes, contratos NDA)
- Quieres que tus agentes laborales puedan compartirse/auditarse sin exponer tu vida personal
- Usas el ecosistema con colaboradores (otro clan que no debe ver tu info personal)

---

*Principio raíz: Security by Design — la privacidad se diseña desde el inicio, no se añade después.*
