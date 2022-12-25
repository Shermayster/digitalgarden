---
{"dg-publish":true,"dg-permalink":"react/thunk-reducer","permalink":"/react/thunk-reducer/"}
---


Thunk is a powerful pattern that allows us to reduce logic inside UI components and integrate external function within React. 

Let's start with regular example. We have react component and we want to fetch data:
```javascript

const fetchMock = () =>
  new Promise(resolve => {
    const data = ["⭐", "✅"]
    setTimeout(() => {
      resolve(data)
    }, 1000)
  })

const appReducer = (state, action) => {
  switch (action.type) {
    case "loading":
      return {
        loading: true,
        data: null,
      }
    case "resolved":
      return {
        loading: false,
        data: action.data,
      }
    default:
      return state
  }
}

const initialState = {
  loading: false,
  data: null,
}


export default function App() {
  const [state, dispatch] = useReducer(appReducer, initialState)
  
  React.useEffect(() => {
	dispatch({type: 'loading'});
	fetchMock()
		.then(res => res.json())
		.then((data) => {
			dispatch({type:"resolved", data})
		})
  }, [])
  
  return (
    <div className="App">
      {state.loading && <div>loading</div>}
      {state.data && (
        <div>
          data:
          {state.data.map(item => (
            <span key={item}>{item}</span>
          ))}
        </div>
      )}
    </div>
  )
}


```

Except for ignoring error handling, there is nothing wrong with the example above. In real life scenarios, components may grow and it can become difficult to understand, especially when UI logic is mixed with business logic. We can use a `thunk reducer` to improve our solution.

Let's create `useThunkReducer`:
```javascript
const useThunkReducer = (reducer, initialState) => {
  const [state, dispatch] = React.useReducer(reducer, initialState)

  const thunkDispatch = React.useCallback(
    action => {
      if (typeof action === "function") {
        action(dispatch)
      } else {
        dispatch(action)
      }
    },
    [dispatch]
  )
  return [state, thunkDispatch]
}
```




```javascript
import React from "react"
import "./styles.css"

const fetchMock = () =>
  new Promise(resolve => {
    const data = ["⭐", "✅"]
    setTimeout(() => {
      resolve(data)
    }, 1000)
  })

const initialState = {
  loading: false,
  data: null,
}

const fetchComponentData = dispatch => {
  dispatch({ type: "loading" })
  fetchMock().then(data => {
    dispatch({ type: "resolved", data })
  })
}

const appReducer = (state, action) => {
  switch (action.type) {
    case "loading":
      return {
        loading: true,
        data: null,
      }
    case "resolved":
      return {
        loading: false,
        data: action.data,
      }
    default:
      return state
  }
}

const useThunkReducer = (reducer, initialState) => {
  const [state, dispatch] = React.useReducer(reducer, initialState)

  const thunkDispatch = React.useCallback(
    action => {
      if (typeof action === "function") {
        action(dispatch)
      } else {
        dispatch(action)
      }
    },
    [dispatch]
  )
  return [state, thunkDispatch]
}

export default function App() {
  const [state, dispatch] = useThunkReducer(appReducer, initialState)
  
  React.useEffect(() => {
    dispatch(fetchComponentData)
  }, [dispatch])
  
  return (
    <div className="App">
      {state.loading && <div>loading</div>}
      {state.data && (
        <div>
          data:
          {state.data.map(item => (
            <span key={item}>{item}</span>
          ))}
        </div>
      )}
    </div>
  )
}
```

Here you can play with an example:

<iframe
  src="https://codesandbox.io/embed/bold-cherry-6hodl?autoresize=1&fontsize=14&hidenavigation=1"
  style="width:90%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="bold-cherry-6hodl"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
  sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>
