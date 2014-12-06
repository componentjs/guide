# Intro

Your application is usually structured into multiple components.  
You have either remote or local components. Local components can be listed in each __component.json__ like so:

```js
"locals": ["qux", "baz"]
```

__Note:__ All components need to be lower case! Component will lowercase all you `require()` calls due to keep compatibility between case sensitive and case insensitive file systems. 

# Nested Structure
Your root component defines a `.paths` array where component try to lookup your local components. So your components don't need to know where other local components exist.

Local components don't need a `.name` field, they just use its folder name. You can also provide a subdirectories as a local component to use kind of namespacing:

```js
"locals": ["foo/bar", "/qux/bar"]
```

Another way to structure your component is to use multiple `.paths` values in your root component. See [Components Structure](../creating-apps-with-components/best-practices.md#Components structure).

# Require Locals

Local components can be required with its name like `require('qux')`.
The result is the exported module of the main file, which you define in your component.json as `.main`.

You can also require the other scripts of a foreign component just by writing: `require('qux/script')`. See also [Aliases](debugging.md#Aliases).

[component specifications](https://github.com/componentjs/spec/blob/master/component.json/specifications.md#locals)
