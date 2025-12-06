🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.1.5 - Strict mode et modules ES6 🆕

## Introduction

JavaScript a évolué au fil des années, et pour des raisons de **compatibilité**, certains comportements problématiques de l'ancien JavaScript ont été conservés. Heureusement, ES5 (2009) a introduit le **"strict mode"** qui rend JavaScript plus sûr et prévisible, et ES6 (2015) a introduit les **modules** qui permettent d'organiser le code proprement.

Ces deux fonctionnalités sont devenues des **standards modernes** et vous devez les utiliser dans tous vos nouveaux projets.

## Le Strict Mode ("use strict") 🔒

### Qu'est-ce que le strict mode ?

Le **strict mode** est un mode d'exécution de JavaScript qui :
- ❌ Interdit certaines pratiques dangereuses ou obsolètes
- ✅ Signale plus d'erreurs pour vous aider à écrire du meilleur code
- 🚀 Peut améliorer les performances dans certains cas

C'est comme un **filet de sécurité** qui vous empêche de faire des erreurs courantes.

### Comment activer le strict mode ?

Il suffit d'écrire `'use strict';` au début de votre fichier ou fonction :

```javascript
// En haut du fichier (strict mode global)
'use strict';

let nom = 'Alice';
console.log(nom);
```

Ou dans une fonction spécifique :

```javascript
function maFonction() {
    'use strict';
    // Strict mode actif seulement dans cette fonction
    let x = 10;
}
```

> 💡 **Important** : `'use strict';` doit être la **première instruction** (après les éventuels commentaires).

### Pourquoi utiliser le strict mode ?

#### 1. Empêche les variables globales accidentelles ✅

**Sans strict mode** (dangereux) :
```javascript
function calculer() {
    resultat = 10 * 5;  // Oups ! Variable globale créée par erreur
    return resultat;
}

calculer();
console.log(resultat);  // 50 - La variable "fuite" dans le scope global !
```

**Avec strict mode** (sécurisé) :
```javascript
'use strict';

function calculer() {
    resultat = 10 * 5;  // ❌ ReferenceError: resultat is not defined
    return resultat;
}
```

Le strict mode vous **force** à déclarer vos variables avec `let`, `const` ou `var`.

#### 2. Empêche la suppression de variables non supprimables ✅

**Sans strict mode** :
```javascript
delete Object.prototype;  // Échoue silencieusement (mauvais !)
```

**Avec strict mode** :
```javascript
'use strict';
delete Object.prototype;  // ❌ TypeError: Cannot delete property
```

#### 3. Interdit les doublons de paramètres ✅

**Sans strict mode** :
```javascript
function addition(a, b, a) {  // Deux paramètres "a" !
    return a + b;  // Lequel des deux "a" ? Confus !
}

addition(1, 2, 3);  // 5 (utilise le dernier "a")
```

**Avec strict mode** :
```javascript
'use strict';

function addition(a, b, a) {  // ❌ SyntaxError: Duplicate parameter name
    return a + b;
}
```

#### 4. Empêche d'utiliser des mots-clés réservés ✅

```javascript
'use strict';

let interface = 'test';  // ❌ SyntaxError
let private = 10;        // ❌ SyntaxError
let package = 'abc';     // ❌ SyntaxError
```

Ces mots sont réservés pour de futures fonctionnalités JavaScript.

#### 5. Interdit l'assignation à des propriétés non modifiables ✅

```javascript
'use strict';

const obj = {};
Object.defineProperty(obj, 'x', {
    value: 42,
    writable: false  // Lecture seule
});

obj.x = 100;  // ❌ TypeError: Cannot assign to read only property
```

Sans strict mode, cette erreur serait **silencieuse** !

### Liste des principales restrictions du strict mode

| Comportement | Sans strict mode | Avec strict mode |
|--------------|------------------|------------------|
| Variable non déclarée | Crée une variable globale | ❌ ReferenceError |
| `delete` variable | Échoue silencieusement | ❌ SyntaxError |
| Paramètres dupliqués | Autorisé | ❌ SyntaxError |
| Octaux littéraux (`0123`) | Autorisé | ❌ SyntaxError |
| `with` statement | Autorisé | ❌ SyntaxError |
| `eval` dans le scope | Peut polluer le scope | Scope isolé |
| `this` dans fonctions | `window` (global) | `undefined` |

### Le strict mode et `this`

Une différence importante concerne la valeur de `this` :

**Sans strict mode** :
```javascript
function afficher() {
    console.log(this);  // window (objet global)
}

afficher();
```

**Avec strict mode** :
```javascript
'use strict';

function afficher() {
    console.log(this);  // undefined (plus sûr !)
}

afficher();
```

> 🔍 **À retenir** : En strict mode, `this` dans une fonction normale est `undefined` au lieu de l'objet global. C'est plus logique et évite des bugs.

### Exemple complet avec strict mode

```javascript
'use strict';

// ✅ Bon : variables déclarées proprement
let nom = 'Alice';
const AGE = 25;

function saluer(prenom) {
    // ✅ Le strict mode est actif dans toute la fonction
    console.log(`Bonjour ${prenom} !`);

    // ❌ Ceci causerait une erreur :
    // ville = 'Paris';  // ReferenceError
}

saluer(nom);

// ❌ Ceci causerait une erreur :
// delete nom;  // SyntaxError

// ❌ Ceci causerait une erreur :
// function test(a, a) {  // SyntaxError
//     return a * 2;
// }
```

## Les Modules ES6 (import/export) 📦

### Qu'est-ce qu'un module ?

Un **module** est un fichier JavaScript qui peut :
- **Exporter** des fonctions, variables ou classes pour que d'autres fichiers les utilisent
- **Importer** des fonctions, variables ou classes depuis d'autres fichiers

C'est la façon moderne d'organiser et de structurer votre code JavaScript.

### Pourquoi utiliser des modules ?

#### Sans modules (ancien style) ❌

**fichier1.js :**
```javascript
function addition(a, b) {
    return a + b;
}
```

**fichier2.js :**
```javascript
function multiplication(a, b) {
    return a * b;
}
```

**index.html :**
```html
<!-- On doit charger les fichiers dans le bon ordre -->
<script src="fichier1.js"></script>
<script src="fichier2.js"></script>
<script src="main.js"></script>
```

**Problèmes :**
- 🚫 Toutes les fonctions sont globales (risque de conflits de noms)
- 🚫 L'ordre de chargement est crucial
- 🚫 Difficile de savoir quelles fonctions sont utilisées où
- 🚫 Pas de réutilisation facile

#### Avec modules (moderne) ✅

**utils.js :**
```javascript
// Exporter des fonctions
export function addition(a, b) {
    return a + b;
}

export function multiplication(a, b) {
    return a * b;
}
```

**main.js :**
```javascript
// Importer seulement ce dont on a besoin
import { addition, multiplication } from './utils.js';

console.log(addition(5, 3));        // 8
console.log(multiplication(5, 3));  // 15
```

**index.html :**
```html
<!-- Un seul script, avec type="module" -->
<script type="module" src="main.js"></script>
```

**Avantages :**
- ✅ Chaque fichier a son propre scope (pas de pollution globale)
- ✅ Import/export explicites (on sait ce qui vient d'où)
- ✅ Gestion automatique des dépendances
- ✅ Strict mode activé automatiquement !

### Syntaxe d'export

Il existe plusieurs façons d'exporter du code.

#### 1. Export nommé (Named exports)

**mathUtils.js :**
```javascript
// Export individuel
export function addition(a, b) {
    return a + b;
}

export function soustraction(a, b) {
    return a - b;
}

export const PI = 3.14159;

// Ou export groupé
function multiplication(a, b) {
    return a * b;
}

function division(a, b) {
    return a / b;
}

export { multiplication, division };
```

#### 2. Export par défaut (Default export)

Un fichier peut avoir **un seul** export par défaut :

**calculatrice.js :**
```javascript
// Export par défaut d'une fonction
export default function calculer(operation, a, b) {
    switch(operation) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return a / b;
        default: return null;
    }
}

// Ou une classe
export default class Calculatrice {
    addition(a, b) {
        return a + b;
    }
}

// Ou un objet
export default {
    version: '1.0',
    author: 'Alice'
};
```

#### 3. Combinaison (exports nommés + export par défaut)

**user.js :**
```javascript
// Export par défaut
export default class User {
    constructor(nom) {
        this.nom = nom;
    }
}

// Exports nommés
export const USER_ROLES = ['admin', 'user', 'guest'];

export function validerNom(nom) {
    return nom.length > 2;
}
```

### Syntaxe d'import

#### 1. Import nommé

```javascript
// Importer des exports nommés
import { addition, soustraction } from './mathUtils.js';

console.log(addition(5, 3));      // 8
console.log(soustraction(5, 3));  // 2

// Importer tout avec un alias
import * as math from './mathUtils.js';

console.log(math.addition(5, 3));        // 8
console.log(math.PI);                     // 3.14159

// Importer avec renommage
import { addition as add, soustraction as sub } from './mathUtils.js';

console.log(add(5, 3));  // 8
console.log(sub(5, 3));  // 2
```

#### 2. Import par défaut

```javascript
// Import par défaut (on choisit le nom)
import calculer from './calculatrice.js';

console.log(calculer('+', 5, 3));  // 8

// Ou avec un autre nom
import calc from './calculatrice.js';

console.log(calc('-', 5, 3));  // 2
```

#### 3. Combinaison (import par défaut + imports nommés)

```javascript
import User, { USER_ROLES, validerNom } from './user.js';

const alice = new User('Alice');
console.log(USER_ROLES);           // ['admin', 'user', 'guest']
console.log(validerNom('Bob'));    // true
```

### Structure de projet avec modules

```
mon-projet/
├── index.html
├── js/
│   ├── main.js              # Point d'entrée
│   ├── config.js            # Configuration
│   ├── utils/
│   │   ├── math.js          # Fonctions mathématiques
│   │   └── string.js        # Fonctions pour les chaînes
│   ├── components/
│   │   ├── header.js        # Composant header
│   │   └── footer.js        # Composant footer
│   └── services/
│       └── api.js           # Appels API
```

**index.html :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon Application</title>
</head>
<body>
    <div id="app"></div>

    <!-- ✅ Type module + defer automatique -->
    <script type="module" src="js/main.js"></script>
</body>
</html>
```

**js/config.js :**
```javascript
// Configuration exportée
export const API_URL = 'https://api.example.com';
export const APP_VERSION = '1.0.0';
export const DEBUG = true;

export default {
    api: API_URL,
    version: APP_VERSION,
    debug: DEBUG
};
```

**js/utils/math.js :**
```javascript
export function addition(a, b) {
    return a + b;
}

export function multiplication(a, b) {
    return a * b;
}

export function moyenne(tableau) {
    const somme = tableau.reduce((acc, val) => acc + val, 0);
    return somme / tableau.length;
}
```

**js/components/header.js :**
```javascript
export function creerHeader() {
    const header = document.createElement('header');
    header.innerHTML = '<h1>Mon Application</h1>';
    return header;
}
```

**js/main.js :**
```javascript
// Imports depuis différents modules
import config from './config.js';
import { addition, moyenne } from './utils/math.js';
import { creerHeader } from './components/header.js';

console.log('Version:', config.version);

// Utiliser les fonctions importées
console.log('Addition:', addition(5, 3));
console.log('Moyenne:', moyenne([1, 2, 3, 4, 5]));

// Créer le header
const app = document.getElementById('app');
app.appendChild(creerHeader());
```

### Différences entre modules et scripts classiques

| Caractéristique | Script classique | Module ES6 |
|----------------|------------------|------------|
| **Strict mode** | Optionnel | ✅ Automatique |
| **Scope** | Global | Local au module |
| **Import/Export** | ❌ Non | ✅ Oui |
| **`this` au niveau racine** | `window` | `undefined` |
| **Chargement** | Bloquant par défaut | Asynchrone (comme defer) |
| **HTML** | `<script src="...">` | `<script type="module" src="...">` |

### Avantages des modules ES6 🚀

#### 1. Scope isolé
```javascript
// module1.js
let nom = 'Alice';  // Privé au module

// module2.js
let nom = 'Bob';    // Pas de conflit !
```

#### 2. Dépendances explicites
```javascript
// On voit clairement d'où viennent les fonctions
import { addition } from './math.js';
import { formater } from './string.js';
```

#### 3. Réutilisation facile
```javascript
// Le même module peut être importé partout
import { addition } from './math.js';
```

#### 4. Tree-shaking (optimisation)
Les outils modernes peuvent supprimer le code non utilisé :
```javascript
// Si vous n'importez que addition, les autres fonctions
// peuvent être retirées du bundle final
import { addition } from './math.js';
```

#### 5. Strict mode automatique
Plus besoin d'écrire `'use strict';` !

### Modules et compatibilité navigateur

Les modules ES6 sont supportés par tous les navigateurs modernes :
- ✅ Chrome 61+
- ✅ Firefox 60+
- ✅ Safari 11+
- ✅ Edge 16+

Pour les anciens navigateurs, vous utiliserez des outils comme **Webpack** ou **Vite** (que nous verrons plus tard).

### Erreurs courantes avec les modules

#### 1. Oublier `type="module"`

```html
<!-- ❌ Ne fonctionne pas -->
<script src="main.js"></script>

<!-- ✅ Correct -->
<script type="module" src="main.js"></script>
```

#### 2. Oublier l'extension `.js` dans les imports

```javascript
// ❌ Ne fonctionne pas
import { addition } from './math';

// ✅ Correct
import { addition } from './math.js';
```

#### 3. CORS (Cross-Origin) en local

Les modules utilisent les requêtes HTTP, donc vous devez utiliser un serveur local, pas `file://`.

**Solutions :**
- Utiliser l'extension "Live Server" dans VSCode
- Ou lancer un serveur simple : `python -m http.server 8000`

#### 4. Import circulaire

```javascript
// module1.js
import { fonctionB } from './module2.js';
export function fonctionA() { /* ... */ }

// module2.js
import { fonctionA } from './module1.js';  // ❌ Référence circulaire !
export function fonctionB() { /* ... */ }
```

Évitez les dépendances circulaires en restructurant votre code.

## Exemple pratique complet

Créons une petite application avec modules :

### Structure
```
app/
├── index.html
└── js/
    ├── main.js
    ├── config.js
    └── utils/
        └── compteur.js
```

### config.js
```javascript
export const APP_NAME = 'Mon Compteur';
export const VERSION = '1.0.0';
export const COULEUR_PRIMAIRE = '#4CAF50';
```

### utils/compteur.js
```javascript
// État du compteur (privé au module)
let valeur = 0;

// Exports nommés
export function incrementer() {
    valeur++;
    return valeur;
}

export function decrementer() {
    valeur--;
    return valeur;
}

export function reinitialiser() {
    valeur = 0;
    return valeur;
}

export function getValeur() {
    return valeur;
}

// Export par défaut
export default {
    incrementer,
    decrementer,
    reinitialiser,
    getValeur
};
```

### main.js
```javascript
// Imports
import { APP_NAME, COULEUR_PRIMAIRE } from './config.js';
import { incrementer, decrementer, reinitialiser, getValeur } from './utils/compteur.js';

// Configuration initiale
console.log(`${APP_NAME} démarré !`);
document.title = APP_NAME;

// Sélection des éléments
const affichage = document.getElementById('valeur');
const btnPlus = document.getElementById('plus');
const btnMoins = document.getElementById('moins');
const btnReset = document.getElementById('reset');

// Fonction pour mettre à jour l'affichage
function mettreAJourAffichage() {
    affichage.textContent = getValeur();
    affichage.style.color = COULEUR_PRIMAIRE;
}

// Événements
btnPlus.addEventListener('click', () => {
    incrementer();
    mettreAJourAffichage();
});

btnMoins.addEventListener('click', () => {
    decrementer();
    mettreAJourAffichage();
});

btnReset.addEventListener('click', () => {
    reinitialiser();
    mettreAJourAffichage();
});

// Initialisation
mettreAJourAffichage();
```

### index.html
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Compteur</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: #f0f0f0;
        }
        .compteur {
            background: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            text-align: center;
        }
        #valeur {
            font-size: 72px;
            font-weight: bold;
            margin: 20px 0;
        }
        button {
            font-size: 24px;
            padding: 10px 20px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background: #4CAF50;
            color: white;
        }
        button:hover {
            background: #45a049;
        }
    </style>
</head>
<body>
    <div class="compteur">
        <h1>Compteur</h1>
        <div id="valeur">0</div>
        <div>
            <button id="moins">-</button>
            <button id="reset">Reset</button>
            <button id="plus">+</button>
        </div>
    </div>

    <!-- ✅ Type module -->
    <script type="module" src="js/main.js"></script>
</body>
</html>
```

## Bonnes pratiques

### ✅ À faire

1. **Toujours utiliser le strict mode** dans les fichiers non-module
2. **Utiliser des modules** pour organiser votre code
3. **Un fichier = une responsabilité** (un module pour les maths, un pour l'API, etc.)
4. **Exporter ce qui doit être public**, garder le reste privé
5. **Nommer les exports clairement** : `export function calculerTotal()` plutôt que `export function calc()`
6. **Utiliser `export default`** pour l'élément principal du module

### ❌ À éviter

1. Ne pas mélanger anciennes et nouvelles méthodes
2. Ne pas créer de dépendances circulaires
3. Ne pas exporter trop de choses d'un seul module (gardez-les focalisés)
4. Ne pas oublier l'extension `.js` dans les imports

## En résumé

### Strict Mode 🔒

| Avantage | Description |
|----------|-------------|
| **Sécurité** | Empêche les erreurs silencieuses |
| **Clarté** | Force les bonnes pratiques |
| **Performance** | Peut optimiser le code |
| **Évolution** | Prépare pour le futur JavaScript |

**Comment activer :**
```javascript
'use strict';  // En haut du fichier
```

### Modules ES6 📦

| Avantage | Description |
|----------|-------------|
| **Organisation** | Code structuré et modulaire |
| **Réutilisation** | Partage facile de code |
| **Scope isolé** | Pas de pollution globale |
| **Maintenance** | Plus facile à déboguer et modifier |
| **Strict mode** | Activé automatiquement |

**Comment utiliser :**
```javascript
// Exporter
export function maFonction() { }

// Importer
import { maFonction } from './module.js';
```

```html
<!-- Dans le HTML -->
<script type="module" src="main.js"></script>
```

> 🎯 **À retenir** : Le strict mode et les modules ES6 sont des fonctionnalités **essentielles** du JavaScript moderne. Utilisez-les systématiquement dans tous vos nouveaux projets !

## Prochaine étape

Vous avez maintenant une solide introduction à JavaScript ! Dans la section suivante, nous allons enfin commencer à coder avec les **variables et types de données modernes** (const et let).

---


🆕 **Moderne** : Ces deux fonctionnalités (strict mode et modules) sont au cœur du JavaScript moderne et professionnel !

⏭️ [Variables et types de données (Approche moderne)](/05-javascript-moderne-fondamentaux/02-variables-et-types/README.md)
