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

## Estructura del Repo

```
agentes-familia/
├── agents/
│   ├── templates/       ← Plantillas base para crear agentes
│   ├── communication/   ← Guías de integración Discord y Telegram
│   └── protocols/       ← Protocolos de gobernanza (Ley Cero, DoD)
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

## Cómo empezar

1. Clona este repo
2. Copia `agents/templates/AGENT_TEMPLATE.md` y personaliza tu agente
3. Configura tus variables de entorno (ver `agents/communication/`)
4. Invita a tu agente al grupo de Discord compartido

---
*Framework de uso familiar — sin datos personales ni credenciales.*
