# Best Practices for Component

## Use wide semver for public components, pin dependencies in your app

You should use wide semver ranges in your public components, specifically the `^` range, to minimize duplicate dependencies in final builds.
However, for your app, you should pin dependencies to make sure updates to dependencies do not break your app.
With Component `1.0.0`, this is easy.
Simply `component pin` all your dependencies,
then once in a while `component update` and test whether your build still works.

There's no need to use `component pin` or `component update` when building a small component.

## Write new components as ES6 modules

Unlike CommonJS or AMD, ES6 module loading is an actual standard.
Begin writing your components as ES6 modules as it will allow your module to be used in more package managers and build systems than just Component and Browserify.

## `require()` specific files with the full extension

Some people like to reach into specific files of modules, for example `require('body-parser/form')`.
Component's build system is manifest-based and does not try to resolve every file passed to `require()`.
It only knows `body-parser`, which is a different component context, but not the files of `body-parser`.
Thus, add the extension to create a full filename like `require('body-parser/form.js')` and your `require` call will now work.

## Publishing to `npm`

If you've chosen a name taken in `npm`'s registry,
publish the component as `<your-username>-<repo>`. 
This allows people to use `require(<user>-<repo>)` in either Component, Browserify, or Node without any hacks.

## Avoid the file builder in development

Instead, you only need to do `component build styles scripts`.
The reason is that you can simply serve the `build/` folder, `components/` folder, and the root folder in development,
and all the files will automatically be served in your app.
This avoids any unnecessary re-symlinking or re-copying during development,
as well as automatic `mtime` checking done by your file server.

## Avoid using files in your app

Instead, move any static files (not included in your `.js` or `.css` files) to separate repositories.
The main reason is that if you serve static assets with your app,
they are not versioned by component.
If instead you move them to a separate repository and add them as dependencies,
they will be versioned by the builder.

## Only use lowercased letters in files and component names

Some file systems are case sensitive, others are not.
Let's keep components as compatible as possible!
