# UNIT 9: React – Topic 2: Building a Real SPA

This second and final topic focuses on **turning basic React knowledge into a real Single Page Application (SPA)**.

The objective is to extend basic React concepts by adding:

- Routing
- Data fetching
- Shared state
- Authentication logic
- Reusable logic using custom hooks

This topic reflects how React is commonly used in **real-world frontend projects**.

---

## 1. React Router v7 – Ways of Using the Router

React Router v7 can be used in **three different ways**, depending on the complexity of the application.  
We present them from **simplest to most advanced**.

In this subject, we will **work mainly with Declarative Mode**, but it is important to understand that other approaches exist.

---

### 1.1 Declarative Mode (used in this course)

Declarative Mode is the **simplest and most flexible** way to use React Router.  
Routes are defined directly in JSX using `<Routes>` and `<Route>` components.

This mode focuses on:

- Navigation
- Rendering components

Data fetching and logic are handled using:

- `useEffect`
- services
- context
- custom hooks

#### Why Declarative Mode?

- Easy to understand
- Minimal abstraction
- Perfect for learning React
- Ideal for small and medium SPAs

#### Basic Setup

```tsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<Users />} />
        <Route path="/users/:id" element={<UserDetail />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

### 1.2 Data Mode (overview)

Data Mode introduces a **more structured approach**.  
Routes are defined using objects instead of JSX.

Key ideas:

- Centralized routing configuration
- Route-based data loading (`loader`)
- Automatic loading and error handling

```tsx
const router = createBrowserRouter([
  {
    path: "users",
    loader: () => fetch("/api/users"),
    element: <Users />,
  },
]);
```

📌 This mode is common in professional projects but introduces more complexity.

---

### 1.3 Framework Mode (overview)

Framework Mode is the **most complete and opinionated** way to use React Router.

Features:

- File-based routing
- Built-in data loading (`loader`)
- Built-in mutations (`action`)
- Strong conventions

```tsx
export async function loader() {
  return fetch("/api/users");
}
```

📌 This mode behaves like a full framework and is **out of scope for this subject**.

---

### 1.4 Comparison of Approaches

| Mode           | Routing Style    | Data APIs | Complexity | Typical Use          |
| -------------- | ---------------- | --------- | ---------- | -------------------- |
| Declarative    | JSX (`<Routes>`) | ❌ No     | Low        | Learning, small SPAs |
| Data Mode      | Route objects    | ✅ Yes    | Medium     | Structured SPAs      |
| Framework Mode | File-based       | ✅ Yes    | High       | Large applications   |

---

## 2. Navigation and Routing Concepts

### Navigation Links

```tsx
<Link to="/users">Users</Link>
```

- Prevents full page reloads
- Keeps SPA behavior

### Programmatic Navigation

```tsx
const navigate = useNavigate();
navigate("/login");
```

### Route Parameters

```tsx
const { id } = useParams();
```

---

## 3. Fetching Data from an API

React applications usually fetch data using `fetch` inside `useEffect`.

```tsx
useEffect(() => {
  async function loadUsers() {
    const response = await fetch("http://localhost:8000/users");
    const data = await response.json();
    setUsers(data);
  }

  loadUsers();
}, []);
```

---

## 4. Separating API Logic (Services)

To keep components clean, API calls should be placed in **service files**.

```ts
export async function getUsers() {
  const response = await fetch("http://localhost:8000/users");
  if (!response.ok) {
    throw new Error("Request failed");
  }
  return response.json();
}
```

---

## 5. Shared State in React

When several components need the same data, state must be shared.

### Context API (Basic)

```tsx
const UserContext = createContext(null);
```

The context usually stores:

- authenticated user
- authentication state
- shared actions (login, logout)

---

## 6. Protected Routes

Some routes should only be accessible to authenticated users.

```tsx
function PrivateRoute({ children }) {
  return isAuthenticated ? children : <Navigate to="/login" />;
}
```

---

## 7. Controlled Forms

Forms in React are usually controlled using state.

```tsx
const [email, setEmail] = useState("");

<input value={email} onChange={(e) => setEmail(e.target.value)} />;
```

---

## 8. Custom Hooks in React

### What is a Custom Hook?

A **custom hook** is a normal JavaScript function that:

- starts with `use`
- can use other hooks
- allows us to **reuse logic**

Custom hooks help us:

- avoid duplicated logic
- keep components simple
- separate logic from UI

---

### Example: `useUser` Authentication Hook

This hook encapsulates **all authentication logic**:

- login
- logout
- register
- interaction with `UserContext`

```ts
import { useContext } from 'react';
import { UserContext } from '../context/UserContext';

export function useUser() {
  const { setUsuario, setIsAuthenticated, setError } =
    useContext(UserContext);

  const login = async (nick, pass) => {
    try {
      const response = await fetch(
        \`http://www.ies-azarquiel.es/paco/apigafas/usuario?nick=\${nick}&pass=\${pass}\`
      );

      if (!response.ok) {
        throw new Error('Error fetching user');
      }

      const data = await response.json();

      if (data.usuario === null) {
        setIsAuthenticated(false);
        setError('Invalid credentials');
      } else {
        setUsuario(data.usuario);
        setIsAuthenticated(true);
        setError(null);
      }
    } catch (err) {
      setError(err.message);
    }
  };

  const logout = () => {
    setUsuario(null);
    setIsAuthenticated(false);
    setError(null);
  };

  const register = async (nick, pass) => {
    try {
      const response = await fetch(
        'http://www.ies-azarquiel.es/paco/apigafas/usuario',
        {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ nick, pass }),
        }
      );

      if (!response.ok) {
        throw new Error('Registration failed');
      }

      await login(nick, pass);
    } catch (err) {
      setError(err.message);
    }
  };

  return { login, logout, register };
}
```

### Why This Hook is a Good Example

- Uses `useContext`
- Centralizes authentication logic
- Keeps components clean
- Realistic professional pattern

---

## 9. Basic Project Structure

```text
src/
 ├─ pages/
 ├─ components/
 ├─ services/
 ├─ context/
 ├─ hooks/
 └─ App.tsx
```

---

## 10. Mini Project: User Management SPA

Students should be able to build an SPA with:

- Routing
- API consumption
- Authentication
- Protected routes
- Detail pages using params

---

## Final Notes

- This topic focuses on **practical React**
- Patterns shown are common in real jobs
- Provides a solid base for frameworks like Next.js
