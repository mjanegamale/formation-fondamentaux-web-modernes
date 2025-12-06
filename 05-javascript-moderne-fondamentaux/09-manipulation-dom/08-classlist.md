🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.8 - Classes CSS : classList (add, remove, toggle, contains) 🆕

## Introduction

Dans la section précédente, vous avez appris à modifier les styles directement avec `element.style`. Maintenant, découvrez **l'approche moderne et recommandée** : manipuler les **classes CSS** avec l'objet **`classList`** !

Cette méthode est :
- ✅ Plus propre et maintenable
- ✅ Plus performante
- ✅ Meilleure pour séparer le style de la logique
- ✅ Plus facile à réutiliser

> **`classList`** est l'API moderne pour manipuler les classes CSS d'un élément. C'est la méthode préférée des développeurs professionnels !

---

## Rappel : Les classes CSS

### Qu'est-ce qu'une classe CSS ?

En HTML, vous pouvez ajouter une ou plusieurs classes à un élément avec l'attribut `class` :

```html
<div class="card">Une carte simple</div>
<div class="card highlight">Une carte en surbrillance</div>
<div class="card highlight active">Une carte active et en surbrillance</div>
```

En CSS, vous définissez les styles pour ces classes :

```css
.card {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
}

.highlight {
    background-color: yellow;
}

.active {
    border-color: blue;
    font-weight: bold;
}
```

### Pourquoi manipuler les classes en JavaScript ?

Changer les classes CSS permet de :
- 🎨 Modifier l'apparence sans toucher au CSS directement
- 🔄 Basculer entre différents états visuels
- 🎯 Appliquer plusieurs styles d'un coup
- ♻️ Réutiliser les mêmes styles partout

---

## L'objet classList

### Qu'est-ce que classList ?

Chaque élément du DOM possède une propriété **`classList`** qui donne accès à ses classes CSS sous forme d'objet avec des méthodes pratiques.

**Exemple :**
```html
<div id="box" class="card highlight">Contenu</div>
```

```javascript
let box = document.getElementById('box');
console.log(box.classList);
// DOMTokenList(2) ["card", "highlight"]
```

### Les méthodes de classList

`classList` offre 4 méthodes principales :

| Méthode | Action |
|---------|--------|
| `add()` | Ajoute une ou plusieurs classes |
| `remove()` | Supprime une ou plusieurs classes |
| `toggle()` | Bascule une classe (ajoute si absente, retire si présente) |
| `contains()` | Vérifie si une classe existe |

---

## 1. add() - Ajouter des classes

### Syntaxe

```javascript
element.classList.add('nom-classe');

// Ajouter plusieurs classes à la fois
element.classList.add('classe1', 'classe2', 'classe3');
```

### Exemples basiques

**HTML :**
```html
<div id="box">Contenu</div>
```

**JavaScript :**
```javascript
let box = document.getElementById('box');

// Ajouter une classe
box.classList.add('highlight');
// Résultat : <div id="box" class="highlight">

// Ajouter plusieurs classes
box.classList.add('card', 'shadow');
// Résultat : <div id="box" class="highlight card shadow">
```

### Si la classe existe déjà

Si vous ajoutez une classe qui existe déjà, **rien ne se passe** (pas d'erreur, pas de doublon) :

```javascript
box.classList.add('highlight');
box.classList.add('highlight');  // N'ajoute pas de doublon
// Résultat : <div class="highlight"> (une seule fois)
```

### Exemple pratique : Mise en surbrillance

**CSS :**
```css
.highlight {
    background-color: yellow;
    padding: 10px;
    border: 2px solid orange;
}
```

**HTML :**
```html
<p id="message">Ceci est un message important</p>
<button id="highlight-btn">Mettre en surbrillance</button>
```

**JavaScript :**
```javascript
let message = document.getElementById('message');
let btn = document.getElementById('highlight-btn');

btn.addEventListener('click', function() {
    message.classList.add('highlight');
});
```

---

## 2. remove() - Supprimer des classes

### Syntaxe

```javascript
element.classList.remove('nom-classe');

// Supprimer plusieurs classes à la fois
element.classList.remove('classe1', 'classe2', 'classe3');
```

### Exemples

```javascript
let box = document.getElementById('box');

// Supprimer une classe
box.classList.remove('highlight');

// Supprimer plusieurs classes
box.classList.remove('card', 'shadow');
```

### Si la classe n'existe pas

Si vous essayez de supprimer une classe qui n'existe pas, **rien ne se passe** (pas d'erreur) :

```javascript
box.classList.remove('inexistante');  // Pas d'erreur, juste ignoré
```

### Exemple pratique : Retirer la surbrillance

```javascript
let message = document.getElementById('message');
let removeBtn = document.getElementById('remove-btn');

removeBtn.addEventListener('click', function() {
    message.classList.remove('highlight');
});
```

---

## 3. toggle() - Basculer une classe 🌟

### Qu'est-ce que toggle ?

**`toggle()`** est probablement la méthode la plus utile ! Elle :
- **Ajoute** la classe si elle n'existe pas
- **Retire** la classe si elle existe déjà

C'est parfait pour les interactions on/off comme :
- Afficher/masquer un menu
- Activer/désactiver un bouton
- Ouvrir/fermer un panneau

### Syntaxe

```javascript
element.classList.toggle('nom-classe');
```

### Exemple simple

```javascript
let box = document.getElementById('box');

// Premier appel : ajoute 'highlight'
box.classList.toggle('highlight');

// Deuxième appel : retire 'highlight'
box.classList.toggle('highlight');

// Troisième appel : ajoute 'highlight'
box.classList.toggle('highlight');
```

### Exemple pratique : Bouton on/off

**CSS :**
```css
.highlight {
    background-color: yellow;
    font-weight: bold;
}
```

**HTML :**
```html
<p id="message">Cliquez sur le bouton</p>
<button id="toggle-btn">Basculer la surbrillance</button>
```

**JavaScript :**
```javascript
let message = document.getElementById('message');
let toggleBtn = document.getElementById('toggle-btn');

toggleBtn.addEventListener('click', function() {
    // Bascule automatiquement la classe
    message.classList.toggle('highlight');
});
```

**Résultat :**
- Premier clic → Ajoute `highlight`
- Deuxième clic → Retire `highlight`
- Troisième clic → Ajoute `highlight`
- Et ainsi de suite...

### toggle() avec condition (avancé)

Vous pouvez aussi forcer l'ajout ou le retrait avec un deuxième paramètre booléen :

```javascript
// Force l'ajout (comme add)
element.classList.toggle('active', true);

// Force le retrait (comme remove)
element.classList.toggle('active', false);

// Exemple pratique
let isActive = someCondition;
element.classList.toggle('active', isActive);
```

### Exemple : Menu déroulant

**CSS :**
```css
.dropdown-content {
    display: none;
    background-color: #f9f9f9;
    padding: 10px;
}

.dropdown-content.show {
    display: block;
}
```

**HTML :**
```html
<button id="menu-btn">Menu</button>
<div id="dropdown" class="dropdown-content">
    <a href="#">Option 1</a>
    <a href="#">Option 2</a>
    <a href="#">Option 3</a>
</div>
```

**JavaScript :**
```javascript
let menuBtn = document.getElementById('menu-btn');
let dropdown = document.getElementById('dropdown');

menuBtn.addEventListener('click', function() {
    dropdown.classList.toggle('show');
});
```

---

## 4. contains() - Vérifier si une classe existe

### Syntaxe

```javascript
element.classList.contains('nom-classe');  // Retourne true ou false
```

### Exemples

```javascript
let box = document.getElementById('box');

// Vérifier si une classe existe
if (box.classList.contains('highlight')) {
    console.log('La boîte est en surbrillance');
} else {
    console.log('La boîte n\'est pas en surbrillance');
}
```

### Exemple pratique : Afficher l'état

```html
<div id="box" class="card">Contenu</div>
<button id="check-btn">Vérifier l'état</button>
<p id="status"></p>
```

```javascript
let box = document.getElementById('box');
let checkBtn = document.getElementById('check-btn');
let status = document.getElementById('status');

checkBtn.addEventListener('click', function() {
    if (box.classList.contains('highlight')) {
        status.textContent = '✅ La boîte est en surbrillance';
    } else {
        status.textContent = '❌ La boîte n\'est pas en surbrillance';
    }
});
```

### Exemple : Logique conditionnelle

```javascript
let button = document.getElementById('btn');

button.addEventListener('click', function() {
    if (this.classList.contains('active')) {
        // Si le bouton est actif, le désactiver
        this.classList.remove('active');
        this.textContent = 'Activer';
    } else {
        // Si le bouton est inactif, l'activer
        this.classList.add('active');
        this.textContent = 'Désactiver';
    }
});
```

---

## Propriétés supplémentaires de classList

### length - Nombre de classes

```javascript
let box = document.getElementById('box');
console.log(box.classList.length);  // Nombre de classes

// Exemple
// <div class="card highlight shadow">
console.log(box.classList.length);  // 3
```

### value - Toutes les classes en chaîne

```javascript
let box = document.getElementById('box');
console.log(box.classList.value);  // "card highlight shadow"

// Équivalent à
console.log(box.className);  // "card highlight shadow"
```

### Accès par index

```javascript
let box = document.getElementById('box');
// <div class="card highlight shadow">

console.log(box.classList[0]);  // "card"
console.log(box.classList[1]);  // "highlight"
console.log(box.classList[2]);  // "shadow"
```

### item() - Obtenir une classe par index

```javascript
let box = document.getElementById('box');

console.log(box.classList.item(0));  // "card"
console.log(box.classList.item(1));  // "highlight"
```

---

## classList vs className

### L'ancienne méthode : className

Avant `classList`, on utilisait la propriété **`className`** :

```javascript
// Ancienne méthode avec className
element.className = 'card highlight';  // Remplace toutes les classes

// Ajouter une classe (compliqué)
element.className += ' active';  // Attention à l'espace !

// Vérifier une classe (compliqué)
if (element.className.indexOf('active') !== -1) {
    // ...
}
```

**Problèmes avec className :**
- ❌ Remplace toutes les classes
- ❌ Manipulation de chaînes complexe
- ❌ Risque d'oublier l'espace
- ❌ Création de doublons possible

### La méthode moderne : classList

```javascript
// Méthode moderne avec classList
element.classList.add('card', 'highlight');  // ✅ Simple

// Ajouter une classe
element.classList.add('active');  // ✅ Facile

// Vérifier une classe
if (element.classList.contains('active')) {  // ✅ Clair
    // ...
}
```

**Avantages de classList :**
- ✅ API claire et intuitive
- ✅ Pas de manipulation de chaînes
- ✅ Pas de doublons possibles
- ✅ Plus sûr et plus performant

### Comparaison côte à côte

| Action | className (ancien) | classList (moderne) |
|--------|-------------------|---------------------|
| **Ajouter** | `el.className += ' active'` | `el.classList.add('active')` ✅ |
| **Supprimer** | Manipulation complexe | `el.classList.remove('active')` ✅ |
| **Basculer** | Logique manuelle | `el.classList.toggle('active')` ✅ |
| **Vérifier** | `el.className.indexOf('x') > -1` | `el.classList.contains('x')` ✅ |

**Recommandation :** Utilisez toujours **`classList`** au lieu de `className` !

---

## Exemples pratiques complets

### Exemple 1 : Système d'onglets

**CSS :**
```css
.tab {
    padding: 10px 20px;
    background-color: #ddd;
    cursor: pointer;
    display: inline-block;
    margin-right: 5px;
}

.tab.active {
    background-color: #4CAF50;
    color: white;
}

.tab-content {
    display: none;
    padding: 20px;
    border: 1px solid #ddd;
}

.tab-content.active {
    display: block;
}
```

**HTML :**
```html
<div class="tabs">
    <div class="tab active" data-tab="home">Accueil</div>
    <div class="tab" data-tab="about">À propos</div>
    <div class="tab" data-tab="contact">Contact</div>
</div>

<div id="home" class="tab-content active">
    <h2>Accueil</h2>
    <p>Contenu de l'accueil</p>
</div>

<div id="about" class="tab-content">
    <h2>À propos</h2>
    <p>Contenu à propos</p>
</div>

<div id="contact" class="tab-content">
    <h2>Contact</h2>
    <p>Contenu contact</p>
</div>
```

**JavaScript :**
```javascript
let tabs = document.querySelectorAll('.tab');
let contents = document.querySelectorAll('.tab-content');

tabs.forEach(tab => {
    tab.addEventListener('click', function() {
        // Retirer 'active' de tous les onglets
        tabs.forEach(t => t.classList.remove('active'));

        // Ajouter 'active' à l'onglet cliqué
        this.classList.add('active');

        // Masquer tous les contenus
        contents.forEach(content => content.classList.remove('active'));

        // Afficher le contenu correspondant
        let targetId = this.dataset.tab;
        let targetContent = document.getElementById(targetId);
        targetContent.classList.add('active');
    });
});
```

### Exemple 2 : Mode sombre/clair

**CSS :**
```css
body {
    transition: background-color 0.3s, color 0.3s;
}

body.dark-mode {
    background-color: #1a1a1a;
    color: #ffffff;
}

.toggle-btn {
    padding: 10px 20px;
    cursor: pointer;
}

body.dark-mode .toggle-btn {
    background-color: #333;
    color: #fff;
}
```

**HTML :**
```html
<button id="theme-toggle">🌙 Mode sombre</button>
<h1>Mon site web</h1>
<p>Cliquez sur le bouton pour changer le thème</p>
```

**JavaScript :**
```javascript
let toggleBtn = document.getElementById('theme-toggle');
let body = document.body;

toggleBtn.addEventListener('click', function() {
    // Basculer le mode sombre
    body.classList.toggle('dark-mode');

    // Changer le texte du bouton
    if (body.classList.contains('dark-mode')) {
        this.textContent = '☀️ Mode clair';
    } else {
        this.textContent = '🌙 Mode sombre';
    }
});
```

### Exemple 3 : Accordéon

**CSS :**
```css
.accordion-item {
    border: 1px solid #ddd;
    margin-bottom: 5px;
}

.accordion-header {
    padding: 15px;
    background-color: #f1f1f1;
    cursor: pointer;
    user-select: none;
}

.accordion-header:hover {
    background-color: #e1e1e1;
}

.accordion-content {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
    padding: 0 15px;
}

.accordion-item.active .accordion-content {
    max-height: 200px;
    padding: 15px;
}

.accordion-header::after {
    content: '+';
    float: right;
    font-size: 20px;
}

.accordion-item.active .accordion-header::after {
    content: '-';
}
```

**HTML :**
```html
<div class="accordion">
    <div class="accordion-item">
        <div class="accordion-header">Section 1</div>
        <div class="accordion-content">
            <p>Contenu de la section 1</p>
        </div>
    </div>

    <div class="accordion-item">
        <div class="accordion-header">Section 2</div>
        <div class="accordion-content">
            <p>Contenu de la section 2</p>
        </div>
    </div>

    <div class="accordion-item">
        <div class="accordion-header">Section 3</div>
        <div class="accordion-content">
            <p>Contenu de la section 3</p>
        </div>
    </div>
</div>
```

**JavaScript :**
```javascript
let headers = document.querySelectorAll('.accordion-header');

headers.forEach(header => {
    header.addEventListener('click', function() {
        let item = this.parentElement;

        // Basculer la classe active
        item.classList.toggle('active');

        // Option : Fermer les autres (un seul ouvert à la fois)
        // let allItems = document.querySelectorAll('.accordion-item');
        // allItems.forEach(otherItem => {
        //     if (otherItem !== item) {
        //         otherItem.classList.remove('active');
        //     }
        // });
    });
});
```

### Exemple 4 : Liste de tâches avec états

**CSS :**
```css
.task {
    padding: 10px;
    margin: 5px 0;
    background-color: #f9f9f9;
    border-left: 4px solid #ddd;
    cursor: pointer;
}

.task.completed {
    text-decoration: line-through;
    opacity: 0.6;
    border-left-color: #4CAF50;
}

.task.important {
    background-color: #fff3cd;
    border-left-color: #ff9800;
    font-weight: bold;
}

.task.completed.important {
    background-color: #e8f5e9;
}
```

**HTML :**
```html
<div id="tasks">
    <div class="task">Faire les courses</div>
    <div class="task important">Appeler le médecin</div>
    <div class="task">Lire un livre</div>
    <div class="task completed">Faire du sport</div>
</div>
<button id="mark-important">Marquer comme important</button>
```

**JavaScript :**
```javascript
let tasks = document.querySelectorAll('.task');

tasks.forEach(task => {
    // Clic pour marquer comme complété
    task.addEventListener('click', function() {
        this.classList.toggle('completed');
    });

    // Double-clic pour marquer comme important
    task.addEventListener('dblclick', function() {
        this.classList.toggle('important');
    });
});
```

---

## Combiner classList avec d'autres méthodes

### Avec les boucles

```javascript
// Ajouter une classe à tous les paragraphes
let paragraphes = document.querySelectorAll('p');
paragraphes.forEach(p => {
    p.classList.add('styled');
});

// Basculer une classe sur plusieurs éléments
let items = document.querySelectorAll('.item');
items.forEach(item => {
    item.classList.toggle('active');
});
```

### Avec les conditions

```javascript
let element = document.getElementById('box');

// Ajouter une classe selon une condition
if (score > 100) {
    element.classList.add('gold');
} else if (score > 50) {
    element.classList.add('silver');
} else {
    element.classList.add('bronze');
}

// Ou de manière plus concise
element.classList.add(score > 100 ? 'gold' : score > 50 ? 'silver' : 'bronze');
```

### Avec les événements

```javascript
let button = document.getElementById('btn');

// Ajouter une classe au survol
button.addEventListener('mouseenter', function() {
    this.classList.add('hover-effect');
});

button.addEventListener('mouseleave', function() {
    this.classList.remove('hover-effect');
});

// Au focus (pour l'accessibilité)
let input = document.getElementById('email');

input.addEventListener('focus', function() {
    this.classList.add('focused');
});

input.addEventListener('blur', function() {
    this.classList.remove('focused');
});
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Utiliser classList (méthode moderne)
element.classList.add('active');  // ✅

// Chaîner les méthodes n'est pas possible, mais vous pouvez faire :
element.classList.add('class1');
element.classList.add('class2');
// Ou en une fois :
element.classList.add('class1', 'class2');  // ✅

// Utiliser toggle pour les états on/off
element.classList.toggle('active');  // ✅ Simple

// Vérifier avant d'agir (si nécessaire)
if (element.classList.contains('hidden')) {
    element.classList.remove('hidden');
}

// Nommer les classes de manière descriptive
element.classList.add('is-active');  // ✅ Clair
element.classList.add('has-error');  // ✅ Descriptif
```

### ❌ À éviter

```javascript
// Ne pas utiliser className pour ajouter/retirer des classes
element.className += ' active';  // ❌ Ancien, fragile
element.classList.add('active');  // ✅ Mieux

// Ne pas mélanger les deux approches
element.className = 'card';
element.classList.add('active');  // ⚠️ Peut créer de la confusion

// Ne pas oublier les guillemets
element.classList.add(active);  // ❌ Erreur
element.classList.add('active');  // ✅ Correct

// Ne pas utiliser toggle avec une logique if/else redondante
if (element.classList.contains('active')) {  // ❌ Inutile
    element.classList.remove('active');
} else {
    element.classList.add('active');
}
element.classList.toggle('active');  // ✅ Équivalent et plus simple
```

---

## Avantages de classList sur les styles inline

### Comparaison

**Avec styles inline (moins bien) :**
```javascript
// ❌ Modifier plusieurs propriétés de style
element.style.backgroundColor = 'yellow';
element.style.padding = '10px';
element.style.border = '2px solid orange';
element.style.borderRadius = '5px';
```

**Avec classList (mieux) :**
```css
.highlight {
    background-color: yellow;
    padding: 10px;
    border: 2px solid orange;
    border-radius: 5px;
}
```
```javascript
// ✅ Une seule ligne
element.classList.add('highlight');
```

### Pourquoi classList est meilleur

1. **Séparation des préoccupations**
   - CSS = Apparence
   - JavaScript = Logique et comportement

2. **Réutilisabilité**
   - La même classe peut être appliquée à plusieurs éléments

3. **Maintenabilité**
   - Changer le style : modifier le CSS, pas le JavaScript

4. **Performance**
   - Les classes sont optimisées par le navigateur

5. **Transitions et animations CSS**
   - Fonctionnent automatiquement avec les classes

6. **Code plus propre**
   - Moins de code JavaScript

---

## Gestion d'états avec classList

Les classes CSS sont parfaites pour gérer les **états** de vos éléments :

```javascript
// États d'un bouton
button.classList.add('loading');     // En chargement
button.classList.add('success');     // Succès
button.classList.add('error');       // Erreur
button.classList.add('disabled');    // Désactivé

// États d'un formulaire
form.classList.add('invalid');       // Invalide
form.classList.add('pristine');      // Pas encore modifié
form.classList.add('dirty');         // Modifié
form.classList.add('submitted');     // Soumis

// États d'un menu
menu.classList.add('open');          // Ouvert
menu.classList.add('closed');        // Fermé
menu.classList.add('minimized');     // Minimisé

// États visuels
element.classList.add('active');     // Actif
element.classList.add('selected');   // Sélectionné
element.classList.add('highlighted'); // En surbrillance
element.classList.add('hidden');     // Caché
element.classList.add('visible');    // Visible
```

---

## Points clés à retenir

✅ **`classList`** est l'API moderne pour manipuler les classes CSS

✅ **`add()`** ajoute une ou plusieurs classes (pas de doublons)

✅ **`remove()`** supprime une ou plusieurs classes

✅ **`toggle()`** bascule une classe (ajoute si absente, retire si présente)

✅ **`contains()`** vérifie si une classe existe (retourne true/false)

✅ **Préférez classList à className** (plus moderne, plus sûr)

✅ **Utilisez les classes plutôt que les styles inline** pour la plupart des cas

✅ Les classes permettent de **séparer la présentation de la logique**

✅ Parfait pour gérer les **états** et les **interactions**

✅ Compatible avec les **transitions et animations CSS**

---

## Tableau récapitulatif

| Méthode | Syntaxe | Utilisation |
|---------|---------|-------------|
| **add()** | `classList.add('classe')` | Ajouter une/des classe(s) |
| **remove()** | `classList.remove('classe')` | Supprimer une/des classe(s) |
| **toggle()** | `classList.toggle('classe')` | Basculer une classe |
| **contains()** | `classList.contains('classe')` | Vérifier si classe existe |
| **length** | `classList.length` | Nombre de classes |
| **item()** | `classList.item(index)` | Obtenir classe par index |

---

## Ce qui vient ensuite

Vous savez maintenant :
1. ✅ Sélectionner des éléments
2. ✅ Modifier leur contenu
3. ✅ Modifier leurs attributs
4. ✅ Modifier leurs styles
5. ✅ Manipuler leurs classes CSS

La prochaine étape : apprendre à **créer de nouveaux éléments** et à les ajouter dynamiquement au DOM !

---

## Ressources supplémentaires

- 📖 [MDN - Element.classList](https://developer.mozilla.org/fr/docs/Web/API/Element/classList)
- 📖 [MDN - DOMTokenList](https://developer.mozilla.org/fr/docs/Web/API/DOMTokenList)
- 💡 [Can I Use - classList](https://caniuse.com/classlist) (Compatibilité navigateurs)

---


⏭️ [Création d'éléments : createElement, createTextNode](/05-javascript-moderne-fondamentaux/09-manipulation-dom/09-creation-elements.md)
