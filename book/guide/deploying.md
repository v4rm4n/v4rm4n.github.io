# Deploying

When the book is ready, compile it to static HTML:

```sh
gleam run -m gleebook build
```

The result lands in `build/gleebook/` and is completely self-contained: the
HTML pages, your `assets/` folder and `custom.css`. Upload that directory to any
static host — GitHub Pages, Netlify, Cloudflare Pages, an S3 bucket or a plain
web server. Links are relative, so it works from a sub-path too.

## Checklist

- [ ] Every chapter in `SUMMARY.md` has a matching `.md` file (the build warns about missing ones)
- [ ] `build/` is in your `.gitignore` (it is, if the project came from `gleam new`)
- [ ] Images referenced from pages live in `assets/`
