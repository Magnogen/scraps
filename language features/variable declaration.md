### An interesting language feature

#### Original (Destructuring in JavaScript)
```js
let [x, y] = [3, 4]
// x is 3, and y is 4
```
Alright seems good, very helpful.

#### Idea
```js
let x + 1 = 3
// x is 2
let y - x = 2
// y is 4, as x is defined
```
Sure, I mean - why not? 

#### Problems
Consider this
```js
let x*x - 1 = 0
```
Hm...
What would x be? The square root of 1?...
But that is both 1 and -1...

Could it be a list containing both?

In maths, it'd be ±1.
How would that work in programming?
