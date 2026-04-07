---
name: create-template-pages
description: >
  Cria paginas de template e monta criativos para Stories e posts do Studio Lagosta,
  conectando textos (slotValues), imagens do Drive e layouts de template.
  Use esta skill sempre que o usuario pedir para criar paginas, montar criativos, montar os stories,
  aplicar textos no template, vincular imagens aos templates, ou preparar posts visuais —
  mesmo que nao diga "template" explicitamente. Tambem se aplica quando o usuario quer alternar
  layouts, criar variacao visual entre stories, ou ajustar o design de um criativo.
  Exemplos: "monte os criativos", "crie as paginas dos stories", "aplica os textos no template",
  "prepara os stories pra semana".
---

# Criacao de Paginas de Template

Voce monta os criativos visuais do Studio Lagosta conectando tres elementos: **layout** (page do template), **textos** (slotValues da /create-copy), e **imagem** (foto do Drive da /analyze-drive-images).

O sistema funciona assim: cada post referencia uma `pageId` (layout visual) e recebe `slotValues` (textos + imagem) que sao aplicados sobre as layers do template no momento da renderizacao. Voce nao precisa editar layers manualmente na maioria dos casos.

---

## Passo 1: Setup do Projeto

Se o projeto ja foi mencionado na conversa, reutilize. Caso contrario:

1. `list-projects` → selecionar projeto
2. `get-knowledge(projectId)` → contexto basico
3. `list-templates(projectId)` → ver templates disponiveis com contagem de pages

---

## Passo 2: Carregar Templates e Pages

Para ver os layouts disponiveis:

```
get-template-pages(templateId: <id>, includeLayerDetails: true)
```

Isso retorna todas as pages do template com suas layers completas. Cada page e um layout visual diferente.

### O que observar em cada page:

- **Nome/tags** — indica o tema (ex: "happy-hour", "almoco", "desejo")
- **Layers de texto** — layers com `type: "text"` que tem `name` correspondendo aos campos de copy (Pre-titulo, Titulo, Subtitulo, Rodape-1, CTA, Badge)
- **Layers de imagem dinamica** — layers com `type: "image"` e `isDynamic: true` — sao os slots onde a foto do Drive sera inserida
- **Layer count** — mais layers = layout mais complexo

---

## Passo 3: Selecionar Page para Cada Post

Para cada post/story, selecione uma page do template:

### Criterios de selecao:

1. **Por tema** — se a page tem tags que correspondem ao tema do post (happy-hour, almoco, etc.)
2. **Por dia da semana** — pages podem ter nomes com dia da semana (legacy)
3. **Variedade visual** — alterne entre pages diferentes para evitar stories identicos. Se tem 5 pages, use todas antes de repetir
4. **Compatibilidade** — verifique se a page tem os slots de texto necessarios (Pre-titulo, Titulo, etc.)

### Dica: use `includeLayerDetails: false` primeiro

Chame `get-template-pages` sem layer details primeiro para ver a lista resumida (nome, tags, layer count). So carregue details completos da page que voce precisa inspecionar.

---

## Passo 4: Montar os slotValues

Os `slotValues` sao um JSON que mapeia nomes de layers para seus valores. E o mecanismo que conecta textos e imagens ao template visual.

### Formato:

```json
{
  "Pre-titulo": "AQUELA CROSTINHA",
  "Titulo": "QUE ESTALA NA PRIMEIRA MORDIDA",
  "Subtitulo": "Carne prensada na chapa, cheddar derretendo",
  "Rodape-1": "Happy Hour 16h - 20h",
  "CTA": "Pede o teu!",
  "Badge": "SMASH",
  "_driveImageId": "1DmPSXqjnby2WAbKvjwZLw-f7PWV8uYb0"
}
```

**Campos de texto:** Fazem match pelo `name` da layer no template. Os valores da /create-copy vao aqui diretamente.

**`_driveImageId`:** Campo especial — o ID do arquivo no Google Drive. Na renderizacao, o sistema automaticamente busca o thumbnail em alta resolucao (1920px) e aplica na primeira layer de imagem dinamica (`isDynamic: true`).

### Importante:
- Nao precisa fazer upload manual da imagem para Blob — o `render-story` resolve via `_driveImageId`
- Os nomes dos campos devem bater exatamente com os nomes das layers no template
- Se um campo nao existe na page, ele e ignorado silenciosamente

---

## Passo 5: Criar os Posts

### Caminho A: Reusar page existente (mais comum)

Quando ja existe uma page com layout adequado, crie o post diretamente referenciando ela:

```
create-post(
  projectId: <id>,
  postType: "STORY",
  caption: "Caption do Instagram...",
  pageId: "<page-id>",
  slotValues: '{"Pre-titulo":"...","Titulo":"...","_driveImageId":"..."}'
  status: "DRAFT"
)
```

O post sera criado como DRAFT com `renderStatus: PENDING`. Quando for hora de agendar, o `render-story` aplica os slotValues sobre a page e gera a imagem final.

**Este e o caminho preferido** — simples, rapido, e usa os layouts ja validados pelo designer.

### Caminho B: Criar page nova

Quando precisa de um layout customizado (ex: clonar uma page e ajustar layers):

1. Carregue a page base com `get-template-pages(templateId, includeLayerDetails: true)`
2. Copie as layers da page base
3. Modifique o que precisa (trocar textos fixos, ajustar posicoes, etc.)
4. Crie a nova page:

```
create-page(
  templateId: <id>,
  name: "Happy Hour - Variacao 2",
  layers: '<JSON string das layers>',
  tags: ["happy-hour"]
)
```

**Atencao com layers:**
- Layers sao **string JSON no banco** — sempre `JSON.parse()` antes de modificar e `JSON.stringify()` ao salvar
- Ao passar para `create-page`, o parametro `layers` deve ser uma **string JSON** (nao objeto)
- Mantenha todos os IDs de layers unicos se estiver clonando

---

## Passo 6: Verificar e Renderizar

Apos criar os posts:

1. **Verificar** com `list-posts(projectId, status: "DRAFT")` que todos foram criados corretamente
2. **Renderizar** com `render-story(postId)` para gerar a imagem final e verificar visualmente
3. Apresentar o resultado ao usuario — o `render-story` retorna a URL da imagem renderizada

---

## Alternando Layouts para Variedade Visual

Para uma serie de stories (ex: 15 stories na semana), alterne entre as pages disponiveis:

```
Posts 1, 4, 7, 10, 13 → Page A (layout principal)
Posts 2, 5, 8, 11, 14 → Page B (layout alternativo)
Posts 3, 6, 9, 12, 15 → Page C (layout variacao)
```

Se o template so tem 2 pages, alterne entre elas. O objetivo e que stories consecutivos nao tenham o mesmo layout visual.

---

## Resumo do Fluxo Tipico

1. `list-templates` → ver templates
2. `get-template-pages(templateId)` → ver pages disponiveis (sem layer details)
3. Para cada post da /create-copy:
   - Selecionar page (alternando para variedade)
   - Montar slotValues (textos + `_driveImageId`)
   - `create-post` com pageId + slotValues como DRAFT
4. `render-story` para verificar visualmente (opcional nesta etapa)
5. Apresentar resultado ao usuario
