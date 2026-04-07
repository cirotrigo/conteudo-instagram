# Happy Hour By Rock - Segunda-feira (2026-04-06) - 3 Stories

## Resumo

Tarefa: Criar 3 stories de Happy Hour para o By Rock (project ID 7) para segunda-feira 06/04/2026.

**Status: create-post foi BLOQUEADO (permissao negada). Abaixo estao os 3 comandos completos prontos para execucao.**

## Descobertas

### Projeto
- **Projeto**: By Rock (ID: 7)
- **Instagram**: by.rock

### Template Identificado
- **Template ID**: 140 (template de Happy Hour do By Rock)
- **Pages disponiveis**:
  - `cmn5ih9wk0009swxqcqlfoddm` (usada em posts de quarta, sexta, domingo)
  - `cmn5iha0s000bswxqynkwofrh` (usada em posts de quinta, sabado, segunda)
- **Formato dos slots** (lowercase): `pre-titulo`, `titulo`, `subtitulo`, `cta`, `badge`, `rodape-1`
- **Imagem de fundo**: via `_driveImageId` no slotValues

### Copies Fornecidas

| Story | Pre-titulo | Titulo | Subtitulo | CTA | Badge |
|-------|-----------|--------|-----------|-----|-------|
| 1 | SEGUNDA NAO PRECISA | SER UM BLUES | Chopp gelado a partir das 16h | Vem pro Rock! | HH |
| 2 | AQUELA BATATA | QUE SALVA A SEGUNDA | Rock Fries com cheddar e bacon | Pede o seu! | HH |
| 3 | ONION RINGS | NA CERVEJA PRETA | Empanados no panko ultra crocantes | Garanta o seu! | HH |

### Imagens (Google Drive IDs)
1. `1y5rA2VxZ4H2LibIpvNdQkFMtz3DKFx0y`
2. `1qWHye1LoN4muBKjERNXpDF1fGCbmsZU6`
3. `1CQfcoO8u3Gxw6Xm5KvAH8GtEYnH9IjmW`

---

## Comandos create-post (3 chamadas)

### Story 1 - 16:00 BRT

```
Tool: mcp__studio-lagosta__create-post
Parameters:
  projectId: 7
  postType: STORY
  caption: "SEGUNDA NAO PRECISA SER UM BLUES - Chopp gelado a partir das 16h. Vem pro Rock!"
  scheduledDatetime: "2026-04-06 16:00"
  status: DRAFT
  pageId: "cmn5ih9wk0009swxqcqlfoddm"
  templateId: 140
  slotValues: "{\"pre-titulo\":\"SEGUNDA NAO PRECISA\",\"titulo\":\"SER UM BLUES\",\"subtitulo\":\"Chopp gelado a partir das 16h\",\"cta\":\"Vem pro Rock!\",\"badge\":\"HH\",\"_driveImageId\":\"1y5rA2VxZ4H2LibIpvNdQkFMtz3DKFx0y\"}"
```

### Story 2 - 16:30 BRT

```
Tool: mcp__studio-lagosta__create-post
Parameters:
  projectId: 7
  postType: STORY
  caption: "AQUELA BATATA QUE SALVA A SEGUNDA - Rock Fries com cheddar e bacon. Pede o seu!"
  scheduledDatetime: "2026-04-06 16:30"
  status: DRAFT
  pageId: "cmn5iha0s000bswxqynkwofrh"
  templateId: 140
  slotValues: "{\"pre-titulo\":\"AQUELA BATATA\",\"titulo\":\"QUE SALVA A SEGUNDA\",\"subtitulo\":\"Rock Fries com cheddar e bacon\",\"cta\":\"Pede o seu!\",\"badge\":\"HH\",\"_driveImageId\":\"1qWHye1LoN4muBKjERNXpDF1fGCbmsZU6\"}"
```

### Story 3 - 17:00 BRT

```
Tool: mcp__studio-lagosta__create-post
Parameters:
  projectId: 7
  postType: STORY
  caption: "ONION RINGS NA CERVEJA PRETA - Empanados no panko ultra crocantes. Garanta o seu!"
  scheduledDatetime: "2026-04-06 17:00"
  status: DRAFT
  pageId: "cmn5ih9wk0009swxqcqlfoddm"
  templateId: 140
  slotValues: "{\"pre-titulo\":\"ONION RINGS\",\"titulo\":\"NA CERVEJA PRETA\",\"subtitulo\":\"Empanados no panko ultra crocantes\",\"cta\":\"Garanta o seu!\",\"badge\":\"HH\",\"_driveImageId\":\"1CQfcoO8u3Gxw6Xm5KvAH8GtEYnH9IjmW\"}"
```

---

## Metodologia (como cheguei nestes parametros)

1. **Identificacao do projeto**: `list-projects` -> By Rock = project ID 7
2. **Identificacao do template**: `list-posts` com dateFrom 2026-03-25 revelou posts existentes de Happy Hour usando **template 140** com slot values em lowercase
3. **Page IDs**: Extraidos dos posts existentes de HH - duas pages alternadas: `cmn5ih9wk0009swxqcqlfoddm` e `cmn5iha0s000bswxqynkwofrh`
4. **Formato dos slots**: Copiado dos posts existentes (ex: post `cmnhs8ivw0001sw11ovkv00es` de quarta-feira)
5. **Imagens**: Mapeadas via `_driveImageId` no slotValues (Google Drive IDs fornecidos pelo usuario)
6. **Horarios**: 16:00, 16:30, 17:00 BRT (padrao happy hour, espacados 30min)
7. **Caption**: Concatenacao de Pre-titulo + Titulo + Subtitulo + CTA (padrao observado nos posts existentes)

## Resultado

**NAO FOI POSSIVEL CRIAR OS POSTS** - a permissao para `create-post` foi negada pelo ambiente de execucao. Os 3 comandos acima estao prontos para serem executados manualmente ou por um agente com permissao adequada.
