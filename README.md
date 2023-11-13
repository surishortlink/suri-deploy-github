# Suri × Deploy to GitHub Pages

You're viewing a template repository tailored for deploying Suri to
[GitHub Pages](https://pages.github.com/) with
[GitHub Actions](https://docs.github.com/en/actions).

What's Suri? Suri is your own link shortener that's easily deployed as a static
site. No server-side hosting, serverless cloud functions, or database necessary.
Head over to the main [`jstayton/suri`](https://github.com/jstayton/suri)
repository to learn more, including additional deployment methods.

## Setup

1. Click the "Use this template" button above and then "Create a new
   repository". Fill in the required details to create a new repository based on
   this one.
2. Go to the "Settings" of your new repository and head to the "Pages" section.
   Under "Build and deployment", change the "Source" to "GitHub Actions".
3. Go to the "Actions" of your new repository. There should be a workflow run
   that likely failed because the previous step wasn't yet completed. Go ahead
   and click into the workflow run and click the "Re-run jobs" button.
4. Any commits to the `main` branch of your new repository will trigger a new
   deploy. You can change this by editing
   [`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml), which is
   the GitHub Actions workflow for building the site and deploying to GitHub
   Pages.
5. If you want to use a custom domain, follow GitHub's guide:
   [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

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

Go ahead and make an edit, then commit and push to your repository. GitHub
Actions should automatically build and deploy your change. That's it!

## Config

Config options are set in [`suri.config.json`](suri.config.json). There is only
one at this point:

| Option | Description                                                        | Type    | Default |
| ------ | ------------------------------------------------------------------ | ------- | ------- |
| `js`   | Whether to redirect with JavaScript instead of a `<meta>` refresh. | Boolean | `false` |
