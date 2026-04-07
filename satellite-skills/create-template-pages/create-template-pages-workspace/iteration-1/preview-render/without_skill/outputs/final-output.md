# Preview Render - Without Skill - Smash Burger By Rock

## Task
Preview a Smash Burger story for By Rock (project ID: 7) before scheduling.

## Input Data

### Copy
| Field | Value |
|-------|-------|
| Pre-titulo | AQUELA CROSTINHA |
| Titulo | QUE ESTALA NA PRIMEIRA MORDIDA |
| Subtitulo | Carne prensada na chapa cheddar derretendo |
| CTA | Pede o teu! |
| Badge | SMASH |

### Image
- **Drive File ID**: `1dlmsU_d3m5BIpXOyi0JBydHn5zq2gf4Q`
- **Filename**: CMT08168.jpg
- **MIME Type**: image/jpeg
- **Thumbnail**: https://lh3.googleusercontent.com/drive-storage/AJQWtBNkyO9umFA91msUy1kPGRowlweIjPQQKLMcGlbaw1bv1x0-flmgx7Prz6Twm5ssnAz-JyWSIc18NCNnMBRqP4sDlGHN-9THhWRSvqJiFRbn8J9eww=s220

### Caption
Tem barulho que da agua na boca...

## Steps Taken (Without Skill)

### 1. Project Discovery
- Called `list-projects` -> Found By Rock as project ID 7
- Called `get-knowledge(projectId: 7)` -> Retrieved knowledge base (menu, hours, posting patterns, tone of voice)

### 2. Template Discovery (STRUGGLED)
- Called `list-templates(projectId: 7, type: "STORY")` -> Result exceeded max tokens (878,815 chars). Could not parse.
- Attempted `get-template-pages` for template IDs 1, 7, 8, 9, 10, 11, 12, 13, 14 -> Most returned oversized results or empty arrays.
- Template IDs 7, 9, 11, 12, 13 returned large page sets (100k-250k+ chars each).
- Could not extract page IDs or layer names from any of these results due to single-line JSON format and token limits.
- **Grep searches** for layer names ("Pre-titulo", "Badge", "CTA") in cached result files were inconsistent due to JSON encoding on single lines.

### 3. Alternative Approach - Existing Posts
- Called `list-posts(projectId: 7, dateFrom: "2026-03-20")` -> Found 20 posts
- **Found one template-based post**: Post ID `cmn70e0b20001jv04w3ahg4hi` with:
  - `pageId: "cmn6yx2k10007swe3hip2mpmx"`
  - `templateId: 141`
  - `renderStatus: "RENDERED"` (successfully rendered before)

### 4. Image Verification
- Called `get-image-thumbnail(driveFileId: "1dlmsU_d3m5BIpXOyi0JBydHn5zq2gf4Q")` -> Confirmed image exists (CMT08168.jpg)

### 5. Post Creation (BLOCKED)
- Attempted `create-post` with:
  - projectId: 7
  - postType: "STORY"
  - caption: "Tem barulho que da agua na boca..."
  - scheduledDatetime: "2026-04-03 12:00"
  - status: "DRAFT"
  - pageId: "cmn6yx2k10007swe3hip2mpmx"
  - templateId: 141
  - slotValues: `{"Pre-titulo":"AQUELA CROSTINHA","Titulo":"QUE ESTALA NA PRIMEIRA MORDIDA","Subtitulo":"Carne prensada na chapa cheddar derretendo","CTA":"Pede o teu!","Badge":"SMASH","_driveImageId":"1dlmsU_d3m5BIpXOyi0JBydHn5zq2gf4Q"}`
- **DENIED** - Permission to use `create-post` was denied.

### 6. Render (BLOCKED)
- Attempted `render-story(postId: ...)` -> **DENIED** - Permission to use `render-story` was denied.

## Result: INCOMPLETE

The task could not be completed because the critical MCP tools (`create-post` and `render-story`) were denied by the permission system. Additionally, `bash` and `plan-week` were also denied.

### What Was Accomplished
- Identified project (By Rock, ID: 7)
- Retrieved knowledge base context
- Found a valid template page (`cmn6yx2k10007swe3hip2mpmx` from template 141) by searching existing rendered posts
- Verified the Drive image exists
- Prepared the complete slotValues payload
- Prepared the complete create-post parameters

### What Was NOT Accomplished
- Could not create the DRAFT post (create-post denied)
- Could not render the story preview (render-story denied)
- No rendered image URL to show

## Key Difficulties Without Skill

1. **Template discovery was extremely painful** - The `list-templates` and `get-template-pages` results for By Rock are enormous (100k-800k+ chars) because the project has many templates with many pages. Without bash/python to parse the JSON, and with grep being ineffective on single-line JSON, finding a valid pageId was very difficult.

2. **Workaround through existing posts** - The only way to find a valid pageId was by searching through historical posts (`list-posts`) and finding one that had already been rendered with a template. This is fragile and depends on prior usage.

3. **No way to verify page slot compatibility** - Without being able to parse template page layer names, there was no way to confirm that the selected page (`cmn6yx2k10007swe3hip2mpmx`) actually has layers named "Pre-titulo", "Titulo", "Subtitulo", "CTA", and "Badge". The slot values for non-existent layers would simply be ignored silently.

4. **Tool permission denials** - The core mutation tools (create-post, render-story) and bash were all denied, making it impossible to complete the actual task.

## Prepared Payload (for reference)

```json
{
  "projectId": 7,
  "postType": "STORY",
  "caption": "Tem barulho que da agua na boca...",
  "scheduledDatetime": "2026-04-03 12:00",
  "status": "DRAFT",
  "pageId": "cmn6yx2k10007swe3hip2mpmx",
  "templateId": 141,
  "slotValues": {
    "Pre-titulo": "AQUELA CROSTINHA",
    "Titulo": "QUE ESTALA NA PRIMEIRA MORDIDA",
    "Subtitulo": "Carne prensada na chapa cheddar derretendo",
    "CTA": "Pede o teu!",
    "Badge": "SMASH",
    "_driveImageId": "1dlmsU_d3m5BIpXOyi0JBydHn5zq2gf4Q"
  }
}
```
