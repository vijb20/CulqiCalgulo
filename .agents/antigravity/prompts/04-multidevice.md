# Prompt — Multi-device

Diseña sincronización de N dispositivos por comercio.

Cada instalación tiene:
merchantId, deviceId, installationId.

Requisitos:
- UUID global;
- idempotencia;
- cursor o updatedAt para incremental sync;
- conflictos explícitos;
- no duplicar pagos;
- aislamiento por merchant;
- dispositivo offline;
- recuperación tras reinstalación.

Documenta qué datos son globales y cuáles son propios del dispositivo.
