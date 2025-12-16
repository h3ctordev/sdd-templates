# Mejores Prácticas para Historias, Épicas, Tareas y Bugs

> Guía completa sobre cómo crear, especificar y gestionar cada tipo de issue en Jira con SDD

**Versión**: 1.0.0  
**Fecha**: 16 de diciembre de 2024  
**Propósito**: Establecer estándares claros para cada tipo de issue

---

## 📊 Tabla Comparativa: Épicas vs Historias vs Tareas vs Bugs

| Criterio                | 📌 ÉPICA              | 📖 HISTORIA        | 📋 TAREA              | 🐛 BUG                 |
| ----------------------- | --------------------- | ------------------ | --------------------- | ---------------------- |
| **¿Qué es?**            | Iniciativa de negocio | Feature específica | Trabajo técnico       | Problema existente     |
| **Tamaño**              | 20-50 pts             | 5-13 pts           | 2-5 pts               | 1-5 pts                |
| **Duración**            | 4-12 semanas          | 2-4 días           | 1-2 días              | 1-3 días               |
| **Valor**               | Estratégico           | Directo usuario    | Indirecto             | Corrección             |
| **Perspectiva**         | "Qué"                 | "Quién/Cómo"       | Técnico               | "Qué no funciona"      |
| **Contiene**            | Historias + Tasks     | Subtasks           | Subtasks              | (Atomic)               |
| **Tiene User Story**    | No                    | Sí                 | No                    | No                     |
| **Acceptance Criteria** | Business goals        | Gherkin scenarios  | Technical checklist   | Reproduction steps     |
| **Dueño**               | Product Manager       | Developer          | Tech Lead/DevOps      | QA/User                |
| **Ejemplos**            | User Management       | Register button    | Setup Database        | Button disabled        |
| **Parent Issue**        | Ninguno               | Epic               | Epic/None             | Epic/None              |
| **Status Flow**         | DISCOVERY→DEV→DONE    | BACKLOG→DEV→DONE   | TODO→IN_PROGRESS→DONE | NEW→TRIAGED→FIXED→DONE |

---

## 🎯 Matriz de Decisión: ¿Qué tipo de issue crear?

```
¿Es un problema en el sistema?
├─ SÍ → 🐛 BUG
│  └─ Reportar con: Pasos reproducción + screenshots
│
└─ NO: ¿Tiene valor visible para usuario final?
   ├─ SÍ → 📖 HISTORIA
   │  └─ Formato: "Como... Quiero... Para..."
   │
   └─ NO: ¿Es trabajo técnico/administrativo?
      ├─ SÍ → 📋 TAREA
      │  └─ Formato: Descripción técnica + checklist
      │
      └─ NO: ¿Agrupa múltiples historias (3+)?
         ├─ SÍ → 📌 ÉPICA
         │  └─ Formato: Objetivo negocio + child issues
         │
         └─ NO: Es demasiado pequeño
            └─ Convertir en SUBTASK de historia existente
```

---

## ✅ Checklist de Calidad para Cada Tipo

### Checklist para ÉPICA

```
ANTES DE CREAR:
- [ ] Objetivo de negocio claro
- [ ] Beneficio para usuario identificado
- [ ] Estimación rough (20+ pts)
- [ ] Dependencias técnicas conocidas
- [ ] Stakeholders alineados

AL CREAR:
- [ ] Descripción > 200 palabras
- [ ] Enlace a especificación en docs/
- [ ] Epic goals definidas
- [ ] Timeline estimado
- [ ] Team size identificado

DURANTE EJECUCIÓN:
- [ ] Historias child linked
- [ ] Progreso actualizado semanalmente
- [ ] Bloqueadores comunicados
- [ ] Especificación sincronizada

AL CERRAR:
- [ ] Todas las historias child DONE
- [ ] Specifications actualizadas
- [ ] Retrospective realizada
- [ ] Lessons learned documentadas
```

### Checklist para HISTORIA

```
ANTES DE CREAR:
- [ ] Feature específica identificada
- [ ] Valor de negocio claro
- [ ] Aceptación criteria definidos
- [ ] Estimación 5-13 pts
- [ ] Epic parent identificado

AL CREAR:
- [ ] User story: Como X, Quiero Y, Para Z
- [ ] 3+ Gherkin scenarios como criteria
- [ ] Link a especificación técnica
- [ ] Definition of Done clara
- [ ] Estimación story points

DURANTE EJECUCIÓN:
- [ ] Branch creada: feat/JIRA-XXX-description
- [ ] Commits regularmente
- [ ] Tests escritos (80%+ coverage)
- [ ] PR creado antes de merge

AL COMPLETAR:
- [ ] Todos acceptance criteria pasados
- [ ] Code review aprobado (2+ devs)
- [ ] Tests pasan 100%
- [ ] Merged a develop
- [ ] Ready for testing
```

### Checklist para TAREA

```
ANTES DE CREAR:
- [ ] Necesidad técnica identificada
- [ ] No es feature visible (→ Historia)
- [ ] No es bug (→ Bug)
- [ ] Estimación 2-5 pts
- [ ] Owner técnico identificado

AL CREAR:
- [ ] Descripción técnica clara
- [ ] Pasos explícitos a completar
- [ ] Checklist de items
- [ ] Criterios de éxito definidos
- [ ] Link a documentación relevante

DURANTE EJECUCIÓN:
- [ ] Actualizar progreso en comentarios
- [ ] Documentar blockers
- [ ] Si tiene código: branch + PR

AL COMPLETAR:
- [ ] Checklist 100% completado
- [ ] Documentación actualizada
- [ ] Notifications enviadas
- [ ] Follow-up issues creadas si necesario
```

### Checklist para BUG

```
ANTES DE CREAR:
- [ ] Bug reproducible
- [ ] Pasos claros documentados
- [ ] Ambiente identificado (prod/staging/dev)
- [ ] Severidad & prioridad asignada
- [ ] Screenshots/videos adjuntos

AL CREAR:
- [ ] Título descriptivo del problema
- [ ] Pasos reproducción (step-by-step)
- [ ] Resultado esperado vs actual
- [ ] Ambiente exacto (browser, OS, version)
- [ ] Frecuencia (siempre/intermitente)
- [ ] Screenshots de antes/después

DURANTE INVESTIGACIÓN:
- [ ] Root cause documentado
- [ ] Hipótesis testeada
- [ ] Propuesta de fix comentada

DURANTE FIX:
- [ ] Branch: fix/JIRA-XXX-description
- [ ] Regression tests agregados
- [ ] Fix testeado en todos browsers
- [ ] PR con descripción completa

AL CERRAR:
- [ ] Fix deployed a producción
- [ ] Monitoreado por 24h
- [ ] QA final verification
- [ ] Related issues linked
```

---

## 📌 ÉPICAS - Guía Completa

### Qué es una Épica

- **Contenedor de múltiples historias relacionadas**
- **Representa una iniciativa o capacidad de negocio completa**
- **Tiempo de vida: Semanas a meses**
- **Scope: Grande (20+ puntos de historia)**

### Cuándo Crear

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

### Estructura Recomendada

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

- **Requirements**: docs/01-requirements.md#user-management
- **Architecture**: docs/02-architecture.md#auth-layer
- **Data Models**: docs/02-architecture.md#data-models

## ✅ Definition of Done (Epic)

- [ ] Todas las historias child completadas
- [ ] Especificación completamente documentada
- [ ] Arquitectura aprobada por Tech Lead
- [ ] 80%+ test coverage en todas las historias
- [ ] Documentación actualizada (API docs, user guide)
- [ ] Deployed a producción exitosamente
- [ ] Monitoring configurado

## 🔗 Child Stories

- ECOM-10: Implement user registration
- ECOM-11: Implement login/logout
- ECOM-12: Implement password reset
- ECOM-13: Implement user profiles
- ECOM-14: Implement RBAC
```

### Flujo de Épica

```
1. PLANNING (Semana anterior)
   ├─ PM define objetivo de negocio
   ├─ Tech Lead estima esfuerzo
   ├─ Crear en Jira con descripción
   └─ Status: TODO

2. DISCOVERY (Track 1)
   ├─ Crear subtareas de análisis
   ├─ Escribir especificación
   ├─ Diseñar arquitectura
   ├─ Stakeholder review
   └─ Status: SPEC_APPROVED

3. REFINEMENT
   ├─ Crear historias child detalladas
   ├─ Estimación de cada historia
   ├─ Asignar a sprints
   └─ Status: READY_FOR_DEVELOPMENT

4. IMPLEMENTATION (Track 2)
   ├─ Desarrolladores implementan
   ├─ Code reviews
   ├─ Testing
   └─ Status: IN_DEVELOPMENT

5. VALIDATION (Track 3)
   ├─ QA testing completo
   ├─ Performance testing
   ├─ Deployment a staging
   └─ Status: READY_FOR_PRODUCTION

6. DEPLOYMENT
   ├─ Production deployment
   ├─ Monitoring setup
   ├─ Post-deployment validation
   └─ Status: DONE ✅

7. POST-RELEASE (Optional)
   ├─ Retrospective
   ├─ Performance analysis
   ├─ Lessons learned
   └─ Status: CLOSED
```

---

## 📖 HISTORIAS - Guía Completa

### Qué es una Historia

- **Funcionalidad específica desde perspectiva del usuario**
- **Tamaño mediano: 5-13 puntos de historia**
- **Completable en 2-4 días de trabajo**
- **Child de una Épica**

### Cuándo Crear

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

### Estructura Recomendada (Gherkin)

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

## 📊 Información de la Historia

| Campo            | Valor                           |
| ---------------- | ------------------------------- |
| **Epic Link**    | ECOM-1 - User Management System |
| **Story Points** | 8                               |
| **Priority**     | HIGH                            |
| **Type**         | Story                           |
| **Sprint**       | Sprint 1                        |

## 📚 Especificación Técnica

**Archivo SDD**: docs/02-architecture.md#auth-registration

**Endpoints**:

- `POST /api/auth/register` - Create new user account
- `GET /api/auth/verify-email/{token}` - Verify email

**Database**:

- Table: `users`
- Fields: id, email, password_hash, created_at, verified_at
- Constraint: unique(email)

## ✅ Definition of Done (Story)

- [ ] Endpoint POST /api/auth/register implementado
- [ ] Validación de email y contraseña funciona
- [ ] Email de verificación se envía correctamente
- [ ] Unit tests: 80%+ coverage
- [ ] Integration tests: Todos scenarios pasan
- [ ] Code review aprobado por 2 devs
- [ ] SDD compliance: 100%
- [ ] Documentación API actualizada

```

### Flujo de Historia

```

1. CREATION
   ├─ PM crea historia en Jira
   ├─ Escribir user story completa
   ├─ Definir acceptance criteria
   └─ Status: BACKLOG

2. REFINEMENT (Sprint Planning)
   ├─ Tech Lead estima story points
   ├─ Asignar a desarrollador
   ├─ Crear branch feat/JIRA-XXX
   └─ Status: READY_FOR_DEVELOPMENT

3. DEVELOPMENT
   ├─ Developer crea rama
   ├─ Implementa feature
   ├─ Escribe tests (80%+ coverage)
   ├─ Commit regularmente
   └─ Status: IN_DEVELOPMENT

4. CODE REVIEW
   ├─ Crear Pull Request
   ├─ Assign 2 reviewers
   ├─ Responder comments
   ├─ Fix requested changes
   └─ Status: IN_REVIEW

5. APPROVAL
   ├─ 2+ reviewers aprueban
   ├─ All CI/CD checks pasan
   ├─ Merge a develop
   └─ Status: APPROVED

6. TESTING
   ├─ QA ejecuta test scenarios
   ├─ Testing en staging env
   ├─ Performance check
   ├─ Regression testing
   └─ Status: TESTED

7. DEPLOYMENT
   ├─ Deploy a producción
   ├─ Health checks
   ├─ Monitoring activado
   └─ Status: DONE ✅

8. CLOSE
   ├─ Resolver comentarios finales
   ├─ Actualizar docs
   └─ Status: CLOSED

```

---

## 📋 TAREAS - Guía Completa

### Qué es una Tarea

- **Trabajo técnico o administrativo sin valor directo del usuario**
- **Tamaño pequeño: 2-5 puntos de historia**
- **No tiene "user story" - es actividad técnica**
- **Puede ser independiente o subtarea de historia**

### Cuándo Crear

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

### Estructura Recomendada

```markdown
# INFRA-23 - Setup PostgreSQL Database for Production

## 📋 Descripción
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

## ✅ Definition of Done (Task)
- [ ] Base de datos creada y accesible
- [ ] Backups funcionando y testeados
- [ ] Monitoring alertas configuradas
- [ ] Runbook de recuperación escrito
- [ ] Security audit completado
- [ ] Dev/staging/prod pueden conectarse
- [ ] Documentation actualizada
````

### Flujo de Tarea

```
1. IDENTIFICATION
   ├─ Tech Lead identifica necesidad
   ├─ Crear tarea con descripción
   ├─ Estimar puntos de historia
   └─ Status: TODO

2. ASSIGNMENT
   ├─ Asignar a developer/DevOps
   ├─ Comunicar urgencia/prioridad
   └─ Status: ASSIGNED

3. EXECUTION
   ├─ Crear rama si es código
   ├─ Ejecutar tarea según descripción
   ├─ Documentar pasos
   └─ Status: IN_PROGRESS

4. VERIFICATION
   ├─ Revisar checklist completado
   ├─ Testing de cambios
   ├─ Code review si aplica
   └─ Status: REVIEW

5. CLOSURE
   ├─ Actualizar documentación
   ├─ Communicar completion
   ├─ Resolver follow-up issues
   └─ Status: DONE ✅
```

---

## 🐛 BUGS - Guía Completa

### Qué es un Bug

- **Problema o comportamiento incorrecto en sistema existente**
- **Descripción clara del problema + pasos para reproducir**
- **Prioridad basada en impacto**
- **Puede tener severidad diferente de prioridad**

### Cuándo Crear

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

### Estructura Recomendada

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
- opacity: 0.5, cursor: not-allowed
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
```
````

### 🔍 Información Técnica

**Environment Details:**

- Firefox Version: 121.0
- OS: Ubuntu 22.04 LTS
- App Version: v1.2.3

**Related Code Files:**

- frontend/src/pages/Register.tsx
- frontend/src/components/Form/FormValidator.js (línea 45)
- frontend/src/styles/register.css

### 📚 Especificación Vinculada

- **Requirements**: docs/01-requirements.md#registration-ui
- **Component Spec**: docs/10-component-architecture.md#form-components

### 👥 Información del Reporter

| Campo             | Valor               |
| ----------------- | ------------------- |
| **Reporter**      | qa-team@company.com |
| **Found In**      | Production          |
| **Date Reported** | 2024-12-16 10:30 AM |

### 📊 Impact Analysis

**Affected Users**: ~35% (Firefox market share)

**Business Impact**:

- Cannot register on Firefox
- Loss of potential customers
- Support tickets increasing

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

```

### Flujo de Bug

```

1. REPORTING
   ├─ QA/User reporta bug
   ├─ Crear issue con detalles
   ├─ Agregar screenshots/videos
   └─ Status: NEW

2. TRIAGE
   ├─ Tech Lead revisa reproducibilidad
   ├─ Asignar severidad & prioridad
   ├─ Asignar investigador
   └─ Status: TRIAGED

3. INVESTIGATION
   ├─ Dev reproduce el bug
   ├─ Identificar root cause
   ├─ Documentar findings
   └─ Status: INVESTIGATING

4. FIX IMPLEMENTATION
   ├─ Crear rama fix/JIRA-XXX
   ├─ Implementar solución
   ├─ Escribir regression tests
   ├─ Commit con referencia a issue
   └─ Status: IN_PROGRESS

5. CODE REVIEW
   ├─ Crear PR
   ├─ Assign 2 reviewers
   ├─ Responder feedback
   ├─ Approvals obtenidos
   └─ Status: REVIEW

6. TESTING
   ├─ QA reproduce con fix
   ├─ Test en todos browsers/OS
   ├─ Regression testing
   ├─ Performance check
   └─ Status: TESTING

7. DEPLOYMENT
   ├─ Merge a develop
   ├─ Deploy a staging
   ├─ Final QA check
   ├─ Deploy a producción
   └─ Status: DEPLOYED

8. VERIFICATION
   ├─ Monitor logs por errores
   ├─ 24h monitoring
   ├─ QA final verification
   └─ Status: VERIFIED ✅

9. CLOSURE
   ├─ Actualizar documentación
   ├─ Link a related issues
   ├─ Lessons learned
   └─ Status: CLOSED

````

---

## 🌳 Niveles de Detalle Recomendados

### Nivel 1: Mínimo Requerido

```markdown
# [TIPO] [ID] - [Título]

## Descripción
[1-2 párrafos explicando qué se necesita]

## Acceptance Criteria
- [ ] Item 1
- [ ] Item 2

## Status
[Current status]
````

### Nivel 2: Estándar (Recomendado)

```markdown
# [TIPO] [ID] - [Título]

## Descripción

[Completa]

## Objetivo

[Qué se quiere lograr]

## Acceptance Criteria

[Detallados, idealmente en Gherkin para historias]

## Especificación Vinculada

[Links a docs/]

## Definition of Done

[Checklist]

## Relaciones

[Blocker For, Depends On, Related To]

## Estimación

[Story points/Tiempo]
```

### Nivel 3: Completo (Para issues críticas)

```markdown
# [TIPO] [ID] - [Título]

## Descripción

[Muy detallada]

## Contexto

[Antecedentes]

## Objetivo & Beneficios

[Explícito]

## Acceptance Criteria

[Exhaustivos]

## Especificación Técnica

[Detalles de implementación]

## Especificación Vinculada

[Links a docs/]

## Definition of Done

[Exhaustivo]

## Relaciones

[Todas las conexiones]

## Información Técnica

[Arquitectura, dependencias]

## Evidencia (si aplica)

[Screenshots, videos, logs]

## Estimación & Timeline

[Detallada]

## Riesgos & Mitigaciones

[Explícitos]

## Preguntas Abiertas

[Si las hay]
```

---

## 💡 Tips Prácticos

### Tip 1: Nomenclatura de Ramas

```
Analysis:       analysis/JIRA-XXX-descriptive-name
Feature:        feat/JIRA-XXX-descriptive-name
Bug Fix:        fix/JIRA-XXX-issue-description
Hotfix:         hotfix/JIRA-XXX-critical-issue
Refactor:       refactor/JIRA-XXX-component-name
Task:           task/JIRA-XXX-task-name
```

### Tip 2: Nomenclatura de Commits

```
feat(PROJ-123): Implement user authentication

- Add JWT token generation
- Implement refresh token rotation
- Add role-based access control

Spec: docs/02-architecture.md#security
Tests: 85% coverage
Fixes: PROJ-123

---

fix(PROJ-150): Fix button disabled state in Firefox

- Add matchMedia polyfill for Firefox compatibility
- Update form validation logic
- Add regression tests

Fixes: PROJ-150
Spec: docs/02-architecture.md#form-validation
```

### Tip 3: Evitar Anti-patrones

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

### Tip 4: Revisar Antes de Crear

```
CHECKLIST PREVIO A CREACIÓN:

Para ÉPICAS:
- [ ] ¿Tiene 3+ historias relacionadas?
- [ ] ¿Suma > 20 story points?
- [ ] ¿Existe una especificación clara?
- [ ] ¿Hay soporte de negocio?

Para HISTORIAS:
- [ ] ¿Es una feature visible al usuario?
- [ ] ¿Puedo completarla en 2-4 días?
- [ ] ¿Está linked a una épica?
- [ ] ¿Son claros los acceptance criteria?

Para TAREAS:
- [ ] ¿Es trabajo técnico puro?
- [ ] ¿No beneficia directamente al usuario?
- [ ] ¿Cabe en 1-2 días?
- [ ] ¿Hay un propósito claro?

Para BUGS:
- [ ] ¿Es reproducible?
- [ ] ¿Tengo pasos exactos?
- [ ] ¿Afecta usuarios reales?
- [ ] ¿Es un problema actual, no feature?
```

---

## 📚 Referencias Cruzadas

Ver también:

- [Guía de Integración SDD + Jira](jira-integration-guide.md)
- [Metodología de Trabajo](../shared/00-metodologia-trabajo.md)
- [Requisitos](../shared/01-requirements.md)
- [Arquitectura](../shared/02-architecture.md)

---

**Versión**: 1.0.0  
**Última actualización**: 16 de diciembre de 2024  
**Status**: ✅ Completado  
**Mantenedor**: [EQUIPO/PERSONA]
