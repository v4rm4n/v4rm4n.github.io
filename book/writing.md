# Writing Pages

Gleebook renders CommonMark with the GitHub extensions, so anything you would
write in a README works here.

## Text formatting

You can write **bold**, *italic*, ~~strikethrough~~ and `inline code`. Links to
other chapters use the `.md` filename, like [the welcome page](index.md), and
are rewritten to `.html` at build time. Footnotes work too.[^1]

## Lists

1. Ordered lists
2. keep their numbers
   - and nest bullets
   - as deep as you like

- [x] Task lists work as well
- [ ] Check this one off

## Tables

| Feature   | Supported | Notes                            |
| :-------- | :-------: | -------------------------------: |
| Tables    |    Yes    | Alignment via the delimiter row  |
| Footnotes |    Yes    | Collected at the end of the page |
| Raw HTML  |    No     | Stripped for safety              |

## Callouts

> Blockquotes render as accented callout boxes. Inline **formatting** and
> `code` work inside them.

## Code blocks

Gleam code is highlighted natively; other languages use highlight.js. Every
block gets a copy button.

```gleam
pub fn greet(name: String) -> String {
  "Hello, " <> name <> "!"
}
```

```sh
gleam run -m gleebook build
```

## Images and video

Use standard image syntax. If the URL is a YouTube link, Gleebook embeds the
video player instead of an image:

```markdown
![A diagram](assets/diagram.png)
![Talk title](https://www.youtube.com/watch?v=VIDEO_ID)
```

[^1]: Footnotes are written as `[^1]` in the text and `[^1]: ...` anywhere in
    the file. They are collected at the bottom of the page.
