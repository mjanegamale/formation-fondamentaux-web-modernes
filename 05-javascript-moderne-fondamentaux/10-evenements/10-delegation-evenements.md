🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.10 - Délégation d'événements

## Introduction

La **délégation d'événements** est une technique puissante et élégante qui consiste à attacher **un seul écouteur d'événement sur un élément parent** pour gérer les événements de **tous ses enfants**.

Cette technique repose sur la **propagation des événements** (bubbling) que nous avons vue dans les leçons précédentes. C'est l'une des optimisations les plus importantes en JavaScript moderne.

## Le problème : Approche directe

### Sans délégation (❌ Inefficace)

Imaginons une liste de tâches où chaque tâche a un bouton "Supprimer" :

```html
<ul id="listeTaches">
    <li>Tâche 1 <button class="supprimer">✕</button></li>
    <li>Tâche 2 <button class="supprimer">✕</button></li>
    <li>Tâche 3 <button class="supprimer">✕</button></li>
    <li>Tâche 4 <button class="supprimer">✕</button></li>
    <li>Tâche 5 <button class="supprimer">✕</button></li>
</ul>
```

```javascript
// ❌ APPROCHE DIRECTE : Un écouteur par bouton
const boutons = document.querySelectorAll('.supprimer');

boutons.forEach(bouton => {
    bouton.addEventListener('click', () => {
        bouton.parentElement.remove();
    });
});
```

### Problèmes de cette approche :

1. **Performance** : 5 tâches = 5 écouteurs. 100 tâches = 100 écouteurs !
2. **Mémoire** : Chaque écouteur consomme de la mémoire
3. **Éléments dynamiques** : Si vous ajoutez une nouvelle tâche, elle n'aura PAS d'écouteur

```javascript
// Ajouter une nouvelle tâche
const nouvelleTache = document.createElement('li');
nouvelleTache.innerHTML = 'Tâche 6 <button class="supprimer">✕</button>';
liste.appendChild(nouvelleTache);

// ❌ Le nouveau bouton ne fonctionne PAS !
// Il faudrait réattacher l'événement manuellement
```

## La solution : Délégation d'événements

### Avec délégation (✅ Efficace)

```javascript
// ✅ DÉLÉGATION : Un seul écouteur sur le parent
const liste = document.getElementById('listeTaches');

liste.addEventListener('click', (event) => {
    // Vérifier si le clic est sur un bouton .supprimer
    if (event.target.classList.contains('supprimer')) {
        event.target.parentElement.remove();
    }
});
```

### Avantages :

1. **Performance** : 1 seul écouteur pour 100 tâches
2. **Mémoire** : Consommation minimale
3. **Éléments dynamiques** : Fonctionne automatiquement pour les nouveaux éléments !

```javascript
// Ajouter une nouvelle tâche
const nouvelleTache = document.createElement('li');
nouvelleTache.innerHTML = 'Tâche 6 <button class="supprimer">✕</button>';
liste.appendChild(nouvelleTache);

// ✅ Le nouveau bouton fonctionne immédiatement !
// Aucun code supplémentaire nécessaire
```

## Comment ça fonctionne ?

### Le mécanisme

Grâce au **bubbling** (remontée des événements), quand vous cliquez sur un bouton enfant, l'événement remonte jusqu'au parent où se trouve l'écouteur.

```
Clic sur bouton "Supprimer"
         ↓
L'événement se propage (bubble)
         ↓
         ↓
         ↓
Arrive au <ul> (parent)
         ↓
L'écouteur sur <ul> se déclenche
         ↓
On vérifie event.target
         ↓
C'est bien un bouton .supprimer ?
         ↓
OUI → Supprimer la tâche
```

### Schéma visuel

```
┌────────────────────────────────────────┐
│  <ul> ← addEventListener est ici       │
│                                        │
│  ┌─────────────────────────────────┐   │
│  │ <li> Tâche 1                    │   │
│  │   <button class="supprimer">    │   │
│  │     ✕ ← Clic ici                │   │
│  │   </button>                     │   │
│  │ </li>                           │   │
│  └─────────────────────────────────┘   │
│                                        │
│  ┌─────────────────────────────────┐   │
│  │ <li> Tâche 2                    │   │
│  │   <button class="supprimer">    │   │
│  │   </button>                     │   │
│  │ </li>                           │   │
│  └─────────────────────────────────┘   │
│                                        │
└────────────────────────────────────────┘

L'événement remonte (bubble) du bouton vers <ul>
<ul> vérifie event.target et réagit en conséquence
```

## Exemples pratiques progressifs

### Exemple 1 : Liste de tâches complète

```html
<div id="app">
    <input type="text" id="nouvelleTache" placeholder="Nouvelle tâche">
    <button id="ajouter">Ajouter</button>
    <ul id="listeTaches"></ul>
</div>
```

```javascript
const app = document.getElementById('app');
const input = document.getElementById('nouvelleTache');
const liste = document.getElementById('listeTaches');

// Délégation sur tout l'app
app.addEventListener('click', (event) => {
    const target = event.target;

    // Ajouter une tâche
    if (target.id === 'ajouter') {
        const texte = input.value.trim();
        if (texte) {
            const li = document.createElement('li');
            li.innerHTML = `
                <span class="texte">${texte}</span>
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

    // Basculer terminée/non terminée
    if (target.classList.contains('texte')) {
        target.style.textDecoration =
            target.style.textDecoration === 'line-through' ? 'none' : 'line-through';
    }
});

// Ajouter avec Enter
input.addEventListener('keydown', (event) => {
    if (event.key === 'Enter') {
        document.getElementById('ajouter').click();
    }
});
```

**Avantages de cet exemple :**
- ✅ Un seul écouteur pour toute l'application
- ✅ Fonctionne pour les tâches futures
- ✅ Code centralisé et facile à maintenir

### Exemple 2 : Galerie d'images dynamique

```html
<div id="galerie"></div>
<button id="ajouterImage">Ajouter une image</button>
```

```javascript
const galerie = document.getElementById('galerie');
const btnAjouter = document.getElementById('ajouterImage');
let compteur = 0;

// Ajouter des images
btnAjouter.addEventListener('click', () => {
    compteur++;
    const img = document.createElement('div');
    img.className = 'image-card';
    img.innerHTML = `
        <img src="https://picsum.photos/200/200?random=${compteur}" alt="Image ${compteur}">
        <button class="supprimer">Supprimer</button>
        <button class="agrandir">🔍 Agrandir</button>
    `;
    galerie.appendChild(img);
});

// Délégation pour gérer tous les boutons
galerie.addEventListener('click', (event) => {
    const carte = event.target.closest('.image-card');
    if (!carte) return;

    // Supprimer l'image
    if (event.target.classList.contains('supprimer')) {
        carte.remove();
    }

    // Agrandir l'image
    if (event.target.classList.contains('agrandir')) {
        const img = carte.querySelector('img');
        alert(`Affichage de : ${img.alt}`);
        // Ici, vous pourriez ouvrir une lightbox
    }
});
```

### Exemple 3 : Tableau avec actions multiples

```html
<table id="tableau">
    <thead>
        <tr>
            <th>Nom</th>
            <th>Email</th>
            <th>Actions</th>
        </tr>
    </thead>
    <tbody id="tableauBody">
        <tr data-id="1">
            <td class="nom">Alice</td>
            <td class="email">alice@example.com</td>
            <td>
                <button class="modifier">✏️</button>
                <button class="supprimer">🗑️</button>
            </td>
        </tr>
        <tr data-id="2">
            <td class="nom">Bob</td>
            <td class="email">bob@example.com</td>
            <td>
                <button class="modifier">✏️</button>
                <button class="supprimer">🗑️</button>
            </td>
        </tr>
    </tbody>
</table>
```

```javascript
const tableauBody = document.getElementById('tableauBody');

// Un seul écouteur pour toutes les actions
tableauBody.addEventListener('click', (event) => {
    const target = event.target;
    const ligne = target.closest('tr');

    if (!ligne) return;

    const id = ligne.dataset.id;
    const nom = ligne.querySelector('.nom').textContent;
    const email = ligne.querySelector('.email').textContent;

    // Modifier
    if (target.classList.contains('modifier')) {
        console.log(`Modifier : ${nom} (ID: ${id})`);

        const nouveauNom = prompt('Nouveau nom :', nom);
        const nouveauEmail = prompt('Nouvel email :', email);

        if (nouveauNom && nouveauEmail) {
            ligne.querySelector('.nom').textContent = nouveauNom;
            ligne.querySelector('.email').textContent = nouveauEmail;
        }
    }

    // Supprimer
    if (target.classList.contains('supprimer')) {
        if (confirm(`Supprimer ${nom} ?`)) {
            ligne.remove();
            console.log(`Supprimé : ${nom} (ID: ${id})`);
        }
    }
});
```

## Utilisation de closest() pour les structures imbriquées

Quand vos éléments contiennent d'autres éléments (icônes, spans, etc.), utilisez `closest()` pour trouver l'élément parent.

### Problème avec des éléments imbriqués

```html
<button class="action">
    <i class="icone">🔥</i>
    <span>Texte du bouton</span>
</button>
```

```javascript
// ❌ PROBLÈME : event.target peut être <i> ou <span>
parent.addEventListener('click', (event) => {
    if (event.target.classList.contains('action')) {
        // Ne marche pas si on clique sur l'icône ou le span !
    }
});

// ✅ SOLUTION : Utiliser closest()
parent.addEventListener('click', (event) => {
    const bouton = event.target.closest('.action');
    if (bouton) {
        // Fonctionne peu importe où on clique dans le bouton
        console.log('Bouton cliqué !');
    }
});
```

### Exemple pratique : Cartes produits

```html
<div id="produits">
    <div class="carte-produit" data-id="1">
        <img src="produit1.jpg" alt="Produit 1">
        <h3>Produit 1</h3>
        <p class="prix">29.99€</p>
        <button class="ajouter-panier">
            <span class="icone">🛒</span>
            <span class="texte">Ajouter au panier</span>
        </button>
    </div>
    <div class="carte-produit" data-id="2">
        <img src="produit2.jpg" alt="Produit 2">
        <h3>Produit 2</h3>
        <p class="prix">39.99€</p>
        <button class="ajouter-panier">
            <span class="icone">🛒</span>
            <span class="texte">Ajouter au panier</span>
        </button>
    </div>
</div>
```

```javascript
const produits = document.getElementById('produits');

produits.addEventListener('click', (event) => {
    // Trouver le bouton parent, peu importe où on clique
    const bouton = event.target.closest('.ajouter-panier');

    if (bouton) {
        // Trouver la carte produit
        const carte = bouton.closest('.carte-produit');
        const id = carte.dataset.id;
        const nom = carte.querySelector('h3').textContent;
        const prix = carte.querySelector('.prix').textContent;

        console.log(`Ajouté au panier : ${nom} - ${prix}`);

        // Animation du bouton
        bouton.textContent = '✓ Ajouté !';
        setTimeout(() => {
            bouton.innerHTML = `
                <span class="icone">🛒</span>
                <span class="texte">Ajouter au panier</span>
            `;
        }, 2000);
    }
});
```

## Comparaison : Avec vs Sans délégation

### Scénario : 1000 boutons

#### Sans délégation (❌)

```javascript
// 1000 écouteurs d'événements
const boutons = document.querySelectorAll('.bouton'); // 1000 boutons

boutons.forEach(bouton => {
    bouton.addEventListener('click', handleClick);
});

// Problèmes :
// - 1000 écouteurs en mémoire
// - Si on ajoute un bouton dynamiquement, il faut réattacher
// - Code dupliqué
```

**Consommation mémoire** : ~1000 × (taille d'un écouteur) = Beaucoup !

#### Avec délégation (✅)

```javascript
// 1 seul écouteur
const conteneur = document.getElementById('conteneur');

conteneur.addEventListener('click', (event) => {
    if (event.target.classList.contains('bouton')) {
        handleClick(event);
    }
});

// Avantages :
// - 1 écouteur en mémoire
// - Fonctionne pour les boutons dynamiques
// - Code centralisé
```

**Consommation mémoire** : 1 écouteur = Minimal !

### Tableau comparatif

| Critère | Sans délégation | Avec délégation |
|---------|-----------------|-----------------|
| **Écouteurs** | Un par élément (100+) | Un seul sur le parent |
| **Mémoire** | Élevée | Minimale |
| **Performance** | Lente (nombreux écouteurs) | Rapide (1 écouteur) |
| **Éléments dynamiques** | ❌ Ne fonctionne pas | ✅ Fonctionne automatiquement |
| **Maintenance** | Difficile (code dupliqué) | Facile (code centralisé) |
| **Complexité** | Simple à comprendre | Requiert compréhension du bubbling |

## Cas d'usage avancés

### Exemple 1 : Menu avec sous-menus

```html
<nav id="menu">
    <ul>
        <li class="menu-item">
            <a href="#" class="lien">Produits</a>
            <ul class="sous-menu">
                <li><a href="#" class="lien">Catégorie 1</a></li>
                <li><a href="#" class="lien">Catégorie 2</a></li>
            </ul>
        </li>
        <li class="menu-item">
            <a href="#" class="lien">Services</a>
            <ul class="sous-menu">
                <li><a href="#" class="lien">Service 1</a></li>
                <li><a href="#" class="lien">Service 2</a></li>
            </ul>
        </li>
    </ul>
</nav>
```

```javascript
const menu = document.getElementById('menu');

menu.addEventListener('click', (event) => {
    // Empêcher la navigation par défaut
    if (event.target.classList.contains('lien')) {
        event.preventDefault();
    }

    // Gérer le menu principal
    const menuItem = event.target.closest('.menu-item > .lien');
    if (menuItem) {
        const sousMenu = menuItem.nextElementSibling;

        // Fermer tous les autres sous-menus
        menu.querySelectorAll('.sous-menu').forEach(sm => {
            if (sm !== sousMenu) {
                sm.style.display = 'none';
            }
        });

        // Basculer le sous-menu actuel
        sousMenu.style.display =
            sousMenu.style.display === 'block' ? 'none' : 'block';
    }

    // Gérer les liens des sous-menus
    const sousMenuLien = event.target.closest('.sous-menu .lien');
    if (sousMenuLien) {
        console.log('Navigation vers :', sousMenuLien.textContent);
        // Fermer tous les sous-menus
        menu.querySelectorAll('.sous-menu').forEach(sm => {
            sm.style.display = 'none';
        });
    }
});
```

### Exemple 2 : Liste triable (Drag & Drop)

```html
<ul id="listeTri">
    <li class="item" draggable="true" data-id="1">Item 1</li>
    <li class="item" draggable="true" data-id="2">Item 2</li>
    <li class="item" draggable="true" data-id="3">Item 3</li>
    <li class="item" draggable="true" data-id="4">Item 4</li>
</ul>
```

```javascript
const liste = document.getElementById('listeTri');
let elementGlisse = null;

// Délégation pour tous les événements de drag
liste.addEventListener('dragstart', (event) => {
    if (event.target.classList.contains('item')) {
        elementGlisse = event.target;
        event.target.style.opacity = '0.5';
    }
});

liste.addEventListener('dragend', (event) => {
    if (event.target.classList.contains('item')) {
        event.target.style.opacity = '1';
    }
});

liste.addEventListener('dragover', (event) => {
    event.preventDefault();

    const cible = event.target.closest('.item');
    if (cible && cible !== elementGlisse) {
        const rect = cible.getBoundingClientRect();
        const milieu = rect.top + rect.height / 2;

        if (event.clientY < milieu) {
            liste.insertBefore(elementGlisse, cible);
        } else {
            liste.insertBefore(elementGlisse, cible.nextSibling);
        }
    }
});
```

### Exemple 3 : Formulaire dynamique

```html
<div id="formulaireDynamique">
    <div id="champs"></div>
    <button class="ajouter-champ">+ Ajouter un champ</button>
    <button class="soumettre">Soumettre</button>
</div>
```

```javascript
const form = document.getElementById('formulaireDynamique');
const champsContainer = document.getElementById('champs');
let compteurChamps = 0;

// Délégation pour tout le formulaire
form.addEventListener('click', (event) => {
    const target = event.target;

    // Ajouter un champ
    if (target.classList.contains('ajouter-champ')) {
        compteurChamps++;
        const champWrapper = document.createElement('div');
        champWrapper.className = 'champ-wrapper';
        champWrapper.innerHTML = `
            <input type="text" name="champ${compteurChamps}" placeholder="Champ ${compteurChamps}">
            <button class="supprimer-champ">✕</button>
        `;
        champsContainer.appendChild(champWrapper);
    }

    // Supprimer un champ
    if (target.classList.contains('supprimer-champ')) {
        target.parentElement.remove();
    }

    // Soumettre
    if (target.classList.contains('soumettre')) {
        const inputs = champsContainer.querySelectorAll('input');
        const valeurs = Array.from(inputs).map(input => ({
            nom: input.name,
            valeur: input.value
        }));
        console.log('Valeurs soumises :', valeurs);
    }
});
```

## Délégation avec différents types d'événements

La délégation fonctionne avec tous les événements qui "remontent" (bubble).

### Événements de souris

```javascript
conteneur.addEventListener('mouseover', (event) => {
    const carte = event.target.closest('.carte');
    if (carte) {
        carte.style.boxShadow = '0 4px 8px rgba(0,0,0,0.2)';
    }
});

conteneur.addEventListener('mouseout', (event) => {
    const carte = event.target.closest('.carte');
    if (carte) {
        carte.style.boxShadow = '';
    }
});
```

### Événements de formulaire

```javascript
form.addEventListener('input', (event) => {
    if (event.target.matches('input[type="email"]')) {
        const email = event.target.value;
        const feedback = event.target.nextElementSibling;

        if (email.includes('@')) {
            feedback.textContent = '✓ Email valide';
            feedback.style.color = 'green';
        } else {
            feedback.textContent = '❌ Email invalide';
            feedback.style.color = 'red';
        }
    }
});

form.addEventListener('change', (event) => {
    if (event.target.matches('select')) {
        console.log('Sélection changée :', event.target.value);
    }
});
```

### Événements de clavier

```javascript
document.addEventListener('keydown', (event) => {
    // Raccourcis clavier globaux
    if (event.ctrlKey && event.key === 's') {
        event.preventDefault();
        console.log('Sauvegarder (Ctrl+S)');
    }

    // Raccourcis spécifiques aux champs
    if (event.target.matches('input[type="text"]')) {
        if (event.key === 'Escape') {
            event.target.value = '';
            event.target.blur();
        }
    }
});
```

## Patterns de vérification courants

### Pattern 1 : Vérification de classe

```javascript
parent.addEventListener('click', (event) => {
    if (event.target.classList.contains('bouton')) {
        // Action
    }
});
```

### Pattern 2 : Vérification de sélecteur (matches)

```javascript
parent.addEventListener('click', (event) => {
    if (event.target.matches('.bouton, button[type="submit"]')) {
        // Action pour plusieurs sélecteurs
    }
});
```

### Pattern 3 : Utilisation de closest()

```javascript
parent.addEventListener('click', (event) => {
    const element = event.target.closest('.element-recherche');
    if (element) {
        // Action avec element
    }
});
```

### Pattern 4 : Vérification multiple

```javascript
parent.addEventListener('click', (event) => {
    const target = event.target;

    if (target.matches('.bouton-1')) {
        // Action 1
    } else if (target.matches('.bouton-2')) {
        // Action 2
    } else if (target.closest('.carte')) {
        // Action 3
    }
});
```

### Pattern 5 : Early return pour clarté

```javascript
parent.addEventListener('click', (event) => {
    const bouton = event.target.closest('.bouton');

    // Early return si pas de bouton
    if (!bouton) return;

    // Le reste du code ne s'exécute que si bouton existe
    console.log('Bouton cliqué');
    bouton.classList.add('actif');
});
```

## Limites et pièges de la délégation

### Limite 1 : Événements qui ne remontent pas

Certains événements ne supportent pas le bubbling :

```javascript
// ❌ Ne fonctionne PAS avec délégation
parent.addEventListener('focus', (event) => {
    // focus ne remonte pas
});

// ✅ Solution : Utiliser focusin
parent.addEventListener('focusin', (event) => {
    // focusin remonte
    if (event.target.matches('input')) {
        console.log('Input a le focus');
    }
});
```

**Liste des événements qui ne remontent pas :**
- `focus` → utiliser `focusin`
- `blur` → utiliser `focusout`
- `mouseenter` → utiliser `mouseover`
- `mouseleave` → utiliser `mouseout`
- `load`, `unload`, `scroll` (dans certains cas)

### Piège 2 : Vérification incorrecte

```javascript
// ❌ FAUX : event.target peut être un enfant
parent.addEventListener('click', (event) => {
    if (event.target.classList.contains('carte')) {
        // Ne marche pas si on clique sur un enfant de .carte
    }
});

// ✅ CORRECT : Utiliser closest()
parent.addEventListener('click', (event) => {
    const carte = event.target.closest('.carte');
    if (carte) {
        // Fonctionne peu importe où on clique dans .carte
    }
});
```

### Piège 3 : Oublier de vérifier

```javascript
// ❌ DANGEREUX : Pas de vérification
parent.addEventListener('click', (event) => {
    event.target.remove(); // Supprime N'IMPORTE quel élément cliqué !
});

// ✅ SÉCURISÉ : Toujours vérifier
parent.addEventListener('click', (event) => {
    if (event.target.classList.contains('supprimable')) {
        event.target.remove();
    }
});
```

### Piège 4 : Déléguer trop haut

```javascript
// ⚠️ PEU PERFORMANT : Délégation sur document
document.addEventListener('click', (event) => {
    // Cet événement se déclenche pour TOUS les clics de la page
    if (event.target.matches('.bouton-specifique')) {
        // Action
    }
});

// ✅ MEILLEUR : Délégation sur le parent le plus proche
const conteneur = document.getElementById('conteneur-boutons');
conteneur.addEventListener('click', (event) => {
    if (event.target.matches('.bouton-specifique')) {
        // Action
    }
});
```

## Bonnes pratiques

### ✅ 1. Déléguer au parent le plus proche

```javascript
// ✅ BIEN : Délégation sur le conteneur direct
const liste = document.getElementById('liste');
liste.addEventListener('click', handleClick);

// ⚠️ MOINS BIEN : Délégation trop haute
document.addEventListener('click', handleClick);
```

### ✅ 2. Toujours utiliser closest() pour les structures imbriquées

```javascript
// ✅ ROBUSTE
parent.addEventListener('click', (event) => {
    const bouton = event.target.closest('.bouton');
    if (bouton) {
        // Fonctionne toujours
    }
});
```

### ✅ 3. Utiliser des sélecteurs spécifiques

```javascript
// ✅ BIEN : Sélecteur spécifique
if (event.target.matches('.btn-supprimer')) { }

// ⚠️ RISQUÉ : Trop générique
if (event.target.tagName === 'BUTTON') { }
```

### ✅ 4. Early return pour clarté

```javascript
// ✅ CLAIR ET LISIBLE
parent.addEventListener('click', (event) => {
    const item = event.target.closest('.item');
    if (!item) return; // Sortir tôt

    // Code pour .item
    console.log('Item cliqué');
});
```

### ✅ 5. Documenter la délégation

```javascript
// ✅ BIEN DOCUMENTÉ
// Délégation d'événements pour gérer les boutons de suppression
// Fonctionne aussi pour les boutons ajoutés dynamiquement
liste.addEventListener('click', (event) => {
    if (event.target.matches('.btn-supprimer')) {
        // Logique de suppression
    }
});
```

## Quand utiliser la délégation ?

### ✅ Utilisez la délégation quand :

- Vous avez **beaucoup d'éléments similaires** (listes, tableaux, grilles)
- Les éléments sont **ajoutés dynamiquement**
- Vous voulez **optimiser les performances**
- Vous voulez **centraliser la logique**

### ⚠️ N'utilisez PAS la délégation quand :

- Vous avez **un seul élément** (attachez directement)
- L'événement **ne remonte pas** (focus, blur, etc.)
- La logique est **très différente** pour chaque élément
- Vous devez **capturer** l'événement (phase de descente)

## Ce qu'il faut retenir

✅ **La délégation** = un écouteur sur le parent pour gérer tous les enfants

✅ **Repose sur le bubbling** : les événements remontent

✅ **Avantages principaux** : performance, mémoire, éléments dynamiques

✅ **Utiliser event.target** pour identifier l'élément cliqué

✅ **Utiliser closest()** pour les structures imbriquées

✅ **Vérifier toujours** avant d'agir (if, matches, closest)

✅ **Déléguer au parent le plus proche**, pas au document

✅ **Certains événements ne remontent pas** (focus → focusin, blur → focusout)

## Dans la prochaine leçon

Maintenant que vous maîtrisez la délégation d'événements, nous allons voir comment **retirer des écouteurs d'événements** avec `removeEventListener()`.

Vous découvrirez :
- Pourquoi et quand retirer des événements
- La syntaxe exacte de removeEventListener()
- Les pièges courants (fonctions anonymes)
- La gestion de la mémoire
- Les bonnes pratiques de nettoyage

---


⏭️ [removeEventListener](/05-javascript-moderne-fondamentaux/10-evenements/11-removeeventlistener.md)
