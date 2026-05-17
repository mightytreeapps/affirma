# Affirma marketing site

Static three-page site to satisfy the URLs Apple asks for during App Store
submission, plus a public landing page.

## Pages

| File             | Purpose                                | App Store Connect field          |
| ---------------- | -------------------------------------- | -------------------------------- |
| `index.html`     | Marketing landing page                 | **Marketing URL** (optional)     |
| `privacy.html`   | Privacy policy                         | **Privacy Policy URL** (required) |
| `support.html`   | Support & contact, FAQ                 | **Support URL** (required)       |

The contact email used throughout is `mightytreeapps@gmail.com`. Search for
it before deploying if you want to change it in one pass.

## Before you ship

1. **Set up the mailbox.** `mightytreeapps@gmail.com` must actually receive
   mail before submission &mdash; Apple's reviewers click the support link.
2. **Fill in the App Store URL.** Both CTAs on `index.html` point to `#`.
   After your app is approved, replace `href="#"` (two places) with the
   real App Store listing URL.
3. **Confirm the data inventory in `privacy.html`** matches what the app
   actually does at the time of submission. The current policy is based
   on the wipe map in `src/features/account/lib/deleteAccountData.ts`.
4. **Pick a domain.** The pages assume relative paths, so they work at any
   host. Suggested options:
   - `affirma.app` (matches the brand &mdash; needs the domain registered)
   - `mightytreeapps.com/affirma`
   - `mightytreeapps.github.io/affirma`

## Deploying

This is a plain static site &mdash; no build step.

### GitHub Pages

1. Push the contents of `marketing-site/` to a repo (or a `docs/` folder
   in an existing repo).
2. In repo settings, enable Pages and point it at that folder.
3. Use the resulting `https://<user>.github.io/<repo>/privacy.html` URL
   in App Store Connect.

### Netlify / Vercel / Cloudflare Pages

1. Connect the repo.
2. Set the publish directory to `marketing-site/`.
3. Leave the build command blank.

### Manual (any static host)

Upload the four files plus `app-icon.png` to the host's web root.

## Updating the policy

If you change the data the app collects (new Firestore collection, new
SDK that phones home, new analytics, etc.):

1. Update the relevant section of `privacy.html`.
2. Bump the `Last updated` date at the top of `privacy.html`.
3. Re-check Apple's **App Privacy** questionnaire in App Store Connect
   against the policy &mdash; they have to agree.
