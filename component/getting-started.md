
# Getting Started: The Basics

## Installing Component

First, you need to install `node.js` v0.10+. If you don't have it installed,
visit [node's download page](http://nodejs.org/download/).

Once installed, install Component from npm by running the following command:

```bash
$ npm install -g component
```

## Using Component

The following is a quick introduction to Component through building a simple
static site.  It demonstrates the basic use of component for compiling local
javascript and css files and remote css files.

### Create index.html

First, create an empty directory, for intance __my-first-component__ as our 
project root.
Then create this file __index.html__ in our project root:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Getting Started with Component</title>
    <link rel="stylesheet" href="build/build.css">
  </head>
  <body>
    <h1>My First Component</h1>
    <p class="blink">Woo!</p>
    <script src="build/build.js"></script>
  </body>
</html>
```

You'll notice that we've linked to __build/build.css__ and __build/build.js__
files. This is where Component will build files to in the default case.

### Create component.json

Let's create the __component.json__ and set the _name_ property.

```json
{
  "name": "my-first-component"
}
```

### Install a remote dependency

We want to include
[normalize.css](https://github.com/necolas/normalize.css), so let's install 
this remote dependency via the command: 
`component install necolas/normalize.css`. If you check the __component.json__ 
file, you'll notice that component add the dependency automatically. You can also do it the other way: add a dependency, then run `component install`.

You should see this output on your stdout:
```bash
github remote: 54 of 60 requests remaining, resetting at Thu Oct 30 2014 00:23:36 GMT+0100 (CET)
github remote: see https://github.com/component/guide/blob/master/changelogs/1.0.0.md#required-authentication for more information.
   installed : necolas/normalize.css@3.0.2 in 283ms
     install : complete
```

We use `necolas/normalize.css` because that's where the code is hosted
on GitHub.[[1]](#remotes) If you don't specify any version via the command,
component will install the latest version, which is __3.0.2__ in this case. 
__^3.0.2__ means that we want to use any version of
__normalize.css__ between __3.0.2__ and below __4.0.0__.[[2]](#semver)


### Create index.css

Now, let's create a CSS file __index.css__. Let's reset the box model
, to start:

```css
* {
  box-sizing: border-box;
}
```

### Create index.js

Now, let's create a JS file __index.js__ that flashes the `Woo!` every 300 
milliseconds in the HTML document.

```js
var blink = document.querySelector('.blink');

setInterval(function () {
  blink.style.visibility = getComputedStyle(blink).visibility === 'hidden'
    ? 'visible'
    : 'hidden';
}, 300);
```

### Add index.js and index.css to component.json

We need to add our files to the __component.json__, so it will end up looking 
like this:

```json
{
  "name": "my-first-component",
  "dependencies": {
    "necolas/normalize.css": "^3.0.2"
  },
  "scripts": ["index.js"],
  "styles": ["index.css"]
}
```

### `component build`

Now, we run `component build`. You'll see an output like this:

```bash
$ component build
       build : resolved in 26ms
       build : files in 126ms
       build : build/build.js in 135ms - 4kb
       build : build/build.css in 130ms - 7kb
```

You'll see __build/build.js__ and __build/build.css__ files as referenced by 
__index.html__.

### Open index.html

Run `open index.html` to open the the file in your browser. Now you'll notice 
that `Woo!` is flashing: the site is built.

## Some observations

- When you run `component build`, all dependencies (listed in __component.json__) 
will be installed automatically, as needed, and included in the build. (This
behavior is different from previous versions of component, which split the
install and build steps.)

- In __build/build.css__, you'll notice that __normalize.css__ is automatically
included in the build _first_. Component concatenates CSS files in the
following order: remote dependencies first, followed by local dependencies
(i.e. listed in __locals__), followed by css files local to the component
(i.e. listed in __styles__). For more info, see [CSS Ordering][css-ordering].

- The __index.js__ will be loaded (required) automatically, so the text starts
flashing immediately when you open the browser.

- Note that `box-sizing: border-box;` is automatically prefixed with `-webkit`
and `-moz`. Component uses the great [autoprefixer](https://github.com/postcss/autoprefixer) by default to generate vendor prefixes.

## Setup Authentication
You might noticed that Component prints a message if you run 
`component install`. It looks like this:
```bash
github remote: 54 of 60 requests remaining, resetting at Thu Oct 30 2014 00:23:36 GMT+0100 (CET)
github remote: see https://github.com/component/guide/blob/master/changelogs/1.0.0.md#required-authentication for more information.
```
GitHub provides 60 request per hour for an unauthenticated access. If you
you need more, you need to use authentication. See [changelog](https://github.com/componentjs/guide/blob/master/changelogs/1.0.0.md#required-authentication) for more information.

### Configuring GitHub access

Component 1.0.0 is using GitHub API to access GitHub repos, one simple way to configure your account is by adding global environment variable to your profile (eg: `.bashrc` r `.zshrc`) like this:

```bash
export GITHUB_USERNAME=<username>
export GITHUB_PASSWORD=<password>
```

One other secure way is by using GitHub oauth token instead of your password:

```bash
export GITHUB_USERNAME=<token>
export GITHUB_PASSWORD=x-oauth-basic
```

You can also use a __.netrc__ file, add the following lines to your `.netrc`](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html)

```bash
machine api.github.com
  login <token>
  password x-oauth-basic
  
machine raw.githubusercontent.com
  login <token>
  password x-oauth-basic
```

`<token>` is generated in the page <https://github.com/settings/applications#personalaccess-tokens>, you can validate it via command:


### Configuring bitbucket access

Component 1.0.0+ supports Bitbucket as a remote as well. The simplest way to support Bitbucket is to add globals to your profile (eg. `.bashrc` or `.zshrc`) like so:

```bash
export BITBUCKET_USERNAME=<username>
export BITBUCKET_PASSWORD=<password>
```

Additionally, you can add Bitbucket credentials directly to your [`.netrc`](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html) file like o:

```bash
machine api.bitbucket.org
  login <username>
  password <password>
```

Currently, Bitbucket does not support generating a personal OAuth access token. The [current documentation on OAuth with BitBucket](https://confluence.atlassian.com/isplay/BITBUCKET/OAuth+on+Bitbucket) only works with app authorization.

## Next steps

If you want to learn different features of component step by
step, you can try out the browse the [c8-experiments repo](https://github.com/timaschew/c8-experiments).

There are also more [examples](https://github.com/componentjs/guide/blob/master/component/examples.md).

-----
**Notes:**

<a name="remotes"></a>
[1] Component uses GitHub repos by default, but can be configured to use other
_remotes_ via custom adapters. See [component/remotes.js][remotes] for details.

<a name="semver"></a>
[2] Component uses npm's semantic version string parser ([node-semver][semver]).


[css-ordering]: https://github.com/componentjs/guide/blob/master/creating-apps-with-components/css-ordering.md
[remotes]: https://github.com/componentjs/remotes.js
[semver]: https://github.com/npm/node-semver
