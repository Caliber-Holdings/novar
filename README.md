# noVAR landing page

Static landing page for noVAR, transparent technology procurement. A Caliber Holdings company.

Live preview: https://caliber-holdings.github.io/novar/

## Structure

- `index.html`: the page (HTML, CSS and JS in one file; fonts and icons load from CDNs)
- `404.html`: branded not found page (uses `<base href="/novar/">`; change to `/` on a custom domain)
- `assets/`: noVAR logos and favicon
- `assets/logos/clean/`: partner and client logos converted to white silhouettes

## Before going live

- Replace the placeholder testimonial in the Results section
- Set `ENDPOINT` in the form script to a real form handler (it currently opens an email draft to help@novar.solutions)
- Remove the `noindex` robots meta tag in `index.html`

## Run locally

```bash
python -m http.server 5173
```
