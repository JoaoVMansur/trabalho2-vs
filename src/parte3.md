# Parte 3 : Destinos dos Vôos
 
 Para uma análise final vamos agora analisar o conjunto de dados com um foco nos destinos dos Vôos.

Ao analisar o conjunto de dados, observamos que para cada vôo de ida de um destino A para um destino B, há um vôo correspondente de volta, ou seja, de B para A, imediatamente subsequente. Isso significa que podemos simplificar nossa análise ao considerar apenas uma dessas perspectivas (ida ou volta), já que os resultados obtidos serão consistentes, independentemente de como segmentamos nossas análises.
  <br>
  <br>
  <br>
Começamos a análise por destinos descobrindo as rotas mais populares.

<div class="grid grid-cols-2">
    <div id="VoosSaida" class="card grid-colspan-2">
        <h1 class="title">Quantidade de Vôos por  Cidade</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosSaida(divWidth - 200))}
        </div>
    </div>
</div>

Optamos por utilizar a ferramenta "heatmap", preenchendo os estados, pois, já que apesar dos destinos dos nossos vôos serem cidades, todas as rotas são relativas às capitais dos seus respectivos estados. Logo, se mostrássemos o mapa levando em consideração os municípios, a visualização ficaria com um aspecto muito "poluído", dificultando a visualização ao invés de simplifica-la. 
<div class="grid grid-cols-2">
    <div id="DestinosSaida" class="card grid-colspan-2">
        <h1 class="title">Voos saindo dos estados mapa</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(DestinosSaida(divWidth - 200))}
        </div>
    </div>
</div>


Com base nisso, podemos observar que Santa Catarina/Florianópolis é o estado/capital que lidera o ranking em número de vôos, seguido por Aracaju e Campo Grande. Essa visualização desafia a expectativa de que Rio de Janeiro e São Paulo seriam os destinos mais populares, revelando que os destinos no Nordeste também são bastante procurados. Esse padrão sugere uma diversidade nas preferências de viagem, destacando a crescente popularidade de destinos menos tradicionais entre os viajantes. A variedade na escolha de destinos não apenas enriquece as opções disponíveis para os passageiros, mas também reflete a dinâmica econômica e turística regional do país, onde várias cidades emergem como importantes centros de atividade aérea.

Optamos por observar também se os vôos por cidade por ano também seguiriam o mesmo padrão apresentado na primeira parte quando analisamos os dados de uma forma mais geral

<div class="grid grid-cols-2">
    <div id="VoosPorAnoPorCidade" class="card grid-colspan-2">
        <h1 class="title">Voos saindo dos estados mapa</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorAnoPorCidade(divWidth - 200))}
        </div>
    </div>
</div>
Como podemos observar na análise de todas as viagens agregadas, os vôos por destino também seguiram o padrão observado na parte 1, mostrando que todos os destinos, em geral, sofreram com a diminuição de visitantes ao longo dos anos. Mesmo sendo um destino notavelmente popular, segundo os dados disponíveis, isso não impediu que ele sofresse uma queda na quantidade de visitantes durante o período estipulado.

# Classe do Vôo Por Região

Neste trecho, iremos analisar a distribuição de tipos de assentos vendidos para os respectivos destinos.

<div class="grid grid-cols-2">
    <div id="TipoPorDestino" class="card grid-colspan-2">
        <h1 class="title">Distribuição de Tipos de Acomodação dos Vôos por Estado</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(TipoPorDestino(divWidth - 200))}
        </div>
    </div>
</div>

Com esta análise nossa intenção era a de verificar se destinos onde a população tem maior poder aquisitivo (Rio de Janeiro e São Paulo) dominariam a quantidade de passagens de primeira classe vendidas. No entanto, por meio da visualização, podemos ver que essa hipótese não se mostrou verdadeira, sendo Florianópolis o destino com mais vôos de primeira classe. Além disso, a região Nordeste, conhecida como uma das mais desfavorecidas do país, teve um volume de vendas de vôos de primeira classe maior que Rio e São Paulo.


# Desings utilizados

Em síntese, nesta parte empregamos quatro tipos de gráficos: o gráfico de barras, barras  compactado, linha e o heat map em cima do mapa do Brasil.

Optamos pelo gráfico de barras compactadas pois nosso objetivo era ilustrar a comparação de três variáveis diferentes (econômica, premium e primeira classe) com suas respectivas quantidades para uma mesma cidade, evidenciando a diferença na quantidade de cada tipo de passagem para cada cidade. Para os canais visuais, cada cor no gráfico representa um tipo de passagem entre as três disponíveis. Já os marcadores, a altura das barras, representam a quantidade de vôos de cada cidade, sendo cada uma das barras um tipo de passagem representada pelas cores.

Para o gráfico de barras comum, o intuito é similar ao do gráfico de barras compactadas, porém, desta vez, temos apenas uma variável. Para os marcadores, foram utilizadas barras horizontais para cada cidade e, como citado anteriormente, a altura representa a quantidade de vôos para cada cidade.

O gráfico compactado de linhas foi utilizado para mostrar a tendência da quantidade de vôos de cada cidade ao longo dos anos. Para os marcadores, usamos linhas que mostram a tendência da quantidade de vôos ao longo do tempo, e cada linha representa uma cidade diferente. Nos canais visuais, cada cor representa uma cidade diferente, facilitando assim a visualização das cidades.

Fizemos um heatmap sobre o mapa do Brasil para termos uma visualização mais clara das regiões com a maior quantidade de vôos representados no conjunto de dados. Os marcadores foram as áreas dos estados e os canais visuais foram a tonalidade da cor de acordo com a quantidade de vôos na região.










```js

const divWidth = Generators.width(document.querySelector("#DestinosSaida"));
import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";
import maplibregl from "maplibre-gl";

const vl = vegaLiteApi.register(vega, vegaLite);

const dataSet = await FileAttachment("./data/flights.csv").csv({ typed: true });
const voosPorEstado  = await FileAttachment("./data/voosPorEstado.csv").csv({ typed: true });
const mapa = await FileAttachment("./data/mapa.json").json({typed: true});


const cityFlightCountsFrom = dataSet.reduce((acc, flight) => {
    const fromCity = flight.from;
    const stateName = fromCity.substring(fromCity.lastIndexOf("(") + 1, fromCity.lastIndexOf(")"));
    const cityName = fromCity.split(" (")[0];
    const id = stateName; // Assuming state abbreviation as id

    if (!acc[id]) {
        acc[id] = {
            id,
            name: cityName,
            count: 0
        };
    }

    acc[id].count++;

    return acc;
}, {});





let flightCounts = dataSet.reduce((acc, voo) => {
    let saida = voo.from;
    acc[saida] = acc[saida] || { nome: saida, count: 0 };
    acc[saida].count++;
    return acc;
}, {});

let CidadesSaida = Object.values(flightCounts).sort((a, b) => a.count - b.count);

const flightsByTypeAndFrom = {};

// Iterar sobre o dataSet e contar os voos
dataSet.forEach(flight => {
    const from = flight.from;
    const flightType = flight.flightType;

    // Verificar se já existe uma entrada para o from
    if (!flightsByTypeAndFrom[from]) {
        flightsByTypeAndFrom[from] = {
            nome: from,
            economic: 0,
            premium: 0,
            firstClass: 0
        };
    }

    // Incrementar o contador para o tipo de voo correspondente
    flightsByTypeAndFrom[from][flightType]++;
});

const tipoPorCidade = Object.keys(flightsByTypeAndFrom).reduce((acc, nome) => {
    acc.push({
        nome: nome,
        firstClass: flightsByTypeAndFrom[nome].firstClass,
        economic: flightsByTypeAndFrom[nome].economic,
        premium: flightsByTypeAndFrom[nome].premium
    });
    return acc;
}, []);

// Step 1: Parse the year from the date string
dataSet.forEach((voo) => {
    let dateParts = voo.date.split('/');
    voo.ano = parseInt(dateParts[2], 10); // Convert year to integer
});

// Step 2: Aggregate flight counts by year and city
let flightsByYearAndFrom = dataSet.reduce((acc, voo) => {
    let from = voo.from;
    let ano = voo.ano;

    // Initialize the entry if it doesn't exist
    if (!acc[ano]) {
        acc[ano] = {
            ano: ano,
            "Recife (PE)": 0,
            "Florianopolis (SC)": 0,
            "Brasilia (DF)": 0,
            "Aracaju (SE)": 0,
            "Salvador (BH)": 0,
            "Campo Grande (MS)": 0,
            "Sao Paulo (SP)": 0,
            "Natal (RN)": 0,
            "Rio de Janeiro (RJ)": 0
        };
    }

    // Increment the count for the respective city and year (if within range)
    if (ano >= 2019 && ano <= 2023) {
        acc[ano][from] = (acc[ano][from] || 0) + 1; // Increment the count for the city
    }
    return acc;
}, {});

// Step 3: Transform the object into an array format
let anoPorCidade = Object.keys(flightsByYearAndFrom).sort().map((ano) => ({
    ano: parseInt(ano, 10),
    "Recife (PE)": flightsByYearAndFrom[ano]["Recife (PE)"] || 0,
    "Florianopolis (SC)": flightsByYearAndFrom[ano]["Florianopolis (SC)"] || 0,
    "Brasilia (DF)": flightsByYearAndFrom[ano]["Brasilia (DF)"] || 0,
    "Aracaju (SE)": flightsByYearAndFrom[ano]["Aracaju (SE)"] || 0,
    "Salvador (BH)": flightsByYearAndFrom[ano]["Salvador (BH)"] || 0,
    "Campo Grande (MT)": flightsByYearAndFrom[ano]["Campo Grande (MS)"] || 0,
    "Sao Paulo (SP)": flightsByYearAndFrom[ano]["Sao Paulo (SP)"] || 0,
    "Natal (RN)": flightsByYearAndFrom[ano]["Natal (RN)"] || 0,
    "Rio de Janeiro (RJ)": flightsByYearAndFrom[ano]["Rio de Janeiro (RJ)"] || 0
}));

console.log(anoPorCidade);

function DestinosSaida(divWidth) {
        return {
            spec: {
                width: divWidth,
                height: 600,
                background: "#FFFFFF",
                projection: {
                    type: "mercator"
                },
                layer: [
                {
                    data: {
                        values: mapa,
                        format: {
                            type: "json",
                            property:"features"
                        }
                    },
                    transform: [
                    {
                        lookup: "properties.sigla",
                        from: {
                            data: {
                                values: voosPorEstado   
                            },
                            key: "sigla",
                            fields: ["count"]
                        }
                    }
                    ],
                    mark: {
                        type: "geoshape",
                        stroke: "#FFFFF",
                        strokeWidth: 1
                    },
                    encoding: {
                        color: {
                            field: "count",
                            type: "quantitative",
                            scale: { scheme: "greens" }
                        }
                    }
                }
            ]
            }
        };
}

function VoosSaida (divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: CidadesSaida
            },
            "mark": {
                "type": "bar"
            },
            "encoding": {
                "x": {
                    "field": "nome",
                    "type": "nominal",
                },
                "y": {
                    "field": "count",
                    "type": "quantitative",
                },
            
            }
        }
    };
}


    function TipoPorDestino(divWidth) {
        return {
            spec: {
                width: divWidth,
                data: {
                    values: tipoPorCidade
                },
                repeat: { "layer": ["economic", "premium", "firstClass"] },
                spec: {
                    "mark": "bar",
                    "encoding": {
                        "x": {
                            "field": "nome",
                            "type": "ordinal",
                            "bandwidth": 10.8 
                        },
                        "y": {
                            "aggregate": "sum",
                            "field": { "repeat": "layer" },
                            "type": "quantitative",
                            "title": "Quantidade de Voos"
                        },
                        "color": { "datum": { "repeat": "layer" }, "title": "Classe", scale: { "range":["#1DB954", "#FF0000", "#8A2BE2"] } },
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

    function VoosPorAnoPorCidade(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: anoPorCidade
            },
            repeat: { "layer": ["Recife (PE)", "Florianopolis (SC)", "Brasilia (DF)", "Aracaju (SE)", "Salvador (BH)", "Campo Grande (MS)", "Sao Paulo (SP)", "Natal (RN)", "Rio de Janeiro (RJ)"] },
            spec: {
                "mark": "line",
                "encoding": {
                    "x": {
                        "field": "ano",
                        "type": "ordinal",
                        "bandwidth": 10.8 
                    },
                    "y": {
                        "aggregate": "sum",
                        "field": { "repeat": "layer" },
                        "type": "quantitative",
                        "title": "Quantidade de Voos"
                    },
                    "color": { "datum": { "repeat": "layer" }, "title": "Agência ", scale: { "range": ["#1DB954", "#FF0000", "#8A2BE2", "#FFA500", "#00CED1", "#FFD700", "#00FF00", "#FF69B4"]
 } },
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
  ```