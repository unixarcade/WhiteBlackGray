# White Black Grey · Symbolmancer Codex

*A self-contained codex of 172 poems — Detroit, 1999–2005 — set in an intricate Art Deco frame and read from a single HTML file with no dependencies, no build step, and no network.*

White Black Grey is a reading instrument for a body of poetry. It is one file. Open it and the whole work is there: every poem, the index, the voice reader, the ornament, the type. Nothing is fetched, nothing is tracked, nothing breaks when the wifi does. It is built to outlast frameworks — the kind of artifact you can drop onto GitHub Pages today and still open, untouched, in twenty years.

---

## The work

One hundred seventy-two poems, written in Detroit between 1999 and 2005, followed by a closing **Thanks** folio — 173 folios in all, roughly fifteen thousand words drawn from a 92-page source manuscript.

Every poem is held twice:

- **Edited** — the reading text, titles and lines cleaned up for the page.
- **Source** — the original manuscript text and title, preserved exactly, reachable with a single toggle.

Each folio also carries a quiet line of metadata — a two-word *mood* ("white flame / tender truth," "black weather / honest descent") and its source page reference — and a spoken rendering used by the voice reader.

The book ends on a deliberate pair. **"Working Girls"** is the author's closing address; **"Thanks"** is the colophon and the archive link. These two folios — and only these two — are touched with gold. Everything before them is white, black, and grey.

---

## Reading it

The codex opens on the first poem. From there:

| Control | What it does |
| --- | --- |
| **Index** | Opens the searchable sidebar of all folios |
| **Search** | Filters the index by title or text across the whole book |
| **All Poems / single** | Switches between one-folio focus and the full continuous read |
| **Source** | Toggles every folio between edited and original manuscript text |
| **Read / Auto Voice** | Reads the current poem aloud; auto-advances through the book |
| **Pace** | Sets reading speed for the voice |
| **Voice picker** | Chooses any voice the browser/OS offers |
| **Back · Next · Random** | Moves through the sequence, or jumps anywhere |
| **Copy Poem** | Copies the current poem's text to the clipboard |
| **Share** | Shares a direct link to the current folio |
| **Motion** | Turns the animated background and verse reveal on or off |

Your view mode, text mode, motion preference, and place in the book are remembered locally between visits.

---

## Design — white, black, grey

The palette is a discipline, not a limitation. The book is monochrome on purpose; the only warmth is the brass `#C9A84C` reserved for the closing pair.

The Art Deco frame is the ornament of the era of the Guardian Building and the Fisher Tower, rebuilt in vector line:

- a **fountain crest** — a sunburst pediment with a tiered obelisk spire — rising behind each title,
- **stepped sunburst corner brackets** in all four corners,
- **fluted pilasters** down the left and right margins,
- a **geometric rosette medallion** at the foot of each folio,
- and a faint geometric field — sunburst, concentric arcs, a lozenge lattice — set far back behind the text.

Every poem opens with an **illuminated drop-cap**, rendered in silver across the book and in gold on the two gold folios. Titles are fitted to their frame so even the longest line ("I Pledge Allegiance to the Anti Humanitarian Xtia League") sits cleanly without clipping, at any width.

---

## Under the hood

- **One file, zero dependencies.** All HTML, CSS, JavaScript, and the full poem data are inlined. No libraries, no fonts to fetch, no API calls.
- **The poems live in the file.** A single `<script type="application/json">` block holds the entire corpus; the page parses it at load and builds every folio from it.
- **Animated background with a fallback.** A WebGL shader paints the moving field; if WebGL is unavailable, a 2D canvas takes over, and if that fails the page is still perfectly readable on a flat background.
- **Voice via the platform.** Reading aloud uses the browser's built-in `speechSynthesis` — no cloud, no key.
- **Preferences in `localStorage`.** View mode, edited/source, motion, and reading position persist locally; nothing leaves the device.
- **Built to degrade gracefully.** The verse-reveal animation is fail-safe by design: lines *rest visible* and animate *from* hidden, so the poetry can never be stranded invisible if motion is reduced, throttled, or unsupported. Turning Motion off, or setting the OS to reduce motion, gives a calm, static read.
- **Responsive.** The layout and ornament scale from wide desktop down to a 390-px phone; the side pilasters step aside on small screens so the verse always has room.

---

## Run it locally

It's a static file. The simplest way:

```
open white_black_grey_symbolmancer_codex.html
```

Or double-click it. That's the whole story for reading.

If you'd rather serve it over `http://` (recommended if you want the voice reader to behave identically across browsers):

```
python3 -m http.server 8000
# then visit http://localhost:8000/white_black_grey_symbolmancer_codex.html
```

No install, no `npm`, no build.

---

## Deploy to GitHub Pages

1. Create a repository and add the HTML file. To have it served at the site root, copy it to `index.html`:
   ```
   cp white_black_grey_symbolmancer_codex.html index.html
   git add index.html && git commit -m "Publish White Black Grey · Symbolmancer Codex"
   git push
   ```
2. In the repo, go to **Settings → Pages**, set **Source** to your default branch (root), and save.
3. Your codex goes live at `https://<username>.github.io/<repo>/`.

Because everything is inlined, there is nothing else to configure. If you update the file, do a hard refresh (or wait out the CDN cache) to see changes.

---

## Editing the codex

All 172 poems and the colophon are stored as a JSON array inside the file, in a `<script id="bookData" type="application/json">` block. Each entry holds its edited and source title, its edited and source text, mood, page references, and word counts.

The data round-trips byte-for-byte, so the safe way to add, fix, or reorder poems is to parse that block, modify the array, and write it back with compact, non-ASCII-preserving serialization. The two gold folios are marked with a `"gold": true` flag; the colophon additionally carries `"kind": "colophon"`. The rendering, ornament, and styling all read from those fields — nothing about a folio's appearance is hard-coded to its position.

---

## Support

If the work means something to you, you can leave a tip:

**CashApp — [$unixarcade](https://cash.app/$unixarcade)**

---

## Archive & colophon

White Black Grey is published under the **Luminosity-e** imprint. The living archive behind it — twenty-five years of public writing — is at:

**[luminosity.livejournal.com](http://www.livejournal.com/users/luminosity)**

*White Black Grey · Symbolmancer Codex · Detroit · 1999–2005*

---

## License

The poems and their text are © Matthew Kowalski. All rights reserved.

You're welcome to read the source of the file, learn from how it's built, and adapt the reader's *code* for your own work; please don't republish the poetry itself without permission. If you reuse the build, a nod back to the archive is appreciated — *be a good neighbor.*
