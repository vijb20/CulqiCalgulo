# Definition of Done

Una tarea solo está terminada cuando:

- [ ] compila;
- [ ] tests relevantes pasan;
- [ ] no introduce secretos;
- [ ] no rompe offline-first;
- [ ] mantiene separación payment status/sync status;
- [ ] tiene manejo de errores;
- [ ] usa IDs idempotentes donde corresponda;
- [ ] no agrega infraestructura obligatoria sin ADR;
- [ ] documentación actualizada si cambia arquitectura;
- [ ] cambios pequeños y revisables;
- [ ] no se mezclan refactors no relacionados.

Para pagos:
- [ ] sandbox/test primero;
- [ ] Webhook validado;
- [ ] idempotencia probada;
- [ ] caso de timeout;
- [ ] caso de duplicado;
- [ ] caso de pago aprobado con sync fallido;
- [ ] caso de devolución si aplica.

Para sincronización:
- [ ] offline;
- [ ] retry;
- [ ] backoff;
- [ ] duplicado;
- [ ] conflicto;
- [ ] recuperación después de reinicio.
