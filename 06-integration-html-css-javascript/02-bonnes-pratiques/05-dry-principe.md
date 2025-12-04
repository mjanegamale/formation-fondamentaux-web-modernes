🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.2.5 - DRY (Don't Repeat Yourself)

## Introduction

Imaginez que vous devez écrire 50 fois la même phrase à la main :

**Méthode 1 : Tout écrire à la main**
```
Je m'engage à ne pas copier-coller mon code
Je m'engage à ne pas copier-coller mon code
Je m'engage à ne pas copier-coller mon code
...
(47 fois de plus)
```

**Méthode 2 : Utiliser une photocopieuse**
```
Écrire une fois → Photocopier 49 fois
✅ Résultat identique en 1/50ème du temps
✅ Si on trouve une faute, on la corrige une seule fois
✅ Modification facile
```

**C'est exactement le principe DRY !**

> **DRY = Don't Repeat Yourself**
> *"Ne te répète pas"*

**Principe opposé : WET**
> **WET = Write Everything Twice** (ou "We Enjoy Typing")
> *"Écrire tout deux fois"* ou *"On aime taper"*

---

## Qu'est-ce que le principe DRY ?

### Définition

> **Chaque connaissance doit avoir une représentation unique, non ambiguë et faisant autorité dans le système.**
>
> — *The Pragmatic Programmer* par Andy Hunt et Dave Thomas

**En termes simples :**
- ✅ Une seule fois = DRY
- ❌ Plusieurs fois = WET

### Analogie : La recette de cuisine

**❌ Approche WET (répétition) :**
```
Recette Pizza Margherita :
1. Préchauffer le four à 220°C
2. Étaler la pâte
3. Ajouter sauce tomate, mozzarella, basilic
4. Cuire 15 minutes

Recette Pizza 4 fromages :
1. Préchauffer le four à 220°C
2. Étaler la pâte
3. Ajouter 4 fromages
4. Cuire 15 minutes

Recette Pizza végétarienne :
1. Préchauffer le four à 220°C
2. Étaler la pâte
3. Ajouter légumes, fromage
4. Cuire 15 minutes
```

**✅ Approche DRY (réutilisation) :**
```
Base Pizza (réutilisable) :
1. Préchauffer le four à 220°C
2. Étaler la pâte
3. [Ajouter garniture spécifique]
4. Cuire 15 minutes

Pizza Margherita :
- Utiliser Base Pizza
- Garniture : sauce tomate, mozzarella, basilic

Pizza 4 fromages :
- Utiliser Base Pizza
- Garniture : 4 fromages

Pizza végétarienne :
- Utiliser Base Pizza
- Garniture : légumes, fromage
```

**Si vous devez changer la température du four, vous le faites une seule fois !**

---

## Pourquoi DRY est crucial ?

### 1. Maintenance facilitée

#### ❌ Code WET (répété)

```javascript
// Validation email en 3 endroits différents
function registerUser(email) {
    if (!email.includes('@') || !email.includes('.')) {
        throw new Error('Email invalide');
    }
    // ...
}

function updateEmail(newEmail) {
    if (!newEmail.includes('@') || !newEmail.includes('.')) {
        throw new Error('Email invalide');
    }
    // ...
}

function sendNewsletter(email) {
    if (!email.includes('@') || !email.includes('.')) {
        throw new Error('Email invalide');
    }
    // ...
}
```

**Problème :** Si vous devez améliorer la validation (ex: vérifier le domaine), vous devez modifier **3 endroits** !

#### ✅ Code DRY (unique)

```javascript
// Validation centralisée
function isValidEmail(email) {
    if (!email.includes('@') || !email.includes('.')) {
        return false;
    }
    return true;
}

function registerUser(email) {
    if (!isValidEmail(email)) {
        throw new Error('Email invalide');
    }
    // ...
}

function updateEmail(newEmail) {
    if (!isValidEmail(newEmail)) {
        throw new Error('Email invalide');
    }
    // ...
}

function sendNewsletter(email) {
    if (!isValidEmail(email)) {
        throw new Error('Email invalide');
    }
    // ...
}
```

**Avantage :** Modifier la validation = 1 seul endroit !

### 2. Moins de bugs

**Statistique :** Les études montrent que :
- Code dupliqué = **2 à 3 fois plus de bugs**
- Car les modifications oublient souvent certaines copies

#### Exemple de bug

```javascript
// ❌ Code dupliqué → Bug introduit
function calculatePriceA(price) {
    const tax = price * 0.2;      // Correct (20%)
    return price + tax;
}

function calculatePriceB(price) {
    const tax = price * 0.2;      // Correct au début
    return price + tax;
}

// Un jour, la TVA change à 21%
// On modifie calculatePriceA mais on OUBLIE calculatePriceB

function calculatePriceA(price) {
    const tax = price * 0.21;     // Mis à jour ✓
    return price + tax;
}

function calculatePriceB(price) {
    const tax = price * 0.2;      // Bug ! Oubli de mise à jour
    return price + tax;
}
```

#### ✅ Avec DRY : Bug impossible

```javascript
const TAX_RATE = 0.2;  // Une seule constante

function calculatePrice(price) {
    const tax = price * TAX_RATE;
    return price + tax;
}

// Quand la TVA change
const TAX_RATE = 0.21;  // Un seul endroit à changer !
```

### 3. Code plus court

```javascript
// ❌ WET : 30 lignes
function getUserName() { return user.name; }
function getUserEmail() { return user.email; }
function getUserAge() { return user.age; }
function getUserCity() { return user.city; }
function getUserCountry() { return user.country; }

// ✅ DRY : 3 lignes
function getUserField(field) {
    return user[field];
}
```

**Plus court = Plus facile à lire et maintenir**

### 4. Tests simplifiés

```javascript
// ❌ WET : Tester 5 fonctions similaires
test('getUserName', () => { /* ... */ });
test('getUserEmail', () => { /* ... */ });
test('getUserAge', () => { /* ... */ });
// ...

// ✅ DRY : Tester 1 fonction générique
test('getUserField', () => {
    expect(getUserField('name')).toBe('John');
    expect(getUserField('email')).toBe('john@example.com');
    // ...
});
```

---

## Comment identifier la duplication ?

### La règle des 3

> **Si vous écrivez quelque chose 3 fois, il est temps de refactoriser.**

1 fois = OK
2 fois = Surveiller
3 fois = Refactoriser !

### Signes de duplication

#### 1. Copy-Paste

Si vous faites **Ctrl+C / Ctrl+V** de code → 🚨 Alerte DRY !

#### 2. Code similaire avec petites variations

```javascript
// ❌ Similaire mais légèrement différent
function validateUserName(name) {
    if (!name) return false;
    if (name.length < 3) return false;
    if (name.length > 50) return false;
    return true;
}

function validateProductName(name) {
    if (!name) return false;
    if (name.length < 3) return false;
    if (name.length > 100) return false;  // Juste la limite change
    return true;
}
```

#### 3. Patterns répétés

```javascript
// ❌ Pattern répété
const user1 = {
    name: data.name,
    email: data.email,
    createdAt: new Date()
};

const user2 = {
    name: data.name,
    email: data.email,
    createdAt: new Date()
};

const user3 = {
    name: data.name,
    email: data.email,
    createdAt: new Date()
};
```

---

## Techniques DRY

### 1. Fonctions (JavaScript)

#### ❌ Avant (WET)

```javascript
// Calculer le prix avec réduction en 3 endroits
const price1 = basePrice1 - (basePrice1 * 0.1);
const price2 = basePrice2 - (basePrice2 * 0.1);
const price3 = basePrice3 - (basePrice3 * 0.1);
```

#### ✅ Après (DRY)

```javascript
function applyDiscount(basePrice, discountRate = 0.1) {
    return basePrice - (basePrice * discountRate);
}

const price1 = applyDiscount(basePrice1);
const price2 = applyDiscount(basePrice2);
const price3 = applyDiscount(basePrice3);
```

### 2. Boucles

#### ❌ Avant (WET)

```javascript
console.log(users[0].name);
console.log(users[1].name);
console.log(users[2].name);
console.log(users[3].name);
console.log(users[4].name);
```

#### ✅ Après (DRY)

```javascript
users.forEach(user => {
    console.log(user.name);
});

// Ou version moderne
users.forEach(user => console.log(user.name));
```

### 3. Variables CSS personnalisées

#### ❌ Avant (WET)

```css
.header {
    color: #007bff;
}

.button {
    background: #007bff;
    border: 2px solid #007bff;
}

.link {
    color: #007bff;
}

.icon {
    fill: #007bff;
}

/* Si on change la couleur principale,
   il faut modifier 5 endroits ! */
```

#### ✅ Après (DRY)

```css
:root {
    --color-primary: #007bff;
}

.header {
    color: var(--color-primary);
}

.button {
    background: var(--color-primary);
    border: 2px solid var(--color-primary);
}

.link {
    color: var(--color-primary);
}

.icon {
    fill: var(--color-primary);
}

/* Changer la couleur = 1 seul endroit ! */
```

### 4. Classes CSS réutilisables

#### ❌ Avant (WET)

```css
.user-profile-box {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.product-card {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.comment-box {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

#### ✅ Après (DRY)

```css
/* Classe utilitaire réutilisable */
.card {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* Variantes spécifiques si nécessaire */
.card--user { /* styles spécifiques utilisateur */ }
.card--product { /* styles spécifiques produit */ }
.card--comment { /* styles spécifiques commentaire */ }
```

```html
<!-- Utilisation -->
<div class="card card--user">Profil</div>
<div class="card card--product">Produit</div>
<div class="card card--comment">Commentaire</div>
```

### 5. Objets de configuration

#### ❌ Avant (WET)

```javascript
const API_URL_USERS = 'https://api.example.com/v1/users';
const API_URL_PRODUCTS = 'https://api.example.com/v1/products';
const API_URL_ORDERS = 'https://api.example.com/v1/orders';
const API_URL_COMMENTS = 'https://api.example.com/v1/comments';

const API_TIMEOUT_USERS = 5000;
const API_TIMEOUT_PRODUCTS = 5000;
const API_TIMEOUT_ORDERS = 5000;
const API_TIMEOUT_COMMENTS = 5000;
```

#### ✅ Après (DRY)

```javascript
const API_CONFIG = {
    baseUrl: 'https://api.example.com/v1',
    timeout: 5000,
    endpoints: {
        users: '/users',
        products: '/products',
        orders: '/orders',
        comments: '/comments'
    }
};

// Utilisation
const usersUrl = `${API_CONFIG.baseUrl}${API_CONFIG.endpoints.users}`;
```

### 6. Mixins et fonctions (CSS avec Sass)

#### ❌ Avant (WET)

```css
.button-primary {
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
}

.button-secondary {
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
}

.button-danger {
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
}
```

#### ✅ Après (DRY avec Sass)

```scss
@mixin button-base {
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
}

.button-primary {
    @include button-base;
    background: blue;
    color: white;
}

.button-secondary {
    @include button-base;
    background: gray;
    color: white;
}

.button-danger {
    @include button-base;
    background: red;
    color: white;
}
```

### 7. Composants réutilisables

#### ❌ Avant (WET HTML)

```html
<!-- Formulaire de login -->
<form>
    <div>
        <label>Email</label>
        <input type="email" name="email">
        <span class="error"></span>
    </div>
    <div>
        <label>Mot de passe</label>
        <input type="password" name="password">
        <span class="error"></span>
    </div>
</form>

<!-- Formulaire d'inscription -->
<form>
    <div>
        <label>Email</label>
        <input type="email" name="email">
        <span class="error"></span>
    </div>
    <div>
        <label>Mot de passe</label>
        <input type="password" name="password">
        <span class="error"></span>
    </div>
    <div>
        <label>Confirmer</label>
        <input type="password" name="confirm">
        <span class="error"></span>
    </div>
</form>

<!-- Répétition du pattern "label + input + error" -->
```

#### ✅ Après (DRY avec fonction JS)

```javascript
// Fonction réutilisable pour créer un champ
function createFormField(label, type, name) {
    return `
        <div class="form-field">
            <label>${label}</label>
            <input type="${type}" name="${name}">
            <span class="error"></span>
        </div>
    `;
}

// Formulaire de login
const loginForm = `
    <form>
        ${createFormField('Email', 'email', 'email')}
        ${createFormField('Mot de passe', 'password', 'password')}
    </form>
`;

// Formulaire d'inscription
const registerForm = `
    <form>
        ${createFormField('Email', 'email', 'email')}
        ${createFormField('Mot de passe', 'password', 'password')}
        ${createFormField('Confirmer', 'password', 'confirm')}
    </form>
`;
```

---

## Exemples complets : Refactoring DRY

### Exemple 1 : Validation de formulaire

#### ❌ Avant (WET - 50 lignes)

```javascript
function validateLoginForm() {
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;

    // Validation email
    if (!email) {
        showError('email', 'Email requis');
        return false;
    }
    if (!email.includes('@')) {
        showError('email', 'Email invalide');
        return false;
    }

    // Validation password
    if (!password) {
        showError('password', 'Mot de passe requis');
        return false;
    }
    if (password.length < 8) {
        showError('password', 'Au moins 8 caractères');
        return false;
    }

    return true;
}

function validateRegisterForm() {
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    const name = document.getElementById('name').value;

    // Validation email (DUPLIQUÉ)
    if (!email) {
        showError('email', 'Email requis');
        return false;
    }
    if (!email.includes('@')) {
        showError('email', 'Email invalide');
        return false;
    }

    // Validation password (DUPLIQUÉ)
    if (!password) {
        showError('password', 'Mot de passe requis');
        return false;
    }
    if (password.length < 8) {
        showError('password', 'Au moins 8 caractères');
        return false;
    }

    // Validation name
    if (!name) {
        showError('name', 'Nom requis');
        return false;
    }

    return true;
}
```

#### ✅ Après (DRY - 30 lignes)

```javascript
// Règles de validation réutilisables
const validationRules = {
    email: [
        { test: value => value, message: 'Email requis' },
        { test: value => value.includes('@'), message: 'Email invalide' }
    ],
    password: [
        { test: value => value, message: 'Mot de passe requis' },
        { test: value => value.length >= 8, message: 'Au moins 8 caractères' }
    ],
    name: [
        { test: value => value, message: 'Nom requis' }
    ]
};

// Fonction générique de validation
function validateField(fieldName, value) {
    const rules = validationRules[fieldName];

    for (const rule of rules) {
        if (!rule.test(value)) {
            showError(fieldName, rule.message);
            return false;
        }
    }

    return true;
}

// Validation de formulaire générique
function validateForm(fieldNames) {
    for (const fieldName of fieldNames) {
        const value = document.getElementById(fieldName).value;
        if (!validateField(fieldName, value)) {
            return false;
        }
    }
    return true;
}

// Utilisation
function validateLoginForm() {
    return validateForm(['email', 'password']);
}

function validateRegisterForm() {
    return validateForm(['email', 'password', 'name']);
}
```

### Exemple 2 : Gestion d'API

#### ❌ Avant (WET)

```javascript
function getUsers() {
    fetch('https://api.example.com/users', {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + token
        }
    })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
}

function getProducts() {
    fetch('https://api.example.com/products', {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + token
        }
    })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
}

function getOrders() {
    fetch('https://api.example.com/orders', {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + token
        }
    })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
}
```

#### ✅ Après (DRY)

```javascript
// Fonction API générique
async function apiRequest(endpoint, options = {}) {
    const baseUrl = 'https://api.example.com';
    const defaultOptions = {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${token}`
        }
    };

    try {
        const response = await fetch(
            `${baseUrl}${endpoint}`,
            { ...defaultOptions, ...options }
        );
        return await response.json();
    } catch (error) {
        console.error('API Error:', error);
        throw error;
    }
}

// Utilisation simple
async function getUsers() {
    return await apiRequest('/users');
}

async function getProducts() {
    return await apiRequest('/products');
}

async function getOrders() {
    return await apiRequest('/orders');
}

// Bonus : POST/PUT/DELETE aussi faciles
async function createUser(userData) {
    return await apiRequest('/users', {
        method: 'POST',
        body: JSON.stringify(userData)
    });
}
```

---

## Quand la répétition est acceptable (WET OK)

### 1. Code vraiment différent qui se ressemble par hasard

```javascript
// ✅ OK : Ces deux fonctions se ressemblent mais font des choses différentes
function formatUserName(user) {
    return user.firstName + ' ' + user.lastName;
}

function formatProductName(product) {
    return product.brand + ' ' + product.model;
}

// ❌ Mauvais de les fusionner :
function formatName(item) {
    // Trop générique et confus
    return item.firstName ?
        item.firstName + ' ' + item.lastName :
        item.brand + ' ' + item.model;
}
```

**Règle :** Si la fusion rend le code plus complexe que la répétition, gardez la répétition !

### 2. Code destiné à diverger

```javascript
// ✅ OK : Ces calculs sont identiques maintenant mais vont diverger
function calculateStudentDiscount(price) {
    return price * 0.9;  // 10% de réduction
}

function calculateSeniorDiscount(price) {
    return price * 0.9;  // 10% de réduction
}

// Dans le futur, les règles changeront différemment
// Mieux vaut les garder séparées dès le début
```

### 3. Tests unitaires

```javascript
// ✅ OK : Duplication dans les tests pour la clarté
test('should validate email', () => {
    expect(validateEmail('test@example.com')).toBe(true);
    expect(validateEmail('invalid')).toBe(false);
    expect(validateEmail('')).toBe(false);
});

test('should validate password', () => {
    expect(validatePassword('12345678')).toBe(true);
    expect(validatePassword('123')).toBe(false);
    expect(validatePassword('')).toBe(false);
});

// Même structure mais c'est OK : les tests doivent être évidents
```

### 4. Configuration spécifique par environnement

```javascript
// ✅ OK : Configurations dupliquées pour la clarté
const developmentConfig = {
    apiUrl: 'http://localhost:3000',
    debug: true,
    timeout: 10000
};

const productionConfig = {
    apiUrl: 'https://api.example.com',
    debug: false,
    timeout: 5000
};

// Mieux que de tout fusionner dans un objet complexe
```

---

## Outils pour détecter la duplication

### 1. VS Code : Extensions

**SonarLint**
- Détecte le code dupliqué automatiquement
- Signale les problèmes de qualité
- Suggestions de refactoring

**Code Metrics**
- Affiche la complexité du code
- Identifie les fonctions trop longues
- Aide à repérer les duplications

### 2. ESLint : Règles anti-duplication

```json
// .eslintrc.json
{
    "rules": {
        "no-duplicate-imports": "error",
        "no-dupe-keys": "error",
        "no-dupe-class-members": "error"
    }
}
```

### 3. Outils en ligne de commande

**JSCPD (JavaScript Copy/Paste Detector)**
```bash
npm install -g jscpd
jscpd src/
```

Génère un rapport de duplication :
```
Found 3 clones with 45 duplicated lines in 2 files
File: src/user.js:10-25 (15 lines)
File: src/product.js:34-49 (15 lines)
```

### 4. Technique manuelle : Recherche

Dans VS Code : `Ctrl+Shift+F` (recherche globale)

Si vous trouvez le même pattern plusieurs fois → Refactorisez !

---

## Checklist DRY

Avant de valider votre code, vérifiez :

### Duplication évidente
- [ ] Pas de code copié-collé
- [ ] Pas de fonctions quasi identiques
- [ ] Pas de valeurs répétées en dur

### Logique métier
- [ ] Les règles métier sont centralisées
- [ ] Les calculs complexes sont dans des fonctions
- [ ] Les validations sont réutilisables

### Configuration
- [ ] Les constantes sont définies une fois
- [ ] Les URLs d'API sont centralisées
- [ ] Les valeurs magiques sont nommées

### CSS
- [ ] Variables CSS pour les valeurs répétées
- [ ] Classes utilitaires pour les patterns communs
- [ ] Pas de duplication de styles

### Refactoring
- [ ] Si copié-collé 3+ fois → Extraire en fonction
- [ ] Si pattern similaire → Généraliser
- [ ] Si valeur en dur répétée → Constante

---

## Le processus de refactoring DRY

### Étape 1 : Identifier

```javascript
// Je remarque que ce code apparaît 3 fois
const total1 = price1 + (price1 * 0.2);
const total2 = price2 + (price2 * 0.2);
const total3 = price3 + (price3 * 0.2);
```

### Étape 2 : Extraire en fonction

```javascript
function calculatePriceWithTax(price) {
    return price + (price * 0.2);
}
```

### Étape 3 : Remplacer

```javascript
const total1 = calculatePriceWithTax(price1);
const total2 = calculatePriceWithTax(price2);
const total3 = calculatePriceWithTax(price3);
```

### Étape 4 : Améliorer

```javascript
// Rendre la taxe configurable
const TAX_RATE = 0.2;

function calculatePriceWithTax(price, taxRate = TAX_RATE) {
    return price + (price * taxRate);
}
```

### Étape 5 : Tester

```javascript
// Vérifier que tout fonctionne encore
console.assert(calculatePriceWithTax(100) === 120);
console.assert(calculatePriceWithTax(100, 0.1) === 110);
```

---

## Erreurs courantes avec DRY

### 1. Sur-optimisation précoce

```javascript
// ❌ MAUVAIS : Généraliser trop tôt
function doEverything(type, data, options, callback, context) {
    // Fonction ultra-générique mais incompréhensible
}

// ✅ BON : Commencer simple, généraliser après 3 usages
function processUser(user) { /* ... */ }
function processProduct(product) { /* ... */ }
// Si un 3ème pattern similaire apparaît → généraliser
```

**Règle :** N'optimisez que quand vous avez 3+ cas d'usage.

### 2. Abstractions trop complexes

```javascript
// ❌ MAUVAIS : Abstraction qui complexifie
function calculate(type, subtype, value, modifier, context) {
    if (type === 'price') {
        if (subtype === 'with-tax') {
            // ...
        } else if (subtype === 'with-discount') {
            // ...
        }
    } else if (type === 'quantity') {
        // ...
    }
    // 50 lignes de if/else...
}

// ✅ BON : Fonctions séparées et claires
function calculatePriceWithTax(price) { /* ... */ }
function calculatePriceWithDiscount(price, discount) { /* ... */ }
function calculateQuantity(items) { /* ... */ }
```

**Règle :** Une abstraction doit **simplifier**, pas compliquer.

### 3. Ignorer le contexte métier

```javascript
// ❌ MAUVAIS : Fusionner des concepts différents
function calculateDiscount(amount) {
    return amount * 0.1;  // 10%
}

// Utilisé pour :
const studentDiscount = calculateDiscount(price);
const loyaltyDiscount = calculateDiscount(price);

// Problème : Les règles métier sont différentes !
// Les étudiants et la fidélité suivent des logiques distinctes

// ✅ BON : Séparer selon la logique métier
function calculateStudentDiscount(price) {
    return price * 0.1;
}

function calculateLoyaltyDiscount(price, loyaltyYears) {
    const rate = Math.min(loyaltyYears * 0.02, 0.2);
    return price * rate;
}
```

---

## Résumé

### Le principe DRY en une phrase

> **Chaque connaissance ne doit exister qu'à un seul endroit.**

### Avantages du DRY

```
✅ Maintenance facile      → 1 seul endroit à modifier
✅ Moins de bugs           → Pas d'oubli de mise à jour
✅ Code plus court         → Plus facile à lire
✅ Tests simplifiés        → Moins de code à tester
✅ Cohérence garantie      → Même logique partout
```

### Techniques principales

```
1. Fonctions              → Logique réutilisable
2. Variables/Constantes   → Valeurs partagées
3. Classes CSS            → Styles réutilisables
4. Variables CSS          → Valeurs de design
5. Configuration          → Paramètres centralisés
6. Composants             → UI réutilisable
```

### La règle des 3

```
1 fois  → Normal
2 fois  → Surveiller
3 fois  → Refactoriser !
```

### Quand WET est OK

```
✅ Code vraiment différent (ressemblance fortuite)
✅ Destiné à diverger
✅ Tests (clarté > DRY)
✅ Configuration par environnement
```

### Citations inspirantes

> *"Duplication is far cheaper than the wrong abstraction."*
>
> — Sandi Metz

> *"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."*
>
> — The Pragmatic Programmer

---

## Pour aller plus loin

Vous avez maintenant complété la section **6.2 - Bonnes pratiques** :
- ✅ 6.2.1 - Code propre et lisible
- ✅ 6.2.2 - Conventions de nommage
- ✅ 6.2.3 - Commentaires et documentation
- ✅ 6.2.4 - Indentation et formatage
- ✅ 6.2.5 - Principe DRY

**Prochaines sections :**
- **6.3** - Accessibilité
- **6.4** - Performance

**Ressources recommandées :**
- *The Pragmatic Programmer* par Andy Hunt et Dave Thomas
- *Refactoring* par Martin Fowler
- *Clean Code* par Robert C. Martin

---

**DRY n'est pas qu'une technique, c'est un état d'esprit !**

**Avant d'écrire du code, demandez-vous : "N'ai-je pas déjà écrit quelque chose de similaire ?" 🤔**

**Si oui → Refactorisez ! Si non → Écrivez, mais gardez DRY en tête pour la prochaine fois ! 🔄✨**

⏭️ [Accessibilité web (a11y)](/06-integration-html-css-javascript/03-accessibilite-web/README.md)
