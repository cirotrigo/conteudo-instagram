# Formato de Layers

Referencia rapida do formato de layers usados nos templates do Studio Lagosta.

## Estrutura de uma Layer

```json
{
  "id": "layer-unique-id",
  "name": "Pre-titulo",
  "type": "text",
  "content": "TEXTO AQUI",
  "x": 100,
  "y": 200,
  "width": 880,
  "height": 80,
  "fontSize": 24,
  "fontFamily": "Montserrat",
  "fontWeight": "bold",
  "fill": "#FFFFFF",
  "textAlign": "center",
  "isDynamic": false,
  "visible": true
}
```

## Tipos de Layer

| type | Descricao | Campos relevantes |
|------|-----------|-------------------|
| `text` | Texto editavel | `content`, `fontSize`, `fontFamily`, `fill`, `textAlign` |
| `image` | Imagem | `fileUrl`, `isDynamic` |
| `shape` | Forma geometrica | `fill`, `stroke`, `opacity` |

## Layers de Imagem Dinamica

Layers com `type: "image"` e `isDynamic: true` sao slots para fotos do Drive. O `render-story` automaticamente resolve `_driveImageId` e aplica o thumbnail em alta resolucao nessa layer.

```json
{
  "id": "bg-img",
  "name": "Imagem - Background",
  "type": "image",
  "fileUrl": "",
  "isDynamic": true,
  "x": 0,
  "y": 0,
  "width": 1080,
  "height": 1920
}
```

## slotValues e Match de Layers

O `applySlotValues` faz match por `layer.id` ou `layer.name`:

```javascript
const slot = slotValues[layer.id] ?? slotValues[layer.name]
```

### Formato simples (string):
```json
{"Pre-titulo": "TEXTO NOVO"}
```
→ Substitui `layer.content` da layer com name "Pre-titulo"

### Formato objeto:
```json
{"bg-img": {"fileUrl": "https://blob.vercel-storage.com/..."}}
```
→ Substitui `layer.fileUrl`

### Campo especial `_driveImageId`:
```json
{"_driveImageId": "1DmPSXqjnby2WAbKvjwZLw-f7PWV8uYb0"}
```
→ Nao e um layer — e processado pelo `render-story` que busca a imagem no Drive e aplica na primeira layer `isDynamic: true`
