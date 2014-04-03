
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
