Every component, module, and app needs an entry point. In general, this is the `index.js` file or whatever is listed as `main`. However, you'll notice that many examples have `component.json`s that look like this:

```json
{
  "name": "app",
  "locals": ["boot"],
  "paths": ["lib"]
}
```

That is, there's no `.scripts`, and a single `boot` local. What this means is that that the entry point is deferred to `boot`, so the build will automatically `require('boot')` instead of `require('app')`. The main reason for doing so is to avoid having any files at the top of your directory, which makes it cleaner.

It's important to either have an JS file as your entry point or a single local. If there's more than one local, Component doesn't know what to do. Is each `local` an entry point? Are they different bundles? Etc. Having multiple locals is more complex and much more opinionated. Thus, if you have multiple locals, you'll get a build error with `component build`.

If you want multiple bundles or multiple entry points for your app, look into [component-bundler](https://github.com/component/bundler.js) as to how to do so with the JS API.
