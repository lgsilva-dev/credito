# Criação de Dados

* Devido a falta de dados, foi desenvolvido um conjunto de dados sintético para o projeto, afim de simular um sistema de análise de concessão de crédito para empresas no contexto financeiro brasileiro.
* O objetivo principal é avaliar a "saúde financeira" das empresas solicitantes e determinar:

  * Se o crédito deve ser concedido
  * Qual o limite de crédito apropriado
  * O modelo considera 11 indicadores chave, cada um com um peso específico na avaliação final:

    * Margem EBITDA (20%): Mede quanto do faturamento se converte em lucro operacional bruto
    * Dívida Líquida/EBITDA (10%): Indica em quantos anos a empresa pagaria sua dívida usando apenas o EBITDA atual
    * Índice de Liquidez (10%): Avalia a capacidade de pagamento no curto prazo
    * Ciclo Financeiro (10%): Mostra quantos dias a empresa opera com capital próprio investido
    * Conversão de EBITDA em FCO (10%): Mede quanto do EBITDA realmente se converte em caixa operacional
    * Auditoria em Demonstrações Financeiras (10%): Verifica se há auditoria independente das demonstrações contábeis
    * Tempo de Atuação em Anos (5%): Considera o histórico e experiência da empresa no mercado
    * Pendências Financeiras (5%): Verifica registros de dívidas não pagas
    * Garantia (5%): Avalia se a empresa apresenta bens que podem ser utilizados como garantia
    * Seguros (5%): Verifica se a empresa possui apólices de seguro ativas
    * Serasa Score PJ (5%): Pontuação de crédito que indica probabilidade de pagamento em dia

* **NOTAS**

Geração dos Indicadores Financeiros
Para cada indicador financeiro, o código segue um padrão:

* Gera valores aleatórios considerando as distribuições apropriadas
* Diferencia empresas de perfil bom e ruim usando distribuições estatísticas distintas
* Atribui uma nota (1-5) com base em faixas de valores
* Calcula a nota ponderada multiplicando a nota pelo peso do indicador

* Os indicadores são gerados de forma correlacionada (exemplo: dívida baseada no EBITDA), simulando dados reais onde as variáveis financeiras normalmente estão interrelacionadas.
* Diferenciação de Perfis: O código usa o array perfil_ruim para consistentemente gerar dados que refletem a saúde financeira global da empresa em todos os indicadores.

Esta estrutura de geração garante um conjunto de dados sintéticos que simula de forma realista o comportamento de empresas no contexto de análise de crédito, com padrões e correlações que se assemelham aos encontrados em dados reais.
