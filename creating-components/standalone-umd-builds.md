
You may create a standalone build, including all dependencies, using the `component build --standalone <name>` command. This will create a [umd](https://github.com/umdjs/umd)-wrapped version of your build.

Services may automatically build UMD-wrapped standalone builds of components. However, it probably uses the component's `name` property as the global name by default. If you would like to use a custom name, for example, a capitalized name, then set `.standalone` as your preferred global name.

```json
{
  "name": "emitter",
  "standalone": "Emitter"
}
```

Note that this `.standalone` name is not in the `component.json` specification and is only relevant to automated builds. It does nothing when you locally build your components.
