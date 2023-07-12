---
sidebar_position: 3
sidebar_label: TireWizard Live Example Part 2
---
# TireWizard Live Example Part 2
<!-- example of our flux system and redux  -->

## Code Folder Structure
  
  ```bash
├── code
│   ├── client
│   │   ├── actions
│   │   │   ├── ApplicationActions.js

```

## Example of Using Redux-Toolkit with Http Requests

```js title="code/client/actions/ApplicationActions.js"
// we are using actions for the ApplicationActions to dispatch the actions to the reducers
 import store from '../store/configureStore';
 import { toggleLoginTextDialog } from './feature/appInfoSlice.js';
// flux actions 
 logOut: function() {
    this.apiGet('/authentication/terminateSecurityToken.php').then(function() {

      var captchaicon = document.getElementsByClassName("grecaptcha-badge");
      if (!isEmpty(captchaicon) && captchaicon[0]) {
        captchaicon[0].className = "grecaptcha-badge";
      }

      this.dispatch(DispatcherActions.LOGOUT_SUCCESSFUL, {});
    }.bind(this));
  },
// using redux-toolkit actions
   logOut: function() {
    this.apiGet('/authentication/terminateSecurityToken.php').then(function() {

      var captchaicon = document.getElementsByClassName("grecaptcha-badge");
      if (!isEmpty(captchaicon) && captchaicon[0]) {
        captchaicon[0].className = "grecaptcha-badge";
      }

      // this.dispatch(DispatcherActions.LOGOUT_SUCCESSFUL, {}); // replace this with redux-toolkit
      store.dispatch(toggleLoginTextDialog(false)); // add this line

    }.bind(this));
  },

  ```

In the context of the code above, you initially had an action for logout functionality which uses the traditional Flux pattern. This action makes a request to the API endpoint '/authentication/terminateSecurityToken.php', then dispatches an action **DispatcherActions.LOGOUT_SUCCESSFUL.**

However, in the updated code, the action **DispatcherActions.LOGOUT_SUCCESSFUL** has been replaced by a Redux Toolkit action, **toggleLoginTextDialog(false).**

Redux Toolkit includes **configureStore** which sets up the Redux store with good defaults. It is imported from **../store/configureStore.**

Then, the Redux Toolkit action is dispatched by calling **store.dispatch()** method which accepts the Redux action.

Here, **toggleLoginTextDialog** is likely a Redux Toolkit action creator function which returns an action with a type and payload. The payload, in this case, is **false**. This action presumably updates the state of a login dialog in the application's Redux store.

## Example of Using Redux in Class Component

```js title="code/client/components/ApplicationRefactor.js"
import {toggleLoginTextDialog} from '../actions/feature/appInfoSlice.js';
// we are using redux in the class component to get the state from the store
  onToggleLoginTextDialog: function () {
    this.props.dispatch(toggleLoginTextDialog(false)); // example of using redux in a class component
    this.dispatch(toggleLoginTextDialog(false)); // example of using redux with mapToStatetoDispatch in a class component
    // below was our original code
    /**
     * if (this.state.loginTextDialogShown) {
     * applicationActions.closeLoginTextDialog();
     * } else {
     * applicationActions.openLoginTextDialog();
     * this.cartItemWasSeen();
     * }
     */
   
  },
/** 
 * @param {object} state
 * When Using Redux in a class component, you can use the mapStateToProps function to get the state from the store
 * @returns {object}
 */
function mapStateToProps(state){
  return {
    loginVisibility:state.info.loginTextDialogOpen,

  }
}
/**
 * @param {function} dispatch
 * When Using Redux in a class component, you can use the mapToStateToDispatch function to dispatch actions to the store
 * @returns {object}
 */

function mapToStateToDispatch(dispatch){
  return {
    dispatch,
    toggleLoginTextDialog: (value) => dispatch(toggleLoginTextDialog(value))
  }
}
export default connect(null)(ApplicationRefactor) // When not using mapStateToProps or mapToStateToDispatch
export default connect(mapStateToProps)(ApplicationRefactor) // when only using mapStateToProps
export default connect(mapStateToProps, mapToStateToDispatch)(ApplicationRefactor) // when using both mapStateToProps and mapToStateToDispatch
export default connect(null, mapToStateToDispatch)(ApplicationRefactor) // when only using mapToStateToDispatch



```

## ApplicationRefactor.js Component

This file, `ApplicationRefactor.js`, is part of the application that uses the Redux library for state management. It imports a Redux action, `toggleLoginTextDialog`, from `appInfoSlice.js`.

### onToggleLoginTextDialog Function

The function `onToggleLoginTextDialog` demonstrates how to dispatch the `toggleLoginTextDialog` action with a payload of `false` within a class component:

1. Using `this.props.dispatch()`, which is typically used when the `connect()` function isn't passed a `mapDispatchToProps` function.
2. Using `this.dispatch()`, which is generally used when the `connect()` function is passed a `mapDispatchToProps` function.

The original code, which is commented out, previously managed the visibility of the login text dialog locally. The new implementation uses Redux.

### mapStateToProps Function

The `mapStateToProps` function retrieves state from the Redux store to use as props in the component. In this case, it returns `loginTextDialogOpen` from the `info` state slice.

### mapToStateToDispatch Function

The `mapToStateToDispatch` function maps Redux actions to the component's props. It accepts the `dispatch` function and returns an object with actions that can be dispatched. Here, it provides the `toggleLoginTextDialog` action.

### connect() Function

The `connect()` function from `react-redux` is used to connect the component to the Redux store:

- `connect(null)(ApplicationRefactor)`: No state or dispatch is mapped to the component's props.
- `connect(mapStateToProps)(ApplicationRefactor)`: Only state is mapped to the component's props.
- `connect(mapStateToProps, mapToStateToDispatch)(ApplicationRefactor)`: Both state and dispatch are mapped to the component's props.
- `connect(null, mapToStateToDispatch)(ApplicationRefactor)`: Only dispatch is mapped to the component's props.

#### Resources

- [Flux](https://facebook.github.io/flux/)
- [Redux Toolkit](https://redux-toolkit.js.org/)
