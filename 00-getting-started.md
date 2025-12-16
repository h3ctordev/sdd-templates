# 00 - Getting Started (Guía de Inicio Rápido)

> **Guía de Inicio Rápido** - Cómo aplicar SDD Templates en tu proyecto

## 🎯 ¿Qué encontrarás aquí?

Esta guía te ayudará a:
1. Elegir los templates correctos para tu proyecto
2. Configurar SDD en tu proyecto nuevo o existente
3. Entender el flujo de trabajo diario con SDD
4. Adaptar los templates a tus necesidades

**Tiempo estimado de setup**: 30-60 minutos

---

## 📋 Paso 1: Identificar Tipo de Proyecto

### ¿Qué estás construyendo?

#### Opción A: Backend/API

**Indicadores**:
- ✅ API REST o GraphQL
- ✅ Servidor Node.js, Python, Go, Java, etc.
- ✅ Microservicio
- ✅ Backend para mobile/web

**Templates que necesitas**:
```bash
shared/                                    # Base (SIEMPRE)
  ├── 00-metodologia-trabajo.md
  ├── 01-requirements.md
  ├── 02-architecture.md
  ├── 08-configuration.md
  └── tracking/

backend/                                   # Específicos backend
  ├── 07-project-structure-backend.md
  └── 09-api-documentation.md

# Copiar también ejemplo de tu framework:
backend/examples/[nestjs|express|fastapi|django]/
```

**Ir a**: [Sección Backend](#setup-backend)

---

#### Opción B: Frontend/Web App

**Indicadores**:
- ✅ Single Page Application (SPA)
- ✅ React, Vue, Angular, Svelte, etc.
- ✅ Aplicación web interactiva
- ✅ Progressive Web App (PWA)

**Templates que necesitas**:
```bash
shared/                                    # Base (SIEMPRE)
  ├── 00-metodologia-trabajo.md
  ├── 01-requirements.md
  ├── 02-architecture.md
  ├── 08-configuration.md
  └── tracking/

frontend/                                  # Específicos frontend
  ├── 07-project-structure-frontend.md
  └── 10-component-architecture.md

# Copiar también ejemplo de tu framework:
frontend/examples/[react|vue|angular|nextjs]/
```

**Ir a**: [Sección Frontend](#setup-frontend)

---

#### Opción C: Monorepo/Fullstack

**Indicadores**:
- ✅ Backend + Frontend en mismo repo
- ✅ Múltiples aplicaciones relacionadas
- ✅ Librerías compartidas entre proyectos
- ✅ Nx, Turborepo, Lerna, pnpm workspaces

**Templates que necesitas**:
```bash
shared/                                    # Base (SIEMPRE)
  ├── 00-metodologia-trabajo.md
  ├── 01-requirements.md
  ├── 02-architecture.md
  ├── 08-configuration.md
  └── tracking/

monorepo/                                  # Específicos monorepo
  ├── 07-project-structure-monorepo.md
  └── 11-workspace-organization.md

# También copiar templates de backend Y frontend si aplica
```

**Ir a**: [Sección Monorepo](#setup-monorepo)

---

## 🚀 Paso 2: Setup Inicial

### Setup Backend

#### 1. Crear estructura de docs

```bash
# En la raíz de tu proyecto
mkdir -p docs/tracking docs/api docs/guides

# Copiar templates compartidos
cp [ruta-a-sdd-templates]/shared/00-metodologia-trabajo.md docs/
cp [ruta-a-sdd-templates]/shared/01-requirements.md docs/
cp [ruta-a-sdd-templates]/shared/02-architecture.md docs/
cp [ruta-a-sdd-templates]/shared/08-configuration.md docs/
cp -r [ruta-a-sdd-templates]/shared/tracking/* docs/tracking/

# Copiar templates de backend
cp [ruta-a-sdd-templates]/backend/07-project-structure-backend.md docs/
cp [ruta-a-sdd-templates]/backend/09-api-documentation.md docs/api/

# Opcional: Copiar ejemplo de tu framework
# cp -r [ruta-a-sdd-templates]/backend/examples/nestjs/* .
```

#### 2. Personalizar templates

**Archivo: `docs/00-metodologia-trabajo.md`**
```bash
# Buscar y reemplazar:
[NOMBRE_PROYECTO] → Tu nombre de proyecto
[MAIN_BRANCH] → main / develop / master
[PACKAGE_MANAGER] → npm / pnpm / yarn
[TEST_COMMAND] → npm test / pnpm test
[LINT_COMMAND] → npm run lint / pnpm run lint
```

**Archivo: `docs/01-requirements.md`**
```bash
# Completar:
- Visión General con tu proyecto
- RF-001, RF-002, etc. con tus requisitos
- RNF (Performance, Seguridad, etc.)
```

**Archivo: `docs/02-architecture.md`**
```bash
# Completar:
- Stack Tecnológico con tus tecnologías
- Patrones que usarás (Repository, Strategy, etc.)
- Módulos de tu sistema
- Decisiones arquitectónicas
```

#### 3. Configurar convenciones

**Archivo: `docs/07-project-structure-backend.md`**
```bash
# Adaptar la estructura de directorios a tu proyecto
# Ejemplo para NestJS:
src/
├── common/
├── config/
├── modules/
├── database/
└── main.ts

# Definir naming conventions:
- Services: *.service.ts
- Controllers: *.controller.ts
- Tests: *.spec.ts
```

#### 4. Primer commit

```bash
git add docs/
git commit -m "docs: add SDD documentation structure"
```

---

### Setup Frontend

#### 1. Crear estructura de docs

```bash
# En la raíz de tu proyecto
mkdir -p docs/tracking docs/guides

# Copiar templates compartidos
cp [ruta-a-sdd-templates]/shared/00-metodologia-trabajo.md docs/
cp [ruta-a-sdd-templates]/shared/01-requirements.md docs/
cp [ruta-a-sdd-templates]/shared/02-architecture.md docs/
cp [ruta-a-sdd-templates]/shared/08-configuration.md docs/
cp -r [ruta-a-sdd-templates]/shared/tracking/* docs/tracking/

# Copiar templates de frontend
cp [ruta-a-sdd-templates]/frontend/07-project-structure-frontend.md docs/
cp [ruta-a-sdd-templates]/frontend/10-component-architecture.md docs/

# Opcional: Copiar ejemplo de tu framework
# cp -r [ruta-a-sdd-templates]/frontend/examples/react/* .
```

#### 2. Personalizar para frontend

**Archivo: `docs/00-metodologia-trabajo.md`**
```bash
# Buscar y reemplazar:
[NOMBRE_PROYECTO] → Tu nombre de proyecto
[PACKAGE_MANAGER] → npm / pnpm / yarn
[TEST_COMMAND] → npm test / vitest
[BUILD_COMMAND] → npm run build / vite build
```

**Archivo: `docs/02-architecture.md`**
```bash
# Completar con tu stack frontend:
- Framework: React/Vue/Angular
- State Management: Redux/Zustand/Pinia
- Routing: React Router/Vue Router
- UI Library: MUI/Chakra/Tailwind
- Build Tool: Vite/Webpack
```

**Archivo: `docs/07-project-structure-frontend.md`**
```bash
# Adaptar estructura de componentes:
src/
├── components/
├── pages/ (o views/)
├── hooks/ (React)
├── stores/ (State management)
├── services/
└── utils/
```

#### 3. Primer commit

```bash
git add docs/
git commit -m "docs: add SDD documentation structure"
```

---

### Setup Monorepo

#### 1. Crear estructura de docs

```bash
# En la raíz del monorepo
mkdir -p docs/tracking docs/api docs/guides

# Copiar templates compartidos
cp [ruta-a-sdd-templates]/shared/* docs/
cp -r [ruta-a-sdd-templates]/shared/tracking/* docs/tracking/

# Copiar templates de monorepo
cp [ruta-a-sdd-templates]/monorepo/07-project-structure-monorepo.md docs/
cp [ruta-a-sdd-templates]/monorepo/11-workspace-organization.md docs/

# Si tienes backend Y frontend, copiar también esos templates
cp [ruta-a-sdd-templates]/backend/07-project-structure-backend.md docs/
cp [ruta-a-sdd-templates]/frontend/07-project-structure-frontend.md docs/
```

#### 2. Personalizar para monorepo

**Archivo: `docs/11-workspace-organization.md`**
```bash
# Definir estructura de workspaces:
apps/
  ├── api/           # Backend
  ├── web/           # Frontend web
  └── mobile/        # App móvil
packages/
  ├── ui/            # Componentes compartidos
  ├── utils/         # Utilidades compartidas
  └── types/         # Tipos compartidos
```

---

## 📖 Paso 3: Primer Feature con SDD

### Ejemplo Práctico: Crear módulo de autenticación

#### 3.1 Leer Especificaciones

```bash
# SIEMPRE el primer paso
less docs/00-metodologia-trabajo.md  # Entender la metodología
less docs/02-architecture.md         # Ver patrones y módulos
less docs/07-project-structure-*.md  # Ver estructura esperada
```

#### 3.2 Definir Requisito

**Editar: `docs/01-requirements.md`**
```markdown
### RF-001: Autenticación de Usuarios

**Descripción**: Sistema de autenticación con JWT

- **RF-001.1**: Usuarios pueden hacer login con email/password
  - **Entrada**: email (string), password (string)
  - **Proceso**: Validar credenciales, generar JWT
  - **Salida**: JWT token, user info
  - **Criterios de aceptación**:
    - [ ] Token expira en 24 horas
    - [ ] Password debe estar hasheado con bcrypt
    - [ ] Rate limiting: 5 intentos por minuto

- **RF-001.2**: Usuarios pueden renovar token
- **RF-001.3**: Usuarios pueden hacer logout
```

#### 3.3 Documentar Arquitectura

**Editar: `docs/02-architecture.md`**
```markdown
### Módulo: Authentication

**Responsabilidad**: Gestionar autenticación y autorización

**Componentes**:
- `auth.controller.ts`: Endpoints de autenticación
- `auth.service.ts`: Lógica de autenticación
- `jwt.strategy.ts`: Estrategia JWT
- `auth.guard.ts`: Guard para proteger rutas

**Dependencias**:
- Depende de: UsersModule
- Usado por: Todos los módulos protegidos

**APIs Públicas**:
- `POST /auth/login`: Autenticar usuario
- `POST /auth/refresh`: Renovar token
- `POST /auth/logout`: Cerrar sesión
```

#### 3.4 Crear Plan de Implementación

```markdown
## Plan de Implementación SDD

**Tarea**: Implementar módulo de autenticación

**Especificaciones consultadas**:
- [x] docs/00-metodologia-trabajo.md (workflow SDD)
- [x] docs/01-requirements.md (RF-001)
- [x] docs/02-architecture.md (Auth Module)
- [x] docs/07-project-structure-*.md (estructura de módulos)

**Archivos a crear**:
- [ ] src/modules/auth/auth.module.ts
- [ ] src/modules/auth/auth.controller.ts
- [ ] src/modules/auth/auth.service.ts
- [ ] src/modules/auth/auth.service.spec.ts
- [ ] src/modules/auth/strategies/jwt.strategy.ts
- [ ] src/modules/auth/guards/jwt-auth.guard.ts
- [ ] src/modules/auth/dto/login.dto.ts

**Pasos**:
1. [x] Leer especificaciones
2. [ ] Crear interfaces/DTOs
3. [ ] Implementar service con lógica
4. [ ] Crear tests para service
5. [ ] Implementar controller
6. [ ] Crear guard y strategy
7. [ ] Integrar con UsersModule
8. [ ] Validar contra specs
```

#### 3.5 Implementar

```bash
# Crear rama
git checkout -b feat/auth-module

# Implementar siguiendo el plan
# (Ver estructura en docs/07-project-structure-*.md)

# Validar cada incremento
npm run lint
npm test
npm run build

# Commit frecuente
git add .
git commit -m "feat(auth): add login endpoint"
```

#### 3.6 Actualizar Tracking

**Editar: `docs/tracking/00-progress-overview.md`**
```markdown
### Fase 1: MVP

#### Features Completados ✅

- [x] **RF-001**: Autenticación de Usuarios
  - Completado: 2025-12-16
  - Tests: ✅
  - Docs: ✅
  - Coverage: 85%
```

---

## 🔄 Paso 4: Flujo de Trabajo Diario

### Rutina Matutina (5-10 minutos)

```bash
# 1. Actualizar código
git checkout develop
git pull origin develop

# 2. Revisar progreso
cat docs/tracking/00-progress-overview.md

# 3. Identificar tarea del día
# Leer especificaciones relevantes

# 4. Crear rama para tarea
git checkout -b [tipo]/[nombre]
```

### Durante el Desarrollo

```bash
# Para cada subtarea:

# 1. Implementar cambio pequeño
# [Escribir código...]

# 2. Validar contra specs
# ¿Cumple lo especificado?

# 3. Validar con tools
npm run lint
npm test

# 4. Commit si todo pasa
git add .
git commit -m "[type]([scope]): [message]"

# 5. Repetir para siguiente subtarea
```

### Antes de Pull Request

```bash
# Checklist completo:
npm run lint           # ✅ Sin errores
npm run test           # ✅ Tests pasan
npm run test:cov       # ✅ Coverage >= umbral
npm run build          # ✅ Build exitoso

# Revisar contra especificaciones
# ¿Cumple RF-XXX completamente?

# Actualizar docs/tracking/00-progress-overview.md
# Marcar feature como completado

# Push y crear PR
git push origin [rama]
```

### Rutina Nocturna (5 minutos)

```bash
# Actualizar progreso
vim docs/tracking/00-progress-overview.md

# Documentar issues encontrados (si hubo)
vim docs/tracking/03-issues-log.md

# Commit de actualizaciones de docs
git add docs/
git commit -m "docs: update progress tracking"
git push
```

---

## 🎨 Paso 5: Personalizar Templates

### Adaptaciones Comunes

#### Cambiar Naming Conventions

**Archivo: `docs/07-project-structure-*.md`**
```markdown
# Si prefieres otros nombres:

# En lugar de:
*.service.ts
*.repository.ts

# Puedes usar:
*.svc.ts
*.repo.ts

# IMPORTANTE: Ser consistente en TODO el proyecto
```

#### Ajustar Coverage Threshold

**Archivo: `docs/00-metodologia-trabajo.md`**
```bash
# Buscar: coverage >= 55%
# Cambiar a tu umbral: coverage >= 80%

# Actualizar también en jest.config.js o similar
```

#### Agregar Secciones Específicas

Puedes agregar secciones adicionales a cualquier template:

```markdown
## [Nueva Sección]: Integración con [Servicio]

[Tu contenido específico...]
```

---

## ✅ Checklist de Setup Completo

### Documentación Base

- [ ] ✅ Copiado `00-metodologia-trabajo.md` y personalizado
- [ ] ✅ Copiado `01-requirements.md` y definido RF-001
- [ ] ✅ Copiado `02-architecture.md` y definido stack
- [ ] ✅ Copiado `08-configuration.md` y definido setup
- [ ] ✅ Copiados templates de tracking

### Documentación Específica

- [ ] ✅ Copiado template de estructura de proyecto
- [ ] ✅ Adaptada estructura a mi proyecto real
- [ ] ✅ Definidas convenciones de nombres
- [ ] ✅ Documentados patrones a usar

### Primer Feature

- [ ] ✅ Definido requisito en `01-requirements.md`
- [ ] ✅ Documentada arquitectura en `02-architecture.md`
- [ ] ✅ Creado plan de implementación
- [ ] ✅ Implementado siguiendo specs
- [ ] ✅ Tests escritos y pasando
- [ ] ✅ Actualizado tracking de progreso

### Proceso

- [ ] ✅ Equipo capacitado en SDD
- [ ] ✅ Flujo de trabajo definido
- [ ] ✅ Git workflow configurado
- [ ] ✅ CI/CD configurado para validar specs

---

## 🆘 Troubleshooting

### "No sé qué template copiar"

**Respuesta**: Copia SIEMPRE `shared/` y luego:
- Backend → `backend/`
- Frontend → `frontend/`
- Ambos → Ambos
- Monorepo → `monorepo/` + los otros dos

### "Los templates son muy largos"

**Respuesta**: Está bien no completar todo desde el inicio.

**Mínimo viable**:
1. `00-metodologia-trabajo.md` - Leer completo
2. `01-requirements.md` - Solo RF-001 para empezar
3. `02-architecture.md` - Solo stack y módulo actual
4. `07-project-structure-*.md` - Solo estructura básica

Completa el resto conforme avanzas.

### "Mi equipo no quiere usar esto"

**Respuesta**: Empieza solo con lo esencial:
1. Usa SDD tú solo primero
2. Muestra los beneficios (menos bugs, más claridad)
3. Propón usar solo `00-metodologia-trabajo.md` para empezar
4. Adopción gradual

### "Esto es mucho overhead"

**Respuesta**: SDD ahorra tiempo a largo plazo.

**Inversión inicial**: 1-2 horas setup
**Ahorro por feature**: 2-4 horas (menos confusión, menos bugs, menos refactors)
**ROI**: Positivo después de 2-3 features

---

## 📚 Próximos Pasos

1. **Leer**: `docs/00-metodologia-trabajo.md` completo
2. **Definir**: Tu primer requisito en `01-requirements.md`
3. **Documentar**: Arquitectura básica en `02-architecture.md`
4. **Implementar**: Tu primer feature siguiendo SDD
5. **Iterar**: Mejorar el proceso continuamente

---

## 💡 Tips para el Éxito

1. **Empieza pequeño**: No intentes documentar todo desde el inicio
2. **Sé consistente**: Usa SDD en TODAS las features, no solo algunas
3. **Actualiza frecuentemente**: Documenta mientras implementas, no después
4. **Involucra al equipo**: SDD funciona mejor con adopción total
5. **Ajusta según necesites**: Los templates son guías, no camisas de fuerza
6. **Celebra las victorias**: Documenta cómo SDD te ayudó a evitar bugs

---

## 🔗 Enlaces Útiles

- Metodología completa: `shared/00-metodologia-trabajo.md`
- Template de requisitos: `shared/01-requirements.md`
- Template de arquitectura: `shared/02-architecture.md`
- Tracking de progreso: `shared/tracking/00-progress-overview.md`
- Issues log: `shared/tracking/03-issues-log.md`

---

**¿Preguntas?** Revisa `shared/00-metodologia-trabajo.md` para conceptos detallados.

**¿Listo para empezar?** Sigue [Paso 2: Setup Inicial](#-paso-2-setup-inicial)
