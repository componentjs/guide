
Component(1) is split into many repositories. This makes maintenance much easier as most have their own test suites. All of these libraries are in the [components organization](https://github.com/component) and have a `.js` suffix.

Note that these are only the official libraries.

### The major libraries you may be interested in are:

- [component-remotes](https://github.com/component/remotes.js) - unify remote endpoint APIs
- [component-resolver](https://github.com/component/resolver.js) - resolve the dependency tree with optional installing
- [component-builder](https://github.com/component/builder2.js) - the build system

### Libraries synonymous to Component(1) commands:

- [component-build](https://github.com/component/build.js)
- [component-create](https://github.com/component/create.js)
- [component-ls](https://github.com/component/ls.js)
- [component-outdated](https://github.com/component/outdated.js)
- [component-pin](https://github.com/component/pin.js)
- [component-update](https://github.com/component/update.js)
- [component-validator](https://github.com/component/validator.js)
- [component-watcher](https://github.com/component/watcher.js)

### component dependencies

```
component
├─┬ component-build
│ ├── builder-autoprefixer
│ └─┬ component-builder
│   ├── component-manifest
│   └── component-require2
├── component-consoler
├── component-flatten
├── component-ls
├── component-outdated2
├── component-pin
├─┬ component-resolver
│ ├── component-consoler
│ ├── component-downloader
│ └── component-validator
├── component-search2
├── component-updater
├── component-watcher
└─┬ component-remotes
  └─┬ component-validator
    └── component-consoler
```


### Other JS libraries:

- [component-bundler](https://github.com/component/bundler.js)
- [component-consoler](https://github.com/component/console.js)
- [component-crawler](https://github.com/component/crawler.js)
- [component-downloader](https://github.com/component/downloader.js)
- [component-flatten](https://github.com/component/flatten.js)
- [component-manifest](https://github.com/component/manifest.js)
- [component-require2](https://github.com/component/require2) - Component's `require()` implementation

### Builder Plugins:

- [builder-autoprefixer](https://github.com/component/builder-autoprefixer)
- [builder-coffee-script](https://github.com/component/builder-coffee)
- [builder-es6-module-to-cjs](https://github.com/component/builder-es6-module-to-cjs)
- [builder-html-minifier](https://github.com/component/builder-html-minifier)
- [builder-jade](https://github.com/component/builder-jade)
- [builder-regenerator](https://github.com/component/builder-regenerator)
- [builder-myth](https://github.com/mnmly/builder-myth)

### Middleware, Servers, and Sites:

- [component-koa](https://github.com/component/koa.js) - middleware for [koa](https://github.com/koajs/koa).
- [component-middleware](https://github.com/component/middleware.js) - middleware for node, connect, express, etc.
- [component-builder-www](https://github.com/component/builder.www) - experimental build server for a potential Component CDN.
- [component-cdn](https://github.com/component/cdn) - experimental CDN for Component.
- [component.github.io](https://github.com/component/component.github.io) - http://component.io

### Documentation:

- [guide](https://github.com/component/guide)
- [specifications](https://github.com/component/spec)
