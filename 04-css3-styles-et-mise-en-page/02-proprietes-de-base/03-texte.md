🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.3 Texte : text-align, decoration, transform

## Introduction

Au-delà de la typographie (police, taille, graisse), CSS offre de nombreuses propriétés pour contrôler l'apparence et la disposition du texte. Dans ce chapitre, nous allons explorer les propriétés essentielles pour aligner, décorer et transformer le texte.

Ces propriétés vous permettront de créer des mises en page textuelles professionnelles et attractives.

---

## text-align : Alignement horizontal du texte

### Qu'est-ce que c'est ?

La propriété `text-align` définit l'alignement horizontal du contenu textuel à l'intérieur de son conteneur.

### Valeurs principales

```css
/* Alignement à gauche (valeur par défaut) */
.left {
  text-align: left;
}

/* Alignement à droite */
.right {
  text-align: right;
}

/* Centrage */
.center {
  text-align: center;
}

/* Justification (alignement des deux côtés) */
.justify {
  text-align: justify;
}
```

### Exemples visuels

#### Alignement à gauche (par défaut)

```css
p {
  text-align: left;
}
```

**Résultat** :
```
Ceci est un paragraphe aligné
à gauche. C'est l'alignement
par défaut du texte.
```

#### Alignement à droite

```css
.date {
  text-align: right;
}
```

**Résultat** :
```
                    12/12/2025
             Paris, France
```

**Usage** : Dates, signatures, contenu dans une langue RTL (arabe, hébreu).

#### Centrage

```css
h1 {
  text-align: center;
}
```

**Résultat** :
```
        Bienvenue sur mon site
```

**Usage** : Titres principaux, slogans, contenu de présentation.

#### Justification

```css
.article {
  text-align: justify;
}
```

**Résultat** :
```
Ceci est un texte justifié qui
s'étend  sur  toute  la largeur
disponible.  Les  espaces  sont
ajustés pour  aligner les  deux
bords.
```

**Note** : La justification ajoute des espaces entre les mots pour aligner les deux bords. À utiliser avec parcimonie.

### Cas d'usage pratiques

```css
/* En-tête de site */
.site-header {
  text-align: center;
}

/* Article de blog */
.article-content {
  text-align: left;      /* Meilleur pour la lecture */
}

/* Pied de page */
.footer {
  text-align: center;
}

/* Menu de navigation */
.nav {
  text-align: right;     /* Navigation alignée à droite */
}

/* Citation */
.quote {
  text-align: center;
  font-style: italic;
}
```

### Alignement d'éléments inline

`text-align` fonctionne aussi pour aligner des éléments inline (comme les images) :

```css
.image-container {
  text-align: center;    /* Centre l'image */
}
```

```html
<div class="image-container">
  <img src="photo.jpg" alt="Photo">
</div>
```

### Important à savoir

⚠️ `text-align` s'applique au **conteneur**, pas à l'élément lui-même :

```css
/* ❌ Ne fonctionne pas */
h1 {
  text-align: center;    /* Le h1 doit être dans un conteneur */
}

/* ✅ Fonctionne */
.header {
  text-align: center;    /* Centre tout le contenu du header */
}
```

---

## text-decoration : Décoration du texte

### Qu'est-ce que c'est ?

La propriété `text-decoration` permet d'ajouter des lignes décoratives au texte : soulignement, ligne au-dessus, ou texte barré.

### Valeurs principales

```css
/* Aucune décoration (valeur par défaut) */
.none {
  text-decoration: none;
}

/* Soulignement */
.underline {
  text-decoration: underline;
}

/* Ligne au-dessus */
.overline {
  text-decoration: overline;
}

/* Texte barré */
.line-through {
  text-decoration: line-through;
}
```

### Exemples visuels

```css
.underlined {
  text-decoration: underline;
}
/* Résultat : Texte souligné */

.overlined {
  text-decoration: overline;
}
/* Résultat : T̅e̅x̅t̅e̅ avec ligne au-dessus */

.strikethrough {
  text-decoration: line-through;
}
/* Résultat : T̶e̶x̶t̶e̶ barré */
```

### Propriétés décomposées (CSS3) 🆕

CSS3 permet de contrôler finement la décoration avec plusieurs sous-propriétés :

#### text-decoration-line

```css
.element {
  text-decoration-line: underline;          /* Type de ligne */
  text-decoration-line: overline;
  text-decoration-line: line-through;
  text-decoration-line: underline overline; /* Plusieurs lignes */
}
```

#### text-decoration-style

```css
.element {
  text-decoration-line: underline;
  text-decoration-style: solid;    /* Ligne pleine (défaut) */
  text-decoration-style: double;   /* Ligne double */
  text-decoration-style: dotted;   /* Pointillés */
  text-decoration-style: dashed;   /* Tirets */
  text-decoration-style: wavy;     /* Ondulée */
}
```

#### text-decoration-color

```css
.element {
  text-decoration-line: underline;
  text-decoration-color: red;      /* Couleur de la ligne */
}
```

#### text-decoration-thickness

```css
.element {
  text-decoration-line: underline;
  text-decoration-thickness: 2px;  /* Épaisseur de la ligne */
}
```

### Syntaxe raccourcie

Vous pouvez combiner toutes ces propriétés en une seule :

```css
.fancy-link {
  /* line style color thickness */
  text-decoration: underline wavy red 2px;
}
```

### Cas d'usage : Les liens

Par défaut, les liens (`<a>`) sont soulignés. Souvent, on retire ce soulignement :

```css
/* Retirer le soulignement des liens */
a {
  text-decoration: none;
  color: #3498DB;
}

/* Ajouter le soulignement au survol */
a:hover {
  text-decoration: underline;
}
```

### Exemples pratiques

```css
/* Lien avec soulignement coloré */
.link-primary {
  color: #333;
  text-decoration: underline;
  text-decoration-color: #3498DB;
  text-decoration-thickness: 2px;
}

/* Effet au survol */
.link-hover:hover {
  text-decoration: underline wavy #E74C3C;
}

/* Prix barré (promotion) */
.old-price {
  text-decoration: line-through;
  color: #999;
}

/* Texte important */
.important {
  text-decoration: underline double red;
}
```

### HTML sémantique

Certaines balises HTML ont une décoration par défaut :

```html
<a href="#">Lien souligné par défaut</a>
<del>Texte supprimé (barré par défaut)</del>
<ins>Texte inséré (souligné par défaut)</ins>
```

Vous pouvez modifier ou supprimer ces styles avec CSS :

```css
del {
  text-decoration: none;         /* Retirer le barré */
  background-color: #ffe0e0;     /* Utiliser du surlignage à la place */
}
```

---

## text-transform : Transformation du texte

### Qu'est-ce que c'est ?

La propriété `text-transform` permet de modifier la casse (majuscules/minuscules) du texte sans changer le contenu HTML.

### Valeurs

```css
/* Aucune transformation (valeur par défaut) */
.none {
  text-transform: none;
}

/* Tout en majuscules */
.uppercase {
  text-transform: uppercase;
}

/* Tout en minuscules */
.lowercase {
  text-transform: lowercase;
}

/* Première lettre de chaque mot en majuscule */
.capitalize {
  text-transform: capitalize;
}
```

### Exemples visuels

```html
<p class="uppercase">bonjour tout le monde</p>
<!-- Affiche : BONJOUR TOUT LE MONDE -->

<p class="lowercase">BONJOUR TOUT LE MONDE</p>
<!-- Affiche : bonjour tout le monde -->

<p class="capitalize">bonjour tout le monde</p>
<!-- Affiche : Bonjour Tout Le Monde -->
```

### Cas d'usage pratiques

#### Titres en majuscules

```css
h1 {
  text-transform: uppercase;
  letter-spacing: 2px;    /* Espacement pour plus de lisibilité */
}
```

```html
<h1>Mon titre</h1>
<!-- Affiche : MON TITRE -->
```

#### Boutons

```css
.button {
  text-transform: uppercase;
  font-size: 0.875rem;
  font-weight: 600;
}
```

```html
<button class="button">Envoyer</button>
<!-- Affiche : ENVOYER -->
```

#### Noms propres

```css
.name {
  text-transform: capitalize;
}
```

```html
<span class="name">jean dupont</span>
<!-- Affiche : Jean Dupont -->
```

#### Navigation

```css
.nav-link {
  text-transform: lowercase;
  font-size: 0.9rem;
}
```

### Important : Capitalize

⚠️ `capitalize` met en majuscule **chaque premier caractère après un espace**, ce qui peut donner des résultats inattendus :

```css
.text {
  text-transform: capitalize;
}
```

```html
<p class="text">l'histoire du web</p>
<!-- Affiche : L'histoire Du Web -->
<!-- Note : "Du" prend aussi une majuscule -->
```

### Avantages de text-transform

1. **Cohérence** : Uniformise la casse même si le contenu HTML est incohérent
2. **Maintenance** : Changez le style sans modifier le HTML
3. **Accessibilité** : Les lecteurs d'écran lisent le texte original

```html
<!-- HTML avec casse normale -->
<button>Envoyer</button>
```

```css
/* CSS transforme en majuscules */
button {
  text-transform: uppercase;
}
/* Affiche : ENVOYER, mais le HTML reste "Envoyer" */
```

---

## Propriétés complémentaires

### text-indent : Retrait de première ligne

Crée un retrait sur la première ligne d'un paragraphe :

```css
p {
  text-indent: 2em;     /* Retrait de 2em */
}

/* Retrait négatif (pour des listes personnalisées) */
.custom-list {
  text-indent: -1em;
  padding-left: 1em;
}
```

**Usage** : Paragraphes de livres, articles formels.

### letter-spacing : Espacement entre les lettres

Contrôle l'espace entre chaque caractère :

```css
/* Espacement positif (lettres espacées) */
.spaced {
  letter-spacing: 2px;
}

/* Espacement négatif (lettres resserrées) */
.tight {
  letter-spacing: -0.5px;
}

/* Normal (valeur par défaut) */
.normal {
  letter-spacing: normal;
}
```

**Exemples pratiques** :

```css
/* Titres en majuscules avec espacement */
h1 {
  text-transform: uppercase;
  letter-spacing: 3px;
}

/* Logo */
.logo {
  font-weight: 700;
  letter-spacing: 1px;
}
```

**⚠️ Attention** : Un espacement excessif rend la lecture difficile.

### word-spacing : Espacement entre les mots

Contrôle l'espace entre les mots :

```css
p {
  word-spacing: 5px;     /* Mots plus espacés */
}

.tight {
  word-spacing: -2px;    /* Mots plus serrés */
}
```

**Usage** : Moins courant que `letter-spacing`.

### text-shadow : Ombre portée du texte

Ajoute une ombre au texte :

```css
/* Syntaxe : offset-x offset-y blur-radius color */
h1 {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
```

**Exemples** :

```css
/* Ombre simple */
.simple-shadow {
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

/* Ombre floue */
.blurry-shadow {
  text-shadow: 0 0 10px rgba(0, 0, 0, 0.8);
}

/* Ombre colorée */
.colored-shadow {
  color: white;
  text-shadow: 2px 2px 8px rgba(52, 152, 219, 0.8);
}

/* Effet relief */
.embossed {
  color: #fff;
  text-shadow: 0 1px 0 #ccc,
               0 2px 0 #bbb,
               0 3px 0 #aaa,
               0 4px 0 #999;
}

/* Ombre multiple */
.neon {
  color: #fff;
  text-shadow: 0 0 5px #fff,
               0 0 10px #fff,
               0 0 20px #ff00de,
               0 0 30px #ff00de;
}
```

### white-space : Gestion des espaces blancs

Contrôle comment les espaces et les retours à la ligne sont gérés :

```css
/* Normal : les espaces multiples sont fusionnés (défaut) */
.normal {
  white-space: normal;
}

/* Nowrap : pas de retour à la ligne automatique */
.nowrap {
  white-space: nowrap;
}

/* Pre : préserve tous les espaces et retours à la ligne */
.pre {
  white-space: pre;
}

/* Pre-wrap : préserve les espaces mais autorise les retours */
.pre-wrap {
  white-space: pre-wrap;
}

/* Pre-line : fusionne les espaces mais préserve les retours */
.pre-line {
  white-space: pre-line;
}
```

**Exemple pratique** :

```css
/* Empêcher un texte de passer à la ligne */
.no-wrap {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;  /* Ajoute ... si le texte déborde */
}
```

### text-overflow : Débordement de texte

Définit comment afficher le texte qui déborde :

```css
.truncate {
  white-space: nowrap;      /* Pas de retour à la ligne */
  overflow: hidden;         /* Cacher le débordement */
  text-overflow: ellipsis;  /* Afficher ... */
}
```

```html
<p class="truncate" style="width: 200px;">
  Ceci est un très long texte qui sera tronqué
</p>
<!-- Affiche : Ceci est un très long text... -->
```

**Valeurs** :
- `clip` : Coupe le texte net (défaut)
- `ellipsis` : Ajoute "..." à la fin
- `string` : Chaîne personnalisée (support limité)

### vertical-align : Alignement vertical

Aligne verticalement les éléments inline :

```css
/* Pour les éléments inline et table-cell */
.baseline {
  vertical-align: baseline;  /* Défaut */
}

.top {
  vertical-align: top;
}

.middle {
  vertical-align: middle;
}

.bottom {
  vertical-align: bottom;
}

/* Avec des valeurs */
.custom {
  vertical-align: 2px;       /* Décale de 2px vers le haut */
  vertical-align: -2px;      /* Décale de 2px vers le bas */
}
```

**Usage courant** : Aligner des icônes avec du texte :

```css
.icon {
  vertical-align: middle;
  margin-right: 5px;
}
```

⚠️ **Attention** : `vertical-align` ne fonctionne **PAS** pour les éléments block. Utilisez Flexbox ou Grid pour l'alignement vertical de blocks.

---

## Exemples pratiques complets

### Titre stylisé

```css
.hero-title {
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  font-size: 3rem;
  font-weight: 700;
  color: #2C3E50;
}
```

### Lien personnalisé

```css
.custom-link {
  color: #3498DB;
  text-decoration: none;
  position: relative;
}

.custom-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #3498DB;
  transition: width 0.3s ease;
}

.custom-link:hover::after {
  width: 100%;
}
```

### Badge/Tag

```css
.badge {
  display: inline-block;
  padding: 0.25em 0.6em;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  text-align: center;
  white-space: nowrap;
  background-color: #E74C3C;
  color: white;
  border-radius: 4px;
  letter-spacing: 0.5px;
}
```

### Citation élégante

```css
.quote {
  text-align: center;
  font-style: italic;
  font-size: 1.25rem;
  color: #555;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
  line-height: 1.8;
  padding: 2rem;
}
```

### Texte tronqué (une ligne)

```css
.truncate-single {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 300px;
}
```

### Texte tronqué (plusieurs lignes)

```css
.truncate-multi {
  display: -webkit-box;
  -webkit-line-clamp: 3;        /* Nombre de lignes */
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

---

## Tableau récapitulatif

| Propriété | Fonction | Valeurs courantes | Usage typique |
|-----------|----------|-------------------|---------------|
| **text-align** | Alignement horizontal | `left`, `right`, `center`, `justify` | Titres centrés, navigation |
| **text-decoration** | Décoration (ligne) | `none`, `underline`, `line-through` | Liens, prix barrés |
| **text-transform** | Casse du texte | `uppercase`, `lowercase`, `capitalize` | Boutons, titres |
| **letter-spacing** | Espacement lettres | `2px`, `-0.5px` | Titres en majuscules |
| **word-spacing** | Espacement mots | `5px` | Rarement utilisé |
| **text-indent** | Retrait première ligne | `2em` | Paragraphes livres |
| **text-shadow** | Ombre du texte | `2px 2px 4px rgba(0,0,0,0.3)` | Effets visuels |
| **white-space** | Gestion espaces | `nowrap`, `pre`, `pre-wrap` | Texte non cassable |
| **text-overflow** | Débordement texte | `ellipsis`, `clip` | Texte tronqué |
| **vertical-align** | Alignement vertical | `top`, `middle`, `bottom` | Icônes avec texte |

---

## Bonnes pratiques

### 1. Alignement du texte

```css
/* ✅ Bon : texte aligné à gauche pour la lecture */
.article {
  text-align: left;
}

/* ❌ Éviter : texte justifié peut créer des espaces irréguliers */
.bad {
  text-align: justify;  /* OK pour l'imprimé, problématique pour le web */
}
```

### 2. Décoration des liens

```css
/* ✅ Bon : indication visuelle au survol */
a {
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

/* ❌ Mauvais : pas d'indication que c'est un lien */
a {
  text-decoration: none;
  color: inherit;  /* Pas de différence visuelle */
}
```

### 3. Majuscules et espacement

```css
/* ✅ Bon : majuscules avec espacement pour lisibilité */
.button {
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* ❌ Mauvais : majuscules sans espacement (difficile à lire) */
.bad {
  text-transform: uppercase;
  letter-spacing: 0;
}
```

### 4. Text-shadow subtil

```css
/* ✅ Bon : ombre subtile */
h1 {
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}

/* ❌ Mauvais : ombre trop prononcée (années 2000) */
.bad {
  text-shadow: 5px 5px 0 #000;
}
```

### 5. White-space pour une ligne

```css
/* ✅ Bon : texte sur une ligne avec ellipse */
.title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* ❌ Incomplet : manque overflow et text-overflow */
.bad {
  white-space: nowrap;  /* Le texte va déborder */
}
```

---

## Accessibilité

### Text-transform et lecteurs d'écran

Les lecteurs d'écran lisent le texte original du HTML, pas la transformation CSS :

```html
<button style="text-transform: uppercase;">envoyer</button>
```

Le lecteur d'écran lira "envoyer", pas "ENVOYER". C'est généralement positif car "ENVOYER" serait lu lettre par lettre.

### Contraste avec text-shadow

Assurez-vous que les ombres n'affectent pas le contraste et la lisibilité :

```css
/* ✅ Bon : ombre légère */
.good {
  color: #333;
  background: #fff;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

/* ❌ Mauvais : ombre réduit le contraste */
.bad {
  color: #ccc;
  background: #fff;
  text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.5);
}
```

### Text-decoration pour les liens

Ne retirez pas complètement la distinction visuelle des liens :

```css
/* ✅ Bon : distinction au survol */
a {
  color: #3498DB;
  text-decoration: none;
}

a:hover,
a:focus {
  text-decoration: underline;
}

/* ❌ Mauvais : aucune distinction */
a {
  color: inherit;
  text-decoration: none;
}
```

---

## Résumé

### Points clés à retenir

1. **text-align** centre ou aligne le texte (left, center, right, justify)
2. **text-decoration** ajoute ou retire des lignes (underline, line-through, none)
3. **text-transform** change la casse sans modifier le HTML (uppercase, lowercase, capitalize)
4. **letter-spacing** espacer les lettres, particulièrement utile avec les majuscules
5. **text-shadow** ajoute des effets visuels, à utiliser avec modération
6. **white-space + text-overflow** permettent de tronquer le texte avec "..."

### Quand utiliser quoi ?

- **Titres centrés** → `text-align: center`
- **Liens sans soulignement** → `text-decoration: none` (+ effet au hover)
- **Boutons** → `text-transform: uppercase` + `letter-spacing`
- **Prix barrés** → `text-decoration: line-through`
- **Texte tronqué** → `white-space: nowrap` + `overflow: hidden` + `text-overflow: ellipsis`
- **Effet visuel** → `text-shadow` (avec parcimonie)

Ces propriétés sont essentielles pour créer des interfaces textuelles claires, lisibles et esthétiques. Expérimentez-les pour trouver le bon équilibre !

⏭️ [Le modèle de boîte (box-model)](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/04-modele-de-boite.md)
