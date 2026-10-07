# Cuaderno de Control Móvil — Kit de Agentes

Este paquete contiene la memoria operativa, reglas, skills y prompts para construir
**Cuaderno de Control Móvil** con dos familias de agentes:

- `android-studio/`: agentes/prompts orientados al desarrollo Android.
- `antigravity/`: agentes/prompts orientados a coordinación, arquitectura, backend serverless,
  investigación, QA y automatización.

## Regla principal

El proyecto debe ser **local-first/offline-first** y priorizar **costo cero / zero-ops**:
no debe exigir que el desarrollador ni el cliente mantengan un servidor propio.

## Arquitectura objetivo

Android:
Kotlin + Jetpack Compose + Clean Architecture + MVVM + Hilt + Room + WorkManager.

Pagos:
`PaymentProvider` como abstracción. Primera integración: Culqi.
Posibles proveedores futuros: Mercado Pago, Izipay u otro proveedor compatible.

Backend:
serverless gestionado, no servidor VPS/VM propio. La implementación concreta
(Cloudflare Workers, Supabase Edge Functions u otra) debe quedar detrás de interfaces
y configuración.

Datos:
Room/SQLite siempre registra localmente. La base externa es opcional y se usa para
sincronización, Webhooks, multi-dispositivo y respaldo.

Seguridad:
nunca almacenar PAN/CVV ni claves secretas del PSP en el APK.

## Orden recomendado

1. Leer `shared/MASTER_SPEC.md`.
2. Leer `shared/DECISIONS.md`.
3. Leer `shared/SECURITY.md`.
4. Leer `shared/DEFINITION_OF_DONE.md`.
5. El agente debe trabajar una tarea pequeña por vez.
6. Ejecutar pruebas después de cada cambio.
7. No introducir infraestructura obligatoria sin justificarla.
8. No cambiar decisiones arquitectónicas sin registrar ADR.

## Nota sobre compatibilidad

Los archivos están escritos en Markdown deliberadamente. `AGENTS.md` y las carpetas
`skills/` pueden adaptarse a la convención exacta que use la versión instalada de
Android Studio o Antigravity. El contenido de las reglas es la fuente de verdad.
