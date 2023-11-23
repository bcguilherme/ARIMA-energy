Passos do Projeto

    Instalação de Pacotes:
        Instalamos os pacotes necessários para o projeto, como scipy e pmdarima.

python

!pip install scipy
!pip install pmdarima

    Importação de Bibliotecas:
        Importamos as bibliotecas essenciais para manipulação de dados, análise de séries temporais e modelagem.

python

import pandas as pd
from statsmodels.tsa.arima.model import ARIMA
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
from statsmodels.tsa.stattools import adfuller
from pmdarima.arima import auto_arima
from statsmodels.tsa.statespace.sarimax import SARIMAX
from sklearn.metrics import mean_absolute_error

    Carregamento e Análise Inicial dos Dados:
        Carregamos os dados do arquivo 'energy.xlsx' e realizamos uma breve análise estatística.

python

df = pd.read_excel('/content/energy.xlsx', index_col='DATE', parse_dates=True)
df.describe()
df.index.min(), df.index.max()

    Visualização da Série Temporal:
        Visualizamos a série temporal da produção de energia.

python

df['producao'].plot(figsize=(10, 6))
plt.show()

    Decomposição da Série Temporal e Teste ADF:
        Realizamos a decomposição da série temporal e aplicamos o teste ADF (Augmented Dickey-Fuller) para verificar a estacionariedade.

python

resultado = seasonal_decompose(df)
fig = plt.figure(figsize=(8, 6))
resultado.plot()

result = adfuller(df['producao'].diff().dropna())
print(f'Teste ADF: {result[0]}, p valor: {result[1]}')

    Modelo ARIMA com Auto-Arima:
        Utilizamos o Auto-Arima para encontrar os melhores parâmetros para o modelo ARIMA.

python

fit_arima = auto_arima(df, d=1, start_q=1, max_p=3, max_q=3, seasonal=True, n=6, D=1, start_P=1, start_Q=1, max_P=2, max_Q=2, information_criterion='aic', trace=True, error_action='ignore', stepwise=True)

    Modelo SARIMAX:
        Aplicamos o modelo SARIMAX para a série temporal.

python

model = SARIMAX(df, order=(1,1,1), seasonal_order=(1,1,2,6))
resultado_sarimax = model.fit()

    Previsões e Intervalo de Confiança:
        Realizamos previsões com o modelo SARIMAX e calculamos o intervalo de confiança.

python

predicoes = resultado_sarimax.get_prediction(start=-12)
predicao_media = predicoes.predicted_mean

intervalo_confianca = predicoes.conf_int()
limite_abaixo = intervalo_confianca.iloc[0, 0]
limite_acima = intervalo_confianca.iloc[0, 1]

    Avaliação da Previsão:
        Calculamos o erro médio absoluto (MAE) para avaliar a qualidade da previsão.

python

mae = mean_absolute_error(df[-12:].values, predicao_media.values)
print(f'MAE: {mae}')

    Forecast e Plotagem:
        Geramos previsões futuras e plotamos o resultado.

python

forecast = resultado_sarimax.get_forecast(steps=12)
forecast_medio = forecast.predicted_mean

intervalo_confianca_forecast = forecast.conf_int()
intervalo_abaixo_f = intervalo_confianca_forecast.iloc[0:, 0]
intervalo_acima_f = intervalo_confianca_forecast.iloc[:, 1]

plt.plot(df.index, df['producao'], label='Dados reais', color='blue')
plt.plot(predicao_media.index, predicao_media, label='Previsões', color='red')
plt.plot(forecast_medio.index, forecast_medio, label='Forecast', color='green')
plt.xlabel('Data')
plt.ylabel('Valor')
plt.legend()
plt.show()
