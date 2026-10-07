# Especificación maestra v1.0

## 1. Producto

**Cuaderno de Control Móvil** es una aplicación Android para controlar productos,
dispositivos, usuarios, pagos, precios y reportes.

Objetivos:
- operar sin depender de Internet para la gestión local;
- registrar siempre primero en la BD local;
- integrar pagos electrónicos;
- recibir confirmaciones de pagos externos mediante Webhooks;
- sincronizar entre varios dispositivos cuando exista backend;
- generar reportes;
- monetizar únicamente mediante banners no intrusivos;
- evitar infraestructura propia obligatoria.

## 2. Arquitectura

```text
                         PROVEEDOR DE PAGOS
                    Culqi / Mercado Pago / Izipay
                               |
                         Webhook HTTPS
                               |
                     SERVERLESS GATEWAY
                               |
                   +-----------+-----------+
                   |                       |
              Event Store              Sync/API
                   |                       |
                   +-----------+-----------+
                               |
                         Base central
                          (opcional)
                               |
              +----------------+----------------+
              |                |                |
          Android 1        Android 2        Android N
              |                |                |
             Room             Room             Room
```

La aplicación Android no debe conectarse directamente a PostgreSQL ni a otra BD
administrada mediante credenciales privilegiadas.

## 3. Local-first

Flujo normal:

```text
UI -> UseCase -> Repository -> Room -> confirmado localmente
                                      |
                                      v
                                  SyncQueue
                                      |
                                      v
                               backend opcional
```

Estados de sincronización:
`LOCAL_ONLY`, `PENDING`, `SYNCING`, `SYNCED`, `ERROR`.

Estados de pago:
`PENDING`, `APPROVED`, `DECLINED`, `CANCELLED`, `ERROR`, `REFUNDED`.

Nunca mezclar ambos estados.

## 4. Multi-dispositivo

Cada instalación debe tener identificadores estables:

- `merchantId`
- `deviceId`
- `installationId`

Cada operación debe tener un UUID global.

La sincronización debe ser idempotente.

Un pago confirmado en un dispositivo puede distribuirse a los demás dispositivos
del mismo comercio mediante la capa central.

## 5. Proveedor de pagos

Crear:

```kotlin
interface PaymentProvider {
    suspend fun createPayment(request: PaymentRequest): PaymentResult
    suspend fun getPaymentStatus(paymentId: String): PaymentStatus
    suspend fun refund(paymentId: String, amount: Long?): RefundResult
}
```

No acoplar las features a Culqi.

Adaptadores previstos:

```text
payment/
  domain/
  culqi/
  mercadopago/
  izipay/
```

La selección real del proveedor se decide mediante configuración y ADR.

## 6. Webhooks

El Webhook no se aloja en Android.

El endpoint será una función serverless gestionada.

Debe:
1. validar autenticidad/firma según el proveedor;
2. aceptar solamente eventos soportados;
3. registrar el evento bruto mínimo necesario;
4. aplicar idempotencia;
5. transformar el evento a un evento de dominio;
6. actualizar el estado del pago;
7. responder rápidamente;
8. usar cola/reintentos cuando el proveedor lo permita.

Nunca confiar únicamente en el cliente Android para marcar un pago como confirmado.

## 7. Entidades mínimas

PRODUCT:
`id, name, description, cost, price, active, createdAt, updatedAt, syncStatus`

CUSTOMER:
`id, name, identifier, active, createdAt, updatedAt, syncStatus`

USER:
`id, username, role, active, createdAt, updatedAt, syncStatus`

DEVICE:
`id, name, identifier, active, createdAt, updatedAt, syncStatus`

PAYMENT:
`id, merchantId, deviceId, userId, productId, customerId, amount, currency,
status, provider, providerPaymentId, externalReference, paymentMethod,
createdAt, updatedAt, syncStatus`

PAYMENT_EVENT:
`id, paymentId, provider, providerEventId, eventType, receivedAt, processedAt,
processingStatus, errorMessage`

SYNC_QUEUE:
`id, entityId, entityType, operation, status, attempts, lastAttempt,
lastError, createdAt, syncedAt`

## 8. Roles

- ADMIN: configuración, usuarios, proveedores, reportes y datos completos.
- WORKER: ventas/pagos y consulta operativa; sin secretos ni datos sensibles.
- VIEWER/CLIENT: consulta restringida.

## 9. Calculadora de precios

Variables:
- costo;
- gastos adicionales;
- utilidad objetivo;
- comisión porcentual;
- comisión fija;
- impuestos;
- redondeo.

Cuando la comisión es porcentual sobre el precio:

`precio = (costoTotal + utilidad + cargoFijo) / (1 - porcentaje)`

La tasa del proveedor debe ser configurable, nunca hardcodeada.

## 10. Reportes

Mínimos:
- ventas por día;
- ventas por período;
- ventas por dispositivo;
- ventas por usuario;
- ventas por método de pago;
- devoluciones;
- sincronización pendiente/error.

Exportación inicial:
CSV y PDF.

## 11. Publicidad

Solo banners no intrusivos.

No mostrar anuncios:
- durante el pago;
- mientras se procesa un pago;
- en el resultado inmediato del pago;
- en configuración sensible;
- sobre controles críticos.

Usar una abstracción:

```kotlin
interface AdvertisingService {
    fun loadBanner()
    fun showBanner()
    fun hideBanner()
    fun destroyBanner()
}
```

## 12. Stack Android

- Kotlin
- Jetpack Compose
- Material 3
- Clean Architecture
- MVVM
- Hilt
- Room
- Coroutines/Flow
- WorkManager
- Kotlin Serialization
- Ktor Client
- Android Keystore
- JUnit + AndroidX Test

No introducir dependencias innecesarias.

## 13. Observabilidad

Registrar:
- correlationId;
- paymentId;
- providerPaymentId;
- deviceId;
- eventId;
- sync status.

Nunca registrar:
- PAN;
- CVV;
- claves secretas;
- tokens sensibles completos;
- credenciales.

## 14. Zero-ops

Prohibido asumir:
- VPS;
- servidor dedicado;
- Kubernetes;
- VM;
- PostgreSQL administrado como requisito;
- dominio propio como requisito de desarrollo.

El backend serverless es una dependencia opcional y gestionada.

## 15. Compatibilidad futura

El sistema debe permitir:
- cambiar proveedor de pagos;
- cambiar proveedor serverless;
- funcionar local-only;
- activar sincronización central;
- agregar nuevos reportes;
- agregar nuevos métodos de pago.
