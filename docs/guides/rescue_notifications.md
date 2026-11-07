# Rescuer WhatsApp and SMS notifications

The mission can notify one rescuer whenever a survivor is confirmed. WhatsApp receives a PNG cropped from that survivor's dossier route plus the full coordinates, axis convention, entry point, route risk, ETA, hazards and turn-by-turn directions. TextBee receives the same operational essentials as SMS. At mission completion, both receive a summary and WhatsApp receives the final all-survivor situation map after all individual route maps have been queued.

## Setup

1. Run `npm install` once at the repository root.
2. Create a TextBee account and pair its Android app. Either export `TEXTBEE_API_KEY` and optional `TEXTBEE_DEVICE_ID`, or put them in the ignored local `.env.notifications` file. Shell environment variables take precedence.
3. Run `npm run swarm` (or run `npm run notifications` beside the frontend).
4. On first use, scan the terminal QR from WhatsApp **Linked devices**. Credentials are stored in ignored `.runtime/baileys-auth/`.
5. In Mission settings, enter the rescuer's number in E.164 format (for example `+919876543210`), choose the channels, then select **Save & enable**.

Optional environment variables:

- `WHATSAPP_ENABLED=false` disables Baileys.
- `BAILEYS_AUTH_DIR=/secure/persistent/path` changes credential storage. Use persistent, access-controlled storage in production.
- `TEXTBEE_BASE_URL` changes the TextBee API base; the default is `https://api.textbee.dev/api/v1`.
- `NOTIFICATION_PORT` changes the local gateway port; update the Vite proxy if it is not 8787.

TextBee sends SMS, not MMS, so it cannot carry the dossier PNG. The SMS explicitly says that the photo was sent over WhatsApp. A TextBee `200` response means the message was accepted for dispatch; delivery still depends on the paired Android phone and carrier.

Baileys is an unofficial WhatsApp Web client. Use a dedicated, consented recipient and follow WhatsApp's terms; do not use this gateway for bulk messaging. `useMultiFileAuthState` is suitable for this local prototype, but production should move auth keys to a durable encrypted database-backed store.

The gateway binds to `127.0.0.1`, validates E.164 numbers, limits request bodies, never exposes credentials to the browser and keeps per-channel idempotency for the running process. The public demo proxy intentionally does not expose these endpoints; production deployment needs authenticated access controls, durable idempotency, persistent Baileys auth storage and an explicit notification proxy configuration.
