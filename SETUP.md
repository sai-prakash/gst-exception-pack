# SETUP — GST Exception Pack waitlist

**Updated:** 2026-10-09 (Asia/Calcutta)  
**Stage:** Design-partner waitlist only. No payments, no checkout, confirmed customers: 0.

## Where the site lives

| Item | Value |
|------|-------|
| Page source | `docs/index.html` (single static file, inline CSS/JS, no framework) |
| Hosting | GitHub Pages — branch `main`, folder `/docs` |
| Live URL | https://sai-prakash.github.io/gst-exception-pack/ |
| Local copy on the box | `/workspace/company-os/ship/gst-exception-pack/` (`site/` → `docs/`) |

## How waitlist submissions are captured

- The form POSTs (via `fetch`) to **FormSubmit** — a free, no-API-key form relay:  
  `FORM_ENDPOINT = "https://formsubmit.co/ajax/saiprak@gmail.com"` (in `docs/index.html`).
- Each signup arrives as an **email to `saiprak@gmail.com`** (subject: *GST Exception Pack — waitlist signup*, table layout) with: name, email, role, monthly invoice volume, GSTIN (optional), note (optional).
- **Until the form is activated, FormSubmit does NOT forward submissions.** The page then shows an honest error and the visible mailto fallback (`saiprak@gmail.com`) — it never shows a fake "you're on the list".

## ⚠️ One-time step Sai must do (≈2 minutes)

1. Open https://sai-prakash.github.io/gst-exception-pack/ and submit the waitlist form once with your own details (e.g. role "Other", note "activation test").
2. Check `saiprak@gmail.com` (and Spam/Promotions) for an email from **FormSubmit** — "Action Required: Activate FormSubmit on …".
3. Click **Activate Form**.
4. Submit the form once more → you should see "You're on the list…" on the page **and** receive a "GST Exception Pack — waitlist signup" email. That is the end-to-end check.
5. (Recommended) The activation email/page gives a **random-string endpoint** (looks like `https://formsubmit.co/<random-string>`). Swap it in to hide your Gmail from the page source:
   - In `docs/index.html`, change `FORM_ENDPOINT` to `https://formsubmit.co/ajax/<random-string>` and the form `action` to `https://formsubmit.co/<random-string>`.
   - Commit + push to `main`; Pages redeploys in ~1 minute.

Tip: create a Gmail filter on subject `GST Exception Pack — waitlist signup` → label `waitlist` so signups are one click away. Export to a sheet later by hand or via a Gmail→Sheets filter.

## Alternative backend (if you'd rather not use FormSubmit)

**Formspree (free tier, dashboard + CSV export):**
1. Sign in at https://formspree.io with `saiprak@gmail.com` → **New form** → name "GST waitlist".
2. Copy the form id (`https://formspree.io/f/xxxxabcd`).
3. In `docs/index.html` set `FORM_ENDPOINT = "https://formspree.io/f/xxxxabcd"` (and the form `action` to the same URL). The JS already sends `Accept: application/json`; Formspree returns `{ "ok": true }`, which the page treats as success.
4. Push to `main`. Submissions then appear in the Formspree dashboard (and by email).

## Guardrails (do not change without a deliberate decision)

- No customer counts, logos, or testimonials until real.
- No payments / checkout / UPI link on this page (`PAYMENT_MODE=blocked`).
- Keep the disclaimer: not a CA firm, not legal or tax advice, no filing on the user's behalf.
- Your Gmail is visible in the page source and mailto link until step 5 above is done — remove the mailto line too if you want it fully hidden.
