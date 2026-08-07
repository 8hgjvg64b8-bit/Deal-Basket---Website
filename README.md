# Deal Basket — website

Static marketing site for the Deal Basket app. Plain HTML, CSS, and a little JavaScript. No build step, no dependencies, nothing to install.

---

## Upload to GitHub Pages

The files in this folder go at the **root of the repository**. Not inside a subfolder. That is what caused the 404 last time.

1. Open your repo on github.com.
2. Delete everything currently in it (select files → Delete).
3. Click **Add file → Upload files**.
4. Drag in the *contents* of this folder — the individual files, not the folder itself. If you drag the folder, GitHub will nest everything one level down and Pages will 404 again.
5. Commit.
6. Go to **Settings → Pages**. Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
7. Under **Custom domain**, enter `dealbasket.app` and save. The `CNAME` file already contains this, so it should populate on its own.
8. Tick **Enforce HTTPS** once the certificate finishes provisioning (usually a few minutes, sometimes an hour).

### DNS at your registrar

For an apex domain (`dealbasket.app`), add four A records pointing at GitHub Pages:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

And a CNAME record for `www` pointing to `<your-github-username>.github.io`.

If those IPs don't work, check GitHub's current list — they publish it under "Managing a custom domain for your GitHub Pages site."

`.app` is an HSTS-preloaded TLD, so it will only ever load over HTTPS. Don't panic if the site is unreachable until the certificate is issued.

---

## Fill these in before launch

Search the files for `[` and you'll find every placeholder. They're highlighted in yellow on the page so they're hard to miss.

| Placeholder | Where | What to put |
|---|---|---|
| `[LEGAL ENTITY NAME]` | privacy.html, terms.html | Your LLC's exact registered name |
| `[BUSINESS MAILING ADDRESS]` | privacy.html, terms.html | A real address you can receive mail at |
| `[EFFECTIVE DATE]` | privacy.html, terms.html | The date you publish |
| `[STATE]` / `[COUNTY, STATE]` | terms.html §14 | Where your LLC is registered |
| `[Hosting and database provider]` etc. | privacy.html §5 | The services you actually end up using |
| `[e.g. 24 months]`, `[e.g. 30 days]` | privacy.html §6 | Retention periods you'll honor |

**These legal pages are drafts, not legal advice.** They're written to match a grocery price-comparison app and to satisfy App Store review, but they describe practices your app has to actually follow. If the app ends up collecting something the policy doesn't mention, the policy is wrong — and a mismatch between your App Privacy answers in App Store Connect and this page is a common rejection reason. Have a lawyer look at both files before you submit.

---

## When the app ships

- **Homepage hero:** replace the two "Get early access" buttons with real App Store / Google Play links.
- **`social-preview.png`:** the Open Graph tags reference `https://dealbasket.app/social-preview.png`, which doesn't exist yet. Make one at 1200×630 and drop it in the root, or links shared on iMessage and social will preview with no image.
- **Apple's Support URL field** in App Store Connect → point it at `https://dealbasket.app/contact.html`.
- **Apple's Privacy Policy URL field** → `https://dealbasket.app/privacy.html`.
- **App icon:** `favicon.svg` is the browser tab icon only. The app icon is a separate asset at 1024×1024 PNG, no transparency, no rounded corners.

---

## What's deliberately not here

- **Testimonials.** There are none, because you don't have users yet. Invented quotes on a pre-launch site are a liability, and App Review doesn't care about them. Add real ones after your TestFlight round.
- **A contact form.** GitHub Pages is static — a form needs a backend. Every "contact us" path on the site is a `mailto:` link instead. If you want a real form later, Formspree or Netlify Forms will do it without moving off static hosting.
- **App screenshots.** The receipt on the homepage stands in for them. Swap in real screenshots once the app's UI is settled; that's the single biggest upgrade this page can get.

---

## Files

```
index.html      Homepage — hero receipt, how it works, features, savings estimate, FAQ
contact.html    Support + contact. This is your App Store Support URL.
privacy.html    Privacy Policy
terms.html      Terms of Service
404.html        Not-found page (uses root-relative links so it works at any URL depth)
style.css       All styling for every page
favicon.svg     Browser tab icon
CNAME           dealbasket.app
robots.txt      Search engine directives
sitemap.xml     Page list for search engines
README.md       This file
```

## Editing notes

- Every page shares `style.css`. Change a color once in the `:root` block at the top and it changes everywhere.
- The header and footer are copy-pasted into each page (no templating in static HTML). If you edit the nav, edit it in all five files.
- The receipt's prices live in the `ITEMS` array in the `<script>` at the bottom of `index.html`. Totals and the savings percentage are calculated from that array, so you can change any price and the math stays correct.
- The savings calculator uses a 12% rate, set as `RATE` in the same script.
- Prices and store names on the site are made up, and the footer says so on every page. Keep that disclaimer if you keep the sample receipt.
