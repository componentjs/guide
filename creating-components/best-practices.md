
To do: merge https://github.com/component/component/wiki/Building-better-components

## Use wide semver ranges

It's more important in the browser than the server to make sure you don't have duplicate components. You don't want to have multiple versions of a component in your final build as that is unnecessary bloat.

To safeguard against this, use wide semver ranges in your public components, and let apps pin dependencies themselves. Use `^` for dependencies `> 1.0.0`, and `~` otherwise.

## Write new components as ES6 modules

Unlike CommonJS or AMD, ES6 module loading is an actual standard.
Begin writing your components as ES6 modules as it will allow your module to be used in more package managers and build systems than just Component and Browserify.

## Publishing to `npm`

If you've chosen a name taken in `npm`'s registry,
publish the component as `<your-username>-<repo>`.
This allows people to use `require(<user>-<repo>)` in either Component, Browserify, or Node without any hacks.

## Only use lowercased letters in files and component names

Some file systems are case sensitive, others are not.
Let's keep components as compatible as possible!

## Don't use vendor prefixes in component CSS

It's hard to correctly add all the required vendor prefixes, and it makes CSS difficult to read and maintain.
Component build includes [autoprefixer] which handles vendor prefixes automatically. Applications can use other solutions to post-process CSS.

## Assume that ES5 is supported

Use `Object.keys` and `Function.bind` and `Array.map` etc. Do not add fixes or take patches for IE8
compatibility, if the problems in question can be resolved by conditionally including your favorite [ES5 shim].

ES5 shim is available as component, but it's probably even better to use infamous IE <= 8 conditional comments to include it.


[autoprefixer]: https://github.com/ai/autoprefixer
[ES5 shim]: https://github.com/es-shims/es5-shim
