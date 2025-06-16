# Projeto de Análise e Previsão da Concessão de Credito PJ

Este Projeto propõe a criação de um modelo preditivo de análise de risco para pessoa jurídica utilizando
dados públicos financeiros históricos de empresas. A concessão de crédito é uma atividade essencial no
mercado financeiro, e a avaliação da saúde financeira de uma empresa é um dos principais fatores para
essa decisão.

Ao automatizar e aprimorar essa análise com técnicas de Aprendizagem de Máquina, estatística e
engenharia de atributos espera-se tornar o processo de avaliação mais preciso e ágil. Isso pode contribuir
para uma alocação de crédito mais eficiente, minimizando inadimplências e refinanciamentos.

<p align="center">
  <img src="https://github.com/lgsilva-dev/credito/blob/main/imagemcredito.png" alt="imagem" width="35%">
</p>

## Processos Realizados:

### Etapas
1. **Entendimento do Negócio.**

2. **Entendimento dos Dados.**

3. Criação do Conjunto de Dados.

4. **Preparação dos Dados.**

5. AED (Análise Exploratória dos Dados).

6. **Modelagem e Treinamento.**

7. **Validação dos Modelos.**

8. **Deployment (Implantação do Modelo)**

* O planejamento do projeto foi desenvolvido com base na **metodologia CRISP-DS (Cross Industry Standard Process for Data Science)**, um processo cíclico amplamente utilizado em Ciência de Dados. A metodologia é composta por **seis etapas principais e interdependentes**, que orientam o desenvolvimento de projetos de forma estruturada e iterativa.

## 1. **Entendimento do Negócio**

* A partir da necessidade de otimizar e aperfeiçoar o processo de análise, liberação de limite e concessão de crédito, foi entendido que seria viável utilizar modelos de Machine Learning para realizar uma predição de concessão, a fim de sugerir ao analista uma análise composta a partir de dados e aprovações vindas da própria empresa analisada, ou seja, os critérios utilizados pelo modelo para aprovação são os mesmos que os analistas já utilizam na empresa, pois o modelo irá aprender o comportamento dos analistas com base nos dados históricos que demonstram a "saúde" da empresa, dados esses vindos de documentos como DRE, Balanço Patrimonial e Serasa, informações que os analistas consideram ao analisar crédito.

* Em conjunto a isto, foi necessário entender sobre os tipos de documentos, os pesos deles em cada cenário e também recorrer a uma pessoa que trabalhou na área para validar hipóteses e questionamentos.

## 2. **Entendimento dos Dados**

* Como o projeto tem como foco a análise, a definição de limite e a concessão de crédito, espera-se que o conjunto de dados contenha tanto as informações utilizadas pelos analistas no momento da tomada de decisão quanto os resultados dessas decisões. Isso permite que o modelo aprenda, a partir de exemplos reais, nos quais cenários o crédito deve ser concedido e qual o valor ideal de limite a ser liberado para cada empresa.

* Os dados reais disponíveis para análise, após serem transformados em formato tabular, resultaram em cinco exemplos referentes a cinco empresas distintas.

* Estes dados não são suficientes para criar um modelo de análise de crédito.

## 3. Criação do Conjunto de Dados

* Como se trata de um estudo de caso, surgiu a necessidade de aumentar este conjunto de dados de forma sintética:
 - O conjunto foi gerado com auxílio do Claude AI da Anthropic.
 - Todo o contexto do projeto foi fornecido à ferramenta, incluindo os objetivos, exemplos de casos e dados reais.
 - Os dados foram gerados já considerando o balanceamento das categorias a serem analisadas, apresentando uma quantidade relevante de cenários para o modelo.
 - Foi gerado um conjunto de dados livre de valores nulos e duplicados, garantindo maior aproveitamento do dataset.
 - Os dados passaram por uma validação que incluiu a verificação da distribuição dos valores para garantir que fossem próximos da realidade, a validação das fórmulas de Limite de Crédito e também dos cálculos de Score e Rating, que são derivados de outras notas.
 - O time funcional também participou da validação dos dados, fornecendo uma segunda aprovação sobre o conjunto.

   
## 4. **Preparação dos Dados**
* Nesta etapa foi verificado se os dados haviam realmente sido criados com uma boa distribuição/balanceados, heterogeneidade dos dados, e livres de valores nulos e duplicados.
* Remoção de colunas desnecessárias e renomeação de algumas colunas para maior praticidade e manuseio.

* Após os dados estarem prontos para manuseio fora geradas as **matrizes de correlação** tanto com as formulas de **Pearson** quanto de **Phi-K** para compreender a relação de linearidade do conjunto de dados e também a dependência dos valores em relação a concessão de crédito.

* Foi identificada uma **alta dimensionalidade** no conjunto de dados devido à grande quantidade de colunas, sendo a maioria composta por indicadores financeiros. Como esses indicadores estão, em sua maioria, relacionados à aprovação de crédito, torna-se importante tratar essa dimensionalidade de forma adequada.
 - Diante disso, será aplicada uma Standarização nos dados que coloca todos os valores em casas próximas, em seguida de uma Análise de Componentes Principais (PCA), com o objetivo de reduzir a dimensionalidade, preservando ao máximo a variabilidade presente no conjunto original.

## 5. AED (Análise Exploratória dos Dados)

* A principal razão de realizar uma Análise Exploratória dos Dados é reforçar as **correlações** extraídas a partir das matrizes, **levantar hipóteses**, **detectar padrões e comportamentos** plotando e relacionando as variáveis disponíveis no conjunto de dados, com isso podemos apoiar as decisões que serão tomadas pelo modelo de Machine Learning pois ele será um espelho das observações do Dataset.

* Nesta etapa, foi possível visualizar, por meio de gráficos como mapas de calor, dispersão e distribuição, as relações entre os indicadores financeiros (variáveis quantitativas), suas respectivas notas (variáveis qualitativas) e o impacto conjunto desses fatores na aprovação e liberação do limite de crédito.
  
## 6. **Modelagem e Treinamento**

**Concessão de Crédito**
* Após o pré-processamento, os dados foram divididos em conjuntos de treino e teste, sendo 80% destinados ao treinamento dos modelos e 20% reservados para avaliação em dados não vistos.

* Foram utilizados diferentes algoritmos de classificação para comparar o desempenho entre abordagens mais simples e modelos mais robustos. Os modelos testados incluem:

    - **Árvore de Decisão** (97% de Acurácia)

    - **Random Forest** (98% de Acurácia)

    - **XGBoost** (99% de Acurácia)

    - **Gradient Boosting** (98% de Acurácia)

A diversidade de algoritmos tem como objetivo avaliar qual a melhor técnica e qual oferece a melhor capacidade de generalização, interpretabilidade e desempenho para o problema de concessão de crédito.

## 7. **Validação dos Modelos**
**Concessão de Crédito**
* Independente do algoritmo  utilizado, todos eles se tratam de problemas de classificação binária (conceder ou não crédito), logo, as métricas de avaliação serão as mesmas.
* As metricas Utilizadas:
  - Matriz de Confusão -  permite visualizar os acertos e erros do modelo, separando verdadeiros e falsos positivos/negativos.
  - Recall - Mede a capacidade do modelo de identificar corretamente os casos positivos (concessões aprovadas).
  - F1-Score - harmônica entre precisão e recall, fornece uma medida balanceada de desempenho.
  - Precisão - Indica a proporção de casos classificados como positivos verdadeiros.
  - Acurácia: Média entre as probabilidades das taxas de verdadeiros positivos e negativos.

* Todas as métricas são dependentes das Matriz de Confusão

* Conclusões sobre os modelos:

Overall: Todos os algoritmos são baseados em árvore,logo, apresentam resultados semelhantes.
 Ao utilizar standarização e PCA em todos os algoritmos não foi observado tanta diferença de performance ao executar tais processos, isso se dá por conta de que modelos baseados em árvore conseguem calcular e generalizar e bastante todos valores e suas distâncias, além de acabar com a interpretabilidade do modelo, pois as features da base de dados se desconfigura e passa a ter resquícios de todas as colunas em todos os componentes que são as novas colunas.

1. **Árvore de decisão:** Modelo ficou muito forte 96% de Acurácia e simples de compreender, não apresentando nenhuma diferença entre Standarização + PCA do dataset normal.

2. **Random Forest:** Algoritmo mais potente que árvore de decisão e tende a enxergar mais nuances do conjunto de dados, ficou ótimo e com 98% de acurácia e com a porcentagem de descobrir se uma empresa não deve receber crédito maior (evitando inadimplências).

3. **XGBoost**: Foi o Algoritmo com o melhor desempenho geral entre os três(99% de Acurácia), obteve os F1-Scores mais altos e demonstrou a lta capacidade discriminatória pois o ROC AUC score extremamente alto (próximo de 1.0) confirma sua excelente capacidade de distinguir entre as classes (Também evitando inadimplências).

4. **Gradient Boost:** O Algoritmo teve um desempenho muito próximo do XGBoost 99% de acurácia, e mesmo dando mais importância para outras features a mais importantes continuam sendo as mesmas dos outros modelos porem em outra ordem.

Conclusão: o **XGBoost se destacou com as métricas mais altas**, tornando-o o candidato principal para implantação, pela sua robustez e desempenho.

Há consistência nas features mais importantes em todos os modelos baseados em árvores reforçando a veracidade dos seus dados e a relevância das métricas financeiras.

## 8. **Deployment (Implantação do Modelo)**

* Após a validação e escolha do melhor modelo com base nas métricas de classificação, o próximo passo é disponibilizá-lo em um ambiente de QA/Produção.

* O deployment consiste em transformar o modelo treinado em um serviço que pode ser utilizado por outros sistemas, aplicações ou usuários finais. Esse processo pode ser feito de diversas formas, como:

  - Exportação do modelo treinado (por exemplo, usando joblib ou pickle);

  - Criação de uma API (por exemplo, com Flask, FastAPI ou via serviços como Azure ML, AWS Sagemaker ou Google Vertex AI);

  - Integração com sistemas corporativos (ERPs, CRMs, ferramentas de BI);

  - Disponibilização em uma interface interativa, como dashboards (Power BI, Streamlit, etc.) ou chatbots.

* O objetivo principal é permitir que novos dados possam ser inseridos e processados pelo modelo de forma automática, retornando previsões como aprovar ou não.
