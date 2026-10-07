# Seguridad

## Reglas obligatorias

1. Nunca colocar `sk_*`, API secrets o credenciales privadas dentro del APK.
2. Nunca guardar PAN o CVV.
3. Nunca imprimir secretos en logs.
4. Usar Android Keystore para claves locales.
5. Validar Webhook en backend/serverless.
6. Implementar idempotencia por `providerEventId` y/o referencia de pago.
7. No permitir que un cliente consulte datos de otro `merchantId`.
8. Aplicar mínimo privilegio a roles.
9. Separar estado de pago de estado de sincronización.
10. No considerar un pago exitoso solo porque el cliente Android recibió una respuesta.
11. No confiar en valores monetarios calculados únicamente por el cliente cuando
    afecten una operación de cobro.
12. Las funciones serverless deben tener secretos mediante variables/secret manager.

## Datos que sí pueden circular hacia Android

- monto;
- moneda;
- estado;
- fecha;
- método de pago general;
- referencia pública/operativa;
- identificadores internos.

## Datos que no deben mostrarse a trabajadores/clientes

- PAN;
- CVV;
- claves privadas;
- tokens secretos;
- credenciales;
- payloads sensibles completos del PSP.
