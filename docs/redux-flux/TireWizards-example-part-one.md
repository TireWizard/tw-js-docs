---
sidebar_position: 2
sidebar_label: TireWizard Live Example Part 1
---
# TireWizard Live Example Part 1
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

## Example of a Flux Action In TireWizards

```js title="code/client/actions/ApplicationActions.js"

  openLoginTextDialog: function(createAccount = false) {
    this.dispatch(DispatcherActions.LOGIN_TEXT_DIALOG_OPEN, createAccount);
  },

export default ExampleActions;
```

In the above example, **openLoginTextDialog** is a Flux action. It takes a **createAccount** argument which has a default value of false. The action creator uses **this.dispatch()** to dispatch an action of type **LOGIN_TEXT_DIALOG_OPEN** with the payload createAccount.

The **dispatch** method sends the action to the Flux store, which will handle the action based on the type.

## Example of a Flux Store In TireWizards

```js title="code/client/stores/ApplicationStore.js"
handlers[DispatcherActions.LOGIN_TEXT_DIALOG_OPEN] = this.onOpenLoginTextDialog;

 onOpenLoginTextDialog: function (createAccount) {
  this.data.loginTextDialogShown = true;
  this.data.loginFailure = false;
  this.data.searchIsActiveFlag = false;
  this.data.loginCreateCustomerAccount = createAccount;
  shoppingCartStore.onShoppingCartClose();
  this.emitChange();
 },

  ```

  In the Flux Store example, **onOpenLoginTextDialog** is a handler function for the **LOGIN_TEXT_DIALOG_OPEN** action. When the action is dispatched, this handler will be invoked with the payload **(createAccount)** from the action. The handler function updates the store's state and invokes **this.emitChange()**, which triggers an update in the components that are listening for changes in the store.

The **handlers** object is a mapping between action types and handler functions. The line **handlers[DispatcherActions.LOGIN_TEXT_DIALOG_OPEN] = this.onOpenLoginTextDialog;** is setting up the handler for the **LOGIN_TEXT_DIALOG_OPEN** action.

## Convert Flux Action to Redux-Toolkit

```js title="redux/features/appInfo/appinfo.js"
import { createSlice } from '@reduxjs/toolkit';

export const appInfoSlice = createSlice({
  name: 'appInfo',
  initialState: {
    loginTextDialogOpen: false,
    createAccount: false,
  },
  reducers: {
    // example one with payload
    openLoginTextDialog: (state, action) => {
      state.loginTextDialogOpen = true;
      state.createAccount = action.payload;
    },
    closeLoginTextDialog: (state) => {
      state.loginTextDialogOpen = false;
    },
    // example two with no payload
    openLoginTextDialog: (state) => {
      state.loginTextDialogOpen = true;
    },
    // example three with no payload toggle 
    toggleLoginTextDialog: (state) => {
      state.loginTextDialogOpen = !state.loginTextDialogOpen;
    },
  },
});

export const { openLoginTextDialog, closeLoginTextDialog } = appInfoSlice.actions; // example one
export const { openLoginTextDialog } = appInfoSlice.actions; // example two
export const { toggleLoginTextDialog } = appInfoSlice.actions; // example three



```

In the Redux-Toolkit example, we use the **createSlice** function, which automatically generates action creators and action types that correspond to the reducers and state.

The **name** option is used as the prefix for the generated action types. The **initialState** option is the initial state for the reducer. The reducers option is an object where the keys will become action type strings, and the functions are the **reducers** that will handle these actions.

In the **reducers** object, we define two reducers: **openLoginTextDialog** and **closeLoginTextDialog**. **openLoginTextDialog** takes the current **state** and an action as arguments. It sets **loginTextDialogOpen** to **true** and **createAccount** to the payload of the action **(action.payload)**. The **closeLoginTextDialog** reducer just sets **loginTextDialogOpen** to **false**.

The **createSlice** function returns an object with the generated action creators as properties. We can use these action creators to dispatch actions to the reducer.

The **appInfoSlice.actions** object contains the generated action creators. We can use these action creators to dispatch actions to the reducer.

## Convert Flux Store to Redux-Toolkit

```js title="code/client/store/configureStore.js"
import {configureStore,combineReducers,getDefaultMiddleware } from "@reduxjs/toolkit";

import loadApplicationInfo from '../redux/features/appInfo';


// below allows for debugging of redux actions
function loggerMiddleware(store) {
    return function(next) {
        return function(action) {
                console.log(action);
            next(action);
        };
    };
}

// Combine multiple reducers into a root reducer
const reducer = combineReducers({
    //reducers will come here
    info:loadApplicationInfo,

  
});

// Configure the Redux store
const store = configureStore({
    reducer,
    middleware:[...getDefaultMiddleware({serializableCheck: false}),loggerMiddleware]
});

export default store;

```

## Explanation:

1. Import Redux Toolkit modules: Modules like configureStore, combineReducers, and getDefaultMiddleware are imported from Redux Toolkit. They help set up the store and combine reducers.

2. Import reducer: The loadApplicationInfo reducer is imported. This reducer handles actions related to application information.

3. Logger middleware: This is a custom middleware for debugging, which logs every action that gets dispatched.

4. Combine reducers: Here, all the reducer functions are combined into a root reducer using combineReducers. In this example, we have only one reducer (loadApplicationInfo) assigned to the key info.

5. Configure the store: The configureStore function is used to configure the Redux store. The root reducer and middleware are set here. getDefaultMiddleware adds default Redux middleware (with serializable check disabled), and our custom loggerMiddleware is also included.

6. Export the store: Finally, the configured store is exported for use in the application.

Note: **This setup allows you to manage application state using Redux, with middleware for additional functionalities. You can add more reducers as your application grows, by including them in the combineReducers function.**

### Tips for translating Flux to Redux

1. Reducers in Redux vs Handlers in Flux: In Flux, each store has its handler functions, but in Redux, there is a single reducer function for the entire app, composed of smaller reducer functions for each part of the state.

2. Actions in Redux vs Dispatchers in Flux: In Flux, actions are sent to all stores, but in Redux, actions are sent through the reducer.

3. Immutable State in Redux: In Redux, state is considered to be immutable. Instead of modifying the state directly, you return a new state from the reducer.

4. Use Redux-Toolkit: Redux Toolkit is designed to simplify the process of setting up and using Redux. It helps to minimize boilerplate code and provides a set of APIs that enhance Redux with power-ups like automatic action creators and reducers generation.

5. Single Source of Truth: In Redux, the state of your whole application is stored in an object tree within a single store, unlike in Flux where you can have multiple stores. This helps you maintain a consistent state across your entire application.

6. Handling Side Effects: Flux does not have a built-in mechanism for handling side effects like asynchronous API calls. With Redux, you can use middlewares like redux-thunk or redux-saga to manage side effects.

## Resources

- [Flux](https://facebook.github.io/flux/)
- [Redux Toolkit](https://redux-toolkit.js.org/)
