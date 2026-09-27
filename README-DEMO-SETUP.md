# Crewsheet — Demo Deployment Guide

This is a genericized, de-identified copy of your Pyrotechnician Tools app, rebranded as
**"Crewsheet"** for showing to prospective customers. It is a static bundle of files —
it does nothing on its own until you deploy your own Google Sheet + Apps Script backend
and host the files somewhere. Follow the steps below.

## 1. Create a fresh Google Sheet + Apps Script deployment

Use the same clone process as your account-migration guide:

1. Create a **new, empty Google Sheet** (don't reuse your production one).
2. Open **Extensions → Apps Script**, paste in `apps_script_secure.gs` from this folder.
3. Run `getOrCreatePhotoFolder` once directly in the Apps Script editor to trigger the
   Google Drive authorization prompt (photo uploads will silently fail otherwise).
4. Deploy it as a **Web App** (Execute as: you, Who has access: Anyone), and copy the
   deployment URL it gives you (looks like `https://script.google.com/macros/s/.../exec`).

## 2. Paste your new deployment URL into the app — REQUIRED

Every page's script currently has this placeholder in place of the real Apps Script URL:

```
PASTE_YOUR_DEMO_APPS_SCRIPT_URL_HERE
```

It appears in 10 files: `index.html`, `checkin.html`, `form.html`, `new-hire.html`,
`operators.html`, `payroll.html`, `pyro-directory.html`, `qr-codes.html`,
`update-info.html`, `venues.html`. Find-and-replace that exact string with your new
deployment URL from step 1 in all 10 files before hosting.

**This is intentional and important**: it guarantees the demo can never accidentally
write to your real production Sheet, but it also means check-in, payroll, and operator
management won't work until you do this step.

## 3. Host the files (e.g. a new GitHub Pages repo)

Create a **new repo** (don't reuse `VortexAAR`) and push all the files in this folder to
it, then enable GitHub Pages. Once you have that URL:

- Open `qr-codes.html` and replace `PASTE_YOUR_DEMO_SITE_URL_HERE` (appears twice) with
  your new Pages URL, so the printed QR flyer and on-screen link point to the real demo
  check-in page instead of a placeholder.

## 4. Demo login passwords

New demo-only passwords (unrelated to your real ones):

- **HP Tools** password: `demo2026`
- **Manage/Edit** password: `manage2026` (also used for the admin/announcements unlock
  on the home page)

## 5. What's already been changed for you

- **Branding**: "Vortex Productions" / "Vortex Fireworks Artists" / "Pyrotechnician
  Tools" → **Crewsheet** everywhere, including the manifest, page titles, and the
  Apps Script Drive folder name.
- **Logo/icon**: replaced Vortex's actual artwork (`logo.jpg`, `icon-192.png`,
  `icon-512.png`) with a new generic flame-burst mark in the same fire-to-water
  gradient theme, since the original was your real company's copyrighted art.
- **Real crew data removed**: your actual crew roster (57 real people — names, home
  addresses, ages, phone numbers, pyrotechnic license numbers) was hardcoded directly
  into `form.html`, `operators.html`, and `payroll.html`. All three have been replaced
  with the same set of 18 fictional operators (fake names, `(555)` phone numbers,
  fictional towns).
- **Real venue/client data removed**: your real venue list (actual stadiums, schools,
  and cities you've worked with, in 5 different hardcoded copies across `venues.html`,
  `checkin.html`, `form.html`, `payroll.html`, `qr-codes.html`) has been replaced with
  fictional venues.
- **Contact emails genericized**: your real emails and the real Utah State Fire
  Marshal's office contact info were replaced with `@example.com` placeholders (these
  won't deliver mail — intentional, so test clicks in the demo can't send anything to
  real people or a real government office).
- **Passwords**: new demo-only password hashes (see above).

## 6. Known limitation carried over from the original app

The After-Action Report form's structure and fields still follow **Utah's actual OSFM
regulatory form**. That's fine for demoing to Utah-based prospects, but if you demo this
to someone in another state, you may want to mention that the report format would need
adapting to their state's fire marshal requirements — that's a separate, bigger piece of
work not done here.

## 7. Optional: refreshing demo data later

If prospects will be clicking around in the live Sheet themselves, consider periodically
re-importing the sample operator/venue data (via the existing CSV import feature) to
reset anything they've edited.
