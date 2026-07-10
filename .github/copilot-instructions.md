# GitHub Copilot — Instrucciones de repositorio

Este repositorio usa un baseline técnico para desarrollo asistido por IA.

## Instrucción principal

Antes de generar, modificar o revisar código, aplica siempre:

1. [`/AGENTS.md`](../AGENTS.md)
2. [`/docs/00-baseline-index.md`](../docs/00-baseline-index.md)
3. [`/docs/01-technical-baseline.md`](../docs/01-technical-baseline.md)
4. [`/docs/02-sdd-workflow.md`](../docs/02-sdd-workflow.md)
5. [`/docs/03-coding-standards.md`](../docs/03-coding-standards.md)
6. [`/docs/04-testing-strategy.md`](../docs/04-testing-strategy.md)
7. `/docs/06-handoff-process.md`

## Handoff obligatorio

- Lee handoffs anteriores antes de implementar.
- Genera handoff obligatorio al cerrar cada US o tarea.
- Los handoffs viven en `/docs/ai/handoffs/`.
- Usa la plantilla `/docs/ai/handoff-template.md`.

## Resumen operativo

- Arquitectura hexagonal por agregados.
- Java 21, Spring Boot 3.2.x, Maven, PostgreSQL, Liquibase, MapStruct y Cucumber.
- OpenAPI es la fuente de verdad de los contratos HTTP.
- El dominio no puede depender de Spring, JPA ni infraestructura.
- La aplicación depende de puertos, no de adaptadores concretos.
- Los adaptadores traducen entre HTTP/persistencia/integraciones y el dominio.
- Los mappers se implementan con MapStruct y se prueban campo a campo.
- Toda funcionalidad debe incluir tests acordes a su capa.
- No ejecutes commits ni pushes.

## Si hay ambigüedad

No inventes reglas de negocio ni arquitectura. Detente, enumera la duda y propón la mínima decisión necesaria para continuar.
