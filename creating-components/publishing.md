
## Pushing Git Tags

Unlike Bower or NPM, Component does not have its own registry.
Instead, you simply `git push` semantically versioned tags.
For example, to publish version `1.0.0` of a component:

```js
git commit -a -m "1.0.0"
git push origin master 1.0.0
```

### Crawling

Instead of publishing, Component has a [crawler](https://github.com/component/crawler.js) that crawls all a GitHub user/organization's repositories.
All crawled repositories will be discoverable through http://component.io as well as `component search`.

However, there are rules to being crawled:

- A `component.json` must exist in the default branch
- The `component.json` must not have `private: true`
- GitHub issues __must__ be enabled
- The repository must not be bare or empty

## Best Practices

### Stick to `master`

In general, you should stick with `master` as your default branch.
By default, Component will check `master` for a `component.json` to check whether the repository is a "component".
Supporting default branches other than `master` would require additional HTTP requests as well as use GitHub API requests.

### Don't prefix `v` to the version

This isn't a big deal, but you should generally not prefix versions with a `v`.
Component will handle both cases, but doing so requires an extra HTTP request.
