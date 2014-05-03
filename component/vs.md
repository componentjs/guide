
Component is one of many frontend solutions. One of the major differences between Component and other solutions is that it is vertically integrated, meaning it does everything from package management to building. Of course, to do so, it is opinionated and is not suitable for every workflow.

## What is the long-term goal of Component?

Component is currently a stopgap for ES6 modules and Web Components.
When all modern browsers start supporting these features,
Component will begin focusing more on semantic versioning and server-side bundling as browsers would be able to handle the rest.

However, we may still use `component.json` as it allows package managers to accurately describe the package and how to consume it without parsing the files of the package.

## When is Component right for me?

Component's philosophy is the UNIX philosophy of the web - to create a platform for small, reusable components that consist of JS, CSS, HTML, images, fonts, etc. With its well-defined specs, using Component means not worrying about most frontend problems such as package management, publishing components to a registry, or creating a custom build process for every single app.

## When is Component wrong for me?

One of the main philosophies with Component is that each component should generally be independent of each other. If they are not independent, then they should only be dependent as a "dependency".

Thus, Component may not be suitable if you use a lot of globals, like jQuery, or use frameworks whose plugins could break other plugins, such as Angular JS.

Since Component is also a package manager, it is not suitable for many frameworks who have their own package management solution, such as [Meteor](http://meteor.com).

Component, by default, only supports CSS and JS, so using CSS preprocessors whose language is not a superset of CSS may cause issues.

## Component vs. npm

Component uses GitHub as a registry and does not have its own. This is in contrast to `npm`, which has its own user namespace and publishing step.

Some benefits include:

- Knowing exactly where code you use is since we use github's `<user>/<repo>` namespace
- No downtime, as GitHub's CDN is generally more reliable than `npm`
- No publishing step except for pushing tags to your repository
- No different username than GitHub usernames
- Flat dependencies, which is more suitable for the browser
- Allow multiple versions of the same dependencies
- Faster installations
- No caching of installations, avoiding any `cache clean` issues
- No "unmet dependency" error messages

## Component vs. Browserify

Component is pretty similar to Browserify. One major difference is that Browserify uses `npm` where as Component does not. However, other differences include:

Browserify resolves dependencies by parsing JS `require()` calls. Component uses `component.json` manifests, which is more verbose. Browserify is easier to use when your app is primarily JS, but Component is easier to use when your app consists of a significant amount of CSS, HTML, images, etc., or if you want to tie JS to its CSS counterparts.

Browserify aims to make `node` modules work in the browser, many of which are unnecessary. On the other hand, Component aims to create modules specifically for the browser. Browserify is better suited for making `node` modules quickly work in the browser.

## Component vs. Bower

Bower is more similar to `npm` than to Component. Like `npm`, Bower's `bower.json` manifest is inclusive except for everything in the relevant `.ignore` file. Component, on the other hand, is exclusive, downloading files only specified in the `component.json`.

However, the major difference between Bower and Component is that `component.json`s are more strict and opinionated: all files listed in the `component.json` are __assumed to be mandatory__. On the other hand, files listed in a `bower.json` are generally optional.

A strict manifest specification allows Component to easily integrate a build process. However, this is impossible with Bower as people publish different types of modules (globals, plugins, AMD, and CommonJS), as well as optional files as shown in this [react-bower issue](https://github.com/reactjs/react-bower/issues/1), making an integrated build process very difficult.

Component's integrated build system allows you to simply include one script and one stylesheet in your page. There's no juggling `<script src="bower_components/jquery"><script>` calls and such.

Like `npm`, `bower` is slower than Component at installing, has an unnecessary publish step, does not support multiple versions of dependencies, and does not cache installations.

## Component vs. RequireJS

Component, by default, uses the CommonJS module system. The major benefit of this is that there are no boilerplate callbacks. However, as of `1.0.0`, Component supports ES6 modules natively.

The major downside is that a build process is required for Component. However, with `1.0.0`, this is not an issue with Component as you can use the `component build --watch` command or rebuild on every request with [middleware](https://github.com/component/middleware.js).

## Component vs Grunt/Gulp/Broccoli/etc.

Since Component is opinionated, there are no special configuration files necessary when creating components and for simple apps. However, once you have a more complex app, you may want to ditch `component(1)` and start using [component-resolve](https://github.com/component/resolver.js) and [component-builder](https://github.com/component/builder2.js) directly.
