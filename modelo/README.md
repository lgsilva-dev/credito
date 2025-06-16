# Documentação dos Modelos de Machine Learning
* Funcionamento, Viéses e Pontos de Atenção.

## Funcionamento
**O que o modelo recebe?**

 Ambos os modelos desenvolvidos (Random Forest e XGBoost) que são classificados como modelos baseados em árvores de decisão devem receber um DataFrame contendo os seguintes campos:

- Margem EBITDA - (float)
- Divida liquida/EBTIDA - (float)
- Indice de liquidez - (float)
- Ciclo Financeiro - (float)
- Conversao Ebitda em FCO - (float)
- Tempo de atuação em anos - (int)
- Auditorias - (int)
- PEFIN - (int)
- Garantia - (int)
- Seguros - (int)
- Serasa Score - (int)

Campos estes que são referentes aos indicadores financeiros do cliente que estão sendo analisados.

**O que o modelo Retorna?**

E o modelo treinado irá retonar um valor que será [0 ou 1] que indica a sugestão de reprovação quando valor = [0] ou aprovação quando retornado valor = [1]

Para utilizar o modelo ja treinado basta utilizar os Arquivos .pkl disponibilizados em credito/modelo/{arquivo.pkl} e desempacota-lo da seguinte forma:

```
try:
    modelo = joblib.load('random_forest_credit_model.pkl')
    print("Modelo Random Forest salvo com sucesso!")
    print(f"Tipo do objeto carregado: {type(modelo)}")
except FileNotFoundError:
    print(f"Erro: O arquivo '{modelo}' não foi encontrado.")
    exit()

```

    

### Random Forest (Floresta Aleatória)

Este modelo constrói um "comitê" de múltiplas árvores de decisão. Cada árvore é treinada em uma amostra aleatória dos dados e considera um subconjunto aleatório das features para fazer suas divisões. A previsão final é determinada pela "votação" (ou média) das previsões de todas as árvores. Isso ajuda a reduzir o overfitting e melhora a generalização.

* **Otimização:** Foi utilizado um processo de `GridSearchCV` para encontrar os hiperparâmetros ideais para o modelo.
    * **Melhores Parâmetros Encontrados:** `{'max_depth': 20, 'max_features': 'sqrt', 'min_samples_leaf': 1, 'n_estimators': 200}`.
* **Features Mais Influentes:** Consistente com outros modelos baseados em árvores, as features que mais influenciaram as decisões do Random Forest foram  **'Margem EBITDA'**, **Indice de Liquidez** e **'Divida liquida/EBITDA'** e outras features como 'Conversão de Ebitda em FCO', 'Auditorias' e 'Serasa Score' também apresentaram alguma relevância.
  
* **Desempenho (Avaliação no Conjunto de Teste):**
    ```
                  precision    recall  f1-score   support

               0       0.95      0.98      0.96       4793  
               1       0.99      0.97      0.98       9824  

        accuracy                           0.98       14617  
       macro avg       0.97      0.98      0.97       14617  
    weighted avg       0.98      0.98      0.98       14617  
    ```
    * **Acurácia:** 0.97 (97% de previsões corretas).
    * **F1-Score:** Alto e bem balanceado para ambas as classes (0.95 e 0.99), indicando um bom equilíbrio entre precisão e recall.
 

### XGBoost (Extreme Gradient Boosting)

O XGBoost é uma implementação altamente otimizada e eficiente do Gradient Boosting. Ele constrói árvores de forma sequencial, onde cada nova árvore tenta corrigir os erros das árvores anteriores. Possui técnicas avançadas para controle de overfitting e é conhecido por sua velocidade e desempenho.

* **Otimização:** Foi utilizado um processo de `GridSearchCV` exaustivo para encontrar os hiperparâmetros ideais para o modelo.
    * **Melhores Parâmetros Encontrados:** `{'colsample_bytree': 0.7, 'learning_rate': 0.1, 'max_depth': 3, 'n_estimators': 300, 'subsample': 0.7}`.
* **Features Mais Influentes:** O XGBoost confirmou e intensificou a importância das mesmas features do Random Forest:
    * **'Divida liquida/EBITDA'**: De longe a feature mais importante, contribuindo com a maior parte do "ganho" na redução do erro do modelo.
    * **'Margem EBITDA'**: A segunda feature mais influente, com contribuição significativa.
    * Outras features como 'Auditorias', 'Conversao Ebitda em FCO' e 'Garantia' também contribuem, mas em escala bem menor.
* **Desempenho (Avaliação no Conjunto de Teste):**
    ```
                  precision    recall  f1-score   support

               0       0.98      1.00      0.99      4793
               1       1.00      0.99      0.99      9824

        accuracy                           0.99     14617
       macro avg       0.99      0.99      0.99     14617
    weighted avg       0.99      0.99      0.99     14617

    ROC AUC Score para XGBoost Otimizado: 0.9997
    ```
    * **Acurácia:** 0.99 (99% de previsões corretas).
    * **F1-Scores:** Quase perfeitos para ambas as classes (0.99 e 0.99), indicando um modelo extremamente preciso e balanceado.
    * **ROC AUC Score:** 0.9997, um valor excepcional que demonstra uma capacidade quase perfeita de discriminar entre as classes.


### Comparativo

| Modelo         | Acurácia no Teste | F1-Score (Classe 0) | F1-Score (Classe 1) | ROC AUC Score |
| :------------- | :---------------- | :------------------ | :------------------ | :------------ |
| Random Forest  | 0.98              | 0.96                | 0.98                | 0.9780        |
|   XGBoost      | 0.99              | 0.98                | 0.99                | 0.9997        |


Mesmo com um desempenho tão alto, modelos de Machine Learning não são infalíveis e carregam certas características e riscos:

1.  **Viés de Dados Históricos:** O modelo aprende com os dados históricos fornecidos. Se esses dados contêm vieses inerentes (por exemplo, políticas de crédito passadas que discriminavam sutilmente certos perfis de empresa ou mercado, ou analises que davam mais importância para X indicadores o modelo irá replicar as importâncias/pesos destes indicadores nas predições), o modelo pode aprender e replicar esses vieses em suas novas previsões. É importante garantir que os dados de treinamento sejam representativos e o mais imparcial possível.
2.  **Generalização para Cenários Futuros (Drift):** O excelente desempenho do modelo é válido para dados com características semelhantes às dos dados de treinamento. Mudanças significativas no cenário econômico (crises, booms), nas políticas de mercado, ou no perfil dos clientes ao longo do tempo podem fazer com que o desempenho do modelo se degrade.
3.  **Interpretabilidade (vs. Desempenho):** Modelos de ensemble como o XGBoost, embora altamente performáticos, são considerados "caixas pretas" em comparação com modelos mais simples. Embora possamos identificar as features mais importantes (como Dívida líquida/EBITDA), entender a lógica exata por trás de cada decisão individual do modelo pode ser complexo.
4.  **Manutenção e Monitoramento Contínuos:** Modelos em produção devem ser monitorados constantemente.
    * **Monitoramento de Desempenho:** Acompanhar a acurácia, F1-Score e ROC AUC em dados reais ao longo do tempo para detectar degradação.
    * **Monitoramento de Dados:** Verificar se as características dos novos dados de entrada (distribuição das features) permanecem consistentes com as dos dados de treinamento.
    * **Retreinamento Periódico:** O modelo deve ser retreinado periodicamente com dados mais recentes para se adaptar a novas tendências e manter a relevância.
5.  **Qualidade dos Dados:** O desempenho do modelo é diretamente proporcional à qualidade dos dados de entrada. Se os dados de novos clientes tiverem erros, inconsistências ou valores ausentes, a previsão do modelo será afetada.

---
