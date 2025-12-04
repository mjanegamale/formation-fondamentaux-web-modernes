🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.2 Typographie : font-family, size, weight, style, line-height

## Introduction

La typographie est l'art de mettre en forme le texte pour le rendre lisible, attrayant et efficace. En CSS, plusieurs propriétés vous permettent de contrôler l'apparence du texte : la police utilisée, sa taille, son épaisseur, son style et l'espacement entre les lignes.

Maîtriser ces propriétés est essentiel car le texte représente généralement la majorité du contenu d'un site web.

---

## font-family : Choisir la police de caractères

### Qu'est-ce que c'est ?

La propriété `font-family` définit la police (ou "fonte") qui sera utilisée pour afficher le texte.

### Syntaxe de base

```css
p {
  font-family: Arial;
}

h1 {
  font-family: "Times New Roman";
}
```

**Note importante** : Si le nom de la police contient des espaces, il doit être entouré de guillemets.

### Les familles de polices génériques

CSS définit 5 familles génériques qui sont garanties de fonctionner sur tous les navigateurs :

```css
/* Polices sans empattement (modernes, épurées) */
.sans-serif {
  font-family: sans-serif;
}

/* Polices avec empattement (traditionnelles, élégantes) */
.serif {
  font-family: serif;
}

/* Polices à chasse fixe (code, technique) */
.monospace {
  font-family: monospace;
}

/* Polices manuscrites */
.cursive {
  font-family: cursive;
}

/* Polices fantaisie/décoratives */
.fantasy {
  font-family: fantasy;
}
```

**Qu'est-ce qu'un empattement ?** Ce sont les petites extensions au bout des lettres. Par exemple, le "T" dans Times New Roman a des empattements, contrairement au "T" dans Arial.

### Liste de secours (fallback)

Il est recommandé de fournir plusieurs polices en liste de secours. Le navigateur essaiera la première, puis la deuxième si elle n'est pas disponible, etc.

```css
body {
  font-family: Arial, Helvetica, sans-serif;
}
```

**Comment ça fonctionne ?**
1. Le navigateur essaie d'utiliser **Arial**
2. Si Arial n'est pas installé, il essaie **Helvetica**
3. Si aucune n'est disponible, il utilise la police **sans-serif** par défaut du système

### Polices web-safe

Certaines polices sont installées sur presque tous les ordinateurs. On les appelle "web-safe fonts" :

```css
/* Sans-serif (sans empattement) */
.arial { font-family: Arial, sans-serif; }
.helvetica { font-family: Helvetica, sans-serif; }
.verdana { font-family: Verdana, sans-serif; }
.tahoma { font-family: Tahoma, sans-serif; }

/* Serif (avec empattement) */
.times { font-family: "Times New Roman", Times, serif; }
.georgia { font-family: Georgia, serif; }

/* Monospace (chasse fixe) */
.courier { font-family: "Courier New", Courier, monospace; }
```

### Polices système modernes

Vous pouvez utiliser les polices natives du système d'exploitation pour un rendu optimal :

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
               "Helvetica Neue", Arial, sans-serif;
}
```

Cette technique utilise :
- **San Francisco** sur macOS/iOS
- **Segoe UI** sur Windows
- **Roboto** sur Android
- Puis des alternatives de secours

### Google Fonts et polices personnalisées

Vous pouvez importer des polices depuis Google Fonts dans votre HTML :

```html
<!-- Dans le <head> de votre HTML -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
```

Puis l'utiliser en CSS :

```css
body {
  font-family: 'Roboto', sans-serif;
}
```

**Important** : Toujours fournir une police de secours !

---

## font-size : Taille du texte

### Qu'est-ce que c'est ?

La propriété `font-size` définit la taille des caractères.

### Unités absolues

#### Pixels (px)

Les pixels sont l'unité la plus courante et la plus simple à comprendre :

```css
p {
  font-size: 16px;  /* Taille standard pour le texte */
}

h1 {
  font-size: 32px;  /* Grand titre */
}

small {
  font-size: 12px;  /* Petit texte */
}
```

**Avantages** : Précis, facile à visualiser
**Inconvénients** : Ne s'adapte pas aux préférences de l'utilisateur

### Unités relatives

#### em

`em` est relatif à la taille de police du parent :

```css
body {
  font-size: 16px;
}

p {
  font-size: 1em;     /* = 16px (même taille que le parent) */
}

h1 {
  font-size: 2em;     /* = 32px (2 × 16px) */
}

small {
  font-size: 0.875em; /* = 14px (0.875 × 16px) */
}
```

**Attention** : Les `em` s'accumulent avec l'imbrication :

```css
.parent {
  font-size: 20px;
}

.enfant {
  font-size: 1.5em;  /* = 30px (1.5 × 20px) */
}

.petit-enfant {
  font-size: 1.5em;  /* = 45px (1.5 × 30px) ⚠️ Effet cumulatif ! */
}
```

#### rem (Root em) - RECOMMANDÉ 🆕

`rem` est relatif à la taille de police de l'élément racine `<html>`, ce qui évite l'effet cumulatif :

```css
html {
  font-size: 16px;  /* Taille de base */
}

p {
  font-size: 1rem;     /* = 16px */
}

h1 {
  font-size: 2rem;     /* = 32px */
}

small {
  font-size: 0.875rem; /* = 14px */
}
```

**Avantages** : Pas d'effet cumulatif, facile à maintenir, accessible
**C'est l'unité recommandée pour un design moderne !**

#### Pourcentages (%)

Les pourcentages fonctionnent comme les `em` :

```css
body {
  font-size: 16px;
}

h1 {
  font-size: 200%;  /* = 32px (200% de 16px) */
}
```

### Mots-clés

CSS propose aussi des mots-clés pour définir des tailles :

```css
p {
  font-size: small;      /* Petit */
  font-size: medium;     /* Moyen (valeur par défaut) */
  font-size: large;      /* Grand */
  font-size: x-large;    /* Très grand */
  font-size: xx-large;   /* Encore plus grand */
}
```

**Usage limité** : Ces mots-clés sont moins précis et rarement utilisés en pratique.

### Recommandations de tailles

Voici des tailles typiques pour différents éléments :

```css
body {
  font-size: 16px;  /* Ou 1rem - Taille de base */
}

p {
  font-size: 1rem;        /* 16px - Texte courant */
}

h1 {
  font-size: 2.5rem;      /* 40px - Titre principal */
}

h2 {
  font-size: 2rem;        /* 32px */
}

h3 {
  font-size: 1.5rem;      /* 24px */
}

small, .caption {
  font-size: 0.875rem;    /* 14px - Petit texte */
}

.lead {
  font-size: 1.25rem;     /* 20px - Texte d'introduction */
}
```

---

## font-weight : Épaisseur du texte

### Qu'est-ce que c'est ?

La propriété `font-weight` contrôle l'épaisseur (graisse) des caractères.

### Valeurs numériques

Les valeurs vont de **100** (ultra-léger) à **900** (ultra-gras) par paliers de 100 :

```css
.ultra-light {
  font-weight: 100;  /* Ultra léger */
}

.light {
  font-weight: 300;  /* Léger */
}

.normal {
  font-weight: 400;  /* Normal (valeur par défaut) */
}

.medium {
  font-weight: 500;  /* Medium */
}

.semi-bold {
  font-weight: 600;  /* Semi-gras */
}

.bold {
  font-weight: 700;  /* Gras */
}

.extra-bold {
  font-weight: 800;  /* Extra-gras */
}

.black {
  font-weight: 900;  /* Ultra-gras / Black */
}
```

**Important** : Toutes les polices ne proposent pas toutes les épaisseurs. Si une épaisseur n'est pas disponible, le navigateur utilisera la plus proche.

### Mots-clés

Il existe aussi des mots-clés pour des valeurs courantes :

```css
p {
  font-weight: normal;  /* = 400 */
}

strong {
  font-weight: bold;    /* = 700 */
}

.lighter {
  font-weight: lighter; /* Plus léger que le parent */
}

.bolder {
  font-weight: bolder;  /* Plus gras que le parent */
}
```

### Exemples pratiques

```css
/* Navigation */
.nav-link {
  font-weight: 500;  /* Medium, bien lisible */
}

/* Titres */
h1, h2, h3 {
  font-weight: 700;  /* Gras pour les titres */
}

/* Texte courant */
p {
  font-weight: 400;  /* Normal pour la lecture */
}

/* Mise en évidence */
.highlight {
  font-weight: 600;  /* Semi-gras */
}

/* Citation */
.quote {
  font-weight: 300;  /* Léger pour un effet élégant */
}
```

### La balise `<strong>` vs CSS

En HTML, `<strong>` met le texte en gras par défaut :

```html
<p>Ce texte est <strong>important</strong>.</p>
```

Mais vous pouvez modifier son apparence en CSS :

```css
strong {
  font-weight: 600;  /* Semi-gras au lieu de gras */
  color: #E74C3C;    /* Ajouter de la couleur */
}
```

---

## font-style : Style du texte

### Qu'est-ce que c'est ?

La propriété `font-style` définit si le texte est normal, italique ou oblique.

### Valeurs

```css
/* Normal - texte droit (valeur par défaut) */
.normal {
  font-style: normal;
}

/* Italique - version cursive de la police */
.italic {
  font-style: italic;
}

/* Oblique - version inclinée de la police */
.oblique {
  font-style: oblique;
}
```

### Différence entre italic et oblique

- **italic** : Version dessinée spécialement de la police, avec des formes différentes
- **oblique** : Simple inclinaison de la police normale

En pratique, si la police ne possède pas de version italique, le navigateur créera une version oblique.

### Exemples pratiques

```css
/* Citations */
blockquote {
  font-style: italic;
}

/* Emphase */
em {
  font-style: italic;  /* Par défaut en HTML */
}

/* Annuler l'italique */
.address {
  font-style: normal;  /* Remettre en normal */
}
```

### La balise `<em>` vs CSS

En HTML, `<em>` met le texte en italique par défaut :

```html
<p>Ce mot est <em>important</em>.</p>
```

Vous pouvez personnaliser son style :

```css
em {
  font-style: normal;     /* Annuler l'italique */
  font-weight: 600;       /* Utiliser du gras à la place */
  color: #3498DB;         /* Ajouter de la couleur */
}
```

---

## line-height : Hauteur de ligne

### Qu'est-ce que c'est ?

La propriété `line-height` définit l'espace vertical entre les lignes de texte. C'est l'une des propriétés les plus importantes pour la lisibilité.

### Syntaxe

```css
p {
  line-height: 1.5;      /* Sans unité (RECOMMANDÉ) */
  line-height: 1.5em;    /* Avec em */
  line-height: 24px;     /* En pixels */
  line-height: 150%;     /* En pourcentage */
}
```

### Valeur sans unité (RECOMMANDÉE) 🆕

C'est la méthode recommandée car elle multiplie la taille de police actuelle :

```css
p {
  font-size: 16px;
  line-height: 1.5;  /* = 24px (1.5 × 16px) */
}

h1 {
  font-size: 32px;
  line-height: 1.5;  /* = 48px (1.5 × 32px) */
}
```

**Avantage** : S'adapte automatiquement à la taille de police.

### Valeurs typiques

```css
/* Texte dense - difficile à lire */
.dense {
  line-height: 1;        /* Pas d'espace supplémentaire */
}

/* Texte standard - correct */
.standard {
  line-height: 1.4;      /* Lisibilité correcte */
}

/* Texte aéré - recommandé pour le web */
.airy {
  line-height: 1.6;      /* Bonne lisibilité */
}

/* Texte très aéré */
.spacious {
  line-height: 2;        /* Double interligne */
}
```

### Recommandations par type de contenu

```css
/* Texte courant / Paragraphes */
p {
  line-height: 1.6;      /* Optimal pour la lecture */
}

/* Titres */
h1, h2, h3 {
  line-height: 1.2;      /* Plus serré pour les titres */
}

/* Texte de petite taille */
.small-text {
  line-height: 1.5;      /* Un peu plus d'espace */
}

/* Navigation */
.nav {
  line-height: 1;        /* Compact pour les menus */
}

/* Code */
code, pre {
  line-height: 1.4;      /* Lisible mais compact */
}
```

### Impact sur la lisibilité

```css
/* ❌ Mauvais : trop serré, difficile à lire */
.bad {
  font-size: 16px;
  line-height: 1;
}

/* ✅ Bon : lisible et confortable */
.good {
  font-size: 16px;
  line-height: 1.6;
}
```

**Règle d'or** : Plus votre texte est long, plus vous avez besoin d'espace entre les lignes.

### Centrer verticalement avec line-height

Astuce : vous pouvez centrer verticalement du texte sur une ligne en faisant correspondre `line-height` et `height` :

```css
.button {
  height: 40px;
  line-height: 40px;  /* Centre le texte verticalement */
  text-align: center;  /* Centre le texte horizontalement */
}
```

**Note** : Cette technique fonctionne seulement pour une seule ligne de texte.

---

## Propriété raccourcie : font

### Qu'est-ce que c'est ?

La propriété `font` permet de définir plusieurs propriétés typographiques en une seule ligne.

### Syntaxe

```css
/* Syntaxe complète */
font: [font-style] [font-weight] font-size[/line-height] font-family;
```

**Important** :
- `font-size` et `font-family` sont **obligatoires**
- Les autres propriétés sont optionnelles
- L'ordre est important !

### Exemples

```css
/* Minimal : taille + famille */
p {
  font: 16px Arial, sans-serif;
}

/* Avec épaisseur */
h1 {
  font: bold 32px Georgia, serif;
}

/* Avec style */
blockquote {
  font: italic 18px "Times New Roman", serif;
}

/* Avec line-height */
.text {
  font: 16px/1.6 Arial, sans-serif;
  /* Équivaut à :
     font-size: 16px;
     line-height: 1.6;
     font-family: Arial, sans-serif;
  */
}

/* Complet */
.complete {
  font: italic bold 18px/1.8 Georgia, serif;
  /* Équivaut à :
     font-style: italic;
     font-weight: bold;
     font-size: 18px;
     line-height: 1.8;
     font-family: Georgia, serif;
  */
}
```

### Avantages et inconvénients

**Avantages** :
- Code plus court
- Moins de répétitions

**Inconvénients** :
- Moins lisible pour les débutants
- Réinitialise toutes les propriétés de police
- Ordre strict à respecter

**Recommandation** : Utilisez les propriétés séparées pour plus de clarté, surtout si vous débutez.

---

## Exemple complet : Système typographique

Voici un exemple de système typographique complet pour un site web :

```css
/* ===== CONFIGURATION DE BASE ===== */
html {
  font-size: 16px;  /* Taille de base pour rem */
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
               "Helvetica Neue", Arial, sans-serif;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.6;
  color: #333;
}

/* ===== TITRES ===== */
h1, h2, h3, h4, h5, h6 {
  font-weight: 700;
  line-height: 1.2;
  margin-top: 0;
  margin-bottom: 0.5em;
}

h1 {
  font-size: 2.5rem;    /* 40px */
}

h2 {
  font-size: 2rem;      /* 32px */
}

h3 {
  font-size: 1.5rem;    /* 24px */
}

h4 {
  font-size: 1.25rem;   /* 20px */
}

h5, h6 {
  font-size: 1rem;      /* 16px */
}

/* ===== TEXTE COURANT ===== */
p {
  margin-top: 0;
  margin-bottom: 1em;
}

/* ===== EMPHASES ===== */
strong, b {
  font-weight: 700;
}

em, i {
  font-style: italic;
}

/* ===== CLASSES UTILITAIRES ===== */
.text-small {
  font-size: 0.875rem;   /* 14px */
}

.text-large {
  font-size: 1.25rem;    /* 20px */
}

.text-light {
  font-weight: 300;
}

.text-bold {
  font-weight: 700;
}

.lead {
  font-size: 1.25rem;
  font-weight: 300;
  line-height: 1.8;
}

/* ===== CODE ===== */
code, pre {
  font-family: "Courier New", Courier, monospace;
  font-size: 0.875rem;
}

/* ===== CITATIONS ===== */
blockquote {
  font-style: italic;
  font-size: 1.125rem;
  line-height: 1.8;
}
```

---

## Bonnes pratiques

### 1. Définissez une taille de base sur `html`

```css
html {
  font-size: 16px;  /* ou 100% */
}
```

Cela facilite l'utilisation des `rem` dans tout votre code.

### 2. Utilisez `rem` pour les tailles de police

```css
/* ✅ Recommandé */
h1 {
  font-size: 2rem;
}

/* ❌ Moins flexible */
h1 {
  font-size: 32px;
}
```

### 3. Limitez le nombre de tailles différentes

Créez une échelle typographique cohérente avec 5-7 tailles maximum :

```css
:root {
  --font-size-xs: 0.75rem;   /* 12px */
  --font-size-sm: 0.875rem;  /* 14px */
  --font-size-base: 1rem;    /* 16px */
  --font-size-lg: 1.25rem;   /* 20px */
  --font-size-xl: 1.5rem;    /* 24px */
  --font-size-2xl: 2rem;     /* 32px */
  --font-size-3xl: 2.5rem;   /* 40px */
}
```

### 4. Assurez une bonne lisibilité

```css
body {
  font-size: 16px;           /* Minimum recommandé */
  line-height: 1.6;          /* Espace confortable */
  max-width: 65ch;           /* Largeur de ligne optimale */
}
```

**Note** : `65ch` = environ 65 caractères de largeur, idéal pour la lecture.

### 5. Utilisez des polices de secours

```css
/* ✅ Bon */
body {
  font-family: "Roboto", Arial, sans-serif;
}

/* ❌ Mauvais - pas de secours */
body {
  font-family: "Roboto";
}
```

### 6. Pensez à la performance

```css
/* Chargez seulement les épaisseurs nécessaires */
/* Au lieu de charger 100-900, chargez seulement : */
/* 400 (normal) et 700 (bold) */
```

### 7. Testez sur différents appareils

La typographie peut paraître différente selon :
- Le système d'exploitation (Windows, Mac, Linux)
- L'écran (retina ou non)
- La taille de l'écran

---

## Accessibilité et typographie

### Taille minimale

```css
/* ✅ Bon - lisible */
body {
  font-size: 16px;
}

/* ❌ Mauvais - trop petit */
body {
  font-size: 12px;
}
```

**Règle** : Ne descendez jamais en dessous de 16px (1rem) pour le texte principal.

### Contraste suffisant

Assurez-vous d'un bon contraste entre le texte et le fond :

```css
/* ✅ Bon contraste */
body {
  color: #333;              /* Gris foncé */
  background-color: #fff;   /* Blanc */
}

/* ❌ Mauvais contraste */
.bad {
  color: #ccc;              /* Gris clair sur blanc = difficile à lire */
  background-color: #fff;
}
```

### Permettre le zoom

Ne bloquez jamais le zoom sur mobile :

```html
<!-- ✅ Bon -->
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- ❌ Mauvais -->
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

---

## Résumé

| Propriété | Fonction | Valeur recommandée |
|-----------|----------|-------------------|
| **font-family** | Choix de la police | Liste avec secours : `Arial, sans-serif` |
| **font-size** | Taille du texte | `rem` (1rem = 16px par défaut) |
| **font-weight** | Épaisseur | 400 (normal), 700 (gras) |
| **font-style** | Style | `normal` ou `italic` |
| **line-height** | Hauteur de ligne | 1.5 à 1.6 pour le texte, 1.2 pour les titres |

### Points clés à retenir

- Utilisez **`rem`** pour les tailles de police (plus flexible que `px`)
- Définissez toujours une **police de secours** avec `font-family`
- Pour la lisibilité, visez un **`line-height` de 1.5 à 1.6** pour le texte courant
- Les valeurs de `font-weight` vont de **100 à 900** (400 = normal, 700 = gras)
- Une bonne typographie améliore grandement l'expérience utilisateur

La typographie est un art subtil : prenez le temps d'ajuster ces propriétés pour trouver le bon équilibre entre esthétique et lisibilité !

⏭️ [Texte : text-align, decoration, transform](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/03-texte.md)
