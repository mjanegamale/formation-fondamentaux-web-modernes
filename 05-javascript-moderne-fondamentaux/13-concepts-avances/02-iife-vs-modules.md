🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.13.2 - IIFE vs Modules ES6 🆕

## Introduction

Dans l'histoire de JavaScript, les développeurs ont toujours eu besoin d'**organiser et isoler leur code**. Deux solutions majeures ont émergé :
- **IIFE** (Immediately Invoked Function Expression) : la solution historique
- **Modules ES6** : la solution moderne et standard

> 🆕 **Approche moderne** : Aujourd'hui, on utilise les **modules ES6**. Mais comprendre les IIFE vous aidera à lire du code ancien et à comprendre pourquoi les modules sont une amélioration majeure.

---

## IIFE : La solution historique

### Qu'est-ce qu'une IIFE ?

**IIFE** signifie **Immediately Invoked Function Expression** (Expression de Fonction Immédiatement Invoquée).

C'est une fonction qui :
1. Est définie
2. Est exécutée immédiatement
3. Crée un scope isolé

### Syntaxe d'une IIFE

```javascript
// Syntaxe de base
(function() {
  console.log("Je m'exécute immédiatement !");
})();

// Avec des paramètres
(function(nom) {
  console.log(`Bonjour ${nom}`);
})("Alice");
```

**Décomposition :**
```javascript
(function() {    // 1. Définition de la fonction
  // code
})               // 2. Parenthèses pour l'expression
();              // 3. Appel immédiat
```

### Pourquoi utiliser une IIFE ?

#### 1. **Éviter la pollution du scope global**

**❌ Sans IIFE :**
```javascript
// fichier1.js
var compteur = 0;
var nom = "Alice";

function incrementer() {
  compteur++;
}

// fichier2.js
var compteur = 10; // ⚠️ Écrase la variable du fichier1 !
var nom = "Bob";   // ⚠️ Conflit !
```

**✅ Avec IIFE :**
```javascript
// fichier1.js
(function() {
  var compteur = 0;
  var nom = "Alice";

  function incrementer() {
    compteur++;
  }

  // Ces variables sont isolées !
})();

// fichier2.js
(function() {
  var compteur = 10; // ✅ Pas de conflit
  var nom = "Bob";   // ✅ Isolé
})();
```

#### 2. **Créer des variables privées**

```javascript
const compteur = (function() {
  let count = 0; // Variable privée

  return {
    incrementer: function() {
      count++;
      return count;
    },
    obtenir: function() {
      return count;
    }
  };
})();

console.log(compteur.incrementer()); // 1
console.log(compteur.incrementer()); // 2
console.log(compteur.obtenir());     // 2
console.log(compteur.count);         // undefined (privé)
```

#### 3. **Module Pattern classique**

```javascript
const MonModule = (function() {
  // Variables privées
  const API_KEY = "secret123";
  let utilisateurs = [];

  // Fonction privée
  function validerUtilisateur(user) {
    return user && user.nom;
  }

  // API publique
  return {
    ajouter: function(user) {
      if (validerUtilisateur(user)) {
        utilisateurs.push(user);
      }
    },

    lister: function() {
      return [...utilisateurs]; // Copie pour protection
    }
  };
})();

MonModule.ajouter({ nom: "Alice" });
console.log(MonModule.lister()); // [{ nom: "Alice" }]
console.log(MonModule.API_KEY);  // undefined (privé)
```

---

## Modules ES6 : La solution moderne 🆕

### Qu'est-ce qu'un module ES6 ?

Un **module ES6** est un fichier JavaScript qui peut :
- **Exporter** des fonctions, objets ou variables
- **Importer** des fonctions, objets ou variables d'autres modules
- Avoir son propre scope isolé automatiquement

### Syntaxe de base

#### Export (partager du code)

```javascript
// mathUtils.js

// Export nommé
export const PI = 3.14159;

export function addition(a, b) {
  return a + b;
}

export function multiplication(a, b) {
  return a * b;
}

// Ou exporter en une fois
const PI = 3.14159;
function addition(a, b) { return a + b; }
function multiplication(a, b) { return a * b; }

export { PI, addition, multiplication };
```

#### Import (utiliser du code)

```javascript
// app.js

// Import nommé
import { PI, addition, multiplication } from './mathUtils.js';

console.log(PI);                    // 3.14159
console.log(addition(5, 3));        // 8
console.log(multiplication(4, 2));  // 8
```

### Export par défaut

Chaque module peut avoir **un seul export par défaut** :

```javascript
// utilisateur.js
export default class Utilisateur {
  constructor(nom) {
    this.nom = nom;
  }

  saluer() {
    console.log(`Bonjour, je suis ${this.nom}`);
  }
}
```

```javascript
// app.js
import Utilisateur from './utilisateur.js';

const user = new Utilisateur("Alice");
user.saluer(); // "Bonjour, je suis Alice"
```

### Importer tout d'un module

```javascript
// mathUtils.js
export const PI = 3.14159;
export function addition(a, b) { return a + b; }
export function soustraction(a, b) { return a - b; }
```

```javascript
// app.js
import * as Math from './mathUtils.js';

console.log(Math.PI);           // 3.14159
console.log(Math.addition(5, 3)); // 8
```

### Renommer lors de l'import/export

```javascript
// Export avec alias
export { maFonction as fonctionPublique };

// Import avec alias
import { addition as add } from './mathUtils.js';

console.log(add(2, 3)); // 5
```

---

## IIFE vs Modules ES6 : Comparaison

### 1. **Isolation du scope**

**IIFE :**
```javascript
(function() {
  const secret = "caché";
  console.log(secret);
})();
console.log(secret); // ❌ Erreur
```

**Modules ES6 :**
```javascript
// module.js
const secret = "caché"; // Automatiquement privé
console.log(secret);

// app.js
import './module.js';
console.log(secret); // ❌ Erreur (non exporté)
```

✅ **Gagnant : Modules ES6** - Isolation automatique, plus claire

---

### 2. **Réutilisation du code**

**IIFE :**
```javascript
// Difficile de réutiliser du code entre fichiers
const MonModule = (function() {
  return {
    maFonction: function() { /* ... */ }
  };
})();

// Dans un autre fichier, il faut :
// 1. Charger le script dans le bon ordre dans le HTML
// 2. Utiliser une variable globale
```

**Modules ES6 :**
```javascript
// utils.js
export function maFonction() { /* ... */ }

// app.js
import { maFonction } from './utils.js';
maFonction();
```

✅ **Gagnant : Modules ES6** - Import/Export explicite et simple

---

### 3. **Gestion des dépendances**

**IIFE :**
```html
<!-- Il faut charger dans le BON ORDRE -->
<script src="jquery.js"></script>
<script src="monModule.js"></script> <!-- Dépend de jQuery -->
<script src="app.js"></script>       <!-- Dépend de monModule -->
```

**Modules ES6 :**
```javascript
// app.js
import { MonModule } from './monModule.js';
import $ from 'jquery';

// L'ordre d'import n'a pas d'importance
// Les dépendances sont gérées automatiquement
```

✅ **Gagnant : Modules ES6** - Gestion automatique des dépendances

---

### 4. **Lisibilité et maintenabilité**

**IIFE :**
```javascript
const App = (function() {
  const config = {};

  return {
    init: function() { /* ... */ },
    update: function() { /* ... */ }
  };
})();
```

**Modules ES6 :**
```javascript
// config.js
export const config = {};

// app.js
import { config } from './config.js';

export function init() { /* ... */ }
export function update() { /* ... */ }
```

✅ **Gagnant : Modules ES6** - Plus lisible, structure claire

---

## Utilisation pratique des Modules ES6

### Structure d'un projet moderne

```
mon-projet/
├── index.html
├── src/
│   ├── app.js          (point d'entrée)
│   ├── utils/
│   │   ├── math.js
│   │   └── string.js
│   ├── components/
│   │   ├── header.js
│   │   └── footer.js
│   └── services/
│       └── api.js
```

### Exemple complet

**1. Fichier HTML**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon App</title>
</head>
<body>
  <!-- ⚠️ Important : type="module" -->
  <script type="module" src="src/app.js"></script>
</body>
</html>
```

**2. Module utilitaire**
```javascript
// src/utils/math.js
export function addition(a, b) {
  return a + b;
}

export function multiplication(a, b) {
  return a * b;
}

export const PI = 3.14159;
```

**3. Module service**
```javascript
// src/services/api.js
const API_URL = 'https://api.example.com';

export async function fetchUtilisateurs() {
  const response = await fetch(`${API_URL}/users`);
  return response.json();
}

export async function creerUtilisateur(data) {
  const response = await fetch(`${API_URL}/users`, {
    method: 'POST',
    body: JSON.stringify(data)
  });
  return response.json();
}
```

**4. Application principale**
```javascript
// src/app.js
import { addition, PI } from './utils/math.js';
import { fetchUtilisateurs } from './services/api.js';

console.log(addition(5, 3)); // 8
console.log(PI);             // 3.14159

// Utilisation asynchrone
fetchUtilisateurs()
  .then(users => console.log(users))
  .catch(error => console.error(error));
```

---

## Cas d'usage : IIFE encore pertinente aujourd'hui ?

### Quand utiliser IIFE (rare) ⚠️

**1. Scripts inline dans HTML**
```html
<script>
  (function() {
    // Code isolé pour ce script uniquement
    const temp = "valeur temporaire";
    console.log(temp);
  })();
  // temp n'existe pas ici
</script>
```

**2. Compatibilité avec du vieux code**
```javascript
// Maintenir du code legacy
const LegacyModule = (function() {
  // ...
})();
```

### Quand utiliser Modules ES6 (toujours) ✅

**1. Tout nouveau projet**
```javascript
// Toujours préférer les modules
export function maFonction() { /* ... */ }
```

**2. Applications modernes**
- React, Vue, Angular utilisent tous les modules ES6
- Build tools (Vite, Webpack) optimisent les modules
- Support natif dans tous les navigateurs modernes

**3. Node.js**
```javascript
// package.json
{
  "type": "module"
}

// Puis utiliser import/export
import fs from 'fs';
```

---

## Migration IIFE → Modules ES6

### Avant (IIFE)
```javascript
// app.js
const App = (function() {
  const config = {
    apiUrl: 'https://api.example.com'
  };

  function init() {
    console.log('App initialisée');
  }

  return {
    init: init,
    config: config
  };
})();

App.init();
```

### Après (Modules ES6)
```javascript
// config.js
export const config = {
  apiUrl: 'https://api.example.com'
};

// app.js
import { config } from './config.js';

export function init() {
  console.log('App initialisée');
}

// main.js
import { init } from './app.js';
init();
```

---

## Avantages des Modules ES6

✅ **Syntaxe standardisée** : Fait partie d'ECMAScript

✅ **Support natif** : Navigateurs et Node.js

✅ **Imports statiques** : Analyse possible avant exécution

✅ **Tree shaking** : Outils peuvent supprimer le code non utilisé

✅ **Chargement asynchrone** : Modules chargés en parallèle

✅ **Scope isolé automatiquement** : Pas besoin de wrapper

✅ **Meilleure organisation** : Un fichier = un module

✅ **Outils de développement** : Meilleur support IDE

---

## Limitations et considérations

### Modules ES6

⚠️ **Mode strict automatique** : Les modules sont en strict mode par défaut

```javascript
// Dans un module, ceci génère une erreur
x = 5; // ❌ ReferenceError: x is not defined
```

⚠️ **`this` au niveau supérieur vaut `undefined`**

```javascript
// Dans un module
console.log(this); // undefined

// Avec IIFE ou script normal
console.log(this); // window (dans un navigateur)
```

⚠️ **CORS** : Lors du chargement de modules locaux

```javascript
// ❌ Ne fonctionne pas en ouvrant le fichier directement
// file:///C:/mon-projet/index.html

// ✅ Nécessite un serveur local
// http://localhost:3000/index.html
```

**Solution** : Utiliser un serveur de développement
```bash
# Avec Node.js
npx serve

# Avec Python
python -m http.server 8000

# Avec VSCode
# Extension : Live Server
```

---

## Compatibilité navigateurs

### Modules ES6

✅ **Support excellent** (2024) :
- Chrome 61+
- Firefox 60+
- Safari 10.1+
- Edge 16+

### Fallback pour anciens navigateurs

```html
<!-- Navigateurs modernes -->
<script type="module" src="app.js"></script>

<!-- Fallback pour anciens navigateurs -->
<script nomodule src="app-legacy.js"></script>
```

---

## Tableau récapitulatif

| Critère | IIFE ⚠️ | Modules ES6 ✅ |
|---------|---------|----------------|
| **Syntaxe** | Complexe | Simple et claire |
| **Isolation** | Manuelle | Automatique |
| **Réutilisation** | Difficile | Facile (import/export) |
| **Dépendances** | Ordre manuel | Gestion automatique |
| **Standard** | Pattern, pas standard | Standard ECMAScript |
| **Outils** | Support limité | Excellent support |
| **Performance** | - | Optimisations possibles |
| **Usage moderne** | ❌ Legacy | ✅ Recommandé |

---

## Recommandations finales

### Pour du nouveau code 🆕

✅ **Toujours utiliser les modules ES6**
```javascript
// ✅ BON
export function maFonction() { /* ... */ }

// ❌ ÉVITER
const MonModule = (function() {
  return { maFonction: function() { /* ... */ } };
})();
```

### Pour du code existant ⚠️

- **Comprendre** les IIFE pour lire du code legacy
- **Migrer progressivement** vers les modules ES6
- **Tester** après migration

### Exceptions rares

- Scripts inline dans HTML (petits scripts)
- Compatibilité extrême (navigateurs très anciens)
- Contraintes techniques spécifiques

---

## Exemple final : Projet complet moderne

```javascript
// utils/validators.js
export function estEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

export function estTelephone(tel) {
  return /^\d{10}$/.test(tel);
}

// services/userService.js
import { estEmail } from '../utils/validators.js';

export async function creerUtilisateur(data) {
  if (!estEmail(data.email)) {
    throw new Error('Email invalide');
  }

  const response = await fetch('/api/users', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
  });

  return response.json();
}

// app.js
import { creerUtilisateur } from './services/userService.js';

async function init() {
  try {
    const user = await creerUtilisateur({
      nom: 'Dupont',
      email: 'dupont@example.com'
    });
    console.log('Utilisateur créé:', user);
  } catch (error) {
    console.error('Erreur:', error);
  }
}

init();
```

---

## Conclusion

- **IIFE** : Solution historique ingénieuse, mais dépassée
- **Modules ES6** : Standard moderne, à utiliser systématiquement
- **Migration** : Progressivement possible depuis IIFE vers modules

Les modules ES6 ne sont pas juste une amélioration des IIFE, c'est une refonte complète de l'organisation du code JavaScript. Ils sont :
- Plus simples à comprendre
- Plus faciles à maintenir
- Mieux supportés par les outils
- Standard de l'industrie

🚀 **Conseil** : Commencez tous vos nouveaux projets avec des modules ES6, et ne regardez les IIFE que pour comprendre du code ancien !

⏭️ [Méthodes call, apply, bind](/05-javascript-moderne-fondamentaux/13-concepts-avances/03-call-apply-bind.md)
