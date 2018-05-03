## Documentation BEM / Unités / [SCSS](#scss) 

* => __Block__
* => __Element__
* => __Modifier__



 BEM apporte une convention de nommage des classes CSS.
  Ce qui compose un page ou une application Web peut toujours être rangé dans une arborescence de blocs, d'éléments et de modificateurs.
 </br>
 </br>
__Block__
</br>
</br>
Un bloc est une entité indépendante, une « brique » de l'application ou de la page Web. Un bloc forme son propre contexte autonome.

__Element__
</br>
</br>
Un élément est une partie d'un bloc

__Modifier__
</br>
</br>
Un modificateur est une propriété qui sert à créer des variantes, pour faire des modifications minimes comme changer des couleurs. Il existe des modificateurs de blocs et des modificateurs d'éléments.

_La méthodologie BEM établit ensuite trois règles essentielles :_
* Les blocs et les éléments doivent chacun avoir un nom unique, lequel sera utilisé comme classe CSS ;
* Les sélecteurs CSS ne doivent pas utiliser les noms des éléments HTML (pas de .menu td) ;


```HTML

block-name
block-name_modifier_name
block-name__element-name
block-name__element-name_modifier_name

```


__Le code html:__
```html
<div class="search-box search-box_light">
  <!-- (input field here) -->
  <button class="search-box__btn search-box__btn_max_visible">Search</button>
</div>

```
__Le code css:__
```css
.search-box {
  height: 300px;
  width: 300px;
}
.search-box_light {
  background-color: #DEF;
  color: #777;
}
.search-box__btn {
  padding: 4px;
}
.search-box__btn_max_visible {
  font-weight: bold;
}

```

## Pseudo attribut :: after & :: before

### Attention
* Il est obligatoire d'avoir un `content:''` afin que vos after/ before s'affichent.
* Vous pouvez leur donner une taille, une position (absolute par rapport à son parent)
* Essentiellement utilisé pour de la décoration

```html
<section class="cover">
<h2 class="cover__title">Présentation</h2>
</section>
```

```css
/* Si je veux des ornements en haut et a gauche d'un titre */

.cover{
&__title{
  font-size: 24px;
  color: #bbb;
  text-align: center;
  position: relative;
  &::before,
  &::after{
    content:'';
    position: absolute;
    top:0;
    display: block;
    width: 50px;
    height: 50px;
    background: green;
  }
  &::before{
    left: 0;
  }
  &::after{
    right: 0;
  }
}
}

```

## Les unités


### REM

L'unité de mesure REM est basée sur la taille de l'élément racine du HTML.
Par défaut, la taille du <html> est de 16px, ce qui veut dire que `1rem = 16px`.
Pour éviter de devoir faire des calculs afin de respecter les tailles relatives à votre maquette,
vous pouvez ré-écrire cette `font-size`afin que `1rem = 10px`

Les proportions et tailles vont s'adapter à la taille de l'écran en cas de zoom, ce qui est impossible en px.

```css

html{
/*
override de la valeur par défaut
afin que 1rem = 10px;
*/
font-size: 62.5%; (passage de 16px a 10 pixel)
}

.mainTitle{
font-size: 2.4rem; (24 pixel)
}

.cover{
width: 32rem; (320 pixel)
}

```

### EM

Le `EM` à contrario du `REM`se base quant à lui sur la taille de son parent direct. (pas son grand-parent).

Cette unité représente la `font-size` calculée de l'élément. Si utilisée avec la propriété `font-size`, elle représente la taille de police héritée de l'élément.

```css

html{
font-size: 100%;
}

.cover{
height: 100px;
&-title{
  font-size: .8em;
}
&-subTitle{
  font-size: .6em;
}
}
```

### VW Sizing (unités)

#### VW(idth) / VH(eigth) / vmin / vmax - Sizing unités

Elles permettent entre autres d'avoir une taille de police et des colonnes variables selon la résolution de l'écran. Lors de la réduction du corps de la fenêtre votre titre se réduira suivant le schéma initialement prévu.

Les valeurs utilisées peuvent être quelque peu déroutantes si vous n'avez pas utilisé ces unités avant. 1VH représente 1% de la fenêtre courante (la zone de contenu de la fenêtre du navigateur) de hauteur, au lieu de 100% comme vous pouvez vous y attendre.

Donc si vous voulez un élément à la hauteur de votre fenêtre, vous devrez le mettre à 100vh. Bien sûr VW fonctionne exactement de la même manière que les unités de VH.

En résumé:

* 1vw = 1% de la largeur de la fenêtre

* 1VH = 1% de la hauteur de la fenêtre

* 1vmin = 1vw ou 1VH, soit la valeur la plus petite

* 1vmax = 1vw ou 1VH, soit la valeur la plus grande

```html
zone > section {
    height: 80vh;
    width: 80vw;
}
```
Ceci définit la hauteur à 80% de la hauteur de la fenêtre, et la largeur à 80% de la largeur de la fenêtre.

<a id="scss">Scss</a>

* #### Variables

__=> SCSS__
```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font-family: $font-stack;
  color: $primary-color;
}
```

__=> CSS__
```css
body {
  font-family: Helvetica;
  color: #333;
}
```

* #### Nesting

Le Nesting permet de respecter la hiérarchie du code html

__=> SCSS__
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

__=> CSS__
```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

* #### Imports


__=> SCSS__
```scss
@import 'reset';

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}

```

__=> CSS__
```css
html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  font-family: Helvetica, sans-serif;
  background-color: #efefef;
}
```

*  ### Mixins


 __=> CSS__

```css
.button {
  padding: 14px 0;
  min-width: 100%;
  border-radius: 4px;
  outline: none;
  background: #4D61D6;
  color: #fff;
  text-align: center;
  letter-spacing: .9px;
  transition: background .3s ease;
}
```
 __=> SCSS__

```scss

@mixin generic-button {
  padding: 14px 0;
  min-width: 100%;
  border-radius: 4px;
  outline: none;
  background: #4D61D6;
  color: #fff;
  text-align: center;
  letter-spacing: .9px;
  transition: background .3s ease;
}

button {
  @include generic-button;
}

```




