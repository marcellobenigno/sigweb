# HTML5 & CSS3 para WebGIS: Do Zero ao Visualizador de Mapas

> **Público-alvo:** Alunos do Curso Superior de Tecnologia em Geoprocessamento (IFPB) || Iniciantes em WebGIS
> **Pré-requisito:** Nenhum. Apenas familiaridade com computador e navegador.
> **Projeto Fio-Condutor:** Ao longo do curso, você construirá um **Visualizador de Mapas Estático** — uma página web completa com mapa, legenda, tabela de atributos e formulário de consulta.

---

## Módulo 1 — Introdução ao HTML e à Web

### 1.1 Aprofundamento Teórico

#### O que é HTML?

HTML (*HyperText Markup Language*) é a linguagem de marcação padrão para criação de documentos na Web. "Marcação" significa que você envolve conteúdo com **tags** — etiquetas que dizem ao navegador *o que é* cada pedaço de informação, não *como ele parece* (isso é papel do CSS).

```
Conteúdo bruto: "Mapa da Bacia do Rio São Francisco"
Com marcação:  <h1>Mapa da Bacia do Rio São Francisco</h1>
```

O navegador lê esse texto marcado e constrói uma árvore de objetos chamada **DOM** (*Document Object Model*). Cada tag vira um nó dessa árvore. Ferramentas WebGIS como Leaflet.js e OpenLayers manipulam esse DOM para inserir e atualizar camadas de mapa dinamicamente.

#### A Tríade da Web

| Camada | Tecnologia | Analogia GIS |
|--------|-----------|--------------|
| Estrutura | HTML5 | Modelo de dados (atributos de feições) |
| Apresentação | CSS3 | Simbologia e cartografia temática |
| Comportamento | JavaScript | Geoprocessamento e interatividade |

> **Nota de Acessibilidade (WCAG 2.1):** Um HTML bem estruturado é o primeiro pilar da acessibilidade. Leitores de tela navegam pela hierarquia de tags para descrever o conteúdo a usuários com deficiência visual — o mesmo raciocínio de uma boa legenda cartográfica.

---

#### Ferramentas Essenciais

**Editor de Código — Sublime Text**
- Plugin recomendado: **HTML-CSS-JS Prettify** (formatação automática via `Ctrl+Shift+H`)
- Plugin recomendado: **LiveReload** (recarrega o navegador automaticamente ao salvar)
- Plugin recomendado: **SublimeLinter + SublimeLinter-html-tidy** (valida o HTML em tempo real, sublinhando erros)
- Plugin recomendado: **A File Icon** (deixa os ícones mais amigáveis)

> **Como instalar plugins:** Acesse o **Package Control** com `Ctrl+Shift+P` → digite `Install Package` → pesquise o nome do plugin.

**Navegador — Google Chrome ou Firefox**
- Abra o **DevTools** com `F12` ou `Ctrl+Shift+I`
- A aba **Elements** exibe o DOM em tempo real
- A aba **Network** mostra as requisições a serviços externos — essencial para depurar chamadas a WMS e WFS

---

#### A Estrutura Básica de um Documento HTML

```html
<!DOCTYPE html>
<!-- Declara que este é um documento HTML5. Sempre na primeira linha. -->

<html lang="pt-BR">
<!-- lang="pt-BR" é essencial para: leitores de tela, SEO e corretor ortográfico -->

  <head>
    <!-- Metadados: não visíveis na página, mas lidos pelo navegador e robôs -->
    <meta charset="UTF-8">
    <!-- UTF-8 garante que acentos e caracteres especiais sejam exibidos corretamente -->

    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Torna a página responsiva em dispositivos móveis — fundamental para WebGIS em campo -->

    <meta name="description" content="Visualizador de mapas da Bacia Hidrográfica do Rio São Francisco">
    <!-- SEO: texto exibido nos resultados de busca do Google -->

    <meta name="author" content="Laboratório de Geoprocessamento - IFPB">

    <title>Visualizador WebGIS | IFPB</title>
    <!-- Texto exibido na aba do navegador e nos favoritos -->
  </head>

  <body>
    <!-- Todo conteúdo visível ao usuário vive aqui -->
    <p>Meu primeiro mapa será exibido aqui.</p>
  </body>

</html>
```

> **Contextualização GIS:** A tag `<meta name="description">` funciona como o resumo de metadados de uma camada no QGIS ou ArcGIS — ela descreve o conteúdo para sistemas externos (motores de busca, aggregators de dados geoespaciais).

---

### 1.2 Exercício Prático

**Exercício 1 — Minha Primeira Página**
Crie um arquivo chamado `index.html`. Escreva a estrutura mínima de um documento HTML5 sem copiar do material. O `<title>` deve ser "WebGIS — [Seu Nome]" e o `<body>` deve conter um parágrafo descrevendo sua área de estudo favorita em geoprocessamento.

---

### 1.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M1:** Crie o arquivo `index.html` que será a base do seu Visualizador de Mapas Estático. Ele deve conter:
- Estrutura HTML5 completa e válida
- `lang="pt-BR"` e `charset="UTF-8"`
- Meta description descrevendo o projeto como um visualizador WebGIS
- Title: "Visualizador WebGIS — [Tema do seu mapa]" (ex: Uso do Solo, Hidrografia, Risco de Enchentes)
- Um comentário `<!-- TODO: estrutura semântica será adicionada no Módulo 5 -->`

---

### 1.4 Glossário Técnico — Módulo 1

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| Markup Language | Linguagem de Marcação | Linguagem que usa tags para estruturar conteúdo |
| Tag | Etiqueta / Marcador | Elemento delimitado por `< >` que define um tipo de conteúdo |
| DOM | Modelo de Objeto do Documento | Representação em árvore dos elementos HTML na memória do navegador |
| Metadata | Metadados | Dados sobre dados; informações que descrevem o documento |
| Viewport | Área de Visualização | Região visível da página na tela do dispositivo |
| Charset | Conjunto de Caracteres | Padrão de codificação de texto (ex: UTF-8) |
| DevTools | Ferramentas do Desenvolvedor | Painel de inspeção do navegador |
| WMS | Web Map Service | Padrão OGC para servir mapas como imagens via Web |

---

## Módulo 2 — Trabalhando com Texto

### 2.1 Aprofundamento Teórico

#### Hierarquia de Títulos — `<h1>` a `<h6>`

Os títulos não são apenas sobre tamanho visual — eles definem a **estrutura hierárquica** do documento, usada por:
- Leitores de tela (acessibilidade WCAG 2.1 — critério 1.3.1)
- Robôs de busca (SEO — o `<h1>` é o título principal indexado pelo Google)
- Leitores de documentos que geram sumários automaticamente

**Regra fundamental:** Use apenas **um `<h1>` por página**, que deve descrever o tema central. Os demais níveis organizam seções e subseções.

```html
<h1>Atlas Digital da Paraíba</h1>         <!-- Título principal da página -->
  <h2>Meio Ambiente</h2>                  <!-- Seção principal -->
    <h3>Recursos Hídricos</h3>            <!-- Subseção -->
      <h4>Bacia do Rio Paraíba</h4>       <!-- Sub-subseção -->
    <h3>Vegetação</h3>
  <h2>Infraestrutura Urbana</h2>
```

---

#### Parágrafos — `<p>`

A tag `<p>` envolve um bloco de texto corrido. O navegador adiciona espaçamento vertical entre parágrafos automaticamente (que pode ser controlado via CSS).

```html
<p>
  O Sensoriamento Remoto é a ciência de obter informações sobre objetos
  ou áreas a partir de dados adquiridos por um dispositivo que não está
  em contato físico com o objeto investigado.
</p>

<p>
  Imagens de satélite, como as do Landsat-8 ou Sentinel-2, são exemplos
  clássicos de produtos de sensoriamento remoto amplamente utilizados
  em análises de uso e cobertura do solo.
</p>
```

---

#### Formatação Semântica de Texto

A distinção entre tags semânticas e apresentacionais é central para HTML5 moderno:

| Tag | Semântica | Apresentação padrão | Uso correto |
|-----|-----------|---------------------|-------------|
| `<strong>` | **Importância** | Negrito | Termos críticos, alertas |
| `<b>` | Sem semântica | Negrito | Destaque visual puro |
| `<em>` | *Ênfase* | Itálico | Palavras com ênfase no discurso |
| `<i>` | Sem semântica | Itálico | Termos técnicos, nomes científicos |
| `<mark>` | Relevância | Marcado/Amarelo | Resultado de busca destacado |
| `<small>` | Texto secundário | Menor | Copyright, notas de rodapé |
| `<sub>` | Subscrito | Abaixo da linha | Fórmulas: CO₂ |
| `<sup>` | Sobrescrito | Acima da linha | Expoentes: km² |
| `<code>` | Código fonte | Monoespaçada | Comandos, funções, parâmetros |
| `<abbr>` | Abreviação | Sublinhado pontilhado | Siglas com título explicativo |

```html
<p>
  A resolução espacial do <strong>Sentinel-2</strong> varia de
  <em>10 a 60 metros</em>, dependendo da banda espectral. A área
  mapeada foi de 1.250 km<sup>2</sup>, com concentração de
  <mark>CO<sub>2</sub></mark> acima do limite estabelecido pelo
  <abbr title="Instituto Brasileiro do Meio Ambiente">IBAMA</abbr>.
</p>

<p>
  Para reprojetar uma camada no QGIS, utilize o comando
  <code>ogr2ogr -t_srs EPSG:4674 saida.shp entrada.shp</code>.
</p>
```

> **Contextualização GIS:** Use `<abbr>` para siglas do universo GIS — SIG, WMS, WFS, OGC, EPSG — sempre com o atributo `title` explicando o significado. Isso melhora a acessibilidade e o entendimento de usuários não especialistas.

---

#### Quebras de Linha `<br>` e Separadores `<hr>`

```html
<!-- <br> — use com parcimônia, apenas quando a quebra faz parte do conteúdo -->
<p>
  Coordenadas do ponto de coleta:<br>
  Latitude: -7.2195° S<br>
  Longitude: -35.9227° W<br>
  Altitude: 550 m
</p>

<!-- <hr> — separador temático entre seções de conteúdo -->
<h2>Camadas Vetoriais</h2>
<p>Polígonos de uso do solo...</p>

<hr>
<!-- Separação temática antes de uma nova seção -->

<h2>Camadas Raster</h2>
<p>Imagens de satélite...</p>
```

> **Boa prática:** Evite usar `<br>` para criar espaçamento visual — isso é função do CSS (`margin`, `padding`). Reserve `<br>` para conteúdo onde a quebra é semanticamente significativa, como endereços ou coordenadas geográficas.

---

### 2.2 Exercícios Práticos

**Exercício 2.A — Página de Apresentação de Camada**
Crie um arquivo `camada.html`. Escreva o conteúdo textual descrevendo uma camada GIS de sua escolha (ex: Hidrografia, Uso do Solo, Limites Municipais) usando:
- Um `<h1>` com o nome da camada
- Um `<h2>` "Descrição" com um `<p>` explicativo
- Um `<h2>` "Especificações Técnicas" com informações usando `<strong>`, `<em>` e `<abbr>`
- Um `<h2>` "Sistema de Referência" com as coordenadas usando `<sub>` e `<sup>` onde apropriado

**Exercício 2.B — Artigo Técnico Marcado**
Dado o texto abaixo (em prosa, sem marcação), aplique as tags HTML semânticas mais adequadas em cada trecho:

```
NDVI - O Índice de Vegetação por Diferença Normalizada
O NDVI (Normalized Difference Vegetation Index) é um índice que varia de -1 a +1.
Valores acima de 0,6 indicam vegetação densa e saudável. ATENÇÃO: valores negativos
geralmente indicam superfícies de água ou nuvens. A fórmula é: (NIR - Red) / (NIR + Red).
```

---

### 2.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M2:** No seu `index.html`, adicione uma seção de texto abaixo do `<body>` com:
- `<h1>` com o nome do seu Visualizador de Mapas
- `<h2>` "Sobre este Mapa" com um `<p>` descrevendo o tema e a área geográfica coberta
- `<h2>` "Fonte dos Dados" com um `<p>` usando `<strong>` para o nome da instituição e `<abbr>` para siglas (ex: `<abbr title="Instituto Brasileiro de Geografia e Estatística">IBGE</abbr>`)
- `<h2>` "Sistema de Referência" com as informações do <abbr>SRC</abbr> usando `<code>` para o código EPSG

---

### 2.4 Glossário Técnico — Módulo 2

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| Semantic HTML | HTML Semântico | Uso de tags que descrevem o *significado* do conteúdo |
| Heading Hierarchy | Hierarquia de Títulos | Organização lógica de `<h1>` a `<h6>` |
| Accessibility | Acessibilidade | Capacidade de uso por pessoas com diferentes habilidades |
| Screen Reader | Leitor de Tela | Software que converte conteúdo HTML em áudio |
| SEO | Otimização para Motores de Busca | Técnicas para melhorar posicionamento em buscadores |
| WCAG | Diretrizes de Acessibilidade para Conteúdo Web | Padrão internacional de acessibilidade (W3C) |
| NDVI | Índice de Vegetação por Diferença Normalizada | Índice espectral para análise de cobertura vegetal |
| EPSG | European Petroleum Survey Group | Repositório de Sistemas de Referência de Coordenadas |

---

## Módulo 3 — Links e Imagens

### 3.1 Aprofundamento Teórico

#### Hiperlinks — `<a>`

A tag `<a>` (*anchor* — âncora) é o elemento que transforma a Web em uma rede interligada. Todo link possui, no mínimo, o atributo `href` (*Hypertext REFerence*) que define o destino.

```html
<!-- Link externo: URL completa (protocolo + domínio + caminho) -->
<a href="https://www.ibge.gov.br/geociencias/downloads-geociencias.html"
   target="_blank"
   rel="noopener noreferrer">
  Baixar dados geoespaciais do IBGE
</a>
```

**Anatomia dos atributos:**

| Atributo | Valor | Função |
|----------|-------|--------|
| `href` | URL ou caminho | Destino do link |
| `target="_blank"` | Nova aba | Abre sem fechar a página atual |
| `rel="noopener noreferrer"` | Segurança | **Obrigatório** com `target="_blank"` — impede que a página destino acesse o `window.opener` (vulnerabilidade de segurança) |
| `title` | Texto | Tooltip ao passar o mouse — útil para acessibilidade |
| `download` | Nome do arquivo | Força download em vez de navegação |

> **Contextualização GIS:** Use links para apontar a recursos geoespaciais externos:

```html
<!-- Link para serviço WMS do INPE -->
<a href="http://www.dgi.inpe.br/geoserver/wms?SERVICE=WMS&REQUEST=GetCapabilities"
   target="_blank"
   rel="noopener noreferrer"
   title="Capacidades do serviço WMS do INPE">
  Serviço WMS — INPE (GetCapabilities)
</a>

<!-- Link para metadados no GeoNetwork -->
<a href="https://metadados.inde.gov.br/geonetwork/srv/por/catalog.search"
   target="_blank"
   rel="noopener noreferrer">
  Catálogo de Metadados — INDE
</a>

<!-- Link de download de shapefile -->
<a href="dados/municipios_pb.zip" download="municipios_pb.zip">
  Download: Municípios da Paraíba (Shapefile, 2,4 MB)
</a>
```

**Links internos (âncoras):**
```html
<!-- Definindo o destino (âncora) -->
<h2 id="tabela-atributos">Tabela de Atributos</h2>

<!-- Link que salta para a âncora na mesma página -->
<a href="#tabela-atributos">Ver tabela de atributos</a>

<!-- Âncora em outra página -->
<a href="mapa.html#legenda">Ver legenda do mapa</a>
```

---

#### Imagens — `<img>`

A tag `<img>` é um **elemento vazio** (sem tag de fechamento) — ela incorpora recursos externos na página. Os atributos `src` e `alt` são obrigatórios segundo as diretrizes WCAG.

```html
<!-- Sintaxe completa e acessível -->
<img
  src="imagens/ortofoto_joao_pessoa_2023.jpg"
  alt="Ortofoto de João Pessoa de 2023 mostrando a região central com o Rio Sanhauá ao fundo"
  width="800"
  height="600"
  loading="lazy"
  title="Ortofoto — Resolução 0,15m — Fonte: SEMAM-JP"
>
```

**Atributos detalhados:**

| Atributo | Obrigatório | Descrição |
|----------|-------------|-----------|
| `src` | Sim | Caminho ou URL da imagem |
| `alt` | **Sim (WCAG)** | Descrição textual da imagem para leitores de tela. Se a imagem é decorativa, use `alt=""` |
| `width` / `height` | Recomendado | Evita *layout shift* (CLS) — o navegador reserva o espaço antes de carregar a imagem |
| `loading="lazy"` | Recomendado | Carrega a imagem apenas quando ela está próxima da viewport — melhora performance |
| `title` | Opcional | Tooltip com metadados da imagem |

> **Contextualização GIS — Tipos de imagem no contexto WebGIS:**

```html
<!-- Ortofoto como imagem estática -->
<figure>
  <img
    src="imagens/ndvi_semiarido_2023.png"
    alt="Mapa NDVI do Semiárido nordestino em 2023. Tons de verde escuro indicam
         vegetação densa na Serra da Borborema; tons amarelos e marrons indicam
         áreas de caatinga degradada e solo exposto."
    width="900"
    height="600"
    loading="lazy"
  >
  <figcaption>
    Figura 1 — Índice NDVI do Semiárido Nordestino (2023).
    Fonte: <strong>Sentinel-2 / ESA</strong>. Processamento: QGIS 3.36.
  </figcaption>
</figure>

<!-- Imagem de mapa com link para versão maior -->
<a href="imagens/mapa_uso_solo_alta_res.pdf" target="_blank" rel="noopener noreferrer">
  <img
    src="imagens/mapa_uso_solo_thumb.jpg"
    alt="Miniatura do mapa de uso e cobertura do solo da Bacia do Rio Gramame"
    width="300"
    height="200"
    loading="lazy"
  >
</a>

<!-- Imagem estática de tile WMS (GetMap) -->
<img
  src="https://geoserver.exemplo.gov.br/wms?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap
       &LAYERS=municipios_pb&STYLES=&CRS=EPSG:4674
       &BBOX=-38.7,-8.3,-34.8,-6.0&WIDTH=800&HEIGHT=600&FORMAT=image/png"
  alt="Mapa dos municípios da Paraíba gerado via WMS GetMap"
  width="800"
  height="600"
>
```

> **Nota sobre `<figure>` e `<figcaption>`:** Use `<figure>` para envolver qualquer conteúdo auto-contido que possa ser movido do fluxo principal — mapas, gráficos, fotos. O `<figcaption>` é a legenda cartográfica da Web.

---

#### Formatos de Imagem para WebGIS

| Formato | Melhor uso | Suporte a transparência |
|---------|-----------|------------------------|
| `PNG` | Mapas, diagramas, textos | Sim (ideal para tiles de mapa) |
| `JPEG` / `JPG` | Ortofotos, imagens de satélite | Não |
| `WebP` | Alternativa moderna ao PNG/JPG | Sim |
| `SVG` | Ícones, símbolos cartográficos vetoriais | Sim |
| `GIF` | Animações simples (ex: sequência temporal) | Sim (1 bit) |

---

### 3.2 Exercícios Práticos

**Exercício 3.A — Galeria de Mapas**
Crie um arquivo `galeria.html` com:
- 3 imagens usando `<figure>` e `<figcaption>` (pode usar imagens de placeholder como `https://placehold.co/800x600`)
- Cada imagem deve ter `alt` descritivo simulando um produto cartográfico (ex: "Mapa de declividade...", "Imagem Landsat-8...")
- Use `loading="lazy"` em todas
- Adicione um link `<a download>` sob cada figura para simular download do arquivo

**Exercício 3.B — Painel de Recursos GIS**
Crie um arquivo `recursos.html` com uma lista de links para serviços e portais de dados geoespaciais reais:
- Pelo menos 2 links para portais de dados abertos (IBGE, INPE, ANA, etc.)
- Pelo menos 1 link para um serviço WMS público
- Pelo menos 1 link interno para uma âncora na mesma página (`#secao-x`)
- Todos os links externos com `target="_blank"` e `rel="noopener noreferrer"`

---

### 3.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M3:** No seu `index.html`, adicione:
1. Uma seção `<figure>` com a imagem estática do seu mapa (use placeholder se não tiver ainda) com `alt` descritivo completo e `<figcaption>` com fonte e sistema de referência
2. Uma seção "Links Úteis" com pelo menos 3 links para dados e serviços relacionados ao tema do seu visualizador

---

### 3.4 Glossário Técnico — Módulo 3

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| Hyperlink / Anchor | Hiperlink / Âncora | Referência navegável entre documentos Web |
| URL | Localizador Uniforme de Recursos | Endereço único de um recurso na Internet |
| Relative Path | Caminho Relativo | Endereço de arquivo em relação ao arquivo atual |
| Absolute Path | Caminho Absoluto | Endereço completo a partir da raiz do servidor |
| Alt Text | Texto Alternativo | Descrição textual de uma imagem para acessibilidade |
| Lazy Loading | Carregamento Preguiçoso | Estratégia que adia o carregamento de recursos não visíveis |
| WMS GetMap | WMS GetMap | Requisição HTTP que retorna uma imagem de mapa de um servidor WMS |
| Ortofoto | Ortofotografia | Fotografia aérea ou de satélite corrigida geometricamente |
| Tile | Tile / Ladrilho | Fragmento de mapa em grade usada por serviços como TMS e WMTS |

---

## Módulo 4 — Listas e Tabelas

### 4.1 Aprofundamento Teórico

#### Listas Não Ordenadas — `<ul>`

Use `<ul>` quando a ordem dos itens **não importa semanticamente**.

```html
<!-- Camadas de um projeto WebGIS -->
<h3>Camadas Disponíveis</h3>
<ul>
  <li>Hidrografia — Rios e lagos (Fonte: ANA)</li>
  <li>Malha Viária — Rodovias e estradas (Fonte: DNIT)</li>
  <li>Uso e Cobertura do Solo — Classificação MAPBIOMAS 2023</li>
  <li>Limites Administrativos — Municípios (Fonte: IBGE 2022)</li>
</ul>

<!-- Lista aninhada: categorias de camadas -->
<ul>
  <li>Camadas de Base
    <ul>
      <li>OpenStreetMap</li>
      <li>Google Satellite</li>
      <li>Esri World Imagery</li>
    </ul>
  </li>
  <li>Camadas Temáticas
    <ul>
      <li>Risco de Inundação</li>
      <li>Aptidão Agrícola</li>
    </ul>
  </li>
</ul>
```

#### Listas Ordenadas — `<ol>`

Use `<ol>` quando a **sequência importa** — passos de um processo, ranking, procedimentos.

```html
<!-- Fluxo de processamento de imagem de satélite -->
<h3>Fluxo de Pré-processamento — Sentinel-2</h3>
<ol>
  <li>Download das cenas no <em>Copernicus Open Access Hub</em></li>
  <li>Correção atmosférica (Sen2Cor)</li>
  <li>Recorte pela área de interesse (clip)</li>
  <li>Reprojeção para SIRGAS 2000 / UTM Zone 25S (EPSG:31985)</li>
  <li>Composição de bandas RGB (B4, B3, B2)</li>
  <li>Cálculo do NDVI</li>
  <li>Exportação em GeoTIFF</li>
</ol>

<!-- Atributos especiais de <ol> -->
<ol start="3" reversed>
  <!-- start="3": começa a numeração em 3 -->
  <!-- reversed: ordem decrescente (ranking) -->
  <li>Bronze — Menor área de desmatamento</li>
  <li>Prata</li>
  <li>Ouro — Maior área de desmatamento</li>
</ol>
```

#### Listas de Definição — `<dl>`, `<dt>`, `<dd>`

Ideal para glossários, metadados e fichas técnicas de camadas.

```html
<h3>Metadados da Camada — Uso do Solo 2023</h3>
<dl>
  <dt>Título</dt>
  <dd>Mapeamento de Uso e Cobertura do Solo — Paraíba 2023</dd>

  <dt>Formato</dt>
  <dd>Shapefile (.shp) e GeoPackage (.gpkg)</dd>

  <dt>Sistema de Referência</dt>
  <dd>SIRGAS 2000 (<code>EPSG:4674</code>)</dd>

  <dt>Escala</dt>
  <dd>1:250.000</dd>

  <dt>Resolução Espacial</dt>
  <dd>30 metros (derivado de Landsat-8 OLI)</dd>

  <dt>Data de Referência</dt>
  <dd><time datetime="2023-06-15">15 de junho de 2023</time></dd>

  <dt>Licença</dt>
  <dd>Creative Commons CC BY 4.0</dd>
</dl>
```

---

#### Tabelas — Estrutura Completa

Tabelas HTML devem ser usadas **exclusivamente para dados tabulares** — nunca para layout visual. No contexto GIS, são perfeitas para representar tabelas de atributos de camadas vetoriais.

```html
<table>
  <!-- caption: título acessível da tabela (obrigatório para WCAG) -->
  <caption>
    Tabela de Atributos — Municípios da Paraíba com maior área (IBGE, 2022)
  </caption>

  <!-- thead: linha(s) de cabeçalho -->
  <thead>
    <tr>
      <!-- scope="col" associa o <th> à coluna — essencial para leitores de tela -->
      <th scope="col">Código IBGE</th>
      <th scope="col">Município</th>
      <th scope="col">Mesorregião</th>
      <th scope="col">Área (km²)</th>
      <th scope="col">Pop. (2022)</th>
      <th scope="col">IDHM</th>
    </tr>
  </thead>

  <!-- tbody: dados principais -->
  <tbody>
    <tr>
      <td>2503704</td>
      <td>Cajazeiras</td>
      <td>Sertão Paraibano</td>
      <td>566,1</td>
      <td>59.795</td>
      <td>0,678</td>
    </tr>
    <tr>
      <td>2507507</td>
      <td>João Pessoa</td>
      <td>Mata Paraibana</td>
      <td>211,5</td>
      <td>852.748</td>
      <td>0,763</td>
    </tr>
    <tr>
      <td>2510907</td>
      <td>Patos</td>
      <td>Sertão Paraibano</td>
      <td>475,1</td>
      <td>105.791</td>
      <td>0,701</td>
    </tr>
  </tbody>

  <!-- tfoot: totais ou notas de rodapé -->
  <tfoot>
    <tr>
      <!-- colspan: mescla 3 colunas horizontalmente -->
      <td colspan="3"><strong>Total parcial (3 municípios)</strong></td>
      <td>1.252,7</td>
      <td>1.018.334</td>
      <td>—</td>
    </tr>
  </tfoot>
</table>
```

**Mesclagem de células — `colspan` e `rowspan`:**

```html
<table>
  <caption>Classificação de Uso do Solo por Mesorregião — PB</caption>
  <thead>
    <tr>
      <th scope="col" rowspan="2">Mesorregião</th>
      <!-- rowspan="2": ocupa 2 linhas verticalmente -->
      <th scope="col" colspan="3">Uso do Solo (km²)</th>
      <!-- colspan="3": ocupa 3 colunas horizontalmente -->
    </tr>
    <tr>
      <th scope="col">Vegetação Nativa</th>
      <th scope="col">Agropecuária</th>
      <th scope="col">Área Urbana</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Sertão Paraibano</th>
      <td>12.450</td>
      <td>8.230</td>
      <td>340</td>
    </tr>
    <tr>
      <th scope="row">Borborema</th>
      <td>4.120</td>
      <td>6.890</td>
      <td>180</td>
    </tr>
  </tbody>
</table>
```

> **Acessibilidade em tabelas (WCAG 1.3.1):**
> - Sempre use `<caption>` — é o título acessível da tabela
> - Use `scope="col"` em `<th>` de cabeçalhos de coluna
> - Use `scope="row"` em `<th>` de cabeçalhos de linha
> - Nunca use tabelas para layout visual

---

### 4.2 Exercícios Práticos

**Exercício 4.A — Tabela de Atributos**
Crie um arquivo `atributos.html` com uma tabela completa (`<caption>`, `<thead>`, `<tbody>`, `<tfoot>`) representando pelo menos 5 feições de uma camada vetorial à sua escolha. Use dados reais ou realistas. A tabela deve ter um campo numérico cujo total seja calculado no `<tfoot>`.

**Exercício 4.B — Painel de Camadas com Listas Aninhadas**
Crie um arquivo `camadas.html` com:
- Uma `<ol>` com os passos do fluxo de trabalho do seu projeto de mapeamento
- Uma `<ul>` aninhada listando as camadas de dados utilizadas por categoria (base, temática, auxiliar)
- Uma `<dl>` com os metadados principais de uma camada (mínimo 6 pares `<dt>`/`<dd>`)

---

### 4.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M4:** No seu `index.html`, adicione:
1. Uma `<table>` com pelo menos 5 linhas representando a tabela de atributos das feições mostradas no seu mapa estático. Use `<caption>`, `<thead>`, `<tbody>`, `<tfoot>` e atributos `scope` para acessibilidade.
2. Uma `<ul>` ou `<dl>` com a lista de camadas ou fontes de dados do projeto.

---

### 4.4 Glossário Técnico — Módulo 4

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| Unordered List | Lista Não Ordenada | Lista de itens sem sequência definida (`<ul>`) |
| Ordered List | Lista Ordenada | Lista de itens com sequência numérica (`<ol>`) |
| Definition List | Lista de Definição | Pares termo/descrição (`<dl>`, `<dt>`, `<dd>`) |
| Table | Tabela | Estrutura de dados em linhas e colunas |
| Table Header | Cabeçalho de Tabela | Célula que rotula uma coluna ou linha (`<th>`) |
| Table Data | Dado de Tabela | Célula com dado (`<td>`) |
| Caption | Legenda / Título | Título descritivo de uma tabela ou figura |
| Colspan | Mesclagem de Colunas | Atributo que une células horizontalmente |
| Rowspan | Mesclagem de Linhas | Atributo que une células verticalmente |
| Attribute Table | Tabela de Atributos | Tabela de dados associada a feições vetoriais em SIG |
| Feature | Feição | Objeto geográfico (ponto, linha, polígono) com atributos |

---

## Módulo 5 — HTML Semântico e Estrutura de Layout

### 5.1 Aprofundamento Teórico

#### O que é HTML Semântico?

HTML semântico significa usar tags que **comunicam o significado** do conteúdo, não apenas sua aparência. Antes do HTML5, tudo era `<div>` e `<span>` com classes como `id="header"`, `id="nav"`, `id="footer"`. O HTML5 criou tags específicas para esses papéis.

**Por que isso importa para WebGIS?**
- **Acessibilidade:** Tecnologias assistivas (leitores de tela) navegam por landmarks semânticos — usuários com deficiência visual pulam direto para `<main>`, `<nav>` ou `<aside>`
- **SEO:** Mecanismos de busca entendem melhor a estrutura e indexam o conteúdo corretamente
- **Manutenção:** Código mais legível e auto-documentado
- **JavaScript:** Frameworks como Leaflet.js e OpenLayers buscam elementos por seletor — `document.getElementById('map')` é mais robusto quando o elemento está dentro de `<main>`

---

#### As Tags de Layout do HTML5

```
┌────────────────────────────────────────────────-─────┐
│                    <header>                          │
│  Logo + Título do Visualizador WebGIS                │
├──────────────────────────────────────────────────────┤
│                     <nav>                            │
│  Controles de Camadas | Ferramentas | Sobre          │
├────────────────────┬─────────────────────────────────┤
│                    │           <aside>               │
│                    │   Legenda do Mapa               │
│    <main>          │   ─────────────                 │
│  id="map"          │   □ Vegetação Nativa            │
│                    │   □ Área Urbana                 │
│  [Imagem do Mapa]  │   □ Corpos d'água               │
│                    │                                 │
│                    │   <section id="atributos">      │
│                    │   Tabela de Atributos           │
├────────────────────┴─────────────────────────────────┤
│                    <footer>                          │
│  Fonte dos dados | Projeção | Datum | Escala         │
└──────────────────────────────────────────────────────┘
```

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Visualizador WebGIS — Uso do Solo PB</title>
</head>
<body>

  <!-- ─── CABEÇALHO ─── -->
  <header>
    <!-- Identidade do projeto: logo, título, subtítulo -->
    <h1>Visualizador WebGIS</h1>
    <p>Mapeamento de Uso e Cobertura do Solo — Paraíba 2023</p>
  </header>

  <!-- ─── NAVEGAÇÃO PRINCIPAL ─── -->
  <nav aria-label="Controles de camadas e ferramentas">
    <!-- aria-label diferencia múltiplos <nav> na página para leitores de tela -->
    <ul>
      <li><a href="#map">Mapa</a></li>
      <li><a href="#legenda">Legenda</a></li>
      <li><a href="#atributos">Atributos</a></li>
      <li><a href="#sobre">Sobre</a></li>
    </ul>
  </nav>

  <!-- ─── CONTEÚDO PRINCIPAL ─── -->
  <main id="map" aria-label="Área principal do mapa">
    <!-- <main> deve haver apenas 1 por página -->
    <!-- aria-label ajuda leitores de tela a identificar a área do mapa -->

    <article id="mapa-estatico">
      <!-- <article> = conteúdo auto-contido e reutilizável -->
      <h2>Mapa de Uso e Cobertura do Solo</h2>
      <figure>
        <img
          src="imagens/uso_solo_pb_2023.png"
          alt="Mapa temático de uso e cobertura do solo da Paraíba em 2023.
               Predominância de Caatinga no Sertão (tons de amarelo) e vegetação
               mais densa na Mata Atlântica costeira (tons de verde escuro)."
          width="900"
          height="600"
          loading="lazy"
        >
        <figcaption>
          Figura 1 — Uso e Cobertura do Solo, Paraíba, 2023.
          Fonte: <strong>MapBiomas</strong> (Coleção 8).
          Projeção: <abbr title="Sistema de Referência Geocêntrico para as Américas">SIRGAS</abbr>
          2000 / <code>EPSG:4674</code>.
        </figcaption>
      </figure>
    </article>

    <section id="consulta">
      <!-- <section> = grupo temático que precisa de um título -->
      <h2>Consultar Feição</h2>
      <p>Selecione uma feição no mapa para ver seus atributos.</p>
      <!-- Formulário de consulta será adicionado no Módulo 6 -->
    </section>

  </main>

  <!-- ─── CONTEÚDO LATERAL ─── -->
  <aside aria-label="Legenda e informações complementares">
    <!-- <aside> = conteúdo relacionado mas secundário ao conteúdo principal -->

    <section id="legenda">
      <h2>Legenda</h2>
      <ul>
        <li>🟩 Vegetação Nativa</li>
        <li>🟨 Pastagem</li>
        <li>🟧 Agropecuária</li>
        <li>🟫 Solo Exposto</li>
        <li>🔵 Corpos d'Água</li>
        <li>⬛ Área Urbana</li>
      </ul>
    </section>

    <section id="sobre">
      <h2>Sobre o Projeto</h2>
      <p>
        Visualizador desenvolvido como projeto da disciplina de
        <strong>WebGIS</strong> no curso de
        <abbr title="Tecnologia em Geoprocessamento">Tecnologia em Geoprocessamento</abbr>
        — <abbr title="Instituto Federal da Paraíba">IFPB</abbr>.
      </p>
    </section>

  </aside>

  <!-- ─── RODAPÉ ─── -->
  <footer>
    <p>
      <small>
        Datum: <strong>SIRGAS 2000</strong> |
        Escala de referência: <strong>1:250.000</strong> |
        Atualizado em: <time datetime="2024-01-10">10 de janeiro de 2024</time>
      </small>
    </p>
    <p>
      <small>
        Dados: <a href="https://mapbiomas.org" target="_blank" rel="noopener noreferrer">MapBiomas</a> |
        Licença: <a href="https://creativecommons.org/licenses/by/4.0/" target="_blank" rel="noopener noreferrer">CC BY 4.0</a>
      </small>
    </p>
  </footer>

</body>
</html>
```

---

#### Tags Semânticas — Referência Rápida

| Tag | Papel | Regra de Uso |
|-----|-------|--------------|
| `<header>` | Cabeçalho | Pode aparecer em `<body>`, `<article>` ou `<section>`. Geralmente contém `<h1>`-`<h6>` e navegação |
| `<nav>` | Navegação | Para blocos de links de navegação. Use `aria-label` se houver mais de um |
| `<main>` | Conteúdo principal | **Apenas 1 por página.** Conteúdo único e central. Não inclua cabeçalho/rodapé |
| `<article>` | Conteúdo independente | Reutilizável fora de contexto (mapa, card de produto, post de blog) |
| `<section>` | Seção temática | Grupo de conteúdo relacionado. **Deve ter um título** (`<h2>`-`<h6>`) |
| `<aside>` | Conteúdo lateral | Relacionado ao conteúdo principal, mas independente (legenda, publicidade, links relacionados) |
| `<footer>` | Rodapé | Metadados de autoria, links secundários, copyright |
| `<figure>` | Conteúdo ilustrativo | Mapas, gráficos, fotos com legenda |
| `<figcaption>` | Legenda da figura | Dentro de `<figure>`. Aparece antes ou após o conteúdo |
| `<time>` | Data/hora | Use o atributo `datetime` no formato ISO 8601 |
| `<address>` | Informações de contato | Endereço físico ou digital do autor/organização |

---

### 5.2 Exercícios Práticos

**Exercício 5.A — Auditoria Semântica**
Pegue o arquivo `index.html` criado nos módulos anteriores e substitua todos os `<div>` por tags semânticas apropriadas. Justifique em comentários HTML cada substituição feita.

**Exercício 5.B — Layout de Portal GIS**
Esboce e codifique em HTML puro (sem CSS) a estrutura semântica de um portal de mapas simples com:
- `<header>` com nome do portal e `<nav>` de categorias (Hidrografia, Vegetação, Infraestrutura)
- `<main>` com `<article>` para o mapa e `<section>` para filtros
- `<aside>` com legenda e tabela de atributos resumida
- `<footer>` com informações de datum, escala e licença

---

### 5.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M5:** Reestruture completamente seu `index.html` usando o layout semântico mostrado neste módulo. A estrutura deve conter:
- `<header>` com `<h1>` e subtítulo descritivo
- `<nav aria-label="...">` com links de âncora para as seções da página
- `<main id="map">` com `<article>` para o mapa e `<section id="consulta">`
- `<aside>` com `<section id="legenda">` e `<section id="sobre">`
- `<footer>` com datum, escala, fonte dos dados e `<time datetime="...">`

---

### 5.4 Glossário Técnico — Módulo 5

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| Semantic HTML | HTML Semântico | Uso de tags com significado estrutural e contextual definido |
| Landmark | Marco / Referência | Região semântica da página usada por tecnologias assistivas |
| ARIA | Accessible Rich Internet Applications | Especificação W3C para acessibilidade de interfaces web |
| `aria-label` | Rótulo ARIA | Atributo que fornece nome acessível a um elemento |
| Layout | Leiaute | Disposição visual dos elementos na página |
| Viewport | Área de Visualização | Região visível da tela no navegador |
| SEO | Otimização para Motores de Busca | Conjunto de práticas para melhorar o posicionamento orgânico |
| Heading | Título / Cabeçalho | Elemento `<h1>`-`<h6>` que define hierarquia de conteúdo |

---

## Módulo 6 — Formulários HTML5

### 6.1 Aprofundamento Teórico

#### Anatomia de um Formulário

Formulários são o principal mecanismo de entrada de dados do usuário na Web. No contexto WebGIS, são usados para filtros de camadas, consultas espaciais, upload de dados e painéis de controle de mapa.

```
<form>                   ← container do formulário
  <fieldset>             ← grupo lógico de campos
    <legend>             ← título do grupo
    <label>              ← rótulo acessível
    <input>              ← campo de entrada
    <select>             ← lista suspensa
    <textarea>           ← área de texto
    <button>             ← botão de ação
  </fieldset>
</form>
```

**Atributos fundamentais de `<form>`:**

| Atributo | Descrição | Exemplo WebGIS |
|----------|-----------|----------------|
| `action` | URL para onde os dados são enviados | `/api/consulta-espacial` |
| `method="get"` | Dados na URL (visíveis, pesquisáveis) | Consultas de mapa, filtros |
| `method="post"` | Dados no corpo da requisição (não visíveis na URL) | Upload de arquivos, senhas |
| `enctype` | Codificação dos dados | `multipart/form-data` para upload de SHP |
| `novalidate` | Desativa validação nativa | Use para validação customizada em JS |

---

#### A Dupla `<label>` + `<input>`

A associação entre `<label>` e `<input>` é **obrigatória pela WCAG 1.3.1**. Existem duas formas:

```html
<!-- Forma 1: for/id (recomendada — flexível no layout) -->
<label for="municipio">Município:</label>
<input type="text" id="municipio" name="municipio">

<!-- Forma 2: label envolvendo o input (implícita) -->
<label>
  Município:
  <input type="text" name="municipio">
</label>
```

> **Por que é crítico:** Sem a associação `<label>`, um usuário de leitor de tela não sabe o que digitar em um campo. Além disso, clicar no `<label>` foca o `<input>` correspondente — melhora a usabilidade em telas touch.

---

#### Tipos de `<input>` — Guia Completo

```html
<form action="/api/filtro-camadas" method="get">

  <fieldset>
    <legend>Filtro de Feições</legend>

    <!-- Texto livre -->
    <label for="nome-municipio">Nome do Município:</label>
    <input
      type="text"
      id="nome-municipio"
      name="municipio"
      placeholder="Ex: Campina Grande"
      autocomplete="off"
      maxlength="100"
    >

    <!-- Numérico com intervalo -->
    <label for="area-min">Área mínima (km²):</label>
    <input
      type="number"
      id="area-min"
      name="area_min"
      min="0"
      max="99999"
      step="0.1"
      value="0"
    >

    <!-- Intervalo de datas (para análise temporal) -->
    <label for="data-imagem">Data da imagem:</label>
    <input
      type="date"
      id="data-imagem"
      name="data_imagem"
      min="2013-04-11"
      max="2024-12-31"
    >

    <!-- Email -->
    <label for="email-solicitante">Seu e-mail:</label>
    <input
      type="email"
      id="email-solicitante"
      name="email"
      placeholder="nome@instituicao.gov.br"
      required
    >

    <!-- URL (para WMS externo) -->
    <label for="url-wms">URL do Serviço WMS:</label>
    <input
      type="url"
      id="url-wms"
      name="wms_url"
      placeholder="https://geoserver.exemplo.gov.br/wms"
    >

    <!-- Range: slider visual (ex: opacidade de camada) -->
    <label for="opacidade">Opacidade da Camada: <output for="opacidade" id="val-opacidade">100</output>%</label>
    <input
      type="range"
      id="opacidade"
      name="opacidade"
      min="0"
      max="100"
      step="5"
      value="100"
    >

    <!-- Cor (ex: simbologia do mapa) -->
    <label for="cor-feicao">Cor das Feições:</label>
    <input type="color" id="cor-feicao" name="cor" value="#2e7d32">

    <!-- Arquivo (upload de shapefile zip) -->
    <label for="upload-shp">Upload de Shapefile (ZIP):</label>
    <input
      type="file"
      id="upload-shp"
      name="shapefile"
      accept=".zip,.shp,.geojson,.kml,.gpkg"
    >

  </fieldset>

  <fieldset>
    <legend>Tipo de Geometria</legend>

    <!-- Radio buttons: escolha única (tipo de feição) -->
    <label>
      <input type="radio" name="geometria" value="ponto" checked>
      Ponto
    </label>
    <label>
      <input type="radio" name="geometria" value="linha">
      Linha
    </label>
    <label>
      <input type="radio" name="geometria" value="poligono">
      Polígono
    </label>
  </fieldset>

  <fieldset>
    <legend>Camadas para Exportar</legend>

    <!-- Checkboxes: múltipla escolha (camadas selecionadas) -->
    <label>
      <input type="checkbox" name="camadas" value="hidrografia" checked>
      Hidrografia
    </label>
    <label>
      <input type="checkbox" name="camadas" value="vegetacao">
      Vegetação Nativa
    </label>
    <label>
      <input type="checkbox" name="camadas" value="malha-viaria">
      Malha Viária
    </label>
  </fieldset>

  <fieldset>
    <legend>Formato de Saída</legend>

    <!-- Select: lista suspensa (formato de exportação) -->
    <label for="formato-saida">Formato de exportação:</label>
    <select id="formato-saida" name="formato">
      <optgroup label="Vetorial">
        <option value="shp">Shapefile (.shp)</option>
        <option value="gpkg" selected>GeoPackage (.gpkg)</option>
        <option value="geojson">GeoJSON (.geojson)</option>
        <option value="kml">KML (.kml)</option>
      </optgroup>
      <optgroup label="Raster">
        <option value="geotiff">GeoTIFF (.tif)</option>
        <option value="png">PNG</option>
      </optgroup>
    </select>

    <!-- Textarea: observações (metadados livres) -->
    <label for="observacoes">Observações / Descrição do uso:</label>
    <textarea
      id="observacoes"
      name="observacoes"
      rows="4"
      cols="50"
      placeholder="Descreva brevemente como você utilizará os dados..."
      maxlength="500"
    ></textarea>

  </fieldset>

  <!-- Botões de ação -->
  <button type="submit">Aplicar Filtro</button>
  <button type="reset">Limpar Campos</button>

</form>
```

---

#### Validação HTML5 Nativa

O HTML5 oferece validação sem JavaScript:

```html
<!-- required: campo obrigatório -->
<input type="text" name="municipio" required>

<!-- pattern: expressão regular (ex: código IBGE de 7 dígitos) -->
<input
  type="text"
  name="codigo_ibge"
  pattern="[0-9]{7}"
  title="Digite o código IBGE de 7 dígitos (ex: 2507507)"
  required
>

<!-- min/max em inputs numéricos e de data -->
<input type="number" name="zoom" min="1" max="20" value="10">

<!-- minlength/maxlength -->
<input type="text" name="nome" minlength="3" maxlength="100">
```

> **Boa prática:** Valide sempre no servidor também. A validação HTML5 pode ser desabilitada pelo usuário — nunca confie só nela para dados críticos.

---

### 6.2 Exercícios Práticos

**Exercício 6.A — Formulário de Consulta Espacial**
Crie um arquivo `consulta.html` com um formulário que simule uma consulta a um banco de dados espacial. Deve conter:
- Campo de texto para nome do município (com `required` e `pattern` para aceitar apenas letras e espaços)
- Campo numérico para população mínima (min: 0)
- Select para mesorregião (com pelo menos 4 opções agrupadas em `<optgroup>` por estado)
- Checkboxes para selecionar tipos de dados (pontos, linhas, polígonos)
- Botões "Consultar" e "Limpar"

**Exercício 6.B — Formulário de Metadados**
Crie um arquivo `metadados.html` com um formulário para preenchimento dos metadados de uma camada GIS, contendo:
- Campos: Título, Resumo (`<textarea>`), Data de criação (`type="date"`), Escala (`type="number"`), Sistema de Referência (`<select>` com EPSG:4674, EPSG:4326, EPSG:31984, EPSG:31985)
- Upload de arquivo thumbnail (`type="file"` aceitando apenas imagens)
- Campo de email do responsável com validação
- Todos os campos obrigatórios devidamente marcados com `required`

---

### 6.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M6:** Adicione ao `<section id="consulta">` do seu `index.html` um formulário de filtragem de feições com:
- Um campo de texto para busca por nome
- Um `<select>` para filtrar por categoria (use as categorias de uso do solo do seu mapa)
- Um `<input type="range">` para controle de opacidade da camada
- Botões "Aplicar" (`type="submit"`) e "Limpar" (`type="reset"`)

---

### 6.4 Glossário Técnico — Módulo 6

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| Form | Formulário | Container HTML para coleta de dados do usuário |
| Input | Campo de Entrada | Elemento interativo para entrada de dados |
| Label | Rótulo | Texto descritivo associado a um campo |
| Fieldset | Grupo de Campos | Agrupamento lógico de campos de um formulário |
| Legend | Legenda do Grupo | Título descritivo de um `<fieldset>` |
| Select | Seleção / Lista Suspensa | Menu de escolha de opções |
| Checkbox | Caixa de Seleção | Campo para múltipla escolha (verdadeiro/falso) |
| Radio Button | Botão de Rádio | Campo para escolha única em um grupo |
| Textarea | Área de Texto | Campo de texto multilinha |
| Validation | Validação | Verificação de dados inseridos conforme regras definidas |
| GET / POST | GET / POST | Métodos HTTP para envio de dados de formulário |
| Required | Obrigatório | Atributo que torna o preenchimento de campo mandatório |
| WFS | Web Feature Service | Padrão OGC para consulta e manipulação de feições geoespaciais via Web |

---

## Módulo 7 — Introdução ao CSS3: Estilizando o Visualizador WebGIS

### 7.1 Aprofundamento Teórico

#### As Três Formas de Incluir CSS

```html
<!-- 1. CSS Inline: aplicado diretamente no elemento (evite — dificulta manutenção) -->
<p style="color: #1a237e; font-size: 16px;">Legenda do mapa</p>

<!-- 2. CSS Interno: dentro do <head> (bom para página única de teste) -->
<head>
  <style>
    body { font-family: sans-serif; }
    #map { border: 2px solid #333; }
  </style>
</head>

<!-- 3. CSS Externo: arquivo .css separado (melhor prática — reutilizável) -->
<head>
  <link rel="stylesheet" href="css/estilos.css">
</head>
```

> **Melhor prática:** Use sempre CSS externo em projetos reais. Para um WebGIS com múltiplas páginas (mapa, tabela, formulário), um único arquivo CSS mantém consistência visual.

---

#### Seletores CSS Essenciais

```css
/* Seletor de tipo: aplica a todos os elementos <h2> */
h2 {
  color: #1a237e;
}

/* Seletor de classe: elementos com class="legenda-item" */
.legenda-item {
  display: flex;
  align-items: center;
  gap: 8px;
}

/* Seletor de ID: elemento único com id="map" */
#map {
  width: 100%;
  height: 500px;
  border: 1px solid #ccc;
}

/* Seletor descendente: <p> dentro de <aside> */
aside p {
  font-size: 0.875rem;
}

/* Pseudo-classe: link quando passamos o mouse */
a:hover {
  color: #e65100;
  text-decoration: underline;
}

/* Pseudo-classe: linha de tabela alternada (zebra) */
tr:nth-child(even) {
  background-color: #f5f5f5;
}
```

`:nth-child(even)` seleciona **filhos em posições pares** (2º, 4º, 6º...). Outros padrões úteis:

| Seletor | Seleciona |
|---|---|
| `:nth-child(even)` | linhas 2, 4, 6... |
| `:nth-child(odd)` | linhas 1, 3, 5... |
| `:nth-child(3n)` | linhas 3, 6, 9... |
| `:nth-child(2n+1)` | mesmo que `odd` |

---

#### O Modelo de Caixas (Box Model)

Todo elemento HTML é uma caixa retangular com quatro camadas:

```
┌─────────────────────────────────────────┐
│               MARGIN                    │  ← espaço externo (transparente)
│  ┌───────────────────────────────────┐  │
│  │            BORDER                 │  │  ← borda visível
│  │  ┌─────────────────────────────┐  │  │
│  │  │          PADDING            │  │  │  ← espaço interno
│  │  │  ┌───────────────────────┐  │  │  │
│  │  │  │      CONTENT          │  │  │  │  ← o conteúdo (texto, imagem)
│  │  │  └───────────────────────┘  │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

```css
/* box-sizing: border-box — o padrão moderno e mais intuitivo */
*, *::before, *::after {
  box-sizing: border-box;
  /* Com border-box, width/height incluem padding e border */
}

#map {
  width: 800px;     /* largura total da caixa */
  height: 500px;
  padding: 16px;    /* espaço interno em todos os lados */
  border: 2px solid #546e7a;
  margin: 0 auto;   /* centraliza horizontalmente */
}
```

---

#### Layout com CSS Flexbox

Flexbox é ideal para disposição de elementos em uma **única direção** (linha ou coluna).

```css
/* Container flex: o pai */
.painel-webgis {
  display: flex;
  flex-direction: row;    /* itens em linha (padrão) */
  gap: 16px;              /* espaço entre itens */
  align-items: stretch;   /* itens esticam para a mesma altura */
}

/* Área do mapa: ocupa o espaço restante */
#map {
  flex: 1;                /* cresce para preencher o espaço disponível */
  min-height: 500px;
  background-color: #e8f5e9;
  border: 2px solid #4caf50;
}

/* Painel lateral: largura fixa */
.painel-lateral {
  flex: 0 0 280px;        /* não cresce, não encolhe, base 280px */
  background-color: #fafafa;
  border-left: 1px solid #e0e0e0;
  padding: 16px;
}
```

```html
<!-- HTML correspondente -->
<div class="painel-webgis">
  <main id="map">
    <img src="imagens/mapa.png" alt="Mapa de uso do solo">
  </main>
  <aside class="painel-lateral">
    <section id="legenda">
      <h2>Legenda</h2>
    </section>
  </aside>
</div>
```

O resultado visual do Flexbox acima:

```
┌─────────────────────────────────────┐
│  .painel-webgis  (flex container)   │
│  ┌────────────┐  ┌───────────────┐  │
│  │   #map     │  │ .painel-lat.  │  │
│  │  flex: 1   │  │ flex: 0 0 280 │  │
│  │  (cresce)  │  │  (fixo 280px) │  │
│  └────────────┘  └───────────────┘  │
└─────────────────────────────────────┘
```

A propriedade `flex` é um atalho para três valores:

```css
flex: 1              /* cresce para preencher o espaço */
flex: 0 0 280px      /* grow=0, shrink=0, basis=280px  */
/*    ↑   ↑    ↑
   cresce encolhe tamanho-base  */
```

- **`flex: 1`** no `#map` → ocupa **todo o espaço que sobra**
- **`flex: 0 0 280px`** no painel → **largura fixa, nunca muda**

---

#### Layout com CSS Grid

CSS Grid é ideal para layouts **bidimensionais** — linhas e colunas simultaneamente.

```css
/* Layout completo do Visualizador WebGIS com Grid */
body {
  display: grid;
  grid-template-areas:
    "header  header"
    "nav     nav"
    "map     aside"
    "footer  footer";
  grid-template-columns: 1fr 280px;
  grid-template-rows: auto auto 1fr auto;
  min-height: 100vh;
  gap: 0;
}

/* Atribuindo elementos às áreas nomeadas */
body > header  { grid-area: header; }
body > nav     { grid-area: nav; }
body > main    { grid-area: map; }
body > aside   { grid-area: aside; }
body > footer  { grid-area: footer; }
```

O resultado visual do Grid acima:

```
┌──────────────────────────────────┐
│           header                 │  ← auto
├──────────────────────────────────┤
│             nav                  │  ← auto
├────────────────────┬─────────────┤
│                    │             │
│        map         │    aside    │  ← 1fr
│     (1fr = resto)  │   (280px)   │
│                    │             │
├──────────────────────────────────┤
│           footer                 │  ← auto
└──────────────────────────────────┘
  ←────── 1fr ──────→←── 280px ───→
```

**Como funciona cada parte:**

- **`grid-template-areas`** — você "desenha" o layout com nomes; repetir o nome faz o elemento ocupar várias colunas (`"header header"`)
- **`1fr`** — fração do espaço disponível (elástico, como `flex: 1`)
- **`280px`** — coluna fixa, independente do tamanho da tela
- **`auto`** nas linhas — altura determinada pelo próprio conteúdo
- **`1fr`** na linha do mapa — ocupa todo o espaço vertical restante

---

**Grid vs Flexbox — quando usar cada um:**

| | Flexbox | Grid |
|---|---|---|
| **Dimensões** | 1D (linha ou coluna) | 2D (linha + coluna) |
| **Ideal para** | Componentes, navbars, cards | Layouts de página inteira |
| **Controle** | Os filhos se organizam | Você define a estrutura |
| **Exemplo WebGIS** | Ícone + rótulo na legenda | Header + Mapa + Sidebar + Footer |

> **Regra prática:** use **Grid** para o esqueleto da página, **Flexbox** para organizar os elementos dentro de cada seção.

---

#### Variáveis CSS (Custom Properties) — Essencial para WebGIS

Variáveis CSS permitem criar um sistema de design consistente — cores de camadas, fontes, tamanhos:

```css
/* Definição das variáveis na raiz do documento */
:root {
  /* Paleta de cores da legenda de uso do solo */
  --cor-vegetacao-nativa:  #2e7d32;
  --cor-pastagem:          #cddc39;
  --cor-agropecuaria:      #ff8f00;
  --cor-solo-exposto:      #795548;
  --cor-corpos-agua:       #1565c0;
  --cor-area-urbana:       #424242;

  /* Cores de interface */
  --cor-primaria:    #1a237e;
  --cor-secundaria:  #546e7a;
  --cor-fundo:       #f5f5f5;
  --cor-borda:       #e0e0e0;

  /* Tipografia */
  --fonte-principal: 'Inter', 'Segoe UI', system-ui, sans-serif;
  --tamanho-base:    16px;

  /* Espaçamentos */
  --espaco-sm: 8px;
  --espaco-md: 16px;
  --espaco-lg: 32px;
}

/* Usando as variáveis */
.legenda-vegetacao { background-color: var(--cor-vegetacao-nativa); }
.legenda-pastagem  { background-color: var(--cor-pastagem); }
.legenda-urbana    { background-color: var(--cor-area-urbana); }

header {
  background-color: var(--cor-primaria);
  color: white;
  padding: var(--espaco-md) var(--espaco-lg);
  font-family: var(--fonte-principal);
}
```

---

#### Responsividade com Media Queries

```css
/* Mobile first: estilos base para telas pequenas */
body {
  display: flex;
  flex-direction: column;
}

/* A partir de 768px (tablet): layout lado a lado */
@media (min-width: 768px) {
  .painel-webgis {
    flex-direction: row;
  }

  #map {
    flex: 1;
  }

  .painel-lateral {
    flex: 0 0 250px;
  }
}

/* A partir de 1200px (desktop): legenda maior */
@media (min-width: 1200px) {
  .painel-lateral {
    flex: 0 0 320px;
  }
}
```

---

#### Estilizando Tabelas de Atributos

```css
/* Tabela de atributos no estilo de SIG desktop */
table {
  width: 100%;
  border-collapse: collapse;   /* remove espaço duplo entre bordas */
  font-size: 0.875rem;
  font-family: var(--fonte-principal);
}

caption {
  font-weight: bold;
  text-align: left;
  padding: var(--espaco-sm);
  background-color: var(--cor-primaria);
  color: white;
}

th {
  background-color: var(--cor-secundaria);
  color: white;
  padding: 8px 12px;
  text-align: left;
  position: sticky;    /* cabeçalho fixo ao rolar */
  top: 0;
}

td {
  padding: 6px 12px;
  border-bottom: 1px solid var(--cor-borda);
}

/* Linhas alternadas (zebra) */
tbody tr:nth-child(even) {
  background-color: #f9fbe7;
}

/* Destaque ao passar o mouse */
tbody tr:hover {
  background-color: #e8f5e9;
  cursor: pointer;
}

tfoot td {
  font-weight: bold;
  background-color: #eeeeee;
  border-top: 2px solid var(--cor-secundaria);
}
```

---

### 7.2 Exercícios Práticos

**Exercício 7.A — Estilizando a Legenda**
Crie o arquivo `css/estilos.css`. Estilize o `<section id="legenda">` do seu `index.html` para que os itens da legenda apareçam com:
- Um quadrado colorido ao lado de cada rótulo (use `display: flex` e `align-items: center`)
- Cada cor definida como variável CSS em `:root`
- Tamanho do quadrado de cor: `16px × 16px`
- Bordas arredondadas no container da legenda (`border-radius`)

**Exercício 7.B — Layout Grid do Visualizador**
Aplique o layout CSS Grid ao `index.html` conforme o modelo apresentado neste módulo. O resultado deve posicionar:
- `<header>` ocupando toda a largura
- `<nav>` abaixo do header, largura total
- `<main>` à esquerda, ocupando o espaço livre
- `<aside>` à direita com 280px de largura
- `<footer>` abaixo de tudo, largura total

---

### 7.3 Desafio de Integração — "Rumo ao WebGIS"

**Tarefa M7 — Projeto Final: Visualizador de Mapas Estático**

Integre tudo que foi aprendido. Seu `index.html` deve estar estilizado com `css/estilos.css` e conter:

1. **Layout CSS Grid** posicionando `<header>`, `<nav>`, `<main>`, `<aside>` e `<footer>`
2. **Variáveis CSS** para a paleta de cores da legenda temática
3. **Tabela de atributos** estilizada (zebra, hover, sticky header)
4. **Formulário de consulta** estilizado com Flexbox nos campos
5. **Responsividade** com ao menos uma media query para mobile (`max-width: 768px`) que empilhe o mapa e a legenda verticalmente
6. **Validação:** Passe o código HTML pelo [Validador W3C](https://validator.w3.org/) e o CSS pelo [CSS Validation Service](https://jigsaw.w3.org/css-validator/). Capture os resultados e anote no `<footer>` como comentário.

---

### 7.4 Glossário Técnico — Módulo 7

| Termo em Inglês | Termo em Português | Definição |
|---|---|---|
| CSS | Folha de Estilos em Cascata | Linguagem para estilizar elementos HTML |
| Selector | Seletor | Padrão que identifica elementos HTML para aplicar estilos |
| Box Model | Modelo de Caixas | Modelo que define content, padding, border e margin |
| Flexbox | Layout Flexível | Módulo CSS para layout unidimensional |
| CSS Grid | Grade CSS | Módulo CSS para layout bidimensional |
| Media Query | Consulta de Mídia | Regra CSS condicional baseada em características do dispositivo |
| Custom Property | Propriedade Personalizada | Variável CSS definida com `--nome` e usada com `var()` |
| Cascade | Cascata | Algoritmo que determina qual estilo prevalece em conflito |
| Specificity | Especificidade | Peso de um seletor que determina prioridade na cascata |
| Responsive Design | Design Responsivo | Abordagem de design que adapta o layout ao dispositivo |
| Mobile First | Mobile Primeiro | Estratégia de escrever CSS para mobile antes de desktop |
| W3C Validator | Validador W3C | Ferramenta oficial para verificar conformidade de HTML/CSS |

---

## Projeto Final — Visualizador de Mapas Estático WebGIS

### Especificações do Projeto

Ao completar todos os módulos, você terá construído uma página web completa com:

| Componente | Módulo | Tecnologia |
|-----------|--------|-----------|
| Estrutura do documento | M1 | HTML5 (`DOCTYPE`, `<head>`, `<body>`) |
| Hierarquia textual e metadados | M2 | `<h1>`-`<h6>`, `<strong>`, `<abbr>`, `<time>` |
| Mapa estático com legenda cartográfica | M3 | `<figure>`, `<img>`, `<figcaption>` |
| Tabela de atributos das feições | M4 | `<table>`, `<thead>`, `<tbody>`, `<tfoot>` |
| Layout semântico completo | M5 | `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>` |
| Formulário de consulta e filtros | M6 | `<form>`, `<input>`, `<select>`, `<fieldset>` |
| Estilização e responsividade | M7 | CSS Grid, Flexbox, Custom Properties, Media Queries |

### Checklist de Qualidade

Antes de entregar, verifique:

- [ ] HTML válido no [W3C Validator](https://validator.w3.org/)
- [ ] CSS válido no [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- [ ] Todas as imagens têm `alt` descritivo (WCAG 1.1.1)
- [ ] Hierarquia de títulos lógica: apenas 1 `<h1>`, sem pular níveis
- [ ] `lang="pt-BR"` no `<html>`
- [ ] `charset="UTF-8"` e `viewport` no `<head>`
- [ ] Todos os `<label>` associados ao `<input>` correto via `for`/`id`
- [ ] `target="_blank"` sempre acompanhado de `rel="noopener noreferrer"`
- [ ] Tabela com `<caption>` e atributos `scope` nos `<th>`
- [ ] Responsividade funcional em tela de 375px (iPhone SE) e 1440px (desktop)

---

*Material didático desenvolvido para o curso de Tecnologia em Geoprocessamento — IFPB.*
*Referências: MDN Web Docs, W3C HTML Living Standard, WCAG 2.1, OGC Standards.*
