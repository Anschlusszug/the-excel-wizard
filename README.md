# The Excel Wizard

Marketing site for **The Excel Wizard** — a consulting practice that rescues
out-of-control Excel workbooks.

- **Live site:** enable GitHub Pages on this repo (Settings → Pages → deploy from `master` root)
- **Stack:** plain HTML + CSS + vanilla JS. No build step, no dependencies.

```
index.html          all markup
assets/styles.css   all styling
assets/img/         hero + problem imagery (local, no hotlinking)
```

---

## Contact form

The form posts to [Web3Forms](https://web3forms.com), which emails submissions
to you. Free plan: **250 submissions/month, unlimited forms, no credit card.**

**Before the form will work, add your access key** (30 seconds, no signup):

1. Go to <https://web3forms.com> and enter the address you want submissions
   delivered to.
2. They show you an **access key** immediately.
3. Put it in `index.html` where it says `YOUR_WEB3FORMS_ACCESS_KEY`:

```html
<input type="hidden" name="access_key" value="YOUR_WEB3FORMS_ACCESS_KEY">
```

Until then the form still validates and still shows a success state, but
nothing is actually delivered — visitors should be pointed at
`hello@theexcelwizard.com` in the meantime.

### What is already wired up

| Feature | Detail |
| --- | --- |
| Delivery | AJAX POST to `api.web3forms.com/submit` |
| Validation | Name, message, and email format checked client-side |
| Spam | Hidden `botcheck` honeypot field (bots get a fake success) |
| UX | Inline success/error states, no page reload, button disabled while sending |
| Fallback | Error state tells the visitor to email directly |

### Alternatives if Web3Forms doesn't suit

- **Formspree** — 50/month free, unlimited forms, needs an account
- **Netlify Forms** — free, but only if you host on Netlify (adds `netlify` to the form tag)
- **Cloudflare Workers** — free tier, more setup, full control

---

## Why the form takes a link, not an upload

The form collects an optional **link** to a file the client shares from their own
Drive/Dropbox/SharePoint, rather than accepting the file directly. This is a
deliberate decision, not a missing feature. File attachments are also a paid-only
Web3Forms feature, so the free plan could not do it regardless.

The reasons, in order of how much they matter:

1. **Client confidentiality.** A spreadsheet consultancy's clients hold their most
   sensitive data in exactly these files — financial models, payroll, customer
   lists. Accepting uploads means storing other people's confidential and
   personal data, which brings GDPR obligations (processor agreements, retention
   limits, deletion on request) that a solo practice has no infrastructure to meet.
2. **Macro risk.** `.xlsm` / `.xlsb` / `.xltm` can carry VBA. The danger is not
   storing a file, it is anything that *parses* it — most upload services
   thumbnail or convert, which means running attacker-controlled code.
3. **Unbounded cost and storage.** A public bucket with no lifecycle rule quietly
   accumulates client data indefinitely.
4. **Better sales process anyway.** You get the problem description in plain text
   first, so the consultation call is useful instead of exploratory.

The form's hint text walks clients through sharing a redacted `.xlsx`, and tells
them screenshots are a fine alternative when the data is too sensitive to share.

**If you later want real uploads**, the requirements are: a dedicated bucket (not
served publicly), short-lived presigned URLs, an allowlist of `xlsx` only with
`xlsm` hard-rejected, lifecycle rules that delete objects automatically, and a
published retention policy.

---

## Imagery

Photos in `assets/img/` come from [Unsplash](https://unsplash.com) under the
Unsplash licence (free for commercial use, no attribution required).

- `hero-dashboard.jpg` — data analytics dashboards
- `spreadsheets.jpg` — reviewing financial spreadsheets

Swap these for real photos of your own work whenever you have them; the CSS
expects roughly 3:2 and 4:3 crops and will letterbox gracefully.
