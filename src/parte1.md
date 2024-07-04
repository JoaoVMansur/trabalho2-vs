# Parte 1: Quantidade de Vôos

<br>
<br>

Neste trabalho iremos demonstrar o resultado de uma investigação acerca de algumas tendências que podem ser observadas por meio da análise do conjunto de dados apresentado atenriormente.

Em uma primeira análise, podemos observar que possuímos acesso a dados que estão na faixa de tempo entre os anos de 2019 a 2023. 

Em 2020 o mundo presenciou uma gigantesca calamidade pública: em 11 de março deste mesmo ano, a OMS caracterizou uma pandemia com foco no vírus que recebeu o nome de COVID-19.
Uma análise interessante que será vista a seguir é aquela que visa constatar se com a disseminação da pandemia do COVID-19 houve algum tipo de variação na quantidade de vôos entre os anos em que o cenário foi de pandemia e observar se tivemos alguma discrepância por conta desse problema. Com isso em mente temos a seguinte visualização:

<div id="VoosPorAno" class="card">
    <h1>Quantidade de vôos por ano</h1>
    <div style="width: 100%; margin-top: 15px;">
        ${ vl.render(VoosPorAno(divWidth - 45)) }
    </div>
</div>

Tendo como ponto de partida o ano de 2019 é possível constatar que houve uma alta significativa na quantidade de vôos realizados até o ano de 2020, passando de aproximadamente 40.000 para algo próximo a 120.000 vôos, que é praticamente o triplo de ocorrências de viagens. Entretanto, à partir de 2020, ano em que foi deflagrada a pandemia do COVID-19, essa alta sofreu um ponto de inflexão que seguiu tendo uma queda constante até o ano de 2023, ano em que houve o controle do vírus causador da pandemia. 

Como podemos observar, apesar de ser uma suspeita válida, o ano de 2019 só não possui menos vôos que 2023. Existe diversas possibilidades para explicar esse fenômeno, entretanto acreditamos que isso se deva a uma particularidade do conjunto de dados apresentados que não se encaixa com a realidade pois ao observar o conjunto de dados mais atentamente notamos que os vôos de 2019 só possuem dados à partir do mês de setembro, portanto vamos comparar a quantidade de vôos em cada ano para seu respectivo mês.

<div class="grid grid-cols-2">
    <div id="VoosPorMesAno" class="card grid-colspan-2">
        <h1 class="title">Quantidade de vôos por mês</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorMesAno(divWidth - 200))}
        </div>
    </div>
</div>

Com a visualização deste gráfico podemos notar que pelo menos para este conjunto de dados, apenas à partid do mês de setembro (09) é que é possível acompanhar a relação da quantidade de vôos por mês para o ano de 2019, que por sinal liderou na quantidade em relação ao mesmo período por mês frente aos demais anos analisados.

Outra informação importante que é possível ser vista no gráfico é que os anos cujos meses tiveram as menores quantidades de vôos realizados são justamente o primeiro e último ano de análise: 2019 e 2023 respectivamente, tendo 2019 ainda como o ano com menor quantidade de vôos realizados, já que a incidência dos mesmos pode ser percebida apenas no último terço do ano.

Em contrapartida, o ano em que houve a maior incidência de vôos ao longo de todos os meses foi o ano de 2020, seguido por 2021 e 2022. Lembrando que neste caso o foco é com relação a quantidade de vôos por meses do ano.

Porém, ao observarmos os outros meses notamos que em sua maiora (desconsiderando o ano de 2019) o ano cujo qual observamos a maior quantidade de vôos para cada mês é justamento 2020. Para os primeiros meses do ano, como de janeiro até pelo menos março, faz um pouco de sentido já que a pandemia foi notificada pela OMS em março de 2020. Entretanto, nos meses seguintes continuamos a notar que o ano de 2020 teve a maior quantidade de vôos registrados.

# Quantidade de Vôos por classe
Agora queremos descobrir a distribuição de acomodações de vôo (Classe Econômica, Premium ou Primeira Classe) em realação aos vôos de cada ano presente no conjunto de dados, para tentar entender melhor que tipo de viagem foi mais requisitada neste período por parte dos passageiros.

<div class="grid grid-cols-2">
    <div id="TiposDeTarifaPorAno" class="card grid-colspan-2">
        <h1 class="title">Quantidade de vôos em cada categoria</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(TiposDeTarifaPorAno(divWidth - 200))}
        </div>
    </div>
</div>

<<<<<<< HEAD:src/questao1.md
É notável uma predominância dos vôos atrelados a Primeira Classe em todos os anos analizados, seguido por um empate técnico entre as outras classes ao longo do mesmo período de tempo, tendo 2020 como o ano com maiores taxas das 3 categorias. 
=======
É notável uma predominância dos vôos atrelados a Primeira Classe. Em todos os anos é possível observar o maior índice de recorrência de vôos sendo atribuído aqueles de Primeira Classe em comparação a qualquer outro tipo de classe é possivel que o  publico alvo das agências de vôo presentes no conjunto de dados seja de uma classe econômica mais elevada. 


<div class="grid grid-cols-2">
    <div id="EconoPremium" class="card grid-colspan-2">
        <h2 class="title">Voos Primeira Classe x Outros</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(EconoPremium(divWidth - 200))}
        </div>
    </div>
</div>

Ao agrupar os voos de classe econômica e premium e compará-los com a quantidade de voos na Primeira Classe, conseguimos finalmente notar uma predominância das outras classes. Optamos por agrupar porque, na realidade, a disparidade de preço e de público entre a premium e a primeira classe é bem maior do que entre a classe econômica e premium. Portanto, agora podemos observar uma distribuição de dados mais compatível com a realidade do mercado aéreo.

Com o objetivo de aprofundar nossa compreensão sobre o público-alvo de cada agência de viagem, decidimos também analisar como cada agência distribuiu a venda de voos por classe. Essa análise não apenas nos permite entender melhor os padrões de consumo dos clientes de cada agência, mas também oferece insights valiosos sobre as preferências de viagem, o perfil socioeconômico dos passageiros e até mesmo estratégias de marketing que podem ser mais eficazes para cada segmento de mercado. Ao examinar detalhadamente esses dados, buscamos não apenas quantificar as vendas por classe, mas também contextualizar essas informações dentro do panorama competitivo do setor aéreo, ajudando a orientar decisões estratégicas futuras das agências de viagem.
>>>>>>> 6fcee9da42c07f9db66afc0ab2f0dfb08e69d748:src/parte1.md

<div class="grid grid-cols-2">
    <div id="VoosPorAgencia" class="card grid-colspan-2">
        <h1 class="title">Quantidade de vôos por agência</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorAgencia(divWidth - 200))}
        </div>
    </div>
</div>

<<<<<<< HEAD:src/questao1.md
Neste ponto da visualização é possível notar qual agência possui o maior indice de incidência em relação a emissão de passagens aéreas. 

Temos um aparente impate técnico entre as empresas CloudFly e Rainbow, e aquela com menor taxa de incidências de vôo foi a Flying Drops.

=======
Apartir dessa vizualizacao podemos          
>>>>>>> 6fcee9da42c07f9db66afc0ab2f0dfb08e69d748:src/parte1.md


<div class="grid grid-cols-2">
    <div id="VoosPorAnoPorAgencia" class="card grid-colspan-2">
        <h1 class="title">Quantidade de vôos por agência por ano</h1>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(VoosPorAnoPorAgencia(divWidth - 200))}
        </div>
    </div>
</div>

<<<<<<< HEAD:src/questao1.md
Com o auxílio do gráfico é possível visualizar com mais clareza que a quantidade de vôos por agência tem valores muito próximos entre as agências CloudFy e Rainbow, a única diferença é que a contagem da quantidade de vôos da CloudFy começa a ser verificada um pouco antes de 2019 e a contagem relativa a Rainbow começa a ser verificada por volta do fim do primeiro terço de 2019. A diferença é basicamente temporal em relação ao início de verificação dos dados.

Já a agência FlyingDrops tem uma verificação da quantidade de vôos por ano mais tímida em comparação com as citadas anteriormente.
=======
Com os gráficos acima, há clara diferença entre os perfis das agências aereas. As agencias 'cloudfly'  e 'rainbow' possuem publico alvo similares, enquanto que 'flyingdrops' tem cenário distinto. Como 'flyingdrops' possui apenas voos de firstclass, que são muito mais caros, apenas uma parcela da população possui condições de utiliza-lá, portanto, isso justifica a quantidade de voos muito menor em relação às outras duas agencias presentes no dataset. Por outro lado, as agências "cloudfly" e "rainbow" possuem quantidade de voos, praticamente, iguais e disponibilizam todos os tipos de classes para seus clientes, desde a mais barata até a mais cara, o que justifica terem uma quantidade de voos muito superior a 'flyingdrops', pois oferecem voos acessiveis aos mais diferentes niveis de poder aquisitivo da população 
>>>>>>> 6fcee9da42c07f9db66afc0ab2f0dfb08e69d748:src/parte1.md

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

```
