# Desktop Pet From Spritesheet

Convert user-provided character material into a local Codex desktop pet package.

Treat web-generated images, screenshots, checkerboard-background images, partial grids, single references, and existing pet folders as source material that must be inspected. Do not assume the input is already a valid spritesheet.

Workflow:

```text
Inspect
-> Validate Against Standard
-> Reuse Valid Assets
-> Repair or Generate Missing Content
-> Assemble
-> QA
-> Install
-> Runtime Observation
-> Revalidate
```

Core rules:

```text
Reuse first.
Prefer deterministic local processing.
Generate only what is missing or invalid.
Never regenerate valid components.
Retry only failed components.
Do not install until structural QA and semantic QA both pass.
Do not claim behavior coverage until runtime observation is checked or clearly reported as unavailable.
```

## 1. Target Standard

The final `spritesheet.webp` must be:

```text
Dimensions: 1536 x 2288
Grid: 8 columns x 11 rows
Cell size: 192 x 208
Background: RGBA transparent
Format: WebP with alpha
```

Rows:

```text
Row 0: idle
Row 1: running/walking right
Row 2: running/walking left
Row 3: waving/greeting
Row 4: jumping/excited hop
Row 5: failed/sad/disappointed
Row 6: waiting/asking/curious
Row 7: running/playful energetic movement
Row 8: review/inspect/think/read-like action
Rows 9-10: 16 look-direction frames
```

Install layout:

```text
~/.codex/pets/<pet-id>/
├─ pet.json
└─ spritesheet.webp
```

`pet.json` must include:

```json
{
  "id": "pet-id",
  "displayName": "宠物名称",
  "description": "一句描述。",
  "spriteVersionNumber": 2,
  "spritesheetPath": "spritesheet.webp"
}
```

Do not invent `animations.json`, `behavior.json`, or other runtime metadata unless the current Codex desktop pet runtime is explicitly confirmed to read and use those files. The v2 package contract is the fixed row protocol plus `pet.json` and `spritesheet.webp`.

## 2. Web Source Guidance

When the user asks for a web image prompt, prefer source material that is easy to reuse and repair:

```text
Best default: one 8-frame action strip per generation.
Second best: a 2-row look-direction sheet for the 16 direction frames.
Last resort: one complete 8 x 11 spritesheet.
```

Explain that full-sheet web generation often creates fake transparency, wrong grids, mixed actions, incorrect directions, and inconsistent character identity. Use complete `8 x 11` generation only when the web tool is known to be reliable.

For action strips, require:

```text
one horizontal row
exactly 8 frames
true alpha transparency
no checkerboard, solid background, labels, borders, or grid lines
one coherent action only
consistent character identity, scale, outfit, and style
full body visible with safe padding
```

For look directions, require:

```text
8 columns x 2 rows
16 directions in the exact v2 order
000 is up/back-up, not normal front idle
090 faces right
180 is down/front-down
270 faces left
continuous rotation
no left/right reversal
```

## 3. Inspect

Inspect every actual file before deciding what to do. Record:

```text
dimensions
format
color mode
alpha channel
true transparency vs fake checkerboard
grid dimensions
cell size or approximate frame bounding boxes
available rows/actions
available look directions
character consistency
cropping, spacing, and scale problems
```

For web-generated source images, explicitly check:

```text
is the background real alpha or a rendered checkerboard?
is the grid 8 x 11, action-strip, direction-sheet, or another layout?
are rows action-consistent or semantically mixed?
are left/right rows reversed or duplicated?
are rows 9-10 present and directionally coherent?
```

Do not trust a visual checkerboard as transparency. If the file is RGB or has fully opaque alpha, treat the checkerboard as background contamination until removed.

## 4. Validate Against Standard

Compare the current assets with the target standard and identify:

```text
valid components
missing components
invalid components
layout defects
background defects
semantic defects
runtime-observation gaps
```

Build a reuse matrix before generating anything:

```text
target row/cell
source row/cell
status: reuse | repair | generate | reject
reason
```

If the input is already fully valid, proceed directly to QA, package, install, runtime observation, and revalidation. Do not call image generation for already-valid assets.

## 5. Reuse And Repair

Keep every component that passes validation. Use deterministic local processing first:

```text
cell extraction
cropping
scaling into 192 x 208 cells
cell reordering
row splitting
layout correction
checkerboard removal
background removal
alpha cleanup
edge despill
sprite assembly
format conversion
```

For fake checkerboard backgrounds:

```text
detect repeating light/dark checker pattern or opaque RGB background
remove background from border-connected regions when possible
preserve character pixels and soft edges
clean transparent RGB residue
verify no checkerboard remains in final alpha
```

Do not regenerate a complete spritesheet because one row or one direction is bad. Freeze validated rows and repair only the failing parts.

## 6. Generate Missing Content

Use image generation only when required content is missing, semantically wrong, or cannot be repaired locally.

Generate at the smallest useful unit:

```text
missing cell -> generate that cell
invalid direction -> repair or regenerate that direction
invalid row -> repair or regenerate that row
missing action family -> generate that row
```

Full-sheet regeneration is the last resort and requires a reason such as unusable source quality, no stable character identity, or pervasive semantic failure.

Generated content must preserve:

```text
character identity
face
body proportions
clothing
accessories
color palette
art style
relative scale
```

After generation, re-run extraction, alpha cleanup, assembly, and QA. If a generated row fails, retry only that row or direction.

## 7. Look Direction Rules

Rows 9-10 contain 16 directions in this fixed order.

Row 9:

```text
000    Up
022.5  Upper-right
045    Upper-right
067.5  Upper-right
090    Right
112.5  Lower-right
135    Lower-right
157.5  Lower-right
```

Row 10:

```text
180    Down
202.5  Lower-left
225    Lower-left
247.5  Lower-left
270    Left
292.5  Upper-left
315    Upper-left
337.5  Upper-left
```

Reject:

```text
front-facing frames used as upward directions
left/right reversal
duplicated side profiles for many angles
random pose changes instead of rotation
mechanical rotation that breaks character design
direction rows with inconsistent outfit, hair, or scale
```

Always create or inspect a dedicated look-direction QA sheet before installing.

## 8. Assemble

Assemble validated and repaired assets into:

```text
1536 x 2288
8 x 11
192 x 208 per cell
RGBA transparent
```

Generate useful QA artifacts when possible:

```text
spritesheet.png
spritesheet.webp
contact-sheet.png
look-directions-qa.png
validation.json
despill-report.json
reuse-matrix.txt or reuse-matrix.json
runtime-observation-notes.txt
```

These QA artifacts are not required runtime package files. The installed pet package should contain only files supported by the current Codex desktop pet runtime.

## 9. QA

Installation requires both Structural QA and Semantic QA.

Structural QA:

```text
1536 x 2288
8 x 11 grid
192 x 208 cells
RGBA/WebP with alpha
valid pet.json with spriteVersionNumber: 2
no missing required frames
no unexpected empty cells
no checkerboard or solid background contamination
no critical cropping or misalignment
no transparent RGB residue that could fringe at runtime
```

Semantic QA:

```text
each standard row has the intended action
rows are internally coherent animation strips
running-right and running-left are not swapped
failed is visibly sad/disappointed and not idle
waiting is visibly curious/asking and not idle
review is visibly inspect/think/read-like and not idle
character identity is consistent
000, 090, 180, and 270 directions are correct
direction sequence is continuous
diagonal directions are correctly ordered
```

If structure passes but semantics fail, do not install. Repair or regenerate only the failing components, then rebuild and re-run QA.

## 10. Packaging And Installation

Before installation:

```text
validate final source spritesheet
validate final pet.json
record or compare source hash when practical
```

Install to:

```text
~/.codex/pets/<pet-id>/
```

Write:

```text
pet.json
spritesheet.webp
```

After installation, re-read installed files and verify:

```text
installed pet.json is valid UTF-8 JSON
installed pet.json has spriteVersionNumber: 2
installed spritesheet.webp passes full validation
installed spritesheet hash matches the validated source spritesheet
```

## 11. Runtime Observation

After installation, distinguish asset correctness from runtime behavior. The spritesheet can be valid even when the current Codex UI only visibly triggers a subset of rows during ordinary use.

Observe or attempt to trigger:

```text
idle / standing -> Row 0
movement right -> Row 1
movement left -> Row 2
waving or greeting, if the runtime exposes it -> Row 3
jump or excited state, if the runtime exposes it -> Row 4
failed or error state, if available -> Row 5
waiting or asking state, if available -> Row 6
active running/playful work state, if available -> Row 7
review/inspect/thinking state, if available -> Row 8
look direction changes, if available -> Rows 9-10
```

Record each item as:

```text
observed
not observed because no runtime trigger was available
observed but wrong row/action appeared
```

If only running is visible during ordinary interaction, do not assume the asset is missing other actions. Inspect the spritesheet rows first, then report whether the limitation appears to be:

```text
asset missing or semantically wrong
runtime trigger unavailable
runtime trigger available but mapping appears wrong
unknown; needs deeper runtime inspection
```

## 12. Completion Criteria

Only mark the task complete when all conditions pass or any unavailable runtime behavior is explicitly reported:

```text
[PASS] Final sprite sheet matches the 8 x 11 v2 standard
[PASS] Required animation rows are present
[PASS] Look directions are correct and continuous
[PASS] Transparency and background are valid
[PASS] No critical cropping or alignment errors
[PASS] Character identity is sufficiently consistent
[PASS] pet.json is valid and uses spriteVersionNumber: 2
[PASS] Installed files match the validated output
[PASS] Installed package revalidates successfully
[PASS/WARN] Runtime observation completed, or unavailable triggers are documented
```

If any critical condition fails:

```text
DO NOT mark the task as complete.
Report the blocker and the smallest next repair needed.
```
