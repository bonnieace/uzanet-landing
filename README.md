# Uzanet landing page

Standalone marketing site for [uzanet.co.ke](https://uzanet.co.ke). The operator
portal remains a separate application in `bonnieace/Mikrotik-Frontend`.

## Local development

```sh
npm ci
npm run dev
```

Run the complete repository check before opening a pull request:

```sh
npm run check
npm audit --omit=dev --audit-level=high
```

## Environment

Copy `.env.example` to `.env.local` when overriding the production-safe
defaults.

| Variable | Purpose | Default behavior |
| --- | --- | --- |
| `VITE_PORTAL_URL` | Operator portal origin and onboarding destination | `https://mikrotikke.netlify.app` |
| `VITE_API_DOCS_URL` | Public FastAPI documentation | `https://api.uzanet.co.ke/docs` |
| `VITE_SHOW_PUBLIC_PRICING` | Shows pricing and hardware bundles | Hidden unless exactly `true` |
| `VITE_SHOW_CUSTOMER_PROOF` | Shows testimonials and integration-logo section | Hidden unless exactly `true` |

Pricing and customer proof are intentionally disabled until the commercial
details and publication permissions are confirmed.

## Netlify deployment

The repository includes `netlify.toml` with the required build and SPA routing
configuration:

- build command: `npm ci && npm run build`
- publish directory: `dist`
- Node.js: 22

Create a dedicated Netlify site from this repository and verify its deploy
preview before assigning `uzanet.co.ke`. Do not attach this domain to the
operator-portal deployment.

## Branches

- `main`: recovered landing baseline and reviewed production changes after merge.
- `audit/baseline-review`: written audit of the recovered implementation.
- production changes should be proposed through pull requests.
