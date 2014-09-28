
# Components structure

Try to keep all your components in a single path unless the number of components you use in that single path is unmanageable.

If you do start using multiple paths, you should not use `locals` not within a path above the current path. For example, suppose you have the following structure:

```js
view/
  user/component.json
  page/component.json
model/
  user/component.json
  page/component.json
```

From `view/user`, you should NOT do `require('user')`. You should prefix every component in `model/` with `model-` and do `require('model-user')` or use [Nested Structure](../creating-components/locals.md#Nested Structure).

# Pin dependencies

Dependency updates may break your app. As a safeguard against this, you should pin your dependencies with `component pin`. Then, once in a while, run `component-update` and test your app to make sure it works with the newest versions of dependencies.

## Avoid the file builder in development

Instead, you only need to do `component build styles scripts`.
The reason is that you can simply serve the `build/` folder, `components/` folder, and the root folder in development,
and all the files will automatically be served in your app.
This avoids any unnecessary re-symlinking or re-copying during development,
as well as automatic `mtime` checking done by your file server.

In fact, you can avoid running `component build` at all during development. You might be interested in these two middleware and boilerplates:

Boilerplates:

- https://github.com/component/boilerplate-koa
- https://github.com/component/boilerplate-express

Middleware:

- https://github.com/component/koa.js
- https://github.com/component/middleware.js

## Avoid using files in your app

Instead, move any static files (not included in your `.js` or `.css` files) to separate repositories.
The main reason is that if you serve static assets with your app,
they are not versioned by component.
If instead you move them to a separate repository and add them as dependencies,
they will be versioned by the builder.
