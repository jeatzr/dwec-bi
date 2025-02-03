# **APPENDIX B Learning TypeScript for React**

This guide introduces you to the essential TypeScript concepts to effectively use it with React, with a brief explanation of **type aliases** and **interfaces**, and when to use each.

---

## 1. **What is TypeScript?**

TypeScript is a superset of JavaScript that adds **static typing**. It helps catch errors during development and makes your code more predictable and maintainable.

Key Features:

- Static typing
- Interfaces and types for defining data structures
- Improved tooling and code completion

---

## 2. **Setup TypeScript in a React Project**

1. Create a React project:

   ```bash
   npx create-react-app my-app --template typescript
   ```

2. Add TypeScript to an existing React project:
   ```bash
   npm install typescript @types/react @types/react-dom
   ```
   Then create a `tsconfig.json` file with \`npx tsc --init\`.

---

## 3. **Basic TypeScript Concepts**

### 3.1 Types

#### Primitives

```typescript
const count: number = 5;
const username: string = "John";
const isLoggedIn: boolean = true;
```

#### Arrays

```typescript
const numbers: number[] = [1, 2, 3];
const names: string[] = ["Alice", "Bob"];
```

#### Objects

```typescript
const user: { id: number; name: string } = {
  id: 1,
  name: "Alice",
};
```

#### Union Types

```typescript
let result: string | number;
result = "Success";
result = 42;
```

---

## 4. **Type Aliases vs Interfaces**

### What is a Type Alias?

A **type alias** is a way to define a custom type name for any TypeScript type. It can describe:

- Primitives
- Objects
- Unions
- Tuples
- Functions

```typescript
type User = {
  id: number;
  name: string;
};

type Status = "active" | "inactive";
type Coordinates = [number, number];
type Callback = (message: string) => void;
```

---

### What is an Interface?

An **interface** is specifically designed to describe the shape of an object. It can be **extended** or **merged**, making it ideal for defining reusable object structures.

```typescript
interface User {
  id: number;
  name: string;
}

interface Admin extends User {
  permissions: string[];
}
```

---

### When to Use Each?

| Use Case                                   | Type Alias                         | Interface                             |
| ------------------------------------------ | ---------------------------------- | ------------------------------------- |
| **Defining primitives, unions, or tuples** | ✅                                 | ❌                                    |
| **Describing object shapes**               | ✅                                 | ✅                                    |
| **Extending or merging types**             | Limited (use intersections: \`&\`) | ✅ \`extends\` or declaration merging |

---

## 5. **TypeScript with React**

### Functional Components with Simple Props

```typescript
import React from "react";

type Props = {
  title: string;
};

const Header: React.FC<Props> = ({ title }) => {
  return <h1>{title}</h1>;
};

export default Header;
```

---

### Props with Complex Data Shapes

#### Example: Array of Objects as Props

When a prop is an array of objects, you can use a type alias or an interface to define its structure.

```typescript
type Item = {
  id: number;
  name: string;
};

type ListProps = {
  items: Item[];
};

const ItemList: React.FC<ListProps> = ({ items }) => {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};

export default ItemList;
```

---

### State with Complex Data Shapes

#### Example: State with an Array of Objects

```typescript
import React, { useState } from "react";

type Task = {
  id: number;
  description: string;
  completed: boolean;
};

const TaskManager: React.FC = () => {
  const [tasks, setTasks] = useState<Task[]>([
    { id: 1, description: "Learn TypeScript", completed: false },
    { id: 2, description: "Build a React app", completed: true },
  ]);

  const toggleTask = (id: number) => {
    setTasks((prevTasks) =>
      prevTasks.map((task) =>
        task.id === id ? { ...task, completed: !task.completed } : task
      )
    );
  };

  return (
    <ul>
      {tasks.map((task) => (
        <li key={task.id}>
          <span
            style={{ textDecoration: task.completed ? "line-through" : "none" }}
          >
            {task.description}
          </span>
          <button onClick={() => toggleTask(task.id)}>
            {task.completed ? "Undo" : "Complete"}
          </button>
        </li>
      ))}
    </ul>
  );
};

export default TaskManager;
```

---

### Props with Nested Objects

#### Example: Nested Objects in Props

```typescript
type Address = {
  street: string;
  city: string;
  postalCode: string;
};

type User = {
  id: number;
  name: string;
  address: Address;
};

type UserCardProps = {
  user: User;
};

const UserCard: React.FC<UserCardProps> = ({ user }) => {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.address.street}</p>
      <p>
        {user.address.city}, {user.address.postalCode}
      </p>
    </div>
  );
};

export default UserCard;
```

---

## 6. **Summary**

- Use **type aliases** for defining **primitives**, **unions**, **tuples**, or **function types**.
- Use **interfaces** for defining **object shapes**, especially when you need **extensibility** or **declaration merging**.
- For props and states with **complex data shapes**, define reusable types/interfaces to maintain clarity and consistency.

By combining these concepts, you can handle React props and state effectively while leveraging TypeScript's power.
