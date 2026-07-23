# McKenney Electric Co — Website

Marketing site for McKenney Electric Co (Charlotte, NC), built with
[Astro](https://astro.build) + Tailwind CSS. Deploys to GitHub Pages at
`mckenneyelectric.co`.

## Commands

```sh
npm install
npm run dev       # localhost:4321
npm run build     # -> dist/
npm run preview   # preview the production build locally
```

## Before this goes live

1. **Contact form.** `src/components/Contact.astro` posts to Formspree but
   uses a placeholder ID. Sign up at [formspree.io](https://formspree.io),
   create a form, and replace `FORMSPREE_ID` near the top of that file with
   your real form ID.

## Deploying

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the
site and publishes it via GitHub Pages. One-time setup on GitHub:

1. Push this repo to GitHub.
2. In the repo's **Settings → Pages**, set **Source** to **GitHub Actions**.
3. In **Settings → Pages → Custom domain**, enter `mckenneyelectric.co` and
   save (the `public/CNAME` file already contains this, so it should
   pre-fill).
4. At your domain registrar, point `mckenneyelectric.co` at GitHub Pages:
   - Four `A` records for the apex domain to GitHub's Pages IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`,
     `185.199.111.153`
   - If you also want `www.mckenneyelectric.co` to work, add a `CNAME`
     record for `www` pointing to `<your-github-username>.github.io`.
5. Back in **Settings → Pages**, check **Enforce HTTPS** once DNS has
   propagated (can take up to a few hours).
