# Text Formatting

When sending text on behalf of a bot in Snack or Github, some formatting options are available:v

## Styling text

| Style | Syntax | Example | Output |
| --- | --- | --- | --- |
| Bold | **text** | **this is bold text** | This is bold text |
| Italic | _text_ | _This text is italicized_ | This text is italicized |
| Strikethrough | ~text~ | ~This was mistaken text~ | This was mistaken text |

## Quoting text

You can quote text with a `>`

Text that is not a quote

> Text that is a quote
> 

## Quoting code

Use single backtick (`) for simple code expressions:

`This is code`

Use triple backticks for code blocks (```)

```jsx
for (const str in string) {
	...
}
```

## instructions

Use `:instruction[open a PR]` to create an inlined instruction
Use `:instruction[you should open a PR right away]{block=true}` to created a block with the instruction highlighted

![Untitled](Text%20Formatting/Untitled.png)

## Links

You can create an inline link by wrapping link text in brackets `[ ]`, and then wrapping the URL in parentheses `( )`: `[link text](url)`. e.g., `[Wilco Homepage](https://app.wilco.gg/home)`.

## Functions

You can also use a basic JS functions manipulations like `slice` `split` `substring` or `toUpperCase`. You can also have all the [Lodash](https://lodash.com/docs/) utility functions, and you can use it by `Lodash.someX...`