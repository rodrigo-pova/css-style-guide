# Guia de estilo CSS / Sass Airbnb

_Uma abordagem mais razoável para CSS e Sass_

## Índice

  1. [Terminologia](#terminologia)
    - [Regras](#regras)
    - [Seletores](#seletores)
    - [Propriedades](#propriedades)
  1. [CSS](#css)
    - [formatação](#formatação)
    - [Comentários](#comentarios)
    - [OOCSS e BEM](#oocss-e-bem)
    - [Seletores ID](#seletores-id)
    - [JavaScript hooks](#javascript-hooks)
    - [Border](#border)
  1. [Sass](#sass)
    - [Sintaxe](#sintaxe)
    - [Ordenação](#ordenação-de-declaração-de-propriedades)
    - [Variáveis](#variáveis)
    - [Mixins](#mixins)
    - [Extend](#extend)
    - [Seletores aninhados](#seletores-aninhados)
  1. [Traduções](#traduções)

## Terminologia

### Regras

Uma “declaração de regra” é o nome dado ao seletor (ou grupo de seletores) acompanhados de um grupo de propriedades. Segue um exemplo:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Seletores

Em uma declaração de regra, "seletores" são os trechos que determinam quais elementos na árvore de DOM serão estilizados pelas propriedades definidas. Seletores podem coincidir com elementos HTML, assim como classes, ID ou qualquer um de seus atributos. Seguem exemplos de seletores:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Propriedades

Finalmente, propriedades são os elementos selecionados de uma regra de declaração. Propriedades são pares de chave-valor, onde uma regra de declaração pode conter uma ou mais declarações de propriedades. Declarações de propriedades são mostradas a seguir:

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

## CSS

### Formatação

* Use _"soft tabs"_ (2 espaços) para indentação.
* Prefira _dashes_ `(-)` no lugar de _camelCase_ em nomes de classes.
  - _Underscores_ `(_)` e _PascalCase_ podem ser utilizados caso você use BEM (veja [OOCSS e BEM](#oocss-e-bem) abaixo).
* Não use seletores ID.
* Quando usar múltiplos seletores em uma regra de declaração, ponha cada um em uma própria linha.
* Coloque um espaço antes da abertura de chaves `{` em declaração de regras.
* Em propriedades, coloque um espaço depois, mas não antes do caractere `:` (dois-pontos).
* Coloque chave de fechamento `}` de uma regra de declaração em uma nova linha.
* Coloque linhas em branco entre declarações de regra.

**Ruim**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Bom**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Comentários

* Prefira comentários de linha (`//` em Sass) a blocos de comentários.
* Prefira comentários em linhas próprias. Evite comentários no final da linha.
* Escreva comentários detalhados para códigos que não são auto-documentados:
  - Usos do _z-index_
  - Compatibilidade ou _hacks_ específicos de navegadores

### OOCSS e BEM

Nós incentivamos algumas combinações de OOCSS e BEM por três razões:

  * Ajuda a criar relações claras e estritas entre CSS e HTML
  * Nos ajuda a criar componentes reutilizáveis e que podem ser usados em composição
  * Permite menor aninhamento e especificidade
  * Ajuda na construção de estilos escaláveis

**OOCSS**, ou _“Object Oriented CSS”_, (CSS orientado a objetos) é uma abordagem para escrita de CSS que encoraja você a pensar sobre seus estilos como uma coleção de "objetos": trechos repetíveis e reutilizáveis que podem ser usados de forma independente em toda uma página.

  * [OOCSS wiki](https://github.com/stubbornella/oocss/wiki) de Nicole Sullivan
  * [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/) de Smashing Magazine

**BEM**, ou _“Block-Element-Modifier”_, é uma convenção de nomes para classes em HTML e CSS. Foi originalmente desenvolvida por Yandex com grandes bases de códigos e escalabilidade em mente, e pode servir como um sólido conjunto de orientações para implementação de OOCSS.

  * [BEM 101](https://css-tricks.com/bem-101/) de CSS Trick
  * [Introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) de Harry Roberts

Nós recomendamos um variante do BEM com "blocos" em formato _PascalCase_, que funciona particularmente bem quando combinado com componentes (ex. React). _Underscores_ e _dashes_ ainda são utilizados para modificadores e filhos.

**Exemplo**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` é um “bloco” e representa um componente de alto nível
  * `.ListingCard__title` é um “elemento” e representa um descendente de `.ListingCard` que ajuda a compor o bloco como um todo.
  * `.ListingCard--featured` é um "modificador" e representa um estado diferente ou variação do bloco `.ListingCard`.

### Seletores ID

Enquanto é possível selecionar elementos por ID em CSS, isto deveria ser considerado um antipadrão. Seletores ID introduzem um nível alto de [especificidade](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) para suas declarações de regras e eles não são reutilizáveis.

Para mais detalhes, leia o seguinte [artigo do CSS Wizardry](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) sobre como lidar com especificidade.

### JavaScript hooks

Evite vincular a mesma classe tanto em seu CSS como no JavaScript. Combinar os dois muitas vezes resulta, no mínimo, em tempo perdido durante refatoração, quando um desenvolvedor deve fazer referência cruzada a cada classe que está alterando, e no pior dos casos, em medo de fazer alterações pelo temor de quebrar alguma funcionalidade.

Recomendamos a criação de classes específicas JavaScript para vinculação, com prefixo `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Border

Utilizar `0` ao invés de `none` para especificar que um estilo não tem borda.

**Ruim**

```css
.foo {
  border: none;
}
```

**Bom**

```css
.foo {
  border: 0;
}
```

## Sass

### Sintaxe

* Use sintaxe `.scss`, nunca a original `.sass`
* Ordene as declarações em CSS regular e `@include` logicamente (veja abaixo)

### Ordenação de declarações de propriedades

1. Declaração de propriedades

    Listar todas as declarações de propriedades padrão, tudo que não seja  `@include` ou um seletor aninhado.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. Declarações `@include`

    Agrupar `@include`s no final torna mais fácil a leitura do seletor inteiro.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Seletores aninhados

    Seletores aninhados, _se necessários_, vão no final, e nada deve vir depois deles. Adicionar espaços em branco entre suas declarações de regras e seletores aninhados, bem como entre seletores aninhados adjacentes. Aplicar as mesmas diretrizes acima para seus seletores aninhados.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### Variáveis

Prefira nomes de variáveis em _dash-case_ (ex. `$my-variable`) em vez de _camelCase_ ou _snake\_case_. É aceitável adicionar um _"underscore"_ como prefixo em nomes de variáveis que se destinam a ser usadas somente dentro do arquivo atual (ex. `$_my-variable`).

### Mixins

_Mixins_ devem ser usados para aplicar _[DRY](https://pt.wikipedia.org/wiki/Don%27t_repeat_yourself)_ ao seu código, adicionar clareza ou abstrair complexidade -- da mesma forma que usar funções bem nomeadas. _Mixins_ que não aceitam nenhum argumento podem ser úteis para isto, mas note que se você não compactar seu _payload_ (ex. gzip), isto pode contribuir para duplicação de código desnecessário nos estilos resultantes.

### Extend

`@extend` deve ser evitado porque possui comportamento não-intuitivo e potencialmente perigoso, especialmente quando usado em seletores aninhados. Mesmo estender seletores _placeholder_ de nível superior pode causar problemas se a ordem dos seletores mudar mais tarde (ex. se eles estão em outros arquivos e a ordem dos mesmos variar). Usar _gzip_ lida com a maior parte das economias que você teria ganho usando `@extend`, e você ainda pode tornar seus estilos menos repetitivos muito bem com _mixins_.

### Seletores aninhados

**Não aninhe seletores em mais de três níveis de profundidade!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

Quando os seletores se tornam muito longos, você provavelmente está escrevendo CSS que é:

* Fortemente acoplado ao HTML (frágil) *—OU—*
* Excessivamente específico (poderoso) *—OU—*
* Não reutilizável

Novamente: **nunca aninhe seletores ID!**

Se você precisar utilizar um seletor ID (e você realmente deve evitar fazer isto), eles nunca devem estar aninhados. Se você estiver fazendo isto, revise sua marcação ou reflita sobre por que tanta especificidade é necessária. Se você estiver escrevendo HTML e CSS bem formados, você **nunca** deve precisar usar isso.

## Traduções

  Este guia também está disponível em outros idiomas:

  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Indonésio**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinês (Tradicional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinês (Simplificado)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **Francês**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japonês**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Coreano**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Português (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russo**: [rtplv/airbnb-css-ru](https://github.com/rtplv/airbnb-css-ru)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Espanhol**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamita**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italiano**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **Alemão**: [tderflinger/css-styleguide](https://github.com/tderflinger/css-styleguide)

**[⬆ Voltar para o início](#Índice)**
