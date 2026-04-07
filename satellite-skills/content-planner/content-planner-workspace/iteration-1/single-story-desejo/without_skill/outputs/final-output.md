# Story de Desejo - By Rock - Smash Burger (Domingo)

## Resultado da Execucao

| Campo | Valor |
|-------|-------|
| **Projeto** | By Rock (ID 7) |
| **Post ID** | `cmni86gzo001fswt2kx8r4xs8` |
| **Tipo** | STORY |
| **Tema** | Desejo (craving) |
| **Status** | SCHEDULED |
| **Agendado para** | 2026-04-05 11:00 BRT (Domingo) |
| **Render Status** | NOT_NEEDED (imagem direta do Drive) |

## Imagem Selecionada

| Campo | Valor |
|-------|-------|
| **Arquivo** | CMT08168.jpg |
| **Drive File ID** | `1dlmsU_d3m5BIpXOyi0JBydHn5zq2gf4Q` |
| **Pasta** | Burguer |
| **Item do Menu** | Smash Sample Burger |
| **Categoria** | BURGERS |
| **Qualidade** | Alta |
| **Descricao** | Smash burger com queijo cheddar derretido e pao brioche, servido com caneca de cerveja |
| **URL** | `https://drive.google.com/uc?id=1dlmsU_d3m5BIpXOyi0JBydHn5zq2gf4Q` |

## Copy / Caption

```
SMASH BURGER NO VOLUME MAXIMO

Carne prensada na chapa, cheddar derretendo, pao brioche selado na manteiga. O Smash Sample Burger do By Rock e daqueles que voce morde e ja quer o proximo.

Vem matar essa vontade.
Domingo o dia e nosso.

R. Eugenio Netto, 82 - Praia do Canto
Aberto das 11h a meia-noite
Delivery: pedido.anota.ai

#byrock #smashburger #burger #hamburger #domingao #praiadorock #vitoria #steakhouse #foodporn #rockandroll
```

## Decisoes Criativas

### Tom de Voz
- Seguiu o padrao By Rock: energetico, rock and roll, irreverente mas acolhedor
- "NO VOLUME MAXIMO" - expressao recorrente do perfil
- Linguagem direta e sensorial para provocar desejo

### Escolha da Imagem
- Selecionada via `search-catalog` com tags `["smash", "burger", "hamburger"]`
- CMT08168.jpg escolhida por ser a imagem com melhor composicao (smash burger + cerveja = desejo)
- Qualidade "alta" no catalogo
- Nunca usada antes (usageCount: 0)

### Horario
- 11:00 BRT - horario de almoco, ideal para story de desejo que provoca fome
- Alinhado com o padrao de postagem do By Rock (09:00, 11:00, 12:00)

### Abordagem
- Post criado como legacy (mediaUrls direto do Drive) em vez de template-based
- Motivo: nao foi possivel navegar a lista de templates (output com 736k+ tokens)
- O post foi agendado com status SCHEDULED para publicacao automatica

## Etapas Executadas

1. Identificado projeto By Rock (ID 7)
2. Consultada knowledge base (cardapio, tom de voz, horarios)
3. Buscadas imagens no catalogo com tags smash/burger/hamburger (9 resultados)
4. Selecionada melhor imagem: CMT08168.jpg (Smash Sample Burger, alta qualidade)
5. Verificado thumbnail da imagem
6. Escrita copy no tom rock and roll do By Rock
7. Criado post via `create-post` (DRAFT)
8. Atualizado status para SCHEDULED via `update-post`
9. Confirmado agendamento: 2026-04-05 11:00 BRT

## Limitacoes Encontradas

- **Templates inacessiveis**: A lista de templates do By Rock gera output com 736k+ tokens, impossibilitando navegacao. Nao foi possivel usar um template de design (page-based) para renderizar a imagem com overlay de texto/logo.
- **Sem render**: Como o post foi criado com mediaUrls (legacy), nao ha render server-side com template. A imagem vai como esta no Drive.
- **Sem verificacao visual final**: Nao foi possivel pre-visualizar o story renderizado.
