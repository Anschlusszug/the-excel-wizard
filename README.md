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

## Imagery

Photos in `assets/img/` come from [Unsplash](https://unsplash.com) under the
Unsplash licence (free for commercial use, no attribution required).

- `hero-dashboard.jpg` — data analytics dashboards
- `spreadsheets.jpg` — reviewing financial spreadsheets

Swap these for real photos of your own work whenever you have them; the CSS
expects roughly 3:2 and 4:3 crops and will letterbox gracefully.
