# Incident Manager

Aplicación Java 21 + Spring Boot para gestionar, sincronizar, clasificar y exponer incidencias mediante API protegida.

## Módulos

```text
incident-manager/
├── incident-manager-app/             # Backend principal
├── incident-manager-acceptance-test/ # Tests de aceptación Cucumber
├── docs/                             # Baseline técnico y documentación de trabajo
├── .github/                          # Instrucciones Copilot, prompts y workflows
└── AGENTS.md                         # Contrato principal para agentes de IA
```

## Baseline técnico para agentes de IA

Este proyecto está preparado para desarrollo asistido por agentes de IA.

Antes de implementar cualquier cambio, un agente debe leer:

- [`AGENTS.md`](AGENTS.md)
- [`docs/00-baseline-index.md`](docs/00-baseline-index.md)
- [`docs/01-technical-baseline.md`](docs/01-technical-baseline.md)
- [`docs/02-sdd-workflow.md`](docs/02-sdd-workflow.md)
- [`docs/03-coding-standards.md`](docs/03-coding-standards.md)
- [`docs/04-testing-strategy.md`](docs/04-testing-strategy.md)

## Stack principal

- Java 21
- Spring Boot 3.2.x
- Maven
- PostgreSQL
- Liquibase
- Spring Security + JWT
- OpenAPI
- MapStruct
- Lombok
- Cucumber
- JUnit 5
- Mockito
- AssertJ

## Arquitectura

El proyecto sigue arquitectura hexagonal por agregados:

```text
<aggregate>/
├── domain/
├── application/
└── infrastructure/
```

Reglas básicas:

- Dominio puro, sin Spring ni JPA.
- Casos de uso definidos mediante puertos de entrada.
- Integraciones y persistencia detrás de puertos de salida.
- Adaptadores en infraestructura.
- OpenAPI como fuente de verdad para contratos HTTP.

## Build y validación

Desde la raíz:

```bash
mvn clean install
```

Compilar aplicación:

```bash
mvn clean compile -pl incident-manager-app
```

Ejecutar aceptación:

```bash
mvn clean test -pl incident-manager-acceptance-test -am
```

Arranque local:

```bash
mvn -pl incident-manager-app spring-boot:run -Dspring-boot.run.profiles=local
```

## Desarrollo local con Docker

```bash
cp .env.example .env
docker compose down
docker compose build app
docker compose up -d postgres mailhog
docker compose up -d app
docker compose logs -f app
```

## Política de Git

El propietario del repositorio controla commits y pushes.

Los agentes de IA no deben ejecutar:

- `git commit`
- `git push`
- `git reset --hard`
- `git rebase`
- `git merge`
- flags `--force` o `--no-verify`

## Documentación relevante

- Baseline: [`docs/00-baseline-index.md`](docs/00-baseline-index.md)
- Arquitectura: [`docs/01-technical-baseline.md`](docs/01-technical-baseline.md)
- SDD: [`docs/02-sdd-workflow.md`](docs/02-sdd-workflow.md)
- Estándares: [`docs/03-coding-standards.md`](docs/03-coding-standards.md)
- Testing: [`docs/04-testing-strategy.md`](docs/04-testing-strategy.md)
- Log de uso IA: [`docs/05-ai-usage-log.md`](docs/05-ai-usage-log.md)
