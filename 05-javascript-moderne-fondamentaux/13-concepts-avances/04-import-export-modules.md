🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.13.4 - Import/Export de modules (ES6) 🆕

## Introduction

Les **modules ES6** (ECMAScript 2015) ont révolutionné la façon d'organiser le code JavaScript. Avant leur arrivée, il n'existait pas de système de modules natif en JavaScript, ce qui rendait la gestion de gros projets difficile.

> 🆕 **Standard moderne** : Les modules ES6 sont aujourd'hui la manière standard et recommandée d'organiser votre code JavaScript.

**Avantages des modules :**
- ✅ Code organisé et maintenable
- ✅ Réutilisabilité
- ✅ Isolation du scope (pas de pollution globale)
- ✅ Dépendances explicites
- ✅ Support natif des navigateurs et Node.js

---

## Concept de base : Qu'est-ce qu'un module ?

Un **module** est simplement un **fichier JavaScript** qui peut :
- **Exporter** (partager) certaines fonctions, variables, classes ou objets
- **Importer** (utiliser) des exports d'autres modules

```
┌─────────────────┐
│  math.js        │
│  (module)       │
│                 │
│  export PI      │ ─────┐
│  export add     │      │
└─────────────────┘      │ Import
                         │
                         ▼
                  ┌─────────────────┐
                  │  app.js         │
                  │  (module)       │
                  │                 │
                  │  import { PI }  │
                  │  import { add } │
                  └─────────────────┘
```

---

## Configuration requise

### Dans le HTML

Pour utiliser les modules ES6 dans le navigateur, ajoutez `type="module"` :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Application</title>
</head>
<body>
  <h1>Application avec modules</h1>

  <!-- ⚠️ IMPORTANT : type="module" -->
  <script type="module" src="app.js"></script>
</body>
</html>
```

**Caractéristiques des modules :**
- Mode strict automatique (`'use strict'`)
- Scope isolé (les variables ne sont pas globales)
- `this` au niveau supérieur vaut `undefined`
- Chargement asynchrone et différé

### Serveur local nécessaire

⚠️ Les modules ne fonctionnent pas avec le protocole `file://`

```bash
# ❌ Ne fonctionne pas
file:///C:/mon-projet/index.html

# ✅ Nécessite un serveur
http://localhost:3000/index.html
```

**Solutions pour serveur local :**

```bash
# Avec Python 3
python -m http.server 8000

# Avec Node.js (http-server)
npx http-server

# Avec Node.js (serve)
npx serve

# Avec l'extension VSCode "Live Server"
# Clic droit → Open with Live Server
```

---

## Export : Partager du code

Il existe deux types d'exports :
1. **Export nommé** (named export) - plusieurs par module
2. **Export par défaut** (default export) - un seul par module

### 1. Exports nommés (Named Exports)

#### Syntaxe 1 : Export direct

```javascript
// math.js

export const PI = 3.14159;

export function addition(a, b) {
  return a + b;
}

export function soustraction(a, b) {
  return a - b;
}

export class Calculatrice {
  constructor() {
    this.resultat = 0;
  }
}
```

#### Syntaxe 2 : Export en fin de fichier

```javascript
// math.js

const PI = 3.14159;

function addition(a, b) {
  return a + b;
}

function soustraction(a, b) {
  return a - b;
}

class Calculatrice {
  constructor() {
    this.resultat = 0;
  }
}

// Export groupé à la fin
export { PI, addition, soustraction, Calculatrice };
```

**Les deux syntaxes sont équivalentes !** Choisissez celle que vous préférez.

#### Export avec alias

```javascript
// math.js

function addition(a, b) {
  return a + b;
}

// Exporter avec un nom différent
export { addition as add };
```

```javascript
// app.js

import { add } from './math.js';

console.log(add(5, 3)); // 8
```

---

### 2. Export par défaut (Default Export)

Chaque module peut avoir **un seul** export par défaut.

#### Syntaxe pour fonctions

```javascript
// calculator.js

export default function calculer(a, b, operation) {
  if (operation === '+') return a + b;
  if (operation === '-') return a - b;
  if (operation === '*') return a * b;
  if (operation === '/') return a / b;
}
```

#### Syntaxe pour classes

```javascript
// User.js

export default class User {
  constructor(nom, email) {
    this.nom = nom;
    this.email = email;
  }

  afficher() {
    console.log(`${this.nom} - ${this.email}`);
  }
}
```

#### Syntaxe pour objets

```javascript
// config.js

export default {
  apiUrl: 'https://api.example.com',
  timeout: 5000,
  debug: true
};
```

#### Export par défaut + exports nommés

On peut **combiner** les deux types d'exports :

```javascript
// utils.js

// Export par défaut
export default function principale() {
  console.log('Fonction principale');
}

// Exports nommés en plus
export const VERSION = '1.0.0';
export function helper() {
  console.log('Fonction helper');
}
```

---

## Import : Utiliser du code

### 1. Import d'exports nommés

```javascript
// math.js
export const PI = 3.14159;
export function addition(a, b) { return a + b; }
export function soustraction(a, b) { return a - b; }
```

```javascript
// app.js

// Import de certains exports
import { PI, addition } from './math.js';

console.log(PI);           // 3.14159
console.log(addition(5, 3)); // 8
```

**Important :**
- Les noms doivent correspondre exactement
- On utilise des accolades `{ }`
- On peut importer un, plusieurs, ou tous les exports

### 2. Import d'export par défaut

```javascript
// calculator.js
export default function calculer(a, b, op) {
  // ...
}
```

```javascript
// app.js

// PAS d'accolades pour l'export par défaut
import calculer from './calculator.js';

// On peut choisir n'importe quel nom
import maFonction from './calculator.js';
import calcul from './calculator.js';

calculer(5, 3, '+'); // 8
```

**Différence clé :**
- Export nommé : `import { nom } from '...'` (nom fixe)
- Export par défaut : `import nomLibre from '...'` (nom libre)

### 3. Import combiné (défaut + nommés)

```javascript
// utils.js
export default function principale() { /* ... */ }
export const VERSION = '1.0.0';
export function helper() { /* ... */ }
```

```javascript
// app.js

import principale, { VERSION, helper } from './utils.js';

principale();         // Fonction par défaut
console.log(VERSION); // "1.0.0"
helper();            // Fonction helper
```

### 4. Import avec alias

```javascript
// Renommer lors de l'import
import { addition as add, soustraction as sub } from './math.js';

console.log(add(5, 3)); // 8
console.log(sub(10, 4)); // 6
```

**Utile pour :**
- Éviter les conflits de noms
- Raccourcir des noms longs
- Clarifier l'usage

### 5. Import de tout (namespace import)

```javascript
// math.js
export const PI = 3.14159;
export function addition(a, b) { return a + b; }
export function soustraction(a, b) { return a - b; }
```

```javascript
// app.js

// Importer TOUT dans un objet
import * as Math from './math.js';

console.log(Math.PI);             // 3.14159
console.log(Math.addition(5, 3));  // 8
console.log(Math.soustraction(10, 4)); // 6
```

**Avantages :**
- Tout est accessible via un namespace
- Évite la pollution du scope
- Clair d'où viennent les fonctions

### 6. Import pour effet de bord uniquement

Parfois, on veut juste exécuter un module sans importer quoi que ce soit :

```javascript
// init.js
console.log('Module initialisé');
document.title = 'Mon App';
```

```javascript
// app.js

// Exécute le module sans import
import './init.js';
```

---

## Chemins d'import

### Chemins relatifs

```javascript
// ✅ Chemins relatifs (toujours avec extension .js)
import { fonction } from './utils.js';           // Même dossier
import { fonction } from '../utils.js';          // Dossier parent
import { fonction } from './helpers/utils.js';   // Sous-dossier
import { fonction } from '../../shared/utils.js'; // Deux niveaux au-dessus
```

**⚠️ Important :**
- Toujours inclure l'extension `.js`
- Utiliser `./` pour le dossier courant
- Utiliser `../` pour remonter d'un niveau

### Chemins absolus (avec configuration)

```javascript
// ❌ Ne fonctionne pas directement dans les navigateurs
import { fonction } from 'utils';
import { fonction } from '@/utils';

// ✅ Nécessite un bundler (Vite, Webpack) ou import maps
```

### Import Maps (navigateurs modernes)

```html
<script type="importmap">
{
  "imports": {
    "utils": "./src/utils.js",
    "lodash": "https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"
  }
}
</script>

<script type="module">
  import { debounce } from 'lodash';
  import { helper } from 'utils';
</script>
```

---

## Exemples pratiques complets

### Exemple 1 : Utilitaires mathématiques

```javascript
// src/utils/math.js

export const PI = 3.14159265359;
export const E = 2.71828182846;

export function addition(a, b) {
  return a + b;
}

export function multiplication(a, b) {
  return a * b;
}

export function puissance(base, exposant) {
  return Math.pow(base, exposant);
}

export function cercleAire(rayon) {
  return PI * rayon * rayon;
}
```

```javascript
// src/app.js

import { PI, addition, cercleAire } from './utils/math.js';

console.log('Pi:', PI);
console.log('5 + 3 =', addition(5, 3));
console.log('Aire cercle (r=5):', cercleAire(5));
```

---

### Exemple 2 : Classe Utilisateur

```javascript
// src/models/User.js

export default class User {
  constructor(nom, email) {
    this.nom = nom;
    this.email = email;
    this.createdAt = new Date();
  }

  afficher() {
    return `${this.nom} (${this.email})`;
  }

  estValide() {
    return this.nom && this.email.includes('@');
  }
}

// Exports nommés supplémentaires
export const USER_ROLES = {
  ADMIN: 'admin',
  USER: 'user',
  GUEST: 'guest'
};

export function creerUtilisateurDefaut() {
  return new User('Invité', 'guest@example.com');
}
```

```javascript
// src/app.js

import User, { USER_ROLES, creerUtilisateurDefaut } from './models/User.js';

// Utilisation de l'export par défaut
const alice = new User('Alice', 'alice@example.com');
console.log(alice.afficher());

// Utilisation des exports nommés
console.log(USER_ROLES.ADMIN);

const invite = creerUtilisateurDefaut();
console.log(invite.afficher());
```

---

### Exemple 3 : Configuration d'application

```javascript
// src/config/database.js

export const dbConfig = {
  host: 'localhost',
  port: 5432,
  database: 'myapp',
  user: 'admin'
};

export function getConnectionString() {
  return `postgres://${dbConfig.user}@${dbConfig.host}:${dbConfig.port}/${dbConfig.database}`;
}
```

```javascript
// src/config/api.js

export default {
  baseUrl: 'https://api.example.com',
  timeout: 5000,
  headers: {
    'Content-Type': 'application/json'
  }
};
```

```javascript
// src/config/index.js

export { dbConfig, getConnectionString } from './database.js';
export { default as apiConfig } from './api.js';
```

```javascript
// src/app.js

import { dbConfig, apiConfig } from './config/index.js';

console.log('Database:', dbConfig.host);
console.log('API:', apiConfig.baseUrl);
```

---

### Exemple 4 : Service API complet

```javascript
// src/services/api.js

const API_URL = 'https://jsonplaceholder.typicode.com';

async function request(endpoint, options = {}) {
  const response = await fetch(`${API_URL}${endpoint}`, {
    headers: {
      'Content-Type': 'application/json',
      ...options.headers
    },
    ...options
  });

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  return response.json();
}

export async function getUsers() {
  return request('/users');
}

export async function getUser(id) {
  return request(`/users/${id}`);
}

export async function createUser(userData) {
  return request('/users', {
    method: 'POST',
    body: JSON.stringify(userData)
  });
}

export async function updateUser(id, userData) {
  return request(`/users/${id}`, {
    method: 'PUT',
    body: JSON.stringify(userData)
  });
}

export async function deleteUser(id) {
  return request(`/users/${id}`, {
    method: 'DELETE'
  });
}
```

```javascript
// src/app.js

import { getUsers, createUser } from './services/api.js';

// Récupérer les utilisateurs
getUsers()
  .then(users => {
    console.log('Utilisateurs:', users);
  })
  .catch(error => {
    console.error('Erreur:', error);
  });

// Créer un utilisateur
createUser({
  name: 'Alice Dupont',
  email: 'alice@example.com'
})
  .then(user => {
    console.log('Utilisateur créé:', user);
  });
```

---

### Exemple 5 : Validation de formulaire

```javascript
// src/utils/validators.js

export function estEmail(email) {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
}

export function estTelephone(tel) {
  const regex = /^(\+33|0)[1-9](\d{2}){4}$/;
  return regex.test(tel.replace(/\s/g, ''));
}

export function estCodePostal(cp) {
  return /^\d{5}$/.test(cp);
}

export function estNonVide(valeur) {
  return valeur && valeur.trim().length > 0;
}

export function longueurMinimum(valeur, min) {
  return valeur && valeur.length >= min;
}
```

```javascript
// src/components/form.js

import {
  estEmail,
  estTelephone,
  estNonVide,
  longueurMinimum
} from '../utils/validators.js';

export function validerFormulaire(formData) {
  const erreurs = [];

  if (!estNonVide(formData.nom)) {
    erreurs.push('Le nom est requis');
  }

  if (!longueurMinimum(formData.nom, 2)) {
    erreurs.push('Le nom doit faire au moins 2 caractères');
  }

  if (!estEmail(formData.email)) {
    erreurs.push('Email invalide');
  }

  if (!estTelephone(formData.telephone)) {
    erreurs.push('Numéro de téléphone invalide');
  }

  return {
    valide: erreurs.length === 0,
    erreurs
  };
}
```

```javascript
// src/app.js

import { validerFormulaire } from './components/form.js';

const formData = {
  nom: 'Alice',
  email: 'alice@example.com',
  telephone: '0612345678'
};

const resultat = validerFormulaire(formData);

if (resultat.valide) {
  console.log('Formulaire valide !');
} else {
  console.log('Erreurs:', resultat.erreurs);
}
```

---

## Réexportation (Re-export)

Utile pour créer un point d'entrée unique pour plusieurs modules.

### Syntaxe de base

```javascript
// src/utils/index.js

// Réexporter des exports nommés
export { addition, soustraction } from './math.js';
export { estEmail, estTelephone } from './validators.js';

// Réexporter tout d'un module
export * from './string.js';

// Réexporter un export par défaut en tant qu'export nommé
export { default as User } from '../models/User.js';
```

```javascript
// src/app.js

// Un seul import au lieu de plusieurs
import { addition, estEmail, User } from './utils/index.js';
```

### Pattern barrel (index.js)

```
src/
├── components/
│   ├── Header.js
│   ├── Footer.js
│   ├── Sidebar.js
│   └── index.js  ← Barrel file
└── app.js
```

```javascript
// src/components/index.js (barrel)

export { default as Header } from './Header.js';
export { default as Footer } from './Footer.js';
export { default as Sidebar } from './Sidebar.js';
```

```javascript
// src/app.js

// ✅ Import groupé
import { Header, Footer, Sidebar } from './components/index.js';

// Au lieu de :
// ❌ Multiples imports
// import Header from './components/Header.js';
// import Footer from './components/Footer.js';
// import Sidebar from './components/Sidebar.js';
```

---

## Import dynamique

Charger des modules **à la demande** (lazy loading).

### Syntaxe

```javascript
// Import dynamique retourne une Promise
import('./module.js')
  .then(module => {
    // Utiliser le module
    module.maFonction();
  })
  .catch(error => {
    console.error('Erreur de chargement:', error);
  });

// Ou avec async/await
async function chargerModule() {
  try {
    const module = await import('./module.js');
    module.maFonction();
  } catch (error) {
    console.error('Erreur:', error);
  }
}
```

### Exemple pratique : Chargement conditionnel

```javascript
// app.js

const bouton = document.getElementById('chargerChart');

bouton.addEventListener('click', async () => {
  // Charger le module uniquement au clic
  const { creerGraphique } = await import('./chart.js');

  creerGraphique(document.getElementById('canvas'));

  bouton.disabled = true;
  bouton.textContent = 'Graphique chargé';
});
```

### Exemple : Routes dynamiques

```javascript
// router.js

async function naviguer(page) {
  let module;

  switch(page) {
    case 'home':
      module = await import('./pages/Home.js');
      break;
    case 'about':
      module = await import('./pages/About.js');
      break;
    case 'contact':
      module = await import('./pages/Contact.js');
      break;
  }

  module.default.render();
}

// Charge uniquement la page nécessaire
naviguer('home');
```

---

## Bonnes pratiques

### 1. Un module, une responsabilité

```javascript
// ✅ BON : Chaque module a un objectif clair
// math.js - Fonctions mathématiques
// validators.js - Validateurs
// api.js - Appels API

// ❌ MAUVAIS : Tout dans un seul fichier
// utils.js - Math + validateurs + API + ...
```

### 2. Exports nommés vs export par défaut

```javascript
// ✅ Préférer les exports nommés pour :
// - Plusieurs exports
// - Fonctions utilitaires
// - Constantes

export function add(a, b) { return a + b; }
export function multiply(a, b) { return a * b; }

// ✅ Export par défaut pour :
// - Un seul export principal
// - Classes
// - Composants React/Vue

export default class Calculator { /* ... */ }
```

### 3. Nommer explicitement les exports

```javascript
// ✅ BON
export function calculerTVA(montant) { /* ... */ }

// ❌ ÉVITER
export default function(montant) { /* ... */ }
// Pas clair quand importé
```

### 4. Organiser les imports

```javascript
// ✅ BON : Grouper et organiser
// 1. Bibliothèques externes
import React from 'react';
import axios from 'axios';

// 2. Modules internes (absolus)
import { config } from '@/config';

// 3. Modules locaux (relatifs)
import { helper } from './utils/helper.js';
import UserService from './services/UserService.js';

// 4. Styles
import './styles.css';
```

### 5. Éviter les imports circulaires

```javascript
// ❌ MAUVAIS : Imports circulaires
// a.js
import { funcB } from './b.js';
export function funcA() { funcB(); }

// b.js
import { funcA } from './a.js';
export function funcB() { funcA(); }

// ✅ BON : Extraire dans un troisième module
// shared.js
export function sharedLogic() { /* ... */ }

// a.js
import { sharedLogic } from './shared.js';

// b.js
import { sharedLogic } from './shared.js';
```

### 6. Extensions de fichiers

```javascript
// ✅ Toujours inclure .js dans les navigateurs
import { func } from './utils.js';

// ❌ Fonctionne avec bundlers mais pas navigateur natif
import { func } from './utils';
```

---

## Pièges courants

### 1. Oublier type="module"

```html
<!-- ❌ Ne fonctionne pas -->
<script src="app.js"></script>

<!-- ✅ Correct -->
<script type="module" src="app.js"></script>
```

### 2. Modifier les exports importés

```javascript
// constants.js
export const CONFIG = { debug: true };

// app.js
import { CONFIG } from './constants.js';

CONFIG.debug = false; // ⚠️ Modifie l'original !

// Autre module
import { CONFIG } from './constants.js';
console.log(CONFIG.debug); // false
```

**Solution :** Utiliser Object.freeze() ou des getters

```javascript
// constants.js
export const CONFIG = Object.freeze({
  debug: true
});
```

### 3. CORS avec modules locaux

```javascript
// ❌ Erreur CORS si ouvert avec file://
// file:///C:/projet/index.html

// ✅ Nécessite un serveur
// http://localhost:3000/index.html
```

### 4. Import de variables non exportées

```javascript
// utils.js
const SECRET = 'abc123'; // Pas exporté

export function getSecret() {
  return SECRET;
}

// app.js
import { SECRET } from './utils.js'; // ❌ Erreur
import { getSecret } from './utils.js'; // ✅ OK
```

---

## Modules dans Node.js

### Activer les modules ES6

```json
// package.json
{
  "type": "module"
}
```

Ou utiliser l'extension `.mjs` :

```javascript
// fichier.mjs
import fs from 'fs';
```

### Import de modules Node.js

```javascript
// Modules natifs
import fs from 'fs';
import path from 'path';
import { readFile } from 'fs/promises';

// Modules npm
import express from 'express';
import axios from 'axios';
```

### Compatibilité avec CommonJS

```javascript
// ✅ Import de module ES6 vers CommonJS possible
import { createServer } from 'http';

// ⚠️ Import de CommonJS vers ES6 nécessite default
import pkg from 'some-commonjs-package';
```

---

## Différence avec CommonJS

### CommonJS (ancien, Node.js)

```javascript
// Exports
module.exports = function() { /* ... */ };
exports.fonction = function() { /* ... */ };

// Imports
const monModule = require('./monModule');
const { fonction } = require('./monModule');
```

### ES6 Modules (moderne)

```javascript
// Exports
export default function() { /* ... */ }
export function fonction() { /* ... */ }

// Imports
import monModule from './monModule.js';
import { fonction } from './monModule.js';
```

**Différences clés :**
- ES6 : Statique (analyse à la compilation)
- CommonJS : Dynamique (exécution runtime)
- ES6 : Meilleure optimisation (tree-shaking)
- ES6 : Standard du web

---

## Tree Shaking

Les bundlers modernes peuvent **supprimer le code non utilisé** avec les modules ES6.

```javascript
// utils.js
export function used() { /* ... */ }
export function notUsed() { /* ... */ }

// app.js
import { used } from './utils.js';

// Build final : notUsed() est supprimée automatiquement
```

---

## Points clés à retenir

✅ **Export nommé** : `export const x = 1;` ou `export { x }`

✅ **Export par défaut** : `export default class MyClass {}`

✅ **Import nommé** : `import { x } from './module.js'`

✅ **Import par défaut** : `import MyClass from './module.js'`

✅ **Import namespace** : `import * as Utils from './utils.js'`

✅ **Import dynamique** : `const module = await import('./module.js')`

✅ **Toujours inclure .js** dans les chemins (navigateurs)

✅ **type="module"** requis dans HTML

✅ **Serveur local** nécessaire pour développement

⚠️ **Scope isolé** : Variables non accessibles globalement

⚠️ **Mode strict** : Activé automatiquement

⚠️ **CORS** : Attention aux politiques de sécurité

---

## Conclusion

Les modules ES6 sont devenus la pierre angulaire de l'organisation du code JavaScript moderne. Ils offrent :

- 📦 **Organisation claire** du code
- 🔒 **Encapsulation** et isolation
- ♻️ **Réutilisabilité** facilitée
- 🚀 **Performance** optimisée (tree-shaking)
- 🌐 **Standard universel** (navigateurs + Node.js)

Maîtriser les imports/exports est essentiel pour travailler avec des frameworks modernes (React, Vue, Angular) et pour structurer efficacement vos applications JavaScript ! 🎯

---

## Ressources complémentaires

- **MDN** : [JavaScript modules](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Modules)
- **ES6 Features** : [http://es6-features.org/](http://es6-features.org/)
- **Can I Use** : Vérifier le support navigateur des modules

**Prochaine étape** : Découvrir les bundlers (Vite, Webpack) qui optimisent l'utilisation des modules !

⏭️ [Intégration HTML/CSS/JavaScript](/06-integration-html-css-javascript/README.md)
