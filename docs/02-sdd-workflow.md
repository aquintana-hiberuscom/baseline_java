# 02 — Spec Driven Development Workflow

## Propósito

Definir el flujo obligatorio para implementar cambios con agentes de IA sin perder control técnico ni trazabilidad.

```text
User Story -> Specification -> Technical Design -> Task Breakdown -> Implementation -> Tests -> Validation -> AI Usage Log / ADR si aplica
```

## 1. User Story primero

Toda feature debe partir de una User Story o requisito equivalente aprobado. Debe incluir rol, objetivo, beneficio, contexto funcional, alcance incluido/excluido, reglas de negocio, criterios de aceptación, supuestos y dudas abiertas.

Formato recomendado:

```text
Como [rol]
quiero [acción/necesidad]
para [beneficio]
```

La US debe pasar INVEST: Independent, Negotiable, Valuable, Estimable, Small y Testable.

## 2. Especificación

Ubicación recomendada:

```text
specs/US-<NNN>-<slug>/specification.md
```

Debe contener referencia a la US origen, intención de negocio, requisitos funcionales, requisitos no funcionales, reglas de negocio, criterios de aceptación, errores esperados, no objetivos y supuestos.

## 3. Diseño técnico

Ubicación recomendada:

```text
specs/US-<NNN>-<slug>/technical-design.md
```

Debe definir agregado afectado, modelo de dominio, puertos de entrada, puertos de salida, servicios de aplicación, adaptadores de entrada/salida, cambios OpenAPI, persistencia, seguridad e impacto en tests.

## 4. Desglose de tareas

Ubicación recomendada:

```text
specs/US-<NNN>-<slug>/tasks.md
```

Orden recomendado: OpenAPI si aplica, dominio, puertos de salida, puertos de entrada, servicios de aplicación, adaptadores de persistencia, adaptadores web, configuración, tests unitarios, integración, aceptación y documentación.

## 5. Implementación

Implementa de dentro hacia fuera. No mezcles refactors grandes con la US si no son necesarios. No introduzcas abstracciones no pedidas por la especificación. Mantén nombres consistentes con negocio.

## 6. Validación

Ubicación recomendada:

```text
specs/US-<NNN>-<slug>/validation.md
```

Debe incluir criterios de aceptación y estado, tests asociados, comandos ejecutados, resultado de build, desviaciones y riesgos pendientes.

## 7. Gestión de cambios

Si aparece una duda o cambio de alcance: no inventes la solución, documenta la duda, propón opciones y actualiza especificación/diseño antes del código.

## 8. Registro de uso de IA

Registra en `/docs/05-ai-usage-log.md` cuando se tome una decisión técnica relevante, se resuelva una ambigüedad, se introduzca una regla reusable o se cambie el baseline.
