# Prompt — Backend Serverless

Diseña el backend sin servidores administrados por nosotros.

Candidatos:
- Supabase Edge Functions + PostgreSQL;
- Cloudflare Workers + Queues + almacenamiento adecuado;
- otros BaaS/serverless equivalentes.

Funciones mínimas:
- Webhook receiver;
- validación;
- idempotencia;
- merchant isolation;
- sincronización;
- consulta de estado;
- auditoría mínima.

Nunca devolver secretos al Android.

Debe existir un modo local-only si el backend no está configurado.
