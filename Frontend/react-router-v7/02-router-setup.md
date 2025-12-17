# React Router v7 – Router Setup

This file defines **how URLs map to route modules**.
All routing starts here.

---

## File: `src/router.ts`

```tsx
import { createBrowserRouter } from 'react-router';
import RootLayout from './routes/root';
import Home from './routes/home';
import Posts, { loader as postsLoader } from './routes/posts';
import Post, { loader as postLoader } from './routes/post';

export const router = createBrowserRouter([
  {
    path: '/',
    element: <RootLayout />,
    children: [
      { index: true, element: <Home /> },
      {
        path: 'posts',
        element: <Posts />,
        loader: postsLoader,
      },
      {
        path: 'posts/:postId',
        element: <Post />,
        loader: postLoader,
      },
    ],
  },
]);
````

---

## File: `src/main.tsx`

```tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { RouterProvider } from 'react-router';
import { router } from './router';

ReactDOM.createRoot(document.getElementById('root')!).render(
  <RouterProvider router={router} />
);
```

---

## Key Points (memory notes)

- `createBrowserRouter` = data router (mandatory for loaders/actions)
    
- Routes are **objects**, not JSX
    
- `index: true` = default child route
    
- Child paths are **relative**, never start with `/`
    
- RouterProvider is mounted **once**
    

---

## Common Mistakes

- ❌ Using `<BrowserRouter>` with loaders
    
- ❌ Creating router inside a component
    
- ❌ Absolute paths in children (`/posts`)
    

---
