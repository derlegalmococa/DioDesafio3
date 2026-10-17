# dashboard-vendas-xbox-game-pass

Dashboard de vendas de assinaturas do Xbox Game Pass construído 100% no Excel. Transforma a base bruta (295 assinaturas de 2024) em indicadores, gráficos e tabelas interativas, com filtros por plano, tipo de assinatura e renovação automática.

## Objetivo
Organizar e visualizar os dados de vendas para responder perguntas de negócio e apoiar decisões: quanto se fatura, de onde vem a receita, quanto os cupons custam e qual o peso dos add-ons (EA Play e Minecraft).

## Arquivo
`dashboard_vendas_xbox.xlsx` — dashboard e dados integrados no mesmo arquivo.

| Aba | Conteúdo |
|---|---|
| **Dashboard** | Filtros, 12 indicadores (cartões), 4 gráficos, mapas de calor plano × tipo e leituras rápidas automáticas. |
| **Cálculos** | Critérios dos filtros, indicadores, tabelas que alimentam os gráficos, perguntas de negócio e conferências. |
| **Bases** | Tabela de dados (`Tabela1`) com as 295 assinaturas. |
| **Assets** | Paleta de cores usada no projeto. |

## Dados utilizados (`base.xlsx`, aba Bases)
295 registros, um por assinante (ID único), de 01/01/2024 a 16/12/2024.

| Coluna | Descrição |
|---|---|
| Subscriber ID, Name | Identificação do assinante (nomes podem se repetir; o ID é único) |
| Plan | Core, Standard ou Ultimate |
| Start Date | Data de início |
| Auto Renewal | Yes/No |
| Subscription Price | Preço da assinatura base |
| Subscription Type | Monthly, Quarterly ou Annual |
| EA Play Season Pass / Price | Contratou (Yes/No) e valor (`-` quando não contratou) |
| Minecraft Season Pass / Price | Contratou (Yes/No) e valor |
| Coupon Value | Desconto aplicado |
| Total Value | Valor líquido = assinatura + EA Play + Minecraft − cupom |

A regra do `Total Value` foi verificada nos 295 registros (100% de aderência). A base não informa a moeda; os valores aparecem com `$`.

## O que o dashboard mostra
- **Filtros** (listas na parte superior): Plano, Tipo de assinatura e Renovação automática. Tudo na tela responde a eles; use “Todos” para limpar.
- **Cartões:** faturamento líquido, assinantes, ticket médio, cupons concedidos, receita de add-ons, % de renovação automática, faturamento bruto, adesão ao EA Play, adesão ao Minecraft, desconto sobre o bruto, mês de pico e plano líder.
- **Gráficos:** faturamento por mês, novas assinaturas por mês, composição do faturamento por plano (assinatura base, EA Play, Minecraft), faturamento por tipo de assinatura e por renovação.
- **Mapas de calor:** faturamento e assinantes por plano × tipo.
- **Leituras rápidas:** frases geradas por fórmula que mudam com os filtros.

## Resultados principais (sem filtros)
- Faturamento líquido: **$7.633** com 295 assinantes (ticket médio ≈ $25,87).
- Plano **Ultimate** concentra 71% do faturamento ($5.388), impulsionado pelos add-ons.
- Receita de add-ons: $6.820 (EA Play $2.940 + Minecraft $3.880) contra $2.935 de assinatura base.
- Cupons somam $2.122, ou 21,8% do faturamento bruto ($9.755).
- Planos anuais: $1.754 (renovação automática $1.537; sem renovação $217).
- Mês de pico: outubro/2024. Janeiro, fevereiro e dezembro têm poucos registros (dados parciais).

## Perguntas de negócio respondidas (aba Cálculos, seção 9)
1. Faturamento total dos planos anuais.
2. Faturamento dos planos anuais com e sem renovação automática.
3. Total de vendas do EA Play Season Pass.
4. Total de vendas do Minecraft Season Pass.
5. Faturamento líquido total, cupons concedidos e plano de maior faturamento (extras).

## Técnicas usadas
Tabela do Excel, intervalos nomeados (`d_plano`, `d_tipo`, `d_renov`, `d_total`, `crit_plano`…), `SOMASES`, `CONT.SES` com critério curinga (`*` para “Todos”), `PROCV`, `ÍNDICE`/`CORRESP`, `DATA`, `DATAM`, validação de dados (listas), formatação condicional (escala de cores), gráficos de colunas, linha, rosca e barras, e uma seção de conferências.

## Como reproduzir
1. Crie uma pasta de trabalho com as abas `Dashboard`, `Cálculos`, `Bases` e `Assets`.
2. Cole a base em `Bases` (A1:M296) e formate como Tabela (`Tabela1`).
3. Crie intervalos nomeados para cada coluna (ex.: `d_plano` = `Bases!$C$2:$C$2000`). Use um intervalo maior que a base para aceitar novas linhas.
4. Em `Cálculos`, monte a tabela de critérios: a seleção do filtro vira `*` quando for “Todos” (ou usa `PROCV` para traduzir Mensal → Monthly etc.) e nomeie `crit_plano`, `crit_tipo`, `crit_renov`.
5. Escreva cada indicador com `SOMASES(d_total; d_plano; crit_plano; d_tipo; crit_tipo; d_renov; crit_renov)`; para meses, acrescente `d_data` com `>=` início e `<` início do mês seguinte.
6. No `Dashboard`, crie as 3 listas de filtro (validação de dados), os cartões ligados aos indicadores e os gráficos apontando para as tabelas de `Cálculos`.
7. Aplique a escala de cores nas matrizes e confira a aba de conferências.

Para atualizar: cole novas linhas na tabela `Bases` (até a linha 2000) e os indicadores se atualizam.

## Diferenças em relação ao modelo
- Filtros por listas suspensas nas três dimensões, em vez de segmentações de dados.
- Indicadores novos: ticket médio, cupons, bruto × líquido, adesão aos add-ons, % de desconto.
- Evolução mensal, composição por plano, mapas de calor e leituras automáticas.
- Aba de conferências que valida a soma e a recomposição do `Total Value`.

## Prints
Adicione capturas do dashboard na pasta `/images` (por exemplo, sem filtro e com Plano = Ultimate e Tipo = Anual).
