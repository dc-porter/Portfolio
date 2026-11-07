# Portfolio

My technical writing portfolio, built with [Astro](https://astro.build) using a docs-as-code workflow.
Every page is written in Markdown. When a change is merged into `main`, GitHub Actions rebuilds
the site and publishes it to GitHub Pages automatically.

**Live site:** https://deepo333.github.io/Portfolio/

---

## Which file controls which page

Everything you'll normally edit is in the **`content/`** folder (words and images) or the
**`public/files/`** folder (PDFs). You shouldn't need to touch anything in `src/`.

| Page | Address | File to edit |
| --- | --- | --- |
| Your name, email, LinkedIn (shown on every page) | — | `content/settings.md` |
| Docs-as-code samples (the Markdown documents themselves) | shown on their work sample page | `content/docs/<file-name>.md` |
| Home (one file per section, listed below) | `/` | `content/home/` |
| Work Samples hub, including the category names and descriptions | `/work/` | `content/pages/work.md` |
| Each work sample's detail page | `/work/<file-name>/` | `content/work/<file-name>.md` |
| About | `/about/` | `content/pages/about.md` |
| Résumé | `/resume/` | `content/pages/resume.md`, plus the PDF at `public/files/resume.pdf` |
| Contact | `/contact/` | `content/pages/contact.md` |

### The home page, section by section

Each section of the home page has its own file in `content/home/`, in the order they appear:

| Section | File | What you edit there |
| --- | --- | --- |
| Hero | `content/home/intro.md` | The small line above your name, the short intro, and the Download résumé button label. The short intro is also the default link-preview description. Your name and job title come from `content/settings.md` |
| Document-type banner | `content/home/banner.md` | The words in the black band that scrolls under the hero |
| Stats | `content/home/stats.md` | The four numbers under the hero |
| Featured work | `content/home/featured.md` | Section heading, intro, and the three category cards: a sample for each (its category becomes the heading) and one line of text |
| Core capabilities | `content/home/capabilities.md` | Each capability's name, icon, and one-sentence description |
| Tools & technologies | `content/home/tools.md` | Groups of tools (numbered 01, 02, ... automatically), each tool's name and icon |
| My process | `content/home/process.md` | Each step's name and description (numbered automatically) |
| Let's work together | `content/home/closing.md` | Heading, text, and link labels. Email and LinkedIn come from `content/settings.md` |

Your name comes from `content/settings.md` and your photo from `content/pages/about.md`,
so you only set them once.

**Fonts:** your name (in the hero, the top bar, and the footer), the big page titles (Work samples,
About me, Résumé, Contact, and every work sample's title), and the large section headings use
**Abril Fatface**. The line above your name is light Jost in small, widely spaced capitals, sized to
fit on one line on desktop screens (it may wrap on phones). Your title is medium-weight Archivo in
wide capitals. Smaller headings use Marcellus, and all other text, including the intro under your
title, uses Jost.

**Accent words:** put underscores around a word in a title to show it in the accent color, for example
`title: Let’s work _together_`. It uses the same font as the rest of the heading. On the black
"Let's work together" band at the bottom of the home page, every word stays white.

**Type sizes:** every page title, every section heading, every card or step heading, and all body
text each have exactly one size, set once at the top of `src/styles/global.css` (`--text-h1`,
`--text-h2`, `--text-h3`, and `--text-body`). Change a size there and it changes everywhere.

**Icons:** each capability has an `icon:` line. The comment at the top of `capabilities.md` lists
every icon name you can use (for example `procedure`, `form`, `archive`, `edit`, `api`).

**Tool logos:** each tool in `tools.md` sits in a thin outlined box, in its group's color, and shows its
real logo. `logo:` takes a name from [Simple Icons](https://simpleicons.org). `logoFile:` points to a
logo file saved in `public/logos/` (the `README.txt` there lists where each came from: vendor websites
and the vendors' own App Store listings). `logoPlate: dark` gives a logo with white lettering a dark
backdrop, and `logoPlate: app` rounds the corners of an app icon. A tool with none of these shows its
name in the box; Livelink does, because no official logo file was available. To add one, save the file
in `public/logos/` and add a `logoFile` line.

**Colors:** the capability cards take turns using navy, olive, ivory beige, and autumn yellow, at 75% opacity (white text on navy and olive, dark text on the light two). The tool boxes use navy, olive, brown, and mustard as outlines. To change a shade, edit the `--tint-` lines at the top of `src/styles/global.css`.

**Hiding an item:** add `hidden: true` under a capability or a tool to keep it off the site without
deleting it. Delete that line to show it again.

### How a Markdown file is organized

Each file has two parts:

```markdown
---
title: About me            ← The top part, between the --- lines, is "frontmatter":
headshot: ./images/me.jpg     labeled settings, one per line, in the form  label: value
---

I'm a technical writer...  ← Everything below is the page text, written in normal Markdown.
```

Lines in the frontmatter that start with `#` are notes to you. They never appear on the site.
Below the frontmatter, anything between `<!--` and `-->` is also a note to you, and it's removed
before the site is published (it doesn't even appear in the page's source code).

### Motion

The site moves gently, and only where it helps:

Animations play each time something scrolls into view, so they replay when you scroll back to
them or return to a page.

- **Home hero:** the line above your name drops in from the top; your name types out letter by
  letter with a blinking cursor, which blinks a few times and fades away; your title slides in from
  the left; and the intro rises up from below. The Download résumé button doesn't move.
- **Page titles:** About me, Work samples, Résumé, and Contact type out letter by letter with a
  blinking cursor, at the same speed as your name on the home page. The **My process** heading
  slides in from the left while its letters fade in one by one.
- **Core capabilities** and **Tools & technologies** headings, and the **stats**, fade in gently.
- **Other headings, cards, and process steps** fade in and rise into place.
- **Banner:** the black band under the hero scrolls from right to left in an endless loop that
  never pauses. An item takes about 6.7 seconds to cross a phone screen and about 25 seconds to
  cross a wide screen.
- **Back to top:** the button at the end of every page scrolls smoothly back to the top.
- **Hover:** with a mouse or trackpad, cards, tiles, and buttons lift slightly. Touch screens get no
  hover effects.

If a visitor has turned on **Reduce motion** on their device, none of this moves: everything shows
immediately, and the banner is a still row. Only opacity and position change, so nothing on the page
shifts while it loads. In the code, `data-reveal` marks what animates (`data-reveal="fade"` and
`data-reveal="letters"` are the gentler styles) and `--reveal-delay` staggers items in a row (see
`src/styles/global.css`).

### Finding what still needs your input

Every place that needs a fact from you is marked **TODO**. To find them all, search the
repository for `TODO` (on GitHub, press `/` on the repository's main page and type `TODO`), or
open each file in `content/` and look for `# TODO` and `<!-- TODO`. Delete each note once you've
dealt with it.

### Where files go

| What | Where to put it | How to refer to it |
| --- | --- | --- |
| Images for work samples | `content/work/images/` | `./images/my-picture.png` |
| Your headshot (used on Home and About) | `content/pages/images/` | `./images/headshot-new.jpg` |
| PDFs (samples and résumé) | `public/files/` | `/files/my-document.pdf` (use lowercase words joined by hyphens, with no spaces) |

### Linking to other pages

In Markdown, link to another page on your site by starting the address with `/`, for example
`[see my résumé](/resume/)` or `[the declaration procedure](/work/wildfire-season-declaration-procedure/)`.
The site adjusts these links automatically so they work on GitHub Pages.

---

## How to add a new work sample

1. **Add your files.**
   - Put a cover image in `content/work/images/`. A 4:3 shape works best (for example 1200 × 900
     pixels). It appears under the sample's title on its card.
   - If the sample is a PDF, put it in `public/files/`.
   - If the sample is a set of images (like slides), put them in `content/work/images/` too.
2. **Copy the template.** In `content/work/`, make a copy of `_TEMPLATE.md` and rename it.
   Use lowercase words joined by hyphens, like `api-quickstart-guide.md`. The file name becomes the
   page address: `/work/api-quickstart-guide/`.
3. **Fill in the frontmatter.** The template explains every field. The important ones:
   - `category` must match one of the names in `content/pages/work.md` exactly
     (`Procedures`, `Resources`, `Forms`, `Presentations`, or `Docs as Code`).
   - `cover` and `coverAlt` set the card image and its description for screen readers.
   - `pdf`, `markdown`, `images`, and `link` control what appears in **The sample** section. Delete the ones you don't use.
     A PDF appears in a viewer on the page, with **Full screen** and **Download** buttons (see
     "How PDFs appear" below).
   - `draft: true` hides the sample until you're ready.
4. **Write the case study.** Replace the text under the two headings, **Overview** and
   **My approach**. Two to four sentences each is plenty.
5. **Publish it** (see the next section).

The sample appears automatically on the Work Samples page under its category, and its detail page
gets a "Previous / Next" link to the other samples. Samples are listed newest first, based on `date`.

Your eight samples are in `content/work/`. Each one shows its PDF from `public/files/` (or, for the
docs-as-code sample, its Markdown document from `content/docs/`), and its card image is in
`content/work/images/`:

| File | Category | On the home page |
| --- | --- | --- |
| `wildfire-season-declaration-procedure.md` | Procedures | |
| `wildfire-threat-assessment-and-response-procedure.md` | Procedures | Yes |
| `wildfire-season-declaration-form.md` | Forms | Yes |
| `change-request-form.md` | Forms | |
| `technical-writing-review-checklist.md` | Resources | Yes |
| `echodyne-field-brief.md` | Resources | |
| `new-employee-onboarding-windows-setup-guide.md` | Presentations | |
| `stripe-retrieve-balance-reference.md` | Docs as Code | |

**Featured work.** The home page shows three category cards, set in `content/home/featured.md`:
one for Procedures, one for Forms, and one for Resources. Each card shows the category name, one line
of text (`description`), and the cover of the sample you list (`sample`, its file name without
`.md`), and the whole card opens that category on the Work Samples page. To show a different cover,
change the `sample` line. Pick samples from different categories; if two share a category, the build
stops and tells you which ones.

**Card images.** Each card image shows the first page of the sample's PDF on a light background.
To make one for a new PDF, take a screenshot of the PDF's first page and place it on a 1200 × 900
pixel canvas in any image editor, or ask Claude to make one the same way.

To remove a sample, delete its `.md` file and the files it uses in `content/work/images/` and `public/files/`.

### How PDFs appear

- **On computers,** the browser's own PDF viewer is built into the sample page, so visitors can
  scroll, zoom, and search the PDF without leaving it.
- **On phones and tablets,** browsers can't show a PDF inside a page, so each page of the PDF is
  drawn into the sample page instead. Visitors scroll through it in a box on the page.
- **Full screen** opens the PDF in an overlay with a large **Close** button at the top. On phones,
  the Back gesture also closes the overlay instead of leaving the site.
- **Download** saves the PDF. If a browser won't download it (some apps' built-in browsers don't),
  the PDF opens in a new tab, so your site stays open in the original tab.
- On phones, **Back to work samples** and **Home** stay pinned under the top menu while scrolling a
  sample page.

This all happens automatically for any PDF you add. Your résumé page works the same way.

### How docs-as-code samples appear

A docs-as-code sample is a Markdown file in `content/docs/`, kept as plain Markdown so it reads
well on GitHub too. To show one on the site:

1. Put the Markdown file in `content/docs/`, for example `content/docs/my-reference.md`.
2. Add a work sample in `content/work/` (copy `_TEMPLATE.md`) with `category: Docs as Code` and
   `markdown: my-reference` (the file name without `.md`).
3. Add a `link` with the file's GitHub address. It becomes the button in the document's top bar,
   for example **View the Markdown source on GitHub**.

The whole document then appears under **The sample**, in the site's fonts and colors. On phones,
each table row becomes a short stacked block, and long lines in code blocks wrap, so the page never
scrolls sideways. The Stripe sample (`content/docs/stripe-retrieve-balance-reference.md`) works this
way. Its GitHub link points at the `main` branch, so it works once this change is merged.

Any category can be hidden with a `hidden: true` line under it in `content/pages/work.md`. That
hides the category and every sample in it.

---

## How publishing works

1. Make your changes on a new branch (in the GitHub website, choose **Create a new branch** when you commit).
2. Open a **pull request** into `main`. GitHub Actions builds the site to check for mistakes. A green
   check means the build succeeded; a red X means something needs fixing (see below).
3. **Merge** the pull request. About a minute later, the live site is updated.

You can also commit directly to `main` for quick fixes. The site publishes the same way.

You can watch progress on the repository's **Actions** tab. To republish without changing anything,
open **Actions → Build and publish site → Run workflow**.

The finished website is stored on a branch called `gh-pages`, which GitHub Pages serves. The workflow
regenerates that branch on every publish, so never edit it by hand. All your work happens on `main`.

### If the build fails

Open the failed run on the **Actions** tab and read the error. The site checks your content before
publishing, so most errors name the file and the problem, for example:

- `content/work/my-sample.md has category "Procedure"...`: the category doesn't match the list
  in `content/pages/work.md`. Check the spelling, including capital letters.
- `...links to "/files/report.pdf", but there is no file at public/files/report.pdf`: the PDF
  is missing or its name is spelled differently.
- `Could not find requested image ./images/cover.png`: the image is missing from the `images` folder,
  or its name is spelled differently.
- `title: Required` (or another field name): a required field is missing from the frontmatter.
- `items.0.icon: Invalid option: expected one of "procedure"|"form"|...`: an icon name is misspelled.
  Use one of the listed names. Items are counted from 0, so `items.0` is the first item in the list.

Because the build stops on errors, a mistake never reaches your live site. The last good version stays up.

---

## Common changes

- **Change your name, email, or LinkedIn:** edit `content/settings.md`.
- **Show the footer's "Site source on GitHub" link again:** in `content/settings.md`, delete the `#` at
  the start of the `sourceCode:` line.
- **Change your name or job title:** edit `name` and `role` in `content/settings.md`. They appear in the home page hero, the footer, and browser tabs.
- **Change a link preview:** when a page is shared on LinkedIn, Slack, or X, the preview shows the
  page's title, its `description` line (each file in `content/pages/`; a work sample uses its
  `summary`), and the image `public/og-image.jpg` (1200 × 630: your headshot, name, and title). Pages
  without a description use the short intro from `content/home/intro.md`. To change the image,
  replace `public/og-image.jpg` with another 1200 × 630 JPEG of the same name.
- **Favicon:** the "DP" monogram in the browser tab (Abril Fatface, black on light beige) is
  `public/favicon.svg`, with `favicon.ico`, `favicon-16x16.png`, `favicon-32x32.png`,
  `apple-touch-icon.png` (180 × 180, for iPhone home screens), and `icon-192.png` / `icon-512.png`
  (listed in `site.webmanifest`) next to it.
- **Change the line above your name, the intro, or the button:** edit `content/home/intro.md`. To add a
  second button that opens your Work Samples page, follow the note at the bottom of that file's settings.
- **Change the scrolling banner:** edit the `items` list in `content/home/banner.md`. To change its
  speed, edit `PHONE` and `WIDE` near the top of the script in `src/components/Marquee.astro`
  (the seconds an item takes to cross the screen).
- **Change the stats:** in `content/home/stats.md`, edit each `value` (keep the quotes, for example
  `"150+"`) and `label`. To mark a number you haven't confirmed yet, add `placeholder: true` under it,
  and a "Placeholder" tag appears next to it.
- **Add, remove, or reorder capabilities, tools, or process steps:** edit the list in the matching
  file in `content/home/`. Copy an existing item (all of its lines, starting with `- name:`) to add one.
- **Add a tool or a tool group:** in `content/home/tools.md`, copy a tool (its `- name:` and `icon:`
  lines) inside a group's `items:` list, or copy a whole group (from `- name:` through its tools).
- **Replace your résumé:** upload your new PDF to `public/files/` as `resume.pdf`, replacing the old one.
- **Change your headshot:** replace `content/pages/images/headshot-new.jpg` with your new photo,
  keeping the same file name. It appears on the Home and About pages. Its left edge fades into the
  grey set by `--hero-bg` at the top of `src/styles/global.css`, so if your new photo has a different
  background color, change `--hero-bg` to match it. A photo with a plain, light background and some
  space beside you works best. (Your earlier photos, `headshot.jpg` and the cutout
  `headshot-cutout.png`, are still in the same folder but aren't used. To switch back to one, change
  `headshot:` in `content/pages/about.md`.)
- **Change the colors:** edit the lines at the top of `src/styles/global.css`. Each line gives the
  light-mode color first and the dark-mode color second, for example
  `--ink: light-dark(#0d0d0d, #f5f4f1);` for the near-black text and buttons. `--hero-bg` is the grey
  behind your photo on the Home and About pages; it matches the photo's studio background. The
  `--tint-` lines set the soft colors of the capability boxes and tool tiles.
- **Change the top navigation:** edit the `links` list in `src/components/Header.astro`.
- **Turn on private visitor analytics:** see [Visitor analytics](#visitor-analytics) below.

### Visitor analytics

The site can count visits with [GoatCounter](https://www.goatcounter.com), which is free for personal
sites, uses no cookies, and doesn't track people across sites. Nothing shows on the public site:
only you see the numbers, on your GoatCounter dashboard.

1. Sign up at goatcounter.com and choose a site code, for example `dairyia`. Your dashboard is then
   at `https://dairyia.goatcounter.com`.
2. In `content/settings.md`, find the `# goatcounter: your-code` line. Delete the `#` and the space
   after it, and replace `your-code` with your site code: `goatcounter: dairyia`.
3. Commit the change. Once the site republishes, visits appear on your dashboard within a minute or so.

To turn analytics off again, put the `#` back at the start of the line.

### Renaming the repository

The site's address follows the repository's name (the repository is currently named `Portfolio`,
so the site is at `https://deepo333.github.io/Portfolio/`). To rename it again:

1. On GitHub, open **Settings → General**, change **Repository name**, and select **Rename**.
2. Open **Actions → Build and publish site → Run workflow** to republish at the new address:
   `https://deepo333.github.io/<new-name>/`. Capital letters in the name matter in the address.
3. Update the old address where it appears: the **Live site** line at the top of this file,
   and `sourceCode` in `content/settings.md` (it's turned off for now; see the note there).

---

## Preview the site on your computer (optional)

You don't need this to publish, but it lets you see changes before pushing them.

1. Install [Node.js](https://nodejs.org) version 24 (the "LTS" version).
2. In a terminal, open this folder and run `npm install` (only needed once).
3. Run `npm run dev`, then open http://localhost:4321 in your browser.
   The page refreshes automatically as you save files. Press `Ctrl + C` to stop.

---

## Behind the scenes

| File or folder | What it does |
| --- | --- |
| `src/pages/` | One template per page type. `src/pages/work/[id].astro` is the work sample detail template. |
| `src/components/` | Reusable pieces: header, footer (email and LinkedIn only), the "Back" link bar, sample cards, the two-column photo section, the scrolling banner (`Marquee.astro`), the typewriter text (`Typewriter.astro`), the "Back to top" button (`BackToTop.astro`), the black category bar on the Work Samples page, accent words, icons, and the PDF viewer (which uses PDF.js to draw PDFs on phones). |
| `src/lib/icons.ts` | The thin-line icons you can pick with `icon:` in Markdown. |
| `src/styles/global.css` | Colors, the type scale, fonts (Abril Fatface for your name, page and sample titles, and home section headings, Archivo for your title, the stats, the process step numbers, the banner, and the category bar, Marcellus for smaller headings, Jost for text, Bodoni Moda italic for accent words), animations, spacing, and light/dark mode. |
| `src/lib/logos.ts` | Looks up tool logos from Simple Icons by name. |
| `src/content.config.ts` | The list of fields each Markdown file can have, and which are required. |
| `src/lib/content.ts` | Loads the content, leaves out drafts and hidden categories, and produces the friendly error messages. |
| `src/plugins/` | Small Markdown helpers: one fixes links for GitHub Pages, the other removes `<!-- notes -->` before publishing. |
| `.github/workflows/deploy.yml` | The GitHub Actions workflow that builds and publishes the site. |
| `astro.config.mjs` | Astro settings. The site's address is filled in automatically during publishing. |
