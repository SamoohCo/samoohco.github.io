# /samooh-new — Add a New Samooh Member

You are adding a new member to samooh.com. Follow these steps precisely.

---

## Step 1: Gather Member Info

If the user hasn't provided all of the following, ask for them before proceeding:

- **Full name** (e.g. "Ankit Kumar")
- **Slug** — the URL slug / first name used for their profile (e.g. "ankit")
- **Photo filename** — confirm the PNG is already at `assets/images/members/{firstname}-{lastname}.png`
- **Role line** — their current title/role in the Samooh style: `Current Role/Title · Context (ex-Company or Org)`. Examples:
  - `Solo Builder, Consumer Crypto · ex-Growth, Buy Me a Coffee`
  - `Founding Team (Product), Stealth Startup · ex-Head of Product, Simpl`
- **Raw blurb** — 1–3 sentences from the user about this person (can be rough/notes)
- **Links** — any subset of: Twitter/X URL, personal website URL, LinkedIn URL

---

## Step 2: Draft the Bio

Using the raw blurb, write a bio in Samooh's voice. **Show this to the user for approval before making any file changes.**

**Bio rules:**
- 2–3 sentences, 70–100 words total
- Third person ("Ankit is…", "She previously…")
- Sentence 1: current work/focus + location or key context
- Sentence 2: notable past experience with **specific company names** (not vague)
- Sentence 3 (optional): scale, achievement, or interesting detail that makes them memorable
- Tone: warm, specific, confident — not hype, no jargon, no buzzwords
- Em-dash ( — ) for asides when needed, just like existing bios

**Reference bios (match this voice):**
> Ankit is a solo builder based in Bangalore, currently building in consumer crypto. He previously led growth at Buy Me a Coffee and was part of the founding team at Gigabrain. He also ships small tools on the side — his projects have collectively been used by over a million people.

> Vidyadhar is a full-stack builder currently on the founding product team at a stealth startup — imagining what AI-native professional networking could look like. He previously led consumer product at Simpl, India's largest BNPL app. He's been building startups since 2012.

**Also draft:**
- A short **gallery role** (shown on hover in community grid): concise, 4–8 words, e.g. `Solo Builder, Consumer Crypto · ex-Buy Me a Coffee`
- A short **tagline** (shown in homepage list): slightly expanded, e.g. `Solo Builder, Consumer Crypto · ex-Buy Me a Coffee`
- An **llms.txt line**: one flowing sentence compressing the full bio. Format: `- **Full Name** — [sentence]. https://samooh.com/{slug}`
- A **meta description sentence**: first sentence of the bio, used in `<meta name="description">` tag

Present all of these to the user and wait for approval or edits before proceeding.

---

## Step 3: Determine Current Member Count

Read `llms.txt` to find the current member count (look for "Samooh currently has X members"). The new member will be number X+1. Use this for all count updates and for the new member's index number (`{count+1}` zero-padded to 2 digits, e.g. "28").

---

## Step 4: Make All File Changes

Once the user approves the bio, make ALL of the following changes. Do them all before committing.

### 4a. Create `{slug}/index.html`

Create the directory and file. Use this exact template — replace all `{PLACEHOLDER}` values:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{FULL_NAME} — Samooh</title>
  <meta name="description" content="{META_DESCRIPTION} A member of Samooh — the community for Indian founders building global products.">
  <meta property="og:title" content="{FULL_NAME} — Samooh">
  <meta property="og:description" content="{ROLE_LINE}">
  <meta property="og:url" content="https://samooh.com/{SLUG}">
  <meta property="og:type" content="profile">
  <meta name="twitter:card" content="summary">
  <meta name="twitter:site" content="@samoohco">
  <link rel="canonical" href="https://samooh.com/{SLUG}">
  <link rel="icon" type="image/png" href="/assets/images/favicon.png">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Hind:wght@400;600;700&family=PT+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Inconsolata:wght@400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="/assets/css/shared.css">
  <meta name="robots" content="index, follow">
  <meta property="og:image" content="https://samooh.com/assets/images/members/{FIRSTNAME}-{LASTNAME}.png">
  <!-- Google Analytics -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=G-M98ZNZMY9S"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-M98ZNZMY9S');
  </script>
  <!-- Structured Data -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@graph": [
      {
        "@type": "Person",
        "@id": "https://samooh.com/{SLUG}#person",
        "name": "{FULL_NAME}",
        "jobTitle": "{ROLE_LINE}",
        "image": "https://samooh.com/assets/images/members/{FIRSTNAME}-{LASTNAME}.png",
        "url": "https://samooh.com/{SLUG}",
        "memberOf": { "@id": "https://samooh.com/#organization" },
        "sameAs": [
          {SAMES_AS_ARRAY}
        ]
      },
      {
        "@type": "ProfilePage",
        "@id": "https://samooh.com/{SLUG}#webpage",
        "url": "https://samooh.com/{SLUG}",
        "name": "{FULL_NAME} — Samooh",
        "description": "{ROLE_LINE}",
        "isPartOf": { "@id": "https://samooh.com/#website" },
        "about": { "@id": "https://samooh.com/{SLUG}#person" },
        "mainEntity": { "@id": "https://samooh.com/{SLUG}#person" },
        "breadcrumb": {
          "@type": "BreadcrumbList",
          "itemListElement": [
            { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://samooh.com" },
            { "@type": "ListItem", "position": 2, "name": "Community", "item": "https://samooh.com/community" },
            { "@type": "ListItem", "position": 3, "name": "{FULL_NAME}", "item": "https://samooh.com/{SLUG}" }
          ]
        }
      }
    ]
  }
  </script>
</head>
<body>
  <nav class="nav" role="navigation">
    <a href="/" class="nav-logo">Samooh <span class="nav-logo-devanagari">समूह</span></a>
    <div class="nav-items">
      <a href="/#about" class="nav-link">About</a>
      <a href="/community" class="nav-link">Community</a>
      <a href="/#apply" class="nav-apply">Apply to Join</a>
    </div>
  </nav>

  <main>
    <div class="profile-page" itemscope itemtype="https://schema.org/Person">
      <a href="/community" class="back-link">← Community</a>

      <div class="member-header">
        <div class="member-header-text">
          <h1 class="member-name" itemprop="name">{FULL_NAME}</h1>
          <p class="member-role" itemprop="jobTitle">{ROLE_LINE}</p>
        </div>
        <div class="member-photo">
          <img src="/assets/images/members/{FIRSTNAME}-{LASTNAME}.png" alt="{FULL_NAME}" itemprop="image">
        </div>
      </div>

      <div class="member-divider"></div>

      <p class="member-bio" itemprop="description">
        {BIO}
      </p>

      <span class="links-label">Links</span>
      <div class="link-row">
        {LINK_BUTTONS}
      </div>
    </div>
  </main>

  <footer class="footer-wrap" role="contentinfo">
    <div class="footer">
      <div class="footer-left">
        <span class="footer-wordmark">Samooh · समूह</span>
        <span class="footer-sub">Indian founders building global products</span>
      </div>
      <nav class="footer-links" aria-label="Footer">
        <a href="https://x.com/samoohco" target="_blank" rel="noopener" class="footer-link">Twitter</a>
        <a href="https://linkedin.com/company/SamoohCo" target="_blank" rel="noopener" class="footer-link">LinkedIn</a>
        <a href="/#about" class="footer-link">About</a>
        <a href="/community" class="footer-link">Community</a>
        <a href="/#apply" class="footer-link">Apply</a>
      </nav>
    </div>
  </footer>
</body>
</html>
```

For `{LINK_BUTTONS}`: the **first** link gets `class="link-btn primary"`, all others get `class="link-btn"`. Twitter link text is "Twitter", website is "Website", LinkedIn is "LinkedIn". All links get `target="_blank" rel="noopener"`.

For `{SAMES_AS_ARRAY}`: comma-separated JSON strings of each link URL, no trailing comma on last item.

### 4b. Update `index.html`

**Update the community count** (line ~591):
```html
<div class="community-count" aria-hidden="true">{NEW_COUNT}</div>
```

**Append a new member row** inside `.member-list`, after the last `</a>` before `</div>` (the closing of `.member-list`):
```html
          <a href="/{SLUG}" class="member-row" role="listitem">
            <span class="member-idx">{INDEX_PADDED}</span>
            <div class="member-info">
              <span class="member-name-text">{FULL_NAME}</span>
              <span class="member-tagline">{TAGLINE}</span>
            </div>
            <span class="member-arrow" aria-hidden="true">→</span>
          </a>
```

Where `{INDEX_PADDED}` is the new count zero-padded to 2 digits (e.g. "28").

### 4c. Update `community/index.html`

**Update meta description** (line ~7):
```html
  <meta name="description" content="Meet the Samooh community — {NEW_COUNT} Indian-origin founders, makers, and builders working on global products.">
```

**Update og:description** (line ~9):
```html
  <meta property="og:description" content="{NEW_COUNT} Indian-origin founders, makers, and builders working on global products.">
```

**Update schema CollectionPage description** (line ~208):
```
"description": "Meet the Samooh community — {NEW_COUNT} Indian-origin founders, makers, and builders working on global products.",
```

**Update ItemList description and numberOfItems** (lines ~221-222):
```
"description": "{NEW_COUNT} Indian-origin founders, makers, and builders working on global products.",
"numberOfItems": {NEW_COUNT},
```

**Append to itemListElement** (after the last `{ "@type": "ListItem", ... }` entry before the closing `]`):
```
          { "@type": "ListItem", "position": {NEW_COUNT}, "url": "https://samooh.com/{SLUG}", "name": "{FULL_NAME}" }
```

**Update member count display** (line ~278):
```html
        <span class="member-count">{NEW_COUNT} members</span>
```

**Append gallery cell** inside `.gallery-grid`, after the last `</div>` closing a `.gallery-cell` before `</div>` (the closing of `.gallery-grid`):
```html

        <div class="gallery-cell">
          <a href="/{SLUG}">
            <img src="/assets/images/members/{FIRSTNAME}-{LASTNAME}.png" alt="{FULL_NAME}" loading="lazy">
            <div class="gallery-overlay">
              <span class="gallery-member-name">{FULL_NAME}</span>
              <span class="gallery-member-role">{GALLERY_ROLE}</span>
            </div>
          </a>
        </div>
```

### 4d. Update `sitemap.xml`

Add a new entry before the closing `</urlset>` tag:

```xml

  <url>
    <loc>https://samooh.com/{SLUG}</loc>
    <changefreq>monthly</changefreq>
    <priority>0.7</priority>
  </url>

```

### 4e. Update `llms.txt`

**Update the count line** (e.g. "Samooh currently has 27 members." → "Samooh currently has 28 members.")

**Append to the Full Member List** (after the last `- **Name** —` line):
```
- {LLMS_LINE}
```

---

## Step 5: Commit and Push

After all files are saved, run:

```
git add {slug}/index.html index.html community/index.html sitemap.xml llms.txt assets/images/members/{FIRSTNAME}-{LASTNAME}.png
git commit -m "Add {FULL_NAME} as new member"
git push
```

Confirm success and tell the user the profile will be live at `https://samooh.com/{slug}` within ~60 seconds (GitHub Pages deploy time).
