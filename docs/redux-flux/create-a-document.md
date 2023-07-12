---
sidebar_position: 1
sidebar_label: Redux Flux Conversion
---

# Convert Our Flux System to Redux

## Redux Toolkit vs Flux

Redux Toolkit and Flux are both popular libraries for managing application state in JavaScript. Below, you will find a comparison of these two libraries.

## Complexity

- **Redux Toolkit**: Redux Toolkit abstracts much of the complexity of working with Redux away. This library provides a more straightforward way to manage state, reducing the amount of boilerplate code.

- **Flux**: Flux, on the other hand, can involve a good deal of complexity. Flux users have to manage dispatchers, actions, and stores manually, which requires more boilerplate code.

## Learning Curve

- **Redux Toolkit**: Redux Toolkit was designed to be the standard way to write Redux logic, and its API is user-friendly. Because of its simplified approach, it has a comparatively smaller learning curve.

- **Flux**: Flux has a more significant learning curve, especially for those new to state management. It requires understanding the Dispatcher system, Stores, and Actions.

## Developer Support and Community

- **Redux Toolkit**: As part of the Redux ecosystem, Redux Toolkit has strong community and developer support. It's also regularly maintained and updated.

- **Flux**: Flux, developed by Facebook, was the precursor to Redux and had robust support. However, with the emergence of Redux and other state management libraries, the Flux community is not as active as before.

<!-- example of our flux system and redux  -->

## Flux Folder Structure

```bash
├── code/client
│   ├── actions
│   │   
│   ├── stores
│   │  


```

## Redux Folder Structure

```bash
├── code/client
│   ├── redux
│   │   ├── features
│   │   │   |── 

```

## Example of a Flux Action

```js title="actions/ExampleActions.js"
import AppDispatcher from '../dispatcher/AppDispatcher';
import ExampleConstants from '../constants/ExampleConstants';

const ExampleActions = {
  exampleAction() {
    AppDispatcher.dispatch({
      actionType: ExampleConstants.EXAMPLE_CONSTANT,
    });
  },
};

export default ExampleActions;
```

## Convert Flux Action to Redux-Toolkit

```js title="redux/features/example/exampleSlice.js"
import { createSlice } from '@reduxjs/toolkit';

export const exampleSlice = createSlice({
  name: 'example',
  initialState: {
    example: false,
  },
  reducers: {
    exampleAction: (state) => {
      state.example = true;
    },
  },
});

export const { exampleAction } = exampleSlice.actions;

export const selectExample = (state) => state.example.example;

export default exampleSlice.reducer;
```


