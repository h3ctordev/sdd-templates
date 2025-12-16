# 📖 Índice de Guías - Mejores Prácticas para Issues en Jira

> Documentación completa y estructurada sobre cómo crear y especificar historias, épicas, tareas y bugs

**Fecha de Actualización**: 16 de diciembre de 2024  
**Versión**: 1.0.0

---

## 📚 Estructura de Documentos

### 📍 ACCESO RÁPIDO A TEMPLATES

**⭐ [templates-issues.md](templates-issues.md)** - **COPIAR Y PEGAR DIRECTAMENTE EN JIRA**

- Template de ÉPICA - Listo para usar
- Template de HISTORIA - Con Gherkin scenarios
- Template de TAREA - Con checklist
- Template de BUG - Con pasos de reproducción

---

### 1. 📋 **[best-practices-issues.md](best-practices-issues.md)** (24 KB)

**Guía completa y detallada sobre cada tipo de issue**

#### Contenido:

✅ **Tabla Comparativa** (Épicas vs Historias vs Tareas vs Bugs)

- 11 criterios de comparación
- Diferencias de tamaño, duración, valor, perspectiva
- Matriz rápida de referencia

✅ **Matriz de Decisión** (¿Qué tipo de issue crear?)

- Árbol de decisiones paso a paso
- 4 preguntas clave
- Casos especiales

✅ **Checklists de Calidad** (18 checklists en total)

- Para cada tipo de issue
- Fases: ANTES/CREAR/DURANTE/COMPLETAR
- Validaciones exhaustivas

✅ **Guía ÉPICAS** (Completa)

- Definición y cuándo crear
- Estructura recomendada + ejemplo real (ECOM-1)
- 7 fases de lifecycle
- 4 checklists especializados

✅ **Guía HISTORIAS** (Completa)

- Definición y cuándo crear
- Estructura con Gherkin scenarios
- Ejemplo real (ECOM-10)
- 8 fases de lifecycle
- 5 checklists especializados

✅ **Guía TAREAS** (Completa)

- Definición y cuándo crear
- Estructura técnica
- Ejemplo real (INFRA-23)
- 5 fases de lifecycle
- 4 checklists especializados

✅ **Guía BUGS** (Completa)

- Definición y cuándo crear
- Estructura de bug report
- Ejemplo real (ECOM-150)
- 9 fases de lifecycle
- 6 checklists especializados

✅ **Niveles de Detalle** (3 niveles)

- Nivel 1: Mínimo requerido
- Nivel 2: Estándar (Recomendado)
- Nivel 3: Completo para issues críticas

✅ **Tips Prácticos**

- Nomenclatura de ramas
- Nomenclatura de commits
- 6 anti-patrones con soluciones
- Checklist previo a creación

---

### 2. 📋 **[jira-integration-guide.md](jira-integration-guide.md)** (56 KB)

**Guía integral de integración SDD + Jira para Dual Track**

#### Contenido Relevante:

✅ **Tabla de Contenidos Actualizada**

- Link a best-practices-issues.md
- Referencia a guía detallada

✅ **Introducción**

- Beneficios de SDD + Jira
- Conceptos clave
- Mapeo SDD ↔ Jira

✅ **Configuración de Jira**

- Estructura de proyectos
- Campos personalizados
- Estados del workflow
- Definition of Done

✅ **Workflow SDD + Dual Track**

- 3 fases de ejecución
- Flujo completo Track 1 + Track 2 + Track 3
- Diagrama visual del proceso

✅ **Múltiples Desarrolladores**

- Asignación y colaboración
- Pair programming
- Trabajo concurrente
- Gestión de conflictos

✅ **Restricciones y Limitaciones**

- Limitaciones de Jira
- Restricciones SDD + Jira
- Anti-patrones
- Curva de aprendizaje

✅ **Checklist de Implementación**

- Fase 1: Preparación
- Fase 2: Piloto
- Fase 3: Rollout
- Fase 4: Optimización continua

✅ **Ejemplo Completo**

- Proyecto E-Commerce
- 5 épicas de ejemplo
- Story completa (ECOM-10)
- Configuración real

---

### 3. 📋 **[CHANGELOG-ISSUES.md](CHANGELOG-ISSUES.md)** (8 KB)

**Resumen ejecutivo de cambios y nuevo contenido**

#### Contenido:

✅ Objetivo cumplido
✅ Archivos creados/modificados
✅ Contenido detallado
✅ Estadísticas del contenido
✅ Cómo usar la guía
✅ Próximos pasos sugeridos

---

## 🎯 Cómo Navegar

### 🚀 SI SOLO QUIERES TEMPLATES LISTOS PARA COPIAR/PEGAR:

👉 **Ir directamente a: [templates-issues.md](templates-issues.md)**

Contiene 4 templates completos y listos para usar:

- ÉPICA template
- HISTORIA template
- TAREA template
- BUG template

Solo copia, rellena los [PLACEHOLDERS], y pega en Jira.

---

### Si eres **Desarrollador**:

1. **Necesito crear un issue nuevo**
   → Leer [Matriz de Decisión](best-practices-issues.md#-matriz-de-decisión-qué-tipo-de-issue-crear) en best-practices-issues.md

2. **Necesito escribir una historia**
   → Leer [Guía HISTORIAS](best-practices-issues.md#-historias--guía-completa) en best-practices-issues.md

3. **Necesito reportar un bug**
   → Leer [Guía BUGS](best-practices-issues.md#-bugs--guía-completa) en best-practices-issues.md

4. **Quiero entender el flujo completo**
   → Leer [Workflow SDD + Dual Track](jira-integration-guide.md#-workflow-sdd--dual-track--workflow) en jira-integration-guide.md

---

### Si eres **Tech Lead**:

1. **Necesito validar issues antes de sprint**
   → Usar [Checklists de Calidad](best-practices-issues.md#-checklist-de-calidad-para-cada-tipo) en best-practices-issues.md

2. **Necesito revisar épicas**
   → Leer [Guía ÉPICAS](best-practices-issues.md#-épicas--guía-completa) en best-practices-issues.md

3. **Necesito revisar code contra SDD**
   → Ver [Definition of Done](jira-integration-guide.md#-definition-of-done-dod) en jira-integration-guide.md

4. **Necesito configurar Jira**
   → Leer [Configuración de Jira](jira-integration-guide.md#-configuración-de-jira--jira-setup) en jira-integration-guide.md

---

### Si eres **Product Manager**:

1. **Necesito crear una épica**
   → Leer [Guía ÉPICAS](best-practices-issues.md#-épicas--guía-completa) en best-practices-issues.md

2. **Necesito refinar historias**
   → Leer [Guía HISTORIAS](best-practices-issues.md#-historias--guía-completa) en best-practices-issues.md

3. **Necesito entender el flujo SDD**
   → Leer [Introducción](jira-integration-guide.md#-introducción--introduction) en jira-integration-guide.md

4. **Necesito ver ejemplos completos**
   → Leer [Ejemplo de Configuración Completa](jira-integration-guide.md#-ejemplo-de-configuración-completa--complete-configuration-example) en jira-integration-guide.md

---

### Si eres **QA/Tester**:

1. **Necesito reportar un bug bien**
   → Leer [Guía BUGS](best-practices-issues.md#-bugs--guía-completa) en best-practices-issues.md

2. **Necesito entender acceptance criteria**
   → Leer [Guía HISTORIAS](best-practices-issues.md#-historias--guía-completa) en best-practices-issues.md

3. **Necesito validar históricos**
   → Leer [Definition of Done](jira-integration-guide.md#-definition-of-done-dod) en jira-integration-guide.md

---

### Si eres **DevOps/Infrastructure**:

1. **Necesito crear una tarea técnica**
   → Leer [Guía TAREAS](best-practices-issues.md#-tareas--guía-completa) en best-practices-issues.md

2. **Necesito entender epic lifecycle**
   → Leer [Guía ÉPICAS](best-practices-issues.md#-épicas--guía-completa) en best-practices-issues.md

3. **Necesito ver ejemplo infraestructura**
   → Ver ejemplo INFRA-23 en [Guía TAREAS](best-practices-issues.md#-tareas--guía-completa)

---

## 📊 Contenido Resumido

### Épicas 📌

| Elemento       | Detalles                        |
| -------------- | ------------------------------- |
| **¿Qué es?**   | Iniciativa de negocio           |
| **Tamaño**     | 20-50 pts                       |
| **Duración**   | 4-12 semanas                    |
| **Ejemplo**    | ECOM-1 - User Management System |
| **Fases**      | 7 (PLANNING → POST-RELEASE)     |
| **Checklists** | 4                               |

---

### Historias 📖

| Elemento       | Detalles                              |
| -------------- | ------------------------------------- |
| **¿Qué es?**   | Feature específica del usuario        |
| **Tamaño**     | 5-13 pts                              |
| **Duración**   | 2-4 días                              |
| **Ejemplo**    | ECOM-10 - Implement User Registration |
| **Fases**      | 8 (CREATION → CLOSE)                  |
| **Checklists** | 5                                     |

---

### Tareas 📋

| Elemento       | Detalles                             |
| -------------- | ------------------------------------ |
| **¿Qué es?**   | Trabajo técnico puro                 |
| **Tamaño**     | 2-5 pts                              |
| **Duración**   | 1-2 días                             |
| **Ejemplo**    | INFRA-23 - Setup PostgreSQL Database |
| **Fases**      | 5 (IDENTIFICATION → CLOSURE)         |
| **Checklists** | 4                                    |

---

### Bugs 🐛

| Elemento       | Detalles                              |
| -------------- | ------------------------------------- |
| **¿Qué es?**   | Problema existente                    |
| **Tamaño**     | 1-5 pts                               |
| **Duración**   | 1-3 días                              |
| **Ejemplo**    | ECOM-150 - Button Disabled on Firefox |
| **Fases**      | 9 (REPORTING → CLOSURE)               |
| **Checklists** | 6                                     |

---

## 🔑 Características Principales

### ✅ Completitud

- **Tabla Comparativa**: 11 criterios
- **Ejemplos Reales**: 12 ejemplos detallados
- **Checklists**: 18 checklists exhaustivos
- **Diagramas**: 4 flujos visuales
- **Anti-patrones**: 6 errores comunes con soluciones

### ✅ Claridad

- Definiciones simples para cada tipo
- Matrices de decisión paso a paso
- Ejemplos reales y contextualizados
- Nomenclatura consistente
- Cross-links entre documentos

### ✅ Practicidad

- Listas de verificación actionables
- Ejemplos copiar-y-pegar
- Templates prontos para usar
- Flujos paso a paso
- Tips prácticos y atajos

### ✅ Escalabilidad

- Desde equipos pequeños hasta 100+ devs
- Agnóstico de metodología
- Agnóstico de tecnología
- Adaptable a diferentes contextos

---

## 🚀 Quick Start

### ⭐ OPCIÓN 1: Usar Templates Directamente (MÁS RÁPIDO)

👉 Ir a [templates-issues.md](templates-issues.md)

```
1. Copiar template del tipo de issue que necesitas
2. Abrir Jira y crear nuevo issue
3. Pegar contenido en Description
4. Rellenar [PLACEHOLDERS] con tu información
5. Guardar
```

**Tiempo**: 2-5 minutos

---

### OPCIÓN 2: Seguir Guía Completa (RECOMENDADO PARA APRENDER)

#### Paso 1: Leer Matriz de Decisión

Ubicación: [best-practices-issues.md - Matriz de Decisión](best-practices-issues.md#-matriz-de-decisión-qué-tipo-de-issue-crear)

#### Paso 2: Seleccionar Tipo de Issue

- ¿Problema? → **BUG** → [Template BUG](templates-issues.md#-template---bug)
- ¿Valor visible? → **HISTORIA** → [Template HISTORIA](templates-issues.md#-template---historia-user-story)
- ¿Técnico? → **TAREA** → [Template TAREA](templates-issues.md#-template---tarea-task)
- ¿3+ historias? → **ÉPICA** → [Template ÉPICA](templates-issues.md#-template---épica)

#### Paso 3: Leer Guía del Tipo Seleccionado

En [best-practices-issues.md](best-practices-issues.md):

- Definición y cuándo crear
- Estructura recomendada
- Ejemplo real
- Lifecycle completo
- Checklists

#### Paso 4: Usar Template Correspondiente

En [templates-issues.md](templates-issues.md):

- Copiar template
- Rellenar placeholders
- Pegar en Jira

#### Paso 5: Validar contra Checklist

Usar el checklist correspondiente para verificar:

- ANTES de crear
- AL crear
- DURANTE ejecución
- AL completar

---

## 📖 Acceso Rápido a Templates

| Tipo        | Link                                                            | Descripción                 |
| ----------- | --------------------------------------------------------------- | --------------------------- |
| 📌 ÉPICA    | [Template](templates-issues.md#-template---épica)               | Para iniciativas de negocio |
| 📖 HISTORIA | [Template](templates-issues.md#-template---historia-user-story) | Para features del usuario   |
| 📋 TAREA    | [Template](templates-issues.md#-template---tarea-task)          | Para trabajo técnico        |
| 🐛 BUG      | [Template](templates-issues.md#-template---bug)                 | Para reportar problemas     |

---

## 📞 Soporte y Feedback

Para preguntas o mejoras a esta documentación:

- Contactar a **[RESPONSABLE]**
- Canal Slack: **#sdd-jira-support**
- Email: **[EMAIL-SOPORTE]**

---

## 📝 Versionamiento

| Versión | Fecha       | Cambios                  |
| ------- | ----------- | ------------------------ |
| 1.0.0   | 16-dic-2024 | Versión inicial completa |

---

## 🎓 Recursos Relacionados

En el mismo repositorio:

- [Guía de Jira Integration](jira-integration-guide.md)
- [Metodología de Trabajo](../shared/00-metodologia-trabajo.md)
- [Requirements Template](../shared/01-requirements.md)
- [Architecture Guidelines](../shared/02-architecture.md)
- [Progress Tracking](../shared/tracking/00-progress-overview.md)

---

**¡Listo para empezar! 🚀**

Selecciona el documento que necesites según tu rol y comienza a crear issues de manera estándar y consistente.
