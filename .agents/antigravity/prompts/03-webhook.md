# Prompt — Webhook Gateway

Diseña un receptor genérico de Webhooks.

Contrato interno:

WebhookEvent:
- provider;
- providerEventId;
- eventType;
- merchantId;
- paymentId/externalReference;
- receivedAt;
- payloadHash;
- processingStatus.

Flujo:
receive -> authenticate -> deduplicate -> persist -> enqueue -> process -> ack.

Responder rápidamente.
No ejecutar procesos largos antes del ACK.
Usar reintentos.
No guardar datos sensibles innecesarios.
