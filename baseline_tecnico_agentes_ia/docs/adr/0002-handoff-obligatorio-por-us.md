# ADR-0002 — Handoff técnico obligatorio por US o tarea

## Estado

Aceptada.

## Contexto

Los agentes de IA pueden perder contexto entre sesiones. Sin un handoff técnico por implementación, futuros agentes pueden duplicar código, ignorar decisiones previas o no reutilizar servicios, DTOs, endpoints, validadores, entidades o tests ya existentes.

## Decisión

Cada User Story o tarea implementada con IA debe cerrar con un handoff técnico obligatorio.

- Plantilla: `docs/ai/handoff-template.md`.
- Destino: `docs/ai/handoffs/`.
- Nombre: `handoff-[yyyyMMdd]-[feature-kebab-case].md`.
- El handoff forma parte del mismo cambio/PR que la implementación.
- Antes de implementar una nueva US, el agente debe revisar handoffs previos relevantes.

## Consecuencias

- Mejora continuidad entre sesiones/agentes.
- Reduce duplicidades.
- Facilita reutilización de código existente.
- Aumenta disciplina documental.
- Requiere mantener handoffs compactos y útiles.
