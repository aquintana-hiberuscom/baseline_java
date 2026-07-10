# 06 — Handoff Process

## Propósito

Definir el proceso obligatorio de handoff técnico al cerrar cada User Story o tarea implementada con IA.

El objetivo es que futuros agentes puedan entender rápidamente qué se hizo, qué código existe, qué debe reutilizarse y qué no debe duplicarse.

## Ubicación

Plantilla oficial:

```text
docs/ai/handoff-template.md
```

Handoffs generados:

```text
docs/ai/handoffs/
```

Convención de nombre:

```text
handoff-[yyyyMMdd]-[feature-kebab-case].md
```

Ejemplo:

```text
docs/ai/handoffs/handoff-20260710-list-products.md
```

## Regla antes de implementar

Antes de iniciar una nueva US o tarea, el agente debe:

1. Leer la US/tarea actual.
2. Leer el baseline técnico.
3. Revisar handoffs previos en `docs/ai/handoffs/`.
4. Priorizar handoffs de la misma capacidad funcional, mismos endpoints, mismos servicios, mismas entidades, mismos DTOs, mismos tests o más recientes.
5. Identificar elementos existentes que debe reutilizar.
6. Identificar código que no debe duplicar.
7. Mencionar en el plan de implementación qué handoffs ha tenido en cuenta.

## Regla al cerrar una US o tarea

Al finalizar, el agente debe:

1. Revisar el diff y el código final.
2. Generar un handoff con `docs/ai/handoff-template.md`.
3. Guardarlo en `docs/ai/handoffs/`.
4. Incluirlo en el mismo cambio/PR que la implementación.
5. Informar en el resumen final la ruta del handoff generado.

## Contenido mínimo del handoff

- Metadatos.
- Resumen ejecutivo.
- Alcance implementado y no incluido.
- Carpetas afectadas.
- Ficheros creados y modificados.
- Endpoints, servicios, DTOs, validadores, persistencia y configuración.
- Tests añadidos o modificados.
- Decisiones técnicas.
- Reutilización obligatoria en futuras US.
- Código que no debe duplicarse.
- Riesgos, limitaciones y deuda técnica.
- Validación final realizada.
- Resumen ultra-compacto para contexto IA.

## Relación con otros documentos

- `AGENTS.md`: obliga a leer y generar handoffs.
- `.github/copilot-instructions.md`: recuerda la regla de handoff a Copilot.
- `.github/prompts/implement-user-story.prompt.md`: incluye el handoff en el flujo de implementación.
- `docs/02-sdd-workflow.md`: incorpora el handoff como cierre del ciclo SDD.
- `docs/05-ai-usage-log.md`: registra cambios de baseline o decisiones relevantes; no sustituye al handoff.

## Diferencia entre AI Usage Log y Handoff

- `docs/05-ai-usage-log.md`: registra decisiones o eventos relevantes de uso de IA.
- `docs/ai/handoffs/*.md`: documenta una implementación concreta y sirve como memoria técnica reutilizable por futuros agentes.
