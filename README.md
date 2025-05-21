# 📊 Walmart Sales Insights: Análise Preditiva e Exploratória das Vendas em 45 Lojas (EUA, 2010-2012)

**Objetivo**: Analisar e prever as vendas de 45 lojas do Walmart nos EUA (2010-2012), identificando padrões sazonais, impactos de promoções e variáveis críticas para otimizar decisões de negócios.

## 📌 Sumário
- [Dataset](#dataset)
- [Descobertas Chave](#-descobertas-chave)
- [Técnicas Utilizadas](#-técnicas-utilizadas)
- [Resultados](#-resultados)
- [Como Reproduzir](#-como-reproduzir)

## Dataset
- **Origem**: O arquivo contém informações sobre as Vendas Semanais de 45 lojas no período de 2010 a 2012, incluindo fatores que impactam as vendas, como Feriados, Temperatura, Preço do Combustível, IPC (Índice de Preços ao Consumidor) e Taxa de Desemprego. Link do dataset: https://www.kaggle.com/datasets/varsharam/walmart-sales-dataset-of-45stores/data
- **Pré-processamento: Análise de dados**:
  - Criação de novas variáveis.
  - Tratamento de valores nulos.
  - Tradução do nome da variáveis para o português
    
- **Pré-processamento: Machine Learning**:
  - Exclusão de variaveis indeferentes pro modelo: ['Fuel_Price', 'Super_Bowl', 'Labour_Day'] .
  - Padronização e normalização de features para melhor performance dos modelos.
  - Divisão de 80/20 para treino e teste dos modelos.

## 🔍 Descobertas Chave
1. **Features Mais Impactantes: Análise de dados**:
   - A loja foi a variável que apresentou um maior impacto nas vendas, isto é, caracteristicas como
     tamanho da loja, localização... impactaram positivamente nas vendas
   - Temperatura, indice de preços e desemprego apresentaram uma correlação negativa em relação a variavel
     target "Vendas Semanais", isso diz que, na medida que essas variaveis caem de valor, aumenta o número
     de vendas.
   - O dia do trabalho e o natal foram feriados que não tiveram praticamente nenhum impacto na variável
     
   **Features Mais Impactantes: Machine Learning**:
   - Dia de ação de graças, Natal e Taxa de desemprego tiveram maior peso nos modelos lineares.
   - Loja, Desemprego, CPI e Temperatura tiveram maior peso nos modelos não lineares.
  

3. **Performance dos Modelos**:

=== Comparação dos Modelos ===
- DESCONSIDERANDO FEATURES QUE POSSUEM INFLUENCIA INFERIOR A 0.01.

RF RMSE: 398472.4917170457
RF R2: 0.4624575598625814

GBT RMSE: 181167.2578936221
GBT R2: 0.8888842839339648

RIDGE RMSE: 497456.4403781198
RIDGE R2: 0.16222734058622656

LASSO RMSE: 497456.4447413191
LASSO R2: 0.16222732588998856

XGBoost RMSE: 86781.98764726309
XGBoost R2: 0.9745038119739273

3. **Visualização Crítica**:


![DACorr](https://github.com/user-attachments/assets/1282b638-8bc4-408c-9f51-151dd585a606)
![DADesempregoVSVendas](https://github.com/user-attachments/assets/ed497011-ca3a-4bf7-9bb5-742ecdffd19c)
![GasolinaVSPreco](https://github.com/user-attachments/assets/99252289-80f4-43b0-8f39-09f753531693)



## ⚙️ Técnicas Utilizadas
- **Análise Exploratória (EDA)**
   - Pandas: Para manipulação e analise de dados.
   - NumPy: Armazenar e manipular dados numéricos de forma eficiente
   - Seaborn - criação de gráficos estatísticos, como foi feito o heatmap
   - Matplotlib - Analise gráfica dos dados
   - PySpark: Para manipulação e análise de Big data.
- **Modelagem**:
  - **Lineares**: Ridge, Lasso.
  - **Não Lineares**: XGBoost, Random Forest, Gradient Boosted Decision Tree.
- **Avaliação**: R², MAE, RMSE (para interpretabilidade).
  - R²: Avalia o quanto o modelo explica a variação dos dados.
  - RMSE (Root Mean Squared Error): Raiz do erro quadrático médico, penaliza erros grandes de forma mais intensa.
  - MAE (Mean Absolute Error): Média dos valores absolutos dos erros, não penaliza grandes desvios, sendo menos sensivel a outliers.

## 📈 Resultados
Em relação a análise de dados, conclui-se que a Loja foi a variável que mais impactou com o crescimento das vendas, considerando fatores
como localização e tamanho por exemplo.

Ao analisarmos os dois gráficos, comparando desemprego e o preço da gasolina com as vendas, percebemos que tanto o preço da gasolina
quanto a taxa de desemprego, ao aumentar até certo ponto: Gasolina com preço superior a $3.75 e indice de desemprego superior a 9%, há uma queda
significativa nas vendas.

Feriados tendem a ter impactos diferentes nas vendas, visto que, o dia do trabalho não houve influência nenhuma nas vendas, em contrapartida, o dia de ação
de graças teve uma correlação de 0.09.

Temperatura teve uma correlação negativa de -0,07 com as vendas, isto é, em regiões mais frias, o número de vendas é consideravelmente maior.

**💻 Resultados no Machine Learning**

Para prever as vendas nas lojas do Walmart, testei diferentes algoritmos de regressão. A avaliação foi feita com base nas métricas RMSE (Root Mean Squared Error) e R² (coeficiente de determinação).

🔹 Desempenho dos Modelos:
XGBoost
RMSE: 86.781,98
R²: 0.974
Melhor desempenho geral, com excelente capacidade preditiva.

GBT (Gradient Boosted Trees)
RMSE: 181.167,25
R²: 0.889
Bom desempenho, destacando-se por capturar padrões não lineares.

Random Forest
RMSE: 398.472,49
R²: 0.462
Performance intermediária, mas com insights relevantes sobre variáveis.

Lasso / Ridge
RMSE: ~497.456
R²: 0.162
Modelos lineares com menor capacidade de previsão neste contexto.

- Importância das Variáveis (Feature Importance)
Variável mais relevante em todos os modelos: Loja
→ Indica que o histórico e perfil da loja influenciam fortemente nas vendas.

Modelos de árvore (RF, GBT, XGBoost):
Variáveis econômicas como Unemployment(Desemprego) e CPI(índice de desemprego) aparecem com grande influência.
Sazonalidade também contribui: month, day e Temperature são relevantes.

Modelos lineares (Lasso, Ridge):
Datas comemorativas como Thanksgiving e Christmas tiveram peso elevado.
Boa capacidade de capturar relações específicas, mesmo com menor performance geral.

**🎯 Conclusão dos Resultados ML**

O modelo XGBoost se destacou como o mais eficaz para prever vendas, demonstrando que técnicas avançadas de boosting são adequadas para lidar com a complexidade do comportamento de consumo nas lojas.

Além disso, a análise de importância das features revelou quais fatores mais influenciam as vendas, auxiliando na tomada de decisões estratégicas para campanhas sazonais, localização e foco em indicadores econômicos.
