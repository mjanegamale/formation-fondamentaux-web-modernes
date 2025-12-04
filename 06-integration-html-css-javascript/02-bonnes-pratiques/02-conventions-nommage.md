🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.2.2 - Conventions de nommage

## Introduction

Imaginez une bibliothèque où les livres sont classés ainsi :

```
📚 Rangement chaotique :
- "harry potter 1"
- "HARRY_POTTER_2"
- "HarryPotter3"
- "harry-potter-4"
- "HarryPotter_5_Final_Version_2"
```

Impossible de s'y retrouver ! Maintenant imaginez :

```
📚 Rangement cohérent :
- "harry-potter-1-ecole-sorciers"
- "harry-potter-2-chambre-secrets"
- "harry-potter-3-prisonnier-azkaban"
- "harry-potter-4-coupe-feu"
- "harry-potter-5-ordre-phenix"
```

**Beaucoup mieux, non ?**

C'est exactement le même principe avec le nommage dans le code. Des **conventions de nommage cohérentes** permettent de :
- Comprendre instantanément le type d'élément (variable, fonction, classe)
- Naviguer facilement dans le code
- Collaborer efficacement
- Éviter les erreurs stupides
- Avoir un code professionnel

---

## Pourquoi les conventions sont cruciales ?

### 1. Communication universelle

Les conventions sont comme un langage universel entre développeurs :

```javascript
// ✅ Tout développeur comprend immédiatement :
const MAX_LOGIN_ATTEMPTS = 3;     // Constante
class UserProfile { }              // Classe
function calculateTotal() { }      // Fonction
let currentUser = null;            // Variable

// ❌ Personne ne comprend :
const MAX_login_AttemptS = 3;
class userprofile { }
function Calculate_Total() { }
let CurrentUser = null;
```

### 2. Lisibilité instantanée

Le cerveau reconnaît les patterns :

```javascript
// Pattern reconnaissable
getUserById()      // fonction (verbe)
isLoggedIn         // booléen (question)
totalAmount        // variable (nom)
API_ENDPOINT       // constante (majuscules)
UserManager        // classe (nom propre)
```

### 3. Éviter les erreurs

Des conventions mal suivies créent de la confusion :

```javascript
// ❌ Quelle est la différence ?
const userdata = getUserData();
const userData = getUserData();
const UserData = getUserData();
const user_data = getUserData();

// Spoiler : Aucune ! C'est juste incohérent.
```

### 4. Productivité accrue

Avec des conventions :
- L'auto-complétion fonctionne mieux
- Vous trouvez plus vite ce que vous cherchez
- Les conflits de noms sont évités
- Le code review est plus rapide

---

## Les styles de casse (case styles)

Il existe plusieurs styles de casse utilisés en programmation. Chacun a son utilité.

### 1. camelCase

**Description :** Première lettre minuscule, chaque mot suivant commence par une majuscule.

```javascript
// ✅ Exemples
firstName
lastName
userProfileData
calculateTotalPrice
isLoggedIn
hasPermission
```

**Utilisation :**
- ✅ Variables JavaScript
- ✅ Fonctions JavaScript
- ✅ Paramètres de fonction
- ✅ Attributs d'objets

**Origine du nom :** Ressemble à des bosses de chameau 🐪

### 2. PascalCase (ou UpperCamelCase)

**Description :** Comme camelCase, mais la première lettre est aussi majuscule.

```javascript
// ✅ Exemples
UserProfile
ShoppingCart
ProductManager
DatabaseConnection
FormValidator
```

**Utilisation :**
- ✅ Noms de classes JavaScript
- ✅ Composants React, Vue, Angular
- ✅ Constructeurs
- ✅ Types TypeScript

**Différence avec camelCase :**
```javascript
// camelCase → commence par minuscule
const userProfile = new UserProfile();
//    └─ variable      └─ classe (PascalCase)
```

### 3. kebab-case (ou dash-case)

**Description :** Tout en minuscules, mots séparés par des tirets `-`.

```css
/* ✅ Exemples */
.user-profile
.shopping-cart
.btn-primary
.nav-menu-item
```

```html
<!-- ✅ Exemples -->
<div class="user-profile">
<button class="btn-primary">
```

```
✅ Fichiers
user-profile.html
shopping-cart.css
product-list.js
```

**Utilisation :**
- ✅ Classes CSS
- ✅ IDs CSS
- ✅ Noms de fichiers
- ✅ URLs
- ✅ Attributs HTML data

**Origine du nom :** Ressemble à des brochettes �串

### 4. snake_case

**Description :** Tout en minuscules, mots séparés par des underscores `_`.

```python
# ✅ Exemples (Python, Ruby)
user_profile
shopping_cart
calculate_total_price
```

**Utilisation en JavaScript :**
- ⚠️ Rare en JavaScript moderne
- ❌ Éviter pour les nouvelles variables/fonctions
- ✅ OK pour des cas spécifiques (données de BDD, APIs externes)

### 5. SCREAMING_SNAKE_CASE

**Description :** Tout en MAJUSCULES, mots séparés par des underscores `_`.

```javascript
// ✅ Exemples
const MAX_LOGIN_ATTEMPTS = 3;
const API_BASE_URL = 'https://api.example.com';
const DEFAULT_TIMEOUT = 5000;
const TAX_RATE = 0.2;
```

**Utilisation :**
- ✅ Constantes globales
- ✅ Variables d'environnement
- ✅ Configuration immuable

**Pourquoi "screaming" ?** Parce que ça "crie" visuellement ! 📢

### 6. Autres styles

**UPPERCASE (tout majuscule) :**
```javascript
// ✅ Acronymes courts
const URL = 'https://example.com';
const API = '/api/v1';
const HTML = '<div></div>';
```

**lowercase (tout minuscule) :**
```javascript
// ❌ À éviter généralement
const username = 'john';  // ✅ OK si c'est un seul mot
const userprofile = {};    // ❌ Difficile à lire
```

---

## Conventions par langage

### HTML : kebab-case

#### Classes et IDs

```html
<!-- ✅ BON : kebab-case -->
<div class="user-profile">
    <div class="user-profile__header">
        <h2 class="user-profile__name">John Doe</h2>
    </div>
    <button class="btn btn--primary">Action</button>
</div>

<div id="main-navigation">
    <ul class="nav-menu">
        <li class="nav-menu-item">
            <a class="nav-menu-link">Accueil</a>
        </li>
    </ul>
</div>

<!-- ❌ MAUVAIS : Styles mélangés -->
<div class="userProfile">          <!-- camelCase en HTML, non ! -->
<div class="User_Profile">         <!-- snake_case + caps, non ! -->
<div class="USERPROFILE">          <!-- Tout majuscule, non ! -->
```

**Pourquoi kebab-case en HTML/CSS ?**
- HTML est insensible à la casse
- Les tirets sont plus lisibles dans les attributs
- Convention universelle du web

#### Attributs data-*

```html
<!-- ✅ BON : kebab-case pour les attributs -->
<button
    data-user-id="123"
    data-action-type="submit"
    data-confirm-message="Êtes-vous sûr ?"
>
    Supprimer
</button>

<!-- ❌ MAUVAIS -->
<button
    data-userId="123"              <!-- camelCase, non ! -->
    data-action_type="submit"      <!-- snake_case, non ! -->
>
```

**Accès en JavaScript :**
```javascript
// Les attributs data-* deviennent camelCase en JS
const button = document.querySelector('button');

// data-user-id → dataset.userId
console.log(button.dataset.userId);        // "123"

// data-action-type → dataset.actionType
console.log(button.dataset.actionType);    // "submit"

// data-confirm-message → dataset.confirmMessage
console.log(button.dataset.confirmMessage); // "Êtes-vous sûr ?"
```

#### Fichiers HTML

```
✅ BON : kebab-case
index.html
about-us.html
contact-form.html
user-profile.html
product-details.html

❌ MAUVAIS
Index.html              (majuscule)
aboutUs.html           (camelCase)
contact_form.html      (snake_case)
UserProfile.html       (PascalCase)
```

### CSS : kebab-case

#### Sélecteurs

```css
/* ✅ BON : kebab-case pour tout */
.container { }
.user-profile { }
.btn-primary { }
.nav-menu-item { }
.form-input-error { }

#main-header { }
#footer-navigation { }

/* ❌ MAUVAIS : Autres styles */
.userProfile { }        /* camelCase, non ! */
.User_Profile { }       /* snake_case + caps, non ! */
.CONTAINER { }          /* majuscules, non ! */
```

#### Méthodologie BEM

BEM (Block Element Modifier) utilise une convention spécifique :

```css
/* Structure BEM */
.block { }                    /* Bloc */
.block__element { }           /* Élément du bloc */
.block--modifier { }          /* Variante du bloc */
.block__element--modifier { } /* Variante de l'élément */

/* ✅ Exemples concrets */
.card { }
.card__header { }
.card__title { }
.card__body { }
.card--featured { }
.card--large { }

.btn { }
.btn--primary { }
.btn--secondary { }
.btn--large { }
.btn--disabled { }

.form { }
.form__input { }
.form__label { }
.form__input--error { }
.form__input--disabled { }
```

**HTML avec BEM :**
```html
<div class="card card--featured">
    <div class="card__header">
        <h3 class="card__title">Titre</h3>
    </div>
    <div class="card__body">
        <p>Contenu de la carte</p>
    </div>
</div>

<button class="btn btn--primary btn--large">
    Cliquer ici
</button>
```

#### Variables CSS

```css
/* ✅ BON : kebab-case avec préfixe */
:root {
    /* Couleurs */
    --color-primary: #007bff;
    --color-secondary: #6c757d;
    --color-success: #28a745;
    --color-danger: #dc3545;

    /* Espacements */
    --spacing-xs: 0.25rem;
    --spacing-sm: 0.5rem;
    --spacing-md: 1rem;
    --spacing-lg: 2rem;

    /* Typographie */
    --font-primary: 'Roboto', sans-serif;
    --font-size-base: 1rem;
    --line-height-base: 1.6;
}

/* ❌ MAUVAIS */
:root {
    --colorPrimary: #007bff;     /* camelCase */
    --Color_Primary: #007bff;    /* snake_case + caps */
    --PRIMARY_COLOR: #007bff;    /* screaming */
}
```

#### Fichiers CSS

```
✅ BON : kebab-case
style.css
reset.css
main-layout.css
components.css
responsive-design.css
dark-theme.css

❌ MAUVAIS
Style.css
mainLayout.css
main_layout.css
```

### JavaScript : Plusieurs conventions

#### Variables : camelCase

```javascript
// ✅ BON : camelCase
let userName = 'John';
let totalAmount = 100;
let isLoggedIn = true;
let currentPage = 1;
let userProfileData = {};

// Tableaux : pluriel
let users = [];
let products = [];
let orderItems = [];

// Objets : singulier
let user = { name: 'John' };
let product = { price: 100 };

// ❌ MAUVAIS
let UserName = 'John';          // PascalCase (réservé aux classes)
let user_name = 'John';         // snake_case (pas JavaScript)
let username = 'John';          // OK si un seul mot, mais moins lisible
let TOTAL_AMOUNT = 100;         // Majuscules (réservé aux constantes)
```

#### Constantes : SCREAMING_SNAKE_CASE

```javascript
// ✅ BON : Constantes globales immuables
const MAX_LOGIN_ATTEMPTS = 3;
const API_BASE_URL = 'https://api.example.com';
const DEFAULT_TIMEOUT = 5000;
const TAX_RATE = 0.2;
const ITEMS_PER_PAGE = 20;

// ✅ BON : Configurations
const CONFIG = {
    API_TIMEOUT: 5000,
    MAX_FILE_SIZE: 10485760, // 10MB
    ALLOWED_EXTENSIONS: ['jpg', 'png', 'gif']
};

// ⚠️ Attention : const !== CONSTANTE
const user = { name: 'John' };  // camelCase car mutable
const users = [];                // camelCase car mutable

// ❌ MAUVAIS : const mutable en majuscules
const USER_DATA = { name: 'John' };  // Peut être modifié, pas une vraie constante
USER_DATA.name = 'Jane';             // ✓ Fonctionne, donc pas immuable
```

**Règle :** SCREAMING_SNAKE_CASE uniquement pour les valeurs **vraiment immuables**.

#### Fonctions : camelCase

```javascript
// ✅ BON : Verbes en camelCase
function getUserById(id) { }
function calculateTotalPrice(items) { }
function validateEmailFormat(email) { }
function saveToDatabase(data) { }
function renderUserProfile() { }

// Booléens : Commencent souvent par is, has, can, should
function isValidEmail(email) { }
function hasPermission(user, action) { }
function canEditPost(user, post) { }
function shouldShowBanner() { }

// ❌ MAUVAIS
function GetUserById() { }           // PascalCase (réservé aux classes)
function get_user_by_id() { }        // snake_case
function GETUSER() { }               // Majuscules
function user() { }                  // Nom (devrait être un verbe)
```

#### Classes : PascalCase

```javascript
// ✅ BON : PascalCase
class UserProfile { }
class ShoppingCart { }
class ProductManager { }
class DatabaseConnection { }
class EmailValidator { }

// ✅ Instanciation
const userProfile = new UserProfile();
const cart = new ShoppingCart();

// ❌ MAUVAIS
class userProfile { }        // camelCase
class user_profile { }       // snake_case
class USERPROFILE { }        // Majuscules
```

#### Méthodes de classe : camelCase

```javascript
class UserProfile {
    // ✅ BON : camelCase pour les méthodes
    constructor(name, email) {
        this.name = name;
        this.email = email;
    }

    getName() {
        return this.name;
    }

    updateEmail(newEmail) {
        this.email = newEmail;
    }

    validateProfile() {
        // ...
    }

    // Méthodes privées (convention avec _)
    _sanitizeInput(input) {
        // ...
    }
}
```

#### Méthodes privées : préfixe _

```javascript
class BankAccount {
    constructor(balance) {
        this.balance = balance;
    }

    // ✅ Public : pas de préfixe
    deposit(amount) {
        this._validateAmount(amount);
        this.balance += amount;
    }

    // ✅ Privé : préfixe _
    _validateAmount(amount) {
        if (amount <= 0) {
            throw new Error('Amount must be positive');
        }
    }

    // ✅ Vraiment privé : # (ES2022)
    #secretKey = 'super-secret';

    #encryptData(data) {
        // Vraiment privé, inaccessible de l'extérieur
    }
}
```

#### Fichiers JavaScript : kebab-case

```
✅ BON : kebab-case
user-profile.js
shopping-cart.js
form-validator.js
api-service.js
utils.js

❌ MAUVAIS
UserProfile.js         (PascalCase pour fichiers)
user_profile.js        (snake_case)
userProfile.js         (camelCase pour fichiers)
```

**Exception :** Composants React/Vue peuvent utiliser PascalCase :
```
✅ OK pour React/Vue
UserProfile.jsx
ShoppingCart.vue
ProductCard.jsx
```

---

## Conventions par type d'élément

### Booléens : Préfixes is, has, can, should

Les booléens devraient se lire comme des questions :

```javascript
// ✅ BON : Questions claires
let isLoggedIn = true;
let hasPermission = false;
let canEdit = true;
let shouldUpdate = false;
let isActive = true;
let hasChildren = false;
let canDelete = true;
let shouldRender = false;

// Utilisation naturelle
if (isLoggedIn) { }
if (hasPermission) { }
if (canEdit && shouldUpdate) { }

// ❌ MAUVAIS : Pas de préfixe
let loggedIn = true;       // ✓ OK mais moins clair
let permission = false;    // Ambigu : permission ou hasPermission ?
let edit = true;           // Trop vague
```

### Tableaux : Pluriel

```javascript
// ✅ BON : Pluriel évident
const users = [];
const products = [];
const items = [];
const categories = [];
const comments = [];

// ✅ Avec suffixe explicite
const userList = [];
const productArray = [];
const itemCollection = [];

// ❌ MAUVAIS : Singulier pour un tableau
const user = [];           // On s'attend à un objet, pas un tableau
const product = [];        // Confusion
```

### Fonctions : Verbes d'action

Les fonctions **font** quelque chose → verbe !

```javascript
// ✅ BON : Verbes clairs
function getUser() { }
function setUser() { }
function createProduct() { }
function updateOrder() { }
function deleteComment() { }
function calculateTotal() { }
function validateForm() { }
function renderComponent() { }
function fetchData() { }
function saveToDatabase() { }

// ✅ Verbes spécifiques selon action
// Récupération
function fetchUserData() { }
function loadProducts() { }
function retrieveOrders() { }

// Modification
function updateUserProfile() { }
function modifySettings() { }
function changePassword() { }

// Suppression
function deleteUser() { }
function removeItem() { }
function clearCache() { }

// Vérification
function validateEmail() { }
function checkPermission() { }
function verifyToken() { }

// ❌ MAUVAIS : Noms au lieu de verbes
function user() { }        // Pas d'action
function data() { }        // Quoi faire avec ?
function form() { }        // Ambigu
```

### Événements : Préfixe handle ou on

```javascript
// ✅ BON : Handlers explicites
function handleClick() { }
function handleSubmit() { }
function handleChange() { }
function handleKeyPress() { }

// ✅ Alternative avec on
function onClick() { }
function onSubmit() { }
function onChange() { }
function onKeyPress() { }

// ✅ Plus spécifique
function handleLoginSubmit() { }
function handleUserNameChange() { }
function handleDeleteButtonClick() { }

// ❌ MAUVAIS
function click() { }               // Pas clair que c'est un handler
function submit() { }              // Trop générique
function doStuff() { }             // Pas descriptif
```

### Composants React/Vue : PascalCase

```javascript
// ✅ BON : PascalCase
function UserProfile() { }
function ShoppingCart() { }
function ProductCard() { }
function NavigationMenu() { }

// ✅ Fichiers correspondants
UserProfile.jsx
ShoppingCart.vue
ProductCard.jsx
NavigationMenu.vue
```

---

## Règles générales de nommage

### 1. Descriptif et explicite

```javascript
// ❌ MAUVAIS : Trop court, cryptique
let d = new Date();
let x = 42;
let tmp = getData();
let arr = [];
let obj = {};

// ✅ BON : Descriptif
let currentDate = new Date();
let maxLoginAttempts = 42;
let temporaryUserData = getData();
let userList = [];
let userProfile = {};
```

### 2. Éviter les abréviations

```javascript
// ❌ MAUVAIS : Abréviations peu claires
let usrNm = 'John';
let qty = 10;
let prc = 99.99;
let btn = document.querySelector('button');
let msg = 'Hello';

// ✅ BON : Mots complets
let userName = 'John';
let quantity = 10;
let price = 99.99;
let button = document.querySelector('button');
let message = 'Hello';

// ✅ OK : Abréviations universelles
let id = 123;
let url = 'https://example.com';
let html = '<div></div>';
let api = '/api/v1';
let max = 100;
let min = 0;
```

### 3. Éviter les mots réservés

```javascript
// ❌ MAUVAIS : Mots réservés JavaScript
let class = 'myClass';      // Erreur de syntaxe !
let function = () => {};    // Erreur !
let new = {};               // Erreur !
let return = 42;            // Erreur !

// ✅ BON : Alternatives
let className = 'myClass';
let functionName = 'test';
let newValue = {};
let returnValue = 42;
```

### 4. Longueur raisonnable

```javascript
// ❌ MAUVAIS : Trop court (pas clair)
let u = getUser();
let p = calcPrice();
let d = new Date();

// ❌ MAUVAIS : Trop long (pénible)
let theCurrentlyAuthenticatedUserProfileDataObject = {};
let theTotalPriceIncludingTaxesAndDiscountsInEuros = 0;

// ✅ BON : Équilibre
let currentUser = getUser();
let totalPrice = calcPrice();
let today = new Date();
```

**Règle empirique :**
- Variables locales courtes : 1-2 mots OK
- Variables globales : 2-3 mots
- Fonctions : 2-4 mots
- Maximum raisonnable : 5 mots

### 5. Contexte et portée

Plus la portée est large, plus le nom doit être descriptif :

```javascript
// ✅ BON : Variable locale courte (contexte clair)
function processUsers() {
    users.forEach(u => {           // "u" OK ici (boucle courte)
        console.log(u.name);
    });
}

// ✅ BON : Variable globale descriptive
const globalUserAuthenticationManager = new AuthManager();

// ✅ Boucles simples
for (let i = 0; i < 10; i++) { }   // "i" est standard
items.map(item => item.id);        // "item" clair dans contexte
```

### 6. Cohérence dans le projet

```javascript
// ❌ MAUVAIS : Incohérent
function getUser() { }
function retrieveProduct() { }
function fetchOrder() { }
function loadComment() { }

// ✅ BON : Cohérent (choisir un verbe et s'y tenir)
function getUser() { }
function getProduct() { }
function getOrder() { }
function getComment() { }

// Ou tous avec fetch
function fetchUser() { }
function fetchProduct() { }
function fetchOrder() { }
function fetchComment() { }
```

---

## Cas particuliers

### URLs et slugs : kebab-case

```javascript
// ✅ BON : URLs avec kebab-case
const urls = {
    home: '/',
    about: '/about-us',
    contact: '/contact-form',
    products: '/products/product-details',
    userProfile: '/user/user-profile'
};

// ✅ Slugs d'articles
'comment-creer-un-site-web'
'les-10-meilleurs-frameworks-javascript'
'guide-complet-pour-debutants'
```

### Énumérations : SCREAMING_SNAKE_CASE

```javascript
// ✅ BON : États comme constantes
const STATUS = {
    PENDING: 'pending',
    APPROVED: 'approved',
    REJECTED: 'rejected'
};

const ROLE = {
    ADMIN: 'admin',
    USER: 'user',
    GUEST: 'guest'
};

// Utilisation
let userStatus = STATUS.PENDING;
```

### Variables d'environnement : SCREAMING_SNAKE_CASE

```bash
# .env
API_BASE_URL=https://api.example.com
DATABASE_URL=postgresql://localhost/mydb
MAX_UPLOAD_SIZE=10485760
JWT_SECRET_KEY=super-secret-key
NODE_ENV=production
```

```javascript
// Accès en JavaScript
const apiUrl = process.env.API_BASE_URL;
const dbUrl = process.env.DATABASE_URL;
```

---

## Erreurs courantes à éviter

### 1. Mélanger les styles

```javascript
// ❌ MAUVAIS : Styles mélangés
const userName = 'John';
const user_email = 'john@example.com';
const UserPhone = '1234567890';
const USER_ADDRESS = '123 Main St';

// ✅ BON : Style cohérent
const userName = 'John';
const userEmail = 'john@example.com';
const userPhone = '1234567890';
const userAddress = '123 Main St';
```

### 2. Noms génériques

```javascript
// ❌ MAUVAIS : Trop générique
function process() { }
function handle() { }
function doStuff() { }
let data = {};
let info = [];
let temp = null;

// ✅ BON : Spécifique
function processPayment() { }
function handleLoginSubmit() { }
function validateUserInput() { }
let userData = {};
let productList = [];
let temporaryEmail = null;
```

### 3. Noms trompeurs

```javascript
// ❌ MAUVAIS : Le nom ne correspond pas au contenu
let users = {};                // users devrait être un tableau !
function getUserList() {       // Retourne un objet, pas une liste
    return { name: 'John' };
}
let isActive = 'yes';          // isActive devrait être un booléen !

// ✅ BON : Nom = contenu
let users = [];
let user = {};
function getUser() {
    return { name: 'John' };
}
let isActive = true;
```

### 4. Acronymes non standard

```javascript
// ❌ MAUVAIS : Acronymes inventés
let usrMgr = new UserManager();
let prdCtlg = getProductCatalog();
let cstmrDtls = {};

// ✅ BON : Mots complets ou acronymes universels
let userManager = new UserManager();
let productCatalog = getProductCatalog();
let customerDetails = {};

// ✅ OK : Acronymes universels
let html = '<div></div>';
let api = '/api/v1';
let url = 'https://example.com';
let id = 123;
```

### 5. Préfixes/Suffixes inconsistants

```javascript
// ❌ MAUVAIS : Inconsistant
function isActive() { }
function checkValidity() { }
function hasPermission() { }
function validEmail() { }        // Devrait être isValidEmail ou checkEmail

// ✅ BON : Cohérent
function isActive() { }
function isValid() { }
function hasPermission() { }
function isValidEmail() { }

// Ou tous avec "check"
function checkActive() { }
function checkValidity() { }
function checkPermission() { }
function checkEmail() { }
```

---

## Guide de style complet

Voici un guide de style complet que vous pouvez adopter pour vos projets :

```javascript
/**
 * GUIDE DE STYLE - CONVENTIONS DE NOMMAGE
 * ========================================
 */

// ====================================
// JAVASCRIPT
// ====================================

// Variables et fonctions → camelCase
let firstName = 'John';
let totalAmount = 100;
function getUserById(id) { }
function calculateTotal() { }

// Classes → PascalCase
class UserProfile { }
class ShoppingCart { }

// Constantes globales → SCREAMING_SNAKE_CASE
const MAX_LOGIN_ATTEMPTS = 3;
const API_BASE_URL = 'https://api.example.com';

// Méthodes privées → préfixe _
class MyClass {
    _privateMethod() { }
    #reallyPrivate() { }  // ES2022
}

// Booléens → is, has, can, should
let isLoggedIn = true;
let hasPermission = false;
let canEdit = true;
let shouldUpdate = false;

// Tableaux → pluriel
const users = [];
const products = [];

// Handlers → handle ou on
function handleClick() { }
function onSubmit() { }

// ====================================
// HTML / CSS
// ====================================

// Classes CSS → kebab-case
.user-profile { }
.btn-primary { }
.nav-menu-item { }

// IDs → kebab-case
#main-navigation { }
#footer-section { }

// Attributs data-* → kebab-case
data-user-id="123"
data-action-type="submit"

// Variables CSS → kebab-case avec préfixe
--color-primary: #007bff;
--spacing-md: 1rem;

// ====================================
// FICHIERS
// ====================================

// Fichiers web → kebab-case
index.html
user-profile.js
main-style.css
product-card.jsx

// Composants React/Vue → PascalCase (optionnel)
UserProfile.jsx
ShoppingCart.vue
```

---

## Checklist de nommage

Avant de valider un nom, vérifiez :

### Variables
- [ ] Utilise camelCase
- [ ] Nom descriptif (pas de `x`, `temp`, `data`)
- [ ] Pluriel pour les tableaux
- [ ] Booléens commencent par is/has/can/should

### Fonctions
- [ ] Utilise camelCase
- [ ] Commence par un verbe (get, set, create, update, etc.)
- [ ] Nom descriptif de l'action
- [ ] Handlers commencent par handle/on

### Classes
- [ ] Utilise PascalCase
- [ ] Nom (pas de verbe)
- [ ] Descriptif du type d'objet

### Constantes
- [ ] SCREAMING_SNAKE_CASE pour les vraies constantes
- [ ] Valeur immuable
- [ ] Nom descriptif

### HTML/CSS
- [ ] kebab-case pour classes et IDs
- [ ] Pas de majuscules
- [ ] Descriptif et sémantique

### Fichiers
- [ ] kebab-case (sauf composants)
- [ ] Extension appropriée
- [ ] Nom descriptif du contenu

---

## Outils pour aider

### ESLint : Règles de nommage

```json
// .eslintrc.json
{
    "rules": {
        "camelcase": ["error", { "properties": "never" }],
        "no-underscore-dangle": "off",
        "new-cap": ["error", { "capIsNew": false }]
    }
}
```

### Convention de nommage dans l'équipe

Créez un fichier `NAMING_CONVENTIONS.md` :

```markdown
# Conventions de nommage

## JavaScript
- Variables : camelCase
- Fonctions : camelCase avec verbe
- Classes : PascalCase
- Constantes : SCREAMING_SNAKE_CASE

## HTML/CSS
- Classes : kebab-case
- IDs : kebab-case
- Fichiers : kebab-case

## Booléens
Préfixes obligatoires : is, has, can, should

## Fonctions
Verbes standards :
- get/fetch : récupération
- set/update : modification
- create/add : création
- delete/remove : suppression
- validate/check : vérification
```

---

## Résumé visuel

```
┌─────────────────────────────────────────────────────┐
│                     JAVASCRIPT                      │
├─────────────────────────────────────────────────────┤
│  Variables         → camelCase                      │
│  Fonctions         → camelCase (verbe)              │
│  Classes           → PascalCase                     │
│  Constantes        → SCREAMING_SNAKE_CASE           │
│  Booléens          → is/has/can/should              │
│  Tableaux          → pluriel                        │
│  Handlers          → handle/on                      │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│                    HTML / CSS                       │
├─────────────────────────────────────────────────────┤
│  Classes CSS       → kebab-case                     │
│  IDs               → kebab-case                     │
│  Attributs data-*  → kebab-case                     │
│  Variables CSS     → kebab-case                     │
│  Fichiers          → kebab-case                     │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│                      GÉNÉRAL                        │
├─────────────────────────────────────────────────────┤
│  Descriptif        ✓ userName                       │
│  Cohérent          ✓ même style partout             │
│  Éviter            ✗ x, tmp, data, info             │
│  Longueur          → 1-4 mots généralement          │
└─────────────────────────────────────────────────────┘
```

---

## Conclusion

### Les 3 règles d'or

1. **Cohérence** : Choisissez un style et tenez-vous-y
2. **Clarté** : Le nom doit révéler l'intention
3. **Conventions** : Suivez les standards de votre langage

### Citation

> *"There are only two hard things in Computer Science: cache invalidation and naming things."*
>
> — Phil Karlton

Le nommage est difficile, mais crucial. Prenez le temps de bien nommer dès le début, ça vous fera gagner des heures plus tard !

### Pour aller plus loin

- **6.2.3** - Commentaires et documentation
- **6.2.4** - Indentation et formatage
- **6.2.5** - Principe DRY

**Ressources :**
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [MDN JavaScript Guidelines](https://developer.mozilla.org/en-US/docs/MDN/Writing_guidelines/Writing_style_guide/Code_style_guide/JavaScript)

---

Un bon nommage = un code qui se lit comme un livre. Investissez dans vos noms, votre futur vous dira merci ! 📚✨

⏭️ [Commentaires et documentation](/06-integration-html-css-javascript/02-bonnes-pratiques/03-commentaires-documentation.md)
