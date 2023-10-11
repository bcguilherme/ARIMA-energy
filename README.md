# ARIMA-energy
Descrição: Análise de Séries Temporais com Previsões e Modelagem SARIMA

Este projeto envolveu uma análise de séries temporais utilizando a linguagem Python e diversas bibliotecas, incluindo NumPy, Pandas, Matplotlib, StatsModels, pmdarima e scikit-learn. O foco da análise foi a previsão de uma série temporal de produção de dados ao longo de um período de tempo.

Aqui estão os principais passos e ações realizados no projeto:

Importação de Bibliotecas: Foram importadas as bibliotecas necessárias, incluindo NumPy, Pandas, Matplotlib, StatsModels, pmdarima e scikit-learn, para análise de dados, previsões e modelagem.

Exploração de Dados Iniciais: A série temporal de produção de dados foi carregada e explorada para entender sua estrutura e tendências. Isso envolveu a análise de estatísticas descritivas, como média, desvio padrão, mínimo e máximo.

Decomposição de Séries Temporais: A série temporal foi decomposta em componentes de tendência, sazonalidade e resíduos usando a função seasonal_decompose da StatsModels. Isso ajudou a entender os padrões subjacentes nos dados.

Teste de Estacionariedade: Foram realizados testes ADF (Augmented Dickey-Fuller) para verificar a estacionariedade dos dados originais e de suas diferenças. Isso é essencial para determinar a ordem de diferenciação necessária.

Modelagem SARIMA: Um modelo SARIMA (Seasonal AutoRegressive Integrated Moving Average) foi ajustado aos dados usando a função auto_arima do pmdarima. O processo de seleção de hiperparâmetros, como ordem de diferenciação, ordens AR (AutoRegressive) e MA (Moving Average), e componentes sazonais, foi automatizado.

Previsões e Intervalo de Confiança: Foram obtidas previsões futuras usando o modelo SARIMA ajustado e calculados intervalos de confiança para as previsões. Isso permitiu estimar a incerteza nas previsões.

Avaliação de Desempenho: O erro médio absoluto (MAE) foi calculado para avaliar o quão bem as previsões do modelo se ajustam aos dados reais.

Visualização de Resultados: Os resultados foram visualizados usando gráficos para mostrar as previsões, intervalos de confiança e os dados reais ao longo do tempo.

Exportação para o GitHub: Os códigos e resultados foram registrados e compartilhados no GitHub para referência futura.
