🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.5.4 - Unités relatives : %, em, rem, vw, vh

## Introduction

En CSS, vous pouvez définir des tailles de deux manières : avec des **unités absolues** (comme les pixels) ou des **unités relatives**. Les unités relatives sont essentielles pour créer des designs flexibles et réellement responsive.

Au lieu de dire "cette boîte fait 300 pixels", on peut dire "cette boîte fait 50% de son conteneur" ou "ce texte fait 1.5 fois la taille de base". Le design s'adapte ainsi automatiquement !

## Unités absolues vs Unités relatives

### Unités absolues (fixes)

Les unités absolues ont une **taille fixe** qui ne change pas.

```css
.element {
    width: 300px;     /* 300 pixels, toujours */
    font-size: 16px;  /* 16 pixels, toujours */
    margin: 20px;     /* 20 pixels, toujours */
}
```

**Principales unités absolues :**
- `px` (pixels) - la plus courante
- `cm`, `mm` (centimètres, millimètres) - rarement utilisés sur le web
- `pt` (points) - principalement pour l'impression

**Problème :** 300px sur un smartphone de 375px de large, c'est énorme ! Sur un écran 4K de 3840px, c'est minuscule.

### Unités relatives (flexibles) ✅

Les unités relatives se **calculent par rapport à autre chose**.

```css
.element {
    width: 50%;        /* 50% de son conteneur parent */
    font-size: 1.5rem; /* 1.5 fois la taille de base */
    padding: 2em;      /* 2 fois la taille de police de cet élément */
}
```

**Avantage :** Le design s'adapte automatiquement selon le contexte !

**Principales unités relatives :**
- `%` (pourcentage)
- `em` (relatif à la taille de police de l'élément)
- `rem` (relatif à la taille de police racine)
- `vw` (viewport width - largeur du viewport)
- `vh` (viewport height - hauteur du viewport)
- `vmin`, `vmax` (plus petite/grande dimension du viewport)

## Le pourcentage (%)

### Principe de base

Le **pourcentage** est relatif à la **dimension correspondante du parent**.

```css
.parent {
    width: 1000px;
}

.enfant {
    width: 50%; /* = 500px (50% de 1000px) */
}
```

### Comportement selon la propriété

#### Pour width (largeur)

```css
.conteneur {
    width: 800px;
}

.element {
    width: 75%; /* = 600px (75% de 800px) */
}
```

**Le pourcentage se calcule sur la largeur du parent.**

#### Pour height (hauteur)

```css
.conteneur {
    height: 400px;
}

.element {
    height: 50%; /* = 200px (50% de 400px) */
}
```

**⚠️ Attention :** Si le parent n'a pas de hauteur définie, `height: 50%` ne fonctionnera pas comme prévu !

#### Pour padding et margin

```css
.element {
    width: 500px;
    padding: 10%; /* = 50px (10% de 500px) */
}
```

**📌 Important :** Pour `padding` et `margin`, le pourcentage se calcule **toujours sur la largeur** du parent, même pour `padding-top` et `padding-bottom` !

```css
.parent {
    width: 1000px;
}

.element {
    padding-top: 10%;    /* = 100px (10% de la LARGEUR du parent) */
    padding-bottom: 10%; /* = 100px (10% de la LARGEUR du parent) */
}
```

**C'est surprenant mais c'est comme ça !** 😅

### Exemples pratiques

#### Exemple 1 : Layout à deux colonnes

```css
.conteneur {
    width: 100%;
    display: flex;
}

.colonne-gauche {
    width: 30%; /* Prend 30% de la largeur */
}

.colonne-droite {
    width: 70%; /* Prend 70% de la largeur */
}
```

#### Exemple 2 : Image responsive

```css
img {
    width: 100%;  /* Prend 100% de la largeur du parent */
    height: auto; /* Conserve les proportions */
}
```

#### Exemple 3 : Conteneur centré avec marges

```css
.conteneur {
    width: 90%;        /* 90% de la largeur de l'écran */
    max-width: 1200px; /* Mais pas plus de 1200px */
    margin: 0 auto;    /* Centré horizontalement */
}
```

### Quand utiliser % ?

**✅ Utilisez % pour :**
- Les largeurs (`width`)
- Les layouts en colonnes
- Les images qui doivent s'adapter à leur conteneur
- Centrer des éléments avec `margin: 0 auto`

**❌ Évitez % pour :**
- Les tailles de police (utilisez `rem` ou `em`)
- Les éléments qui doivent garder une taille minimum (préférez `min-width`)

## L'unité em

### Principe de base

**1em** = la taille de police **de l'élément lui-même** (ou héritée de son parent).

```css
.element {
    font-size: 20px;
    padding: 2em; /* = 40px (2 × 20px) */
    margin: 1em;  /* = 20px (1 × 20px) */
}
```

### Comprendre le calcul

```css
body {
    font-size: 16px; /* Taille de base */
}

.texte {
    font-size: 20px;
    padding: 1.5em; /* = 30px (1.5 × 20px) */
}

.petit {
    font-size: 14px;
    padding: 1.5em; /* = 21px (1.5 × 14px) */
}
```

**Chaque élément calcule `em` selon SA propre taille de police.**

### L'effet de cascade (attention !)

```css
body {
    font-size: 16px;
}

.niveau1 {
    font-size: 1.5em; /* = 24px (1.5 × 16px) */
}

.niveau2 {
    font-size: 1.5em; /* = 36px (1.5 × 24px) - Hérité de .niveau1 ! */
}

.niveau3 {
    font-size: 1.5em; /* = 54px (1.5 × 36px) - Encore plus grand ! */
}
```

**HTML :**
```html
<div class="niveau1">
    Texte niveau 1 (24px)
    <div class="niveau2">
        Texte niveau 2 (36px)
        <div class="niveau3">
            Texte niveau 3 (54px)
        </div>
    </div>
</div>
```

**⚠️ Problème :** L'effet se multiplie à chaque niveau ! Cela peut vite devenir incontrôlable.

### Exemples pratiques

#### Exemple 1 : Padding proportionnel à la taille de texte

```css
.bouton {
    font-size: 16px;
    padding: 0.75em 1.5em; /* S'adapte à la taille de police */
    /* = padding: 12px 24px */
}

.bouton-grand {
    font-size: 20px;
    padding: 0.75em 1.5em; /* Même code, mais plus grand ! */
    /* = padding: 15px 30px */
}
```

**Avantage :** Créez un bouton, changez juste la taille de police, le padding s'adapte automatiquement !

#### Exemple 2 : Espacement cohérent

```css
.section {
    font-size: 18px;
    padding: 2em;      /* 36px */
    margin-bottom: 1em; /* 18px */
}

.section h2 {
    margin-bottom: 0.5em; /* 9px */
}
```

### Quand utiliser em ?

**✅ Utilisez em pour :**
- `padding` et `margin` quand vous voulez qu'ils soient proportionnels à la taille de police
- Créer des composants modulaires (comme des boutons)
- Les espacements à l'intérieur d'un élément

**❌ Évitez em pour :**
- Les tailles de police (l'effet de cascade peut être problématique)
- Les largeurs et hauteurs (préférez `%` ou `rem`)

## L'unité rem (Root em) 🆕

### Principe de base

**1rem** = la taille de police de **l'élément racine** (`<html>`), toujours.

Par défaut, les navigateurs utilisent `16px` pour `<html>`.

```css
/* Par défaut */
html {
    font-size: 16px; /* Défini par le navigateur */
}

.element {
    font-size: 1rem;   /* = 16px */
    font-size: 1.5rem; /* = 24px */
    font-size: 2rem;   /* = 32px */
}
```

### Différence avec em

**em** : relatif à l'élément lui-même
**rem** : relatif à la racine (`<html>`), **toujours**

```css
html {
    font-size: 16px;
}

.niveau1 {
    font-size: 1.5rem; /* = 24px (1.5 × 16px) */
}

.niveau2 {
    font-size: 1.5rem; /* = 24px (1.5 × 16px) - Même taille ! */
}

.niveau3 {
    font-size: 1.5rem; /* = 24px (1.5 × 16px) - Toujours pareil ! */
}
```

**✅ Avantage :** Pas d'effet de cascade, tout est prévisible !

### Exemple comparatif

```css
html {
    font-size: 16px;
}

/* Avec EM */
.parent-em {
    font-size: 20px;
}

.enfant-em {
    font-size: 1.5em;  /* = 30px (1.5 × 20px du parent) */
    padding: 2em;       /* = 60px (2 × 30px de lui-même) */
}

/* Avec REM */
.parent-rem {
    font-size: 20px; /* N'a aucun impact sur rem ! */
}

.enfant-rem {
    font-size: 1.5rem; /* = 24px (1.5 × 16px de html) */
    padding: 2rem;     /* = 32px (2 × 16px de html) */
}
```

### Définir une base personnalisée

Beaucoup de développeurs définissent une base à 10px pour faciliter les calculs :

```css
html {
    font-size: 62.5%; /* 62.5% de 16px = 10px */
}

body {
    font-size: 1.6rem; /* = 16px */
}

h1 {
    font-size: 3.2rem; /* = 32px */
}

.petit-texte {
    font-size: 1.4rem; /* = 14px */
}
```

**Avantage :** Facile à calculer mentalement (1.6rem = 16px, 2rem = 20px, etc.)

### Exemples pratiques

#### Exemple 1 : Système de tailles cohérent

```css
html {
    font-size: 16px;
}

body {
    font-size: 1rem; /* 16px */
}

h1 {
    font-size: 2.5rem;   /* 40px */
    margin-bottom: 1rem; /* 16px */
}

h2 {
    font-size: 2rem;     /* 32px */
    margin-bottom: 1rem; /* 16px */
}

p {
    font-size: 1rem;       /* 16px */
    margin-bottom: 1.5rem; /* 24px */
    line-height: 1.6;
}
```

#### Exemple 2 : Responsive avec rem

```css
html {
    font-size: 16px; /* Base mobile */
}

/* Sur tablette, on augmente la base */
@media (min-width: 768px) {
    html {
        font-size: 18px;
    }
    /* Tous les rem s'adaptent automatiquement ! */
}

/* Sur desktop */
@media (min-width: 1024px) {
    html {
        font-size: 20px;
    }
}

/* Le reste du CSS n'a pas besoin de changer */
.titre {
    font-size: 2rem; /* 32px mobile, 36px tablette, 40px desktop */
}
```

**🎯 Technique puissante :** En changeant juste `font-size` sur `html`, tout le site s'adapte !

### Quand utiliser rem ?

**✅ Utilisez rem pour :**
- Les tailles de police (recommandé !)
- Les espacements globaux (`margin`, `padding`)
- Tout ce qui doit être cohérent dans tout le site
- Les media queries pour un scaling global

**❌ Évitez rem pour :**
- Les bordures (généralement 1px suffit)
- Les composants qui doivent être vraiment indépendants

## Les unités viewport : vw et vh

### Le viewport

Le **viewport** est la zone visible du navigateur (la fenêtre).

**Rappel :** Sur desktop, c'est la fenêtre du navigateur. Sur mobile, c'est l'écran de l'appareil.

### vw (Viewport Width)

**1vw** = 1% de la **largeur du viewport**

```css
.element {
    width: 50vw; /* 50% de la largeur du viewport */
}
```

**Exemples concrets :**
- Viewport de 1000px de large : `1vw = 10px`, donc `50vw = 500px`
- Viewport de 375px de large (mobile) : `1vw = 3.75px`, donc `50vw = 187.5px`

### vh (Viewport Height)

**1vh** = 1% de la **hauteur du viewport**

```css
.element {
    height: 100vh; /* 100% de la hauteur du viewport */
}
```

**Exemples concrets :**
- Viewport de 800px de haut : `1vh = 8px`, donc `100vh = 800px`
- Viewport de 667px de haut (iPhone) : `1vh = 6.67px`, donc `100vh = 667px`

### Différence avec %

```css
.parent {
    height: 400px;
}

.enfant-pourcent {
    height: 50%; /* 50% du parent = 200px */
}

.enfant-vh {
    height: 50vh; /* 50% du VIEWPORT (pas du parent) */
    /* Si viewport = 800px de haut, alors 50vh = 400px */
}
```

**📌 Important :**
- `%` : relatif au **parent**
- `vh`/`vw` : relatif au **viewport** (toute la fenêtre)

### Exemples pratiques

#### Exemple 1 : Hero section plein écran

```css
.hero {
    width: 100vw;
    height: 100vh; /* Prend tout l'écran */
    background-image: url('hero.jpg');
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

**Résultat :** Une section qui occupe exactement tout l'écran, quelle que soit sa taille !

#### Exemple 2 : Typographie fluide

```css
h1 {
    font-size: 5vw; /* S'adapte à la largeur de l'écran */
}
```

**Exemples :**
- Sur 1920px de large : `5vw = 96px`
- Sur 768px de large : `5vw = 38.4px`
- Sur 375px de large : `5vw = 18.75px`

**⚠️ Attention :** Le texte peut devenir trop grand ou trop petit. Solution : combiner avec `clamp()` (voir plus bas).

#### Exemple 3 : Sidebar fixe

```css
.sidebar {
    width: 25vw;        /* 25% de la largeur du viewport */
    height: 100vh;      /* Toute la hauteur du viewport */
    position: fixed;
    left: 0;
    top: 0;
}

.contenu {
    margin-left: 25vw;  /* Pour éviter le chevauchement */
    padding: 2rem;
}
```

### vmin et vmax

**vmin** = la plus **petite** dimension entre la largeur et la hauteur
**vmax** = la plus **grande** dimension entre la largeur et la hauteur

```css
/* Viewport 1920px × 1080px */
/* vmin = 1080px (la plus petite) */
/* vmax = 1920px (la plus grande) */

.element {
    width: 50vmin;  /* = 540px (50% de 1080px) */
    height: 50vmax; /* = 960px (50% de 1920px) */
}
```

**Usage :** Rarement utilisés, mais utiles pour créer des éléments carrés ou des designs qui s'adaptent à l'orientation.

```css
/* Carré qui s'adapte toujours */
.carre {
    width: 50vmin;
    height: 50vmin; /* Toujours carré */
}
```

### Problème mobile avec vh

Sur mobile, la barre d'adresse du navigateur peut apparaître/disparaître, ce qui change la hauteur du viewport.

```css
.hero {
    height: 100vh; /* Peut causer des problèmes sur mobile */
}
```

**Solution moderne :** Utiliser les nouvelles unités `dvh` (dynamic viewport height) ou JavaScript, mais c'est plus avancé.

**Solution simple :** Ajouter un `min-height` :

```css
.hero {
    min-height: 100vh;
    height: auto;
}
```

### Quand utiliser vw/vh ?

**✅ Utilisez vw/vh pour :**
- Les sections plein écran
- Les overlays/modales
- Les éléments qui doivent toujours être visibles
- Les designs créatifs

**❌ Évitez vw/vh pour :**
- Les tailles de police seules (risque de texte illisible)
- Les petits éléments (préférez `rem` ou `%`)

## Combinaisons et techniques avancées

### La fonction clamp() 🆕

**clamp()** permet de définir une valeur min, idéale et max en une seule ligne !

```css
.element {
    font-size: clamp(16px, 4vw, 32px);
    /* Min: 16px, Idéal: 4vw, Max: 32px */
}
```

**Comportement :**
- Si `4vw < 16px` → `16px`
- Si `16px < 4vw < 32px` → `4vw` (fluide)
- Si `4vw > 32px` → `32px`

**Exemple pratique : Typographie fluide**

```css
h1 {
    font-size: clamp(24px, 5vw, 48px);
    /* Mobile: 24px minimum, Desktop: jusqu'à 48px */
}

p {
    font-size: clamp(16px, 2vw, 20px);
}
```

### Combiner plusieurs unités

```css
.conteneur {
    width: 90%;              /* 90% du parent */
    max-width: 1200px;       /* Mais pas plus de 1200px */
    margin: 2rem auto;       /* Marges en rem, centré */
    padding: 5vw;            /* Padding relatif au viewport */
    min-height: 50vh;        /* Au moins 50% de la hauteur du viewport */
}
```

### Calc() : faire des calculs

```css
.element {
    width: calc(100% - 40px);           /* 100% moins 40px */
    height: calc(100vh - 80px);         /* Toute la hauteur moins le header */
    padding: calc(2rem + 1vw);          /* Combinaison de rem et vw */
    margin-left: calc(50% - 600px);     /* Centrage personnalisé */
}
```

**Exemple pratique : Layout avec sidebar fixe**

```css
.sidebar {
    width: 300px;
    position: fixed;
}

.contenu {
    width: calc(100% - 300px); /* Toute la largeur moins la sidebar */
    margin-left: 300px;
}
```

## Tableau récapitulatif

| Unité | Relatif à | Usage principal | Exemple |
|-------|-----------|-----------------|---------|
| `%` | Dimension correspondante du **parent** | Largeurs, layouts | `width: 50%` |
| `em` | Taille de police de **l'élément** | Padding/margin proportionnels | `padding: 1.5em` |
| `rem` | Taille de police de **html** (racine) | Tailles de police, espacements | `font-size: 1.5rem` |
| `vw` | 1% de la **largeur du viewport** | Éléments plein écran, typo fluide | `width: 100vw` |
| `vh` | 1% de la **hauteur du viewport** | Sections plein écran | `height: 100vh` |
| `vmin` | 1% de la plus **petite** dimension | Éléments carrés adaptatifs | `width: 50vmin` |
| `vmax` | 1% de la plus **grande** dimension | Designs créatifs | `width: 50vmax` |

## Bonnes pratiques

### 1. Choisir la bonne unité pour chaque usage

```css
/* ✅ RECOMMANDÉ */
.element {
    /* Tailles de police : rem */
    font-size: 1.5rem;

    /* Espacements : rem ou em */
    margin: 2rem;
    padding: 1.5em;

    /* Largeurs : % avec max-width en px ou rem */
    width: 90%;
    max-width: 1200px;

    /* Bordures : px */
    border: 1px solid #ccc;
}
```

### 2. Définir une base cohérente

```css
/* Base du site */
html {
    font-size: 16px; /* ou 62.5% pour base 10px */
}

body {
    font-size: 1rem;
    line-height: 1.6;
}
```

### 3. Utiliser des variables CSS

```css
:root {
    --font-size-base: 1rem;
    --font-size-lg: 1.25rem;
    --font-size-xl: 1.5rem;
    --font-size-2xl: 2rem;

    --spacing-sm: 0.5rem;
    --spacing-md: 1rem;
    --spacing-lg: 2rem;
}

.titre {
    font-size: var(--font-size-2xl);
    margin-bottom: var(--spacing-lg);
}
```

### 4. Responsive avec rem

```css
/* Changez juste la base, tout s'adapte ! */
html {
    font-size: 14px; /* Mobile */
}

@media (min-width: 768px) {
    html {
        font-size: 16px; /* Tablette */
    }
}

@media (min-width: 1024px) {
    html {
        font-size: 18px; /* Desktop */
    }
}

/* Le reste reste identique */
.conteneur {
    padding: 2rem; /* S'adapte automatiquement ! */
}
```

## Erreurs courantes

### ❌ Erreur 1 : Utiliser em pour les font-size imbriqués

```css
/* MAUVAIS */
.parent {
    font-size: 1.5em;
}

.enfant {
    font-size: 1.5em; /* Se multiplie ! */
}
```

**Solution :** Utilisez `rem` pour les tailles de police.

### ❌ Erreur 2 : Oublier max-width avec %

```css
/* MAUVAIS - Trop large sur grand écran */
.conteneur {
    width: 100%;
}

/* BON */
.conteneur {
    width: 90%;
    max-width: 1200px;
}
```

### ❌ Erreur 3 : vw pour les tailles de police sans limite

```css
/* MAUVAIS - Peut devenir illisible */
h1 {
    font-size: 5vw;
}

/* BON - Avec limites */
h1 {
    font-size: clamp(24px, 5vw, 48px);
}
```

### ❌ Erreur 4 : Mélanger les unités sans réfléchir

```css
/* CONFUS */
.element {
    width: 50%;
    padding: 20px;
    margin: 1.5em;
    font-size: 2vw;
}

/* MIEUX - Cohérent */
.element {
    width: 50%;
    padding: 1.5rem;
    margin: 1rem;
    font-size: 1.25rem;
}
```

## Récapitulatif

Les **unités relatives** sont essentielles pour créer des designs flexibles et responsive.

**Unités principales :**
- **`%`** : relatif au parent (largeurs principalement)
- **`rem`** : relatif à la racine (tailles de police, espacements) ⭐ **Le plus utilisé**
- **`em`** : relatif à l'élément (padding/margin proportionnels)
- **`vw`/`vh`** : relatif au viewport (sections plein écran)

**Recommandations :**
- Tailles de police → `rem`
- Espacements globaux → `rem`
- Espacements proportionnels → `em`
- Largeurs → `%` + `max-width`
- Sections plein écran → `vw`/`vh`
- Bordures → `px`

**Technique puissante :**
```css
html {
    font-size: 16px; /* Mobile */
}

@media (min-width: 768px) {
    html {
        font-size: 18px; /* Tout s'adapte ! */
    }
}
```

---

**📚 Points à retenir :**

- Les unités relatives rendent votre design **flexible** et **adaptable**
- **`rem`** est l'unité moderne recommandée pour la plupart des usages
- **`em`** a un effet de cascade, `rem` non
- **`vw`/`vh`** sont parfaits pour les sections plein écran
- Utilisez `clamp()` pour créer des designs vraiment fluides
- **Combinez** les unités intelligemment avec `calc()`

**🔜 Prochaine étape :**
Dans la section suivante (4.5.5), nous verrons comment rendre les **images responsives** avec les bonnes techniques et attributs HTML.

**💡 Astuce de pro :**
Créez un système de design avec des variables CSS utilisant `rem`. Vous pourrez ajuster tout votre site en changeant quelques valeurs seulement !

⏭️ [Images responsives](/04-css3-styles-et-mise-en-page/05-responsive-design/05-images-responsives.md)
