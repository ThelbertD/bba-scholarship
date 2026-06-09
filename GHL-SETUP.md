# Transferring the Scholarship Page to GoHighLevel (GHL)

Use **`index-ghl.html`** — it's your scholarship page, pre-wired for GHL. Your
original `index.html` is left untouched.

What it does (unchanged from before):
- Applicant fills the form → details are POSTed to your **Google Sheet** (via the
  existing Apps Script endpoint).
- Based on the **coach** they select, they're redirected to that coach's
  **thank-you page** (now separate GHL funnel steps).

You only need to fill in two sets of URLs. Both live at the top of the
`<script>` block in `index-ghl.html`.

---

## Step 1 — Build the funnel steps in GHL

In **Sites ▸ Funnels**, create one funnel (e.g. "BBA Scholarship") with **5 steps**:

| Step | Purpose |
|------|---------|
| 1. Application | the scholarship page (this file) |
| 2. Thank You — Jase | thank-you for Jase |
| 3. Thank You — Carly | thank-you for Carly |
| 4. Thank You — Dom | thank-you for Dom |
| 5. Thank You — Erin | thank-you for Erin |

For each thank-you step, paste the matching `thankyou-<name>/index.html` from this
repo into a Custom Code element (same media-upload approach as below).

---

## Step 2 — Upload media to GHL

Go to **Sites ▸ Media** and upload everything from the `img/` folder **and** the
member-story `.mp4` files. After each upload, click it and **copy its URL**.

---

## Step 3 — Paste the page into the Application step

1. Open the **Application** step in the GHL funnel builder.
2. Drag in a **Custom JS/HTML** (Code) element, full width.
3. Set the section/row **padding to 0** so it spans edge-to-edge.
4. Open `index-ghl.html`, copy **everything from `<style>` through the closing
   `</script>`** (you can skip the `<!DOCTYPE>`, `<html>`, `<head>`, `<body>`
   wrapper tags), and paste it into the Code element.

---

## Step 4 — Fill in the URLs (the only editing you do)

Near the top of the `<script>` you'll find two clearly-marked blocks:

**❶ `MEDIA` map** — paste each GHL Media URL between the quotes. The key (left
side) stays as-is; the comment tells you which person/asset it is:
```js
"img/WEBFILES%20(2).jpg": "https://.../your-banner.jpg",  // hero birthday banner
"dan_t%20%28720p%29.mp4": "https://.../dan_t.mp4",         // Dan T
```

**❷ `pages` map** — paste the public URL of each coach's GHL thank-you step:
```js
var pages = {
  Jase:  'https://your-domain.com/scholarship-thankyou-jase',
  Carly: 'https://your-domain.com/scholarship-thankyou-carly',
  Dom:   'https://your-domain.com/scholarship-thankyou-dom',
  Erin:  'https://your-domain.com/scholarship-thankyou-erin',
};
```

The Google Sheet endpoint (`SHEET_ENDPOINT`) is already set — leave it alone.

---

## Notes

- **Form data still goes only to your Google Sheet**, not GHL's contact list
  (that's what you chose). The custom form handles validation, the Sheet POST,
  and the coach redirect itself — you do **not** need to add a native GHL form.
- The two member-story testimonials that are already **Vimeo embeds** (Matt K,
  Vikki M) need no upload — they stay as-is.
- The coach dropdown values (`Jase`, `Carly`, `Dom`, `Erin`) must match the keys
  in the `pages` map exactly. They already do.
- If GHL's editor strips the `<style>`/`<script>`, paste the page instead via
  **Funnel Settings ▸ Custom CSS/JS** (styles in CSS, the script in JS/footer)
  and keep only the markup in the Code element.
