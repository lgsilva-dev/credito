# Análise Exploratória de Dados (AED) - Projeto de Análise de Crédito

Esta pasta contém os notebooks Jupyter que foram utilizados para a Análise Exploratória de Dados (AED) do projeto de análise de crédito. O objetivo principal da AED é compreender a estrutura dos dados, identificar padrões, detectar anomalias, compreender a relação entre a massa de dados gerada artificialmente com ela mesma e também com a aprovação de crédito e preparar os dados para as etapas de modelagem.

## Conteúdo da Pasta

* `CreditoEDA.ipynb`: Notebook de Limpeza e Exploração dos Dados.
* `validacoes.ipynb`: Notebook de Validação e Análise de Correlação.

## Propósito dos Cadernos

### `CreditoEDA.ipynb` (Caderno de Limpeza e Exploração dos Dados)

Este notebook é o ponto de partida para a AED. Suas principais finalidades são:

* **Limpeza de Dados:** Tratar inconsistências, colunas desnecessárias, renomear colunas, verificar valores nulos e duplicados e quaisquer outros problemas que possam comprometer a qualidade dos dados.
* **Análise Exploratória Inicial:** Realizar análises descritivas, visualizar distribuições de variáveis, identificar outliers e entender a composição geral do dataset.
* **Preparação para Análises Mais Profundas:** Assegurar que os dados estejam em um formato adequado e limpo para as etapas de validação e modelagem.

### `validacoes.ipynb` (Caderno de Validação e Análise de Correlação)

Após a limpeza e exploração inicial, este notebook aprofunda a análise, com foco em:

* **Validação de Dados:** Verificar se os dados tratados no notebook anterior fazem sentido e estão consistentes com as expectativas do negócio.
* **Análise de Correlação:** Investigar a relação entre a massa de dados (inclusive dados gerados artificialmente, conforme mencionado) e a variável de aprovação de crédito. Este notebook explora como diferentes variáveis financeiras e de negócio (Faturamento, EBITDA, Serasa Score, etc.) se correlacionam com a decisão de crédito.
* **Compreensão do Impacto das Variáveis:** O objetivo é compreender quais dados têm maior peso e como podem influenciar a concessão de crédito, servindo como uma base fundamental para o entendimento do futuro modelo de Machine Learning.

## Conclusões Gerais sobre a AED

* **Colunas com maior correlação de phi_k com a concessão de crédito:**
  * RATING GO ON	1.000000
  * SCORE GO ON	0.994118
  * Divida liquida/EBTIDA	0.968655
  * Margem EBITDA	0.959538
  * Indice de liquidez	0.943840
  * Serasa Score	0.891745
  * Conversao Ebitda em FCO	0.827627
  * PEFIN	0.755028
  * Ciclo Financeiro	0.710156
  * Auditorias	0.700356
  * Garantia	0.599859
  * Tempo de atuação em anos	0.562323
  * Seguros	0.445830

* **Correlações gerais:**
  As colunas se relacionam entre si, porém, não tanto quanto dados reais, por ex: Uma coluna com valores derivados de EBITDA devem ter uma correlação alta umas com as outras e como nossos dados são gerados sintéticos e aleatorios para cada coluna não tem como construir  uma relação tão forte, estas relações implicam no modelo de Machine Learning que será desenvolvido, pois os modelo é um mero reflexo dos dados e da qualidade deles.

* **Disclaimer:**
  Este conjunto de dados foi gerado artificialmente, logo, as conclusões geradas são também artificais e cabem somente para este estudo de caso, não é porque o conjunto de dados foi baseado em dados reais que ele tem a capacidade de estar em um projeto real.
  
