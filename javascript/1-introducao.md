# Introdução ao JavaScript e a Biblioteca Leaflet

## Por que JavaScript importa para mapas

* JavaScript (JS) é a linguagem que roda no navegador e permite interagir com a página: capturar eventos, manipular HTML/CSS, trabalhar com APIs, etc.

* Quando usamos Leaflet, estamos usando JS para: criar o mapa, adicionar camadas, responder a cliques/arrastos, manipular coordenadas geográficas.

* Portanto, antes de mergulhar nos mapas, precisamos dominar alguns fundamentos de JS: variáveis, tipos, funções, objetos, arrays, eventos.

## Instalação mínima do Leaflet

* No HTML você inclui (geralmente) o CSS e o JS do Leaflet (por exemplo via CDN) e cria um `<div id="map">` para o mapa.

* Em JS:

```html
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
     integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY="
     crossorigin=""/>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
     integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo="
     crossorigin=""></script>
```


```html
<div id="map" style="height: 400px;"></div>

<script>
  const map = L.map('map').setView([0,0], 2);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(map);
</script>

```

## Neste material, você irá aprender

* Conceitos de JS básicos: variáveis, tipos, operadores, funções, objetos, arrays.

* Manipulação do DOM (Document Object Model) e eventos — útil para interagir com mapas.

* Trabalhar com coordenadas geográficas, camadas do mapa, eventos de mapa (usando Leaflet).

* Um pequeno fluxo de projeto integrado JS + Leaflet.


## Variáveis, tipos de dados e operadores

### Variáveis
* Em JS, usamos `let`, `const` ou `var` (embora `let` e `const` sejam recomendados hoje).


```js
const city = 'João Pessoa';
let zoomLevel = 13;
```

* const para valor que não muda, let para valor que pode mudar.


### Tipos de dados

* string, number, boolean, null, undefined, object, symbol, bigint.

```js
const lat = -7.1153;
const hasMap = true;
let userName = null;
let userZoom; // undefined
```

### Operadores

* Aritméticos (`+`, `-`, `*`, `/`, `%`), comparação (`===`, `!==`, `<`, `>`), lógicos (`&&`, `||`, `!`).

* Exemplo com Leaflet:

```js
if (zoomLevel > 10 && hasMap) {
  map.setZoom(zoomLevel);
}
```

*** Aplicação no Leaflet

* Use variáveis para definir centro, zoom, camadas:

```js
const center = [-7.1153, -34.861];  // João Pessoa
const zoom = 12;
const map = L.map('map').setView(center, zoom);
```

* Tipos de dados: o centro é um array de dois números (number[]), zoom é um number.

* Operadores podem decidir se você muda o zoom ou não etc.

## Funções, objetos e arrays

### Funções

* Funções permitem agrupar lógica reutilizável:

```js
function initializeMap(center, zoom) {
  return L.map('map').setView(center, zoom);
}
const map = initializeMap(center, zoom);
```

* Também podemos usar *arrow functions*:

```js
const initializeMap = (center, zoom) => L.map('map').setView(center, zoom);

const map = initializeMap(center, zoom);
```

### Objetos

* Objetos são coleções de pares chave-valor:

```js
const layerOptions = {
  attribution: '© OpenStreetMap contributors',
  maxZoom: 19
};
L.tileLayer(tileUrl, layerOptions).addTo(map);
```

### Arrays

* Arrays são listas ordenadas:

```js
const cities = [
  { name: "João Pessoa", coords: [-7.1153, -34.861] },
  { name: "Recife", coords: [-8.0476, -34.8770] }
];
```

* Você pode iterar e adicionar marcadores:

```js
cities.forEach(city => {
  L.marker(city.coords).addTo(map).bindPopup(city.name);
});

```	

### Aplicação no Leaflet

* Função para adicionar marcador genérico:

```js
function addCityMarker(city) {
  L.marker(city.coords)
    .addTo(map)
    .bindPopup(city.name);
}
cities.forEach(addCityMarker);
```
* Objeto para opções de mapa, camada, marcador.

* Array para lista de locais/geometrias para representar no mapa.


## Manipulação do DOM e eventos básicos

### DOM (Document Object Model)

* Em JS você pode acessar/manipular elementos HTML:

```js
const btn = document.getElementById('btnZoomIn');
btn.addEventListener('click', () => {
  map.zoomIn();
});

```

* Isso permite que controles HTML interajam com o mapa.


### Eventos

* Eventos JS comuns: `click`, `change`, `keyup, etc.

* No Leaflet, o mapa e os marcadores também emitem eventos. Exemplo:

```js
map.on('click', (e) => {
  console.log("Você clicou em", e.latlng);
  L.popup()
    .setLatLng(e.latlng)
    .setContent("Você clicou no ponto: " + e.latlng.toString())
    .openOn(map);
});
```

* Veja que usamos e.latlng para obter coordenadas do clique.

### Aplicação ao mapa

* Você pode criar botões HTML para controlar zoom, mudar camada, ligar/desligar marcador, etc.

* Exemplo: ao clicar no mapa, adiciona um marcador:

```js
map.on('click', function(e) {
  L.marker(e.latlng).addTo(map)
    .bindPopup("Marcador em " + e.latlng.toString())
    .openPopup();
});
```

* Isso traz a lógica JS + interação com o mapa via Leaflet.

## Métodos úteis e cadeia de chamadas (“method chaining”)

### Métodos e cadeias

* Em JS (como em Leaflet) muitos métodos retornam o próprio objeto para permitir chamadas encadeadas:

```js 
L.marker([lat, lng])
  .addTo(map)
  .bindPopup("Texto")
  .openPopup();
```

* No Leaflet, o objeto mapa (map) tem métodos como `setView`, `flyTo`, `panTo`, `addLayer`, etc.


### Exemplos de métodos do mapa


* `map.setView([lat, lng], zoom);`

* `map.flyTo([lat, lng], zoom, options);`

* `map.addLayer(layer)`; ou `layer.addTo(map);`

* `map.removeLayer(layer);`


### Aplicação no Leaflet e JS

* Suponha que você tenha um botão que chama flyTo para uma coordenada pré-definida:

```js
document.getElementById('btnGoJP').addEventListener('click', () => {
  map.flyTo([-7.1153, -34.861], 14, { duration: 2 });
});
```

* Método `flyTo cria animação suave para o ponto desejado.

* Isto mostra como métodos JS e API do Leaflet se combinam.


## Trabalhando com camadas, marcadores e popups

### Camadas (Layers)

* Em Leaflet, uma “camada” pode ser um tileLayer, um marcador, um polígono, um grupo de camadas.

* Você adiciona a camada ao mapa com .addTo(map) ou map.addLayer(layer).

* Tile layer exemplo:

```js
const tiles = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', { attribution: ... });
tiles.addTo(map);
```

### Marcadores e Popups

* Marcador: `L.marker([lat, lng], options?)`.
* Popup: `.bindPopup("Texto aqui")` ligado ao marcador ou diretamente ao mapa.

Exemplo:

```js
const marker = L.marker([-7.1153, -34.861])
  .addTo(map)
  .bindPopup("João Pessoa")
  .openPopup();
```
