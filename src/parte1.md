# Parte 1: Quantidade de Voos

<br>
<br>





Em 2020, o mundo presenciou uma gigantesca calamidade pública: em 11 de março deste ano, a OMS caracterizou uma pandemia com foco no vírus que recebeu o nome de COVID-19. Uma análise interessante que será vista a seguir visa constatar se, com a disseminação da pandemia de COVID-19, houve algum tipo de variação na quantidade de voos entre os anos em que o cenário foi de pandemia e observar se tivemos alguma discrepância por conta desse problema. Com isso em mente, temos a seguinte visualização:
<div id="VoosPorAno" class="card">
    <h1>Quantidade de Voos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(VoosPorAno(divWidth - 45)) }
    </div>
</div>

Tendo como ponto de partida o ano de 2019, é possível constatar que houve uma alta significativa na quantidade de voos realizados até o ano de 2020, passando de aproximadamente 40.000 para algo próximo a 120.000 voos, o que é praticamente o triplo de ocorrências de viagens. Entretanto, a partir de 2020, ano em que foi deflagrada a pandemia de COVID-19, essa alta sofreu um ponto de inflexão, com uma queda constante até o ano de 2023, quando houve o controle do vírus causador da pandemia.

Como podemos observar, apesar de ser uma suspeita válida, o ano de 2019 só não possui menos voos que 2023. Existem diversas possibilidades para explicar esse fenômeno. Entretanto, acreditamos que isso se deve a uma particularidade do conjunto de dados apresentado, que não se encaixa com a realidade. Ao observar o conjunto de dados mais atentamente, notamos que os voos de 2019 só possuem dados a partir do mês de setembro. Portanto, vamos comparar a quantidade de voos em cada ano para seu respectivo mês.
<div class="grid grid-cols-2">
    <div id="VoosPorMesAno" class="card grid-colspan-2">
        <h1 class="title">Quantidade de Voos por mês</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorMesAno(divWidth - 200))}
        </div>
    </div>
</div>

Com a visualização deste gráfico, podemos notar que, para este conjunto de dados, apenas a partir do mês de setembro (09) é possível acompanhar a relação da quantidade de voos por mês para o ano de 2019. Notamos que, por sinal, 2019 liderou na quantidade de voos em relação ao mesmo período por mês frente aos demais anos analisados.

Outra informação importante visível no gráfico é que os anos cujos meses tiveram as menores quantidades de voos realizados são justamente o primeiro e o último ano de análise: 2019 e 2023, respectivamente, com 2019 ainda sendo o ano com a menor quantidade de voos realizados, já que a incidência dos mesmos pode ser percebida apenas no último terço do ano.

Em contrapartida, o ano em que houve a maior incidência de voos ao longo de todos os meses foi 2020, seguido por 2021 e 2022. Vale lembrar que, neste caso, o foco é a quantidade de voos por mês do ano.

Ao observarmos os outros meses, notamos que, na maioria das vezes (desconsiderando o ano de 2019), o ano em que observamos a maior quantidade de voos para cada mês é justamente 2020. Para os primeiros meses do ano, como de janeiro até pelo menos março, isso faz sentido, já que a pandemia foi notificada pela OMS em março de 2020. Entretanto, nos meses seguintes, continuamos a notar que o ano de 2020 teve a maior quantidade de voos registrados.

# Quantidade de Voos por classe
Agora, queremos descobrir a distribuição de acomodações de voo (Classe Econômica, Premium ou Primeira Classe) em relação aos voos de cada ano presente no conjunto de dados, para tentar entender melhor que tipo de viagem foi mais requisitada pelos passageiros neste período.

<div class="grid grid-cols-2">
    <div id="TiposDeTarifaPorAno" class="card grid-colspan-2">
        <h1 class="title">Quantidade de Voos em cada categoria</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(TiposDeTarifaPorAno(divWidth - 200))}
        </div>
    </div>
</div>

É notável a predominância dos voos atrelados à Primeira Classe. Em todos os anos, é possível observar que o maior índice de recorrência de voos é atribuído à Primeira Classe, em comparação a qualquer outro tipo de classe. É possível que o público-alvo das agências de voo presentes no conjunto de dados seja de uma classe econômica mais elevada.

<div class="grid grid-cols-2">
    <div id="EconoPremium" class="card grid-colspan-2">
        <h1 class="title">Voos Primeira Classe x Outros</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(EconoPremium(divWidth - 200))}
        </div>
    </div>
</div>

Ao agrupar os voos de Classe Econômica e Premium e compará-los com a quantidade de voos na Primeira Classe, conseguimos finalmente notar uma predominância das outras classes. Optamos por agrupar porque, na realidade, a disparidade de preço e de público entre a Premium e a Primeira Classe é bem maior do que entre a Classe Econômica e Premium. Portanto, agora podemos observar uma distribuição de dados mais compatível com a realidade do mercado aéreo.

# Voos por Agencia 
Agora, queremos entender melhor o perfil de cada agência de viagens. Vamos analisar a quantidade de passagens aéreas vendidas por cada uma ao longo dos anos presentes no conjunto de dados.

<div class="grid grid-cols-2">
    <div id="VoosPorAgencia" class="card grid-colspan-2">
        <h1 class="title">Quantidade de Voos por agência</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorAgencia(divWidth - 200))}
        </div>
    </div>
</div>

Podemos notar uma grande disparidade entre as agências CloudFly, Rainbow, e FlyingDrops. Com a finalidade de entender melhor o porquê disso, decidimos verificar a quantidade de tarifas que cada agência vendeu nesse mesmo período.

<div id="QuantidadePorTipo" class="card">
    <h1>Quantidade de Voos por tipo por agência</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(QuantidadePorTipo(divWidth - 45)) }
    </div>
</div>
Agora, com esta visualização, é possível entender o motivo da grande disparidade na quantidade de voos vendidos. Como a agência FlyingDrops vendeu apenas assentos de primeira classe durante todo o período, é natural que a quantidade de passagens vendidas seja inferior em comparação às outras duas agências. Isso sugere que essa agência possivelmente se dirige a um público com um poder aquisitivo mais elevado em relação às outras. Vamos analisar se isso afetou o faturamento da agência mais tarde, na parte 2.



<div class="grid grid-cols-2">
    <div id="VoosPorAnoPorAgencia" class="card grid-colspan-2">
        <h1 class="title">Quantidade de Voos por agência por ano</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorAnoPorAgencia(divWidth - 200))}
        </div>
    </div>
</div>
Com esta última visualização, observamos que a tendência na quantidade total de voos vendidos por ano pelas agências seguiu um padrão muito similar ao da primeira visualização apresentada no início desta análise.



# Desings utilizados.

Nesta análise, utilizamos quatro tipos de gráficos distintos: o gráfico de barras, o gráfico de barras compactadas, o gráfico de linhas e o gráfico de linhas compactadas.

Optamos pelo gráfico de barras compactadas para ilustrar a comparação entre a quantidade de voos para cada mês de cada ano, a quantidade de cada tipo de passagem (econômica, premium, primeira classe) em cada ano, a comparação entre a agregação das passagens econômica e premium versus primeira classe a cada ano, e, por fim, a quantidade de voos de cada classe que cada agência vendeu. O objetivo foi evidenciar as diferenças entre as variáveis apresentadas. Para os canais visuais, cada cor no gráfico representa um tipo de passagem entre as três disponíveis. No gráfico dos meses, cada cor representa um ano diferente. Já os marcadores, a altura das barras, representam a quantidade de cada uma das variáveis propostas. Em geral, o eixo y continha a quantidade, ou seja, a altura da barra vertical indicava a quantidade de cada variável, e o eixo x representava os anos do conjunto de dados em dois gráficos e as agências em um deles.

Para o gráfico de barras comum, o intuito é similar ao do gráfico de barras compactadas, porém, desta vez, temos apenas uma variável. Para os marcadores, foram utilizadas barras horizontais para cada agência e, como citado anteriormente, a altura representa a quantidade de voos vendidos por cada agência.

O gráfico compactado de linhas foi utilizado para mostrar a tendência da quantidade de passagens vendidas por cada agência ao longo dos anos. Para os marcadores, usamos linhas que mostram a tendência da quantidade de passagens vendidas ao longo do tempo, e cada linha representa uma agência diferente. Nos canais visuais, cada cor representa uma agência diferente, facilitando assim a visualização de cada uma.

O gráfico de linhas foi utilizado para mostrar a tendência da quantidade de voos ao longo do período presente no conjunto de dados. O marcador é uma linha que representa o eixo y do gráfico, onde temos a quantidade de voos ao longo dos anos presentes no eixo x.





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

let flightEconoPremiumEFirst = Object.values(flightTypeCountsByYear).map(item => {
    return {
        year: item.year,
        econoPremium: item.economic + item.premium,
        firstClass: item.firstClass
    };
})

console.log(flightEconoPremiumEFirst)


let agencyFlightCounts = {};

dataSet.forEach(voo => {
    let agencyName = voo.agency; // Assuming the dataset has an 'agency' field

    if (!agencyFlightCounts[agencyName]) {
        agencyFlightCounts[agencyName] = { agency: agencyName, flightCount: 0 };
    }

    agencyFlightCounts[agencyName].flightCount += 1;
});

// Convert the object to an array if needed
let agencyFlightCountsArray = Object.values(agencyFlightCounts).map(item => {
    return {
        agency: item.agency,
        flightCount: item.flightCount
    };
});
let agencyYearFlightCounts = {};

dataSet.forEach(voo => {
    let agencyName = voo.agency; // Assuming the dataset has an 'agency' field
    let flightYear = new Date(voo.date).getFullYear(); // Assuming the dataset has a 'date' field

    if (!agencyYearFlightCounts[flightYear]) {
        agencyYearFlightCounts[flightYear] = { year: flightYear };
    }

    if (!agencyYearFlightCounts[flightYear][agencyName]) {
        agencyYearFlightCounts[flightYear][agencyName] = 0;
    }

    agencyYearFlightCounts[flightYear][agencyName] += 1;
});

// Convert the object to an array if needed
let agencyYearFlightCountsArray = Object.values(agencyYearFlightCounts);

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


console.log(flightTypeCountsByYearArray)



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

 function EconoPremium(divWidth) {
        return {
            spec: {
                width: divWidth,
                data: {
                    values: flightEconoPremiumEFirst
                },
                repeat: { "layer": ["econoPremium", "firstClass"] },
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
                    "color": { "datum": { "repeat": "layer" }, "title": "Ano", scale: { "range":["#1DB954", "#FF0000", "#8A2BE2", "#3a68bc", "#FFA500"] } },
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

function VoosPorAgencia(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: agencyFlightCountsArray
            },
            "mark": {
                "type": "bar"
            },
            "encoding": {
                "x": {
                    "field": "agency",
                    "type": "nominal",
                },
                "y": {
                    "field": "flightCount",
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
                    "color": { "datum": { "repeat": "layer" }, "title": "Classe", scale: { "range":["#1DB954", "#FF0000", "#8A2BE2", "#3a68bc", "#FFA500"] } },
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



function VoosPorAnoPorAgencia(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: agencyYearFlightCountsArray
            },
            repeat: { "layer": ["CloudFy", "FlyingDrops", "Rainbow"] },
            spec: {
                "mark": "line",
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
                    "color": { "datum": { "repeat": "layer" }, "title": "Agência ", scale: { "range":["#1DB954", "#FF0000", "#8A2BE2"] } },
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
