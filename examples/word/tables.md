# tables

Generates Word, Excel, and PowerPoint table documents exercising every supported table property.

See [tables.sh](tables.sh) and [tables.docx](tables.docx).

## Properties demonstrated (Word / docx)

### table

| Key | Op | Notes |
|-----|----|-------|
| `cols` | add/get | Column count |
| `rows` | add/get | Row count |
| `width` | add/set/get | Table width (twips, cm, %, etc.) |
| `style` | add/set/get | Table style name (`medium1`..`dark2`, `none`, or GUID) |
| `align` | add/set/get | `left` \| `center` \| `right` |
| `indent` | add/set/get | Table indent in twips |
| `cellSpacing` | add/set/get | Space between cells in twips |
| `layout` | add/set/get | `fixed` \| `autofit` |
| `padding` | add/set | Default cell padding (all sides) in twips |
| `direction` | add/set/get | `rtl` writes `<w:bidiVisual/>` (mirrors column order) |
| `colWidths` | add/get | Comma-separated per-column widths in twips |
| `border.all` | add/set | All six edges shorthand; format `STYLE;SIZE;COLOR` (docx) |
| `border.top` | add/set | Outer top border |
| `border.bottom` | add/set | Outer bottom border |
| `border.left` | add/set | Outer left border |
| `border.right` | add/set | Outer right border |
| `border.horizontal` | add/set | Inside-horizontal dividers (between rows) |
| `border.vertical` | add/set | Inside-vertical dividers (between columns) |

> **Skipped**: `data` — produces `UNSUPPORTED` warning in the current binary despite being listed in schema; functional but not warning-clean.

### table-row

| Key | Op | Notes |
|-----|----|-------|
| `height` | add/set/get | Row height (AtLeast rule) |
| `height.exact` | add/set | Row height (Exact rule, cannot grow); readback via `height` + `height.rule=exact` |
| `header` | add/set/get | Repeat row as table header on every page |

### table-cell

| Key | Op | Notes |
|-----|----|-------|
| `text` | add/set/get | Cell text content |
| `width` | add/set/get | Cell width in twips |
| `fill` | add/set/get | Cell background color |
| `align` | set/get | Horizontal text alignment |
| `valign` | set/get | Vertical cell alignment |
| `font` | set/get | Font family for all runs in cell |
| `size` | set/get | Font size for all runs in cell |
| `bold` | set/get | Bold for all runs |
| `italic` | set/get | Italic for all runs |
| `underline` | set/get | Underline style (`none`, `single`, `double`, etc.) |
| `strike` | set/get | Strike-through for all runs |
| `color` | set/get | Run text color |
| `highlight` | set/get | Text highlight color (Word palette names) |
| `direction` | add/set/get | `rtl` writes `<w:bidi/>` on all cell paragraphs |
| `textDirection` | set/get | Text flow: `lrtb`, `btlr`, `tbrl`, etc. |
| `nowrap` | set/get | Disable text wrapping |
| `fitText` | set | Squeeze text to fit cell width |
| `colspan` | set/get | Column span (gridSpan) |
| `vmerge` | set/get | Vertical merge: `restart` \| `continue` |
| `hmerge` | set/get | Horizontal merge (legacy): `restart` \| `continue` |
| `padding.top` | set/get | Top cell margin in twips |
| `padding.bottom` | set/get | Bottom cell margin in twips |
| `padding.left` | set/get | Left cell margin in twips |
| `padding.right` | set/get | Right cell margin in twips |
| `border.all` | add/set | All four edges shorthand |
| `border.top` | set | Top cell border |
| `border.bottom` | set | Bottom cell border |
| `border.left` | set | Left cell border |
| `border.right` | set | Right cell border |
| `border.tl2br` | add/set/get | Diagonal top-left to bottom-right |
| `border.tr2bl` | add/set/get | Diagonal top-right to bottom-left |
| `skipGridSync` | set | Suppress tblGrid sync side effect when setting width |

