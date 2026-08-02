# A4RESUME

> A zero-dependency, single-file block-based resume editor that runs entirely in your browser.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Made with HTML](https://img.shields.io/badge/Made%20with-HTML/CSS/JS-orange.svg)](https://developer.mozilla.org/)
[![No Build](https://img.shields.io/badge/No%20Build-Step-blue.svg)](#)
[![Single File](https://img.shields.io/badge/Single%20File-~50KB-green.svg)](#)

A4RESUME is a minimalist resume layout tool inspired by the mental model of a structured document. Instead of a free-form canvas, every document is a recursive tree of **blocks** arranged as rows (vertical stacks) or columns (horizontal strips). The result prints cleanly to a single A4 page — no runtime, no backend, no tracking.

---

## Highlights

- **Single file, zero install** — `index.html` is the whole app. No bundlers, no `npm install`, no server. Open it in a browser and start typing.
- **Block tree model** — Documents are a hierarchy of row/column containers and leaf text blocks. Recursion gives you any layout without manual positioning.
- **Live tree view** — A sidebar mirrors the document structure, letting you navigate and understand nesting at a glance.
- **Print-perfect** — WYSIWYG editing on an A4 canvas; what you see is what prints.
- **Local-first** — Data persists to `localStorage`; export/import as `.a4r` (JSON) files. Your data never leaves your machine.
- **Keyboard-friendly text formatting** — Bold, italic, underline, font family, size, and color — all preserved as inline styles.

---

## Features

### Document operations

| Action | Description |
| --- | --- |
| **New** | Clear the canvas and start from a single empty block. |
| **Open** | Import a `.a4r` / `.json` file. |
| **Save** | Export the current document as a timestamped `.a4r` file. |
| **Print** | Send the A4 canvas to the printer or "Save as PDF". |

### Block structure

| Action | Description |
| --- | --- |
| **Move prev / next** | Reorder the selected block among its siblings. Icons adapt to the parent direction (↑↓ for vertical layouts, ←→ for horizontal). |
| **Add sub row** | Convert the selected block into a vertical stack and append a child. |
| **Add sub col** | Convert the selected block into a horizontal row and append a child. |
| **Merge with prev / next sibling** | Absorb an adjacent sibling into the selected block. |
| **Remove** | Delete the selected block. |
| **Image** | Insert an image into an empty block. |

### Block formatting

- Border styles: none / all / top / bottom / left / right
- Background color picker

### Text formatting (leaf blocks only)

- Font family: IBM Plex Sans / Serif / Mono
- Font size: 10 / 12 / 14 / 16 / 18 / 20 px
- **B**old, *I*talic, <u>U</u>nderline
- Text color picker

---

## Getting Started

### Run locally

No build step required.

1. Download `index.html`.
2. Double-click to open it in any modern browser.
3. Start building your resume.

That's it.

### Run as a hosted page

Upload `index.html` to any static host (GitHub Pages, Netlify, Cloudflare Pages, etc.). Because the app is a single self-contained file, there is nothing else to deploy.

---

## How It Works

### The block model

Every document element is a `<div class="block">`. A block is one of:

| Type | Marker | Behavior |
| --- | --- | --- |
| **Row container** | `data-dir="row"` | Children stack **vertically** (flex column). |
| **Column container** | `data-dir="col"` | Children sit **side by side** (flex row, equal width). |
| **Leaf block** | *(no `data-dir`)* | A single line of editable text (`contenteditable`). |
| **Image block** | `data-img` | Holds a single `<img>`. |

The A4 root is always a row container, so top-level blocks stack vertically by default.

### Why rows stack vertically

The naming follows the **child role**, not the flex axis: a `row` container's children each occupy one *row* of the stack, so they pile up. A `col` container's children each become one *column*, so they sit abreast.

### Persistence

- Editing auto-saves to `localStorage` under a versioned key (`a4resume_data_vX`), so schema changes won't corrupt older sessions.
- The **Save** button exports a portable `.a4r` file (JSON), named with a `yyMMdd_hhmmss` timestamp.

---

## File Format

`.a4r` files are plain JSON. Each node is either a leaf or a container:

```json
{
  "dir": "row",
  "children": [
    { "content": "Jane Doe" },
    {
      "dir": "col",
      "children": [
        { "content": "Experience" },
        { "content": "Education" }
      ]
    }
  ]
}
```

- **Leaf**: `{ "content": "..." }`
- **Container**: `{ "dir": "row" | "col", "children": [...] }`

Format attributes (`border`, `bg`, inline text styles) are preserved on the corresponding nodes.

---

## Project Structure

```
a4resume/
├── index.html   # the entire application (markup, styles, logic)
├── LICENSE
└── README.md
```

That's the whole project — by design.

---

## Browser Support

Tested on the latest versions of Chrome, Edge, and Firefox. Uses only stable web platform features (`contenteditable`, Flexbox, `localStorage`, File API).

---

## Contributing

Contributions are welcome. The codebase is intentionally small and self-contained; please keep new features aligned with the single-file, zero-dependency philosophy.

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/amazing`).
3. Commit your changes (`git commit -m 'Add amazing feature'`).
4. Push to the branch (`git push origin feature/amazing`).
5. Open a Pull Request.

Please avoid introducing build tooling, external dependencies, or backend services.

---

## License

[MIT](./LICENSE) © Chittle Skuny
