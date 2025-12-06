🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.6 - L'objet Event et ses propriétés

## Introduction

Chaque fois qu'un événement se produit dans le navigateur (clic, touche pressée, soumission de formulaire, etc.), JavaScript crée automatiquement un **objet Event** qui contient toutes les informations sur cet événement.

Cet objet est extrêmement utile car il nous permet de savoir :
- **Quel** élément a déclenché l'événement
- **Où** l'événement s'est produit (position de la souris, etc.)
- **Quelle** touche a été pressée
- Et bien d'autres informations...

Dans cette leçon, nous allons explorer en détail cet objet Event et ses propriétés les plus utiles.

## Qu'est-ce que l'objet Event ?

L'objet Event est un **objet JavaScript** automatiquement créé par le navigateur et **passé en paramètre** à votre fonction gestionnaire d'événement.

### Accéder à l'objet Event

Pour accéder à l'objet Event, il suffit de l'accepter comme paramètre dans votre fonction :

```javascript
element.addEventListener('click', function(event) {
    console.log(event); // L'objet Event complet
});
```

### Conventions de nommage

Par convention, on appelle souvent ce paramètre :
- `event` (le plus courant)
- `e` (version courte)
- `evt` (alternative)

```javascript
// Toutes ces syntaxes sont valides

// Version longue (recommandée pour les débutants)
bouton.addEventListener('click', function(event) {
    console.log(event);
});

// Version courte avec fonction fléchée
bouton.addEventListener('click', (e) => {
    console.log(e);
});

// Version très courte (si un seul paramètre)
bouton.addEventListener('click', e => {
    console.log(e);
});
```

### Exemple : Explorer l'objet Event

```html
<button id="monBouton">Cliquez-moi</button>
```

```javascript
const bouton = document.getElementById('monBouton');

bouton.addEventListener('click', (event) => {
    console.log('Objet Event complet :', event);
    console.log('Type d\'événement :', event.type);
    console.log('Élément cliqué :', event.target);
});
```

## Propriétés communes de l'objet Event

Certaines propriétés sont disponibles **quel que soit le type d'événement**. Voici les plus importantes :

### 1. event.type

Renvoie le **type d'événement** sous forme de chaîne de caractères.

```javascript
element.addEventListener('click', (event) => {
    console.log(event.type); // "click"
});

element.addEventListener('mouseover', (event) => {
    console.log(event.type); // "mouseover"
});
```

#### Exemple pratique : Gestionnaire unique pour plusieurs événements

```html
<button id="bouton">Cliquez ou survolez</button>
<p id="message"></p>
```

```javascript
const bouton = document.getElementById('bouton');
const message = document.getElementById('message');

function gererEvenement(event) {
    if (event.type === 'click') {
        message.textContent = 'Vous avez cliqué !';
    } else if (event.type === 'mouseover') {
        message.textContent = 'Vous survolez le bouton';
    } else if (event.type === 'mouseout') {
        message.textContent = '';
    }
}

bouton.addEventListener('click', gererEvenement);
bouton.addEventListener('mouseover', gererEvenement);
bouton.addEventListener('mouseout', gererEvenement);
```

### 2. event.target

Renvoie **l'élément qui a déclenché l'événement** (l'élément sur lequel l'utilisateur a réellement cliqué, par exemple).

```javascript
bouton.addEventListener('click', (event) => {
    console.log(event.target); // L'élément <button>
});
```

#### Exemple : Identifier l'élément cliqué

```html
<div id="conteneur">
    <button class="btn">Bouton 1</button>
    <button class="btn">Bouton 2</button>
    <button class="btn">Bouton 3</button>
</div>
```

```javascript
const boutons = document.querySelectorAll('.btn');

boutons.forEach(bouton => {
    bouton.addEventListener('click', (event) => {
        console.log('Texte du bouton cliqué :', event.target.textContent);
    });
});
```

### 3. event.currentTarget

Renvoie **l'élément sur lequel l'écouteur d'événement est attaché**.

> **Note importante** : `target` et `currentTarget` peuvent être différents ! Nous verrons la différence en détail dans la prochaine leçon.

```javascript
const conteneur = document.getElementById('conteneur');

conteneur.addEventListener('click', (event) => {
    console.log('target :', event.target);         // L'élément cliqué
    console.log('currentTarget :', event.currentTarget); // Le conteneur
});
```

### 4. event.timeStamp

Renvoie le **moment où l'événement s'est produit** (en millisecondes depuis le chargement de la page).

```javascript
document.addEventListener('click', (event) => {
    console.log('Événement déclenché après :', event.timeStamp, 'ms');
});
```

#### Exemple pratique : Détecter un double-clic manuel

```html
<button id="bouton">Cliquez rapidement deux fois</button>
<p id="resultat"></p>
```

```javascript
const bouton = document.getElementById('bouton');
const resultat = document.getElementById('resultat');
let dernierClic = 0;

bouton.addEventListener('click', (event) => {
    const tempsEcoule = event.timeStamp - dernierClic;

    if (tempsEcoule < 300) { // Moins de 300ms entre les clics
        resultat.textContent = 'Double-clic détecté !';
    } else {
        resultat.textContent = 'Clic simple';
    }

    dernierClic = event.timeStamp;
});
```

### 5. event.isTrusted

Indique si l'événement a été déclenché par **une action de l'utilisateur** (`true`) ou par **du code JavaScript** (`false`).

```javascript
bouton.addEventListener('click', (event) => {
    if (event.isTrusted) {
        console.log('Clic réel de l\'utilisateur');
    } else {
        console.log('Clic déclenché par du code');
    }
});

// Déclencher un clic par code
bouton.click(); // event.isTrusted sera false
```

### 6. event.bubbles

Indique si l'événement **remonte** dans l'arbre DOM (bubbling). Nous verrons ce concept en détail dans une prochaine leçon.

```javascript
element.addEventListener('click', (event) => {
    console.log('Cet événement remonte-t-il ?', event.bubbles); // true pour click
});
```

## Propriétés spécifiques aux événements de souris

Ces propriétés sont disponibles uniquement pour les événements de souris (`click`, `mousemove`, etc.).

### Propriétés de position

#### event.clientX / event.clientY

Position de la souris **par rapport à la fenêtre du navigateur** (viewport).

```html
<div id="zone" style="width: 400px; height: 300px; background: lightblue;">
    Déplacez la souris
</div>
<p>X: <span id="x">0</span>, Y: <span id="y">0</span></p>
```

```javascript
const zone = document.getElementById('zone');
const xSpan = document.getElementById('x');
const ySpan = document.getElementById('y');

zone.addEventListener('mousemove', (event) => {
    xSpan.textContent = event.clientX;
    ySpan.textContent = event.clientY;
});
```

#### event.pageX / event.pageY

Position de la souris **par rapport à la page complète** (inclut le défilement).

```javascript
document.addEventListener('click', (event) => {
    console.log('Position dans la fenêtre :', event.clientX, event.clientY);
    console.log('Position dans la page :', event.pageX, event.pageY);
});
```

#### event.offsetX / event.offsetY

Position de la souris **par rapport à l'élément ciblé**.

```html
<div id="boite" style="width: 200px; height: 200px; background: coral; position: relative;">
    Cliquez dans la boîte
</div>
```

```javascript
const boite = document.getElementById('boite');

boite.addEventListener('click', (event) => {
    console.log('Position dans la boîte :', event.offsetX, event.offsetY);

    // Afficher un point à l'endroit du clic
    const point = document.createElement('div');
    point.style.position = 'absolute';
    point.style.left = event.offsetX + 'px';
    point.style.top = event.offsetY + 'px';
    point.style.width = '10px';
    point.style.height = '10px';
    point.style.background = 'black';
    point.style.borderRadius = '50%';
    boite.appendChild(point);
});
```

#### event.screenX / event.screenY

Position de la souris **par rapport à l'écran physique** (rarement utilisé).

### Comparaison des propriétés de position

```javascript
document.addEventListener('click', (event) => {
    console.log('clientX/Y (fenêtre) :', event.clientX, event.clientY);
    console.log('pageX/Y (page) :', event.pageX, event.pageY);
    console.log('offsetX/Y (élément) :', event.offsetX, event.offsetY);
    console.log('screenX/Y (écran) :', event.screenX, event.screenY);
});
```

### event.button

Indique **quel bouton de la souris** a été utilisé :

- `0` : Bouton gauche
- `1` : Bouton du milieu (molette)
- `2` : Bouton droit

```html
<div id="zone" style="width: 300px; height: 200px; background: lightgreen;">
    Essayez les différents boutons de la souris
</div>
<p id="resultat"></p>
```

```javascript
const zone = document.getElementById('zone');
const resultat = document.getElementById('resultat');

zone.addEventListener('mousedown', (event) => {
    if (event.button === 0) {
        resultat.textContent = 'Bouton gauche';
    } else if (event.button === 1) {
        resultat.textContent = 'Bouton du milieu';
    } else if (event.button === 2) {
        resultat.textContent = 'Bouton droit';
    }
});

// Empêcher le menu contextuel sur clic droit
zone.addEventListener('contextmenu', (event) => {
    event.preventDefault();
});
```

### Touches modificatrices

Ces propriétés indiquent si une touche modificatrice était enfoncée :

```javascript
element.addEventListener('click', (event) => {
    console.log('Ctrl enfoncé ?', event.ctrlKey);   // true ou false
    console.log('Shift enfoncé ?', event.shiftKey); // true ou false
    console.log('Alt enfoncé ?', event.altKey);     // true ou false
    console.log('Meta enfoncé ?', event.metaKey);   // Cmd/Win
});
```

#### Exemple : Actions différentes selon les modificateurs

```html
<div id="canvas" style="width: 400px; height: 300px; background: #f0f0f0; position: relative;">
    Cliquez avec différentes touches modificatrices
</div>
```

```javascript
const canvas = document.getElementById('canvas');

canvas.addEventListener('click', (event) => {
    const point = document.createElement('div');
    point.style.position = 'absolute';
    point.style.left = event.offsetX + 'px';
    point.style.top = event.offsetY + 'px';
    point.style.width = '20px';
    point.style.height = '20px';
    point.style.borderRadius = '50%';

    if (event.ctrlKey) {
        point.style.background = 'red';
    } else if (event.shiftKey) {
        point.style.background = 'blue';
    } else if (event.altKey) {
        point.style.background = 'green';
    } else {
        point.style.background = 'black';
    }

    canvas.appendChild(point);
});
```

## Propriétés spécifiques aux événements de clavier

Ces propriétés sont disponibles pour les événements de clavier (`keydown`, `keyup`).

### event.key

La **valeur** de la touche pressée.

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Touche pressée :', event.key);
    // 'a', 'Enter', 'ArrowUp', 'Escape', etc.
});
```

### event.code

Le **code physique** de la touche (position sur le clavier).

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Code de la touche :', event.code);
    // 'KeyA', 'Enter', 'ArrowUp', 'Escape', etc.
});
```

### event.repeat

Indique si la touche est **maintenue enfoncée** (répétition automatique).

```html
<p>Appuyez et maintenez une touche</p>
<p id="compteur">0</p>
```

```javascript
const compteur = document.getElementById('compteur');
let compte = 0;

document.addEventListener('keydown', (event) => {
    if (event.repeat) {
        compte++;
        compteur.textContent = compte;
    }
});

document.addEventListener('keyup', () => {
    compte = 0;
    compteur.textContent = 0;
});
```

### Touches modificatrices

Les mêmes propriétés que pour la souris :

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Ctrl :', event.ctrlKey);
    console.log('Shift :', event.shiftKey);
    console.log('Alt :', event.altKey);
    console.log('Meta :', event.metaKey);
});
```

## Propriétés spécifiques aux événements de formulaire

### event.target.value

Pour les champs de formulaire, `event.target.value` donne la **valeur actuelle** du champ.

```html
<input type="text" id="nom" placeholder="Votre nom">
<p id="affichage"></p>
```

```javascript
const nom = document.getElementById('nom');
const affichage = document.getElementById('affichage');

nom.addEventListener('input', (event) => {
    affichage.textContent = `Vous avez tapé : ${event.target.value}`;
});
```

### event.target.checked

Pour les checkboxes et radio buttons, indique si l'élément est **coché**.

```html
<label>
    <input type="checkbox" id="accepte">
    J'accepte les conditions
</label>
<p id="status"></p>
```

```javascript
const accepte = document.getElementById('accepte');
const status = document.getElementById('status');

accepte.addEventListener('change', (event) => {
    if (event.target.checked) {
        status.textContent = 'Conditions acceptées ✓';
        status.style.color = 'green';
    } else {
        status.textContent = 'Conditions non acceptées';
        status.style.color = 'red';
    }
});
```

## Méthodes de l'objet Event

L'objet Event possède aussi des **méthodes** importantes :

### event.preventDefault()

Empêche le **comportement par défaut** de l'événement.

#### Exemples d'usage :

```javascript
// Empêcher la soumission d'un formulaire
form.addEventListener('submit', (event) => {
    event.preventDefault();
    console.log('Formulaire non soumis');
});

// Empêcher le clic droit (menu contextuel)
element.addEventListener('contextmenu', (event) => {
    event.preventDefault();
    console.log('Menu contextuel bloqué');
});

// Empêcher le comportement d'un lien
lien.addEventListener('click', (event) => {
    event.preventDefault();
    console.log('Navigation bloquée');
});
```

### event.stopPropagation()

Arrête la **propagation** de l'événement (bubbling et capturing). Nous verrons ce concept en détail dans la leçon suivante.

```javascript
element.addEventListener('click', (event) => {
    event.stopPropagation();
    console.log('L\'événement ne remontera pas aux parents');
});
```

### event.stopImmediatePropagation()

Arrête la propagation **ET** empêche les autres écouteurs sur le **même élément** de s'exécuter.

```javascript
element.addEventListener('click', (event) => {
    event.stopImmediatePropagation();
    console.log('Premier gestionnaire');
});

element.addEventListener('click', () => {
    console.log('Ce code ne s\'exécutera jamais');
});
```

## Exemples pratiques complets

### Exemple 1 : Dessin avec la souris

```html
<canvas id="canvas" width="600" height="400" style="border: 1px solid black;"></canvas>
<p>Cliquez et glissez pour dessiner</p>
```

```javascript
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
let estEnTrainDeDessiner = false;

canvas.addEventListener('mousedown', (event) => {
    estEnTrainDeDessiner = true;
    ctx.beginPath();
    ctx.moveTo(event.offsetX, event.offsetY);
});

canvas.addEventListener('mousemove', (event) => {
    if (estEnTrainDeDessiner) {
        ctx.lineTo(event.offsetX, event.offsetY);
        ctx.stroke();
    }
});

canvas.addEventListener('mouseup', () => {
    estEnTrainDeDessiner = false;
});

canvas.addEventListener('mouseleave', () => {
    estEnTrainDeDessiner = false;
});
```

### Exemple 2 : Info-bulle qui suit la souris

```html
<div id="zone" style="width: 400px; height: 300px; background: lightblue; position: relative;">
    Déplacez la souris
</div>
<div id="tooltip" style="position: absolute; background: black; color: white; padding: 5px; border-radius: 3px; display: none; pointer-events: none;">
    Info-bulle
</div>
```

```javascript
const zone = document.getElementById('zone');
const tooltip = document.getElementById('tooltip');

zone.addEventListener('mouseenter', () => {
    tooltip.style.display = 'block';
});

zone.addEventListener('mousemove', (event) => {
    tooltip.style.left = (event.pageX + 10) + 'px';
    tooltip.style.top = (event.pageY + 10) + 'px';
    tooltip.textContent = `X: ${event.offsetX}, Y: ${event.offsetY}`;
});

zone.addEventListener('mouseleave', () => {
    tooltip.style.display = 'none';
});
```

### Exemple 3 : Formulaire avec détection des modifications

```html
<form id="form">
    <input type="text" name="nom" placeholder="Nom">
    <input type="email" name="email" placeholder="Email">
    <textarea name="message" placeholder="Message"></textarea>
    <button type="submit">Envoyer</button>
</form>
<p id="modifications"></p>
```

```javascript
const form = document.getElementById('form');
const modifications = document.getElementById('modifications');
const valeursInitiales = {};
let aDesModifications = false;

// Enregistrer les valeurs initiales
form.querySelectorAll('input, textarea').forEach(champ => {
    valeursInitiales[champ.name] = champ.value;
});

// Détecter les modifications
form.addEventListener('input', (event) => {
    const champ = event.target;
    const valeurInitiale = valeursInitiales[champ.name];
    const valeurActuelle = champ.value;

    if (valeurInitiale !== valeurActuelle) {
        aDesModifications = true;
        modifications.textContent = '⚠️ Modifications non sauvegardées';
        modifications.style.color = 'orange';
    }
});

form.addEventListener('submit', (event) => {
    event.preventDefault();

    if (aDesModifications) {
        modifications.textContent = '✓ Sauvegardé !';
        modifications.style.color = 'green';
        aDesModifications = false;

        // Mettre à jour les valeurs initiales
        form.querySelectorAll('input, textarea').forEach(champ => {
            valeursInitiales[champ.name] = champ.value;
        });
    }
});
```

### Exemple 4 : Jeu de réaction

```html
<div id="cible" style="width: 50px; height: 50px; background: red; border-radius: 50%; position: absolute; cursor: pointer;"></div>
<p>Clics réussis : <span id="score">0</span></p>
<p>Temps de réaction moyen : <span id="tempsmoyen">-</span> ms</p>
```

```javascript
const cible = document.getElementById('cible');
const scoreElement = document.getElementById('score');
const tempsMoyenElement = document.getElementById('tempsmoyen');

let score = 0;
let tempsApparition = 0;
let tempsTotal = 0;

function deplacerCible() {
    const maxX = window.innerWidth - 50;
    const maxY = window.innerHeight - 50;

    cible.style.left = Math.random() * maxX + 'px';
    cible.style.top = Math.random() * maxY + 'px';

    tempsApparition = Date.now();
}

cible.addEventListener('click', (event) => {
    const tempsReaction = Date.now() - tempsApparition;

    score++;
    tempsTotal += tempsReaction;

    scoreElement.textContent = score;
    tempsMoyenElement.textContent = Math.round(tempsTotal / score);

    deplacerCible();
});

// Démarrer
deplacerCible();
```

### Exemple 5 : Log complet des propriétés d'un événement

```html
<button id="bouton">Cliquez avec différentes touches</button>
<pre id="log"></pre>
```

```javascript
const bouton = document.getElementById('bouton');
const log = document.getElementById('log');

bouton.addEventListener('click', (event) => {
    const info = {
        type: event.type,
        target: event.target.tagName,
        currentTarget: event.currentTarget.tagName,
        timeStamp: Math.round(event.timeStamp),
        isTrusted: event.isTrusted,
        bubbles: event.bubbles,
        clientX: event.clientX,
        clientY: event.clientY,
        pageX: event.pageX,
        pageY: event.pageY,
        offsetX: event.offsetX,
        offsetY: event.offsetY,
        button: event.button,
        ctrlKey: event.ctrlKey,
        shiftKey: event.shiftKey,
        altKey: event.altKey,
        metaKey: event.metaKey
    };

    log.textContent = JSON.stringify(info, null, 2);
});
```

## Tableau récapitulatif des propriétés

### Propriétés communes

| Propriété | Type | Description |
|-----------|------|-------------|
| `type` | string | Type d'événement ('click', 'keydown', etc.) |
| `target` | Element | Élément qui a déclenché l'événement |
| `currentTarget` | Element | Élément sur lequel l'écouteur est attaché |
| `timeStamp` | number | Moment de l'événement (ms) |
| `isTrusted` | boolean | Événement réel (true) ou programmé (false) |
| `bubbles` | boolean | L'événement remonte-t-il ? |

### Propriétés de souris

| Propriété | Type | Description |
|-----------|------|-------------|
| `clientX/Y` | number | Position par rapport à la fenêtre |
| `pageX/Y` | number | Position par rapport à la page |
| `offsetX/Y` | number | Position par rapport à l'élément |
| `screenX/Y` | number | Position par rapport à l'écran |
| `button` | number | Bouton de souris (0, 1, 2) |
| `ctrlKey` | boolean | Ctrl enfoncé ? |
| `shiftKey` | boolean | Shift enfoncé ? |
| `altKey` | boolean | Alt enfoncé ? |
| `metaKey` | boolean | Meta (Cmd/Win) enfoncé ? |

### Propriétés de clavier

| Propriété | Type | Description |
|-----------|------|-------------|
| `key` | string | Valeur de la touche |
| `code` | string | Code physique de la touche |
| `repeat` | boolean | Touche maintenue ? |
| `ctrlKey` | boolean | Ctrl enfoncé ? |
| `shiftKey` | boolean | Shift enfoncé ? |
| `altKey` | boolean | Alt enfoncé ? |
| `metaKey` | boolean | Meta enfoncé ? |

## Bonnes pratiques

### ✅ 1. Toujours accepter l'objet Event en paramètre

```javascript
// ✅ BIEN
element.addEventListener('click', (event) => {
    console.log(event.target);
});

// ⚠️ MOINS BIEN - Vous perdez l'accès à event
element.addEventListener('click', () => {
    console.log('Clic');
});
```

### ✅ 2. Utiliser les propriétés appropriées

```javascript
// ✅ BIEN - Utiliser event.key pour les touches
if (event.key === 'Enter') { }

// ❌ ÉVITER - keyCode est déprécié
if (event.keyCode === 13) { }
```

### ✅ 3. Vérifier l'existence des propriétés

Certaines propriétés n'existent que pour certains types d'événements :

```javascript
element.addEventListener('click', (event) => {
    // clientX existe pour les événements de souris
    if (event.clientX !== undefined) {
        console.log('Position X :', event.clientX);
    }
});
```

### ✅ 4. Utiliser event.preventDefault() avec précaution

```javascript
// ✅ BIEN - Empêcher la soumission pour valider
form.addEventListener('submit', (event) => {
    event.preventDefault();
    if (validerFormulaire()) {
        // Soumettre manuellement
    }
});

// ⚠️ ATTENTION - Peut casser l'accessibilité
lien.addEventListener('click', (event) => {
    event.preventDefault(); // Le lien ne fonctionnera plus du tout
});
```

## Ce qu'il faut retenir

✅ **L'objet Event** est automatiquement créé et passé en paramètre

✅ **event.target** : l'élément qui a déclenché l'événement

✅ **event.type** : le type d'événement ('click', 'keydown', etc.)

✅ **Propriétés de position** : clientX/Y, pageX/Y, offsetX/Y pour la souris

✅ **Propriétés de clavier** : key, code, repeat

✅ **Touches modificatrices** : ctrlKey, shiftKey, altKey, metaKey

✅ **event.preventDefault()** : empêche le comportement par défaut

✅ **Différentes propriétés** selon le type d'événement

## Dans la prochaine leçon

Maintenant que vous connaissez l'objet Event et ses propriétés, nous allons explorer la différence entre **event.target** et **event.currentTarget**, un concept important pour comprendre la propagation des événements.

Vous découvrirez :
- La différence exacte entre target et currentTarget
- Pourquoi cette différence existe
- Comment utiliser chacun correctement
- Des cas pratiques concrets

---


⏭️ [event.target vs event.currentTarget](/05-javascript-moderne-fondamentaux/10-evenements/07-target-currenttarget.md)
