# Parte 1: Quantidade de Voos

<br>
<br>
Neste trabalho vamos investigar as tendencias que podemos observar por meio da analise do conjunto de dados apresentado

Em uma primeira analise, podemos observar temos dados de 2019 ate 2023. Com a pandemia do covid-19 queremos saber a variacao na quantidade de voos entre os anos e observar se tivemos uma disparidade por conta desse problema. Com isso em mente temos a seguinte visualizacao:


<div id="VoosPorAno" class="card">
    <h1>Quantidade de voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(VoosPorAno(divWidth - 45)) }
    </div>
</div>
Como podemos observar, apesar de ser uma suposição valida, o ano de 2019 so não possui menos voos que 2023. Existem diversas possibilidades para explicar esse fenomeno, porem acreditamos que isso seja uma particularidade do conjunto de dados apresentados que não se encaixa com a realidade pois ao observar o conjunto de dados mais atentamente notamos que os voos de 2019 so possuem dados apartir do mes de setembro, portanto vamos comprar a quantidade de voos em cada ano para seu respectivo mes.

<div class="grid grid-cols-2">
    <div id="VoosPorMesAno" class="card grid-colspan-2">
        <h2 class="title">Posição no Chart de Cada Plataforma</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorMesAno(divWidth - 200))}
        </div>
    </div>
</div>

Com esse  vizualização agora podemos ver que pelo menos para os meses os quais 2019 tem voos foi ele que obteve a maior quantidade de voos. Porem ao observarmos os meses outros meses vemos que em sua maiora(desconsiderando 2019) o ano o qual temos a maior quantidade de voos para cada mes e o ano de  2020. Para os primeiros meses do ano como de janeiro ate pelo menos marco ate que faz sentido pois a pandemia comecou por volta de abril/maio mas os meses seguintes continuamos a observar que o ano de 2020 teve a maior quantidade de voos.

# Quantidade de Voos por classe
Agora queremos saber a distribuicao de tipo de voo(economica, primium ou primeira classe) em realcao aos voos de cada ano presente no conjunto de dados.

<div class="grid grid-cols-2">
    <div id="TiposDeTarifaPorAno" class="card grid-colspan-2">
        <h2 class="title">Quantidade de Voos em cada categoria</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(TiposDeTarifaPorAno(divWidth - 200))}
        </div>
    </div>
</div>

Uma dominancia dos voos de primeira classe foi encotntrada, em todos os anos tivemos mais voos de primeira classe do que de outros meios separados,

```js 
const divWidth = Generators.width(document.querySelector("#VoosPorAno"));
import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";

const vl = vegaLiteApi.register(vega, vegaLite);

const dataSet = await FileAttachment("./data/flights.csv").csv({typed: true});

dataSet.forEach((voo) => {
    let dateParts = voo.date.split('/');
    voo.ano = dateParts[2];
});

let flightCounts = dataSet.reduce((acc, voo) => {
    let ano = voo.ano;
    if (!acc[ano]) {
        acc[ano] = { ano: ano, quantidade: 0 };
    }
    acc[ano].quantidade += 1;
    return acc;
}, {});

let flightCountsPerYearArray = Object.values(flightCounts);

let flightCountsPerYearMonthArray = [];

flightCountsPerYearArray.forEach(yearData => {
    let year = yearData.ano;
    
    // Create an object to store counts per month for the current year
    let countsPerMonth = {};
    
    // Filter dataSet for flights in the current year
    dataSet.filter(voo => voo.ano === year)
        .forEach(voo => {
            let dateParts = voo.date.split('/');
            let month = dateParts[0];
            
            // Initialize count for the month if it doesn't exist
            if (!countsPerMonth[month]) {
                countsPerMonth[month] = {
                    year: year,
                    month: month,
                    quantidade: 0
                };
            }
            
            // Increment count for the month
            countsPerMonth[month].quantidade += 1;
        });
    
    // Convert countsPerMonth object to an array and add to flightCountsPerYearMonthArray
    flightCountsPerYearMonthArray.push(...Object.values(countsPerMonth));
});
flightCountsPerYearMonthArray.sort((a, b) => {
    // Compare years first
    if (a.year !== b.year) {
        return a.year - b.year;
    }
    
    // If years are the same, compare months
    let monthA = parseInt(a.month);
    let monthB = parseInt(b.month);
    
    return monthA - monthB;
});
let MesesAgregadosArray = flightCountsPerYearMonthArray.reduce((acc, voo) => {
    let month = voo.month;
    let year = voo.year;
    let quantidade = voo.quantidade;
    
    // Find the existing month object or create a new one
    let existingMonth = acc.find(item => item.mes === month);
    if (!existingMonth) {
        existingMonth = {
            mes: month,
            2019: 0,
            2020: 0,
            2021: 0,
            2022: 0,
            2023: 0
        };
        acc.push(existingMonth);
    }
    
    // Add the quantidade to the respective year in the existing month object
    existingMonth[year] += quantidade;
    
    return acc;
}, []);

console.log(MesesAgregadosArray);



let flightTypeCountsByYear = {};

dataSet.forEach(voo => {
    let dateParts = voo.date.split('/');
    let year = dateParts[2];
    let flightType = voo.flightType;

    if (!flightTypeCountsByYear[year]) {
        flightTypeCountsByYear[year] = { year: year, economic: 0, premium: 0, firstClass: 0 };
    }

    switch (flightType) {
        case 'economic':
            flightTypeCountsByYear[year].economic += 1;
            break;
        case 'premium':
            flightTypeCountsByYear[year].premium += 1;
            break;
        case 'firstClass':
            flightTypeCountsByYear[year].firstClass += 1;
            break;
        default:
            break;
    }
});

let flightTypeCountsByYearArray = Object.values(flightTypeCountsByYear).map(item => {
    return {
        year: item.year,
        economic: item.economic,
        premium: item.premium,
        firstClass: item.firstClass
    };
});

console.log(flightTypeCountsByYearArray);


```





```js


function VoosPorAno (divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: flightCountsPerYearArray
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
                    "field": "quantidade",
                    "type": "quantitative",
                },
            
            }
        }
    };
}
    function TiposDeTarifaPorAno(divWidth) {
        return {
            spec: {
                width: divWidth,
                data: {
                    values: flightTypeCountsByYearArray
                },
                repeat: { "layer": ["economic", "premium", "firstClass"] },
                spec: {
                    "mark": "bar",
                    "encoding": {
                        "x": {
                            "field": "year",
                            "type": "ordinal",
                            "bandwidth": 10.8 
                        },
                        "y": {
                            "aggregate": "sum",
                            "field": { "repeat": "layer" },
                            "type": "quantitative",
                            "title": "Quantidade de Voos"
                        },
                        "color": { "datum": { "repeat": "layer" }, "title": "Streaming Chart", scale: { "range":["#1DB954", "#FF0000", "#8A2BE2"] } },
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


function VoosPorMesAno(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: MesesAgregadosArray
            },
            repeat: { "layer": ["2019", "2020", "2021", "2022","2023"] },
            spec: {
                "mark": "bar",
                "encoding": {
                    "x": {
                        "field": "mes",
                        "type": "ordinal",
                        "bandwidth": 10.8 
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

```