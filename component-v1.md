
# Component v1.0.0

Component has finally received the developer love it needed for a long time!
The goals of this release are:

- add semantic versioning support
- fix many issues with component in general
- prune `component(1)` of options and features
- make creating components easier

The next version, `v1.1.0`, will focus on making apps with components easier.

Please note that `component(1)` is designed for building small, public components,
as well as building apps that do not need a custom build process.
If you need to use plugins or process your builds,
you should use the JS API instead.

## What's New

### Semantic Versioning

For a while, Component users were plagued by a lack of semantic versioning support.
But fear no longer! Component now supports semver.
This also means that Component supports multiple versions of a dependency in a single build __and__ app.

Please use `^` semver ranges in your public components.
Since we're dealing with frontend development, we want as few duplicates as possible.
But please, stop using `*`!

### Pinning and Updating

Although semantic versioning is great, you still want to pin your app's dependencies to specific versions.
Otherwise, something might break your app, and hunting the cause might be nontrivial.
So Component has added a few commands to make pinning dependencies and updating them easier.

- `component pin` - pin all your dependencies that users semver ranges to a single version.
- `component outdated` - check whether any of your pinned dependencies are outdated.
- `component update` - update all your pinned dependencies to the latest version.

Note that these commands only update the `component.json` files.
To actually install these new versions,
run `component install` again.

### ~~Registry~~ Crawler

Most package managers have a registry, but we've found that these registries are an extra source of pain.
Instead, Component uses GitHub as a registry!
For a while, we used a [wiki](https://github.com/component/component/wiki/Components) to keep track of components,
but this was a pain in the ass to update and maintain.

Now, we have a dedicated crawler that simply crawls a github user or organization for components!
Instead of a publish step, all you have to do is `component crawl <user>`, and __all__ of your components will essentially be "published".
Users can now search for your component using `component search` or at http://component.io.

### ES6 Module Support

Component v1 now supports ES6 modules by default.
Simply write an ES6 module with node-like module references, and your app should still work.
Note that CommonJS and ES6 modules are not completely compatible, so you may run into compatibility issues.

### Smarter Require()s

Not all the maintainers of the [component](https://github.com/component) organization use Component - many use `npm` and `browserify`.
However, this has been a pain as components are generally named with `npm`'s namespace in mind.

The solution now is to use `require(<user>-<repo>)` in your components, then publish the component to `npm` as `<user>-<repo>`.
No more aliasing hackery will be required on the `browserify` and `node` side.

### Glob Support

Many people complained about having to listen every single file in a `component.json` manually.
Alas, now you can simply do `"js": ["**/*.js"]`!
Keep in mind that this will slow down your build process,
so only use globs when necessary.

## What's Removed

### Custom Remotes

For now, `component(1)` only supports GitHub as a remote.
This is primarily because of semantic versioning support - we have to create an adapter for every remote.
If you need to use a remote other than GitHub,
you should stick to `v0.x` for now.

Feel free to add more [remotes](https://github.com/component/remotes.js)!

### Commands

Some commands have been removed as they were deemed unnecessary.
These commands are:

- `component convert`
- `component wiki`
- `component info`
- `component changes`

### build --use

Support for using plugins from `component(1)` has been removed.
If you need to use a builder plugin,
you should use the JS API instead.

## Other Changes

The `component.json` [specifications](https://github.com/component/spec) have changed over time.
Any relevant changes will be warned to you when using `component(1)` using [component-validator](https://github.com/component/validator.js).

The internals of `component(1)` have also changed drastically.
Be sure to understand the following internal modules if you wish to use the more powerful JS API:

