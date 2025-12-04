🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3.3 - Éléments flex : flex-grow, flex-shrink, flex-basis

## Introduction

Dans les leçons précédentes, nous avons vu les propriétés du **conteneur flex** qui contrôlent la disposition globale. Maintenant, découvrons les propriétés des **éléments flex individuels** qui permettent de contrôler comment chaque élément se comporte à l'intérieur du conteneur.

### Propriétés du conteneur vs propriétés des éléments

```css
/* ✅ Propriétés du CONTENEUR (parent) */
.conteneur {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

/* ✅ Propriétés des ÉLÉMENTS (enfants) */
.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0;
}
```

### Les trois propriétés essentielles des éléments

1. **`flex-grow`** : capacité à **grandir** et occuper l'espace disponible
2. **`flex-shrink`** : capacité à **rétrécir** si l'espace manque
3. **`flex-basis`** : taille de **base** de l'élément avant distribution de l'espace

> **💡 Ces propriétés répondent à la question** : "Comment l'espace disponible doit-il être distribué entre les éléments ?"

---

## 1. `flex-grow` : Capacité à grandir

La propriété `flex-grow` définit la **capacité d'un élément à grandir** pour occuper l'espace libre disponible dans le conteneur.

### Syntaxe

```css
.item {
  flex-grow: nombre; /* 0 par défaut */
}
```

- **Valeur** : un nombre positif (0, 1, 2, 3, etc.)
- **Par défaut** : `0` (l'élément ne grandit pas)

### Comment ça fonctionne ?

`flex-grow` est un **ratio** qui détermine quelle proportion de l'espace libre chaque élément va recevoir.

#### Exemple 1 : Tous les éléments avec `flex-grow: 1`

```css
.conteneur {
  display: flex;
  width: 600px;
}

.item {
  flex-grow: 1; /* Tous les éléments grandissent également */
  background-color: #4CAF50;
  padding: 20px;
}
```

**Résultat** : Les trois éléments se partagent l'espace **de manière égale**.

```
┌──────────────────────────────────────────────┐
│  [   Item 1   ] [   Item 2   ] [   Item 3   ]│
│      33%            33%            33%       │
└──────────────────────────────────────────────┘
```

#### Exemple 2 : Différents ratios de `flex-grow`

```css
.item1 { flex-grow: 1; }
.item2 { flex-grow: 2; } /* Grandit 2x plus que item1 */
.item3 { flex-grow: 1; }
```

**Comment calculer :**
- Total des ratios : 1 + 2 + 1 = 4
- Item1 : 1/4 de l'espace = 25%
- Item2 : 2/4 de l'espace = 50%
- Item3 : 1/4 de l'espace = 25%

**Résultat visuel :**

```
┌─────────────────────────────────────────────┐
│  [ Item 1 ] [    Item 2     ] [ Item 3 ]    │
│     25%           50%            25%        │
└─────────────────────────────────────────────┘
```

#### Exemple 3 : Un seul élément avec `flex-grow`

```css
.item1 { flex-grow: 0; } /* Garde sa taille naturelle */
.item2 { flex-grow: 1; } /* Prend tout l'espace restant */
.item3 { flex-grow: 0; } /* Garde sa taille naturelle */
```

**Résultat visuel :**

```
┌─────────────────────────────────────────────┐
│ [Item 1] [       Item 2         ] [Item 3]  │
│  taille     prend tout l'espace    taille   │
│  fixe          disponible           fixe    │
└─────────────────────────────────────────────┘
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Flex Grow</title>
  <style>
    .conteneur {
      display: flex;
      background-color: #f0f0f0;
      padding: 20px;
      gap: 10px;
    }

    .item {
      background-color: #4CAF50;
      color: white;
      padding: 20px;
      text-align: center;
    }

    .item1 { flex-grow: 1; }
    .item2 { flex-grow: 2; } /* Grandit 2 fois plus */
    .item3 { flex-grow: 1; }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item item1">Grow 1</div>
    <div class="item item2">Grow 2</div>
    <div class="item item3">Grow 1</div>
  </div>
</body>
</html>
```

### Cas d'usage courant : Layout avec sidebar

```css
.conteneur {
  display: flex;
}

.sidebar {
  flex-grow: 0; /* Garde sa largeur fixe */
  width: 250px;
}

.contenu-principal {
  flex-grow: 1; /* Prend tout l'espace restant */
}
```

**Résultat :**

```
┌────────────────────────────────────────┐
│ [Sidebar] [  Contenu principal       ] │
│  250px        tout l'espace restant    │
└────────────────────────────────────────┘
```

---

## 2. `flex-shrink` : Capacité à rétrécir

La propriété `flex-shrink` définit la **capacité d'un élément à rétrécir** si l'espace manque dans le conteneur.

### Syntaxe

```css
.item {
  flex-shrink: nombre; /* 1 par défaut */
}
```

- **Valeur** : un nombre positif (0, 1, 2, 3, etc.)
- **Par défaut** : `1` (l'élément peut rétrécir)
- **`0`** : l'élément ne rétrécit JAMAIS

### Comment ça fonctionne ?

`flex-shrink` détermine **quelle proportion de l'espace manquant** chaque élément va "absorber" en rétrécissant.

#### Exemple 1 : Comportement par défaut (`flex-shrink: 1`)

```css
.conteneur {
  display: flex;
  width: 400px; /* Conteneur petit */
}

.item {
  flex-shrink: 1; /* Valeur par défaut */
  width: 200px;   /* Chaque item veut 200px */
}
```

**Problème** : 3 items × 200px = 600px, mais le conteneur fait seulement 400px !

**Solution** : Les items rétrécissent **proportionnellement** pour tenir dans l'espace disponible.

```
┌─────────────────────────────┐
│ [Item 1] [Item 2] [Item 3]  │  ← tous rétrécis également
│  ~133px    ~133px    ~133px │
└─────────────────────────────┘
```

#### Exemple 2 : Empêcher un élément de rétrécir

```css
.item1 { flex-shrink: 0; }  /* NE rétrécit PAS */
.item2 { flex-shrink: 1; }  /* Peut rétrécir */
.item3 { flex-shrink: 1; }  /* Peut rétrécir */
```

**Résultat** : Item1 garde sa largeur, les autres s'adaptent.

```
┌─────────────────────────────┐
│ [Item 1] [Item 2]  [Item 3] │  ← Item1 garde 200px
│  200px     100px     100px  │     Item2 et Item3 rétrécissent
└─────────────────────────────┘
```

#### Exemple 3 : Différents ratios de rétrécissement

```css
.item1 { flex-shrink: 1; }
.item2 { flex-shrink: 3; }  /* Rétrécit 3x plus que item1 */
.item3 { flex-shrink: 1; }
```

**Résultat** : Item2 "absorbe" plus de rétrécissement que les autres.

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Flex Shrink</title>
  <style>
    .conteneur {
      display: flex;
      background-color: #f0f0f0;
      padding: 20px;
      width: 400px; /* Conteneur volontairement petit */
      gap: 10px;
    }

    .item {
      background-color: #2196F3;
      color: white;
      padding: 20px;
      width: 200px; /* Tous veulent 200px */
      text-align: center;
    }

    .item1 { flex-shrink: 0; }  /* Ne rétrécit pas */
    .item2 { flex-shrink: 1; }  /* Rétrécit normalement */
    .item3 { flex-shrink: 1; }  /* Rétrécit normalement */
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item item1">Shrink 0</div>
    <div class="item item2">Shrink 1</div>
    <div class="item item3">Shrink 1</div>
  </div>
</body>
</html>
```

### Cas d'usage : Boutons dans une barre d'outils

```css
.barre-outils {
  display: flex;
  gap: 10px;
}

.logo {
  flex-shrink: 0; /* Le logo ne rétrécit jamais */
  width: 150px;
}

.bouton {
  flex-shrink: 1; /* Les boutons peuvent rétrécir si besoin */
}
```

---

## 3. `flex-basis` : Taille de base

La propriété `flex-basis` définit la **taille initiale** de l'élément avant que l'espace libre ne soit distribué (avec `flex-grow`) ou que l'espace manquant ne soit absorbé (avec `flex-shrink`).

### Syntaxe

```css
.item {
  flex-basis: valeur; /* auto par défaut */
}
```

**Valeurs possibles :**
- **`auto`** (défaut) : utilise la largeur/hauteur de l'élément
- **Longueur** : `200px`, `20%`, `10rem`, etc.
- **`0`** : ignore la taille du contenu

### `flex-basis` vs `width`

`flex-basis` est similaire à `width` (pour `flex-direction: row`) ou `height` (pour `flex-direction: column`), mais avec une différence importante :

```css
/* Ces deux déclarations sont SIMILAIRES mais pas identiques */
.item {
  width: 200px;
}

.item {
  flex-basis: 200px;
}
```

**Différence** : `flex-basis` est la taille **avant** l'application de `flex-grow` et `flex-shrink`, tandis que `width` est une taille fixe.

> **💡 Règle générale** : Avec Flexbox, préférez `flex-basis` à `width`.

### Comprendre `flex-basis` avec un exemple

```css
.conteneur {
  display: flex;
  width: 600px;
}

.item {
  flex-basis: 100px; /* Chaque item commence à 100px */
  flex-grow: 1;      /* Puis grandit pour remplir l'espace */
}
```

**Calcul :**
1. Chaque item part de 100px (flex-basis)
2. 3 items × 100px = 300px utilisés
3. Espace restant : 600px - 300px = 300px
4. Cet espace est distribué avec `flex-grow: 1` (également)
5. Chaque item reçoit 100px supplémentaires
6. **Taille finale** : 100px + 100px = 200px par item

### `flex-basis: 0` : Un cas particulier important

Quand `flex-basis: 0`, la taille du contenu est **ignorée** et seul le ratio de `flex-grow` compte.

```css
.item1 {
  flex-basis: 0;
  flex-grow: 1;
}

.item2 {
  flex-basis: 0;
  flex-grow: 2; /* Sera exactement 2x plus grand que item1 */
}
```

**Sans `flex-basis: 0` :**
```
┌─────────────────────────────────────┐
│ [  Item 1 long   ] [   Item 2  ]    │
│   taille variable selon le contenu  │
└─────────────────────────────────────┘
```

**Avec `flex-basis: 0` :**
```
┌─────────────────────────────────────┐
│ [ Item 1 ] [    Item 2      ]       │
│    33%           67%                │
└─────────────────────────────────────┘
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Flex Basis</title>
  <style>
    .conteneur {
      display: flex;
      background-color: #f0f0f0;
      padding: 20px;
      gap: 10px;
    }

    .item {
      background-color: #FF9800;
      color: white;
      padding: 20px;
      text-align: center;
    }

    .item1 {
      flex-basis: 100px;
      flex-grow: 1;
    }

    .item2 {
      flex-basis: 200px; /* Part de 200px */
      flex-grow: 1;
    }

    .item3 {
      flex-basis: 100px;
      flex-grow: 1;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item item1">Basis 100px</div>
    <div class="item item2">Basis 200px</div>
    <div class="item item3">Basis 100px</div>
  </div>
</body>
</html>
```

---

## 4. La propriété raccourcie `flex`

Au lieu d'écrire `flex-grow`, `flex-shrink` et `flex-basis` séparément, on utilise généralement la **propriété raccourcie** `flex`.

### Syntaxe

```css
.item {
  flex: [flex-grow] [flex-shrink] [flex-basis];
}
```

### Valeurs courantes

#### `flex: 1` (le plus courant)

```css
.item {
  flex: 1;
}

/* Équivalent à : */
.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0;
}
```

**Usage** : Les éléments partagent l'espace de manière **parfaitement égale**.

#### `flex: auto`

```css
.item {
  flex: auto;
}

/* Équivalent à : */
.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: auto;
}
```

**Usage** : Les éléments grandissent et rétrécissent en fonction de leur contenu.

#### `flex: none`

```css
.item {
  flex: none;
}

/* Équivalent à : */
.item {
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: auto;
}
```

**Usage** : L'élément garde sa taille, ne grandit ni ne rétrécit.

#### `flex: 0 0 200px`

```css
.item {
  flex: 0 0 200px;
}

/* Équivalent à : */
.item {
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: 200px;
}
```

**Usage** : Élément de taille fixe (200px), ne change jamais.

### Tableau récapitulatif

| Syntaxe | flex-grow | flex-shrink | flex-basis | Usage |
|---------|-----------|-------------|------------|-------|
| `flex: 1` | 1 | 1 | 0 | Éléments égaux |
| `flex: 2` | 2 | 1 | 0 | Élément 2x plus grand |
| `flex: auto` | 1 | 1 | auto | Basé sur le contenu |
| `flex: none` | 0 | 0 | auto | Taille fixe (contenu) |
| `flex: 0 0 200px` | 0 | 0 | 200px | Taille fixe (200px) |

---

## Exemples pratiques courants

### 1. Layout classique : Sidebar + Contenu

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Layout Sidebar</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
    }

    .conteneur {
      display: flex;
      min-height: 100vh;
    }

    .sidebar {
      flex: 0 0 250px; /* Largeur fixe 250px */
      background-color: #333;
      color: white;
      padding: 20px;
    }

    .contenu {
      flex: 1; /* Prend tout l'espace restant */
      padding: 20px;
      background-color: #f5f5f5;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <aside class="sidebar">
      <h2>Menu</h2>
      <ul>
        <li>Accueil</li>
        <li>Services</li>
        <li>Contact</li>
      </ul>
    </aside>

    <main class="contenu">
      <h1>Contenu principal</h1>
      <p>Ce contenu prend tout l'espace disponible.</p>
    </main>
  </div>
</body>
</html>
```

### 2. Grille de cartes responsive

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Grille de cartes</title>
  <style>
    .conteneur {
      display: flex;
      gap: 20px;
      padding: 20px;
    }

    .carte {
      flex: 1; /* Toutes les cartes partagent l'espace également */
      min-width: 200px; /* Largeur minimale */
      background-color: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 20px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .carte h3 {
      margin-top: 0;
      color: #333;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="carte">
      <h3>Service 1</h3>
      <p>Description du service 1</p>
    </div>

    <div class="carte">
      <h3>Service 2</h3>
      <p>Description du service 2</p>
    </div>

    <div class="carte">
      <h3>Service 3</h3>
      <p>Description du service 3</p>
    </div>
  </div>
</body>
</html>
```

### 3. Barre de progression

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Barre de progression</title>
  <style>
    .barre-container {
      display: flex;
      height: 40px;
      background-color: #e0e0e0;
      border-radius: 20px;
      overflow: hidden;
    }

    .progression {
      flex: 0 0 60%; /* 60% de progression */
      background: linear-gradient(90deg, #4CAF50, #8BC34A);
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      transition: flex-basis 0.3s ease;
    }
  </style>
</head>
<body>
  <div class="barre-container">
    <div class="progression">60%</div>
  </div>
</body>
</html>
```

### 4. Footer qui reste en bas (Sticky Footer)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Sticky Footer</title>
  <style>
    body {
      margin: 0;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    header {
      flex: 0 0 auto; /* Taille basée sur le contenu */
      background-color: #333;
      color: white;
      padding: 20px;
    }

    main {
      flex: 1; /* Prend tout l'espace disponible */
      padding: 20px;
    }

    footer {
      flex: 0 0 auto; /* Taille basée sur le contenu */
      background-color: #333;
      color: white;
      padding: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <header>
    <h1>Mon Site</h1>
  </header>

  <main>
    <p>Le contenu principal s'étend...</p>
    <p>...et le footer reste toujours en bas !</p>
  </main>

  <footer>
    <p>&copy; 2025 Mon Site</p>
  </footer>
</body>
</html>
```

---

## Comparaison visuelle : Impact des propriétés

### Scénario : 3 items dans un conteneur de 600px

```css
.conteneur {
  display: flex;
  width: 600px;
}
```

#### Cas 1 : `flex: 1` sur tous les items

```css
.item { flex: 1; }
```

```
┌─────────────────────────────────────┐
│  [   200px   ] [   200px   ] [   200px   ] │
│     Item 1        Item 2        Item 3     │
└─────────────────────────────────────┘
```

#### Cas 2 : Différents ratios

```css
.item1 { flex: 1; }
.item2 { flex: 2; }
.item3 { flex: 1; }
```

```
┌─────────────────────────────────────┐
│ [ 150px ] [    300px    ] [ 150px ] │
│  Item 1      Item 2        Item 3   │
└─────────────────────────────────────┘
```

#### Cas 3 : Un item fixe, les autres flexibles

```css
.item1 { flex: 0 0 100px; } /* Fixe à 100px */
.item2 { flex: 1; }
.item3 { flex: 1; }
```

```
┌─────────────────────────────────────┐
│ [100px] [   250px   ] [   250px   ] │
│  Item 1     Item 2        Item 3    │
└─────────────────────────────────────┘
```

---

## Points clés à retenir

✅ **`flex-grow`** : contrôle la capacité à grandir (ratio de distribution)

✅ **`flex-shrink`** : contrôle la capacité à rétrécir (ratio de réduction)

✅ **`flex-basis`** : définit la taille de base avant distribution

✅ **`flex: 1`** est la syntaxe la plus courante (éléments égaux)

✅ **`flex: 0 0 XXpx`** crée un élément de taille fixe

✅ Préférez la propriété raccourcie **`flex`** plutôt que les trois propriétés séparées

✅ **`flex-basis: 0`** force un calcul basé uniquement sur les ratios de `flex-grow`

---

## Erreurs courantes à éviter

❌ **Confondre `width` et `flex-basis`** : avec Flexbox, utilisez `flex-basis`

❌ **Oublier que `flex-shrink: 1` est la valeur par défaut** : les éléments rétrécissent automatiquement

❌ **Utiliser `flex-grow` sans comprendre `flex-basis`** : le point de départ compte !

❌ **Mélanger unités absolues et flex** : `width: 200px` + `flex: 1` peut causer des comportements inattendus

❌ **Ne pas tester avec différentes tailles de conteneur** : vérifiez toujours le comportement responsive

---

## Quand utiliser quoi ?

### `flex: 1` → Éléments égaux
**Cas d'usage** : Cartes, colonnes égales, navigation

```css
.carte { flex: 1; }
```

### `flex: 0 0 XXpx` → Taille fixe
**Cas d'usage** : Sidebar, toolbar, icônes

```css
.sidebar { flex: 0 0 250px; }
```

### `flex: auto` → Basé sur le contenu
**Cas d'usage** : Boutons, badges, éléments de taille variable

```css
.bouton { flex: auto; }
```

### `flex: none` → Pas de flexibilité
**Cas d'usage** : Logos, images, éléments qui ne doivent jamais changer

```css
.logo { flex: none; }
```

---

## Conclusion

Les propriétés `flex-grow`, `flex-shrink` et `flex-basis` (combinées dans `flex`) donnent un **contrôle précis** sur la manière dont les éléments individuels se comportent dans un conteneur flex.

**En combinant :**
- Les propriétés du **conteneur** (`flex-direction`, `justify-content`, `align-items`)
- Les propriétés des **éléments** (`flex-grow`, `flex-shrink`, `flex-basis`)

...vous pouvez créer pratiquement **n'importe quel layout moderne** de manière simple et responsive !

Dans la prochaine leçon, nous comparerons Flexbox et CSS Grid pour comprendre quand utiliser l'un ou l'autre.

---


⏭️ [Flexbox vs Grid : quand utiliser quoi](/04-css3-styles-et-mise-en-page/03-mise-en-page-moderne/04-flexbox-vs-grid.md)
