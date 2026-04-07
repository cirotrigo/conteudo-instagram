# Guia do Sistema revisao-story.html

## 1. Visao Geral

O `revisao-story.html` e o previewer/editor interativo de Stories do Instagram do Studio Lagosta. Ele permite:

- **Editar textos** diretamente nos campos (headline, body, pre-titulo, CTA, etc.)
- **Trocar imagens** do acervo no Google Drive via modal de busca
- **Ajustar overlays** (cor, intensidade, direcao do gradiente)
- **Controlar tamanho de fontes** com botoes [−] [+] por campo (FontScale)
- **Copiar output formatado** para colar de volta no Claude (botao "Copiar tudo")

### Localizacao dos arquivos

- **Template base**: `~/.claude/skills/conteudo-instagram/revisao-story.html`
- **Copias por projeto**: `~/.claude/skills/conteudo-instagram/projects/{id}-{slug}/revisao-story.html` (com Design System inline)

---

## 2. Arquitetura

### Arquivos necessarios

O revisao-story.html depende de 3 arquivos JavaScript externos (ou DS inline no HTML):

| Arquivo | Conteudo |
|---------|----------|
| `design.js` | Paleta de cores, tipografia (fontes base64), logo base64, storyTemplates |
| `slides.js` | Array de stories (S[]) com textos, imagens e configuracoes |
| `gallery.js` | Todas as imagens do Drive para troca via modal |

### Estrutura dos dados

```javascript
// design.js exporta:
const DS = {
  palette: { brand: '#...', accent: '#...', dark: '#...', light: '#...' },
  typography: { headline: { family, weight, base64 }, body: { ... } },
  logoB64: 'data:image/png;base64,...',
  storyTemplates: { S1: {...}, S2: {...}, ... S15: {...} }
};

// slides.js exporta:
const META = { project: 'Nome', slug: 'slug' };
const S = [
  { id: 'S1', template: 'S1', headline: '...', body: '...', img: { id, url, name }, ... },
  ...
];

// gallery.js exporta:
const G = [
  { id: 'driveFileId', name: 'foto.jpg', thumb: '/thumb?id=DRIVE_FILE_ID' },
  ...
];

// FontScale (dentro de cada slide):
const FC = { headline: 1.0, body: 1.0, pretitle: 1.0, cta: 1.0, badge: 1.0 };
```

---

## 3. Como Usar para um Novo Projeto

### 3.1 Preparar dados

1. **Carregar assets do projeto** via MCP:
   - `get-brand-assets` para obter `brand.json` e `design-system.json`
   - Logo e fontes em base64

2. **Gerar `design.js`** com:
   - `palette` (cores brand, accent, dark, light)
   - `typography` (familias de fonte com src base64)
   - `logoB64` (logo em data URI)
   - `storyTemplates` (configuracoes S1-S15)

3. **Gerar `gallery.js`** com imagens do Drive:
   - Usar MCP `list-drive-images` com `limit=500`
   - Thumbnails devem usar URL de proxy local: `/thumb?id=DRIVE_FILE_ID`

4. **Gerar `slides.js`** com os stories:
   - Array S[] com textos pre-preenchidos
   - Imagens pre-selecionadas do acervo
   - META com nome e slug do projeto

### 3.2 Servidor Proxy (server.py)

O servidor proxy e **necessario** porque thumbnails do Google Drive (`lh3.googleusercontent.com`) retornam 403 sem autenticacao.

**O que o server.py faz:**
- Proxy autenticado via OAuth (refresh token do `.env`)
- Cache em disco (`.thumb-cache/`) para evitar requests repetidos
- Serve arquivos estaticos (HTML, JS, CSS)
- Roda em `localhost:8787`

**Comandos para iniciar:**

```bash
# Matar processo anterior na porta 8787
lsof -ti:8787 | xargs kill -9 2>/dev/null

# Iniciar servidor e abrir no browser
cd /tmp/{dir-do-projeto} && python3 server.py &
open http://localhost:8787/revisao-story.html
```

### 3.3 Fluxo de Revisao

1. Abrir `http://localhost:8787/revisao-story.html` no browser
2. **Editar textos**: clicar nos campos de input e alterar headline, body, CTA, etc.
3. **Ajustar FontScale**: usar botoes [−] [+] ao lado de cada campo (step 10%, range 50%-200%)
4. **Trocar overlay**: ajustar cor, intensidade e direcao do gradiente
5. **Trocar imagens**: clicar "Buscar no Drive" para abrir modal com galeria completa
6. **Finalizar**: clicar **"Copiar tudo"** e colar o output no Claude

### 3.4 Exportacao para PNG

Apos o usuario colar o output do "Copiar tudo", o fluxo de exportacao e:

1. **Parsear o copy output** — extrair textos, imagens e FontScale de cada slide
2. **Respeitar FontScale** — formula: `base_preview * 2 * fontScale`
3. **Baixar imagens do Drive** como base64 via OAuth (cache em `.cache-{fileId}`)
4. **Gerar HTMLs individuais** — resolucao base 405x720px, fontes e logo embutidos em base64
5. **Exportar via Playwright**:
   - Viewport: 405x720px
   - `device_scale_factor`: 1080/405 = 2.667
   - Resultado: PNGs 1080x1920px
6. **Output**: arquivos salvos em `~/Downloads/story-{slug}/`

---

## 4. Templates Disponiveis (S1-S15)

| Template | Nome | Descricao |
|----------|------|-----------|
| S1 | Centered Focus | Overlay bottom, texto centralizado |
| S2 | Editorial Asymmetric | Overlay left, texto a esquerda |
| S3 | Info / List | Overlay bottom, lista de itens |
| S4 | Production Tip | Overlay bottom, badge + CTA outline |
| S5 | Production Setup | Overlay bottom, badge accent + info rows |
| S6 | Final Result / Promo | Dual overlay ou gradiente brand |
| S7 | Testimonial | Dual overlay, citacao centralizada |
| S8 | Highlight Product | Overlay left, preco em destaque |
| S9 | Weekly Schedule | Overlay bottom 70%, tabela elegante |
| S10 | Oferta Explosiva | Overlay bottom, desconto agressivo |
| S11 | Promo Topo | Overlay top, glass pill precos, logo rodape |
| S12 | Promo Lateral | Overlay bottom, border-left accent, badge outline |
| S13 | Promo Card | Glassmorphism card com blur |
| S14 | Infos Centro | Dual overlay, icones SVG, logo watermark |
| S15 | Infos Lateral | Dual overlay, border-left, info rows + logo canto |

---

## 5. FontScale

O FontScale permite ajuste fino do tamanho de cada campo de texto individualmente.

### Controles
- Botoes **[−]** e **[+]** ao lado de cada campo de texto
- Step: 10% por clique
- Range: 50% a 200%

### Armazenamento
```javascript
s.fontScale = { headline: 1.3, body: 1.0, pretitle: 1.0, cta: 1.0, badge: 1.0 };
```

### Aplicacao no preview
```javascript
sz(base, key) = base * fontScale[key]
```

### Aplicacao na exportacao
```javascript
sz(base, key, fs) = base * 2 * fontScale[key]
```

### No copy output
Aparece formatado como:
```
FontScale: headline 130%, body 110%
```

---

## 6. Projetos Configurados

| ID | Slug | Pasta |
|----|------|-------|
| 6 | espeto-gaucho | `projects/6-espeto-gaucho/` |
| 8 | lagosta-criativa | `projects/8-lagosta-criativa/` |

---

## 7. Checklist para Novo Projeto

1. [ ] Criar pasta `projects/{id}-{slug}/`
2. [ ] Gerar `brand.json` (logo base64, fontes base64)
3. [ ] Gerar `design-system.json` (palette, typography, storyTemplates S1-S15)
4. [ ] Copiar fontes para `projects/{id}-{slug}/fonts/`
5. [ ] Copiar `revisao-story.html` base para a pasta do projeto (ou usar com `design.js` externo)
6. [ ] Gerar `gallery.js` com imagens do Drive via `list-drive-images`
7. [ ] Configurar `server.py` com credenciais OAuth do projeto
8. [ ] Testar preview em `localhost:8787`
9. [ ] Testar exportacao para PNG via Playwright
