# BDWeb – Blood Donation Static Website

Static, frontend-only website for a blood donation organization. It includes a landing page, About, Donate, Contact, and policy pages with responsive layout, client-side validation, and a small UI enhancement (custom cursor) — all without a backend.

## Features

- Responsive UI with Bootstrap 5 and Bootstrap Icons (via CDN)
- Pages: Home, About, Donate, Contact, Privacy, Terms, Accessibility
- Images and carousel on the home page
- Client-side validated forms (no backend): Donate and Contact
- WhatsApp quick-contact button
- Accessibility statement and considerations (focus, labels, reduced motion)

## Project Structure

```
Project/
├─ public/
│  ├─ index.html
│  ├─ about.html
│  ├─ donate.html
│  ├─ contact.html
│  ├─ privacy.html
│  ├─ terms.html
│  └─ accessibility.html
├─ assets/
│  ├─ images/
│  │  ├─ hero-image.jpg
│  │  ├─ slider-image1.jpg
│  │  ├─ slider-image2.jpg
│  │  └─ slider-image3.jpg
│  └─ vendor/            (optional, local libs not used by default)
│     ├─ bootstrap/
│     └─ jquery/
└─ .htaccess             (placeholder)
```

Notes on paths:
- HTML files are under `public/` and reference images at `../assets/...`.
- When serving the site, the web root should be the repository root (BDWeb), not the `public` folder, so that `../assets/...` resolves correctly.
- If your host requires publishing `public/` as the web root, either move/copy `assets/` under `public/` and update URLs, or change references in HTML from `../assets/...` to `/assets/...` and deploy both folders.

## Local Development

Option A — XAMPP/Apache (this repo is under `htdocs`):
- Start Apache in XAMPP and visit `http://localhost/BDWeb/public/index.html`.
- Assets resolve to `http://localhost/BDWeb/assets/...`.

Option B — Open from filesystem:
- Open `public/index.html` in a browser. Images will work as long as the browser allows file-relative `../assets/...` access from `public/`.

Option C — Any static server:
- Serve the repo root, for example:
  - Node: `npx serve .` (or any static server)
  - Python: `python -m http.server` (then open `/BDWeb/public/index.html`)

## External Dependencies (CDN)

- Bootstrap CSS/JS: `cdn.jsdelivr.net` (v5.3.3)
- Bootstrap Icons: `cdn.jsdelivr.net` (v1.11.3)
- Google Fonts: Lato, Neuton

These CDNs are referenced in each HTML page. The `assets/vendor/` folder contains optional local copies (Bootstrap, jQuery) if you prefer offline or self-hosted assets.

Switching to local vendor assets (optional):
- Replace the CDN `<link>`/`<script>` tags with paths under `assets/vendor/...`.
- Example for Bootstrap CSS/JS:
  - CSS: `<link rel="stylesheet" href="../assets/vendor/bootstrap/css/bootstrap.min.css">`
  - JS: `<script src="../assets/vendor/bootstrap/js/bootstrap.bundle.min.js"></script>`

## Customization

- Branding: Replace `assets/images/logo.png` and `assets/images/logo-extra.png` as needed.
- Content: Update copy in `public/*.html` pages (hero text, FAQs, policy dates, contact info).
- Images: Replace `assets/images/hero-image.jpg` and `slider-image*.jpg`.
- Forms: Client-side only. To submit to a backend, add an `action` or fetch handler.
- UI Extras: The “premium cursor” is inline JS/CSS in pages; remove those blocks to disable.

## Accessibility

- Semantic HTML, labeled form controls, visible focus, and reduced-motion support are in place.
- See `public/accessibility.html` for the statement and details.

## Privacy & Terms

- See `public/privacy.html` and `public/terms.html`. Update dates and details to match your organization’s policies.

## Deployment

- Any static host works. Ensure both `public/` and `assets/` are deployed and URL paths resolve.
- Recommended: publish the repository root so `public/` HTML can load `../assets/...`.
- If a host requires a single “publish directory”, either:
  - publish the repo root, or
  - publish `public/` and move/copy `assets/` into `public/` while updating asset URLs accordingly.

## Routing and .htaccess (Apache)

Clean URLs like `/about` are supported via `/.htaccess` rewrites that serve pages from `public/` while allowing `/assets` to be served directly.

- Webroot: Point your domain to the repository root (BDWeb), not `public/`.
- Entry: `/` maps to `public/index.html`.
- Clean pages: `/about` maps to `public/about.html` (and `/about.html` also works).
- Static files: `/assets/...` served as-is.

Apache requirements:
- Enable `mod_rewrite` and allow overrides for the site:
  - Debian/Ubuntu: `sudo a2enmod rewrite && sudo systemctl restart apache2`
  - Ensure your vhost has `AllowOverride All` for the site directory.
- Optional: enforce HTTPS by uncommenting the HTTPS block inside `/.htaccess`.

Deploying to a subfolder (e.g., `https://example.com/bdweb/`):
- Keep domain webroot at the repo root.
- Update `RewriteBase` in `/.htaccess` from `/` to `/bdweb/` if your server requires it for correct relative matching.

Nginx (optional equivalent):
- Serve the repo root, map `/` to `public/index.html`, try files in `public` first, and fall back to `public/$uri.html`. Ask if you want a snippet tailored to your server.

## Notes & Limitations

- Forms are demo-only; they show success messages but do not send data anywhere.
- The `.htaccess` file is currently empty; include rules as needed for your server.
 - Root `/.htaccess` contains routing rules for clean URLs and asset handling.
- `assets/vendor/` is optional and not referenced by default pages (CDN is used).

## Troubleshooting

- 404 on `/about`: Ensure `mod_rewrite` is enabled and `AllowOverride All` is set; verify `/.htaccess` is loaded.
- Images not loading after deploy: Confirm the domain webroot includes both `public/` and `assets/`, and that page URLs reference `../assets/...` correctly from `public/`.
- CDN blocked/offline: Switch to local vendor assets under `assets/vendor/` and update `<link>`/`<script>` tags accordingly.

## License

No license specified. Add one if you intend to share or open-source.
# BloodDonationStaticWebsite
