# Clone Page Layout - Espeto Gaucho (Jardim Camburi)

## Resumo da Tarefa

Clonar a primeira page do template existente do Espeto Gaucho e alterar o texto fixo do Rodape-1 para: **"Av. Ranulpho, 111 - Jardim Camburi"**.

## Caminho Utilizado: Caminho B (criar page nova com layers clonadas)

### Passo 1: Identificacao do Projeto e Template

- **Projeto**: Espeto Gaucho (projectId: 6)
- **Template base**: IA (templateId: 58)
- **Page base**: Pagina 1 (pageId: `cmhy873fc0001jv04amj1zy1j`)

### Passo 2: Layers da Page Base (carregadas com includeLayerDetails: true)

A primeira page do template 58 possui 7 layers:

| Order | Name | Type |
|-------|------|------|
| 0 | Gradiente - Preto para Transparente (Baixo) | gradient |
| 1 | Gradiente - Preto para Transparente (Cima) | gradient |
| 2 | Texto - Titulo Principal Copy | text (content: "ESPETO DE CORACAO") |
| 3 | Texto - Titulo Principal Copy | text (content: "promocoes a partir das 17h") |
| 4 | Texto - Titulo Principal Copy Copy | rich-text (content: "de R$ 39,00 por R$ 29,90") |
| 5 | Texto - Titulo Principal Copy | text (content: "QUINTA PEDE UMA PROMOCAO DE RESPEITO") |
| 6 | Logo - logo-espeto-g.png | logo |

### Passo 3: Modificacao - Adicionar Layer Rodape-1

Uma nova layer de texto foi adicionada como order 7 com o nome "Rodape-1" e o conteudo fixo solicitado.

**Nova layer adicionada:**

```json
{
  "id": "rodape-1-layer",
  "name": "Rodape-1",
  "size": { "width": 800, "height": 60 },
  "type": "text",
  "order": 7,
  "style": {
    "align": "center",
    "color": "#FFFFFF",
    "fontSize": 28,
    "fontStyle": "normal",
    "textAlign": "center",
    "fontFamily": "Montserrat",
    "fontWeight": "normal",
    "lineHeight": 1,
    "letterSpacing": 1
  },
  "locked": false,
  "content": "Av. Ranulpho, 111 - Jardim Camburi",
  "visible": true,
  "position": { "x": 140, "y": 1840 },
  "rotation": 0,
  "textboxConfig": {
    "autoWrap": {
      "breakMode": "word",
      "autoExpand": false,
      "lineHeight": 1.2
    },
    "textMode": "auto-wrap-fixed"
  }
}
```

### Passo 4: Chamada create-page

A chamada para criar a nova page seria:

```
create-page(
  templateId: 58,
  name: "Espeto Gaucho - Jardim Camburi",
  tags: ["Jardim Camburi"],
  layers: '<JSON string com as 8 layers - 7 clonadas + 1 Rodape-1 nova>'
)
```

**Parametro `layers` (JSON string completo):**

```json
[
  {
    "id": "122bddda-1499-40ed-a621-b5966684148e",
    "name": "Gradiente - Preto para Transparente (Baixo)",
    "size": { "width": 1080, "height": 1920 },
    "type": "gradient",
    "order": 0,
    "style": {
      "gradientType": "linear",
      "gradientAngle": 0,
      "gradientStops": [
        { "id": "1", "color": "#000000", "opacity": 0.86, "position": 0 },
        { "id": "2", "color": "#000000", "opacity": 0, "position": 0.29 }
      ]
    },
    "locked": false,
    "visible": true,
    "position": { "x": 0, "y": 0 }
  },
  {
    "id": "77c1a56a-2633-4355-92e7-14ec9439aa7e",
    "name": "Gradiente - Preto para Transparente (Cima)",
    "size": { "width": 1080, "height": 1920 },
    "type": "gradient",
    "order": 1,
    "style": {
      "gradientType": "linear",
      "gradientAngle": 181,
      "gradientStops": [
        { "id": "1", "color": "#000000", "opacity": 0.84, "position": 0 },
        { "id": "2", "color": "#000000", "opacity": 0, "position": 0.33 }
      ]
    },
    "locked": false,
    "visible": true,
    "position": { "x": 0, "y": 0 }
  },
  {
    "id": "3a174796-f026-45b1-bb14-bbf063a18e8b",
    "name": "Texto - Titulo Principal Copy",
    "size": { "width": 702, "height": 118 },
    "type": "text",
    "order": 2,
    "style": {
      "align": "center",
      "color": "#FFFFFF",
      "fontSize": 121,
      "textAlign": "center",
      "fontFamily": "Roadhawk 900 Black",
      "fontWeight": "100",
      "lineHeight": 1,
      "letterSpacing": 1,
      "textTransform": "uppercase"
    },
    "locked": false,
    "content": "ESPETO DE CORACAO",
    "effects": {
      "shadow": {
        "enabled": true,
        "shadowBlur": 11,
        "shadowColor": "#000000",
        "shadowOffsetX": 12,
        "shadowOffsetY": 5,
        "shadowOpacity": 0.5
      }
    },
    "visible": true,
    "position": { "x": 189, "y": 1520 },
    "rotation": 0,
    "textboxConfig": {
      "autoWrap": { "breakMode": "word", "autoExpand": false, "lineHeight": 1.2 },
      "textMode": "auto-wrap-fixed"
    }
  },
  {
    "id": "531c98f7-ebe0-4b69-bbbf-ad4464e761d1",
    "name": "Texto - Titulo Principal Copy",
    "size": { "width": 784, "height": 78 },
    "type": "text",
    "order": 3,
    "style": {
      "align": "center",
      "color": "#FFFFFF",
      "fontSize": 38,
      "fontStyle": "normal",
      "textAlign": "center",
      "fontFamily": "Montserrat",
      "fontWeight": "bold",
      "lineHeight": 1,
      "textTransform": "uppercase"
    },
    "locked": false,
    "content": "promocoes a partir das 17h",
    "visible": true,
    "position": { "x": 148, "y": 1730 },
    "rotation": 0,
    "textboxConfig": {
      "autoWrap": { "breakMode": "word", "autoExpand": false, "lineHeight": 1.2 },
      "textMode": "auto-wrap-fixed"
    }
  },
  {
    "id": "3095c4ca-2338-45d6-84e5-3569797ebd34",
    "name": "Texto - Titulo Principal Copy Copy",
    "size": { "width": 763, "height": 69 },
    "type": "rich-text",
    "order": 4,
    "style": {
      "align": "center",
      "color": "#F4301A",
      "fontSize": 41,
      "fontStyle": "normal",
      "textAlign": "center",
      "fontFamily": "Montserrat",
      "fontWeight": "bold",
      "lineHeight": 1,
      "textTransform": "uppercase"
    },
    "locked": false,
    "content": "de R$ 39,00 por R$ 29,90",
    "effects": {
      "shadow": {
        "enabled": true,
        "shadowBlur": 13,
        "shadowColor": "#000000",
        "shadowOffsetX": 5,
        "shadowOffsetY": 3,
        "shadowOpacity": 0.5
      }
    },
    "visible": true,
    "position": { "x": 158.5, "y": 1661 },
    "rotation": 0,
    "textboxConfig": {
      "autoWrap": { "breakMode": "word", "autoExpand": false, "lineHeight": 1.2 },
      "textMode": "auto-wrap-fixed"
    },
    "richTextStyles": [
      { "end": 12, "start": 3, "textDecoration": "line-through" },
      { "end": 24, "fill": "#33e136", "start": 16, "fontStyle": "bold" }
    ]
  },
  {
    "id": "f302b53f-20d0-407f-9304-fee6fb685baa",
    "name": "Texto - Titulo Principal Copy",
    "size": { "width": 684, "height": 187 },
    "type": "text",
    "order": 5,
    "style": {
      "align": "center",
      "color": "#FFFFFF",
      "fontSize": 50,
      "fontStyle": "normal",
      "textAlign": "left",
      "fontFamily": "Montserrat",
      "fontWeight": "normal",
      "lineHeight": 1,
      "letterSpacing": 1,
      "textTransform": "uppercase"
    },
    "locked": false,
    "content": "QUINTA PEDE UMA PROMOCAO DE RESPEITO",
    "effects": {
      "shadow": {
        "enabled": true,
        "shadowBlur": 10,
        "shadowColor": "#000000",
        "shadowOffsetX": 5,
        "shadowOffsetY": 5,
        "shadowOpacity": 0.5
      }
    },
    "visible": true,
    "position": { "x": 75, "y": 172 },
    "rotation": 0,
    "textboxConfig": {
      "autoWrap": { "breakMode": "word", "autoExpand": false, "lineHeight": 1.2 },
      "textMode": "auto-wrap-fixed"
    }
  },
  {
    "id": "fcefd3c9-8029-4f03-a369-0cf1de6c163b",
    "name": "Logo - logo-espeto-g.png",
    "size": { "width": 153, "height": 168 },
    "type": "logo",
    "order": 6,
    "style": {
      "blur": 0,
      "border": { "color": "#000000", "width": 0, "radius": 0 },
      "contrast": 0,
      "objectFit": "cover",
      "brightness": 0
    },
    "locked": false,
    "fileUrl": "https://sqc9qfyearji7bel.public.blob.vercel-storage.com/projects/6/logos/1760564487128-logo-espeto-g.png",
    "visible": true,
    "position": { "x": 817, "y": 172 },
    "rotation": 0
  },
  {
    "id": "rodape-1-layer",
    "name": "Rodape-1",
    "size": { "width": 800, "height": 60 },
    "type": "text",
    "order": 7,
    "style": {
      "align": "center",
      "color": "#FFFFFF",
      "fontSize": 28,
      "fontStyle": "normal",
      "textAlign": "center",
      "fontFamily": "Montserrat",
      "fontWeight": "normal",
      "lineHeight": 1,
      "letterSpacing": 1
    },
    "locked": false,
    "content": "Av. Ranulpho, 111 - Jardim Camburi",
    "visible": true,
    "position": { "x": 140, "y": 1840 },
    "rotation": 0,
    "textboxConfig": {
      "autoWrap": { "breakMode": "word", "autoExpand": false, "lineHeight": 1.2 },
      "textMode": "auto-wrap-fixed"
    }
  }
]
```

### Status

A chamada `create-page` foi preparada mas nao foi executada porque a permissao para o MCP tool `create-page` foi negada durante a sessao. Para concluir, execute a chamada acima via MCP ou diretamente no Studio Lagosta.

### Notas

- Nenhum dos templates existentes do Espeto Gaucho (projectId: 6) possuia uma layer chamada "Rodape-1". Os templates usam o padrao de nomes "Texto - Titulo Principal", "Texto - Titulo", etc.
- A layer "Rodape-1" foi criada como nova layer de texto (order 7), posicionada na parte inferior do Story (y: 1840), com fonte Montserrat 28px branca, centralizada.
- Todos os IDs de layers originais foram mantidos. A layer nova recebeu o id `rodape-1-layer`.
- O canvas e 1080x1920 (padrao Story).
