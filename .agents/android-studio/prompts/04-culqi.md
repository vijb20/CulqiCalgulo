# Prompt — Culqi

Integra Culqi usando únicamente documentación oficial y el SDK/API vigente.

Antes de programar:
- identifica flujo de tokenización;
- identifica flujo de cargo/orden;
- identifica eventos Webhook;
- distingue pagos síncronos/asíncronos;
- identifica qué puede vivir en Android y qué requiere backend.

Reglas:
- public key solamente donde sea seguro;
- secret key solamente en serverless;
- no inventar endpoints;
- pruebas en sandbox primero.

El resultado debe implementar únicamente el contrato PaymentProvider.
