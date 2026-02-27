# Guía de Onboarding — Ecosistema de Agentes
**Para el segundo miembro de la familia**
*Desde cero hasta conectado a Telegram y Discord*

---

## ANTES DE EMPEZAR

Necesitas tener instalado:
- **Python 3** o **Node.js** (para scripts opcionales)
- **curl** (ya viene en Mac/Linux)
- **git**
- Una cuenta de **GitHub**
- Una cuenta de **Telegram** (en tu teléfono)
- Acceso al servidor de **Discord** compartido

---

## PARTE 1 — TELEGRAM: Crear tu bot y conectarte al grupo

### Paso 1.1 — Crear tu bot con BotFather

1. Abre Telegram en tu teléfono o escritorio
2. Busca `@BotFather` (el oficial, tiene la palomita azul)
3. Escribe `/newbot`
4. BotFather te pregunta: **"¿Cómo se llamará tu bot?"**
   - Escribe el nombre visible, ej: `Dani Bot`
5. Luego pregunta: **"¿Cuál será el username?"**
   - Debe terminar en `bot`, ej: `dani_agentes_bot`
6. BotFather te responde con tu **TOKEN**. Se ve así:
   ```
   7123456789:AABBCCDDEEFFaabbccddeeff1234567890
   ```
   **Guárdalo. Es tu contraseña del bot.**

### Paso 1.2 — Agregar el bot al grupo familiar

1. Pídele a la otra persona que te agregue al grupo de Telegram
2. Una vez en el grupo, abre el grupo → toca el nombre → **Agregar miembros**
3. Busca tu bot por su username (ej: `@dani_agentes_bot`) y agrégalo
4. Envía cualquier mensaje en el grupo desde tu teléfono (activa el bot)

### Paso 1.3 — Obtener el Chat ID del grupo

Abre una terminal y ejecuta (reemplaza `TU_TOKEN`):

```bash
curl "https://api.telegram.org/botTU_TOKEN/getUpdates"
```

Busca en la respuesta este fragmento:
```json
"chat": {
  "id": -1234567890,
  "title": "Nombre del Grupo",
  "type": "group"
}
```

El número que empieza con `-` es tu **TELEGRAM_GROUP_ID**. Guárdalo.

### Paso 1.4 — Probar el envío al grupo

```bash
curl -X POST "https://api.telegram.org/botTU_TOKEN/sendMessage" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_id": "TU_GROUP_ID",
    "text": "🤖 Bot de Dani conectado al grupo",
    "parse_mode": "Markdown"
  }'
```

Si recibes el mensaje en el grupo, ¡está listo!

---

## PARTE 2 — DISCORD: Crear webhooks para tus canales

### Paso 2.1 — Unirte al servidor compartido

Pídele a la otra persona la invitación al servidor de Discord. Una vez dentro verás los canales compartidos:
- `#puente-humano`
- `#laboratorio-agentes`
- `#archivo-decisiones`

### Paso 2.2 — Crear tu canal privado de bitácora

1. En el servidor de Discord, haz clic en **+** junto a "Canales de texto"
2. Nómbralo: `bitacora-dani`
3. En permisos, define que solo tú y tus bots pueden publicar

### Paso 2.3 — Crear webhooks para tus canales

Necesitas un webhook propio para cada canal al que tus agentes van a publicar. Son 4 en total:

| Canal | Tipo | Para qué |
|---|---|---|
| `#bitacora-dani` | Privado (tuyo) | Logs internos de tus agentes |
| `#laboratorio-agentes` | Compartido | Colaboración entre ecosistemas |
| `#archivo-decisiones` | Compartido | Veredictos finales |
| `#puente-humano` | Compartido | Comunicación directa entre humanos |

**Nota:** Los canales compartidos ya existen en el servidor. Solo necesitas crear tu propio webhook en cada uno — esto no afecta los webhooks de la otra persona.

Para cada uno de los 4 canales:

1. Haz clic en el canal → **Editar Canal** (ícono de engranaje)
2. Ve a **Integraciones** → **Webhooks** → **Nuevo Webhook**
3. Ponle nombre `Bot Dani` y copia la URL completa

La URL se ve así:
```
https://discord.com/api/webhooks/1234567890/abcdef...xyz
```

**Guarda cada URL. Una por canal. Si no puedes crear el webhook en un canal compartido, pídele a la administradora del servidor que te dé permiso de "Gestionar Webhooks" en ese canal.**

### Paso 2.4 — Probar el webhook

```bash
curl -X POST "TU_WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "Agente-Dani",
    "content": "🤖 Conexión confirmada desde el ecosistema de Dani"
  }'
```

Si aparece el mensaje en el canal de Discord, ¡funciona!

---

## PARTE 3 — CONFIGURAR TUS VARIABLES DE ENTORNO

### Paso 3.1 — Crear la carpeta segura de secretos

```bash
mkdir -p ~/.secrets/mi-ecosistema
chmod 700 ~/.secrets/mi-ecosistema
```

### Paso 3.2 — Crear tu archivo de variables

```bash
nano ~/.secrets/mi-ecosistema/env_vars.sh
```

Escribe esto (reemplaza con tus valores reales):

```bash
# Telegram
export TELEGRAM_BOT_TOKEN="7123456789:AABBCCDDEEFFaabbccddeeff1234567890"
export TELEGRAM_GROUP_ID="-1234567890"

# Discord
export DISCORD_WEBHOOK_BITACORA="https://discord.com/api/webhooks/..."
export DISCORD_WEBHOOK_LABORATORIO="https://discord.com/api/webhooks/..."
export DISCORD_WEBHOOK_DECISIONES="https://discord.com/api/webhooks/..."
export DISCORD_WEBHOOK_PUENTE="https://discord.com/api/webhooks/..."
```

Guarda con `Ctrl+O`, cierra con `Ctrl+X`.

```bash
chmod 600 ~/.secrets/mi-ecosistema/env_vars.sh
```

### Paso 3.3 — Cargar las variables en tu sesión

```bash
source ~/.secrets/mi-ecosistema/env_vars.sh
```

Para que se carguen automáticamente cada vez que abres la terminal:

```bash
echo 'source ~/.secrets/mi-ecosistema/env_vars.sh' >> ~/.zshrc
```

---

## PARTE 4 — TU PRIMER AGENTE

### Paso 4.1 — Clonar el framework

```bash
git clone https://github.com/jeipgg/agentes-familia.git
cd agentes-familia
```

### Paso 4.2 — Crear tu agente desde la plantilla

```bash
cp agents/templates/AGENT_TEMPLATE.md mi-agente.md
```

Edita `mi-agente.md` con tu editor favorito y completa:
- Nombre del agente
- Dimensión (estrategia, bienestar, operaciones...)
- Skills principales
- Canales de reporte

### Paso 4.3 — Crear tu script de comunicación

Crea un archivo `mi_agente.sh`:

```bash
#!/bin/bash
source ~/.secrets/mi-ecosistema/env_vars.sh

# Función: publicar en Telegram
telegram_msg() {
  curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage" \
    -H "Content-Type: application/json" \
    -d "{
      \"chat_id\": \"${TELEGRAM_GROUP_ID}\",
      \"text\": \"$1\",
      \"parse_mode\": \"Markdown\"
    }" > /dev/null
  echo "✅ Telegram: enviado"
}

# Función: publicar en Discord
discord_msg() {
  local webhook=$1
  local mensaje=$2
  curl -s -X POST "$webhook" \
    -H "Content-Type: application/json" \
    -d "{
      \"username\": \"Agente-Dani\",
      \"content\": \"$mensaje\"
    }" > /dev/null
  echo "✅ Discord: enviado"
}

# Uso:
# telegram_msg "Hola desde el agente de Dani 🤖"
# discord_msg "$DISCORD_WEBHOOK_LABORATORIO" "Reporte desde ecosistema Dani"
```

```bash
chmod +x mi_agente.sh
```

---

## PARTE 5 — PROTOCOLO DE COLABORACIÓN CON EL OTRO ECOSISTEMA

### Cuándo publicar en cada canal

| Canal | Cuándo |
|---|---|
| `#bitacora-dani` | Logs internos de tus agentes (solo tú) |
| `#laboratorio-agentes` | Cuando tu agente propone algo al otro ecosistema |
| `#archivo-decisiones` | Solo veredictos finales aprobados por ambos humanos |
| `#puente-humano` | Comunicación directa entre los dos humanos |
| Telegram grupo | Alertas cortas y urgentes |

### Template para publicar en #laboratorio-agentes

```bash
discord_msg "$DISCORD_WEBHOOK_LABORATORIO" \
"**[AGENTE-DANI] → [TEMA]**
📋 Contexto: descripción breve
🎯 Propuesta: qué propones
⏳ Urgencia: alta / media / baja
✅ Requiere aprobación humana: sí / no"
```

---

## PARTE 6 — VERIFICACIÓN FINAL

Corre este checklist antes de considerar que estás conectado:

```bash
source ~/.secrets/mi-ecosistema/env_vars.sh

# Test Telegram
echo "Probando Telegram..."
curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage" \
  -H "Content-Type: application/json" \
  -d '{"chat_id": "'"$TELEGRAM_GROUP_ID"'", "text": "✅ Ecosistema Dani — conexión verificada"}' \
  | python3 -c "import sys,json; r=json.load(sys.stdin); print('OK' if r['ok'] else 'ERROR')"

# Test Discord
echo "Probando Discord..."
curl -s -X POST "$DISCORD_WEBHOOK_LABORATORIO" \
  -H "Content-Type: application/json" \
  -d '{"username":"Agente-Dani","content":"✅ Ecosistema Dani — conexión verificada"}' \
  && echo "OK"
```

Si ambos muestran `OK` y los mensajes llegan, **estás listo.**

---

## RESUMEN DE LO QUE TIENES AL FINAL

```
~/.secrets/mi-ecosistema/
└── env_vars.sh          ← Todos tus tokens (privado, nunca al repo)

agentes-familia/
├── mi-agente.md         ← Tu agente personalizado
└── mi_agente.sh         ← Script de comunicación

Canales activos:
✅ Telegram — grupo familiar
✅ Discord #bitacora-dani
✅ Discord #laboratorio-agentes
```

---

*Cualquier duda, el canal es `#puente-humano` en Discord.*
