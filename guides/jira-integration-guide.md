# Guía de Integración: SDD Templates + Jira (Dual Track)

> **SDD + Jira para Múltiples Desarrolladores** | Agnóstico de Metodología  
> Template genérico para integrar Specification-Driven Development con Jira en proyectos Dual Track

**Versión**: 1.0.0  
**Última actualización**: 16 de diciembre de 2024  
**Autor**: [EQUIPO/PERSONA]  
**Mantenedor**: [RESPONSABLE]

---

## 📋 Tabla de Contenidos

1. [Introducción](#introducción)
2. [Conceptos Clave](#conceptos-clave)
3. [Configuración de Jira](#configuración-de-jira)
4. [Workflow SDD + Dual Track](#workflow-sdd--dual-track)
5. [Mejores Prácticas](#mejores-prácticas)
6. [Múltiples Desarrolladores](#múltiples-desarrolladores)
7. [Restricciones y Limitaciones](#restricciones-y-limitaciones)
8. [Checklist de Implementación](#checklist-de-implementación)

---

## 🎯 Introducción / Introduction

### ¿Por Qué SDD + Jira?

**SDD (Specification-Driven Development)** proporciona:

- ✅ Especificaciones como fuente de verdad
- ✅ Validación continua contra requisitos
- ✅ Documentación sincronizada con código

**Jira** proporciona:

- ✅ Gestión de tareas escalable
- ✅ Tracking de progreso
- ✅ Colaboración entre equipos

**Dual Track** permite:

- ✅ Desarrollo de features en paralelo
- ✅ Separación clara entre exploración e implementación
- ✅ Velocidad en entrega

### Beneficios de Esta Integración

| Beneficio         | Descripción                                          |
| ----------------- | ---------------------------------------------------- |
| **Claridad**      | Especificaciones claras en Jira, vinculadas a código |
| **Trazabilidad**  | Todo requisito tiene ticket asociado                 |
| **Validación**    | PR validadas contra specs en Jira                    |
| **Escalabilidad** | Funciona con 2 o 200 desarrolladores                 |
| **Agnóstico**     | No requiere Scrum, Kanban, etc.                      |

---

## 🔑 Conceptos Clave / Key Concepts

### Dual Track Explicado

```
┌─────────────────────────────────────────┐
│         DUAL TRACK WORKFLOW              │
├─────────────────────────────────────────┤
│                                          │
│  TRACK 1: DISCOVERY/EXPLORATION          │
│  (Análisis, diseño, prototipos)          │
│  ├─ Refinement de requisitos             │
│  ├─ Diseño de arquitectura               │
│  ├─ Pruebas de concepto                  │
│  └─ Documentación de especificaciones    │
│                                          │
│  TRACK 2: DELIVERY/IMPLEMENTATION        │
│  (Codificación, testing, deployment)     │
│  ├─ Implementación de features           │
│  ├─ Testing (unit, integration, e2e)     │
│  ├─ Code review y validación             │
│  └─ Deployment y monitoreo               │
│                                          │
│  INTERSECCIÓN: SDD VALIDATION            │
│  ├─ Código valida specs                  │
│  ├─ Tests validan requisitos             │
│  ├─ Documentación sincronizada           │
│  └─ Trazabilidad completa                │
│                                          │
└─────────────────────────────────────────┘
```

### Mapeo SDD ↔ Jira

| SDD Component      | Jira Equivalent    | Ubicación                 |
| ------------------ | ------------------ | ------------------------- |
| **Especificación** | Epic + Child Tasks | `docs/01-requirements.md` |
| **Arquitectura**   | Design Decision    | `docs/02-architecture.md` |
| **Implementación** | Story + Subtasks   | Story en Jira + Branch    |
| **Validación**     | Definition of Done | Checklist en Story        |
| **Tracking**       | Progress Reports   | `docs/tracking/`          |

---

## ⚙️ Configuración de Jira / Jira Setup

### 1. Estructura de Proyectos

**Opción A: Un Proyecto con Múltiples Epics** (Recomendado)

```
Proyecto: [NOMBRE_PROYECTO]
├─ Epic: Track 1 - Discovery & Specs
│  ├─ Task: Refine Requirements
│  ├─ Task: Design Architecture
│  ├─ Task: Document Specifications
│  └─ Task: Create POC
│
├─ Epic: Track 2 - Implementation
│  ├─ Story: Feature 1
│  │  ├─ Subtask: Code
│  │  ├─ Subtask: Test
│  │  └─ Subtask: Code Review
│  ├─ Story: Feature 2
│  └─ Story: Bug Fix 1
│
└─ Epic: Track 3 - Deployment & Operations
   ├─ Task: Deploy to Staging
   ├─ Task: Production Deployment
   └─ Task: Monitoring Setup
```

**Opción B: Múltiples Proyectos** (Para equipos muy grandes)

```
Proyecto Discovery:  [PROYECTO]-DISC
├─ Tareas de análisis y diseño
└─ Epics por línea de producto

Proyecto Development: [PROYECTO]-DEV
├─ Historias de implementación
├─ Bugs
└─ Mejoras técnicas

Proyecto Operations:  [PROYECTO]-OPS
├─ Deployment
├─ Monitoreo
└─ Incidentes
```

### 2. Campos Personalizados Recomendados

**Field 1: Especificación Vinculada**

```
Type: Link
Description: Enlace al documento SDD relevante
Values:
  - docs/01-requirements.md
  - docs/02-architecture.md
  - docs/07-project-structure-*.md
  - docs/tracking/*
```

**Field 2: Rama Git Asociada**

```
Type: Text
Description: Rama de feature/fix asociada
Format: feat/JIRA-XXX-feature-name
Example: feat/PROJ-123-user-authentication
```

**Field 3: Estado de Cumplimiento SDD**

```
Type: Dropdown
Values:
  - ✅ Especificación Completa (Ready for Dev)
  - 🔄 En Revisión (Under Review)
  - ⚠️ Incompleta (Incomplete)
  - ❌ No Aplica (N/A)
```

**Field 4: Developers Asignados**

```
Type: Multi-User
Description: Todos los devs trabajando en la tarea
Purpose: Facilitar colaboración
```

### 3. Estados Personalizados del Workflow

```
DISCOVERY TRACK:
┌─────────────────────────────────────────┐
│ TODO → IN RESEARCH → IN DESIGN          │
│      → SPEC REVIEW → SPEC APPROVED      │
│      → READY FOR DEV                    │
└─────────────────────────────────────────┘

IMPLEMENTATION TRACK:
┌─────────────────────────────────────────┐
│ BACKLOG → IN PROGRESS                   │
│        → CODE REVIEW → APPROVED         │
│        → TESTING → TESTED               │
│        → READY FOR MERGE                │
└─────────────────────────────────────────┘

POST-IMPLEMENTATION:
┌─────────────────────────────────────────┐
│ MERGED → IN STAGING → STAGING OK        │
│       → IN PRODUCTION → DONE            │
└─────────────────────────────────────────┘
```

### 4. Definition of Done (DoD)

**Para Track 1 (Discovery):**

```
- [ ] Especificación escrita en docs/01-requirements.md
- [ ] Arquitectura documentada en docs/02-architecture.md
- [ ] Aceptado por stakeholders
- [ ] Enlace a especificación en Jira
- [ ] Estimación de esfuerzo realizado
- [ ] Criterios de aceptación claros
- [ ] Dependencias identificadas
```

**Para Track 2 (Implementation):**

```
- [ ] Código valida especificación (SDD compliance)
- [ ] Unit tests > 55% coverage
- [ ] Integration tests pasando
- [ ] Code review aprobado por 2+ devs
- [ ] Sonarqube/linting pasando
- [ ] Documentación actualizada
- [ ] Changelog actualizado
- [ ] Deployment ready
```

**Para Track 3 (Operations):**

```
- [ ] Deployed a staging exitosamente
- [ ] Smoke tests pasando
- [ ] Performance metrics en baseline
- [ ] Monitoring configurado
- [ ] Rollback plan documentado
- [ ] Deployed a producción
- [ ] Health checks OK
```

---

## 🔄 Workflow SDD + Dual Track / Workflow

### Flujo Estándar de Tareas

```
FASE 1: DESCUBRIMIENTO (Track 1)
═════════════════════════════════

1. Crear Epic en Jira
   ├─ Title: Feature X
   ├─ Description: Business value
   └─ Link: /docs/

2. Crear tareas de análisis
   ├─ "Analyze requirements"
   ├─ "Design architecture"
   ├─ "Create specification"
   └─ Status: TODO

3. Trabajar en especificación
   ├─ Leer docs/01-requirements.md
   ├─ Crear rama: analysis/JIRA-XXX-feature-name
   ├─ Documentar requirements
   ├─ Diagramar arquitectura
   └─ Crear PR

4. Review de especificación
   ├─ 2+ stakeholders revisan
   ├─ Feedback → Actualizar docs
   ├─ Approve PR
   └─ Mark as "SPEC APPROVED" en Jira

5. Mark as "READY FOR DEV"
   ├─ Especificación final en docs/
   ├─ Estimación realizada
   ├─ Epic vinculado en Jira
   └─ Asignar a desarrolladores


FASE 2: IMPLEMENTACIÓN (Track 2)
════════════════════════════════

1. Crear Stories desde Epic aprobado
   ├─ Una historia por "chunked" feature
   ├─ Title: "Implement [feature aspect]"
   ├─ Acceptance Criteria: Basado en specs
   └─ Assign: Desarrollador responsable

2. Crear rama de desarrollo
   ├─ Branch: feat/JIRA-XXX-short-description
   ├─ Base: develop
   └─ Link en Jira: "Branch" field

3. Implementar según SDD
   ├─ Leer docs/02-architecture.md
   ├─ Leer docs/07-project-structure-*.md
   ├─ Implementar funcionalidad
   ├─ Escribir tests
   └─ Commit frecuentes

4. Pull Request
   ├─ Title: "JIRA-XXX: Feature description"
   ├─ Description: Link a specs + cambios
   ├─ Checklist de DoD
   └─ Assign: 2+ reviewers

5. Code Review
   ├─ Reviewer 1: Código + tests
   ├─ Reviewer 2: Specs compliance
   ├─ Requested changes: Actualizar
   └─ Approve: Ambos reviewers

6. Merge & Deployment
   ├─ Squash merge to develop
   ├─ Deploy to staging
   ├─ Smoke tests
   └─ Mark in Jira: "READY FOR MERGE"


FASE 3: VALIDACIÓN Y DEPLOYMENT (Track 3)
═══════════════════════════════════════════

1. Test en Staging
   ├─ QA tests all scenarios
   ├─ Performance checks
   ├─ Regression testing
   └─ Approve or back to Track 2

2. Production Deployment
   ├─ Schedule: Off-peak hours
   ├─ Blue-green deployment
   ├─ Rollback plan ready
   └─ Team on standby

3. Post-Deployment
   ├─ Monitoring checks
   ├─ Error rate OK
   ├─ Performance OK
   └─ Mark in Jira: "DONE"

4. Close Epic
   ├─ Retrospective
   ├─ Update docs/tracking/
   ├─ Document lessons learned
   └─ Close Epic
```

---

## 🏆 Mejores Prácticas / Best Practices

### 1. Nomenclatura de Ramas y Commits

```
BRANCHES
────────
Discovery:      analysis/JIRA-XXX-descriptive-name
Feature:        feat/JIRA-XXX-descriptive-name
Bug Fix:        fix/JIRA-XXX-issue-description
Hotfix:         hotfix/JIRA-XXX-critical-issue
Refactor:       refactor/JIRA-XXX-component-name

COMMITS
───────
feat(JIRA-XXX): Add feature description

- List key changes
- Reference specs: docs/02-architecture.md
- Changelog impact

EJEMPLO:
git commit -m "feat(PROJ-123): Implement user authentication

- Add JWT token generation
- Implement refresh token rotation
- Add role-based access control

Spec: docs/02-architecture.md#security
Tests: 85% coverage
"
```

### 2. Vinculación SDD ↔ Jira

**En cada Jira Story, incluir:**

```markdown
## 📋 Especificación Vinculada / Linked Specification

- **Requirements**: [Link a docs/01-requirements.md]
- **Architecture**: [Link a docs/02-architecture.md]
- **Structure**: [Link a docs/07-project-structure-*.md]
- **Tracking**: [Link a docs/tracking/00-progress-overview.md]

## 🎯 Acceptance Criteria (from Specs)

- [ ] Cumple punto 1 de spec
- [ ] Cumple punto 2 de spec
- [ ] Tests cubren casos de uso

## ✅ Definition of Done

- [ ] Código implementado según specs
- [ ] Tests con 55%+ coverage
- [ ] Code review aprobado
- [ ] Documentación actualizada
```

### 3. Estados de Cumplimiento

```
✅ ESPECIFICACIÓN COMPLETA
   Cuando: Todos los requisitos están documentados
   Quién: PM + Tech Lead
   Acción: Mover a "READY FOR DEV"

🔄 EN REVISIÓN
   Cuando: Esperando feedback de stakeholders
   Quién: Product Manager
   Acción: Setear reviewers

⚠️ INCOMPLETA
   Cuando: Faltan requisitos o hay ambigüedad
   Quién: Cualquier desarrollador
   Acción: Comentar qué falta, volver a DISCOVERY

✅ IMPLEMENTACIÓN OK
   Cuando: Código merged y tests OK
   Quién: Tech Lead
   Acción: Mover a "READY FOR PRODUCTION"

✅ PRODUCCIÓN
   Cuando: Deployed exitosamente
   Quién: DevOps/Release Manager
   Acción: Cerrar Epic, DONE
```

### 4. Etiquetas de Prioridad

```
🔴 BLOCKER       - Bloquea desarrollo
🟠 CRITICAL      - Necesario para release
🟡 HIGH          - Importante, hacer pronto
🟢 MEDIUM        - Normal priority
🔵 LOW           - Puede esperar
⚪ TECHNICAL     - Deuda técnica
```

### 5. Comunicación en Jira

**En Comments, usar:**

```
@persona - Para mencionar alguien específico
/vote - Para votar si es importante
/link - Para vincular con otra tarea
/time - Para logging de tiempo
/todo - Para crear subtareas on-the-fly

EJEMPLO:
@dev-team Revisemos la arquitectura antes de empezar
/link blocks PROJ-456
/time 2h 30m
```

---

## 👥 Múltiples Desarrolladores / Multiple Developers

### 1. Asignación y Colaboración

**Modelo de Asignación:**

```
PRIMARY ASSIGNEE
└─ Dev responsable de task
   ├─ Crea rama
   ├─ Hace commits principales
   ├─ Crea PR
   └─ Responsable de merge

SECONDARY ASSIGNEES (en campo personalizado)
├─ Dev 2: Pair programming
├─ Dev 3: Código review especializado
└─ Dev 4: Testing especializado

REVIEWER ROTATION
├─ Semana 1: Dev A + Dev B
├─ Semana 2: Dev B + Dev C
├─ Semana 3: Dev C + Dev D
└─ Semana 4: Dev A + Dev D
└─ Beneficio: Conocimiento distribuido
```

### 2. Pair Programming en Jira

**Cuando usar Pair Programming:**

```
✅ BUENAS SITUACIONES:
   - Código crítico (autenticación, pagos)
   - Junior + Senior developer
   - Nuevo patrón de arquitectura
   - Bug difícil de reproducir

❌ EVITAR PAIR PROGRAMMING EN:
   - Tareas repetitivas
   - Refactoring simple
   - Testing rutinario
   - Documentación
```

**Configuración Jira:**

```
Story: "Implement payment processing"

Assignee: dev-senior@company.com
Collaborators: dev-junior@company.com

Branch: feat/PROJ-789-payment-processing
Strategy: Pair Programming

Pair Session 1: 2h
Pair Session 2: 2h
Pair Session 3: 1h
Total: 5h

Comment: "Pair programming sessions:
- Session 1: Setup + Architecture
- Session 2: Implementation
- Session 3: Testing + edge cases
Logged time: /time 5h"
```

### 3. Trabajo Concurrente (Múltiples Devs en Mismo Código)

**Estrategia de Branches:**

```
ESCENARIO: Feature A requiere cambios en Módulo Compartido

Opción 1: Feature Branch por Dev
──────────────────────────────
feat/PROJ-111-user-auth
├─ Auth logic (Dev A)
├─ JWT tokens (Dev B)
└─ Unit tests (Dev C)

Merge: Cada parte cuando esté lista
Integración: En develop

Opción 2: Subtasks con Branching
────────────────────────────────
Story: PROJ-111 - User Authentication System
├─ Subtask 1: Auth logic (Dev A) → feat/PROJ-111-1
├─ Subtask 2: JWT tokens (Dev B) → feat/PROJ-111-2
├─ Subtask 3: Integration (Dev C) → feat/PROJ-111-3
└─ Subtask 4: Tests (Dev D) → feat/PROJ-111-4

Merge Order: Específico para evitar conflictos
```

### 4. Gestión de Conflictos

**En Jira:**

```
CONFLICTO DETECTADO
│
├─ Task: "Resolver conflicto de merge PROJ-456"
├─ Assignee: Dev más senior del par
├─ Priority: BLOCKER
├─ Comment:
│  "Conflicto entre feat/PROJ-456 y feat/PROJ-457
│   en archivo: src/modules/auth/service.ts
│   @dev-a @dev-b - Reunion síncrona para resolver"
└─ Status: IN PROGRESS

DESPUÉS:
├─ Merge exitoso
├─ Comment: "Resuelto - Dev A hizo merge"
├─ Time logged: /time 1h 30m
└─ Status: DONE
```

### 5. Documentación Compartida

**Ubicación en Jira:**

```
Epic > Description
│
├─ Diseño de arquitectura (Markdown con diagramas)
├─ Links a docs/ en el repo
├─ Decisiones clave
└─ Cambios importantes

Actualizado por: Tech Lead
Frecuencia: Inicial + cuando hay cambios
Revisar por: Todos los devs antes de empezar
```

---

## 🚫 Restricciones y Limitaciones / Constraints & Limitations

### 1. Limitaciones de Jira

| Limitación                   | Impacto                       | Mitigación                   |
| ---------------------------- | ----------------------------- | ---------------------------- |
| **Max 100 custom fields**    | No podemos mapear todo        | Usar 5-10 campos críticos    |
| **API rate limits**          | Automatización lenta          | Batch operations, scheduled  |
| **Proyectos max 10K issues** | Historial muy largo           | Archive old issues anually   |
| **Reporting limitado**       | Métricas complejas difíciles  | Integrar con Jira Automation |
| **Campos sin versionado**    | No ver cambios históricos\*\* | Usar Activity log + comments |

### 2. Restricciones SDD + Jira

```
RESTRICCIÓN 1: Sincronización de Documentos
─────────────────────────────────────────
Problema:  Jira Description ≠ docs/01-requirements.md
Solución:  Source of truth = docs/
           Jira = referencia + checklist

RESTRICCIÓN 2: Múltiples Equipos
─────────────────────────────────
Problema:  Equipos pueden sobrescribirse mutuamente
Solución:  Clear ownership + code review
           Ramas separadas por equipo
           MRs/PRs requeridos siempre

RESTRICCIÓN 3: Validación de Especificaciones
──────────────────────────────────────────────
Problema:  Jira no valida que código cumpla specs
Solución:  Code review checklist
           Usar linting + testing
           PR requires specs approval

RESTRICCIÓN 4: Escalabilidad de Tracking
────────────────────────────────────────
Problema:  100 devs = 100 historias paralelas
Solución:  Epics agrupan historias
           Proyectos separados si > 500 issues
           Automación para actualizar status

RESTRICCIÓN 5: Agnóstico de Metodología
───────────────────────────────────────
Problema:  SDD no prescribe sprints/ceremonies
Solución:  Adaptar Jira a tu metodología
           No forzar ceremonias innecesarias
           Ser flexible con iteraciones
```

### 3. Cuando NO Usar Esta Integración

```
❌ NO USAR SI:
   - Equipo < 3 personas (overhead innecesario)
   - Proyecto < 2 semanas (demasiado overhead)
   - Equipo no está geográficamente distribuido
   - No hay specs claras previas
   - Presupuesto no existe

✅ USA CUANDO:
   - Equipo > 5 personas
   - Proyecto > 3 meses
   - Múltiples equipos/stakeholders
   - Cambios frecuentes esperados
   - Compliance/traceability importante
```

### 4. Curva de Aprendizaje

```
SEMANA 1-2: Setup
───────────
- Configurar Jira
- Crear campos personalizados
- Entrenar equipo
- Ajustar workflows
Tiempo: 20-40 horas

SEMANA 3-4: Estabilización
──────────
- Primeras tareas en flujo
- Ajustes en procesos
- Troubleshooting
Tiempo: 10-15 horas

SEMANA 5+: Normal
────────
- Flujo automático
- Mejoras incrementales
- Metrics collection
Tiempo: 5-10 horas/semana

TOTAL OVERHEAD: 15-20% inicialmente → 5-10% estable
```

### 5. Antipatrones a Evitar

```
❌ ANTIPATRÓN 1: Epic = Sprint
   Problema: Epics muy grandes, sprints muy cortos
   Solución: Epic = Feature, Sprint = subset

❌ ANTIPATRÓN 2: Historias sin especificación
   Problema: Dev no sabe qué hacer
   Solución: Spec aprobado ANTES de crear Story

❌ ANTIPATRÓN 3: Nobody updates Jira
   Problema: Jira desincronizado con realidad
   Solución: Actualizar DIARIO, 5 min por dev

❌ ANTIPATRÓN 4: Demasiados campos personalizados
   Problema: Jira overwhelm, lento
   Solución: Max 10 campos, ser selectivo

❌ ANTIPATRÓN 5: No validar Specs Compliance
   Problema: Código que no cumple specs
   Solución: Checklist en DoD, code review

❌ ANTIPATRÓN 6: Ignorar la documentación SDD
   Problema: Jira se vuelve única fuente de verdad
   Solución: Actualizar docs/ siempre con Jira
```

---

## ✅ Checklist de Implementación / Implementation Checklist

### Fase 1: Preparación (1-2 semanas)

- [ ] **Jira Setup**
  - [ ] Crear proyecto [PROYECTO]
  - [ ] Definir Epics principales
  - [ ] Crear 5-10 campos personalizados
  - [ ] Configurar 3 workflows (Discovery/Dev/Ops)
  - [ ] Establecer Definition of Done

- [ ] **SDD Repository**
  - [ ] Clonar sdd-templates repo
  - [ ] Personalizar con [PLACEHOLDERS]
  - [ ] Crear branch `docs/sdd-setup`
  - [ ] Inicializar docs/ en proyecto principal
  - [ ] Crear `01-requirements.md` inicial
  - [ ] Crear `02-architecture.md` inicial

- [ ] **Entrenamiento**
  - [ ] Training session 1: SDD metodología (2h)
  - [ ] Training session 2: Jira workflow (2h)
  - [ ] Training session 3: Hands-on practice (3h)
  - [ ] Crear cheat sheet en Confluence
  - [ ] Video tutoriales grabados

- [ ] **Documentación**
  - [ ] Crear guía en Confluence
  - [ ] Documentar procesos locales
  - [ ] Crear templates de issue
  - [ ] Documentar custom fields

### Fase 2: Piloto (2-4 semanas)

- [ ] **Pilot Team**
  - [ ] Seleccionar 3-5 devs para piloto
  - [ ] Asignar pequeño feature como prueba
  - [ ] Usar workflow SDD completo

- [ ] **First Feature**
  - [ ] Track 1: Especificar feature
  - [ ] Track 2: Implementar
  - [ ] Track 3: Deploy a staging
  - [ ] Retrospective y ajustes

- [ ] **Métricas**
  - [ ] Medir tiempo spec → implementation
  - [ ] Contar PRs rechazadas por specs mismatch
  - [ ] Velocidad de development
  - [ ] Retrabajos por specs incompletas

- [ ] **Ajustes**
  - [ ] Feedback del piloto team
  - [ ] Ajustar workflows si necesario
  - [ ] Optimizar custom fields
  - [ ] Mejorar templates

### Fase 3: Rollout (1-2 semanas)

- [ ] **Full Team**
  - [ ] Training para todo el equipo
  - [ ] Suministrar acceso a Jira
  - [ ] Asignar roles/permisos

- [ ] **Primer Sprint/Ciclo**
  - [ ] Ejecutar workflow completo
  - [ ] Monitorear adoption
  - [ ] Resolver bloqueadores

- [ ] **Support**
  - [ ] Designar Jira admin/champion
  - [ ] Crear canal #jira-help
  - [ ] Daily standup primeras 2 semanas

### Fase 4: Optimización Continua (Ongoing)

- [ ] **Monthly Reviews**
  - [ ] Revisar métricas
  - [ ] Recolectar feedback
  - [ ] Ajustar workflows
  - [ ] Actualizar documentación

- [ ] **Automation**
  - [ ] Auto-crear subtasks
  - [ ] Auto-actualizar status
  - [ ] Auto-generar reports
  - [ ] Auto-sync con docs/tracking

- [ ] **Integration**
  - [ ] Jira ↔ GitHub webhooks
  - [ ] Jira ↔ Slack notifications
  - [ ] Jira ↔ Confluence docs
  - [ ] Jira ↔ Analytics

---

## 📊 Ejemplo de Configuración Completa / Complete Configuration Example

### Proyecto Ejemplo: E-Commerce Platform

**Nombre Jira**: ECOM (E-Commerce)  
**Equipo**: 8 desarrolladores  
**Duración**: 6 meses  
**Metodología**: Dual Track + bi-weekly sprints

### Estructura de Epics

```
Epic 1: ECOM-1 - User Management System
├─ Story ECOM-10: Implement user registration
├─ Story ECOM-11: Implement login/logout
├─ Story ECOM-12: Implement password reset
└─ Story ECOM-13: Implement user profiles

Epic 2: ECOM-2 - Product Catalog
├─ Story ECOM-20: Product listing
├─ Story ECOM-21: Product details page
├─ Story ECOM-22: Product search
└─ Story ECOM-23: Product filtering

Epic 3: ECOM-3 - Shopping Cart
├─ Story ECOM-30: Add to cart
├─ Story ECOM-31: Remove from cart
├─ Story ECOM-32: Cart persistence
└─ Story ECOM-33: Cart summary

Epic 4: ECOM-4 - Payment Processing
├─ Story ECOM-40: Payment gateway integration
├─ Story ECOM-41: Payment error handling
├─ Story ECOM-42: Payment receipt
└─ Story ECOM-43: Refund handling

Epic 5: ECOM-5 - Order Management
├─ Story ECOM-50: Order creation
├─ Story ECOM-51: Order tracking
├─ Story ECOM-52: Order history
└─ Story ECOM-53: Order cancellation
```

### Workflow Visual (Epic ECOM-1)

```
TIMELINE VISUALIZACIÓN
╔════════════════════════════════════════════════════════╗
║  Week 1-2: DISCOVERY (Track 1)                        ║
║  ├─ ECOM-1 created (TODO)                             ║
║  ├─ Analysis tasks (IN RESEARCH)                      ║
║  ├─ Spec writing (IN DESIGN)                          ║
║  └─ Stakeholder review (SPEC REVIEW) → APPROVED      ║
║                                                        ║
║  Week 3-4: IMPLEMENTATION (Track 2)                   ║
║  ├─ ECOM-10 (Backlog → In Progress)                   ║
║  ├─ ECOM-11 (Backlog → In Progress)                   ║
║  ├─ Code reviews (IN REVIEW)                          ║
║  └─ All approved (READY FOR MERGE)                    ║
║                                                        ║
║  Week 5: DEPLOYMENT (Track 3)                         ║
║  ├─ Staging deployment                                ║
║  ├─ QA testing                                        ║
║  ├─ Production deployment                             ║
║  └─ Epic DONE ✅                                       ║
╚════════════════════════════════════════════════════════╝
```

### Ejemplo de Story Completa

```
Title: ECOM-10 - Implement user registration

Type: Story
Epic Link: ECOM-1 - User Management System
Status: IN PROGRESS

Assignee: dev-alice@company.com
Secondary Assignees: dev-bob@company.com (pair), dev-charlie@company.com (code review)

Priority: HIGH
Story Points: 8

📋 Specification Linked:
- Requirement: docs/01-requirements.md#user-registration
- Architecture: docs/02-architecture.md#auth-layer
- Structure: docs/07-project-structure-backend.md#modules

🎯 Acceptance Criteria:
- [ ] User can enter email, password, confirm password
- [ ] Password validation: min 8 chars, 1 uppercase, 1 number
- [ ] Email uniqueness validation
- [ ] Success: Redirect to login page
- [ ] Error: Show validation errors inline
- [ ] Email verification sent (future phase)

✅ Definition of Done:
- [ ] Código implementado en rama feat/ECOM-10
- [ ] Unitests: 80%+ coverage
- [ ] Integration tests: Happy path + error cases
- [ ] Code reviewed por 2 devs
- [ ] Cumple SDD specs 100%
- [ ] No regressions en ECOM-9
- [ ] Documentación actualizada
- [ ] Changelog entry

🔗 Related:
- Blocks: ECOM-11 (login requires registration)
- Related: ECOM-13 (user profiles)

📝 Comments:
Dev Alice: "Starting pair programming with Bob. Expected 8h total."
Dev Bob: "Setup development environment, running tests locally"
Dev Charlie: "Ready for code review, monitoring this issue"

⏱️ Time Logged:
- Pair session 1: 2h (Alice + Bob)
- Pair session 2: 2.5h (Alice + Bob)
- Code review: 1h (Charlie)
- Fixes: 1.5h (Alice)
Total: 7h
```

---

## 🔧 Comando de Git + Jira / Git + Jira Commands

### Git Hooks para Automatización

```bash
# .git/hooks/commit-msg
#!/bin/bash
# Auto-prepend JIRA ticket number

BRANCH=$(git rev-parse --abbrev-ref HEAD)
TICKET=$(echo $BRANCH | grep -oE '[A-Z]+-[0-9]+')

if [ ! -z "$TICKET" ]; then
  sed -i "1s/^/$TICKET: /" $1
fi
```

### Jira CLI Commands

```bash
# Crear issue desde CLI
jira issue create --type Story --project ECOM \
  --summary "Implement feature X" \
  --description "Detailed description" \
  --assignee dev-alice

# Cambiar status
jira issue move ECOM-10 --transition "Ready for Dev"

# Agregar comment
jira issue comment ECOM-10 -m "Starting implementation"

# Link a especificación
jira link ECOM-10 --type "relates to" \
  --linked-issue "docs/01-requirements.md"

# Ver status
jira issue view ECOM-10

# List issues assigned
jira issue list --assignee=dev-alice --status "In Progress"
```

---

## 🎓 Conclusión y Recursos / Conclusion & Resources

### Resumen de Implementación

Esta guía proporciona:
✅ Configuración completa de Jira para SDD  
✅ Workflows para Dual Track  
✅ Mejores prácticas para múltiples devs  
✅ Gestión de restricciones  
✅ Checklist de implementación

### Próximos Pasos

1. **Personalizar** esta guía con tus valores [PLACEHOLDERS]
2. **Configurar** Jira según templates proporcionados
3. **Entrenar** equipo en SDD + Jira
4. **Ejecutar** piloto con pequeño feature
5. **Iterar** basado en feedback real

### Recursos Adicionales

- 📖 Guía SDD: `sdd-templates/shared/00-metodologia-trabajo.md`
- 📋 Requirements Template: `sdd-templates/shared/01-requirements.md`
- 🏗️ Architecture Template: `sdd-templates/shared/02-architecture.md`
- 📊 Progress Tracking: `sdd-templates/shared/tracking/00-progress-overview.md`
- 🐛 Issues Log: `sdd-templates/shared/tracking/03-issues-log.md`

### Contacto y Soporte

- **Jira Admin**: [RESPONSABLE-JIRA]
- **SDD Champion**: [RESPONSABLE-SDD]
- **Canal Slack**: #sdd-jira-support
- **Email**: [EMAIL-SOPORTE]

---

**Versión**: 1.0.0  
**Última actualización**: 16 de diciembre de 2024  
**Status**: ✅ Completado y listo para usar  
**Mantenedor**: [EQUIPO/PERSONA]
