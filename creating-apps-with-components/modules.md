# Modules

The Philosophy of Component is to create small self contained modules that do one thing very well. In the land of Javascript there is no such thing as a module system yet. Because of that, Component has it's own module system based on the [commonjs]() spec. If you have programmed with node before this should sound very familiar. If you haven't, check out this great [Introduction]() where you learn all about it. As of ECMAScript 6, a module system is baked right into the language. Event though commonjs modules are great we want to move forward and support the official module spec. The Browser support for ES6 Modules isn't wide enough to use it in production but Component has a solution to use ES6 modules Today! Let's take a look how we do it:

Let's import a module with ES6:

```js
import store from 'dex';
```

This simply gets rewritten into standard commonjs `require()`s

```js
var store = require('dex');
```

As the ES6 spec finalizes we can remove this additional build step but it'll be a great solution before it lands in all major browser as it will allow users more time to adapt their components to the native module system.

## Compatibility with existing components

### commonjs ► ES6
Components that are based on commonjs can be imported via ES6 modules.

_a.js:_

```js
module.exports = function (a, b) { return a + b }
```

_b.js:_

```js
import add from './a.js'

add(3, 5)
// => 8
```

### ES6 ► commonjs
Components that are based on ES6 modules can be imported via commonjs.

_a.js:_

```js
export default function (a, b) { return a + b }
```

_b.js:_

```js
var add = require('./a.js')

add(3, 5)
// => 8
```

## How to use ES6 modules

### Import...

... a method:

```js
import { set, get } from 'map'

// =>
//   var set = require('map').set
//   var get = require('map').get
```

... a default method:

```js
import foo from 'foo'

// => var foo = require('foo')
```

... all methods:

```js
import * from 'map'

// =>
//   var a = require('map').a
//   var b = require('map').b
// ...
```

... local files:

```js
import local from './local'

// => var local = require('./local')
```

### Export...

... a method:

```js
export function fn () {}

// => exports.fn = function () {}
```

... a default method:

```js
export default function fn () {}

// => module.exports = function fn () {}
```
