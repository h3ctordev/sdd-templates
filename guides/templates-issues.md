# 📋 Templates para Issues en Jira

> Plantillas listas para copiar/pegar en Jira para Épicas, Historias, Tareas y Bugs

**Versión**: 1.0.0  
**Fecha**: 16 de diciembre de 2024  
**Propósito**: Proporcionar templates estándar para crear issues de calidad

---

## 📌 TEMPLATE - ÉPICA

### Cómo usar este template:

1. Copiar el contenido completo
2. Abrir Jira y crear una nueva Épica
3. Pegar el contenido en el campo Description
4. Rellenar los [PLACEHOLDERS] con tu información
5. Guardar

---

```markdown
# [NOMBRE DE LA ÉPICA]

## 📋 Descripción / Description

[DESCRIPCIÓN COMPLETA DE LA ÉPICA - 2-3 párrafos explicando el contexto y objetivo]

**Objetivo de Negocio**:
[QUÉ SE QUIERE LOGRAR DESDE LA PERSPECTIVA DEL NEGOCIO]

**Beneficio Esperado**:
[BENEFICIO PARA LOS USUARIOS FINALES O LA ORGANIZACIÓN]

## 🎯 Alcance / Scope

### Incluido (In Scope)

- [ ] [Feature 1 a implementar]
- [ ] [Feature 2 a implementar]
- [ ] [Feature 3 a implementar]
- [ ] [Feature 4 a implementar]

### Excluido (Out of Scope)

- [ ] [Característica futura - fase 2]
- [ ] [Característica no prioritaria]

## 📊 Estimación y Timeline

| Elemento                  | Valor                                    |
| ------------------------- | ---------------------------------------- |
| **Story Points Totales**  | [XX] puntos                              |
| **Duración Estimada**     | [X-X] semanas                            |
| **Equipo Recomendado**    | [X-X] desarrolladores                    |
| **Dependencias Externas** | [Listar dependencias críticas o NINGUNA] |

## 📚 Especificación Vinculada / Linked Specification

- **Requirements**: [Link a docs/01-requirements.md#section]
- **Architecture**: [Link a docs/02-architecture.md#section]
- **Data Models**: [Link a docs/02-architecture.md#data-models]
- **Project Structure**: [Link a docs/07-project-structure-*.md]

## ✅ Definition of Done (Epic Level)

- [ ] Todas las historias child han sido completadas y marcadas como DONE
- [ ] Especificación técnica completamente documentada en docs/
- [ ] Arquitectura revisada y aprobada por Tech Lead
- [ ] 80%+ de cobertura de tests en todas las historias
- [ ] Documentación de usuario (si aplica) actualizada
- [ ] API documentation completada (si aplica)
- [ ] Deployment a staging ambiente completado exitosamente
- [ ] Production deployment completado
- [ ] Monitoring y alertas configuradas
- [ ] Post-release validation exitosa

## 🔗 Child Stories / Historias Relacionadas

- [ ] [JIRA-XXX: Descripción de historia 1]
- [ ] [JIRA-XXX: Descripción de historia 2]
- [ ] [JIRA-XXX: Descripción de historia 3]
- [ ] [JIRA-XXX: Descripción de historia 4]

## 🗂️ Dependencias y Bloqueadores

**Depende de (Depends On):**

- JIRA-YYY: [Descripción de dependency]

**Bloquea (Blocks):**

- JIRA-ZZZ: [Descripción de qué bloquea]

**Relacionado con (Related To):**

- JIRA-AAA: [Descripción]

## 📝 Aceptación de Negocio / Business Acceptance

- [ ] Product Owner revisó y aprobó la especificación
- [ ] Stakeholders validaron los requisitos de negocio
- [ ] Criterios de éxito de negocio definidos y aceptados

## 👥 Información de Asignación

| Campo            | Valor                     |
| ---------------- | ------------------------- |
| **Epic Owner**   | [Nombre/Email]            |
| **Tech Lead**    | [Nombre/Email]            |
| **Primary Team** | [Nombre del equipo]       |
| **Stakeholders** | [Nombres de stakeholders] |

## 🚨 Riesgos y Mitigación

| Riesgo     | Probabilidad    | Impacto         | Mitigación           |
| ---------- | --------------- | --------------- | -------------------- |
| [Riesgo 1] | Alto/Medio/Bajo | Alto/Medio/Bajo | [Plan de mitigación] |
| [Riesgo 2] | Alto/Medio/Bajo | Alto/Medio/Bajo | [Plan de mitigación] |

## 📝 Notas y Contexto Adicional

[Cualquier información adicional, decisiones clave, o contexto que sea importante para el equipo]

## 🏷️ Labels / Etiquetas

`backend` `frontend` `critical` `[AGREGAR MÁS SEGÚN SEA NECESARIO]`

## 📍 Componentes Afectados

- [Nombre del componente 1]
- [Nombre del componente 2]
- [Nombre del componente 3]
```

---

## 📖 TEMPLATE - HISTORIA (USER STORY)

### Cómo usar este template:

1. Copiar el contenido completo
2. Abrir Jira y crear una nueva Story
3. Pegar el contenido en el campo Description
4. Rellenar los [PLACEHOLDERS]
5. Estimar en story points
6. Asignar a Sprint
7. Guardar

---

````markdown
# [TÍTULO DE LA HISTORIA]

## 📖 Historia de Usuario / User Story

Como **[ROL DEL USUARIO]**
Quiero **[QUÉ ACCIÓN DESEA REALIZAR]**
Para que **[BENEFICIO O VALOR QUE OBTIENE]**

## 🎯 Acceptance Criteria (Gherkin Format)

### Scenario 1: [Descripción del scenario exitoso]

```gherkin
Given [Condición inicial]
When [Acción que realiza el usuario]
And [Acción adicional si aplica]
Then [Resultado esperado]
And [Resultado adicional si aplica]
```
````

### Scenario 2: [Descripción de edge case]

```gherkin
Given [Condición inicial]
When [Acción que realiza el usuario]
Then [Resultado esperado]
```

### Scenario 3: [Descripción de caso de error]

```gherkin
Given [Condición inicial]
When [Acción que realiza el usuario]
Then [Mensaje de error esperado]
And [Comportamiento adicional esperado]
```

## 📊 Información de la Historia

| Campo            | Valor                           |
| ---------------- | ------------------------------- |
| **Epic Link**    | [JIRA-XXX - Nombre de la épica] |
| **Story Points** | [5-13]                          |
| **Priority**     | HIGH / MEDIUM / LOW             |
| **Type**         | Story                           |
| **Sprint**       | [Nombre del sprint]             |

## 📚 Especificación Técnica / Technical Specification

### Endpoints (si aplica)

```
[GET/POST/PUT/DELETE] /api/v1/[endpoint]
[GET/POST/PUT/DELETE] /api/v1/[endpoint]
```

### Database Changes (si aplica)

**New Tables:**

- `[table_name]` - [descripción]
  - `id` (PK)
  - `[field1]` ([type])
  - `[field2]` ([type])

**Modified Tables:**

- `[existing_table]` - [cambios a realizar]

**Constraints:**

- `unique([field1])`
- `foreign_key([field2])`

### Technical Details

- [Detalle técnico 1]
- [Detalle técnico 2]
- [Detalle técnico 3]

### Non-Functional Requirements

- Performance: [Requerimiento de performance si aplica]
- Security: [Requerimiento de seguridad]
- Scalability: [Requerimiento de escalabilidad]

## 📚 Especificación Vinculada / Linked Specification

- **Requirements**: [Link a docs/01-requirements.md#section]
- **Architecture**: [Link a docs/02-architecture.md#section]
- **Component Architecture**: [Link a docs/10-component-architecture.md#section]

## ✅ Definition of Done (Story Level)

### Development

- [ ] Código implementado en rama feat/[JIRA-XXX-description]
- [ ] Commits significativos con mensajes descriptivos
- [ ] Código sigue los estándares del proyecto
- [ ] No hay TODOs sin resolver en el código

### Testing

- [ ] Unit tests escritos (80%+ code coverage)
- [ ] Integration tests para happy path
- [ ] Edge cases testeados
- [ ] Manual testing completado localmente

### Code Quality

- [ ] Code review aprobado por 2+ desarrolladores
- [ ] Linting/formatting pasando sin errores
- [ ] SonarQube / Static analysis sin issues críticos
- [ ] No hay warnings sin explicación

### Documentation

- [ ] Documentación técnica actualizada
- [ ] API documentation (Swagger/OpenAPI) actualizada
- [ ] Changelog entry creado
- [ ] Screenshots/videos agregados si UI changes

### Integration

- [ ] Merged a rama develop
- [ ] CI/CD pipeline completado exitosamente
- [ ] Deployed a staging environment
- [ ] Health checks en staging pasando

## 🔗 Relaciones

**Depende de (Depends On):**

- [ ] [JIRA-XXX: Descripción]

**Bloquea (Blocks):**

- [ ] [JIRA-XXX: Descripción]

**Relacionado con (Related To):**

- [ ] [JIRA-XXX: Descripción]

## 🚀 Criterios de Aceptación de Negocio

- [ ] Funcionalidad funciona como se describe en AC
- [ ] No hay regressions en funcionalidad relacionada
- [ ] Performance es aceptable
- [ ] UX es intuitivo y accesible

## 👥 Información de Asignación

| Campo                   | Valor                        |
| ----------------------- | ---------------------------- |
| **Assignee**            | [Desarrollador principal]    |
| **Secondary Assignees** | [Pair programmers si aplica] |
| **Reviewers**           | [Tech lead + otro dev]       |

## 📝 Notas para el Desarrollador

[Notas específicas, tips de implementación, o contexto útil]

## 🏷️ Labels

`backend` `frontend` `database` `api` `[AGREGAR SEGÚN SEA NECESARIO]`

````

---

## 📋 TEMPLATE - TAREA (TASK)

### Cómo usar este template:
1. Copiar el contenido completo
2. Abrir Jira y crear una nueva Task
3. Pegar el contenido en el campo Description
4. Rellenar los [PLACEHOLDERS]
5. Estimar en story points
6. Guardar

---

```markdown
# [TÍTULO DE LA TAREA]

## 📋 Descripción / Description

[DESCRIPCIÓN CLARA Y CONCISA DE LA TAREA TÉCNICA]

**Objetivo:**
[QUÉ SE QUIERE LOGRAR]

**Impacto:**
[CÓMO IMPACTA AL PROYECTO/EQUIPO]

## 🎯 Objetivo y Justificación

### Por qué se necesita esta tarea:
- [Razón 1]
- [Razón 2]
- [Razón 3]

### Beneficios esperados:
- [Beneficio 1]
- [Beneficio 2]

## 📊 Información de la Tarea

| Campo | Valor |
|-------|-------|
| **Type** | Task |
| **Story Points** | [2-5] |
| **Priority** | CRITICAL / HIGH / MEDIUM / LOW |
| **Epic Link** | [JIRA-XXX - Épica si aplica] |

## ✅ Checklist de Items

### Fase 1: Preparación
- [ ] [Item 1 a completar]
- [ ] [Item 2 a completar]
- [ ] [Item 3 a completar]

### Fase 2: Ejecución
- [ ] [Item 1 a completar]
- [ ] [Item 2 a completar]
- [ ] [Item 3 a completar]

### Fase 3: Validación
- [ ] [Item 1 a completar]
- [ ] [Item 2 a completar]
- [ ] [Item 3 a completar]

### Fase 4: Finalización
- [ ] [Item 1 a completar]
- [ ] [Item 2 a completar]

## 📚 Documentación Técnica

### Requerimientos Técnicos
- [Requerimiento 1]
- [Requerimiento 2]
- [Requerimiento 3]

### Pasos Detallados (si aplica)

1. [Paso 1 - Descripción]
   - Sub-paso 1a
   - Sub-paso 1b

2. [Paso 2 - Descripción]
   - Sub-paso 2a
   - Sub-paso 2b

3. [Paso 3 - Descripción]

### Configuración Requerida (si aplica)

````

[Configuración 1]
[Configuración 2]
[Configuración 3]

````

### Comandos (si aplica)

```bash
# Comando 1 - Descripción
command1

# Comando 2 - Descripción
command2

# Comando 3 - Descripción
command3
````

## ✅ Definition of Done (Task Level)

- [ ] Todos los items del checklist completados
- [ ] Checklist 100% verificado
- [ ] Documentación de la tarea actualizada
- [ ] Screenshots/evidencia agregados si aplica
- [ ] Notificación enviada a stakeholders interesados
- [ ] Follow-up issues creadas si se identifica trabajo adicional
- [ ] Task marcada como DONE

## 📋 Criterios de Validación

- [ ] [Criterio 1]
- [ ] [Criterio 2]
- [ ] [Criterio 3]

## 🔗 Relaciones

**Depende de (Depends On):**

- [ ] [JIRA-XXX: Descripción]

**Bloquea (Blocks):**

- [ ] [JIRA-XXX: Descripción]

**Relacionado con (Related To):**

- [ ] [JIRA-XXX: Descripción]

## 🚨 Riesgos y Consideraciones

| Riesgo     | Probabilidad    | Mitigación   |
| ---------- | --------------- | ------------ |
| [Riesgo 1] | Alto/Medio/Bajo | [Mitigación] |
| [Riesgo 2] | Alto/Medio/Bajo | [Mitigación] |

## 📝 Notas Importantes

[Cualquier nota, contexto importante, o consideraciones especiales]

## 🏷️ Labels

`infrastructure` `devops` `database` `configuration` `[AGREGAR SEGÚN SEA NECESARIO]`

## 👥 Asignación

| Campo        | Valor                   |
| ------------ | ----------------------- |
| **Assignee** | [Responsable principal] |
| **Reviewer** | [Revisor técnico]       |

````

---

## 🐛 TEMPLATE - BUG

### Cómo usar este template:
1. Copiar el contenido completo
2. Abrir Jira y crear un nuevo Bug
3. Pegar el contenido en el campo Description
4. Rellenar todos los [PLACEHOLDERS] con información específica
5. Adjuntar screenshots/videos
6. Asignar prioridad según severidad
7. Guardar

---

```markdown
# [TÍTULO DESCRIPTIVO DEL BUG]

## 🐛 Reporte de Bug

### 📝 Resumen

[DESCRIPCIÓN CONCISA DEL PROBLEMA - 1-2 frases]

### 📊 Severidad y Prioridad

| Atributo | Valor |
|----------|-------|
| **Severity** | 🔴 CRITICAL / 🟠 HIGH / 🟡 MEDIUM / 🔵 LOW |
| **Priority** | BLOCKER / CRITICAL / HIGH / MEDIUM / LOW |
| **Affected Users** | [Número aproximado o %] |
| **Environment** | Production / Staging / Development |

### 🔴 Impacto de Negocio

[Descripción del impacto en los usuarios finales o negocio]
- [Impacto 1]
- [Impacto 2]
- [Impacto 3]

## 🔄 Pasos para Reproducir

### Precondiciones (Entorno necesario):
- Browser: [Navegador y versión si aplica]
- OS: [Sistema operativo y versión]
- URL: [URL específica]
- Usuario: [Tipo de usuario - autenticado/no autenticado]
- Otros: [Otras precondiciones]

### Pasos Exactos:

1. [Paso 1 - Descripción clara]
2. [Paso 2 - Descripción clara]
3. [Paso 3 - Descripción clara]
4. [Paso 4 - Acción que genera el bug]

### Resultado Esperado:
[QUÉ DEBERÍA SUCEDER]

### Resultado Actual:
[QUÉ SUCEDE EN REALIDAD - EL BUG]

## 📸 Evidencia

### Screenshots

- **Screenshot 1**: [Descripción] - [Link o imagen adjunta]
- **Screenshot 2**: [Descripción] - [Link o imagen adjunta]

### Video de Reproducción

- [Link al video o video adjunto]

### Console Errors / Logs

````

[Error logs del navegador, servidor, o sistema]
[Stack trace si aplica]

```

## 🖥️ Información del Ambiente

| Dato | Valor |
|------|-------|
| **Browser** | [Navegador y versión exacta] |
| **OS** | [Sistema operativo y versión] |
| **Device** | [Desktop/Mobile - modelo si aplica] |
| **App Version** | [Versión de la aplicación] |
| **Timestamp** | [Fecha y hora exacta en que ocurrió] |

### Browser DevTools Information

```

User Agent: [Copiar de DevTools]
LocalStorage: [Si relevante]
Cookies: [Si relevante]
Network: [Si relevante]

````

## 📚 Especificación Vinculada

- **Related Feature**: [JIRA-XXX - Descripción]
- **Requirements**: [Link a docs/01-requirements.md#section]
- **Architecture**: [Link a docs/02-architecture.md#section]
- **Component**: [Link a docs/10-component-architecture.md#section]

## 🔗 Relaciones

**Related Issues:**
- [ ] [JIRA-XXX: Descripción - Similar bug]
- [ ] [JIRA-XXX: Descripción - Related feature]

**Blocks (Si bloquea a otros):**
- [ ] [JIRA-XXX: Descripción]

**Depends On:**
- [ ] [JIRA-XXX: Descripción - Fix necesario antes]

## 🔍 Información Técnica

### Archivos Afectados

- `[ruta/archivo1.js]`
- `[ruta/archivo2.tsx]`
- `[ruta/archivo3.css]`

### Línea de Código Problemática

```javascript
// En [archivo.js] línea XX
var problemático = "código aquí";
````

### Hipótesis de Root Cause

[Descripción de la posible causa raíz del bug]

### Componentes Afectados

- [Componente 1]
- [Componente 2]
- [Componente 3]

## 📊 Frecuencia del Bug

- [ ] **Siempre**: Ocurre cada vez que se reproduce
- [ ] **Intermitente**: Ocurre a veces
- [ ] **Específico**: Solo bajo ciertas condiciones

**Condiciones específicas (si aplica):**
[Describir cuándo ocurre específicamente]

## 🔄 Workaround (Solución Temporal)

[Si existe una forma de evitar el bug temporalmente, describirla]

Si no existe: No hay workaround disponible

## ✅ Definition of Done (Bug Fix)

### Investigation

- [ ] Root cause identificado y documentado
- [ ] Hipótesis confirmada mediante testing
- [ ] Componentes afectados identificados

### Fix Implementation

- [ ] Fix implementado en rama fix/[JIRA-XXX-description]
- [ ] Regression tests agregados
- [ ] Fix testeado localmente
- [ ] Testeado en múltiples browsers/OS si aplica

### Code Review

- [ ] Pull Request creado
- [ ] Code review aprobado por 2+ developers
- [ ] Todos los comentarios resueltos
- [ ] CI/CD checks pasando

### Testing

- [ ] QA reproduce el bug con fix
- [ ] Bug no se reproduce con fix
- [ ] Regression testing completado
- [ ] Performance impact verificado

### Deployment

- [ ] Fix merged a develop
- [ ] Deployed a staging environment
- [ ] Final QA verification en staging
- [ ] Deployed a production
- [ ] Health checks en production pasando

### Post-Deployment

- [ ] Monitoreado por 24h
- [ ] Logs monitoreados por errores relacionados
- [ ] Usuarios notificados si fue critico
- [ ] Bug marcado como DONE

## 👥 Información del Reporte

| Campo                | Valor                               |
| -------------------- | ----------------------------------- |
| **Reporter**         | [Nombre/Email de quien reporta]     |
| **Found In**         | Production / Staging / Development  |
| **Date Reported**    | [Fecha y hora]                      |
| **First Occurrence** | [Cuándo se observó por primera vez] |
| **Last Verified**    | [Cuándo se verificó por última vez] |

## 🏷️ Labels

`bug` `critical` `frontend` `backend` `ui` `performance` `[AGREGAR SEGÚN SEA NECESARIO]`

## 📝 Notas Adicionales

[Cualquier información adicional o contexto importante para el equipo de fix]

```

---

## 🎨 Cómo Personalizar los Templates

### 1. Reemplazar Placeholders

Todos los `[PLACEHOLDERS]` deben ser reemplazados con tu información específica:

```

[TEXTO AQUÍ] → Tu texto específico
[JIRA-XXX] → Tu ID de Jira real
[Link] → URL real

```

### 2. Adaptar a tu Contexto

- Eliminar secciones que no apliquen
- Agregar secciones específicas de tu proyecto
- Ajustar labels según tu taxonomía de Jira
- Modificar campos según tu workflow

### 3. Guardar como Templates en Jira

Para hacer estos templates reutilizables en Jira:

1. Ir a Jira → Settings → Screens
2. Crear una pantalla personalizada con estos campos
3. Crear esquemas de issuetype que usen estos templates
4. Asignar a tu proyecto

---

## 📋 Comparativa: Qué Template Usar

| Situación | Template |
|-----------|----------|
| Iniciativa de negocio grande (3+ historias) | **ÉPICA** |
| Feature visible al usuario (5-13 pts) | **HISTORIA** |
| Trabajo técnico puro (2-5 pts) | **TAREA** |
| Problema existente a reparar | **BUG** |

---

## 🚀 Quick Start - Usar un Template

### Para Épica:
```

1. Copiar template de ÉPICA
2. Reemplazar [PLACEHOLDERS] con tu info
3. Crear Épica en Jira
4. Pegar contenido
5. Agregar historias child

```

### Para Historia:
```

1. Copiar template de HISTORIA
2. Rellenar user story (Como... Quiero... Para...)
3. Escribir scenarios en Gherkin
4. Pegar en Jira
5. Estimar y asignar

```

### Para Tarea:
```

1. Copiar template de TAREA
2. Describir qué hacer
3. Crear checklist
4. Pegar en Jira
5. Asignar responsable

```

### Para Bug:
```

1. Copiar template de BUG
2. Describir problema exactamente
3. Adjuntar screenshots
4. Pegar en Jira
5. Setear severidad/prioridad

```

---

## 💡 Tips de Mejor Uso

### ✅ HACER:
- Rellenar todos los campos relevantes
- Ser específico y descriptivo
- Adjuntar evidencia (screenshots, videos)
- Vincular a especificaciones
- Usar Markdown para formato

### ❌ NO HACER:
- Dejar placeholders vacíos
- Ser vago o ambiguo
- Omitir información crítica
- Mezclar multiple issues en uno
- Ignorar el Definition of Done

---

## 📚 Archivos Relacionados

Para más información sobre estos templates, consulta:

- [best-practices-issues.md](best-practices-issues.md) - Guía completa
- [jira-integration-guide.md](jira-integration-guide.md) - Integración SDD
- [README.md](README.md) - Índice de todas las guías

---

**Versión**: 1.0.0
**Última actualización**: 16 de diciembre de 2024
**Status**: ✅ Listo para usar
**Mantenedor**: [EQUIPO/PERSONA]
```
