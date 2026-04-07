# Agendamento Happy Hour - By Rock (07 a 11 de Abril 2026)

## Resumo da Situacao

- **Projeto**: By Rock (ID: 7) - @by.rock
- **Periodo solicitado**: 07/04 a 11/04/2026
- **Pedido**: 15 stories de happy hour (3 por dia, horarios organicos)
- **DRAFTs encontrados**: 0 (nenhum post com status DRAFT)
- **Posts ja SCHEDULED no periodo**: 10 stories

### Posts Ja Agendados (07-11/04)

| # | Dia | Horario (BRT) | Tema | Caption (resumo) | Status | Render |
|---|-----|---------------|------|-------------------|--------|--------|
| 1 | Seg 07/04 | 14:07 | Restaurant Week | Fish & Chips Baviera | SCHEDULED | NOT_NEEDED |
| 2 | Seg 07/04 | 14:19 | Happy Hour | Segunda Rock - HH ate 50% OFF | SCHEDULED | RENDERED |
| 3 | Ter 08/04 | 14:02 | Restaurant Week | Tropeiro Hermano | SCHEDULED | NOT_NEEDED |
| 4 | Ter 08/04 | 14:16 | Almoco | Frango no almoco | SCHEDULED | RENDERED |
| 5 | Qua 09/04 | 14:11 | Happy Hour | Quartou no Rock - Onion Rings HH | SCHEDULED | RENDERED |
| 6 | Qua 09/04 | 14:12 | Restaurant Week | Gnocchi au Poivre | SCHEDULED | NOT_NEEDED |
| 7 | Qui 10/04 | 14:08 | Restaurant Week | Fish & Chips Baviera (ultimos dias) | SCHEDULED | NOT_NEEDED |
| 8 | Qui 10/04 | 14:23 | Almoco | Suina no almoco | SCHEDULED | RENDERED |
| 9 | Sex 11/04 | 14:26 | Happy Hour | Sextou na Veia - Sausage Mix HH | SCHEDULED | RENDERED |
| 10 | Sex 11/04 | 18:37 | Restaurant Week | Tropeiro Hermano (storytelling) | SCHEDULED | NOT_NEEDED |

**Observacao**: A maioria dos posts existentes esta concentrada no horario ~14h BRT. Faltam stories nos horarios de pico do happy hour (16h-19h) e no almoco (11h-13h) em varios dias.

---

## Grade Proposta (SE houvesse 15 DRAFTs de Happy Hour)

Considerando que o happy hour do By Rock e das 16h as 20h (knowledge base diz 17h-20h com 30% OFF, cardapio diz 16h-20h com ate 50% OFF), os horarios foram pensados para cobrir:
- **Pre-happy hour** (16h-17h) - gerar desejo/antecipacao
- **Pico do HH** (17h-18h30) - engajamento maximo
- **Final do HH** (18h30-19h30) - urgencia / "ainda da tempo"

### Grade Semanal - 3 Stories/Dia (Horarios Organicos em BRT)

| # | Dia | Horario (BRT) | Slot | Sugestao de Tema |
|---|-----|---------------|------|------------------|
| 1 | Seg 07/04 | 16:12 | Pre-HH | Chopp gelado + "Segunda pede rock" |
| 2 | Seg 07/04 | 17:41 | Pico HH | Petisco HH (Rock Fries ou Onion Rings) |
| 3 | Seg 07/04 | 19:08 | Final HH | "Ainda da tempo" - drink ou cerveja artesanal |
| 4 | Ter 08/04 | 16:23 | Pre-HH | Ambiente do bar + "Terca tambem tem rock" |
| 5 | Ter 08/04 | 17:55 | Pico HH | Petisco HH (Torresmo Rock ou Coxinhac) |
| 6 | Ter 08/04 | 19:17 | Final HH | Cerveja + petisco - "Vem fechar o dia no rock" |
| 7 | Qua 09/04 | 16:07 | Pre-HH | "Quartou? Nao, ROCKOU" - chopp |
| 8 | Qua 09/04 | 17:33 | Pico HH | Special Bread ou Fries & Ribs HH |
| 9 | Qua 09/04 | 18:52 | Final HH | Drink autoral + "O meio da semana tem sabor" |
| 10 | Qui 10/04 | 16:38 | Pre-HH | "Quinta na veia" - Sausage Mix |
| 11 | Qui 10/04 | 17:22 | Pico HH | Pastel Backstage ou Hermanos chapa |
| 12 | Qui 10/04 | 19:03 | Final HH | Vinho + petisco - "Aquece a quinta" |
| 13 | Sex 11/04 | 16:17 | Pre-HH | "SEXTOU!" - chopp + ambiente |
| 14 | Sex 11/04 | 17:47 | Pico HH | Smash Sample Burger HH + cerveja |
| 15 | Sex 11/04 | 18:41 | Final HH | "Noite de rock comeca agora" - drinks |

### Principios Aplicados
- **Minutos variados**: 07, 12, 17, 22, 23, 33, 38, 41, 47, 52, 55, 03, 08 (nunca :00 ou :30)
- **Espacamento minimo**: ~90min entre stories do mesmo dia
- **Horarios de pico HH**: Todos entre 16h-19h30 (faixa do happy hour By Rock)
- **Tom organico**: Parece postagem humana, nao bot
- **Sem conflito**: Nenhum horario colide com os 10 posts ja agendados

---

## Resultado da Execucao

**STATUS: NAO EXECUTADO** - Nao havia posts DRAFT para agendar.

### O que seria necessario para executar:
1. Criar 15 posts como DRAFT (via `/create-template-pages` ou `create-post`) com:
   - Copies de happy hour no tom rock and roll do By Rock
   - Imagens do Drive (cerveja, ambiente, petiscos)
   - Templates de story (ID 140 - HH template ja usado nos posts existentes)
2. Renderizar cada post com `render-story`
3. Apresentar renders para aprovacao visual
4. Aplicar os horarios da grade acima com `update-post` (scheduledDatetime + status: SCHEDULED)

### Proximos Passos Sugeridos
- Criar os 15 posts DRAFT de happy hour (copies + imagens)
- Depois executar este agendamento com a grade proposta
- Revisar se os 10 posts ja existentes cobrem os outros temas (almoco, restaurant week) ou se precisam de ajuste

---

*Gerado em 02/04/2026 | Projeto By Rock (ID: 7) | Studio Lagosta*
