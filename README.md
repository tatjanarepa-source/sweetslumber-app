# sweetslumber-app

Marketing site, privacy policy, and account-deletion page for the **Sweet Slumber** baby sleep
tracker app (`com.tatjanka000.sleeptracker`). This is a plain static HTML site — no build step.

## Live site

**https://sweetslumber.app**

- `index.html` — landing page
- `privacy-policy.html` — privacy policy
- `delete-account.html` — account & data deletion instructions (linked from the Google Play
  Data Safety form)
- `auth-action.html` — Firebase auth action handler (password reset, etc.)
- `style.css` — shared styling
- `CNAME` — custom domain config for GitHub Pages (`sweetslumber.app`) — do not delete

## How publishing works

This repo is connected to **GitHub Pages**, building from the `main` branch, root folder.
**Any push to `main` automatically rebuilds and republishes the live site** — usually within
1-2 minutes. There is no separate deploy step, no CI file, and no manual upload anywhere
(Porkbun only hosts the domain's DNS, not the files).

To make a change:

```
git clone https://github.com/tatjanarepa-source/sweetslumber-app.git
# edit the .html/.css files
git add -A
git commit -m "describe the change"
git push origin main
```

Then check it's actually live:

```
curl -sI https://sweetslumber.app/<file>.html
```

### If the site doesn't update after a push

Check **Settings → Pages** on this repo on GitHub:
- "Last deployed" should update shortly after each push. If it's stuck on an old date, the
  custom domain's DNS check may be stuck (seen once already, in July 2026, after which no
  further deploys happened for months without anyone noticing).
- Fix: clear the **Custom domain** field, save, wait ~15 seconds, re-enter `sweetslumber.app`,
  save again. Confirm it now says "DNS check successful". If "Last deployed" still doesn't
  move, push an empty commit (`git commit --allow-empty -m "trigger rebuild"`) to force a
  fresh deploy.

## Google Play Console

The "Delete account URL" field in Policy → App content → Data safety should be
`https://sweetslumber.app/delete-account.html`. It must resolve live and show the app/developer
name — Google's automated check will reject the Data Safety form otherwise.
