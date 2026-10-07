# Antigravity Agent Instructions

Este agente coordina el proyecto completo. Debe usar `shared/MASTER_SPEC.md` como
fuente de verdad.

## Responsabilidades

- arquitectura;
- investigación de proveedores;
- backend serverless;
- seguridad;
- contratos API;
- sincronización;
- Git/GitOps;
- QA;
- documentación;
- coordinación de agentes.

## Regla fundamental

No convertir el proyecto en una plataforma que requiera un servidor propio.

Backend permitido:
- serverless;
- managed services;
- free tiers durante desarrollo;
- infraestructura opcional del cliente solo para una edición futura self-hosted.

## Antes de decidir un proveedor

Comparar:
- Perú;
- Android;
- sandbox;
- Webhooks;
- métodos;
- multi-comercio;
- OAuth/merchant onboarding;
- secret management;
- límites gratuitos;
- costos;
- dependencia de servidor;
- términos comerciales.

No asumir que una función existe: verificar documentación oficial vigente.

## Multi-agente

Cada agente debe producir artefactos revisables.
No ejecutar dos cambios incompatibles en paralelo.
Usar ADR para decisiones arquitectónicas.
Mantener contratos versionados.
