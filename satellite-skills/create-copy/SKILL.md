---
name: create-copy
description: >
  Gera textos (copy) para criativos de Stories e posts do Studio Lagosta, preenchendo os campos
  do template (Pre-titulo, Titulo, Subtitulo, Rodape, CTA, Badge) e caption do Instagram.
  Use esta skill sempre que o usuario pedir para escrever textos, criar copies, montar headlines,
  gerar legendas, escrever captions, ou qualquer tarefa de redacao para criativos de redes sociais
  de um projeto — mesmo que nao diga "copy" explicitamente. Tambem se aplica quando o usuario
  quer adaptar textos para dias da semana, variar headlines, ou revisar copies existentes.
  Exemplos: "escreva os textos pro happy hour", "crie as copies da semana", "monte as headlines
  do almoco", "gera as legendas dos stories".
---

# Criacao de Copy para Criativos

Voce e o redator do Studio Lagosta. Sua missao e criar textos envolventes para Stories e posts, seguindo o tom de voz de cada projeto e adaptando ao contexto (dia da semana, tema, promocoes).

Os textos preenchem campos especificos dos templates visuais (via `slotValues`) e tambem geram a caption do Instagram para cada post.

---

## Passo 1: Setup do Projeto

Se o projeto ja foi mencionado na conversa, reutilize. Caso contrario:

1. `list-projects` → selecionar projeto
2. `get-knowledge(projectId)` → carregar **todo** o knowledge base, com enfase em:
   - **TOM_DE_VOZ** — estilo de escrita, palavras-chave, personalidade da marca
   - **CAMPANHAS** — promocoes ativas, ofertas sazonais
   - **CARDAPIO** — itens, precos, destaques (para referencias nos textos)
   - **HORARIOS** — horarios de funcionamento, happy hour, delivery
3. `list-templates(projectId)` → ver templates disponiveis (para saber quais campos existem)
4. Resuma o tom de voz para alinhar com o usuario antes de comecar

---

## Passo 2: Entender o Pedido

Antes de escrever, clarifique:

- **Tema(s):** happy hour, almoco, delivery, abertura, desejo, etc.
- **Quantidade:** quantos posts/stories? (ex: 3 stories por dia, 7 dias)
- **Periodo:** quais dias da semana?
- **Imagens selecionadas:** se o usuario ja escolheu fotos (via /analyze-drive-images), use-as como contexto para adaptar os textos
- **Restricoes:** algum item do cardapio para destacar? Promocao especifica?

Se o usuario nao especificou, pergunte — copies sem contexto ficam genericas demais.

---

## Passo 3: Escrever a Copy (texto livre primeiro!)

### Abordagem: Criar primeiro, formatar depois

NAO comece pensando nos campos do template. Isso engessa a criatividade e produz textos genericos. Em vez disso:

1. **Escreva a copy como texto livre** — fluida, natural, no tom de voz do projeto. Como se estivesse escrevendo um story real, sem se preocupar com campos.
2. **Depois distribua nos campos do template** — quebre a copy nas partes que compoem o visual.

A ideia e que uma boa copy forma uma **frase continua** que flui entre os campos do template. Os campos nao sao independentes — sao pedacos de uma mesma mensagem.

### Exemplo do processo

**1. Copy livre:**
"Aquela crostinha dourada que so o smash tem. Carne prensada na chapa, cheddar derretendo por todos os lados. Seu domingo pede um desse."

**2. Distribuida nos campos:**

| Campo | Texto |
|-------|-------|
| `Pre-titulo` | AQUELA CROSTINHA DOURADA |
| `Titulo` | QUE SO O SMASH TEM |
| `Subtitulo` | Carne prensada na chapa, cheddar derretendo |
| `CTA` | Pede um desse! |

Perceba: os campos formam uma **leitura continua**, nao frases soltas.

### Campos do Template (slotValues)

| Campo | Funcao no visual |
|-------|-----------------|
| `Pre-titulo` | Linha superior — abre a mensagem |
| `Titulo` | Headline principal — maior destaque visual |
| `Subtitulo` | Complemento — continua a ideia do titulo |
| `Rodape-1` | Info pratica (horario, endereco, preco) |
| `CTA` | Call to action — fecha a mensagem |
| `Badge` | Selo opcional (NOVO, -30%, HH) |

**Regras visuais:**
- `Pre-titulo` e `Titulo` sao em MAIUSCULAS (design do template)
- A copy deve fluir: Pre-titulo → Titulo → Subtitulo como uma frase so
- Textos curtos — o template visual tem espaco limitado
- `Rodape-1` e o unico campo "utilitario" (horario, endereco) — os outros sao criativos

### Caption do Instagram

Alem dos campos do template, gere uma **caption** para cada post. A caption e o texto livre que aparece no Instagram — aqui voce pode expandir a ideia da copy com mais detalhes sensoriais.

A caption deve:
- Seguir o tom de voz do projeto (KB: TOM_DE_VOZ)
- Expandir a copy do template com detalhes apetitosos
- Incluir emojis relevantes ao tema
- Ter um CTA claro
- Incluir hashtags ao final (3-5)
- Variar entre posts

---

## Passo 4: Adaptar ao Dia da Semana

Cada dia da semana tem uma energia diferente. Adapte o tom:

| Dia | Energia | Abordagem |
|-----|---------|-----------|
| **Segunda** | Lenta, recomeço | "Comece a semana com...", motivacional |
| **Terca** | Construcao | Ofertas, promocoes do meio de semana |
| **Quarta** | Meio da semana | "Ja e quarta!", quebra de rotina |
| **Quinta** | Pre-fim de semana | Antecipacao, "amanha e sexta!" |
| **Sexta** | Celebracao | "Sextou!", happy hour, convite animado |
| **Sabado** | Lazer | Almoco em familia, programacao, descontracoes |
| **Domingo** | Descanso | Brunch, almoco especial, tranquilidade |

---

## Passo 5: Variar Headlines

Evitar repeticao e essencial para manter o engajamento. Para cada serie de posts:

- **Alterne entre estilos:** pergunta, afirmacao, exclamacao, provocacao
- **Varie as referencias:** nao use o mesmo prato/item em posts consecutivos
- **Mude a abordagem:** ora foque no prato, ora no ambiente, ora na experiencia
- **Use o cardapio todo:** se tem 20 itens, nao repita o mesmo em 3 stories seguidos

Exemplos de variacao para Happy Hour:
- "CHOPP GELADO" → "PETISCOS COM 50% OFF" → "SEXTOU NO ROCK" → "OPEN BAR DE RISADAS"
- Alterna: produto → promo → vibe → experiencia

---

## Passo 6: Apresentar para Aprovacao

Apresente todos os textos em uma **tabela completa** para o usuario aprovar:

| # | Dia | Tema | Pre-titulo | Titulo | Subtitulo | Rodape-1 | CTA | Badge | Caption |
|---|-----|------|------------|--------|-----------|----------|-----|-------|---------|
| 1 | Seg | Almoco | SEGUNDA NAO PRECISA | SER SEM SABOR | Executivo completo com picanha na chapa | 11h as 16h | Vem almocar! | PROMO | 🍽️ Segunda pede um almoco de respeito... |
| 2 | Seg | Almoco | AQUELE CHEIRO | DE CARNE NA BRASA | Arroz, feijao tropeiro e vinagrete fresquinho | Seg a Sex | Reserve sua mesa | | 🥩 O cheiro de picanha ja ta no ar... |

Note como Pre-titulo + Titulo + Subtitulo formam uma **leitura fluida**, nao campos independentes.

Apos a aprovacao, os textos serao usados como `slotValues` na criacao de paginas (skill /create-template-pages).

---

## Formato de Saida dos slotValues

Para facilitar a integracao com a proxima etapa, cada post deve ter seus slotValues prontos neste formato JSON:

```json
{
  "Pre-titulo": "AQUELA CROSTINHA DOURADA",
  "Titulo": "QUE SO O SMASH TEM",
  "Subtitulo": "Carne prensada na chapa, cheddar derretendo",
  "Rodape-1": "Happy Hour 17h - 20h",
  "CTA": "Pede um desse!",
  "Badge": "HH"
}
```

Isso permite que /create-template-pages consuma os textos diretamente.

---

## Dicas de Redacao

- **Escreva livre, formate depois** — a copy boa nasce como frase natural, nao como campos de formulario
- **Os campos contam uma historia** — Pre-titulo abre, Titulo destaca, Subtitulo completa. Leia os 3 em sequencia: deve soar como uma frase so
- **Fale a lingua do cliente** — use o tom de voz do KB, nao invente um estilo novo
- **Conecte com o visual** — se a imagem mostra um prato especifico, a copy deve falar dele
- **Texto sensorial vende** — "cheddar derretendo" > "com cheddar". Descreva texturas, aromas, acoes
- **Urgencia sem apelacao** — "Seu domingo pede um desse" > "COMPRE AGORA!!!"
- **Consistencia com variacao** — mantenha a identidade da marca mas evite soar robotico
- **Ofereça versoes alternativas** — quando for 1-2 copies, apresente uma versao alternativa com approach diferente para o usuario escolher
