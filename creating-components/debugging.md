# Debugging

If you run `component build --dev` your build output become almost commented out and at the end you see a line which looks like so:

```
//# sourceURL=file.js"
```

Actually this works in Chrome without problems, but Firefox doesn't support it and Safari show you the reference files but the breakpoints don't work.

# Aliases

Furthermore you have aliases for the registered modules with the `--dev` option. With the aliases you can open the browser console and require aliases instead of the full module name.

If a local components name is unique in your app, you can just require the name. Otherwise you need to use a canonical path, relative to the root component, starting with `./`, for instance you have defined to paths in your root component: `['view', 'model']` and in each of them a `user` component. Then you need to `require('./view/user')`.

If you want to require another file than defined in the `.main` field of your component, you also need a canonical path.

Ditto for remote componets, for instance you can `require('emitter')` if you have only one component with the name. If there is a name clash, you can type `require('component~emitter')`, joining username and repository with `~`. The canonical paths contains the version as well, like: `component~emitter@1.0.0`