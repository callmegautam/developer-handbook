# React Router v7 – Folder Structure

React Router v7 works best when routes are treated as **modules**.
Each route owns:
- UI
- data (loader)
- mutations (action)
- errors

## Recommended Structure (Production)

``
```
src/
├─ routes/
│  ├─ root.tsx          # Root layout (Navbar, Footer, <Outlet />)
│  ├─ home.tsx          # "/" route
│  ├─ posts.tsx         # "/posts"
│  ├─ post.tsx          # "/posts/:postId"
│
├─ router.ts            # createBrowserRouter config
├─ main.tsx             # RouterProvider entry
└─ app.css
```

---

## Why this structure works

- **One file = one route**
    
- No “pages/components/hooks” mess
    
- Easy to colocate:
    
    - `loader`
        
    - `action`
        
    - `ErrorBoundary`
        
- Scales cleanly for large apps
    

---

## What lives inside a route file (`posts.tsx` example)

posts.tsx can export:

- `default` → route component
    
- `loader` → data fetching
    
- `action` → mutations
    
- `ErrorBoundary` → error UI
    

This keeps logic **close to the URL it belongs to**.

---

## Rules (important)

- ❌ Don’t fetch server data in `useEffect`
    
- ❌ Don’t centralize all loaders in one file
    
- ✅ Keep routes flat, layouts nested
    
- ✅ Let URL drive state, not Redux
    

---
