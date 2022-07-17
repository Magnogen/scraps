### The Sequential Assignment Operator

[[ Jump to the operator ]](#introducing-sequential-assignment)

So we all know how it goes.
You want to implement a fibonacci algorithm in your new language of choice.

It might look something like this: (example in JavaScript)
```js
var result = []
var a = 0
var b = 1
var c = 0
for (var i in Array(100)) {
    result.push(a)
    c = a + b
    a = b
    b = c
}
```

Now that's a lot of lines, isn't it?

What if I told you that everything in the `for` loop could be condensed to _one_ line with my new operator syntax?

But first, a little bit of back story.

#### How it came to be

I've worked on a language called Carbogen recently, and it has a unique method of assignment.
It does it like so:
```js
a = 0
b = 1
a = (b = a) // here's the change!
```
In Carbogen, assignment returns what the variable _used_ to hold, rather than the new value, which is what most languages do.
In the above example, that one line means that `a` and `b`'s values get swapped. 
Neat, right?

> Side note:
> In Carbogen, there's a different syntax for setting multiple variables to the same value, it looks like this:
> ```js
> a = b = c = d = 1
> ```

I was also working on a (now very scrapped, hence why it's here) language called Xatrian.

Xatrian's goal was to be a substitute for the weblangs, but it was to be _majorly_ compressed.
Every program looked like it was minified - yes, I know.
I wanted to make each program as small as possible, and that included a heck of a type casting system, a form of goto statement instead of control flow, and symbols everywhere.
I won't snippet it here, simply because it looks like a terrible jumbled mess of characters and symbols.

So when it came to me wanting to make a fibonacci function, I decided that something from Carbogen could work.

I made a whole new operator for _one_ edge case. Amazing.
So here it is! 

#### Introducing: Sequential Assignment!

I got the idea of the syntax from JavaScript's arrow `=>` function in ES6.
In that case, it's like a value _becomes_ another value through a function, but what about swapping it round so that the first variable takes on the value of the second?

Basically the syntax becomes something like:
```js
a <= b
```
On its own like this, there is literally no difference between just using an `=`.
However, the magic happens when you chain another one onto it:
```js
a <= b <= c
```
Here, `a` gets the value of `b`, and `b` gets the value of `c`!

But something weird happens when you loop back round on yourself:
```js
a <= b <= a
```
What would happen here?
Would `a` and `b` have the same value now?
If so, which one?

Actually, this does the same thing as my Carbogen example earlier - it swaps the two variables' values over.
No need for a temporary variable, easy peasy.

How I imagine it, you can sorta view them as chunks. Sort of like:
_"After this line is done, `a` takes the value of what `b` was, and `b` takes on the old value of `a`."_

Which sorta makes sense. If you _really_ think about it.
(Don't think too hard though, you might break something. My mind is not meant to be understood sometimes.) 

Now all you need to know for the fibonacci example is that `<+=` is the same as `+=`.
It would look something like this with Sequential Assignment Operators:
```js
var result = []
var a = 0
var b = 1
for (var i in Array(100)) {
    result.push(a)
    a <= b <+= a
}
```
There's no need for that `c` variable anymore and, if you really want to, you can fiddle with the array syntax.
Allowing `[1, 2, 3] + 4 == [1, 2, 3, 4]` would produce this:
```js
var result = []
var a = 0
var b = 1
for (var i in Array(100)) {
    result <+= a <= b <+= a
}
```
Tahdah! One line of code.

#### Final thoughts

I just thought I should get this out there.
Maybe it'd be an interesting concept in someone else's language.
Maybe - juuust maybe - it might make it into JavaScript!

Who am I kidding, this doesn't really help with readability, and it's probably very ambiguous too.
I have now idea how to test that kind of thing.

What are your thoughts? How would you improve upon it?
