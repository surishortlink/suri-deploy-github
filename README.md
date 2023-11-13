# Suri × Deploy to GitHub Pages

You're viewing a template repository tailored for deploying Suri to
[GitHub Pages](https://pages.github.com/).

What's Suri? Suri is your own link shortener that's easily deployed as a static
site. No server-side hosting, serverless cloud functions, or database necessary.
Head over to the main [`jstayton/suri`](https://github.com/jstayton/suri)
repository to learn more, including additional deployment methods.

## Install

_TBD_

## Manage Links

Links are managed through [`./src/links.json`](./src/links.json), which is
seeded with a few examples to start:

```json
{
  "/": "https://github.com/jstayton/suri",
  "1": "https://fee.org/articles/the-use-of-knowledge-in-society/",
  "tw": "https://twitter.com"
}
```

It couldn't be simpler: the key is the "shortlink" path that gets redirected,
and the value is the target URL. Keys can be as short or as long as you want,
using whatever mixture of characters you want. `/` is a special entry for
redirecting the root path.

Go ahead and make an edit, then commit and push to your repository. GitHub Pages
should automatically build and deploy your change. That's it!

## Config

Config options are set in [`suri.config.json`](suri.config.json). There is only
one at this point:

| Option | Description                                                        | Type    | Default |
| ------ | ------------------------------------------------------------------ | ------- | ------- |
| `js`   | Whether to redirect with JavaScript instead of a `<meta>` refresh. | Boolean | `false` |
