# Dashboard de Vendas, Custos, Margem de Lucro e KPI

Dashboard desenvolvido no **Microsoft Power BI** para analisar vendas, custos de envio, lucro, margem e desempenho em relação a uma meta.

Meu projeto utiliza quatro bases relacionadas — **Clientes, Pedidos, Produtos e Vendas** — permitindo praticar modelagem de dados, relacionamentos entre tabelas, tratamento de duplicidades e cálculos em DAX.

## Objetivo

O dashboard foi criado para responder às seguintes perguntas:

- Qual é o lucro médio por categoria?
- Qual é o valor total vendido por modo de envio?
- Quais mercados possuem maior custo médio de envio?
- Qual é a média do valor das vendas em relação à meta?
- Como a margem de lucro se comporta ao longo do tempo?

## Dados

O projeto contém:

- 51.290 registros de vendas
- 25.035 pedidos distintos
- 1.590 clientes
- 10.292 produtos
- Período de 2011 a 2014
- Valor total de vendas de aproximadamente 12,64 milhões

Essas informações foram distribuídas nas tabelas:

- `Clientes.csv`
- `Pedidos.csv`
- `Produtos.csv`
- `Vendas.csv`

## Modelagem

Foi criado um modelo com relacionamentos de **um para muitos**, no qual Clientes, Pedidos e Produtos funcionam como tabelas de dimensão e Vendas como tabela fato.

Antes da criação dos relacionamentos, foram tratados registros duplicados nas tabelas de Pedidos e Produtos para garantir valores únicos no lado `1`.

## Tratamento e metodologia

O desenvolvimento seguiu estas etapas:

1. Importação dos quatro arquivos CSV
2. Validação de cabeçalhos e tipos de dados
3. Tratamento de duplicidades no Power Query
4. Criação dos relacionamentos entre as tabelas
5. Criação das colunas calculadas de lucro e margem
6. Escolha dos visuais conforme as perguntas de negócio
7. Aplicação de filtro por ano e mês
8. Validação dos cálculos e da interação entre os gráficos

## Cálculos em DAX

### Lucro

```DAX
Lucro =
Vendas[Valor Venda] - Vendas[Custo Envio]
```

### Margem de lucro

```DAX
MargemLucro =
ROUND(
    DIVIDE(
        Vendas[Lucro],
        Vendas[Valor Venda],
        0
    ) * 100,
    2
)
```

A função `DIVIDE` foi utilizada para evitar erros em casos de divisão por zero.

## Indicadores e visuais

<img width="872" height="488" alt="Captura de tela 2026-07-14 133843" src="https://github.com/user-attachments/assets/6c7db201-49df-4dd9-b19f-9a8f1270547e" />

- **Gráfico de rosca:** média de lucro por categoria
- **Gráfico de cascata:** total de vendas por modo de envio
- **Medidor KPI:** média do valor de venda comparada à meta de 350
- **Treemap:** custo médio de envio por mercado
- **Gráfico de linhas:** evolução da margem de lucro ao longo do tempo
- **Segmentação:** filtro por ano e mês

A média geral do valor de venda é de aproximadamente **246,49**, abaixo da meta definida no KPI.

## Conceitos aplicados

- Modelo de dados
- Tabela fato e tabelas dimensão
- Relacionamento de um para muitos
- Cardinalidade
- Limpeza de duplicidades
- Power Query
- Colunas calculadas em DAX
- Lucro e margem de lucro
- KPI e definição de meta
- Hierarquia de datas
- Interatividade entre visuais

## Principais aprendizados

O projeto me demonstrou que os relacionamentos são essenciais para que filtros e cálculos funcionem corretamente entre tabelas diferentes. Também reforçou que um gráfico pode apresentar resultados incorretos quando o modelo está incompleto. O Lucro e margem representam conceitos diferentes E um KPI precisa de uma meta clara para permitir comparação.

## Próximas melhorias

- Criar medidas DAX em vez de depender apenas de colunas calculadas
- Adicionar faturamento, lucro total e margem geral em cartões
- Criar uma tabela calendário própria
- Comparar o resultado atual com o período anterior
- Investigar os períodos de queda da margem
- Criar páginas de detalhamento por produto, cliente e mercado

## Como você pode visualizar

1. Baixe o arquivo `lab 2.pbix`
2. Abra no Microsoft Power BI Desktop
3. Utilize o filtro de ano e mês
4. Clique nos gráficos para explorar as interações
