📊 Análise de Churn com SQL + Power BI
 
Desenvolvi uma análise em SQL para identificar clientes com risco de churn a partir da recência de compra, utilizando a data da última transação da base.
O objetivo é apoiar o time de CRM com insights acionáveis para retenção e reativação.


Pipeline de Dados

1. Extração e transformação (SQL)

* Cálculo da última compra por cliente
* Criação da métrica de recência (meses sem compra)
* Classificação em **Ativo vs. Em Risco de Churn**
* Agregações para análise (volume, ticket médio, distribuição)

2. Consumo no Power BI
Os dados tratados foram utilizados como base para construção de um dashboard interativo com:

* KPIs de clientes em risco
* Distribuição por status (ativo vs. risco de churn)
* Análise de tempo sem compra
* Comparação de comportamento entre grupos

Conexão SQL → Power BI
A conexão foi realizada via banco relacional, permitindo atualização dos dados no Power BI.

Etapas:
1. Integração com o banco (MySQL)
2. Importação ou conexão direta das tabelas tratadas
3. Modelagem dos dados no Power BI
4. Criação de medidas e visualizações


Principais Métricas (DAX – Power BI)
```DAX
Clientes em Risco = 
CALCULATE(
    24306 - SELECTEDVALUE('db_vendas _view_ult_compra_cliente'[mes_ult_compra])
)
```
```DAX
Percentual em Risco = 
DIVIDE(
    [Clientes em Risco],
    ('total_clientes_ult_compra]) * 100
)
```
```DAX
total_clientes_ult_compra = 
COUNTROWS('db_vendas _view_ult_compra_cliente')
```

📌 Principais insights
* Parte relevante da base apresenta **inatividade prolongada**
* Risco maior em clientes com **baixa frequência de compra**
* Diferença de comportamento entre clientes ativos e em risco
* Identificação de grupo prioritário para reativação

🎯 Recomendações
* Campanhas de reativação por tempo sem compra
* Priorizar clientes com maior ticket médio
* Ações preventivas antes de 4 meses de inatividade
