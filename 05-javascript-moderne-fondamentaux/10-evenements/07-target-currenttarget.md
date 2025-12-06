🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.7 - event.target vs event.currentTarget

## Introduction

`event.target` et `event.currentTarget` sont deux propriétés de l'objet Event qui semblent similaires mais qui ont des **significations très différentes**. Cette différence est source de confusion pour beaucoup de débutants, mais une fois comprise, elle devient un outil puissant.

Dans cette leçon, nous allons comprendre exactement ce qui les distingue et comment les utiliser correctement.

## La différence fondamentale

### Définitions

**`event.target`**
- C'est **l'élément qui a réellement déclenché l'événement**
- C'est l'élément sur lequel l'utilisateur a **réellement cliqué**
- Peut être n'importe quel descendant de l'élément écouté

**`event.currentTarget`**
- C'est **l'élément sur lequel l'écouteur d'événement est attaché**
- C'est **toujours** l'élément auquel vous avez fait `addEventListener`
- Ne change jamais pendant la propagation

### Analogie du monde réel

Imaginez un bâtiment avec un système d'alarme :

- **`event.target`** = L'endroit exact où l'intrusion a eu lieu (une fenêtre spécifique au 3e étage)
- **`event.currentTarget`** = Le panneau d'alarme principal qui reçoit tous les signaux (à l'entrée)

Le panneau principal (`currentTarget`) reçoit toujours les alertes, mais l'intrusion (`target`) peut avoir lieu à différents endroits.

## Exemple simple pour comprendre

### HTML
```html
<div id="parent" style="padding: 30px; background: lightblue;">
    PARENT
    <button id="enfant">ENFANT (bouton)</button>
</div>
<p id="resultat"></p>
```

### JavaScript
```javascript
const parent = document.getElementById('parent');
const enfant = document.getElementById('enfant');
const resultat = document.getElementById('resultat');

parent.addEventListener('click', (event) => {
    resultat.innerHTML = `
        <strong>Clic détecté :</strong><br>
        event.target = ${event.target.id}<br>
        event.currentTarget = ${event.currentTarget.id}
    `;
});
```

### Résultats selon où vous cliquez :

**Si vous cliquez sur le PARENT (zone bleue) :**
```
event.target = parent
event.currentTarget = parent
```
→ Les deux sont identiques car vous avez cliqué directement sur l'élément écouté

**Si vous cliquez sur le BOUTON ENFANT :**
```
event.target = enfant
event.currentTarget = parent
```
→ `target` est le bouton (où vous avez cliqué), mais `currentTarget` reste le parent (où l'écouteur est attaché)

## Visualisation du concept

```
┌─────────────────────────────────────────┐
│  DIV PARENT (currentTarget)             │
│  ← addEventListener est ici             │
│                                         │
│  ┌──────────────────────────┐           │
│  │  BUTTON ENFANT           │           │
│  │  ← Clic ici (target)     │           │
│  └──────────────────────────┘           │
│                                         │
└─────────────────────────────────────────┘

Événement détecté :
- target = BUTTON (l'élément cliqué)
- currentTarget = DIV (l'élément qui écoute)
```

## Exemples pratiques détaillés

### Exemple 1 : Identification de l'élément cliqué

```html
<ul id="liste">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
    <li>Item 4</li>
</ul>
<p id="message"></p>
```

```javascript
const liste = document.getElementById('liste');
const message = document.getElementById('message');

liste.addEventListener('click', (event) => {
    console.log('target :', event.target);           // L'élément <li> cliqué
    console.log('currentTarget :', event.currentTarget); // Toujours <ul>

    // Utiliser target pour savoir quel item a été cliqué
    if (event.target.tagName === 'LI') {
        message.textContent = `Vous avez cliqué sur : ${event.target.textContent}`;
    }
});
```

**Pourquoi c'est utile ?**
- Vous n'avez besoin que d'**un seul écouteur** sur la liste
- Vous pouvez identifier **quel item** a été cliqué avec `event.target`
- Plus performant que d'attacher un écouteur à chaque `<li>`

### Exemple 2 : Structure HTML complexe

```html
<div id="carte" class="carte">
    <h3 class="titre">Titre de la carte</h3>
    <p class="description">Description de la carte</p>
    <button class="bouton">En savoir plus</button>
</div>
<p id="info"></p>
```

```javascript
const carte = document.querySelector('.carte');
const info = document.getElementById('info');

carte.addEventListener('click', (event) => {
    info.innerHTML = `
        Élément cliqué (target) : ${event.target.className || event.target.tagName}<br>
        Élément écouté (currentTarget) : ${event.currentTarget.className}
    `;
});
```

**Résultats possibles :**

- Clic sur le titre → `target = titre`, `currentTarget = carte`
- Clic sur la description → `target = description`, `currentTarget = carte`
- Clic sur le bouton → `target = bouton`, `currentTarget = carte`
- Clic sur la carte elle-même → `target = carte`, `currentTarget = carte`

### Exemple 3 : Galerie d'images

```html
<div id="galerie" style="display: flex; gap: 10px;">
    <img src="photo1.jpg" alt="Photo 1" data-id="1">
    <img src="photo2.jpg" alt="Photo 2" data-id="2">
    <img src="photo3.jpg" alt="Photo 3" data-id="3">
</div>
<p id="selection"></p>
```

```javascript
const galerie = document.getElementById('galerie');
const selection = document.getElementById('selection');

galerie.addEventListener('click', (event) => {
    // event.target = l'image cliquée
    // event.currentTarget = la div galerie

    if (event.target.tagName === 'IMG') {
        const photoId = event.target.dataset.id;
        const photoAlt = event.target.alt;

        selection.textContent = `Photo sélectionnée : ${photoAlt} (ID: ${photoId})`;
    }
});
```

## Cas d'usage : Quand utiliser quoi ?

### Utilisez `event.target` quand :

✅ Vous voulez savoir **quel élément exact** a été cliqué

```javascript
container.addEventListener('click', (event) => {
    // Identifier l'élément cliqué
    console.log('Vous avez cliqué sur :', event.target);
});
```

✅ Vous voulez récupérer des informations de l'élément cliqué

```javascript
liste.addEventListener('click', (event) => {
    const texte = event.target.textContent;
    const id = event.target.dataset.id;
    console.log(texte, id);
});
```

✅ Vous voulez modifier l'élément cliqué spécifiquement

```javascript
container.addEventListener('click', (event) => {
    if (event.target.classList.contains('bouton')) {
        event.target.classList.add('actif');
    }
});
```

### Utilisez `event.currentTarget` quand :

✅ Vous voulez toujours référencer l'élément qui écoute

```javascript
const menu = document.getElementById('menu');

menu.addEventListener('click', (event) => {
    // Toujours le menu, peu importe où vous cliquez dedans
    event.currentTarget.classList.toggle('ouvert');
});
```

✅ Vous voulez modifier le conteneur, pas l'élément cliqué

```javascript
const boite = document.getElementById('boite');

boite.addEventListener('click', (event) => {
    // Changer le fond de la boîte, pas de l'élément cliqué
    event.currentTarget.style.backgroundColor = 'lightcoral';
});
```

✅ Alternative à `this` dans les fonctions traditionnelles

```javascript
element.addEventListener('click', function(event) {
    // event.currentTarget est plus fiable que this
    console.log(event.currentTarget === this); // true (dans fonction normale)
});
```

## Le concept de délégation d'événements

La différence entre `target` et `currentTarget` est la base de la **délégation d'événements**, une technique très importante en JavaScript.

### Sans délégation (❌ inefficace)

```javascript
// Attacher un événement à chaque bouton individuellement
const boutons = document.querySelectorAll('.bouton');

boutons.forEach(bouton => {
    bouton.addEventListener('click', () => {
        console.log('Bouton cliqué');
    });
});

// Problème : 100 boutons = 100 écouteurs = lourd en mémoire
```

### Avec délégation (✅ efficace)

```javascript
// Un seul événement sur le conteneur parent
const conteneur = document.getElementById('conteneur');

conteneur.addEventListener('click', (event) => {
    // Vérifier si le clic est sur un bouton
    if (event.target.classList.contains('bouton')) {
        console.log('Bouton cliqué :', event.target.textContent);
    }
});

// Avantage : 1 seul écouteur pour 100 boutons !
```

### Exemple pratique : Liste de tâches

```html
<div id="todo-app">
    <input type="text" id="nouvelle-tache" placeholder="Nouvelle tâche">
    <button id="ajouter">Ajouter</button>
    <ul id="liste-taches">
        <!-- Les tâches seront ajoutées ici dynamiquement -->
    </ul>
</div>
```

```javascript
const app = document.getElementById('todo-app');
const input = document.getElementById('nouvelle-tache');
const liste = document.getElementById('liste-taches');

// Délégation d'événements sur tout l'app
app.addEventListener('click', (event) => {
    const target = event.target;

    // Ajouter une tâche
    if (target.id === 'ajouter') {
        if (input.value.trim()) {
            const li = document.createElement('li');
            li.innerHTML = `
                <span>${input.value}</span>
                <button class="supprimer">✕</button>
            `;
            liste.appendChild(li);
            input.value = '';
        }
    }

    // Supprimer une tâche
    if (target.classList.contains('supprimer')) {
        target.parentElement.remove();
    }

    // Marquer comme complétée
    if (target.tagName === 'SPAN' && target.parentElement.tagName === 'LI') {
        target.style.textDecoration =
            target.style.textDecoration === 'line-through' ? 'none' : 'line-through';
    }
});
```

**Avantages de cette approche :**
- ✅ Un seul écouteur pour toute l'application
- ✅ Fonctionne même pour les éléments ajoutés dynamiquement
- ✅ Meilleure performance
- ✅ Code plus maintenable

## Pièges courants et solutions

### Piège 1 : Confondre target et currentTarget

```javascript
// ❌ ERREUR FRÉQUENTE
parent.addEventListener('click', (event) => {
    // On veut modifier le parent mais on utilise target
    event.target.classList.add('actif'); // Modifie l'enfant cliqué !
});

// ✅ CORRECT
parent.addEventListener('click', (event) => {
    // Modifier le parent
    event.currentTarget.classList.add('actif');
});
```

### Piège 2 : Vérifier le type d'élément

```javascript
// ❌ PAS ROBUSTE
container.addEventListener('click', (event) => {
    const texte = event.target.textContent;
    // Si target est un élément vide, ça peut causer des bugs
});

// ✅ MEILLEUR
container.addEventListener('click', (event) => {
    if (event.target.classList.contains('item')) {
        const texte = event.target.textContent;
        // Maintenant c'est sûr
    }
});
```

### Piège 3 : Éléments imbriqués

```html
<button class="bouton">
    <span>Texte</span>
    <i class="icone">🔥</i>
</button>
```

```javascript
// ❌ PROBLÈME
document.addEventListener('click', (event) => {
    if (event.target.classList.contains('bouton')) {
        // Ne marche pas si on clique sur le span ou l'icône !
        console.log('Bouton cliqué');
    }
});

// ✅ SOLUTION : Remonter jusqu'au bouton
document.addEventListener('click', (event) => {
    const bouton = event.target.closest('.bouton');
    if (bouton) {
        console.log('Bouton cliqué');
    }
});
```

## La méthode closest() : votre meilleur ami

La méthode `closest()` remonte dans l'arbre DOM jusqu'à trouver un élément correspondant.

```javascript
element.addEventListener('click', (event) => {
    // Trouver le bouton parent, même si on clique sur un enfant
    const bouton = event.target.closest('.bouton');

    if (bouton) {
        console.log('Bouton trouvé :', bouton);
    }
});
```

### Exemple pratique avec closest()

```html
<div id="menu">
    <div class="menu-item">
        <span class="icone">🏠</span>
        <span class="texte">Accueil</span>
    </div>
    <div class="menu-item">
        <span class="icone">👤</span>
        <span class="texte">Profil</span>
    </div>
    <div class="menu-item">
        <span class="icone">⚙️</span>
        <span class="texte">Paramètres</span>
    </div>
</div>
```

```javascript
const menu = document.getElementById('menu');

menu.addEventListener('click', (event) => {
    // Peu importe si on clique sur l'icône ou le texte
    const menuItem = event.target.closest('.menu-item');

    if (menuItem) {
        const texte = menuItem.querySelector('.texte').textContent;
        console.log('Menu sélectionné :', texte);

        // Retirer la classe active de tous les items
        menu.querySelectorAll('.menu-item').forEach(item => {
            item.classList.remove('actif');
        });

        // Ajouter la classe active à l'item cliqué
        menuItem.classList.add('actif');
    }
});
```

## Exemples pratiques complets

### Exemple 1 : Tableau interactif

```html
<table id="tableau">
    <thead>
        <tr>
            <th>Nom</th>
            <th>Âge</th>
            <th>Actions</th>
        </tr>
    </thead>
    <tbody>
        <tr data-id="1">
            <td>Alice</td>
            <td>25</td>
            <td>
                <button class="modifier">Modifier</button>
                <button class="supprimer">Supprimer</button>
            </td>
        </tr>
        <tr data-id="2">
            <td>Bob</td>
            <td>30</td>
            <td>
                <button class="modifier">Modifier</button>
                <button class="supprimer">Supprimer</button>
            </td>
        </tr>
    </tbody>
</table>
```

```javascript
const tableau = document.getElementById('tableau');

tableau.addEventListener('click', (event) => {
    const target = event.target;

    // Trouver la ligne concernée
    const ligne = target.closest('tr');

    if (!ligne) return;

    const id = ligne.dataset.id;
    const nom = ligne.querySelector('td:first-child').textContent;

    // Modifier
    if (target.classList.contains('modifier')) {
        console.log(`Modifier ${nom} (ID: ${id})`);
        // Logique de modification
    }

    // Supprimer
    if (target.classList.contains('supprimer')) {
        if (confirm(`Supprimer ${nom} ?`)) {
            ligne.remove();
            console.log(`${nom} supprimé`);
        }
    }
});
```

### Exemple 2 : Accordéon

```html
<div id="accordeon">
    <div class="item">
        <div class="titre">Question 1</div>
        <div class="contenu" style="display: none;">Réponse 1</div>
    </div>
    <div class="item">
        <div class="titre">Question 2</div>
        <div class="contenu" style="display: none;">Réponse 2</div>
    </div>
    <div class="item">
        <div class="titre">Question 3</div>
        <div class="contenu" style="display: none;">Réponse 3</div>
    </div>
</div>
```

```javascript
const accordeon = document.getElementById('accordeon');

accordeon.addEventListener('click', (event) => {
    const titre = event.target.closest('.titre');

    if (titre) {
        const item = titre.parentElement;
        const contenu = item.querySelector('.contenu');

        // Basculer l'affichage
        if (contenu.style.display === 'none') {
            contenu.style.display = 'block';
            titre.classList.add('ouvert');
        } else {
            contenu.style.display = 'none';
            titre.classList.remove('ouvert');
        }
    }
});
```

### Exemple 3 : Carte de sélection multiple

```html
<div id="grille" style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px;">
    <div class="carte" data-id="1">Carte 1</div>
    <div class="carte" data-id="2">Carte 2</div>
    <div class="carte" data-id="3">Carte 3</div>
    <div class="carte" data-id="4">Carte 4</div>
    <div class="carte" data-id="5">Carte 5</div>
    <div class="carte" data-id="6">Carte 6</div>
</div>
<p>Sélectionnées : <span id="selection">0</span></p>
```

```javascript
const grille = document.getElementById('grille');
const selection = document.getElementById('selection');
const cartesSelectionnees = new Set();

grille.addEventListener('click', (event) => {
    const carte = event.target.closest('.carte');

    if (carte) {
        const id = carte.dataset.id;

        if (event.ctrlKey || event.metaKey) {
            // Sélection multiple avec Ctrl
            if (cartesSelectionnees.has(id)) {
                cartesSelectionnees.delete(id);
                carte.classList.remove('selectionnee');
            } else {
                cartesSelectionnees.add(id);
                carte.classList.add('selectionnee');
            }
        } else {
            // Sélection simple
            grille.querySelectorAll('.carte').forEach(c => {
                c.classList.remove('selectionnee');
            });
            cartesSelectionnees.clear();
            cartesSelectionnees.add(id);
            carte.classList.add('selectionnee');
        }

        selection.textContent = cartesSelectionnees.size;
    }
});
```

## Résumé visuel

```
HTML Structure:
┌────────────────────────────────────┐
│ <div id="parent">                  │  ← addEventListener attaché ici
│   <div class="enfant">             │     (currentTarget)
│     <button>                       │
│       <span>Cliquez</span>         │  ← Clic réel ici (target)
│     </button>                      │
│   </div>                           │
│ </div>                             │
└────────────────────────────────────┘

Résultat :
event.target = <span>
event.currentTarget = <div id="parent">
```

## Tableau comparatif

| Critère | event.target | event.currentTarget |
|---------|-------------|---------------------|
| **Définition** | Élément qui a déclenché l'événement | Élément sur lequel addEventListener est attaché |
| **Peut changer** | ✅ Oui (selon où on clique) | ❌ Non (toujours le même) |
| **Utilisation** | Identifier l'élément exact cliqué | Référencer le conteneur écouté |
| **Délégation** | ✅ Essentiel | Secondaire |
| **Équivalent** | - | `this` (en fonction normale) |

## Bonnes pratiques

### ✅ 1. Utiliser closest() pour les structures imbriquées

```javascript
// ✅ BIEN - Fonctionne même avec des enfants
container.addEventListener('click', (event) => {
    const item = event.target.closest('.item');
    if (item) {
        // Logique
    }
});

// ⚠️ FRAGILE - Échoue si on clique sur un enfant
container.addEventListener('click', (event) => {
    if (event.target.classList.contains('item')) {
        // Logique
    }
});
```

### ✅ 2. Utiliser la délégation pour les éléments dynamiques

```javascript
// ✅ BIEN - Fonctionne même pour les futurs éléments
parent.addEventListener('click', (event) => {
    if (event.target.matches('.bouton')) {
        // Fonctionne même si le bouton est ajouté après
    }
});
```

### ✅ 3. Vérifier que l'élément existe

```javascript
// ✅ BIEN
container.addEventListener('click', (event) => {
    const item = event.target.closest('.item');

    if (item) {
        // Safe : item existe
        const id = item.dataset.id;
    }
});
```

### ✅ 4. Utiliser currentTarget pour modifier le conteneur

```javascript
// ✅ BIEN - Modifier le conteneur
parent.addEventListener('click', (event) => {
    event.currentTarget.classList.toggle('actif');
});

// ❌ MAUVAIS - Modifie l'élément cliqué, pas le conteneur
parent.addEventListener('click', (event) => {
    event.target.classList.toggle('actif');
});
```

## Ce qu'il faut retenir

✅ **event.target** = l'élément qui a **réellement déclenché** l'événement

✅ **event.currentTarget** = l'élément sur lequel **addEventListener** est attaché

✅ **Ils peuvent être différents** à cause de la propagation des événements

✅ **Utilisez target** pour identifier l'élément cliqué

✅ **Utilisez currentTarget** pour référencer le conteneur écouté

✅ **closest()** est très utile pour gérer les structures imbriquées

✅ **La délégation d'événements** repose sur cette différence

✅ **Un seul écouteur** sur un parent peut gérer plusieurs enfants

## Dans la prochaine leçon

Maintenant que vous comprenez la différence entre `target` et `currentTarget`, nous allons explorer en profondeur la **propagation des événements** : bubbling et capturing.

Vous découvrirez :
- Comment les événements se propagent dans le DOM
- La différence entre bubbling et capturing
- Comment contrôler cette propagation
- Pourquoi c'est important pour la délégation

---


⏭️ [Propagation : bubbling et capturing](/05-javascript-moderne-fondamentaux/10-evenements/08-propagation.md)
