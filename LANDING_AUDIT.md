# Uzanet landing-page baseline audit

Audit date: 2026-09-14

## TL;DR

The original landing page was recovered intact from the `uzanet-landing/`
subdirectory of `bonnieace/Mikrotik`. Its landing-only history has been
extracted into this standalone repository. The recovered application compiles,
but it is not ready to replace the operator portal at `uzanet.co.ke` yet.

The immediate blockers are:

1. The mobile menu relies on an undefined `mobileMenuOpen` state.
2. ESLint reports 13 errors.
3. The page publishes commercial and product claims that are not evidenced by
   the current backend, including Paystack, Africa's Talking, public API keys,
   fixed subscription limits, unlimited API calls, 24/7 support and white-label
   availability.
4. The API example points to `api.uzanet.com`, while the live API uses
   `api.uzanet.co.ke`, and it demonstrates an API-key flow while the operator API
   currently uses OAuth2 password login and bearer JWTs.
5. Testimonials and several “partner” relationships are not verifiable from
   the codebase and should not be presented as customer endorsements or formal
   partnerships without business confirmation.
6. Many service, hardware, social, resource, company and legal links point to
   `#`; the contact section is commented out.
7. The app loads Tailwind's browser/development runtime from a CDN instead of
   compiling Tailwind during the build.
8. `npm audit --omit=dev` reports two high-severity dependency advisories in
   `nanoid` and `postcss`.

Do not connect the production domain to this baseline until the launch blockers
are handled in a separate, reviewable change.

## What was recovered

The recovered app is a Vue 3/Vite single-page application with:

- a fixed navigation bar and mobile navigation;
- hero and product-category sections;
- ten service cards;
- a three-step “How It Works” section;
- a developer/API section with a JavaScript example;
- three testimonials;
- integration/partner logos;
- three software pricing plans and two hardware bundles;
- a footer with resource, company and legal navigation;
- CTA rewrites that route operator onboarding to
  `https://mikrotikke.netlify.app/onboard` and API documentation to
  `https://api.uzanet.co.ke/docs` by default.

The landing-only default branch retains two commits from the backend history:

| Commit | Date | Purpose |
| --- | --- | --- |
| `a5b9316` | 2026-04-26 | Original landing-page implementation |
| `589e474` | 2026-09-09 | Route selected CTAs to onboarding and API docs |

## Verification results

| Check | Result | Notes |
| --- | --- | --- |
| `npm ci` | Pass | Lockfile installs successfully |
| `npm run build` | Pass | Vite emits a production bundle |
| `npx eslint .` | Fail | 13 errors: duplicate/unused keys and invalid image end tags |
| `npm audit --omit=dev` | Fail | Two high-severity dependency advisories |
| Landing-only history extraction | Pass | Backend files are excluded; recovered history is retained |
| Live production mapping | Fail | `uzanet.co.ke` currently serves the operator portal rather than this landing app |

## Findings by severity

### Launch blockers

#### 1. Broken mobile-menu state

`src/views/HomeView.vue` reads and writes `mobileMenuOpen`, but the script setup
does not declare it. The production compiler permits this and emits accesses to
the component render context, so a successful build does not prove that the
menu works. This is a functional mobile regression.

#### 2. Unsupported or unverified public claims

The page currently advertises:

- Paystack payment processing;
- Africa's Talking SMS/Voice integration;
- generic real-time webhooks;
- API rate-limit headers;
- fixed user and API-call allowances;
- unlimited users and API calls;
- a complete financial suite;
- 24/7 dedicated support;
- white-label options;
- Microsoft AD/LDAP login;
- global hardware shipping;
- “certified” access points.

The backend source currently supports M-Pesa and KopoKopo payment providers,
Hotspot and PPPoE operations, operator JWT authentication, router management,
payment callbacks and captive-portal operations. It does not evidence the other
claims above. Business-only services may still exist, but they need explicit
confirmation before publication.

#### 3. Misleading API example

The developer example uses `https://api.uzanet.com/v1/users` and a placeholder
API key. The deployed API base is `https://api.uzanet.co.ke`, its routes are
under `/api/v1`, and the operator API authenticates through
`/api/v1/auth/token`. Publishing the current example would send developers to
the wrong host and teach the wrong authentication flow.

#### 4. Unverified endorsements and partnerships

The page names Paul Kimani/FastConnect ISP, Tabitha Properties Hotspot and David
Chen/LocalNet as customers. It also presents vendor/integration logos under
“Partners & Integrations.” These should be treated as unverified until the
business owner confirms permission and accuracy. Integration compatibility is
not automatically a formal partnership.

#### 5. Dead conversion and legal paths

Numerous links use `href="#"`. The contact/free-trial section is commented out,
and the footer's privacy, terms, data-processing and cookie links have no
destinations. This makes several primary conversion paths and all displayed
legal paths non-functional.

### High priority

#### 6. Production styling depends on a browser CDN

`index.html` loads `@tailwindcss/browser@4` from jsDelivr. That package is meant
to generate styles in the browser and makes rendering depend on a third-party
runtime. Tailwind should be installed and compiled locally so the deployed CSS
is deterministic and covered by the build.

Font Awesome is also loaded from a public CDN without an integrity attribute.
It should either be bundled or pinned with appropriate supply-chain controls.

#### 7. Dependency advisories

The production dependency audit reports high-severity advisories through
`nanoid` and `postcss`. The lockfile needs a controlled upgrade followed by a
fresh build, lint and browser check.

#### 8. Incorrect SEO metadata

Open Graph metadata points to `https://www.uzanet.com`, not
`https://uzanet.co.ke`. There is no canonical URL or production social image.
The footer copyright year is also fixed at 2025.

#### 9. Hardware copy is inaccurate

The RB951Ui is described as dual-band, and the L009UiGS-2HaxD-IN is described as
a Cloud Core Router. These descriptions should be replaced with confirmed
manufacturer specifications before hardware bundles are published. Bundle
prices also need current commercial confirmation.

### Maintainability and polish

- `src/App.vue` changes CTA destinations by scanning and mutating rendered DOM
  text. Links should receive their real destinations directly from component
  data or props.
- The starter Vue demo components, store and `/about` route remain even though
  they are not part of the landing experience.
- Ten public assets are unreferenced. The largest is `acacia.png` at about
  3.5 MB.
- Several images omit useful `alt` text, and the mobile-menu button has no
  accessible label or expanded-state metadata.
- Language options in the footer do not change the page language.
- Copy contains spacing, grammar and brand-casing inconsistencies.
- There is no automated test suite or CI workflow for build, lint, links or
  responsive behavior.
- The README is still the default Vue starter text and does not document the
  production deployment contract.

## Recommended remediation order

1. Preserve this default branch as the recovered baseline.
2. Create a review branch that fixes the menu and lint failures, compiles
   Tailwind locally, upgrades vulnerable dependencies and removes dead code.
3. Replace or temporarily hide unsupported pricing, endorsements,
   partnerships, API claims and hardware details until each is confirmed.
4. Rewrite the developer example against the real authentication and route
   contract.
5. Connect every CTA, contact and legal path to a real destination.
6. Add a Netlify build contract (`npm ci`, `npm run build`, publish `dist`) and
   environment variables for the portal and API documentation URLs.
7. Add CI for install, lint, build and broken-link checks, then run desktop and
   mobile browser verification.
8. Only after a clean deploy preview should `uzanet.co.ke` be moved away from
   the operator-portal deployment.

## Deployment separation target

The intended topology is:

| Public surface | Repository | Deployment purpose |
| --- | --- | --- |
| `uzanet.co.ke` | `bonnieace/uzanet-landing` | Marketing/landing site |
| `mikrotikke.netlify.app` | `bonnieace/Mikrotik-Frontend` | New operator portal |
| `admin.uzanet.co.ke` | `bonnieace/uzanet` | Legacy operator portal |
| `api.uzanet.co.ke` | `bonnieace/Mikrotik` | Backend API |
| Mobile app | `bonnieace/uzanet-mobile` | Customer/operator mobile experience |

DNS and Netlify domain assignments are intentionally outside this baseline
audit and must not change until the standalone landing deployment is verified.
