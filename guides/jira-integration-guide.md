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
5. [Mejores Prácticas para Historias, Épicas, Tareas y Bugs](#-mejores-prácticas-para-historias-épicas-tareas-y-bugs--best-practices-for-stories-epics-tasks--bugs)
6. [Mejores Prácticas General](#mejores-prácticas--best-practices)
7. [Múltiples Desarrolladores](#múltiples-desarrolladores)
8. [Restricciones y Limitaciones](#restricciones-y-limitaciones)
9. [Checklist de Implementación](#checklist-de-implementación)
10. **[Referencia: Best Practices Detalladas](best-practices-issues.md)** - Guía completa separada

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

## � Mejores Prácticas para Historias, Épicas, Tareas y Bugs / Best Practices for Stories, Epics, Tasks & Bugs

### Anatomía de Cada Tipo de Issue

#### 1️⃣ ÉPICAS / Epics

**¿Qué es?**

- Contenedor de múltiples historias relacionadas
- Representa una iniciativa o capacidad de negocio completa
- Tiempo de vida: Semanas a meses
- Scope: Grande (20+ puntos de historia)

**Cuándo Crear:**

```
✅ CREAR ÉPICA CUANDO:
   - Iniciativa estratégica de negocio
   - Múltiples historias relacionadas (3+)
   - Timeline: 2+ sprints
   - Stakeholders principales interesados

❌ NO CREAR SI:
   - Solo 1-2 historias
   - Tarea one-off
   - Menos de 1 semana de trabajo
```

**Estructura Recomendada:**

```markdown
# ECOM-1 - User Management System

## 📋 Descripción / Description

Implementar sistema completo de gestión de usuarios incluyendo
registro, login, perfil y autenticación.

**Objetivo de Negocio**:
Permitir que usuarios se registren y gestionen sus cuentas de forma segura.

**Beneficio**:
Aumentar adopción de plataforma, permitir personalización por usuario.

## 🎯 Alcance / Scope

- [ ] User registration with email verification
- [ ] Login/logout with JWT tokens
- [ ] Password reset via email
- [ ] User profile management
- [ ] Role-based access control (RBAC)
- [ ] Social login (future phase, out of scope)

## 📊 Estimación

- **Effort**: 40 story points (8 sprints)
- **Duration**: 8-10 semanas
- **Team Size**: 3-4 developers
- **Dependencies**: Database setup, Email service

## 📚 Especificación Vinculada / Linked Specification

- **Requirements**: [docs/01-requirements.md#user-management](link)
- **Architecture**: [docs/02-architecture.md#auth-layer](link)
- **Data Models**: [docs/02-architecture.md#data-models](link)

## ✅ Definition of Done (Epic)

- [ ] Todas las historias child completadas
- [ ] Especificación completamente documentada
- [ ] Arquitectura aprobada por Tech Lead
- [ ] 80%+ test coverage en todas las historias
- [ ] Documentación actualizada (API docs, user guide)
- [ ] Deployed a producción exitosamente
- [ ] Monitoring configurado

## 📈 Aceptación de Negocio

- [ ] Product Owner revisó y aprobó
- [ ] Stakeholders validaron funcionalidad
- [ ] Metrics: X% aumento en adopción

## 🔗 Child Stories

- ECOM-10: Implement user registration
- ECOM-11: Implement login/logout
- ECOM-12: Implement password reset
- ECOM-13: Implement user profiles
- ECOM-14: Implement RBAC

## 📝 Notas

- Prioridad: ALTA - Bloqueador para otras épicas
- Riesgos: Integración de email, performance con muchos usuarios
- Dependencias: INFRA-5 (Database), INFRA-6 (Email service)
```

**Flujo de Épica:**

```
┌──────────────────────────────────────────┐
│ EPIC LIFECYCLE                           │
├──────────────────────────────────────────┤
│                                          │
│ 1. PLANNING (Semana anterior)            │
│    ├─ PM define objetivo de negocio      │
│    ├─ Tech Lead estima esfuerzo          │
│    ├─ Crear en Jira con descripción      │
│    └─ Status: TODO                       │
│                                          │
│ 2. DISCOVERY (Track 1)                   │
│    ├─ Crear subtareas de análisis        │
│    ├─ Escribir especificación            │
│    ├─ Diseñar arquitectura               │
│    ├─ Stakeholder review                 │
│    └─ Status: SPEC_APPROVED              │
│                                          │
│ 3. REFINEMENT                            │
│    ├─ Crear historias child detalladas   │
│    ├─ Estimación de cada historia        │
│    ├─ Asignar a sprints                  │
│    └─ Status: READY_FOR_DEVELOPMENT      │
│                                          │
│ 4. IMPLEMENTATION (Track 2)              │
│    ├─ Desarrolladores implementan        │
│    ├─ Code reviews                       │
│    ├─ Testing                            │
│    └─ Status: IN_DEVELOPMENT             │
│                                          │
│ 5. VALIDATION (Track 3)                  │
│    ├─ QA testing completo                │
│    ├─ Performance testing                │
│    ├─ Deployment a staging               │
│    └─ Status: READY_FOR_PRODUCTION       │
│                                          │
│ 6. DEPLOYMENT                            │
│    ├─ Production deployment              │
│    ├─ Monitoring setup                   │
│    ├─ Post-deployment validation         │
│    └─ Status: DONE ✅                    │
│                                          │
│ 7. POST-RELEASE (Optional)               │
│    ├─ Retrospective                      │
│    ├─ Performance analysis               │
│    ├─ Lessons learned                    │
│    └─ Status: CLOSED                     │
│                                          │
└──────────────────────────────────────────┘
```

---

#### 2️⃣ HISTORIAS / Stories (User Stories)

**¿Qué es?**

- Funcionalidad específica desde perspectiva del usuario
- Tamaño mediano: 5-13 puntos de historia
- Completable en 2-4 días de trabajo
- Child de una Épica

**Cuándo Crear:**

```
✅ CREAR HISTORIA CUANDO:
   - Feature visible al usuario final
   - Valor de negocio claro
   - Puede completarse en un sprint
   - Aceptación criterios bien definidos

❌ NO CREAR SI:
   - Tarea técnica pura (→ Task)
   - Problema existente (→ Bug)
   - Muy pequeño (→ Subtask)
   - Muy grande (→ Epic)
```

**Formato Recomendado (Gherkin):**

````markdown
# ECOM-10 - Implement User Registration

## 📖 Historia de Usuario / User Story

Como **usuario nuevo**
Quiero **registrarme con email y contraseña**
Para que **pueda crear una cuenta y acceder a la plataforma**

## 🎯 Acceptance Criteria

### Scenario 1: Registro exitoso con datos válidos

```gherkin
Given Estoy en la página de registro
When Ingreso email "user@example.com"
  And Ingreso contraseña "SecurePass123!"
  And Hago clic en "Registrarse"
Then Debería ver mensaje "Registro exitoso"
  And Debería ser redirigido a página de login
  And Email de verificación debería ser enviado
```
````

### Scenario 2: Email ya registrado

```gherkin
Given El email "existing@example.com" ya está registrado
When Intento registrarme con ese email
Then Debería ver error "Este email ya está registrado"
  And No debería crear la cuenta
```

### Scenario 3: Contraseña débil

```gherkin
Given Estoy en página de registro
When Intento ingresar contraseña "weak"
Then Debería ver error "Contraseña muy débil"
  And Debería mostrar requisitos: 8+ chars, mayúscula, número
```

### Scenario 4: Campos requeridos

```gherkin
Given Estoy en página de registro
When Intento enviar sin completar campos
Then Debería mostrar errores en campos vacíos
  And Botón "Registrarse" debería estar deshabilitado
```

## 📊 Información de la Historia

| Campo            | Valor                           |
| ---------------- | ------------------------------- |
| **Epic Link**    | ECOM-1 - User Management System |
| **Story Points** | 8                               |
| **Priority**     | HIGH                            |
| **Type**         | Story                           |
| **Sprint**       | Sprint 1                        |
| **Assignee**     | dev-alice@company.com           |

## 📚 Especificación Técnica

**Archivo SDD**: [docs/02-architecture.md#auth-registration](link)

**Endpoints**:

- `POST /api/auth/register` - Create new user account
- `GET /api/auth/verify-email/{token}` - Verify email

**Database**:

- Table: `users`
- Fields: id, email, password_hash, created_at, verified_at
- Constraint: unique(email)

**Security**:

- Use bcrypt for password hashing (cost factor: 12)
- Rate limit: 5 registrations per IP per hour
- Email verification token expires: 24 hours

## ✅ Definition of Done (Story)

- [ ] Endpoint POST /api/auth/register implementado
- [ ] Validación de email y contraseña funciona
- [ ] Email de verificación se envía correctamente
- [ ] Unit tests: 80%+ coverage
- [ ] Integration tests: Todos scenarios pasan
- [ ] Code review aprobado por 2 devs
- [ ] SDD compliance: 100%
- [ ] Documentación API actualizada
- [ ] No hay regressions en otras historias

## 🔗 Relaciones

**Depends On:**

- ECOM-1 (Epic)
- INFRA-6 (Email service setup)

**Related To:**

- ECOM-11 (Login - usa estos datos)
- ECOM-12 (Password reset - usa este email)

**Blocks:**

- ECOM-11 (No se puede login sin registro)

## 📝 Notas Técnicas

- Usar HTTPS para formulario de registro
- Password strength meter en UI
- Enviar email de verificación asincronamente
- Considerar GDPR compliance
- A/B test: social login en fase 2

## ⏱️ Estimación

- Dev Time: 5h (pairing 2 devs)
- Code Review: 1h
- Testing: 1h
- Deployment: 0.5h
- **Total**: 7.5h ~ 8 story points

```

**Flujo de Historia:**

```

┌──────────────────────────────────────────┐
│ STORY LIFECYCLE │
├──────────────────────────────────────────┤
│ │
│ 1. CREATION │
│ ├─ PM crea historia en Jira │
│ ├─ Escribir user story completa │
│ ├─ Definir acceptance criteria │
│ └─ Status: BACKLOG │
│ │
│ 2. REFINEMENT (Sprint Planning) │
│ ├─ Tech Lead estima story points │
│ ├─ Asignar a desarrollador │
│ ├─ Crear branch feat/JIRA-XXX │
│ └─ Status: READY_FOR_DEVELOPMENT │
│ │
│ 3. DEVELOPMENT │
│ ├─ Developer crea rama │
│ ├─ Implementa feature │
│ ├─ Escribe tests (80%+ coverage) │
│ ├─ Commit regularmente │
│ └─ Status: IN_DEVELOPMENT │
│ │
│ 4. CODE REVIEW │
│ ├─ Crear Pull Request │
│ ├─ Assign 2 reviewers │
│ ├─ Responder comments │
│ ├─ Fix requested changes │
│ └─ Status: IN_REVIEW │
│ │
│ 5. APPROVAL │
│ ├─ 2+ reviewers aprueban │
│ ├─ All CI/CD checks pasan │
│ ├─ Merge a develop │
│ └─ Status: APPROVED │
│ │
│ 6. TESTING │
│ ├─ QA ejecuta test scenarios │
│ ├─ Testing en staging env │
│ ├─ Performance check │
│ ├─ Regression testing │
│ └─ Status: TESTED │
│ │
│ 7. DEPLOYMENT │
│ ├─ Deploy a producción │
│ ├─ Health checks │
│ ├─ Monitoring activado │
│ └─ Status: DONE ✅ │
│ │
│ 8. CLOSE │
│ ├─ Resolver comentarios finales │
│ ├─ Actualizar docs │
│ └─ Status: CLOSED │
│ │
└──────────────────────────────────────────┘

```

---

#### 3️⃣ TAREAS / Tasks

**¿Qué es?**
- Trabajo técnico o administrativo sin valor directo del usuario
- Tamaño pequeño: 2-5 puntos de historia
- No tiene "user story" - es actividad técnica
- Puede ser independiente o subtarea de historia

**Cuándo Crear:**
```

✅ CREAR TAREA CUANDO:

- Trabajo técnico puro (refactor, setup)
- Tarea administrativa (doc, training)
- Investigación técnica (spike)
- Deuda técnica necesaria
- Setup de infraestructura

❌ NO CREAR SI:

- Tiene valor directo para usuario (→ Story)
- Problema existente (→ Bug)
- Muy grande (→ Epic)

````

**Estructura Recomendada:**

```markdown
# INFRA-23 - Setup PostgreSQL Database for Production

## 📋 Descripción / Description
Configurar instancia de PostgreSQL para entorno de producción con:
- Backups automáticos
- Replicación para HA
- Monitoring y alertas
- Acceso seguro (VPC, SSL)

## 🎯 Objetivos

### Configuración de Base de Datos
- [ ] Crear instancia RDS PostgreSQL 14.x
- [ ] Configurar 2 réplicas para alta disponibilidad
- [ ] Setup de backups automáticos (diarios, retención 30 días)
- [ ] Restore testing de backups

### Seguridad
- [ ] SSL/TLS para todas las conexiones
- [ ] Configurar VPC security groups
- [ ] Restrict access a VPN/bastion host solamente
- [ ] Rotate master password después de setup
- [ ] Enable audit logging

### Monitoreo
- [ ] CloudWatch metrics para CPU, memory, connections
- [ ] Alertas: CPU > 80%, connections > threshold
- [ ] Query performance insights habilitado
- [ ] Setup de logs a CloudWatch

### Documentación
- [ ] Crear runbook para recuperación ante desastre
- [ ] Documentar connection strings para dev/staging/prod
- [ ] Crear checklist de mantenimiento mensual

## 📊 Información de la Tarea

| Campo | Valor |
|-------|-------|
| **Type** | Task |
| **Story Points** | 5 |
| **Priority** | CRITICAL |
| **Epic Link** | INFRA-1 - Infrastructure Setup |
| **Assignee** | devops-team |

## 📚 Especificación Técnica

**Ambiente**: AWS Production
**Timeline**: 1-2 días
**Blocker**: Necesario antes de deployment de ECOM-1

**Pasos**:
1. Crear RDS instance en us-east-1
2. Configure replication to us-west-2
3. Setup CloudWatch monitoring
4. Test backup/restore
5. Security audit
6. Update connection strings en aplicación

## ✅ Definition of Done (Task)

- [ ] Base de datos creada y accesible
- [ ] Backups funcionando y testeados
- [ ] Monitoring alertas configuradas
- [ ] Runbook de recuperación escrito
- [ ] Security audit completado
- [ ] Dev/staging/prod pueden conectarse
- [ ] Documentation actualizada
- [ ] Ticket de follow-up para maintenance

## 🔗 Dependencias

**Blocker For:**
- ECOM-1 (User Management - necesita DB)
- ECOM-2 (Product Catalog - necesita DB)

**Depends On:**
- AWS account provisioning
- VPC setup (INFRA-22)

## ⏱️ Estimación

- Planning & design: 1h
- Implementation: 3h
- Testing & validation: 1h
- **Total**: 5 story points

## 📝 Recursos

- [AWS RDS Setup Guide](link)
- [PostgreSQL HA Architecture](link)
- [Infrastructure as Code repo](link)
````

**Flujo de Tarea:**

```
┌──────────────────────────────────────────┐
│ TASK LIFECYCLE                           │
├──────────────────────────────────────────┤
│                                          │
│ 1. IDENTIFICATION                        │
│    ├─ Tech Lead identifica necesidad     │
│    ├─ Crear tarea con descripción        │
│    ├─ Estimar puntos de historia         │
│    └─ Status: TODO                       │
│                                          │
│ 2. ASSIGNMENT                            │
│    ├─ Asignar a developer/DevOps         │
│    ├─ Comunicar urgencia/prioridad       │
│    └─ Status: ASSIGNED                   │
│                                          │
│ 3. EXECUTION                             │
│    ├─ Crear rama si es código            │
│    ├─ Ejecutar tarea según descripción   │
│    ├─ Documentar pasos                   │
│    └─ Status: IN_PROGRESS                │
│                                          │
│ 4. VERIFICATION                          │
│    ├─ Revisar checklist completado       │
│    ├─ Testing de cambios                 │
│    ├─ Code review si aplica              │
│    └─ Status: REVIEW                     │
│                                          │
│ 5. CLOSURE                               │
│    ├─ Actualizar documentación           │
│    ├─ Communicar completion              │
│    ├─ Resolver follow-up issues          │
│    └─ Status: DONE ✅                    │
│                                          │
└──────────────────────────────────────────┘
```

---

#### 4️⃣ BUGS / Bug Reports

**¿Qué es?**

- Problema o comportamiento incorrecto en sistema existente
- Descripción clara del problema + pasos para reproducir
- Prioridad basada en impacto (blocker < critical < high < medium < low)
- Puede tener severidad diferente de prioridad

**Cuándo Crear:**

```
✅ CREAR BUG CUANDO:
   - Comportamiento incorrecto observado
   - No cumple aceptación criteria de feature
   - Falla no intencional
   - Error en producción o staging
   - Regression de funcionalidad previa

❌ NO CREAR SI:
   - Es feature request (→ Story)
   - Es tarea técnica (→ Task)
   - Es documentación incorrecta (→ Doc issue)
```

**Formato Recomendado:**

````markdown
# ECOM-150 - User Registration Button Disabled on Firefox

## 🐛 Bug Report

### 📝 Descripción

El botón "Registrarse" se queda deshabilitado (disabled) en Firefox después de
llenar el formulario de registro con datos válidos. En Chrome y Safari funciona
correctamente.

### 📊 Severidad & Prioridad

| Atributo           | Valor                                  |
| ------------------ | -------------------------------------- |
| **Severity**       | 🔴 CRITICAL (Bloquea feature completa) |
| **Priority**       | 🔴 BLOCKER (Afecta producción)         |
| **Affected Users** | ~35% (Firefox users)                   |
| **Environment**    | Production                             |
| **Type**           | Bug                                    |

### 🔄 Pasos para Reproducir

**Precondiciones:**

- Browser: Firefox 121+
- URL: https://app.example.com/register
- Estado: No autenticado

**Pasos:**

1. Navegar a página de registro
2. Llenar email: `test@example.com`
3. Llenar contraseña: `SecurePass123!`
4. Llenar confirm password: `SecurePass123!`
5. Observar botón "Registrarse"

**Resultado Esperado:**

- Botón debería estar habilitado (clickeable)
- Color verde, cursor cambia a pointer

**Resultado Actual:**

- Botón sigue deshabilitado (grayed out)
- `opacity: 0.5`, `cursor: not-allowed`
- Imposible hacer click

### 🖼️ Evidencia

**Screenshots:**

- [Chrome - Button Enabled](link-to-screenshot)
- [Firefox - Button Disabled](link-to-screenshot)

**Video de Reproducción:**

- [Bug Video](link-to-video)

**Browser Console Errors:**

```javascript
Uncaught TypeError: window.matchMedia is not a function
  at form-validator.js:45
  at HTMLFormElement.addEventListener (form-validator.js:1)
```
````

### 🔍 Información Técnica

**Environment Details:**

- Firefox Version: 121.0
- OS: Ubuntu 22.04 LTS
- Node Version: N/A (Client-side)
- App Version: v1.2.3

**Browser DevTools Info:**

```
User Agent: Mozilla/5.0 (X11; Linux x86_64; rv:121.0)
  Gecko/20100101 Firefox/121.0
LocalStorage: Empty
Cookies: Normal
```

**Related Code Files:**

- `frontend/src/pages/Register.tsx`
- `frontend/src/components/Form/FormValidator.js` (línea 45)
- `frontend/src/styles/register.css`

### 📚 Especificación Vinculada

- **Requirements**: [docs/01-requirements.md#registration-ui](link)
- **Component Spec**: [docs/10-component-architecture.md#form-components](link)

### 🔗 Relaciones

**Related Issues:**

- ECOM-10 (Feature: User Registration)
- ECOM-156 (Similar: Button disabled in Safari iOS)

**Blocks:**

- ECOM-1 (Epic - Cannot release without fixing)

**Similar Issues:**

- BROWSER-234 (matchMedia not supported)

### 👥 Información del Reporter

| Campo              | Valor               |
| ------------------ | ------------------- |
| **Reporter**       | qa-team@company.com |
| **Found In**       | Production          |
| **Date Reported**  | 2024-12-16 10:30 AM |
| **First Seen**     | 2024-12-15 14:00 PM |
| **Last Confirmed** | 2024-12-16 11:45 AM |

### 📊 Impact Analysis

**Affected Users**:

- ~35% (Firefox market share)
- Approximately 2,500 potential users

**Business Impact**:

- Cannot register on Firefox
- Loss of potential customers
- Support tickets increasing

**Priority Justification**:

- Blocker: Core feature completely broken
- Production: Users cannot register
- Revenue Impact: Potential sales loss

### ✅ Definition of Done (Bug Fix)

- [ ] Root cause identificada
- [ ] Fix implementado
- [ ] Tested en Firefox 121+ (y otros browsers)
- [ ] Code review aprobado
- [ ] Unit tests agregados para prevenir regression
- [ ] Manual testing completado
- [ ] QA sign-off
- [ ] Deployed a staging
- [ ] Deployed a producción
- [ ] Monitored por 24h
- [ ] Cerrado

### 🔄 Workaround (Temporal)

Mientras se arregla, usuarios pueden:

1. Usar Chrome, Safari o Edge
2. Usar Firefox en modo privado (no siempre funciona)
3. Disabilitar extensiones (puede ayudar)

### 📝 Notas Técnicas

**Hipótesis de Root Cause:**

- `window.matchMedia` no está disponible en Firefox
- Polyfill faltante para form-validator.js
- CSS media queries evaluadas en JS incorrecto

**Investigación Necesaria:**

- Revisar form-validator.js línea 45
- Check si polyfill está cargado
- Test en Firefox developer edition

**Posibles Soluciones:**

1. Add matchMedia polyfill
2. Use try-catch en JavaScript
3. Refactor form validation lógica

### 🏷️ Labels

`frontend` `bug` `critical` `browser-compatibility` `form-validation`

### ⏱️ Estimación

- Investigation: 0.5h
- Fix: 1h
- Testing: 1h
- Deployment: 0.5h
- **Total**: 3 story points

### 🎯 Acceptance Criteria

- [ ] Botón "Registrarse" habilitado en Firefox
- [ ] Funciona en Firefox 115+
- [ ] No hay console errors
- [ ] Botón clickeable en todos los browsers
- [ ] Visual consistency en todos browsers

```

**Flujo de Bug:**

```

┌──────────────────────────────────────────┐
│ BUG LIFECYCLE │
├──────────────────────────────────────────┤
│ │
│ 1. REPORTING │
│ ├─ QA/User reporta bug │
│ ├─ Crear issue con detalles │
│ ├─ Agregar screenshots/videos │
│ └─ Status: NEW │
│ │
│ 2. TRIAGE │
│ ├─ Tech Lead revisa reproducibilidad │
│ ├─ Asignar severidad & prioridad │
│ ├─ Asignar investigador │
│ └─ Status: TRIAGED │
│ │
│ 3. INVESTIGATION │
│ ├─ Dev reproduce el bug │
│ ├─ Identificar root cause │
│ ├─ Documentar findings │
│ └─ Status: INVESTIGATING │
│ │
│ 4. FIX IMPLEMENTATION │
│ ├─ Crear rama fix/JIRA-XXX │
│ ├─ Implementar solución │
│ ├─ Escribir regression tests │
│ ├─ Commit con referencia a issue │
│ └─ Status: IN_PROGRESS │
│ │
│ 5. CODE REVIEW │
│ ├─ Crear PR │
│ ├─ Assign 2 reviewers │
│ ├─ Responder feedback │
│ ├─ Approvals obtenidos │
│ └─ Status: REVIEW │
│ │
│ 6. TESTING │
│ ├─ QA reproduce con fix │
│ ├─ Test en todos browsers/OS │
│ ├─ Regression testing │
│ ├─ Performance check │
│ └─ Status: TESTING │
│ │
│ 7. DEPLOYMENT │
│ ├─ Merge a develop │
│ ├─ Deploy a staging │
│ ├─ Final QA check │
│ ├─ Deploy a producción │
│ └─ Status: DEPLOYED │
│ │
│ 8. VERIFICATION │
│ ├─ Monitor logs por errores │
│ ├─ 24h monitoring │
│ ├─ QA final verification │
│ └─ Status: VERIFIED ✅ │
│ │
│ 9. CLOSURE │
│ ├─ Actualizar documentación │
│ ├─ Link a related issues │
│ ├─ Lessons learned │
│ └─ Status: CLOSED │
│ │
└──────────────────────────────────────────┘

```

---

## �🏆 Mejores Prácticas / Best Practices

### 1. Nomenclatura de Ramas y Commits

```

BRANCHES
────────
Discovery: analysis/JIRA-XXX-descriptive-name
Feature: feat/JIRA-XXX-descriptive-name
Bug Fix: fix/JIRA-XXX-issue-description
Hotfix: hotfix/JIRA-XXX-critical-issue
Refactor: refactor/JIRA-XXX-component-name

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

````

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
````

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
- **🎯 Best Practices Detalladas**: [best-practices-issues.md](best-practices-issues.md) - Guía completa sobre cómo crear Épicas, Historias, Tareas y Bugs

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
