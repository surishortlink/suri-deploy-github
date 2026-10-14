<h1 align="center" width="100%">
  <img src="https://raw.githubusercontent.com/surishortlink/suri/HEAD/logo.png" width="200" alt="Suri" />
</h1>

<h3 align="center" width="100%">
  <i>Your own short links as an easily deployed static site on GitHub Pages</i>
</h3>

You're viewing a template repository tailored for deploying Suri to
[GitHub Pages](https://pages.github.com/) with
[GitHub Actions](https://docs.github.com/en/actions). Head over to
[the main repository](https://github.com/surishortlink/suri) to learn more about
Suri, including additional deployment options.

## Setup: Step By Step

1. Hit the "Use this template" button above and then "Create a new repository".
   Fill in the required details to create a new repository based on this one.
   On a free GitHub plan, the repository must be public for GitHub Pages to
   work.
2. Go to the "Settings" of your new repository and head to the "Pages" section.
   Under "Build and deployment", change the "Source" to "GitHub Actions".
3. Go to the "Actions" of your new repository and select the "Deploy to GitHub
   Pages" workflow. Hit the "Run workflow" button to build and deploy your site
   for the first time.

### Auto-Deploy

Any commits to the `main` branch of your new repository will trigger a new build
and deploy. Pull requests are built without deploying, so a mistake in
`links.json` is caught before it's merged. You can change this by editing
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml), which is the
GitHub Actions workflow for building the site and deploying to GitHub Pages.

### Custom Domain

Without a custom domain, GitHub Pages serves your site from
`https://<username>.github.io/<repository>/` (unless the repository is named
`<username>.github.io`), so every short link includes the repository name, like
`/<repository>/gh`. Suri's default `favicon.ico` and `robots.txt` also go
unused there, since browsers and crawlers only look for them at the root of a
domain.

To use a custom domain, follow GitHub's guide:
[Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

### Updating Suri

[Dependabot](https://docs.github.com/en/code-security/dependabot) opens a pull
request in your repository about a week after a new version of Suri is released.
You can also update it yourself:

```bash
npm install @surishortlink/suri@latest
```

Then commit the updated `package.json` and `package-lock.json`. Before updating
to a new major version, check
[the release notes](https://github.com/surishortlink/suri/releases) for breaking
changes.

## How It Works

### Manage Links

At the heart of Suri is the [`links.json`](src/links.json) file, located in the
`src` directory, where you manage your links. All of the template repositories
include this file seeded with a few examples:

```json
{
  "/": "https://www.youtube.com/watch?v=CsHiG-43Fzg",
  "1": "https://fee.org/articles/the-use-of-knowledge-in-society/",
  "gh": "https://github.com/surishortlink/suri"
}
```

It couldn't be simpler: the key is the "short link" path that gets redirected,
and the value is the target URL. Keys can be as short or as long as you want,
and can include `/` for nested paths, like `gh/suri`. Avoid `?` and `#`, which
browsers treat as the start of a query string or fragment. `/` is a special
entry for redirecting the root path.

### Build Static Site

Suri ships with a `suri` executable file that generates the static site from the
`links.json` file. The static site is output to a directory named `build`.

All of the template repositories are configured with a `build` script that
invokes this executable, making the command you run simple:

```bash
npm run build
```

When you make a change to the `links.json` file, simply re-run this command to
re-generate the static site, which can then be re-deployed. This template
repository is configured to do this automatically.

### Config

Configuration is handled through the [`suri.config.json`](suri.config.json) file
in the root directory. There is only one option at this point:

| Option | Description                                                        | Type    | Default |
| ------ | ------------------------------------------------------------------ | ------- | ------- |
| `js`   | Whether to redirect with JavaScript instead of a `<meta>` refresh. | Boolean | `false` |

### Public Directory

Finally, any files in the `public` directory will be copied over to the `build`
directory without modification when the static site is built. This can be useful
for files like `favicon.ico` or `robots.txt` (that said, Suri provides sensible
defaults for both).
