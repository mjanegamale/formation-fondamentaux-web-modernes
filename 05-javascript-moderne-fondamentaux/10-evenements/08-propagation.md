🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.8 - Propagation : bubbling et capturing

## Introduction

Quand vous cliquez sur un élément dans une page web, quelque chose de fascinant se produit : l'événement ne reste pas uniquement sur cet élément, il **voyage** à travers le DOM. Ce voyage s'appelle la **propagation des événements**.

Comprendre la propagation est essentiel pour :
- Maîtriser la délégation d'événements
- Éviter les comportements inattendus
- Contrôler précisément vos interactions

Dans cette leçon, nous allons explorer en détail ce mécanisme.

## Qu'est-ce que la propagation ?

### Définition simple

Quand un événement se produit sur un élément, il ne se déclenche pas uniquement sur cet élément, mais aussi sur **tous ses ancêtres** (parents, grands-parents, etc.).

### Analogie du monde réel

Imaginez que vous jetez une pierre dans un lac :
1. **Impact** : La pierre touche l'eau (l'élément cliqué)
2. **Ondes** : Des cercles se forment et s'étendent vers l'extérieur (propagation)
3. **Bord du lac** : Les ondes atteignent finalement le bord (document)

De la même manière, un clic se propage de l'élément cliqué jusqu'à la racine du document.

## Les trois phases de propagation

Un événement passe par **trois phases** distinctes :

### 1. Phase de Capturing (Descente) 📥

L'événement **descend** du document vers l'élément cible.

```
Document
  ↓
Body
  ↓
Parent
  ↓
Élément cliqué (TARGET)
```

### 2. Phase Target (Cible) 🎯

L'événement atteint **l'élément réellement cliqué**.

### 3. Phase de Bubbling (Remontée) 📤

L'événement **remonte** de l'élément cible vers le document.

```
Élément cliqué (TARGET)
  ↑
Parent
  ↑
Body
  ↑
Document
```

### Schéma complet

```
PHASE 1: CAPTURING (Descente)        PHASE 3: BUBBLING (Remontée)
─────────────────────────             ─────────────────────────
Document
  ↓                                     ↑
Body                                  Body
  ↓                                     ↑
Container                             Container
  ↓                                     ↑
Button ←───── PHASE 2: TARGET ─────→ Button
```

## Le Bubbling (Remontée) - Comportement par défaut

Par défaut, les événements utilisent la phase de **bubbling** (remontée). C'est le comportement le plus courant et le plus utile.

### Exemple simple

```html
<div id="grand-parent" style="padding: 40px; background: lightblue;">
    GRAND-PARENT
    <div id="parent" style="padding: 30px; background: lightgreen;">
        PARENT
        <button id="enfant">ENFANT</button>
    </div>
</div>
```

```javascript
const grandParent = document.getElementById('grand-parent');
const parent = document.getElementById('parent');
const enfant = document.getElementById('enfant');

grandParent.addEventListener('click', () => {
    console.log('3. Grand-parent cliqué');
});

parent.addEventListener('click', () => {
    console.log('2. Parent cliqué');
});

enfant.addEventListener('click', () => {
    console.log('1. Enfant cliqué');
});
```

**Si vous cliquez sur le bouton ENFANT, la console affichera :**
```
1. Enfant cliqué
2. Parent cliqué
3. Grand-parent cliqué
```

L'événement **remonte** (bubble) de l'enfant vers les parents !

### Pourquoi c'est utile ?

Cette remontée permet la **délégation d'événements** que nous avons vue dans la leçon précédente :

```javascript
// Un seul écouteur sur le parent
parent.addEventListener('click', (event) => {
    console.log('Élément cliqué :', event.target.id);
});

// Fonctionne pour tous les enfants, même ajoutés dynamiquement !
```

## Visualisation interactive du bubbling

```html
<div id="niveau1" style="padding: 50px; background: #ffcccc;">
    Niveau 1
    <div id="niveau2" style="padding: 40px; background: #ffeecc;">
        Niveau 2
        <div id="niveau3" style="padding: 30px; background: #ffffcc;">
            Niveau 3
            <button id="niveau4">Cliquez-moi</button>
        </div>
    </div>
</div>
<ul id="log"></ul>
```

```javascript
const niveau1 = document.getElementById('niveau1');
const niveau2 = document.getElementById('niveau2');
const niveau3 = document.getElementById('niveau3');
const niveau4 = document.getElementById('niveau4');
const log = document.getElementById('log');

function ajouterLog(message) {
    const li = document.createElement('li');
    li.textContent = message;
    log.appendChild(li);
}

niveau1.addEventListener('click', () => {
    ajouterLog('4️⃣ Niveau 1 - Remontée finale');
});

niveau2.addEventListener('click', () => {
    ajouterLog('3️⃣ Niveau 2 - Remontée');
});

niveau3.addEventListener('click', () => {
    ajouterLog('2️⃣ Niveau 3 - Remontée');
});

niveau4.addEventListener('click', () => {
    ajouterLog('1️⃣ Bouton - Clic initial');
    log.innerHTML = ''; // Réinitialiser avant d'afficher
});
```

## Le Capturing (Descente) - Moins utilisé

Le capturing permet d'écouter un événement pendant sa **descente**, avant qu'il n'atteigne la cible.

### Comment activer le capturing ?

Il faut passer `true` (ou `{capture: true}`) comme troisième paramètre à `addEventListener` :

```javascript
element.addEventListener('click', fonction, true);
// ou
element.addEventListener('click', fonction, { capture: true });
```

### Exemple de capturing

```html
<div id="parent" style="padding: 30px; background: lightblue;">
    PARENT
    <button id="enfant">ENFANT</button>
</div>
```

```javascript
const parent = document.getElementById('parent');
const enfant = document.getElementById('enfant');

// Écouteur en CAPTURING (descente)
parent.addEventListener('click', () => {
    console.log('1. Parent (CAPTURING - descente)');
}, true);

// Écouteur normal (bubbling)
enfant.addEventListener('click', () => {
    console.log('2. Enfant (cible)');
});

// Écouteur en BUBBLING (remontée)
parent.addEventListener('click', () => {
    console.log('3. Parent (BUBBLING - remontée)');
});
```

**Résultat du clic sur ENFANT :**
```
1. Parent (CAPTURING - descente)
2. Enfant (cible)
3. Parent (BUBBLING - remontée)
```

### Ordre complet avec capturing et bubbling

```javascript
document.addEventListener('click', () => console.log('1. Document CAPTURING'), true);
parent.addEventListener('click', () => console.log('2. Parent CAPTURING'), true);
enfant.addEventListener('click', () => console.log('3. Enfant TARGET'));
parent.addEventListener('click', () => console.log('4. Parent BUBBLING'));
document.addEventListener('click', () => console.log('5. Document BUBBLING'));
```

**Ordre d'exécution :**
```
Descente (Capturing):    1. Document → 2. Parent
Cible:                   3. Enfant
Remontée (Bubbling):     4. Parent → 5. Document
```

## Contrôler la propagation

### stopPropagation() - Arrêter la propagation

Cette méthode **arrête** la propagation de l'événement (empêche la remontée ou la descente).

```javascript
enfant.addEventListener('click', (event) => {
    console.log('Enfant cliqué');
    event.stopPropagation(); // Arrêter la propagation
});

parent.addEventListener('click', () => {
    console.log('Parent cliqué'); // Ne s'exécutera PAS
});
```

#### Exemple pratique : Modal qui ne se ferme pas au clic interne

```html
<div id="overlay" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5);">
    <div id="modal" style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 20px;">
        <h2>Ma Modal</h2>
        <p>Contenu de la modal</p>
        <button id="fermer">Fermer</button>
    </div>
</div>
```

```javascript
const overlay = document.getElementById('overlay');
const modal = document.getElementById('modal');
const fermer = document.getElementById('fermer');

// Fermer au clic sur l'overlay
overlay.addEventListener('click', () => {
    overlay.style.display = 'none';
    console.log('Modal fermée');
});

// Empêcher la fermeture au clic sur la modal elle-même
modal.addEventListener('click', (event) => {
    event.stopPropagation(); // Le clic ne remonte pas à overlay
    console.log('Clic sur la modal (ne ferme pas)');
});

// Fermer avec le bouton
fermer.addEventListener('click', () => {
    overlay.style.display = 'none';
});
```

### stopImmediatePropagation() - Arrêter tout

Cette méthode arrête la propagation **ET** empêche les autres écouteurs **sur le même élément** de s'exécuter.

```javascript
const bouton = document.getElementById('bouton');

bouton.addEventListener('click', (event) => {
    console.log('Premier écouteur');
    event.stopImmediatePropagation();
});

bouton.addEventListener('click', () => {
    console.log('Deuxième écouteur'); // Ne s'exécutera JAMAIS
});

parent.addEventListener('click', () => {
    console.log('Parent'); // Ne s'exécutera pas non plus
});
```

**Résultat :**
```
Premier écouteur
(Tout s'arrête)
```

### Différence stopPropagation vs stopImmediatePropagation

```javascript
const element = document.getElementById('element');

// Exemple avec stopPropagation
element.addEventListener('click', (event) => {
    console.log('1. Premier');
    event.stopPropagation();
});

element.addEventListener('click', () => {
    console.log('2. Deuxième'); // S'EXÉCUTE
});

parent.addEventListener('click', () => {
    console.log('3. Parent'); // NE s'exécute PAS
});

// Résultat : 1, 2
```

```javascript
// Exemple avec stopImmediatePropagation
element.addEventListener('click', (event) => {
    console.log('1. Premier');
    event.stopImmediatePropagation();
});

element.addEventListener('click', () => {
    console.log('2. Deuxième'); // NE s'exécute PAS
});

parent.addEventListener('click', () => {
    console.log('3. Parent'); // NE s'exécute PAS
});

// Résultat : 1 seulement
```

## Cas pratiques de la propagation

### Cas 1 : Menu déroulant

```html
<div id="menu">
    <button id="btnMenu">Menu</button>
    <ul id="sousMenu" style="display: none;">
        <li>Option 1</li>
        <li>Option 2</li>
        <li>Option 3</li>
    </ul>
</div>
```

```javascript
const btnMenu = document.getElementById('btnMenu');
const sousMenu = document.getElementById('sousMenu');
const menu = document.getElementById('menu');

// Ouvrir le menu
btnMenu.addEventListener('click', (event) => {
    event.stopPropagation(); // Empêcher la fermeture immédiate
    sousMenu.style.display = 'block';
});

// Empêcher la fermeture au clic dans le menu
menu.addEventListener('click', (event) => {
    event.stopPropagation();
});

// Fermer au clic ailleurs
document.addEventListener('click', () => {
    sousMenu.style.display = 'none';
});
```

### Cas 2 : Liste de tâches avec délégation

```html
<ul id="listeTaches">
    <li>
        <span class="texte">Tâche 1</span>
        <button class="supprimer">✕</button>
    </li>
    <li>
        <span class="texte">Tâche 2</span>
        <button class="supprimer">✕</button>
    </li>
</ul>
```

```javascript
const liste = document.getElementById('listeTaches');

liste.addEventListener('click', (event) => {
    // Supprimer la tâche
    if (event.target.classList.contains('supprimer')) {
        event.stopPropagation(); // Empêcher le basculement
        event.target.closest('li').remove();
    }

    // Basculer terminée/non terminée
    if (event.target.classList.contains('texte')) {
        event.target.style.textDecoration =
            event.target.style.textDecoration === 'line-through' ? 'none' : 'line-through';
    }
});
```

### Cas 3 : Carte cliquable avec bouton d'action

```html
<div class="carte" data-id="1">
    <h3>Titre de la carte</h3>
    <p>Description...</p>
    <button class="action">Action spéciale</button>
</div>
```

```javascript
const carte = document.querySelector('.carte');

// Clic sur la carte entière
carte.addEventListener('click', () => {
    console.log('Carte cliquée - Ouvrir détails');
    window.location.href = '/details/1';
});

// Clic sur le bouton (empêcher l'ouverture des détails)
carte.querySelector('.action').addEventListener('click', (event) => {
    event.stopPropagation(); // Ne pas déclencher le clic de la carte
    console.log('Action spéciale uniquement');
    // Faire quelque chose de différent
});
```

## Événements qui ne "bubble" pas

Certains événements **ne remontent pas** naturellement :

- `focus` (utilisez `focusin` pour le bubbling)
- `blur` (utilisez `focusout` pour le bubbling)
- `mouseenter` (utilisez `mouseover` pour le bubbling)
- `mouseleave` (utilisez `mouseout` pour le bubbling)
- `load`
- `unload`
- `scroll` (dans certains cas)

### Exemple : focus vs focusin

```javascript
// focus ne remonte PAS
parent.addEventListener('focus', () => {
    console.log('Ne se déclenchera pas'); // ❌
});

// focusin remonte
parent.addEventListener('focusin', () => {
    console.log('Se déclenchera !'); // ✅
});
```

## Vérifier si un événement remonte

Vous pouvez vérifier la propriété `bubbles` de l'objet Event :

```javascript
element.addEventListener('click', (event) => {
    console.log('Cet événement remonte ?', event.bubbles); // true
});

input.addEventListener('focus', (event) => {
    console.log('Focus remonte ?', event.bubbles); // false
});
```

## Exemples pratiques complets

### Exemple 1 : Système d'onglets

```html
<div id="tabs">
    <div class="tabs-header">
        <button class="tab-btn actif" data-tab="tab1">Onglet 1</button>
        <button class="tab-btn" data-tab="tab2">Onglet 2</button>
        <button class="tab-btn" data-tab="tab3">Onglet 3</button>
    </div>
    <div class="tabs-content">
        <div id="tab1" class="tab-pane actif">Contenu 1</div>
        <div id="tab2" class="tab-pane">Contenu 2</div>
        <div id="tab3" class="tab-pane">Contenu 3</div>
    </div>
</div>
```

```javascript
const tabsHeader = document.querySelector('.tabs-header');

// Délégation d'événements grâce au bubbling
tabsHeader.addEventListener('click', (event) => {
    const bouton = event.target.closest('.tab-btn');

    if (bouton) {
        const tabId = bouton.dataset.tab;

        // Retirer la classe actif de tous les boutons
        tabsHeader.querySelectorAll('.tab-btn').forEach(btn => {
            btn.classList.remove('actif');
        });

        // Ajouter la classe actif au bouton cliqué
        bouton.classList.add('actif');

        // Gérer les panneaux
        document.querySelectorAll('.tab-pane').forEach(pane => {
            pane.classList.remove('actif');
        });

        document.getElementById(tabId).classList.add('actif');
    }
});
```

### Exemple 2 : Gestionnaire de drag and drop simplifié

```html
<div id="zone-drag" style="padding: 20px; border: 2px dashed #ccc;">
    <div class="item draggable" draggable="true">Item 1</div>
    <div class="item draggable" draggable="true">Item 2</div>
    <div class="item draggable" draggable="true">Item 3</div>
</div>
```

```javascript
const zone = document.getElementById('zone-drag');
let elementGlisse = null;

// Utiliser la délégation grâce au bubbling
zone.addEventListener('dragstart', (event) => {
    if (event.target.classList.contains('draggable')) {
        elementGlisse = event.target;
        event.target.style.opacity = '0.5';
    }
});

zone.addEventListener('dragend', (event) => {
    if (event.target.classList.contains('draggable')) {
        event.target.style.opacity = '1';
    }
});

zone.addEventListener('dragover', (event) => {
    event.preventDefault(); // Permettre le drop
});

zone.addEventListener('drop', (event) => {
    event.preventDefault();

    if (event.target.classList.contains('item') && event.target !== elementGlisse) {
        // Échanger les positions
        const tous = Array.from(zone.querySelectorAll('.item'));
        const indexGlisse = tous.indexOf(elementGlisse);
        const indexCible = tous.indexOf(event.target);

        if (indexGlisse < indexCible) {
            event.target.after(elementGlisse);
        } else {
            event.target.before(elementGlisse);
        }
    }
});
```

### Exemple 3 : Système de notifications avec fermeture

```html
<div id="conteneur-notifications"></div>
<button id="ajouterNotif">Ajouter une notification</button>
```

```javascript
const conteneur = document.getElementById('conteneur-notifications');
const btnAjouter = document.getElementById('ajouterNotif');
let compteur = 0;

// Ajouter une notification
btnAjouter.addEventListener('click', () => {
    compteur++;
    const notif = document.createElement('div');
    notif.className = 'notification';
    notif.innerHTML = `
        <span>Notification ${compteur}</span>
        <button class="fermer">✕</button>
    `;
    conteneur.appendChild(notif);
});

// Délégation pour gérer toutes les fermetures
conteneur.addEventListener('click', (event) => {
    if (event.target.classList.contains('fermer')) {
        event.stopPropagation(); // Empêcher d'autres actions
        event.target.closest('.notification').remove();
    }
});
```

## Debugging de la propagation

Voici un outil pratique pour visualiser la propagation :

```html
<div id="debug-zone">
    <div id="d1" style="padding: 40px; background: #ffcccc;">
        D1
        <div id="d2" style="padding: 30px; background: #ccffcc;">
            D2
            <button id="d3">D3</button>
        </div>
    </div>
</div>
<ul id="debug-log"></ul>
<button id="reset">Réinitialiser</button>
```

```javascript
const zone = document.getElementById('debug-zone');
const log = document.getElementById('debug-log');
const reset = document.getElementById('reset');

function logger(message, phase) {
    const li = document.createElement('li');
    li.textContent = `${phase}: ${message}`;
    li.style.color = phase === 'CAPTURE' ? 'blue' : 'green';
    log.appendChild(li);
}

// Capturing
zone.addEventListener('click', (e) => {
    logger(e.target.id, 'CAPTURE');
}, true);

document.getElementById('d1').addEventListener('click', (e) => {
    logger('D1', 'CAPTURE');
}, true);

document.getElementById('d2').addEventListener('click', (e) => {
    logger('D2', 'CAPTURE');
}, true);

document.getElementById('d3').addEventListener('click', (e) => {
    logger('D3 (TARGET)', 'TARGET');
});

// Bubbling
document.getElementById('d2').addEventListener('click', (e) => {
    logger('D2', 'BUBBLE');
});

document.getElementById('d1').addEventListener('click', (e) => {
    logger('D1', 'BUBBLE');
});

zone.addEventListener('click', (e) => {
    logger('Zone', 'BUBBLE');
});

reset.addEventListener('click', () => {
    log.innerHTML = '';
});
```

## Tableau récapitulatif

| Concept | Description | Usage |
|---------|-------------|-------|
| **Bubbling** | Remontée de l'élément vers document | Par défaut, très courant |
| **Capturing** | Descente du document vers l'élément | Rare, cas spécifiques |
| **Target phase** | L'événement atteint la cible | Automatique |
| **stopPropagation()** | Arrête la propagation | Empêcher remontée/descente |
| **stopImmediatePropagation()** | Arrête tout | Arrêter + autres écouteurs |
| **event.bubbles** | L'événement remonte-t-il ? | Vérification |

## Bonnes pratiques

### ✅ 1. Utiliser le bubbling par défaut (délégation)

```javascript
// ✅ BIEN - Un écouteur pour tous
parent.addEventListener('click', (event) => {
    if (event.target.matches('.item')) {
        // Gérer l'item
    }
});

// ❌ MOINS BIEN - Un écouteur par élément
items.forEach(item => {
    item.addEventListener('click', handleClick);
});
```

### ✅ 2. Utiliser stopPropagation() avec parcimonie

```javascript
// ✅ BON USAGE - Empêcher un comportement indésirable
modal.addEventListener('click', (event) => {
    event.stopPropagation(); // La modal ne doit pas fermer
});

// ⚠️ À ÉVITER - Peut casser d'autres fonctionnalités
element.addEventListener('click', (event) => {
    event.stopPropagation(); // Pourquoi ? Risque de bugs
});
```

### ✅ 3. Préférer la délégation au capturing

```javascript
// ✅ PRÉFÉRÉ - Bubbling avec délégation
parent.addEventListener('click', (event) => {
    // Logique
});

// ⚠️ RARE - Capturing (sauf besoin spécifique)
parent.addEventListener('click', (event) => {
    // Logique
}, true);
```

### ✅ 4. Documenter l'usage de stopPropagation()

```javascript
// ✅ BIEN - Expliquer pourquoi
modal.addEventListener('click', (event) => {
    // Empêcher la fermeture de la modal au clic interne
    event.stopPropagation();
});
```

## Ce qu'il faut retenir

✅ **Les événements se propagent** à travers le DOM en 3 phases

✅ **Bubbling (remontée)** : comportement par défaut, de l'élément vers document

✅ **Capturing (descente)** : du document vers l'élément, activé avec `true` ou `{capture: true}`

✅ **La délégation d'événements** repose sur le bubbling

✅ **stopPropagation()** : arrête la propagation

✅ **stopImmediatePropagation()** : arrête tout (propagation + autres écouteurs)

✅ **Certains événements ne remontent pas** (focus, blur, mouseenter, mouseleave)

✅ **Le bubbling permet d'optimiser** les performances (moins d'écouteurs)

## Dans la prochaine leçon

Maintenant que vous maîtrisez la propagation des événements, nous allons voir **preventDefault()** et **stopPropagation()** en détail, avec des cas pratiques concrets.

Vous découvrirez :
- Quand utiliser preventDefault()
- Quand utiliser stopPropagation()
- Les différences et les cas d'usage
- Les pièges à éviter

---


⏭️ [preventDefault() et stopPropagation()](/05-javascript-moderne-fondamentaux/10-evenements/09-preventdefault-stoppropagation.md)
