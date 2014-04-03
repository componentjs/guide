
If you're running into issues with Component, the first step you should do is run `component validate`. This will validate your `component.json` files and tell you if there are any major issues with your `component.json`.

The next step is to use the `DEBUG` environmental variable. [Read more about how DEBUG works](https://github.com/visionmedia/debug). For a quick debug statement, run your command prefixed with `DEBUG=component*`. For example, this debugs a `component update` command:

```bash
$ DEBUG=component* component update
  component-resolver remote not set - defaulting to ["github"] +0ms
  component-resolver:locals resolving local at "/Users/jong/Workspace/test" +0ms
  component-resolver resolving "asdf" +11ms
  component-resolver:locals resolving "asdf"'s local dependency "test". +5ms
  component-resolver:locals looking up "asdf"'s local dependency "test" at "/Users/jong/Workspace/test/lib/test". +0ms
  component-resolver remaining dependencies: 0 +1ms
  component-resolver remaining semver: 0 +0ms
  component-resolver:locals resolving local at "/Users/jong/Workspace/test/lib/test" +1ms
  component-resolver resolving "test" +2ms
  component-resolver remaining dependencies: 0 +0ms
  component-resolver remaining semver: 0 +0ms
  component-resolver:locals resolved local "asdf" +1ms
  component-resolver finished resolving locals +1ms
  component-resolver finished resolving dependencies (1) +0ms
  component-resolver finished installing dependencies +0ms
      update : updating asdf's pinned dependencies
      update : updated asdf's ranged dependencies in 743ms
```
