
## `04-provider.md`

# Provider (Wrapper)

`Provider` makes the Redux store available to the entire React tree.

## `main.tsx` or `index.tsx`

```tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from 'react-redux';
import { store } from './store/store';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')!).render(
  <Provider store={store}>
    <App />
  </Provider>
);
````

Notes:

- Provider must wrap the app once
    
- Never create store inside a component

---