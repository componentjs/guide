
# Installing Component

First, you need to install `node.js` v0.10+. If you don't have it installed,
visit [node's download page](http://nodejs.org/download/).

Once installed, install Component from npm by running the following command:

```bash
$ npm install -g component
```

# Using Component

The following is a quick introduction to Component through building a simple
static site.  It demonstrates the basic use of component for compiling local
javascript and css files and remote css files.

## Create index.html

First, create an `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Getting Started with Component</title>
    <link rel="stylesheet" href="build/build.css">
  </head>
  <body>
    <h1>Getting Started with Component</h1>
    <p class="blink">Woo!</p>
    <script src="build/build.js"></script>
  </body>
</html>
```

You'll notice that we've linked to `build/build.css` and `build/build.js`
files. This is where Component will build files to.

## Create component.json

Let's create the `component.json`. We want to automatically include
[normalize.css](https://github.com/necolas/normalize.css), so our
`component.json` will look like this:

```json
{
  "name": "getting-started-with-component",
  "dependencies": {
    "necolas/normalize.css": "^3.0.0"
  }
}
```

We use `necolas/normalize.css` because that's where the code is hosted
on GitHub.[1][#remotes] `^3.0.0` means that we want to use any version of
`normalize.css` between `3.0.0` and below `4.0.0`.[2][#semver]


## Create index.css

Now, let's create a CSS file `index.css`. Let's reset the box model, to start:

```css
* {
  box-sizing: border-box;
}
```

## Create index.js

Now, let's create a JS file `index.js` that flashes the `Woo!` in the document.

```js
var blink = document.querySelector('.blink');

setInterval(function () {
  blink.style.visibility = getComputedStyle(blink).visibility === 'hidden'
    ? 'visible'
    : 'hidden';
}, 300);
```

## Add index.js and index.css to component.json

We need to add our files to the `component.json`, so it will end up looking 
like this:

```json
{
  "name": "getting-started-with-component",
  "dependencies": {
    "necolas/normalize.css": "^3.0.0"
  },
  "scripts": ["index.js"],
  "styles": ["index.css"]
}
```

## `component build`

Now, we run `component build`. You'll see an output like this:

```bash
$ component build
   installed : necolas/normalize.css@3.0.1 in 267ms
       build : resolved in 1221ms
       build : files in 12ms
       build : build/build.js in 76ms - 1kb
       build : build/build.css in 80ms - 7kb
```

You'll see `build/build.js` and `build/build.css` files as referenced by 
`index.html`.

## Open index.html

Run `open index.html`. Now you'll notice that `Woo!` is flashing: the
site is built.

## Some observations

- When you run `component build`, all dependencies (listed in `component.json`) 
will be installed automatically, as needed, and included in the build. (This
behavior is different from previous versions of component, which split the
install and build steps.)

- In `build/build.css`, you'll notice that `normalize.css` is automatically
included in the build _first_. Component concatenates CSS files in the
following order: remote dependencies first, followed by local dependencies
(i.e. listed in `locals`), followed by css files local to the component
(i.e. listed in `styles`). For more info, see [CSS Ordering][css-ordering].

- Note that `box-sizing: border-box;` is automatically prefixed with `-webkit`
and `-moz`. Component uses autoprefixer by default to generate vendor prefixes.


-----
<a name="remotes"></a>
Component uses GitHub repos by default, but can be configured to use other
_remotes_ via custom adapters. See [component/remotes.js][remotes] for details.

<a name="semver"></a>
Component uses npm's semantic version string parser ([node-semver][semver]).


[css-ordering]: https://github.com/component/guide/blob/master/creating-apps-with-components/css-ordering.md
[remotes]: https://github.com/component/remotes.js
[semver]: https://github.com/isaacs/node-semver
