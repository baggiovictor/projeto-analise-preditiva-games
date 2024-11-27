# **Previsão de Vendas Globais de Jogos Usando Machine Learning**

## **Introdução**
- O objetivo do projeto foi criar um modelo preditivo capaz de prever as vendas globais de jogos com base em dados históricos, como vendas regionais, gênero, plataforma e ano de lançamento.
- A análise foi realizada usando o algoritmo **Random Forest Regressor**, conhecido por sua robustez e capacidade de lidar com dados categóricos e numéricos.

---

## **Metodologia**
1. **Dados utilizados**:
   - O dataset contém informações sobre vendas de jogos em milhões de cópias em diferentes regiões (América do Norte, Europa, Japão e outras), além de características como gênero, plataforma e distribuidora.
   - Dados ausentes foram tratados, e variáveis categóricas foram codificadas para uso no modelo.

2. **Treinamento do modelo**:
   - O modelo foi treinado com **80% dos dados** e avaliado com os **20% restantes**.
   - Métricas de desempenho: **RMSE (Root Mean Squared Error)**, **R² Score** e **MAE (Mean Absolute Error)**.

---

## **Desempenho do Modelo**
- **RMSE (Erro Médio Quadrático):** 1.97 milhões de cópias.
- **R² Score:** 0.86, indicando que 86% da variação nas vendas globais foi explicada pelo modelo.
- **MAE (Erro Médio Absoluto):** 1.03 milhões de cópias.

---

## **Análise dos Jogos da Nintendo**
1. **Foco nos jogos da Nintendo**:
   - Analisamos um subconjunto específico de dados apenas com jogos publicados pela Nintendo, conhecida por suas franquias de sucesso como Mario, Pokémon e Zelda.
   - O modelo previu as vendas globais desses jogos com alta precisão.

2. **Gráfico: Vendas Reais vs. Previstas**:
   - O gráfico mostrou que o modelo teve um bom desempenho ao prever vendas globais de jogos da Nintendo.
   - Os pontos se concentraram próximos da linha diagonal, indicando que as previsões estão alinhadas com os valores reais.

3. **Gráfico: Relação entre Vendas Regionais e Globais**:
   - As vendas na América do Norte e Europa tiveram maior correlação com as vendas globais.
   - O mercado japonês mostrou menor impacto relativo nas vendas globais de jogos da Nintendo, mas é altamente relevante para certos gêneros como RPGs.

---

## **Insights Derivados**
1. **Importância das Vendas Regionais**:
   - Jogos com alto desempenho em regiões como América do Norte e Europa tendem a liderar as vendas globais. Isso reflete o tamanho e a força desses mercados.

2. **Impacto das Características do Jogo**:
   - Jogos de gêneros como **Esportes** e **RPGs** são especialmente relevantes em determinadas regiões. Por exemplo, RPGs performam melhor no Japão, enquanto Esportes lideram nos EUA.

3. **Nintendo como um Caso de Sucesso**:
   - Os jogos da Nintendo, em plataformas como Wii e NES, dominam as vendas globais. Isso demonstra como plataformas populares e franquias de renome influenciam o sucesso global.

4. **Precisão do Modelo**:
   - Com **R² de 0.86**, o modelo pode ser confiavelmente utilizado para prever o desempenho de novos jogos com base em características similares.

---

## **Conclusões**
- O modelo demonstrou ser uma ferramenta poderosa para prever vendas globais de jogos e oferecer insights valiosos para publishers e desenvolvedores.
- Para a Nintendo, o modelo destacou como franquias fortes, plataformas populares e regiões específicas contribuem para o sucesso global.
- Este modelo pode ser expandido e aplicado a previsões para outros publishers ou em análise de tendências futuras.

---

https://colab.research.google.com/drive/1T4REjgRO2YUoJOEtEZLuJgeBX_RcEQSc#scrollTo=9H4U6AyZOpp6