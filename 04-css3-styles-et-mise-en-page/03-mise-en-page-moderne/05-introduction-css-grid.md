🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3.5 - Introduction à CSS Grid

## Qu'est-ce que CSS Grid ?

CSS Grid (ou Grid Layout) est un système de mise en page **bidimensionnel** qui permet d'organiser des éléments dans des **lignes ET des colonnes** simultanément. C'est l'outil le plus puissant pour créer des layouts complexes en CSS.

### L'évolution des layouts CSS

```
📜 Années 2000 : Tables HTML (❌ mauvaise pratique)
    ↓
🎈 Années 2010 : Float + Position (⚠️ complexe)
    ↓
📦 2015 : Flexbox (✅ 1D - lignes OU colonnes)
    ↓
📐 2017 : CSS Grid (✅ 2D - lignes ET colonnes)
```

CSS Grid représente l'aboutissement de l'évolution des techniques de layout en CSS.

### Pourquoi Grid existe-t-il ?

Avant Grid, créer certains layouts était **très complexe** :

```html
<!-- ❌ Avant Grid : nécessitait beaucoup de divs imbriqués -->
<div class="wrapper">
  <div class="row">
    <div class="col-4">...</div>
    <div class="col-8">...</div>
  </div>
  <div class="row">
    <div class="col-6">...</div>
    <div class="col-6">...</div>
  </div>
</div>
```

```html
<!-- ✅ Avec Grid : structure claire et simple -->
<div class="grid">
  <div class="item-1">...</div>
  <div class="item-2">...</div>
  <div class="item-3">...</div>
  <div class="item-4">...</div>
</div>
```

---

## La puissance de Grid : Exemples visuels

### Ce que Grid peut faire facilement

#### Layout de page complet

```
┌──────────────────────────────────────┐
│           HEADER                     │
├──────────┬──────────────┬────────────┤
│ SIDEBAR  │    MAIN      │   ASIDE    │
│          │   CONTENT    │            │
│          │              │            │
├──────────┴──────────────┴────────────┤
│           FOOTER                     │
└──────────────────────────────────────┘
```

```css
/* Une seule déclaration Grid pour toute la structure ! */
.container {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
}
```

#### Galerie d'images responsive

```
┌────────────────────────────────────┐
│ [Img 1] [Img 2] [Img 3] [Img 4]    │
│ [Img 5] [Img 6] [Img 7] [Img 8]    │
│ [Img 9] [Img10] [Img11] [Img12]    │
└────────────────────────────────────┘
```

```css
.galerie {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}
```

#### Dashboard avec éléments de tailles variables

```
┌────────────────────────────────────┐
│ [  Widget 1    ] [W2] [W3]         │
│ [  (large)     ] [W4] [W5]         │
│ [W6] [W7] [W8] [W9] [W10]          │
└────────────────────────────────────┘
```

**Avec Grid, on peut facilement créer des éléments qui occupent plusieurs cellules !**

---

## Concepts fondamentaux de Grid

### 1. Le conteneur Grid (Grid Container)

C'est l'élément parent auquel on applique `display: grid`. Il devient un conteneur grid qui contrôle la disposition de ses enfants.

```css
.conteneur {
  display: grid;
}
```

### 2. Les éléments Grid (Grid Items)

Ce sont les **enfants directs** du conteneur grid. Ils seront automatiquement placés dans la grille.

```html
<div class="conteneur">
  <!-- Ces trois div sont des éléments grid -->
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

> **📌 Important** : Seuls les **enfants directs** deviennent des items grid, pas les petits-enfants.

---

## Terminologie de Grid

Pour bien comprendre Grid, il faut connaître quelques termes essentiels.

### Lignes de grille (Grid Lines)

Les **lignes** qui délimitent la grille. Elles sont numérotées à partir de 1.

```
    1       2       3       4
    ↓       ↓       ↓       ↓
1 → ┌───────┬───────┬───────┐
    │       │       │       │
2 → ├───────┼───────┼───────┤
    │       │       │       │
3 → ├───────┼───────┼───────┤
    │       │       │       │
4 → └───────┴───────┴───────┘
```

**Explication** :
- Lignes verticales : 1, 2, 3, 4
- Lignes horizontales : 1, 2, 3, 4
- Une grille 3×3 a 4 lignes verticales et 4 lignes horizontales

### Pistes (Grid Tracks)

Une **piste** est l'espace entre deux lignes adjacentes. C'est soit une **colonne** soit une **ligne**.

```
┌───────┬───────┬───────┐
│Piste 1│Piste 2│Piste 3│ ← Pistes colonnes
├───────┼───────┼───────┤
│       │       │       │   ← Piste ligne 1
├───────┼───────┼───────┤
│       │       │       │   ← Piste ligne 2
└───────┴───────┴───────┘
```

### Cellules (Grid Cells)

Une **cellule** est l'intersection d'une ligne et d'une colonne. C'est la plus petite unité de la grille.

```
┌───────┬───────┬───────┐
│Cell 1 │Cell 2 │Cell 3 │
├───────┼───────┼───────┤
│Cell 4 │Cell 5 │Cell 6 │
├───────┼───────┼───────┤
│Cell 7 │Cell 8 │Cell 9 │
└───────┴───────┴───────┘
```

### Zone (Grid Area)

Une **zone** est un espace rectangulaire composé d'une ou plusieurs cellules.

```
┌───────────────┬───────┐
│               │       │
│   Zone A      │ Zone B│
│   (2×2)       │       │
├───────┬───────┼───────┤
│Zone C │ Zone D│Zone E │
└───────┴───────┴───────┘
```

---

## Activer Grid : `display: grid`

Pour transformer un élément en conteneur grid, il suffit d'une ligne de CSS :

```css
.conteneur {
  display: grid;
}
```

### Que se passe-t-il quand on applique `display: grid` ?

1. Le conteneur devient un **conteneur grid**
2. Tous les **enfants directs** deviennent automatiquement des **items grid**
3. Par défaut, Grid crée **une seule colonne** et autant de lignes que nécessaire
4. Les items s'empilent verticalement (comme des `display: block`)

### Premier exemple

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Premier Grid</title>
  <style>
    .conteneur {
      display: grid;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .item {
      background-color: #4CAF50;
      color: white;
      padding: 20px;
      margin: 5px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item">Item 1</div>
    <div class="item">Item 2</div>
    <div class="item">Item 3</div>
  </div>
</body>
</html>
```

**Résultat visuel** (comportement par défaut) :

```
┌────────────────────┐
│      Item 1        │
├────────────────────┤
│      Item 2        │
├────────────────────┤
│      Item 3        │
└────────────────────┘
```

> **🤔 Question** : "Mais ça ressemble à du display: block normal !"

**Réponse** : C'est vrai ! Sans autres propriétés, Grid se comporte comme du block. La magie opère quand on définit des colonnes et des lignes.

---

## Créer une vraie grille : `grid-template-columns`

Pour créer des colonnes, on utilise `grid-template-columns` :

```css
.conteneur {
  display: grid;
  grid-template-columns: 200px 200px 200px; /* 3 colonnes de 200px */
}
```

### Exemple : Grille 3 colonnes

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Grille 3 colonnes</title>
  <style>
    .conteneur {
      display: grid;
      grid-template-columns: 200px 200px 200px;
      gap: 10px; /* Espacement entre les cellules */
      background-color: #f0f0f0;
      padding: 20px;
    }

    .item {
      background-color: #2196F3;
      color: white;
      padding: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
  </div>
</body>
</html>
```

**Résultat visuel :**

```
┌────────┬────────┬────────┐
│ Item 1 │ Item 2 │ Item 3 │
├────────┼────────┼────────┤
│ Item 4 │ Item 5 │ Item 6 │
└────────┴────────┴────────┘
```

**Ce qui se passe** :
- Grid crée 3 colonnes de 200px chacune
- Les items se placent automatiquement dans les cellules
- Quand une ligne est pleine, Grid crée une nouvelle ligne

---

## L'unité `fr` : La révolution de Grid

### Qu'est-ce que `fr` ?

`fr` signifie **"fraction"**. C'est une unité flexible qui représente une **fraction de l'espace disponible**.

```css
.conteneur {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* 3 colonnes égales */
}
```

### Comprendre `fr` avec des exemples

#### Exemple 1 : Colonnes égales

```css
.conteneur {
  grid-template-columns: 1fr 1fr 1fr;
}
```

**Calcul** :
- Total : 1 + 1 + 1 = 3 fractions
- Colonne 1 : 1/3 de l'espace = 33.33%
- Colonne 2 : 1/3 de l'espace = 33.33%
- Colonne 3 : 1/3 de l'espace = 33.33%

```
┌────────────┬────────────┬────────────┐
│    33%     │    33%     │    33%     │
└────────────┴────────────┴────────────┘
```

#### Exemple 2 : Colonnes inégales

```css
.conteneur {
  grid-template-columns: 2fr 1fr 1fr;
}
```

**Calcul** :
- Total : 2 + 1 + 1 = 4 fractions
- Colonne 1 : 2/4 de l'espace = 50%
- Colonne 2 : 1/4 de l'espace = 25%
- Colonne 3 : 1/4 de l'espace = 25%

```
┌──────────────────┬─────────┬─────────┐
│       50%        │   25%   │   25%   │
└──────────────────┴─────────┴─────────┘
```

#### Exemple 3 : Mélange `fr` et pixels

```css
.conteneur {
  grid-template-columns: 200px 1fr 1fr;
}
```

**Calcul** :
- 200px sont réservés pour la première colonne
- L'espace restant est divisé en 2 (1fr + 1fr)
- Si le conteneur fait 800px :
  - Colonne 1 : 200px (fixe)
  - Espace restant : 800px - 200px = 600px
  - Colonne 2 : 300px (1/2 de 600px)
  - Colonne 3 : 300px (1/2 de 600px)

```
┌──────┬──────────────┬──────────────┐
│200px │     300px    │     300px    │
│(fixe)│   (flexible) │   (flexible) │
└──────┴──────────────┴──────────────┘
```

### Pourquoi `fr` est génial ?

- ✅ **Responsive automatique** : s'adapte à la taille du conteneur
- ✅ **Simple** : pas de calculs de pourcentages complexes
- ✅ **Flexible** : se combine avec des tailles fixes
- ✅ **Intuitif** : les ratios sont clairs (1:2:1, etc.)

---

## La fonction `repeat()` : Éviter la répétition

Au lieu d'écrire la même valeur plusieurs fois, on utilise `repeat()` :

### Syntaxe

```css
grid-template-columns: repeat(nombre, taille);
```

### Exemples

#### Sans `repeat()` ❌

```css
.conteneur {
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
}
```

#### Avec `repeat()` ✅

```css
.conteneur {
  grid-template-columns: repeat(6, 1fr);
}
```

**Les deux sont identiques !**

### Exemples avancés

```css
/* 4 colonnes égales */
grid-template-columns: repeat(4, 1fr);

/* 3 colonnes de 200px */
grid-template-columns: repeat(3, 200px);

/* Pattern répété */
grid-template-columns: repeat(2, 1fr 2fr);
/* Équivalent à : 1fr 2fr 1fr 2fr */
```

---

## Espacement : La propriété `gap`

Grid offre une propriété simple pour espacer les cellules : `gap`.

### Syntaxe

```css
.conteneur {
  display: grid;
  gap: 20px; /* Espacement de 20px entre toutes les cellules */
}
```

### Différentes syntaxes de `gap`

```css
/* Même espacement partout */
gap: 20px;

/* Espacement lignes / colonnes */
gap: 20px 30px;
/*  ↑      ↑
  lignes colonnes */

/* Ou séparément */
row-gap: 20px;
column-gap: 30px;
```

### Exemple visuel

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

```
┌──────┐   ┌──────┐   ┌──────┐
│Item 1│   │Item 2│   │Item 3│
└──────┘   └──────┘   └──────┘
   ↑ 20px entre les colonnes

   ↓ 20px entre les lignes

┌──────┐   ┌──────┐   ┌──────┐
│Item 4│   │Item 5│   │Item 6│
└──────┘   └──────┘   └──────┘
```

### Avantage de `gap` sur `margin`

```css
/* ❌ Avec margin, il faut gérer les bords */
.item {
  margin: 10px;
}
/* Problème : margin aussi sur les bords extérieurs */

/* ✅ Avec gap, espacement uniquement entre les items */
.conteneur {
  gap: 20px;
}
/* Parfait : pas d'espace sur les bords ! */
```

---

## Lignes : `grid-template-rows`

Comme pour les colonnes, on peut définir la hauteur des lignes :

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 200px 100px; /* 3 lignes de hauteurs différentes */
}
```

**Résultat visuel :**

```
┌──────┬──────┬──────┐
│      │      │      │  ← 100px
├──────┼──────┼──────┤
│      │      │      │
│      │      │      │  ← 200px
├──────┼──────┼──────┤
│      │      │      │  ← 100px
└──────┴──────┴──────┘
```

### Hauteur automatique

Si on ne spécifie pas `grid-template-rows`, la hauteur des lignes s'adapte automatiquement au contenu :

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  /* Pas de grid-template-rows : hauteur automatique */
}
```

**C'est souvent le comportement souhaité !**

---

## Exemple complet : Galerie d'images

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Galerie Grid</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-color: #f5f5f5;
    }

    h1 {
      text-align: center;
      margin-bottom: 30px;
      color: #333;
    }

    .galerie {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .photo {
      background-color: #ddd;
      height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 8px;
      font-size: 24px;
      color: #666;
      transition: transform 0.3s;
    }

    .photo:hover {
      transform: scale(1.05);
    }
  </style>
</head>
<body>
  <h1>Ma Galerie Photos</h1>

  <div class="galerie">
    <div class="photo">Photo 1</div>
    <div class="photo">Photo 2</div>
    <div class="photo">Photo 3</div>
    <div class="photo">Photo 4</div>
    <div class="photo">Photo 5</div>
    <div class="photo">Photo 6</div>
    <div class="photo">Photo 7</div>
    <div class="photo">Photo 8</div>
  </div>
</body>
</html>
```

**Ce que fait le code** :
- `display: grid` : active Grid
- `grid-template-columns: repeat(4, 1fr)` : 4 colonnes égales
- `gap: 20px` : espace de 20px entre les photos
- Les 8 photos se placent automatiquement dans la grille !

---

## Grid vs Block par défaut

### Sans Grid (comportement normal)

```html
<div class="conteneur">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```

```css
/* Pas de display: grid */
.item {
  background-color: lightblue;
  padding: 20px;
}
```

**Résultat** : Les éléments s'empilent verticalement.

```
┌────────────────────┐
│      Item 1        │
├────────────────────┤
│      Item 2        │
├────────────────────┤
│      Item 3        │
└────────────────────┘
```

### Avec Grid

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

**Résultat** : Les éléments forment une grille.

```
┌──────┬──────┬──────┐
│Item 1│Item 2│Item 3│
└──────┴──────┴──────┘
```

---

## Placement automatique des items

Par défaut, Grid place les items **automatiquement** de gauche à droite, puis crée une nouvelle ligne quand nécessaire.

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

```html
<div class="conteneur">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
</div>
```

**Placement automatique :**

```
┌───┬───┬───┐
│ 1 │ 2 │ 3 │  ← Ligne 1 (créée automatiquement)
├───┼───┼───┤
│ 4 │ 5 │   │  ← Ligne 2 (créée automatiquement)
└───┴───┴───┘
```

**C'est magique !** Grid gère tout automatiquement.

---

## Comparaison : Grid vs Flexbox

### Flexbox : Une direction

```css
.flex-container {
  display: flex;
  gap: 10px;
}
```

```
┌────┬────┬────┬────┬────┐
│ 1  │ 2  │ 3  │ 4  │ 5  │  ← Une seule ligne
└────┴────┴────┴────┴────┘
```

**Pour avoir plusieurs lignes, il faut `flex-wrap`**

### Grid : Deux dimensions

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

```
┌───┬───┬───┐
│ 1 │ 2 │ 3 │  ← Ligne 1
├───┼───┼───┤
│ 4 │ 5 │   │  ← Ligne 2 (automatique)
└───┴───┴───┘
```

**Grid crée automatiquement des lignes ET des colonnes**

---

## Propriétés Grid de base : Récapitulatif

### Sur le conteneur Grid

```css
.conteneur {
  /* Activer Grid */
  display: grid;

  /* Définir les colonnes */
  grid-template-columns: repeat(3, 1fr);

  /* Définir les lignes (optionnel) */
  grid-template-rows: 100px 200px;

  /* Espacement */
  gap: 20px;
}
```

### Unités disponibles

```css
/* Pixels (fixe) */
grid-template-columns: 200px 300px 200px;

/* Fractions (flexible) */
grid-template-columns: 1fr 2fr 1fr;

/* Pourcentages */
grid-template-columns: 25% 50% 25%;

/* Mélange */
grid-template-columns: 200px 1fr 1fr;

/* Auto (s'adapte au contenu) */
grid-template-columns: auto 1fr auto;
```

---

## Cas d'usage courants

### 1. Grille d'images régulière

```css
.galerie {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
}
```

### 2. Layout simple 2 colonnes

```css
.conteneur {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 20px;
}
```

```
┌───────┬──────────────────┐
│ 300px │   Reste          │
│ (fixe)│   (flexible)     │
└───────┴──────────────────┘
```

### 3. Grille responsive simple

```css
.produits {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

**S'adapte automatiquement à la largeur du conteneur !**

---

## Points clés à retenir

✅ **Grid est bidimensionnel** : lignes ET colonnes simultanément

✅ **`display: grid`** active Grid sur le conteneur

✅ **`grid-template-columns`** définit les colonnes

✅ **`fr`** est l'unité flexible de Grid (comme `flex: 1` mais plus puissant)

✅ **`repeat()`** évite les répétitions

✅ **`gap`** crée des espacements propres entre les cellules

✅ **Placement automatique** : Grid place les items intelligemment

✅ **Terminologie** : lignes de grille, pistes, cellules, zones

---

## Différences importantes avec Flexbox

| Caractéristique | Flexbox | Grid |
|-----------------|---------|------|
| **Dimensions** | 1D (ligne OU colonne) | 2D (lignes ET colonnes) |
| **Placement** | Séquentiel | Cellules définies |
| **Flexibilité** | Basée sur le contenu | Basée sur la structure |
| **Use case** | Composants, navigation | Layouts, grilles |
| **Complexité** | Plus simple | Plus puissant |

---

## Ce que Grid NE fait PAS (pour l'instant)

Dans cette introduction, nous n'avons vu que les bases. Grid peut faire **beaucoup plus** :

- 🔲 Placer manuellement les items dans des cellules spécifiques
- 🔲 Créer des items qui s'étendent sur plusieurs cellules
- 🔲 Définir des zones nommées (grid-template-areas)
- 🔲 Aligner les items dans leurs cellules
- 🔲 Créer des grilles responsive complexes
- 🔲 Superposer des éléments

**Nous verrons tout cela dans les prochaines leçons !**

---

## Exemple pratique : Card Layout

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Card Layout Grid</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      padding: 40px;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 30px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .card {
      background: white;
      border-radius: 10px;
      padding: 30px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 6px 12px rgba(0,0,0,0.15);
    }

    .card h2 {
      color: #333;
      margin-bottom: 15px;
    }

    .card p {
      color: #666;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="card">
      <h2>Service 1</h2>
      <p>Description du premier service. Grid permet de créer des layouts propres et organisés.</p>
    </div>

    <div class="card">
      <h2>Service 2</h2>
      <p>Description du deuxième service. Les cartes s'adaptent automatiquement.</p>
    </div>

    <div class="card">
      <h2>Service 3</h2>
      <p>Description du troisième service. L'espacement est uniforme grâce à gap.</p>
    </div>

    <div class="card">
      <h2>Service 4</h2>
      <p>Grid crée automatiquement une nouvelle ligne quand nécessaire.</p>
    </div>

    <div class="card">
      <h2>Service 5</h2>
      <p>Tout est responsive par défaut avec les unités fr.</p>
    </div>

    <div class="card">
      <h2>Service 6</h2>
      <p>Simple, puissant, et moderne. C'est Grid !</p>
    </div>
  </div>
</body>
</html>
```

**Avec seulement 3 lignes de CSS Grid** :
```css
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 30px;
```

Nous obtenons un layout professionnel et responsive !

---

## Conclusion

CSS Grid est un **outil puissant** qui révolutionne la création de layouts en CSS. Dans cette introduction, nous avons vu :

- **Comment activer Grid** avec `display: grid`
- **Créer des colonnes** avec `grid-template-columns`
- **L'unité `fr`** pour des colonnes flexibles
- **La fonction `repeat()`** pour éviter les répétitions
- **La propriété `gap`** pour espacer les cellules
- **Le placement automatique** des items

### Ce n'est que le début !

Dans les prochaines leçons, nous explorerons :
- Le positionnement manuel des items
- Les items qui s'étendent sur plusieurs cellules
- Les grilles nommées avec `grid-template-areas`
- L'alignement précis avec `justify-items` et `align-items`
- Les techniques responsive avancées

Grid est un **investissement** qui en vaut la peine. Une fois maîtrisé, vous pourrez créer pratiquement n'importe quel layout complexe avec simplicité et élégance.

---


Dans la prochaine leçon, nous approfondirons les propriétés de colonnes et de lignes, et découvrirons des techniques plus avancées !

⏭️ [Grid : grid-template-columns/rows, grid-gap](/04-css3-styles-et-mise-en-page/03-mise-en-page-moderne/06-grid-template-et-gap.md)
