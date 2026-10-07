# Prompt — Payment Provider

Implementa la abstracción `PaymentProvider`.

No acoples UI a Culqi.

Crear modelos:
PaymentRequest, PaymentResult, PaymentStatus, RefundResult.

Crear errores tipados:
Network, Validation, Provider, Authentication, Timeout, Unknown.

El adaptador debe poder reemplazarse por Mercado Pago/Izipay sin modificar
las features de pagos.

No almacenar secretos.
No guardar PAN/CVV.
