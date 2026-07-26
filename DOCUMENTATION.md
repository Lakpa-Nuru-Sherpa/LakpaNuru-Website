# Site structure — how this all fits together

## Folder layout

```
your-repo/
├── index.html        ← About page (this is your homepage)
├── works.html         ← Works page
├── contact.html       ← Contact page
├── css/
│   └── style.css      ← ALL styling lives here — one shared file
├── images/
│   ├── README.txt
│   └── profile-photo.jpg   ← add your own photo here
├── fonts/
│   └── README.txt      ← your handwriting font goes here later
└── DOCUMENTATION.md    ← this file
```

Three pages, one stylesheet. Each `.html` file only contains content —
none of them have their own `<style>` block. That's deliberate: change a
color or font once in `style.css` and it updates on every page.

## How each HTML file is put together

Every page has the same three pieces, in this order:

1. **`<head>`** — page title, the Google Fonts link, and the link to
   `css/style.css`. You generally won't touch this except to change the
   `<title>` per page.
2. **`<header class="site-header">`** — the nav bar with your name and
   the three links. It's copy-pasted at the top of all three files.
   The current page's link has `aria-current="page"` on it, which is
   what gives it the underline — when you copy this header elsewhere,
   move that attribute to match.
3. **`<main>`** — the actual page content. This is the only part that's
   meaningfully different between the three pages.
4. **`<footer class="site-footer">`** — copyright line, same on all pages.

## Where things live in `style.css`

The file is organized top to bottom as:

- **`:root { ... }`** — design tokens. Every color and font used
  anywhere on the site is a variable defined here (e.g. `--accent`,
  `--font-display`). Change the value once here rather than hunting
  through the file for hex codes.
- **`@font-face` (commented out)** — ready to go for your handwriting
  font. See "Adding your handwriting font" below.
- **Reset & base** — default text color, link styles, focus outline,
  heading styles shared by all pages.
- **Layout** — the nav bar, page width, footer.
- **About page**, **Works page**, **Contact page** — one section each,
  clearly labeled with comments, containing only the styles specific to
  that page.

## Editing content

- **About page (`index.html`)**: edit the text inside `<p class="bio">`,
  and change `Who am I?` if you want different wording. Swap the `src`
  on the `<img>` tag if you name your photo something other than
  `profile-photo.jpg`.
- **Works page (`works.html`)**: each project is one `<article
  class="work-card">` block. Copy-paste that whole block to add more
  projects, or delete one to remove a project. Replace the `work-thumb`
  div's text with an `<img>` tag once you have real screenshots.
- **Contact page (`contact.html`)**: each row in the list is one `<li>`
  inside `<ul class="contact-list">`. Edit the `href` and link text, or
  copy a row to add another platform.

## Adding your handwriting font later

When your handwriting font file (usually `.woff2`) is ready:

1. Drop the font file into the `/fonts` folder.
2. In `css/style.css`, find the commented-out `@font-face` block near
   the top and uncomment it.
3. Point its `url(...)` at your file, e.g. `url('../fonts/my-hand.woff2')`.
4. Change the `--font-display` variable (also near the top of the file)
   to your font's name, e.g. `--font-display: 'MyHandwriting', cursive;`

Every `h1`/`h2`/`h3` on every page reads from `--font-display`, so this
one change is enough to re-skin all the headings across the whole site.

## Committing to git

Nothing here is git-specific — just commit the whole folder as-is:

```
git add .
git commit -m "Add personal site: about, works, contact"
git push
```

## A note on the design

The palette is a warm paper background with an ink-dark text color, a
bronze accent for links and labels, and a deep sage for hover states —
defined as `--bg`, `--ink`, `--accent`, and `--accent-deep` in
`style.css`. Headings use Fraunces (a display serif with some
character), body text uses Inter, and small labels use JetBrains Mono
in uppercase with tracked letter-spacing — a common way to add a bit of
"documentation" texture to a personal site without adding more color.

The one flourish is the small hand-drawn underline beneath "Who am I?"
on the About page — a nod to the handwriting font you're planning to
add, so the finished site should feel consistent when it arrives.
