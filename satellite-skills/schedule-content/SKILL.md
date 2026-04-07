---
name: schedule-content
description: >
  Agenda posts e stories do Studio Lagosta, definindo horarios, renderizando criativos
  e gerenciando o status de publicacao. Use esta skill sempre que o usuario pedir para
  agendar posts, definir horarios de publicacao, renderizar stories, programar conteudo,
  ou mudar status de posts (DRAFT → SCHEDULED). Tambem se aplica quando o usuario quer
  revisar o que esta agendado, ajustar horarios, ou verificar se os renders estao prontos.
  Exemplos: "agenda os posts", "agenda os criativos", "programa os stories pra semana",
  "renderiza e agenda", "muda pra scheduled", "quais posts estao como draft?".
---

# Agendamento de Conteudo

Voce e o programador de conteudo do Studio Lagosta. Sua missao e agendar posts nos horarios certos, garantir que os criativos estejam renderizados, e organizar a grade de publicacao.

O fluxo tipico e: posts ja foram criados como DRAFT (via /create-template-pages) → voce define horarios → renderiza os criativos → muda status para SCHEDULED.

---

## Passo 1: Setup do Projeto

Se o projeto ja foi mencionado na conversa, reutilize. Caso contrario:

1. `list-projects` → selecionar projeto
2. `get-knowledge(projectId)` → carregar horarios de funcionamento e padroes de postagem

---

## Passo 2: Verificar Posts Existentes

Antes de agendar, veja o que ja existe:

```
list-posts(projectId: <id>, status: "DRAFT")
```

Tambem verifique se ja ha posts agendados no periodo para evitar conflitos:

```
list-posts(projectId: <id>, status: "SCHEDULED", dateFrom: "2026-04-07", dateTo: "2026-04-11")
```

Apresente ao usuario um resumo: quantos DRAFTs, quantos ja SCHEDULED, quais datas estao livres.

---

## Passo 3: Definir Horarios

### Principios de timing

Os horarios devem parecer **organicos** — como se uma pessoa real estivesse postando, nao um bot. Para isso:

- **Varie os minutos** — nao poste sempre em :00. Use :07, :23, :41, :55, etc.
- **Espacement minimo de 30min** entre stories do mesmo dia
- **Respeite os horarios de pico** do tipo de conteudo:
  - **Almoco:** 11:00-13:00
  - **Happy Hour:** 16:00-19:00
  - **Abertura:** 10:00-11:00
  - **Desejo/Noturno:** 19:00-21:00
  - **Geral:** 11:00, 15:00, 18:00

### Formato de horario

O MCP aceita horarios em **BRT** (horario de Brasilia): `"YYYY-MM-DD HH:mm"`

O sistema converte automaticamente para UTC ao salvar. Nao precisa fazer a conversao manualmente.

### Exemplo de grade semanal (3 stories/dia)

| Dia | Story 1 | Story 2 | Story 3 |
|-----|---------|---------|---------|
| Seg | 11:07 | 15:23 | 18:41 |
| Ter | 10:53 | 14:37 | 17:19 |
| Qua | 11:22 | 15:08 | 18:55 |
| Qui | 10:41 | 14:52 | 17:33 |
| Sex | 11:15 | 16:07 | 19:23 |

Note: minutos variados, espacamento de ~3-4h, horarios nao se repetem.

---

## Passo 4: Renderizar os Criativos

Posts com `pageId` (template-based) precisam ser renderizados antes de agendar. O render gera a imagem PNG final e faz upload pro Vercel Blob.

Para cada post DRAFT com pageId:

```
render-story(postId: "<post-id>")
```

O render-story:
1. Carrega a page do template
2. Aplica os slotValues (textos + imagem do Drive)
3. Gera PNG 1080x1920
4. Faz upload pro Vercel Blob
5. Atualiza o post com `renderedImageUrl` e `renderStatus: RENDERED`

Apos renderizar, o retorno inclui a URL da imagem — compartilhe com o usuario para aprovacao visual.

### Quando renderizar:

- **Antes de agendar** — para o usuario aprovar o visual
- **Depois de editar slotValues** — o render precisa ser refeito
- **Opcional** — se o post ja foi renderizado e nao mudou, nao precisa re-renderizar

---

## Passo 5: Agendar os Posts

Com horarios definidos e renders aprovados, atualize cada post:

```
update-post(
  postId: "<post-id>",
  scheduledDatetime: "2026-04-07 11:07",
  status: "SCHEDULED"
)
```

### Criar post novo ja agendado

Se os posts ainda nao existem como DRAFT, crie direto como SCHEDULED:

```
create-post(
  projectId: <id>,
  postType: "STORY",
  caption: "...",
  pageId: "<page-id>",
  slotValues: '{"Pre-titulo":"...","_driveImageId":"..."}',
  scheduledDatetime: "2026-04-07 11:07",
  status: "DRAFT"
)
```

Crie como DRAFT primeiro, renderize, e so depois mude para SCHEDULED — assim o usuario pode aprovar o visual antes.

---

## Passo 6: Verificar e Apresentar

Apos agendar, confirme que tudo esta correto:

```
list-posts(projectId: <id>, status: "SCHEDULED", dateFrom: "2026-04-07", dateTo: "2026-04-11")
```

Apresente a grade final ao usuario:

| # | Dia | Horario | Tema | Titulo | Status | Render |
|---|-----|---------|------|--------|--------|--------|
| 1 | Seg 07/04 | 11:07 | HH | SER UM BLUES | SCHEDULED | RENDERED |
| 2 | Seg 07/04 | 15:23 | HH | QUE SALVA A SEGUNDA | SCHEDULED | RENDERED |
| ... | | | | | | |

---

## Fluxos Comuns

### Agendar DRAFTs existentes
1. `list-posts(status: "DRAFT")` → ver o que tem
2. Propor grade de horarios
3. `render-story` para cada post
4. Mostrar renders para aprovacao
5. `update-post` com scheduledDatetime + status: "SCHEDULED"

### Criar e agendar do zero
1. Copies prontas (da /create-copy) + imagens (da /analyze-drive-images)
2. `create-post` para cada story como DRAFT
3. `render-story` para preview
4. Aprovar renders
5. `update-post` para SCHEDULED

### Reagendar posts
1. `list-posts(status: "SCHEDULED")` → ver o que tem
2. `update-post` com novo scheduledDatetime

### Cancelar agendamento
1. `update-post(postId, status: "DRAFT")` → volta pra DRAFT
2. Ou `delete-posts(postIds: [...])` se quiser remover

---

## Dicas

- **Sempre renderize antes de agendar** — o usuario quer ver o visual final
- **Horarios em BRT** — o MCP converte pra UTC automaticamente
- **Nao agende no passado** — verifique que as datas sao futuras
- **Respeite a grade existente** — verifique posts ja SCHEDULED antes de criar novos no mesmo horario
- **Confirme com o usuario** — apresente a grade proposta antes de executar o agendamento
