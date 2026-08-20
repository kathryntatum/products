# Tried

A public page of products I've actually used, arranged spatially rather than listed.

## Files

- `index.html` — the site. View-only by default.
- `products.json` — all the data. This is the only file you edit day to day.

## Publishing

1. Create a **public** repo (Pages needs public on the free tier).
2. Upload `index.html` and `products.json` to the root.
3. Settings → Pages → Source: **Deploy from a branch** → `main` / `root` → Save.
4. Wait about a minute. Your URL is `https://<username>.github.io/<repo>/`.

## Updating

Two ways, pick whichever you prefer.

**Edit in the browser (easier for rearranging)**
1. Open your live URL with `?edit` on the end — e.g. `https://you.github.io/tried/?edit`
2. Add, edit, delete, drag cards around, reorder the ranking. Changes save in your browser only; the public page is untouched.
3. Click **Copy products.json**.
4. In GitHub, open `products.json` → pencil icon → select all → paste → Commit.

**Edit the JSON directly (easier for small fixes)**

Open `products.json` in GitHub and edit it. Fields per product:

| field | what it does |
|---|---|
| `name` | product name |
| `brand` | shown small above the name |
| `category` | one of Skincare, Makeup, Hair, Body, Fragrance, Tools, Other |
| `color` | the swatch spine, any hex |
| `rating` | 1–5 |
| `verdict` | `yes` / `maybe` / `no` — would you buy it again |
| `note` | optional short opinion |
| `shade` | optional shade/color name, shown next to the brand |
| `link` | optional URL; shows a "Look" link |
| `amazonLink` | optional Amazon URL; shows an "Amazon" link next to "Look" |
| `image` | optional photo URL; shown across the top of the card, sized to the photo's own proportions |
| `x`, `y` | position on the shelf, in pixels |

The top-level `title`, `intro`, `handle`, and `updated` fields control the header and footer.

## Notes

- Order in the `items` array is the ranking order.
- Below 760px the shelf falls back to a stacked grid, since a free canvas isn't usable on a phone. Ranking order drives that layout, so keep it sensible.
- Opening `index.html` directly from your desktop won't work — browsers block reading `products.json` from `file://`. Run `python3 -m http.server` in the folder to preview locally, or just push and check the live URL.
- `?edit` isn't a password. It hides the editing UI from casual visitors, nothing more. The real protection is that nobody can change your site without repo access.
