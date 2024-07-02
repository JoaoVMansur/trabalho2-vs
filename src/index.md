# Trabalho 2: Visualização de Dados

Este trabalho é fruto da análise de um conjunto de dados provenientes de uma competição entitulada "Datathon", que é um evento realizado em um fim de semana no qual é proposto que os participantes trabalhem em casos de negócio do mundo real de diferentes áreas de aprendizado de máquina, IA e ciência de dados. 

O conjunto de dados utilizado é derivado da Argo Solutions, Empresa líder em tecnologia na América Latina, que atua proporcionando o desenvolvimento de soluções que facilitem a gestão de despesas de viagens corporativas utilizando a tecnologia para promover estes processos e consequentemente seus respectivos resultados.


# Data Set Utilizado - Travel Dataset (Datathon 2019):

```js
const dataSet = await FileAttachment("./data/flights.csv").csv({typed: true});

view(Inputs.table(dataSet));

```
# Observações: 
Com base no conjunto de dados exposto acima é possível visualizar as seguintes informações pertinentes acerca desta análise: O código da viagem, o código do usuário,  origem e destino dos vôos, o tipo de classe em que o passageiro decidiu ser acomodado, o preço relativo a cada trecho realizado, o tempo de deslocamento, a distância percorrida em cada viagem, qual foi a agência que realizou a venda da passagem aérea e, por fim, a data vôo.
