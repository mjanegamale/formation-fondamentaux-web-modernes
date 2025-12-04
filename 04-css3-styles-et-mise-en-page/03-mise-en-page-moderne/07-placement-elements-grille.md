🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3.7 - Placement d'éléments dans la grille

## Introduction

Jusqu'à présent, nous avons laissé Grid **placer automatiquement** les items dans les cellules. Mais l'une des forces de Grid est de pouvoir **contrôler précisément** où chaque élément se place et combien de cellules il occupe.

Dans cette leçon, nous allons découvrir comment :
- Placer un item dans une cellule spécifique
- Faire qu'un item s'étende sur plusieurs colonnes ou lignes
- Utiliser les zones nommées pour des layouts complexes
- Aligner les items dans leurs cellules

---

## Rappel : Lignes de grille numérotées

Avant de placer des éléments, il faut comprendre comment Grid **numérote les lignes**.

### Numérotation des lignes

```
Colonnes →
    1       2       3       4
    ↓       ↓       ↓       ↓
1 → ┌───────┬───────┬───────┐
    │   A   │   B   │   C   │
2 → ├───────┼───────┼───────┤
    │   D   │   E   │   F   │
3 → ├───────┼───────┼───────┤
    │   G   │   H   │   I   │
4 → └───────┴───────┴───────┘
```

**Points importants** :
- Les lignes sont numérotées **à partir de 1** (pas de 0)
- Une grille 3×3 a **4 lignes verticales** et **4 lignes horizontales**
- Les lignes délimitent les cellules, elles ne sont pas les cellules elles-mêmes

### Numérotation inversée

On peut aussi compter depuis la fin avec des **nombres négatifs** :

```
    1       2       3      -1
    ↓       ↓       ↓       ↓
1 → ┌───────┬───────┬───────┐ ← -4
    │   A   │   B   │   C   │
2 → ├───────┼───────┼───────┤ ← -3
    │   D   │   E   │   F   │
3 → ├───────┼───────┼───────┤ ← -2
    │   G   │   H   │   I   │
4 → └───────┴───────┴───────┘ ← -1
```

**Utilité** : `-1` représente toujours la dernière ligne, pratique pour les layouts responsives !

---

## 1. Placement de base : `grid-column` et `grid-row`

### 1.1 `grid-column-start` et `grid-column-end`

Ces propriétés définissent **où commence et se termine** un item horizontalement.

```css
.item {
  grid-column-start: 1;  /* Commence à la ligne verticale 1 */
  grid-column-end: 3;    /* Se termine à la ligne verticale 3 */
}
```

**Résultat visuel** :

```
    1       2       3       4
    ↓       ↓       ↓       ↓
  ┌─────────────────┬───────┐
  │      Item       │       │  ← Item s'étend de la ligne 1 à 3
  │   (colonnes     │       │     (occupe 2 colonnes)
  │    1 et 2)      │       │
  └─────────────────┴───────┘
```

### 1.2 Syntaxe raccourcie : `grid-column`

Au lieu d'écrire start et end séparément, on utilise la syntaxe raccourcie :

```css
.item {
  grid-column: 1 / 3;  /* De la ligne 1 à la ligne 3 */
}
```

**Syntaxe** : `grid-column: start / end;`

### 1.3 `grid-row-start` et `grid-row-end`

Même principe, mais pour les lignes horizontales :

```css
.item {
  grid-row-start: 1;
  grid-row-end: 3;
}

/* Ou en raccourci : */
.item {
  grid-row: 1 / 3;
}
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Placement Grid</title>
  <style>
    .conteneur {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: repeat(3, 100px);
      gap: 10px;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .item {
      background-color: #4CAF50;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 20px;
      border-radius: 5px;
    }

    .item1 {
      grid-column: 1 / 3;  /* Colonnes 1-2 */
      grid-row: 1 / 2;     /* Ligne 1 */
      background-color: #2196F3;
    }

    .item2 {
      grid-column: 3 / 5;  /* Colonnes 3-4 */
      grid-row: 1 / 3;     /* Lignes 1-2 */
      background-color: #FF9800;
    }

    .item3 {
      grid-column: 1 / 2;  /* Colonne 1 */
      grid-row: 2 / 4;     /* Lignes 2-3 */
      background-color: #9C27B0;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item item1">Item 1<br>(2 cols)</div>
    <div class="item item2">Item 2<br>(2 cols × 2 rows)</div>
    <div class="item item3">Item 3<br>(2 rows)</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
    <div class="item">7</div>
  </div>
</body>
</html>
```

**Résultat visuel** :

```
┌─────────────┬─────────────┐
│   Item 1    │             │
│  (2 cols)   │   Item 2    │
├──┬──────────┤  (2x2)      │
│I │    4     │             │
│t ├──────────┼──────┬──────┤
│e │    5     │  6   │   7  │
│m │          │      │      │
│3 │          │      │      │
└──┴──────────┴──────┴──────┘
```

---

## 2. Le mot-clé `span` : Étendre sur plusieurs cellules

Au lieu de spécifier les lignes de début et de fin, on peut utiliser `span` pour dire "**étends-toi sur X cellules**".

### Syntaxe avec `span`

```css
.item {
  grid-column: span 2;  /* S'étend sur 2 colonnes */
}
```

### Comparaison

```css
/* Méthode 1 : Lignes explicites */
.item {
  grid-column: 1 / 3;  /* De la ligne 1 à 3 = 2 colonnes */
}

/* Méthode 2 : Span */
.item {
  grid-column: span 2;  /* S'étend sur 2 colonnes (à partir de sa position) */
}
```

**Différence** : Avec `span`, Grid place automatiquement l'item et l'étend sur le nombre de cellules demandé.

### Exemples avec `span`

#### Exemple 1 : Étendre sur plusieurs colonnes

```css
.item-large {
  grid-column: span 2;  /* 2 colonnes de large */
}
```

```html
<div class="conteneur">
  <div class="item item-large">Large (2 cols)</div>
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

**Résultat** :

```
┌──────────────┬──────┐
│    Large     │  1   │
│   (2 cols)   │      │
├──────┬───────┴──────┤
│  2   │      3       │
└──────┴──────────────┘
```

#### Exemple 2 : Étendre sur lignes et colonnes

```css
.item-hero {
  grid-column: span 3;  /* 3 colonnes */
  grid-row: span 2;     /* 2 lignes */
}
```

**Résultat** :

```
┌────────────────────────┬──┐
│                        │1 │
│      Item Hero         ├──┤
│     (3 cols × 2 rows)  │2 │
├──────┬──────┬──────────┴──┤
│  3   │  4   │     5       │
└──────┴──────┴─────────────┘
```

#### Exemple 3 : Combiner position et span

```css
.item {
  grid-column: 2 / span 2;  /* Commence à la colonne 2, s'étend sur 2 colonnes */
  grid-row: 1 / span 3;     /* Commence à la ligne 1, s'étend sur 3 lignes */
}
```

**Résultat** :

```
    1       2       3       4
    ↓       ↓       ↓       ↓
  ┌───────┬─────────────────┐
  │   A   │                 │
  ├───────┤      Item       │ ← Commence à col 2
  │   B   │   (2 cols ×     │   S'étend sur 2 cols
  ├───────┤    3 rows)      │   et 3 lignes
  │   C   │                 │
  └───────┴─────────────────┘
```

---

## 3. Jusqu'à la fin : Utiliser `-1`

Le nombre `-1` représente la **dernière ligne** de la grille.

### Exemple : Étendre jusqu'à la fin

```css
.header {
  grid-column: 1 / -1;  /* De la première à la dernière colonne */
}
```

**Résultat** :

```
┌──────────────────────────────┐
│          Header              │ ← S'étend sur toutes les colonnes
├──────┬──────┬──────┬─────────┤
│  A   │  B   │  C   │    D    │
└──────┴──────┴──────┴─────────┘
```

### Cas d'usage typiques

#### Header et Footer pleine largeur

```css
.header {
  grid-column: 1 / -1;  /* Toute la largeur */
}

.footer {
  grid-column: 1 / -1;  /* Toute la largeur */
}
```

```
┌──────────────────────────────┐
│          Header              │
├──────┬──────┬──────┬─────────┤
│  A   │  B   │  C   │    D    │
├──────┴──────┴──────┴─────────┤
│          Footer              │
└──────────────────────────────┘
```

#### Sidebar jusqu'en bas

```css
.sidebar {
  grid-column: 1 / 2;
  grid-row: 1 / -1;  /* De haut en bas */
}
```

```
┌────┬──────────────┐
│    │   Content    │
│ S  ├──────────────┤
│ i  │   Content    │
│ d  ├──────────────┤
│ e  │   Content    │
│    │              │
└────┴──────────────┘
```

---

## 4. `grid-area` : Placement en une seule propriété

`grid-area` est une **super-propriété raccourcie** qui combine row-start, column-start, row-end et column-end.

### Syntaxe

```css
.item {
  grid-area: row-start / column-start / row-end / column-end;
}
```

**Ordre** : 🔴 **Attention** ! L'ordre est différent des propriétés individuelles :
1. `grid-row-start`
2. `grid-column-start`
3. `grid-row-end`
4. `grid-column-end`

### Exemple

```css
/* Au lieu de : */
.item {
  grid-row: 1 / 3;
  grid-column: 2 / 4;
}

/* On peut écrire : */
.item {
  grid-area: 1 / 2 / 3 / 4;
  /*        ↑   ↑   ↑   ↑
         row col row col
        start start end end */
}
```

**Résultat** :

```
    1       2       3       4
    ↓       ↓       ↓       ↓
1 → ┌───────┬───────────────┐
    │   A   │               │
2 → ├───────┤     Item      │
    │   B   │ (rows 1-3,    │
3 → ├───────┤  cols 2-4)    │
    │   C   │               │
4 → └───────┴───────────────┘
```

### Avec `span`

```css
.item {
  grid-area: 1 / 2 / span 2 / span 2;
  /*        row col  rows   cols
           start start span  span */
}
```

---

## 5. Zones nommées : `grid-template-areas`

C'est l'une des fonctionnalités les **plus puissantes** de Grid : donner des **noms** aux zones et placer les items par leur nom.

### Principe

1. **Définir les zones** sur le conteneur avec `grid-template-areas`
2. **Assigner les items** aux zones avec `grid-area: nom-zone`

### Syntaxe de base

```css
.conteneur {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header  header  header"
    "sidebar main    aside"
    "footer  footer  footer";
}
```

**Chaque ligne entre guillemets** représente une ligne de la grille.
**Chaque mot** représente une cellule.

### Assigner les items aux zones

```css
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

### Exemple complet : Layout classique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Layout avec zones nommées</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
    }

    .page {
      display: grid;
      grid-template-columns: 200px 1fr 200px;
      grid-template-rows: auto 1fr auto;
      grid-template-areas:
        "header  header  header"
        "sidebar main    aside"
        "footer  footer  footer";
      min-height: 100vh;
      gap: 10px;
      padding: 10px;
    }

    .header {
      grid-area: header;
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      padding: 30px;
      text-align: center;
    }

    .sidebar {
      grid-area: sidebar;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .main {
      grid-area: main;
      background-color: white;
      padding: 30px;
    }

    .aside {
      grid-area: aside;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .footer {
      grid-area: footer;
      background-color: #333;
      color: white;
      padding: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="page">
    <header class="header">
      <h1>Mon Site Web</h1>
    </header>

    <aside class="sidebar">
      <h2>Navigation</h2>
      <ul>
        <li>Accueil</li>
        <li>À propos</li>
        <li>Contact</li>
      </ul>
    </aside>

    <main class="main">
      <h2>Contenu Principal</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </main>

    <aside class="aside">
      <h3>Publicités</h3>
      <p>Espace pub</p>
    </aside>

    <footer class="footer">
      <p>&copy; 2025 Mon Site</p>
    </footer>
  </div>
</body>
</html>
```

**Résultat visuel** :

```
┌────────────────────────────────┐
│          HEADER                │
├────────┬──────────────┬────────┤
│SIDEBAR │     MAIN     │ ASIDE  │
│        │   CONTENT    │        │
│        │              │        │
├────────┴──────────────┴────────┤
│          FOOTER                │
└────────────────────────────────┘
```

**Avantages** :
- ✅ **Lisible** : la structure est visible dans le CSS
- ✅ **Maintenable** : facile de changer le layout
- ✅ **Sémantique** : noms descriptifs

---

### Cellules vides avec `.`

Si vous voulez laisser une cellule **vide**, utilisez un point `.`

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas:
    "header header header header"
    "sidebar main main ."
    "footer footer footer footer";
}
```

**Résultat** :

```
┌──────────────────────────────┐
│          Header              │
├────┬──────────────┬──────────┤
│Side│     Main     │  (vide)  │
├────┴──────────────┴──────────┤
│          Footer              │
└──────────────────────────────┘
```

---

### Layout responsive avec zones nommées

On peut **réorganiser complètement** le layout en changeant seulement `grid-template-areas` !

```css
/* Desktop */
.page {
  grid-template-columns: 200px 1fr 200px;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
}

/* Tablette */
@media (max-width: 768px) {
  .page {
    grid-template-columns: 200px 1fr;
    grid-template-areas:
      "header header"
      "sidebar main"
      "footer footer";
  }

  .aside {
    display: none; /* Cache l'aside sur tablette */
  }
}

/* Mobile */
@media (max-width: 480px) {
  .page {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "main"
      "sidebar"
      "footer";
  }
}
```

**Résultat selon la taille d'écran** :

```
DESKTOP
┌────────────────────────┐
│       Header           │
├────┬──────────┬────────┤
│Side│   Main   │ Aside  │
├────┴──────────┴────────┤
│       Footer           │
└────────────────────────┘

MOBILE
┌──────────────┐
│   Header     │
├──────────────┤
│     Main     │
├──────────────┤
│   Sidebar    │
├──────────────┤
│   Footer     │
└──────────────┘
```

**Puissant** : Le HTML ne change pas, seul le CSS change !

---

## 6. Alignement des items dans leurs cellules

Par défaut, les items remplissent toute leur cellule. Mais on peut contrôler leur alignement.

### 6.1 `justify-self` : Alignement horizontal

Aligne l'item **horizontalement** dans sa cellule.

**Valeurs** :
- `start` : à gauche
- `end` : à droite
- `center` : centré
- `stretch` : étire (défaut)

```css
.item {
  justify-self: center;
}
```

**Exemple visuel** :

```
justify-self: start
┌────────────────────┐
│[Item]              │
└────────────────────┘

justify-self: center
┌────────────────────┐
│      [Item]        │
└────────────────────┘

justify-self: end
┌────────────────────┐
│              [Item]│
└────────────────────┘

justify-self: stretch
┌────────────────────┐
│[      Item       ] │
└────────────────────┘
```

### 6.2 `align-self` : Alignement vertical

Aligne l'item **verticalement** dans sa cellule.

**Valeurs** :
- `start` : en haut
- `end` : en bas
- `center` : centré
- `stretch` : étire (défaut)

```css
.item {
  align-self: center;
}
```

**Exemple visuel** :

```
align-self: start
┌─────┐
│Item │
│     │
│     │
└─────┘

align-self: center
┌─────┐
│     │
│Item │
│     │
└─────┘

align-self: end
┌─────┐
│     │
│     │
│Item │
└─────┘

align-self: stretch
┌─────┐
│Item │
│Item │
│Item │
└─────┘
```

### 6.3 `place-self` : Raccourci

Combine `align-self` et `justify-self` :

```css
.item {
  place-self: center center;
  /*          ↑       ↑
           align  justify */
}

/* Ou si les deux valeurs sont identiques : */
.item {
  place-self: center; /* center center */
}
```

### Exemple complet d'alignement

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Alignement Grid</title>
  <style>
    .conteneur {
      display: grid;
      grid-template-columns: repeat(3, 200px);
      grid-template-rows: repeat(2, 150px);
      gap: 10px;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .item {
      background-color: #2196F3;
      color: white;
      padding: 20px;
      border-radius: 5px;
    }

    .item1 {
      justify-self: start;
      align-self: start;
    }

    .item2 {
      justify-self: center;
      align-self: center;
    }

    .item3 {
      justify-self: end;
      align-self: end;
    }

    .item4 {
      place-self: center;
    }

    .item5 {
      /* stretch par défaut */
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item item1">Start Start</div>
    <div class="item item2">Center</div>
    <div class="item item3">End End</div>
    <div class="item item4">Center<br>(place-self)</div>
    <div class="item item5">Stretch<br>(défaut)</div>
  </div>
</body>
</html>
```

---

## 7. Alignement global : Sur le conteneur

On peut aussi définir l'alignement **par défaut** pour tous les items sur le conteneur.

### `justify-items` : Alignement horizontal de tous les items

```css
.conteneur {
  display: grid;
  justify-items: center; /* Tous les items centrés horizontalement */
}
```

### `align-items` : Alignement vertical de tous les items

```css
.conteneur {
  display: grid;
  align-items: center; /* Tous les items centrés verticalement */
}
```

### `place-items` : Raccourci

```css
.conteneur {
  display: grid;
  place-items: center; /* Tous les items centrés */
}
```

---

## 8. Exemples pratiques avancés

### Exemple 1 : Galerie avec image hero

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Galerie Hero</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      padding: 20px;
      background-color: #1a1a1a;
    }

    .galerie {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-auto-rows: 200px;
      gap: 15px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .photo {
      background: linear-gradient(135deg, #667eea, #764ba2);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 24px;
      font-weight: bold;
      overflow: hidden;
      position: relative;
    }

    .photo img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .hero {
      grid-column: span 2;
      grid-row: span 2;
      font-size: 36px;
    }
  </style>
</head>
<body>
  <div class="galerie">
    <div class="photo hero">HERO</div>
    <div class="photo">1</div>
    <div class="photo">2</div>
    <div class="photo">3</div>
    <div class="photo">4</div>
    <div class="photo">5</div>
    <div class="photo">6</div>
    <div class="photo">7</div>
    <div class="photo">8</div>
    <div class="photo">9</div>
  </div>
</body>
</html>
```

**Résultat** :

```
┌─────────────┬────┬────┐
│             │ 1  │ 2  │
│    HERO     ├────┼────┤
│   (2×2)     │ 3  │ 4  │
├──────┬──────┼────┼────┤
│  5   │  6   │ 7  │ 8  │
├──────┴──────┴────┴────┤
│  9   │ 10   │ 11 │ 12 │
└──────┴──────┴────┴────┘
```

---

### Exemple 2 : Magazine Layout

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Magazine Layout</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Georgia', serif;
      background-color: #f5f5f5;
      padding: 20px;
    }

    .magazine {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      grid-auto-rows: 150px;
      gap: 20px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .article {
      background: white;
      padding: 30px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      border-radius: 10px;
      overflow: hidden;
    }

    .article h2 {
      margin-bottom: 15px;
      color: #333;
    }

    .article p {
      color: #666;
      line-height: 1.6;
    }

    .featured {
      grid-column: span 4;
      grid-row: span 2;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
    }

    .featured h2 {
      color: white;
      font-size: 32px;
    }

    .secondary {
      grid-column: span 2;
    }

    .tertiary {
      grid-column: span 2;
    }
  </style>
</head>
<body>
  <div class="magazine">
    <article class="article featured">
      <h2>Article Principal</h2>
      <p>Cet article occupe 4 colonnes sur 2 lignes. C'est le contenu le plus important de la page.</p>
    </article>

    <article class="article secondary">
      <h2>Article 2</h2>
      <p>Article secondaire sur 2 colonnes.</p>
    </article>

    <article class="article secondary">
      <h2>Article 3</h2>
      <p>Article secondaire sur 2 colonnes.</p>
    </article>

    <article class="article tertiary">
      <h2>Article 4</h2>
      <p>Plus petit article.</p>
    </article>

    <article class="article tertiary">
      <h2>Article 5</h2>
      <p>Plus petit article.</p>
    </article>

    <article class="article tertiary">
      <h2>Article 6</h2>
      <p>Plus petit article.</p>
    </article>
  </div>
</body>
</html>
```

---

### Exemple 3 : Dashboard complexe

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Dashboard</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f0f2f5;
    }

    .dashboard {
      display: grid;
      grid-template-columns: repeat(12, 1fr);
      grid-auto-rows: minmax(100px, auto);
      gap: 20px;
      padding: 20px;
      max-width: 1600px;
      margin: 0 auto;
    }

    .widget {
      background: white;
      border-radius: 12px;
      padding: 25px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }

    .widget h3 {
      margin-bottom: 15px;
      color: #333;
      font-size: 18px;
    }

    .header {
      grid-column: 1 / -1;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
    }

    .big-stat {
      grid-column: span 3;
    }

    .chart-main {
      grid-column: span 8;
      grid-row: span 2;
    }

    .chart-side {
      grid-column: span 4;
      grid-row: span 2;
    }

    .small-stat {
      grid-column: span 3;
    }
  </style>
</head>
<body>
  <div class="dashboard">
    <div class="widget header">
      <h2>Dashboard Analytics</h2>
    </div>

    <div class="widget big-stat">
      <h3>Visiteurs</h3>
      <div style="font-size: 36px; color: #4CAF50;">12,345</div>
    </div>

    <div class="widget big-stat">
      <h3>Revenus</h3>
      <div style="font-size: 36px; color: #2196F3;">€45,678</div>
    </div>

    <div class="widget big-stat">
      <h3>Commandes</h3>
      <div style="font-size: 36px; color: #FF9800;">856</div>
    </div>

    <div class="widget big-stat">
      <h3>Clients</h3>
      <div style="font-size: 36px; color: #9C27B0;">2,341</div>
    </div>

    <div class="widget chart-main">
      <h3>Graphique Principal</h3>
      <p>Grande zone pour un graphique de tendances...</p>
    </div>

    <div class="widget chart-side">
      <h3>Répartition</h3>
      <p>Graphique circulaire ou statistiques...</p>
    </div>

    <div class="widget small-stat">
      <h3>Taux conversion</h3>
      <div>3.2%</div>
    </div>

    <div class="widget small-stat">
      <h3>Pages/visite</h3>
      <div>4.5</div>
    </div>

    <div class="widget small-stat">
      <h3>Durée moyenne</h3>
      <div>2m 34s</div>
    </div>

    <div class="widget small-stat">
      <h3>Taux de rebond</h3>
      <div>42%</div>
    </div>
  </div>
</body>
</html>
```

---

## Récapitulatif des propriétés

### Placement sur les items

```css
/* Méthode 1 : Lignes explicites */
grid-column: 1 / 3;
grid-row: 2 / 4;

/* Méthode 2 : Span */
grid-column: span 2;
grid-row: span 2;

/* Méthode 3 : grid-area (tout en un) */
grid-area: 1 / 2 / 3 / 4;
/*        row col row col
         start start end end */

/* Méthode 4 : Zones nommées */
grid-area: header;
```

### Zones nommées sur le conteneur

```css
.conteneur {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
}
```

### Alignement des items

```css
/* Sur un item individuel */
justify-self: center;  /* Horizontal */
align-self: center;    /* Vertical */
place-self: center;    /* Les deux */

/* Sur tous les items (conteneur) */
justify-items: center;
align-items: center;
place-items: center;
```

---

## Points clés à retenir

✅ **Lignes numérotées** : Commencent à 1, `-1` = dernière ligne

✅ **`grid-column` et `grid-row`** : Placement précis avec start/end

✅ **`span`** : Étendre sur X cellules (plus intuitif que start/end)

✅ **`1 / -1`** : S'étend sur toute la grille (header, footer)

✅ **`grid-template-areas`** : Layouts visuels et sémantiques

✅ **Zones nommées** : Parfait pour layouts complexes et responsive

✅ **`justify-self` / `align-self`** : Aligner items dans leurs cellules

✅ **Combinaisons** : Placement automatique + placement manuel = puissant

---

## Conseils d'utilisation

### Quand utiliser le placement automatique ?

- ✅ **Galeries régulières** : Laissez Grid placer automatiquement
- ✅ **Listes de cartes** : Pas besoin de contrôle précis

### Quand utiliser le placement manuel ?

- ✅ **Layouts asymétriques** : Magazine, portfolio
- ✅ **Items de tailles variables** : Hero, widgets spéciaux
- ✅ **Structures complexes** : Dashboards, applications

### Quand utiliser les zones nommées ?

- ✅ **Layouts de page** : Header, sidebar, main, footer
- ✅ **Responsive design** : Réorganiser facilement
- ✅ **Collaboration** : Code lisible et compréhensible

---

## Conclusion

Le placement d'éléments dans Grid offre une **flexibilité inégalée** :

- **Placement automatique** pour les cas simples
- **Placement manuel** pour le contrôle précis
- **Zones nommées** pour la lisibilité et la maintenance
- **Span** pour étendre facilement sur plusieurs cellules
- **Alignement** pour positionner dans les cellules

Combiné avec ce que nous avons vu précédemment (`grid-template-columns/rows`, `gap`, `fr`, `minmax`), vous avez maintenant **tous les outils** pour créer n'importe quel layout moderne !

CSS Grid est devenu le standard pour les layouts complexes en CSS. Une fois maîtrisé, vous ne reviendrez plus aux anciennes techniques ! 🎉

---


Vous avez terminé la section sur la mise en page moderne ! Félicitations ! 🎊

⏭️ [Positionnement et contexte](/04-css3-styles-et-mise-en-page/04-positionnement-et-contexte/README.md)
