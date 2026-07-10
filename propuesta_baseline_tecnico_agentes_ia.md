# Propuesta de baseline técnico para agentes IA

Incluye la estructura recomendada y el contenido optimizado para un proyecto Java + Spring Boot + arquitectura hexagonal.

## Ficheros incluidos

- `.github/copilot-instructions.md`
- `.github/instructions/java.instructions.md`
- `.github/prompts/implement-user-story.prompt.md`
- `AGENTS.md`
- `README.md`
- `docs/00-baseline-index.md`
- `docs/01-technical-baseline.md`
- `docs/02-sdd-workflow.md`
- `docs/03-coding-standards.md`
- `docs/04-testing-strategy.md`
- `docs/05-ai-usage-log.md`
- `docs/adr/0001-baseline-tecnico-agentes-ia.md`


## 1. AGENTS queda como contrato operativo del agente
Lo he dejado como el fichero que responde a:

qué debe leer el agente,
qué reglas no puede saltarse,
en qué orden aplicar instrucciones,
qué comandos puede ejecutar,
qué operaciones Git tiene prohibidas,
cómo debe terminar y reportar una tarea.



##  2. .github/copilot-instructions.md queda corto y estable

Actúa como una entrada global para Copilot:

resume el baseline,
enlaza a AGENTS,
enlaza a /docs,
evita duplicar todo el contenido.

Esto es importante porque Copilot puede usar ese fichero como contexto global de repositorio. [eu-prod.as...rosoft.com]

##  3. Añado .github/instructions/java.instructions.md
Este fichero es específico para código Java/Spring/hexagonal. Es decir, cuando el agente trabaje sobre código Java, tiene reglas más concretas:

estructura por agregado,
dependencias entre capas,
mappers,
testing,
ubicación de DTOs,
uso de puertos,
reglas de controladores y servicios.

Esta separación evita que el baseline global tenga demasiada granularidad.
## 4. Añado .github/prompts/implement-user-story.prompt.md
Esto es muy útil para tu caso real: tienes una US completa como la que generamos y quieres que Copilot la implemente bien.
Ese prompt reutilizable le fuerza a:

leer el baseline,
detectar impacto,
diseñar por capas,
implementar siguiendo arquitectura,
añadir tests,
reportar criterios cubiertos.

No es obligatorio, pero para tu forma de trabajar con US + agentes es muy práctico.
## 5. README queda como onboarding humano
He reducido la responsabilidad del README:

qué es el proyecto,
módulos,
stack,
comandos básicos,
enlaces al baseline.

El README no debería ser el sitio donde el agente tenga que buscar todas las reglas finas.
##  6. /docs queda dividido por responsabilidad
He separado los documentos así:




Fichero							Responsabilidad
/docs/00-baseline-index.md				Mapa de documentos, orden de lectura y fuentes de verdad.
/docs/01-technical-baseline.md				Arquitectura, stack, estructura, OpenAPI, seguridad, persistencia.
/docs/02-sdd-workflow.md				Flujo User Story → spec → diseño → tasks → tests → validación.
/docs/03-coding-standards.md				Naming, MapStruct, Lombok, controllers, services, logging.
/docs/04-testing-strategy.md				Qué test corresponde a cada capa y quality gates.
/docs/05-ai-usage-log.md				Trazabilidad del uso de IA y decisiones.
/docs/adr/0001-baseline-tecnico-agentes-ia.md		Decisión formal de arquitectura documental.



Mi recomendación final de baseline
Para proyectos con agentes IA, yo usaría esta regla:

AGENTS.md gobierna el comportamiento del agente. 
.github/copilot-instructions.md activa el contexto global de Copilot. 
/docs contiene las reglas técnicas mantenibles. 
.github/prompts contiene workflows reutilizables.

Esa combinación es más robusta que tener un único AGENTS.md gigante.