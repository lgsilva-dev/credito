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

* Criação de um conjunto de Dados Sintéticos
* Validação dos Dados Artificiais
* Limpeza e Tratamento dos Dados
* Exploração dos dados (AED)
  - Correlações
  - Gráficos da Distribuição das Variáveis - Qualitativas e Quantitativas
  - Estatísticas Básicas    
* Normalização dos Dados
* PCA
* Modelagem
    - Modelo 1
    - Modelo 2
    - Modelo 3
* Validação
* Explicação do Modelo
* Deploy

  Os processos realizados são baseados na metodologia CRISP-DS

  ## Cadernos
  
  O projeto foi desenvolvido em cadernos python.
  
  **Conteúdo dos cadernos:**
1. CreditoCreateData.ipynb > Função da criação dos dados e validação do dataset
2.  CreditoEDA.ipynb > Limpeza e tratamento dos dados sintéticos e primeiras explorações.
3. Validacoes.ipynb > Plot de gráficos dos indicadores e suas relações.
4. BaseDf.ipynb > Limpeza e tratamento dos dados originais para comparação com dados sintéticos.
5. model.ipynb > Normalização, PCA, Modelagem e Validação.
