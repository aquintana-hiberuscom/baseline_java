# AGENTS.md — Baseline técnico para agentes de IA

> **Ámbito**: este fichero es el contrato principal para cualquier agente de IA que implemente, modifique, revise o valide código en este repositorio.
>
> **Regla principal**: ningún cambio es válido si contradice este fichero o la documentación enlazada en `/docs`.

## 1. Orden de precedencia

Cuando existan varias instrucciones, aplica este orden:

1. Instrucciones explícitas del usuario en la conversación actual.
2. `AGENTS.md` más cercano al directorio donde se va a trabajar.
3. `.github/copilot-instructions.md`.
4. `.github/instructions/*.instructions.md` aplicables al path modificado.
5. Documentos de `/docs`, empezando por `/docs/00-baseline-index.md`.
6. Convenciones existentes en el código.

Si hay conflicto entre documentos, **detente y explica el conflicto antes de implementar**.

## 2. Documentación obligatoria

Antes de escribir código, lee y aplica:

- [`/docs/00-baseline-index.md`](docs/00-baseline-index.md): índice, fuentes de verdad y trazabilidad.
- [`/docs/01-technical-baseline.md`](docs/01-technical-baseline.md): arquitectura, stack, estructura y reglas técnicas no negociables.
- [`/docs/02-sdd-workflow.md`](docs/02-sdd-workflow.md): flujo Spec Driven Development.
- [`/docs/03-coding-standards.md`](docs/03-coding-standards.md): estándares de implementación.
- [`/docs/04-testing-strategy.md`](docs/04-testing-strategy.md): estrategia de pruebas y quality gates.

## 3. Contexto del proyecto

- Proyecto: `incident-manager`.
- Tipo: aplicación Java 21 + Spring Boot 3.2.x.
- Build: Maven multi-módulo.
- Arquitectura: hexagonal por agregados, también conocida como Ports & Adapters.
- Módulos principales:
  - `incident-manager-app`: aplicación backend principal.
  - `incident-manager-acceptance-test`: pruebas de aceptación Cucumber.
- Contrato HTTP: la especificación OpenAPI del módulo de aplicación es fuente de verdad para los endpoints.

## 4. Reglas no negociables

### 4.1 Arquitectura

- Cada agregado debe mantener separación `domain`, `application` e `infrastructure`.
- El dominio no puede importar Spring, JPA, HTTP, Feign ni clases de infraestructura.
- La capa de aplicación define y usa puertos.
- Los controladores REST son adaptadores de entrada y no contienen lógica de negocio.
- Los repositorios, clientes externos y persistencia son adaptadores de salida.
- Las entidades JPA no pueden filtrarse hacia dominio ni aplicación.
- Toda integración externa debe estar detrás de un puerto de salida.

### 4.2 Contrato primero

- Si el cambio afecta a la API HTTP, empieza por OpenAPI.
- No edites código generado manualmente.
- Tras modificar OpenAPI, regenera y adapta implementaciones y tests.

### 4.3 Mappers

- Todos los mappers entre capas deben implementarse con MapStruct.
- Los mappers no deben estar dentro de directorios `dto`.
- Usa directorios hermanos como `mapper` o `mappers` junto a `dto`.
- Todo mapper nuevo o modificado debe tener test unitario exhaustivo campo a campo.
- Está prohibido `BeanUtils.copyProperties`.

### 4.4 Testing

- Ninguna funcionalidad se considera terminada sin tests automatizados.
- Tests de dominio y aplicación no deben arrancar contexto Spring.
- Cada criterio de aceptación debe mapearse al menos a un test o escenario verificable.
- Los tests de aceptación viven en `incident-manager-acceptance-test`.

### 4.5 Git

Permitido sin confirmación adicional:

- `git status`
- `git diff`
- `git log`

Prohibido salvo petición explícita del usuario:

- `git add`
- `git commit`
- `git push`
- `git reset --hard`
- `git rebase`
- `git merge`
- `git stash drop`
- flags `--force` o `--no-verify`

El propietario del repositorio controla commits y pushes.

## 5. Flujo obligatorio antes de implementar una US

Para cualquier User Story, tarea técnica o bug:

1. Localiza la User Story o requisito funcional.
2. Comprueba criterios de aceptación, alcance, no objetivos y dudas abiertas.
3. Si no existe especificación técnica suficiente, genera o actualiza la especificación antes de implementar.
4. Diseña el cambio por capas:
   - dominio,
   - puertos de aplicación,
   - servicios de aplicación,
   - adaptadores de entrada/salida,
   - configuración,
   - tests.
5. Implementa de dentro hacia fuera, respetando dependencias.
6. Añade o actualiza tests.
7. Ejecuta validaciones locales aplicables.
8. Resume cambios, tests ejecutados y cualquier desviación.

## 6. Comandos de validación estándar

Desde la raíz del repositorio:

```bash
mvn clean install
mvn clean compile -pl incident-manager-app
mvn clean test -pl incident-manager-acceptance-test -am
```

Si se modifica OpenAPI:

```bash
mvn clean compile -pl incident-manager-app
mvn clean compile -pl incident-manager-acceptance-test -am
```

## 7. Qué debe devolver el agente al finalizar

Siempre devuelve:

- Resumen de cambios.
- Ficheros modificados.
- Tests añadidos o actualizados.
- Comandos ejecutados y resultado.
- Criterios de aceptación cubiertos.
- Riesgos, dudas o decisiones pendientes.

No ocultes errores. Si algo no se ha podido validar, indícalo explícitamente.
