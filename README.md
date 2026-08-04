# A4RESUME

[![Languages: HTML/CSS/JS](https://img.shields.io/badge/languages-HTML%2FCSS%2FJS-orange.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A4RESUME is a minimalist resume layout tool. Instead of a free-form canvas, every document is a recursive tree of **blocks** arranged as rows or columns. The result prints cleanly to a single A4 page.

## Highlights

- **Single File** — `index.html` is the whole app, no `npm install`, no bundlers, no server.
- **Live Block Tree** — A recursive row/column structure mirrored by a visual sidebar, allowing intuitive navigation and layout control without manual positioning.
- **What You See Is What You Get** — Zero surprises when printing.
- **Local First** — Your data never leaves your machine, persisting safely in localStorage or as JSON files.

## Features

### Document

| Action | Description |
| --- | --- |
| **New** | Clear the canvas and start from empty. |
| **Open** | Import a `.A4R` file. |
| **Save** | Export as a `.A4R` file. |
| **Print** | Send the canvas to the printer. |

### Block

| Action | Description |
| --- | --- |
| **Move Prev/Next** | Reorder the selected block among its siblings. |
| **Add Sub Row** | Convert the selected block into a vertical stack and append a child. |
| **Add Sub Col** | Convert the selected block into a horizontal stack and append a child. |
| **Merge With Prev/Next Sib** | Absorb an adjacent sibling into the selected block. |
| **Image** | Insert an image into a blank leaf. |
| **Remove** | Remove the selected block. |

## Getting Started

**No build step required.**

### Local Usage

Download `index.html` and double-click it to open in any modern browser.

### Hosted Usage

Upload `index.html` to any static host.

## How It Works

Every document element is a `<div class="block">`. A block is one of:

| Type | Marker | Behavior |
| --- | --- | --- |
| **Row Container** | `data-dir="row"` | Children in a **vertical layout** (flex column). |
| **Col Container** | `data-dir="col"` | Children in a **horizontal layout** (flex row). |
| **Leaf block** | *(no `data-dir`)* | A single line (`contenteditable`). |
| **Image block** | `data-img` | Holds a single `<img>`. |

The A4 root is always a row container.

## File Format

`.A4R` files are plain JSON. Each node is either a leaf or a container:

- **Leaf**: `{ "content": "..." }`
- **Container**: `{ "dir": "row" | "col", "children": [...] }`

## Contributing

Contributions are welcome.

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/amazing`).
3. Commit your changes (`git commit -m 'Add amazing feature'`).
4. Push to the branch (`git push origin feature/amazing`).
5. Open a Pull Request.

Please keep it **single-file**.

## License

[MIT](./LICENSE) © Chittle Skuny
