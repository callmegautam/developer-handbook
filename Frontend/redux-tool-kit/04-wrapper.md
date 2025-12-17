# Wrapper

A wrapper is a component that provides a higher-level interface for other components. It is used to encapsulate the logic and state of a component and to provide a more convenient way to use it.

### create `App.js` file

```js
import { Provider } from 'react-redux';
import { store } from './store/store.ts';

<Provider store={store}>
    <App />
</Provider>;
```
