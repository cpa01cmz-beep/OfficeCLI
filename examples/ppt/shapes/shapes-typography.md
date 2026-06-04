# Shape Typography

Three files work together:

- **shapes-typography.sh** — Shell script that builds the deck.
- **shapes-typography.pptx** — The generated 4-slide deck.
- **shapes-typography.md** — This file.

Fills in the typography props NOT touched by `textboxes-basic`:
paragraph-level spacing, character spacing, kerning threshold,
case rendering, BCP-47 language tag, RTL direction, and the
complex-script font slot.

## Regenerate

```bash
cd examples/ppt
bash shapes/shapes-typography.sh
# → shapes/shapes-typography.pptx
```

## Slides

### Slide 1 — Paragraph spacing

Three identical 3-paragraph blocks; only the spacing props differ:

| Spec | Effect |
|---|---|
| default | tight default leading |
| `lineSpacing=1.5x` | 150% line height (multiplier) |
| `spaceBefore=12pt + spaceAfter=12pt` | gap between paragraphs |

`lineSpacing` accepts multiple input forms via `SpacingConverter`:

```bash
--prop lineSpacing=1.5x       # multiplier
--prop lineSpacing=150%       # percent form
--prop lineSpacing=18pt       # fixed
--prop lineSpacing=0.5cm      # length
```

`spaceBefore` / `spaceAfter` accept any length string (`12pt`,
`0.5cm`, `0.25in`). Aliases: `spacebefore`, `spaceafter`,
`linespacing`. All three props can also be set on individual
paragraphs (`--type paragraph --prop spaceBefore=...`) for
mixed-spacing layouts.

### Slide 2 — Character spacing, kerning, case

**`spacing=`** — character spacing in 1/100 pt (a.k.a. tracking).
Same string repeated at four spacing values shows the effect:

```bash
--prop spacing=-50    # negative = tighter
--prop spacing=200    # positive = looser
--prop spacing=500    # very loose, theatrical
```

Aliases: `spc`, `charspacing`, `letterspacing`.

**`kern=`** — minimum font size (in 1/100 pt) at which OpenType
kerning pairs are applied:

```bash
--prop kern=0       # disabled (no kerning at any size)
--prop kern=1       # enabled at all sizes (1 = 0.01pt threshold)
--prop kern=1200    # only kern from 12pt up
```

**`cap=`** — letter-case rendering mode:

| Value | Aliases | Effect |
|---|---|---|
| `none` | (default) | text as written |
| `small` | `smallCaps`, `smallcaps` | mAJUSCULE for lower-case |
| `all` | `allCaps`, `allcaps` | MAJUSCULES throughout |

The underlying string is unchanged; only the visual rendering differs,
so search/copy preserves case.

### Slide 3 — `direction=rtl` + `font.cs`

The same Arabic string rendered twice:

- **Left box (LTR, default):** `font.cs="Arabic Typesetting"` only —
  the trailing digits/punctuation land in their LTR-natural slots.
- **Right box (RTL):** `direction=rtl` + `align=right` reorders the
  whole paragraph right-to-left, which is what Arabic readers expect.

```bash
officecli add file.pptx /slide[3] --type textbox \
  --prop text="مرحبا بالعالم — 2026" \
  --prop direction=rtl \
  --prop font.cs="Arabic Typesetting" \
  --prop align=right
```

`direction=` aliases: `dir`, `rtl`. Same machinery covers Hebrew,
Urdu, Persian, Yiddish, etc. — pick the right `font.cs` face.

> 💡 `font.cs` is the **complex-script** font slot (DrawingML
> `a:cs`). PowerPoint picks it automatically for code points in
> the Arabic/Hebrew/Thai/Indic ranges. Latin and East-Asian chars
> in the same paragraph still use `font.latin` / `font.ea`.

### Slide 4 — Bare `font` + BCP-47 `lang` tag

**Bare `font=`** targets BOTH the Latin (`a:latin`) and EastAsian
(`a:ea`) slots in one shot — useful for documents in a single script.
Per-script `font.latin` / `font.ea` / `font.cs` overrides give finer
control when you need different faces per script.

```bash
--prop font="Times New Roman"           # both Latin and EA
--prop font.latin=Georgia \
--prop font.ea="Yu Mincho"              # per-script
```

**`lang=`** — BCP-47 language tag on the first run's `rPr/@lang`.
Affects spellcheck, hyphenation, and font fallback in PowerPoint:

```bash
--prop lang=en-US          # US English (default)
--prop lang=en-GB          # British English
--prop lang=fr-FR          # French
--prop lang=ja-JP          # Japanese
--prop lang=ar-SA          # Arabic (Saudi Arabia)
```

Aliases: `altLang`, `altlang`. Tag is validated against BCP-47 shape;
max 35 characters.

### Slide 5 — `strike` / `underline` / `valign` / `margin` / `list` / `lineOpacity` / `animation`

**`strike=`** and **`underline=`** — set at shape level, they apply as
defaults to all runs inside the shape:

```bash
--prop strike=single      # strikethrough (sngStrike)
--prop underline=single   # underline (sng)
```

**`valign=`** — vertical text position inside the shape bounding box:

| Value | Position |
|---|---|
| `top` | text anchored to top |
| `middle` | vertically centered |
| `bottom` | text anchored to bottom |

**`margin=`** — uniform inner text padding (alias of `marginLeft` /
`marginRight` / `marginTop` / `marginBottom` all at once):

```bash
--prop margin=0.4in     # 0.4in inner padding on all four sides
```

**`list=`** — shape-level bullet/numbered list (applies to ALL
paragraphs in the shape):

```bash
--prop list=bullet      # filled circle bullets
--prop list=numbered    # 1. 2. 3. …
```

After `Add`, append more items with `--type paragraph`.

**`lineOpacity=`** — outline transparency as a 0–1 fraction:

```bash
--prop lineOpacity=0.35   # 35% opacity stroke (65% transparent)
```

Requires a non-none line color (`line=` or `lineColor=`).

**`animation=`** — entrance animation preset applied to this shape
(see `animations.sh` for the full animation showcase):

```bash
--prop animation=fadeIn     # canonical name or alias
```

**Features covered:** `lineSpacing`, `spaceBefore`, `spaceAfter`,
`spacing` (char tracking), `kern` threshold, `cap=none|small|all`,
`direction=rtl`, `font` (bare), `font.cs`, `lang` BCP-47 tag,
`strike`, `underline`, `valign`, `margin`, `list`, `lineOpacity`,
`animation`.
