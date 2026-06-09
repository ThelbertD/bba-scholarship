# Scholarship Form — fields for a native GHL form

Rebuild these as a GHL form so GHL automations (e.g. send email on submit) can
trigger. Standard fields (Name/Email/Phone) use GHL's built-ins; the rest should
be GHL **Custom Fields** so they save to the contact and can be used in emails.

| # | Label | Type | Required | Options |
|---|-------|------|----------|---------|
| 1 | Full Name | Text | yes | — |
| 2 | Email | Email | yes | — |
| 3 | Phone | Phone | yes | — |
| 4 | Which BBA Coach are you coming to this application from? | Dropdown | yes | Jase, Carly, Dom, Erin |
| 5 | Where are you originally coming to this application from? | Dropdown | yes | Facebook, Instagram, Tiktok, YouTube, LinkedIn, BBA Podcast, Website, Email |
| 6 | Instagram Username | Text | yes | placeholder: @yourhandle |
| 7 | Facebook Name or TikTok Username | Text | no | optional |
| 8 | How old are you currently? | Number | yes | e.g. 44 |
| 9 | What City and Country are you located in? | Text | yes | e.g. Sydney, Australia |
| 10 | What health, fitness or life goals are you looking to achieve if we were to choose you? | Text area | yes | — |
| 11 | Please tell us why we should choose you? | Text area | yes | — |

## Original field names (from the current custom form)

```
full_name        (text,    required)
email            (email,   required)
phone            (tel,     required)
coach            (select,  required)  -> Jase | Carly | Dom | Erin
source           (select,  required)  -> Facebook | Instagram | Tiktok | YouTube | LinkedIn | BBA Podcast | Website | Email
instagram        (text,    required)
facebook_tiktok  (text,    optional)
age              (number,  required)
location         (text,    required)
goals            (textarea,required)
why              (textarea,required)
```

## Raw HTML of the current form (reference)

```html
<form>
  <label>Full Name *</label>
  <input type="text" name="full_name" placeholder="Your name" required>

  <label>Email *</label>
  <input type="email" name="email" placeholder="you@email.com" required>

  <label>Phone *</label>
  <input type="tel" name="phone" placeholder="Best contact number" required>

  <label>Which BBA Coach are you coming to this application from? *</label>
  <select name="coach" required>
    <option value="" disabled selected>Select your coach</option>
    <option value="Jase">Jase</option>
    <option value="Carly">Carly</option>
    <option value="Dom">Dom</option>
    <option value="Erin">Erin</option>
  </select>

  <label>Where are you originally coming to this application from? *</label>
  <select name="source" required>
    <option value="" disabled selected>Select a source</option>
    <option value="Facebook">Facebook</option>
    <option value="Instagram">Instagram</option>
    <option value="Tiktok">Tiktok</option>
    <option value="YouTube">YouTube</option>
    <option value="LinkedIn">LinkedIn</option>
    <option value="BBA Podcast">BBA Podcast</option>
    <option value="Website">Website</option>
    <option value="Email">Email</option>
  </select>

  <label>Instagram Username *</label>
  <input type="text" name="instagram" placeholder="@yourhandle" required>

  <label>Facebook Name or TikTok Username</label>
  <input type="text" name="facebook_tiktok" placeholder="Optional">

  <label>How old are you currently? *</label>
  <input type="number" name="age" placeholder="e.g. 44" required>

  <label>What City and Country are you located in? *</label>
  <input type="text" name="location" placeholder="e.g. Sydney, Australia" required>

  <label>What health, fitness or life goals are you looking to achieve if we were to choose you? *</label>
  <textarea name="goals" required></textarea>

  <label>Please tell us why we should choose you? *</label>
  <textarea name="why" required></textarea>

  <button type="submit">Submit Application</button>
</form>
```

## IMPORTANT — integration note

The form currently embedded on the landing page is **custom HTML inside the
iframe** and submits to **Google Sheets**, NOT to GHL. GHL automations can only
trigger on a **native GHL form**. So to send email via GHL automation you must
pick one approach:

- **Option A — Replace with a GHL form.** Build the form above as a real GHL
  form and drop it on the GHL landing page (outside/over the iframe, or rebuild
  the apply section in GHL). Then a Workflow trigger "Form submitted" can send
  the email. Note: the coach-based redirect + Google Sheet would need to be
  re-done with GHL Workflow actions (Sheets action + conditional redirect).

- **Option B — Keep the custom form, also notify GHL.** Keep the current
  form/Sheet/redirect and additionally POST submissions to a GHL inbound
  webhook (Workflow trigger "Inbound Webhook"), then send the email from there.
  Keeps the existing design and redirect intact.
