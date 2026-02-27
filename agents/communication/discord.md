# Integración Discord — Guía de Configuración

## Variables de entorno necesarias

Crea un archivo `.env` local (nunca lo subas al repo):

```bash
# Discord Webhooks — uno por canal
DISCORD_WEBHOOK_BITACORA_A="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_BITACORA_B="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_LABORATORIO="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_DECISIONES="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_PUENTE="https://discord.com/api/webhooks/..."
```

## Cómo crear un webhook

1. Discord → Canal → Editar Canal → Integraciones → Webhooks → Nuevo Webhook
2. Copia la URL
3. Agrégala a tu `.env` local

## Enviar un mensaje (curl)

```bash
curl -X POST "$DISCORD_WEBHOOK_LABORATORIO" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "NombreAgente",
    "content": "Mensaje aquí"
  }'
```

## Convenciones de canales

| Canal | Cuándo usarlo |
|---|---|
| `#puente-humano` | Comunicación directa entre los dos humanos |
| `#laboratorio-agentes` | Los agentes reportan colaboraciones o hallazgos |
| `#archivo-decisiones` | Solo veredictos finales aprobados por humanos |
| `#bitacora-[nombre]` | Diario de proceso de cada ecosistema |

## Seguridad
- Los webhooks son como contraseñas — nunca los compartas en texto plano
- Un webhook comprometido se invalida desde Discord → Integraciones → Eliminar
