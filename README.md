# ODEVI – website

**Odd and even make islands.** This repository is the website for [ODEVI](https://odevi.app), a number puzzle for iPhone (and later Android): fill the grid so every row and column holds each number once, while odd and even neighbours join into islands of exactly the right size.

The site is plain static HTML served by GitHub Pages. There is no build step, no framework and no tracking.

## Pages

| File | URL | Purpose |
| --- | --- | --- |
| `index.html` | [odevi.app](https://odevi.app) | Home page with a playable 4×4 sample puzzle, the three rules, levels and features |
| `privacy.html` | [odevi.app/privacy](https://odevi.app/privacy) | Privacy policy, covering version 1.0 (no data collected) and the ad-supported versions from 1.1 |
| `support.html` | [odevi.app/support](https://odevi.app/support) | Contact details and FAQ |
| `version.json` | [odevi.app/version.json](https://odevi.app/version.json) | Read by the app to decide whether an update is required |

The privacy and support URLs are the ones given in App Store Connect and Google Play Console. Keep them stable.

Each page is self-contained (inline CSS and JavaScript) and supports light and dark mode. Fonts are Bricolage Grotesque and IBM Plex Sans from Google Fonts.

## version.json – the update check

At launch, and whenever it returns to the foreground, the app downloads `version.json`. If the installed version is lower than `minimumVersion`, the app shows a blocking **Update ODEVI** screen that links to the store. If the file can't be read, the app keeps working as normal.

```json
{
  "minimumVersion": "1.0",
  "storeUrl": "https://apps.apple.com/app/id6830254784"
}
```

| Field | Meaning |
| --- | --- |
| `minimumVersion` | Lowest app version allowed to run. Compared with the app's version number (for example `1.0`, `1.1`). |
| `storeUrl` | Where the update button takes iPhone users. |
| `android.minimumVersion` *(optional)* | Overrides `minimumVersion` for the Android app, if the two platforms need to differ. |

**To force everyone onto a new version:** wait until that version is live in the store, then raise `minimumVersion` and commit. For example, set it to `"1.1"` once the ad-supported 1.1 is released.

> ⚠️ Never raise `minimumVersion` above a version that users can actually download. Everyone on older versions would be locked out with nothing to update to.

The file must stay valid JSON. Check it at [jsonlint.com](https://jsonlint.com) before you commit.

## Publishing

1. Edit files directly on GitHub (pencil icon) or upload new versions with **Add file › Upload files**.
2. Commit to `main`. GitHub Pages publishes the change within a minute or two.
3. **Settings › Pages** shows the build status and the live address.

### Custom domain (odevi.app)

1. In **Settings › Pages › Custom domain**, enter `odevi.app` and save. GitHub then adds a `CNAME` file to this repository. Do not delete it.
2. At the domain registrar, point the domain at GitHub Pages with four `A` records for `@` (185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153) and a `CNAME` record for `www` pointing to `odevigame.github.io`.
3. When the DNS check passes, tick **Enforce HTTPS**. `.app` domains work only over HTTPS.

Until the domain is live, the site is available at <https://odevigame.github.io>.

## Images

The home page refers to two files that should sit in the root of this repository. Both are in `ODEVI-web-images.zip`:

- `og-image.png` (1200×630), the preview image when the site is shared, from `social/`
- `apple-touch-icon.png` (180×180), the iPhone home-screen icon, from `icons/`

## Before each app release

- [ ] The privacy policy matches what the new version actually does, and its effective date is updated
- [ ] The App Store and Google Play privacy details match the policy
- [ ] The FAQ on the support page is still accurate
- [ ] `version.json` is raised only after the new version is live

## Contact

ODEVI is made by one independent developer in Norway. Questions, bug reports and ideas: [mail@odevi.app](mailto:mail@odevi.app).

© 2026 ODEVI
