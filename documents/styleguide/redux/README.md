# 🧰 Redux
  - [Types](#types)
  - [Action Creators](#action-creators)
  - [Thunks](#thunks)
  - [State](#state)
  - [Reducer](#reducer)

Each reducer should be defined as its own namespace

## Types
* Any type or interface needed for this part of the application
* Don't be afraid of splitting things into different files
* Declaration merge by wrapping entire file in namespace

```typescript
// types/user/rawUser.d.ts

declare namespace User {
  export interface RawUser {
    username: string;
    email: string;
  }
}
```

## Action Creators
* Action creators as well as the `ActionTypes` type should be in this file. All other interfaces or types should be placed in sibling files
  * A `ActionCreators` namespace should be exported containing all the action creators for the reducer
  * `ActionTypes` should be defined outside of the `ActionCreators` namespace
  * `ActionTypes` type will need to be added to `types/redux/actionCreators.ts`

```typescript
// types/user/actionCreators.d.ts

declare namespace User {
  export namespace ActionCreators {
    export interface SetLoggedIn {
      type: 'user/SET_LOGGED_IN';
      status: boolean;
    }

    export interface ReceiveUser {
      type: 'user/RECEIVE_USER';
      user: User.RawUser;
    }
  }

  export type ActionTypes = SetLoggedIn | ReceiveUser;
}
```

* Action creators return a defined type
```typescript
// redux/user/actions/actionCreators.ts

// Good
export const setLoggedIn = (status: boolean): User.SetLoggedIn => ({
  type: 'user/SET_LOGGED_IN',
  status
});

// Bad
export const setLoggedIn = (status: boolean) => ({
  type: 'user/SET_LOGGED_IN',
  status
});
```

* Action creator (`camelCase`) and associated interface (`PascalCase`) should share the same name
```typescript
// redux/user/actions/actionCreators.ts

// Good
export const setUserLogged = (status: boolean): User.SetLoggedIn => ({
  type: 'user/SET_LOGGED_IN',
  status
});

// Bad
export const setUserStatus = (status: boolean): User.SetLoggedIn => ({
  type: 'user/SET_LOGGED_IN',
  status
});
```

* Although this example is typesafe, parameters should be explicitly typed for clarity
```typescript
// redux/user/actions/actionCreators.ts

// Good
export const setLoggedIn = (status: boolean): User.SetLoggedIn => ({
  type: 'user/SET_LOGGED_IN',
  status
});

// Bad
interface SetUserLogged {
  (status: boolean): User.SetLoggedInUser.SetLoggedIn;
}

export const setLoggedIn: SetUserLogged = (status) => ({
  type: 'user/SET_LOGGED_IN',
  status
});
```

## Thunks
Thunks are asynchronous functions that dispatch action creator(s) or synchrous functions that dispatch multiple action creators
* Thunks return `Redux.ThunkResult<T>`
  * This will make `dispatch` and `getState` typesafe
  * The `T` generic is what is returned by the thunk
  * If the thunk is asynchronous, wrap what is returned with `Promise<T>`
```typescript
// redux/user/actions/thunks.ts

// Good
export const getUser = (userId: string): Redux.ThunkResult<Promise<void>> => async (dispatch, getState) => {
  const state = getState();
  const { userId } = state.user;
  const user = await getUserAPI(userId);
  dispatch(receiveUser(user));
};

export const logOut = (userId: string): Redux.ThunkResult<void> => (dispatch) => {
  dispatch(receiveUser(null));
  dispatch(setLoggedIn(false));
};

export const getUserAgain = (): Redux.ThunkResult<Promise<boolean>> => async (dispatch) => {
  let status = true
  try {
    const user = await getUserAPI();
    dispatch(receiveUser(user));
  } catch (error) {
    status = false
  }
  return false
};

// Bad
import { ThunkDispatch } from 'redux-thunk';

export const requestUserPoorly = (userId: string) => async (dispatch: ThunkDispatch, state: () => Redux.State) => {
  const state = getState();
  const { userId } = state.user;
  const user = await getUserAPI(userId);
  dispatch(receiveUser(user));
};

export const requestUserImage = (userId: string) => async (dispatch: ThunkDispatch) => {
  const image = await getUserImageAPI(userId);
  dispatch(receiveUserImage(image)); // Is this an action? It won't be caught with typescript
};
```

## State
* Only one interface, representing the Redux reducer state, should be defined in this file
* The interface name is the same name as the Redux state property
```typescript
// types/redux/user.ts

export interface User {
  status: boolean;
  currentUser: User.RawUser;
}
```

## Reducer
* Helper functions should be defined in sibling files
* `stateCopy` can be passed to helper functions but should be pure functions
* Refer to comments for guidance
```typescript
// redux/user/index.ts

import { cloneDeep } from 'lodash';
import initialState from './initialState';

const reducer = (state: Redux.User = initialState, action: User.ActionTypes) => {
  const stateCopy = cloneDeep(state); // Clone state outside of switch statement
  switch (action.type) { // Ensure that `action.type` is not destructed before case statement to ensure typesafety
    case 'user/SET_LOGGED_IN': { // Block scope each case statement
      stateCopy.status = action.status;
      break; // Break at the end of each case
    }
    case 'user/RECEIVE_USER': {
      stateCopy.currentUser = action.user;
      break;
    }
    default:
      return state; // Default returns default state
  }
  return stateCopy; // Reducer function returns stateCopy
}

export default reducer;
```
