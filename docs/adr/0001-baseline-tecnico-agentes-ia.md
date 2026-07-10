# ADR-0001 — Baseline técnico para desarrollo con agentes de IA

## Estado

Aceptada.

## Contexto

El proyecto se desarrolla con apoyo de agentes de IA. Sin un baseline técnico claro, un agente puede implementar una User Story usando criterios propios, generando inconsistencias en arquitectura, naming, testing, contratos o estructura de paquetes.

Existían varias fuentes de instrucciones: `AGENTS.md`, `README.md`, `copilot-instructions.md`, `docs/technical-specification.md`, `docs/sdd-specification.md` y `docs/coding-standards.md`.

## Decisión

Se adopta una estructura separada por responsabilidad:

- `/AGENTS.md`: contrato operativo principal para agentes.
- `/.github/copilot-instructions.md`: instrucciones globales, cortas y siempre aplicables para GitHub Copilot.
- `/.github/instructions/*.instructions.md`: instrucciones específicas por path o tecnología.
- `/.github/prompts/*.prompt.md`: prompts reutilizables para tareas frecuentes.
- `/docs/00-baseline-index.md`: índice y mapa de fuentes de verdad.
- `/docs/01-technical-baseline.md`: arquitectura y reglas técnicas no negociables.
- `/docs/02-sdd-workflow.md`: flujo Spec Driven Development.
- `/docs/03-coding-standards.md`: reglas de implementación.
- `/docs/04-testing-strategy.md`: estrategia de pruebas.
- `/docs/05-ai-usage-log.md`: trazabilidad del uso de IA.
- `/docs/adr/`: decisiones de arquitectura.

## Consecuencias positivas

Reduce duplicidad, facilita que Copilot y otros agentes encuentren reglas aplicables, distingue onboarding humano de reglas de agentes y mejora trazabilidad US → especificación → diseño → código → tests.

## Consecuencias negativas

Hay más ficheros que mantener y se requiere disciplina para no duplicar contenido.

## Regla de mantenimiento

- Cambio de comportamiento del agente: actualizar `AGENTS.md`.
- Cambio de arquitectura: actualizar `docs/01-technical-baseline.md`.
- Cambio de flujo: actualizar `docs/02-sdd-workflow.md`.
- Cambio de estilo de código: actualizar `docs/03-coding-standards.md`.
- Cambio de testing: actualizar `docs/04-testing-strategy.md`.
- Decisión relevante: crear o actualizar un ADR.
