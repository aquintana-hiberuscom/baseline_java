---
applyTo: "incident-manager-app/src/main/java/**/*.java,incident-manager-app/src/test/java/**/*.java,incident-manager-acceptance-test/src/test/**/*.java"
---

# Instrucciones específicas para Java, Spring Boot y arquitectura hexagonal

## Dependencias entre capas

- `domain` no importa Spring, JPA, Feign, HTTP ni clases de infraestructura.
- `application` define puertos y servicios de caso de uso.
- `infrastructure` implementa adaptadores y configuración técnica.
- Los controladores dependen de puertos de entrada.
- Los servicios de aplicación dependen de puertos de salida.
- Los adaptadores de salida implementan puertos de salida.

## Paquetes esperados por agregado

```text
<aggregate>/
  domain/
    model/
    exception/
  application/
    port/in/
    port/out/
    service/
  infrastructure/
    adapter/in/web/
      dto/
      mapper/
    adapter/out/persistence/
      entity/
      mapper/
    adapter/out/<external-system>/
    config/
```

## Reglas de implementación

- Usa constructor injection. No uses field injection.
- Usa `@RequiredArgsConstructor` cuando aplique.
- Usa `@Transactional` preferentemente en servicios de aplicación cuando el caso de uso lo requiera.
- No devuelvas entidades JPA desde controladores.
- No coloques DTOs en dominio.
- No coloques lógica de negocio en controladores, mappers ni repositorios.
- Usa nombres de responsabilidad: `CreateXUseCase`, `XRepositoryPort`, `XService`, `XController`, `XJpaEntity`, `XWebMapper`.

## MapStruct

- Usa `@Mapper(componentModel = "spring")`.
- Los mappers viven junto al adaptador que los necesita, pero nunca dentro de `dto`.
- Añade tests exhaustivos de mapeo campo a campo.

## Tests

- Dominio: JUnit 5 + AssertJ, sin Spring.
- Aplicación: JUnit 5 + Mockito, sin Spring.
- Web: `@WebMvcTest` cuando aplique.
- Persistencia: `@DataJpaTest` o Testcontainers si procede.
- Aceptación: Cucumber en `incident-manager-acceptance-test`.
