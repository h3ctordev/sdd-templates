# 07 - Estructura del Proyecto Backend

> **Template Genérico para Backend** - Aplicable a NestJS, Express, FastAPI, Django, Spring Boot, etc.

## Propósito de este Documento

Este documento define la estructura estándar esperada para proyectos backend siguiendo la metodología SDD. La estructura es flexible y adaptable a cualquier framework o lenguaje de backend.

---

## Estructura Base Recomendada

```
proyecto-backend/
│
├── .github/                                # Configuración GitHub
│   └── workflows/                          # CI/CD pipelines
│       ├── ci.yml
│       ├── test.yml
│       └── deploy.yml
│
├── docs/                                   # Documentación SDD (IMPORTANTE)
│   ├── 00-metodologia-trabajo.md
│   ├── 01-requirements.md
│   ├── 02-architecture.md
│   ├── 07-project-structure-backend.md     # Este documento
│   ├── 08-configuration.md
│   ├── 09-api-documentation.md
│   ├── api/                                # Documentación de API
│   │   ├── endpoints.md
│   │   └── examples.md
│   ├── guides/
│   │   ├── quick-start-guide.md
│   │   ├── database-setup.md
│   │   └── deployment.md
│   └── tracking/                           # Tracking de progreso
│       ├── 00-progress-overview.md
│       ├── 03-issues-log.md
│       └── 04-decisions-log.md
│
├── src/                                    # Código fuente principal
│   │
│   ├── common/                             # Recursos compartidos entre módulos
│   │   │
│   │   ├── decorators/                     # Decoradores personalizados (NestJS)
│   │   │   ├── validate.decorator.ts
│   │   │   ├── auth.decorator.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── filters/                        # Filtros de excepciones globales
│   │   │   ├── http-exception.filter.ts
│   │   │   ├── all-exceptions.filter.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── guards/                         # Guards de autenticación/autorización
│   │   │   ├── auth.guard.ts
│   │   │   ├── roles.guard.ts
│   │   │   ├── rate-limit.guard.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── interfaces/                     # Interfaces compartidas SOLO
│   │   │   ├── user.interface.ts
│   │   │   ├── auth.interface.ts
│   │   │   ├── paginated.interface.ts
│   │   │   ├── error.interface.ts
│   │   │   └── index.ts                    # Barrel file
│   │   │
│   │   ├── exceptions/                     # Excepciones personalizadas
│   │   │   ├── unauthorized.exception.ts
│   │   │   ├── validation-error.exception.ts
│   │   │   ├── not-found.exception.ts
│   │   │   ├── conflict.exception.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── middleware/                     # Middleware global
│   │   │   ├── request-logger.middleware.ts
│   │   │   ├── cors.middleware.ts
│   │   │   ├── request-id.middleware.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── utils/                          # Utilidades compartidas
│   │   │   ├── date.utils.ts
│   │   │   ├── string.utils.ts
│   │   │   ├── validation.utils.ts
│   │   │   ├── crypto.utils.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── constants/                      # Constantes globales
│   │   │   ├── http-status.constants.ts
│   │   │   ├── error-codes.constants.ts
│   │   │   ├── messages.constants.ts       # Mensajes para usuario (español)
│   │   │   └── index.ts
│   │   │
│   │   └── test/                           # Helpers para testing
│   │       ├── mock.factory.ts
│   │       ├── mock.builder.ts
│   │       └── index.ts
│   │
│   ├── config/                             # Configuración centralizada
│   │   ├── app.config.ts                   # Configuración general
│   │   ├── database.config.ts              # Configuración de BD
│   │   ├── cache.config.ts                 # Configuración de cache
│   │   ├── auth.config.ts                  # Configuración de autenticación
│   │   ├── logging.config.ts               # Configuración de logging
│   │   ├── rate-limit.config.ts            # Rate limiting
│   │   ├── cors.config.ts                  # CORS config
│   │   ├── validation.config.ts            # Validación global
│   │   └── index.ts                        # Barrel file
│   │
│   ├── database/                           # Capa de persistencia
│   │   ├── schemas/                        # Modelos de datos (Mongoose, SQLAlchemy, etc.)
│   │   │   ├── user.schema.ts
│   │   │   ├── base.schema.ts              # Schema base con timestamps
│   │   │   ├── audit.schema.ts             # Para auditoría
│   │   │   └── index.ts
│   │   │
│   │   ├── migrations/                     # Migraciones de BD
│   │   │   ├── 001_create_users_table.ts
│   │   │   └── .gitkeep
│   │   │
│   │   ├── seeds/                          # Seeds para datos iniciales
│   │   │   ├── seed-admin.ts
│   │   │   ├── seed-roles.ts
│   │   │   └── index.ts
│   │   │
│   │   └── database.module.ts              # Módulo de conexión
│   │
│   ├── modules/                            # Módulos de dominio (business logic)
│   │   │
│   │   ├── auth/                           # Ejemplo: Módulo de autenticación
│   │   │   ├── dto/                        # Data Transfer Objects
│   │   │   │   ├── login.dto.ts
│   │   │   │   ├── register.dto.ts
│   │   │   │   ├── refresh-token.dto.ts
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── entities/                   # Entidades de dominio (si no usa schema)
│   │   │   │   ├── user.entity.ts
│   │   │   │   └── token.entity.ts
│   │   │   │
│   │   │   ├── strategies/                 # Estrategias de autenticación
│   │   │   │   ├── jwt.strategy.ts
│   │   │   │   ├── local.strategy.ts       # (si usa)
│   │   │   │   ├── google.strategy.ts      # (si usa OAuth)
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── guards/                     # Guards específicos del módulo
│   │   │   │   ├── jwt-auth.guard.ts
│   │   │   │   └── optional-jwt.guard.ts
│   │   │   │
│   │   │   ├── decorators/                 # Decoradores específicos del módulo
│   │   │   │   ├── current-user.decorator.ts
│   │   │   │   └── public.decorator.ts
│   │   │   │
│   │   │   ├── auth.module.ts              # Definición del módulo
│   │   │   ├── auth.controller.ts          # API endpoints
│   │   │   ├── auth.service.ts             # Lógica de negocio
│   │   │   ├── auth.service.spec.ts        # Unit tests
│   │   │   ├── auth.repository.ts          # Acceso a datos
│   │   │   ├── auth.repository.spec.ts
│   │   │   └── auth-validator.ts           # Validación de dominio
│   │   │
│   │   ├── users/                          # Módulo de usuarios (estructura similar)
│   │   │   ├── dto/
│   │   │   ├── entities/
│   │   │   ├── users.module.ts
│   │   │   ├── users.controller.ts
│   │   │   ├── users.service.ts
│   │   │   ├── users.service.spec.ts
│   │   │   ├── users.repository.ts
│   │   │   └── users.repository.spec.ts
│   │   │
│   │   └── [otros-modulos]/                # Mismo patrón para otros módulos
│   │       ├── dto/
│   │       ├── [nombre].module.ts
│   │       ├── [nombre].controller.ts
│   │       ├── [nombre].service.ts
│   │       ├── [nombre].service.spec.ts
│   │       ├── [nombre].repository.ts
│   │       └── [nombre].repository.spec.ts
│   │
│   ├── queue/                              # Cola de mensajes/jobs (si aplica)
│   │   ├── jobs/
│   │   │   ├── send-email.job.ts
│   │   │   ├── process-image.job.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── queue.module.ts
│   │   └── queue.service.ts
│   │
│   ├── scheduler/                          # Tareas programadas (si aplica)
│   │   ├── tasks/
│   │   │   ├── cleanup-expired-tokens.task.ts
│   │   │   ├── generate-daily-report.task.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── scheduler.module.ts
│   │   └── scheduler.service.ts
│   │
│   ├── app.module.ts                       # Módulo raíz
│   ├── app.controller.ts                   # Controlador raíz
│   ├── app.service.ts                      # Servicio raíz
│   ├── main.ts                             # Entry point
│   └── logger.ts                           # Configuración de logging
│
├── test/                                   # Tests (separados de src/)
│   ├── integration/                        # Integration tests
│   │   ├── auth.integration.spec.ts
│   │   ├── users.integration.spec.ts
│   │   └── fixtures/
│   │
│   ├── e2e/                                # End-to-End tests
│   │   ├── auth.e2e-spec.ts
│   │   ├── users.e2e-spec.ts
│   │   └── jest-e2e.json
│   │
│   └── helpers/                            # Helpers compartidos para tests
│       ├── test-database.helper.ts
│       ├── test-request.helper.ts
│       └── factories/
│
├── logs/                                   # Archivos de log (gitignored)
│   └── .gitkeep
│
├── scripts/                                # Scripts útiles
│   ├── seed-database.sh
│   ├── migrate-database.sh
│   ├── generate-docs.sh
│   └── .gitkeep
│
├── .env.example                            # Template de variables de entorno
├── .env                                    # (Gitignored) Desarrollo local
├── .env.test                               # (Gitignored) Testing
├── .gitignore
├── .prettierrc                             # Formatter config
├── .eslintrc.js                            # Linter config (si JavaScript/TypeScript)
├── tsconfig.json                           # TypeScript config (si aplica)
├── tsconfig.build.json                     # TypeScript build config
├── jest.config.js                          # Testing config
├── docker-compose.yml                      # Local development
├── Dockerfile                              # Production image
├── docker-compose.prod.yml                 # Production stack
│
├── package.json                            # Package manager (Node.js)
├── pnpm-lock.yaml                          # Lock file
├── README.md                               # Readme del proyecto
├── LICENSE
└── .gitattributes                          # Git attributes
```

---

## Convenciones de Nombres

### Archivos

| Tipo                 | Convención                     | Ejemplo                                    |
| -------------------- | ------------------------------ | ------------------------------------------ |
| **Módulo**           | `[nombre].module.ts`           | `auth.module.ts`                           |
| **Controlador**      | `[nombre].controller.ts`       | `users.controller.ts`                      |
| **Servicio**         | `[nombre].service.ts`          | `auth.service.ts`                          |
| **Repository**       | `[nombre].repository.ts`       | `users.repository.ts`                      |
| **DTO**              | `[action]-[entity].dto.ts`     | `create-user.dto.ts`, `update-user.dto.ts` |
| **Entity**           | `[nombre].entity.ts`           | `user.entity.ts`                           |
| **Schema**           | `[nombre].schema.ts`           | `user.schema.ts`                           |
| **Guard**            | `[nombre].guard.ts`            | `jwt-auth.guard.ts`                        |
| **Decorator**        | `[nombre].decorator.ts`        | `public.decorator.ts`                      |
| **Filter**           | `[nombre].filter.ts`           | `http-exception.filter.ts`                 |
| **Middleware**       | `[nombre].middleware.ts`       | `request-logger.middleware.ts`             |
| **Util**             | `[nombre].utils.ts`            | `date.utils.ts`                            |
| **Constant**         | `[nombre].constants.ts`        | `error-codes.constants.ts`                 |
| **Test**             | `[nombre].spec.ts`             | `auth.service.spec.ts`                     |
| **E2E Test**         | `[nombre].e2e-spec.ts`         | `auth.e2e-spec.ts`                         |
| **Integration Test** | `[nombre].integration.spec.ts` | `auth.integration.spec.ts`                 |

### Directorios

- **snake_case para módulos**: `user-management`, `payment-processing`
- **camelCase para funcionalidad**: `src/common/decorators`
- **plural para colecciones**: `modules`, `schemas`, `migrations`
- **singular para archivos**: `user.schema.ts` (no `users.schema.ts`)

---

## Estructura de Módulos

### Módulo Estándar

Cada módulo debe seguir esta estructura:

```
src/modules/[nombre-modulo]/
├── dto/                          # Data Transfer Objects
│   ├── create-[entity].dto.ts
│   ├── update-[entity].dto.ts
│   ├── list-query.dto.ts         # Para queries con paginación
│   └── index.ts                  # Barrel export
│
├── entities/ (si no usa schemas)  # O usar schemas en src/database
│   ├── [entity].entity.ts
│   └── index.ts
│
├── [nombre].module.ts             # Definición del módulo
├── [nombre].controller.ts          # Endpoints HTTP
├── [nombre].service.ts             # Lógica de negocio
├── [nombre].service.spec.ts        # Unit tests del service
├── [nombre].repository.ts          # Acceso a datos
├── [nombre].repository.spec.ts     # Unit tests del repository
└── [nombre]-validator.ts           # Validación de dominio
```

### Ejemplo: Módulo de Usuarios

```typescript
// users.module.ts
import { Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { UsersController } from './users.controller';
import { UsersRepository } from './users.repository';

@Module({
  controllers: [UsersController],
  providers: [UsersService, UsersRepository],
  exports: [UsersService], // Exportar si otros módulos lo necesitan
})
export class UsersModule {}
```

---

## Patrones Arquitectónicos

### 1. Repository Pattern (OBLIGATORIO)

**Regla**: Los services NUNCA acceden directamente a la base de datos. SIEMPRE usan repositories.

**Incorrecto**:

```typescript
// ❌ BAD
@Injectable()
export class UsersService {
  constructor(@InjectModel(User.name) private userModel: Model<UserDocument>) {}

  async findById(id: string) {
    return this.userModel.findById(id); // Acceso directo a modelo ❌
  }
}
```

**Correcto**:

```typescript
// ✅ GOOD
@Injectable()
export class UsersRepository {
  constructor(@InjectModel(User.name) private userModel: Model<UserDocument>) {}

  async findById(id: string) {
    return this.userModel.findById(id);
  }
}

@Injectable()
export class UsersService {
  constructor(private readonly usersRepository: UsersRepository) {}

  async getUserById(id: string) {
    return this.usersRepository.findById(id); // Acceso via repository ✅
  }
}
```

### 2. Dependency Injection (OBLIGATORIO)

**Inyectar via constructor**, no usar lookups manuales.

```typescript
// ✅ GOOD
@Injectable()
export class UsersService {
  constructor(
    private readonly usersRepository: UsersRepository,
    private readonly emailService: EmailService,
  ) {}
}
```

### 3. DTOs para Validación

**Usar DTOs** para validación de entrada en endpoints.

```typescript
// create-user.dto.ts
import { IsEmail, IsString, MinLength } from 'class-validator';

export class CreateUserDto {
  @IsEmail()
  email: string;

  @IsString()
  @MinLength(6)
  password: string;

  @IsString()
  name: string;
}

// users.controller.ts
@Post()
async create(@Body() createUserDto: CreateUserDto) {
  return this.usersService.create(createUserDto);
}
```

### 4. Error Handling Consistente

**Usar excepciones personalizadas** para errores de lógica de negocio.

```typescript
// common/exceptions/user-not-found.exception.ts
import { NotFoundException } from '@nestjs/common';

export class UserNotFoundException extends NotFoundException {
  constructor(userId: string) {
    super(`User with ID "${userId}" not found`);
  }
}

// En el service:
async getUserById(id: string) {
  const user = await this.repository.findById(id);
  if (!user) {
    throw new UserNotFoundException(id);
  }
  return user;
}
```

---

## Layers (Capas)

### Capa de Presentación (Controllers)

**Responsabilidad**:

- Recibir requests HTTP
- Validar inputs (usando DTOs)
- Llamar al service
- Formatear responses
- NO contiene lógica de negocio

**Reglas**:

- Los controllers son thin (delgados)
- Toda lógica va en services
- Validaciones via DTOs + class-validator

```typescript
@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get(':id')
  async getUser(@Param('id') id: string) {
    // Controller delgado: solo orquesta
    return this.usersService.getUserById(id);
  }

  @Post()
  async createUser(@Body() dto: CreateUserDto) {
    // DTO se valida automáticamente
    return this.usersService.create(dto);
  }
}
```

### Capa de Lógica de Negocio (Services)

**Responsabilidad**:

- Implementar lógica de negocio
- Coordinar operaciones
- Validar reglas de negocio
- Usar repositories para datos
- NO hacer validación de HTTP/request

**Reglas**:

- Services usan repositories para datos
- Servicios pueden usar otros servicios
- Toda lógica compleja aquí
- Lanzar excepciones de negocio

```typescript
@Injectable()
export class UsersService {
  constructor(
    private readonly usersRepository: UsersRepository,
    private readonly emailService: EmailService,
  ) {}

  async create(dto: CreateUserDto) {
    // 1. Validar lógica de negocio
    const existingUser = await this.usersRepository.findByEmail(dto.email);
    if (existingUser) {
      throw new ConflictException('Email already registered');
    }

    // 2. Operaciones relacionadas
    const hashedPassword = await hash(dto.password);
    const user = await this.usersRepository.create({
      ...dto,
      password: hashedPassword,
    });

    // 3. Side effects
    await this.emailService.sendWelcomeEmail(user.email);

    return user;
  }
}
```

### Capa de Acceso a Datos (Repositories)

**Responsabilidad**:

- Único lugar que accede a BD
- Convertir modelos de BD a entidades
- Queries optimizadas
- NO contiene lógica de negocio

**Reglas**:

- Retorna entidades de dominio
- Nunca modelos de BD crudos
- Manejo de errores de BD
- Índices y optimizaciones

```typescript
@Injectable()
export class UsersRepository {
  constructor(@InjectModel(User.name) private userModel: Model<UserDocument>) {}

  async findById(id: string): Promise<User | null> {
    return this.userModel.findById(id).lean().exec();
  }

  async findByEmail(email: string): Promise<User | null> {
    return this.userModel.findOne({ email }).lean().exec();
  }

  async create(data: CreateUserInput): Promise<User> {
    const user = new this.userModel(data);
    return user.save();
  }
}
```

---

## Testing Strategy

### Unit Tests (src/\*_/_.spec.ts)

**Para**: Services, repositories, utilities

**Ubicación**: Co-located con el código

**Ejemplo**:

```typescript
// users.service.spec.ts
describe('UsersService', () => {
  let service: UsersService;
  let repository: MockType<UsersRepository>;

  beforeEach(() => {
    // Setup
  });

  it('should create user successfully', async () => {
    // Arrange
    const dto = { email: 'test@example.com', password: '123456' };

    // Act
    const result = await service.create(dto);

    // Assert
    expect(result.email).toBe(dto.email);
  });

  it('should throw if email already exists', async () => {
    // Arrange
    repository.findByEmail.mockResolvedValueOnce({ email: 'test@example.com' });

    // Act & Assert
    await expect(service.create(dto)).rejects.toThrow(ConflictException);
  });
});
```

### Integration Tests (test/integration/\*.spec.ts)

**Para**: Flujos completos de módulos

**Ejemplo**:

```typescript
// test/integration/users.integration.spec.ts
describe('Users Module Integration', () => {
  let app: INestApplication;

  beforeAll(async () => {
    const moduleFixture = await Test.createTestingModule({
      imports: [UsersModule, TypeOrmModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it('should create and retrieve user', async () => {
    const response = await request(app.getHttpServer())
      .post('/users')
      .send({ email: 'test@example.com', password: '123456' });

    expect(response.status).toBe(201);
    expect(response.body.email).toBe('test@example.com');
  });
});
```

### E2E Tests (test/e2e/\*.e2e-spec.ts)

**Para**: Flujos completos de usuario

**Cuándo**: Rutas críticas de negocio

---

## Checklist de Completitud de Módulo

Antes de considerar un módulo completo:

- [ ] ✅ DTO con validaciones completas
- [ ] ✅ Controller implementado y documentado
- [ ] ✅ Service con lógica de negocio
- [ ] ✅ Repository implementado
- [ ] ✅ Unit tests para service (coverage >= umbral)
- [ ] ✅ Unit tests para repository
- [ ] ✅ Integration tests para flujo completo
- [ ] ✅ Error handling apropiado
- [ ] ✅ Logging en lugares estratégicos
- [ ] ✅ API documentada (Swagger/OpenAPI)
- [ ] ✅ Specs en docs/01-requirements.md completadas
- [ ] ✅ Specs en docs/02-architecture.md completadas

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
