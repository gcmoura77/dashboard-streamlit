# Construindo um Dashboard em Python com Streamlit

Além do Streamlit como frontend, usarei o pandas para tratamento dos dados e o Altair/Ploty para a visualizaçao destes dados.

Este hands-on foi baseado neste outro tutorial https://blog.streamlit.io/crafting-a-dashboard-app-in-python-using-streamlit/ criado por Chanin Nantasenamat (https://blog.streamlit.io/author/chanin/)

Os objetivos de aprendizado aqui são: 

1. Definir as principais métricas
2. Realizar a Análise Exploratória dos Dados 
3. Construir o dashboard com Streamlit

## Como será o Dashboard?

![Image](https://blog.streamlit.io/content/images/size/w1000/2024/01/streamlit-dashboard-components.jpg)

## 1. Definir as principais métricas

Primeira coisa que precisa ser feita é a defição de boa métricas para medir o que reamente é importante.

### 1.1 Visão Geral de métricas

O objetivo de qualquer painel é apresentar insights que forneçam a base para a tomada de decisões baseada em dados. Qual é o objetivo principal do painel? Isso orientará as perguntas subsequentes que você deseja que o painel responda na forma de métricas principais.

Por exemplo:

* Nas vendas, o objetivo principal pode ser entender: “Como está o desempenho das equipes de vendas?” As métricas podem incluir receita total por representante de vendas, unidades vendidas por território ou novos leads gerados ao longo do tempo. 

- Em marketing, o objetivo principal pode ser entender “Qual é o desempenho da minha campanha?” isso pode incluir a medição de indicadores avançados, como taxas de resposta ou taxa de cliques, e indicadores atrasados, como taxa de conversão de receita ou custos de aquisição de clientes. 

- Em finanças, o painel pode precisar responder “Quão lucrativo é o nosso negócio?” isso pode incluir lucro bruto, margem operacional e retorno sobre ativos.

### 1.2 Métricas principais selecionadas para a aplicação

A questão principal que este Dashboard populacional pretende responder é: como as populações dos estados dos EUA mudam ao longo do tempo? Que perguntas precisamos fazer para nos ajudar a responder a essa meta do painel? 

1. Como as populações totais se comparam entre os diferentes estados? 
2. Como as populações dos estados evoluem ao longo do tempo e como elas se comparam entre si? 
3. Em um determinado ano, quais estados tiveram mais de 50.000 pessoas entrando ou saindo? Rotularemos essas métricas de migração de entrada e saída.

## 2. Realizar a Análise Exploratória dos Dados 

Uma vez definidas as métricas, precisaremos coletar e obter um conhecimento sólido sobre os dados disponíveis antes de podermos apresentá-los de forma visualmente estética em nosso painel.

A análise exploratória de dados, ou em inglês **Exploratory Data Analysis (EDA)** pode ser definida como um processo iterativo de compreensão dos dados que envolve fazer e responder perguntas por meio de um trabalho investigativo de análise dos dados. Em essência, seu Dashboard começa como uma tela em branco e o EDA fornece uma abordagem pragmática para criar dados visuais atraentes que contam uma história.

Algumas notas importantes baseadas no trabalho de John Turkey:

-  `“O maior valor de um gráfico é quando ele nos obriga a ver o que nunca esperávamos.”` Na verdade, Tukey introduziu o Box and Whisker Plot (também conhecido como Box Plot).
- Ter uma mentalidade flexível e aberta na abordagem dos dados, daí a natureza “exploratória” da EDA.

### 2.1 Quais dados estão disponíveis?

Os dados são do censo americano disponíveis no sitem do [US Census Bureau](https://www.census.gov/data/datasets/time-series/demo/popest/2010s-state-total.html) e foram selecionadas 3 informações importantes para servir de base para as métricas: estados, ano e população.

```
states, states_code, id, year, population
Alabama, AL, 1, 2010, 4785437
Alaska, AK, 2, 2010, 713910
Arizona, AZ, 4, 2010, 6407172
Arkansas, AR, 5, 2010, 2921964
California, CA, 6, 2010, 37319502
```

### 2.2. Preparação dos dados

Consolide as colunas do ano em uma única coluna unificada. A vantagem de subdividir os dados por ano fornecerá o formato necessário para gerar possíveis visualizações (por exemplo, um mapa de calor, choropleth map, etc.) e um dataframe classificável.

### 2.3. Seleção dos gráficos para melhor visualização das principais métricas.

Agora que temos uma melhor compreensão dos dados ao nosso alcance e das principais métricas a serem medidas, é hora de decidir como visualizar os resultados em nosso painel. Existem inúmeras maneiras de visualizar seus conjuntos de dados. Aqui está o que foi selecionado para nosso aplicativo de painel populacional.

1. Qual é a comparação da população total entre os diferentes estados? 
- Um choropleth map adiciona uma dimensão geoespacial para destacar os estados mais e menos povoados.

2. Como as populações de diferentes estados evoluem ao longo do tempo e como elas se comparam entre si?
- Um mapa de calor oferece uma visão abrangente dos estados com os valores populacionais mais altos e mais baixos, apresentando essas informações em diferentes anos
- A classificação do dataframe fornece uma comparação rápida e direta dos estados mais e menos povoados, eliminando assim a necessidade de percorrer diferentes seções dos gráficos.

3. Num determinado ano, que percentual de todos os estados tiveram migração de entrada/saída de mais de 50.000 pessoas? 
- Um gráfico de rosca é um gráfico de pizza com um arco interno vazio e estamos usando isso para visualizar a porcentagem de migração de estado de entrada e saída.

Existe uma variedade enorme de visualizações que poderia ser experimentadas e pode-se descobrir estas opções na coleção crescente de componentes personalizados que a comunidade produz. Alguns que você pode experimentar:

- streamlit-extras: extensões de funcionalidades do Streamlit.
- streamlit-shadcn-ui:  série de interfaces de componentes de frontend como: modal, hovercard, badges, etc. 
- streamlit-elements: permite a criação de componentes de Dashboard arrastáveis e redimensionáveis.

## Mapa dos Estados Brasileiros
[How to create and interactive map of Brazil using Plotly.Express-Geojson in Python](https://python.plainenglish.io/how-to-create-a-interative-map-using-plotly-express-geojson-to-brazil-in-python-fb5527ae38fc)

## Construindo o Dashboard com Streamlit
