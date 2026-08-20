# nurbly-site

One page: the privacy policy for the Nürbly Android app. Google Play will not
publish an app without a public privacy policy URL, and it re-checks that the
URL still loads after the app is live, so this is deliberately hosted off the
laptop rather than behind the Cloudflare tunnel.

The page is a copy of `play/privacy/index.html` in the Nürbly repo
(`~/projects/android/nurbly`). That file is the source. When it changes, copy
it here and push.

## Publishing it

The GitHub CLI is installed but not logged in. Run this yourself once:

```
gh auth login
```

Then, from this directory:

```
git init -b main
git add -A
git commit -m "Privacy policy for Nurbly"
gh repo create nurbly-site --public --source=. --push
gh api -X POST repos/{owner}/nurbly-site/pages -f 'source[branch]=main' -f 'source[path]=/'
```

The page appears at `https://<your-github-user>.github.io/nurbly-site/` within
a couple of minutes. Put that URL in Play Console under
Policy > App content > Privacy policy.

## Why a whole repo for one file

Play treats a dead privacy policy URL as a policy violation, and the laptop is
a laptop. GitHub Pages costs nothing and does not go down when this machine
reboots.
