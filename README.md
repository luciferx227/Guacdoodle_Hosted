# Guacdoodle — hosted build

This repository contains **only the compiled output** of the Guacdoodle site. It
exists so GitHub Pages has something public to serve while the source stays in a
private repository.

**Do not edit these files by hand.** Everything here is generated and will be
overwritten on the next deploy.

- **Source:** the private `Guacdoodle` repo
- **Live site:** `https://<user>.github.io/Guacdoodle_Hosted/`

---

## Why the split

Publishing GitHub Pages from a private repository requires GitHub Pro, Team or
Enterprise. On the free plan Pages only serves public repos — so the source repo
stays private and only the built assets are published here.

## One-time setup

1. Push this repo to GitHub as **`Guacdoodle_Hosted`**, public.
2. **Settings → Pages → Source: Deploy from a branch**, branch `main`, folder
   `/ (root)`.

The `.nojekyll` file is required: without it Pages runs the output through
Jekyll, which silently drops files and folders whose names start with an
underscore.

## Updating the site

From the private source repo:

```bash
npm run deploy:hosted
```

That rebuilds with the correct base path and syncs the output here. Then:

```bash
git add -A && git commit -m "deploy" && git push
```

## Base path

Asset URLs are built for `/Guacdoodle_Hosted/` because GitHub Pages serves a
project site from a subpath — and those URLs are **case-sensitive**, so the base
must match this repo's name exactly.

If you later point a custom domain at this repo, rebuild with `npm run build`
instead (base `/`) and add a `CNAME` file here.

## A note on the Supabase key

The Supabase **anon** key is compiled into the JavaScript in this repo. That is
intended and safe — it is a public identifier, and row-level security is what
protects the data. The **service-role** key is never included; it lives only in
Supabase Edge Function secrets.
