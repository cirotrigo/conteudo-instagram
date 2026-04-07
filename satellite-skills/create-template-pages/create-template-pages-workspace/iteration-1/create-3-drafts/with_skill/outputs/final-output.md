# Criativos Happy Hour - By Rock (Segunda-feira 2026-04-06)

## Resumo

Projeto: **By Rock** (ID: 7)
Template: **Segunda** (ID: 83)
Tipo: STORY
Status: **DRAFT** (os 3 posts nao puderam ser criados automaticamente pois a permissao para `create-post` foi negada)

---

## Configuracao do Template

Template 83 (Segunda) possui 12 pages com os seguintes slots de texto:
- `Texto - Titulo Principal` / `Texto - Titulo Principal Copy` (titulo com efeito shadow)
- `Texto - Subtitulo` / `Texto - Subtitulo Copy` (subtitulo com efeito shadow)
- `Texto - Texto do corpo` (pre-titulo/body text)
- `CTA` (call-to-action)
- Elemento de badge HH ja presente no template: `Elemento - selo-BY-HH.png`
- Imagens dinamicas via `_driveImageId`

---

## Story 1 - Chopp

**Page ID:** `cmj3i7l20000fkw04xyurxfj8`
**Horario:** 17:00 BRT
**Caption:** Happy Hour By Rock - Chopp gelado a partir das 16h. Vem pro Rock!

**slotValues:**
```json
{
  "Texto - Titulo Principal": "SER UM BLUES",
  "Texto - Titulo Principal Copy": "SER UM BLUES",
  "Texto - Subtitulo": "Chopp gelado a partir das 16h",
  "Texto - Subtitulo Copy": "Chopp gelado a partir das 16h",
  "Texto - Texto do corpo": "SEGUNDA NAO PRECISA",
  "CTA": "Vem pro Rock!",
  "_driveImageId": "1y5rA2VxZ4H2LibIpvNdQkFMtz3DKFx0y"
}
```

**Chamada MCP (create-post):**
```
projectId: 7
postType: "STORY"
caption: "Happy Hour By Rock - Chopp gelado a partir das 16h. Vem pro Rock!"
scheduledDatetime: "2026-04-06 17:00"
pageId: "cmj3i7l20000fkw04xyurxfj8"
slotValues: (JSON acima)
status: "DRAFT"
```

---

## Story 2 - Rock Fries

**Page ID:** `cmj6dc5es0001jl04j1ld24d5`
**Horario:** 18:00 BRT
**Caption:** Happy Hour By Rock - Rock Fries com cheddar e bacon. Pede o seu!

**slotValues:**
```json
{
  "Texto - Titulo Principal": "QUE SALVA A SEGUNDA",
  "Texto - Titulo Principal Copy": "QUE SALVA A SEGUNDA",
  "Texto - Subtitulo": "Rock Fries com cheddar e bacon",
  "Texto - Subtitulo Copy": "Rock Fries com cheddar e bacon",
  "Texto - Texto do corpo": "AQUELA BATATA",
  "CTA": "Pede o seu!",
  "_driveImageId": "1qWHye1LoN4muBKjERNXpDF1fGCbmsZU6"
}
```

**Chamada MCP (create-post):**
```
projectId: 7
postType: "STORY"
caption: "Happy Hour By Rock - Rock Fries com cheddar e bacon. Pede o seu!"
scheduledDatetime: "2026-04-06 18:00"
pageId: "cmj6dc5es0001jl04j1ld24d5"
slotValues: (JSON acima)
status: "DRAFT"
```

---

## Story 3 - Onion Rings

**Page ID:** `cmjd9kryu0007sw1avbazu3ma`
**Horario:** 19:00 BRT
**Caption:** Happy Hour By Rock - Onion Rings empanados no panko ultra crocantes. Garanta o seu!

**slotValues:**
```json
{
  "Texto - Titulo Principal": "NA CERVEJA PRETA",
  "Texto - Titulo Principal Copy": "NA CERVEJA PRETA",
  "Texto - Subtitulo": "Empanados no panko ultra crocantes",
  "Texto - Subtitulo Copy": "Empanados no panko ultra crocantes",
  "Texto - Texto do corpo": "ONION RINGS",
  "CTA": "Garanta o seu!",
  "_driveImageId": "1CQfcoO8u3Gxw6Xm5KvAH8GtEYnH9IjmW"
}
```

**Chamada MCP (create-post):**
```
projectId: 7
postType: "STORY"
caption: "Happy Hour By Rock - Onion Rings empanados no panko ultra crocantes. Garanta o seu!"
scheduledDatetime: "2026-04-06 19:00"
pageId: "cmjd9kryu0007sw1avbazu3ma"
slotValues: (JSON acima)
status: "DRAFT"
```

---

## Mapeamento Copy -> Slots do Template

| Campo Copy | Slot do Template | Notas |
|---|---|---|
| Pre-titulo | `Texto - Texto do corpo` | Texto acima do titulo principal |
| Titulo | `Texto - Titulo Principal` + `Texto - Titulo Principal Copy` | Titulo com duplicata para efeito shadow |
| Subtitulo | `Texto - Subtitulo` + `Texto - Subtitulo Copy` | Subtitulo com duplicata para efeito shadow |
| CTA | `CTA` | Call-to-action |
| Badge (HH) | Ja presente no template como `Elemento - selo-BY-HH.png` | Nao precisa de slot |

## Imagens (Google Drive IDs)

| Story | Drive File ID |
|---|---|
| 1 (Chopp) | `1y5rA2VxZ4H2LibIpvNdQkFMtz3DKFx0y` |
| 2 (Rock Fries) | `1qWHye1LoN4muBKjERNXpDF1fGCbmsZU6` |
| 3 (Onion Rings) | `1CQfcoO8u3Gxw6Xm5KvAH8GtEYnH9IjmW` |

## Pages Selecionadas (variedade visual)

Tres pages distintas do template 83 (Segunda) para evitar layouts repetidos:
1. `cmj3i7l20000fkw04xyurxfj8` (Pagina 1)
2. `cmj6dc5es0001jl04j1ld24d5` (Pagina 2)
3. `cmjd9kryu0007sw1avbazu3ma` (Pagina 3)

## Status

**BLOQUEADO:** A permissao para o MCP tool `create-post` foi negada pelo ambiente. Os 3 posts DRAFT precisam ser criados manualmente ou com permissao habilitada. Todas as chamadas estao documentadas acima com os parametros exatos.

## Proximos Passos (apos criacao dos DRAFTs)

1. Executar `create-post` para cada um dos 3 stories acima
2. Verificar com `list-posts(projectId: 7, status: "DRAFT")`
3. Renderizar com `render-story(postId)` para cada post
4. Revisar resultado visual
