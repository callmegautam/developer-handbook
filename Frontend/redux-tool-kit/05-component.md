
# Redux Hooks (Usage)

Use hooks instead of `connect`.

## Typed hooks (recommended)

```ts
import { useDispatch, useSelector } from 'react-redux';
import type { RootState, AppDispatch } from './store';

export const useAppDispatch = () => useDispatch<AppDispatch>();
export const useAppSelector = useSelector.withTypes<RootState>();
````

## Using in components

```tsx
import { useAppDispatch, useAppSelector } from '../store/hooks';
import { addTodo, toggleTodo } from '../store/slices/todoSlice';

const dispatch = useAppDispatch();

dispatch(toggleTodo(id));

const todos = useAppSelector(state => state.todos.todos);
```

Notes:

- Always select minimal state
    
- Dispatch actions, never call reducers directly

---
