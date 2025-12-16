# 07 - Estructura del Proyecto Frontend

> **Template Genérico para Frontend** - Aplicable a React, Vue, Angular, Next.js, Svelte, etc.

## Propósito de este Documento

Este documento define la estructura estándar esperada para proyectos frontend siguiendo la metodología SDD. La estructura es flexible y adaptable a cualquier framework UI moderno.

---

## Estructura Base Recomendada

```
proyecto-frontend/
│
├── .github/                                # Configuración GitHub
│   └── workflows/                          # CI/CD pipelines
│       ├── ci.yml
│       ├── test.yml
│       ├── build.yml
│       └── deploy.yml
│
├── docs/                                   # Documentación SDD (IMPORTANTE)
│   ├── 00-metodologia-trabajo.md
│   ├── 01-requirements.md
│   ├── 02-architecture.md
│   ├── 07-project-structure-frontend.md    # Este documento
│   ├── 08-configuration.md
│   ├── 10-component-architecture.md
│   ├── 11-component-patterns.md
│   ├── guides/
│   │   ├── quick-start-guide.md
│   │   ├── styling-guide.md
│   │   ├── state-management.md
│   │   └── testing-guide.md
│   └── tracking/                           # Tracking de progreso
│       ├── 00-progress-overview.md
│       ├── 03-issues-log.md
│       └── 04-decisions-log.md
│
├── public/                                 # Archivos estáticos
│   ├── favicon.ico
│   ├── favicon.svg
│   ├── robots.txt
│   ├── manifest.json                       # PWA
│   └── assets/
│       └── images/
│           ├── logo.svg
│           ├── hero.jpg
│           └── .gitkeep
│
├── src/                                    # Código fuente
│   │
│   ├── main.tsx                            # Entry point (o index.tsx)
│   ├── App.tsx                             # Componente raíz
│   ├── main.css                            # Estilos globales
│   │
│   ├── components/                         # Componentes reutilizables
│   │   ├── common/                         # Componentes genéricos
│   │   │   ├── Header/
│   │   │   │   ├── Header.tsx
│   │   │   │   ├── Header.module.css       # (o .scss)
│   │   │   │   ├── Header.spec.tsx         # Tests
│   │   │   │   └── index.ts                # Barrel export
│   │   │   │
│   │   │   ├── Footer/
│   │   │   ├── Navigation/
│   │   │   ├── Button/
│   │   │   ├── Input/
│   │   │   ├── Modal/
│   │   │   ├── Card/
│   │   │   ├── Alert/
│   │   │   ├── Spinner/
│   │   │   ├── Badge/
│   │   │   └── index.ts                    # Barrel export
│   │   │
│   │   ├── layout/                         # Componentes de layout
│   │   │   ├── MainLayout/
│   │   │   │   ├── MainLayout.tsx
│   │   │   │   ├── MainLayout.module.css
│   │   │   │   ├── MainLayout.spec.tsx
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── AdminLayout/
│   │   │   ├── AuthLayout/
│   │   │   └── index.ts
│   │   │
│   │   ├── forms/                          # Componentes de formularios
│   │   │   ├── LoginForm/
│   │   │   ├── RegisterForm/
│   │   │   ├── ProfileForm/
│   │   │   └── index.ts
│   │   │
│   │   └── index.ts                        # Barrel export de todos
│   │
│   ├── features/                           # Módulos de características
│   │   │
│   │   ├── auth/                           # Ejemplo: Autenticación
│   │   │   ├── components/
│   │   │   │   ├── LoginPage.tsx
│   │   │   │   ├── RegisterPage.tsx
│   │   │   │   ├── ForgotPasswordPage.tsx
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── hooks/                      # Custom hooks
│   │   │   │   ├── useAuth.ts
│   │   │   │   ├── useLogin.ts
│   │   │   │   ├── useRegister.ts
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── services/                   # API calls
│   │   │   │   ├── authService.ts
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── store/                      # State management (Redux, Zustand, Pinia)
│   │   │   │   ├── authSlice.ts            # (Redux)
│   │   │   │   ├── authStore.ts            # (Zustand)
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   ├── types/                      # TypeScript types
│   │   │   │   ├── auth.types.ts
│   │   │   │   └── index.ts
│   │   │   │
│   │   │   └── index.ts
│   │   │
│   │   ├── dashboard/                      # Módulo Dashboard (similar estructura)
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   ├── services/
│   │   │   ├── store/
│   │   │   ├── types/
│   │   │   └── index.ts
│   │   │
│   │   ├── users/                          # Módulo Usuarios
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   ├── services/
│   │   │   ├── store/
│   │   │   ├── types/
│   │   │   └── index.ts
│   │   │
│   │   └── [otras-features]/
│   │       ├── components/
│   │       ├── hooks/
│   │       ├── services/
│   │       ├── store/
│   │       ├── types/
│   │       └── index.ts
│   │
│   ├── pages/                              # Páginas/Rutas (si no usa routing en features)
│   │   ├── Home.tsx
│   │   ├── About.tsx
│   │   ├── Dashboard.tsx
│   │   ├── NotFound.tsx
│   │   └── index.ts
│   │
│   ├── store/                              # Estado global (si aplica)
│   │   ├── slices/                         # Redux
│   │   │   ├── userSlice.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── store.ts                        # Configuración del store
│   │   └── index.ts
│   │
│   ├── hooks/                              # Custom hooks compartidos
│   │   ├── useTheme.ts
│   │   ├── useLocalStorage.ts
│   │   ├── useAsync.ts
│   │   ├── useDebounce.ts
│   │   ├── usePagination.ts
│   │   ├── useForm.ts
│   │   └── index.ts
│   │
│   ├── services/                           # API services compartidos
│   │   ├── api.ts                          # Configuración de HTTP client
│   │   ├── apiClient.ts                    # Instancia del cliente
│   │   ├── baseService.ts                  # Clase base
│   │   ├── errorHandler.ts                 # Manejo de errores
│   │   └── index.ts
│   │
│   ├── types/                              # TypeScript types compartidos
│   │   ├── index.ts                        # Tipos generales
│   │   ├── api.types.ts                    # Tipos de API
│   │   ├── user.types.ts
│   │   ├── common.types.ts
│   │   └── api-responses.types.ts           # Respuestas genéricas
│   │
│   ├── utils/                              # Utilidades compartidas
│   │   ├── formatters.ts                   # Formateo de datos
│   │   ├── validators.ts                   # Validación de cliente
│   │   ├── storage.ts                      # LocalStorage helpers
│   │   ├── date.utils.ts
│   │   ├── string.utils.ts
│   │   ├── array.utils.ts
│   │   ├── object.utils.ts
│   │   └── index.ts
│   │
│   ├── styles/                             # Estilos compartidos
│   │   ├── variables.css                   # CSS variables
│   │   ├── variables.scss                  # (o SCSS variables)
│   │   ├── mixins.scss
│   │   ├── globals.css
│   │   ├── animations.css
│   │   ├── themes/
│   │   │   ├── light.css
│   │   │   ├── dark.css
│   │   │   └── index.css
│   │   └── index.css
│   │
│   ├── constants/                          # Constantes
│   │   ├── api.constants.ts                # URLs, endpoints
│   │   ├── messages.constants.ts           # Mensajes (en español)
│   │   ├── routes.constants.ts             # Rutas
│   │   ├── config.constants.ts
│   │   └── index.ts
│   │
│   ├── config/                             # Configuración
│   │   ├── app.config.ts
│   │   ├── api.config.ts
│   │   ├── routes.config.ts
│   │   └── index.ts
│   │
│   ├── middleware/                         # Middleware/Interceptors
│   │   ├── errorBoundary.tsx
│   │   ├── authMiddleware.ts
│   │   ├── api-interceptors.ts
│   │   └── index.ts
│   │
│   ├── i18n/                               # Internacionalización (si aplica)
│   │   ├── locales/
│   │   │   ├── es.json
│   │   │   ├── en.json
│   │   │   └── index.ts
│   │   │
│   │   └── i18n.config.ts
│   │
│   └── vite-env.d.ts                       # (si usa Vite)
│
├── test/                                   # Tests
│   ├── unit/                               # Unit tests
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── utils/
│   │   └── setup.ts
│   │
│   ├── integration/                        # Integration tests
│   │   ├── auth.integration.spec.tsx
│   │   ├── dashboard.integration.spec.tsx
│   │   └── setup.ts
│   │
│   ├── e2e/                                # E2E tests (Cypress, Playwright)
│   │   ├── auth.cy.ts
│   │   ├── dashboard.cy.ts
│   │   ├── fixtures/
│   │   └── support/
│   │
│   └── mocks/                              # MSW mocks
│       ├── handlers.ts
│       ├── server.ts
│       └── fixtures.ts
│
├── .env.example                            # Template de variables
├── .env                                    # (Gitignored) Desarrollo
├── .env.test                               # (Gitignored) Testing
├── .env.production                         # (Gitignored) Production
├── .gitignore
├── .prettierrc                             # Code formatter
├── .eslintrc.json                          # Linter
├── tsconfig.json                           # TypeScript config
├── vite.config.ts                          # Vite config (o webpack.config.js)
├── vitest.config.ts                        # Vitest config (o jest.config.js)
├── cypress.config.ts                       # Cypress config (si usa)
├── package.json
├── pnpm-lock.yaml                          # Lock file
├── README.md
├── LICENSE
└── .gitattributes
```

---

## Convenciones de Nombres

### Archivos de Componentes

```
├── Button/
│   ├── Button.tsx                          # Componente
│   ├── Button.module.css                   # Estilos
│   ├── Button.spec.tsx                     # Tests
│   ├── Button.stories.tsx                  # Storybook (si aplica)
│   ├── index.ts                            # Barrel export
│   └── types.ts                            # Types específicos
```

### Convención de Nombres

| Tipo             | Convención                          | Ejemplo                                 |
| ---------------- | ----------------------------------- | --------------------------------------- |
| **Componentes**  | PascalCase                          | `UserCard.tsx`, `LoginForm.tsx`         |
| **Custom Hooks** | camelCase + "use" prefix            | `useAuth.ts`, `usePagination.ts`        |
| **Services**     | camelCase                           | `authService.ts`, `userService.ts`      |
| **Utils**        | camelCase                           | `formatters.ts`, `validators.ts`        |
| **Types**        | PascalCase                          | `User.types.ts`, `ApiResponse.types.ts` |
| **Constants**    | UPPER_SNAKE_CASE                    | `API_BASE_URL`, `MAX_RETRIES`           |
| **Dirs**         | kebab-case                          | `common-components`, `feature-auth`     |
| **Tests**        | `[filename].spec.tsx` o `.test.tsx` | `Button.spec.tsx`                       |

---

## Estructura de Componentes

### Componente Simple

````typescript
// Button.tsx
import React from 'react';
import styles from './Button.module.css';
import type { ButtonProps } from './types';

/**
 * Componente Button reutilizable
 *
 * @example
 * ```tsx
 * <Button onClick={handleClick} variant="primary">
 *   Click me
 * </Button>
 * ```
 */
export const Button: React.FC<ButtonProps> = ({
  children,
  variant = 'primary',
  disabled = false,
  onClick,
  ...props
}) => {
  return (
    <button
      className={`${styles.button} ${styles[variant]}`}
      disabled={disabled}
      onClick={onClick}
      {...props}
    >
      {children}
    </button>
  );
};

export default Button;
````

### Componente con State (React Hooks)

```typescript
// UserProfile.tsx
import React, { useState, useEffect } from 'react';
import { useAuth } from '../hooks';
import { userService } from '../services';
import styles from './UserProfile.module.css';

export const UserProfile: React.FC = () => {
  const { user } = useAuth();
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState<string | null>(null);
  const [profile, setProfile] = useState(null);

  useEffect(() => {
    if (!user?.id) return;

    const loadProfile = async () => {
      setLoading(true);
      setError(null);
      try {
        const data = await userService.getProfile(user.id);
        setProfile(data);
      } catch (err) {
        setError('Failed to load profile');
        console.error(err);
      } finally {
        setLoading(false);
      }
    };

    loadProfile();
  }, [user?.id]);

  if (loading) return <div className={styles.loading}>Loading...</div>;
  if (error) return <div className={styles.error}>{error}</div>;
  if (!profile) return null;

  return <div className={styles.profile}>{/* ... */}</div>;
};
```

### Componente con Custom Hook

```typescript
// TaskList.tsx
import React from 'react';
import { useFetch } from '../hooks';
import { taskService } from '../services';

export const TaskList: React.FC = () => {
  const { data: tasks, loading, error } = useFetch(
    () => taskService.getTasks(),
    [],
  );

  if (loading) return <p>Loading tasks...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {tasks.map((task) => (
        <li key={task.id}>{task.title}</li>
      ))}
    </ul>
  );
};
```

---

## Custom Hooks

### Estructura de Hook

```typescript
// hooks/useAsync.ts
import { useEffect, useState, useCallback } from 'react';

interface AsyncState<T> {
  status: 'idle' | 'pending' | 'success' | 'error';
  data: T | null;
  error: Error | null;
}

export function useAsync<T>(asyncFunction: () => Promise<T>, immediate = true) {
  const [state, setState] = useState<AsyncState<T>>({
    status: 'idle',
    data: null,
    error: null,
  });

  const execute = useCallback(async () => {
    setState({ status: 'pending', data: null, error: null });
    try {
      const response = await asyncFunction();
      setState({ status: 'success', data: response, error: null });
      return response;
    } catch (error) {
      setState({
        status: 'error',
        data: null,
        error: error as Error,
      });
      throw error;
    }
  }, [asyncFunction]);

  useEffect(() => {
    if (immediate) {
      execute();
    }
  }, [execute, immediate]);

  return { ...state, execute };
}
```

### Ejemplo: useAuth Hook

```typescript
// hooks/useAuth.ts
import { useContext } from 'react';
import { AuthContext } from '../context/AuthContext';

export function useAuth() {
  const context = useContext(AuthContext);

  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }

  return context;
}
```

---

## Services / API Integration

### Estructura Base

```typescript
// services/api.ts
import axios, { AxiosInstance, AxiosError } from 'axios';
import { config } from '../config';

const apiClient: AxiosInstance = axios.create({
  baseURL: config.API_BASE_URL,
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Interceptor para agregar token
apiClient.interceptors.request.use((config) => {
  const token = localStorage.getItem('authToken');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Interceptor para manejo de errores
apiClient.interceptors.response.use(
  (response) => response,
  (error: AxiosError) => {
    if (error.response?.status === 401) {
      // Token expirado o inválido
      localStorage.removeItem('authToken');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  },
);

export default apiClient;
```

### Service Específico

```typescript
// services/userService.ts
import apiClient from './api';
import type { User, CreateUserDto, UpdateUserDto } from '../types';

class UserService {
  async getUser(id: string): Promise<User> {
    const response = await apiClient.get(`/users/${id}`);
    return response.data.data; // Asume estructura {data: {...}}
  }

  async listUsers(page = 1, limit = 10): Promise<{ data: User[] }> {
    const response = await apiClient.get('/users', {
      params: { page, limit },
    });
    return response.data;
  }

  async createUser(dto: CreateUserDto): Promise<User> {
    const response = await apiClient.post('/users', dto);
    return response.data.data;
  }

  async updateUser(id: string, dto: UpdateUserDto): Promise<User> {
    const response = await apiClient.put(`/users/${id}`, dto);
    return response.data.data;
  }

  async deleteUser(id: string): Promise<void> {
    await apiClient.delete(`/users/${id}`);
  }
}

export const userService = new UserService();
```

---

## State Management

### Redux (con Redux Toolkit)

```typescript
// store/slices/userSlice.ts
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import { userService } from '../../services';
import type { User } from '../../types';

interface UserState {
  current: User | null;
  loading: boolean;
  error: string | null;
}

const initialState: UserState = {
  current: null,
  loading: false,
  error: null,
};

export const fetchUser = createAsyncThunk(
  'user/fetchUser',
  async (id: string, { rejectWithValue }) => {
    try {
      return await userService.getUser(id);
    } catch (error) {
      return rejectWithValue('Failed to fetch user');
    }
  },
);

export const userSlice = createSlice({
  name: 'user',
  initialState,
  reducers: {
    clearUser: (state) => {
      state.current = null;
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchUser.pending, (state) => {
        state.loading = true;
        state.error = null;
      })
      .addCase(fetchUser.fulfilled, (state, action) => {
        state.loading = false;
        state.current = action.payload;
      })
      .addCase(fetchUser.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload as string;
      });
  },
});

export const { clearUser } = userSlice.actions;
export default userSlice.reducer;
```

### Zustand (Alternativa)

```typescript
// store/userStore.ts
import { create } from 'zustand';
import { userService } from '../services';
import type { User } from '../types';

interface UserStore {
  user: User | null;
  loading: boolean;
  error: string | null;
  fetchUser: (id: string) => Promise<void>;
  clearUser: () => void;
}

export const useUserStore = create<UserStore>((set) => ({
  user: null,
  loading: false,
  error: null,

  fetchUser: async (id: string) => {
    set({ loading: true, error: null });
    try {
      const user = await userService.getUser(id);
      set({ user, loading: false });
    } catch (error) {
      set({ error: 'Failed to fetch user', loading: false });
    }
  },

  clearUser: () => set({ user: null }),
}));
```

---

## Testing

### Unit Test de Componente

```typescript
// components/Button.spec.tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { Button } from './Button';

describe('Button Component', () => {
  it('should render button with text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByRole('button', { name: /click me/i })).toBeInTheDocument();
  });

  it('should call onClick handler when clicked', async () => {
    const handleClick = jest.fn();
    render(<Button onClick={handleClick}>Click</Button>);

    await userEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('should be disabled when disabled prop is true', () => {
    render(<Button disabled>Disabled</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });

  it('should apply correct variant class', () => {
    const { container } = render(<Button variant="secondary">Button</Button>);
    expect(container.querySelector('.secondary')).toBeInTheDocument();
  });
});
```

### Unit Test de Hook

```typescript
// hooks/useAsync.spec.ts
import { renderHook, waitFor } from '@testing-library/react';
import { useAsync } from './useAsync';

describe('useAsync', () => {
  it('should start in idle state', () => {
    const asyncFn = jest.fn();
    const { result } = renderHook(() => useAsync(asyncFn, false));

    expect(result.current.status).toBe('idle');
    expect(result.current.data).toBeNull();
  });

  it('should transition to success state', async () => {
    const asyncFn = jest.fn().mockResolvedValue({ id: 1, name: 'Test' });
    const { result } = renderHook(() => useAsync(asyncFn));

    await waitFor(() => {
      expect(result.current.status).toBe('success');
    });

    expect(result.current.data).toEqual({ id: 1, name: 'Test' });
  });

  it('should handle errors', async () => {
    const error = new Error('Test error');
    const asyncFn = jest.fn().mockRejectedValue(error);
    const { result } = renderHook(() => useAsync(asyncFn));

    await waitFor(() => {
      expect(result.current.status).toBe('error');
    });

    expect(result.current.error).toBe(error);
  });
});
```

### Integration Test

```typescript
// test/integration/auth.integration.spec.tsx
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { LoginPage } from '../features/auth/components/LoginPage';
import { server } from '../test/mocks/server';
import { rest } from 'msw';

describe('Auth Integration', () => {
  it('should login successfully', async () => {
    server.use(
      rest.post('*/api/auth/login', (req, res, ctx) => {
        return res(ctx.json({ data: { token: 'test-token' } }));
      }),
    );

    render(<LoginPage />);

    await userEvent.type(
      screen.getByLabelText(/email/i),
      'test@example.com',
    );
    await userEvent.type(
      screen.getByLabelText(/password/i),
      'password123',
    );
    await userEvent.click(screen.getByRole('button', { name: /login/i }));

    await waitFor(() => {
      expect(screen.queryByText(/loading/i)).not.toBeInTheDocument();
    });
  });
});
```

---

## Estilos CSS

### CSS Modules Pattern

```css
/* Button.module.css */
.button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.primary {
  background-color: var(--color-primary);
  color: white;
}

.primary:hover {
  background-color: var(--color-primary-dark);
}

.secondary {
  background-color: var(--color-secondary);
  color: var(--color-text);
}

.disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Variables CSS Globales

```css
/* styles/variables.css */
:root {
  /* Colors */
  --color-primary: #007bff;
  --color-primary-dark: #0056b3;
  --color-secondary: #6c757d;
  --color-success: #28a745;
  --color-danger: #dc3545;
  --color-warning: #ffc107;
  --color-info: #17a2b8;

  --color-text: #212529;
  --color-text-muted: #6c757d;
  --color-background: #ffffff;
  --color-border: #dee2e6;

  /* Spacing */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;
  --spacing-2xl: 3rem;

  /* Typography */
  --font-size-base: 1rem;
  --font-size-sm: 0.875rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;

  --line-height-tight: 1.2;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.75;

  /* Shadows */
  --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);

  /* Border Radius */
  --radius-sm: 0.25rem;
  --radius-md: 0.375rem;
  --radius-lg: 0.5rem;
}
```

---

## Checklist de Completitud de Módulo Frontend

Antes de considerar una feature completa:

- [ ] ✅ Componentes implementados
- [ ] ✅ Custom hooks creados
- [ ] ✅ API service integrado
- [ ] ✅ State management configurado
- [ ] ✅ Unit tests para componentes (coverage >= 70%)
- [ ] ✅ Unit tests para hooks
- [ ] ✅ Integration tests para flujo
- [ ] ✅ E2E tests para rutas críticas
- [ ] ✅ Estilos completados
- [ ] ✅ TypeScript types definidos
- [ ] ✅ Error handling implementado
- [ ] ✅ Loading states
- [ ] ✅ Accesibilidad (WCAG 2.1)
- [ ] ✅ Specs en docs completadas

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
