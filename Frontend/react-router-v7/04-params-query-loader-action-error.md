# Params, Query Params, Loader, Action & Error Handling

This file covers **data + mutations + URL-driven state**.
This is the heart of React Router v7.

---

## 1. Route Params

### Route definition (in `router.ts`)

```ts
{
  path: 'posts/:postId',
  element: <Post />,
  loader: postLoader,
}
````

### File: `src/routes/post.tsx`

```tsx
import { useParams } from 'react-router';

export default function Post() {
  const { postId } = useParams();
  return <p>Post ID: {postId}</p>;
}
```

---

## 2. Query Params (Search Params)

### File: `src/routes/posts.tsx`

```tsx
import { useSearchParams } from 'react-router';

export default function Posts() {
  const [searchParams, setSearchParams] = useSearchParams();

  const page = searchParams.get('page') ?? '1';

  return (
    <>
      <p>Page: {page}</p>
      <button onClick={() => setSearchParams({ page: '2' })}>
        Next
      </button>
    </>
  );
}
```

Rules:

- Query params = filters, pagination, sorting
    
- Changing search params **re-runs loader**
    

---

## 3. Loader (Data Fetching)

### File: `src/routes/posts.tsx`

```ts
export async function loader() {
  const res = await fetch('/api/posts');

  if (!res.ok) {
    throw new Response('Failed to load posts', { status: 500 });
  }

  return res.json();
}
```

### Using loader data

```tsx
import { useLoaderData } from 'react-router';

const posts = useLoaderData<typeof loader>();
```

Rules:

- Runs before render
    
- Runs on navigation & revalidation
    
- Replaces most `useEffect` fetching
    

---

## 4. Action (Mutations)

### File: `src/routes/posts.tsx`

```ts
export async function action({ request }) {
  const formData = await request.formData();

  await fetch('/api/posts', {
    method: 'POST',
    body: formData,
  });

  return null;
}
```

Rules:

- Handles POST / PUT / DELETE
    
- Used with `<Form />`
    
- Automatically revalidates loaders
    

---

## 5. Error Boundary

### File: `src/routes/posts.tsx`

```tsx
import { useRouteError } from 'react-router';

export function ErrorBoundary() {
  const error = useRouteError();
  return <p>Something went wrong</p>;
}
```

### Route config

```ts
{
  path: 'posts',
  element: <Posts />,
  loader,
  action,
  errorElement: <ErrorBoundary />,
}
```

Rules:

- Errors bubble to nearest errorElement
    
- Loader + action errors both land here
    

---

## Mental Model (Important)

```txt
URL change → loader → render
Form submit → action → revalidate loaders
```
