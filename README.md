# noVAR landing page

Static landing page for noVAR, transparent technology procurement. A Caliber Holdings company.

**Preview:** https://caliber-holdings.github.io/novar/

This is currently a **preview deployment**. It is hidden from search engines and still contains placeholder content. Follow the go-live checklist below before pointing novar.solutions at it.

---

## Go-live checklist: making this the real novar.solutions

Do these in order. Each step lists the file and the exact thing to change.

### 1. Replace the placeholder testimonial

- **File:** `index.html`
- **Find:** the comment `<!-- PLACEHOLDER TESTIMONIAL` in the Results section.
- **Change:**
  - Replace the quote text inside `<p class="heading-5">` with a real, client-approved quote.
  - Replace `Client name` and `Title, Company` with the real attribution.
  - Delete the line `<span class="ph-badge chip caption-3">Placeholder testimonial</span>`.
  - Delete the `PLACEHOLDER TESTIMONIAL` comment.
- **Check:** get written approval from the client to use their name and quote.

### 2. Connect the contact form to a real form handler

- **File:** `index.html`
- **Find:** `const ENDPOINT = '';` in the script near the bottom (search for `ENDPOINT`).
- **Change:** set it to the URL that should receive submissions, for example a HubSpot, Salesforce, Power Automate or Formspree endpoint:
  ```js
  const ENDPOINT = 'https://your-form-handler.example.com/submit';
  ```
- **What it sends:** a JSON `POST` with `name`, `company`, `email`, `phone` and `message`.
- **Until this is set:** clicking Submit opens the visitor's email app with a message to help@novar.solutions already filled in. Nothing is stored anywhere.
- **Check:** submit a test request on the live site and confirm it arrives.

### 3. Allow search engines to index the page

- **File:** `index.html`
- **Find and delete these two lines** near the top of `<head>`:
  ```html
  <!-- Preview deployment: kept out of search so it does not compete with novar.solutions. Remove when this becomes the live site. -->
  <meta name="robots" content="noindex, nofollow">
  ```
- Leave the `noindex` tag in `404.html` as it is. Not found pages should never be indexed.

### 4. Point novar.solutions at this site

**a. Add the custom domain in GitHub**

1. Go to **Settings → Pages** in this repo.
2. Under **Custom domain**, enter `novar.solutions` (or `www.novar.solutions`) and click **Save**. GitHub adds a `CNAME` file to the repo.
3. Once DNS has propagated, tick **Enforce HTTPS**.

**b. Update DNS** at the domain registrar or DNS host for novar.solutions:

| Type  | Host / name | Value                     |
|-------|-------------|---------------------------|
| A     | `@`         | `185.199.108.153`         |
| A     | `@`         | `185.199.109.153`         |
| A     | `@`         | `185.199.110.153`         |
| A     | `@`         | `185.199.111.153`         |
| CNAME | `www`       | `caliber-holdings.github.io` |

Remove the old records that point to the current website host first. DNS changes can take up to 24 hours to apply everywhere.

Recommended: verify the domain under the Caliber-Holdings organization settings (**Settings → Pages → Add a domain**) so nobody else can claim it on GitHub.

**c. Update paths that assume the `/novar/` subfolder**

The preview lives at `/novar/`. On the custom domain the site lives at the root, so update:

| File         | Find                                                         | Change to                                              |
|--------------|--------------------------------------------------------------|--------------------------------------------------------|
| `404.html`   | `<base href="/novar/">`                                      | `<base href="/">`                                      |
| `index.html` | `https://caliber-holdings.github.io/novar/assets/` (2 places, `og:image` and `twitter:image`) | `https://novar.solutions/assets/` |

**d. Check after the switch**

- https://novar.solutions loads the new page with all logos.
- https://novar.solutions/anything-made-up shows the branded 404 page with the logo.
- Sharing the link on LinkedIn or Teams shows the noVAR logo preview.
- The form test from step 2 still works.

### Optional before launch

- Point the footer's data privacy policy link at a page on the new site if the old site is retired (it currently links to `https://www.novar.solutions/data-privacy-policy`).
- Confirm the partner descriptions on the five featured cards (Nutanix, HPE, Ruckus, Palo Alto Networks, Fortinet) match how noVAR positions each partner.
- Confirm permission to display each client logo in the "Trusted by" strip.

---

## Structure

- `index.html`: the whole page (HTML, CSS and JS in one file; Geist font and Phosphor icons load from CDNs)
- `404.html`: branded not found page
- `assets/`: noVAR logos and favicon
- `assets/logos/`: original client and partner logo files as supplied
- `assets/logos/clean/`: all logos converted to white silhouettes for the dark page. Add new logos here and register them in the `LOGOS` list in `index.html`

## Updating the site

Edit files, commit and push to `main`. GitHub Pages republishes automatically, usually within a minute.

## Run locally

```bash
python -m http.server 5173
```

Then open http://localhost:5173. The 404 page's logo only resolves correctly on the deployed site because of its `<base href>`.
