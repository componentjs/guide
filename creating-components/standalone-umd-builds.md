
You may create a standalone build, including all dependencies, using the `component build --standalone <name>` command. This will create a [umd](https://github.com/umdjs/umd)-wrapped version of your build.

Services may automatically build UMD-wrapped standalone builds of components. However, it probably uses the component's `name` property as the global name by default. If you would like to use a custom name, for example, a capitalized name, then set `.standalone` as your preferred global name.

```json
{
  "name": "emitter",
  "standalone": "Emitter"
}
```

Note that this `.standalone` property is not in the `component.json` specification and is only relevant to automated builds. It does nothing with your local components.


Evaluation priority: 

1. CLI parameter passed after `--standalone` or `--umd`
2. `.standalone` property in the root component
3. `.name` property in the root component
