
# Trabalho 2: Visualização de Dados

Neste trabalho, vamos analisar o conjunto de dados de viagens.



# Data Set:

```js
const dataSet = await FileAttachment("./data/flights.csv").csv({typed: true});

view(Inputs.table(dataSet));

```
# Comentario 
Temos o conjunto de dados acima que nos tras informacoes sobre origem e destino, preco  distancia percorrida, qual agencia realizou a venda do ticket e a data do voo.


