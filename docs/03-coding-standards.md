# 03 — Coding Standards

## Propósito

Definir reglas de implementación del día a día. Complementa el baseline técnico sin duplicar arquitectura extensa.

## Principios generales

- Claridad sobre cleverness.
- Nombres explícitos y orientados a responsabilidad.
- Métodos pequeños y legibles.
- Sin lógica de negocio en infraestructura.
- Sin dependencias de framework en dominio.
- Sin código muerto o abstracciones innecesarias.

## Naming

| Elemento | Patrón |
|---|---|
| Puerto de entrada | `CreateIncidentUseCase`, `ListProductsUseCase` |
| Puerto de salida | `IncidentRepositoryPort`, `ProductCatalogPort` |
| Servicio aplicación | `CreateIncidentService`, `ListProductsService` |
| Controlador | `IncidentController`, `ProductController` |
| Entidad JPA | `IncidentJpaEntity`, `ProductJpaEntity` |
| DTO request | `CreateIncidentRequest`, `ProductSearchRequest` |
| DTO response | `IncidentResponse`, `ProductSummaryResponse` |
| Mapper web | `IncidentWebMapper`, `ProductWebMapper` |
| Mapper persistencia | `IncidentPersistenceMapper`, `ProductPersistenceMapper` |

Evitar `Manager`, `Helper`, `Utils`, `CommonService` y `Processor` genérico.

## Inyección de dependencias

Constructor injection obligatoria. Prohibido field injection y `@Autowired` en atributos. Usar `@RequiredArgsConstructor` cuando aplique.

## Lombok

Lombok reduce ruido, no sustituye diseño. Usar `@RequiredArgsConstructor` en servicios/componentes/controladores, `@Slf4j` para logging y evitar `@Data` en JPA entities con relaciones complejas.

## MapStruct

- Usar `@Mapper(componentModel = "spring")`.
- Mappers cerca del adaptador que los usa.
- Nunca dentro de `dto`.
- Usar mappings explícitos si nombres difieren.
- Añadir test unitario exhaustivo.
- Prohibido `BeanUtils.copyProperties`.

Estructura:

```text
adapter/in/web/
  dto/
  mapper/
adapter/out/persistence/
  entity/
  mapper/
```

## Controllers

Exponen HTTP, validan entrada técnica, delegan a puertos de entrada y devuelven DTOs. No llaman repositorios, Feign ni contienen reglas de negocio.

## Application services

Implementan casos de uso, orquestan dominio y puertos de salida, y son el lugar preferente para transacciones si aplica.

## Persistence

Entidades JPA no salen de infraestructura. Repositorios Spring Data no se inyectan fuera del adaptador. Migraciones con Liquibase.

## Feign e integraciones

Feign solo en infraestructura. Application usa puertos de salida. Traducir errores externos. No propagar modelos externos al dominio.

## Errores

Errores de dominio en dominio, errores de caso de uso en aplicación si no son puramente técnicos y traducción HTTP en infraestructura.

## Logging

No logar secretos, tokens ni datos sensibles. Logar contexto útil para diagnóstico. No usar logs como sustituto de tests.
