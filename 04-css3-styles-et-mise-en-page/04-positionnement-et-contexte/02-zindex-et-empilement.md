🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.4.2 - Z-index et contextes d'empilement

## Introduction

Quand des éléments se superposent sur une page web, il faut déterminer **lequel apparaît au-dessus** des autres. C'est le rôle de la propriété `z-index` et du système d'**empilement** (stacking) en CSS.

### Le concept de la troisième dimension

Imaginez votre page web comme un **empilement de calques** :

```
     Vue de côté (axe Z)
          ↑
          │
    ┌─────┼─────┐  ← Élément en haut (z-index élevé)
    │     │     │
    ├─────┼─────┤  ← Élément du milieu
    │     │     │
    ├─────┼─────┤  ← Élément en bas (z-index bas)
    │     │     │
────┴─────┴─────┴──── Page (z-index: 0)
```

**Vue du dessus** (ce que vous voyez) :

```
┌─────────────────┐
│    Élément 3    │ ← Le plus haut est visible
│  (au-dessus)    │
└─────────────────┘
```

---

## 1. Empilement par défaut (sans z-index)

### Règles naturelles d'empilement

Même **sans utiliser `z-index`**, le navigateur a des règles pour déterminer quel élément apparaît au-dessus :

#### Règle 1 : Ordre dans le HTML

Les éléments qui apparaissent **plus tard** dans le HTML sont au-dessus :

```html
<div class="box1">Premier dans le HTML</div>
<div class="box2">Deuxième dans le HTML (au-dessus)</div>
```

**Résultat visuel** (si elles se chevauchent) :

```
┌──────────┐
│  Box 1   │
│    ┌─────┼─────┐
│    │ Box │ 2   │  ← Box 2 au-dessus
└────┼─────┘     │
     └───────────┘
```

#### Règle 2 : Éléments positionnés vs non-positionnés

Les éléments **positionnés** (`position` différent de `static`) passent automatiquement au-dessus des éléments non-positionnés :

```html
<div class="normal">Élément normal (static)</div>
<div class="positioned">Élément positionné (relative/absolute/fixed)</div>
```

**L'élément positionné sera au-dessus**, même s'il est premier dans le HTML.

### Exemple de l'empilement naturel

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Empilement naturel</title>
  <style>
    .container {
      padding: 50px;
    }

    .box {
      width: 200px;
      height: 200px;
      padding: 20px;
      color: white;
      font-weight: bold;
    }

    .box1 {
      background-color: rgba(255, 0, 0, 0.7);
      position: relative;
      top: 0;
      left: 0;
    }

    .box2 {
      background-color: rgba(0, 255, 0, 0.7);
      position: relative;
      top: -100px;
      left: 50px;
    }

    .box3 {
      background-color: rgba(0, 0, 255, 0.7);
      position: relative;
      top: -200px;
      left: 100px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box box1">Box 1<br>(première)</div>
    <div class="box box2">Box 2<br>(deuxième - au-dessus de 1)</div>
    <div class="box box3">Box 3<br>(troisième - au-dessus de tous)</div>
  </div>
</body>
</html>
```

**Sans `z-index`** : Box 3 est au-dessus car elle est la dernière dans le HTML.

---

## 2. La propriété `z-index`

### Qu'est-ce que `z-index` ?

`z-index` permet de contrôler **manuellement l'ordre d'empilement** des éléments positionnés.

```css
.element {
  position: relative; /* OU absolute, fixed, sticky */
  z-index: 10;
}
```

### ⚠️ Règle critique : z-index ne fonctionne qu'avec des éléments positionnés

```css
/* ❌ Ne fonctionne PAS */
.element {
  position: static; /* Valeur par défaut */
  z-index: 999;     /* IGNORÉ ! */
}

/* ✅ Fonctionne */
.element {
  position: relative; /* OU absolute, fixed, sticky */
  z-index: 999;       /* Pris en compte */
}
```

### Valeurs de z-index

```css
/* Entiers positifs */
z-index: 1;
z-index: 10;
z-index: 999;
z-index: 9999;

/* Entiers négatifs */
z-index: -1;
z-index: -10;

/* Auto (valeur par défaut) */
z-index: auto;

/* Pas de décimales */
z-index: 1.5; /* ❌ Invalide */
```

### Comment ça fonctionne ?

**Plus le nombre est élevé, plus l'élément est au-dessus** :

```
z-index: 100  ← Au-dessus de tout
z-index: 50
z-index: 10
z-index: 5
z-index: 1
z-index: 0    ← Défaut
z-index: -1   ← En dessous
```

### Exemple simple

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Z-index basique</title>
  <style>
    .container {
      position: relative;
      height: 300px;
    }

    .box {
      position: absolute;
      width: 150px;
      height: 150px;
      padding: 20px;
      color: white;
      font-weight: bold;
    }

    .rouge {
      background-color: rgba(255, 0, 0, 0.8);
      top: 50px;
      left: 50px;
      z-index: 1;
    }

    .vert {
      background-color: rgba(0, 255, 0, 0.8);
      top: 100px;
      left: 100px;
      z-index: 3; /* Le plus élevé - au-dessus */
    }

    .bleu {
      background-color: rgba(0, 0, 255, 0.8);
      top: 150px;
      left: 150px;
      z-index: 2;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box rouge">Rouge<br>z-index: 1</div>
    <div class="box vert">Vert<br>z-index: 3<br>(au-dessus)</div>
    <div class="box bleu">Bleu<br>z-index: 2</div>
  </div>
</body>
</html>
```

**Ordre d'affichage** (de bas en haut) :
1. Rouge (z-index: 1)
2. Bleu (z-index: 2)
3. Vert (z-index: 3) ← Visible au-dessus

---

## 3. Les contextes d'empilement (Stacking Contexts)

### Le piège : Pourquoi z-index: 9999 ne fonctionne pas toujours ?

Vous avez peut-être déjà vécu cette frustration :

```css
.element {
  position: relative;
  z-index: 9999; /* Devrait être au-dessus de TOUT, non ? */
}
```

**Mais non !** L'élément reste en dessous d'un autre qui a seulement `z-index: 10`.

**Pourquoi ?** À cause des **contextes d'empilement**.

### Qu'est-ce qu'un contexte d'empilement ?

Un contexte d'empilement est comme une **"bulle isolée"** où les z-index sont **locaux** à cette bulle.

```
Contexte d'empilement 1
┌─────────────────────────┐
│ z-index: 1              │
│ ├─ Enfant (z: 9999)     │ ← DANS le contexte 1
│ └─ Enfant (z: 5)        │
└─────────────────────────┘

Contexte d'empilement 2
┌─────────────────────────┐
│ z-index: 2              │ ← Ce contexte est au-dessus
│ ├─ Enfant (z: 1)        │ ← Même avec z: 1, au-dessus
│ └─ Enfant (z: 2)        │    de tout le contexte 1 !
└─────────────────────────┘
```

**Règle d'or** : Les enfants ne peuvent **jamais sortir** de leur contexte d'empilement parent.

### Exemple du problème

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Contexte d'empilement</title>
  <style>
    .parent1 {
      position: relative;
      z-index: 1; /* Crée un contexte d'empilement */
      background-color: rgba(255, 0, 0, 0.3);
      padding: 20px;
      margin: 20px;
    }

    .parent2 {
      position: relative;
      z-index: 2; /* Contexte au-dessus de parent1 */
      background-color: rgba(0, 0, 255, 0.3);
      padding: 20px;
      margin: 20px;
    }

    .child1 {
      position: relative;
      z-index: 9999; /* Très élevé mais DANS parent1 */
      background-color: yellow;
      padding: 20px;
    }

    .child2 {
      position: relative;
      z-index: 1; /* Faible mais DANS parent2 (qui est au-dessus) */
      background-color: lightgreen;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="parent1">
    Parent 1 (z-index: 1)
    <div class="child1">
      Enfant 1 (z-index: 9999)<br>
      Mais reste dans le contexte du parent 1
    </div>
  </div>

  <div class="parent2">
    Parent 2 (z-index: 2)
    <div class="child2">
      Enfant 2 (z-index: 1)<br>
      Mais au-dessus de tout parent 1 !
    </div>
  </div>
</body>
</html>
```

**Résultat** : Même avec `z-index: 9999`, l'enfant 1 ne peut pas passer au-dessus de parent2 et ses enfants.

---

## 4. Qu'est-ce qui crée un contexte d'empilement ?

### Conditions principales

Un élément crée un nouveau contexte d'empilement quand :

#### 1. `position` + `z-index` (différent de `auto`)

```css
.element {
  position: relative; /* OU absolute, fixed, sticky */
  z-index: 1;         /* Différent de auto */
}
/* ✅ Crée un contexte d'empilement */
```

```css
.element {
  position: relative;
  z-index: auto;      /* Valeur par défaut */
}
/* ❌ Ne crée PAS de contexte */
```

#### 2. `opacity` inférieure à 1

```css
.element {
  opacity: 0.99;
}
/* ✅ Crée un contexte d'empilement */
```

#### 3. `transform` (différent de `none`)

```css
.element {
  transform: translateX(10px);
}
/* ✅ Crée un contexte d'empilement */
```

#### 4. Autres propriétés

```css
/* Tous créent un contexte d'empilement : */
filter: blur(5px);
clip-path: circle(50%);
mix-blend-mode: multiply;
isolation: isolate;
will-change: transform;
```

### Tableau récapitulatif

| Propriété | Valeur | Crée un contexte ? |
|-----------|--------|-------------------|
| `position: relative` + `z-index: auto` | Par défaut | ❌ Non |
| `position: relative` + `z-index: 1` | Avec z-index | ✅ Oui |
| `position: absolute` + `z-index: 1` | Avec z-index | ✅ Oui |
| `position: fixed` | Toujours | ✅ Oui |
| `opacity: 0.99` | < 1 | ✅ Oui |
| `opacity: 1` | = 1 | ❌ Non |
| `transform: translateX(10px)` | Toute valeur | ✅ Oui |
| `filter: blur(5px)` | Toute valeur | ✅ Oui |

---

## 5. Débugger les problèmes de z-index

### Méthode 1 : DevTools du navigateur

**Chrome/Edge/Firefox** :
1. Inspectez l'élément
2. Regardez l'onglet "Layers" ou "3D View"
3. Visualisez les contextes d'empilement

### Méthode 2 : Isoler le problème

```css
/* Ajoutez temporairement des bordures colorées */
.parent {
  border: 3px solid red;
}

.child {
  border: 3px solid blue;
}
```

### Méthode 3 : Vérifier les conditions

**Checklist de debug** :

```
☐ L'élément a-t-il position: relative/absolute/fixed/sticky ?
☐ L'élément a-t-il un z-index défini ?
☐ Le parent crée-t-il un contexte d'empilement ?
☐ Y a-t-il une opacity < 1 quelque part ?
☐ Y a-t-il un transform ?
```

### Exemple de debug

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Debug z-index</title>
  <style>
    /* Situation problématique */
    .sidebar {
      position: relative;
      z-index: 1;
      opacity: 0.99; /* ⚠️ Crée un contexte d'empilement ! */
    }

    .dropdown {
      position: absolute;
      z-index: 9999; /* Ne sort pas de .sidebar */
    }

    /* Solution 1 : Retirer opacity */
    .sidebar-fixed {
      position: relative;
      z-index: 1;
      /* opacity: 0.99; ← Retiré */
    }

    /* Solution 2 : Augmenter z-index du parent */
    .sidebar-high-z {
      position: relative;
      z-index: 10000; /* Plus élevé que les autres éléments */
      opacity: 0.99;
    }
  </style>
</head>
<body>
  <h2>Problème et solutions</h2>
</body>
</html>
```

---

## 6. Bonnes pratiques pour z-index

### Système de niveaux

Plutôt que d'utiliser des nombres aléatoires, utilisez un **système organisé** :

```css
/* ❌ Mauvaise pratique */
.header { z-index: 9999; }
.modal { z-index: 99999; }
.tooltip { z-index: 999999; }

/* ✅ Bonne pratique : Système par niveaux */
:root {
  /* Définir des variables CSS */
  --z-dropdown: 1000;
  --z-sticky: 1100;
  --z-fixed: 1200;
  --z-modal-backdrop: 1300;
  --z-modal: 1400;
  --z-popover: 1500;
  --z-tooltip: 1600;
}

.dropdown {
  z-index: var(--z-dropdown);
}

.modal-backdrop {
  z-index: var(--z-modal-backdrop);
}

.modal {
  z-index: var(--z-modal);
}
```

### Échelle recommandée

```css
/* Base (contenu normal) */
.content { z-index: 1; }

/* Navigation et UI fixe */
.header { z-index: 100; }
.sidebar { z-index: 100; }

/* Overlays légers */
.dropdown { z-index: 1000; }
.popover { z-index: 1000; }

/* Overlays importants */
.modal-backdrop { z-index: 2000; }
.modal { z-index: 2010; }

/* Notifications et tooltips (toujours visibles) */
.toast { z-index: 3000; }
.tooltip { z-index: 3000; }
```

### Documentation

```css
/* Documentez vos z-index */
.modal {
  position: fixed;
  z-index: 2010; /* Au-dessus du backdrop (2000) mais sous les tooltips (3000) */
}
```

---

## 7. Cas d'usage pratiques

### Exemple 1 : Modal avec overlay

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Modal avec z-index</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 50px;
    }

    /* Contenu normal */
    .content {
      position: relative;
      z-index: 1;
      background-color: #f0f0f0;
      padding: 30px;
      border-radius: 10px;
    }

    /* Overlay sombre */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      z-index: 1000; /* Au-dessus du contenu */
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* Modal */
    .modal {
      position: relative;
      z-index: 1010; /* Au-dessus de l'overlay */
      background: white;
      padding: 40px;
      border-radius: 10px;
      max-width: 500px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.3);
    }

    /* Bouton fermer */
    .modal-close {
      position: absolute;
      top: 15px;
      right: 15px;
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
      z-index: 1; /* Au-dessus du contenu de la modal */
    }
  </style>
</head>
<body>
  <div class="content">
    <h1>Contenu de la page</h1>
    <p>Ce contenu est en dessous de la modal (z-index: 1).</p>
  </div>

  <!-- Modal (normalement cachée avec display: none) -->
  <div class="modal-overlay">
    <div class="modal">
      <button class="modal-close">&times;</button>
      <h2>Titre de la Modal</h2>
      <p>La modal a un z-index élevé pour apparaître au-dessus du contenu.</p>
      <p>L'overlay est entre le contenu et la modal.</p>
    </div>
  </div>
</body>
</html>
```

**Structure z-index** :
```
Tooltip (z: 3000)        ← Toujours visible
Modal (z: 1010)          ← Au-dessus de l'overlay
Overlay (z: 1000)        ← Masque le contenu
Contenu (z: 1)           ← En dessous
```

---

### Exemple 2 : Dropdown qui passe au-dessus d'autres éléments

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Dropdown z-index</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 20px;
    }

    .card {
      position: relative; /* Contexte pour le dropdown */
      background: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 20px;
      height: 200px;
    }

    .button {
      padding: 10px 20px;
      background: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    /* Dropdown */
    .dropdown {
      position: absolute;
      top: 100%;
      left: 0;
      margin-top: 5px;
      background: white;
      border: 1px solid #ddd;
      border-radius: 5px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      padding: 10px;
      min-width: 200px;
      z-index: 100; /* Au-dessus des autres cartes */
    }

    .dropdown ul {
      list-style: none;
    }

    .dropdown li {
      padding: 8px;
      cursor: pointer;
    }

    .dropdown li:hover {
      background-color: #f0f0f0;
    }
  </style>
</head>
<body>
  <h1>Cards avec Dropdown</h1>
  <p>Le dropdown doit passer au-dessus des autres cartes grâce à z-index.</p>
  <br>

  <div class="container">
    <div class="card">
      <h3>Carte 1</h3>
      <button class="button">Menu</button>
      <div class="dropdown">
        <ul>
          <li>Option 1</li>
          <li>Option 2</li>
          <li>Option 3</li>
        </ul>
      </div>
    </div>

    <div class="card">
      <h3>Carte 2</h3>
      <p>Cette carte est à côté</p>
    </div>

    <div class="card">
      <h3>Carte 3</h3>
      <p>Le dropdown de Carte 1 passe au-dessus grâce à z-index: 100</p>
    </div>
  </div>
</body>
</html>
```

---

### Exemple 3 : Sticky header avec z-index

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Sticky avec z-index</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
    }

    /* Header sticky */
    .header {
      position: sticky;
      top: 0;
      background: #2c3e50;
      color: white;
      padding: 20px;
      z-index: 1000; /* Au-dessus du contenu qui scroll */
    }

    /* Section avec image qui pourrait passer au-dessus */
    .section {
      position: relative;
      padding: 50px;
      min-height: 400px;
    }

    .section:nth-child(even) {
      background-color: #ecf0f1;
    }

    /* Image positionnée */
    .floating-image {
      position: absolute;
      top: 50px;
      right: 50px;
      width: 200px;
      height: 200px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      z-index: 10; /* Plus bas que le header */
    }
  </style>
</head>
<body>
  <header class="header">
    <h1>Header Sticky (z-index: 1000)</h1>
    <p>Je reste au-dessus de tout le contenu</p>
  </header>

  <section class="section">
    <h2>Section 1</h2>
    <p>Scrollez pour voir le header rester en haut.</p>
    <div class="floating-image">Image<br>(z: 10)</div>
  </section>

  <section class="section">
    <h2>Section 2</h2>
    <p>Le header passe au-dessus des images grâce à z-index: 1000.</p>
    <div class="floating-image">Image<br>(z: 10)</div>
  </section>

  <section class="section">
    <h2>Section 3</h2>
    <p>Même avec position: absolute, les images restent en dessous du header.</p>
  </section>
</body>
</html>
```

---

## 8. Problèmes courants et solutions

### Problème 1 : z-index ne fonctionne pas

**Symptôme** : J'ai mis `z-index: 9999` mais l'élément reste en dessous.

**Causes possibles** :

```css
/* ❌ Cause 1 : Pas de position */
.element {
  z-index: 9999;
  /* Pas de position définie = static par défaut */
}

/* ✅ Solution */
.element {
  position: relative;
  z-index: 9999;
}
```

```css
/* ❌ Cause 2 : Parent crée un contexte d'empilement */
.parent {
  position: relative;
  z-index: 1; /* Crée un contexte */
  opacity: 0.99; /* OU transform, etc. */
}

.child {
  position: relative;
  z-index: 9999; /* Piégé dans le contexte du parent */
}

/* ✅ Solution : Augmenter z-index du parent */
.parent {
  z-index: 100; /* Plus élevé que les autres éléments */
}
```

---

### Problème 2 : Modal en dessous du contenu

**Symptôme** : Ma modal apparaît derrière le contenu de la page.

**Solution** :

```css
/* S'assurer que la modal a un z-index élevé */
.modal-overlay {
  position: fixed;
  z-index: 1000;
}

.modal {
  position: relative;
  z-index: 1010;
}

/* Vérifier qu'aucun élément du contenu n'a un z-index encore plus élevé */
```

---

### Problème 3 : Dropdown coupé par overflow

**Symptôme** : Mon dropdown est coupé par le conteneur parent.

```css
/* ❌ Parent avec overflow: hidden */
.card {
  overflow: hidden; /* Coupe le dropdown ! */
}

/* ✅ Solutions possibles */

/* Solution 1 : Retirer overflow */
.card {
  /* overflow: hidden; */
}

/* Solution 2 : Placer le dropdown en dehors avec JavaScript */
document.body.appendChild(dropdownElement);

/* Solution 3 : Utiliser position: fixed au lieu de absolute */
.dropdown {
  position: fixed; /* Échappe à overflow: hidden */
}
```

---

### Problème 4 : Tooltip invisible

**Symptôme** : Mon tooltip ne s'affiche pas ou est coupé.

```css
/* ✅ Solution : z-index très élevé */
.tooltip {
  position: absolute;
  z-index: 9999; /* Au-dessus de tout */
}

/* Alternative : Utiliser position: fixed */
.tooltip {
  position: fixed;
  z-index: 9999;
}
```

---

## 9. Isolation : Créer un contexte volontairement

La propriété `isolation` permet de créer un contexte d'empilement **explicitement** :

```css
.container {
  isolation: isolate; /* Crée un contexte d'empilement */
}
```

### Cas d'usage

**Isoler une section** pour que ses z-index ne puissent pas interférer avec le reste de la page :

```css
/* Composant isolé */
.component {
  isolation: isolate;
}

.component .element {
  position: relative;
  z-index: 999; /* Ne sort pas du composant */
}
```

---

## 10. Récapitulatif visuel

### Hiérarchie d'empilement typique

```
┌─────────────────────────────────┐
│  Tooltips (z: 9000)             │ ← Toujours visible
├─────────────────────────────────┤
│  Modals (z: 2000)               │ ← Overlays importants
├─────────────────────────────────┤
│  Dropdowns (z: 1000)            │ ← Menus déroulants
├─────────────────────────────────┤
│  Sticky elements (z: 100)       │ ← Navigation fixe
├─────────────────────────────────┤
│  Positioned elements (z: 1-10)  │ ← Éléments positionnés
├─────────────────────────────────┤
│  Normal flow (z: 0 ou auto)     │ ← Contenu normal
├─────────────────────────────────┤
│  Behind elements (z: -1)        │ ← Arrière-plans
└─────────────────────────────────┘
```

---

## Points clés à retenir

✅ **z-index ne fonctionne qu'avec des éléments positionnés** (relative, absolute, fixed, sticky)

✅ **Plus le z-index est élevé, plus l'élément est au-dessus**

✅ **Les contextes d'empilement isolent les z-index** : un enfant ne peut pas sortir de son contexte

✅ **Plusieurs propriétés créent des contextes** : position + z-index, opacity < 1, transform, etc.

✅ **Utilisez un système organisé** : définissez des niveaux plutôt que des nombres aléatoires

✅ **Debuggez avec les DevTools** : visualisez les contextes d'empilement en 3D

✅ **Documentez vos z-index** : expliquez pourquoi tel élément a tel z-index

---

## Checklist de debug z-index

Quand un z-index ne fonctionne pas comme prévu :

```
☐ L'élément a-t-il position: relative/absolute/fixed/sticky ?
☐ Le z-index est-il un nombre entier (pas auto) ?
☐ Y a-t-il un parent qui crée un contexte d'empilement ?
☐ Vérifier opacity < 1 sur les parents
☐ Vérifier transform sur les parents
☐ Vérifier filter sur les parents
☐ Comparer les z-index au même niveau (même contexte)
☐ Utiliser les DevTools pour visualiser les layers
```

---

## Bonnes pratiques finales

### ✅ À faire

- Définir un système de z-index cohérent dans tout le projet
- Documenter les z-index importants
- Utiliser des variables CSS pour les niveaux
- Tester sur différents navigateurs
- Utiliser `isolation: isolate` pour les composants

### ❌ À éviter

- Augmenter aveuglément jusqu'à 999999
- Utiliser z-index sans position
- Créer des contextes d'empilement par accident (opacity, transform)
- Mélanger différents systèmes de numérotation

---

## Conclusion

Le `z-index` et les contextes d'empilement peuvent sembler complexes au début, mais en comprenant ces principes clés, vous pourrez :

- Contrôler précisément l'ordre d'affichage des éléments
- Résoudre rapidement les problèmes de superposition
- Créer des interfaces complexes avec modals, dropdowns, tooltips
- Éviter les bugs frustrants liés au z-index

**Règle d'or** : Toujours vérifier si un contexte d'empilement est créé quelque part dans la hiérarchie des parents. C'est la cause n°1 des problèmes de z-index !

---


Dans la prochaine leçon, nous verrons les techniques anciennes de mise en page (pour comprendre le code legacy), mais vous utiliserez rarement ces techniques dans du code moderne ! 🎉

⏭️ [ Float et clear (LEGACY - Maintenance uniquement)](/04-css3-styles-et-mise-en-page/04-positionnement-et-contexte/03-float-et-clear-legacy.md)
