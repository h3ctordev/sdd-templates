# 11 - Organización del Workspace Monorepo

> **Template Genérico para Organización de Workspace** - Mejores prácticas y patrones

## Propósito

Este documento define patrones, mejores prácticas y estrategias para organizar y mantener un monorepo saludable y escalable.

---

## Estrategias de Organización

### Estrategia 1: Por Tipo + Dominio

**Recomendado para**: Monorepos grandes con múltiples dominios

```
packages/
├── shared/
│   ├── types/
│   ├── ui/
│   ├── utils/
│   └── api-client/
│
├── core/                    # Dominio: Core
│   ├── backend
│   ├── database-migrations
│   └── shared-services
│
├── features/                # Dominio: Features
│   ├── auth-backend
│   ├── auth-frontend
│   ├── users-backend
│   ├── users-frontend
│   ├── tasks-backend
│   └── tasks-frontend
│
├── admin/                   # Dominio: Admin
│   ├── admin-backend
│   ├── admin-frontend
│   └── admin-shared
│
├── mobile/                  # Dominio: Mobile
│   ├── mobile-app
│   └── mobile-shared
│
└── infra/                   # Dominio: Infrastructure
    ├── docker-images
    ├── kubernetes-config
    └── terraform
```

### Estrategia 2: Por Aplicación

**Recomendado para**: Monorepos medianos con pocas aplicaciones

```
packages/
├── shared/
│   ├── types/
│   ├── ui/
│   └── utils/
│
├── backend/
│   ├── src/
│   ├── test/
│   └── package.json
│
├── frontend/
│   ├── src/
│   ├── test/
│   └── package.json
│
└── admin/
    ├── src/
    ├── test/
    └── package.json
```

### Estrategia 3: Monorepo Escalado (Google/Meta style)

**Recomendado para**: Monorepos muy grandes con múltiples equipos

```
packages/
├── common/                  # Completamente compartido
│   ├── types/
│   ├── exceptions/
│   ├── utils/
│   ├── constants/
│   └── testing/
│
├── internal/                # Uso interno (no para exportar)
│   ├── scripts/
│   ├── generators/
│   ├── config/
│   └── plugins/
│
├── experimental/            # Features experimentales
│   ├── feature-x/
│   └── feature-y/
│
├── team-a/                  # Owned by Team A
│   ├── api-backend/
│   ├── api-frontend/
│   ├── shared/
│   └── services/
│
├── team-b/                  # Owned by Team B
│   ├── dashboard-backend/
│   ├── dashboard-frontend/
│   ├── shared/
│   └── services/
│
└── team-c/                  # Owned by Team C
    ├── admin-backend/
    ├── admin-frontend/
    ├── shared/
    └── services/
```

---

## Directrices de Organización

### Principio 1: Cohesión Alta

Los paquetes relacionados deben estar juntos.

**❌ BAD**:

```
packages/
├── types/
├── user-types/
├── backend/
├── backend-types/
├── frontend/
├── frontend-utils/
```

**✅ GOOD**:

```
packages/
├── shared/
│   ├── types/
│   └── utils/
├── backend/
├── frontend/
```

### Principio 2: Acoplamiento Bajo

Los paquetes deben ser independientes.

**❌ BAD - Alto acoplamiento**:

```
// packages/auth-backend/src/index.ts
export { authService } from './services/auth.service';

// packages/users-backend/src/index.ts
import { authService } from '@[empresa]/auth-backend';
// Uso directo de implementation detail ❌
```

**✅ GOOD - Bajo acoplamiento**:

```
// packages/shared-types/src/auth.types.ts
export interface AuthToken { /* ... */ }

// packages/auth-backend/src/index.ts
export type { AuthToken } from '@[empresa]/shared-types';
export { getTokenPayload } from './utils/token.utils';

// packages/users-backend/src/index.ts
import type { AuthToken } from '@[empresa]/shared-types';
// Depende de tipos públicos, no de implementation ✅
```

### Principio 3: Cambios Localizados

Los cambios deben afectar el menor número de paquetes posible.

**❌ BAD - Cambios ripple**:

```
Si cambio API de shared/types/
  → Afecta: backend, frontend, mobile, admin
  → 6+ paquetes necesitan update
```

**✅ GOOD - Cambios localizados**:

```
Si cambio API de shared/types/
  → Creo versión 2.0.0
  → Los packages gradualmente migran
  → Puedo mantener ambas versiones
```

---

## Gestión de Dependencias

### Matriz de Dependencias Permitidas

```
           ↓ Puede depender de →

       shared/  backend/  frontend/  mobile/
shared/   ✓       ✗         ✗         ✗
backend/  ✓       ✓         ✗         ✗
frontend/ ✓       ✗         ✓         ✗
mobile/   ✓       ✗         ✗         ✓
infra/    ✓       ✓         ✓         ✓

Regla: No hay dependencias hacia arriba
```

### Ejemplo: Estructura de Dependencias Válida

```
shared/types ← shared/utils ← shared/api-client
              ↓               ↓
            backend ←→ frontend
```

### Herramientas para Validar Dependencias

**Nx**:

```bash
# Visualizar grafo de dependencias
pnpm nx dep-graph

# Validar límites
pnpm nx lint --rules @nx/enforce-module-boundaries
```

**Lerna + Madge**:

```bash
# Detectar ciclos
madge --circular --extensions ts,tsx src/

# Generar grafo
madge --image dependency-graph.png src/
```

---

## Patrones de Integración

### Patrón 1: Compartir Tipos

```
shared/types/
├── user.types.ts
├── api.types.ts
├── domain.types.ts
└── index.ts

Exports: Types ONLY (0 runtime code)
Dependencias: NONE
```

```typescript
// packages/backend/src/modules/user/user.service.ts
import type { User, CreateUserDto } from '@[empresa]/shared-types';

// Usa tipos pero no lógica ✅
export class UserService {
  async create(dto: CreateUserDto): Promise<User> {
    /* ... */
  }
}
```

### Patrón 2: Compartir Utilidades

```
shared/utils/
├── formatters.ts      # Lógica pura, 0 dependencias
├── validators.ts      # Lógica pura
├── helpers.ts
└── index.ts

Exports: Funciones puras
Dependencias: Solo shared/types
```

```typescript
// packages/frontend/src/components/UserCard.tsx
import { formatDate } from '@[empresa]/shared-utils';

export const UserCard = ({ user }: Props) => (
  <div>
    <h3>{user.name}</h3>
    <p>Joined: {formatDate(user.createdAt)}</p>
  </div>
);
```

### Patrón 3: Cliente API Compartido

```
shared/api-client/
├── api-client.ts      # Instancia de Axios/Fetch
├── interceptors/      # Lógica de interceptors
├── error-handler.ts
└── index.ts

Exports: Instancia preconfigurada
Dependencias: shared/types, shared/utils
```

```typescript
// shared/api-client/src/index.ts
import axios from 'axios';
import { handleError } from './error-handler';

export const apiClient = axios.create({
  baseURL: process.env.REACT_APP_API_URL,
  timeout: 10000,
});

apiClient.interceptors.response.use(
  (response) => response,
  (error) => handleError(error),
);
```

### Patrón 4: Feature Compartida (Monolito Distribuido)

```
features/auth/
├── auth-types/       # Tipos de auth
│   ├── src/
│   │   ├── user.types.ts
│   │   ├── token.types.ts
│   │   └── index.ts
│   └── package.json
│
├── auth-services/    # Servicios (backend)
│   ├── src/
│   │   ├── auth.service.ts
│   │   ├── token.service.ts
│   │   └── index.ts
│   └── package.json
│
├── auth-components/  # Componentes (frontend)
│   ├── src/
│   │   ├── LoginForm.tsx
│   │   ├── RegisterForm.tsx
│   │   └── index.ts
│   └── package.json
│
└── auth-hooks/       # Hooks (frontend)
    ├── src/
    │   ├── useAuth.ts
    │   └── index.ts
    └── package.json
```

---

## Versionado y Releases

### Estrategia 1: Versiones Independientes (Recomendado)

Cada paquete tiene su propia versión.

```
@[empresa]/shared-types: 2.0.0
@[empresa]/backend: 1.5.2
@[empresa]/frontend: 3.1.0
```

**Ventajas**:

- Flexibilidad
- Cambios no fuerzan releases de otros paquetes
- Mejor seguimiento de compatibilidad

**Herramientas**: Lerna, Changesets

### Estrategia 2: Versión Única (Monolitica)

Todos los paquetes usan la misma versión.

```
monorepo: 1.2.3

@[empresa]/shared-types: 1.2.3
@[empresa]/backend: 1.2.3
@[empresa]/frontend: 1.2.3
```

**Ventajas**:

- Simplicidad
- Garantiza compatibilidad entre paquetes

**Desventajas**:

- Releases innecesarios
- Difícil de escalar

---

## CODEOWNERS y Ownership

### CODEOWNERS File

```
# .github/CODEOWNERS

# Shared code
/packages/shared/types/           @team-frontend @team-backend
/packages/shared/utils/           @team-frontend @team-backend
/packages/shared/api-client/      @team-frontend

# Backend owned by Team Backend
/packages/backend/                @team-backend
/packages/auth-services/          @team-backend

# Frontend owned by Team Frontend
/packages/frontend/               @team-frontend
/packages/ui-components/          @team-frontend

# Infra owned by DevOps
/infra/                           @devops-team
/.github/workflows/               @devops-team
/docker*/                         @devops-team
```

### Tags de Propietario (Nx)

```json
// nx.json
{
  "projects": {
    "backend": {
      "tags": ["type:app", "owner:backend-team"]
    },
    "frontend": {
      "tags": ["type:app", "owner:frontend-team"]
    },
    "ui-components": {
      "tags": ["type:lib", "scope:shared", "owner:frontend-team"]
    }
  }
}
```

---

## Documentación del Workspace

### README Raíz

```markdown
# [Proyecto] Monorepo

Monorepo con [X] packages que incluye:

- Backend (NestJS)
- Frontend (React)
- Librerías compartidas

## Quick Start

\`\`\`bash
pnpm install
pnpm dev
\`\`\`

## Estructura

- `packages/shared/` - Código compartido
- `packages/backend/` - API principal
- `packages/frontend/` - Web principal
- `docs/` - Documentación SDD

## Guías

- [Agregar nuevo package](docs/guides/adding-new-package.md)
- [Contribuir](CONTRIBUTING.md)
- [Arquitectura](docs/architecture/)
```

### Documentación de Paquetes

```
packages/backend/
├── README.md                    # Cómo ejecutar
├── src/                         # Código
└── docs/                        # Documentación específica
    ├── api.md                   # Documentación API
    ├── database.md              # Schema y migrations
    └── modules.md               # Descripción de módulos
```

---

## Scripts Comunes del Workspace

### package.json (Root)

```json
{
  "scripts": {
    "// ============ Development ============": "",
    "dev": "pnpm --filter ... --parallel run dev",
    "dev:backend": "pnpm --filter @[empresa]/backend run dev",
    "dev:frontend": "pnpm --filter @[empresa]/frontend run dev",

    "// ============ Building ============": "",
    "build": "pnpm --filter ... run build",
    "build:affected": "pnpm nx affected -t build",

    "// ============ Testing ============": "",
    "test": "pnpm --filter ... run test",
    "test:affected": "pnpm nx affected -t test",
    "test:cov": "pnpm --filter ... run test:cov",
    "test:e2e": "pnpm --filter ... run test:e2e",

    "// ============ Linting & Formatting ============": "",
    "lint": "pnpm --filter ... run lint",
    "lint:affected": "pnpm nx affected -t lint",
    "format": "prettier --write .",
    "type-check": "pnpm --filter ... run type-check",

    "// ============ Utilities ============": "",
    "clean": "pnpm --filter ... run clean && rm -rf node_modules",
    "reinstall": "pnpm clean && pnpm install",
    "graph": "pnpm nx dep-graph"
  }
}
```

---

## Checklist de Salud del Monorepo

Ejecutar regularmente:

```bash
# 1. Verificar dependencias circulares
pnpm nx affected --criticalPath

# 2. Verificar imports correctos
pnpm lint

# 3. Verificar todos los tests pasan
pnpm test

# 4. Verificar type checking
pnpm type-check

# 5. Ver grafo de dependencias
pnpm nx dep-graph

# 6. Verificar tamaño de bundles
pnpm nx run @[empresa]/frontend:build --stats-json
```

### Pre-commit Hook

```bash
#!/bin/sh
# .husky/pre-commit

echo "🔍 Running pre-commit checks..."

# Lint archivos changed
pnpm nx affected --base origin/main -t lint --parallel

if [ $? -ne 0 ]; then
  echo "❌ Lint failed"
  exit 1
fi

# Type checking
pnpm nx affected --base origin/main -t type-check --parallel

if [ $? -ne 0 ]; then
  echo "❌ Type checking failed"
  exit 1
fi

echo "✅ All checks passed"
```

---

## Patrones Avanzados

### Patrón: Monorepo Distribuido con Microservicios

```
packages/
├── core-types/
├── shared-utils/
├── api-gateway/          # Kong/Nginx config
├── services/
│   ├── auth-service/
│   ├── user-service/
│   ├── task-service/
│   ├── notification-service/
│   └── file-service/
├── frontend/
├── admin-frontend/
└── infrastructure/
```

**Comunicación**:

- Services → API Gateway → Frontend
- Services ← Message Queue (RabbitMQ/Kafka)
- Shared types vía paquete `core-types`

### Patrón: Backend for Frontend (BFF)

```
packages/
├── core-api/             # API principal con toda lógica
├── web-bff/              # BFF para web, consume core-api
├── mobile-bff/           # BFF para mobile, consume core-api
├── web-frontend/
├── mobile-app/
└── shared/
```

**Ventaja**: Diferentes frontends pueden tener diferentes necesidades

---

## Troubleshooting Común

### Problema: Build Lento

**Síntomas**: `pnpm build` toma > 10 minutos

**Soluciones**:

1. Usar `pnpm nx affected -t build` (solo afectados)
2. Habilitar distributed caching (Nx Cloud)
3. Revisar dependencias circulares
4. Optimizar imports (tree-shaking)

### Problema: Dependencias Circulares

**Síntomas**: Imports falla, hoisting issues

**Solución**:

```bash
# Detectar
pnpm nx dep-graph | grep "circular"

# Refactorizar - Extraer tipos a paquete intermedio
packages/shared/types/ ← backend ← frontend (eliminar backend ← frontend)
```

### Problema: Versiones Conflictivas

**Síntomas**: `npm ERR! peer dep missing`

**Solución**:

```json
// pnpm-workspace.yaml
catalogs:
  default:
    react: "^18.0.0"
    react-dom: "^18.0.0"

// package.json
{
  "dependencies": {
    "react": "@catalog"
  }
}
```

---

## Checklist Final

- [ ] ✅ Estructura clara y entendible
- [ ] ✅ Dependencias acíclicas
- [ ] ✅ Ownership definido (CODEOWNERS)
- [ ] ✅ Documentación actualizada
- [ ] ✅ CI/CD pipeline optimizado
- [ ] ✅ Scripts de desarrollo documentados
- [ ] ✅ Procesos de release claros
- [ ] ✅ Guidelines de contribución
- [ ] ✅ Pre-commit hooks configurados
- [ ] ✅ Matriz de dependencias validada

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
