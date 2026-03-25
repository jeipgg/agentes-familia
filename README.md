# Agentes Familia — Sociedad de Agentes Digital

Un framework para construir una pequeña sociedad de agentes de IA entre personas cercanas, donde cada quien tiene su propio ecosistema de agentes que se comunican por Discord y Telegram.

## Concepto

Cada miembro de la familia tiene:
- Sus propios **agentes personales** (estrategia, bienestar, operaciones)
- Sus propios **canales de comunicación** (Telegram, Discord)
- Una **zona compartida** donde los agentes colaboran

```
Miembro A — Agentes ──→ #laboratorio-agentes (Discord) ←── Miembro B — Agentes
                                    ↓
                        Grupo Familiar (Telegram)
                                    ↓
                        #archivo-decisiones (Discord)
```

## Galería de Agentes

Roles probados en ecosistemas reales. Úsalos como punto de partida — renómbralos, combínalos, adáptalos a tu contexto.

| Rol | Archivo | Para qué sirve |
|---|---|---|
| **Orquestador** | `agents/roles/orquestador.md` | Coordina todos los demás agentes. Memoria maestra del ecosistema. |
| **Guardián de Seguridad** | `agents/roles/guardian-seguridad.md` | Audita integraciones, rota credenciales, responde incidentes. |
| **Auditor Financiero** | `agents/roles/auditor-financiero.md` | Verifica cálculos, analiza costos reales, detecta anomalías. |
| **Coordinador de Ops** | `agents/roles/coordinador-ops.md` | Crea tickets, hace seguimiento de compromisos, detecta bloqueos. |
| **Maestro de Aprendizaje** | `agents/roles/maestro-aprendizaje.md` | Documenta lecciones, detecta patrones de error, propone mejoras. |
| **Guardián del Bienestar** | `agents/roles/guardian-bienestar.md` | Aplica la Ley Cero. Detecta sobrecarga. Protege al humano. |
| **Gateway de Comunicación** | `agents/roles/gateway-comunicacion.md` | Centraliza mensajes a Telegram y Discord. Filtra PII. |
| **Arquitecto Técnico** | `agents/roles/arquitecto-tecnico.md` | Valida propuestas técnicas. Audita deuda. Revisa código. |
| **QA & Testing** | `agents/roles/qa-testing.md` | Diseña y ejecuta pruebas. Nada sale sin pasar por aquí. |
| **Asesor Legal** | `agents/roles/asesor-legal.md` | Revisa contratos, redacta borradores, alerta vencimientos. |
| **Arquitecto de Procesos** | `agents/roles/arquitecto-procesos.md` | Diagnostica fricciones, crea SOPs ejecutables, ciclo PDCA. Skills transversales: flowchart Mermaid, RACI, feedback. |

### ¿Cuál necesito primero?

Si estás empezando: **Orquestador + Guardián del Bienestar + uno según tu contexto** (financiero, operativo o técnico). Los tres juntos forman la triada mínima. Si tu ecosistema ya opera y quieres que los procesos escalen: suma el **Arquitecto de Procesos** — es el rol que convierte el conocimiento tácito en procedimientos que cualquiera puede ejecutar.

## Estructura del Repo

```
agentes-familia/
├── agents/
│   ├── roles/           ← Agentes listos para usar y adaptar
│   ├── templates/       ← Plantillas base para crear los tuyos
│   ├── communication/   ← Guías de integración Discord y Telegram
│   └── protocols/       ← Protocolos de gobernanza (Ley Cero, DoD, HERMES)
└── examples/            ← Ejemplos de cómo los agentes colaboran
```

## Canales Discord sugeridos

| Canal | Propósito |
|---|---|
| `#puente-humano` | Comunicación directa entre miembros |
| `#laboratorio-agentes` | Colaboración entre agentes de distintos ecosistemas |
| `#archivo-decisiones` | Veredictos finales aprobados por humanos |
| `#bitacora-[nombre]` | Diario de cada ecosistema (uno por miembro) |

## Principios

1. **Ley Cero:** El bienestar humano siempre es prioridad sobre la ejecución.
2. **Soberanía:** Cada miembro es dueño exclusivo de su ecosistema.
3. **Transparencia:** Las decisiones que afectan a ambos van a `#archivo-decisiones`.
4. **Seguridad:** Ningún token, credencial o dato personal viaja por los canales compartidos.
5. **Triada mínima:** Ninguna decisión importante se toma con menos de 3 perspectivas.

## Cómo empezar

1. Clona este repo
2. Lee `agents/roles/orquestador.md` — es el primero que necesitas
3. Elige los roles que aplican a tu contexto
4. Copia `agents/templates/AGENT_TEMPLATE.md` y adapta cada rol a tu realidad
5. Configura tus variables de entorno (ver `agents/communication/`)
6. Conecta a Discord y Telegram siguiendo `GUIA_ONBOARDING.md`

---
*Framework de uso libre — sin datos personales ni credenciales. Construido desde la práctica, compartido para la comunidad.*
