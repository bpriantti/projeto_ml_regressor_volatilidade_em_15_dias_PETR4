# Projeto ML Regressor Volatilidade em 15 Dias PETR4
____

__Bussines Problem:__
> Durante a rotina de investimentos torna-se importante a estimação da volatilidade tanto para estimar a variação de portfólios ou para operações estruturadas de compra ou venda de volatilidade, sendo necessário o desenvolvimento de modelos quantitativos para o forecasting futuro de movimentos de alta ou baixa de volatilidade.

__Objetivo:__   

> Desenvolver um modelo quantitativo de Machine Learning, utilizando o framework sklearn, statsmodels para o forecasting da volatilidade em 15 dias do ativo PETR4 listado na bolsa de valores brasileira B3.

__Autor:__  
   - Bruno Priantti.
    
__Contato:__  
  - bpriantti@gmail.com

__Encontre-me:__  
   -  https://www.linkedin.com/in/bpriantti/  
   -  https://github.com/bpriantti
   -  https://www.instagram.com/brunopriantti/
   
__Frameworks Utilizados:__

- Numpy: https://numpy.org/doc/  
- Pandas: https://pandas.pydata.org/
- Matplotlib: https://matplotlib.org/ 
- Seaborn: https://seaborn.pydata.org/  
- Plotly: https://plotly.com/  
- Scikit learn: https://scikit-learn.org/stable/index.html
- Statsmodels: https://www.statsmodels.org/stable/index.html

__Project Steps:__

__Step 01:__ Processo de Aquisição de Dados

Realizou-se o processo de ETL com a API de dados, yfinance e com isso obteve-se a série histórica do ativo petr4 desde de 2017 a 2022:

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-1.png?raw=true"  width="600" >

__Step 02:__ Processo de Data Wralling

> Em seguida realizou-se o processo de data wralling que consiste em cálculos, manipulações e cálculo de features como variáveis independentes e variáveis alvo, para este caso a variável alvo é a volatilidade em 15 dias futuros, diante disso calculou-se a volatilidade em 15 dias e em seguida realizou-se lag trazendo os 15 dias futuros para o dia atual, sendo esta nossa variável target.

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-2.png?raw=true"  width="600">

> Realizou-se como demonstrado abaixo a visualização da distribuição de frequência da variável target:

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-3.png?raw=true"  width="600">

> Em seguida calculou-se as features que serviram para entrada do modelo de machine learning, optou-se por utilizar features de média, volatilidade de janelas diferentes, podemos observar as features na figura abaixo:

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-4.png?raw=true"  width="700">

> Adiante observou-se a correlação entre as features, estas que com alta correlação podem prejudicar o modelo o enviando informações duplicadas para resolver isso podemos utilizar basicamente dois approaches, ou removemos as features altamente correlacionadas ou utilizamos técnicas como a 
__Principal Component Analysis__ , esta que possibilita um tratamento algébrico a base de dados removendo a correlação os eixos entre features nos entregando um conjunto de features descorrelacionadas.

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-5.PNG?raw=true"  width="500">

__Step 03:__ Processo de Data Split

A partir desse ponto realizou-se o processo de data split em train/test, para seguinte research do modelo de machine learning, utilizou-se a proporção de 60%.

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-6.PNG?raw=true"  width="700">

__Step 04:__ Aplicando PCA:

Após a divisão de dados realizou-se o treinamento da PCA para a base de treinamento e  em seguida aplicou-se para a base de teste, evitando assim o que chamamos de data leakage que consiste em um expressão para indicar o vazamento de informações futuras para o nosso modelo, podendo nos dar uma performance melhor que o esperado que nao se tornaria concentra com o modelo em produção, como observamos temos o nosso conjunto de features totalmente descorrelacionado. 

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-7.PNG?raw=true"  width="500">

__Step 05:__ Treinando o Modelo:

Embora para o predict de volatilidade sejam comumente usados os modelos GARCH,TGARCH, optou-se aqui por utilizar o modelo de linear regression com o propósito de verificar o desempenho de um modelo simples no entanto muito conciso em seus resultados, para isso utilizou-se o framework statsmodels, observe abaixo o resultado do treinamento do modelo.

<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-8.PNG?raw=true"  width="500">

__Step 06:__ Avaliando o Modelo:

> Vamos agora avaliar a performance do modelo para dados de teste, no repport abaixo:


Repport Avaliação  Modelo:

Avaliação train: 
>MAE:  0.007  
RMSE:  0.01  

Avaliação test:  
>MAE:  0.009  
RMSE:  0.019  

MAE % base:  
>A vol média da base é: 0.028  
O percentual do MAE em relaçao à média da base: 32.75%  

Obs: 
> Obs 1: como podemos observar o Rsquare é de aproximadamente 15%, podemos traduzir isso como que o modelo consegue explicar em 15% a variável target, vamos agora avaliar outras métricas de regressão como o MAE, RMSE, todos para a base de teste.

> Obs 2: Como podemos observar o percentual do MAE em relação a média da base é maior do que 10%, sendo isso um indicativo de que a regressão pode não performar muito bem, no entanto vamos avaliar a performance dos valores previstos vs realizados.

- Gráfico Previstos vs Realizados:
<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-9.PNG?raw=true"  width="500">

- Gráfico Feature Importance:
<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-10.PNG?raw=true"  width="500">

- Avaliando Performance do Modelo:
<img src="https://github.com/bpriantti/Projeto_ML_Regressor_Volatilidade_em_15_dias_PETR4/blob/main/images/image-11.png?raw=true"  width="700">

Obs:
> Como notamos o modelo se tem a capacidade de prever momentos de alta e baixa da volatilidade, caso levássemos isso para a previsão em operações de volatilidade acertaremos a direção da vol, isso mostra que mesmo que com as métricas de regressao nao tao positivas ainda assim este modelo pode ser útil.
