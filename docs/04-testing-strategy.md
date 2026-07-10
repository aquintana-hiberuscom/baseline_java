# 04 — Testing Strategy

## Propósito

Definir qué tipo de test corresponde a cada capa y qué debe validar un agente antes de dar una tarea por terminada.

## Tests por capa

| Capa | Tipo | Herramientas | Contexto Spring |
|---|---|---|---|
| Domain | Unit test | JUnit 5 + AssertJ | No |
| Application | Unit test | JUnit 5 + Mockito + AssertJ | No |
| Web adapter | Slice test | `@WebMvcTest`, MockMvc | Sí, acotado |
| Persistence adapter | Integration test | `@DataJpaTest`, H2/Testcontainers | Sí, acotado |
| Full flow | Integration test | `@SpringBootTest` | Sí |
| Acceptance | Cucumber | Cucumber + JUnit | Sí |

## Reglas generales

- Toda US debe cubrir sus criterios de aceptación.
- Todo bug fix debe añadir o actualizar test siempre que sea viable.
- Dominio y aplicación no deben arrancar Spring.
- Mockear puertos de salida en tests de servicios de aplicación.
- Evitar `@SpringBootTest` por defecto.

## Tests de mappers

Todo mapper debe tener test exhaustivo: verifica cada campo origen/destino, falla si un campo relevante no se comprueba, cubre nulos y transformaciones si aplica, y usa datos representativos.

## Tests de controladores

Validan path, query params, request body, códigos HTTP, serialización/deserialización, errores de validación y seguridad cuando aplique.

## Tests de aplicación

Validan orquestación del caso de uso, reglas de aplicación, interacción con puertos de salida, errores esperados y no dependencia de infraestructura.

## Tests de persistencia

Validan mappings JPA, consultas, filtros, ordenación, paginación, restricciones relevantes y compatibilidad con migraciones si aplica.

## Tests de aceptación

Ubicación:

```text
incident-manager-acceptance-test/src/test/resources/features/
incident-manager-acceptance-test/src/test/java/
```

Escenarios en lenguaje de negocio, alineados con criterios de aceptación.

## Quality gates locales

```bash
mvn clean compile -pl incident-manager-app
mvn test -pl incident-manager-app
mvn clean test -pl incident-manager-acceptance-test -am
mvn clean install
```

Si no se puede ejecutar algún comando, documentarlo en el resumen final.
