# 00 - Metodología de Trabajo: Specification-Driven Development (SDD)

> **Template Genérico** - Adaptable a cualquier proyecto de software

## Índice

- [Objetivo](#objetivo)
- [¿Qué es Specification-Driven Development?](#qué-es-specification-driven-development)
- [Principios Fundamentales](#principios-fundamentales)
- [Flujo de Trabajo Estándar](#flujo-de-trabajo-estándar)
- [Trabajo con IA](#trabajo-con-ia-agentes-y-copilot)
- [Trabajo Manual](#trabajo-manual-desarrollo-tradicional)
- [Reglas de Implementación](#reglas-de-implementación)
- [Control de Calidad](#control-de-calidad)
- [Gestión de Documentación](#gestión-de-documentación)

---

## Objetivo

Este documento establece la metodología de trabajo oficial para **[NOMBRE DEL PROYECTO]** basada en **Specification-Driven Development (SDD)**. Define cómo los desarrolladores deben abordar las tareas, ya sea trabajando con agentes de IA (GitHub Copilot, ChatGPT, Claude) o escribiendo código manualmente.

**CRÍTICO**: Esta especificación es obligatoria para todos los desarrolladores y debe consultarse antes de iniciar cualquier tarea.

---

## ¿Qué es Specification-Driven Development?

**Specification-Driven Development (SDD)** es una metodología de desarrollo donde las especificaciones técnicas son la **fuente de verdad absoluta** y guían todas las decisiones de implementación.

### Características del SDD

1. **Especificaciones Primero** 📝
   - Las especificaciones se escriben ANTES de la implementación
   - El código debe cumplir con las especificaciones, no al revés
   - Cualquier desviación requiere actualizar las especificaciones primero

2. **Documentación como Contrato** 📋
   - Las especificaciones son contratos entre desarrolladores
   - Define comportamientos esperados sin ambigüedad
   - Reduce suposiciones y malentendidos

3. **Validación Continua** ✅
   - Cada implementación se valida contra las especificaciones
   - Las revisiones de código verifican cumplimiento de specs
   - Los tests se escriben basándose en las especificaciones

4. **Evolución Controlada** 🔄
   - Los cambios arquitectónicos se documentan primero
   - Las especificaciones se versionan implícitamente (historial de cambios)
   - La documentación evoluciona con el proyecto

### Beneficios del SDD

- ✅ **Consistencia**: Todo el equipo trabaja con la misma comprensión
- ✅ **Calidad**: El código cumple requisitos desde el diseño
- ✅ **Mantenibilidad**: Nuevos desarrolladores entienden el sistema rápidamente
- ✅ **Trazabilidad**: Decisiones documentadas y justificadas
- ✅ **Trabajo con IA**: Los agentes de IA pueden seguir especificaciones precisas

### SDD vs Otras Metodologías

| Aspecto            | TDD                | BDD                  | **SDD**          |
| ------------------ | ------------------ | -------------------- | ---------------- |
| **Guía principal** | Tests              | Comportamiento       | Especificaciones |
| **Documentación**  | Opcional           | User stories         | Obligatoria      |
| **Validación**     | Tests pasan        | Escenarios OK        | Cumple specs     |
| **Alcance**        | Unidades/Funciones | Features             | Sistema completo |
| **Actualización**  | Refactor tests     | Actualizar scenarios | Actualizar specs |

**En este proyecto**: Combinamos SDD (guía arquitectónica) + TDD (calidad de código)

---

## Principios Fundamentales del SDD

### 1. Specifications First (Las Especificaciones Son Primero)

**Mantra**: "Si no está en las specs, no existe"

- **SIEMPRE** consultar los documentos en `/docs` antes de implementar
- **NUNCA** asumir comportamientos sin verificar las especificaciones
- **NUNCA** desviarse de las especificaciones sin aprobación explícita
- **SIEMPRE** actualizar las especificaciones ANTES de implementar cambios arquitectónicos

```bash
# ❌ Flujo INCORRECTO
1. Implementar funcionalidad
2. Documentar después (tal vez)

# ✅ Flujo CORRECTO (SDD)
1. Leer/Actualizar especificaciones
2. Validar comprensión
3. Implementar según specs
4. Verificar cumplimiento
```

### 2. Specifications as Contract (Especificaciones como Contrato)

**Mantra**: "El código cumple las specs, no al revés"

- Las especificaciones definen el comportamiento esperado
- El código que no cumple las specs está incorrecto, aunque funcione
- Los tests validan que el código cumple las specs
- Las code reviews verifican cumplimiento de especificaciones

### 3. Quality over Speed (Calidad sobre Velocidad)

**Mantra**: "Correcto primero, rápido después"

- El código debe ser correcto según las especificaciones
- Validar cumplimiento de specs antes de continuar
- Escribir tests basados en las especificaciones
- Refactorizar manteniendo conformidad con specs

### 4. Documentation is Code (La Documentación es Código)

**Mantra**: "Código sin specs = código no mantenible"

- La documentación debe reflejar la realidad del código
- Actualizar especificaciones es parte del desarrollo, no opcional
- Documentar decisiones arquitectónicas importantes
- Mantener ejemplos sincronizados con el código

### 5. Incremental and Validated (Incremental y Validado)

**Mantra**: "Pequeños pasos, validación continua"

- Dividir tareas grandes en subtareas manejables
- Validar cada incremento contra especificaciones
- Hacer commits frecuentes con mensajes descriptivos
- No acumular cambios masivos sin probar

---

## Flujo de Trabajo Estándar (SDD)

El flujo de trabajo SDD garantiza que cada línea de código esté alineada con las especificaciones del proyecto.

### Fase 1: Preparación - Leer y Comprender Especificaciones (OBLIGATORIA)

**Objetivo**: Entender completamente QUÉ se debe hacer según las especificaciones

**Para CUALQUIER tarea, SIEMPRE seguir estos pasos:**

#### 1.1 Identificar Especificaciones Relevantes

```bash
# Revisar la lista de especificaciones
ls -la docs/

# Identificar cuáles son relevantes para tu tarea
# Ejemplo: Para crear un nuevo módulo/componente
# - 02-architecture.md (arquitectura del sistema)
# - 07-project-structure-*.md (estructura de archivos)
# - 06-data-models.md (si requiere base de datos - backend)
```

#### 1.2 Leer las Especificaciones Completas

- **NO escanear rápidamente** - leer con atención
- **Tomar notas** de los requisitos clave
- **Identificar dependencias** con otros módulos/componentes
- **Verificar restricciones** y reglas obligatorias

#### 1.3 Crear Plan de Implementación (Basado en Specs)

**Plantilla obligatoria:**

```markdown
## Plan de Implementación SDD

**Tarea**: [Descripción breve]

**Especificaciones consultadas** (con secciones específicas):

- [ ] 00-metodologia-trabajo.md (workflow SDD)
- [ ] 02-architecture.md (secciones X, Y)
- [ ] 07-project-structure-*.md (estructura de módulos/componentes)
- [ ] [Otros documentos relevantes]

**Cumplimiento de especificaciones**:

- [ ] ✅ Sigue los patrones arquitectónicos definidos
- [ ] ✅ Usa las convenciones de nombres establecidas
- [ ] ✅ Implementa las interfaces/contratos especificadas
- [ ] ✅ Cumple requisitos de calidad (tests, coverage)

**Archivos a crear/modificar**:

- [ ] [Lista de archivos]

**Dependencias**:

- [ ] [Lista de módulos/componentes dependientes]

**Tests requeridos** (basados en specs):

- [ ] Unit tests (coverage >= [DEFINIR]%)
- [ ] Integration tests (si aplica)
- [ ] E2E tests (si aplica)

**Validación contra especificaciones**:

- [ ] Verificar cada paso cumple con specs antes de continuar
- [ ] Actualizar specs si se descubren ambigüedades

**Pasos**:

1. Leer specs completas relacionadas
2. [Pasos específicos según tipo de proyecto]
```

#### 1.4 Validación de Comprensión (SDD)

**Antes de implementar, verificar:**

- [ ] ¿Entiendo completamente las especificaciones relevantes?
- [ ] ¿Hay contradicciones o ambigüedades en las specs?
- [ ] ¿Mi plan cumple con TODAS las especificaciones?
- [ ] ¿Necesito actualizar alguna especificación antes de empezar?

**Si hay dudas o ambigüedades**: Preguntar al equipo o actualizar las specs primero.

---

### Fase 2: Implementación - Código que Cumple Especificaciones

**Objetivo**: Implementar código que cumple al 100% con las especificaciones

#### 2.1 Configurar Entorno

```bash
# Asegurar dependencias actualizadas
[PACKAGE_MANAGER] install  # npm, pnpm, yarn, etc.

# Asegurarse de estar en rama principal actualizada
git checkout [MAIN_BRANCH]  # main, develop, master
git pull origin [MAIN_BRANCH]

# Crear rama para la tarea
git checkout -b [BRANCH_TYPE]/[BRANCH_NAME]
# Ejemplos:
# git checkout -b feat/nueva-funcionalidad
# git checkout -b fix/nombre-del-bug
# git checkout -b docs/actualizacion-docs

# Verificar que tests existentes pasan
[TEST_COMMAND]  # npm test, pnpm test, etc.
```

#### 2.2 Implementar Incrementalmente (SDD)

**Orden recomendado (adaptar según tipo de proyecto):**

1. **Interfaces/Tipos/Contratos** (según specs)
2. **Estructura base** (archivos vacíos con estructura)
3. **Implementación core** (lógica principal)
4. **Tests** (validación de comportamiento)
5. **Integración** (conectar con otros módulos/componentes)
6. **Documentación** (actualizar si es necesario)

**⚠️ CRÍTICO**: Después de cada paso, validar cumplimiento de especificaciones.

#### 2.3 Validar Cada Incremento Contra Especificaciones

**Después de cada cambio significativo, validar:**

```bash
# 1. Verificar sintaxis y convenciones
[LINT_COMMAND]  # npm run lint, pnpm run lint, etc.
# ✅ ¿Cumple con las convenciones de código?

# 2. Ejecutar tests
[TEST_COMMAND]
# ✅ ¿Los tests validan el comportamiento especificado?

# 3. Verificar que compila/ejecuta
[BUILD_COMMAND]  # npm run build, pnpm run build, etc.
# ✅ ¿No hay errores de compilación/ejecución?

# 4. Revisar contra especificaciones
# ✅ ¿El código implementa lo que dicen las specs?
# ✅ ¿Sigue todos los patterns especificados?
# ✅ ¿No hay desviaciones sin justificar?

# 5. Si TODO cumple, hacer commit atómico
git add .
git commit -m "[TYPE]([SCOPE]): [DESCRIPTION]"
# Conventional Commits: feat, fix, docs, chore, refactor, test
```

**Checklist de validación por incremento:**

- [ ] ✅ Código cumple especificaciones relevantes
- [ ] ✅ Lint/formato pasa sin errores
- [ ] ✅ Tests pasan y validan specs
- [ ] ✅ Build/compilación exitosa
- [ ] ✅ No hay desviaciones de specs sin documentar

**Si algo no cumple especificaciones:**

1. Corregir el código (no las specs)
2. O actualizar specs primero si hay error en ellas
3. Nunca asumir "está bien aunque no cumpla las specs"

#### 2.4 Flujo de Trabajo con Git

**Modelo de Branching**: [DEFINIR: Git Flow, GitHub Flow, etc.]

##### Estructura de Ramas

- **`[MAIN_BRANCH]`**: Rama principal (main, master, develop)
- **`feat/*`**: Nuevas funcionalidades
- **`fix/*`**: Correcciones de bugs
- **`docs/*`**: Cambios en documentación
- **`chore/*`**: Mantenimiento
- **`hotfix/*`**: Correcciones urgentes

##### Flujo Estándar

```bash
# 1. Actualizar rama principal
git checkout [MAIN_BRANCH]
git pull origin [MAIN_BRANCH]

# 2. Crear rama de trabajo
git checkout -b [TYPE]/[NAME]

# 3. Implementar (con commits frecuentes)
# [Hacer cambios]
git add .
git commit -m "[TYPE]([SCOPE]): [DESCRIPTION]"

# 4. Mantener rama actualizada (si es largo plazo)
git fetch origin [MAIN_BRANCH]
git rebase origin/[MAIN_BRANCH]

# 5. Push de la rama
git push origin [TYPE]/[NAME]

# 6. Crear Pull Request
# [En plataforma: GitHub, GitLab, etc.]
```

##### Conventional Commits

**Formato**: `<type>(<scope>): <subject>`

**Types**:

- `feat`: Nueva funcionalidad
- `fix`: Corrección de bug
- `docs`: Cambios en documentación
- `style`: Formato (no afecta código)
- `refactor`: Refactorización de código
- `test`: Agregar o modificar tests
- `chore`: Mantenimiento (deps, configs)

**Ejemplos**:

```bash
feat(auth): add JWT authentication
fix(api): resolve null pointer in user service
docs(readme): update installation instructions
chore(deps): upgrade dependencies to latest
```

---

### Fase 3: Validación Final - Verificar Cumplimiento Completo

**Objetivo**: Garantizar que el código cumple TODAS las especificaciones

#### 3.1 Checklist de Código

**Antes de crear Pull Request, verificar:**

- [ ] ✅ Sigue convenciones de nombres de archivos
- [ ] ✅ Usa patrones arquitectónicos especificados
- [ ] ✅ Implementa manejo de errores según specs
- [ ] ✅ Incluye logging apropiado
- [ ] ✅ No hay código comentado sin justificación
- [ ] ✅ No hay console.log o debugging code
- [ ] ✅ Imports organizados según convenciones
- [ ] ✅ Código documentado apropiadamente

#### 3.2 Checklist de Tests

**Validar calidad de tests:**

- [ ] ✅ Unit tests escritos para nueva funcionalidad
- [ ] ✅ Coverage >= [DEFINIR]% (configurar umbral mínimo)
- [ ] ✅ Tests usan mocks apropiadamente
- [ ] ✅ Assertions claras y específicas
- [ ] ✅ Tests validan comportamiento especificado
- [ ] ✅ Edge cases cubiertos
- [ ] ✅ Tests pasan consistentemente

#### 3.3 Checklist de Documentación

**Actualizar documentación si es necesario:**

- [ ] ✅ Specs actualizadas si hubo cambios arquitectónicos
- [ ] ✅ Comentarios en código para lógica compleja
- [ ] ✅ README actualizado si afecta setup
- [ ] ✅ Ejemplos de uso incluidos (si aplica)
- [ ] ✅ API documentation actualizada (si aplica)

#### 3.4 Checklist de Progreso

**Actualizar tracking de progreso:**

- [ ] ✅ Actualizar `docs/tracking/00-progress-overview.md` con features completados
- [ ] ✅ Documentar bugs resueltos en `docs/tracking/03-issues-log.md`
- [ ] ✅ Registrar decisiones arquitectónicas en `docs/tracking/04-decisions-log.md`
- [ ] ✅ Marcar fechas de implementación para tracking temporal

#### 3.5 Suite Completa de Validación

```bash
# Ejecutar suite completa antes de PR
[LINT_COMMAND]           # Verificar convenciones
[TEST_COMMAND]           # Ejecutar todos los tests
[TEST_COVERAGE_COMMAND]  # Verificar coverage
[BUILD_COMMAND]          # Verificar compilación/build

# Si TODO pasa, hacer push y crear PR
git push origin [BRANCH_NAME]
```

---

## Trabajo con IA (Agentes y Copilot)

**SDD es ideal para trabajar con IA** porque las especificaciones proporcionan contexto claro y preciso.

### Ventajas de SDD + IA

1. **Especificaciones claras** → IA genera código correcto desde el inicio
2. **Validación automática** → Fácil verificar que el código cumple specs
3. **Contexto completo** → IA entiende arquitectura y decisiones
4. **Menos iteraciones** → Menos correcciones necesarias
5. **Onboarding rápido** → IA puede "leer" todas las specs y entender el proyecto

### Guía de Uso con IA

#### 1. Proporcionar Contexto de Especificaciones

**Template de prompt para IA:**

```markdown
Contexto: Estoy trabajando en [NOMBRE_PROYECTO] siguiendo SDD.

Especificaciones:
- docs/01-requirements.md: [Requisito específico]
- docs/02-architecture.md: [Decisión arquitectónica]
- docs/07-project-structure-*.md: [Patrón de organización]

Tarea: [Descripción de la tarea]

Requisitos:
1. Leer las especificaciones mencionadas
2. Implementar según el patrón definido
3. Incluir tests [según umbral de coverage]
4. Validar cumplimiento de specs
5. Usar [LENGUAJE/FRAMEWORK específico]

Restricciones:
- [Lista de restricciones según specs]
```

#### 2. Flujo de Trabajo con IA

```bash
# Fase 1: Preparación
1. Identificar especificaciones relevantes
2. Copiar contenido de specs al prompt de IA
3. Describir tarea específica con contexto completo

# Fase 2: Generación
4. IA genera código basado en especificaciones
5. Revisar código generado contra specs
6. Validar que cumple TODAS las especificaciones

# Fase 3: Validación
7. Ejecutar suite de validación (lint, test, build)
8. Corregir desviaciones si existen
9. Commit solo cuando cumple especificaciones

# Fase 4: Iteración (si es necesario)
10. Si IA no cumplió alguna spec, proporcionar feedback específico
11. Solicitar corrección referenciando la especificación exacta
12. Repetir validación
```

#### 3. Revisión de Código Generado por IA

**CRÍTICO**: Nunca confiar ciegamente en código generado por IA.

**Checklist de revisión:**

- [ ] ✅ Código cumple especificaciones mencionadas
- [ ] ✅ Sigue convenciones del proyecto
- [ ] ✅ No introduce antipatrones
- [ ] ✅ Tests validan comportamiento correcto
- [ ] ✅ Maneja errores apropiadamente
- [ ] ✅ No tiene dependencias innecesarias
- [ ] ✅ Performance aceptable

#### 4. Mejores Prácticas con IA

**DO ✅**:

- Proporcionar especificaciones completas en el prompt
- Referenciar secciones específicas de documentos
- Solicitar que siga patrones establecidos
- Pedir que genere tests basados en specs
- Validar cada output contra especificaciones
- Usar IA como asistente, no como decisor

**DON'T ❌**:

- Asumir que IA conoce las especificaciones sin proporcionarlas
- Aceptar código que no cumple especificaciones
- Dejar que IA tome decisiones arquitectónicas sin validar con specs
- Omitir revisión de código generado
- Usar código sin entenderlo

---

## Trabajo Manual (Desarrollo Tradicional)

**Cuando NO usar IA:**

- Decisiones arquitectónicas críticas
- Código de seguridad sensible
- Lógica de negocio compleja
- Optimizaciones de performance
- Cuando prefieres control total

### Flujo Manual con SDD

El flujo es idéntico a trabajar con IA, pero sin el paso de generación:

1. **Leer especificaciones** relevantes
2. **Planificar implementación** basada en specs
3. **Escribir código** cumpliendo especificaciones
4. **Escribir tests** basados en comportamiento especificado
5. **Validar** cada incremento contra specs
6. **Commit frecuente** con mensajes descriptivos
7. **Actualizar documentación** si es necesario

---

## Reglas de Implementación

### Reglas Obligatorias (CRÍTICAS)

1. **NUNCA desviarse de especificaciones sin actualizar docs primero**
2. **SIEMPRE leer specs relevantes antes de implementar**
3. **SIEMPRE validar cumplimiento después de cada incremento**
4. **SIEMPRE escribir tests basados en especificaciones**
5. **SIEMPRE hacer commits frecuentes con mensajes descriptivos**
6. **NUNCA asumir comportamientos no especificados**
7. **NUNCA omitir documentación de cambios arquitectónicos**

### Convenciones de Código

**Adaptar según lenguaje/framework:**

```markdown
# Nombres de Archivos (ejemplo):
- Componentes/Módulos: [CONVENCION_NOMBRE]
- Tests: [CONVENCION_TESTS]
- Tipos/Interfaces: [CONVENCION_TIPOS]

# Organización de Imports:
1. [Tipo de imports externos]
2. [Tipo de imports internos]
3. [Tipo de imports locales]

# Comentarios:
- [LENGUAJE de comentarios: inglés/español]
- JSDoc/docstrings para funciones públicas
- Comentarios inline solo para lógica compleja
```

### Control de Versiones

**Git Workflow**: [DEFINIR según proyecto]

**Branch Naming**:

- `feat/[nombre-descriptivo]`
- `fix/[nombre-descriptivo]`
- `docs/[nombre-descriptivo]`
- `chore/[nombre-descriptivo]`

**Commit Messages**: Conventional Commits obligatorio

---

## Control de Calidad

### Umbrales de Calidad (Configurar según proyecto)

```yaml
Code Coverage: >= [XX]%  # Ejemplo: 80%, 70%, 55%
Lint Errors: 0
Type Errors: 0
Security Vulnerabilities: 0
Performance Budget: [DEFINIR]
```

### Code Review Checklist

**Para revisores de PR:**

- [ ] ✅ Código cumple especificaciones mencionadas en PR description
- [ ] ✅ Tests validan comportamiento especificado
- [ ] ✅ Sigue convenciones del proyecto
- [ ] ✅ No introduce deuda técnica
- [ ] ✅ Documentación actualizada si es necesario
- [ ] ✅ No hay cambios sin justificar
- [ ] ✅ Commits son atómicos y descriptivos

### Definition of Done

**Una tarea se considera completada cuando:**

- [ ] ✅ Cumple TODAS las especificaciones relevantes
- [ ] ✅ Tests escritos y passing
- [ ] ✅ Coverage >= umbral definido
- [ ] ✅ Lint/formato pasa
- [ ] ✅ Build exitoso
- [ ] ✅ Code review aprobado
- [ ] ✅ Documentación actualizada
- [ ] ✅ Tracking actualizado (progress overview, issues log)
- [ ] ✅ Merged a rama principal

---

## Gestión de Documentación

### Organización de `/docs`

```
docs/
├── 00-metodologia-trabajo.md          # Este documento
├── 01-requirements.md                 # Requisitos funcionales/no funcionales
├── 02-architecture.md                 # Decisiones arquitectónicas
├── 07-project-structure-*.md          # Estructura de archivos
├── 08-configuration.md                # Setup y configuración
│
├── api/                               # (Opcional) Documentación de API
│   └── [endpoints-documentation].md
│
├── guides/                            # (Opcional) Guías y tutoriales
│   ├── quick-start-guide.md
│   └── [otras-guias].md
│
└── tracking/                          # Tracking de progreso
    ├── 00-progress-overview.md        # Estado general del proyecto
    ├── 03-issues-log.md               # Log de bugs y resoluciones
    └── 04-decisions-log.md            # Log de decisiones arquitectónicas
```

### Actualización de Documentación

**Cuándo actualizar:**

1. **Cambios arquitectónicos**: Actualizar `02-architecture.md` ANTES de implementar
2. **Nuevos requisitos**: Actualizar `01-requirements.md`
3. **Cambios en estructura**: Actualizar `07-project-structure-*.md`
4. **Features completados**: Actualizar `tracking/00-progress-overview.md`
5. **Bugs resueltos**: Documentar en `tracking/03-issues-log.md`
6. **Decisiones importantes**: Registrar en `tracking/04-decisions-log.md`

**Template para actualización de specs:**

```markdown
## [Fecha] - [Tipo de Cambio]

**Razón**: [Por qué se necesita el cambio]

**Cambios**:
- [Lista de cambios en especificaciones]

**Impacto**:
- [Módulos/componentes afectados]

**Validación**:
- [Cómo verificar que el cambio es correcto]
```

---

## Resumen Ejecutivo

### Mantra de SDD

> "Especificaciones → Código → Validación → Documentación"

### Flujo en 5 Pasos

1. **LEER** especificaciones relevantes
2. **PLANIFICAR** implementación basada en specs
3. **IMPLEMENTAR** código que cumple especificaciones
4. **VALIDAR** contra especificaciones (lint + test + build)
5. **ACTUALIZAR** tracking y documentación si es necesario

### Checklist Diario

**Inicio de día:**

- [ ] ✅ `git pull` para actualizar
- [ ] ✅ Revisar `tracking/00-progress-overview.md`
- [ ] ✅ Identificar tarea del día

**Durante desarrollo:**

- [ ] ✅ Leer especificaciones relevantes
- [ ] ✅ Implementar en pasos pequeños
- [ ] ✅ Validar cada incremento (lint + test + build)
- [ ] ✅ Commit frecuente

**Fin de día:**

- [ ] ✅ Actualizar `tracking/00-progress-overview.md`
- [ ] ✅ Documentar issues en `tracking/03-issues-log.md`
- [ ] ✅ Push de cambios
- [ ] ✅ Crear PR si feature está completo

---

## Apéndice: Adaptación por Tipo de Proyecto

### Backend

Ver: `backend/07-project-structure-backend.md`

- Repository Pattern
- Dependency Injection
- API Documentation
- Database schemas

### Frontend

Ver: `frontend/07-project-structure-frontend.md`

- Component patterns
- State management
- Styling conventions
- Testing strategies

### Monorepo

Ver: `monorepo/07-project-structure-monorepo.md`

- Workspace organization
- Shared libraries
- Dependency management
- Build orchestration

---

**Versión del template**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
