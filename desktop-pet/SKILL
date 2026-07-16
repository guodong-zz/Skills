# Desktop Pet From Spritesheet

## 1. Purpose

将用户提供的任意角色相关输入转换为符合 Codex 桌宠标准的本地宠物包。

不要预设输入类型。

所有输入统一按照以下逻辑处理：

```text
Inspect
→ Validate Against Standard
→ Reuse Valid Assets
→ Repair or Generate Missing Content
→ Assemble
→ QA
→ Install
→ Revalidate
```

核心原则：

```text
Reuse first.
Prefer local processing.
Generate only what is missing or invalid.
Never regenerate valid components.
Retry only failed components.
```

---

# 2. Target Standard

最终 `spritesheet.webp` 必须满足：

```text
Dimensions: 1536 × 2288
Grid: 8 columns × 11 rows
Cell size: 192 × 208
Background: RGBA transparent
```

结构：

```text
Rows 0–8
Standard animation frames

Rows 9–10
16 look-direction frames
```

最终安装目录：

```text
~/.codex/pets/<pet-id>/
├── pet.json
└── spritesheet.webp
```

`pet.json`：

```json
{
  "id": "pet-id",
  "displayName": "宠物名",
  "description": "一句描述。",
  "spriteVersionNumber": 2,
  "spritesheetPath": "spritesheet.webp"
}
```

---

# 3. Workflow

## Step 1 — Inspect

检查所有可用输入和实际文件，包括：

```text
dimensions
format
alpha channel
grid or frame structure
background
available animation content
available look directions
character consistency
```

不得仅根据用户描述判断文件是否合规。

---

## Step 2 — Validate Against Standard

比较当前资产与目标标准。

识别：

```text
valid components
missing components
invalid components
layout defects
background defects
semantic defects
```

如果已经完全合规：

```text
QA
→ Package
→ Install
→ Revalidate
```

不调用图像生成。

---

## Step 3 — Reuse and Repair

保留所有已经验证合格的内容。

优先使用本地确定性处理解决：

```text
cropping
cell extraction
cell reordering
layout correction
background removal
checkerboard removal
alpha cleanup
sprite assembly
format conversion
```

不得因局部问题重新生成完整 sprite sheet。

---

## Step 4 — Generate Missing Content

只有视觉内容缺失、语义错误或无法本地修复时才使用图像生成。

例如：

```text
missing frame
→ generate that frame

invalid direction
→ repair or regenerate that direction

invalid row
→ repair or regenerate that row
```

完整重新生成只能作为最后手段。

---

## Step 5 — Assemble

将所有合格资产组装为：

```text
1536 × 2288
8 × 11
192 × 208 per cell
```

可生成：

```text
spritesheet.png
spritesheet.webp
contact-sheet.png
look-directions-qa.png
validation.json
```

---

# 4. Look Direction Rules

第 9–10 行方向顺序固定。

## Row 9

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

## Row 10

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

四个关键方向必须明确：

```text
000 = Up
090 = Right
180 = Down
270 = Left
```

`000` 不得使用正脸待机图代替。

如果需要生成观察方向，应先确保四个关键方向正确，再补齐中间方向。

方向变化必须自然、连续、顺序正确。

不得使用：

```text
repeated side profiles
incorrect mirroring
mechanical full-body rotation
front-facing frames as upward directions
```

---

# 5. Character Consistency

新生成内容必须尽可能保持：

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

如果只有部分 frame 不一致，只重新生成不合格部分。

---

# 6. QA

安装前必须同时通过 Structural QA 和 Semantic QA。

## Structural QA

检查：

```text
1536 × 2288
8 × 11 grid
192 × 208 cells
valid alpha transparency
no missing required frames
no unexpected empty cells
no checkerboard or solid background contamination
no critical cropping or misalignment
```

## Semantic QA

检查：

```text
animation meaning is recognizable
character identity is consistent

000 clearly looks up
090 clearly looks right
180 clearly looks down
270 clearly looks left

look-direction sequence is continuous
left/right directions are not reversed
diagonal directions are correctly ordered
```

结构正确但语义错误时，不得安装。

---

# 7. Packaging and Installation

创建：

```text
~/.codex/pets/<pet-id>/
```

写入：

```text
pet.json
spritesheet.webp
```

安装前验证源文件。

安装后重新读取：

```text
~/.codex/pets/<pet-id>/spritesheet.webp
```

并再次确认最终安装文件与已验证源文件一致。

---

# 8. Completion Criteria

只有满足以下条件时才算完成：

```text
[PASS] Final sprite sheet matches the 8×11 standard
[PASS] Required animation frames are present
[PASS] Look directions are correct and continuous
[PASS] Transparency and background are valid
[PASS] No critical cropping or alignment errors
[PASS] Character identity is sufficiently consistent
[PASS] Installed files match the validated output
```

如果任意关键条件失败：

```text
DO NOT mark the task as complete.
```
