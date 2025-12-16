# 07 - Estructura del Proyecto Monorepo

> **Template Genérico para Monorepo** - Aplicable a Nx, Turborepo, Lerna, pnpm workspaces

## Propósito de este Documento

Este documento define la estructura estándar esperada para proyectos monorepo siguiendo la metodología SDD. La estructura es flexible y adaptable a diferentes herramientas y casos de uso.

---

## Estructura Base Recomendada

```
proyecto-monorepo/
│
├── .github/                                # Configuración GitHub
│   ├── workflows/                          # CI/CD pipelines
│   │   ├── ci.yml                          # Runs on: push, PR
│   │   ├── test.yml                        # Test all affected
│   │   ├── build.yml                       # Build all affected
│   │   └── deploy.yml                      # Deploy to prod
│   │
│   └── CODEOWNERS                          # Propietarios de código
│
├── docs/                                   # Documentación SDD compartida
│   ├── 00-metodologia-trabajo.md
│   ├── 01-requirements.md
│   ├── 02-architecture.md
│   ├── 07-project-structure-monorepo.md    # Este documento
│   ├── 08-configuration.md
│   ├── 11-workspace-organization.md
│   ├── architecture/
│   │   ├── monorepo-strategy.md            # Estrategia del monorepo
│   │   ├── module-boundaries.md            # Límites de módulos
│   │   ├── dependency-graph.md             # Gráfico de dependencias
│   │   └── integration-strategy.md         # Integración B2B
│   │
│   ├── guides/
│   │   ├── quick-start-guide.md
│   │   ├── adding-new-package.md           # Cómo agregar paquetes
│   │   ├── dependency-management.md        # Gestión de dependencias
│   │   ├── testing-strategy.md
│   │   └── deployment-strategy.md
│   │
│   └── tracking/
│       ├── 00-progress-overview.md
│       ├── 03-issues-log.md
│       └── 04-decisions-log.md
│
├── packages/                               # Paquetes reutilizables
│   │
│   ├── shared/                             # Código compartido
│   │   ├── ui-components/                  # Librería de componentes UI
│   │   │   ├── src/
│   │   │   │   ├── components/
│   │   │   │   ├── hooks/
│   │   │   │   ├── styles/
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── package.json
│   │   │   ├── tsconfig.json
│   │   │   ├── .eslintrc.json
│   │   │   └── README.md
│   │   │
│   │   ├── utilities/                      # Utilidades compartidas
│   │   │   ├── src/
│   │   │   │   ├── formatters/
│   │   │   │   ├── validators/
│   │   │   │   ├── helpers/
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── package.json
│   │   │   └── tsconfig.json
│   │   │
│   │   ├── types/                          # Tipos compartidos
│   │   │   ├── src/
│   │   │   │   ├── api.types.ts
│   │   │   │   ├── domain.types.ts
│   │   │   │   ├── common.types.ts
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── package.json
│   │   │   └── tsconfig.json
│   │   │
│   │   ├── api-client/                     # Cliente HTTP compartido
│   │   │   ├── src/
│   │   │   │   ├── base-client.ts
│   │   │   │   ├── interceptors/
│   │   │   │   ├── error-handler.ts
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── package.json
│   │   │   └── tsconfig.json
│   │   │
│   │   └── testing-utils/                  # Utilidades de testing
│   │       ├── src/
│   │       │   ├── mocks/
│   │       │   ├── fixtures/
│   │       │   ├── helpers/
│   │       │   └── index.ts
│   │       │
│   │       ├── package.json
│   │       └── tsconfig.json
│   │
│   ├── backend/                            # Backend como paquete
│   │   ├── src/
│   │   │   ├── main.ts
│   │   │   ├── app.module.ts
│   │   │   ├── config/
│   │   │   ├── modules/
│   │   │   ├── database/
│   │   │   └── common/
│   │   │
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── nest-cli.json
│   │   ├── .eslintrc.json
│   │   ├── jest.config.js
│   │   ├── Dockerfile
│   │   └── docker-compose.yml
│   │
│   └── frontend/                           # Frontend como paquete
│       ├── src/
│       │   ├── main.tsx
│       │   ├── App.tsx
│       │   ├── components/
│       │   ├── pages/
│       │   ├── features/
│       │   └── styles/
│       │
│       ├── public/
│       ├── package.json
│       ├── tsconfig.json
│       ├── vite.config.ts
│       ├── .eslintrc.json
│       ├── vitest.config.ts
│       └── index.html
│
├── apps/                                   # Aplicaciones (si es diferente a packages)
│   ├── backend/
│   ├── frontend/
│   ├── admin-panel/
│   ├── mobile/
│   └── api-docs/                           # Documentación API (Swagger)
│
├── tools/                                  # Herramientas y scripts
│   ├── scripts/
│   │   ├── generate-types.sh               # Genera tipos compartidos
│   │   ├── seed-database.sh                # Siembra BD
│   │   ├── build-all.sh                    # Build de todo
│   │   └── .gitkeep
│   │
│   └── generators/                         # Generadores de código (Nx)
│       ├── component-generator/
│       ├── module-generator/
│       └── .gitkeep
│
├── infra/                                  # Infraestructura
│   ├── docker/
│   │   ├── Dockerfile.api
│   │   ├── Dockerfile.web
│   │   └── Dockerfile.nginx
│   │
│   ├── kubernetes/
│   │   ├── deployments/
│   │   ├── services/
│   │   └── configmaps/
│   │
│   ├── terraform/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   │
│   └── nginx/
│       └── nginx.conf
│
├── test/                                   # Tests compartidos
│   ├── integration/
│   ├── e2e/
│   ├── performance/
│   └── fixtures/
│
├── .env.example                            # Template de .env
├── .env                                    # (Gitignored)
├── .gitignore
├── .prettierrc                             # Formato compartido
├── .eslintrc.json                          # Linter compartido
├── tsconfig.json                           # TypeScript base
├── tsconfig.build.json
│
├── package.json                            # Root package.json
├── pnpm-lock.yaml                          # pnpm lock (recomendado)
├── pnpm-workspace.yaml                     # Configuración workspaces
├── nx.json                                 # (Si usa Nx)
├── turbo.json                              # (Si usa Turborepo)
├── lerna.json                              # (Si usa Lerna)
│
├── README.md                               # README principal
├── CONTRIBUTING.md                         # Guía de contribución
├── LICENSE
└── .gitattributes
```

---

## Configuración del Workspace

### pnpm-workspace.yaml (Recomendado)

```yaml
packages:
  # Paquetes compartidos
  - 'packages/shared/**'
  # Aplicaciones
  - 'packages/backend'
  - 'packages/frontend'
  # Herramientas
  - 'tools/**'
```

### package.json (Root)

```json
{
  "name": "@[empresa]/monorepo",
  "version": "1.0.0",
  "description": "Monorepo para [proyecto]",
  "private": true,
  "type": "module",
  "engines": {
    "node": ">=18.0.0",
    "pnpm": ">=8.0.0"
  },
  "scripts": {
    "dev": "pnpm --filter ... --parallel run dev",
    "build": "pnpm --filter ... run build",
    "test": "pnpm --filter ... run test",
    "test:cov": "pnpm --filter ... run test:cov",
    "test:e2e": "pnpm --filter ... run test:e2e",
    "lint": "pnpm --filter ... run lint",
    "format": "pnpm --filter ... run format",
    "type-check": "pnpm --filter ... run type-check",
    "clean": "pnpm --filter ... run clean && rm -rf node_modules dist",
    "install-hooks": "husky install"
  },
  "devDependencies": {
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "@typescript-eslint/parser": "^6.0.0",
    "eslint": "^8.0.0",
    "prettier": "^3.0.0",
    "typescript": "^5.0.0"
  },
  "packageManager": "pnpm@8.0.0"
}
```

### Nx Configuration (nx.json)

```json
{
  "extends": "nx/presets/npm.json",
  "plugins": [
    {
      "plugin": "@nx/linter/eslint",
      "options": {
        "targetName": "lint"
      }
    }
  ],
  "nxCloud": {
    "accessToken": "[TOKEN]"
  },
  "defaultBase": "main",
  "tasksRunnerOptions": {
    "default": {
      "runner": "nx/tasks-runners/default",
      "options": {
        "cacheableOperations": ["build", "test", "lint", "type-check"],
        "parallel": 4
      }
    }
  }
}
```

### Turborepo Configuration (turbo.json)

```json
{
  "extends": ["//docs/shared-turbo-config.json"],
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**", ".next/**", "build/**"]
    },
    "test": {
      "outputs": ["coverage/**"],
      "cache": false
    },
    "lint": {
      "outputs": [".eslintcache"],
      "cache": true
    },
    "type-check": {
      "cache": true
    }
  },
  "globalDependencies": ["**/.env", ".env.example"]
}
```

---

## Estructura de un Paquete

### Paquete Simple (Librería)

```
packages/utilities/
├── src/
│   ├── formatters.ts
│   ├── validators.ts
│   ├── helpers.ts
│   └── index.ts
│
├── tests/
│   ├── formatters.spec.ts
│   ├── validators.spec.ts
│   └── helpers.spec.ts
│
├── dist/                           # (Generated)
├── .eslintrc.json
├── package.json
├── README.md
├── tsconfig.json
└── tsconfig.build.json
```

### Paquete Complejo (Aplicación)

```
packages/backend/
├── src/
│   ├── config/
│   ├── modules/
│   ├── database/
│   ├── common/
│   ├── main.ts
│   └── app.module.ts
│
├── test/
│   ├── integration/
│   └── e2e/
│
├── dist/                           # (Generated)
├── Dockerfile
├── docker-compose.yml
├── .eslintrc.json
├── .dockerignore
├── nest-cli.json
├── jest.config.js
├── package.json
├── README.md
├── tsconfig.json
├── tsconfig.build.json
└── tsconfig.spec.json
```

---

## Gestión de Dependencias

### Dependencias Compartidas (Root)

```json
{
  "devDependencies": {
    "typescript": "^5.0.0",
    "@types/node": "^20.0.0",
    "eslint": "^8.0.0",
    "prettier": "^3.0.0"
  }
}
```

### Dependencias de Paquete

```json
// packages/backend/package.json
{
  "name": "@[empresa]/backend",
  "version": "1.0.0",
  "dependencies": {
    "@nestjs/common": "^10.0.0",
    "@[empresa]/shared-types": "workspace:*"
  },
  "devDependencies": {
    "@nestjs/cli": "^10.0.0"
  }
}

// packages/frontend/package.json
{
  "name": "@[empresa]/frontend",
  "version": "1.0.0",
  "dependencies": {
    "react": "^18.0.0",
    "@[empresa]/ui-components": "workspace:*",
    "@[empresa]/shared-types": "workspace:*"
  },
  "devDependencies": {
    "@types/react": "^18.0.0"
  }
}
```

### Convención de Nombres de Paquetes

```
@[empresa]/backend         # Backend principal
@[empresa]/frontend        # Frontend principal
@[empresa]/ui-components   # Librería de componentes
@[empresa]/shared-types    # Tipos compartidos
@[empresa]/api-client      # Cliente HTTP
@[empresa]/utilities       # Utilidades
```

---

## Límites de Módulos

### Tag System (Nx)

```json
// nx.json
{
  "projects": {
    "backend": {
      "tags": ["type:app", "domain:core", "team:backend"]
    },
    "frontend": {
      "tags": ["type:app", "domain:ui", "team:frontend"]
    },
    "ui-components": {
      "tags": ["type:lib", "scope:shared", "team:frontend"]
    },
    "shared-types": {
      "tags": ["type:lib", "scope:shared"]
    }
  }
}
```

### Rules de Dependencias

```json
// nx.json
{
  "namedInputs": {
    "default": ["{projectRoot}/**/*"],
    "production": ["!{projectRoot}/**/*.spec.ts", "!{projectRoot}/**/*.test.ts"]
  },
  "targetDefaults": {
    "build": {
      "inputs": ["production", "^production"]
    }
  }
}
```

---

## CI/CD Pipeline

### GitHub Actions - Build Afectados

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  affected:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: pnpm/action-setup@v2
        with:
          version: 8

      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'pnpm'

      - run: pnpm install

      # Test de los paquetes afectados
      - run: pnpm nx affected -t test --parallel

      # Build de los paquetes afectados
      - run: pnpm nx affected -t build --parallel

      # Lint de los paquetes afectados
      - run: pnpm nx affected -t lint --parallel
```

### GitHub Actions - Deploy

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: pnpm/action-setup@v2
        with:
          version: 8

      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'pnpm'

      - run: pnpm install

      # Build backend
      - run: pnpm --filter @[empresa]/backend build
      - uses: docker/build-push-action@v5
        with:
          context: packages/backend
          push: true
          tags: gcr.io/[project]/backend:${{ github.sha }}

      # Build frontend
      - run: pnpm --filter @[empresa]/frontend build
      - uses: docker/build-push-action@v5
        with:
          context: packages/frontend
          push: true
          tags: gcr.io/[project]/frontend:${{ github.sha }}
```

---

## Checklist para Agregar Nuevo Paquete

- [ ] ✅ Crear directorio en `packages/`
- [ ] ✅ Crear `package.json` con nombre `@[empresa]/[nombre]`
- [ ] ✅ Crear `tsconfig.json` extiendiendo del root
- [ ] ✅ Crear `README.md` con descripción
- [ ] ✅ Crear estructura `src/` con `index.ts`
- [ ] ✅ Agregar scripts en `package.json`
- [ ] ✅ Configurar `.eslintrc.json`
- [ ] ✅ Actualizar `pnpm-workspace.yaml` si es necesario
- [ ] ✅ Agregar a root `nx.json` con tags
- [ ] ✅ Crear tests iniciales
- [ ] ✅ Documentar dependencias en README

---

## Comandos Comunes

```bash
# Instalar dependencias
pnpm install

# Desarrollo
pnpm dev                               # Todos los paquetes
pnpm --filter @[empresa]/backend dev   # Solo backend
pnpm --filter @[empresa]/frontend dev  # Solo frontend

# Build
pnpm build                             # Todos
pnpm nx affected -t build              # Solo afectados

# Testing
pnpm test                              # Todos
pnpm nx affected -t test               # Solo afectados
pnpm test:cov                          # Con cobertura

# Linting
pnpm lint                              # Todos
pnpm format                            # Formatear todo

# Limpieza
pnpm clean                             # Limpiar todos los dist/

# Análisis de dependencias
pnpm nx dep-graph                      # Grafo de dependencias
pnpm nx affected:dep-graph             # Grafo de afectados
```

---

## Convenciones

### Nombres de Paquetes

```
@[empresa]/[tipo]-[nombre]

Ejemplos:
@[empresa]/shared-types      # shared = compartido
@[empresa]/shared-ui         # shared = compartido
@[empresa]/shared-utils
@[empresa]/backend           # Sin prefijo = aplicación principal
@[empresa]/frontend          # Sin prefijo = aplicación principal
```

### Versionado Semántico

```
MAJOR.MINOR.PATCH

1.2.3
│ │ └─ PATCH (bug fixes)
│ └─── MINOR (new features)
└───── MAJOR (breaking changes)

Cambios de versión:
- Cambios breaking → MAJOR
- Nuevas features → MINOR
- Bug fixes → PATCH
```

---

## Checklist Monorepo

Antes de considerar el monorepo "listo":

- [ ] ✅ Todos los paquetes tienen `package.json` correcto
- [ ] ✅ `pnpm-workspace.yaml` o `nx.json` configurado
- [ ] ✅ CI/CD pipeline funcionando
- [ ] ✅ Todos los tests pasan
- [ ] ✅ Lint sin errores
- [ ] ✅ Documentación compartida actualizada
- [ ] ✅ Contribuidores pueden agregar paquetes fácilmente
- [ ] ✅ Dependencias compartidas en root
- [ ] ✅ Boundary rules implementadas
- [ ] ✅ Build afectados optimizado

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
