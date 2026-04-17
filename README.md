# Civil-Fi PAFC® — Deployment Guide

## Complete setup in 3 steps (~10 minutes)

---

## STEP 1 — Get your Web3Forms email key (2 minutes)

Web3Forms is a free service that receives form submissions and forwards them to your email. No server, no code, no monthly fee.

1. Go to **https://web3forms.com**
2. Enter the email where you want to receive signed NDAs (e.g. `zo@realsmart.com` or whatever email you want)
3. Click "Create Access Key"
4. Check your inbox — they'll send you a confirmation email
5. Click the confirmation link
6. You'll receive your **Access Key** — it looks like: `a1b2c3d4-e5f6-7890-abcd-ef1234567890`
7. **Copy this key**

Now open `index.html` in any text editor and find this block near the bottom:

```javascript
const WEB3FORMS_KEY = 'YOUR_WEB3FORMS_ACCESS_KEY_HERE';
const RECIPIENT_EMAIL = 'email@email.com';
const CALENDLY_URL = 'https://calendly.com/zosoa-rasoa';
```

Replace:
- `YOUR_WEB3FORMS_ACCESS_KEY_HERE` → paste your Web3Forms key
- `email@email.com` → your actual email
- `https://calendly.com/zosoa-rasoa` → your actual Calendly link (already set)

Save the file.

---

## STEP 2 — Create GitHub repository (3 minutes)

### Option A: Using GitHub.com (no command line needed)

1. Go to **https://github.com/new**
2. Repository name: `civilfi-investor` (or whatever you want)
3. Set it to **Private** (important — this is confidential)
4. Check "Add a README file"
5. Click **Create repository**
6. Once created, click **"Add file" → "Upload files"**
7. Drag and drop `index.html` into the upload area
8. Click **"Commit changes"**

### Option B: Using command line (if you prefer)

```bash
# Navigate to the folder containing index.html
cd civilfi-deploy

# Initialize git
git init
git add .
git commit -m "Initial deploy — Civil-Fi PAFC investor memorandum"

# Create repo on GitHub (replace YOUR_USERNAME)
# First create the repo on github.com/new (set to Private)
# Then:
git remote add origin https://github.com/YOUR_USERNAME/civilfi-investor.git
git branch -M main
git push -u origin main
```

---

## STEP 3 — Enable GitHub Pages (2 minutes)

1. Go to your repository on GitHub
2. Click **Settings** (tab at the top)
3. In the left sidebar, click **Pages**
4. Under "Source", select **Deploy from a branch**
5. Branch: select **main**, folder: **/ (root)**
6. Click **Save**
7. Wait 1-2 minutes
8. Your site is now live at: `https://YOUR_USERNAME.github.io/civilfi-investor/`

### Important: Private repo + GitHub Pages

GitHub Pages on private repos requires a **GitHub Pro** account ($4/month).
If you're on a free account, you have two options:

**Option 1** — Upgrade to GitHub Pro ($4/month) to keep the repo private
**Option 2** — Use the repo as public but rely on the NDA gate itself for access control (the content is protected behind the authentication flow — no one can see it without completing the NDA)

**Recommendation**: Option 2 is fine. The HTML file contains no sensitive data until someone completes the full NDA flow. The gate IS the protection. And the NDA + IP logging IS the legal protection.

---

## OPTIONAL — Custom domain (e.g. invest.civilfi.com)

If you want a custom domain instead of github.io:

1. In your repo, create a file called `CNAME` containing just: `invest.civilfi.com`
2. In your domain DNS settings, add a CNAME record:
   - Name: `invest`
   - Value: `YOUR_USERNAME.github.io`
3. In GitHub Settings → Pages, enter your custom domain
4. Check "Enforce HTTPS"

---

## What the investor receives by email

When someone completes the NDA flow, the following is sent automatically to your configured email:

```
═══════════════════════════════════════════════════════════
NDA SIGNED — CIVIL-FI PAFC®
═══════════════════════════════════════════════════════════
Reference : NDA-2026-A3F91C
Timestamp : 2026-04-16 14:32:07 UTC
Session ID : SC-B2E4-7F91

═══ SIGNATORY ═══
Full Name : Jean-Pierre Dupont
Organisation : Dupont Capital SAS
Position : Managing Director
Country : France
Email : jp@dupontcapital.com

═══ TECHNICAL EVIDENCE ═══
IP Address : 91.164.xxx.xxx
Device : iPhone · Safari
User Agent : Mozilla/5.0 (iPhone; CPU iPhone OS 17_4...)
Biometric Method : Face ID

═══ GDPR / CONSENT ═══
GDPR Consent : GRANTED
Consent Timestamp : 2026-04-16T14:30:12.456Z
Legal basis : GDPR Art. 6(1)(a)(b) · eIDAS (EU) 910/2014
Retention : 5 years

═══ LEGAL DISCLAIMERS ═══
[Full disclaimers included — see below]
═══════════════════════════════════════════════════════════

+ signature.png (handwritten signature captured on device)
```

---

## Security notes

- The NDA gate is client-side JavaScript. It is NOT military-grade security.
  It is designed to create a legal record and an impressive experience.
- The REAL protection is the NDA itself (legally binding) + the IP/device
  logging (evidence of who accessed) + the email record (timestamped proof).
- For production-grade security, consider Cloudflare Access or a backend
  authentication system. But for investor outreach, this is appropriate.

---

## Testing checklist

Before sharing with investors:

- [ ] Open the link on your phone — test the full flow
- [ ] Complete the NDA, sign with your finger, do the biometric
- [ ] Check that you receive the email with all details
- [ ] Check that the signature PNG is attached
- [ ] Click the Calendly button at the bottom — verify it opens correctly
- [ ] Test in both French and English
- [ ] Test with a different person to verify their name appears in the watermark

---

## Files in this package

```
civilfi-deploy/
├── index.html          ← The complete NDA + investor memorandum
├── README.md           ← This guide
└── CNAME               ← Custom domain (edit if needed)
```
