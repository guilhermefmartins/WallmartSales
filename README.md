# 📊 Análise de Severidade de Câncer: Modelos Lineares vs. Não Lineares

**Objetivo**: Prever o "Target_Severity_Score" com base em variáveis como hábitos de vida, fatores genéticos e custos de tratamento, comparando desempenho de modelos lineares e não lineares.

## 📌 Sumário
- [Dataset](#dataset)
- [Descobertas Chave](#-descobertas-chave)
- [Técnicas Utilizadas](#-técnicas-utilizadas)
- [Resultados](#-resultados)
- [Como Reproduzir](#-como-reproduzir)

## Dataset
- **Origem**: Dados sintéticos simulando pacientes com câncer (2015-2024).
- **Pré-processamento**:
  - Exclusão de variaveis indeferentes pro modelo.
  - Tratamento de valores nulos.
  - OneHotEncoder para features não ordenadas
  - LabelEncoder quando havia uma relação natural de ordenação
  - Padronização e normalização de features para melhor performance dos modelos.

## 🔍 Descobertas Chave
1. **Features Mais Impactantes**:
   - `Smoking` e `Genetic_Risk` tiveram maior peso nos modelos não lineares.
   - `Treatment_Cost_USD` mostrou relação inversa com o score de severidade, isto é, quanto mais caro for custo de tratamento do cancer, menor o risco corrido.
   -  (coef. negativo em modelos lineares).

2. **Performance dos Modelos**:

=== Comparação dos Modelos ===
           Model       R²      MAE     RMSE
   Decision Tree 0.886747 0.322330 0.401145
   Random Forest 0.954968 0.202192 0.252951
         XGBoost 0.995268 0.065404 0.082000
LinearRegression 0.999994 0.002496 0.002886
           Ridge 0.999994 0.002496 0.002886
           Lasso 0.999952 0.006624 0.008233

3. **Visualização Crítica**:
 ![image](https://github.com/user-attachments/assets/a4b01a5b-7429-4592-8261-bef5a6132390)
 ![image](https://github.com/user-attachments/assets/4b38eec9-5f80-49cd-9a78-c3e0a1f5f13e)
 ![image](https://github.com/user-attachments/assets/fcb0bc64-f127-45f6-9132-9dd3e5b0efc4)
 ![image](https://github.com/user-attachments/assets/023fef94-368d-4d18-8250-7e50bfa94f6e)
 ![image](https://github.com/user-attachments/assets/d2cde309-ae92-45b3-ad0a-4cdb5cc52fce)


## ⚙️ Técnicas Utilizadas
- **Análise Exploratória (EDA)**
   - Pandas: Para manipulação e analise de dados.
   - NumPy: Armazenar e manipular dados numéricos de forma eficiente
   - Seaborn - criação de gráficos estatísticos, como foi feito o heatmap
   - Matplotlib - Analise gráfica dos dados
- **Modelagem**:
  - **Lineares**: Regressão Linear, Ridge, Lasso.
  - **Não Lineares**: XGBoost, Random Forest, Decision Trees.
- **Avaliação**: R², MAE, RMSE (para interpretabilidade).
  - R²: Avalia o quanto o modelo explica a variação dos dados.
  - RMSE (Root Mean Squared Error): Raiz do erro quadrático médico, penaliza erros grandes de forma mais intensa.
  - MAE (Mean Absolute Error): Média dos valores absolutos dos erros, não penaliza grandes desvios, sendo menos sensivel a outliers.

## 📈 Resultados
A análise revelou que os modelos lineares (Linear Regression, Ridge e Lasso) performaram excepcionalmente bem, com valores de R² superiores a 0.999, indicando alta capacidade de explicar a variabilidade dos dados.
Além disso, os erros (MAE e RMSE) foram extremamente baixos, sugerindo previsões precisas e estáveis. Esses resultados apontam para uma predominância de relações lineares entre as variáveis.

Por outro lado, os modelos não lineares (Decision Tree, Random Forest e XGBoost) também apresentaram boa performance, com destaque para o XGBoost (R² = 0.995), que capturou interações complexas entre variáveis.
O Random Forest também se mostrou robusto, enquanto o Decision Tree teve um desempenho inferior, mas ainda interpretável.

As análises de importância de features destacaram Smoking, Genetic_Risk, Alcohol_Use e Air_Pollution como os principais fatores de influência em ambos os tipos de modelos, 
validando as correlações encontradas na etapa de análise exploratória. Isso reforça a confiabilidade dos modelos em identificar padrões críticos para a severidade do câncer.
