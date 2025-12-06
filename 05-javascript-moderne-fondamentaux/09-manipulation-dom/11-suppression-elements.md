🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.11 - Suppression d'éléments : remove, removeChild

## Introduction

Vous savez maintenant créer et insérer des éléments dans le DOM. Il est temps d'apprendre à les **supprimer** ! La suppression d'éléments est essentielle pour créer des interfaces dynamiques et interactives.

JavaScript offre plusieurs méthodes pour supprimer des éléments :
- 🗑️ Supprimer un élément spécifique
- 🧹 Vider complètement un conteneur
- 🔄 Remplacer un élément par un autre

> **Note importante :** Une fois supprimé du DOM, un élément existe toujours en mémoire si vous en avez gardé une référence. Vous pouvez donc le réinsérer plus tard !

---

## remove() - La méthode moderne 🆕

### Qu'est-ce que remove ?

**`remove()`** est la méthode **moderne et simple** pour supprimer un élément du DOM.

### Syntaxe

```javascript
element.remove();
```

C'est tout ! L'élément se supprime lui-même du DOM.

### Exemple basique

**HTML initial :**
```html
<div id="container">
    <p id="para1">Premier paragraphe</p>
    <p id="para2">Deuxième paragraphe</p>
    <p id="para3">Troisième paragraphe</p>
</div>
```

**JavaScript :**
```javascript
let para2 = document.getElementById('para2');
para2.remove();
```

**Résultat :**
```html
<div id="container">
    <p id="para1">Premier paragraphe</p>
    <p id="para3">Troisième paragraphe</p>
</div>
```

Le deuxième paragraphe a disparu !

### Exemple interactif : Bouton de suppression

**HTML :**
```html
<div class="card">
    <h3>Ma carte</h3>
    <p>Contenu de la carte</p>
    <button class="btn-delete">Supprimer</button>
</div>
```

**JavaScript :**
```javascript
let boutonSupprimer = document.querySelector('.btn-delete');

boutonSupprimer.addEventListener('click', function() {
    // Supprimer la carte parente
    let carte = this.closest('.card');
    carte.remove();
});
```

**Explication :**
- `this.closest('.card')` remonte dans le DOM pour trouver l'élément parent avec la classe `card`
- `.remove()` supprime toute la carte

### L'élément existe toujours en mémoire

**Important :** Après suppression, si vous avez gardé une référence, l'élément existe toujours en mémoire :

```javascript
let paragraphe = document.getElementById('mon-para');

// Supprimer du DOM
paragraphe.remove();

// L'élément existe toujours en mémoire !
console.log(paragraphe);  // <p id="mon-para">...</p>

// On peut le réinsérer
document.body.append(paragraphe);  // Il réapparaît !
```

---

## removeChild() - La méthode classique

### Qu'est-ce que removeChild ?

**`removeChild()`** est la méthode classique pour supprimer un élément. Elle est appelée sur le **parent** et nécessite de connaître l'élément à supprimer.

### Syntaxe

```javascript
elementParent.removeChild(elementEnfant);
```

### Exemple basique

**HTML :**
```html
<ul id="liste">
    <li id="item1">Item 1</li>
    <li id="item2">Item 2</li>
    <li id="item3">Item 3</li>
</ul>
```

**JavaScript :**
```javascript
let liste = document.getElementById('liste');
let item2 = document.getElementById('item2');

// Supprimer item2 de la liste
liste.removeChild(item2);
```

**Résultat :**
```html
<ul id="liste">
    <li id="item1">Item 1</li>
    <li id="item3">Item 3</li>
</ul>
```

### Différence avec remove()

**Avec remove() (moderne) :**
```javascript
let item = document.getElementById('item2');
item.remove();  // ✅ Simple et direct
```

**Avec removeChild() (classique) :**
```javascript
let liste = document.getElementById('liste');
let item = document.getElementById('item2');
liste.removeChild(item);  // Il faut connaître le parent
```

**Ou de manière plus générique :**
```javascript
let item = document.getElementById('item2');
item.parentElement.removeChild(item);  // On récupère le parent d'abord
```

### Retour de removeChild

`removeChild()` retourne l'élément qui a été supprimé :

```javascript
let liste = document.getElementById('liste');
let item = document.getElementById('item2');

let elementSupprime = liste.removeChild(item);
console.log(elementSupprime);  // <li id="item2">Item 2</li>

// On peut le réinsérer ailleurs
document.body.appendChild(elementSupprime);
```

---

## remove vs removeChild : Comparaison

| Critère | remove() | removeChild() |
|---------|----------|---------------|
| **Année** | Moderne (2015+) | Classique (DOM Level 1) |
| **Syntaxe** | `element.remove()` | `parent.removeChild(element)` |
| **Besoin du parent** | ❌ Non | ✅ Oui |
| **Simplicité** | ✅ Très simple | ⚠️ Plus verbeux |
| **Retour** | undefined | L'élément supprimé |
| **Compatibilité** | Navigateurs modernes | Tous navigateurs |

### Quelle méthode utiliser ?

**Pour les nouveaux projets :**
- ✅ Utilisez **`remove()`** (plus simple et moderne)

**Pour les anciens projets ou compatibilité maximale :**
- ✅ Utilisez **`removeChild()`** (fonctionne partout)

**Conversion :**
```javascript
// Ancien code
element.parentElement.removeChild(element);

// Moderne (équivalent)
element.remove();
```

---

## Vider un conteneur

### Le problème

Comment supprimer **tous les enfants** d'un élément ?

**HTML :**
```html
<ul id="liste">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
    <li>Item 4</li>
</ul>
```

### Méthode 1 : innerHTML = '' (simple mais...)

La méthode la plus simple :

```javascript
let liste = document.getElementById('liste');
liste.innerHTML = '';
```

**Résultat :** La liste est vide !

**⚠️ Attention :**
- Supprime **tous les événements** attachés aux éléments
- Peut avoir des effets de bord
- OK pour du contenu simple sans événements

### Méthode 2 : textContent = '' (pour le texte uniquement)

```javascript
let element = document.getElementById('container');
element.textContent = '';
```

**Note :** Cela supprime aussi les éléments HTML, pas seulement le texte !

### Méthode 3 : Boucle while (plus propre)

La méthode recommandée quand vous voulez être sûr :

```javascript
let liste = document.getElementById('liste');

// Supprimer tous les enfants un par un
while (liste.firstChild) {
    liste.removeChild(liste.firstChild);
}
```

**Avantages :**
- ✅ Préserve les événements (si vous en avez besoin ailleurs)
- ✅ Plus prévisible
- ✅ Fonctionne partout

### Méthode 4 : replaceChildren() (très moderne) 🆕

La méthode la plus récente et la plus propre :

```javascript
let liste = document.getElementById('liste');
liste.replaceChildren();  // Vide le conteneur
```

**Ou pour remplacer par de nouveaux enfants :**
```javascript
let nouveauItem1 = document.createElement('li');
nouveauItem1.textContent = 'Nouveau 1';

let nouveauItem2 = document.createElement('li');
nouveauItem2.textContent = 'Nouveau 2';

liste.replaceChildren(nouveauItem1, nouveauItem2);
// Remplace tous les anciens enfants par les nouveaux
```

### Exemple pratique : Réinitialiser une liste

```html
<ul id="tasks">
    <li>Tâche 1</li>
    <li>Tâche 2</li>
    <li>Tâche 3</li>
</ul>
<button id="clear-btn">Tout effacer</button>
```

```javascript
let tasks = document.getElementById('tasks');
let clearBtn = document.getElementById('clear-btn');

clearBtn.addEventListener('click', function() {
    // Vider la liste
    tasks.innerHTML = '';
    // Ou : tasks.replaceChildren();
    // Ou : while (tasks.firstChild) { tasks.removeChild(tasks.firstChild); }
});
```

---

## Supprimer plusieurs éléments

### Supprimer tous les éléments d'une sélection

**HTML :**
```html
<div id="container">
    <p class="temp">Temporaire 1</p>
    <p class="keep">À garder</p>
    <p class="temp">Temporaire 2</p>
    <p class="temp">Temporaire 3</p>
</div>
```

**JavaScript :**
```javascript
// Sélectionner tous les éléments temporaires
let tempElements = document.querySelectorAll('.temp');

// Supprimer chacun
tempElements.forEach(element => {
    element.remove();
});
```

**Résultat :**
```html
<div id="container">
    <p class="keep">À garder</p>
</div>
```

### Exemple : Supprimer les éléments cochés

```html
<ul id="todo-list">
    <li><input type="checkbox"> Tâche 1</li>
    <li><input type="checkbox" checked> Tâche 2</li>
    <li><input type="checkbox"> Tâche 3</li>
    <li><input type="checkbox" checked> Tâche 4</li>
</ul>
<button id="delete-completed">Supprimer les tâches terminées</button>
```

```javascript
let deleteBtn = document.getElementById('delete-completed');

deleteBtn.addEventListener('click', function() {
    // Trouver toutes les cases cochées
    let checkedItems = document.querySelectorAll('#todo-list input[type="checkbox"]:checked');

    // Supprimer chaque item parent (le <li>)
    checkedItems.forEach(checkbox => {
        let li = checkbox.closest('li');
        li.remove();
    });
});
```

---

## Remplacer un élément

### replaceWith() - Méthode moderne 🆕

**`replaceWith()`** remplace un élément par un ou plusieurs autres éléments.

### Syntaxe

```javascript
ancienElement.replaceWith(nouveauElement);
// Ou avec plusieurs éléments
ancienElement.replaceWith(elem1, elem2, elem3);
```

### Exemple basique

**HTML :**
```html
<div id="container">
    <p id="old">Ancien paragraphe</p>
</div>
```

**JavaScript :**
```javascript
let ancien = document.getElementById('old');

// Créer le nouveau
let nouveau = document.createElement('p');
nouveau.textContent = 'Nouveau paragraphe';
nouveau.id = 'new';

// Remplacer
ancien.replaceWith(nouveau);
```

**Résultat :**
```html
<div id="container">
    <p id="new">Nouveau paragraphe</p>
</div>
```

### Remplacer par plusieurs éléments

```javascript
let ancien = document.getElementById('old');

let titre = document.createElement('h2');
titre.textContent = 'Titre';

let paragraphe = document.createElement('p');
paragraphe.textContent = 'Paragraphe';

// Remplacer par deux éléments
ancien.replaceWith(titre, paragraphe);
```

**Résultat :**
```html
<div id="container">
    <h2>Titre</h2>
    <p>Paragraphe</p>
</div>
```

### Remplacer par du texte

```javascript
let element = document.getElementById('old');
element.replaceWith('Juste du texte');
```

### replaceChild() - Méthode classique

L'équivalent classique de `replaceWith()` :

```javascript
parent.replaceChild(nouveauElement, ancienElement);
```

**Exemple :**
```javascript
let container = document.getElementById('container');
let ancien = document.getElementById('old');
let nouveau = document.createElement('p');
nouveau.textContent = 'Nouveau';

// Remplacer (méthode classique)
container.replaceChild(nouveau, ancien);
```

### Comparaison

```javascript
// Moderne (simple)
ancien.replaceWith(nouveau);

// Classique (plus verbeux)
ancien.parentElement.replaceChild(nouveau, ancien);
```

---

## Exemples pratiques complets

### Exemple 1 : Liste de courses avec suppression

```html
<div id="shopping-list">
    <h2>Ma liste de courses</h2>
    <ul id="items"></ul>
    <input type="text" id="item-input" placeholder="Nouvel article">
    <button id="add-btn">Ajouter</button>
</div>
```

```javascript
let itemsList = document.getElementById('items');
let input = document.getElementById('item-input');
let addBtn = document.getElementById('add-btn');

function ajouterArticle(texte) {
    let li = document.createElement('li');

    let span = document.createElement('span');
    span.textContent = texte;

    let btnSupprimer = document.createElement('button');
    btnSupprimer.textContent = '✕';
    btnSupprimer.classList.add('btn-delete');

    // Événement de suppression
    btnSupprimer.addEventListener('click', function() {
        li.remove();  // Supprime le <li> entier
    });

    li.append(span, btnSupprimer);
    itemsList.append(li);
}

addBtn.addEventListener('click', function() {
    let texte = input.value.trim();
    if (texte) {
        ajouterArticle(texte);
        input.value = '';
    }
});
```

### Exemple 2 : Galerie d'images avec suppression

```html
<div id="gallery"></div>
<button id="add-image">Ajouter une image</button>
```

```javascript
let gallery = document.getElementById('gallery');
let addImageBtn = document.getElementById('add-image');
let compteur = 1;

function creerImage(numero) {
    let figure = document.createElement('figure');
    figure.classList.add('image-item');

    let img = document.createElement('img');
    img.src = `https://picsum.photos/200/200?random=${numero}`;
    img.alt = `Image ${numero}`;

    let caption = document.createElement('figcaption');
    caption.textContent = `Image ${numero}`;

    let btnSupprimer = document.createElement('button');
    btnSupprimer.textContent = '🗑️ Supprimer';
    btnSupprimer.classList.add('btn-delete');

    btnSupprimer.addEventListener('click', function() {
        // Animation avant suppression (optionnel)
        figure.style.opacity = '0';
        figure.style.transition = 'opacity 0.3s';

        setTimeout(() => {
            figure.remove();
        }, 300);
    });

    figure.append(img, caption, btnSupprimer);
    return figure;
}

addImageBtn.addEventListener('click', function() {
    let image = creerImage(compteur);
    gallery.append(image);
    compteur++;
});

// Ajouter quelques images par défaut
for (let i = 0; i < 3; i++) {
    let image = creerImage(compteur);
    gallery.append(image);
    compteur++;
}
```

### Exemple 3 : Système de filtres

```html
<div id="filters">
    <button data-filter="all" class="active">Tous</button>
    <button data-filter="urgent">Urgent</button>
    <button data-filter="normal">Normal</button>
    <button data-filter="low">Basse priorité</button>
</div>

<div id="tasks">
    <div class="task" data-priority="urgent">Tâche urgente</div>
    <div class="task" data-priority="normal">Tâche normale</div>
    <div class="task" data-priority="low">Tâche basse priorité</div>
    <div class="task" data-priority="urgent">Autre tâche urgente</div>
</div>
```

```javascript
let filterButtons = document.querySelectorAll('#filters button');
let tasks = document.querySelectorAll('.task');

filterButtons.forEach(button => {
    button.addEventListener('click', function() {
        let filter = this.dataset.filter;

        // Retirer la classe active de tous les boutons
        filterButtons.forEach(btn => btn.classList.remove('active'));

        // Ajouter la classe active au bouton cliqué
        this.classList.add('active');

        // Filtrer les tâches
        tasks.forEach(task => {
            if (filter === 'all' || task.dataset.priority === filter) {
                task.style.display = 'block';
            } else {
                task.style.display = 'none';
            }
        });
    });
});
```

### Exemple 4 : Modal avec suppression

```html
<button id="open-modal">Ouvrir le modal</button>

<div id="modal-overlay" style="display: none;">
    <div class="modal">
        <h2>Mon Modal</h2>
        <p>Contenu du modal</p>
        <button id="close-modal">Fermer</button>
    </div>
</div>
```

```javascript
let openBtn = document.getElementById('open-modal');
let closeBtn = document.getElementById('close-modal');
let overlay = document.getElementById('modal-overlay');

openBtn.addEventListener('click', function() {
    overlay.style.display = 'flex';
});

closeBtn.addEventListener('click', function() {
    // Option 1 : Cacher (ne supprime pas)
    overlay.style.display = 'none';

    // Option 2 : Supprimer complètement
    // overlay.remove();
});

// Fermer en cliquant sur l'overlay
overlay.addEventListener('click', function(e) {
    if (e.target === overlay) {
        overlay.style.display = 'none';
    }
});
```

---

## Vérifier avant de supprimer

### Vérifier l'existence

Avant de supprimer, vérifiez que l'élément existe :

```javascript
let element = document.getElementById('mon-element');

if (element) {
    element.remove();
} else {
    console.log('Élément non trouvé');
}
```

### Confirmation utilisateur

Pour les suppressions importantes, demandez confirmation :

```javascript
let btnSupprimer = document.getElementById('delete-account');

btnSupprimer.addEventListener('click', function() {
    let confirmation = confirm('Êtes-vous sûr de vouloir supprimer votre compte ?');

    if (confirmation) {
        // Supprimer le compte
        console.log('Compte supprimé');
    } else {
        console.log('Suppression annulée');
    }
});
```

### Vérifier le nombre d'éléments

```javascript
let liste = document.getElementById('liste');

if (liste.children.length > 0) {
    // Il y a des éléments à supprimer
    liste.innerHTML = '';
} else {
    console.log('La liste est déjà vide');
}
```

---

## Animations avant suppression

Pour une meilleure expérience utilisateur, ajoutez une animation avant de supprimer :

### Exemple avec transition CSS

**CSS :**
```css
.fade-out {
    opacity: 0;
    transition: opacity 0.3s ease;
}
```

**JavaScript :**
```javascript
function supprimerAvecAnimation(element) {
    // Ajouter la classe d'animation
    element.classList.add('fade-out');

    // Supprimer après l'animation
    setTimeout(() => {
        element.remove();
    }, 300);  // Durée de la transition
}

// Utilisation
let item = document.getElementById('item');
supprimerAvecAnimation(item);
```

### Exemple avec slide up

**CSS :**
```css
.slide-up {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
}
```

**JavaScript :**
```javascript
function supprimerAvecSlide(element) {
    // Récupérer la hauteur actuelle
    let hauteur = element.offsetHeight;
    element.style.maxHeight = hauteur + 'px';

    // Forcer un reflow
    element.offsetHeight;

    // Ajouter la classe
    element.classList.add('slide-up');

    // Supprimer après l'animation
    setTimeout(() => {
        element.remove();
    }, 300);
}
```

---

## Restaurer un élément supprimé

### Garder une référence

Si vous gardez une référence, vous pouvez restaurer un élément :

```javascript
let elementSupprime = null;

function supprimer(element) {
    elementSupprime = element;
    element.remove();
}

function restaurer() {
    if (elementSupprime) {
        document.body.append(elementSupprime);
        elementSupprime = null;
    }
}

// Utilisation
let item = document.getElementById('item');
supprimer(item);

// Plus tard...
restaurer();  // L'élément réapparaît !
```

### Système d'annulation (Undo)

```javascript
let historiqueSuppressions = [];

function supprimerAvecHistorique(element) {
    // Sauvegarder avant de supprimer
    historiqueSuppressions.push({
        element: element,
        parent: element.parentElement,
        nextSibling: element.nextElementSibling
    });

    element.remove();
}

function annuler() {
    if (historiqueSuppressions.length > 0) {
        let derniere = historiqueSuppressions.pop();

        // Réinsérer à la bonne position
        if (derniere.nextSibling) {
            derniere.parent.insertBefore(derniere.element, derniere.nextSibling);
        } else {
            derniere.parent.appendChild(derniere.element);
        }
    }
}

// Utilisation
let item = document.getElementById('item');
supprimerAvecHistorique(item);

// Annuler
annuler();  // L'élément revient à sa place !
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Utiliser remove() pour la simplicité (moderne)
element.remove();  // ✅

// Vérifier l'existence avant de supprimer
if (element) {
    element.remove();
}

// Demander confirmation pour les suppressions importantes
if (confirm('Supprimer ?')) {
    element.remove();
}

// Vider un conteneur proprement
container.innerHTML = '';  // ✅ Simple pour du contenu sans événements

// Ou pour plus de contrôle
while (container.firstChild) {
    container.removeChild(container.firstChild);
}

// Animer avant de supprimer (meilleure UX)
element.classList.add('fade-out');
setTimeout(() => element.remove(), 300);

// Garder une référence si besoin de restaurer
let backup = element;
element.remove();
```

### ❌ À éviter

```javascript
// Ne pas oublier de vérifier l'existence
element.remove();  // ❌ Peut planter si element est null

// Ne pas supprimer dans une boucle sur une collection vivante
let items = document.getElementsByClassName('item');
for (let i = 0; i < items.length; i++) {
    items[i].remove();  // ❌ La collection change pendant la boucle !
}

// Solution : utiliser querySelectorAll (NodeList statique)
let items = document.querySelectorAll('.item');
items.forEach(item => item.remove());  // ✅

// Ne pas supprimer sans réfléchir aux conséquences
element.remove();  // Les événements attachés sont perdus

// Ne pas oublier de nettoyer les références
element.remove();
// Si vous avez encore des références, l'élément reste en mémoire
```

---

## Suppression et gestion de la mémoire

### Fuites mémoire potentielles

Quand vous supprimez un élément, JavaScript peut le garder en mémoire si :
- Vous avez encore des références vers lui
- Des événements sont encore attachés
- Des timers (setTimeout, setInterval) y font référence

### Exemple de fuite

```javascript
let elements = [];

function creerElement() {
    let div = document.createElement('div');
    div.textContent = 'Element';
    document.body.append(div);

    elements.push(div);  // Garde une référence
}

function supprimerTous() {
    let divs = document.querySelectorAll('div');
    divs.forEach(div => div.remove());

    // ⚠️ Les éléments sont toujours en mémoire dans le tableau !
    console.log(elements.length);  // Toujours là
}
```

### Solution

```javascript
function supprimerTous() {
    let divs = document.querySelectorAll('div');
    divs.forEach(div => div.remove());

    // Nettoyer les références
    elements = [];  // ✅ Libère la mémoire
}
```

---

## Points clés à retenir

✅ **`remove()`** est la méthode moderne pour supprimer un élément 🆕

✅ **`removeChild()`** est la méthode classique (nécessite le parent)

✅ Pour **vider un conteneur** : `innerHTML = ''` ou `replaceChildren()`

✅ **`replaceWith()`** remplace un élément par un autre 🆕

✅ Un élément supprimé du DOM peut être **réinséré** si vous gardez une référence

✅ Suppression de plusieurs éléments : utiliser `querySelectorAll()` + `forEach()`

✅ Toujours **vérifier l'existence** avant de supprimer

✅ **Animer** avant de supprimer pour une meilleure UX

✅ Attention aux **fuites mémoire** avec les références persistantes

✅ Pour les suppressions importantes, demander **confirmation**

---

## Résumé des méthodes

| Méthode | Action | Moderne | Syntaxe |
|---------|--------|---------|---------|
| **remove()** | Supprime l'élément | ✅ | `element.remove()` |
| **removeChild()** | Supprime un enfant | ❌ | `parent.removeChild(enfant)` |
| **replaceWith()** | Remplace l'élément | ✅ | `ancien.replaceWith(nouveau)` |
| **replaceChild()** | Remplace un enfant | ❌ | `parent.replaceChild(nouveau, ancien)` |
| **replaceChildren()** | Remplace tous les enfants | ✅ | `parent.replaceChildren(...)` |
| **innerHTML = ''** | Vide le conteneur | ❌ | `element.innerHTML = ''` |

---

## Ce qui vient ensuite

Vous avez maintenant appris toutes les opérations de base sur le DOM :
- ✅ Sélectionner des éléments
- ✅ Modifier leur contenu et attributs
- ✅ Modifier leurs styles et classes
- ✅ Créer de nouveaux éléments
- ✅ Insérer des éléments
- ✅ Supprimer des éléments

La prochaine étape : apprendre à **naviguer** dans le DOM (parents, enfants, frères) pour manipuler les éléments de manière relative !

---

## Ressources supplémentaires

- 📖 [MDN - Element.remove()](https://developer.mozilla.org/fr/docs/Web/API/Element/remove)
- 📖 [MDN - Node.removeChild()](https://developer.mozilla.org/fr/docs/Web/API/Node/removeChild)
- 📖 [MDN - Element.replaceWith()](https://developer.mozilla.org/fr/docs/Web/API/Element/replaceWith)
- 📖 [MDN - Element.replaceChildren()](https://developer.mozilla.org/fr/docs/Web/API/Element/replaceChildren)

---


⏭️ [Navigation dans le DOM : parentElement, children, nextElementSibling](/05-javascript-moderne-fondamentaux/09-manipulation-dom/12-navigation-dom.md)
