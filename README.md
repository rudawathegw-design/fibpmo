# fibpmo.com — PMO Portal

A one-domain launcher for First Iraq Bank's PMO.

```
fibpmo.com/            → access-code page (this folder's index.html)
   ├─ code "fib"  →  fibpmo.com/report/      (weekly report — shown inside fibpmo.com, URL stays put)
   └─ code "pmo"  →  fibpmo.com/dashboard/   (PMO dashboard: live PowerPoint + Excel, view only)
```

## Files in this folder
| File | What it is |
|------|------------|
| `index.html` | The access-code gate (the page people land on at fibpmo.com) |
| `report/index.html` | Wraps the weekly report so it shows inside fibpmo.com (URL stays on the domain) |
| `dashboard/index.html` | The PMO dashboard — live, read-only PowerPoint + Excel + portfolio |
| `CNAME` | Tells GitHub Pages the custom domain is `fibpmo.com` (do not delete) |

---

## How to put it online (one repo, free)

### 1. Create the GitHub repo
- New repo, e.g. **`fibpmo`** (public — GitHub Pages free tier needs public).
- Upload **everything in this folder**, keeping the structure (`index.html`, `CNAME`, and the `dashboard/` folder with its `index.html`).

### 2. Turn on GitHub Pages
- Repo **Settings → Pages**.
- **Source:** Deploy from a branch → `main` → `/ (root)` → Save.
- It goes live first at `https://rudawathegw-design.github.io/fibpmo/`.

### 3. Buy the domain
- `fibpmo.com` from any registrar. Cheapest with no markup: **Cloudflare Registrar (~$9/yr)**. Namecheap/GoDaddy also fine.

### 4. Point the domain at GitHub Pages (DNS records)
At your registrar's DNS settings, add:

**Apex (`fibpmo.com`) — four A records:**
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
**Apex — four AAAA (IPv6) records (optional but recommended):**
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```
**`www` subdomain — one CNAME record:**
```
www  →  rudawathegw-design.github.io
```

### 5. Set the custom domain in GitHub
- **Settings → Pages → Custom domain** → type `fibpmo.com` → Save.
- Wait for the **DNS check** to pass (can take a few minutes up to 48h to propagate).
- Then tick **Enforce HTTPS** (the free certificate provisions within ~1 hour).

Done — `fibpmo.com` now serves the access-code page.

---

## Changing things later

- **Change a code or destination:** edit the `ROUTES` block near the bottom of `index.html`.
  ```js
  var ROUTES = {
    "fib": "report/",
    "pmo": "dashboard/"
  };
  ```
- **Update the live files:** nothing to change here — the dashboard always shows the latest SharePoint version of the PowerPoint and Excel.

---

## Two things to know

**1. The codes are not real security.** `fib` and `pmo` live in the page source — anyone who opens "View Source" can read them and both destination URLs. This is a friendly launcher, not a lock. The actual report and SharePoint files stay protected by their own logins. If you ever need true protection on this domain, switch to **Cloudflare Access** (free, real login) — ask and it can be set up.

**2. The live embeds will only work if you do this in SharePoint first.** The dashboard embeds the PowerPoint/Excel by their links — but **personal OneDrive links (`.../personal/...`) are normally blocked from showing inside a frame on another website**, so on fibpmo.com the frames may come up blank. To make them render (and stay truly read-only):

  1. Move both files into the **PMO Team Site library** (not personal OneDrive). This also stops the link-expiry problem for good.
  2. For each file: **Share → Embed** → copy the `<iframe …>` code SharePoint generates. That code carries the right cross-site token.
  3. Replace the two `<iframe>` blocks in `dashboard/index.html` with the copied code.
  4. Set the file's sharing to **"people in your org — can view"** (not edit). This is what makes both the embed *and* the "Full screen" link genuinely view-only — the read-only-ness comes from the SharePoint permission, not the page. If the link allows editing, anyone clicking "Full screen" could edit.

  Send me the two Embed codes and I'll paste them in for you.
