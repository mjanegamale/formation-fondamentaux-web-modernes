🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3.2 - Conteneur flex : flex-direction, justify-content, align-items

## Introduction

Maintenant que nous avons vu comment activer Flexbox avec `display: flex`, découvrons les **propriétés les plus importantes** du conteneur flex. Ces trois propriétés vous permettront de contrôler la disposition de vos éléments dans la grande majorité des cas.

### Les trois propriétés essentielles

1. **`flex-direction`** : définit la direction des éléments (horizontal ou vertical)
2. **`justify-content`** : contrôle l'alignement sur l'axe principal
3. **`align-items`** : contrôle l'alignement sur l'axe secondaire

> **💡 Astuce** : Ces trois propriétés s'appliquent toujours sur le **conteneur** (le parent), jamais sur les éléments individuels.

---

## 1. `flex-direction` : Choisir la direction

La propriété `flex-direction` détermine **dans quelle direction** les éléments flex sont disposés.

### Syntaxe

```css
.conteneur {
  display: flex;
  flex-direction: valeur;
}
```

### Les quatre valeurs possibles

#### `row` (valeur par défaut)

Les éléments se placent **en ligne**, de gauche à droite.

```css
.conteneur {
  display: flex;
  flex-direction: row; /* Valeur par défaut */
}
```

**Représentation visuelle :**

```
┌─────────────────────────────────────┐
│  [Item 1] [Item 2] [Item 3]         │  ← gauche à droite
└─────────────────────────────────────┘
```

#### `row-reverse`

Les éléments se placent **en ligne**, mais de droite à gauche (ordre inversé).

```css
.conteneur {
  display: flex;
  flex-direction: row-reverse;
}
```

**Représentation visuelle :**

```
┌─────────────────────────────────────┐
│        [Item 3] [Item 2] [Item 1]   │  ← droite à gauche
└─────────────────────────────────────┘
```

#### `column`

Les éléments se placent **en colonne**, de haut en bas.

```css
.conteneur {
  display: flex;
  flex-direction: column;
}
```

**Représentation visuelle :**

```
┌──────────┐
│ Item 1   │  ↓
├──────────┤
│ Item 2   │  haut
├──────────┤
│ Item 3   │  vers
└──────────┘  bas
```

#### `column-reverse`

Les éléments se placent **en colonne**, mais de bas en haut (ordre inversé).

```css
.conteneur {
  display: flex;
  flex-direction: column-reverse;
}
```

**Représentation visuelle :**

```
┌──────────┐
│ Item 3   │  ↑
├──────────┤
│ Item 2   │  bas
├──────────┤
│ Item 1   │  vers
└──────────┘  haut
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Flex Direction</title>
  <style>
    .conteneur {
      display: flex;
      flex-direction: row; /* Changez pour tester : column, row-reverse, column-reverse */
      background-color: #f0f0f0;
      padding: 20px;
    }

    .item {
      background-color: #4CAF50;
      color: white;
      padding: 20px;
      margin: 10px;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
</body>
</html>
```

### Impact de `flex-direction` sur les axes

**📌 Point crucial** : `flex-direction` change **l'axe principal** !

- **`row` ou `row-reverse`** → Axe principal = horizontal (→)
- **`column` ou `column-reverse`** → Axe principal = vertical (↓)

Cela impacte directement `justify-content` et `align-items` que nous allons voir maintenant.

---

## 2. `justify-content` : Alignement sur l'axe principal

La propriété `justify-content` contrôle **comment les éléments sont répartis le long de l'axe principal** (la direction définie par `flex-direction`).

### Syntaxe

```css
.conteneur {
  display: flex;
  justify-content: valeur;
}
```

### Les valeurs principales

#### `flex-start` (valeur par défaut)

Les éléments sont alignés **au début** de l'axe principal.

```css
.conteneur {
  display: flex;
  justify-content: flex-start;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│ [1][2][3]                           │  ← alignés à gauche
└─────────────────────────────────────┘
```

#### `flex-end`

Les éléments sont alignés **à la fin** de l'axe principal.

```css
.conteneur {
  display: flex;
  justify-content: flex-end;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│                          [1][2][3]  │  ← alignés à droite
└─────────────────────────────────────┘
```

#### `center`

Les éléments sont **centrés** sur l'axe principal.

```css
.conteneur {
  display: flex;
  justify-content: center;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│            [1][2][3]                │  ← centrés
└─────────────────────────────────────┘
```

#### `space-between`

Les éléments sont **répartis uniformément** : le premier élément au début, le dernier à la fin, et l'espace est distribué entre les éléments.

```css
.conteneur {
  display: flex;
  justify-content: space-between;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│ [1]        [2]        [3]           │  ← espace entre les éléments
└─────────────────────────────────────┘
```

#### `space-around`

Les éléments sont répartis avec un **espace égal autour** de chaque élément.

```css
.conteneur {
  display: flex;
  justify-content: space-around;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│   [1]      [2]      [3]             │  ← espace autour de chaque élément
└─────────────────────────────────────┘
```

> **Note** : L'espace entre deux éléments est deux fois plus grand que l'espace entre un élément et le bord.

#### `space-evenly`

Les éléments sont répartis avec un **espace strictement égal** entre eux et aux bords.

```css
.conteneur {
  display: flex;
  justify-content: space-evenly;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│    [1]     [2]     [3]              │  ← espace strictement égal partout
└─────────────────────────────────────┘
```

### Exemple interactif

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Justify Content</title>
  <style>
    .conteneur {
      display: flex;
      justify-content: space-between; /* Changez cette valeur pour tester */
      background-color: #f0f0f0;
      padding: 20px;
      height: 200px;
    }

    .item {
      background-color: #2196F3;
      color: white;
      padding: 20px;
      width: 80px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
</body>
</html>
```

### Avec `flex-direction: column`

Quand l'axe principal est vertical, `justify-content` aligne verticalement :

```css
.conteneur {
  display: flex;
  flex-direction: column;
  justify-content: center; /* Centre verticalement */
  height: 400px;
}
```

**Représentation visuelle :**

```
┌──────────┐
│          │
│  Item 1  │  ← éléments
│  Item 2  │     centrés
│  Item 3  │     verticalement
│          │
└──────────┘
```

---

## 3. `align-items` : Alignement sur l'axe secondaire

La propriété `align-items` contrôle **comment les éléments sont alignés sur l'axe secondaire** (perpendiculaire à `flex-direction`).

### Syntaxe

```css
.conteneur {
  display: flex;
  align-items: valeur;
}
```

### Les valeurs principales

#### `stretch` (valeur par défaut)

Les éléments s'**étirent** pour remplir toute la hauteur (ou largeur) du conteneur.

```css
.conteneur {
  display: flex;
  align-items: stretch;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│ ┌───┐ ┌───┐ ┌───┐                   │
│ │ 1 │ │ 2 │ │ 3 │  ← éléments       │
│ │   │ │   │ │   │    étirés en      │
│ └───┘ └───┘ └───┘    hauteur        │
└─────────────────────────────────────┘
```

> **Note** : Pour que `stretch` fonctionne, les éléments ne doivent pas avoir de hauteur définie.

#### `flex-start`

Les éléments sont alignés **au début** de l'axe secondaire.

```css
.conteneur {
  display: flex;
  align-items: flex-start;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│ [1] [2] [3]      ← alignés en haut  │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

#### `flex-end`

Les éléments sont alignés **à la fin** de l'axe secondaire.

```css
.conteneur {
  display: flex;
  align-items: flex-end;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│ [1] [2] [3]      ← alignés en bas   │
└─────────────────────────────────────┘
```

#### `center`

Les éléments sont **centrés** sur l'axe secondaire.

```css
.conteneur {
  display: flex;
  align-items: center;
}
```

**Avec `flex-direction: row` :**

```
┌─────────────────────────────────────┐
│                                     │
│ [1] [2] [3]      ← centrés          │
│                    verticalement    │
└─────────────────────────────────────┘
```

#### `baseline`

Les éléments sont alignés sur leur **ligne de base de texte**.

```css
.conteneur {
  display: flex;
  align-items: baseline;
}
```

**Utile quand les éléments ont des tailles de texte différentes :**

```
┌─────────────────────────────────────┐
│     Grand                           │
│ [1] texte [2] [3]  ← alignés sur    │
│                      la baseline    │
└─────────────────────────────────────┘
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Align Items</title>
  <style>
    .conteneur {
      display: flex;
      align-items: center; /* Changez cette valeur pour tester */
      background-color: #f0f0f0;
      padding: 20px;
      height: 300px;
    }

    .item {
      background-color: #FF9800;
      color: white;
      padding: 20px;
      margin: 10px;
    }

    /* Différentes hauteurs pour mieux voir l'effet */
    .item:nth-child(1) { height: 50px; }
    .item:nth-child(2) { height: 80px; }
    .item:nth-child(3) { height: 60px; }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
</body>
</html>
```

### Avec `flex-direction: column`

Quand l'axe principal est vertical, `align-items` aligne horizontalement :

```css
.conteneur {
  display: flex;
  flex-direction: column;
  align-items: center; /* Centre horizontalement */
}
```

**Représentation visuelle :**

```
┌──────────────────┐
│     [Item 1]     │  ← éléments
│     [Item 2]     │     centrés
│     [Item 3]     │     horizontalement
└──────────────────┘
```

---

## Combinaisons courantes

### Centrer parfaitement un élément

Pour centrer un élément à la fois **horizontalement ET verticalement** :

```css
.conteneur {
  display: flex;
  justify-content: center;  /* Centre horizontalement */
  align-items: center;       /* Centre verticalement */
  height: 100vh;             /* Pleine hauteur de la fenêtre */
}
```

**Représentation visuelle :**

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│              [Contenu]              │  ← centré parfaitement
│                                     │
│                                     │
└─────────────────────────────────────┘
```

### Navigation horizontale avec éléments espacés

```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
}
```

**Résultat :**

```
┌─────────────────────────────────────┐
│ [Logo]    [Menu]    [Contact]       │  ← espacés et centrés verticalement
└─────────────────────────────────────┘
```

### Colonne centrée

```css
.conteneur {
  display: flex;
  flex-direction: column;
  justify-content: center;  /* Centre verticalement (axe principal) */
  align-items: center;       /* Centre horizontalement (axe secondaire) */
  height: 100vh;
}
```

### Cartes avec espacement uniforme

```css
.galerie {
  display: flex;
  justify-content: space-evenly;
  align-items: stretch;  /* Toutes les cartes ont la même hauteur */
  padding: 20px;
}
```

---

## Tableau récapitulatif

### `flex-direction`

| Valeur | Description | Axe principal |
|--------|-------------|---------------|
| `row` | En ligne, gauche → droite | Horizontal → |
| `row-reverse` | En ligne, droite → gauche | Horizontal ← |
| `column` | En colonne, haut → bas | Vertical ↓ |
| `column-reverse` | En colonne, bas → haut | Vertical ↑ |

### `justify-content` (axe principal)

| Valeur | Description |
|--------|-------------|
| `flex-start` | Aligné au début |
| `flex-end` | Aligné à la fin |
| `center` | Centré |
| `space-between` | Espace entre les éléments |
| `space-around` | Espace autour des éléments |
| `space-evenly` | Espace égal partout |

### `align-items` (axe secondaire)

| Valeur | Description |
|--------|-------------|
| `stretch` | Étiré sur toute la hauteur/largeur |
| `flex-start` | Aligné au début |
| `flex-end` | Aligné à la fin |
| `center` | Centré |
| `baseline` | Aligné sur la ligne de base du texte |

---

## Exemple pratique : Barre de navigation moderne

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Navigation Flexbox</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #333;
      padding: 1rem 2rem;
    }

    .logo {
      color: white;
      font-size: 1.5rem;
      font-weight: bold;
    }

    .menu {
      display: flex;
      gap: 2rem;
      list-style: none;
    }

    .menu a {
      color: white;
      text-decoration: none;
    }

    .menu a:hover {
      color: #4CAF50;
    }

    .btn-contact {
      background-color: #4CAF50;
      color: white;
      padding: 0.5rem 1.5rem;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <nav>
    <div class="logo">MonSite</div>

    <ul class="menu">
      <li><a href="#">Accueil</a></li>
      <li><a href="#">Services</a></li>
      <li><a href="#">Portfolio</a></li>
      <li><a href="#">À propos</a></li>
    </ul>

    <button class="btn-contact">Contact</button>
  </nav>
</body>
</html>
```

**Ce que fait Flexbox ici :**
- `justify-content: space-between` : répartit logo, menu et bouton
- `align-items: center` : aligne tout verticalement
- `display: flex` sur `.menu` : place les liens en ligne
- `gap: 2rem` : espace les liens du menu

---

## Points clés à retenir

✅ **`flex-direction`** définit la direction principale (row ou column)

✅ **`justify-content`** aligne sur l'**axe principal** (la direction choisie)

✅ **`align-items`** aligne sur l'**axe secondaire** (perpendiculaire)

✅ Pour **centrer parfaitement** : utilisez les deux propriétés avec `center`

✅ **`space-between`** et **`space-evenly`** sont parfaits pour répartir des éléments

✅ Pensez aux **axes** : ils changent selon `flex-direction` !

---

## Erreurs courantes à éviter

❌ **Confondre les axes** : `justify-content` suit toujours `flex-direction`

❌ **Oublier la hauteur du conteneur** : `align-items: center` ne marche que si le conteneur a une hauteur

❌ **Utiliser `align-items: stretch` avec une hauteur définie** sur les éléments

❌ **Mélanger les propriétés** du conteneur et des éléments (nous verrons les propriétés des éléments dans la prochaine leçon)

---

## Conclusion

Ces trois propriétés constituent le **cœur de Flexbox**. En les maîtrisant, vous pouvez déjà créer la majorité des layouts modernes :

- **Navigation responsive**
- **Cartes alignées**
- **Centrage parfait**
- **Galeries d'images**
- **Footers fixes**

Dans la prochaine leçon, nous explorerons les **propriétés des éléments flex** (`flex-grow`, `flex-shrink`, `flex-basis`) qui permettent de contrôler individuellement chaque élément.

---


⏭️ [Éléments flex : flex-grow, flex-shrink, flex-basis](/04-css3-styles-et-mise-en-page/03-mise-en-page-moderne/03-elements-flex.md)
