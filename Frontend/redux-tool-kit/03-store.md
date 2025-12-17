# Store

The store is the central hub of the application. It holds the state of the application and provides methods to access and update the state. The store is created using the `createStore` function from the `@reduxjs/toolkit` package.

### create `store.js` file

```js
import { configureStore } from '@reduxjs/toolkit';
import todoReducer from './slices/todoSlice';

export const store = configureStore({
    reducer: {
        todos: todoReducer,
    },
});
```

for typescript

# create `store.ts` file

```ts
import { configureStore } from '@reduxjs/toolkit';
import todosSlice from './slices/todoSlice';

export const store = configureStore({
    reducer: {
        todos: todosSlice,
    },
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```
