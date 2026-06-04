# numbering

Generates a Word document exercising every supported numbering list property.

See [numbering.sh](numbering.sh) and [numbering.docx](numbering.docx).

## Properties demonstrated

### abstractNum

| Key | Op | Notes |
|-----|----|-------|
| `name` | add/set/get | Human-readable name shown in Word's Numbering dialog |
| `type` | add/set/get | `hybridMultilevel` \| `multilevel` \| `singleLevel` |
| `styleLink` | add/set/get | Back-reference to a numbering style (`w:styleLink`) |
| `numStyleLink` | add/set/get | Link to another abstractNum via numbering style (`w:numStyleLink`) |
| `level<N>.format` | add | `decimal`, `lowerLetter`, `lowerRoman`, `bullet`, etc. |
| `level<N>.text` | add | lvlText template; `%N` inserts level N counter |
| `level<N>.start` | add | Starting number for level N |
| `level<N>.indent` | add | Left indent in twips |
| `level<N>.hanging` | add | Hanging indent in twips |
| `level<N>.justification` | add | `left` \| `center` \| `right` |
| `level<N>.suff` | add | `tab` \| `space` \| `nothing` |
| `level<N>.font` | add | Marker font family |
| `level<N>.size` | add | Marker font size (pt) |
| `level<N>.color` | add | Marker color |
| `level<N>.bold` | add | Bold marker |
| `level<N>.italic` | add | Italic marker |

### level (via Set on `/numbering/abstractNum[@id=N]/level[L]`)

| Key | Op | Notes |
|-----|----|-------|
| `format` | add/set/get | numFmt for this level |
| `lvlText` | add/set/get | Level text template |
| `start` | add/set/get | Starting number |
| `indent` | add/set/get | Left indent in twips |
| `hanging` | add/set/get | Hanging indent in twips |
| `justification` | add/set/get | Marker alignment |
| `direction` | add | `rtl` writes `<w:bidi/>` on the level's pPr |
| `isLgl` | add/set | Render counter as decimal regardless of numFmt (legal style) |
| `lvlRestart` | add/set | Level at which to restart counter; `0` = never restart |
| `suff` | add/set | Separator between marker and content |

---
