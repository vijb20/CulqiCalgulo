# Prompt — Base local

Implementa Room como fuente operacional local.

Entidades:
PRODUCT, CUSTOMER, USER, DEVICE, PAYMENT, PAYMENT_EVENT, SYNC_QUEUE.

Requisitos:
- UUID;
- timestamps;
- migrations;
- repositories;
- DAO;
- tests;
- separación paymentStatus/syncStatus;
- transacciones cuando corresponda.

Demuestra:
1. crear producto offline;
2. registrar pago offline;
3. reiniciar app;
4. recuperar datos.
