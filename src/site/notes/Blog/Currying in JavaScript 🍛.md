---
{"dg-publish":true,"dg-permalink":"fp/currying","permalink":"/fp/currying/"}
---

# Currying in JavaScript 🍛
---
[[2023-01-14\|2023-01-14]]
# Currying in JavaScript 🍛

## What is Currying?

With carrying we can transform function that takes multiple arguments intro **sequence of functions** that takes one argument.
Let's see an example:

```JavaScript
function sum(a,b) {
    return a + b;
}
```

_sum_ function receives two arguments and returns sum of them.
Let's transform it into two sequence functions that take one argument:

```JavaScript
function sum(a) {
    return function(b) {
        return a + b;
    }
}
/* or if you want to use ES6 syntax */
const sum = a => b => a + b;
```

Now we can execute our functions in this way:

```JavaScript
sum(2)(3); // -> 5
```

When we call sum function the first time it will return an **anonymous function**.

```JavaScript
const addFive = sum(5); // addFive is a function!!! 💥
```

It gives us **flexibility** to compose our functions.
We can build helper functions and reuse them in our app.

```JavaScript
const addTwo = sum(2);
const addFive = sum(5);
```

```JavaScript
addTwo(3); // -> 5
addTwo(6); // -> 8
addFive(5); // -> 10
```

I makes our code more declarative
