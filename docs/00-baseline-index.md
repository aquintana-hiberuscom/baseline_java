# 00 — Índice del baseline técnico

Este documento define cómo se organizan las especificaciones técnicas del proyecto y cuál es la fuente de verdad para cada tipo de decisión.

## Objetivo

Evitar que cada agente de IA implemente “a su manera”. El baseline técnico debe permitir que cualquier agente pueda entender la arquitectura objetivo, localizar reglas aplicables, mantener trazabilidad entre US, especificación, código y tests, y validar que no se ha saltado ninguna regla.

## Ficheros y responsabilidades

| Ruta | Responsabilidad |
|---|---|
| `/AGENTS.md` | Contrato principal para agentes de IA. Contiene reglas operativas, límites y orden de lectura. |
| `/.github/copilot-instructions.md` | Instrucciones globales de GitHub Copilot para el repositorio. Debe ser corto y remitir a `/AGENTS.md` y `/docs`. |
| `/.github/instructions/java-hexagonal.instructions.md` | Instrucciones específicas para paths Java/Spring/hexagonal. |
| `/.github/prompts/implement-user-story.prompt.md` | Prompt reutilizable para implementar una US siguiendo el baseline. |
| `/README.md` | Onboarding humano del proyecto. No debe ser el baseline completo. |
| `/docs/01-technical-baseline.md` | Arquitectura, stack, módulos, estructura y reglas técnicas no negociables. |
| `/docs/02-sdd-workflow.md` | Flujo Spec Driven Development: US → especificación → diseño → tareas → implementación → validación. |
| `/docs/03-coding-standards.md` | Convenciones de código del día a día. |
| `/docs/04-testing-strategy.md` | Estrategia de pruebas, tipos de test y quality gates. |
| `/docs/05-ai-usage-log.md` | Registro de decisiones y acciones relevantes realizadas con IA. |
| `/docs/adr/` | Architecture Decision Records para decisiones técnicas relevantes. |

## Qué NO debe duplicarse

- `README.md` no debe duplicar todo el baseline; solo enlazarlo.
- `copilot-instructions.md` no debe ser enorme; debe actuar como entrada corta y estable.
- `AGENTS.md` debe contener reglas operativas para agentes, no toda la documentación técnica extensa.
- Los estándares de código no deben repetir decisiones arquitectónicas completas.
- La estrategia de testing no debe mezclarse con reglas de naming o estructura de paquetes.

## Fuentes de verdad

| Tema | Fuente de verdad |
|---|---|
| Comportamiento de agentes IA | `/AGENTS.md` |
| Arquitectura y stack | `/docs/01-technical-baseline.md` |
| Flujo de implementación desde US | `/docs/02-sdd-workflow.md` |
| Estilo de código | `/docs/03-coding-standards.md` |
| Pruebas y validación | `/docs/04-testing-strategy.md` |
| Contratos HTTP | OpenAPI del módulo `incident-manager-app` |
| Decisiones relevantes | `/docs/adr/` |
| Onboarding humano | `/README.md` |

## Orden de trabajo para una nueva US

1. Leer la US completa.
2. Validar que la US tiene criterios de aceptación verificables.
3. Leer `/AGENTS.md`.
4. Leer este índice.
5. Leer los documentos aplicables según el tipo de cambio.
6. Si afecta a HTTP, revisar o modificar OpenAPI primero.
7. Diseñar por capas.
8. Implementar de dentro hacia fuera.
9. Añadir tests.
10. Validar criterios de aceptación.
11. Documentar cambios relevantes en `/docs/05-ai-usage-log.md` si aplica.

## Convención de documentación funcional recomendada

```text
functional/
└── US/
    └── US-001-listado-productos-disponibles.md
```

Cada US debería incluir historia de usuario, contexto, alcance, criterios de aceptación, reglas de negocio, supuestos, dudas abiertas y revisión INVEST.

## Convención de especificaciones técnicas por feature

```text
specs/
└── US-001-listado-productos-disponibles/
    ├── specification.md
    ├── technical-design.md
    ├── tasks.md
    └── validation.md
```

Esta estructura evita mezclar el baseline estable del proyecto con documentación específica de una feature.
