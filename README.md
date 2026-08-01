# Synergy Pictures U.K. — website

Static site. One HTML file, no build step, no dependencies. The crest is embedded
in the HTML as a data URI, so the page renders correctly even with nothing else
uploaded.

---

## Deploy to GitHub Pages

1. Create a new **public** repository on GitHub.
2. Upload **everything in this folder**, keeping the structure intact.
   (`Add file` → `Upload files` → drag the whole contents in → `Commit changes`.)
3. `Settings` → `Pages` → Source: **Deploy from a branch** → Branch: **main** → Folder: **/ (root)** → `Save`.
4. Wait 1–2 minutes. The site is live at `https://<username>.github.io/<repo>/`.

Do not rename `index.html`. GitHub Pages will not serve anything else as the homepage.

### Custom domain (e.g. synergypictures.co.uk)

1. Create a file in the repo root named `CNAME` containing only your domain, e.g. `synergypictures.co.uk`
2. At your DNS provider add four A records for the apex domain pointing to
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   and a CNAME record for `www` pointing to `<username>.github.io`.
3. `Settings` → `Pages` → enter the domain → tick **Enforce HTTPS** once the
   certificate has issued (can take up to 24 hours).

---

## Files

```
index.html          The site. Everything is in here.
.nojekyll           Stops GitHub running Jekyll over the repo. Leave it.
brand/
  og-image.png      Link-preview image (1200x630) for Slack/LinkedIn/iMessage.
  synergy-crest.png Transparent crest, for decks and letterheads.
  synergy-lockup.png Original full lockup on navy.
stills/             Put film stills here. Empty until you add them.
```

---

## Before you go live

### 1. Fix the two share-preview URLs

Open `index.html`, search for `REPLACE-ME`, and set both `og:url` and `og:image`
to your real live address, for example:

```
https://yourname.github.io/synergy-pictures-uk/
https://yourname.github.io/synergy-pictures-uk/brand/og-image.png
```

These must be full absolute URLs. Relative paths do not work for link previews.

### 2. Add real stills

The Pictures section currently shows placeholder panels. For each of the three,
find the `<div class="plate ...">` block, delete the `<span class="plate__ph">`
placeholder inside it, and put an image tag in its place:

```html
<div class="plate plate--scope">
  <img src="stills/still-01.jpg" alt="">
</div>
```

- Lead still: about **2000 x 836 px** (2.39:1, scope)
- The two below: about **1600 x 865 px** (1.85:1, flat)
- Export JPEG at roughly 80% quality. Keep each file under ~400 KB.
- **Lowercase filenames, no spaces.** GitHub Pages is case-sensitive:
  `Still-01.JPG` will 404 where `still-01.jpg` works. This is the most common
  way a Pages site breaks.

### 3. Replace every placeholder

Everything in square brackets is unfilled. Search `index.html` for `[` and work
through the list:

| Placeholder | Where |
|---|---|
| `[00]` x3, `[£000m]` | Ledger strip under the hero |
| `[Film Title]`, `[Name]`, `[Territory]`, `[Year]` | Pictures + Transactions |
| `[Festival selection]`, `[Broadcaster or distributor attached]`, `[Co-production partner]` | Pictures |
| `[A single line of press...]`, `[Publication]` | Press quote |
| `[£0,000,000]` x3 | Tombstones |
| `[£0m to £00m]`, `[£0m]`, `[List active territories.]`, `[Six weeks]`, `[broker]`, `[interim and final]` | Governance |
| `[Street Address]`, `[London, Postcode]`, `[+44 (0)20 0000 0000]` | Footer |
| `[00000000]`, `[Registered Address]` | Footer legal |

Also check the three email addresses (`submissions@`, `distribution@`,
`capital@` at `synergypictures.co.uk`) and the dead `#` links on
LinkedIn / Press / Privacy / Terms / Modern Slavery.

### 4. Two things that are not cosmetic

- **The legal paragraph in the footer is a placeholder and must be settled with
  a U.K. solicitor before publication.** If the site invites or facilitates
  investment, FCA rules on financial promotions may apply to it.
- **The tombstones and the press quote must be real.** They are the credibility
  of the whole page. If you do not yet have transactions you can name, delete
  the Transactions section and the ledger figures rather than inventing them.

---

## Editing notes

- Fonts (Bodoni Moda, Marcellus, Spectral) load from Google Fonts over HTTPS.
- All colour, spacing and type tokens are CSS custom properties in `:root` at the
  top of the `<style>` block. Change the palette there, not further down.
- Motion is disabled automatically for visitors with reduced-motion enabled.
- To remove a whole section, delete its `<section>` block and the matching link
  in the masthead nav and the footer.
