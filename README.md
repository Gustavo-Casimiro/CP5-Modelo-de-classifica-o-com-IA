# CP5-Modelo-de-classificação

Desenvolvimento de projeto de modelo de classificação

  Objetivo de classificação

  Este projeto classifica registros de vendas da BMW em ‘baixo’, ‘médio’ e ‘alto’ volume com base em características de produto e mercado, como modelo, ano, região, preço e especificações técnicas. A variável alvo é sales_class, derivada de Sales_Volume por discretização em três faixas de demanda, configurando uma tarefa de classificação multiclasse. O objetivo é fornecer categorias claras de desempenho comercial para suportar análises comparativas entre modelos e regiões e orientar decisões táticas.

Justificativa da escolha do tema

  Classificar o volume de vendas em faixas facilita a priorização de ações de marketing, abastecimento e planejamento de estoque. Em um portfólio amplo e mercados distintos, categorizar demanda reduz a complexidade e melhora a comunicação entre times, permitindo alertas e metas por faixa (baixo/médio/alto) e comparações consistentes ao longo do tempo.

Descrição do Dataset

  Fonte dos dados: Kaggle
  https://www.kaggle.com/datasets/ahmadrazakashif/bmw-worldwide-sales-records-20102024

  Linhas: 50000
  Colunas: 11

  Variáveis: Modelo, ano, região, cor, tipo de combustível, transmissão, tamanho do motor, Quilometragem, preço, vendas, classificação de vendas.

Modelos de classificação:

  index,modelo,acuracia,precisao,recall,f1
  0,LogisticRegression,0.9983,0.9982999499249916,0.9983,0.9982999645641482
  1,LDA,0.9023,0.9159810806937079,0.9023,0.899182036771681
  2,GaussianNB,0.9023,0.9159810806937079,0.9023,0.899182036771681

  A acurácia reporta a proporção de previsões corretas no conjunto de teste e é útil quando as classes estão razoavelmente equilibradas.

  Usamos acurácia para comparar rapidamente os modelos, sabendo que, em cenários desbalanceados, ela pode mascarar erros na classe minoritária.

Precisão
  A precisão indica, entre as instâncias previstas como positivas por uma classe, quantas realmente pertencem a essa classe, sendo crítica quando o custo de falso positivo é alto.

  Relatamos precisão por classe e média (macro/weighted) para evitar que o desempenho em classes dominantes esconda baixa qualidade em classes menores.

Recall
  O recall mede, entre todas as instâncias verdadeiramente positivas de uma classe, quantas o modelo conseguiu capturar, sendo vital quando o custo de falso negativo é alto.​​

F1-Score
  Priorizamos recall (ou F1) quando a classe de interesse é minoritária, para reduzir a perda de casos relevantes.

Análise comparativa entre os modelos:
  A Tabela de Métricas resume acurácia, precisão, recall e F1 no conjunto de teste para cada modelo, ordenada pelo F1 para refletir melhor o equilíbrio entre precisão e recall.

  O modelo selecionado apresentou maior F1 sem degradar substancialmente a precisão, além de melhor distribuição de acertos na matriz de confusão.

  Escolhemos o modelo final porque maximiza F1 nas classes de maior interesse e mantém precisão adequada, equilibrando captura e confiabilidade das previsões.

  Apesar da acurácia similar entre modelos, a melhor pontuação de F1 e a matriz de confusão mais homogênea sustentam a decisão.

Justificativa do modelo final escolhido:
  Selecionou‑se o modelo final por maximizar F1 sem perda significativa de precisão, equilibrando captura de casos relevantes e confiabilidade das previsões. Além disso, sua matriz de confusão é mais homogênea entre classes, alinhando‑se ao objetivo de negócio de          reduzir erros na classe de maior interesse.

  Em termos práticos, oferece melhor trade‑off entre identificar corretamente registros de ‘alto’ volume e evitar alarmes falsos, o que atende à priorização de estoque e campanhas. Como próximos passos, aplicaremos validação cruzada estratificada e ajuste de               hiperparâmetros para consolidar a robustez do resultado.

Principais aprendizados:
  O pipeline de classificação com pré-processamento reprodutível (imputação, encoding e padronização) foi essencial para estabilizar o desempenho entre modelos e reduzir impacto de nulos e escalas diferentes nas variáveis.​

  Entre Regressão Logística, LDA e Gaussian Naive Bayes, observou-se variação nas trocas entre precisão e recall; ordenar por F1 ajudou a balancear cobertura e confiabilidade das previsões.​

  A análise da matriz de confusão mostrou que a maior confusão ocorre entre classes adjacentes de volume (ex.: médio vs alto), sugerindo fronteiras próximas e possível necessidade de melhor engenharia de atributos.

Melhorias futuras:
  Validação cruzada estratificada e ajuste de hiperparâmetros (ex.: C e penalty na Regressão Logística; parâmetros de priors no Naive Bayes) para robustez e ganho de generalização.​

  Engenharia de atributos: agregações por região/ano/mês, sazonalidade, indicadores de mix de modelos e faixas de preço, além de interações relevantes, para aumentar separabilidade entre classes.​

  Tratamento de desbalanceamento, se presente, via class_weight, amostragem e corte de decisão ajustado à métrica prioritária.
