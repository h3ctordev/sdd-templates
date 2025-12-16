# 04 - Decisions Log (Registro de Decisiones Arquitectónicas)

> **Template Genérico** - Architectural Decision Records (ADRs)

## Propósito de este Documento

Este documento registra todas las **decisiones arquitectónicas significativas** del proyecto, siguiendo el patrón ADR (Architectural Decision Record).

**Cuándo crear un ADR**:
- ✅ Elección de tecnologías principales (framework, database, etc.)
- ✅ Patrones arquitectónicos (microservicios, monolito, etc.)
- ✅ Decisiones que afectan a múltiples módulos
- ✅ Trade-offs significativos
- ✅ Cambios arquitectónicos importantes

**NO crear ADR para**:
- ❌ Decisiones de implementación menores
- ❌ Configuraciones triviales
- ❌ Bugs y fixes
- ❌ Cambios en requisitos de negocio (usar 01-requirements.md)

---

## Template de ADR

```markdown
## ADR-XXX: [Título Corto y Descriptivo]

**Fecha**: YYYY-MM-DD

**Estado**: [Propuesta/Aceptada/Rechazada/Obsoleta/Reemplazada por ADR-YYY]

**Autores**: [Nombre(s)]

**Revisores**: [Nombre(s)]

**Decisor final**: [Nombre o rol]

---

### Contexto

[Descripción de la situación que requiere una decisión]

**Problema**:
[¿Qué problema estamos tratando de resolver?]

**Restricciones**:
- [Restricción 1: tiempo, presupuesto, tecnología, equipo, etc.]
- [Restricción 2]

**Requisitos**:
- [Requisito 1 que la solución debe cumplir]
- [Requisito 2]

---

### Decisión

[La decisión que tomamos - clara y concisa]

**Enfoque elegido**: [Nombre de la solución]

**Justificación**: [Por qué esta solución es la mejor para nuestro contexto]

---

### Alternativas Consideradas

#### Opción 1: [Nombre de la alternativa]

**Descripción**: [Breve descripción]

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]

**Contras**:
- ❌ [Contra 1]
- ❌ [Contra 2]

**Por qué NO se eligió**: [Explicación]

#### Opción 2: [Otra alternativa]

[Mismo formato que Opción 1]

#### Opción 3: [Otra alternativa]

[Mismo formato que Opción 1]

---

### Matriz de Evaluación

| Criterio               | Peso | Opción 1 | Opción 2 | Opción Elegida |
| ---------------------- | ---- | -------- | -------- | -------------- |
| Performance            | 30%  | 7/10     | 5/10     | **9/10**       |
| Mantenibilidad         | 25%  | 6/10     | 9/10     | **8/10**       |
| Costo                  | 20%  | 8/10     | 4/10     | **7/10**       |
| Curva de aprendizaje   | 15%  | 5/10     | 8/10     | **6/10**       |
| Escalabilidad          | 10%  | 6/10     | 7/10     | **9/10**       |
| **Total ponderado**    |      | 6.6      | 6.5      | **7.9**        |

---

### Consecuencias

#### Positivas ✅

- [Consecuencia positiva 1]
- [Consecuencia positiva 2]
- [Consecuencia positiva 3]

#### Negativas ⚠️

- [Consecuencia negativa 1]
- [Consecuencia negativa 2]

#### Neutral ℹ️

- [Aspecto neutral 1]

---

### Impacto

**Módulos afectados**:
- [Módulo 1]
- [Módulo 2]

**Cambios requeridos**:
- [ ] [Cambio 1 en código]
- [ ] [Cambio 2 en infraestructura]
- [ ] [Cambio 3 en documentación]

**Esfuerzo estimado**: [X] días/semanas

**Riesgos**:
- [Riesgo 1 y su mitigación]
- [Riesgo 2 y su mitigación]

---

### Implementación

**Plan de implementación**:
1. [Paso 1]
2. [Paso 2]
3. [Paso 3]

**Criterios de éxito**:
- [ ] [Criterio 1 medible]
- [ ] [Criterio 2 medible]
- [ ] [Criterio 3 medible]

**Fecha de implementación**: [FECHA]

**Responsable**: [Nombre]

---

### Validación

**Métricas para validar la decisión**:
- [Métrica 1: ej. "Reducción de latencia en 50%"]
- [Métrica 2: ej. "Tiempo de desarrollo reducido en 30%"]

**Período de evaluación**: [X] meses

**Fecha de revisión**: [FECHA]

**Resultado de la validación** (completar después):
- [Resultado 1]
- [Resultado 2]
- **Conclusión**: [¿Fue la decisión correcta? ¿Qué ajustes se hicieron?]

---

### Referencias

- Documentación relacionada: [links]
- Issues relacionados: [links]
- Artículos/papers: [links]
- Experiencias similares: [links]

---
```

---

## Índice de ADRs

| ID  | Título | Estado | Fecha | Impacto |
| --- | ------ | ------ | ----- | ------- |
| [ADR-003](#adr-003-ejemplo-adr-activo) | [Ejemplo ADR Activo] | ✅ Aceptada | 2025-12-16 | Alto |
| [ADR-002](#adr-002-ejemplo-adr-obsoleto) | [Ejemplo ADR Obsoleto] | 🔄 Obsoleta | 2025-11-01 | Medio |
| [ADR-001](#adr-001-primer-adr) | [Primer ADR] | ✅ Aceptada | 2025-10-01 | Alto |

---

## ADRs Activos

### ADR-003: [Ejemplo ADR Activo]

**Fecha**: 2025-12-16

**Estado**: ✅ Aceptada

**Autores**: [Nombre]

**Decisor final**: [Nombre o rol]

[Completar template...]

---

## ADRs Obsoletos

### ADR-002: [Ejemplo ADR Obsoleto]

**Fecha**: 2025-11-01

**Estado**: 🔄 Obsoleta - Reemplazada por ADR-003

**Razón de obsolescencia**: [Por qué ya no aplica esta decisión]

[Template original completado...]

---

### ADR-001: [Primer ADR del Proyecto]

**Fecha**: 2025-10-01

**Estado**: ✅ Aceptada (aún vigente)

[Template completado...]

---

## Categorías de Decisiones

### Tecnología y Stack

ADRs relacionados: ADR-001, ADR-005

### Arquitectura y Patrones

ADRs relacionados: ADR-002, ADR-003, ADR-007

### Seguridad

ADRs relacionados: ADR-004, ADR-006

### Performance y Escalabilidad

ADRs relacionados: ADR-003

### DevOps e Infraestructura

ADRs relacionados: ADR-008

---

## Proceso de Decisión

### 1. Identificar Necesidad

Cuando surge una decisión arquitectónica:
1. Identificar el problema claramente
2. Recopilar contexto y restricciones
3. Definir criterios de evaluación

### 2. Investigación

1. Investigar alternativas disponibles
2. Consultar con equipo técnico
3. Revisar experiencias de otros proyectos
4. Crear POCs si es necesario

### 3. Propuesta

1. Crear ADR con estado "Propuesta"
2. Completar secciones de contexto y alternativas
3. Incluir matriz de evaluación
4. Compartir con equipo para feedback

### 4. Discusión

1. Reunión de revisión con stakeholders
2. Debatir pros/contras
3. Considerar impacto a largo plazo
4. Documentar feedback en el ADR

### 5. Decisión

1. Decisor final aprueba la decisión
2. Actualizar estado a "Aceptada" o "Rechazada"
3. Comunicar decisión al equipo
4. Planificar implementación

### 6. Implementación

1. Ejecutar plan de implementación
2. Actualizar ADR con progreso
3. Documentar desviaciones si ocurren

### 7. Validación

1. Medir métricas definidas
2. Evaluar si se cumplieron objetivos
3. Actualizar sección de validación
4. Decidir si mantener, ajustar o revertir

---

## Plantilla Ligera (Para Decisiones Menores)

```markdown
## Decisión: [Título]

**Fecha**: YYYY-MM-DD

**Contexto**: [1-2 líneas]

**Decisión**: [Lo que decidimos]

**Razón**: [Por qué]

**Alternativas**: [Qué más consideramos]

**Consecuencias**: [Impacto esperado]
```

---

## Estadísticas de ADRs

- **Total de ADRs**: [X]
- **Aceptadas**: [X] ([Y]%)
- **Rechazadas**: [X] ([Y]%)
- **Obsoletas**: [X] ([Y]%)
- **En propuesta**: [X] ([Y]%)

**Por categoría**:
- Tecnología: [X] ADRs
- Arquitectura: [X] ADRs
- Seguridad: [X] ADRs
- Performance: [X] ADRs
- DevOps: [X] ADRs

---

## Decisiones Críticas (High-Impact)

Las siguientes decisiones tuvieron el mayor impacto en el proyecto:

1. **ADR-XXX**: [Título] - [Breve descripción del impacto]
2. **ADR-YYY**: [Título] - [Breve descripción del impacto]
3. **ADR-ZZZ**: [Título] - [Breve descripción del impacto]

---

## Lecciones Aprendidas

### De Decisiones Exitosas

- [Lección 1 de decisión que funcionó muy bien]
- [Lección 2]

### De Decisiones Revertidas

- [Lección 1 de decisión que hubo que revertir]
- [Lección 2]

### Mejores Prácticas Identificadas

- [Práctica 1 para toma de decisiones futuras]
- [Práctica 2]

---

## Checklist para Nuevos ADRs

Antes de finalizar un ADR, verificar:

- [ ] ✅ Contexto claramente explicado
- [ ] ✅ Problema bien definido
- [ ] ✅ Al menos 2-3 alternativas consideradas
- [ ] ✅ Pros y contras documentados para cada opción
- [ ] ✅ Matriz de evaluación incluida (para decisiones complejas)
- [ ] ✅ Consecuencias (positivas y negativas) identificadas
- [ ] ✅ Impacto en módulos/equipo/timeline considerado
- [ ] ✅ Criterios de validación definidos
- [ ] ✅ Revisado por al menos 2 personas
- [ ] ✅ Aprobado por decisor final

---

**Última actualización**: [FECHA]  
**Total de decisiones documentadas**: [X]  
**Mantenedor**: [EQUIPO/PERSONA]
