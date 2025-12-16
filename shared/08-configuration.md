# 08 - Configuración del Sistema

> **Template Genérico** - Define configuración del proyecto y setup

## Requisitos del Sistema

### Hardware Mínimo

**Desarrollo**:
- CPU: [Especificación mínima]
- RAM: [X] GB
- Disco: [X] GB libres
- Red: Conexión a internet

**Producción**:
- CPU: [Especificación mínima]
- RAM: [X] GB
- Disco: [X] GB libres
- Bandwidth: [X] Mbps

### Software Requerido

| Software | Versión Mínima | Versión Recomendada | Notas |
|----------|----------------|---------------------|-------|
| [Node.js/Python/etc.] | [X.Y] | [X.Y] | [Nota] |
| [Package Manager] | [X.Y] | [X.Y] | [Nota] |
| [Database] | [X.Y] | [X.Y] | [Nota] |
| [Docker] | [X.Y] | [X.Y] | Opcional para desarrollo |
| [Git] | [X.Y] | [X.Y] | Control de versiones |

---

## Instalación y Setup

### 1. Clonar Repositorio

```bash
git clone [REPOSITORY_URL]
cd [PROJECT_NAME]
```

### 2. Instalar Dependencias

```bash
# Instalar dependencias del proyecto
[PACKAGE_MANAGER] install

# Ejemplos:
# npm install
# pnpm install
# yarn install
# pip install -r requirements.txt
```

### 3. Configurar Variables de Entorno

Copiar archivo de ejemplo y personalizar:

```bash
cp .env.example .env
```

Editar `.env` con los valores apropiados (ver sección "Variables de Entorno" abajo).

### 4. Setup de Base de Datos (si aplica)

```bash
# Iniciar base de datos (si usa Docker)
docker-compose up -d [database-service]

# Ejecutar migraciones
[MIGRATION_COMMAND]

# Ejemplos:
# pnpm run migration:run
# npm run migrate
# python manage.py migrate
# npx prisma migrate dev

# (Opcional) Seed con datos de prueba
[SEED_COMMAND]
```

### 5. Verificar Instalación

```bash
# Ejecutar tests
[TEST_COMMAND]

# Ejemplos:
# pnpm test
# npm test
# pytest
# cargo test

# Verificar build
[BUILD_COMMAND]

# Ejemplos:
# pnpm run build
# npm run build
# python setup.py build
```

### 6. Iniciar Servidor de Desarrollo

```bash
# Modo desarrollo con hot reload
[DEV_COMMAND]

# Ejemplos:
# pnpm run start:dev
# npm run dev
# python manage.py runserver
# cargo run
```

El servidor debería estar corriendo en: `http://localhost:[PORT]`

---

## Variables de Entorno

### Archivo `.env.example`

```bash
# ==============================================
# CONFIGURACIÓN GENERAL
# ==============================================
NODE_ENV=development                    # development | staging | production
PORT=3000                               # Puerto del servidor
APP_NAME=[PROJECT_NAME]                 # Nombre de la aplicación
LOG_LEVEL=debug                         # error | warn | info | debug

# ==============================================
# BASE DE DATOS
# ==============================================
DATABASE_URL=postgresql://user:pass@localhost:5432/dbname
# O para MongoDB:
# DATABASE_URL=mongodb://localhost:27017/dbname

# Pool de conexiones (opcional)
DATABASE_POOL_MIN=2
DATABASE_POOL_MAX=10

# ==============================================
# AUTENTICACIÓN Y SEGURIDAD
# ==============================================
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRATION=24h                      # Expiración del token
JWT_REFRESH_SECRET=your-refresh-secret  # Para refresh tokens
JWT_REFRESH_EXPIRATION=7d

# Encriptación de contraseñas
BCRYPT_ROUNDS=10                        # Número de rounds para bcrypt

# ==============================================
# CACHE (Redis)
# ==============================================
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=                         # Dejar vacío si no hay password
REDIS_DB=0                              # Database number (0-15)
REDIS_TTL=3600                          # TTL por defecto en segundos

# ==============================================
# SERVICIOS EXTERNOS
# ==============================================
# API de terceros
EXTERNAL_API_URL=https://api.example.com
EXTERNAL_API_KEY=your-api-key-here

# Almacenamiento (S3/GCS/etc.)
STORAGE_PROVIDER=local                  # local | s3 | gcs
STORAGE_BUCKET=my-bucket
STORAGE_REGION=us-east-1
STORAGE_ACCESS_KEY=your-access-key
STORAGE_SECRET_KEY=your-secret-key

# Email (SMTP)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false                       # true para puerto 465
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# ==============================================
# MONITOREO Y OBSERVABILIDAD
# ==============================================
# Sentry (opcional)
SENTRY_DSN=https://[key]@sentry.io/[project]

# New Relic (opcional)
NEW_RELIC_LICENSE_KEY=your-license-key
NEW_RELIC_APP_NAME=[PROJECT_NAME]

# ==============================================
# CONFIGURACIÓN DE DESARROLLO
# ==============================================
# Swagger/OpenAPI
SWAGGER_ENABLED=true                    # Habilitar docs en /api/docs

# Debug mode
DEBUG=false                             # Más verbose logging

# Hot reload
WATCH_MODE=true

# ==============================================
# RATE LIMITING
# ==============================================
RATE_LIMIT_WINDOW_MS=60000              # 1 minuto en ms
RATE_LIMIT_MAX_REQUESTS=100             # Máximo requests por ventana

# ==============================================
# CORS
# ==============================================
CORS_ORIGIN=http://localhost:3000,http://localhost:5173
CORS_CREDENTIALS=true

# ==============================================
# FRONTEND (si aplica)
# ==============================================
VITE_API_URL=http://localhost:3000/api
NEXT_PUBLIC_API_URL=http://localhost:3000/api
```

### Validación de Variables de Entorno

**Archivo de validación** (ejemplo con Joi o Zod):

```typescript
import Joi from 'joi';

const envSchema = Joi.object({
  NODE_ENV: Joi.string()
    .valid('development', 'staging', 'production')
    .default('development'),
  PORT: Joi.number().default(3000),
  DATABASE_URL: Joi.string().required(),
  JWT_SECRET: Joi.string().required().min(32),
  // ... más validaciones
}).unknown();

export const validateEnv = () => {
  const { error, value } = envSchema.validate(process.env);
  if (error) {
    throw new Error(`Config validation error: ${error.message}`);
  }
  return value;
};
```

---

## Configuración por Entorno

### Development

**Propósito**: Desarrollo local

**Características**:
- Hot reload habilitado
- Debug mode activo
- Swagger/docs habilitados
- Base de datos local o Docker
- Sin autenticación estricta (opcional)
- Logs verbose

**Variables específicas**:
```bash
NODE_ENV=development
LOG_LEVEL=debug
SWAGGER_ENABLED=true
DEBUG=true
```

### Staging

**Propósito**: Testing pre-producción

**Características**:
- Simula producción lo más posible
- Base de datos separada de producción
- Autenticación habilitada
- Monitoreo habilitado
- Logs estructurados

**Variables específicas**:
```bash
NODE_ENV=staging
LOG_LEVEL=info
SWAGGER_ENABLED=true
DEBUG=false
```

### Production

**Propósito**: Usuarios finales

**Características**:
- Performance optimizado
- Seguridad máxima
- Monitoreo completo
- Backups automáticos
- Rate limiting estricto
- Logs a servicio externo

**Variables específicas**:
```bash
NODE_ENV=production
LOG_LEVEL=warn
SWAGGER_ENABLED=false
DEBUG=false
```

---

## Archivos de Configuración

### 1. Package Manager Config

**`package.json`** (Node.js):
```json
{
  "name": "[project-name]",
  "version": "1.0.0",
  "scripts": {
    "dev": "[comando desarrollo]",
    "build": "[comando build]",
    "start": "[comando producción]",
    "test": "[comando tests]",
    "lint": "[comando lint]",
    "format": "[comando format]"
  },
  "dependencies": {},
  "devDependencies": {}
}
```

**`pyproject.toml`** (Python):
```toml
[project]
name = "[project-name]"
version = "1.0.0"
dependencies = []

[project.scripts]
dev = "[comando desarrollo]"
```

### 2. Linter Config

**`.eslintrc.js`** (JavaScript/TypeScript):
```javascript
module.exports = {
  parser: '@typescript-eslint/parser',
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  rules: {
    // Personalizar reglas
  },
};
```

**`.pylintrc`** (Python):
```ini
[MASTER]
disable=
    C0111, # missing-docstring
    
[FORMAT]
max-line-length=100
```

### 3. Formatter Config

**`.prettierrc`**:
```json
{
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 80,
  "tabWidth": 2,
  "semi": true
}
```

### 4. TypeScript Config (si aplica)

**`tsconfig.json`**:
```json
{
  "compilerOptions": {
    "target": "ES2023",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "**/*.spec.ts"]
}
```

### 5. Docker Config

**`Dockerfile`**:
```dockerfile
FROM [base-image]:[version]

WORKDIR /app

COPY package*.json ./
RUN [install-command]

COPY . .
RUN [build-command]

EXPOSE [PORT]

CMD ["[start-command]"]
```

**`docker-compose.yml`**:
```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "[PORT]:[PORT]"
    environment:
      - NODE_ENV=development
    depends_on:
      - database
      - redis

  database:
    image: [db-image]:[version]
    environment:
      - [DB_ENV_VARS]
    volumes:
      - db-data:/var/lib/[database]

  redis:
    image: redis:alpine
    ports:
      - "6379:6379"

volumes:
  db-data:
```

### 6. Git Config

**`.gitignore`**:
```
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.pyc
__pycache__/

# Environment
.env
.env.local
.env.*.local

# IDE
.vscode/
.idea/
*.swp
*.swo

# Logs
logs/
*.log

# OS
.DS_Store
Thumbs.db

# Test coverage
coverage/
.nyc_output/

# Temporary files
tmp/
temp/
```

---

## Database Setup

### Migraciones

**Crear migración**:
```bash
[CREATE_MIGRATION_COMMAND] [nombre-descriptivo]

# Ejemplos:
# pnpm run migration:create add-users-table
# python manage.py makemigrations
# npx prisma migrate dev --name add-users-table
```

**Ejecutar migraciones**:
```bash
[RUN_MIGRATION_COMMAND]

# Ejemplos:
# pnpm run migration:run
# python manage.py migrate
# npx prisma migrate deploy
```

**Revertir migración**:
```bash
[REVERT_MIGRATION_COMMAND]

# Ejemplos:
# pnpm run migration:revert
# python manage.py migrate [app] [previous-migration]
# npx prisma migrate resolve --rolled-back [migration-name]
```

### Seeds

**Crear seed**:
```bash
[SEED_COMMAND]

# Ejemplos:
# pnpm run seed
# python manage.py loaddata fixtures/initial-data.json
# npx prisma db seed
```

---

## Testing Configuration

### Unit Tests

**Comando**:
```bash
[TEST_COMMAND]

# Ejemplos:
# pnpm test
# npm run test
# pytest
```

**Configuración** (`jest.config.js` ejemplo):
```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/src'],
  testMatch: ['**/*.spec.ts', '**/*.test.ts'],
  collectCoverageFrom: [
    'src/**/*.ts',
    '!src/**/*.spec.ts',
    '!src/**/*.test.ts',
  ],
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80,
    },
  },
};
```

### Integration/E2E Tests

**Comando**:
```bash
[E2E_COMMAND]

# Ejemplos:
# pnpm run test:e2e
# npm run test:integration
# pytest tests/integration
```

---

## CI/CD Setup

### GitHub Actions (ejemplo)

**`.github/workflows/ci.yml`**:
```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup [Runtime]
        uses: actions/setup-[runtime]@v3
        with:
          [runtime]-version: '[version]'
      
      - name: Install dependencies
        run: [install-command]
      
      - name: Lint
        run: [lint-command]
      
      - name: Test
        run: [test-command]
      
      - name: Build
        run: [build-command]
```

---

## Comandos Útiles

### Desarrollo

```bash
# Iniciar desarrollo
[dev-command]

# Linting
[lint-command]

# Formateo
[format-command]

# Tests
[test-command]

# Tests con coverage
[test-coverage-command]

# Tests en watch mode
[test-watch-command]
```

### Build y Deploy

```bash
# Build para producción
[build-command]

# Iniciar en producción
[start-prod-command]

# Generar documentación
[docs-command]
```

### Base de Datos

```bash
# Migración
[migration-command]

# Seed
[seed-command]

# Backup
[backup-command]

# Restore
[restore-command]
```

---

## Troubleshooting

### Problema 1: [Descripción del problema común]

**Síntomas**:
- [Síntoma 1]
- [Síntoma 2]

**Solución**:
```bash
# Pasos para resolver
[comando-solucion]
```

### Problema 2: [Otro problema común]

[Seguir mismo formato]

---

## Referencias

- [Documentación oficial de [framework]]: [URL]
- [Documentación de [database]]: [URL]
- [Guías de deployment]: [URL]

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
