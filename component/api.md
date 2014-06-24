
These are docs for specific `component(1)` commands.

## build

Builds your component into `.js` and `.css` bundles and installs any necessary dependencies in the process.

You __should__ use the `--watch` option, especially when building components, as it will make subsequent builds very fast as file transformations are cached in memory. When using `--watch`, you can type `r`, `s`, and `c` to `build`, `build scripts`, and `build styles`, respectively.

Livereload users, you could use the `--reload` option, this is simply `--watch` with a livereload server. Don't forget to enable your favorite [livereload browser extension](http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-) or just include the [livereload client script](http://feedback.livereload.com/knowledgebase/articles/86180-how-do-i-add-the-script-tag-manually).

An alternative to the `--watch` option is using [middleware](repositories.md#middleware), more suited for apps.

The `--dev` option does the following:

- Installs and includes development dependencies in the build.
- Use [source URLs](https://developers.google.com/chrome-developer-tools/docs/javascript-debugging) for better debugging in Chrome.
- Create aliases so you can `require()` without worrying about versions.

## crawl

This pings the [crawler](https://github.com/component/crawler.js) to crawl a specific user or organization. Note that executing `component crawl` only adds this specific user/organization to the crawl queue.

You can then search for these components using `component search`.

## duplicates

To minimize the bundle size, this will check for any dependencies that have multiple versions installed, and list which components use each version.

## install

Installs all the components to the `components/` folder. This step is generally unnecessary as the `component build` command already handles it.

## link

This will link a component on your hard drive to the current `components/` folder, treating it as a versioned dependency. There are, however, rules to linking:

- The component cannot be inside the current folder, i.e. the path must start with `..`.
- Do not include `component.json` in the path - link the folder.
- The component must have a `.repository` field, though you can override this field with `--repository`.
- The component must have a `.version` field.

## ls

Show the dependency tree of the current component.

## outdated

Checks for any outdated __pinned__ dependencies. This is more suited for apps.

## pin

Pin any semver-ranged dependencies to the highest, installed version. This is more suited for apps as public components __should__ use semver ranges..

## search

Search [crawled](http://github.com/component/crawler.js) components.

## update

Update any outdated __pinned__ dependencies. This is more suited for apps.

## validate

Checks all your `component.json`s for [specification compliance](https://github.com/component/spec/blob/master/component.json/specifications.md).
