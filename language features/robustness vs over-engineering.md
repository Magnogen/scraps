### Attempting to make things simpler

Alright, hypothetically, you want to check a condition on a number.
Say, you wanted a way to see if it's positive.

The simplest way to do that is with a little check to see if it's greater than 0.
```js
if (x >= 0) console.log('x is positive!')
```
But then, imagine if you wanted to see if it's less than a certain maximum number, say, 100.
```js
if (x >= 0 && x <= 100) console.log('x can be a percentage!')
```
Okay, good.

Now you want to do some error checking, so you think about it and you write the following:
```js
if (!(x >= 0 && x <= 100)) console.error('x needs to be between 0 and 100!')
```
That's quite a lot of characters for one little check.
You could make it smaller, by checking each condition, and use an `||` instead of an `&&`, but that would make things a little less easy to read.

#### Using a function to help

One way to fix those problems is to make a function, similar to P5.js' `random()` function, it'd be used like so:
```js
if ( in_range(x, 0, 100)) console.log('it fits!')
if (!in_range(x, 0, 100)) console.log('it doesnt...')
```
And that certainly helps with readability!
Anyone looking over that could see what it means.

The function would look something like this:
```js
function in_range(x, min, max) {
    return ( x >= min && x <= max ) 
}
```
A single line, but it helps to split things up for readability. 

Now, there are a few edge cases for this function.
Say, a user _only_ wanted to see the number is positive?
They might leave the `max` argument out.
Or, they wanted to see if the number is less than 100, including negative numbers?
Then they'd leave out the `min` argument. 

You can accommodate for that like so:
```js
function in_range(x, min, max) {
    if (min === undefined) return x <= max
    if (max === undefined) return x >= min 
    return ( x >= min && x <= max ) 
} 
```
There. All the edge cases are dealt with.

Actually... We're thinking along the lines of not passing an argument, what if they don't pass _either_ `max` or `min`?
It's a bit of a strange case, but it could happen.

Lets accommodate for that. 
```js
function in_range(x, min, max) {
    if (min === max && min === undefined) return true
    if (min === undefined) return x <= max
    if (max === undefined) return x >= min 
    return ( x >= min && x <= max ) 
} 
```
`x` will always fit into a range where the bounds are at infinity! 

Alrighty. All done! _Actually..._

What if they just call the function without a number to check?

_* sigh *_
```js
function in_range(x, min, max) {
    if (x === undefined) return false
    if (min === max && min === undefined) return true
    if (min === undefined) return x <= max
    if (max === undefined) return x >= min 
    return ( x >= min && x <= max ) 
} 
``` 
It can't fit into a range of numbers if it's not actually a number!

Oh no. That reminds me. 

Type checking.
```js
function in_range(x, min, max) {
    if (!(typeof x   === 'number' &&
          typeof min === 'number' &&
          typeof max === 'number')) return false
    if (min === max && min === undefined) return true
    if (min === undefined) return x <= max
    if (max === undefined) return x >= min 
    return ( x >= min && x <= max ) 
} 
```
Okay, that's good. The function can't check if a `Banana` fits between a `Purple` and a `"three"`, after all.

#### Final thoughts

We started with a problem, so we tried to find a solution.
It worked, but then we had to accommodate for edge cases.

Those darn edge cases. 

Maybe it's better to just use that conditional check from the start.

```
simplicity > robustness
```
