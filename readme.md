# Detecção de Anomalias em Transações Financeiras (R + Power BI)

Projeto desenvolvido durante o capítulo 18 do curso **"Microsoft Power BI para Business Intelligence e Data Science"** da Data Science Academy.  
Os dados utilizados são **fictícios**.

---

## Descrição

Este projeto simula um cenário em que uma empresa financeira possui dados históricos de clientes com duas transações (chamadas de `transacao1` e `transacao2`).  
Os gestores suspeitam que algumas dessas transações possam ser fraudulentas e desejam identificar **anomalias**.  

Utilizando **Machine Learning com o algoritmo Isolation Forest**, os dados foram agrupados e analisados para detectar possíveis anomalias.  
O resultado foi disponibilizado em **gráficos no Power BI**, permitindo uma visualização clara e interativa.

---

## Definição do Problema

- Detectar transações financeiras que possam ser consideradas **anomalias**.  
- Criar um modelo de Machine Learning em R para identificar padrões e destacar registros suspeitos.  
- Disponibilizar os resultados em **dashboards no Power BI** para análise visual.  

---

## Dados

- `dados_historicos.csv`: dataset fictício com transações financeiras históricas.  
- `novos_dados.csv`: dataset fictício com novas transações para validação do modelo.  
- `previsoes_novos_dados.csv`: resultado das previsões, incluindo o **anomaly score** e o status (`anomalia` ou `normal`).  

---

## Ferramentas Utilizadas

- **R** (tidyverse, dplyr, solitude, ggplot2, readr)  
- **Rtools**  
- **RStudio**  
- **Power BI Desktop**  

---

## Passo a Passo

1. **Instalação e carregamento de pacotes R**  
   ```r
   install.packages("tidyverse")
   install.packages("dplyr")
   install.packages("solitude")
   install.packages("ggplot2")
   install.packages("readr")

   library(tidyverse)
   library(dplyr)
   library(solitude)
   library(ggplot2)
   library(readr)
Carregamento e visualização dos dados históricos

r
dados_historicos_dsa <- read_csv("dados_historicos.csv")
View(dados_historicos_dsa)
Construção do modelo de Machine Learning (Isolation Forest)

r
modelo_ml_dsa = isolationForest$new() 
modelo_ml_dsa$fit(dados_historicos_dsa)
previsoes_historico = dados_historicos_dsa %>%
  modelo_ml_dsa$predict() %>%
  arrange(desc(anomaly_score))
Definição do score de anomalia

r
indices_historico = previsoes_historico[which(previsoes_historico$anomaly_score > 0.62)]
anomalias_historico = dados_historicos_dsa[indices_historico$id, ]
normais_historico = dados_historicos_dsa[-indices_historico$id, ]
Visualização dos resultados em R

Density Plot

Scatter Plot (anomalias em vermelho, normais em azul/turquesa)

Box Plot para análise comparativa

Aplicação do modelo em novos dados

r
novos_dados_dsa <- read.csv("novos_dados.csv")
previsoes_novos_dados = modelo_ml_dsa$predict(novos_dados_dsa)
Exportação dos resultados

r
write.csv(previsoes_novos_dados, "previsoes_novos_dados.csv")
Análise no Power BI

Importação do arquivo previsoes_novos_dados.csv

Criação de Box Plot com script R

Dashboard final com visualização interativa

## Dashboard Final
![Dashboard Power BI](imagens/dashboard_final.png)

## Conclusão
Este projeto demonstra como R e Power BI podem ser integrados para resolver problemas de detecção de anomalias em dados financeiros, oferecendo insights visuais e práticos para apoiar a tomada de decisão.
