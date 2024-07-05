# Parte 2: Preço dos Vôos
<br>
<br>
<br>

Para a segunda parte deste estudo iremos analisar os dados pela perspectiva do custo das passagens.

Em primeiro lugar gostaríamos de analisar a evolução do preço médio das passagens para cada ano.


<div id="PrecoMedioPorAno" class="card">
    <h1>Preço médio das passagem ao longo dos anos</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoMedioPorAno(divWidth - 45)) }
    </div>
</div>

Com base nesta visualização, foi possível observar uma certa correspondência lógica com relação a hipótese levantada na Parte 1 deste trabalho, de que o mercado aéreo sofreu impactos por conta da pandemia do COVID-19. É possível observar uma redução do preço médio das passagens ao longo dos anos atrelados ao período da pandemia, assim como houve uma tendência ao retorno do aumento no preço das tarifas das passagens aéreas em 2023, que foi o ano em que a disseminação do vírus conseguiu ser controlada com eficácia. Porém, a diferença do preço médio das passagens possui um valor considerado irrisório para que seja visto como significativo.

# Agências

Neste trecho iremos focar nossa observação em relação ao preço médio das tarifas de Voo em relação as agências de viagem.


<div id="PrecoMedioPorAgencia" class="card">
    <h1>Preço médio por agência</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoMedioPorAgencia(divWidth - 45)) }
    </div>
</div>

Como podemos verificar, as agênncias de viagem Rainbow e CloudFly tem um preço médio praticamente idêntico, entretanto a FlyingDrops apresentou uma disparidade em relacao as duas anteriores. Qual seria o motivo?


Como mostrado na parte 1 deste trabalho, verificamos que a agência FlyingDrops vendeu apenas passagens na Primeira Classe durante todo o período analisado. Isso explica o motivo de ela ter um preço médio superior ao das outras agências. No entanto, após aquela análise, surgiu a dúvida se a saúde financeira da agência seria afetada, já que o número de passagens aéreas vendidas pela FlyingDrops foi significativamente inferior em comparação às outras duas agências. Agora, com essa visualização, podemos ver que pelo menos o preço médio das passagens vendidas pela agência foi satisfatório. No entanto, não podemos depender apenas do preço médio; também queremos saber sobre o faturamento total das agências.

<div id="GanhoTotalAgencias" class="card">
    <h1>Faturamento bruto por agência</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(GanhoTotalAgencias(divWidth - 45)) }
    </div>
</div>

Podemos observar que, apesar do ticket médio mais alto da agência FlyingDrops, seu faturamento foi menos da metade comparado às outras duas agências. Isso sugere que, apesar de se concentrar no público A+++, que geralmente busca serviços de primeira classe e preço mais elevado, a FlyingDrops enfrentou desafios significativos em termos de volume de vendas. Essa disparidade indica que, enquanto pode ter alcançado sucesso entre um segmento mais exclusivo e lucrativo em termos individuais, o impacto total no faturamento foi inferior ao das suas concorrentes.

# Distancia e Duração

Agora vamos analisar a relacao entre distância percorrida e preço das passagens aéras. 

Consideramos apenas tarifas de Voos na classe Econômica.
<div id="PrecoDistancia" class="card">
    <h1>Preço x Distancia</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoDistancia(divWidth - 45)) }
    </div>
</div>
A relação entre distância e preço das tarifas é evidente, pois observamos que quanto maior a distância entre os trechos dos voos, maior é o valor das passagens. Essa relação também se aplica à comparação entre preço e tempo de voo, onde ambas as grandezas são diretamente proporcionais: à medida que uma aumenta, a outra também aumenta, seguindo o mesmo padrão de comportamento.

<div id="PrecoTempo" class="card">
    <h1>Preço x Tempo de Voo</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoTempo(divWidth - 45)) }
    </div>
</div>

# Desings utilizados.

Nesta análise, utilizamos três tipos de gráficos distintos: o gráfico de barras, o gráfico de linhas e o scatterplot.

Para os gráficos de barras, utilizamos para mostrar o preço médio das passagens vendidas por agência durante todo o período e o faturamento bruto total das agências. Para os marcadores, utilizamos barras verticais em que a altura representa o preço médio da passagem e o faturamento total das agências, enquanto o eixo y contém as agências representadas no conjunto de dados.

O gráfico de linhas foi utilizado para mostrar a tendência do preço médio geral das passagens ao longo do período presente no conjunto de dados. O marcador é uma linha que representa o eixo y do gráfico, onde temos o preço médio da passagem ao longo dos anos presente no eixo x.

O scatterplot foi escolhido para representar a correlação entre duas variáveis, sendo ele utilizado em dois casos: na relação Preço x Distância e na relação Preço x Tempo de voo. Para os marcadores, utilizamos círculos que se posicionam no gráfico de acordo com a sua relação entre as características citadas. Quanto maior o preço, mais alto no eixo y o círculo será posicionado; e quanto maior o tempo ou a distância do voo, mais à direita do gráfico o círculo será posicionado.

```js
const divWidth = Generators.width(document.querySelector("#PrecoMedioPorAno"));

import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";

const vl = vegaLiteApi.register(vega, vegaLite);


const dataSet = await FileAttachment("./data/flights.csv").csv({typed: true});

// Create a helper function to get the year from a date string
const getYear = (dateString) => new Date(dateString).getFullYear();

// Aggregate data by year
const aggregatedData = dataSet.reduce((acc, item) => {
    const year = getYear(item.date);
    if (!acc[year]) {
        acc[year] = { sum: 0, count: 0 };
    }
    acc[year].sum += item.price;
    acc[year].count += 1;
    return acc;
}, {});

// Calculate the average price for each year
const avgPricesByYear = Object.keys(aggregatedData).reduce((acc, year) => {
    acc.push({
        ano: year,
        preco: (aggregatedData[year].sum / aggregatedData[year].count).toFixed(2)
    });
    return acc;
}, []);

console.log(avgPricesByYear);

const agencyData = dataSet.reduce((acc, item) => {
    const agency = item.agency;

    if (!acc[agency]) {
        acc[agency] = { sum: 0, count: 0 };
    }
    acc[agency].sum += item.price;
    acc[agency].count += 1;
    return acc;
}, {});

// Calculate the average price for each agency and include the quantity, rounding to two decimal places
const avgPricesByAgency = Object.keys(agencyData).reduce((acc, agency) => {
    acc.push({
        agencia: agency,
        preco: (agencyData[agency].sum / agencyData[agency].count).toFixed(2), // Rounding to 2 decimal places
        quantidade: agencyData[agency].count
    });
    return acc;
}, []);

const TotalEarnings = Object.keys(agencyData).reduce((acc, agency) => {
    acc.push({
        agencia: agency,
        totalEarnings: agencyData[agency].sum.toFixed(2), // Rounding to 2 decimal places if needed
        quantidade: agencyData[agency].count
    });
    return acc;
}, []);

console.log("GANHO TOTALLLL")
console.log(TotalEarnings);

const tipoVooAgencia = dataSet.reduce((acc, item) => {
    const agency = item.agency;
    const flightType = item.flightType;

    if (!acc[agency]) {
        acc[agency] = { firstClass: 0, economy: 0 , premium: 0};
    }
    if (flightType === 'firstClass') {
        acc[agency].firstClass += 1;
    } else if (flightType === 'economic') {
        acc[agency].economy += 1;
    }else if (flightType =='premium'){
        acc[agency].premium += 1
    }
    return acc;
}, {});

const flightTypeCountsByAgency = Object.keys(tipoVooAgencia).reduce((acc, agency) => {
    acc.push({
        agencia: agency,
        firstClass: tipoVooAgencia[agency].firstClass,
        economy: tipoVooAgencia[agency].economy,
        premium: tipoVooAgencia[agency].premium
    });
    return acc;
}, []);


const precoDistancia = dataSet
    .filter(entry => entry.flightType === 'economic')
    .map(entry => ({
        distancia: entry.distance,
        preco: entry.price
    }));


const precoTempo = dataSet
    .filter(entry => entry.flightType === 'economic')
    .map(entry => ({
        tempo: entry.time,
        preco: entry.price
    }));

```


```js


function PrecoMedioPorAno (divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: avgPricesByYear
            },
            "mark": {
                "type": "line"
            },
            "encoding": {
                "x": {
                    "field": "ano",
                    "type": "nominal",
                },
                "y": {
                    "field": "preco",
                    "type": "ordinal",
                },
            
            }
        }
    };
}


function PrecoMedioPorAgencia(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: avgPricesByAgency
            },
            "mark": {
                "type": "bar"
            },
            "encoding": {
                "x": {
                    "field": "agencia",
                    "type": "nominal",
                },
                "y": {
                    "field": "preco",
                    "type": "quantitative",
                },
            
            }
        }
    };
}
function GanhoTotalAgencias(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: TotalEarnings
            },
            "mark": {
                "type": "bar"
            },
            "encoding": {
                "x": {
                    "field": "agencia",
                    "type": "nominal",
                },
                "y": {
                    "field": "totalEarnings",
                    "type": "quantitative",
                },
            
            }
        }
    };
}

function QuantidadePorTipo(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: flightTypeCountsByAgency
            },
            repeat: { "layer": ["economy", "firstClass", "premium"] },
            spec: {
                "mark": {"type": "bar", "width": {"band": 0.5}},
                "encoding": {
                    "x": {
                        "field": "agencia",
                        "type": "nominal",
                        "band": 10
                    },
                    "y": {
                        "aggregate": "sum",
                        "field": { "repeat": "layer" },
                        "type": "quantitative",
                        "title": "Quantidade de Voos"
                    },
                    "color": { "datum": { "repeat": "layer" }, "title": "Streaming Chart", scale: { "range":["#1DB954", "#FF0000", "#8A2BE2", "#3a68bc", "#FFA500"] } },
                    "xOffset": { "datum": { "repeat": "layer" }
                    }
                },
                "config": {
                    "mark": { "invalid": null },
                    "scale": { "y": { "zero": true } },
                    "axis": { "title": "Título da Legenda Lateral" }
                },
                "transform": [
                    {
                        "stack": "y",
                        "as": ["y_start", "y_end"],
                        "groupby": ["quantidade"]
                    }
                ]
            }
        }
    };
}


    function PrecoDistancia(divWidth) {
        return {
            spec: {
                width: divWidth,
                height: 400,
                data: {
                    values: precoDistancia
                },
                "mark": {
                    "type": "circle"
                },
                "encoding": {
                    "x": {
                        "field": "distancia",
                        "type": "quantitative"
                    },
                    "y": {
                        "field": "preco",
                        "type": "quantitative"
                    },

                }
            }
        };
    }


function PrecoTempo(divWidth) {
    return {
        spec: {
            width: divWidth,
            height: 400,
            data: {
                values: precoTempo
            },
            "mark": {
                "type": "circle"
            },
            "encoding": {
                "x": {
                    "field": "tempo",
                    "type": "quantitative"
                },
                "y": {
                    "field": "preco",
                    "type": "quantitative"
                },

            }
        }
    };
}
```