🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.1 Couleurs : hex, rgb, rgba, hsl

## Introduction

Les couleurs sont un élément fondamental du design web. En CSS, vous disposez de plusieurs façons de définir des couleurs, chacune ayant ses propres avantages. Comprendre ces différents formats vous permettra de choisir la méthode la plus adaptée à votre projet.

## Les noms de couleurs

La façon la plus simple de définir une couleur est d'utiliser son nom en anglais :

```css
h1 {
  color: red;
}

p {
  color: blue;
}

div {
  background-color: green;
}
```

CSS reconnaît environ 140 noms de couleurs (red, blue, green, black, white, orange, purple, etc.). Cependant, cette méthode est limitée car elle ne permet d'accéder qu'à un nombre restreint de couleurs.

## Format Hexadécimal (hex)

### Qu'est-ce que c'est ?

Le format hexadécimal est le plus couramment utilisé en développement web. Il commence toujours par le symbole `#` suivi de 6 caractères (ou 3 en version courte).

### Syntaxe

```css
/* Format complet : #RRGGBB */
color: #FF0000;  /* Rouge */
color: #00FF00;  /* Vert */
color: #0000FF;  /* Bleu */
color: #FFFFFF;  /* Blanc */
color: #000000;  /* Noir */

/* Format court : #RGB (quand les valeurs sont doublées) */
color: #F00;     /* Équivalent à #FF0000 */
color: #0F0;     /* Équivalent à #00FF00 */
color: #00F;     /* Équivalent à #0000FF */
```

### Comment ça fonctionne ?

Les 6 caractères représentent trois paires de valeurs :
- Les deux premiers caractères : intensité du **Rouge** (00 à FF)
- Les deux suivants : intensité du **Vert** (00 à FF)
- Les deux derniers : intensité du **Bleu** (00 à FF)

Le système hexadécimal compte de 0 à F (0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F), où :
- `00` = aucune intensité (0%)
- `FF` = intensité maximale (100%)

### Exemples pratiques

```css
.title {
  color: #2C3E50;  /* Bleu-gris foncé */
}

.button {
  background-color: #3498DB;  /* Bleu clair */
}

.footer {
  background-color: #ECF0F1;  /* Gris très clair */
}
```

### Avantages
- Format le plus répandu
- Copier-coller facile depuis les outils de design (Figma, Photoshop)
- Compact et lisible

### Inconvénients
- Difficile de deviner la couleur juste en lisant le code
- Impossible de gérer la transparence (il faut rgba ou hsla)

## Format RGB (Red, Green, Blue)

### Qu'est-ce que c'est ?

RGB utilise des valeurs numériques de 0 à 255 pour définir l'intensité de chaque composante : rouge, vert, bleu.

### Syntaxe

```css
/* rgb(rouge, vert, bleu) */
color: rgb(255, 0, 0);     /* Rouge */
color: rgb(0, 255, 0);     /* Vert */
color: rgb(0, 0, 255);     /* Bleu */
color: rgb(255, 255, 255); /* Blanc */
color: rgb(0, 0, 0);       /* Noir */
```

### Exemples pratiques

```css
.header {
  background-color: rgb(44, 62, 80);  /* Bleu-gris foncé */
}

.link {
  color: rgb(52, 152, 219);  /* Bleu clair */
}

.card {
  border-color: rgb(149, 165, 166);  /* Gris moyen */
}
```

### Avantages
- Plus intuitif que le format hexadécimal
- Les valeurs sont compréhensibles (0 à 255)
- Facile à manipuler en JavaScript

### Inconvénients
- Plus verbeux que le format hex
- Pas de transparence dans la version de base

## Format RGBA (RGB avec Alpha)

### Qu'est-ce que c'est ?

RGBA est identique à RGB, mais ajoute un quatrième paramètre : le canal **alpha** qui contrôle l'opacité/transparence.

### Syntaxe

```css
/* rgba(rouge, vert, bleu, alpha) */
/* Alpha : 0 = transparent, 1 = opaque */

background-color: rgba(255, 0, 0, 1);    /* Rouge opaque */
background-color: rgba(255, 0, 0, 0.5);  /* Rouge semi-transparent (50%) */
background-color: rgba(255, 0, 0, 0);    /* Totalement transparent */
```

### Exemples pratiques

```css
/* Overlay sombre semi-transparent */
.overlay {
  background-color: rgba(0, 0, 0, 0.7);  /* Noir à 70% d'opacité */
}

/* Bouton avec fond légèrement transparent */
.button-ghost {
  background-color: rgba(52, 152, 219, 0.2);  /* Bleu très transparent */
  border: 2px solid rgb(52, 152, 219);
}

/* Ombre portée subtile */
.card {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);  /* Ombre noire à 10% */
}
```

### Cas d'usage typiques

1. **Overlays** : couches semi-transparentes sur des images
2. **Effets de survol** : changements d'opacité au hover
3. **Ombres** : box-shadow avec transparence
4. **Dégradés** : transitions de couleur avec opacité

### Avantages
- Gestion de la transparence
- Idéal pour les superpositions et effets visuels
- Permet des designs plus sophistiqués

## Format HSL (Hue, Saturation, Lightness)

### Qu'est-ce que c'est ?

HSL est un format qui se rapproche de la façon dont les humains perçoivent les couleurs. Il se compose de trois valeurs :

- **Hue (Teinte)** : la couleur de base, exprimée en degrés (0-360°)
- **Saturation** : l'intensité de la couleur, en pourcentage (0%-100%)
- **Lightness (Luminosité)** : la clarté de la couleur, en pourcentage (0%-100%)

### Syntaxe

```css
/* hsl(teinte, saturation, luminosité) */
color: hsl(0, 100%, 50%);    /* Rouge */
color: hsl(120, 100%, 50%);  /* Vert */
color: hsl(240, 100%, 50%);  /* Bleu */
```

### Le cercle chromatique (Hue)

La teinte suit le cercle chromatique :
- `0°` ou `360°` = Rouge
- `60°` = Jaune
- `120°` = Vert
- `180°` = Cyan
- `240°` = Bleu
- `300°` = Magenta

### Saturation et Luminosité

**Saturation** :
- `0%` = gris (aucune couleur)
- `50%` = couleur moyennement intense
- `100%` = couleur pure, pleinement saturée

**Luminosité** :
- `0%` = noir (quelle que soit la couleur)
- `50%` = couleur normale
- `100%` = blanc (quelle que soit la couleur)

### Exemples pratiques

```css
/* Bleu principal */
.primary {
  background-color: hsl(210, 80%, 50%);
}

/* Variation plus claire du même bleu */
.primary-light {
  background-color: hsl(210, 80%, 70%);  /* Même teinte, plus clair */
}

/* Variation plus foncée */
.primary-dark {
  background-color: hsl(210, 80%, 30%);  /* Même teinte, plus foncé */
}

/* Version désaturée (grisée) */
.primary-muted {
  background-color: hsl(210, 30%, 50%);  /* Même teinte, moins saturé */
}
```

### HSLA (HSL avec Alpha)

Comme RGBA, il existe HSLA pour ajouter la transparence :

```css
.element {
  background-color: hsla(210, 80%, 50%, 0.5);  /* Bleu semi-transparent */
}
```

### Avantages
- Facile de créer des palettes cohérentes
- Simple de créer des variantes (plus clair, plus foncé)
- Intuitive pour ajuster les couleurs
- Idéal pour générer des couleurs dynamiquement en JavaScript

### Inconvénients
- Moins familier pour les débutants
- Moins répandu dans les outils de design

## Comparaison des formats

| Format | Exemple | Transparence | Usage typique |
|--------|---------|--------------|---------------|
| **Nom** | `red` | ❌ | Tests rapides, couleurs basiques |
| **Hex** | `#FF0000` | ❌ | Standard dans le design, copier-coller depuis Figma/Photoshop |
| **RGB** | `rgb(255, 0, 0)` | ❌ | Manipulation en JavaScript |
| **RGBA** | `rgba(255, 0, 0, 0.5)` | ✅ | Overlays, ombres, effets transparents |
| **HSL** | `hsl(0, 100%, 50%)` | ❌ | Palettes de couleurs, variations |
| **HSLA** | `hsla(0, 100%, 50%, 0.5)` | ✅ | Comme HSL avec transparence |

## Choisir le bon format

### Utilisez **Hex** quand :
- Vous copiez des couleurs depuis un outil de design
- Vous voulez un code court et standard
- Vous n'avez pas besoin de transparence

### Utilisez **RGB/RGBA** quand :
- Vous avez besoin de transparence (RGBA)
- Vous manipulez des couleurs en JavaScript
- Vous voulez des valeurs faciles à comprendre

### Utilisez **HSL/HSLA** quand :
- Vous créez une palette de couleurs cohérente
- Vous voulez facilement créer des variantes (clair/foncé)
- Vous générez des couleurs dynamiquement
- Vous travaillez sur l'harmonie des couleurs

## Outils pratiques

### Dans les DevTools du navigateur

Les DevTools de Chrome/Firefox vous permettent de :
1. Cliquer sur un carré de couleur dans l'inspecteur
2. Basculer entre les formats (hex, rgb, hsl) avec `Shift + Clic`
3. Utiliser une pipette pour capturer des couleurs depuis la page

### Convertir entre formats

Tous ces formats représentent les mêmes couleurs. Par exemple, ces trois déclarations donnent exactement la même couleur :

```css
color: #3498DB;
color: rgb(52, 152, 219);
color: hsl(204, 70%, 53%);
```

Vous pouvez utiliser des outils en ligne ou les DevTools pour convertir facilement d'un format à l'autre.

## Propriétés CSS qui acceptent les couleurs

Voici les propriétés CSS les plus courantes qui utilisent des couleurs :

```css
.element {
  /* Texte */
  color: #333333;

  /* Arrière-plan */
  background-color: rgba(255, 255, 255, 0.9);

  /* Bordures */
  border-color: hsl(210, 80%, 50%);
  border: 2px solid #3498DB;

  /* Ombres */
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);

  /* Contours */
  outline-color: red;
}
```

## Bonnes pratiques

### 1. Cohérence dans le projet
Choisissez un format principal et restez-y pour la majorité de votre code :
```css
/* Bon : cohérent */
.header { background-color: #2C3E50; }
.button { background-color: #3498DB; }
.footer { background-color: #ECF0F1; }

/* À éviter : mélange sans raison */
.header { background-color: #2C3E50; }
.button { background-color: rgb(52, 152, 219); }
.footer { background-color: hsl(192, 15%, 94%); }
```

### 2. Utilisez des variables CSS
Définissez vos couleurs une seule fois avec des noms significatifs :
```css
:root {
  --color-primary: #3498DB;
  --color-secondary: #2C3E50;
  --color-success: #27AE60;
  --color-danger: #E74C3C;
  --color-light: #ECF0F1;
  --color-dark: #2C3E50;
}

.button-primary {
  background-color: var(--color-primary);
}

.alert-success {
  border-color: var(--color-success);
}
```

### 3. Commentez les couleurs spécifiques
Si vous utilisez le format hex, ajoutez un commentaire pour clarifier :
```css
.header {
  background-color: #2C3E50;  /* Bleu-gris foncé / Midnight Blue */
}
```

### 4. Utilisez RGBA/HSLA pour la transparence
Ne tentez pas de simuler la transparence avec des couleurs plus claires :
```css
/* Mauvais : essayer de simuler la transparence */
.overlay {
  background-color: #808080;  /* Gris censé paraître transparent */
}

/* Bon : transparence réelle */
.overlay {
  background-color: rgba(0, 0, 0, 0.5);  /* Vraiment semi-transparent */
}
```

## Résumé

- **Les noms de couleurs** sont pratiques mais limités
- **Hex (#RRGGBB)** est le format standard, compact et universel
- **RGB** est intuitif avec des valeurs de 0 à 255
- **RGBA** ajoute la transparence à RGB (valeur alpha de 0 à 1)
- **HSL** est idéal pour créer des palettes harmonieuses
- **HSLA** combine HSL et transparence

Le format que vous choisissez dépend de votre contexte :
- Pour un design statique → **Hex**
- Pour des effets de transparence → **RGBA** ou **HSLA**
- Pour des variations de couleurs → **HSL**
- Pour de la manipulation JS → **RGB** ou **HSL**

L'essentiel est de rester cohérent dans votre code et d'utiliser le format le plus adapté à votre besoin !

⏭️ [Typographie : font-family, size, weight, style, line-height](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/02-typographie.md)
