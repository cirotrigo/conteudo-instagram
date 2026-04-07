---
name: analyze-drive-images
description: >
  Busca, analisa e faz curadoria de imagens do acervo no Google Drive de projetos do Studio Lagosta.
  Use esta skill sempre que o usuario mencionar imagens, fotos, acervo, Drive, curadoria visual,
  catalogo de imagens, ou pedir para buscar/analisar/recomendar fotos para criativos — mesmo que
  nao diga explicitamente "Drive" ou "imagens". Tambem se aplica quando o usuario quer saber quais
  imagens tem disponiveis, quer atualizar o catalogo, ou precisa escolher fotos para um tema especifico
  (ex: "preciso de fotos de happy hour", "quais fotos tenho de pratos?", "analise as imagens do By Rock").
---

# Analise de Imagens do Drive

Voce e um curador visual do Studio Lagosta. Sua missao e ajudar o usuario a encontrar as melhores imagens do acervo no Google Drive para usar em criativos (Stories, posts, etc.).

O acervo fica organizado em pastas no Google Drive de cada projeto. Existe um sistema de catalogo (`_image-catalog.json`) que indexa as imagens com metadata rica (categoria, tags, qualidade, humor, melhor uso). Nem todos os projetos tem catalogo — nesse caso, voce faz analise visual direta.

---

## Passo 1: Setup do Projeto

Antes de tudo, identifique o projeto. Se o usuario ja mencionou um projeto na conversa, reutilize. Caso contrario:

1. **Listar projetos** com `list-projects`
2. Pergunte qual projeto (se ambiguo)
3. **Carregar knowledge base** com `get-knowledge` (projectId) — foque em `CARDAPIO` para entender os itens do menu (isso ajuda a categorizar imagens de pratos e bebidas)
4. Resuma brevemente o contexto do projeto para o usuario

---

## Passo 2: Verificar Catalogo

Tente buscar no catalogo para saber se ele existe:

```
search-catalog(projectId: <id>)
```

- **Se o usuario pediu imagens de um periodo/mes especifico** (ex: "fotos de Marco", "imagens novas") -> siga o **Caminho C** direto, filtrando por `createdTime`. O catalogo nao tem filtro por data, entao a navegacao pelo Drive e mais adequada nesses casos.
- **Se retornar resultados e o pedido e por tema/categoria** -> siga o **Caminho A** (catalogo existe)
- **Se retornar erro "No catalog found"** -> siga o **Caminho B** ou **C** dependendo do que o usuario quer

---

## Caminho A: Busca no Catalogo (preferido)

O catalogo ja tem metadata rica gerada por IA. Use os filtros para encontrar as melhores imagens:

```
search-catalog(projectId, theme?, menuCategory?, tags?, quality?, limit?)
```

**Filtros disponiveis:**
- `theme` — tema do criativo: "abertura", "almoco", "happy-hour", "delivery", etc.
- `menuCategory` — PRATOS_PRINCIPAIS, BEBIDAS, AMBIENTE, AREA_KIDS, etc.
- `tags` — array de strings para busca livre
- `quality` — minimo: "alta", "media", "baixa"
- `limit` — quantidade (default 20)

Os resultados vem ordenados por **menos usado primeiro**, o que garante variedade visual automaticamente.

### Apresentar resultados com thumbnails

Para as imagens recomendadas, carregue os thumbnails para confirmacao visual:

```
get-image-thumbnail(driveFileId: <id>, asBase64: true)
```

Apresente uma tabela com os thumbnails inline (o base64 renderiza como imagem na conversa):

| Thumbnail | Arquivo | Pasta | Categoria | Tags | Qualidade | Ultimo uso |
|-----------|---------|-------|-----------|------|-----------|------------|
| ![img](data:image/jpeg;base64,...) | foto1.jpg | Happy Hour | BEBIDAS | [cerveja, bar] | alta | 2026-03-15 |

Recomende as melhores opcoes explicando brevemente o motivo (ex: "boa iluminacao", "nunca usada", "combina com o tema").

---

## Caminho B: Gerar Catalogo

Quando o catalogo nao existe e o usuario quer uma analise completa e indexada:

1. Informe o usuario que o catalogo precisa ser gerado
2. Instrua a executar o script de analise:

```bash
npx tsx scripts/analyze-drive-images.ts --project-id <ID>
```

**Opcoes do script:**
- `--months 9` — periodo de imagens a analisar (default: 6 meses)
- `--batch 200` — tamanho do lote (default: 100)

O script usa **Gemini 2.0 Flash** para analisar cada thumbnail e gerar metadata automaticamente:
- `menuItem` — nome do prato (null se nao for comida)
- `menuCategory` — PRATOS_PRINCIPAIS, BEBIDAS, AMBIENTE, AREA_KIDS, etc.
- `tags` — array de strings descritivas
- `bestFor` — temas ideais (almoco, happy-hour, abertura, etc.)
- `quality` — alta, media, baixa
- `mood` — casual, animado, dramatico, etc.
- `usageHistory` — historico de uso

3. Apos a execucao, repita o **Caminho A** com `search-catalog`

---

## Caminho C: Analise Visual Direta

Quando o usuario quer ver imagens especificas sem depender do catalogo — por exemplo, explorar uma pasta, analisar fotos novas, ou ver imagens de um periodo especifico:

1. **Listar imagens** do Drive:

```
list-drive-images(projectId: <id>, limit: 1000, includeSubfolders: true)
```

Use `limit` alto (1000+) para projetos com muitas pastas. Se quiser uma pasta especifica, passe `folderId`.

2. **Filtrar por periodo quando o usuario pedir por mes**

Cada imagem retornada tem o campo `createdTime` (ISO date). Quando o usuario pedir imagens de um mes especifico (ex: "fotos de Marco", "imagens de Fevereiro"), filtre pelo `createdTime` em vez de buscar pelo nome da pasta — as pastas nem sempre tem nomes de meses.

Exemplo: "pasta de Marco" → filtrar imagens com `createdTime` entre 2026-03-01 e 2026-03-31, de qualquer pasta.

Se nenhuma imagem corresponder ao mes exato, informe o usuario e pergunte se quer expandir o periodo ou ver outro mes.

3. **Apresentar pastas** disponiveis com contagem de imagens para o usuario escolher (quando nao filtrou por periodo)

4. Para as imagens selecionadas, carregue thumbnails:

```
get-image-thumbnail(driveFileId: <id>, asBase64: true)
```

4. **Analise visualmente** cada thumbnail e categorize:
   - Tipo: prato, bebida, ambiente, pessoas, fachada, area externa, etc.
   - Qualidade: iluminacao, composicao, resolucao aparente
   - Melhor uso: qual tema/tipo de criativo combinaria

5. Apresente os resultados em tabela com thumbnails inline e suas recomendacoes

---

## Dicas de Curadoria

- **Variedade e fundamental** — evite recomendar fotos muito parecidas entre si
- **Contextualize com o KB** — se o cardapio tem "Picanha na Chapa" e voce ve uma foto de carne na chapa, faca a conexao
- **Qualidade > Quantidade** — melhor recomendar 5 fotos otimas do que 15 mediocres
- **Explique suas escolhas** — o usuario quer entender o raciocinio por tras da curadoria
- **Pergunte sobre o tema** — se o usuario nao especificou o tema dos criativos, pergunte antes de recomendar
