🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.1.3 - Modules JavaScript et type="module"

## Introduction

Imaginez que vous construisez un grand puzzle. Au début, avec quelques pièces, tout va bien. Mais avec 1000 pièces toutes mélangées dans une boîte, ça devient vite ingérable !

C'est exactement le problème que les **modules JavaScript** viennent résoudre. Au lieu d'avoir tout votre code dans un seul énorme fichier (ou plusieurs fichiers qui se marchent dessus), les modules vous permettent d'organiser votre code en **petits morceaux indépendants et réutilisables**.

### Ce que vous allez apprendre

Dans ce chapitre, nous allons découvrir :
- 📦 Ce que sont les modules JavaScript (ES6 modules)
- 🔧 Comment utiliser `import` et `export`
- 🎯 L'attribut `type="module"` dans les balises `<script>`
- 🆚 Les différences avec les scripts classiques
- ✨ Les avantages des modules dans vos projets

---

## Le problème sans modules

### Scenario 1 : Tout dans un seul fichier

Voici ce qui arrive quand on met tout le code dans un seul fichier :

```javascript
// app.js - 2000 lignes de code !

// Fonctions utilitaires
function formatDate(date) { /* ... */ }
function capitalize(str) { /* ... */ }
function slugify(text) { /* ... */ }
// ... 20 autres fonctions utilitaires

// Gestion du slider
function initSlider() { /* ... */ }
function nextSlide() { /* ... */ }
function prevSlide() { /* ... */ }
// ... code du slider

// Gestion du formulaire
function validateForm() { /* ... */ }
function submitForm() { /* ... */ }
// ... code du formulaire

// Gestion de la modal
function openModal() { /* ... */ }
function closeModal() { /* ... */ }
// ... code de la modal

// Gestion du menu
function toggleMenu() { /* ... */ }
// ... code du menu

// Et encore 1500 lignes...
```

**Problèmes :**
- ❌ Impossible de s'y retrouver (2000 lignes !)
- ❌ Difficile de maintenir
- ❌ Impossible de réutiliser une partie du code
- ❌ Risque de conflits de noms
- ❌ Tout est chargé même si on n'en a pas besoin

### Scenario 2 : Plusieurs fichiers sans modules

Avant les modules, on faisait comme ça :

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mon Site</title>
</head>
<body>
    <!-- Contenu -->

    <!-- Charger tous les scripts -->
    <script src="utils.js"></script>
    <script src="slider.js"></script>
    <script src="form.js"></script>
    <script src="modal.js"></script>
    <script src="menu.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

**Problèmes :**
- ❌ Toutes les fonctions sont **globales** (pollution du scope global)
- ❌ **Ordre de chargement critique** : si `app.js` utilise `utils.js`, il doit être après
- ❌ **Conflits de noms** : si deux fichiers ont une fonction `init()`, collision !
- ❌ Difficile de savoir quelles dépendances chaque fichier a besoin
- ❌ Tout est chargé, même ce qui n'est pas utilisé

### Exemple de pollution du scope global

```javascript
// utils.js
function formatDate(date) {
    return date.toLocaleDateString();
}

// slider.js
function formatDate(date) {  // ❌ CONFLIT ! Même nom
    return date.toISOString();
}

// Quelle version de formatDate() sera utilisée ?
// La dernière chargée écrase la première !
```

---

## La solution : Les modules ES6

### Qu'est-ce qu'un module ?

> Un **module** est un fichier JavaScript qui peut **exporter** des fonctions, objets ou valeurs pour qu'ils soient **importés** et utilisés dans d'autres fichiers.

**Avantages :**
- ✅ **Isolation** : chaque module a son propre scope
- ✅ **Réutilisabilité** : les modules peuvent être importés partout
- ✅ **Dépendances explicites** : on sait exactement ce dont chaque fichier a besoin
- ✅ **Pas de pollution globale** : rien n'est global par défaut
- ✅ **Chargement optimisé** : seul ce qui est importé est utilisé

### Une analogie simple

Pensez aux modules comme à des **boîtes à outils** :

🧰 **Boîte 1 : Outils de menuiserie**
- Marteau
- Scie
- Tournevis

🧰 **Boîte 2 : Outils de plomberie**
- Clé à molette
- Joint
- Ruban téflon

Quand vous faites de la menuiserie, vous **importez** seulement la boîte de menuiserie. Vous n'avez pas tous les outils du monde éparpillés devant vous, juste ceux dont vous avez besoin !

---

## Syntaxe des modules : Export

### Export nommé (Named Export)

C'est la méthode la plus courante. Vous exportez plusieurs choses depuis un même fichier.

#### Méthode 1 : Export au moment de la déclaration

```javascript
// utils.js

// Exporter une fonction
export function formatDate(date) {
    return date.toLocaleDateString('fr-FR');
}

// Exporter une autre fonction
export function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
}

// Exporter une constante
export const API_URL = 'https://api.example.com';

// Exporter un objet
export const config = {
    timeout: 5000,
    retries: 3
};
```

#### Méthode 2 : Export à la fin du fichier

```javascript
// utils.js

function formatDate(date) {
    return date.toLocaleDateString('fr-FR');
}

function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
}

const API_URL = 'https://api.example.com';

// Exporter tout à la fin
export { formatDate, capitalize, API_URL };
```

Les deux méthodes sont équivalentes. Choisissez celle qui vous semble la plus claire.

### Export par défaut (Default Export)

Chaque module peut avoir **un seul** export par défaut. C'est utile quand un fichier exporte principalement une chose.

```javascript
// Slider.js

// Export par défaut d'une classe
export default class Slider {
    constructor(selector) {
        this.slider = document.querySelector(selector);
        this.currentSlide = 0;
    }

    next() {
        this.currentSlide++;
        this.updateSlider();
    }

    prev() {
        this.currentSlide--;
        this.updateSlider();
    }

    updateSlider() {
        // Logique de mise à jour
    }
}
```

Ou avec une fonction :

```javascript
// api.js

// Export par défaut d'une fonction
export default async function fetchData(url) {
    try {
        const response = await fetch(url);
        return await response.json();
    } catch (error) {
        console.error('Erreur:', error);
        throw error;
    }
}
```

### Combiner exports nommés et export par défaut

Vous pouvez avoir les deux dans un même fichier :

```javascript
// calculator.js

// Export par défaut
export default class Calculator {
    add(a, b) { return a + b; }
    subtract(a, b) { return a - b; }
}

// Exports nommés supplémentaires
export const PI = 3.14159;
export const E = 2.71828;

export function square(x) {
    return x * x;
}
```

---

## Syntaxe des modules : Import

### Import nommé

Pour importer des exports nommés, utilisez la même syntaxe :

```javascript
// app.js

// Importer des fonctions spécifiques
import { formatDate, capitalize } from './utils.js';

// Utilisation
const today = formatDate(new Date());
const name = capitalize('john');

console.log(today, name);
```

**Important :**
- Les noms entre accolades doivent **exactement correspondre** aux noms exportés
- Le chemin doit inclure l'extension `.js`
- Le chemin commence par `./` (relatif) ou `/` (absolu)

### Import avec alias

Vous pouvez renommer ce que vous importez :

```javascript
// app.js

// Renommer pour éviter les conflits ou clarifier
import { formatDate as formatDateFR } from './utils.js';
import { formatDate as formatDateEN } from './utils-en.js';

const dateFR = formatDateFR(new Date());
const dateEN = formatDateEN(new Date());
```

### Import par défaut

L'import par défaut se fait **sans accolades** et vous pouvez choisir le nom :

```javascript
// app.js

// Import de l'export par défaut (pas d'accolades)
import Slider from './Slider.js';

// Le nom peut être différent de l'export
import MonSlider from './Slider.js';  // ✅ Ça marche aussi

// Utilisation
const slider = new Slider('.gallery');
```

### Import mixte (défaut + nommés)

```javascript
// app.js

// Import de l'export par défaut ET des exports nommés
import Calculator, { PI, E, square } from './calculator.js';

const calc = new Calculator();
console.log(calc.add(2, 3));
console.log(PI);
console.log(square(5));
```

### Import de tout

Vous pouvez importer tout le contenu d'un module sous un namespace :

```javascript
// app.js

// Importer tout sous le nom "Utils"
import * as Utils from './utils.js';

// Utilisation avec le namespace
const date = Utils.formatDate(new Date());
const text = Utils.capitalize('hello');
console.log(Utils.API_URL);
```

### Import pour effet de bord

Parfois, vous voulez juste exécuter un fichier sans rien importer :

```javascript
// app.js

// Exécute polyfills.js mais n'importe rien
import './polyfills.js';
```

---

## L'attribut type="module"

### Utilisation dans le HTML

Pour utiliser des modules dans votre HTML, vous devez ajouter l'attribut `type="module"` :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon Application avec Modules</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="app"></div>

    <!-- ✅ Script de type module -->
    <script type="module" src="app.js"></script>
</body>
</html>
```

**Sans `type="module"`, les imports ne fonctionneront pas !**

### Scripts inline avec modules

Vous pouvez aussi écrire du code module directement dans le HTML :

```html
<script type="module">
    import { formatDate } from './utils.js';

    const today = formatDate(new Date());
    document.getElementById('date').textContent = today;
</script>
```

---

## Différences entre scripts classiques et modules

### Tableau comparatif

| Caractéristique | Script classique | Module (`type="module"`) |
|----------------|------------------|-------------------------|
| **Scope** | Global | Local au module |
| **Mode strict** | Optionnel | Toujours activé (`'use strict'`) |
| **Imports** | ❌ Non supportés | ✅ `import` / `export` |
| **Chargement** | Bloquant (par défaut) | Différé automatiquement |
| **`this` au niveau racine** | `window` | `undefined` |
| **Variables globales** | Créées automatiquement | Doivent être explicites |
| **CORS** | Pas de restriction | Soumis aux règles CORS |

### Détails des différences

#### 1. Scope isolé

**Script classique :**
```javascript
// script.js
var username = 'John';  // ❌ Variable globale !
console.log(window.username);  // 'John'
```

**Module :**
```javascript
// app.js (module)
const username = 'John';  // ✅ Variable locale au module
console.log(window.username);  // undefined
```

#### 2. Mode strict automatique

**Script classique :**
```javascript
// script.js
function test() {
    x = 10;  // ✅ Ça marche (crée une variable globale)
}
```

**Module :**
```javascript
// app.js (module)
function test() {
    x = 10;  // ❌ Erreur : x is not defined
    // Le mode strict est automatiquement activé
}
```

#### 3. Chargement différé (defer)

Les modules sont automatiquement chargés avec un comportement similaire à `defer` :

```html
<!-- Script classique : bloque le parsing HTML -->
<script src="script.js"></script>

<!-- Module : ne bloque pas, se charge en parallèle -->
<script type="module" src="app.js"></script>
```

#### 4. Compatibilité avec les anciens navigateurs

Pour supporter les anciens navigateurs qui ne comprennent pas les modules, utilisez `nomodule` :

```html
<!-- Pour les navigateurs modernes -->
<script type="module" src="app.js"></script>

<!-- Fallback pour les anciens navigateurs -->
<script nomodule src="app-legacy.js"></script>
```

---

## Exemple complet : Refactoring avec modules

### Avant : Sans modules

**Structure :**
```
projet-sans-modules/
├── index.html
└── scripts/
    ├── utils.js
    ├── slider.js
    ├── form.js
    └── app.js
```

**index.html :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <title>Sans Modules</title>
</head>
<body>
    <div id="app"></div>

    <!-- ❌ Ordre critique ! -->
    <script src="scripts/utils.js"></script>
    <script src="scripts/slider.js"></script>
    <script src="scripts/form.js"></script>
    <script src="scripts/app.js"></script>
</body>
</html>
```

**utils.js :**
```javascript
// ❌ Fonctions globales
function formatDate(date) {
    return date.toLocaleDateString('fr-FR');
}

function debounce(func, wait) {
    let timeout;
    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func(...args), wait);
    };
}
```

**slider.js :**
```javascript
// ❌ Classe globale
class Slider {
    constructor(selector) {
        this.element = document.querySelector(selector);
        this.init();
    }
    // ...
}
```

**app.js :**
```javascript
// ❌ Utilise les variables globales
document.addEventListener('DOMContentLoaded', () => {
    const slider = new Slider('.gallery');  // Où est défini Slider ?
    const date = formatDate(new Date());    // Où est défini formatDate ?
});
```

### Après : Avec modules

**Structure :**
```
projet-avec-modules/
├── index.html
└── js/
    ├── utils/
    │   └── helpers.js
    ├── components/
    │   ├── Slider.js
    │   └── Form.js
    └── main.js
```

**index.html :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Avec Modules</title>
</head>
<body>
    <div class="gallery">
        <!-- Slides -->
    </div>

    <form class="contact-form">
        <!-- Champs -->
    </form>

    <!-- ✅ Un seul point d'entrée -->
    <script type="module" src="js/main.js"></script>
</body>
</html>
```

**js/utils/helpers.js :**
```javascript
// ✅ Exports explicites
export function formatDate(date) {
    return date.toLocaleDateString('fr-FR', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
    });
}

export function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

export function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}
```

**js/components/Slider.js :**
```javascript
// ✅ Export par défaut d'une classe
export default class Slider {
    constructor(selector, options = {}) {
        this.element = document.querySelector(selector);
        this.currentSlide = 0;
        this.options = {
            autoplay: false,
            interval: 3000,
            ...options
        };

        if (this.element) {
            this.init();
        }
    }

    init() {
        this.slides = this.element.querySelectorAll('.slide');
        this.setupControls();

        if (this.options.autoplay) {
            this.startAutoplay();
        }
    }

    setupControls() {
        const prevBtn = this.element.querySelector('.slider__prev');
        const nextBtn = this.element.querySelector('.slider__next');

        if (prevBtn) {
            prevBtn.addEventListener('click', () => this.prev());
        }

        if (nextBtn) {
            nextBtn.addEventListener('click', () => this.next());
        }
    }

    next() {
        this.currentSlide = (this.currentSlide + 1) % this.slides.length;
        this.updateSlider();
    }

    prev() {
        this.currentSlide = this.currentSlide === 0
            ? this.slides.length - 1
            : this.currentSlide - 1;
        this.updateSlider();
    }

    updateSlider() {
        this.slides.forEach((slide, index) => {
            slide.classList.toggle('active', index === this.currentSlide);
        });
    }

    startAutoplay() {
        this.autoplayInterval = setInterval(() => {
            this.next();
        }, this.options.interval);
    }

    stopAutoplay() {
        if (this.autoplayInterval) {
            clearInterval(this.autoplayInterval);
        }
    }
}
```

**js/components/Form.js :**
```javascript
// ✅ Import d'une dépendance
import { debounce } from '../utils/helpers.js';

export default class Form {
    constructor(selector) {
        this.form = document.querySelector(selector);

        if (this.form) {
            this.init();
        }
    }

    init() {
        this.setupValidation();
        this.setupSubmit();
    }

    setupValidation() {
        const inputs = this.form.querySelectorAll('input, textarea');

        inputs.forEach(input => {
            // Utilisation de la fonction debounce importée
            const debouncedValidation = debounce(() => {
                this.validateField(input);
            }, 300);

            input.addEventListener('input', debouncedValidation);
        });
    }

    validateField(field) {
        const value = field.value.trim();
        const isValid = field.checkValidity();

        field.classList.toggle('is-invalid', !isValid);
        field.classList.toggle('is-valid', isValid && value !== '');
    }

    setupSubmit() {
        this.form.addEventListener('submit', (e) => {
            e.preventDefault();
            this.handleSubmit();
        });
    }

    async handleSubmit() {
        const formData = new FormData(this.form);
        const data = Object.fromEntries(formData);

        try {
            // Logique de soumission
            console.log('Données du formulaire:', data);
        } catch (error) {
            console.error('Erreur de soumission:', error);
        }
    }
}
```

**js/main.js :**
```javascript
// ✅ Point d'entrée unique avec imports explicites
import Slider from './components/Slider.js';
import Form from './components/Form.js';
import { formatDate } from './utils/helpers.js';

// Configuration
const CONFIG = {
    slider: {
        selector: '.gallery',
        options: {
            autoplay: true,
            interval: 5000
        }
    },
    form: {
        selector: '.contact-form'
    }
};

// Fonction d'initialisation
function init() {
    console.log('🚀 Application initialisée le', formatDate(new Date()));

    // Initialiser le slider
    const slider = new Slider(
        CONFIG.slider.selector,
        CONFIG.slider.options
    );

    // Initialiser le formulaire
    const form = new Form(CONFIG.form.selector);

    // Autres initialisations...
}

// Lancer l'application quand le DOM est prêt
if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
} else {
    init();
}
```

### Avantages de cette organisation

- ✅ **Dépendances claires** : on voit exactement ce dont chaque fichier a besoin
- ✅ **Pas de pollution globale** : chaque module est isolé
- ✅ **Réutilisable** : `Slider` et `Form` peuvent être utilisés dans d'autres projets
- ✅ **Maintenable** : chaque composant est dans son propre fichier
- ✅ **Testable** : chaque module peut être testé indépendamment
- ✅ **Ordre de chargement automatique** : les dépendances sont gérées par le navigateur

---

## Cas pratiques et patterns

### Pattern 1 : Configuration centralisée

**config.js :**
```javascript
export const API_CONFIG = {
    baseURL: 'https://api.example.com',
    timeout: 5000,
    headers: {
        'Content-Type': 'application/json'
    }
};

export const UI_CONFIG = {
    animationDuration: 300,
    debounceDelay: 300,
    theme: 'light'
};
```

**Utilisation :**
```javascript
import { API_CONFIG, UI_CONFIG } from './config.js';

console.log(API_CONFIG.baseURL);
console.log(UI_CONFIG.theme);
```

### Pattern 2 : Service API

**services/api.js :**
```javascript
import { API_CONFIG } from '../config.js';

class ApiService {
    constructor() {
        this.baseURL = API_CONFIG.baseURL;
    }

    async get(endpoint) {
        const response = await fetch(`${this.baseURL}${endpoint}`);
        return this.handleResponse(response);
    }

    async post(endpoint, data) {
        const response = await fetch(`${this.baseURL}${endpoint}`, {
            method: 'POST',
            headers: API_CONFIG.headers,
            body: JSON.stringify(data)
        });
        return this.handleResponse(response);
    }

    async handleResponse(response) {
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json();
    }
}

// Export d'une instance unique (Singleton)
export default new ApiService();
```

**Utilisation :**
```javascript
import api from './services/api.js';

async function loadUsers() {
    try {
        const users = await api.get('/users');
        console.log(users);
    } catch (error) {
        console.error('Erreur:', error);
    }
}
```

### Pattern 3 : Utilities avec exports multiples

**utils/dom.js :**
```javascript
export function $(selector) {
    return document.querySelector(selector);
}

export function $$(selector) {
    return Array.from(document.querySelectorAll(selector));
}

export function createElement(tag, attrs = {}, children = []) {
    const element = document.createElement(tag);

    Object.entries(attrs).forEach(([key, value]) => {
        if (key === 'className') {
            element.className = value;
        } else if (key === 'dataset') {
            Object.entries(value).forEach(([dataKey, dataValue]) => {
                element.dataset[dataKey] = dataValue;
            });
        } else {
            element.setAttribute(key, value);
        }
    });

    children.forEach(child => {
        if (typeof child === 'string') {
            element.appendChild(document.createTextNode(child));
        } else {
            element.appendChild(child);
        }
    });

    return element;
}

export function on(element, event, handler) {
    element.addEventListener(event, handler);
    return () => element.removeEventListener(event, handler);
}
```

**Utilisation :**
```javascript
import { $, $$, createElement, on } from './utils/dom.js';

const header = $('.header');
const buttons = $$('.btn');

const newDiv = createElement('div', {
    className: 'box',
    dataset: { id: '123' }
}, ['Contenu']);

const removeListener = on(header, 'click', () => {
    console.log('Header clicked');
});
```

---

## Bonnes pratiques

### 1. Un module = Une responsabilité

Chaque module doit avoir une seule responsabilité claire :

```
✅ BON
js/
├── components/
│   ├── Slider.js      ← Gère uniquement le slider
│   ├── Modal.js       ← Gère uniquement les modales
│   └── Form.js        ← Gère uniquement les formulaires

❌ MAUVAIS
js/
└── everything.js      ← Fait tout
```

### 2. Nommage cohérent

```javascript
// ✅ Classes en PascalCase
export default class UserProfile { }

// ✅ Fonctions et variables en camelCase
export function formatDate() { }
export const API_URL = '...';

// ✅ Constantes en SCREAMING_SNAKE_CASE
export const MAX_RETRIES = 3;
```

### 3. Exports explicites en fin de fichier

Pour les exports nommés, regroupez-les à la fin :

```javascript
// helper.js

function add(a, b) { return a + b; }
function subtract(a, b) { return a - b; }
function multiply(a, b) { return a * b; }

// ✅ Vue d'ensemble claire de ce qui est exporté
export { add, subtract, multiply };
```

### 4. Import organisés

Organisez vos imports par catégorie :

```javascript
// main.js

// 1. Bibliothèques externes (si vous en avez)
// import React from 'react';

// 2. Composants
import Slider from './components/Slider.js';
import Modal from './components/Modal.js';
import Form from './components/Form.js';

// 3. Utilitaires
import { formatDate, debounce } from './utils/helpers.js';
import { $, $$ } from './utils/dom.js';

// 4. Configuration
import { API_CONFIG } from './config.js';

// 5. Styles (avec les bundlers)
// import './styles/main.css';
```

### 5. Éviter les imports circulaires

```javascript
// ❌ MAUVAIS : Import circulaire

// moduleA.js
import { functionB } from './moduleB.js';
export function functionA() { functionB(); }

// moduleB.js
import { functionA } from './moduleA.js';  // ❌ Circulaire !
export function functionB() { functionA(); }
```

**Solution :** Extraire le code commun dans un troisième module.

### 6. Utiliser des chemins relatifs clairs

```javascript
// ✅ BON : Chemin relatif explicite
import Slider from './components/Slider.js';
import { formatDate } from '../utils/helpers.js';

// ❌ ÉVITER : Chemins absolus (sauf configuration spéciale)
import Slider from '/js/components/Slider.js';
```

---

## Limitations et considérations

### 1. Support navigateur

Les modules ES6 sont supportés par tous les navigateurs modernes, mais pas par les très anciens (IE11 et antérieurs).

**Solution :** Utiliser le fallback `nomodule` :

```html
<!-- Navigateurs modernes -->
<script type="module" src="app.js"></script>

<!-- Anciens navigateurs -->
<script nomodule src="app-legacy.js"></script>
```

### 2. CORS et protocole file://

Les modules sont soumis aux règles CORS. Vous **ne pouvez pas** les tester en ouvrant directement `index.html` dans le navigateur (`file://`).

**Solutions :**

**A. Utiliser un serveur local simple :**

```bash
# Avec Python 3
python -m http.server 8000

# Avec Node.js (si vous avez installé http-server)
npx http-server

# Avec VS Code : extension "Live Server"
```

Puis accéder à `http://localhost:8000`

**B. Utiliser l'extension VS Code "Live Server"**
1. Installer "Live Server" dans VS Code
2. Clic droit sur `index.html` → "Open with Live Server"

### 3. Chemins et extensions

**Important :** Toujours inclure l'extension `.js` dans les imports !

```javascript
// ✅ BON
import Slider from './Slider.js';

// ❌ MAUVAIS (ne fonctionne pas dans le navigateur)
import Slider from './Slider';
```

### 4. Ordre d'exécution

Les modules sont toujours exécutés en mode `defer`, ce qui signifie qu'ils attendent que le HTML soit parsé.

```html
<script type="module">
    // Ce code s'exécute APRÈS le parsing du HTML
    console.log(document.body); // ✅ Disponible
</script>
```

---

## Debugging des modules

### Vérifier si les modules sont chargés

```javascript
// main.js
console.log('✅ Module main.js chargé');

import Slider from './components/Slider.js';
console.log('✅ Module Slider.js importé');
```

### Erreurs courantes

#### Erreur 1 : CORS

```
Access to script at 'file:///...' from origin 'null' has been blocked by CORS policy
```

**Solution :** Utiliser un serveur local (voir section CORS ci-dessus)

#### Erreur 2 : Extension manquante

```
Failed to resolve module specifier "Slider"
```

**Solution :** Ajouter `.js` :
```javascript
import Slider from './Slider.js';  // ✅
```

#### Erreur 3 : Chemin incorrect

```
Failed to load module script: Expected a JavaScript module script but the server responded with a MIME type of "text/html"
```

**Solution :** Vérifier que le chemin vers le fichier est correct

#### Erreur 4 : Export manquant

```
The requested module './utils.js' does not provide an export named 'formatDate'
```

**Solution :** Vérifier que la fonction est bien exportée dans `utils.js`

---

## Résumé

### Les modules JavaScript ES6, c'est :

**📦 Organisation**
- Diviser le code en petits fichiers réutilisables
- Chaque module a une responsabilité unique

**🔒 Isolation**
- Chaque module a son propre scope
- Pas de pollution du scope global

**🔗 Dépendances explicites**
- On sait exactement ce dont chaque fichier a besoin
- Import/export clairs

**⚡ Performance**
- Chargement optimisé
- Seul ce qui est importé est utilisé

### Syntaxe à retenir

```javascript
// EXPORT
export function maFonction() { }           // Export nommé
export default class MaClasse { }          // Export par défaut
export { func1, func2 };                   // Export groupé

// IMPORT
import { maFonction } from './module.js';  // Import nommé
import MaClasse from './module.js';        // Import par défaut
import * as Utils from './module.js';      // Import tout
import { func as fn } from './module.js';  // Import avec alias
```

### Dans le HTML

```html
<!-- Toujours avec type="module" -->
<script type="module" src="app.js"></script>
```

### Règles d'or

1. ✅ Toujours utiliser `type="module"`
2. ✅ Toujours inclure l'extension `.js`
3. ✅ Utiliser un serveur local pour tester
4. ✅ Un module = une responsabilité
5. ✅ Préférer les exports nommés pour les utilitaires
6. ✅ Préférer l'export par défaut pour les classes/composants

---

## Pour aller plus loin

Les modules ES6 sont la **fondation** du développement JavaScript moderne. Tous les frameworks (React, Vue, Angular) les utilisent intensivement.

Dans les prochaines sections :
- **6.1.4** - Chemins relatifs vs absolus pour optimiser l'organisation
- **6.1.5** - Ordre de chargement des ressources

Les modules peuvent sembler complexes au début, mais avec un peu de pratique, ils deviennent naturels et vous ne pourrez plus vous en passer ! 🚀

**Conseil :** Commencez simple (2-3 modules), puis augmentez progressivement la modularité de vos projets.

⏭️ [Chemins relatifs et absolus](/06-integration-html-css-javascript/01-architecture-projet-moderne/04-chemins-relatifs-absolus.md)
