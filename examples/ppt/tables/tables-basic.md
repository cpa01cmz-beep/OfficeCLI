# Basic PPT Tables

Three files work together:

- **tables-basic.sh** — Shell script that calls `officecli` to build the deck.
- **tables-basic.pptx** — The generated 5-slide deck.
- **tables-basic.md** — This file.

## Regenerate

```bash
cd examples/ppt
bash tables-basic.sh
# → tables-basic.pptx
```

## Slides

### Slide 1 — Inline `data=` seed

Whole table populated in a single command with `data="H1,H2;R1C1,R1C2"`
(commas separate cells, semicolons separate rows).

```bash
officecli add file.pptx /slide[1] --type table \
  --prop x=0.5in --prop y=1.2in --prop width=12in --prop height=2in \
  --prop headerFill=4472C4 --prop bodyFill=DEEAF6 \
  --prop data="Region,Q1,Q2,Q3,Q4;North,120,135,142,168;South,98,110,121,140;East,165,178,190,205"
```

> ⚠ `headerFill` / `bodyFill` are a **per-cell stamp** applied at table
> creation, not a table-level property. If you later run `add row` or
> `add column`, the new cells will not auto-color — you have to set
> their `fill` explicitly. Want appended rows/columns to follow the
> coloring automatically? Use a theme style instead:
> `--prop style=medium2 --prop firstRow=true --prop bandedRows=true`.
> See [tables-rows-cols.md](tables-rows-cols.md) for the side-by-side
> comparison.

### Slide 2 — Empty grid + per-cell `set`

Reserve the grid with `rows`/`cols`, then set each cell. Useful when cell
values aren't known up-front, or different cells need different styling.

```bash
officecli add file.pptx /slide[2] --type table \
  --prop rows=4 --prop cols=3 --prop headerFill=2E75B6

officecli set file.pptx /slide[2]/table[1]/tr[1]/tc[1] \
  --prop text="Product" --prop bold=true --prop color=FFFFFF
```

### Slide 3 — Cell fill variations

`fill` (alias `background`/`shd`) accepts several forms:

| Form | Example |
|---|---|
| Solid hex | `fill=FF0000` or `fill=#FF0000` |
| Named color | `fill=red` |
| `rgb(...)` | `fill="rgb(255,0,0)"` |
| Theme color | `fill=accent1` (also `accent2..6`, `dk1`, `dk2`, `lt1`, `lt2`, `hyperlink`) |
| Gradient | `fill="FF0000-0000FF-90"` — `"COLOR1-COLOR2[-ANGLE]"`, angle in degrees |
| No fill | `fill=none` — transparent (page bg shows through) |

Theme colors follow the deck theme — recolor the deck and the table follows.
Hex/named colors are absolute.

### Slide 4 — Cell typography

Text-formatting properties applied directly on a cell (no inner run needed):

| Property | Example | Effect |
|---|---|---|
| `italic=true` | `--prop italic=true` | italic text in cell |
| `underline=single` | `--prop underline=single` | underlined text |
| `strike=single` | `--prop strike=single` | strikethrough |
| `font="Georgia"` | `--prop font="Georgia"` | font face override |
| `wrap=false` | `--prop wrap=false` | disable word-wrap (text clips) |
| `linespacing=1.5x` | `--prop linespacing=1.5x` | paragraph line spacing |
| `spacebefore=4pt` | `--prop spacebefore=4pt` | space above paragraph |
| `spaceafter=4pt` | `--prop spaceafter=4pt` | space below paragraph |

### Slide 5 — Cell layout

Cell-geometry properties:

| Property | Example | Effect |
|---|---|---|
| `padding=0.25in` | `--prop padding=0.25in` | uniform inner margin |
| `padding.bottom=0.3in` | `--prop padding.bottom=0.3in` | bottom edge only |
| `opacity=0.4` | `--prop opacity=0.4` + `fill=...` | fill transparency |
| `image=path` | `--prop image=/img.png` | picture fill (blipFill) |
| `textdirection=vert` | `--prop textdirection=vert` | vertical text |
| `direction=rtl` | `--prop direction=rtl` | RTL paragraph |
| `bevel=circle` | `--prop bevel=circle` | 3D cell bevel (set-only) |
| `border.right=2pt solid E63946` | `--prop border.right=...` | right-edge border |

> `opacity` requires a fill on the same cell. `bevel` is set-only (no Get
> readback — OOXML 3D cell data is write-only from the handler's
> perspective). `id`, `zorder`, and `colWidths` on tables are read-only.

**Features:** `data=` inline seed, `headerFill`/`bodyFill`, `rows`/`cols`,
per-cell `text`/`bold`/`color`/`fill` (solid/named/rgb/theme/gradient/none),
`italic`, `underline`, `strike`, `font`, `wrap`, `linespacing`,
`spacebefore`, `spaceafter`, `padding`, `padding.bottom`, `opacity`,
`image`, `textdirection`, `direction`, `merge.right`, `bevel`,
`border.right`, EMU-parseable dimensions (`0.5in`).
