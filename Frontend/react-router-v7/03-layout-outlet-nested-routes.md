# Layout, Outlet & Nested Routes

Layouts are routes that render shared UI and delegate
child rendering using `<Outlet />`.

---

## File: `src/routes/root.tsx`

```tsx
import { Outlet } from 'react-router';

export default function RootLayout() {
  return (
    <>
      <header>Navbar</header>

      <main>
        <Outlet />
      </main>

      <footer>Footer</footer>
    </>
  );
}
````

---

## How `<Outlet />` Works

- `<Outlet />` is a **placeholder**
    
- React Router renders the matched child route here
    
- Without `<Outlet />`, child routes will NOT render
    

---

## Nested Route Configuration (from `router.ts`)

```ts
{
  path: '/',
  element: <RootLayout />,
  children: [
    { index: true, element: <Home /> },
    { path: 'posts', element: <Posts /> },
  ],
}
```

URL → Rendered UI:

```txt
/        → RootLayout + Home
/posts   → RootLayout + Posts
```

---

## Nested Layouts (Advanced)

```ts
{
  path: 'dashboard',
  element: <DashboardLayout />,
  children: [
    { index: true, element: <DashboardHome /> },
    { path: 'settings', element: <Settings /> },
  ],
}
```

Each layout **must** render its own `<Outlet />`.

---

## Rules (Important)

- Layout = route + UI shell
    
- Outlet = child injection point
    
- Nested routes share parent loaders (if any)
    
- Deep nesting is OK, over-nesting is not
    

---

## Common Mistakes

- ❌ Forgetting `<Outlet />`
    
- ❌ Using layouts as normal components
    
- ❌ Duplicating navbar in every page
    

---
