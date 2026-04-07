# Conteudo Espeto Gaucho - Almoco Quarta 09/04/2026

## Resumo

- **Projeto**: Espeto Gaucho (ID: 6)
- **Template**: IA (ID: 58), Pagina 1 (`cmhy873fc0001jv04amj1zy1j`)
- **Tipo**: STORY
- **Data**: Quarta-feira, 09/04/2026
- **Tema**: Almoco
- **Quantidade**: 2 stories
- **Status final**: SCHEDULED + RENDERED

---

## Fase 0: Setup

- **Projeto**: Espeto Gaucho (projectId: 6)
- **KB carregado**: Tom de voz gaucho (tche, bah, baita), cardapio completo, promocoes atuais
- **Template**: ID 58 com 2 pages (Pagina 1 = layout com textos, Pagina 2 = video)
- **Grade existente 09/04**: Vazia (nenhum post agendado)

---

## Fase 1: Curadoria de Imagens (PULADA)

Imagens ja escolhidas pelo usuario:

| Story | Drive File ID | Tema |
|-------|--------------|------|
| 1 | `1FWp2FwDVy8kCfWC574Jhg3hIDSENyhi8` | Almoco |
| 2 | `1V3cSnfqAc4ZUT02LZh3p1RqCVUjSJAA-` | Almoco |

---

## Fase 2: Redacao de Copies

### Tom de voz aplicado
Regional gaucho, informal, acolhedor. Expressoes: "tche", "bah", "de respeito". Foco em sabor, fartura e tradicao. Energia de quarta-feira: quebra de rotina, meio da semana.

### Story 1 - Picanha na Brasa

**Copy livre:**
"Quarta-feira e aquele cheiro de carne na brasa ja ta no ar. Picanha suculenta, farofa crocante e tropeiro de respeito. Nao precisa esperar o fim de semana pra comer um churrasco de verdade."

**slotValues:**
```json
{
  "Texto - Titulo Principal Copy": "PICANHA NA BRASA",
  "Texto - Titulo Principal Copy Copy": "de R$ 104,50 por R$ 84,99",
  "_driveImageId": "1FWp2FwDVy8kCfWC574Jhg3hIDSENyhi8"
}
```

**Caption Instagram:**
Quarta-feira e aquele cheiro de carne na brasa ja ta no ar, tche! Picanha suculenta, farofa crocante e tropeiro de respeito. Nao precisa esperar o fim de semana pra comer um churrasco de verdade. Vem pro Espeto Gaucho! Av. Ranulpho, 111 - Jardim Camburi #EspetoGaucho #ChurrascoDeVerdade #JardimCamburi

### Story 2 - Costela no Bafo

**Copy livre:**
"Bah, essa costela derretendo na boca e coisa de outro mundo! Costela no bafo com creme de aipim, farofa e vinagrete. Almoco gaucho de verdade so aqui."

**slotValues:**
```json
{
  "Texto - Titulo Principal Copy": "COSTELA NO BAFO",
  "Texto - Titulo Principal Copy Copy": "de R$ 149,00 por R$ 99,90",
  "_driveImageId": "1V3cSnfqAc4ZUT02LZh3p1RqCVUjSJAA-"
}
```

**Caption Instagram:**
Bah, essa costela derretendo na boca e coisa de outro mundo! Costela no bafo com creme de aipim, farofa e vinagrete. Almoco gaucho de verdade so aqui. Chega mais, tche! Av. Ranulpho, 111 - Jardim Camburi #EspetoGaucho #CostelaNoBafo #ChurrascoGaucho

---

## Fase 3: Montagem de Criativos

### Posts criados como DRAFT

| # | Post ID | Page ID | Status |
|---|---------|---------|--------|
| 1 | `cmni86epx001dswt2xc7wmhc9` | `cmhy873fc0001jv04amj1zy1j` | DRAFT -> RENDERED |
| 2 | `cmni86i5b001hswt2ca2lx7lf` | `cmhy873fc0001jv04amj1zy1j` | DRAFT -> RENDERED |

### Renders

| # | Render URL | Size |
|---|-----------|------|
| 1 | https://sqc9qfyearji7bel.public.blob.vercel-storage.com/posts/rendered/cmni86epx001dswt2xc7wmhc9-1775179741456.png | 89 KB |
| 2 | https://sqc9qfyearji7bel.public.blob.vercel-storage.com/posts/rendered/cmni86i5b001hswt2ca2lx7lf-1775179744101.png | 89 KB |

**Nota:** Ambos renders tem 89KB, o que pode indicar que as imagens do Drive nao foram carregadas como background (a Pagina 1 do template 58 nao possui uma layer de imagem com `isDynamic: true`). O template pode precisar de ajuste para suportar imagens dinamicas via `_driveImageId`. Recomenda-se verificar visualmente os renders.

---

## Fase 4: Agendamento

### Grade final - Quarta 09/04/2026

| # | Horario (BRT) | Tema | Titulo | Post ID | Status | Render |
|---|--------------|------|--------|---------|--------|--------|
| 1 | 11:22 | Picanha | PICANHA NA BRASA | `cmni86epx001dswt2xc7wmhc9` | SCHEDULED | RENDERED |
| 2 | 12:47 | Costela | COSTELA NO BAFO | `cmni86i5b001hswt2ca2lx7lf` | SCHEDULED | RENDERED |

### Horarios escolhidos
- **11:22** - Horario de almoco, minutos variados para parecer organico
- **12:47** - Pico do almoco, espacamento de ~1h25 entre stories

---

## Mapeamento Template -> Copy

| Campo Copy | Slot do Template | Notas |
|---|---|---|
| Titulo principal | `Texto - Titulo Principal Copy` | Aplicado a 3 layers com mesmo nome (headline, titulo, subtitulo) |
| Preco/Promocao | `Texto - Titulo Principal Copy Copy` | Rich-text com preco riscado + preco novo |
| Imagem fundo | `_driveImageId` | ID do Google Drive |

---

## Observacoes

1. **Template 58 (Espeto Gaucho)** tem layer names duplicados ("Texto - Titulo Principal Copy" aparece 3 vezes), o que limita a customizacao individual de cada campo. O slotValue aplica o mesmo texto em todas as layers com o mesmo nome.
2. **Sem layer dinamica de imagem**: A Pagina 1 nao possui layer com `isDynamic: true`, entao o `_driveImageId` pode nao ter sido aplicado como background. Verificar visualmente.
3. **Horarios organicos**: Minutos variados (22 e 47) para evitar padrao de bot.
4. **Promocoes incluidas**: Picanha 500g de R$104,50 por R$84,99 e Costela no Bafo 1kg de R$149,00 por R$99,90 (valores do KB).

## Ferramentas MCP utilizadas
- `list-projects` - Identificar projeto
- `get-knowledge(projectId: 6)` - Carregar KB completo
- `list-templates(projectId: 6)` - Listar templates
- `get-template-pages(templateId: 58, includeLayerDetails: true)` - Inspecionar layers
- `list-posts(projectId: 6, status: "SCHEDULED", dateFrom: "2026-04-09")` - Verificar grade existente
- `create-post` x2 - Criar stories como DRAFT
- `render-story` x2 - Renderizar criativos
- `update-post` x2 - Mudar status para SCHEDULED
- `list-posts` - Verificacao final
