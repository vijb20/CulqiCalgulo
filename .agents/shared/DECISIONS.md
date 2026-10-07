# Decisiones arquitectónicas

## ADR-001 — Local-first
Room/SQLite es la fuente operacional local. La nube nunca bloquea las funciones
locales.

## ADR-002 — Zero-ops
No mantener servidores propios. Backend únicamente serverless/managed cuando sea
necesario.

## ADR-003 — PaymentProvider
Las features nunca llaman directamente a SDK/API de un PSP. Usan una abstracción.

## ADR-004 — Webhooks
Las confirmaciones de pago se consideran confiables cuando llegan por el mecanismo
oficial del PSP y superan validación/idempotencia.

## ADR-005 — Secretos
Las claves privadas de proveedores viven únicamente en secretos del entorno
serverless/backend. Nunca en APK, repositorio o Room.

## ADR-006 — Multi-device
Los pagos usan UUID global + merchantId + deviceId + externalReference para
correlación e idempotencia.

## ADR-007 — Publicidad
Solo banners no intrusivos y desacoplados de la lógica de pagos.

## ADR-008 — Proveedor inicial
Culqi es el primer adaptador previsto, pero la arquitectura no debe quedar
acoplada a Culqi.

## ADR-009 — Infraestructura
No elegir tecnología por familiaridad si aumenta el costo operativo. Quarkus puede
existir como backend self-hosted futuro, no como requisito del MVP zero-ops.

## ADR-010 — Cambios
Todo cambio que afecte seguridad, pagos, sincronización, persistencia o costo debe
crear/actualizar un ADR antes de implementarse.
