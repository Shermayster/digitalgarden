---
{"dg-publish":true,"permalink":"/rx-js-scan-operator/","tags":"gardenEntry"}
---

How to use scan operator in RxJS and how it's different from reduce operator

#rxjs
# Scan operator is an accumulator

Scan operator accumulates emitted values.
It will emit accumulated result on every value.

Here's an example:

```javascript
from([1, 2, 3])
  .pipe(
    scan((total, current) => {
      return total + current
    }, 0)
  )
  .subscribe(result => {
    console.log(result) // 1,3,6
  })
```

reduce operator will accumulate all values and then will emit a result

```javascript
from([1, 2, 3])
  .pipe(
    reduce((total, current) => {
      return total + current
    }, 0)
  )
  .subscribe(result => {
    console.log(result) // 6
  })
```

Let's see how we can implement it as Array.scan() method

```javascript
/*
 🛑 this implementation is for learning propose. 
 It's not recommended to add methods to Array in production code.
*/
Array.prototype.scan = function scan(cb, initValue) {
  let accumulatedValue = initValue
  let newArray = []
  for (const item of this) {
    accumulatedValue = cb(accumulatedValue, item)
    newArray.push(accumulatedValue)
  }
  return newArray
}
```

Now we can use the method in Array:

```javascript
const arr = [1, 2, 3]
const resultScan = arr.scan((acc, current) => acc + current, 0) //=> [1,3,6]
const resultReduce = arr.reduce((acc, current) => acc + current, 0) //=> 6
```
