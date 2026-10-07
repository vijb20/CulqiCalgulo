# Prompt — Sincronización

Implementa sincronización local-first.

Estados:
LOCAL_ONLY -> PENDING -> SYNCING -> SYNCED
ERROR -> RETRY

Usa WorkManager con:
- constraints de red;
- backoff;
- límite de reintentos;
- idempotencia;
- logs sin secretos.

Si la BD externa no responde:
- el usuario sigue operando;
- los datos quedan locales;
- se reintenta después.

No borrar la cola hasta recibir confirmación de procesamiento.
