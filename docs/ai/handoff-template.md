# Plantilla obligatoria de handoff técnico por User Story o tarea

## Uso obligatorio

Al finalizar la implementación de cualquier User Story o tarea, el agente de IA debe generar un fichero de handoff técnico usando esta plantilla.

## Objetivo

Dejar contexto compacto, verificable y reutilizable para que futuros agentes puedan entender:

- qué se ha implementado,
- qué archivos y clases se han creado o modificado,
- qué endpoints, contratos, DTOs, mappers, servicios, entidades, migraciones y tests se han tocado,
- qué decisiones técnicas se han tomado,
- qué código debe reutilizarse,
- qué código no debe duplicarse,
- qué riesgos o deuda quedan pendientes.

## Ubicación del handoff generado

```text
docs/ai/handoffs/handoff-[yyyyMMdd]-[feature-kebab-case].md
```

## Handoff técnico - [NOMBRE_DE_LA_FEATURE]

### 1. Metadatos

| Campo | Valor |
|---|---|
| Feature | [NOMBRE_DE_LA_FEATURE] |
| User Story / Work item | [ID O N/A] |
| Fecha | [YYYY-MM-DD] |
| Rama | [BRANCH O N/A] |
| Commit / PR | [COMMIT / PR O N/A] |
| Agente / sesión | [IDENTIFICADOR SI APLICA] |
| Estado | [completado / parcial / bloqueado] |

### 2. Resumen ejecutivo

Máximo 8-10 líneas:

- Propósito funcional.
- Alcance técnico.
- Backend afectado.
- Persistencia afectada, si aplica.
- Tests añadidos o modificados.
- Estado final.

### 3. Alcance implementado

#### Incluido

- [Funcionalidad concreta implementada]

#### No incluido

- [Elemento relacionado pero no implementado]

### 4. Mapa de carpetas afectadas

```text
incident-manager-app/src/main/java/...
incident-manager-app/src/test/java/...
incident-manager-acceptance-test/src/test/...
```

### 5. Archivos creados

| Archivo | Propósito | Reutilizar en futuras US |
|---|---|---|
| [ruta/archivo] | [qué contiene] | [sí/no + motivo] |

Si no hay archivos creados: `No se han creado archivos nuevos.`

### 6. Archivos modificados

| Archivo | Cambio realizado | Motivo |
|---|---|---|
| [ruta/archivo] | [descripción compacta] | [por qué se cambió] |

Si no hay archivos modificados: `No se han modificado archivos existentes.`

### 7. Backend

#### 7.1 Endpoints

| Método | Ruta | Versión | Controller / UseCase | Descripción |
|---|---|---|---|---|
| [GET/POST/PUT/PATCH/DELETE] | [/api/...] | [v1/v2] | [Clase.Método] | [qué hace] |

Si no aplica: `No se han añadido ni modificado endpoints backend.`

#### 7.2 Puertos y servicios de aplicación

| Tipo | Clase | Método relevante | Responsabilidad |
|---|---|---|---|
| Inbound port / Outbound port / Service | [Clase] | [Método] | [responsabilidad] |

#### 7.3 DTOs, mappers y contratos

| Tipo | Archivo | Uso |
|---|---|---|
| Request/Response/Mapper/OpenAPI schema | [ruta] | [uso] |

#### 7.4 Validaciones

| Ubicación | Regla |
|---|---|
| [archivo/clase] | [regla validada] |

#### 7.5 Persistencia

| Elemento | Cambio |
|---|---|
| Entidad JPA | [entidad afectada o N/A] |
| Repository / Adapter | [cambio o N/A] |
| Liquibase | [changeset o N/A] |
| Constraint / índice | [detalle o N/A] |

### 8. Integraciones externas

| Integración | Puerto | Adaptador | Cambio |
|---|---|---|---|
| [ServiceNow/Email/LLM/etc.] | [Port] | [Adapter] | [cambio] |

Si no aplica: `No se han realizado cambios en integraciones externas.`

### 9. Tests

| Tipo | Archivo | Qué valida |
|---|---|---|
| Unit / Slice / Integration / Acceptance | [ruta] | [regla / endpoint / flujo] |

Tests pendientes recomendados:

- [test pendiente o N/A]

### 10. Dependencias y configuración

#### Dependencias nuevas

| Dependencia | Motivo | Dónde se configura |
|---|---|---|
| [paquete] | [justificación] | [pom.xml / otro] |

Si no hay dependencias nuevas: `No se han añadido dependencias nuevas.`

#### Configuración nueva

| Clave / sección | Archivo | Propósito |
|---|---|---|
| [clave] | [archivo] | [uso] |

### 11. Decisiones técnicas tomadas

- [Decisión]: [motivo / trade-off].

### 12. Reutilización obligatoria en futuras US

- [Clase / servicio / método / componente]: reutilizar para [caso].

### 13. Código que NO debe duplicarse

- [Elemento existente]: no duplicar porque [motivo].

### 14. Riesgos, limitaciones y deuda técnica

| Tipo | Descripción | Recomendación |
|---|---|---|
| Riesgo / Limitación / Deuda técnica | [detalle] | [acción sugerida] |

Si no hay riesgos conocidos: `No se han identificado riesgos o deuda técnica relevante en esta implementación.`

### 15. Validación final realizada

- [ ] Build ejecutado correctamente.
- [ ] Tests unitarios ejecutados correctamente.
- [ ] Tests de integración ejecutados correctamente.
- [ ] Tests de aceptación ejecutados correctamente.
- [ ] OpenAPI revisado/regenerado si aplica.
- [ ] Liquibase revisado si aplica.
- [ ] No se ha introducido lógica de negocio en infraestructura.
- [ ] No se ha duplicado código ya existente.

Validaciones no ejecutadas:

- [validación]: [motivo]

### 16. Lectura recomendada para el siguiente agente

- Este handoff.
- `/AGENTS.md`.
- `/docs/00-baseline-index.md`.
- `/docs/06-handoff-process.md`.
- Handoffs relacionados en `/docs/ai/handoffs/`.
- Archivos concretos listados en las secciones 5 y 6.

### 17. Resumen ultra-compacto para contexto IA

Máximo 10 bullets:

- [Qué se implementó].
- [Endpoint/servicio principal].
- [DTOs/mappers principales].
- [Persistencia afectada].
- [Tests añadidos].
- [Qué reutilizar].
- [Qué no duplicar].
- [Riesgo pendiente].

## Reglas de calidad

- Ser concreto y verificable.
- No incluir teoría genérica.
- No repetir la US completa.
- No pegar bloques grandes de código.
- Usar rutas reales.
- Usar nombres reales de clases, métodos y endpoints.
- Indicar explícitamente si una sección no aplica.
- Mantenerse compacto.
- No ocultar limitaciones ni validaciones no ejecutadas.
