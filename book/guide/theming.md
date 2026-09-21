# Theming

Gleebook ships with two themes: **Cyberpunk Pink** (dark) and **Rust Olive**
(light). The toggle at the bottom of the sidebar switches between them, and the
choice is remembered in the browser.

You can also force a theme through the URL, which is handy for sharing links:

```
index.html?theme=cyberpunk
index.html?theme=olive
```

## Custom colours

`book/custom.css` is copied into the build and loaded after the built-in
styles, so anything in it wins. The themes are driven by CSS variables;
override the ones you want, per theme:

```css
[data-theme='cyberpunk'] {
  --gb-accent: #7dd3fc;
}

[data-theme='olive'] {
  --gb-accent: #b45309;
}
```

| Variable | Controls |
| --- | --- |
| `--gb-bg`, `--gb-text` | Page background and body text |
| `--gb-sidebar`, `--gb-border` | Sidebar background and borders |
| `--gb-accent` | Brand colour, links, active chapter |
| `--gb-nav-text`, `--gb-nav-hover`, `--gb-nav-active` | Sidebar link states |
| `--gb-code-bg`, `--gb-code-bar`, `--gb-code-bar-text` | Code block body and title bar |
| `--gb-callout` | Callout background |
| `--gb-syn-*` | Syntax highlighting palette |

Plain CSS works as well: the content column has the `gleebook-prose` class, so
`.gleebook-prose h2 { ... }` is a safe hook.
