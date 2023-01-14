---
{"dg-publish":true,"dg-permalink":"javascript/ecma-22","permalink":"/javascript/ecma-22/"}
---

# Notes on ECMAScript 2022

## Private class member
Allows to incapsulate class property.

```javascript
class Car {  
  #engine = 1;  
  checkEngine() {  
    return this.#engine;  
  }  
}  
const myCar = new Car(); 
console.log(myCar.checkEngine()) // 1
console.log(myCar.#engine) // undefined
```

## Static class member

```javascript
class Car {  
  engine = 1;  
  static checkEngine() {  
    return this.engine;  
  }  
}  
console.log(Car.checkEngine()); // 1
const myCar = new Car();  
console.log(myCar.checkEngine()) // Error: myCar.checkEngine is not a function
```

## Top-level await 

You can now you await at the top levels without async function.
```javascript
const asyncTask = () => {  
  return new Promise((resolve) => {  
    setTimeout(() => {  
      resolve('done');  
    }, 1000);  
  });  
};  
const state = await asyncTask(); // will wait for 1 second
console.log('asyncTask state:', state); // asyncTask state: done
```

## .at() method
Similar to `array[index]` , but supporting negative values. 
```javascript
const arr = ['a', 'b', 'c', 'd', 'e'];  
console.log(arr.at(1)); // b  
console.log(arr.at(-1)); // e
```

## Object.hashOwn() method
the method is useful to check if an object has an own property non-inherited property.
```javascript
const objPrototype = {  
  protoProp: 'protoProp',  
}  
  
const obj = {  
  __proto__: objPrototype,  
  prop: 'objectProp',  
}  
  
console.log('protoProp' in obj) // true  
console.log(Object.hasOwn(obj, 'protoProp')) // false
```