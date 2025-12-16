# SDD Templates - Specification-Driven Development

## 📋 ¿Qué es SDD Templates?

Este conjunto de templates permite aplicar la metodología **Specification-Driven Development (SDD)** en cualquier tipo de proyecto de software. SDD es una metodología donde las especificaciones técnicas son la **fuente de verdad absoluta** y guían todas las decisiones de implementación.

## 🎯 ¿Para quién es esto?

- **Equipos de desarrollo** que buscan consistencia y calidad
- **Developers individuales** que quieren estructura en sus proyectos
- **Proyectos con IA** (GitHub Copilot, ChatGPT) que necesitan especificaciones claras
- **Proyectos open source** que requieren documentación clara para colaboradores
- **Startups** que necesitan escalar rápidamente con calidad

## 📁 Estructura de Templates

```
sdd-templates/
├── README.md                              # Este archivo / This file
├── 00-getting-started.md                  # Guía de inicio / Getting started guide
├── IMPLEMENTATION-SUMMARY.md              # Resumen consolidado / Consolidated summary
│
├── shared/                                 # Templates base (usar siempre)
│   ├── 00-metodologia-trabajo.md          # SDD methodology
│   ├── 01-requirements.md                 # Requirements template
│   ├── 02-architecture.md                 # Architecture template
│   ├── 08-configuration.md                # Configuration template
│   │
│   └── tracking/
│       ├── 00-progress-overview.md        # Progress tracking
│       ├── 03-issues-log.md               # Bug documentation
│       └── 04-decisions-log.md            # Architecture decisions
│
├── backend/                               # Templates específicos backend
│   ├── 07-project-structure-backend.md    # Directory structure
│   └── 09-api-documentation.md            # API documentation
│
├── frontend/                              # Templates específicos frontend
│   ├── 07-project-structure-frontend.md   # Directory structure
│   └── 10-component-architecture.md       # Component patterns
│
└── monorepo/                              # Templates para monorepos
    ├── 07-project-structure-monorepo.md   # Monorepo structure
    └── 11-workspace-organization.md       # Workspace organization
```

## 🚀 Inicio Rápido

### 1. Elige tu tipo de proyecto

- **Backend** (API, microservicio, servidor): `backend/`
- **Frontend** (web app, mobile app): `frontend/`
- **Monorepo** (fullstack, múltiples apps): `monorepo/`

### 2. Copia los templates necesarios

```bash
# Para proyecto backend (ejemplo NestJS)
mkdir -p my-project/docs
cp sdd-templates/shared/* my-project/docs/
cp sdd-templates/backend/07-project-structure-backend.md my-project/docs/
cp sdd-templates/backend/09-api-documentation.md my-project/docs/

# Para proyecto frontend (ejemplo React)
mkdir -p my-project/docs
cp sdd-templates/shared/* my-project/docs/
cp sdd-templates/frontend/07-project-structure-frontend.md my-project/docs/
cp sdd-templates/frontend/10-component-architecture.md my-project/docs/

# Para monorepo (ejemplo Nx)
mkdir -p my-project/docs
cp sdd-templates/shared/* my-project/docs/
cp sdd-templates/monorepo/07-project-structure-monorepo.md my-project/docs/
cp sdd-templates/monorepo/11-workspace-organization.md my-project/docs/
```

### 3. Personaliza los templates

1. Abre `docs/01-requirements.md` y define tus requisitos
2. Abre `docs/02-architecture.md` y diseña tu arquitectura
3. Abre `docs/07-project-structure-*.md` y adapta la estructura a tu proyecto
4. Lee `docs/00-metodologia-trabajo.md` para entender el flujo de trabajo

### 4. Aplica la metodología

Sigue el flujo SDD en cada tarea:

1. **Leer especificaciones** relevantes
2. **Comprender** los requisitos
3. **Implementar** según specs
4. **Validar** cumplimiento
5. **Actualizar** documentación si es necesario

## � Documentos de Referencia / Reference Documents

### `IMPLEMENTATION-SUMMARY.md` - Resumen Consolidado / Consolidated Summary

**Propósito**: Visión general completa de todos los 16 templates  
**Cuándo leer**: Cuando quieras entender qué templates existen y qué cubren  
**Contiene**:

- Inventario de 16 templates con detalles
- Estadísticas de contenido (8,000+ líneas, 120+ ejemplos)
- Matrices de cobertura (por tipo de proyecto y aspecto)
- Frameworks y tecnologías soportadas
- Ruta de aprendizaje estructurada
- Sistema de placeholders para personalización

### `CONSOLIDATION-SUMMARY.md` - Historial de Integración / Integration History

**Propósito**: Documento de control de cambios  
**Contiene**:

- Archivos consolidados y proceso
- Mejoras implementadas
- Checklist de validación
- Notas de mantenimiento

---

## 📖 Documentos Core (Siempre necesarios) / Core Documents (Always Required)

### 1. `00-metodologia-trabajo.md` ⭐ MÁS IMPORTANTE / MOST IMPORTANT

**Propósito**: Define cómo trabajar con SDD  
**Cuándo usar**: SIEMPRE - antes de cualquier tarea  
**Contiene**:

- Principios fundamentales de SDD
- Flujo de trabajo estándar
- Trabajo con IA vs trabajo manual
- Reglas de implementación
- Control de calidad

### 2. `01-requirements.md`

**Propósito**: Requisitos funcionales y no funcionales  
**Cuándo usar**: Al iniciar proyecto y durante planificación  
**Contiene**:

- RF (Requisitos Funcionales)
- RNF (Requisitos No Funcionales)
- Casos de uso
- Criterios de aceptación

### 3. `02-architecture.md`

**Propósito**: Diseño arquitectónico del sistema  
**Cuándo usar**: Al diseñar o modificar arquitectura  
**Contiene**:

- Decisiones arquitectónicas
- Patrones de diseño
- Diagrama de componentes
- Stack tecnológico

### 4. `07-project-structure-*.md`

**Propósito**: Organización de archivos y convenciones  
**Cuándo usar**: Al crear nuevos módulos/componentes  
**Contiene**:

- Estructura de directorios esperada
- Convenciones de nombres
- Organización de código
- Ejemplos prácticos

### 5. `08-configuration.md`

**Propósito**: Configuración del proyecto  
**Cuándo usar**: Al configurar entornos  
**Contiene**:

- Variables de entorno
- Archivos de configuración
- Setup para desarrollo/producción

## 🔧 Templates por Tipo de Proyecto

### Backend (API, Microservicio, Servidor)

**Tecnologías soportadas**: NestJS, Express, Fastify, FastAPI, Django, Spring Boot

**Templates incluidos**:

- ✅ `07-project-structure-backend.md` - Estructura modular para backend
- ✅ `09-api-documentation.md` - Documentación de endpoints (OpenAPI/Swagger)
- ✅ Ejemplos de estructura para frameworks populares

**Características**:

- Arquitectura en capas (controller/service/repository)
- Documentación de API REST/GraphQL
- Manejo de errores y excepciones
- Validación de datos
- Testing (unit/integration/e2e)

### Frontend (Web App, Mobile App)

**Tecnologías soportadas**: React, Vue, Angular, Next.js, Svelte, React Native

**Templates incluidos**:

- ✅ `07-project-structure-frontend.md` - Estructura de componentes
- ✅ `10-component-architecture.md` - Patrones de componentes
- ✅ Ejemplos para diferentes frameworks

**Características**:

- Organización de componentes
- Gestión de estado
- Routing y navegación
- Estilos y theming
- Testing de componentes

### Monorepo (Fullstack, Múltiples Apps)

**Tecnologías soportadas**: Nx, Turborepo, Lerna, pnpm workspaces

**Templates incluidos**:

- ✅ `07-project-structure-monorepo.md` - Organización de workspaces
- ✅ `11-workspace-organization.md` - Gestión de dependencias compartidas
- ✅ Ejemplos para diferentes herramientas

**Características**:

- Workspace compartidos
- Librerías compartidas
- Scripts compartidos
- Build optimizado
- Versionado coordinado

## 🎓 Conceptos Clave de SDD

### 1. Specifications First (Especificaciones Primero)

- Las especificaciones se escriben ANTES del código
- El código debe cumplir las especificaciones
- Cualquier desviación requiere actualizar las specs primero

### 2. Documentation as Contract (Documentación como Contrato)

- Las especificaciones definen el comportamiento esperado
- El código que no cumple las specs está incorrecto
- Las code reviews verifican cumplimiento de especificaciones

### 3. Quality over Speed (Calidad sobre Velocidad)

- Correcto primero, rápido después
- Validar cumplimiento antes de continuar
- No acumular deuda técnica

### 4. Incremental and Validated (Incremental y Validado)

- Pequeños pasos con validación continua
- Commits frecuentes
- Testing continuo

## 🤖 Trabajo con IA (GitHub Copilot, ChatGPT, Claude)

SDD es **ideal para trabajar con IA** porque:

1. **Especificaciones claras** → IA genera código correcto
2. **Validación automática** → Verificar que el código cumple specs
3. **Contexto completo** → IA entiende el proyecto completo
4. **Menos correcciones** → Menos iteraciones necesarias

### Prompt Example para IA

```markdown
Contexto: Estoy trabajando en un proyecto backend NestJS siguiendo SDD.

Especificaciones:

- docs/01-requirements.md: RF-003 - Autenticación JWT
- docs/02-architecture.md: Sección "Auth Module"
- docs/07-project-structure-backend.md: Patrón de módulos

Tarea: Implementar módulo de autenticación según especificaciones.

Requisitos:

1. Leer las especificaciones mencionadas
2. Implementar según el patrón definido
3. Incluir tests unitarios
4. Validar cumplimiento de specs
```

## 📋 Checklist de Implementación

Antes de considerar una tarea completa:

- [ ] ✅ Leí las especificaciones relevantes
- [ ] ✅ Entendí los requisitos completamente
- [ ] ✅ El código cumple las especificaciones
- [ ] ✅ Escribí tests basados en las specs
- [ ] ✅ Los tests pasan (coverage >= 55%)
- [ ] ✅ El código sigue las convenciones del proyecto
- [ ] ✅ Actualicé documentación si fue necesario
- [ ] ✅ Hice commit con mensaje descriptivo
- [ ] ✅ El build pasa sin errores

## 🔄 Flujo de Trabajo Diario

### Inicio de Día

1. `git pull` para obtener últimos cambios
2. Revisar `docs/tracking/00-progress-overview.md`
3. Identificar tarea del día

### Durante el Desarrollo

1. Leer especificaciones relevantes
2. Implementar en pasos pequeños
3. Validar cada incremento (lint + test + build)
4. Commit frecuente

### Fin de Día

1. Actualizar `docs/tracking/00-progress-overview.md`
2. Documentar issues en `docs/tracking/03-issues-log.md`
3. Push de cambios
4. Code review (si aplica)

## 📚 Recursos Adicionales

- **Guía de inicio**: Ver `00-getting-started.md`
- **Ejemplos completos**: Revisar carpetas `examples/` por tecnología
- **Troubleshooting**: Ver `docs/tracking/03-issues-log.md`
- **Decisiones arquitectónicas**: Ver `docs/tracking/04-decisions-log.md`

## 🔌 Integraciones y Guías Especializadas / Integrations & Specialized Guides

### Jira Integration Guide

**Para proyectos usando Jira + Dual Track:**

📖 **Guía Completa**: [guides/jira-integration-guide.md](guides/jira-integration-guide.md)

**Cubre:**

- ✅ Configuración de Jira para SDD
- ✅ Workflows Dual Track (Discovery + Implementation)
- ✅ Mejores prácticas para múltiples desarrolladores
- ✅ Gestión de restricciones y limitaciones
- ✅ Ejemplo de configuración completa
- ✅ Checklist de implementación

**Ideal para:**

- Equipos > 5 personas
- Proyectos con stakeholders múltiples
- Necesidad de traceabilidad completa
- Distribución geográfica del equipo
- Proyectos > 3 meses

---

## 🤝 Contribuciones

¿Quieres mejorar estos templates?

1. Fork el repositorio
2. Crea tu rama: `git checkout -b feat/mejora-template`
3. Sigue SDD para tus cambios
4. Abre un Pull Request

## 📝 Licencia

Estos templates son de código abierto y pueden usarse libremente en proyectos personales o comerciales.

---

**Creado con ❤️ usando Specification-Driven Development**
