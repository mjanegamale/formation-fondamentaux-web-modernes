🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3.6 - Grid : grid-template-columns/rows, grid-gap

## Introduction

Dans cette leçon, nous allons approfondir les propriétés fondamentales de CSS Grid que nous avons introduites précédemment. Ces propriétés constituent le **cœur** de Grid et déterminent la structure de votre grille.

### Les trois propriétés essentielles

1. **`grid-template-columns`** : définit les colonnes de la grille
2. **`grid-template-rows`** : définit les lignes de la grille
3. **`gap`** (anciennement `grid-gap`) : définit l'espacement entre les cellules

> **💡 Rappel** : Ces propriétés s'appliquent toujours sur le **conteneur Grid**, jamais sur les items individuels.

---

## 1. `grid-template-columns` en profondeur

La propriété `grid-template-columns` définit le nombre de colonnes et leur largeur.

### Syntaxe de base

```css
.conteneur {
  display: grid;
  grid-template-columns: [taille-col1] [taille-col2] [taille-col3] ...;
}
```

Chaque valeur représente la largeur d'une colonne.

---

### 1.1 Unités disponibles

#### Pixels (px) - Taille fixe

```css
.conteneur {
  display: grid;
  grid-template-columns: 200px 300px 200px;
}
```

```
┌──────┬─────────┬──────┐
│ 200px│  300px  │ 200px│
│ Col 1│  Col 2  │ Col 3│
└──────┴─────────┴──────┘
```

**Avantages** : Contrôle précis de la largeur
**Inconvénients** : Pas responsive

#### Pourcentages (%) - Relatif au conteneur

```css
.conteneur {
  display: grid;
  grid-template-columns: 25% 50% 25%;
}
```

```
┌───────┬──────────────┬───────┐
│  25%  │     50%      │  25%  │
└───────┴──────────────┴───────┘
```

**Avantages** : Responsive
**Inconvénients** : Difficile de gérer les espacements

#### Fractions (fr) - L'unité Grid par excellence

```css
.conteneur {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
```

```
┌───────┬──────────────┬───────┐
│  25%  │     50%      │  25%  │
│  1fr  │     2fr      │  1fr  │
└───────┴──────────────┴───────┘
```

**Calcul** :
- Total : 1 + 2 + 1 = 4 fractions
- Col 1 : 1/4 = 25%
- Col 2 : 2/4 = 50%
- Col 3 : 1/4 = 25%

**Avantages** : Flexible, simple, responsive
**Recommandation** : ✅ **Utilisez `fr` par défaut avec Grid**

#### Auto - S'adapte au contenu

```css
.conteneur {
  display: grid;
  grid-template-columns: auto auto auto;
}
```

**Comportement** : Chaque colonne prend la largeur de son contenu le plus large.

```
┌──────┬──────────────────┬────┐
│Court │  Contenu long    │OK  │
│      │  qui s'étend     │    │
└──────┴──────────────────┴────┘
```

**Avantages** : S'adapte au contenu
**Inconvénients** : Difficile à prédire

---

### 1.2 Combinaisons d'unités

On peut mélanger différentes unités pour créer des layouts complexes.

#### Exemple 1 : Sidebar fixe + Contenu flexible

```css
.conteneur {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 20px;
}
```

```
┌──────┬────────────────────────┐
│250px │  Prend tout l'espace   │
│(fixe)│     disponible (1fr)   │
│      │                        │
└──────┴────────────────────────┘
```

**Cas d'usage** : Layout avec sidebar

#### Exemple 2 : 3 colonnes avec sidebar et aside

```css
.conteneur {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  gap: 20px;
}
```

```
┌──────┬──────────────┬──────┐
│200px │     1fr      │200px │
│Side  │    Main      │Aside │
│bar   │   Content    │      │
└──────┴──────────────┴──────┘
```

**Cas d'usage** : Layout de blog avec sidebar et publicités

#### Exemple 3 : Header + colonnes variables

```css
.conteneur {
  display: grid;
  grid-template-columns: 100px 2fr 1fr;
  gap: 15px;
}
```

```
┌──────┬──────────────┬───────┐
│100px │     2fr      │  1fr  │
│ Logo │   (66.66%)   │(33.33)│
└──────┴──────────────┴───────┘
```

---

### 1.3 La fonction `repeat()` approfondie

`repeat()` permet de répéter un pattern de colonnes.

#### Syntaxe

```css
grid-template-columns: repeat(nombre, pattern);
```

#### Exemple simple

```css
/* Au lieu de : */
grid-template-columns: 1fr 1fr 1fr 1fr 1fr;

/* Écrire : */
grid-template-columns: repeat(5, 1fr);
```

#### Répéter un pattern complexe

```css
/* Répète le pattern "100px 1fr" 3 fois */
grid-template-columns: repeat(3, 100px 1fr);

/* Équivalent à : */
grid-template-columns: 100px 1fr 100px 1fr 100px 1fr;
```

**Résultat visuel :**

```
┌────┬────┬────┬────┬────┬────┐
│100 │1fr │100 │1fr │100 │1fr │
│ px │    │ px │    │ px │    │
└────┴────┴────┴────┴────┴────┘
```

#### Combiner `repeat()` avec d'autres valeurs

```css
grid-template-columns: 200px repeat(3, 1fr) 200px;

/* Équivalent à : */
grid-template-columns: 200px 1fr 1fr 1fr 200px;
```

```
┌──────┬────┬────┬────┬──────┐
│200px │1fr │1fr │1fr │200px │
└──────┴────┴────┴────┴──────┘
```

---

### 1.4 La fonction `minmax()` - Pour le responsive

`minmax()` définit une taille **minimum** et **maximum** pour une colonne.

#### Syntaxe

```css
grid-template-columns: minmax(min, max);
```

#### Exemple 1 : Colonne flexible avec minimum

```css
.conteneur {
  display: grid;
  grid-template-columns: minmax(200px, 1fr) minmax(200px, 1fr);
  gap: 20px;
}
```

**Comportement** :
- Chaque colonne fait **au minimum 200px**
- Chaque colonne grandit jusqu'à **1fr** (égales)
- Si le conteneur fait 1000px : chaque colonne = 490px (1fr = 490px)
- Si le conteneur fait 500px : chaque colonne = 240px (mais minimum 200px appliqué)

#### Exemple 2 : Contenu flexible avec maximum

```css
.conteneur {
  display: grid;
  grid-template-columns: 200px minmax(300px, 2fr) minmax(200px, 1fr);
}
```

```
┌──────┬────────────────┬──────────┐
│200px │ min:300px      │min:200px │
│(fixe)│ max:2fr        │max:1fr   │
└──────┴────────────────┴──────────┘
```

#### Exemple 3 : Largeur maximum avec `auto`

```css
grid-template-columns: repeat(3, minmax(100px, auto));
```

**Comportement** :
- Minimum : 100px
- Maximum : `auto` (s'adapte au contenu)

---

### 1.5 Grilles responsive avec `auto-fit` et `auto-fill`

Ces mots-clés permettent de créer des grilles **automatiquement responsive**.

#### `auto-fill` : Remplit avec autant de colonnes que possible

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(auto-fill, 200px);
  gap: 20px;
}
```

**Comportement** :
- Crée autant de colonnes de 200px que possible
- Les colonnes vides restent présentes

**Si le conteneur fait 850px :**

```
┌──────┬──────┬──────┬──────┐ [vide]
│ 200  │ 200  │ 200  │ 200  │   50px restants
└──────┴──────┴──────┴──────┘
```

#### `auto-fit` : S'adapte aux items existants

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(auto-fit, 200px);
  gap: 20px;
}
```

**Comportement** :
- Similaire à `auto-fill`
- Mais les colonnes vides **disparaissent** (collapsed)

**Si le conteneur fait 850px avec seulement 3 items :**

```
┌──────┬──────┬──────┐
│ 200  │ 200  │ 200  │ Les colonnes vides
└──────┴──────┴──────┘ ont disparu
```

#### La technique ultime : `auto-fit` + `minmax()`

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

**C'est la recette magique pour des grilles responsive !**

**Comportement** :
- Crée autant de colonnes que possible
- Chaque colonne fait au minimum 250px
- Les colonnes grandissent pour remplir l'espace (1fr)
- S'adapte automatiquement à toutes les tailles d'écran

**Exemple visuel selon la largeur d'écran :**

```
GRAND ÉCRAN (1200px)
┌────────┬────────┬────────┬────────┐
│  Item  │  Item  │  Item  │  Item  │
└────────┴────────┴────────┴────────┘

ÉCRAN MOYEN (800px)
┌─────────────┬─────────────┐
│    Item     │    Item     │
├─────────────┼─────────────┤
│    Item     │    Item     │
└─────────────┴─────────────┘

PETIT ÉCRAN (400px)
┌──────────────────────┐
│        Item          │
├──────────────────────┤
│        Item          │
├──────────────────────┤
│        Item          │
└──────────────────────┘
```

### Exemple complet responsive

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Grille Responsive</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      padding: 20px;
      background-color: #f5f5f5;
    }

    .galerie {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
    }

    .carte {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      min-height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      color: #333;
    }
  </style>
</head>
<body>
  <div class="galerie">
    <div class="carte">1</div>
    <div class="carte">2</div>
    <div class="carte">3</div>
    <div class="carte">4</div>
    <div class="carte">5</div>
    <div class="carte">6</div>
  </div>
</body>
</html>
```

**Redimensionnez la fenêtre** : la grille s'adapte automatiquement ! 🎉

---

## 2. `grid-template-rows` en profondeur

La propriété `grid-template-rows` fonctionne comme `grid-template-columns`, mais pour les **lignes**.

### Syntaxe de base

```css
.conteneur {
  display: grid;
  grid-template-rows: [hauteur-ligne1] [hauteur-ligne2] ...;
}
```

---

### 2.1 Définir la hauteur des lignes

#### Hauteurs fixes

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 200px 150px;
  gap: 10px;
}
```

```
┌────┬────┬────┐
│    │    │    │ ← 100px
├────┼────┼────┤
│    │    │    │
│    │    │    │ ← 200px
├────┼────┼────┤
│    │    │    │ ← 150px
└────┴────┴────┘
```

#### Avec `fr`

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr 2fr 1fr;
  height: 400px; /* Hauteur totale nécessaire */
  gap: 10px;
}
```

**Calcul** (avec conteneur de 400px) :
- Total : 1 + 2 + 1 = 4 fractions
- Ligne 1 : 1/4 × 400px = 100px
- Ligne 2 : 2/4 × 400px = 200px
- Ligne 3 : 1/4 × 400px = 100px

#### Avec `minmax()`

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: minmax(100px, auto) minmax(200px, auto);
  gap: 10px;
}
```

**Comportement** :
- Ligne 1 : minimum 100px, s'adapte au contenu
- Ligne 2 : minimum 200px, s'adapte au contenu

---

### 2.2 Hauteur automatique (comportement par défaut)

**Si vous ne définissez pas `grid-template-rows`, la hauteur est automatique.**

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  /* Pas de grid-template-rows */
}
```

**Comportement** : Chaque ligne prend la hauteur de son contenu le plus haut.

```
┌────┬────┬────┐
│A   │BBBB│C   │ ← Hauteur = contenu le plus haut (BBBB)
├────┼────┼────┤
│D   │E   │FFF │ ← Hauteur = contenu le plus haut (FFF)
│    │    │FFF │
└────┴────┴────┘
```

**C'est généralement ce qu'on veut !** ✅

---

### 2.3 Grille implicite vs explicite

#### Grille explicite

Les lignes/colonnes définies avec `grid-template-columns/rows`.

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 100px; /* 2 lignes explicites */
}
```

**Si vous avez 9 items, mais seulement 2 lignes définies :**

```
┌────┬────┬────┐
│ 1  │ 2  │ 3  │ ← Ligne 1 (100px - explicite)
├────┼────┼────┤
│ 4  │ 5  │ 6  │ ← Ligne 2 (100px - explicite)
├────┼────┼────┤
│ 7  │ 8  │ 9  │ ← Ligne 3 (auto - IMPLICITE)
└────┴────┴────┘
```

#### Contrôler les lignes implicites

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 100px;
  grid-auto-rows: 80px; /* Hauteur des lignes implicites */
}
```

```
┌────┬────┬────┐
│ 1  │ 2  │ 3  │ ← 100px (explicite)
├────┼────┼────┤
│ 4  │ 5  │ 6  │ ← 100px (explicite)
├────┼────┼────┤
│ 7  │ 8  │ 9  │ ← 80px (implicite, contrôlée)
└────┴────┴────┘
```

---

### 2.4 Exemple : Dashboard avec lignes définies

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Dashboard Grid</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
    }

    .dashboard {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: 80px 1fr 1fr;
      height: 100vh;
      gap: 10px;
      padding: 10px;
      background-color: #f0f0f0;
    }

    .widget {
      background: white;
      border-radius: 8px;
      padding: 20px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .header {
      grid-column: 1 / -1; /* S'étend sur toutes les colonnes */
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      font-size: 24px;
    }
  </style>
</head>
<body>
  <div class="dashboard">
    <div class="widget header">Dashboard Header</div>
    <div class="widget">Widget 1</div>
    <div class="widget">Widget 2</div>
    <div class="widget">Widget 3</div>
    <div class="widget">Widget 4</div>
    <div class="widget">Widget 5</div>
    <div class="widget">Widget 6</div>
    <div class="widget">Widget 7</div>
    <div class="widget">Widget 8</div>
  </div>
</body>
</html>
```

**Structure** :
- Ligne 1 : 80px (header)
- Lignes 2-3 : 1fr chacune (widgets)

---

## 3. `gap` (anciennement `grid-gap`) en profondeur

La propriété `gap` définit l'**espacement entre les cellules** de la grille.

> **📌 Note** : `grid-gap` est l'ancien nom. Utilisez `gap` (fonctionne aussi avec Flexbox).

---

### 3.1 Syntaxes de `gap`

#### Une seule valeur

```css
.conteneur {
  display: grid;
  gap: 20px; /* 20px entre lignes ET colonnes */
}
```

#### Deux valeurs

```css
.conteneur {
  display: grid;
  gap: 20px 30px;
  /*   ↑    ↑
    lignes colonnes */
}
```

#### Propriétés séparées

```css
.conteneur {
  display: grid;
  row-gap: 20px;    /* Espacement vertical */
  column-gap: 30px; /* Espacement horizontal */
}
```

---

### 3.2 Visualisation de `gap`

#### Sans `gap`

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  /* Pas de gap */
}
```

```
┌────┬────┬────┐
│ 1  │ 2  │ 3  │ ← Les cellules se touchent
└────┴────┴────┘
```

#### Avec `gap: 20px`

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

```
┌────┐  ┌────┐  ┌────┐
│ 1  │  │ 2  │  │ 3  │
└────┘  └────┘  └────┘
   ↑ 20px ↑ 20px ↑
```

#### Avec `gap: 10px 30px` (lignes différentes de colonnes)

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px 30px;
}
```

```
┌────┐     ┌────┐     ┌────┐
│ 1  │     │ 2  │     │ 3  │
└────┘     └────┘     └────┘
   ↑ 30px    ↑ 30px    ↑

↓ 10px

┌────┐     ┌────┐     ┌────┐
│ 4  │     │ 5  │     │ 6  │
└────┘     └────┘     └────┘
```

---

### 3.3 `gap` vs `margin`

#### ❌ Avec `margin` (problématique)

```css
.item {
  margin: 10px;
}
```

**Problème** : Margin ajoute de l'espace **aussi sur les bords extérieurs** du conteneur.

```
        10px de marge en trop ↓
    ┌─────────────────────────┐
10px│  ┌────┐  ┌────┐  ┌────┐ │10px
 ←  │  │ 1  │  │ 2  │  │ 3  │ │ →
    │  └────┘  └────┘  └────┘ │
    └─────────────────────────┘
               ↑ 10px de marge en trop
```

#### ✅ Avec `gap` (propre)

```css
.conteneur {
  gap: 20px;
}
```

**Résultat** : Espacement **uniquement entre les cellules**, pas sur les bords.

```
┌─────────────────────────┐
│┌────┐  ┌────┐  ┌────┐   │ ← Pas d'espace ici
││ 1  │  │ 2  │  │ 3  │   │
│└────┘  └────┘  └────┘   │ ← Ni ici
└─────────────────────────┘
```

**Conclusion** : Toujours utiliser `gap` avec Grid ! ✅

---

### 3.4 `gap` avec différentes unités

```css
/* Pixels */
gap: 20px;

/* Em (relatif à la taille de police) */
gap: 1.5em;

/* Rem (relatif à la taille de police root) */
gap: 2rem;

/* Pourcentages (relatif au conteneur) */
gap: 5%;

/* Calc */
gap: calc(2rem + 10px);
```

---

### 3.5 Exemples pratiques de `gap`

#### Galerie d'images serrée

```css
.galerie {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 5px; /* Petit espacement */
}
```

#### Layout aéré

```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 40px; /* Grand espacement */
}
```

#### Cards avec espacement différent

```css
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  row-gap: 30px;    /* Plus d'espace vertical */
  column-gap: 20px; /* Moins d'espace horizontal */
}
```

---

## 4. Exemples pratiques complets

### Exemple 1 : Layout de blog moderne

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Blog Layout</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f5f5f5;
    }

    .page {
      display: grid;
      grid-template-columns: 250px 1fr 200px;
      grid-template-rows: auto 1fr auto;
      min-height: 100vh;
      gap: 20px;
      padding: 20px;
      max-width: 1400px;
      margin: 0 auto;
    }

    header {
      grid-column: 1 / -1; /* Span toutes les colonnes */
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      padding: 30px;
      border-radius: 10px;
    }

    .sidebar {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    main {
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .ads {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    footer {
      grid-column: 1 / -1;
      background: #333;
      color: white;
      padding: 20px;
      text-align: center;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <div class="page">
    <header>
      <h1>Mon Blog</h1>
      <p>Un blog moderne avec CSS Grid</p>
    </header>

    <aside class="sidebar">
      <h2>Catégories</h2>
      <ul>
        <li>Technologie</li>
        <li>Design</li>
        <li>Développement</li>
      </ul>
    </aside>

    <main>
      <h2>Article Principal</h2>
      <p>Contenu de l'article qui prend tout l'espace disponible grâce à 1fr.</p>
    </main>

    <aside class="ads">
      <h3>Publicités</h3>
      <div>Espace pub</div>
    </aside>

    <footer>
      <p>&copy; 2025 Mon Blog</p>
    </footer>
  </div>
</body>
</html>
```

**Propriétés Grid utilisées** :
- `grid-template-columns: 250px 1fr 200px` : 3 colonnes
- `grid-template-rows: auto 1fr auto` : header et footer auto, contenu flexible
- `gap: 20px` : espacement uniforme

---

### Exemple 2 : Galerie responsive avec différentes tailles

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Galerie Responsive</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      padding: 20px;
      background-color: #1a1a1a;
      font-family: Arial, sans-serif;
    }

    h1 {
      color: white;
      text-align: center;
      margin-bottom: 30px;
    }

    .galerie {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
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
      transition: transform 0.3s, box-shadow 0.3s;
      cursor: pointer;
    }

    .photo:hover {
      transform: scale(1.05);
      box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    }

    /* Éléments spéciaux qui s'étendent */
    .photo-large {
      grid-column: span 2;
      grid-row: span 2;
    }

    .photo-wide {
      grid-column: span 2;
    }

    .photo-tall {
      grid-row: span 2;
    }
  </style>
</head>
<body>
  <h1>Galerie Dynamique</h1>

  <div class="galerie">
    <div class="photo photo-large">Large</div>
    <div class="photo">1</div>
    <div class="photo">2</div>
    <div class="photo photo-tall">Tall</div>
    <div class="photo">3</div>
    <div class="photo">4</div>
    <div class="photo photo-wide">Wide</div>
    <div class="photo">5</div>
    <div class="photo">6</div>
    <div class="photo">7</div>
    <div class="photo photo-large">Large 2</div>
    <div class="photo">8</div>
  </div>
</body>
</html>
```

**Propriétés Grid utilisées** :
- `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))` : responsive
- `grid-auto-rows: 200px` : hauteur uniforme
- `gap: 15px` : espacement propre

---

### Exemple 3 : Dashboard avec minmax()

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Dashboard Responsive</title>
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
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      grid-auto-rows: minmax(150px, auto);
      gap: 20px;
      padding: 20px;
      max-width: 1400px;
      margin: 0 auto;
    }

    .stat {
      background: white;
      border-radius: 12px;
      padding: 30px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    .stat h3 {
      color: #666;
      font-size: 14px;
      text-transform: uppercase;
      margin-bottom: 10px;
    }

    .stat .value {
      font-size: 36px;
      font-weight: bold;
      color: #333;
      margin-bottom: 10px;
    }

    .stat .change {
      font-size: 14px;
      color: #4CAF50;
    }

    .stat.negative .change {
      color: #f44336;
    }
  </style>
</head>
<body>
  <div class="dashboard">
    <div class="stat">
      <h3>Visiteurs</h3>
      <div class="value">12,345</div>
      <div class="change">↑ +12.5% ce mois</div>
    </div>

    <div class="stat">
      <h3>Revenus</h3>
      <div class="value">€45,678</div>
      <div class="change">↑ +8.2% ce mois</div>
    </div>

    <div class="stat negative">
      <h3>Taux de rebond</h3>
      <div class="value">42%</div>
      <div class="change">↓ -3.1% ce mois</div>
    </div>

    <div class="stat">
      <h3>Nouveaux clients</h3>
      <div class="value">856</div>
      <div class="change">↑ +15.3% ce mois</div>
    </div>

    <div class="stat">
      <h3>Commandes</h3>
      <div class="value">1,234</div>
      <div class="change">↑ +6.7% ce mois</div>
    </div>

    <div class="stat">
      <h3>Produits vendus</h3>
      <div class="value">3,456</div>
      <div class="change">↑ +9.4% ce mois</div>
    </div>
  </div>
</body>
</html>
```

**Propriétés Grid utilisées** :
- `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))` : s'adapte
- `grid-auto-rows: minmax(150px, auto)` : hauteur flexible
- `gap: 20px` : espacement cohérent

---

## Récapitulatif des propriétés

### `grid-template-columns`

```css
/* Valeurs fixes */
grid-template-columns: 200px 300px 200px;

/* Fractions */
grid-template-columns: 1fr 2fr 1fr;

/* Répétition */
grid-template-columns: repeat(4, 1fr);

/* Mixte */
grid-template-columns: 200px 1fr 1fr;

/* Responsive avec minmax */
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```

### `grid-template-rows`

```css
/* Valeurs fixes */
grid-template-rows: 100px 200px 100px;

/* Fractions */
grid-template-rows: 1fr 2fr 1fr;

/* Auto (par défaut) */
/* Pas besoin de définir, s'adapte au contenu */

/* Contrôler les lignes implicites */
grid-auto-rows: 100px;
grid-auto-rows: minmax(100px, auto);
```

### `gap`

```css
/* Même espacement partout */
gap: 20px;

/* Différent pour lignes et colonnes */
gap: 20px 30px;
/*   ↑     ↑
  lignes colonnes */

/* Séparé */
row-gap: 20px;
column-gap: 30px;
```

---

## Points clés à retenir

✅ **`grid-template-columns`** définit la structure horizontale

✅ **`fr`** est l'unité idéale pour Grid (flexible et simple)

✅ **`repeat()`** évite les répétitions

✅ **`minmax()`** permet des colonnes/lignes flexibles avec limites

✅ **`auto-fit`** + **`minmax()`** = grille responsive magique

✅ **`grid-template-rows`** est souvent laissé en `auto` (s'adapte au contenu)

✅ **`gap`** crée des espacements propres (contrairement à margin)

✅ **`grid-auto-rows`** contrôle les lignes créées automatiquement

---

## Erreurs courantes à éviter

❌ **Utiliser des pourcentages au lieu de `fr`**
```css
/* ❌ Moins flexible */
grid-template-columns: 33.33% 33.33% 33.33%;

/* ✅ Plus simple avec fr */
grid-template-columns: repeat(3, 1fr);
```

❌ **Utiliser `margin` au lieu de `gap`**
```css
/* ❌ Crée de l'espace sur les bords */
.item { margin: 10px; }

/* ✅ Espacement uniquement entre les items */
.conteneur { gap: 20px; }
```

❌ **Oublier que `fr` nécessite de l'espace disponible**
```css
/* ❌ Si le conteneur n'a pas de largeur définie */
.conteneur {
  display: grid;
  grid-template-columns: 1fr 1fr;
  /* Peut ne pas fonctionner comme prévu */
}

/* ✅ Avec largeur ou dans un conteneur dimensionné */
.conteneur {
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 100%;
}
```

---

## Conclusion

Les propriétés `grid-template-columns`, `grid-template-rows` et `gap` forment le **cœur de CSS Grid**. En les maîtrisant, vous pouvez créer :

- 📐 **Grilles simples** avec `repeat()` et `fr`
- 📱 **Layouts responsive** avec `auto-fit` et `minmax()`
- 🎨 **Structures complexes** avec des colonnes/lignes mixtes
- ✨ **Espacements propres** avec `gap`

### La recette magique responsive

```css
.conteneur {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

**Cette seule déclaration crée une grille qui s'adapte à toutes les tailles d'écran !**

Dans la prochaine leçon, nous verrons comment **placer manuellement les items** dans la grille pour créer des layouts encore plus sophistiqués.

---


⏭️ [Placement d'éléments dans la grille](/04-css3-styles-et-mise-en-page/03-mise-en-page-moderne/07-placement-elements-grille.md)
