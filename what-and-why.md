
# What is Component?

Component is a full-stack frontend development solution. It is a package manager for both remote and local dependencies as well as a build process. Some people compare it to just `npm`, when really they should be comparing it to `npm + browserify + rework-npm` or `bower + requirejs + grunt/gulp`.

# Why Component?

## No Registry

Component's package manager installs modules from their source, ex. GitHub, instead of a central registry like `npm` or `bower`. Some benefits include:

- No downtime (`npm`)
- No publishing step (`npm`)
- Fast with GitHub's CDN

## First-class images, styles, fonts, files, etc.

Like Bower, Component treats non-JS files as first-class citizens. For Browserify, you would have to do `fs.readFile()` hacks or use non-standard `package.json` properties.

A downside is that Component makes authoring JS-heavy (compared to CSS) apps a little more annoying due to additional `component.json` files.

## Stricter Specifications

Browserify does not handle anything but JS, and there is no standard in `package.json` for non-JS files, making consuming non-JS files a little more complicated.

Bower's specifications are not strict. For example, it could include multiple types of the same file, whereas Component does not allow that. Here's an example with [Facebook's React](https://github.com/facebook/react-bower/issues/1). This makes an integrated and elegant build process virtually impossible with Bower.

## Local Modules

Component supports local modules, i.e. `require('my-local-module')`. Browserify and node.js do not as all non-relative modules must be defined in `node_modules`. This allows you to avoid any `../` calls.

## Namespacing

## Simplified Directory

Traditional apps store their frontend assets like:

```
public/
  js/
  css/
  images/
  fonts/
```

However, this doesn't work too well as now `css` and `js` related to a single component are in entirely separate folders.

Component believes in small components that consist of its own `js`, `css`, etc., very similar to Web Components. Thus, a Component app will have a structure like:

```
client/
  button/
    component.json
    index.css
    index.js
    background.img
```

Now, to find any frontend assets that are related to `buttons`, you only have to look inside `client/buttons/`.

## Local Dependency Tree

## Convert Local Components to Remote

## Easier CSS ordering

When concatening your CSS files, order is important. However, listing the __exact__ order in your build process is a little bit of a pain in the ass.

```css
@import "normalize.css"
@import "reset.css"
@import "type.css"
@import "layout.css"
@import "buttons.css" /* depends on type.css */
@import "asides.css"
@import "aside-buttons.css" /* depends on buttons.css and asides.css*/
```

There are some problems with this traditional approach:

- You must to define each file once and only once.
- It doesn't manage each CSS file's dependencies well.
- It becomes unmanageable with many CSS files.

The solution is to split each file into separate components. Each component will list its local dependencies as `locals`:

`aside-buttons`:

```json
{
  "locals": [
    "buttons",
    "asides"
  ],
  "styles": [
    "index.css"
  ]
}
```

`buttons`:

```json
{
  "locals": [
    "type"
  ],
  "styles": [
    "index.css"
  ]
}
```

Then in your `boot` component, you simply list all the components:

`boot`:

```json
{
  "dependencies": {
    "necolas/normalize.css": "*"
  },
  "locals": [
    "reset.css",
    "type.css",
    "layout.css",
    "aside-buttons.css"
  ]
}
```

Component will now include all the CSS in the correct order, guaranteeing that a component's `dependencies` and `locals` will __always__ be included before the component itself.

Note that the order of `locals` is important for CSS as they are added in the order written.

## No configuration files

With `package.json`, your dependency list will become very large. This does not happen with `component.json`s as you split up your app into local components.

