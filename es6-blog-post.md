ES6(ECMAScript 6 or a.k.a ES2015) is the JavaScript's first update to the language since 2009 and makes compilers like CoffeeScript no longer needed. 

Now that JavaScript is catching up with the rest of the world, taking advantage of its new tricks is not too hard coming from CoffeeScript.

**Babel**

Before jumping into the new syntax wins, it is important to note that as of time this article was written, ES6 is not [supported by all browsers](https://kangax.github.io/compat-table/es6/). To take advantage of the newest features, the Babel plugin will help to transpile ES6 to today's ES5. Check out [the Babel documentation](https://babeljs.io/docs/learn-es2015/) for details on that. 

The contributors have made it clear they want to make all future iterations of JavaScript available today and have a popular portion of the community convinced this is the way to stay up to date with new features in JavaScript going forward.

**let**

CoffeeScript prides itself with the ability to leave off variable assignments, which makes this first feature hard to compare directly to CoffeeScript, but knowing the difference between `let` and `var` can be helpful when converting CoffeeScript to ES6.

The `let` keyword actually works the same as `var` except that it is bound by the [lexical scope](http://whatis.techtarget.com/definition/lexical-scoping-static-scoping), which means you can only access the `let` within the bounds of the closure's it was written in. `var`s however can be hoisted in the global scope unintentionally.

*`let`s are the new `var`s*

```js
// ES6 
let countNumbers = function() {
  for(let num = 0; num < 3; num++) {
    console.log(num);
  }

  console.log("I can see " + num)
}

countNumbers()
//=> 0
//=> 1
//=> 2
//=> 3
//=> num is undefined


// ES5
var countNumbers = function() {
  for(var num = 0; num < 3; num++) {
    console.log(num);
  }

  console.log("I can't see " + num)
}

countNumbers()
//=> 0
//=> 1
//=> 2
//=> 3
//=> I can see 3


// CoffeeScript

countNumbers = ->
  while num = 0 < 3
    console.log num
    num++
  console.log 'I can see ' + num
  return

countNumbers()
//=> 0
//=> 1
//=> 2
//=> 3
//=> I can see 3
```
**example inspired by [this Stack Overflow post](http://stackoverflow.com/questions/762011/let-keyword-vs-var-keyword)*

Keeping the `let`'s scope within the function prevents potential memory leaks and unintended variable assignments.

**Fat arrows `=>`**

The new `=>` is very similar to the `=>` in CoffeeScript and with the addition of some curly braces will work similarly.

```js
// CoffeeScript
addFour = (number) ->  number + 4

//ES6
let addFour = (number) => {
  return number + 4;
}

// more ES6
let addFour = (number) => number + 4

console.log(addFour(6))
//=> 10
```

One key difference with `=>` is that `this` has lexical scope`, which means the surrounding context of the function is inferred on the inside of the `=>` function([more details on that here](https://babeljs.io/docs/learn-es2015/)).

**Modules**

*i.e. import/export*

`export` replaces the old `modules.export` and comes with the key word `default` for function imports without destructuring (see below).

```js
// CoffeeScript

// mathStuff.coffee
module.exports = {
 addFour = (number) ->  number + 4
 addTwo = (number) ->  number + 2
}

// anotherFile.coffee
math = require('./mathStuff')

console.log("#{math.addFour(2)} + #{math.addTwo(2)}")
//=> 6 + 6

// ES6

// mathStuff.js
export let addFour = (number) =>  number + 4
export function addTwo(number) {
  return number + 2
}

// anotherFile.js
import math from './mathStuff';

console.log(addFour(2) + ' + ' + addTwo(4))
//=> 6 + 6 

```

**Destructuring**

Destructuring is another similarity with CoffeeScript. ES6 does give you the ability to destructure modules. I use destructuring all the time now when pulling out methods from libraries.

```js
//ES6 anotherFile.js
import { addTwo } from './mathStuff';

console.log(addFour(2) + ' + ' + addTwo(4))
//=> 6 + 6
```

**Template Strings**

Template strings are great if you are used to string interpolation in CoffeeScript. 

Luckily the ECMAScript 6 team had this in mind.
```js
// anotherFile.js

console.log(`${addFour(2)} + ${addTwo(4)}`)
//=> 6


// anotherFile.coffee

console.log("#{math.addFour(2)} + #{math.addTwo(2)}")
//=> 6 + 6
```
That's the basics, but to find out more general tips on ES6, check out ponyfoo's article on the subject [here](https://ponyfoo.com/articles/es6).

**Why Switch?**

It's apparent that ES6 is not too far off from what you get with CoffeeScript and actually requires the addition of variable assignments, `{}`, `()` and `;`s.

What you currently don't have with CoffeeScript is the weight of the JavaScript community working to improve the language as a whole. 

If you are looking to implement the latest features in the language, ES6 is definitely the direction you want to migrate towards. 
 

