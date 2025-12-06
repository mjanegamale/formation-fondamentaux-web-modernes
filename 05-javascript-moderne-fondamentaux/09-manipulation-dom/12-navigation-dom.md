🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.12 - Navigation dans le DOM : parentElement, children, nextElementSibling

## Introduction

Vous savez maintenant sélectionner, modifier, créer, insérer et supprimer des éléments. La dernière compétence essentielle : **naviguer** dans le DOM pour accéder aux éléments **relatifs** à un élément donné !

Naviguer dans le DOM signifie se déplacer de parent en enfant, de frère en frère, comme dans un arbre généalogique :
- 👨 Remonter vers le **parent**
- 👶 Descendre vers les **enfants**
- 👫 Se déplacer entre **frères et sœurs**

> **Pourquoi c'est important ?** Souvent, vous avez une référence à un élément et vous devez accéder à ses voisins sans connaître leurs ID ou classes.

---

## L'arbre DOM : Rappel de la structure

Le DOM est organisé comme un **arbre généalogique** :

```
html (racine)
  ├── head
  │    └── title
  │         └── "Mon site"
  └── body
       ├── header
       │    ├── h1
       │    │    └── "Bienvenue"
       │    └── nav
       ├── main
       │    ├── article
       │    │    ├── h2
       │    │    └── p
       │    └── aside
       └── footer
```

Chaque élément a des **relations** avec les autres :
- **Parent** : L'élément qui le contient
- **Enfants** : Les éléments qu'il contient
- **Frères/Sœurs (siblings)** : Les éléments au même niveau

---

## Vocabulaire des relations DOM

**Exemple HTML :**
```html
<div id="container">
    <h2 id="title">Titre</h2>
    <p id="para1">Premier paragraphe</p>
    <p id="para2">Deuxième paragraphe</p>
</div>
```

**Relations :**
- `<div>` est le **parent** de `<h2>` et des deux `<p>`
- `<h2>` et les deux `<p>` sont les **enfants** de `<div>`
- `<h2>` et `<p id="para1">` sont des **frères** (siblings)
- `<p id="para1">` et `<p id="para2">` sont des **frères**
- `<h2>` est le **premier enfant** de `<div>`
- `<p id="para2">` est le **dernier enfant** de `<div>`

---

## 1. Accéder au parent

### parentElement - Le parent (élément)

**`parentElement`** retourne l'élément **parent** direct.

**Syntaxe :**
```javascript
let parent = element.parentElement;
```

**Exemple :**
```html
<div id="container">
    <p id="para">Mon paragraphe</p>
</div>
```

```javascript
let para = document.getElementById('para');
let parent = para.parentElement;

console.log(parent);  // <div id="container">...</div>
console.log(parent.id);  // "container"
```

### Remonter plusieurs niveaux

Vous pouvez chaîner `.parentElement` :

```html
<body>
    <div id="wrapper">
        <div id="container">
            <p id="para">Texte</p>
        </div>
    </div>
</body>
```

```javascript
let para = document.getElementById('para');

let container = para.parentElement;
console.log(container.id);  // "container"

let wrapper = para.parentElement.parentElement;
console.log(wrapper.id);  // "wrapper"

let body = para.parentElement.parentElement.parentElement;
console.log(body.tagName);  // "BODY"
```

### parentNode vs parentElement

Il existe aussi **`parentNode`**, une propriété plus ancienne :

```javascript
let parent1 = element.parentElement;  // Retourne un Element
let parent2 = element.parentNode;     // Retourne un Node
```

**Différence :**
- `parentElement` : Retourne uniquement des **éléments HTML** (ou null)
- `parentNode` : Retourne tout type de **nœud** (éléments, texte, commentaires...)

**Recommandation :** Utilisez **`parentElement`** (plus clair et moderne).

### closest() - Trouver l'ancêtre le plus proche

**`closest()`** remonte dans le DOM jusqu'à trouver un élément qui correspond au sélecteur.

**Syntaxe :**
```javascript
let ancetre = element.closest('selecteur-css');
```

**Exemple :**
```html
<div class="card">
    <div class="card-body">
        <p id="text">
            <span id="highlight">Texte en surbrillance</span>
        </p>
    </div>
</div>
```

```javascript
let span = document.getElementById('highlight');

// Trouver la carte parente
let card = span.closest('.card');
console.log(card);  // <div class="card">...</div>

// Trouver le paragraphe parent
let para = span.closest('p');
console.log(para.id);  // "text"
```

**Utilité :** Très pratique pour les événements délégués !

**Exemple pratique :**
```html
<div class="product-card" data-id="123">
    <h3>Produit</h3>
    <p>Description</p>
    <button class="btn-buy">Acheter</button>
</div>
```

```javascript
document.addEventListener('click', function(e) {
    if (e.target.classList.contains('btn-buy')) {
        // Trouver la carte parente
        let card = e.target.closest('.product-card');
        let productId = card.dataset.id;
        console.log(`Acheter le produit ${productId}`);
    }
});
```

### Si le parent n'existe pas

Si un élément n'a pas de parent (cas rare), `parentElement` retourne **`null`** :

```javascript
let html = document.documentElement;
console.log(html.parentElement);  // null (html n'a pas de parent élément)
```

---

## 2. Accéder aux enfants

### children - Tous les enfants

**`children`** retourne une **HTMLCollection** de tous les éléments enfants.

**Syntaxe :**
```javascript
let enfants = element.children;
```

**Exemple :**
```html
<ul id="liste">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

```javascript
let liste = document.getElementById('liste');
let enfants = liste.children;

console.log(enfants);  // HTMLCollection(3) [li, li, li]
console.log(enfants.length);  // 3

// Accéder à un enfant spécifique
console.log(enfants[0]);  // <li>Item 1</li>
console.log(enfants[1]);  // <li>Item 2</li>
```

### Parcourir les enfants

```javascript
let liste = document.getElementById('liste');

// Méthode 1 : Boucle for
for (let i = 0; i < liste.children.length; i++) {
    console.log(liste.children[i].textContent);
}

// Méthode 2 : for...of
for (let enfant of liste.children) {
    console.log(enfant.textContent);
}

// Méthode 3 : forEach (après conversion)
Array.from(liste.children).forEach(enfant => {
    console.log(enfant.textContent);
});
```

### firstElementChild - Premier enfant

**`firstElementChild`** retourne le **premier enfant** élément.

```html
<div id="container">
    <h2>Titre</h2>
    <p>Paragraphe 1</p>
    <p>Paragraphe 2</p>
</div>
```

```javascript
let container = document.getElementById('container');
let premier = container.firstElementChild;

console.log(premier);  // <h2>Titre</h2>
console.log(premier.tagName);  // "H2"
```

### lastElementChild - Dernier enfant

**`lastElementChild`** retourne le **dernier enfant** élément.

```javascript
let container = document.getElementById('container');
let dernier = container.lastElementChild;

console.log(dernier);  // <p>Paragraphe 2</p>
```

### childElementCount - Nombre d'enfants

```javascript
let container = document.getElementById('container');
console.log(container.childElementCount);  // 3
```

### Vérifier si un élément a des enfants

```javascript
let container = document.getElementById('container');

if (container.children.length > 0) {
    console.log('Le container a des enfants');
} else {
    console.log('Le container est vide');
}

// Ou avec childElementCount
if (container.childElementCount > 0) {
    console.log('Le container a des enfants');
}
```

### childNodes vs children

**`childNodes`** retourne **tous les nœuds** enfants (éléments, texte, commentaires) :

```html
<div id="container">
    Texte avant
    <p>Paragraphe</p>
    Texte après
</div>
```

```javascript
let container = document.getElementById('container');

console.log(container.childNodes);
// NodeList(5) [text, p, text, ...]
// Inclut les nœuds de texte !

console.log(container.children);
// HTMLCollection(1) [p]
// Seulement les éléments HTML
```

**Recommandation :** Utilisez **`children`** (ignore les nœuds de texte).

---

## 3. Accéder aux frères et sœurs

### nextElementSibling - Frère suivant

**`nextElementSibling`** retourne l'élément **frère suivant** (au même niveau).

**Syntaxe :**
```javascript
let suivant = element.nextElementSibling;
```

**Exemple :**
```html
<div id="container">
    <p id="para1">Premier</p>
    <p id="para2">Deuxième</p>
    <p id="para3">Troisième</p>
</div>
```

```javascript
let para1 = document.getElementById('para1');
let suivant = para1.nextElementSibling;

console.log(suivant);  // <p id="para2">Deuxième</p>
console.log(suivant.id);  // "para2"
```

### Chaîner pour avancer plusieurs fois

```javascript
let para1 = document.getElementById('para1');

// Avancer de deux
let para3 = para1.nextElementSibling.nextElementSibling;
console.log(para3.id);  // "para3"
```

### S'il n'y a pas de frère suivant

Si l'élément est le dernier, `nextElementSibling` retourne **`null`** :

```javascript
let para3 = document.getElementById('para3');
console.log(para3.nextElementSibling);  // null
```

### previousElementSibling - Frère précédent

**`previousElementSibling`** retourne l'élément **frère précédent**.

```javascript
let para3 = document.getElementById('para3');
let precedent = para3.previousElementSibling;

console.log(precedent);  // <p id="para2">Deuxième</p>
console.log(precedent.id);  // "para2"
```

### Naviguer entre frères

```javascript
let para2 = document.getElementById('para2');

let avant = para2.previousElementSibling;
let apres = para2.nextElementSibling;

console.log(avant.id);   // "para1"
console.log(apres.id);   // "para3"
```

### nextSibling vs nextElementSibling

**`nextSibling`** inclut les nœuds de texte (espaces, sauts de ligne) :

```html
<div>
    <p id="para1">Premier</p>
    <p id="para2">Deuxième</p>
</div>
```

```javascript
let para1 = document.getElementById('para1');

console.log(para1.nextSibling);
// #text (le saut de ligne entre les <p>)

console.log(para1.nextElementSibling);
// <p id="para2">Deuxième</p>
```

**Recommandation :** Utilisez **`nextElementSibling`** (ignore les nœuds de texte).

---

## Tableau récapitulatif des propriétés

| Propriété | Retourne | Description |
|-----------|----------|-------------|
| **parentElement** | Element ou null | Parent direct |
| **children** | HTMLCollection | Tous les enfants éléments |
| **firstElementChild** | Element ou null | Premier enfant élément |
| **lastElementChild** | Element ou null | Dernier enfant élément |
| **childElementCount** | Number | Nombre d'enfants éléments |
| **nextElementSibling** | Element ou null | Frère suivant |
| **previousElementSibling** | Element ou null | Frère précédent |
| **closest(selector)** | Element ou null | Ancêtre correspondant au sélecteur |

---

## Exemples pratiques complets

### Exemple 1 : Système d'onglets

```html
<div class="tabs">
    <button class="tab-btn active">Onglet 1</button>
    <button class="tab-btn">Onglet 2</button>
    <button class="tab-btn">Onglet 3</button>
</div>

<div class="tab-content active">Contenu 1</div>
<div class="tab-content">Contenu 2</div>
<div class="tab-content">Contenu 3</div>
```

```javascript
let tabButtons = document.querySelectorAll('.tab-btn');

tabButtons.forEach((button, index) => {
    button.addEventListener('click', function() {
        // Retirer 'active' de tous les boutons
        tabButtons.forEach(btn => btn.classList.remove('active'));

        // Ajouter 'active' au bouton cliqué
        this.classList.add('active');

        // Trouver le container parent
        let tabsContainer = this.parentElement;

        // Trouver les contenus (frères du container)
        let contentsContainer = tabsContainer.nextElementSibling;

        // Cacher tous les contenus
        let allContents = document.querySelectorAll('.tab-content');
        allContents.forEach(content => content.classList.remove('active'));

        // Afficher le contenu correspondant
        allContents[index].classList.add('active');
    });
});
```

### Exemple 2 : Accordéon

```html
<div class="accordion">
    <div class="accordion-item">
        <div class="accordion-header">Section 1</div>
        <div class="accordion-content">Contenu 1</div>
    </div>
    <div class="accordion-item">
        <div class="accordion-header">Section 2</div>
        <div class="accordion-content">Contenu 2</div>
    </div>
    <div class="accordion-item">
        <div class="accordion-header">Section 3</div>
        <div class="accordion-content">Contenu 3</div>
    </div>
</div>
```

```javascript
let headers = document.querySelectorAll('.accordion-header');

headers.forEach(header => {
    header.addEventListener('click', function() {
        // Trouver l'item parent
        let item = this.parentElement;

        // Trouver le contenu (frère suivant)
        let content = this.nextElementSibling;

        // Basculer l'affichage
        item.classList.toggle('active');

        if (item.classList.contains('active')) {
            content.style.maxHeight = content.scrollHeight + 'px';
        } else {
            content.style.maxHeight = '0';
        }
    });
});
```

### Exemple 3 : Navigation entre images

```html
<div class="gallery">
    <button id="prev">◄ Précédent</button>
    <div class="images">
        <img src="image1.jpg" class="active">
        <img src="image2.jpg">
        <img src="image3.jpg">
        <img src="image4.jpg">
    </div>
    <button id="next">Suivant ►</button>
</div>
```

```javascript
let prevBtn = document.getElementById('prev');
let nextBtn = document.getElementById('next');

prevBtn.addEventListener('click', function() {
    let currentImage = document.querySelector('.images img.active');
    let prevImage = currentImage.previousElementSibling;

    if (prevImage) {
        currentImage.classList.remove('active');
        prevImage.classList.add('active');
    }
});

nextBtn.addEventListener('click', function() {
    let currentImage = document.querySelector('.images img.active');
    let nextImage = currentImage.nextElementSibling;

    if (nextImage) {
        currentImage.classList.remove('active');
        nextImage.classList.add('active');
    }
});
```

### Exemple 4 : Liste de tâches avec réorganisation

```html
<ul id="tasks">
    <li>
        <span>Tâche 1</span>
        <button class="btn-up">↑</button>
        <button class="btn-down">↓</button>
        <button class="btn-delete">✕</button>
    </li>
    <li>
        <span>Tâche 2</span>
        <button class="btn-up">↑</button>
        <button class="btn-down">↓</button>
        <button class="btn-delete">✕</button>
    </li>
    <li>
        <span>Tâche 3</span>
        <button class="btn-up">↑</button>
        <button class="btn-down">↓</button>
        <button class="btn-delete">✕</button>
    </li>
</ul>
```

```javascript
let tasksList = document.getElementById('tasks');

// Délégation d'événements
tasksList.addEventListener('click', function(e) {
    let button = e.target;
    let li = button.closest('li');

    if (button.classList.contains('btn-up')) {
        // Monter la tâche
        let prev = li.previousElementSibling;
        if (prev) {
            tasksList.insertBefore(li, prev);
        }
    }

    else if (button.classList.contains('btn-down')) {
        // Descendre la tâche
        let next = li.nextElementSibling;
        if (next) {
            tasksList.insertBefore(next, li);
        }
    }

    else if (button.classList.contains('btn-delete')) {
        // Supprimer la tâche
        li.remove();
    }
});
```

### Exemple 5 : Fil d'Ariane (Breadcrumb)

```html
<div class="container">
    <div class="section">
        <div class="subsection">
            <div class="item" id="current-item">
                Item actuel
            </div>
        </div>
    </div>
</div>
```

```javascript
function creerFilAriane(element) {
    let chemin = [];
    let current = element;

    // Remonter jusqu'à la racine
    while (current && current !== document.body) {
        let nom = current.className || current.tagName.toLowerCase();
        chemin.unshift(nom);  // Ajouter au début
        current = current.parentElement;
    }

    return chemin.join(' > ');
}

let item = document.getElementById('current-item');
let breadcrumb = creerFilAriane(item);
console.log(breadcrumb);
// "container > section > subsection > item"
```

---

## Navigation complexe

### Trouver tous les ancêtres

```javascript
function obtenirAncetres(element) {
    let ancetres = [];
    let current = element.parentElement;

    while (current) {
        ancetres.push(current);
        current = current.parentElement;
    }

    return ancetres;
}

let element = document.getElementById('mon-element');
let ancetres = obtenirAncetres(element);
console.log(ancetres);
```

### Trouver tous les descendants

```javascript
function obtenirDescendants(element) {
    let descendants = [];

    function parcourir(elem) {
        for (let enfant of elem.children) {
            descendants.push(enfant);
            parcourir(enfant);  // Récursif
        }
    }

    parcourir(element);
    return descendants;
}

let container = document.getElementById('container');
let descendants = obtenirDescendants(container);
console.log(descendants);
```

### Compter les niveaux de profondeur

```javascript
function obtenirProfondeur(element) {
    let profondeur = 0;
    let current = element;

    while (current.parentElement) {
        profondeur++;
        current = current.parentElement;
    }

    return profondeur;
}

let element = document.getElementById('mon-element');
console.log(`Profondeur : ${obtenirProfondeur(element)}`);
```

---

## Combiner navigation et manipulation

### Exemple : Colorier les éléments liés

```javascript
let element = document.getElementById('target');

// Colorier le parent
element.parentElement.style.backgroundColor = 'lightblue';

// Colorier tous les enfants
for (let enfant of element.children) {
    enfant.style.backgroundColor = 'lightgreen';
}

// Colorier le frère suivant
if (element.nextElementSibling) {
    element.nextElementSibling.style.backgroundColor = 'lightyellow';
}

// Colorier le frère précédent
if (element.previousElementSibling) {
    element.previousElementSibling.style.backgroundColor = 'lightcoral';
}
```

### Exemple : Numéroter automatiquement

```javascript
let container = document.getElementById('articles');

// Numéroter tous les articles
Array.from(container.children).forEach((article, index) => {
    let numero = document.createElement('span');
    numero.textContent = `#${index + 1}`;
    numero.classList.add('numero');
    article.insertBefore(numero, article.firstElementChild);
});
```

---

## Vérifications et sécurité

### Toujours vérifier l'existence

```javascript
let element = document.getElementById('mon-element');

// ✅ Vérifier avant d'accéder au parent
if (element && element.parentElement) {
    console.log(element.parentElement);
}

// ✅ Vérifier le frère suivant
let suivant = element.nextElementSibling;
if (suivant) {
    suivant.style.color = 'red';
}

// ✅ Vérifier s'il y a des enfants
if (element.children.length > 0) {
    console.log('Il y a des enfants');
}
```

### Éviter les boucles infinies

```javascript
// ❌ Risque de boucle infinie si mal codé
let current = element;
while (current) {
    console.log(current);
    current = current.parentElement;  // ✅ Finira par être null
}

// ✅ Ajouter une condition de sortie
let current = element;
let compteur = 0;
while (current && compteur < 100) {
    console.log(current);
    current = current.parentElement;
    compteur++;
}
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Utiliser les propriétés Element (modernes)
element.parentElement  // ✅
element.children  // ✅
element.nextElementSibling  // ✅

// Vérifier l'existence avant d'utiliser
if (element.parentElement) {
    // ...
}

// Utiliser closest() pour trouver un ancêtre
let card = button.closest('.card');  // ✅ Pratique

// Stocker les références si utilisées plusieurs fois
let parent = element.parentElement;
let enfants = parent.children;

// Utiliser for...of pour parcourir les enfants
for (let enfant of element.children) {
    console.log(enfant);
}
```

### ❌ À éviter

```javascript
// Éviter les propriétés Node si vous voulez des éléments
element.parentNode  // ⚠️ Peut retourner des nœuds de texte
element.childNodes  // ⚠️ Inclut les nœuds de texte
element.nextSibling  // ⚠️ Peut être un nœud de texte

// Ne pas oublier de vérifier l'existence
element.parentElement.style.color = 'red';  // ❌ Si null, erreur !

// Ne pas supposer qu'il y a toujours un frère
element.nextElementSibling.remove();  // ❌ Si null, erreur !

// Éviter les chaînages trop longs sans vérification
element.parentElement.parentElement.parentElement.remove();  // ❌ Fragile
```

---

## Différences Element vs Node

### Propriétés Element (recommandées)

```javascript
element.parentElement
element.children
element.firstElementChild
element.lastElementChild
element.nextElementSibling
element.previousElementSibling
```

**Retournent :** Uniquement des **éléments HTML** (ou null)
**Ignorent :** Les nœuds de texte, commentaires

### Propriétés Node (anciennes)

```javascript
element.parentNode
element.childNodes
element.firstChild
element.lastChild
element.nextSibling
element.previousSibling
```

**Retournent :** N'importe quel **type de nœud**
**Incluent :** Texte, commentaires, éléments

### Pourquoi préférer Element ?

```html
<div id="container">
    Texte avant
    <p id="para">Paragraphe</p>
    Texte après
</div>
```

```javascript
let container = document.getElementById('container');

// Avec childNodes (inclut les nœuds de texte)
console.log(container.childNodes);
// NodeList(5) [text, p, text]  // Compliqué !

// Avec children (seulement les éléments)
console.log(container.children);
// HTMLCollection(1) [p]  // ✅ Plus clair
```

---

## Visualisation des relations

```
          parentElement
                ↑
                |
    [previousElementSibling] ← [ELEMENT] → [nextElementSibling]
                |
                ↓
             children
                |
        ┌───────┴───────┐
        |       |       |
  firstElementChild   lastElementChild
```

---

## Points clés à retenir

✅ **`parentElement`** remonte vers le parent

✅ **`children`** descend vers tous les enfants

✅ **`firstElementChild`** / **`lastElementChild`** pour le premier/dernier enfant

✅ **`nextElementSibling`** / **`previousElementSibling`** pour naviguer entre frères

✅ **`closest(selector)`** trouve l'ancêtre le plus proche correspondant

✅ Préférez les propriétés **Element** (ignorent les nœuds de texte)

✅ **Toujours vérifier** que la propriété n'est pas null avant utilisation

✅ La navigation permet d'accéder aux éléments **sans connaître leur ID**

✅ Très utile pour la **délégation d'événements** et les **composants**

✅ Peut être combinée avec manipulation pour des effets complexes

---

## Conclusion du chapitre Manipulation du DOM

Félicitations ! Vous maîtrisez maintenant toutes les compétences essentielles pour manipuler le DOM :

1. ✅ **Comprendre** le DOM et son fonctionnement
2. ✅ **Sélectionner** des éléments (querySelector, getElementById...)
3. ✅ **Modifier** le contenu (innerHTML, textContent)
4. ✅ **Modifier** les attributs (getAttribute, setAttribute, dataset)
5. ✅ **Modifier** les styles (style, classList)
6. ✅ **Créer** des éléments (createElement)
7. ✅ **Insérer** des éléments (append, appendChild...)
8. ✅ **Supprimer** des éléments (remove, removeChild)
9. ✅ **Naviguer** dans le DOM (parentElement, children...)

Vous avez maintenant toutes les bases pour créer des **interfaces web dynamiques et interactives** !

---

## Ce qui vient ensuite

Avec ces compétences de manipulation du DOM, vous êtes prêt pour le chapitre suivant : **les événements** ! Vous apprendrez à réagir aux actions de l'utilisateur (clics, saisies, mouvements de souris...) pour rendre vos pages vraiment interactives.

---

## Ressources supplémentaires

- 📖 [MDN - Element.parentElement](https://developer.mozilla.org/fr/docs/Web/API/Element/parentElement)
- 📖 [MDN - Element.children](https://developer.mozilla.org/fr/docs/Web/API/Element/children)
- 📖 [MDN - Element.nextElementSibling](https://developer.mozilla.org/fr/docs/Web/API/Element/nextElementSibling)
- 📖 [MDN - Element.closest()](https://developer.mozilla.org/fr/docs/Web/API/Element/closest)
- 📖 [MDN - Traversing the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Traversing_an_HTML_table_with_JavaScript_and_DOM_Interfaces)

---


⏭️ [Événements](/05-javascript-moderne-fondamentaux/10-evenements/README.md)
