# HERMES — Protocolo de Comunicación entre Ecosistemas de Agentes

**Basado en:** [dereyesm/hermes](https://github.com/dereyesm/hermes)
**Versión de referencia:** HERMES v4.0

---

## Concepto

HERMES es un protocolo de mensajería asíncrona para que ecosistemas de agentes de distintas personas se comuniquen de forma estructurada, trazable y segura.

Cada persona tiene un **clan** (su ecosistema de agentes). HERMES define cómo los clanes hablan entre sí.

```
Clan A (tu ecosistema)          Clan B (otro ecosistema)
──────────────────────          ────────────────────────
[agente-1]                      [agente-X]
[agente-2]  ──► bus.jsonl ──►  [agente-Y]
[agente-3]                      [agente-Z]
```

---

## Estructura de un Paquete HERMES

```json
{
  "ts":   "2026-01-01T10:00:00Z",
  "src":  "mi_agente",
  "dst":  "agente_destino",
  "type": "request",
  "msg":  "Contenido del mensaje",
  "ttl":  86400,
  "ack":  [],
  "reply": "none"
}
```

| Campo | Descripción |
|---|---|
| `ts` | Timestamp ISO 8601 |
| `src` | ID del agente emisor |
| `dst` | ID del agente receptor (o `"*"` para broadcast) |
| `type` | Tipo de mensaje (ver tabla abajo) |
| `msg` | Contenido |
| `ttl` | Tiempo de vida en segundos |
| `ack` | Lista de agentes que han acusado recibo |
| `reply` | ID del mensaje al que responde (o `"none"`) |

---

## Tipos de Mensaje

| Type | Uso |
|---|---|
| `request` | Solicitar algo a otro agente |
| `response` | Responder a una solicitud |
| `event` | Notificar un evento (sin respuesta requerida) |
| `alert` | Alerta de alta prioridad |
| `dojo_input` | Proponer una skill nueva al agente de aprendizaje |
| `ecosystem_manifest` | Compartir la descripción del ecosistema con otro clan |
| `handshake` | Primer contacto entre dos clanes |

---

## Namespaces — Cómo Organizar tu Clan

Un namespace es un área funcional de tu ecosistema. Cada agente pertenece a uno.

**Namespaces sugeridos:**

| Namespace | Propósito típico |
|---|---|
| `estrategia` | Agente orquestador principal — interface con el humano |
| `legal` | Revisión de contratos y obligaciones |
| `seguridad` | QA, auditoría de código, gestión de riesgos |
| `operaciones` | Proyectos, finanzas, agenda |
| `bienestar` | Salud, descanso, rutinas personales |
| `gateway` | Única puerta de entrada/salida del clan |
| `controller` | Meta-auditoría — lee todo, no actúa directamente |

**Reglas de diseño:**
- Un agente pertenece a UN namespace
- El gateway es el único que habla con el exterior
- El controller audita en modo read-only

---

## Ciclo de Sesión (SYN/FIN)

Cada sesión de trabajo con un agente tiene dos momentos clave:

```
SYN (inicio):  Lee el estado del bus → entiende qué pasó mientras no estabas
               Lee collective_state.md → estado actual del clan

FIN (cierre):  Actualiza tu sección en collective_state.md
               Escribe un event al bus con lo que hiciste
```

Este ciclo evita que los agentes trabajen sobre información desactualizada.

---

## Regla ARC-1918 (Firewall por defecto)

> **Por defecto: DENEGAR todo.**
> Solo fluyen los mensajes de los canales explícitamente permitidos.

Ningún dato de tu clan sale a otro clan sin aprobación explícita del humano soberano.

---

## Relay Inter-Clan (Agora)

Para conectar dos clanes, ambas personas crean un relay que sincroniza los mensajes:

```
Clan A                    Relay (GitHub privado)          Clan B
──────                    ──────────────────────          ──────
bus.jsonl ──► a_outbox.jsonl                   b_outbox.jsonl ──► bus.jsonl
              b_outbox.jsonl ◄──────────────── a_outbox.jsonl
```

- El relay es un repo GitHub privado, ambas personas como collaborators
- Cada clan tiene su daemon que hace poll cada N segundos
- Solo el gateway puede leer/escribir mensajes inter-clan

---

## collective_state.md — Memoria Colectiva del Clan

Cada clan tiene un archivo `collective_state.md` donde cada agente escribe su estado en FIN de sesión (máx 5 líneas útiles).

```markdown
## namespace-estrategia — NombreAgente
**Última actualización:** 2026-01-01
**Estado:** ACTIVO — resumen de lo más relevante
**Pendiente:** qué sigue
```

Este archivo es el "estado del mundo" que cualquier agente lee al inicio de sesión.

---

*Para implementación de referencia, ver: https://github.com/dereyesm/hermes*
