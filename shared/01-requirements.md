# 01 - Requisitos del Sistema

> **Template Genérico** - Define requisitos funcionales y no funcionales del proyecto

## Visión General

**Nombre del Proyecto**: [NOMBRE_PROYECTO]

**Descripción**: [Breve descripción de qué hace el sistema y su propósito principal]

**Objetivo**: [Objetivo principal que busca resolver]

---

## Requisitos Funcionales (RF)

> **Nota**: Los requisitos funcionales describen QUÉ debe hacer el sistema.

### RF-001: [Nombre del Módulo/Feature Principal]

**Descripción**: [Descripción general de la funcionalidad]

- **RF-001.1**: [Requisito específico 1]
  - **Entrada**: [Qué recibe]
  - **Proceso**: [Qué hace]
  - **Salida**: [Qué devuelve]
  - **Criterios de aceptación**:
    - [ ] [Criterio 1]
    - [ ] [Criterio 2]
- **RF-001.2**: [Requisito específico 2]
- **RF-001.3**: [Requisito específico 3]

**Ejemplos de uso**:

```
[Ejemplo 1: Caso típico]
Input: [Datos de entrada]
Output: [Resultado esperado]

[Ejemplo 2: Edge case]
Input: [Datos de entrada]
Output: [Resultado esperado]
```

**Validaciones**:

- [ ] [Validación 1]
- [ ] [Validación 2]

**Errores posibles**:

- `ERROR_CODE_1`: [Descripción del error]
- `ERROR_CODE_2`: [Descripción del error]

---

### RF-002: [Segundo Módulo/Feature]

[Seguir mismo formato que RF-001]

---

### RF-003: [Tercer Módulo/Feature]

[Seguir mismo formato que RF-001]

---

## Template de Requisito Funcional

**Usar este template para cada nuevo requisito:**

```markdown
### RF-XXX: [Nombre del Requisito]

**Descripción**: [Qué hace esta funcionalidad]

**Requisitos detallados**:

- **RF-XXX.1**: [Sub-requisito 1]
  - **Entrada**: [Datos de entrada]
  - **Proceso**: [Lógica a aplicar]
  - **Salida**: [Resultado esperado]
  - **Criterios de aceptación**:
    - [ ] [Criterio medible 1]
    - [ ] [Criterio medible 2]
- **RF-XXX.2**: [Sub-requisito 2]

**Ejemplos de uso**:
[Casos de uso concretos]

**Validaciones**:
[Reglas de validación]

**Errores posibles**:
[Lista de errores]

**Dependencias**:
[Otros requisitos que deben cumplirse primero]

**Prioridad**: [Alta/Media/Baja]
**Estado**: [No iniciado/En progreso/Completado]
```

---

## Requisitos No Funcionales (RNF)

> **Nota**: Los requisitos no funcionales describen CÓMO debe comportarse el sistema.

### RNF-001: Performance

- **RNF-001.1**: El sistema debe responder en menos de [X] ms para operaciones de lectura
- **RNF-001.2**: El sistema debe soportar [X] operaciones concurrentes
- **RNF-001.3**: El tiempo de carga inicial no debe exceder [X] segundos

**Métricas**:

- Latencia p95: <= [X] ms
- Throughput: >= [X] requests/second
- Time to First Byte: <= [X] ms

### RNF-002: Escalabilidad

- **RNF-002.1**: El sistema debe escalar horizontalmente hasta [X] instancias
- **RNF-002.2**: El sistema debe manejar [X] usuarios concurrentes
- **RNF-002.3**: La base de datos debe soportar [X] registros sin degradación

### RNF-003: Seguridad

- **RNF-003.1**: Toda comunicación debe ser a través de HTTPS/TLS
- **RNF-003.2**: Contraseñas deben estar hasheadas con [algoritmo]
- **RNF-003.3**: Implementar rate limiting de [X] requests por [Y] tiempo
- **RNF-003.4**: Sanitizar todas las entradas de usuario
- **RNF-003.5**: Implementar autenticación [JWT/OAuth2/otro]

### RNF-004: Disponibilidad

- **RNF-004.1**: Uptime objetivo: [X]% (ej: 99.9%)
- **RNF-004.2**: Recovery Time Objective (RTO): [X] horas
- **RNF-004.3**: Recovery Point Objective (RPO): [X] horas
- **RNF-004.4**: Backups automáticos cada [X] horas

### RNF-005: Usabilidad

- **RNF-005.1**: La interfaz debe ser responsive (mobile, tablet, desktop)
- **RNF-005.2**: Cumplir con estándares de accesibilidad [WCAG 2.1 AA/AAA]
- **RNF-005.3**: Mensajes de error deben ser claros y accionables
- **RNF-005.4**: Soporte para [idiomas: español, inglés, etc.]

### RNF-006: Mantenibilidad

- **RNF-006.1**: Código debe tener coverage de tests >= [X]%
- **RNF-006.2**: Documentación actualizada para todas las APIs
- **RNF-006.3**: Código debe pasar linter sin warnings
- **RNF-006.4**: Logs estructurados con niveles apropiados

### RNF-007: Monitoreo y Observabilidad

- **RNF-007.1**: Implementar logging estructurado
- **RNF-007.2**: Métricas de negocio y técnicas en tiempo real
- **RNF-007.3**: Alertas configuradas para eventos críticos
- **RNF-007.4**: Tracing distribuido para requests

### RNF-008: Compatibilidad

- **RNF-008.1**: Soportar navegadores: [Chrome, Firefox, Safari, Edge - últimas 2 versiones]
- **RNF-008.2**: Soportar Node.js: [versión X o superior]
- **RNF-008.3**: Soportar bases de datos: [PostgreSQL X+, MongoDB X+, etc.]

---

## Casos de Uso

### UC-001: [Nombre del Caso de Uso]

**Actor**: [Usuario, Sistema, Administrador, etc.]

**Precondiciones**:

- [Condición 1 que debe cumplirse antes]
- [Condición 2 que debe cumplirse antes]

**Flujo Principal**:

1. [Actor] [realiza acción 1]
2. [Sistema] [responde con acción 2]
3. [Actor] [realiza acción 3]
4. [Sistema] [procesa y devuelve resultado]

**Flujos Alternativos**:

- **3a**: Si [condición alternativa], entonces:
  1. [Sistema hace X]
  2. Volver al paso 4
- **3b**: Si [otra condición], entonces:
  1. [Sistema hace Y]
  2. Terminar caso de uso

**Postcondiciones**:

- [Estado final del sistema después del caso de uso]

**Excepciones**:

- **E1**: [Descripción del error posible]
  - **Manejo**: [Cómo se maneja]

---

## Restricciones y Limitaciones

### Restricciones Técnicas

- [Restricción 1: ej. "Debe usar framework X por decisión del equipo"]
- [Restricción 2: ej. "Debe ejecutarse en contenedores Docker"]
- [Restricción 3: ej. "Integración con servicio externo Y obligatoria"]

### Limitaciones Conocidas

- [Limitación 1: ej. "No soporta archivos mayores a 10MB"]
- [Limitación 2: ej. "Solo disponible en horarios X por dependencia externa"]
- [Limitación 3: ej. "Requiere conexión a internet para funcionalidad Y"]

### Dependencias Externas

- **[Nombre del Servicio/API]**: [Descripción y propósito]
  - Versión: [X.Y.Z]
  - Documentación: [URL]
  - Criticidad: [Alta/Media/Baja]

---

## Roadmap de Features (Opcional)

### MVP (Minimum Viable Product)

**Fecha objetivo**: [FECHA]

**Features incluidos**:

- [ ] RF-001: [Feature 1]
- [ ] RF-002: [Feature 2]
- [ ] RF-003: [Feature 3]

### Post-MVP

**Prioridad Alta**:

- [ ] RF-004: [Feature 4]
- [ ] RF-005: [Feature 5]

**Prioridad Media**:

- [ ] RF-006: [Feature 6]
- [ ] RF-007: [Feature 7]

**Prioridad Baja** (Nice to have):

- [ ] RF-008: [Feature 8]
- [ ] RF-009: [Feature 9]

---

## Matriz de Trazabilidad

| Requisito | Prioridad | Módulo      | Estado      | Tests | Docs |
| --------- | --------- | ----------- | ----------- | ----- | ---- |
| RF-001    | Alta      | [Módulo]    | Completado  | ✅    | ✅   |
| RF-002    | Alta      | [Módulo]    | En progreso | ⏳    | ✅   |
| RF-003    | Media     | [Módulo]    | No iniciado | ❌    | ✅   |
| RNF-001   | Alta      | Performance | Completado  | ✅    | ✅   |

**Leyenda**:

- ✅ Completo
- ⏳ En progreso
- ❌ No iniciado

---

## Glosario

**[Término 1]**: [Definición clara del término técnico o de negocio]

**[Término 2]**: [Definición clara del término técnico o de negocio]

**[Término 3]**: [Definición clara del término técnico o de negocio]

---

## Historial de Cambios

| Fecha      | Versión | Cambios                          | Autor     |
| ---------- | ------- | -------------------------------- | --------- |
| YYYY-MM-DD | 1.0.0   | Versión inicial del documento    | [Autor]   |
| YYYY-MM-DD | 1.1.0   | Agregar RF-XXX                   | [Autor]   |
| YYYY-MM-DD | 1.2.0   | Actualizar criterios RNF-001     | [Autor]   |

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Próxima revisión**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
