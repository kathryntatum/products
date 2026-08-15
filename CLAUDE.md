# CLAUDE.md

Context for this project. Read before making changes.

## What this is

A personal, public page of beauty products the owner has actually tried — not a wishlist, not
sponsored content. Two views of the same data: a free-position **Shelf** canvas and an ordered
**Ranking** list. Hosted on GitHub Pages at `github.com/kathryntatum/products`.

It is deliberately a small static site. No build step, no framework tooling, no package.json.
React and Babel load from CDN at runtime. Keep it that way unless asked — the whole point is that
a non-developer can edit one JSON file in GitHub's web UI and the site updates.

## Files

- `index.html` — the entire app. Styles, markup, and React components in one file.
- `products.json` — all content and layout. The only file edited day to day.
- `README.md` — end-user setup and update instructions.

## Data schema

Top level: `title`, `intro`, `handle`, `updated`, `items`.

Each item in `items`:

| field | notes |
|---|---|
| `id` | unique string |
| `name` | product name |
| `brand` | rendered small, above the name |
| `category` | Skincare, Makeup, Hair, Body, Fragrance, Tools, Other |
| `color` | hex for the swatch spine |
| `rating` | 1–5 |
| `verdict` | `yes` / `maybe` / `no` — would buy again |
| `note` | optional short opinion |
| `link` | optional URL |
| `image` | optional photo URL, rendered as a full-width photo (190px tall) across the top of the card |
| `x`, `y` | pixel position on the Shelf canvas |

**Array order is the ranking order.** It also drives the mobile layout.

## Design system

Do not restyle without being asked. These tokens are deliberate:

```
--ink        #191C24   text
--ink-soft   #5A6070   secondary text
--field      #D6DBD2   page background (sage grey)
--field-deep #C4CABE   canvas background
--paper      #FCFBF8   cards
--mulberry   #77384F   accent, ratings, "buy again"
--brass      #A8863F   "maybe"
```

Type: Iowan Old Style / Palatino serif stack for display, system sans for body, monospace for all
labels, data, and small caps. The monospace-for-metadata treatment is intentional — it frames the
page as a trial log rather than a shop.

**The signature element is the swatch spine**: the colored bar down the left edge of every card.
Zoomed out, the shelf reads as a palette before it reads as text. This is the one memorable thing.
Don't dilute it by adding competing color elsewhere.

**Product photos (`image` field) were added deliberately, Aug 2026, at the owner's request.**
Started as a small 52px thumbnail to protect the spine as the dominant color signal, then the
owner explicitly asked for the photo to be the majority of the card and the title to shrink — so
now it is full-width card art (190px) with a smaller title beneath. The spine still runs the full
height of the card as a persistent accent, but it's no longer the dominant visual on cards that
have a photo. Don't re-shrink the photo back down without being asked; that was a deliberate,
two-step decision, not an accident.

## Decisions already made — don't silently reverse these

- **Rating and verdict are separate fields.** Liking something and rebuying it diverge, and the gap
  is the interesting part. Don't collapse them into one score.
- **Below 760px the canvas becomes a stacked grid.** Free positioning is unusable on a phone. Mobile
  uses array order, which is why ranking order must stay sensible even when the shelf is the
  primary view.
- **`?edit` unlocks the editing UI**, stores drafts in `localStorage`, and publishes via a
  "Copy products.json" button. It is *not* security and was never meant to be — it hides the UI,
  nothing more. Don't build auth on top of it; repo access is the real control.
- **View-only by default.** Visitors cannot drag, edit, or reorder.
- **Public page is served from `products.json`**, never from `localStorage`. A visitor must see the
  owner's arrangement, not an empty shelf.

## Content workflow

Source data lives in a **private Pinterest board** ("Tried" section). Pinterest cannot be accessed
programmatically — no connector exists, and Pinterest blocks automated fetching at the site level,
public boards included. So content moves by hand: the owner screenshots the board, and those
screenshots are transcribed into `products.json` entries.

If asked to "sync from Pinterest" or "pull the latest pins," the answer is that it isn't possible.
Ask for screenshots.

## Deployment

GitHub Pages, `main` branch, root. Live at `kathryntatum.github.io/products`.
Files must stay at repo root — Pages serves them relative to the site root, and `index.html`
fetches `products.json` as a sibling.

Local preview requires a server (`python3 -m http.server`); opening `index.html` via `file://`
fails because browsers block the fetch.

## Not yet decided

- Whether to attach affiliate links. If they're added, the hardcoded footer line
  "Nothing here is sponsored" must be replaced with a proper FTC disclosure.
- Whether to point a custom domain at the site. The current URL contains the owner's legal
  surname, which differs from the public creator handle.
