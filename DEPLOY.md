# Deploy universalaillc.com

The new Universal AI LLC site is built and committed locally at `~/Desktop/Projects/websites/universalaillc/`.

The current GoDaddy "Launching Soon" placeholder needs to be replaced. Pick ONE of the two paths below.

---

## Option A — GitHub Pages (recommended; matches your other 4 sites)

This is the same pattern you use for jineo-app, banchan-app, cooked-app, and glowup-app. Free, fast, and you control the source. Takes ~10 minutes.

### 1. Create the GitHub repo
- Go to https://github.com/Zentry07
- New repo → name `universalaillc-site` → public → don't init with README

### 2. Push from your Mac
```bash
cd ~/Desktop/Projects/websites/universalaillc
git remote add origin https://github.com/Zentry07/universalaillc-site.git
git branch -M main
git push -u origin main
```

### 3. Enable GitHub Pages
- Repo → Settings → Pages → Source: `Deploy from a branch` → Branch: `main` / root → Save

### 4. Add the custom domain (universalaillc.com)
- Repo → Settings → Pages → Custom domain: `universalaillc.com` → Save
- GitHub will automatically create a `CNAME` file in the repo
- Wait for DNS check; enable "Enforce HTTPS" once it goes green

### 5. Update DNS at your domain registrar
You're currently on GoDaddy. Log in, go to universalaillc.com → DNS settings, and replace the existing A records with these GitHub Pages IPs:

```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
CNAME www  zentry07.github.io
```

**Keep your existing MX records intact** (the Google Workspace `1 smtp.google.com.` ones) — those handle your contact@ email and must not be touched.

### 6. Wait for DNS to propagate (5-30 min)
Test with: `curl -I https://universalaillc.com` — should show GitHub headers, no more GoDaddy.

---

## Option B — GoDaddy Website Builder (faster but less ideal)

If you want to skip GitHub and just edit the existing GoDaddy placeholder:

1. Log in to GoDaddy → My Products → Website Builder for universalaillc.com
2. Delete the existing "Launching Soon" template
3. Create a new "Custom HTML" page → paste the contents of `index.html`
4. Save and publish

Repeat for `/privacy` and `/terms` pages (paste `privacy.html` and `terms.html` content).

**Why this is worse**: GoDaddy will inject extra script tags and you can't version-control changes. But it's the fastest path if you don't want to touch DNS.

---

## After deploy: verify before replying to Apple

```bash
curl -s https://universalaillc.com | grep -o "Universal AI LLC" | head -1
curl -s https://universalaillc.com/privacy.html | grep -o "Privacy Policy" | head -1
curl -s https://universalaillc.com/terms.html | grep -o "Terms of Service" | head -1
```

All three should return matches. Once they do, reply to Nero from contact@universalaillc.com and you're done with prep.

---

## Why this matters for the Apple migration

Apple's pre-migration check requires a **publicly available organization website at a domain associated with the org**. The GoDaddy "Launching Soon" placeholder doesn't prove ownership or authority — it's a generic stock page. The new site:

- Names "Universal AI LLC" prominently in the title and header
- Lists all 3 apps with App Store links
- Includes registered email (contact@universalaillc.com) and Maryland location
- References Apple Developer Team ID NMND2RQBF3
- Has a privacy policy and terms of service (Apple Review Guideline 5.1.1)

This makes the org-conversion review obvious for Apple's team and reduces the chance of follow-up questions.
