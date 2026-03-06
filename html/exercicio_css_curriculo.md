# 🎨 Aula de CSS — Estilização do Currículo

> **Objetivo:** Compreender as propriedades CSS utilizadas em cada seção de uma página, com foco em variáveis, unidades de medida, layout com Flexbox e dimensionamento responsivo.

---

## 📌 Índice

1. [Variáveis CSS (Custom Properties)](#1-variáveis-css)
2. [Unidades de Medida em CSS](#2-unidades-de-medida-em-css)
3. [Layout Base — `html` e `body`](#3-layout-base--html-e-body)
4. [Navegação — `nav`](#4-navegação--nav)
5. [Cabeçalho — `header`](#5-cabeçalho--header)
6. [Conteúdo Principal — `main` e `.conteudo`](#6-conteúdo-principal--main-e-conteudo)
7. [Rodapé — `footer`](#7-rodapé--footer)
8. [Erros no Código Original](#8-erros-no-código-original)
9. [Resumo das Formas de Dimensionamento](#9-resumo-das-formas-de-dimensionamento)

---

## 1. Variáveis CSS

```css
:root {
    --ifpb-verde: #009639;
    --ifpb-vermelho: #E31D1A;
    --ifpb-cinza-escuro: #4d4d4d;
    --ifpb-cinza-claro: #f4f4f4;
    --ifpb-branco: #ffffff;
    --sombra: 0 4px 8px rgba(0, 0, 0, 0.1);
    --transicao: all 0.3s ease;
}
```

### O que é `:root`?

`:root` é um **seletor pseudo-classe** que representa o elemento raiz do documento HTML (equivalente à tag `<html>`). É o local ideal para declarar **variáveis globais** (CSS Custom Properties), pois ficam disponíveis para **todos os elementos** da página.

### O que são variáveis CSS?

Variáveis CSS (ou *custom properties*) permitem armazenar valores reutilizáveis. A sintaxe é:

```css
--nome-da-variavel: valor;
```

Para **usar** a variável:

```css
color: var(--ifpb-verde);
```

### Análise das variáveis

| Variável | Valor | Uso |
|---|---|---|
| `--ifpb-verde` | `#009639` | Cor principal da marca IFPB |
| `--ifpb-vermelho` | `#E31D1A` | Destaque e bordas de ênfase |
| `--ifpb-cinza-escuro` | `#4d4d4d` | Textos secundários e rodapé |
| `--ifpb-cinza-claro` | `#f4f4f4` | Fundo suave da página |
| `--ifpb-branco` | `#ffffff` | Fundos de cards e textos claros |
| `--sombra` | `0 4px 8px rgba(...)` | Sombra padrão reutilizável |
| `--transicao` | `all 0.3s ease` | Animação suave padrão |

### Entendendo `rgba()`

```css
rgba(0, 0, 0, 0.1)
```

- `rgba` = Red, Green, Blue, **Alpha** (transparência)
- Valores de cor: de `0` a `255`
- Alpha: de `0` (totalmente transparente) a `1` (totalmente opaco)
- `rgba(0, 0, 0, 0.1)` = preto com 10% de opacidade → sombra discreta

### Entendendo a `--sombra`

```css
--sombra: 0 4px 8px rgba(0, 0, 0, 0.1);
```

A propriedade `box-shadow` aceita os valores:

```
deslocamento-x | deslocamento-y | desfoque | cor
      0        |      4px       |   8px    | rgba(0,0,0,0.1)
```

---

## 2. Unidades de Medida em CSS

Antes de analisar os seletores, é essencial entender as **unidades** utilizadas no código.

### 2.1 Unidades Absolutas

| Unidade | Nome | Uso recomendado |
|---|---|---|
| `px` | Pixel | Valores fixos: bordas, sombras, ícones |
| `pt` | Ponto | Impressão |
| `cm`, `mm` | Centímetro/Milímetro | Impressão |

```css
border-radius: 4px;   /* fixo, não escala */
gap: 20px;            /* espaço fixo entre itens */
```

> ⚠️ `px` é preciso, mas **não se adapta** ao tamanho da tela ou às preferências do usuário.

---

### 2.2 Unidades Relativas à Fonte

| Unidade | Referência | Exemplo |
|---|---|---|
| `rem` | Tamanho da fonte do `<html>` (padrão: 16px) | `1rem = 16px` |
| `em` | Tamanho da fonte do **elemento pai** | Pode acumular em elementos aninhados |

```css
font-size: 0.9rem;   /* 0.9 × 16px = 14.4px */
font-size: 2.5rem;   /* 2.5 × 16px = 40px */
padding: 1rem;       /* 16px — escala com preferências do usuário */
```

**Por que usar `rem` em vez de `px`?**

- Respeita o zoom do navegador
- Respeita configurações de acessibilidade do sistema operacional
- Facilita reescalonamento global (basta alterar o `font-size` do `html`)

---

### 2.3 Unidades Relativas à Viewport

| Unidade | Significado |
|---|---|
| `vw` | 1% da **largura** da janela do navegador |
| `vh` | 1% da **altura** da janela do navegador |
| `vmin` | 1% do menor entre vw e vh |
| `vmax` | 1% do maior entre vw e vh |

```css
min-height: 100vh;  /* altura mínima = 100% da altura da janela */
```

---

### 2.4 Unidades Percentuais

```css
width: 100%;
```

- `%` é **relativo ao elemento pai**
- `width: 100%` = tão largo quanto o elemento que o contém

---

## 3. Layout Base — `html` e `body`

```css
html {
    height: 100%;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: var(--ifpb-cinza-claro);
    color: #333;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    margin: 0;
}
```

### Propriedades explicadas

#### `html { height: 100% }`
Define que o `<html>` ocupa 100% da altura disponível do navegador. Isso serve de **base** para que elementos filhos (como `body`) possam usar `height: 100%` como referência.

#### `font-family`
Define a **família tipográfica** com uma lista de fontes em ordem de preferência (*fallback*):

```
'Segoe UI' → Tahoma → Geneva → Verdana → sans-serif (genérica)
```

O navegador tenta cada fonte da lista até encontrar uma instalada no sistema.

#### `background-color` e `color`
- `background-color`: cor de fundo do elemento
- `color`: cor do **texto** (herdada pelos elementos filhos)

#### `display: flex` + `flex-direction: column`
Transforma o `body` em um **container Flexbox vertical**. Isso é essencial para o padrão **"footer grudado no rodapé"**:

```
┌────────────────┐
│     <nav>      │
├────────────────┤
│    <header>    │
├────────────────┤
│     <main>     │  ← cresce para preencher o espaço
│   (flex: 1)    │
├────────────────┤
│    <footer>    │
└────────────────┘
```

#### `min-height: 100vh`
Garante que o `body` tenha **no mínimo** a altura total da janela. Se o conteúdo for menor, o body se estende assim mesmo — mantendo o footer no fundo.

> **`height` vs `min-height`:**
> - `height: 100vh` — força a altura exata; se o conteúdo for maior, haverá overflow
> - `min-height: 100vh` — define um **mínimo**; o elemento pode crescer além disso ✅

#### `margin: 0`
Remove a margem padrão do navegador (browsers adicionam `margin: 8px` ao `body` por padrão).

---

## 4. Navegação — `nav`

```css
nav {
    background-color: var(--ifpb-verde);
    padding: 1rem;
    display: flex;
    justify-content: center;
    gap: 20px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}
```

### `padding`

O `padding` cria **espaçamento interno** (entre o conteúdo e a borda do elemento):

```
padding: 1rem;  → aplica 1rem nos 4 lados
```

Pode ser especificado individualmente:

```css
padding: 10px 20px;          /* vertical | horizontal */
padding: 10px 20px 5px 15px; /* top | right | bottom | left */
padding-top: 10px;
```

### `justify-content: center`
No Flexbox, alinha os itens **no eixo principal** (horizontal, neste caso) ao centro.

| Valor | Efeito |
|---|---|
| `flex-start` | Alinha ao início |
| `flex-end` | Alinha ao fim |
| `center` | Centraliza |
| `space-between` | Distribui com espaço entre os itens |
| `space-around` | Distribui com espaço ao redor |

### `gap: 20px`
Define o **espaço entre os itens** flex (ou grid). Mais moderno e limpo que usar `margin` nos filhos.

---

### Links da navegação

```css
nav a {
    color: var(--ifpb-branco);
    text-decoration: none;
    font-weight: bold;
    text-transform: uppercase;
    font-size: 0.9rem;
    padding: 5px 15px;
    border-radius: 4px;
    transition: var(--transicao);
}
```

| Propriedade | Valor | Efeito |
|---|---|---|
| `text-decoration: none` | — | Remove o sublinhado padrão dos links |
| `font-weight: bold` | — | Texto em negrito |
| `text-transform: uppercase` | — | Converte para MAIÚSCULAS via CSS |
| `font-size: 0.9rem` | 14.4px | Texto ligeiramente menor que o padrão |
| `padding: 5px 15px` | — | Área clicável maior (5px vertical, 15px horizontal) |
| `border-radius: 4px` | — | Cantos levemente arredondados |
| `transition: all 0.3s ease` | — | Animação suave em todas as propriedades |

### Efeito hover

```css
nav a:hover {
    background-color: rgba(255, 255, 255, 0.2);
    transform: translateY(-2px);
}
```

- `rgba(255, 255, 255, 0.2)`: fundo branco com 20% de opacidade ao passar o mouse
- `transform: translateY(-2px)`: move o elemento **2px para cima** — cria efeito de "levantar"

> O `transition` definido anteriormente faz com que essa mudança aconteça suavemente em 0.3 segundos.

---

## 5. Cabeçalho — `header`

```css
header {
    background-color: var(--ifpb-branco);
    padding: 40px 20px;
    text-align: center;
    border-bottom: 5px solid var(--ifpb-vermelho);
}

header h1 {
    color: var(--ifpb-verde);
    font-size: 2.5rem;
    margin: 0;
}
```

### `border-bottom`

Aplica borda **apenas na parte inferior**:

```
border-bottom: espessura | estilo | cor
               5px       | solid  | #E31D1A
```

Estilos de borda: `solid`, `dashed`, `dotted`, `double`, `none`

### `font-size: 2.5rem`
`2.5 × 16px = 40px` — título grande e de destaque.

### `margin: 0` no `h1`
Browsers adicionam margens padrão aos títulos (`h1`–`h6`). `margin: 0` remove esse espaço indesejado dentro do header.

---

## 6. Conteúdo Principal — `main` e `.conteudo`

```css
main {
    flex: 1 0 auto;
    max-width: 1000px;
    margin: 40px auto;
    padding: 0 20px;
    width: 100%;
}
```

### `flex: 1 0 auto` — A propriedade mais importante desta seção

`flex` é um atalho para três propriedades:

```
flex: flex-grow | flex-shrink | flex-basis
       1        |      0      |    auto
```

| Propriedade | Valor | Significado |
|---|---|---|
| `flex-grow: 1` | 1 | **Cresce** para preencher o espaço disponível |
| `flex-shrink: 0` | 0 | **Não encolhe** abaixo do seu tamanho natural |
| `flex-basis: auto` | auto | Tamanho base é determinado pelo conteúdo |

> 💡 Este é o segredo do **footer fixo no rodapé**: o `main` absorve todo o espaço vazio entre o header e o footer.

### `max-width: 1000px`
Limita a largura máxima do conteúdo. Em telas grandes, o texto não fica espalhado por toda a largura — melhora a legibilidade.

### `margin: 40px auto`
```
margin: vertical | horizontal
        40px     |   auto
```

`auto` nas margens horizontais = **centraliza** o elemento (funciona quando o elemento tem largura definida).

### `width: 100%`
Garante que o `main` ocupe toda a largura do pai, mas respeitando o `max-width: 1000px`.

---

### `.conteudo` — Card de conteúdo

```css
.conteudo {
    background: var(--ifpb-branco);
    padding: 40px;
    border-radius: 8px;
    box-shadow: var(--sombra);
}
```

| Propriedade | Efeito |
|---|---|
| `border-radius: 8px` | Cantos arredondados — visual de "card" |
| `box-shadow: var(--sombra)` | Sombra suave reutilizando a variável definida no `:root` |

---

### Listas dentro de `.conteudo`

```css
.conteudo ul {
    list-style: none;
    padding: 0;
}

.conteudo li {
    margin-bottom: 15px;
    font-size: 1.1rem;
    line-height: 1.6;
    border-bottom: 1px solid #f0f0f0;
    padding-bottom: 15px;
}

.conteudo li:last-child {
    border-bottom: none;
    margin-bottom: 0;
}
```

#### `list-style: none`
Remove os marcadores padrão das listas (`•`, números, etc.).

#### `line-height: 1.6`
Define a **altura da linha** — o espaço entre linhas de texto. Valor **sem unidade** = múltiplo do `font-size` atual:

```
1.1rem × 1.6 = ~28px de altura de linha
```

> Valores entre `1.4` e `1.8` são ideais para **leitura confortável**.

#### `:last-child`
Pseudo-classe que seleciona o **último filho** de seu pai. Usado aqui para remover a borda do último item da lista, evitando borda dupla ou sobrando no final.

---

### Elemento `strong` dentro de `li`

```css
.conteudo li strong {
    color: var(--ifpb-cinza-escuro);
    min-width: 180px;
    display: inline-block;
}
```

#### `display: inline-block`
O `<strong>` é naturalmente `inline` — não aceita `width`. Ao mudar para `inline-block`, ele passa a aceitar dimensões:

| display | Aceita width/height? | Quebra linha? |
|---|---|---|
| `inline` | ❌ | ❌ |
| `block` | ✅ | ✅ |
| `inline-block` | ✅ | ❌ |

#### `min-width: 180px`
Define uma **largura mínima** para o `strong`. Isso alinha visualmente os rótulos de uma lista de definições:

```
Nome:        João Silva
Matrícula:   20241234
Curso:       Informática
```

---

## 7. Rodapé — `footer`

```css
footer {
    flex-shrink: 0;
    background-color: var(--ifpb-cinza-escuro);
    color: var(--ifpb-branco);
    text-align: center;
    padding: 20px;
    font-size: 0.9rem;
}
```

### `flex-shrink: 0`
Impede que o footer seja **comprimido** pelo Flexbox. Sem isso, em telas pequenas, o footer poderia encolher de forma indesejada.

> Lembre: no `body` temos `display: flex; flex-direction: column`. O footer é um **item flex**, e `flex-shrink: 0` garante que ele mantenha seu tamanho original.

---

## 8. Erros no Código Original

O código original contém alguns **erros de digitação**. Identifique-os como exercício:

| Linha com erro | Problema | Correção |
|---|---|---|
| `--ifpb-verde: #0096 state-39` | Valor de cor inválido | `--ifpb-verde: #009639` |
| `background-color: var(--ifpb fly-cinza-claro)` | Espaço no nome da variável | `var(--ifpb-cinza-claro)` |
| `font-weight examine: bold` | Propriedade inexistente | `font-weight: bold` |
| `color: var(--_ifpb-cinza-escuro)` | Underscore extra no nome | `var(--ifpb-cinza-escuro)` |
| `padding: 20px; hospital-size: 0.9rem` | Propriedade inexistente | `padding: 20px; font-size: 0.9rem` |

> 🧠 **Dica:** O navegador simplesmente **ignora** propriedades ou valores inválidos, sem exibir erro na página. Use as ferramentas de desenvolvedor (F12) para identificar problemas.

---

## 9. Resumo das Formas de Dimensionamento

```
┌─────────────────────────────────────────────────────────────────┐
│                   UNIDADES E DIMENSIONAMENTO                    │
├──────────────┬──────────────────────────────────────────────────┤
│  px          │ Fixo. Ideal para bordas, sombras, ícones         │
│  rem         │ Relativo à fonte do <html>. Ideal para textos    │
│  em          │ Relativo à fonte do pai. Cuidado com cascata     │
│  %           │ Relativo ao elemento pai. Ideal para layouts     │
│  vh / vw     │ Relativo à janela. Ideal para seções de tela     │
├──────────────┴──────────────────────────────────────────────────┤
│                   FLEXBOX PARA LAYOUT                           │
├─────────────────────────────────────────────────────────────────┤
│  flex-grow    │ Quanto o item CRESCE para preencher espaço      │
│  flex-shrink  │ Quanto o item ENCOLHE quando falta espaço       │
│  flex-basis   │ Tamanho BASE antes de crescer/encolher          │
│  flex: 1 0 auto → Cresce, não encolhe, tamanho automático       │
├─────────────────────────────────────────────────────────────────┤
│                   PADRÃO FOOTER NO RODAPÉ                       │
├─────────────────────────────────────────────────────────────────┤
│  body: display:flex; flex-direction:column; min-height:100vh    │
│  main: flex: 1 0 auto  (ocupa todo o espaço restante)           │
│  footer: flex-shrink: 0  (não encolhe)                          │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✅ Exercícios Práticos

1. **Altere as variáveis** de cor no `:root` e observe como toda a página muda de uma vez.
2. **Substitua `rem` por `px`** no `font-size` dos links e observe a diferença ao aumentar o zoom do navegador.
3. **Remova o `flex: 1 0 auto`** do `main` e veja o que acontece com o footer quando o conteúdo é pequeno.
4. **Adicione `width: 100%`** e **`box-sizing: border-box`** ao footer e explique por que não há overflow horizontal.
5. **Crie uma nova variável** `--ifpb-amarelo: #FFD700` no `:root` e use-a em algum elemento.

---

*Material didático elaborado para a disciplina de SIGWeb — CST em Geoprocessamento - IFPB*
