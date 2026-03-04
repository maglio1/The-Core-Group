# Change Log — 2026-03-03

## Session: Deploy to GitHub Pages & Repoint DNS from Squarespace — Started 2026-03-03 ~22:00:00

---

### 2026-03-03 ~22:10:00
**Action:** CREATE
**Target:** /AI_TheCoreGroup/CNAME
**Why:** GitHub Pages requires a CNAME file to configure a custom domain
**Before:** N/A — new file
**After:** `www.thecoregroup.com` (initially created with wrong domain; corrected later)

---

### 2026-03-03 ~22:15:00
**Action:** CONFIG
**Target:** GitHub repo maglio1/The-Core-Group — Visibility
**Why:** GitHub Pages requires public repos on free plan
**Before:** Repository was PRIVATE
**After:** Repository changed to PUBLIC

---

### 2026-03-03 ~22:20:00
**Action:** CONFIG
**Target:** GitHub repo maglio1/The-Core-Group — GitHub Pages settings
**Why:** Enable GitHub Pages to serve the website
**Before:** GitHub Pages was not configured
**After:** GitHub Pages enabled — Source: Deploy from branch, Branch: main, Folder: / (root)

---

### 2026-03-03 ~22:30:00
**Action:** DELETE
**Target:** Squarespace DNS — coregroupmarketing.com — Squarespace Defaults
**Why:** Remove default Squarespace DNS records that point to Squarespace servers so we can point to GitHub Pages instead
**Before:** 4 A records pointing to Squarespace IPs (198.185.159.x range), CNAME www → ext-sq.squarespace.com, HTTPS record, _domainconnect CNAME
**After:** Squarespace Defaults section removed. Email Security records (DKIM, DMARC, SPF) preserved.

---

### 2026-03-03 ~22:40:00
**Action:** CREATE
**Target:** Squarespace DNS — coregroupmarketing.com — Custom A Record #1
**Why:** Point apex domain to GitHub Pages server
**Before:** No custom A records existed
**After:** A record: Host=@, Data=185.199.108.153, TTL=4hrs

---

### 2026-03-03 ~22:41:00
**Action:** CREATE
**Target:** Squarespace DNS — coregroupmarketing.com — Custom A Record #2
**Why:** Point apex domain to GitHub Pages server (redundancy)
**Before:** 1 custom A record existed
**After:** A record: Host=@, Data=185.199.109.153, TTL=4hrs

---

### 2026-03-03 ~22:42:00
**Action:** CREATE
**Target:** Squarespace DNS — coregroupmarketing.com — Custom A Record #3
**Why:** Point apex domain to GitHub Pages server (redundancy)
**Before:** 2 custom A records existed
**After:** A record: Host=@, Data=185.199.110.153, TTL=4hrs

---

### 2026-03-03 ~22:43:00
**Action:** CREATE
**Target:** Squarespace DNS — coregroupmarketing.com — Custom A Record #4
**Why:** Point apex domain to GitHub Pages server (redundancy)
**Before:** 3 custom A records existed
**After:** A record: Host=@, Data=185.199.111.153, TTL=4hrs

---

### 2026-03-03 23:05:00
**Action:** CREATE
**Target:** Squarespace DNS — coregroupmarketing.com — Custom CNAME Record
**Why:** Point www subdomain to GitHub Pages so www.coregroupmarketing.com resolves correctly
**Before:** No CNAME record for www
**After:** CNAME record: Host=www, Data=maglio1.github.io, TTL=4hrs

---

### 2026-03-03 23:06:00
**Action:** CONFIG
**Target:** GitHub repo maglio1/The-Core-Group — GitHub Pages Custom Domain
**Why:** Correct the custom domain from thecoregroup.com to coregroupmarketing.com
**Before:** Custom domain was `www.thecoregroup.com`
**After:** Custom domain changed to `www.coregroupmarketing.com`. DNS check successful.

---

### 2026-03-03 23:07:00
**Action:** EDIT
**Target:** /AI_TheCoreGroup/CNAME (local copy)
**Why:** Sync local CNAME file with the corrected domain
**Before:** `www.thecoregroup.com`
**After:** `www.coregroupmarketing.com`

Note: GitHub automatically updated the CNAME file in the repo when the custom domain was saved in Pages settings (commit "Update CNAME" by maglio1).

---

## SESSION SUMMARY — 2026-03-03 23:08:24

- Total changes: 10
- Files created: CNAME (in repo, via GitHub Pages settings auto-commit)
- Files modified: CNAME (local copy updated from thecoregroup.com to coregroupmarketing.com)
- Files deleted: None
- DNS records added in Squarespace for coregroupmarketing.com:
  - 4x A records (@ → GitHub Pages IPs)
  - 1x CNAME record (www → maglio1.github.io)
- DNS records removed from Squarespace: Squarespace Defaults (A records, CNAME, HTTPS, _domainconnect)
- DNS records preserved: Email Security (DKIM, DMARC, SPF)
- GitHub settings changed: Repo visibility (private → public), Pages enabled, custom domain set
- Potential rollback concerns:
  - Repo is now PUBLIC — was previously private. To reverse: Settings > Danger Zone > Change visibility
  - Squarespace default DNS records were deleted — if reverting to Squarespace hosting, you'd need to re-add them or use the "Restore Squarespace Defaults" option
  - HTTPS enforcement not yet enabled — certificate provisioning in progress. Check back in ~30 min to enable.
