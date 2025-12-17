

# Store

The store:
- holds the entire app state
- combines all slice reducers
- provides dispatch + getState

## `store.ts`

```ts
import { configureStore } from '@reduxjs/toolkit';
import todoReducer from './slices/todoSlice';

export const store = configureStore({
  reducer: {
    todos: todoReducer,
  },
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
````

Notes:

- `configureStore` sets up DevTools + middleware automatically
    
- No `createStore` in modern Redux

---