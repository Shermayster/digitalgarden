---
{"dg-publish":true,"dg-permalink":"webplatform/extract-values-from-form","permalink":"/webplatform/extract-values-from-form/"}
---

# How to extract values from HTML form
[[2023-01-14\|2023-01-14]]
Working with JS frameworks like React, Vue Svelte, and Angular, we sometimes forget how much the browser's native API can give us.  

Tracking all control inputs with JS frameworks and state management can be useful, but sometimes your app doesn't need that extra complexity. 

I personally prefer to use native browser inputs and APIs as much as possible, and only move to controlled forms when I need more complex validation or custom inputs.

```html
<form onsubmit="onSubmit()">
  <div>
    <label for="username">username</label>
    <input type="text" name="username" id="username" />
  </div>
  <div>
    <label from="password">password</label>
    <input type="password" id="password" />
  </div>
  <button type="submit">submit</button>
</form>
```

```javascript
function onSubmit(e) {
  e.preventDefault()
  const { username, password } = e.target.elements
  const usernameValue = username.value
  const passwordValue = password.value
}
```

We can improve it a bit with destructure

```javascript
function onSubmit(e) {
  e.preventDefault()
  const {
    username: { value: usernameValue },
    password: { value: passwordValue },
  } = e.target.elements
}
```
