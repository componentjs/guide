## Install Component

First, you need to install `node.js` v0.10+. If you don't have it installed, visit [node's download page](http://nodejs.org/download/).

Once installed, install Component by running the following command:

```bash
$ npm install -g component
```

## Create index.html

Let's quickly create a basic static site. First, create an `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Getting Started with Component</title>
    <link rel="stylesheet" href="build/build.css">
  </head>
  <body>
    <h1>Getting Started with Component</h1>
    <p>Woo!</p>
    <script src="build/build.js"></script>
  </body>
</html>
```

You'll notice that we've linked to `build/build.css` and `build/build.js` files. This is where Component will build files to.

## Create component.json

Let's create the `component.json`. We want to automatically include [normalize.css](https://github.com/necolas/normalize.css), so our `component.json` will look like this:

```json
{
  "name": "getting-started-with-component",
  "dependencies": {
    "necolas/normalize.css": "^3.0.0"
  }
}
```

We use `necolas/normalize.css` because that's where the code is hosted on GitHub. `^3.0.0` means that we want to use any version of `normalize.css` between `3.0.0` and below `4.0.0`.

## Create index.css

Now, let's create a CSS file `index.css`. `box-sizing: border-box;` is the best, so let's reset the entire document style with that rule:

```css
* {
  box-sizing: border-box;
}
```

## Create index.js

Now, let's create a JS file `index.js` that flashes the `Woo!` in the document.

```js
var p = document.querySelector('p');

setInterval(function () {
  p.style.visibility = getComputedStyle(p).visibility === 'hidden'
    ? 'visible'
    : 'hidden';
}, 300);
```

## Add index.js and index.css to component.json

We need to add our files to the `component.json`, so it will end up looking like this:

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

## component build

Now, we run `component build`. You'll see an output like this:

```bash
$ component build
   installed : necolas/normalize.css@3.0.1 in 267ms
       build : resolved in 1221ms
       build : files in 12ms
       build : build/build.js in 76ms - 1kb
       build : build/build.css in 80ms - 7kb
```

All dependencies will be installed automatically.
You'll see `build/build.js` and `build/build.css` files as referenced by `index.html`.

## Open index.html

Run `open index.html`. Now you'll notice that `Woo!` is flashing!

Now view `build/build.css`. You'll notice that `normalize.css` is automatically included in the build, and that `box-sizing: border-box;` is automatically prefixed with `-webkit` and `-moz`.
