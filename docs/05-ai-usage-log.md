# 05 — AI Usage Log

Registro de uso de IA para decisiones, especificaciones y cambios relevantes.

## Cuándo registrar

Registrar cuando se toma una decisión técnica relevante, se crea o modifica el baseline, se genera una especificación importante, se resuelve una ambigüedad, se introduce una convención reusable o se detecta un riesgo relevante.

No registrar prompts triviales, correcciones menores, pruebas exploratorias sin decisión o errores temporales sin impacto.

## Formato

```markdown
## YYYY-MM-DD — <título breve>

- Tipo: decisión | especificación | implementación | validación | baseline | riesgo
- Contexto:
- Entrada usada:
- Resultado:
- Decisión tomada:
- Ficheros afectados:
- Pendientes:
```

## Entradas

### 2026-07-10 — Creación de baseline técnico para agentes IA

- Tipo: baseline
- Contexto: consolidación de instrucciones para Copilot/agentes IA en proyecto Java + Spring Boot + arquitectura hexagonal.
- Entrada usada: `AGENTS.md`, `README.md`, `copilot-instructions.md`, `docs/technical-specification.md`, `docs/sdd-specification.md`, `docs/coding-standards.md`.
- Resultado: baseline reorganizado en ficheros con responsabilidades separadas.
- Decisión tomada: usar `AGENTS.md` como contrato principal de agentes, `.github/copilot-instructions.md` como instrucción global corta, `.github/instructions` para reglas path-specific y `/docs` para baseline estable.
- Ficheros afectados: ver `/docs/00-baseline-index.md`.
- Pendientes: revisar con el equipo si se desea añadir workflows CI/CD o ADRs adicionales.
```
