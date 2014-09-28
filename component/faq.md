
> Please note that this FAQ is a little out of date and was written before 1.0.0.

## Why components?

  Client-side development currently suffers from a lack of structure, more importantly this lack of structure and fundamental sharing of assets makes it difficult to abstract libraries into smaller subsets. Normally you would think twice about separating your library into several parts, because telling end-users to install several pieces is tedious, error-prone, and frankly annoying. Component makes this extremely easy, and we may all benefit from creating smaller lego-blocks for the web.

## What is a component?

  As mentioned in my original [blog post](http://tjholowaychuk.tumblr.com/post/27984551477/components) components are packages containing any combination of assets. For example a component may be javascript and css, fonts and images, only css, or only javascript. Components may also have server portions as well, however for (most) public components this is not recommended, as server components written in different languages are obviously difficult to share among communities. Components are _not_ related to node in any way, however the implementation of the `component(1)` executable that I have created was written with node.

## Why component.json and why not use npm?

  While this is not set in stone, going with component.json instead of package.json removes the ambiguity of which packages may or not actually support "components". package.json has been twisted and changed to suit specific needs of npm as well as other javascript environments, though it could be "fixed" we see the clear separation as a clean break, treating components as first class citizens, not an after-thought.

Due to npm's "global" registry namespace even the name field of component.json and package.json may differ, if your package supports both environments this simply does not work because npm has exhausted many common names, and dependencies are defined in a different manner, thus rendering them incompatible.

 For projects that do happen to support both component and node.js this may appear to be an annoyance, however a very small one. Adding fallback mechanisms to component for package.json support only complicates implementations, documentation, and produces additional unnecessary confusion. Component is designed as a fresh take on how things could be, not what they were.

 Another issue with using npm is that packages are ambiguous between environments. Attempts have been made to allow _any_ npm module to work in the browser, regardless of it being designed as such, making discovery and compatibility more difficult.

  We also utilize many JSON keys that have different meanings in package.json, and others which are not guaranteed to be safe in the long-term.

  Lastly npm conveniences only node users. With the component spec developers may use the component(1) written with node, or implement their own to match the spec. Asking "why not use npm?" is like asking "why not use gem?", or any other package manager. Components are a concept not an implementation.

 The component.json requirements are detailed in the [[Spec]]

## How can I use components on node?

You can have a look at [component-as-module](https://github.com/eldargab/component-as-module).

## Why Github style namespacing?

  Some may view this as a "bad" feature, however it comes with a few nice benefits. The
  first being that you automatically know where docs can be found because you know where
  the repository lives!

  Another benefit is that there is no name squatting, anyone can use whatever name they like.
  For example `component/dialog`, `visionmedia/dialog`, and `tootallnate/dialog` all use the
  name "dialog", however you could use all three as dependencies in various components within
  your application, and still `require('dialog')`.

  This dependency on Github is only implied, but not specifying a _full_ url in component.json
  files you may use a simple [file server](https://github.com/component/server) to either localize
  modifications to components on Github, or to serve private components for your organization.

## Why commonjs instead of AMD?

  Arguably both AMD and build steps are codesmell, however we're aiming to make the development experience a better one by helping to write cleaner modules. How these modules get loaded is purely an implementation detail. With the help of explicit dependencies listed in component.json there's nothing stopping components from being loaded async as needed, or choosing to do a single, or several file build, that choice is yours to make for your application's needs. Many AMD applications compile to single files for production anyway, as 300+ xhrs (at least today) would not be a great idea. AMD vs CJS is mostly just a subjective style debate.

## Why explicitly list all assets in component.json?

  Some expect component(1) to auto-discover scripts via parsing `require()`s, personally I find this an unnecessary hack, for several reasons. The first being that if your component has enough scripts that it's inconvenient to list a few in an array, then that's a sure sign your component is too large. Secondly this adds additional needless complication to implementations of component, and lastly the explicit listing of assets is what makes `component install` so much faster than similar tools, we can download binaries directly in parallel from the remote instead of git clones, or fetching and unpacking tarballs.

## Do I have to manually build all the time?

  No, the `component build` command is one method of performing a build, however you may use a builder within your application (builder.js for example), to re-build on request. The `component build` command is great for development of individual components because it's already available to you and requires no setup. I recommend using a "watcher" (https://github.com/visionmedia/watch) and backgrounding this while you work on a component, then it's as if there was no build step at all, you'll just be able to work on the component's assets freely. For example `$ watch make &`, then `fg` to bring that job back as the foreground job in your shell.

## Can I use component as a build tool for my larger framework?

  Yes! Large frameworks like Angular, Ember, or even smaller ones like Backbone may still benefit from utilizing components. By separating these behemoths into smaller pieces not only does it decrease coupling for the authors, you get all of the development environment benefits that components provide, while still being able to produce a "stand-alone" build for distribution to users via `component build --standalone`. Additionally this allows users who _do_ use component to access your framework through it, as well as all the subcomponents, it's a win-win for both parties.

## Will component work with Rails, Django, [your framework here]?

 Yes! The spec was designed in such a way to maximize simplicity so that
other communities could write similar tool-chains in their own native language. Nothing about component is coupled with node.js, however the current set of "official" tools is written with node. Eventually we may ship binaries to make this even easier.

## How do I use local private dependencies?

  To use private components, add a `"local"` key to `component.json`, for example: `"local": ["foo", "bar"]`. Local dependencies will not be installed from a remote location, but `component(1)` will traverse them and install any dependencies these components may have.

  If you want to use different directories for components, for example `./components` for public components and `./lib` for private components, add a `"paths"` key to your `component.json`, as follows: `"paths": ["components", "lib"]`. `component(1)` will then search both `./components` and `./lib` for components.


## How do I use private Github repositories?
  
  You just need to use authentication via environmental variables or __.netrc__ file.

  Alternatively you may serve private components without Github using any web server that uses the same urls as Github. See Julian Gruber's [contre](https://github.com/godmodelabs/contre) as one example of this with git integration, or the [component/server](https://github.com/component/server) example which serves from components disk.

## How should I structure my application?

  This is a heated debate, with no real answer. The sample [Todo list](https://github.com/component/todo) application has several branches, each implementing a different application structure to demonstrate various ways to approach the task. Some prefer structuring their application linearly by "resource", as in a single flat-listed directory containing all client / server components in one. Others prefer traditional Rails-style MVC directory structure focusing on domain-specific tasks, and splitting associated resource files into directories such as "models", "controllers" and "views". There are pros and cons of each approach, it's your call.

## Can I use components without component(1)?

  Any component can be built to produce a "standalone" version. This build wraps all the dependencies in a function and exposes only a single global variable that you specify, allowing _any_ component to work in _any_ application. To do this simply execute the following in a component directory:

    $ component build --standalone myGlobalVariable

## Where can I find branding documents for component?

  All logos and other assets will be uploaded to [https://github.com/component/component/downloads](https://github.com/component/component/downloads).

## What about "Web Components"?

  The "Web Components" spec is an umbrella term for various client-side technologies that will help developers create reusable code. This includes Shadow DOM, scoped styles, decorators and so on, many of which are very useful features, however do not "solve" other problems such as packaging, component discovery, installation, builds etcetera.

  We view the future of web components to be complimentary to our effort with component(1), our components serve as a solid abstraction that will work seamlessly with or without web components. For example web components require a single `.html` file for the browser to fetch, which we may easily compile with our existing system, without developer modifications, making component(1) a future-proof solution which remains working for legacy systems.

  In short web components themselves won't really affect how component(1) developers build components at all, you'll just have additional browser features available to you for creating custom tags and so on.

## What are the benefits of creating an application out of private components?

  Modern applications are often developed in a non-modular fashion, for example CSS often lives in a directory such as `./styles`, views in `./views`, models in `./models` and so on. While this is certainly not a poor way to develop an application, there are several benefits and gotchas when creating an application solely from well-defined modules.

  If your application shares code between one or more other applications using modules makes it extremely easy to share between the two. If you suddenly decide another application could really use this private module you can simply copy/paste, link, or create a private repo out of what already exists in your codebase. Removing unused code is also another nice benefit since all dependencies, styles, scripts, etc are self-contained within the module you can simply delete the directory. Normally this can be a painstaking process as it's unclear what utilities, styles, images and scripts relate to the module.

  One obvious downside of this technique is the bookkeeping overhead of maintaing dependencies within each module instead of at the application-level.
