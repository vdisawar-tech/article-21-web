# article-21-web

Static marketing + compliance website for **Article 21**, built to satisfy US carrier /
The Campaign Registry (TCR) review for A2P 10DLC SMS campaign registration.

Plain static HTML + one CSS file — no build step. Deployed to **GitHub Pages** and served
on a subdomain of the Squarespace-managed domain via DNS.

## Pages

| File | Purpose |
| --- | --- |
| `index.html` | Home / About + services + contact block |
| `contact.html` | Contact details |
| `privacy-policy.html` | Privacy Policy (mobile/SMS no-share clause, subprocessors) |
| `sms-terms.html` | SMS / Messaging Terms (program, STOP/HELP, "rates may apply") |
| `404.html` | Not-found page |
| `assets/style.css` | Shared styles |

## Preview locally

```bash
cd article-21-web
python3 -m http.server 8000
# open http://localhost:8000
```

Anything highlighted in yellow on the page is a `[PLACEHOLDER]` awaiting a real value.

## Deploy

Push to `main`. The workflow at `.github/workflows/pages.yml` publishes the site to GitHub
Pages automatically (Pages **Source = GitHub Actions**).

## Custom domain (apex — one-time)

The site is served at the apex `articletwentyone.com` (set in the repo `CNAME` file).

1. In **Squarespace → Domains → `articletwentyone.com` → DNS Settings**, remove any
   conflicting default A/CNAME records on the root, then add **four A records** (Host `@`):
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
2. (Optional, recommended) add a **CNAME** record: Host `www`, Value `vdisawar-tech.github.io`
   so `www.articletwentyone.com` redirects to the apex.
3. In **GitHub → repo → Settings → Pages**, set the custom domain to `articletwentyone.com`
   and enable **Enforce HTTPS** (after DNS propagates, GitHub provisions a free certificate).

Only the **A records** (website) change. **MX / email records are untouched**, so Squarespace-
or Google-managed email keeps working.
