# 01 — Technical Baseline

## Propósito

Define la arquitectura técnica objetivo y las reglas no negociables de implementación para `incident-manager`.

## Stack técnico

| Categoría | Decisión |
|---|---|
| Lenguaje | Java 21 |
| Framework | Spring Boot 3.2.x |
| Build | Maven multi-módulo |
| Arquitectura | Hexagonal por agregados |
| Persistencia | Spring Data JPA + Hibernate |
| Base de datos | PostgreSQL |
| Migraciones | Liquibase |
| Seguridad | Spring Security + JWT |
| Contrato HTTP | OpenAPI |
| Mapping | MapStruct |
| Boilerplate | Lombok |
| Tests unitarios | JUnit 5, AssertJ, Mockito |
| Tests aceptación | Cucumber |

## Estructura de módulos

```text
incident-manager/
├── incident-manager-app/
├── incident-manager-acceptance-test/
├── docs/
├── .github/
└── AGENTS.md
```

## Estructura por agregado

```text
<aggregate>/
├── domain/
│   ├── model/
│   ├── valueobject/
│   └── exception/
├── application/
│   ├── port/in/
│   ├── port/out/
│   └── service/
└── infrastructure/
    ├── adapter/in/web/
    │   ├── dto/
    │   └── mapper/
    ├── adapter/out/persistence/
    │   ├── entity/
    │   ├── mapper/
    │   └── repository/
    ├── adapter/out/<external-system>/
    └── config/
```

## Regla de dependencias

Permitido:

```text
infrastructure -> application -> domain
```

Prohibido:

```text
domain -> application
domain -> infrastructure
application -> infrastructure
```

## Responsabilidad de cada capa

### Domain

Contiene entidades de dominio, value objects, reglas de negocio puras y excepciones de dominio. No contiene Spring, JPA, DTOs HTTP, entidades JPA, Feign ni serialización.

### Application

Contiene puertos de entrada, puertos de salida, servicios de aplicación y orquestación de casos de uso. Los servicios implementan puertos de entrada y dependen de puertos de salida.

### Infrastructure

Contiene controladores REST, DTOs, mappers web, adaptadores de persistencia, entidades JPA, repositorios, clientes externos, configuración y handlers técnicos. Traduce entre modelos técnicos y dominio. No contiene lógica de negocio.

## OpenAPI

OpenAPI es fuente de verdad para contratos HTTP. Si una US cambia endpoints, parámetros, respuestas, errores o seguridad: modifica OpenAPI primero, regenera código, adapta controladores/DTOs y actualiza tests.

## Persistencia

- Entidades JPA solo en infraestructura.
- Repositorios Spring Data solo en infraestructura.
- Dominio no conoce JPA.
- Identificadores estándar UUID salvo justificación documentada.
- Cambios de esquema con Liquibase.

## Seguridad

- Rutas no públicas protegidas con Spring Security.
- JWT cuando aplique.
- Scopes, roles y reglas de autorización reflejados en OpenAPI y tests.
- No hardcodear secretos.

## Integraciones externas

- Toda integración externa detrás de un puerto de salida.
- Feign u otro cliente HTTP solo en infraestructura.
- Los errores externos se traducen a errores de aplicación o dominio controlados.

## Definition of Done técnica

Una feature está terminada cuando respeta arquitectura hexagonal, cubre criterios de aceptación con tests, no introduce dependencias prohibidas, actualiza OpenAPI si afecta al contrato, añade migraciones si cambia persistencia, mantiene mappers con MapStruct y tests, ejecuta validaciones locales y documenta decisiones relevantes si aplica.
