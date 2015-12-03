ES6(ECMAScript 6 or a.k.a ES2015) is the JavaScript's first update to the language since 2009 and makes compilers like CoffeeScript no longer needed. 

Now that JavaScript is catching up with the rest of the world, taking advantage of it's new tricks is not too hard coming from CoffeeScript.

**Babel**

Before jumping into the new syntax wins, it is important to note that ES6 [supported by all browsers](https://kangax.github.io/compat-table/es6/). To take advantage of the newest features, the Babel plugin will help to transpile ES6 to today's ES5. Check out [their documentation](https://babeljs.io/docs/learn-es2015/) for details on that. 

The contributors have made it clear they want to make all future iterations of JavaScript available today and have a popular portion of the JS community convinced this is the way to stay up to date with new features in JavaScript going forward.

**let**

CoffeeScript prides itself with the ability to leave off variable assignments, which makes this first feature hard to compare directly to CoffeeScript, but knowing the difference between `let` and `var` will help out with the consideration of an ES6 conversion.

The `let` keyword actually works the same as `var` except that it is functionally scopes, which means you can access the `let` within the bounds of the closure it was written in. `var`'s however can be hoisted in the global scope unintentionally.

*`let`'s are the new `var`'s*

```
// ES6 
let number = 2;

let math = function(number) {
  let number_four = 4;
  console.log(number + number_four);
}

console.log(number + number_four);
//=> 6
//=> number_four is undefined

// ES5
var number = 2;

var math = function(number) {
  var number_four = 4;
  console.log(number + number_four);
}

console.log(number + number_four);
// 6

// CoffeeScript
number = 2

math = (number) ->
  number_four = 4
  console.log number + number_four

console.log number + number_four
//=> number_four is not defined
```

Keeping the `let`'s scope within the function prevents potential memory leaks and unintended variable assignments.

**Fat arrows `=>`**

The new `=>` is very similar to the `->` in CoffeeScript and with the addition of some curly braces will work similar.

```
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

One key difference with `=>` is the lexical scope of `this`, which means the surrounding context of the function is inferred on the inside of the `=>` function([more details on that here](https://babeljs.io/docs/learn-es2015/)).

**Modules**

*i.e. import/export*

`export` replaces the old `modules.export` and comes with the key word `default` for function imports without destructuring (see below).

```
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

Destructuring is another carry over from similarity from CoffeeScript. ES6 does give you the ability to destructure modules. I use destructuring all the time now when pulling out methods from libraries.

```
//ES6 anotherFile.js
import { addTwo } from './mathStuff';

console.log(addFour(2) + ' + ' + addTwo(4))
//=> 6 + 6
```

**Template Strings**

Template strings are great if you are used to string interpolation in CoffeeScript. 

Luckily the ECMAScript 6 team had this in mind.
```
// anotherFile.js

console.log(`${addFour(2)} + ${addTwo(4)}`)
//=> 6


// anotherFile.coffee

console.log("#{math.addFour(2)} + #{math.addTwo(2)}")
//=> 6 + 6
```
That is the basics, but to find out more general tips on ES6 in ponyfoo's article on the subject [here](https://ponyfoo.com/articles/es6).

**Why Switch?**

It's apparent that ES6 is not too far off from what you get with CoffeeScript and actually requires the additional of variable assignments, `{}`, `()` and `;`'s.

What you currently don't have with CoffeeScript is the weight of the JavaScript community working to improve the language as a whole. 

If you are looking to implement the latest feature in the language, ES6 is definitely the direction you want to migrate towards. 
 

