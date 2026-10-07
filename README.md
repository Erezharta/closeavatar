# CloseAvatar website

Static marketing site for [CloseAvatar](https://closeavatar.com/): plain HTML and CSS, no build step, no dependencies, no secrets.

| File | Purpose |
| --- | --- |
| `index.html` | Landing page |
| `privacy.html` | Privacy page |
| `styles.css`, `fonts/`, `favicon.svg` | Styling, self-hosted fonts (Instrument Serif, Inter Tight, JetBrains Mono; OFL) and icon |
| `CNAME` | Custom domain for GitHub Pages (`closeavatar.com`) |
| `robots.txt`, `sitemap.xml` | SEO basics |
| `.github/workflows/pages.yml` | GitHub Pages deploy workflow |

## Preview locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy option A: GitHub Pages (simplest)

1. Merge the PR into `main`.
2. In the repo go to **Settings → Pages → Build and deployment → Source: GitHub Actions**. The included workflow publishes on every push to `main`.
   *(Alternative: Source "Deploy from a branch", pick `main` and `/ (root)`. Or push to a dedicated `deploy` branch and select that.)*
3. Under **Settings → Pages → Custom domain** enter `closeavatar.com`, then tick **Enforce HTTPS** once the certificate is issued.

### DNS for GitHub Pages

At your DNS provider for `closeavatar.com`:

| Type | Name | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `erezharta.github.io` |

Check GitHub's [custom domain docs](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site) in case the IPs have changed.

## Deploy option B: Cloudflare Pages

1. Cloudflare dashboard → **Workers & Pages → Create → Pages → Connect to Git**, pick this repo.
2. Production branch `main`, framework preset **None**, build command empty, output directory `/` (repo root).
3. After the first deploy, open the project → **Custom domains → Set up a custom domain** → `closeavatar.com`.
   - If the domain's DNS is on Cloudflare, records are created for you.
   - Otherwise add a `CNAME` for `www` to `<project>.pages.dev` and move the apex to Cloudflare DNS (apex CNAMEs need Cloudflare's flattening).
4. Delete the `CNAME` file and the Pages workflow if you only use Cloudflare.

## Contact

hello@closeavatar.com
