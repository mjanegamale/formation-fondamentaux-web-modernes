🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.4.1 - Types de positionnement : static, relative, absolute, fixed, sticky

## Introduction

Le **positionnement** en CSS permet de contrôler précisément **où les éléments apparaissent** sur la page. C'est différent de Flexbox et Grid qui organisent des groupes d'éléments : le positionnement vous permet de sortir du flux normal pour placer un élément exactement où vous le souhaitez.

### La propriété `position`

Tout se joue avec une seule propriété CSS :

```css
.element {
  position: valeur;
}
```

**Les 5 valeurs possibles** :
1. `static` - Positionnement par défaut (flux normal)
2. `relative` - Positionnement relatif à sa position d'origine
3. `absolute` - Positionnement absolu par rapport à un parent
4. `fixed` - Positionnement fixe par rapport à la fenêtre
5. `sticky` - Combinaison de relative et fixed

> **💡 Concept clé** : Une fois qu'on change `position`, on peut utiliser les propriétés `top`, `right`, `bottom`, `left` pour déplacer l'élément.

---

## Le flux normal (avant positionnement)

Avant de voir les différents types de positionnement, comprenons le **flux normal** du document.

### Flux normal = ordre naturel

Par défaut, les éléments s'affichent dans l'ordre où ils apparaissent dans le HTML :

```html
<div>Premier élément</div>
<div>Deuxième élément</div>
<div>Troisième élément</div>
```

**Résultat visuel** (éléments block) :

```
┌────────────────────┐
│ Premier élément    │
├────────────────────┤
│ Deuxième élément   │
├────────────────────┤
│ Troisième élément  │
└────────────────────┘
```

Les éléments suivent le flux : de haut en bas pour les éléments block, de gauche à droite pour les inline.

---

## 1. `position: static` - Le positionnement par défaut

### Qu'est-ce que c'est ?

`static` est la valeur **par défaut** de tous les éléments. Vous n'avez presque jamais besoin de l'écrire explicitement.

```css
.element {
  position: static; /* Valeur par défaut */
}
```

### Caractéristiques

- ✅ L'élément suit le **flux normal** du document
- ✅ Les propriétés `top`, `right`, `bottom`, `left` **n'ont aucun effet**
- ✅ L'élément ne crée pas de **contexte de positionnement**

### Exemple

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Position Static</title>
  <style>
    .box {
      background-color: #4CAF50;
      color: white;
      padding: 20px;
      margin: 10px;
    }

    .box-static {
      position: static; /* Comportement par défaut */
      top: 50px;        /* N'a AUCUN effet avec static */
      left: 50px;       /* N'a AUCUN effet avec static */
    }
  </style>
</head>
<body>
  <div class="box">Box 1 (normale)</div>
  <div class="box box-static">Box 2 (static - identique)</div>
  <div class="box">Box 3 (normale)</div>
</body>
</html>
```

**Résultat** : Les trois boîtes s'affichent normalement, l'une sous l'autre. Les propriétés `top` et `left` sont ignorées.

### Quand utiliser `static` ?

**Presque jamais !** C'est la valeur par défaut, donc inutile de l'écrire sauf pour **réinitialiser** un positionnement :

```css
.element {
  position: absolute; /* Quelque part dans le code */
}

/* Plus tard, on veut revenir au flux normal */
@media (max-width: 768px) {
  .element {
    position: static; /* Réinitialise le positionnement */
  }
}
```

---

## 2. `position: relative` - Positionnement relatif

### Qu'est-ce que c'est ?

`relative` permet de **déplacer un élément par rapport à sa position d'origine** dans le flux normal.

```css
.element {
  position: relative;
  top: 20px;    /* Descend de 20px */
  left: 30px;   /* Va vers la droite de 30px */
}
```

### Caractéristiques

- ✅ L'élément reste dans le **flux normal** (l'espace qu'il occupait est conservé)
- ✅ On peut le déplacer avec `top`, `right`, `bottom`, `left`
- ✅ Les autres éléments ne sont **pas affectés** par le déplacement
- ✅ Crée un **contexte de positionnement** pour les enfants absolus

### Comment ça fonctionne ?

L'élément est d'abord placé normalement, puis **décalé** selon les valeurs spécifiées :

```
Position d'origine (invisible)
      ↓
    [   ]          L'élément
      ↘            est décalé
        [Box]      mais son espace
                   d'origine reste réservé
```

### Exemple visuel

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Position Relative</title>
  <style>
    .container {
      background-color: #f0f0f0;
      padding: 20px;
    }

    .box {
      background-color: #2196F3;
      color: white;
      padding: 20px;
      margin: 10px;
    }

    .box-relative {
      position: relative;
      top: 30px;        /* Descend de 30px */
      left: 50px;       /* Va à droite de 50px */
      background-color: #FF9800;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box">Box 1</div>
    <div class="box box-relative">Box 2 (relative)</div>
    <div class="box">Box 3</div>
  </div>
</body>
</html>
```

**Résultat visuel** :

```
┌────────────────────────────────┐
│ [Box 1]                        │
│                                │
│    [espace vide]               │ ← Espace réservé pour Box 2
│         [Box 2]                │ ← Box 2 décalée mais espace gardé
│                                │
│ [Box 3]                        │ ← Box 3 reste à sa place normale
└────────────────────────────────┘
```

### Les propriétés de décalage

```css
.element {
  position: relative;

  top: 20px;     /* Décale vers le BAS de 20px */
  bottom: 20px;  /* Décale vers le HAUT de 20px */
  left: 20px;    /* Décale vers la DROITE de 20px */
  right: 20px;   /* Décale vers la GAUCHE de 20px */
}
```

**⚠️ Attention** : `top` et `bottom` (ou `left` et `right`) peuvent se contredire. En général, on n'utilise qu'un des deux.

### Cas d'usage courants

#### 1. Ajustement léger de position

```css
.icon {
  position: relative;
  top: 2px; /* Aligne légèrement une icône avec le texte */
}
```

#### 2. Créer un contexte pour position absolute

```css
.card {
  position: relative; /* Crée le contexte */
}

.card-badge {
  position: absolute; /* Se positionne par rapport à .card */
  top: 10px;
  right: 10px;
}
```

#### 3. Animations et transitions

```css
.button {
  position: relative;
  top: 0;
  transition: top 0.3s;
}

.button:hover {
  top: -3px; /* Le bouton "monte" au survol */
}
```

---

## 3. `position: absolute` - Positionnement absolu

### Qu'est-ce que c'est ?

`absolute` **sort l'élément du flux normal** et le positionne par rapport à son **plus proche ancêtre positionné** (qui a `position: relative`, `absolute`, `fixed`, ou `sticky`).

```css
.element {
  position: absolute;
  top: 20px;
  right: 20px;
}
```

### Caractéristiques

- ❗ L'élément est **retiré du flux** (ne prend plus de place)
- ❗ Les autres éléments se comportent comme s'il n'existait pas
- ✅ Se positionne par rapport à l'ancêtre positionné le plus proche
- ✅ Si aucun ancêtre positionné : se positionne par rapport à `<html>`
- ✅ Peut être positionné avec `top`, `right`, `bottom`, `left`

### Le concept de contexte de positionnement

C'est **LE concept clé** pour comprendre `absolute` :

```html
<div class="parent" style="position: relative;">
  <div class="enfant" style="position: absolute; top: 10px; right: 10px;">
    Je me positionne par rapport à .parent !
  </div>
</div>
```

**Règle d'or** : Un élément `absolute` se positionne par rapport au **premier parent qui a une position différente de static**.

### Exemple visuel

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Position Absolute</title>
  <style>
    .container {
      position: relative; /* Crée le contexte de positionnement */
      background-color: #f0f0f0;
      padding: 20px;
      height: 300px;
      margin: 20px;
      border: 2px dashed #999;
    }

    .box-normal {
      background-color: #2196F3;
      color: white;
      padding: 20px;
      margin: 10px;
    }

    .box-absolute {
      position: absolute;
      top: 20px;        /* 20px depuis le haut du container */
      right: 20px;      /* 20px depuis la droite du container */
      background-color: #FF9800;
      color: white;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box-normal">Box normale 1</div>
    <div class="box-absolute">Box absolute</div>
    <div class="box-normal">Box normale 2</div>
  </div>
</body>
</html>
```

**Résultat visuel** :

```
┌─────────────────────────────┐ ← container (relative)
│ [Box normale 1]             │
│                 [Box absolu]│ ← Position : top: 20px, right: 20px
│                             │
│ [Box normale 2]             │ ← Remonte car Box absolue ne prend pas de place
│                             │
└─────────────────────────────┘
```

### Positionnement dans les coins

```css
/* Coin supérieur gauche */
.top-left {
  position: absolute;
  top: 0;
  left: 0;
}

/* Coin supérieur droit */
.top-right {
  position: absolute;
  top: 0;
  right: 0;
}

/* Coin inférieur gauche */
.bottom-left {
  position: absolute;
  bottom: 0;
  left: 0;
}

/* Coin inférieur droit */
.bottom-right {
  position: absolute;
  bottom: 0;
  right: 0;
}

/* Centré */
.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

### Cas d'usage courants

#### 1. Badges et notifications

```html
<div class="card" style="position: relative;">
  <img src="product.jpg" alt="Produit">
  <span class="badge" style="position: absolute; top: 10px; right: 10px;">
    NOUVEAU
  </span>
</div>
```

#### 2. Overlays et modales

```css
.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
}
```

#### 3. Tooltips

```css
.tooltip-container {
  position: relative;
}

.tooltip {
  position: absolute;
  bottom: 100%; /* Au-dessus de l'élément parent */
  left: 50%;
  transform: translateX(-50%);
}
```

### Exemple complet : Carte avec badge

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Carte avec Badge</title>
  <style>
    .card {
      position: relative; /* Contexte pour le badge */
      width: 300px;
      background: white;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      margin: 50px;
    }

    .card-image {
      width: 100%;
      height: 200px;
      background: linear-gradient(135deg, #667eea, #764ba2);
    }

    .card-content {
      padding: 20px;
    }

    .badge {
      position: absolute;
      top: 15px;
      right: 15px;
      background-color: #FF5722;
      color: white;
      padding: 8px 15px;
      border-radius: 20px;
      font-weight: bold;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <div class="card">
    <div class="card-image"></div>
    <div class="badge">-20%</div>
    <div class="card-content">
      <h3>Produit en promotion</h3>
      <p>Description du produit avec badge positionné en absolute.</p>
    </div>
  </div>
</body>
</html>
```

---

## 4. `position: fixed` - Positionnement fixe

### Qu'est-ce que c'est ?

`fixed` positionne l'élément par rapport à la **fenêtre du navigateur** (viewport) et il **reste fixe lors du scroll**.

```css
.element {
  position: fixed;
  top: 0;
  right: 0;
}
```

### Caractéristiques

- ❗ L'élément est **retiré du flux** (comme `absolute`)
- ✅ Se positionne par rapport à la **fenêtre** (viewport)
- ✅ **Reste visible** même lors du scroll
- ✅ Ignore tous les parents, même avec `position: relative`

### Exemple : Header fixe

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Header Fixe</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      padding-top: 70px; /* Espace pour le header fixe */
    }

    .header {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 60px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      display: flex;
      align-items: center;
      padding: 0 30px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      z-index: 1000;
    }

    .content {
      padding: 20px;
      max-width: 800px;
      margin: 0 auto;
    }

    .section {
      height: 400px;
      margin-bottom: 20px;
      background-color: #f0f0f0;
      padding: 20px;
      border-radius: 8px;
    }
  </style>
</head>
<body>
  <header class="header">
    <h1>Header Fixe - Scrollez la page !</h1>
  </header>

  <main class="content">
    <div class="section">
      <h2>Section 1</h2>
      <p>Le header reste fixe en haut même quand vous scrollez.</p>
    </div>

    <div class="section">
      <h2>Section 2</h2>
      <p>Continuez à scroller pour voir l'effet.</p>
    </div>

    <div class="section">
      <h2>Section 3</h2>
      <p>Le header est toujours visible !</p>
    </div>
  </main>
</body>
</html>
```

### Cas d'usage courants

#### 1. Navigation fixe en haut

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
}
```

#### 2. Bouton "Retour en haut"

```css
.back-to-top {
  position: fixed;
  bottom: 30px;
  right: 30px;
  z-index: 1000;
}
```

#### 3. Chat widget

```css
.chat-widget {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 350px;
  height: 500px;
}
```

#### 4. Sidebar fixe

```css
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 250px;
  height: 100vh;
  overflow-y: auto;
}
```

### ⚠️ Attention avec `fixed`

**Problème 1** : L'élément ne prend plus de place

```css
/* ❌ Sans compensation */
.header {
  position: fixed;
  height: 60px;
}

/* Le contenu passe sous le header ! */
```

```css
/* ✅ Avec compensation */
body {
  padding-top: 60px; /* Hauteur du header */
}
```

**Problème 2** : Peut bloquer l'accès au contenu sur mobile

```css
/* Mieux sur mobile : réduire ou cacher */
@media (max-width: 768px) {
  .sidebar-fixed {
    display: none; /* Ou transform pour un menu hamburger */
  }
}
```

---

## 5. `position: sticky` - Positionnement collant

### Qu'est-ce que c'est ?

`sticky` est un **hybride** entre `relative` et `fixed`. L'élément se comporte comme `relative` jusqu'à atteindre un seuil de scroll, puis devient `fixed`.

```css
.element {
  position: sticky;
  top: 0; /* Devient "collé" en haut quand on scroll */
}
```

### Caractéristiques

- ✅ Reste dans le **flux normal** (comme `relative`)
- ✅ Devient **fixe** quand on atteint le seuil défini
- ✅ Ne devient fixe que **dans son conteneur parent**
- ✅ Nécessite au moins une propriété `top`, `right`, `bottom`, ou `left`

### Comment ça fonctionne ?

```
┌─────────────────────┐
│   [Contenu]         │
│   [Contenu]         │ ← On scroll...
│                     │
│   [Sticky Element]  │ ← Position normale au départ
│                     │
│   [Contenu]         │
│   [Contenu]         │
└─────────────────────┘

         ↓ Après scroll ↓

┌─────────────────────┐
│ [Sticky Element]    │ ← Devient fixe en haut !
├─────────────────────┤
│   [Contenu]         │
│   [Contenu]         │ ← Continue de scroller sous sticky
│   [Contenu]         │
└─────────────────────┘
```

### Exemple : Table header collant

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Sticky Header</title>
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

    h1 {
      margin-bottom: 30px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    thead {
      position: sticky;
      top: 0;
      z-index: 10;
    }

    th {
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      padding: 15px;
      text-align: left;
    }

    td {
      padding: 15px;
      border-bottom: 1px solid #ddd;
      background: white;
    }

    tr:nth-child(even) td {
      background-color: #f9f9f9;
    }
  </style>
</head>
<body>
  <h1>Tableau avec en-tête collant</h1>
  <p>Scrollez vers le bas - l'en-tête reste visible !</p>
  <br>

  <table>
    <thead>
      <tr>
        <th>Nom</th>
        <th>Prénom</th>
        <th>Email</th>
        <th>Ville</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Dupont</td><td>Jean</td><td>jean.dupont@email.com</td><td>Paris</td></tr>
      <tr><td>Martin</td><td>Sophie</td><td>sophie.martin@email.com</td><td>Lyon</td></tr>
      <tr><td>Bernard</td><td>Pierre</td><td>pierre.bernard@email.com</td><td>Marseille</td></tr>
      <tr><td>Dubois</td><td>Marie</td><td>marie.dubois@email.com</td><td>Toulouse</td></tr>
      <tr><td>Thomas</td><td>Paul</td><td>paul.thomas@email.com</td><td>Nice</td></tr>
      <tr><td>Robert</td><td>Julie</td><td>julie.robert@email.com</td><td>Nantes</td></tr>
      <tr><td>Petit</td><td>Marc</td><td>marc.petit@email.com</td><td>Strasbourg</td></tr>
      <tr><td>Richard</td><td>Anne</td><td>anne.richard@email.com</td><td>Bordeaux</td></tr>
      <tr><td>Durand</td><td>Luc</td><td>luc.durand@email.com</td><td>Lille</td></tr>
      <tr><td>Leroy</td><td>Emma</td><td>emma.leroy@email.com</td><td>Rennes</td></tr>
      <tr><td>Moreau</td><td>Tom</td><td>tom.moreau@email.com</td><td>Reims</td></tr>
      <tr><td>Simon</td><td>Léa</td><td>lea.simon@email.com</td><td>Dijon</td></tr>
      <tr><td>Laurent</td><td>Hugo</td><td>hugo.laurent@email.com</td><td>Grenoble</td></tr>
      <tr><td>Lefebvre</td><td>Chloé</td><td>chloe.lefebvre@email.com</td><td>Angers</td></tr>
      <tr><td>Michel</td><td>Lucas</td><td>lucas.michel@email.com</td><td>Toulon</td></tr>
      <!-- Ajoutez plus de lignes pour tester le scroll -->
    </tbody>
  </table>
</body>
</html>
```

### Cas d'usage courants

#### 1. En-têtes de section

```css
.section-header {
  position: sticky;
  top: 60px; /* En dessous d'un header fixe */
  background: white;
  z-index: 5;
}
```

#### 2. Sidebar qui colle

```css
.sidebar {
  position: sticky;
  top: 20px;
  align-self: start; /* Important avec Flexbox/Grid */
}
```

#### 3. Call-to-action qui reste visible

```css
.cta-button {
  position: sticky;
  bottom: 20px;
  margin-top: auto;
}
```

### ⚠️ Particularités de `sticky`

**Condition 1** : Nécessite un seuil
```css
/* ❌ Ne marchera pas */
.element {
  position: sticky;
  /* Pas de top/bottom/left/right = ne colle jamais */
}

/* ✅ Fonctionne */
.element {
  position: sticky;
  top: 0;
}
```

**Condition 2** : Le parent doit avoir de la place pour scroller
```css
/* ❌ Le parent n'a pas de hauteur définie */
.parent {
  /* overflow: hidden; empêche aussi sticky */
}

/* ✅ Le parent permet le scroll */
.parent {
  height: 500px;
  overflow-y: auto;
}
```

**Condition 3** : Ne fonctionne que dans son conteneur
```css
/* Sticky s'arrête quand son parent sort de l'écran */
.section {
  /* sticky restera collé jusqu'à ce que .section soit entièrement scrollé */
}

.section .sticky-element {
  position: sticky;
  top: 0;
}
```

---

## Tableau comparatif

| Propriété | Dans le flux ? | Référence | Scroll | Use case typique |
|-----------|----------------|-----------|--------|------------------|
| `static` | ✅ Oui | - | Scroll normalement | Par défaut |
| `relative` | ✅ Oui (espace réservé) | Lui-même | Scroll normalement | Contexte pour absolute, ajustements |
| `absolute` | ❌ Non | Ancêtre positionné | Scroll avec parent | Badges, overlays, tooltips |
| `fixed` | ❌ Non | Fenêtre (viewport) | Ne scroll pas | Headers, boutons flottants |
| `sticky` | ✅ Oui | Parent puis viewport | Hybride | Table headers, sidebars |

---

## Les propriétés de décalage

Une fois qu'on a changé `position` (sauf `static`), on peut utiliser :

```css
.element {
  position: absolute; /* ou relative, fixed, sticky */

  top: 20px;     /* Distance depuis le HAUT */
  right: 20px;   /* Distance depuis la DROITE */
  bottom: 20px;  /* Distance depuis le BAS */
  left: 20px;    /* Distance depuis la GAUCHE */
}
```

### Valeurs possibles

```css
/* Pixels */
top: 20px;

/* Pourcentages (relatif au parent) */
top: 50%;

/* Em / Rem */
top: 2rem;

/* Calc */
top: calc(50% - 25px);

/* Auto (valeur par défaut) */
top: auto;
```

### Combinaisons

```css
/* Coller en haut à gauche */
.element {
  top: 0;
  left: 0;
}

/* Centrer horizontalement */
.element {
  left: 50%;
  transform: translateX(-50%);
}

/* Centrer complètement */
.element {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Étendre sur toute la largeur */
.element {
  left: 0;
  right: 0;
}

/* Étendre sur toute la zone */
.element {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
```

---

## Exemples pratiques complets

### Exemple 1 : Modal / Popup

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Modal</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 50px;
    }

    /* Overlay qui couvre toute la page */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
    }

    /* Modal centrée */
    .modal {
      position: relative; /* Pour le bouton de fermeture */
      background: white;
      border-radius: 10px;
      padding: 40px;
      max-width: 500px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.3);
    }

    /* Bouton fermer en absolute */
    .modal-close {
      position: absolute;
      top: 15px;
      right: 15px;
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
      color: #999;
    }

    .modal-close:hover {
      color: #333;
    }
  </style>
</head>
<body>
  <h1>Exemple de Modal</h1>
  <p>Cliquez sur le bouton pour ouvrir la modal.</p>

  <!-- La modal (normalement cachée avec display: none) -->
  <div class="modal-overlay">
    <div class="modal">
      <button class="modal-close">&times;</button>
      <h2>Titre de la Modal</h2>
      <p>Contenu de la modal avec un overlay fixed et une modal centrée.</p>
      <p>Le bouton de fermeture est en position absolute par rapport à la modal.</p>
    </div>
  </div>
</body>
</html>
```

---

### Exemple 2 : Layout complet avec navigation fixe

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Layout Complet</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      padding-top: 70px; /* Espace pour le header fixe */
    }

    /* Header fixe en haut */
    .header {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 60px;
      background: #2c3e50;
      color: white;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 30px;
      z-index: 1000;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .header nav a {
      color: white;
      text-decoration: none;
      margin-left: 20px;
    }

    /* Contenu principal */
    .content {
      max-width: 1200px;
      margin: 0 auto;
      padding: 30px;
    }

    /* Carte avec badge */
    .card {
      position: relative; /* Contexte pour le badge */
      background: white;
      border-radius: 10px;
      padding: 30px;
      margin-bottom: 30px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      min-height: 400px;
    }

    .badge {
      position: absolute;
      top: -10px;
      right: 20px;
      background: #e74c3c;
      color: white;
      padding: 8px 20px;
      border-radius: 20px;
      font-weight: bold;
    }

    /* Bouton retour en haut (fixed) */
    .back-to-top {
      position: fixed;
      bottom: 30px;
      right: 30px;
      width: 50px;
      height: 50px;
      background: #3498db;
      color: white;
      border: none;
      border-radius: 50%;
      font-size: 24px;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      z-index: 999;
    }

    .back-to-top:hover {
      background: #2980b9;
    }
  </style>
</head>
<body>
  <!-- Header fixe -->
  <header class="header">
    <div class="logo">Mon Site</div>
    <nav>
      <a href="#">Accueil</a>
      <a href="#">Services</a>
      <a href="#">Contact</a>
    </nav>
  </header>

  <!-- Contenu -->
  <main class="content">
    <div class="card">
      <div class="badge">NOUVEAU</div>
      <h2>Section 1</h2>
      <p>Le header reste fixe en haut.</p>
      <p>Le badge est en position absolute par rapport à la carte.</p>
    </div>

    <div class="card">
      <h2>Section 2</h2>
      <p>Scrollez pour voir le bouton "retour en haut" en bas à droite.</p>
    </div>

    <div class="card">
      <div class="badge">PROMO</div>
      <h2>Section 3</h2>
      <p>Chaque élément utilise le type de positionnement approprié.</p>
    </div>
  </main>

  <!-- Bouton retour en haut (fixe) -->
  <button class="back-to-top">↑</button>
</body>
</html>
```

---

## Points clés à retenir

✅ **`static`** : Comportement par défaut, rarement utilisé explicitement

✅ **`relative`** : Décale par rapport à la position d'origine, crée un contexte pour absolute

✅ **`absolute`** : Sort du flux, se positionne par rapport à l'ancêtre positionné

✅ **`fixed`** : Sort du flux, se positionne par rapport à la fenêtre, ne scroll pas

✅ **`sticky`** : Hybride relative/fixed, reste dans le flux puis devient collant

✅ **Contexte de positionnement** : `absolute` cherche le premier parent non-static

✅ **Propriétés de décalage** : `top`, `right`, `bottom`, `left` (sauf avec `static`)

---

## Erreurs courantes à éviter

❌ **Oublier `position: relative` sur le parent d'un absolute**
```css
/* ❌ L'absolute se positionne par rapport à <html> */
.card .badge {
  position: absolute;
  top: 10px;
  right: 10px;
}

/* ✅ Créer le contexte */
.card {
  position: relative;
}
```

❌ **Ne pas compenser un élément fixed**
```css
/* ❌ Le contenu passe sous le header */
.header {
  position: fixed;
  height: 60px;
}

/* ✅ Ajouter padding au body */
body {
  padding-top: 60px;
}
```

❌ **Confondre absolute et fixed**
```css
/* absolute scroll avec la page */
/* fixed reste visible en permanence */
```

❌ **Oublier z-index avec des éléments positionnés**
```css
/* Les éléments peuvent se chevaucher */
/* Utilisez z-index pour contrôler l'ordre */
.modal {
  z-index: 1000;
}
```

---

## Quand utiliser quel positionnement ?

### `relative` pour :
- ✅ Créer un contexte pour `absolute`
- ✅ Ajuster légèrement la position d'un élément
- ✅ Animations et transitions

### `absolute` pour :
- ✅ Badges, tags, labels
- ✅ Overlays et modales
- ✅ Tooltips
- ✅ Icons positionnés précisément
- ✅ Tout élément qui doit "flotter" par rapport à un parent

### `fixed` pour :
- ✅ Navigation qui reste visible
- ✅ Boutons flottants (retour en haut, chat)
- ✅ Barres de cookies
- ✅ Notifications persistantes

### `sticky` pour :
- ✅ Headers de tableaux
- ✅ En-têtes de section
- ✅ Sidebars qui collent en scrollant
- ✅ Call-to-action qui reste visible

---

## Conclusion

Le positionnement CSS est un outil **puissant** qui permet un contrôle précis de la disposition des éléments. Chaque type de positionnement a son utilité :

- **`static`** est le défaut et représente le flux normal
- **`relative`** ajuste légèrement et crée des contextes
- **`absolute`** permet un placement précis hors du flux
- **`fixed`** garde des éléments toujours visibles
- **`sticky`** combine le meilleur de relative et fixed

En comprenant ces différents types et en les combinant avec Flexbox et Grid, vous avez tous les outils pour créer **n'importe quelle interface** moderne !

Dans la prochaine leçon, nous verrons le **z-index** et les contextes d'empilement pour contrôler l'ordre de superposition des éléments positionnés.

---


⏭️ [Z-index et contextes d'empilement](/04-css3-styles-et-mise-en-page/04-positionnement-et-contexte/02-zindex-et-empilement.md)
