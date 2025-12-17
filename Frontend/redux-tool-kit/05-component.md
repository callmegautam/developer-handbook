```js
import { useDispatch, useSelector } from 'react-redux';
import { addTodo, toggleTodo } from '../store/todoSlice';
import type { RootState } from '../store/store';
import type React from 'react';

const dispatch = useDispatch();

dispatch(toggleTodo(id));

const todos = useSelector((state: RootState) => state.todos.todos);
```
