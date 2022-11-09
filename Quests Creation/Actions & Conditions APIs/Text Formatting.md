# Text Formatting

When sending text on behalf of a bot in Snack or Github, several formatting options are available:

## Styling text

| Style | Syntax | Example | Output |
| --- | --- | --- | --- |
| Bold | `**text**` | **this is bold text** | This is bold text |
| Italic | `_text_` | _This text is italicized_ | This text is italicized |
| Strikethrough | `~text~` | ~This was mistaken text~ | This was mistaken text |

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

## Instructions

Use `:instruction[open a PR]` to create an inline instruction
<img width="758" alt="image" src="https://user-images.githubusercontent.com/42963541/195080979-02e62443-57e2-4f02-bfd9-df1ff12a60ae.png">

Use `:instruction[you should open a PR right away]{block=true}` to create a block with the instruction highlighted
<img width="816" alt="image" src="https://user-images.githubusercontent.com/42963541/195081021-d39539ef-a4c5-43ed-a583-13d962bf517a.png">


## Code Instructions
Use `:codeInstruction[highlighted code instruction]` to create an inline code instruction
<img width="806" alt="image" src="https://user-images.githubusercontent.com/42963541/195080158-4e29f4fe-f067-4851-b514-fe9f5b999a88.png">

Use `:codeInstruction[you should open a PR right away]{block=true}` to create a block with the code instruction highlighted
<img width="818" alt="image" src="https://user-images.githubusercontent.com/42963541/195080302-1654d97c-7329-4dbf-8ae7-7c55b31ffec9.png">


## Links

You can create an inline link by wrapping link text in brackets `[ ]`, and then wrapping the URL in parentheses `( )`: `[link text](url)`. e.g., `[Wilco Homepage](https://app.wilco.gg/home)`.

## Functions

You can also use a basic JS functions manipulations like `slice` `split` `substring` or `toUpperCase`. You can also have all the [Lodash](https://lodash.com/docs/) utility functions, and you can use it by `Lodash.someX...`

## Input
Use `:input[clickable text to display]{text='message to type on click'}` to create an inline clickable text that will type a given message on behalf of the user.
