# ⚛️ React App Building — Complete Module-Wise Documentation

> A structured, progressive guide from zero to production-ready React developer.

---

## 📋 Table of Contents

1. [Module 1 — Prerequisites](#module-1)
2. [Module 2 — React Fundamentals](#module-2)
3. [Module 3 — React Hooks (Core)](#module-3)
4. [Module 4 — Component Patterns](#module-4)
5. [Module 5 — Routing with React Router](#module-5)
6. [Module 6 — Data Fetching & APIs](#module-6)
7. [Module 7 — Advanced Hooks](#module-7)
8. [Module 8 — State Management](#module-8)
9. [Module 9 — Styling Approaches](#module-9)
10. [Module 10 — Forms & Validation](#module-10)
11. [Module 11 — Performance Optimization](#module-11)
12. [Module 12 — Testing React Apps](#module-12)
13. [Module 13 — TypeScript with React](#module-13)
14. [Module 14 — Next.js (Full-Stack React)](#module-14)
15. [Module 15 — Deployment & DevOps](#module-15)
16. [Projects & Practice](#projects)

---

<a name="module-1"></a>
## 📦 Module 1 — Prerequisites

### 1.1 HTML & CSS Essentials
```html
<!-- Semantic HTML -->
<header>, <nav>, <main>, <section>, <article>, <footer>

<!-- Flexbox -->
<div style="display: flex; justify-content: space-between; align-items: center;">

<!-- CSS Grid -->
<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem;">
```

### 1.2 JavaScript (ES6+) Must-Know Concepts

**Destructuring**
```js
const { name, age } = user;
const [first, ...rest] = array;
```

**Spread & Rest**
```js
const newArr = [...arr1, ...arr2];
const merged = { ...obj1, ...obj2 };
function sum(...nums) { return nums.reduce((a, b) => a + b, 0); }
```

**Arrow Functions**
```js
const double = (n) => n * 2;
const greet = name => `Hello, ${name}!`;
```

**Array Methods**
```js
const doubled = [1, 2, 3].map(n => n * 2);          // [2, 4, 6]
const evens   = [1, 2, 3, 4].filter(n => n % 2 === 0); // [2, 4]
const sum     = [1, 2, 3].reduce((acc, n) => acc + n, 0); // 6
const found   = users.find(u => u.id === 5);
const exists  = users.some(u => u.active);
```

**Promises & Async/Await**
```js
// Promise
fetch('/api/data')
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));

// Async/Await
async function getData() {
  try {
    const res = await fetch('/api/data');
    const data = await res.json();
    return data;
  } catch (err) {
    console.error(err);
  }
}
```

**Modules (import/export)**
```js
// Named exports
export const PI = 3.14;
export function add(a, b) { return a + b; }

// Default export
export default function App() { return <div>App</div>; }

// Imports
import App from './App';
import { PI, add } from './utils';
```

**Ternary & Short-Circuit**
```js
const label = isLoggedIn ? "Logout" : "Login";
const display = user && <UserCard user={user} />;
const name = user?.profile?.name ?? "Anonymous"; // optional chaining + nullish coalescing
```

### 1.3 Setup Your Dev Environment
```bash
# Install Node.js (LTS) from nodejs.org

# Verify
node -v   # v20.x or higher
npm -v    # 10.x or higher

# Create a React app with Vite (recommended)
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```

---

<a name="module-2"></a>
## 📦 Module 2 — React Fundamentals

### 2.1 What is React?
React is a JavaScript library for building user interfaces using a component-based architecture. It uses a **Virtual DOM** to efficiently update the real DOM.

### 2.2 JSX — JavaScript XML
```jsx
// JSX is NOT HTML — it's syntactic sugar for React.createElement()
const element = <h1 className="title">Hello, {name}!</h1>;

// Rules:
// 1. Use className instead of class
// 2. Self-close empty tags: <img />, <br />
// 3. Return a single root element (or Fragment)
// 4. JavaScript expressions go in curly braces {}

// Fragments — avoid extra DOM nodes
return (
  <>
    <h1>Title</h1>
    <p>Paragraph</p>
  </>
);
```

### 2.3 Functional Components
```jsx
// Basic component
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Arrow function component
const Button = ({ label, onClick }) => (
  <button onClick={onClick}>{label}</button>
);

// Usage
<Greeting name="Alice" />
<Button label="Click Me" onClick={() => alert('Clicked!')} />
```

### 2.4 Props — Passing Data
```jsx
// Parent
function App() {
  return <UserCard name="Alice" age={25} isAdmin={true} />;
}

// Child
function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      {isAdmin && <span>Admin</span>}
    </div>
  );
}

// Props with default values
function Button({ label = "Submit", variant = "primary" }) {
  return <button className={variant}>{label}</button>;
}

// Spreading props
function Input(props) {
  return <input {...props} />;
}

// children prop
function Card({ children, title }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      <div>{children}</div>
    </div>
  );
}
// Usage: <Card title="My Card"><p>Content here</p></Card>
```

### 2.5 State with useState
```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // [state, setter]

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(prev => prev - 1)}>Decrement</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}

// Object state — always spread to preserve other fields
const [user, setUser] = useState({ name: '', email: '' });
setUser(prev => ({ ...prev, name: 'Alice' })); // ✅

// Array state
const [items, setItems] = useState([]);
setItems(prev => [...prev, newItem]);             // Add
setItems(prev => prev.filter(i => i.id !== id)); // Remove
setItems(prev => prev.map(i => i.id === id ? {...i, done: true} : i)); // Update
```

### 2.6 Event Handling
```jsx
function Form() {
  const handleClick = (e) => {
    e.preventDefault();
    console.log('Clicked!');
  };

  const handleChange = (e) => {
    console.log(e.target.value);
  };

  return (
    <form onSubmit={handleClick}>
      <input onChange={handleChange} type="text" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 2.7 Conditional Rendering
```jsx
function Status({ isLoggedIn, role }) {
  // Method 1: Ternary
  return <div>{isLoggedIn ? <Dashboard /> : <Login />}</div>;

  // Method 2: &&
  return <div>{isLoggedIn && <Dashboard />}</div>;

  // Method 3: if/else (outside JSX)
  if (!isLoggedIn) return <Login />;
  if (role === 'admin') return <AdminDashboard />;
  return <UserDashboard />;
}
```

### 2.8 Lists & Keys
```jsx
const todos = [
  { id: 1, text: 'Learn React', done: false },
  { id: 2, text: 'Build an App', done: true },
];

function TodoList() {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id} style={{ textDecoration: todo.done ? 'line-through' : 'none' }}>
          {todo.text}
        </li>
      ))}
    </ul>
  );
}
// ⚠️ key must be unique and stable — avoid using array index
```

---

<a name="module-3"></a>
## 📦 Module 3 — React Hooks (Core)

### 3.1 useEffect — Side Effects
```jsx
import { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  // Runs after every render
  useEffect(() => { console.log('Rendered'); });

  // Runs only once (on mount)
  useEffect(() => { console.log('Mounted'); }, []);

  // Runs when userId changes
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(setUser);
  }, [userId]);

  // Cleanup (runs before re-run or unmount)
  useEffect(() => {
    const timer = setInterval(() => console.log('tick'), 1000);
    return () => clearInterval(timer); // Cleanup!
  }, []);

  return <div>{user?.name}</div>;
}
```

### 3.2 useRef — DOM Access & Persistent Values
```jsx
import { useRef } from 'react';

function TextInput() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus(); // Direct DOM access
  };

  return (
    <>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus</button>
    </>
  );
}

// Persist value without re-render
function Timer() {
  const countRef = useRef(0); // Doesn't trigger re-render on change

  useEffect(() => {
    const id = setInterval(() => { countRef.current += 1; }, 1000);
    return () => clearInterval(id);
  }, []);
}
```

### 3.3 useContext — Global Data
```jsx
import { createContext, useContext, useState } from 'react';

// 1. Create Context
const ThemeContext = createContext('light');

// 2. Provide Context
function App() {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Page />
    </ThemeContext.Provider>
  );
}

// 3. Consume Context (anywhere in the tree)
function ThemedButton() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button
      style={{ background: theme === 'dark' ? '#333' : '#fff' }}
      onClick={() => setTheme(t => t === 'dark' ? 'light' : 'dark')}
    >
      Toggle Theme
    </button>
  );
}
```

---

<a name="module-4"></a>
## 📦 Module 4 — Component Patterns

### 4.1 Lifting State Up
```jsx
// Move shared state to the nearest common parent
function Parent() {
  const [value, setValue] = useState('');
  return (
    <>
      <InputChild value={value} onChange={setValue} />
      <DisplayChild value={value} />
    </>
  );
}
```

### 4.2 Compound Components Pattern
```jsx
// Tab component using compound pattern
function Tabs({ children, defaultTab }) {
  const [active, setActive] = useState(defaultTab);
  return (
    <TabContext.Provider value={{ active, setActive }}>
      {children}
    </TabContext.Provider>
  );
}

Tabs.Tab = function Tab({ id, children }) {
  const { active, setActive } = useContext(TabContext);
  return (
    <button
      className={active === id ? 'active' : ''}
      onClick={() => setActive(id)}
    >{children}</button>
  );
};

Tabs.Panel = function Panel({ id, children }) {
  const { active } = useContext(TabContext);
  return active === id ? <div>{children}</div> : null;
};

// Usage
<Tabs defaultTab="home">
  <Tabs.Tab id="home">Home</Tabs.Tab>
  <Tabs.Tab id="about">About</Tabs.Tab>
  <Tabs.Panel id="home">Home Content</Tabs.Panel>
  <Tabs.Panel id="about">About Content</Tabs.Panel>
</Tabs>
```

### 4.3 Render Props Pattern
```jsx
function MouseTracker({ render }) {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  return (
    <div onMouseMove={e => setPos({ x: e.clientX, y: e.clientY })}>
      {render(pos)}
    </div>
  );
}

// Usage
<MouseTracker render={({ x, y }) => <p>Mouse at {x}, {y}</p>} />
```

### 4.4 Higher Order Components (HOC)
```jsx
function withAuth(Component) {
  return function ProtectedComponent(props) {
    const { isAuthenticated } = useAuth();
    if (!isAuthenticated) return <Navigate to="/login" />;
    return <Component {...props} />;
  };
}

// Usage
const ProtectedDashboard = withAuth(Dashboard);
```

---

<a name="module-5"></a>
## 📦 Module 5 — Routing with React Router v6

### 5.1 Setup
```bash
npm install react-router-dom
```

### 5.2 Basic Routing
```jsx
import { BrowserRouter, Routes, Route, Link, NavLink } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <NavLink to="/" className={({ isActive }) => isActive ? 'active' : ''}>Home</NavLink>
        <NavLink to="/about">About</NavLink>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users/:id" element={<UserDetail />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### 5.3 Route Params & Navigation
```jsx
import { useParams, useNavigate, useLocation, useSearchParams } from 'react-router-dom';

function UserDetail() {
  const { id } = useParams();               // URL params
  const navigate = useNavigate();           // Programmatic navigation
  const location = useLocation();           // Current location object
  const [searchParams] = useSearchParams(); // ?query=value

  const query = searchParams.get('query');

  return (
    <div>
      <h1>User ID: {id}</h1>
      <button onClick={() => navigate(-1)}>Go Back</button>
      <button onClick={() => navigate('/home', { state: { from: 'UserDetail' } })}>
        Go Home
      </button>
    </div>
  );
}
```

### 5.4 Nested Routes & Layout Routes
```jsx
function App() {
  return (
    <Routes>
      <Route path="/" element={<Layout />}>      {/* Layout wraps children */}
        <Route index element={<Home />} />
        <Route path="dashboard" element={<Dashboard />}>
          <Route index element={<DashboardHome />} />
          <Route path="settings" element={<Settings />} />
        </Route>
      </Route>
    </Routes>
  );
}

// Layout component — must include <Outlet />
function Layout() {
  return (
    <div>
      <Navbar />
      <main>
        <Outlet />           {/* Child routes render here */}
      </main>
      <Footer />
    </div>
  );
}
```

### 5.5 Protected Routes
```jsx
function PrivateRoute({ children }) {
  const { user } = useAuth();
  return user ? children : <Navigate to="/login" replace />;
}

// Usage in Routes
<Route path="/dashboard" element={
  <PrivateRoute><Dashboard /></PrivateRoute>
} />
```

---

<a name="module-6"></a>
## 📦 Module 6 — Data Fetching & APIs

### 6.1 Fetch API (Basic)
```jsx
function Posts() {
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();
    
    fetch('https://jsonplaceholder.typicode.com/posts', {
      signal: controller.signal
    })
      .then(res => {
        if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
        return res.json();
      })
      .then(data => { setPosts(data); setLoading(false); })
      .catch(err => {
        if (err.name !== 'AbortError') setError(err.message);
      });

    return () => controller.abort(); // Cleanup on unmount
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return <ul>{posts.map(p => <li key={p.id}>{p.title}</li>)}</ul>;
}
```

### 6.2 Axios (Alternative)
```bash
npm install axios
```
```jsx
import axios from 'axios';

// Axios instance with defaults
const api = axios.create({
  baseURL: 'https://api.example.com',
  headers: { 'Content-Type': 'application/json' }
});

// Interceptors for auth token
api.interceptors.request.use(config => {
  config.headers.Authorization = `Bearer ${localStorage.getItem('token')}`;
  return config;
});

// Usage
const { data } = await api.get('/users');
await api.post('/users', { name: 'Alice' });
await api.put(`/users/${id}`, updatedUser);
await api.delete(`/users/${id}`);
```

### 6.3 TanStack Query (React Query) — Recommended
```bash
npm install @tanstack/react-query
```
```jsx
import { QueryClient, QueryClientProvider, useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

const queryClient = new QueryClient();

// Wrap App
function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <MyApp />
    </QueryClientProvider>
  );
}

// Fetch data
function Posts() {
  const { data, isLoading, error } = useQuery({
    queryKey: ['posts'],
    queryFn: () => fetch('/api/posts').then(r => r.json()),
    staleTime: 1000 * 60 * 5, // Cache for 5 minutes
  });

  if (isLoading) return <Spinner />;
  if (error) return <Error message={error.message} />;
  return <PostList posts={data} />;
}

// Mutate data
function AddPost() {
  const queryClient = useQueryClient();
  const mutation = useMutation({
    mutationFn: (post) => fetch('/api/posts', { method: 'POST', body: JSON.stringify(post) }),
    onSuccess: () => queryClient.invalidateQueries({ queryKey: ['posts'] }), // Refetch
  });

  return <button onClick={() => mutation.mutate({ title: 'New Post' })}>Add</button>;
}
```

---

<a name="module-7"></a>
## 📦 Module 7 — Advanced Hooks

### 7.1 useReducer — Complex State Logic
```jsx
import { useReducer } from 'react';

const initialState = { count: 0, history: [] };

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1, history: [...state.history, 'increment'] };
    case 'DECREMENT':
      return { count: state.count - 1, history: [...state.history, 'decrement'] };
    case 'RESET':
      return initialState;
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
      <button onClick={() => dispatch({ type: 'RESET' })}>Reset</button>
    </div>
  );
}
```

### 7.2 useMemo & useCallback — Memoization
```jsx
import { useMemo, useCallback } from 'react';

function ExpensiveList({ items, filter, onItemClick }) {
  // useMemo — memoize a computed value
  const filteredItems = useMemo(
    () => items.filter(item => item.name.includes(filter)),
    [items, filter] // Recompute only when these change
  );

  // useCallback — memoize a function reference
  const handleClick = useCallback(
    (id) => { onItemClick(id); },
    [onItemClick]
  );

  return (
    <ul>
      {filteredItems.map(item => (
        <li key={item.id} onClick={() => handleClick(item.id)}>{item.name}</li>
      ))}
    </ul>
  );
}
```

### 7.3 Custom Hooks — Reusable Logic
```jsx
// useFetch — reusable data fetching
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then(res => res.json())
      .then(d => { setData(d); setLoading(false); })
      .catch(e => { setError(e); setLoading(false); });
  }, [url]);

  return { data, loading, error };
}

// useLocalStorage — persist state
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(
    () => JSON.parse(localStorage.getItem(key)) ?? initialValue
  );

  const setStoredValue = (newValue) => {
    setValue(newValue);
    localStorage.setItem(key, JSON.stringify(newValue));
  };

  return [value, setStoredValue];
}

// useDebounce — delay execution
function useDebounce(value, delay) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const timer = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);
  return debounced;
}

// Usage
function SearchBox() {
  const [query, setQuery] = useState('');
  const debouncedQuery = useDebounce(query, 400);
  const { data } = useFetch(`/api/search?q=${debouncedQuery}`);
  // ...
}
```

---

<a name="module-8"></a>
## 📦 Module 8 — State Management

### 8.1 Context API (Built-in)
Best for: Theme, Auth, Language — app-wide but infrequently updated data.
```jsx
// auth-context.jsx
const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = async (credentials) => {
    const userData = await loginAPI(credentials);
    setUser(userData);
  };

  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export const useAuth = () => useContext(AuthContext);
```

### 8.2 Zustand — Lightweight & Recommended
```bash
npm install zustand
```
```jsx
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

// Store
const useCartStore = create(
  persist(
    (set, get) => ({
      items: [],
      total: 0,
      addItem: (item) => set(state => ({
        items: [...state.items, item],
        total: state.total + item.price
      })),
      removeItem: (id) => set(state => ({
        items: state.items.filter(i => i.id !== id),
        total: state.total - state.items.find(i => i.id === id)?.price
      })),
      clearCart: () => set({ items: [], total: 0 }),
    }),
    { name: 'cart-storage' } // Persist to localStorage
  )
);

// Usage — no Provider needed!
function CartButton() {
  const { items, addItem } = useCartStore();
  return (
    <button onClick={() => addItem({ id: 1, name: 'Phone', price: 999 })}>
      Cart ({items.length})
    </button>
  );
}
```

### 8.3 Redux Toolkit (Large Apps)
```bash
npm install @reduxjs/toolkit react-redux
```
```jsx
// store/counterSlice.js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

// Async thunk
export const fetchUser = createAsyncThunk('user/fetch', async (id) => {
  const res = await fetch(`/api/users/${id}`);
  return res.json();
});

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0, status: 'idle' },
  reducers: {
    increment: state => { state.value += 1; },
    decrement: state => { state.value -= 1; },
    incrementByAmount: (state, action) => { state.value += action.payload; },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchUser.pending, state => { state.status = 'loading'; })
      .addCase(fetchUser.fulfilled, (state, action) => {
        state.status = 'idle';
        state.user = action.payload;
      });
  }
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default counterSlice.reducer;

// store/index.js
import { configureStore } from '@reduxjs/toolkit';
const store = configureStore({ reducer: { counter: counterReducer } });

// Component
import { useSelector, useDispatch } from 'react-redux';
function Counter() {
  const count = useSelector(state => state.counter.value);
  const dispatch = useDispatch();
  return <button onClick={() => dispatch(increment())}>Count: {count}</button>;
}
```

---

<a name="module-9"></a>
## 📦 Module 9 — Styling Approaches

### 9.1 CSS Modules (Scoped CSS)
```css
/* Button.module.css */
.button { padding: 8px 16px; border-radius: 4px; }
.primary { background: #007bff; color: white; }
.danger  { background: #dc3545; color: white; }
```
```jsx
import styles from './Button.module.css';

function Button({ variant = 'primary', children }) {
  return (
    <button className={`${styles.button} ${styles[variant]}`}>
      {children}
    </button>
  );
}
```

### 9.2 Tailwind CSS (Utility-First)
```bash
npm install tailwindcss @tailwindcss/vite
```
```jsx
function Card({ title, description }) {
  return (
    <div className="bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition-shadow">
      <h2 className="text-xl font-bold text-gray-900 mb-2">{title}</h2>
      <p className="text-gray-600 text-sm">{description}</p>
      <button className="mt-4 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700">
        Read More
      </button>
    </div>
  );
}
```

### 9.3 Styled Components (CSS-in-JS)
```bash
npm install styled-components
```
```jsx
import styled from 'styled-components';

const Button = styled.button`
  padding: 8px 16px;
  border-radius: 4px;
  background: ${props => props.variant === 'primary' ? '#007bff' : '#6c757d'};
  color: white;
  border: none;
  cursor: pointer;

  &:hover {
    opacity: 0.9;
  }
`;

// Usage
<Button variant="primary">Submit</Button>
<Button variant="secondary">Cancel</Button>
```

---

<a name="module-10"></a>
## 📦 Module 10 — Forms & Validation

### 10.1 Controlled Forms (Basic)
```jsx
function RegisterForm() {
  const [form, setForm] = useState({ name: '', email: '', password: '' });
  const [errors, setErrors] = useState({});

  const validate = () => {
    const errs = {};
    if (!form.name) errs.name = 'Name is required';
    if (!/\S+@\S+\.\S+/.test(form.email)) errs.email = 'Invalid email';
    if (form.password.length < 6) errs.password = 'Min 6 characters';
    return errs;
  };

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prev => ({ ...prev, [name]: value }));
    setErrors(prev => ({ ...prev, [name]: '' }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const errs = validate();
    if (Object.keys(errs).length) { setErrors(errs); return; }
    console.log('Submitted:', form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input name="name" value={form.name} onChange={handleChange} placeholder="Name" />
        {errors.name && <span className="error">{errors.name}</span>}
      </div>
      <div>
        <input name="email" value={form.email} onChange={handleChange} placeholder="Email" />
        {errors.email && <span className="error">{errors.email}</span>}
      </div>
      <button type="submit">Register</button>
    </form>
  );
}
```

### 10.2 React Hook Form (Recommended for Complex Forms)
```bash
npm install react-hook-form zod @hookform/resolvers
```
```jsx
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const schema = z.object({
  name: z.string().min(2, 'Name must be at least 2 characters'),
  email: z.string().email('Invalid email address'),
  password: z.string().min(6, 'Password must be at least 6 characters'),
});

function RegisterForm() {
  const { register, handleSubmit, formState: { errors, isSubmitting } } = useForm({
    resolver: zodResolver(schema),
  });

  const onSubmit = async (data) => {
    await new Promise(r => setTimeout(r, 1000)); // Simulate API
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('name')} placeholder="Name" />
      {errors.name && <p>{errors.name.message}</p>}

      <input {...register('email')} placeholder="Email" />
      {errors.email && <p>{errors.email.message}</p>}

      <input {...register('password')} type="password" placeholder="Password" />
      {errors.password && <p>{errors.password.message}</p>}

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Registering...' : 'Register'}
      </button>
    </form>
  );
}
```

---

<a name="module-11"></a>
## 📦 Module 11 — Performance Optimization

### 11.1 React.memo — Skip Re-renders
```jsx
// Without memo: re-renders whenever parent renders
// With memo: only re-renders when props actually change
const ExpensiveChild = React.memo(function ExpensiveChild({ data, onClick }) {
  console.log('ExpensiveChild rendered');
  return <div onClick={onClick}>{data.title}</div>;
});
```

### 11.2 Code Splitting & Lazy Loading
```jsx
import { lazy, Suspense } from 'react';

// Lazy load components (dynamic import)
const Dashboard = lazy(() => import('./pages/Dashboard'));
const Settings  = lazy(() => import('./pages/Settings'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/settings"  element={<Settings />} />
      </Routes>
    </Suspense>
  );
}
```

### 11.3 Virtualization (Large Lists)
```bash
npm install @tanstack/react-virtual
```
```jsx
import { useVirtualizer } from '@tanstack/react-virtual';

function VirtualList({ items }) {
  const parentRef = useRef(null);

  const virtualizer = useVirtualizer({
    count: items.length,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 50,
  });

  return (
    <div ref={parentRef} style={{ height: '500px', overflow: 'auto' }}>
      <div style={{ height: virtualizer.getTotalSize() }}>
        {virtualizer.getVirtualItems().map(virtualItem => (
          <div key={virtualItem.key} style={{ transform: `translateY(${virtualItem.start}px)` }}>
            {items[virtualItem.index].name}
          </div>
        ))}
      </div>
    </div>
  );
}
```

### 11.4 Performance Checklist
- ✅ Use React.memo for components with expensive renders
- ✅ Use useCallback to stabilize function props
- ✅ Use useMemo for expensive computations
- ✅ Code split large pages/routes
- ✅ Virtualize long lists (1000+ items)
- ✅ Avoid inline objects/functions in JSX (creates new reference each render)
- ✅ Use React DevTools Profiler to identify bottlenecks

---

<a name="module-12"></a>
## 📦 Module 12 — Testing React Apps

### 12.1 Setup
```bash
# Vitest + Testing Library (recommended with Vite)
npm install -D vitest @testing-library/react @testing-library/jest-dom @testing-library/user-event jsdom
```

### 12.2 Unit Testing Components
```jsx
// Button.test.jsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect, vi } from 'vitest';
import Button from './Button';

describe('Button', () => {
  it('renders the label', () => {
    render(<Button label="Click Me" onClick={() => {}} />);
    expect(screen.getByText('Click Me')).toBeInTheDocument();
  });

  it('calls onClick when clicked', async () => {
    const handleClick = vi.fn();
    render(<Button label="Click" onClick={handleClick} />);
    await userEvent.click(screen.getByText('Click'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('is disabled when loading', () => {
    render(<Button label="Submit" loading={true} />);
    expect(screen.getByRole('button')).toBeDisabled();
  });
});
```

### 12.3 Testing Async & API Calls
```jsx
import { rest } from 'msw';
import { setupServer } from 'msw/node';

const server = setupServer(
  rest.get('/api/users', (req, res, ctx) => {
    return res(ctx.json([{ id: 1, name: 'Alice' }]));
  })
);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());

it('fetches and displays users', async () => {
  render(<UserList />);
  expect(screen.getByText('Loading...')).toBeInTheDocument();
  await screen.findByText('Alice'); // Waits for async
  expect(screen.queryByText('Loading...')).not.toBeInTheDocument();
});
```

---

<a name="module-13"></a>
## 📦 Module 13 — TypeScript with React

### 13.1 Setup
```bash
npm create vite@latest my-app -- --template react-ts
```

### 13.2 Typing Components & Props
```tsx
// Types for props
interface UserCardProps {
  name: string;
  age: number;
  isAdmin?: boolean;
  onClick: (id: number) => void;
  children?: React.ReactNode;
}

const UserCard: React.FC<UserCardProps> = ({ name, age, isAdmin = false, onClick, children }) => {
  return (
    <div>
      <h2>{name} ({age})</h2>
      {isAdmin && <span>Admin</span>}
      {children}
      <button onClick={() => onClick(1)}>Select</button>
    </div>
  );
};
```

### 13.3 Typing Hooks
```tsx
// useState with type
const [user, setUser] = useState<User | null>(null);
const [items, setItems] = useState<string[]>([]);

// useRef with type
const inputRef = useRef<HTMLInputElement>(null);

// Custom hook with types
interface FetchResult<T> {
  data: T | null;
  loading: boolean;
  error: string | null;
}

function useFetch<T>(url: string): FetchResult<T> {
  const [data, setData] = useState<T | null>(null);
  // ...
  return { data, loading, error };
}

// Usage
const { data } = useFetch<User[]>('/api/users');
```

---

<a name="module-14"></a>
## 📦 Module 14 — Next.js (Full-Stack React)

### 14.1 Setup
```bash
npx create-next-app@latest my-app --typescript --tailwind --app
```

### 14.2 App Router — File-Based Routing
```
app/
├── layout.tsx          → Root layout (wraps all pages)
├── page.tsx            → Home page (/)
├── about/
│   └── page.tsx        → About page (/about)
├── blog/
│   ├── page.tsx        → Blog index (/blog)
│   └── [slug]/
│       └── page.tsx    → Dynamic route (/blog/:slug)
└── api/
    └── users/
        └── route.ts    → API Route (/api/users)
```

### 14.3 Server vs Client Components
```tsx
// Server Component (default) — runs on server, no hooks
// app/page.tsx
async function HomePage() {
  const posts = await fetch('https://api.example.com/posts').then(r => r.json());
  return <PostList posts={posts} />;
}

// Client Component — for interactivity, hooks, events
// components/Counter.tsx
'use client';
import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(c => c + 1)}>Count: {count}</button>;
}
```

### 14.4 API Routes
```tsx
// app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET() {
  const users = await db.users.findAll();
  return NextResponse.json(users);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await db.users.create(body);
  return NextResponse.json(user, { status: 201 });
}
```

### 14.5 Metadata & SEO
```tsx
// Static metadata
export const metadata = {
  title: 'My App',
  description: 'Built with Next.js',
  openGraph: { title: 'My App', images: ['/og-image.png'] }
};

// Dynamic metadata
export async function generateMetadata({ params }) {
  const post = await getPost(params.slug);
  return { title: post.title, description: post.excerpt };
}
```

---

<a name="module-15"></a>
## 📦 Module 15 — Deployment & DevOps

### 15.1 Deploying React (Vite) to Vercel
```bash
# Build
npm run build        # Creates /dist folder

# Deploy with Vercel CLI
npm install -g vercel
vercel               # Follow prompts — auto-detects Vite!

# Or connect GitHub repo at vercel.com for auto-deploy on push
```

### 15.2 Deploying Next.js
```bash
# Vercel (recommended — made by same team)
vercel

# Or self-hosted with Docker
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN npm ci && npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

### 15.3 Environment Variables
```bash
# .env.local (never commit this!)
VITE_API_URL=https://api.example.com
NEXT_PUBLIC_API_URL=https://api.example.com  # Next.js prefix for client

# Access in code
const api = import.meta.env.VITE_API_URL;       // Vite
const api = process.env.NEXT_PUBLIC_API_URL;     // Next.js
```

### 15.4 CI/CD with GitHub Actions
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
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with: { node-version: '20' }
      - run: npm ci
      - run: npm run build
      - run: npm test
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
```

---

<a name="projects"></a>
## 🏗️ Project Ideas by Module

| Level | Project | Modules Used |
|-------|---------|-------------|
| Beginner | Todo App | M2, M3 |
| Beginner | Weather App | M2, M3, M6 |
| Beginner | Quiz App | M2, M3, M4 |
| Intermediate | Movie Search App | M5, M6, M9 |
| Intermediate | E-Commerce Cart | M5, M8, M10 |
| Intermediate | Blog with Auth | M5, M6, M8 |
| Advanced | Full-stack CRUD App | M14, all |
| Advanced | Real-time Chat | M14, WebSockets |
| Advanced | Dashboard + Charts | M6, M8, M11 |

---

## 📚 Best Resources

| Resource | Type | Link |
|----------|------|------|
| Official React Docs | Docs | react.dev |
| The Odin Project | Course | theodinproject.com |
| TanStack Docs | Docs | tanstack.com |
| Next.js Docs | Docs | nextjs.org/docs |
| Jack Herrington | YouTube | youtube.com/@jherr |
| Fireship | YouTube | youtube.com/@Fireship |
| Kevin Powell (CSS) | YouTube | youtube.com/@KevinPowell |
| Josh W Comeau | Blog | joshwcomeau.com |

---

## 🗺️ Learning Roadmap

```
WEEK 1-2 : Module 1  → JavaScript ES6+, Node setup
WEEK 3-4 : Module 2  → JSX, Components, Props, State
WEEK 5   : Module 3  → useEffect, useRef, useContext
WEEK 6   : Module 4  → Component Patterns
WEEK 7   : Module 5  → React Router
WEEK 8   : Module 6  → Data Fetching + React Query
WEEK 9   : Module 7  → Advanced Hooks + Custom Hooks
WEEK 10  : Module 8  → State Management (Zustand)
WEEK 11  : Module 9  → Styling (Tailwind CSS)
WEEK 12  : Module 10 → Forms + Validation
WEEK 13  : Module 11 → Performance Optimization
WEEK 14  : Module 12 → Testing
WEEK 15  : Module 13 → TypeScript
WEEK 16+ : Module 14 → Next.js
           Module 15 → Deployment
```

---

> 💡 **Golden Rule:** After each module, build something. Don't move forward until you can build a mini-project using what you've learned. The best React developer is the one who builds the most.
