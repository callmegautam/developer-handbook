# Slice

A slice:
- owns a piece of state
- defines reducers (state updates)
- auto-generates action creators

One slice = one domain (todos, auth, user, etc.)

## `todoSlice.ts`

```ts
import { createSlice, type PayloadAction } from '@reduxjs/toolkit';

export interface Todo {
  id: string;
  title: string;
  completed: boolean;
}

interface TodoState {
  todos: Todo[];
}

const initialState: TodoState = {
  todos: [],
};

const todoSlice = createSlice({
  name: 'todos',
  initialState,
  reducers: {
    addTodo(state, action: PayloadAction<Todo>) {
      state.todos.push(action.payload);
    },
    removeTodo(state, action: PayloadAction<string>) {
      state.todos = state.todos.filter(t => t.id !== action.payload);
    },
    toggleTodo(state, action: PayloadAction<string>) {
      const todo = state.todos.find(t => t.id === action.payload);
      if (todo) todo.completed = !todo.completed;
    },
  },
});

export const { addTodo, removeTodo, toggleTodo } = todoSlice.actions;
export default todoSlice.reducer;
````

Notes:

- Direct mutation is OK (Immer under the hood)
    
- Reducers must be synchronous

---
