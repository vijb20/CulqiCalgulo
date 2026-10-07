# Prompt — Security Review

Audita el módulo actual.

Busca:
- secretos en código;
- claves en BuildConfig;
- logs sensibles;
- PAN/CVV;
- almacenamiento inseguro;
- llamadas directas a BD;
- estados de pago falsificables;
- falta de idempotencia;
- autorización por merchantId;
- problemas de backup/export.

No modifiques código sin explicar el riesgo y la corrección.
