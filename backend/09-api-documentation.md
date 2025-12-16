# 09 - Documentación de API

> **Template Genérico para Documentación API** - Aplicable a REST, GraphQL, gRPC

## Propósito

Este documento define los estándares para documentar APIs siguiendo principios SDD y las mejores prácticas de OpenAPI 3.0.

---

## Principios de Diseño de API

### 1. RESTful Conventions (para REST APIs)

**Recursos como nouns**:

```
✅ GET    /api/users                    (lista de usuarios)
✅ POST   /api/users                    (crear usuario)
✅ GET    /api/users/{id}               (obtener usuario)
✅ PUT    /api/users/{id}               (actualizar usuario)
✅ DELETE /api/users/{id}               (eliminar usuario)
✅ GET    /api/users/{id}/tasks         (tareas de usuario)

❌ GET    /api/getUsers                 (verb instead of resource)
❌ POST   /api/createUser               (verb in path)
```

### 2. Versionado de API

**Opción 1: URL Path** (Recomendado para mayor claridad)

```
GET /api/v1/users
GET /api/v2/users
```

**Opción 2: Header**

```
GET /api/users
Header: API-Version: 1
```

### 3. Validación de Entrada

**Todos los inputs deben ser validados**:

```typescript
// ✅ GOOD
@Post()
async create(@Body() createUserDto: CreateUserDto) {
  // DTO automáticamente valida:
  // - email es email válido
  // - password tiene mínimo 8 caracteres
  // - name no está vacío
  return this.usersService.create(createUserDto);
}

// ❌ BAD
@Post()
async create(@Body() body: any) {
  // Sin validación, acepta cualquier cosa
}
```

### 4. Códigos HTTP Apropiados

| Código  | Significado           | Cuándo Usar                         |
| ------- | --------------------- | ----------------------------------- |
| **200** | OK                    | Request exitoso, respuesta con body |
| **201** | Created               | Recurso creado exitosamente         |
| **204** | No Content            | Request exitoso, sin body (DELETE)  |
| **400** | Bad Request           | Datos inválidos en request          |
| **401** | Unauthorized          | Autenticación requerida             |
| **403** | Forbidden             | Autenticado pero sin permiso        |
| **404** | Not Found             | Recurso no existe                   |
| **409** | Conflict              | Violación de restricción única      |
| **422** | Unprocessable Entity  | Validación de negocio fallida       |
| **429** | Too Many Requests     | Rate limit excedido                 |
| **500** | Internal Server Error | Error del servidor                  |
| **503** | Service Unavailable   | Servidor en mantenimiento           |

---

## OpenAPI 3.0 / Swagger Configuration

### Configuración Base (NestJS + Swagger)

```typescript
// src/main.ts
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('[PROJECT] API')
    .setDescription('API documentation for [PROJECT]')
    .setVersion('1.0.0')
    .addTag('users', 'User management endpoints')
    .addTag('tasks', 'Task management endpoints')
    .addTag('auth', 'Authentication endpoints')
    .addServer('http://localhost:3000', 'Development')
    .addServer('https://api.example.com', 'Production')
    .addBearerAuth(
      { type: 'http', scheme: 'bearer', bearerFormat: 'JWT' },
      'bearer',
    )
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api/docs', app, document, {
    swaggerOptions: {
      persistAuthorization: true,
      operationsSorter: 'method',
    },
  });

  await app.listen(3000);
}
```

### Documentación de Endpoints

**Estructura completa**:

```typescript
import {
  Controller,
  Get,
  Post,
  Body,
  Param,
  Query,
  UseGuards,
} from '@nestjs/common';
import {
  ApiTags,
  ApiOperation,
  ApiResponse,
  ApiParam,
  ApiQuery,
  ApiBearerAuth,
} from '@nestjs/swagger';

@ApiTags('users') // Agrupa endpoints en la UI
@Controller('api/v1/users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  /**
   * Crear nuevo usuario
   */
  @Post()
  @ApiOperation({
    summary: 'Create new user',
    description: 'Creates a new user account with email and password',
    operationId: 'createUser',
  })
  @ApiResponse({
    status: 201,
    description: 'User created successfully',
    type: UserResponseDto,
  })
  @ApiResponse({
    status: 400,
    description: 'Invalid input data',
    schema: {
      example: {
        statusCode: 400,
        message: ['email must be an email'],
        error: 'Bad Request',
      },
    },
  })
  @ApiResponse({
    status: 409,
    description: 'Email already registered',
    schema: {
      example: {
        statusCode: 409,
        message: 'Email already registered',
        error: 'Conflict',
      },
    },
  })
  async create(@Body() createUserDto: CreateUserDto): Promise<UserResponseDto> {
    return this.usersService.create(createUserDto);
  }

  /**
   * Obtener usuario por ID
   */
  @Get(':id')
  @ApiOperation({
    summary: 'Get user by ID',
    description: 'Retrieves a user by their ID',
    operationId: 'getUserById',
  })
  @ApiParam({
    name: 'id',
    description: 'User ID',
    example: '507f1f77bcf86cd799439011',
  })
  @ApiResponse({
    status: 200,
    description: 'User found',
    type: UserResponseDto,
  })
  @ApiResponse({
    status: 404,
    description: 'User not found',
  })
  async findOne(@Param('id') id: string): Promise<UserResponseDto> {
    return this.usersService.findById(id);
  }

  /**
   * Listar usuarios con paginación y filtros
   */
  @Get()
  @ApiOperation({
    summary: 'List users',
    description: 'Retrieves a paginated list of users',
    operationId: 'listUsers',
  })
  @ApiQuery({
    name: 'page',
    description: 'Page number (1-indexed)',
    required: false,
    example: 1,
    type: Number,
  })
  @ApiQuery({
    name: 'limit',
    description: 'Items per page',
    required: false,
    example: 10,
    type: Number,
  })
  @ApiQuery({
    name: 'role',
    description: 'Filter by role',
    required: false,
    enum: ['admin', 'user', 'moderator'],
  })
  @ApiResponse({
    status: 200,
    description: 'List of users',
    schema: {
      example: {
        data: [
          {
            id: '507f1f77bcf86cd799439011',
            email: 'user@example.com',
            name: 'John Doe',
            role: 'user',
            createdAt: '2024-01-01T00:00:00Z',
          },
        ],
        pagination: {
          page: 1,
          limit: 10,
          total: 42,
          pages: 5,
        },
      },
    },
  })
  async findAll(
    @Query() queryDto: ListUsersQueryDto,
  ): Promise<PaginatedResponse<UserResponseDto>> {
    return this.usersService.findAll(queryDto);
  }

  /**
   * Actualizar usuario
   */
  @Put(':id')
  @ApiBearerAuth('bearer')
  @UseGuards(JwtAuthGuard)
  @ApiOperation({
    summary: 'Update user',
    description: 'Updates an existing user (authenticated required)',
    operationId: 'updateUser',
  })
  @ApiParam({ name: 'id', description: 'User ID' })
  @ApiResponse({
    status: 200,
    description: 'User updated successfully',
    type: UserResponseDto,
  })
  @ApiResponse({
    status: 401,
    description: 'Unauthorized - JWT token required',
  })
  @ApiResponse({
    status: 403,
    description: 'Forbidden - Cannot update other users',
  })
  @ApiResponse({
    status: 404,
    description: 'User not found',
  })
  async update(
    @Param('id') id: string,
    @Body() updateUserDto: UpdateUserDto,
  ): Promise<UserResponseDto> {
    return this.usersService.update(id, updateUserDto);
  }

  /**
   * Eliminar usuario
   */
  @Delete(':id')
  @ApiBearerAuth('bearer')
  @UseGuards(JwtAuthGuard)
  @ApiOperation({
    summary: 'Delete user',
    description: 'Soft deletes a user (authenticated required)',
    operationId: 'deleteUser',
  })
  @ApiParam({ name: 'id', description: 'User ID' })
  @ApiResponse({
    status: 204,
    description: 'User deleted successfully',
  })
  @ApiResponse({
    status: 401,
    description: 'Unauthorized',
  })
  @ApiResponse({
    status: 404,
    description: 'User not found',
  })
  async delete(@Param('id') id: string): Promise<void> {
    await this.usersService.delete(id);
  }
}
```

---

## DTOs con Documentación

### Ejemplo: CreateUserDto

```typescript
import {
  IsEmail,
  IsString,
  MinLength,
  MaxLength,
  IsOptional,
} from 'class-validator';
import { ApiProperty } from '@nestjs/swagger';

export class CreateUserDto {
  @ApiProperty({
    description: 'User email address',
    example: 'john.doe@example.com',
    format: 'email',
  })
  @IsEmail({}, { message: 'Email must be valid' })
  email: string;

  @ApiProperty({
    description: 'User password (at least 8 characters)',
    example: 'SecurePassword123!',
    minLength: 8,
    maxLength: 128,
  })
  @IsString()
  @MinLength(8, { message: 'Password must be at least 8 characters' })
  @MaxLength(128)
  password: string;

  @ApiProperty({
    description: 'User full name',
    example: 'John Doe',
    minLength: 2,
    maxLength: 255,
  })
  @IsString()
  @MinLength(2)
  @MaxLength(255)
  name: string;

  @ApiProperty({
    description: 'User timezone',
    example: 'America/New_York',
    required: false,
    default: 'UTC',
  })
  @IsOptional()
  @IsString()
  timezone?: string;
}
```

### Ejemplo: UserResponseDto

```typescript
export class UserResponseDto {
  @ApiProperty({
    description: 'User unique identifier',
    example: '507f1f77bcf86cd799439011',
  })
  id: string;

  @ApiProperty({
    description: 'User email address',
    example: 'john.doe@example.com',
  })
  email: string;

  @ApiProperty({
    description: 'User full name',
    example: 'John Doe',
  })
  name: string;

  @ApiProperty({
    description: 'User role',
    enum: ['admin', 'user', 'moderator'],
    example: 'user',
  })
  role: string;

  @ApiProperty({
    description: 'User creation timestamp',
    example: '2024-01-01T00:00:00Z',
  })
  createdAt: string;

  @ApiProperty({
    description: 'Last update timestamp',
    example: '2024-01-15T10:30:00Z',
  })
  updatedAt: string;

  // ❌ NEVER include sensitive data
  // password: string;        // ❌ NO
  // passwordHash: string;    // ❌ NO
  // refreshToken: string;    // ❌ NO
}
```

---

## Patrones de Respuesta

### Success Response

```json
{
  "data": {
    "id": "507f1f77bcf86cd799439011",
    "email": "user@example.com",
    "name": "John Doe"
  },
  "meta": {
    "timestamp": "2024-01-15T10:30:00Z",
    "version": "1.0.0"
  }
}
```

### Paginated Response

```json
{
  "data": [
    { "id": "1", "email": "user1@example.com" },
    { "id": "2", "email": "user2@example.com" }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 42,
    "pages": 5,
    "hasNext": true,
    "hasPrev": false
  },
  "meta": {
    "timestamp": "2024-01-15T10:30:00Z"
  }
}
```

### Error Response

```json
{
  "statusCode": 400,
  "message": ["email must be an email", "password is too short"],
  "error": "Bad Request",
  "timestamp": "2024-01-15T10:30:00Z",
  "path": "/api/v1/users"
}
```

---

## Error Handling

### Excepciones Mapeadas a Códigos HTTP

```typescript
// common/filters/http-exception.filter.ts
import { Catch, ArgumentsHost, HttpExceptionFilter } from '@nestjs/common';

@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();

    let status = 500;
    let message = 'Internal server error';
    let error = 'Internal Server Error';

    if (exception instanceof HttpException) {
      status = exception.getStatus();
      const exceptionResponse = exception.getResponse();

      if (typeof exceptionResponse === 'object') {
        message = exceptionResponse['message'] || message;
        error = exceptionResponse['error'] || error;
      } else {
        message = exceptionResponse as string;
      }
    }

    response.status(status).json({
      statusCode: status,
      message,
      error,
      timestamp: new Date().toISOString(),
      path: request.url,
    });
  }
}
```

---

## Rate Limiting

### Configuración

```typescript
// src/config/rate-limit.config.ts
export const RATE_LIMIT_CONFIG = {
  default: {
    windowMs: 15 * 60 * 1000, // 15 minutos
    max: 100, // máximo 100 requests
  },
  auth: {
    windowMs: 15 * 60 * 1000,
    max: 5, // 5 intentos de login
  },
  api: {
    windowMs: 60 * 1000, // 1 minuto
    max: 30, // 30 requests por minuto
  },
};
```

### Implementación

```typescript
// src/main.ts
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 100,
  message: 'Too many requests from this IP',
  standardHeaders: true,
  legacyHeaders: false,
});

app.use(limiter);

// Rate limit específico para login
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5,
  skipSuccessfulRequests: true,
});

app.use('/api/auth/login', loginLimiter);
```

---

## CORS Configuration

```typescript
// src/main.ts
app.enableCors({
  origin: process.env.CORS_ORIGIN?.split(',') || 'localhost',
  credentials: true,
  methods: 'GET,HEAD,PUT,PATCH,POST,DELETE',
  allowedHeaders: 'Content-Type,Authorization',
  maxAge: 3600,
});
```

---

## Seguridad en APIs

### 1. Autenticación

```typescript
// Usar JWT Bearer tokens
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

### 2. Validación de Input

```typescript
// ✅ GOOD: Usar DTOs con class-validator
@Post()
async create(@Body() createUserDto: CreateUserDto) {}

// ❌ BAD: Sin validación
@Post()
async create(@Body() body: any) {}
```

### 3. No Exponer Errores Internos

```typescript
// ❌ BAD
throw new InternalServerErrorException(
  'Database connection failed: ' + error.message,
);

// ✅ GOOD
this.logger.error('Database error:', error);
throw new InternalServerErrorException('Database operation failed');
```

### 4. Sanitización de Output

```typescript
// ❌ NO incluyas en respuesta
{
  password: 'hashed_password_here',
  refreshToken: 'secret_token',
  apiKey: 'secret_key',
}

// ✅ SIEMPRE usa DTOs
class UserResponseDto {
  id: string;
  email: string;
  name: string;
  // Solo datos públicos
}
```

---

## Documentación de Cambios de API

### Changelog Template

````markdown
## API Changelog

### v2.0.0 - 2024-01-15

**Breaking Changes:**

- Deprecated: `GET /api/users/search` → Use `GET /api/users?query=...`
- Changed: Response structure now includes `meta` object

**New Features:**

- Added: `POST /api/users/{id}/avatar` - Upload user avatar
- Added: Query parameters: `page`, `limit`, `sort` to `GET /api/users`

**Improvements:**

- Performance: Reduced response time by 40%
- Security: Added rate limiting to all endpoints

**Bug Fixes:**

- Fixed: Pagination offset calculation

### Migration Guide

```typescript
// Old
const users = await fetch('/api/users/search?q=john');

// New
const users = await fetch('/api/users?query=john&page=1&limit=10');
```
````

```

---

## Checklist API Documentation

Antes de considerar una API documentada:

- [ ] ✅ Todos los endpoints tienen `@ApiOperation()`
- [ ] ✅ Todos los parámetros tienen `@ApiParam()` o `@ApiQuery()`
- [ ] ✅ Todas las respuestas tienen `@ApiResponse()`
- [ ] ✅ Todos los DTOs tienen `@ApiProperty()`
- [ ] ✅ Swagger UI muestra todos los endpoints correctamente
- [ ] ✅ Ejemplos de requests/responses en documentation
- [ ] ✅ Rate limiting documentado
- [ ] ✅ Error codes documentados
- [ ] ✅ Authentication requerida documentada
- [ ] ✅ CORS configurado apropiadamente
- [ ] ✅ Changelog actualizado

---

**Versión del documento**: 1.0.0
**Última actualización**: [FECHA]
**Mantenedor**: [EQUIPO/PERSONA]
```
