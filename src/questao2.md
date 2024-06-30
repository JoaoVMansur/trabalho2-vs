# Parte 2: Preco dos Voos.
<br>
<br>
<br>

Para essa segunda parte vamos analisar os dados de uma perspectiva do custo das passagens.
Primeiro gostariamos de analisar a evolucao do preco medio das passagens para cada ano


<div id="PrecoMedioPorAno" class="card">
    <h1>Quantidade de voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoMedioPorAno(divWidth - 45)) }
    </div>
</div>

Conseguimos por meio dessa visualizacao observar uma certa logica com a hipotese levantada na parte 1 de que o mercado aereo foi impactado pela pandemia do covid-19, podemos ver uma reducao do preco medio das passagens ao longo dos anos de pandemia e uma tendencia de volta de alta em 2023 que foi quando o virus foi vencido.Porem, a diferenca do preco medio das passagens e muito pequena para ser levada a serio.

# Agencias

Vamos observar agora o preco medio das passagens em relacao as agencias de viagem.


<div id="PrecoMedioPorAgencia" class="card">
    <h1>Quantidade de voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoMedioPorAgencia(divWidth - 45)) }
    </div>
</div>

Podemos ver quer as agencias Rainbow e CloudFly tem um preco medio praticamente identico, porem a FlyingDrops apresentou uma disparidade em relacao as duas outras. qual seria o motivo?

Para os tipos de passagens aereas temos 3 tipos, Economica, Premium e First Class. Ao analisar o conjunto de dados temos a seguinte distribuicao
<div id="QuantidadePorTipo" class="card">
    <h1>Quantidade de voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(QuantidadePorTipo(divWidth - 45)) }
    </div>
</div>
Com essa visualizacao e possivel observar que o motivo de o valor medio do preco das passagens da agencia FLyingDrops ser mais alto e de que ela e a unica que vende apenas voos de First Class.

Agora vamos analisar a relacao entre distancia e preco das passagens. Consideramos apenas tarifas de voos na classe economica.
<div id="PrecoDistancia" class="card">
    <h1>Quantidade de voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoDistancia(divWidth - 45)) }
    </div>
</div>
E clara a relacao entre distancia e preco pois conseguimos observar que quanto mais longe o voo e o mesmo vale para a relacao entre preco x tempo pois assim como a distancia sao proporcinais, a medida que uma cresce a outra tambem.



<div id="PrecoTempo" class="card">
    <h1>Quantidade de voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(PrecoTempo(divWidth - 45)) }
    </div>
</div>
# Desings utilizados.

Nesta análise, utilizamos dois tipos de gráficos distintos: o gráfico de barras e o gráfico de linhas.

Para visualizar o processo de filtragem e apresentar os dados após a manipulação, decidimos utilizar um gráfico de barras, uma escolha eficaz para uma representação visual clara da quantidade de músicas ao longo dos anos analisados. As barras verticais coloridas funcionam como marcadores, cada uma representando a quantidade de músicas em seus respectivos anos. Quanto aos canais visuais, a altura das barras reflete a quantidade de músicas em cada ano, enquanto o eixo x denota os anos e o eixo y representa a contagem ou número de músicas.

Para acompanhar a variação do top 10 das músicas e dos artistas ao longo do tempo, optamos por empregar o gráfico de linhas. Essa escolha nos permite visualizar de forma clara e intuitiva as mudanças nos dados ao longo dos anos, fornecendo insights valiosos sobre as tendências e padrões que emergem nesse período.Nosso gráfico de linhas utiliza uma linha contínua como marcador, destacando a mudança ao longo do tempo nos dados do top 10. Quanto aos canais visuais, o eixo x, assim como no gráfico de barras, representa os anos. Já a altura da linha representa a quantidade de streams no respectivo ano, permitindo uma compreensão imediata da evolução desses dados ao longo do tempo.



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

console.log(avgPricesByAgency);

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