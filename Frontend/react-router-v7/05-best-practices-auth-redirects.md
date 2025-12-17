# React Router v7 – Best Practices, Auth & Redirects

This file covers things that are NOT optional in real apps.

---

## 1. Redirects (Loader-based)

Redirects should happen in loaders, not components.

### File: `src/routes/protected.tsx`

```ts
import { redirect } from 'react-router';

export async function loader() {
  const isLoggedIn = false; // check cookie / session

  if (!isLoggedIn) {
    throw redirect('/login');
  }

  return null;
}
````

Rules:

- Redirects are control flow
    
- UI should never decide navigation based on auth
    

---

## 2. Auth-Protected Routes (Correct Pattern)

### File: `src/routes/dashboard.tsx`

```tsx
export async function loader() {
  const user = await getUser();

  if (!user) {
    throw redirect('/login');
  }

  return user;
}

export default function Dashboard() {
  return <h1>Dashboard</h1>;
}
```

Why this is correct:

- Auth check happens before render
    
- No UI flicker
    
- Works on refresh
    

---

## 3. `<Form />` vs `fetch`

Always prefer `<Form />`.

### Correct

```tsx
import { Form } from 'react-router';

<Form method="post">
  <input name="title" />
  <button type="submit">Create</button>
</Form>
```

Why:

- Auto calls action
    
- Handles pending states
    
- Revalidates loaders automatically
    

Avoid:

- manual `fetch` in onSubmit
    
- storing server data in state
    

---

## 4. When NOT to Use React Query

Do NOT use React Query for:

- route-level data
    
- server-rendered pages
    
- SEO-critical pages
    

Use React Query only for:

- client-only interactions
    
- background polling
    
- highly interactive widgets
    

Rule:

- URL data → React Router
    
- UI-only data → React Query
    

---

## 5. Performance Rules

- Keep loaders small and focused
    
- Fetch only what the route needs
    
- Split routes, not components
    
- Use nested routes to avoid refetching parent data
    

---

## 6. Common Anti-Patterns (Avoid)

- ❌ useEffect + fetch for page data
    
- ❌ auth logic inside components
    
- ❌ global state for server data
    
- ❌ one giant routes file
    
- ❌ imperative navigation for control flow
    

---

## Final Mental Model (Lock This In)

```txt
Router controls data
Loader controls fetch
Action controls mutation
UI only renders results
```

If you follow this, React Router v7 feels boring
and boring architecture is the goal.