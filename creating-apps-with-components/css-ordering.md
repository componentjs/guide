
Traditionally, you would manually list all your `CSS` files into a concatenation step like so:

```css
@import "normalize.css"
@import "reset.css"
@import "type.css"
@import "layout.css"
@import "buttons.css" /* depends on type.css */
@import "asides.css"
@import "aside-buttons.css" /* depends on buttons.css and asides.css*/
```

However, this is unmanageable with a lot of CSS files as you are prone to ordering mistakes and duplicates. It is also difficult to understand which CSS files are dependent on other CSS files, as demonstrated by the comments.

Thus, with Component, you can split each CSS file into its own separate component, perhaps with relevant JS files, like this:

`aside-buttons`:

```json
{
  "locals": [
    "buttons",
    "asides"
  ],
  "scripts": ["*.js"],
  "styles": ["*.css"]
}
```

`locals` means local dependencies. By listing `buttons` and `asides` as local dependencies, Component will guarantee that `buttons` and `asides` are placed before `aside-buttons` in the CSS build.

Then in your `boot` component, you simply list all the components, placing dependencies you __need__ at the top first:

```json
{
  "dependencies": {
    "necolas/normalize.css": "*"
  },
  "locals": [
    "reset",
    "type",
    "layout",
    "buttons",
    "asides",
    "aside-buttons"
  ]
}
```

Component will now handle the CSS ordering itself, so you don't have to worry about whether CSS files are included twice or are in the wrong or right order. The only downside to this is that it is a little verbose.
