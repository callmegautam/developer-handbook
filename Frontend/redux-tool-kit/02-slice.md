# Slice

A slice is a part of the state tree. It is a small part of the state tree that is responsible for a single part of the application. Slices are used to group related state together and to keep the state of the application in a manageable way.

### create `todoSlice.js` file

```js
import { createSlice } from '@reduxjs/toolkit';

const todoSlice = createSlice({
    name: 'todos',
    initialState: {
        todos: [],
    },
    reducers: {
        addTodo: (state: , action) => {
            state.todos.push(action.payload);
        },
        removeTodo: (state, action) => {
            state.todos = state.todos.filter((todo) => todo.id !== action.payload);
        },
        toggleTodo: (state, action) => {
            const todo = state.todos.find((todo) => todo.id === action.payload);
            if (todo) {
                todo.completed = !todo.completed;
            }
        },
    },
});

export const { addTodo, removeTodo, toggleTodo } = todoSlice.actions;
export default todoSlice.reducer;
```

for typescript

```ts
import { createSlice, type PayloadAction } from '@reduxjs/toolkit';

interface Todo {
    id: string;
    title: string;
    completed: boolean;
}

interface TodoState {
    todos: Todo[];
}

const todoSlice = createSlice({
    name: 'todos',
    initialState: {
        todos: [],
    } as TodoState,
    reducers: {
        addTodo: (state: TodoState, action: PayloadAction<Todo>) => {
            state.todos.push(action.payload);
        },
        removeTodo: (state: TodoState, action: PayloadAction<string>) => {
            state.todos = state.todos.filter((todo) => todo.id !== action.payload);
        },
        toggleTodo: (state: TodoState, action: PayloadAction<string>) => {
            const todo = state.todos.find((todo) => todo.id === action.payload);
            if (todo) {
                todo.completed = !todo.completed;
            }
        },
    },
});

export const { addTodo, removeTodo, toggleTodo } = todoSlice.actions;
export default todoSlice.reducer;
```
