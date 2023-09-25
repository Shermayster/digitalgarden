---
{"dg-publish":true,"dg-permalink":"learning/redux","permalink":"/learning/redux/"}
---

# Redux
#React 
# **Fundamentals of Redux**

Principles:
1. Describe state of your application as single javascript object
2. **State tree should be readonly**. When you need to update state tree, user action. Only requirement for action is to have `type` property. You free to use any structure to action. 
3. **State mutation should be described with pure function.** State mutation should be with previous state, actions and should return new state. This function is called the reducer

Basic Redux implementation

```javascript
const createStore = (reducer) => {
    let state;
    let listeners = [];
    
    const getState = () => state;
    
    const dispatch = (action) => {
        state = reducer(state, action);
        listeners.forEach(listener => listeners());
    }
    
    const subscribe = (listener) => {
        listeners.push(listener);
        return () => {
            listeners = listeners.filter(l => l !== listener);
        };
    };
    
    dispatch({});
    
    return { getState, dispatch, subscribe };
}

```

You can make composition with many reducers. You can call one reducer from another reducer

---

# **React Redux**

course link: [https://frontendmasters.com/courses/redux\-fundamentals](https://frontendmasters.com/courses/redux-fundamentals)

material: [https://stevekinney.github.io/redux\-fundamentals/](https://stevekinney.github.io/redux-fundamentals/)

Redux has much more functionality than useReducer

![image](/img/user/Notes/1.Projects/React Lectures/Redux_attachments/Pasted image 20230114172906.png)
**Redux API**
- applyMiddleware
- bindActionCreators
- combineReducers
- compose
- createStore

**Compose**

It's just a helper function. compose takes a series of functions as arguments and returns a new function that applies each those functions from right\-to\-left.

```javascript
const makeLouder = (string) => string.toUpperCase();
const repeatThreeTimes = (string) => string.repeat(3);
const embolden = (string) => string.bold();

//compose
const makeLouderAndBoldAndRepeatThreeTimes = redux.compose(
  embolden,
  repeatThreeTimes,
  makeLouder
);

```

**createStore**
creates a store for Redux. 

```javascript
type ApplicationState = {};
type Action = { type: string; [key: string]: any };

type Reducer = (state: ApplicationState, action: Action) => ApplicationState;

// we need to provide a reducer to redux store
const initialState = { value: 0 };

const INCREMENT = "INCREMENT";
const ADD = "ADD";

// 💥 Why creating a function is powerful? 
// You can change implementation in the future in place.
const increment = () => ({ type: INCREMENT });
const add = (number) => ({ type: ADD, payload: number });

const reducer = (state = initialState, action) => {
  if (action.type === INCREMENT) {
    return { value: state.value + 1 };
  }

  if (action.type === ADD) {
    return { value: state.value + action.payload };
  }

  return state;
};

const store = redux.createStore(reducer);
```

```javascript
const increment = () => ({ type: INCREMENT });
const add = (number) => ({ type: ADD, payload: number });
```

**Some Rules for Reducers**
- No mutating objects. If you touch it, your replace it.
- You have to return something and ideally, it should be the unchanged state if there is nothing you need to do it.
- It's just a JavaScript function

**Redux Store API**

- `dispatch`
- `subscribe`
- `getState`
- `replaceReducer`


So, **how do we get actions into that reducer to modify the state?** we dispatch them.

```javascript
store.dispatch(action);
```

```javascript
const store = createStore(reducer);

console.log(store.getState()); // { value: 0 }
store.dispatch(increment());
console.log(store.getState()); // { value: 1 }
```

```javascript
const subscriber = () => console.log('Subscriber!' store.getState().value);

const unsubscribe = store.subscribe(subscriber);

store.dispatch(increment()); // "Subscriber! 1"
store.dispatch(add(4)); // "Subscriber! 5"

unsubscribe();

store.dispatch(add(1000)); // (Silence)
```

**Enhancers** 
An enhancer is a function that **allows you to add functionality** to Redux that it doesn't come with out of the box. We'll see this when we want to hook it up to the developer tools or when we want add some the ability to do asynchronous tasks \(e.g. make a server\-side HTTP requests\).

 A function that doing side effects and running actual action. **Example of enhancer: Redux DevTools**

Example of implementation:

```javascript
const monitorReducerEnhancer = (createStore) => (
  reducer,
  initialState,
  enhancer
) => {
  const monitoredReducer = (state, action) => {
    const start = performance.now();
    const newState = reducer(state, action);
    const end = performance.now();
    const diff = round(end - start);

    console.log("Reducer process time:", diff);

    return newState;
  };

  return createStore(monitoredReducer, initialState, enhancer);
};
```

applyMiddleware is a way to produce an enhancer out of chain of middleware.

```javascript
const enhancer = applyMiddleware(
 firstMiddleware,
 secondMiddleware,
 thirdMiddleware
);
```

Middleware have the following API:

```javascript
const someMiddleware = (store) => (next) => (action) => {
 // Do stuff before the action reaches the reducer or the next piece of middleware.
 next(action);
 // Do stuff after the action has worked through the reducer.
};
```

`next` is either the next piece of middleware or it's store.dispatch. **If you don't call next, you will swallow the action and it will never hit the reducer.**

Here is a quick example:

```javascript
const logMiddleware = (store) => (next) => (action) => {
 console.log("Before", store.getState(), { action });
 next(action);
 console.log("After", store.getState(), { action });
};

const store = createStore(reducer, applyMiddleware(logMiddleware));
```

Our examples are intentionally contrived, but if you wanted to you could use both our enhancer and our middleware. But, if createStoreonly takes one enhancer—then how?

```javascript
const middlewares = applyMiddleware(logMiddleware);
const enhancer = compose(middleware, logEnhancer);
```

## **Redux With React**

The first—and arguably most important part—is a component called Provider. This is a component that takes the store and threads it through your React application using the [Context API](https://reactjs.org/docs/context.html).

### Binding Actions

At a simple version of this might look as follows:

```javascript
const actions = bindActionCreators({ increment, decrement, set }, dispatch);
```

And now we could put them into the component.

```html
<button onClick={() => actions.increment()}>Increment</button>
<button onClick={() => actions.set(0)}>Reset</button>
<button onClick={() => actions.decrement()}>Decrement</button>
```

You could even create a hook if you wanted to do this on the regular.

In a new file called set\-actions.js:

```javascript
import { bindActionCreators } from "redux";
import { useDispatch } from "react-redux";
import { useMemo } from "react";

export function useActions(actions) {
 const dispatch = useDispatch();
 return useMemo(() => {
   return bindActionCreators(actions, dispatch);
 }, [actions, dispatch]);
}
```

And now we can use this whenever.

```javascript
const actions = useActions({ increment, decrement, set });
```


## **Hooks vs HOC**


Hooks are:

-  Pros:
    - simpler to work with. 
    - less code
- Cons:
    - the code more coupled and require to bring redux store to test the component

HOC:
- Pros:
    - easy to test
    - storybook integration
    - Better performance. Memorisations and caching is done automatically
- Cons:
    - a bit overkill

## Advanced Redux
Links:
- [https://github.com/stevekinney/supertasker](https://github.com/stevekinney/supertasker)
- [https://github.com/stevekinney/Frontend-Masters-November-2022/tree/main/Advanced%20Redux](https://github.com/stevekinney/Frontend-Masters-November-2022/tree/main/Advanced%20Redux)

### Why to use RTK
It reduce required boilerplate and gives opinionated way to work with Redux.  

### Redux Saga
Redux middleware based on [[Notes/Blog/Saga Pattern\|Saga Pattern]]






