# Dashboard de Locação de Veículos — Power BI

Relatório para acompanhar a operação de uma locadora: quanto entra, de quais clientes, com que frequência e o que se espera para os próximos períodos.

**Projeto de estudo com dados fictícios.** Nenhuma informação real de empresa ou de pessoa física.

## O problema

Uma locadora precisa responder, toda semana, a perguntas que costumam estar espalhadas em planilhas: quanto faturamos e como isso se compara ao ano anterior, quais clientes estão ativos e quais estão com cadastro irregular, e quanto se roda por locação. O relatório reúne essas respostas em um único arquivo navegável.

## Páginas

| Página | O que responde |
|---|---|
| CAPA | Tela de abertura com botão de navegação |
| LOCAÇÃO DE VEÍCULOS | Faturamento total, por ano e por dia da semana, quantidade de clientes, média de KM e resumo de consumos |
| CLIENTES | Situação cadastral da base, distribuição por categoria e listas de controle de cadastro |
| PREVISÃO | Ticket médio, faturamento e projeção de vendas com intervalo de confiança |

## Modelo de dados

| Tabela | Papel no modelo |
|---|---|
| tb_km | Fato: locações, com data, placa, marca, modelo, KM e total da venda |
| tb_cli | Dimensão: clientes, com ID, nome e situação cadastral |
| MEDIDAS | Tabela dedicada apenas às medidas DAX, para manter o modelo organizado |
| INNER JOIN e ANT LEFT | Consultas de mesclagem criadas no Power Query |

As duas últimas merecem destaque. Em vez de trazer tudo em uma tabela só, o modelo usa mesclagem de consultas no Power Query: um inner join para cruzar locações com clientes cadastrados e um left anti join para isolar os registros que existem em uma tabela e não existem na outra. É assim que o relatório encontra locação sem cliente correspondente, que é um problema de qualidade de dados antes de ser um problema de visualização.

## Medidas DAX

| Medida | Para que serve |
|---|---|
| FATURAMENTO | Receita total do período filtrado |
| FAT MEDIDA | Faturamento usado nas comparações percentuais entre anos |
| TICKET_MED_SLR | Ticket médio por locação |
| MEDIA DE KM | Quilometragem média rodada |
| TT_CIDADES | Total de cidades atendidas |

## Recursos usados

Previsão nativa do Power BI no gráfico de linha, com limite superior e inferior de confiança. Visuais customizados do AppSource (Text Filter para busca livre por cliente e Word Cloud). Navegação por botões entre a capa e as páginas do relatório. Segmentações, hierarquia de datas e plano de fundo personalizado.

## Como abrir

Baixe o arquivo Locacao_Veiculos.pbix e abra no Power BI Desktop. O modelo já vem com os dados importados, não é preciso configurar nenhuma conexão.

## Stack

Power BI Desktop, Power Query (M), DAX, modelagem de dados.
