# Análise Exploratória de Dados (AED) - Projeto de Análise de Crédito

Esta pasta contém os notebooks Jupyter que foram utilizados para a Análise Exploratória de Dados (AED) do projeto de análise de crédito. O objetivo principal da AED é compreender a estrutura dos dados, identificar padrões, detectar anomalias, compreender a relação entre a massa de dados gerada artificialmente com ela mesma e também com a aprovação de crédito e preparar os dados para as etapas de modelagem.

## Conteúdo da Pasta

* `CreditoEDA.ipynb`: Notebook de Limpeza e Exploração dos Dados.
* `validacoes.ipynb`: Notebook de Validação e Análise de Correlação.

## Propósito dos Cadernos

### `CreditoEDA.ipynb` (Caderno de Limpeza e Exploração dos Dados)

Este notebook é o ponto de partida para a AED. Suas principais finalidades são:

* **Limpeza de Dados:** Tratar inconsistências e quaisquer outros problemas que possam comprometer a qualidade dos dados.
* **Análise Exploratória Inicial:** Realizar análises descritivas, visualizar distribuições de variáveis, identificar outliers e entender a composição geral do dataset.
* **Preparação para Análises Mais Profundas:** Assegurar que os dados estejam em um formato adequado e limpo para as etapas de validação e modelagem.
* **Utilização da Biblioteca `phik`**: Este notebook emprega a biblioteca `phik` para calcular correlações e informações mútuas, permitindo a identificação de relacionamentos mais complexos e não lineares entre as variáveis, o que é crucial para uma compreensão aprofundada dos dados.

### `validacoes.ipynb` (Caderno de Validação e Análise de Correlação)

Após a limpeza e exploração inicial, este notebook aprofunda a análise, com foco em:

* **Validação de Dados:** Verificar se os dados tratados no notebook anterior fazem sentido e estão consistentes com as expectativas do negócio.
* **Análise de Correlação:** Investigar a relação entre a massa de dados (inclusive dados gerados artificialmente, conforme mencionado) e a variável de aprovação de crédito. Este notebook explora como diferentes variáveis financeiras e de negócio (Faturamento, EBITDA, Serasa Score, etc.) se correlacionam com a decisão de crédito.
* **Compreensão do Impacto das Variáveis:** O objetivo é compreender quais dados têm maior peso e como podem influenciar a concessão de crédito, servindo como uma base fundamental para o entendimento do futuro modelo de Machine Learning.

## Conclusões Gerais sobre a AED

A Análise Exploratória de Dados, realizada através desses dois notebooks, é fundamental para o sucesso do projeto de análise de crédito. Através dela, pudemos:

* **Garantir a Qualidade dos Dados:** Identificar e tratar problemas nos dados, tornando-os confiáveis para as próximas etapas.
* **Obter Insights Valiosos:** Compreender as distribuições das variáveis e suas relações, especialmente como elas impactam a aprovação de crédito.
* **Fundamentar a Modelagem:** Aprofundar o conhecimento sobre os dados é crucial para construir um modelo de Machine Learning robusto e preciso. As correlações e padrões descobertos aqui servirão de base para a seleção de features e o desenvolvimento do modelo.
* **Entender a Relevância das Variáveis:** A análise de correlação destacou quais variáveis financeiras e de comportamento (como Faturamento, EBITDA, Serasa Score, etc.) possuem maior influência na decisão de crédito, validando a importância dessas características para o modelo.
