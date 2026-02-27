# Integración Telegram — Guía de Configuración

## Variables de entorno necesarias

```bash
# Telegram — en tu .env local (nunca al repo)
TELEGRAM_BOT_TOKEN_A="bot_token_aqui"
TELEGRAM_GROUP_ID="-100xxxxxxxxxx"   # El ID del grupo compartido (empieza con -)
```

## Cómo obtener el Chat ID del grupo

1. Agrega el bot al grupo
2. Ejecuta:
```bash
curl "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN_A/getUpdates"
```
3. Busca en la respuesta el campo `"chat": {"id": -XXXXXXXXXX}` del grupo

## Enviar un mensaje (curl)

```bash
curl -X POST "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN_A/sendMessage" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_id": "'"$TELEGRAM_GROUP_ID"'",
    "text": "Mensaje aquí",
    "parse_mode": "Markdown"
  }'
```

## Convenciones

- **Telegram grupal:** Avisos cortos, alertas urgentes, resúmenes de máximo 3 puntos
- **No usar Telegram** para reportes largos → usar Discord `#bitacora`
- Los bots no deben publicar en el grupo durante momentos de descanso (Ley Cero)

## Seguridad
- El token del bot es como una contraseña — vive solo en `.env` o variables de entorno del sistema
- Si el token se compromete: BotFather → /revoke
