# fibpmo.com

Static launcher site served by GitHub Pages.

## Files

| File | What it is |
|------|------------|
| `index.html` | Landing page |
| `dashboard/index.html` | Encrypted page — content is AES-256-GCM ciphertext; nothing readable without the key |
| `CNAME` | Custom-domain config for GitHub Pages (do not delete) |

## Notes

- All sensitive content on this site is either encrypted at rest (AES-256-GCM,
  PBKDF2-derived keys) or hosted behind separate logins elsewhere. The HTML in
  this repo contains no readable confidential data, codes, or destinations.
- Local build/maintenance tooling is gitignored and never published.

## Hosting

GitHub Pages, deploy from branch `master`, root folder. Custom domain set in
**Settings → Pages**; HTTPS enforced.
