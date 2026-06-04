# formulas

Generates a Word document exercising every supported equation property.

See [formulas.sh](formulas.sh) and [formulas.docx](formulas.docx).

## Properties demonstrated

### equation

| Key | Values | Notes |
|-----|--------|-------|
| `formula` | LaTeX-ish string | Math expression; aliases: `text` |
| `mode` | `display` \| `inline` | `display` (default) wraps in `oMathPara`; `inline` appends `oMath` to the parent paragraph |

