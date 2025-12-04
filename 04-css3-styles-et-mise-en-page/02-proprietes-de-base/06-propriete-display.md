🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.6 Propriété display : block, inline, inline-block, none

## Introduction

La propriété `display` est l'une des plus importantes en CSS. Elle détermine **comment un élément est affiché** et **comment il se comporte** dans le flux de la page.

Comprendre `display` est essentiel car elle contrôle :
- Si un élément prend toute la largeur disponible ou seulement celle dont il a besoin
- Si plusieurs éléments peuvent se placer côte à côte
- Si on peut définir une largeur et hauteur
- Comment l'élément interagit avec les marges et le padding

---

## Les valeurs de display par défaut

Chaque élément HTML a une valeur `display` par défaut définie par le navigateur.

### Éléments block par défaut

Ces éléments prennent toute la largeur disponible et commencent sur une nouvelle ligne :

```html
<div>, <p>, <h1> à <h6>, <ul>, <ol>, <li>,
<section>, <article>, <header>, <footer>, <nav>,
<form>, <table>, <blockquote>, <pre>, <hr>
```

### Éléments inline par défaut

Ces éléments prennent seulement la largeur nécessaire et restent sur la même ligne :

```html
<span>, <a>, <strong>, <em>, <b>, <i>,
<img>, <input>, <button>, <label>,
<code>, <small>, <abbr>
```

**Important** : Vous pouvez changer la valeur `display` de n'importe quel élément avec CSS !

---

## display: block

### Caractéristiques

Les éléments `block` ont ces comportements :

```css
.element-block {
  display: block;
}
```

**Comportements :**
1. ✅ Commence sur une **nouvelle ligne**
2. ✅ Prend **toute la largeur disponible** (100% par défaut)
3. ✅ Peut avoir `width` et `height`
4. ✅ Respecte tous les `margin` (haut, bas, gauche, droite)
5. ✅ Respecte tous les `padding`
6. ✅ Empile verticalement les éléments (un sous l'autre)

### Visualisation

```html
<div class="block">Bloc 1</div>
<div class="block">Bloc 2</div>
<div class="block">Bloc 3</div>
```

```css
.block {
  display: block;
  background-color: lightblue;
  padding: 10px;
  margin-bottom: 10px;
}
```

**Rendu visuel :**
```
┌─────────────────────────────────────┐
│          Bloc 1                     │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│          Bloc 2                     │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│          Bloc 3                     │
└─────────────────────────────────────┘
```

Chaque bloc prend toute la largeur et est sur sa propre ligne.

### Exemples pratiques

```css
/* Transformer un lien en bouton block */
.button-block {
  display: block;
  width: 200px;        /* On peut définir une largeur */
  padding: 15px;
  text-align: center;
  background-color: #3498DB;
  color: white;
  text-decoration: none;
}

/* Transformer une image en block */
img {
  display: block;
  max-width: 100%;     /* Image responsive */
  height: auto;
}

/* Liste horizontale en block */
.nav-item {
  display: block;
  padding: 10px 20px;
  border-bottom: 1px solid #ddd;
}
```

### Cas d'usage typiques

```css
/* Centrer une image */
img {
  display: block;
  margin: 0 auto;      /* Nécessite display: block */
}

/* Navigation verticale */
.nav-vertical a {
  display: block;
  padding: 10px;
}

/* Sections de page */
section {
  display: block;      /* Déjà block par défaut */
  padding: 40px 0;
}
```

---

## display: inline

### Caractéristiques

Les éléments `inline` ont ces comportements :

```css
.element-inline {
  display: inline;
}
```

**Comportements :**
1. ✅ Reste sur la **même ligne** que les autres éléments inline
2. ✅ Prend **seulement la largeur du contenu**
3. ❌ **N'accepte PAS** `width` et `height` (ignorés)
4. ⚠️ Accepte `margin-left` et `margin-right`, mais **ignore** `margin-top` et `margin-bottom`
5. ✅ Respecte tous les `padding` (mais ne "pousse" pas verticalement les autres éléments)
6. ✅ Suit le flux du texte (comme des mots dans une phrase)

### Visualisation

```html
<span class="inline">Inline 1</span>
<span class="inline">Inline 2</span>
<span class="inline">Inline 3</span>
```

```css
.inline {
  display: inline;
  background-color: lightgreen;
  padding: 5px;
}
```

**Rendu visuel :**
```
┌────────────────────────────────────────────┐
│ [Inline 1] [Inline 2] [Inline 3]           │
└────────────────────────────────────────────┘
```

Les éléments sont côte à côte, sur la même ligne.

### Exemples pratiques

```css
/* Mise en évidence dans le texte */
.highlight {
  display: inline;     /* Déjà inline par défaut pour span */
  background-color: yellow;
  padding: 2px 4px;
}

/* Lien dans un paragraphe */
a {
  display: inline;     /* Déjà inline par défaut */
  color: #3498DB;
  text-decoration: underline;
}

/* Badge inline */
.badge {
  display: inline;
  padding: 2px 8px;
  background-color: #E74C3C;
  color: white;
  border-radius: 3px;
  font-size: 0.75em;
}
```

### Limitations importantes

```css
/* ❌ N'a AUCUN effet sur un élément inline */
.inline-element {
  display: inline;
  width: 200px;        /* IGNORÉ */
  height: 100px;       /* IGNORÉ */
  margin-top: 20px;    /* IGNORÉ */
  margin-bottom: 20px; /* IGNORÉ */
}

/* ✅ Fonctionne */
.inline-element {
  display: inline;
  margin-left: 10px;   /* Fonctionne */
  margin-right: 10px;  /* Fonctionne */
  padding: 5px;        /* Fonctionne */
}
```

### Comportement du padding sur inline

Le padding fonctionne sur les éléments inline, mais de façon particulière :

```css
.inline-padded {
  display: inline;
  padding: 20px;       /* Appliqué, mais... */
  background-color: lightblue;
}
```

**Important** : Le padding est visible, mais il ne "pousse" pas les éléments au-dessus et en-dessous. Il peut donc se superposer à d'autres éléments.

---

## display: inline-block

### Caractéristiques

`inline-block` combine le meilleur des deux mondes :

```css
.element-inline-block {
  display: inline-block;
}
```

**Comportements :**
1. ✅ Reste sur la **même ligne** (comme inline)
2. ✅ Peut avoir `width` et `height` (comme block)
3. ✅ Respecte **tous** les `margin` (comme block)
4. ✅ Respecte **tous** les `padding` (comme block)
5. ✅ Prend seulement la largeur nécessaire (ou celle définie)
6. ✅ Permet de placer des éléments côte à côte avec dimensions contrôlées

### Visualisation

```html
<div class="inline-block">Boîte 1</div>
<div class="inline-block">Boîte 2</div>
<div class="inline-block">Boîte 3</div>
```

```css
.inline-block {
  display: inline-block;
  width: 150px;
  height: 100px;
  background-color: lightcoral;
  padding: 10px;
  margin: 5px;
  vertical-align: top;
}
```

**Rendu visuel :**
```
┌──────────┐ ┌──────────┐ ┌──────────┐
│ Boîte 1  │ │ Boîte 2  │ │ Boîte 3  │
│          │ │          │ │          │
└──────────┘ └──────────┘ └──────────┘
```

Les boîtes sont côte à côte ET on peut contrôler leurs dimensions.

### Exemples pratiques

```css
/* Boutons côte à côte */
.button {
  display: inline-block;
  padding: 10px 20px;
  margin: 5px;
  background-color: #3498DB;
  color: white;
  text-decoration: none;
  border-radius: 4px;
}

/* Grille de cartes simple */
.card {
  display: inline-block;
  width: 300px;
  padding: 20px;
  margin: 10px;
  border: 1px solid #ddd;
  vertical-align: top;  /* Aligner en haut */
}

/* Navigation horizontale avec espacement */
.nav-link {
  display: inline-block;
  padding: 10px 15px;
  margin: 0 5px;
}

/* Icône + texte alignés */
.icon-text {
  display: inline-block;
  vertical-align: middle;
}
```

### Astuce : vertical-align

Avec `inline-block`, vous pouvez utiliser `vertical-align` pour aligner verticalement :

```css
.item {
  display: inline-block;
  vertical-align: top;      /* Aligner en haut */
  vertical-align: middle;   /* Aligner au milieu */
  vertical-align: bottom;   /* Aligner en bas */
}
```

### Problème : Espace indésirable

⚠️ Les éléments `inline-block` peuvent avoir un petit espace entre eux à cause des espaces dans le HTML :

```html
<!-- Espace créé entre les divs à cause du retour à la ligne -->
<div class="box">1</div>
<div class="box">2</div>
<div class="box">3</div>
```

**Solutions :**

```css
/* Solution 1 : font-size: 0 sur le parent */
.container {
  font-size: 0;
}
.box {
  font-size: 1rem;  /* Rétablir la taille */
}

/* Solution 2 : margin négatif */
.box {
  margin-right: -4px;
}

/* Solution 3 : Utiliser Flexbox à la place */
.container {
  display: flex;
  gap: 10px;
}
```

---

## display: none

### Caractéristiques

```css
.element-hidden {
  display: none;
}
```

**Comportements :**
1. ✅ L'élément est **complètement retiré** du flux de la page
2. ✅ Ne prend **aucune place** (comme s'il n'existait pas)
3. ✅ N'est **pas visible**
4. ✅ Les autres éléments se repositionnent comme si l'élément n'était pas là
5. ⚠️ L'élément existe toujours dans le DOM (accessible en JavaScript)

### Visualisation

```html
<div>Élément visible 1</div>
<div class="hidden">Élément caché</div>
<div>Élément visible 2</div>
```

```css
.hidden {
  display: none;
}
```

**Rendu visuel :**
```
┌─────────────────────┐
│ Élément visible 1   │
└─────────────────────┘
┌─────────────────────┐
│ Élément visible 2   │
└─────────────────────┘
```

L'élément caché ne prend aucune place.

### display: none vs visibility: hidden

**Différence importante :**

```css
/* display: none - L'élément disparaît complètement */
.hidden-display {
  display: none;
  /* Ne prend aucune place */
}

/* visibility: hidden - L'élément est invisible mais garde sa place */
.hidden-visibility {
  visibility: hidden;
  /* Prend toujours de la place (espace vide) */
}
```

**Comparaison visuelle :**

```html
<!-- Avec display: none -->
<div>Visible 1</div>
<div style="display: none;">Caché</div>
<div>Visible 2</div>
```
```
[Visible 1]
[Visible 2]    ← Collé au premier
```

```html
<!-- Avec visibility: hidden -->
<div>Visible 1</div>
<div style="visibility: hidden;">Caché</div>
<div>Visible 2</div>
```
```
[Visible 1]
             ← Espace vide
[Visible 2]
```

### Exemples pratiques

```css
/* Menu mobile caché par défaut */
.mobile-menu {
  display: none;
}

.mobile-menu.active {
  display: block;
}

/* Contenu conditionnel */
.success-message {
  display: none;
  padding: 10px;
  background-color: #27AE60;
  color: white;
}

.success-message.show {
  display: block;
}

/* Responsive : cacher sur mobile */
@media (max-width: 768px) {
  .desktop-only {
    display: none;
  }
}

/* Responsive : afficher sur mobile */
.mobile-only {
  display: none;
}

@media (max-width: 768px) {
  .mobile-only {
    display: block;
  }
}
```

### Accessibilité

⚠️ **Important pour l'accessibilité** : `display: none` cache l'élément aux lecteurs d'écran.

```css
/* ❌ Caché pour tout le monde (y compris lecteurs d'écran) */
.hidden {
  display: none;
}

/* ✅ Caché visuellement mais accessible aux lecteurs d'écran */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

---

## Tableau comparatif

| Propriété | Nouvelle ligne | Largeur | Width/Height | Margin | Padding | Usage typique |
|-----------|----------------|---------|--------------|---------|---------|---------------|
| **block** | ✅ Oui | 100% par défaut | ✅ Oui | ✅ Tous | ✅ Tous | Sections, conteneurs |
| **inline** | ❌ Non | Contenu | ❌ Non | ⚠️ H seulement | ⚠️ Superpose | Texte, liens |
| **inline-block** | ❌ Non | Contenu ou défini | ✅ Oui | ✅ Tous | ✅ Tous | Boutons, grilles simples |
| **none** | N/A | Aucune | N/A | N/A | N/A | Cacher des éléments |

**Légende :**
- ✅ Oui = Fonctionne complètement
- ❌ Non = Ne fonctionne pas / ignoré
- ⚠️ = Fonctionne partiellement
- H = Horizontal uniquement

---

## Autres valeurs de display

### display: flex 🆕

Layout moderne pour aligner et distribuer des éléments :

```css
.container {
  display: flex;
  gap: 20px;
}
```

**Avantages :** Contrôle puissant de l'alignement, espacement automatique, responsive.

*(Sera vu en détail dans le chapitre suivant)*

### display: grid 🆕

Layout moderne pour créer des grilles complexes :

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

**Avantages :** Grilles bidimensionnelles, placement précis.

*(Sera vu en détail dans le chapitre suivant)*

### display: table (legacy)

Fait se comporter un élément comme un tableau :

```css
.table {
  display: table;
}

.row {
  display: table-row;
}

.cell {
  display: table-cell;
}
```

**Note :** Utilisé avant Flexbox/Grid, moins courant aujourd'hui.

---

## Cas d'usage pratiques

### Cas 1 : Navigation horizontale

```html
<nav class="nav">
  <a href="#" class="nav-link">Accueil</a>
  <a href="#" class="nav-link">Services</a>
  <a href="#" class="nav-link">Contact</a>
</nav>
```

```css
/* Option 1 : inline-block */
.nav-link {
  display: inline-block;
  padding: 10px 20px;
  margin: 0 5px;
}

/* Option 2 : Flexbox (moderne) */
.nav {
  display: flex;
  gap: 10px;
}
.nav-link {
  padding: 10px 20px;
}
```

### Cas 2 : Grille de produits

```html
<div class="products">
  <div class="product-card">Produit 1</div>
  <div class="product-card">Produit 2</div>
  <div class="product-card">Produit 3</div>
</div>
```

```css
/* Option 1 : inline-block */
.product-card {
  display: inline-block;
  width: 300px;
  padding: 20px;
  margin: 10px;
  vertical-align: top;
}

/* Option 2 : Grid (moderne) */
.products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}
.product-card {
  padding: 20px;
}
```

### Cas 3 : Menu toggle (mobile)

```html
<button class="menu-toggle">Menu</button>
<nav class="menu">
  <a href="#">Lien 1</a>
  <a href="#">Lien 2</a>
  <a href="#">Lien 3</a>
</nav>
```

```css
/* Menu caché par défaut sur mobile */
@media (max-width: 768px) {
  .menu {
    display: none;
  }

  .menu.active {
    display: block;
  }

  .menu a {
    display: block;  /* Navigation verticale */
    padding: 15px;
  }
}

/* Menu visible sur desktop */
@media (min-width: 769px) {
  .menu-toggle {
    display: none;  /* Cacher le bouton */
  }

  .menu a {
    display: inline-block;  /* Navigation horizontale */
    padding: 10px 15px;
  }
}
```

### Cas 4 : Badge/Compteur

```html
<button>
  Messages
  <span class="badge">5</span>
</button>
```

```css
.badge {
  display: inline-block;
  min-width: 20px;
  padding: 2px 6px;
  background-color: #E74C3C;
  color: white;
  border-radius: 10px;
  font-size: 0.75em;
  text-align: center;
}
```

---

## Techniques avancées

### Centrage avec display: block

```css
/* Centrer horizontalement */
.center-horizontal {
  display: block;
  width: 300px;
  margin: 0 auto;
}

/* Centrer une image */
img.centered {
  display: block;
  max-width: 100%;
  margin: 0 auto;
}
```

### Layout responsive avec display

```css
/* Desktop : côte à côte */
.item {
  display: inline-block;
  width: 48%;
  margin: 1%;
  vertical-align: top;
}

/* Mobile : empilés */
@media (max-width: 768px) {
  .item {
    display: block;
    width: 100%;
    margin-bottom: 20px;
  }
}
```

### Toggle avec JavaScript

```html
<button onclick="toggleElement()">Toggle</button>
<div id="content">Contenu à afficher/cacher</div>
```

```javascript
function toggleElement() {
  const element = document.getElementById('content');
  if (element.style.display === 'none') {
    element.style.display = 'block';
  } else {
    element.style.display = 'none';
  }
}
```

---

## Erreurs courantes et solutions

### Erreur 1 : Width sur élément inline

```css
/* ❌ Ne fonctionne pas */
span {
  display: inline;
  width: 200px;  /* Ignoré ! */
}

/* ✅ Solution */
span {
  display: inline-block;
  width: 200px;
}
```

### Erreur 2 : Centrer un élément inline

```css
/* ❌ Ne fonctionne pas */
span {
  display: inline;
  margin: 0 auto;  /* N'a aucun effet */
}

/* ✅ Solution 1 : transformer en block */
span {
  display: block;
  width: 200px;
  margin: 0 auto;
}

/* ✅ Solution 2 : centrer le parent */
.parent {
  text-align: center;
}
span {
  display: inline-block;
}
```

### Erreur 3 : Espace entre inline-block

```css
/* ❌ Problème : espace indésirable */
.item {
  display: inline-block;
  width: 33.33%;
  /* Ne rentre pas à cause de l'espace ! */
}

/* ✅ Solution */
.container {
  font-size: 0;
}
.item {
  font-size: 1rem;
  display: inline-block;
  width: 33.33%;
}
```

### Erreur 4 : Oublier vertical-align

```css
/* ❌ Problème : alignement bizarre */
.box {
  display: inline-block;
  height: 100px;
  /* Par défaut, aligné sur la baseline */
}

/* ✅ Solution */
.box {
  display: inline-block;
  height: 100px;
  vertical-align: top;  /* Aligner en haut */
}
```

### Erreur 5 : display: none et accessibilité

```css
/* ❌ Mauvais : cache aux lecteurs d'écran aussi */
.visually-hidden {
  display: none;
}

/* ✅ Bon : cache visuellement mais garde accessible */
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

---

## Bonnes pratiques

### 1. Privilégiez Flexbox et Grid

Pour les layouts modernes, préférez Flexbox et Grid à inline-block :

```css
/* ❌ Ancien (fonctionne mais moins flexible) */
.item {
  display: inline-block;
  width: 33.33%;
  vertical-align: top;
}

/* ✅ Moderne (plus propre et flexible) */
.container {
  display: flex;
  gap: 20px;
}
.item {
  flex: 1;
}
```

### 2. Utilisez display judicieusement

```css
/* ✅ Bon : utiliser la valeur appropriée */
.button {
  display: inline-block;  /* Peut avoir des dimensions */
}

.section {
  display: block;  /* Prend toute la largeur */
}

.highlight {
  display: inline;  /* Dans le flux du texte */
}
```

### 3. Responsive avec display

```css
/* ✅ Bon : adapter le display selon la taille */
.nav-item {
  display: block;  /* Mobile : vertical */
}

@media (min-width: 768px) {
  .nav-item {
    display: inline-block;  /* Desktop : horizontal */
  }
}
```

### 4. Commentez les changements de display

```css
/* ✅ Bon : expliquer pourquoi */
.logo {
  display: block;  /* Pour centrer avec margin: 0 auto */
  margin: 0 auto;
}
```

### 5. Testez l'accessibilité

```css
/* ✅ Bon : se demander si l'élément doit rester accessible */
.desktop-only {
  display: none;  /* OK, vraiment caché */
}

.skip-link {
  /* Visuellement caché mais accessible */
  position: absolute;
  left: -10000px;
  /* Ne pas utiliser display: none */
}
```

---

## Résumé

### Points clés à retenir

1. **block** = nouvelle ligne, prend toute la largeur, dimensions contrôlables
2. **inline** = même ligne, largeur du contenu, pas de dimensions
3. **inline-block** = même ligne AVEC dimensions contrôlables (meilleur des deux)
4. **none** = complètement caché, ne prend aucune place
5. **Flexbox et Grid** sont les solutions modernes pour la mise en page

### Quand utiliser quoi ?

| Besoin | Solution |
|--------|----------|
| Section de page | `display: block` |
| Texte avec mise en forme | `display: inline` |
| Boutons côte à côte | `display: inline-block` ou Flexbox |
| Grille de cartes | `display: inline-block`, Grid ou Flexbox |
| Navigation horizontale | `display: inline-block` ou Flexbox |
| Cacher un élément | `display: none` |
| Layout complexe | Flexbox ou Grid |

### Syntaxe essentielle

```css
/* Valeurs principales */
.element {
  display: block;        /* Élément block */
  display: inline;       /* Élément inline */
  display: inline-block; /* Hybride */
  display: none;         /* Caché */

  /* Modernes (vus plus tard) */
  display: flex;         /* Flexbox */
  display: grid;         /* Grid */
}
```

La propriété `display` est fondamentale en CSS. Elle détermine comment les éléments se comportent et interagissent entre eux. Maîtriser ces valeurs est essentiel avant d'aborder Flexbox et Grid !

---

## Pour aller plus loin

Dans les prochains chapitres, vous découvrirez :
- **Flexbox** : pour aligner et distribuer des éléments de façon flexible
- **Grid** : pour créer des mises en page complexes en deux dimensions
- **Position** : pour sortir du flux normal et placer précisément les éléments

Ces outils modernes remplaceront souvent l'utilisation de `inline-block` pour les layouts complexes, mais comprendre les bases de `display` reste essentiel !

⏭️ [Backgrounds et images de fond](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/07-backgrounds.md)
