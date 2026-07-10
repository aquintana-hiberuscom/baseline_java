---
description: Implementar una User Story siguiendo el baseline técnico del repositorio
---

# Implementar User Story con baseline técnico

Usa este prompt cuando quieras que un agente implemente una US del proyecto.

## Prompt

Quiero que implementes la siguiente User Story siguiendo estrictamente el baseline técnico del repositorio.

Antes de escribir código:

1. Lee `/AGENTS.md`.
2. Lee `/docs/00-baseline-index.md`.
3. Lee `/docs/01-technical-baseline.md`.
4. Lee `/docs/02-sdd-workflow.md`.
5. Lee `/docs/03-coding-standards.md`.
6. Lee `/docs/04-testing-strategy.md`.
7. Lee `/docs/06-handoff-process.md`.
8. Revisa `/docs/ai/handoffs/*.md` y prioriza handoffs de la misma capacidad, mismos endpoints, mismos servicios, mismas entidades o recientes.
9. Identifica si la US afecta a OpenAPI, dominio, aplicación, infraestructura, persistencia, seguridad o tests de aceptación.
10. Propón brevemente el diseño por capas y los ficheros que vas a tocar.

Durante la implementación:

- Respeta arquitectura hexagonal por agregados.
- No pongas lógica de negocio en controladores ni adaptadores.
- Usa puertos de entrada y salida.
- Usa MapStruct para mapeos.
- Añade tests de la capa correspondiente.
- Si modificas contrato HTTP, empieza por OpenAPI y regenera.

Al finalizar:

- Genera handoff obligatorio usando `/docs/ai/handoff-template.md`.
- Guarda el handoff en `/docs/ai/handoffs/handoff-[yyyyMMdd]-[feature-kebab-case].md`.
- Devuelve resumen, tests, comandos, criterios cubiertos, handoff generado y riesgos.

Al finalizar devuelve:

- Resumen de cambios.
- Ficheros modificados.
- Tests añadidos.
- Comandos ejecutados.
- Criterios de aceptación cubiertos.
- Dudas o riesgos pendientes.

## User Story

Pega aquí la US completa en Markdown.
