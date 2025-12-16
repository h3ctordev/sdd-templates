# 03 - Issues Log (Registro de Problemas y Resoluciones)

> **Template Genérico** - Documentación centralizada de bugs, issues y sus resoluciones

## Propósito de este Documento

**CRÍTICO**: Este es el **único lugar centralizado** para documentar TODOS los bugs, issues y problemas del proyecto. NO crear archivos separados para cada bug.

**Cuándo documentar aquí**:
- ✅ Cualquier bug encontrado
- ✅ Issues técnicos o arquitectónicos
- ✅ Problemas de performance
- ✅ Errores en producción/staging
- ✅ Resolución de problemas
- ✅ Workarounds temporales

**Formato**: Orden cronológico (más reciente primero)

---

## Leyenda de Estados

- 🔴 **Crítico**: Afecta funcionalidad principal, producción down
- 🟡 **Alto**: Afecta funcionalidad importante, workaround disponible
- 🟢 **Medio**: Afecta funcionalidad secundaria
- 🔵 **Bajo**: Mejora, no afecta funcionalidad
- ✅ **Resuelto**: Problema completamente resuelto
- ⏳ **En Progreso**: Trabajando en la solución
- 📋 **Pendiente**: Identificado pero no iniciado

---

## Template para Nuevos Issues

```markdown
## ISSUE-XXX: [Título Descriptivo del Problema]

**Fecha**: YYYY-MM-DD

**Prioridad**: [🔴 Crítico / 🟡 Alto / 🟢 Medio / 🔵 Bajo]

**Estado**: [✅ Resuelto / ⏳ En Progreso / 📋 Pendiente]

**Reportado por**: [Nombre o rol]

**Asignado a**: [Nombre o rol]

### Descripción del Problema

[Descripción detallada del problema encontrado]

### Contexto

- **Entorno**: [Development/Staging/Production]
- **Versión**: [vX.Y.Z]
- **Branch**: [nombre-del-branch]
- **Módulo afectado**: [Nombre del módulo/componente]
- **Usuario afectado**: [Si aplica]

### Pasos para Reproducir

1. [Paso 1]
2. [Paso 2]
3. [Paso 3]

**Resultado esperado**: [Qué debería pasar]

**Resultado actual**: [Qué pasa en realidad]

### Logs/Errores

```
[Copiar logs relevantes, stack traces, mensajes de error]
```

### Causa Raíz

[Explicación técnica de por qué ocurre el problema]

**Archivos involucrados**:
- `[ruta/archivo1.ext]` - [Descripción del problema en este archivo]
- `[ruta/archivo2.ext]` - [Descripción del problema en este archivo]

### Solución Implementada

**Enfoque**:
[Descripción de cómo se resolvió el problema]

**Cambios realizados**:

1. **[Archivo/Módulo 1]**:
   - [Cambio 1]
   - [Cambio 2]

2. **[Archivo/Módulo 2]**:
   - [Cambio 1]

**Commits relacionados**:
- [hash corto]: [mensaje del commit]
- [hash corto]: [mensaje del commit]

**PR/MR**: #[número]

### Testing

**Tests agregados**:
- [ ] Unit tests para caso específico
- [ ] Integration tests
- [ ] E2E tests (si aplica)
- [ ] Manual testing en [entornos]

**Validación**:
- [ ] Verificado en development
- [ ] Verificado en staging
- [ ] Verificado en production (si aplica)

### Medidas Preventivas

**Para evitar que vuelva a ocurrir**:
1. [Medida 1: ej. "Agregar validación en...]
2. [Medida 2: ej. "Documentar edge case en...]
3. [Medida 3: ej. "Agregar tests para..."]

### Lecciones Aprendidas

[Qué aprendimos de este issue]

### Enlaces Relacionados

- Issue en GitHub/Jira: [link]
- Documentación relacionada: [link]
- ADR relacionado: [link]

---
```

---

## Issues Activos

### ISSUE-003: [Ejemplo de Issue En Progreso]

**Fecha**: 2025-12-16

**Prioridad**: 🟡 Alto

**Estado**: ⏳ En Progreso

**Reportado por**: [Nombre]

**Asignado a**: [Nombre]

### Descripción del Problema

[Descripción...]

[Resto del template completado]

---

## Issues Resueltos

### ISSUE-002: [Ejemplo de Issue Resuelto]

**Fecha**: 2025-12-15

**Prioridad**: 🟢 Medio

**Estado**: ✅ Resuelto

**Fecha de resolución**: 2025-12-15

**Reportado por**: [Nombre]

**Resuelto por**: [Nombre]

### Descripción del Problema

[Descripción...]

[Resto del template completado]

---

### ISSUE-001: [Primer Issue del Proyecto]

**Fecha**: 2025-12-01

**Prioridad**: 🔴 Crítico

**Estado**: ✅ Resuelto

**Fecha de resolución**: 2025-12-02

[Template completo...]

---

## Estadísticas de Issues

### Por Prioridad

- 🔴 Críticos: [X] total ([Y] resueltos, [Z] activos)
- 🟡 Altos: [X] total ([Y] resueltos, [Z] activos)
- 🟢 Medios: [X] total ([Y] resueltos, [Z] activos)
- 🔵 Bajos: [X] total ([Y] resueltos, [Z] activos)

### Por Estado

- ✅ Resueltos: [X] ([Y]%)
- ⏳ En Progreso: [X] ([Y]%)
- 📋 Pendientes: [X] ([Y]%)

### Por Módulo

| Módulo          | Issues Totales | Resueltos | Activos |
| --------------- | -------------- | --------- | ------- |
| [Módulo 1]      | [X]            | [Y]       | [Z]     |
| [Módulo 2]      | [X]            | [Y]       | [Z]     |

### Tiempo Promedio de Resolución

- Críticos: [X] horas
- Altos: [X] días
- Medios: [X] días
- Bajos: [X] semanas

---

## Issues Recurrentes

### Patrón 1: [Descripción del Patrón]

**Frecuencia**: [X] veces en [Y] meses

**Issues relacionados**: ISSUE-001, ISSUE-005, ISSUE-012

**Causa común**: [Explicación]

**Solución permanente recomendada**: [Recomendación]

---

## Workarounds Temporales Activos

### Workaround 1: [Descripción]

**Para issue**: ISSUE-XXX

**Aplicado en**: [Fecha]

**Descripción**: [Cómo funciona el workaround]

**Impacto**: [Qué limitaciones tiene]

**Plan para solución permanente**: [Cuándo y cómo se implementará la solución real]

---

## Matriz de Impacto

| Issue ID | Prioridad | Módulos Afectados | Usuarios Impactados | Tiempo de Resolución |
| -------- | --------- | ----------------- | ------------------- | -------------------- |
| ISSUE-001 | 🔴       | [Módulos]         | [N o "Todos"]       | [X] horas            |
| ISSUE-002 | 🟡       | [Módulos]         | [N]                 | [X] días             |

---

## Checklist de Documentación de Issues

Antes de cerrar un issue como resuelto, verificar:

- [ ] ✅ Descripción del problema está clara
- [ ] ✅ Causa raíz identificada y documentada
- [ ] ✅ Solución implementada y explicada
- [ ] ✅ Tests agregados para prevenir regresión
- [ ] ✅ Cambios revisados por code review
- [ ] ✅ Validado en staging (mínimo)
- [ ] ✅ Medidas preventivas implementadas
- [ ] ✅ Documentación actualizada si fue necesario
- [ ] ✅ Lecciones aprendidas documentadas
- [ ] ✅ Issues relacionados cerrados/actualizados

---

## Plantilla Rápida para Bug Reports

**Para reportar un bug rápidamente (luego completar el template completo):**

```markdown
## BUG: [Título breve]

**Dónde**: [Módulo/archivo]
**Cuándo**: [FECHA y hora si es relevante]
**Qué**: [Qué salió mal en 1-2 líneas]
**Error**: [Mensaje de error o comportamiento inesperado]
**Urgencia**: [🔴/🟡/🟢/🔵]
```

---

## Notas Importantes

1. **SIEMPRE documentar bugs aquí** - No crear archivos separados
2. **Ser específico** - Incluir logs, stack traces, pasos exactos
3. **Identificar causa raíz** - No solo el síntoma
4. **Documentar solución** - Para referencia futura
5. **Agregar tests** - Prevenir regresión
6. **Actualizar rápido** - Documentar mientras está fresco
7. **Cross-referenciar** - Linkear a issues, PRs, ADRs relacionados

---

**Última actualización**: [FECHA]  
**Total de issues documentados**: [X]  
**Mantenedor**: [EQUIPO/PERSONA]
