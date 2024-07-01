# Parte 3 : Destinos dos Voos
 
  <br>
  <br>
  <br>

# Desings utilizados

Nesta pergunta, empregamos dois tipos de gráficos: o gráfico de barras compactado e o gráfico de pizza

 Para a primeira análise, optamos pelo gráfico de pizza, pois nosso objetivo era ilustrar as partes de um todo, evidenciando a importância de cada plataforma de streaming representada. Quando buscamos representar partes de um todo, o gráfico de pizza é a escolha mais apropriada.
 Para os canais visuais, o gráfico de pizza apresenta um círculo dividido em fatias, cada uma representando a proporção de uma plataforma de streaming. Já os marcadores consistem em três cores distintas, cada uma correspondendo a uma plataforma de streaming específica. Essas cores foram selecionadas com base nas paletas de cores das respectivas logos de cada plataforma.


Para a segunda análise, utilizamos dois tipos de gráficos: o gráfico de barras compactadas horizontais e o gráfico de pizza, novamente. Optamos pelo gráfico de barras compactadas horizontais para comparar as posições de cada música nos charts de cada plataforma de forma clara e direta, permitindo visualizar as diferenças entre os charts das plataformas. O gráfico de pizza foi novamente empregado, desta vez para demonstrar a participação de cada plataforma em relação aos valores nulos presentes no conjunto de dados sobre a posição nos charts das plataformas. Para os marcadores, cada música e sua posição no chart das plataformas foram representadas por barras verticais, sendo que cada plataforma possui sua própria barra vertical específica. Quanto aos canais visuais, as barras verticais de cada plataforma possuem cores diferentes, escolhidas como na análise anterior, de acordo com a paleta de cores da plataforma. O gráfico de barras segue o mesmo conceito descrito anteriormente



<div style="width: 100%;  height: 500px; margin-top: 15px;">
    <h2 class="title">EX04</h2>
    <div id="ex04" style="width: 100%; height: 430px;  margin-top: 15px;">
    </div>
</div>


<div class="grid grid-cols-2">
    <div id="ex01" class="card grid-colspan-2">
        <h2 class="title">Quantidade de Voos por agencia</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${vl.render(ex01(divWidth - 200))}
        </div>
    </div>
</div>











```js

import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";
import maplibregl from "maplibre-gl";

const vl = vegaLiteApi.register(vega, vegaLite);

const dataSet = await FileAttachment("./data/flights.csv").csv({ typed: true });
const divWidth = Generators.width(document.querySelector("#ex01"));
const data  = await FileAttachment("./data/voosCidade.csv").csv({ typed: true });
const mapa = await FileAttachment("./data/mapa.json").json({typed: true});


const cityFlightCounts = dataSet.reduce((acc, flight) => {
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

console.log(cityFlightCounts)


function ex01(divWidth) {
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
                                values: data   
                            },
                            key: "sigla",
                            fields: ["count"]
                        }
                    }
                    ],
                    mark: {
                        type: "geoshape",
                        stroke: "#BFBFBF",
                        strokeWidth: 1
                    },
                    encoding: {
                        color: {
                            field: "count",
                            type: "quantitative",
                            scale: { scheme: "blues" }
                        }
                    }
                }
            ]
            }
        };
}

// function ex04() {
//     const map02 = document.querySelector("#ex04");
//     const divWidth04 = Generators.width(map02);
//     map02.style.width = `${divWidth04}px`;
//     map02.style.height = '400px';

//     const map = new maplibregl.Map({
//         container: map02,
//         style: "https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json",
//         center: [-51.9253, -14.2350],
//         zoom: 4,
//     });

//     map.on('load', async () => {
//         // Load Brazil geoJSON data
//         const brazilGeoJSON = await FileAttachment("./data/brazil_geo.json").json();

//         // Add Brazil geoJSON as a source
//         map.addSource('brazil', {
//             'type': 'geojson',
//             'data': brazilGeoJSON
//         });

//         // Add layer for Brazil boundaries
//         map.addLayer({
//             'id': 'brazil-boundaries',
//             'type': 'line',
//             'source': 'brazil',
//             'layout': {},
//             'paint': {
//                 'line-color': '#888',
//                 'line-width': 1
//             }
//         });

//         // Add layer for flights heatmap
//         map.addSource('flights', {
//             'type': 'geojson',
//             'data': flightGeoJSON
//         });

//         map.addLayer({
//             'id': 'flights-heatmap',
//             'type': 'heatmap',
//             'source': 'flights',
//             'maxzoom': 9,
//             'paint': {
//                 'heatmap-weight': [
//                     'interpolate',
//                     ['linear'],
//                     ['get', 'count'],
//                     0,
//                     0,
//                     60000,
//                     1
//                 ],
//                 'heatmap-intensity': [
//                     'interpolate',
//                     ['linear'],
//                     ['zoom'],
//                     0,
//                     1,
//                     9,
//                     3
//                 ],
//                 'heatmap-color': [
//                     'interpolate',
//                     ['linear'],
//                     ['heatmap-density'],
//                     0,
//                     'rgba(33,102,172,0)',
//                     0.2,
//                     'rgb(103,169,207)',
//                     0.4,
//                     'rgb(209,229,240)',
//                     0.6,
//                     'rgb(253,219,199)',
//                     0.8,
//                     'rgb(239,138,98)',
//                     1,
//                     'rgb(178,24,43)'
//                 ],
//                 'heatmap-radius': [
//                     'interpolate',
//                     ['linear'],
//                     ['zoom'],
//                     0,
//                     2,
//                     9,
//                     20
//                 ],
//                 'heatmap-opacity': [
//                     'interpolate',
//                     ['linear'],
//                     ['zoom'],
//                     7,
//                     1,
//                     9,
//                     0
//                 ]
//             }
//         });
//     });

//     map.on('idle', () => {
//         map.resize();
//     });

//     map.on('error', (event) => {
//         console.error('Map error:', event.error);
//     });

//     return map;
// }

// ex04();




  ```