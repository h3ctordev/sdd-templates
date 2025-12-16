# 10 - Arquitectura de Componentes Frontend

> **Template Genérico para Arquitectura de Componentes** - Aplicable a React, Vue, Angular, Svelte

## Propósito

Este documento define patrones, mejores prácticas y principios para la arquitectura de componentes frontend siguiendo la metodología SDD.

---

## Principios de Diseño de Componentes

### 1. Single Responsibility Principle (SRP)

Cada componente debe tener UNA responsabilidad clara.

**❌ BAD - Componente con demasiadas responsabilidades**:

```typescript
export const UserDashboard = () => {
  // - Maneja authentication
  // - Carga datos de usuario
  // - Gestiona tareas
  // - Formatea fechas
  // - Maneja UI
  // DEMASIADO!
  return <div>...</div>;
};
```

**✅ GOOD - Responsabilidades separadas**:

```typescript
// Hook para auth
export const useAuth = () => { /* ... */ };

// Hook para datos
export const useUserTasks = (userId) => { /* ... */ };

// Utilidad para formateo
export const formatDate = (date) => { /* ... */ };

// Componente enfocado en presentación
export const UserDashboard = ({ user, tasks }) => {
  return <div>...</div>;
};
```

### 2. Composición sobre Herencia

**❌ BAD - Herencia de componentes**:

```typescript
class BaseButton extends React.Component {
  render() {
    /* ... */
  }
}

class PrimaryButton extends BaseButton {
  // override render
}
```

**✅ GOOD - Composición**:

```typescript
interface ButtonProps {
  variant: 'primary' | 'secondary';
  children: React.ReactNode;
}

export const Button: React.FC<ButtonProps> = ({ variant, children }) => (
  <button className={`btn btn-${variant}`}>{children}</button>
);
```

### 3. Props sobre Configuración Global

**❌ BAD - Configuración implícita**:

```typescript
export const Form = () => {
  const config = getGlobalConfig(); // ¿Dónde viene?
  return <form>{/* ... */}</form>;
};
```

**✅ GOOD - Props explícitos**:

```typescript
interface FormProps {
  onSubmit: (data: FormData) => void;
  fields: FormField[];
  submitButtonText?: string;
}

export const Form: React.FC<FormProps> = ({
  onSubmit,
  fields,
  submitButtonText = 'Submit',
}) => (
  <form onSubmit={onSubmit}>{/* ... */}</form>
);
```

### 4. Presentational vs Container Components

**Presentational Components** (Dumb):

- Solo reciben props
- NO tienen estado
- NO hacen llamadas a API
- Reutilizables y testables
- Ejemplo: Button, Card, Input

**Container Components** (Smart):

- Pueden tener estado
- Hacen llamadas a API
- Acceden a store/context
- Pasan props a componentes presentacionales
- Ejemplo: UserListContainer, DashboardPage

```typescript
// Presentational
export const UserCard: React.FC<UserCardProps> = ({ user, onEdit }) => (
  <div className="user-card">
    <h3>{user.name}</h3>
    <p>{user.email}</p>
    <button onClick={() => onEdit(user.id)}>Edit</button>
  </div>
);

// Container
export const UserListContainer: React.FC = () => {
  const { users, loading, error } = useUsers();

  if (loading) return <Spinner />;
  if (error) return <ErrorAlert message={error} />;

  return (
    <div>
      {users.map((user) => (
        <UserCard
          key={user.id}
          user={user}
          onEdit={handleEdit}
        />
      ))}
    </div>
  );
};
```

---

## Patrones de Componentes

### 1. Compound Components

Para componentes que trabajan juntos.

```typescript
// Menu.tsx - Componente compuesto
import React, { createContext, useState } from 'react';

interface MenuContextType {
  isOpen: boolean;
  toggle: () => void;
  close: () => void;
}

const MenuContext = createContext<MenuContextType | undefined>(undefined);

export const Menu: React.FC<{ children: React.ReactNode }> = ({
  children,
}) => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <MenuContext.Provider
      value={{
        isOpen,
        toggle: () => setIsOpen(!isOpen),
        close: () => setIsOpen(false),
      }}
    >
      {children}
    </MenuContext.Provider>
  );
};

export const MenuTrigger: React.FC<{ children: React.ReactNode }> = ({
  children,
}) => {
  const context = React.useContext(MenuContext);
  if (!context) throw new Error('MenuTrigger must be within Menu');

  return (
    <button onClick={context.toggle} aria-expanded={context.isOpen}>
      {children}
    </button>
  );
};

export const MenuContent: React.FC<{ children: React.ReactNode }> = ({
  children,
}) => {
  const context = React.useContext(MenuContext);
  if (!context) throw new Error('MenuContent must be within Menu');

  return context.isOpen ? <div role="menu">{children}</div> : null;
};

export const MenuItem: React.FC<{
  onClick: () => void;
  children: React.ReactNode;
}> = ({ onClick, children }) => {
  const context = React.useContext(MenuContext);

  return (
    <button
      role="menuitem"
      onClick={() => {
        onClick();
        context?.close();
      }}
    >
      {children}
    </button>
  );
};

// Uso:
<Menu>
  <MenuTrigger>Open Menu</MenuTrigger>
  <MenuContent>
    <MenuItem onClick={handleEdit}>Edit</MenuItem>
    <MenuItem onClick={handleDelete}>Delete</MenuItem>
  </MenuContent>
</Menu>
```

### 2. Render Props Pattern

Para compartir lógica entre componentes.

```typescript
interface RenderPropsProps<T> {
  data: T[];
  render: (items: T[], loading: boolean, error?: Error) => React.ReactNode;
}

export const DataFetcher: React.FC<RenderPropsProps<User>> = ({
  data,
  render,
}) => {
  const [loading, setLoading] = React.useState(false);
  const [error, setError] = React.useState<Error>();

  // Lógica compartida aquí

  return <>{render(data, loading, error)}</>;
};

// Uso:
<DataFetcher
  data={users}
  render={(users, loading, error) => (
    <>
      {loading && <Spinner />}
      {error && <ErrorAlert message={error.message} />}
      {users.map((user) => (
        <UserCard key={user.id} user={user} />
      ))}
    </>
  )}
/>
```

### 3. Higher-Order Components (HOC)

Para envolver componentes con funcionalidad adicional.

```typescript
interface WithAuthProps {
  isAuthenticated: boolean;
  user: User | null;
}

export function withAuth<P extends WithAuthProps>(
  Component: React.ComponentType<P>,
) {
  return (props: Omit<P, keyof WithAuthProps>) => {
    const { user, isAuthenticated } = useAuth();

    if (!isAuthenticated) {
      return <Redirect to="/login" />;
    }

    return (
      <Component
        {...(props as P)}
        isAuthenticated={isAuthenticated}
        user={user}
      />
    );
  };
}

// Uso:
export const ProtectedDashboard = withAuth(Dashboard);
```

### 4. Custom Hooks Pattern

Para compartir lógica stateful.

```typescript
// Hook personalizado
interface UsePaginationProps {
  initialPage?: number;
  itemsPerPage?: number;
}

export function usePagination<T>(
  items: T[],
  { initialPage = 1, itemsPerPage = 10 }: UsePaginationProps = {},
) {
  const [currentPage, setCurrentPage] = React.useState(initialPage);

  const paginatedItems = items.slice(
    (currentPage - 1) * itemsPerPage,
    currentPage * itemsPerPage,
  );

  const pageCount = Math.ceil(items.length / itemsPerPage);

  return {
    items: paginatedItems,
    currentPage,
    pageCount,
    goToPage: (page: number) => setCurrentPage(Math.max(1, Math.min(page, pageCount))),
    nextPage: () => setCurrentPage((p) => Math.min(p + 1, pageCount)),
    prevPage: () => setCurrentPage((p) => Math.max(p - 1, 1)),
  };
}

// Uso en componente:
export const UsersList = () => {
  const users = [/* ... */];
  const { items, currentPage, pageCount, goToPage } = usePagination(users);

  return (
    <>
      {items.map((user) => (
        <UserCard key={user.id} user={user} />
      ))}
      <Pagination
        current={currentPage}
        total={pageCount}
        onChange={goToPage}
      />
    </>
  );
};
```

### 5. Provider Pattern (Context API)

Para estado global.

```typescript
interface AppContextType {
  user: User | null;
  setUser: (user: User | null) => void;
  theme: 'light' | 'dark';
  toggleTheme: () => void;
}

const AppContext = React.createContext<AppContextType | undefined>(undefined);

export const AppProvider: React.FC<{ children: React.ReactNode }> = ({
  children,
}) => {
  const [user, setUser] = React.useState<User | null>(null);
  const [theme, setTheme] = React.useState<'light' | 'dark'>('light');

  const value: AppContextType = {
    user,
    setUser,
    theme,
    toggleTheme: () => setTheme(theme === 'light' ? 'dark' : 'light'),
  };

  return (
    <AppContext.Provider value={value}>{children}</AppContext.Provider>
  );
};

export function useAppContext() {
  const context = React.useContext(AppContext);
  if (!context) {
    throw new Error('useAppContext must be used within AppProvider');
  }
  return context;
}

// Uso:
export const App = () => (
  <AppProvider>
    <MainLayout />
  </AppProvider>
);
```

---

## Organización de Arquivos por Tipo

### Componente Pequeño (< 50 líneas)

```
Button/
├── Button.tsx                    # Componente
├── index.ts                      # Export
└── Button.module.css             # Estilos
```

### Componente Mediano (50-200 líneas)

```
UserCard/
├── UserCard.tsx                  # Componente
├── UserCard.module.css           # Estilos
├── UserCard.spec.tsx             # Tests
├── types.ts                      # Types específicos
└── index.ts                      # Export
```

### Componente Complejo (> 200 líneas)

```
UserForm/
├── UserForm.tsx                  # Componente principal
├── UserForm.module.css
├── UserForm.spec.tsx
├── useUserForm.ts                # Hook personalizado para lógica
├── validation.ts                 # Validación específica
├── types.ts
├── constants.ts                  # Constantes locales
└── index.ts
```

---

## TypeScript Types

### Props Interface Pattern

```typescript
// ✅ GOOD
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'small' | 'medium' | 'large';
  isLoading?: boolean;
  children: React.ReactNode;
}

export const Button: React.FC<ButtonProps> = ({
  variant = 'primary',
  size = 'medium',
  isLoading = false,
  children,
  ...buttonProps
}) => {
  return (
    <button
      className={`btn btn-${variant} btn-${size}`}
      disabled={isLoading}
      {...buttonProps}
    >
      {isLoading ? '...' : children}
    </button>
  );
};
```

### Component Types Compartidos

```typescript
// types/components.types.ts

// Estatus de datos
export type AsyncStatus = 'idle' | 'pending' | 'success' | 'error';

// Respuesta de API
export interface ApiResponse<T> {
  data: T;
  meta?: {
    timestamp: string;
    version: string;
  };
}

// Estado paginado
export interface PaginatedResponse<T> {
  data: T[];
  pagination: {
    page: number;
    limit: number;
    total: number;
    pages: number;
  };
}

// Props comunes
export interface BaseComponentProps {
  className?: string;
  testId?: string;
}

export interface FormProps extends BaseComponentProps {
  onSubmit: (data: unknown) => Promise<void> | void;
  isLoading?: boolean;
  error?: string | null;
}
```

---

## Accesibilidad (WCAG 2.1)

### Checklist de Accesibilidad

- [ ] ✅ Contraste de colores >= 4.5:1 (normal text)
- [ ] ✅ Labels asociados con inputs
- [ ] ✅ ARIA attributes donde sea necesario
- [ ] ✅ Navegación por teclado
- [ ] ✅ Focus visible
- [ ] ✅ Estructura semántica HTML
- [ ] ✅ Alt text en imágenes
- [ ] ✅ Tamaño mínimo de click: 44x44px

### Ejemplo: Formulario Accesible

```typescript
interface AccessibleFormProps {
  onSubmit: (data: FormData) => void;
}

export const AccessibleForm: React.FC<AccessibleFormProps> = ({
  onSubmit,
}) => {
  const [errors, setErrors] = React.useState<Record<string, string>>({});
  const inputRef = React.useRef<HTMLInputElement>(null);

  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    // Validar
    // Actualizar errors
    // Llamar onSubmit
  };

  return (
    <form onSubmit={handleSubmit}>
      {/* Label asociado con input */}
      <label htmlFor="email">
        Email *
        <span aria-label="required">*</span>
      </label>
      <input
        id="email"
        ref={inputRef}
        type="email"
        aria-required="true"
        aria-invalid={!!errors.email}
        aria-describedby="email-error"
        required
      />

      {/* Mensaje de error accesible */}
      {errors.email && (
        <div id="email-error" role="alert" className="error">
          {errors.email}
        </div>
      )}

      {/* Botón accesible */}
      <button
        type="submit"
        aria-label="Submit the form"
        className="button"
        style={{ minWidth: '44px', minHeight: '44px' }}
      >
        Submit
      </button>
    </form>
  );
};
```

---

## Performance Optimization

### 1. Memoization con React.memo

```typescript
interface UserItemProps {
  user: User;
  onSelect: (userId: string) => void;
}

export const UserItem = React.memo(
  ({ user, onSelect }: UserItemProps) => {
    console.log('Rendering UserItem:', user.id);
    return (
      <div onClick={() => onSelect(user.id)}>
        {user.name}
      </div>
    );
  },
  (prevProps, nextProps) => {
    // Custom comparison
    return prevProps.user.id === nextProps.user.id;
  },
);
```

### 2. useMemo para Cálculos Costosos

```typescript
export const ExpensiveComponent = ({ items }: { items: Item[] }) => {
  const sortedItems = React.useMemo(() => {
    console.log('Sorting items...');
    return items.sort((a, b) => a.value - b.value);
  }, [items]);

  return <div>{sortedItems.map((item) => item.name)}</div>;
};
```

### 3. useCallback para Funciones

```typescript
export const ListComponent = ({ onItemSelect }: Props) => {
  const handleSelect = React.useCallback(
    (id: string) => {
      onItemSelect(id);
    },
    [onItemSelect],
  );

  return (
    <ul>
      {items.map((item) => (
        <li key={item.id} onClick={() => handleSelect(item.id)}>
          {item.name}
        </li>
      ))}
    </ul>
  );
};
```

### 4. Code Splitting

```typescript
// routes.tsx
import React from 'react';

const HomePage = React.lazy(() => import('./pages/Home'));
const DashboardPage = React.lazy(() => import('./pages/Dashboard'));

export const routes = [
  { path: '/', element: <HomePage /> },
  { path: '/dashboard', element: <DashboardPage /> },
];
```

---

## Error Boundaries

```typescript
interface ErrorBoundaryProps {
  children: React.ReactNode;
  fallback?: React.ReactNode;
}

interface ErrorBoundaryState {
  hasError: boolean;
  error?: Error;
}

export class ErrorBoundary extends React.Component<
  ErrorBoundaryProps,
  ErrorBoundaryState
> {
  constructor(props: ErrorBoundaryProps) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error): ErrorBoundaryState {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    console.error('ErrorBoundary caught:', error, errorInfo);
    // Log a servicio de error tracking
  }

  render() {
    if (this.state.hasError) {
      return (
        this.props.fallback || (
          <div className="error-boundary">
            <h2>Algo salió mal</h2>
            <p>{this.state.error?.message}</p>
          </div>
        )
      );
    }

    return this.props.children;
  }
}
```

---

## Checklist de Componente

Antes de considerar un componente "listo para producción":

- [ ] ✅ Props bien tipados con TypeScript
- [ ] ✅ JSDoc con ejemplos de uso
- [ ] ✅ Tests unitarios (coverage >= 80%)
- [ ] ✅ Accesibilidad (WCAG 2.1)
- [ ] ✅ Estilos responsivos
- [ ] ✅ Error handling
- [ ] ✅ Loading states
- [ ] ✅ Performance optimizado (memoization si necesario)
- [ ] ✅ Documentación en Storybook
- [ ] ✅ TypeScript sin `any`
- [ ] ✅ Sin console.log en producción
- [ ] ✅ Propiedades sensibles no expuestas

---

**Versión del documento**: 1.0.0  
**Última actualización**: [FECHA]  
**Mantenedor**: [EQUIPO/PERSONA]
