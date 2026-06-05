# Shopify Staging Environment Setup

This repo is wired to auto-deploy to a Shopify dev/staging store on every push to `main`.

## Required GitHub Repository Secrets

Go to **Settings → Secrets and variables → Actions** and add:

| Secret | Value |
|--------|-------|
| `SHOPIFY_API_KEY` | `0abb9d59730f67c95332fa1815155950` |
| `SHOPIFY_API_SECRET` | The app secret from partners.shopify.com |
| `SHOPIFY_FLAG_STORE` | Dev store URL, e.g. `koiiswim-dev.myshopify.com` |
| `SHOPIFY_CLI_THEME_TOKEN` | Theme Access Password (Shopify Admin → Apps → Theme Access) |
| `SHOPIFY_STAGING_THEME_ID` | ID of the theme to push to (from Shopify admin URL) |

## Connecting the Dev App to This Repo (Partner Dashboard)

1. Log in to [partners.shopify.com](https://partners.shopify.com)
2. Open the app with client ID `0abb9d59730f67c95332fa1815155950`
3. Go to **App setup → GitHub**
4. Connect `cheynetomagents/koiiswim-com` and select the `main` branch

This enables Shopify to auto-update the app's URLs and extensions whenever `main` changes.

## Workflows

| Workflow | Trigger | What it does |
|----------|---------|-------------|
| `deploy-staging.yml` | push to `main` | Runs `shopify app deploy` — syncs app extensions & config |
| `theme-deploy-staging.yml` | push to `main` (theme files only) | Runs `shopify theme push` — pushes theme code to staging store |

## Local Development

```bash
# 1. Clone the repo
git clone https://github.com/cheynetomagents/koiiswim-com.git
cd koiiswim-com

# 2. Copy env template
cp .env.example .env
# Fill in SHOPIFY_FLAG_STORE, SHOPIFY_API_SECRET, etc.

# 3. Install deps (once you add a package.json)
npm install

# 4. Start dev server (opens tunnel to your dev store)
npx shopify app dev
```
