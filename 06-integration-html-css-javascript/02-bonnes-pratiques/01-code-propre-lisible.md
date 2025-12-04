🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.2.1 - Code propre et lisible

## Introduction

Imaginez deux recettes de cuisine pour le même plat :

**Recette 1 (illisible) :**
```
mettretouslesingredientsdansleboldumélangerbattre3mntajouterlafarineaupeutit1c
mettraufour180pendant45minutes
```

**Recette 2 (lisible) :**
```
1. Dans un bol, mélanger :
   - 3 œufs
   - 100g de sucre
   - 1 sachet de sucre vanillé

2. Battre pendant 3 minutes

3. Ajouter progressivement 150g de farine

4. Mettre au four à 180°C pendant 45 minutes
```

**Laquelle préférez-vous ?** La réponse est évidente !

C'est exactement pareil avec le code. Un **code propre et lisible** est un code que :
- Vous comprenez en un coup d'œil
- Vous pouvez modifier sans tout casser
- Vos collègues peuvent reprendre facilement
- Vous-même comprenez encore 6 mois plus tard

---

## Pourquoi le code propre est crucial ?

### Le mythe du "ça marche, c'est suffisant"

Beaucoup de débutants pensent : *"Tant que mon code fonctionne, peu importe comment il est écrit."*

**C'est faux.** Voici pourquoi :

#### 1. Le code est lu 10x plus souvent qu'il n'est écrit

```
Temps passé à écrire du code :     ████ (20%)
Temps passé à lire du code :       ████████████████████ (80%)
```

Vous passez la majorité de votre temps à :
- Relire votre propre code
- Comprendre le code des autres
- Déboguer
- Modifier et faire évoluer

**Si le code est illisible, tout prend 10x plus de temps.**

#### 2. Vous oubliez votre propre code

Revenez sur un projet après 3 mois. Si le code est mal écrit, vous vous demanderez : *"Mais qui a écrit ce truc ??!"*

Spoiler : c'était vous. 😅

#### 3. Le code est un outil de communication

Le code communique avec :
- **Votre futur vous** (dans 6 mois)
- **Vos collègues** (qui vont reprendre votre projet)
- **Les nouveaux arrivants** (qui doivent comprendre rapidement)
- **Les contributeurs** (sur des projets open-source)

**Un code propre = une communication claire**

#### 4. La dette technique

Du code sale accumule de la "dette technique" :

```
Code sale → Plus difficile à modifier
           → Plus de bugs
           → Plus de temps perdu
           → Frustration
           → Projet abandonné
```

**Un code propre est un investissement sur le long terme.**

---

## Les 7 principes du code propre

### 1. La lisibilité avant tout

**Principe :** Le code doit se lire comme un livre.

#### ❌ Code illisible

```javascript
function f(x,y,z){let a=x*y;let b=a+z;if(b>100){return b*2;}else{return b;}}
```

**Problèmes :**
- Tout sur une ligne
- Noms de variables cryptiques (`f`, `x`, `a`, `b`)
- Pas d'espaces
- Difficile à comprendre

#### ✅ Code lisible

```javascript
function calculateTotal(price, quantity, discount) {
    const subtotal = price * quantity;
    const total = subtotal + discount;

    if (total > 100) {
        return total * 2;
    } else {
        return total;
    }
}
```

**Améliorations :**
- Une instruction par ligne
- Noms descriptifs (`calculateTotal`, `price`, `subtotal`)
- Espacement cohérent
- Structure claire
- On comprend immédiatement ce que fait la fonction

### 2. L'indentation et le formatage

**Principe :** Une indentation cohérente révèle la structure du code.

#### ❌ HTML mal indenté

```html
<div>
<header>
<h1>Titre</h1>
<nav>
<ul>
<li><a href="#">Lien 1</a></li>
<li><a href="#">Lien 2</a></li>
</ul>
</nav>
</header>
<main>
<article>
<h2>Article</h2>
<p>Contenu</p>
</article>
</main>
</div>
```

**Impossible de voir la hiérarchie !**

#### ✅ HTML bien indenté

```html
<div>
    <header>
        <h1>Titre</h1>
        <nav>
            <ul>
                <li><a href="#">Lien 1</a></li>
                <li><a href="#">Lien 2</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2>Article</h2>
            <p>Contenu</p>
        </article>
    </main>
</div>
```

**La structure saute aux yeux !**

**Règles d'indentation :**
- ✅ Utilisez 2 ou 4 espaces (choisissez et restez cohérent)
- ✅ Chaque niveau de profondeur = un niveau d'indentation
- ✅ Les balises fermantes au même niveau que les ouvrantes
- ✅ Sautez une ligne entre les sections logiques

#### ❌ CSS mal formaté

```css
.btn{background:#007bff;color:white;padding:10px 20px;border:none;border-radius:4px;}
.btn:hover{background:#0056b3;}
.btn-large{padding:15px 30px;font-size:18px;}
```

#### ✅ CSS bien formaté

```css
.btn {
    background: #007bff;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
}

.btn:hover {
    background: #0056b3;
}

.btn-large {
    padding: 15px 30px;
    font-size: 18px;
}
```

**Règles CSS :**
- ✅ Une propriété par ligne
- ✅ Espace après les `:`
- ✅ Ligne vide entre les sélecteurs
- ✅ Propriétés alignées

#### ❌ JavaScript mal formaté

```javascript
function getData(){if(data){return data.map(item=>{return{id:item.id,name:item.name,price:item.price*1.2};});}else{return[];}}
```

#### ✅ JavaScript bien formaté

```javascript
function getData() {
    if (data) {
        return data.map(item => {
            return {
                id: item.id,
                name: item.name,
                price: item.price * 1.2
            };
        });
    } else {
        return [];
    }
}
```

**Règles JavaScript :**
- ✅ Accolades sur leur propre ligne (ou style Stroustrup cohérent)
- ✅ Espaces autour des opérateurs (`=`, `+`, `*`, etc.)
- ✅ Une instruction par ligne
- ✅ Indentation des blocs

### 3. Nommage explicite

**Principe :** Les noms doivent révéler l'intention.

#### ❌ Noms cryptiques

```javascript
const d = new Date();
const x = 42;
const temp = getUser();

function f() { }
function process() { }
function doStuff() { }
```

**Problèmes :**
- On ne sait pas ce que représentent ces variables
- Trop générique (`temp`, `process`, `doStuff`)
- Impossible à comprendre sans contexte

#### ✅ Noms descriptifs

```javascript
const currentDate = new Date();
const maxLoginAttempts = 42;
const loggedInUser = getUser();

function calculateTotalPrice() { }
function validateEmailFormat() { }
function saveUserToDatabase() { }
```

**Avantages :**
- On comprend immédiatement le rôle de chaque variable
- Pas besoin de commentaires
- Auto-documenté

#### Conventions de nommage

**Variables et fonctions (camelCase) :**
```javascript
// ✅ BON
const firstName = 'John';
const totalAmount = 100;
function getUserById() { }
function calculateTax() { }
```

**Classes (PascalCase) :**
```javascript
// ✅ BON
class UserProfile { }
class ShoppingCart { }
class ProductManager { }
```

**Constantes (SCREAMING_SNAKE_CASE) :**
```javascript
// ✅ BON
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.example.com';
const DEFAULT_TIMEOUT = 5000;
```

**Classes CSS (kebab-case) :**
```css
/* ✅ BON */
.user-profile { }
.shopping-cart { }
.btn-primary { }
.nav-menu-item { }
```

**Fichiers (kebab-case) :**
```
✅ BON
user-profile.js
shopping-cart.css
product-detail.html

❌ ÉVITER
UserProfile.js
shopping_cart.css
productDetail.html
```

### 4. Fonctions courtes et focalisées

**Principe :** Une fonction = une responsabilité.

#### ❌ Fonction qui fait tout

```javascript
function processOrder(order) {
    // Valider
    if (!order.email) return false;
    if (!order.items.length) return false;

    // Calculer
    let total = 0;
    for (let item of order.items) {
        total += item.price * item.quantity;
    }

    // Appliquer réduction
    if (order.coupon) {
        total = total * 0.9;
    }

    // Ajouter taxes
    total = total * 1.2;

    // Enregistrer en base
    db.save(order);

    // Envoyer email
    sendEmail(order.email, total);

    // Logger
    console.log('Order processed');

    return true;
}
```

**Problèmes :**
- Fait trop de choses différentes
- Difficile à tester
- Difficile à maintenir
- Impossible à réutiliser

#### ✅ Fonctions séparées et focalisées

```javascript
function processOrder(order) {
    if (!validateOrder(order)) {
        return false;
    }

    const total = calculateOrderTotal(order);
    saveOrder(order, total);
    notifyCustomer(order.email, total);
    logOrderProcessing(order.id);

    return true;
}

function validateOrder(order) {
    return order.email && order.items.length > 0;
}

function calculateOrderTotal(order) {
    const subtotal = calculateSubtotal(order.items);
    const discountedTotal = applyDiscount(subtotal, order.coupon);
    return addTaxes(discountedTotal);
}

function calculateSubtotal(items) {
    return items.reduce((sum, item) => {
        return sum + (item.price * item.quantity);
    }, 0);
}

function applyDiscount(amount, coupon) {
    return coupon ? amount * 0.9 : amount;
}

function addTaxes(amount) {
    return amount * 1.2;
}

function saveOrder(order, total) {
    db.save({ ...order, total });
}

function notifyCustomer(email, total) {
    sendEmail(email, `Votre commande de ${total}€ a été traitée`);
}

function logOrderProcessing(orderId) {
    console.log(`Order ${orderId} processed`);
}
```

**Avantages :**
- Chaque fonction a un rôle clair
- Facile à tester individuellement
- Réutilisable
- Facile à comprendre et maintenir
- On peut lire `processOrder` comme une histoire

**Règle générale :** Si votre fonction fait plus de 20 lignes, demandez-vous si elle ne devrait pas être découpée.

### 5. Éviter la complexité inutile

**Principe :** Le code le plus simple qui fonctionne est le meilleur.

#### ❌ Trop complexe

```javascript
function isEven(number) {
    if (number % 2 === 0) {
        return true;
    } else {
        return false;
    }
}
```

#### ✅ Simple et direct

```javascript
function isEven(number) {
    return number % 2 === 0;
}
```

#### ❌ Conditions imbriquées

```javascript
function getDiscount(user) {
    if (user) {
        if (user.isPremium) {
            if (user.orders > 10) {
                return 0.3;
            } else {
                return 0.2;
            }
        } else {
            if (user.orders > 5) {
                return 0.1;
            } else {
                return 0;
            }
        }
    } else {
        return 0;
    }
}
```

**Difficile à suivre !**

#### ✅ Conditions plates (early returns)

```javascript
function getDiscount(user) {
    if (!user) return 0;
    if (!user.isPremium && user.orders <= 5) return 0;

    if (user.isPremium) {
        return user.orders > 10 ? 0.3 : 0.2;
    }

    return 0.1;
}
```

**Ou mieux encore avec une structure de données :**

```javascript
function getDiscount(user) {
    if (!user) return 0;

    const discounts = {
        premium: {
            high: 0.3,    // > 10 orders
            normal: 0.2   // ≤ 10 orders
        },
        standard: {
            active: 0.1,  // > 5 orders
            new: 0        // ≤ 5 orders
        }
    };

    const tier = user.isPremium ? 'premium' : 'standard';
    const level = user.isPremium
        ? (user.orders > 10 ? 'high' : 'normal')
        : (user.orders > 5 ? 'active' : 'new');

    return discounts[tier][level];
}
```

### 6. Cohérence

**Principe :** Choisissez un style et tenez-vous-y dans tout le projet.

#### ❌ Incohérent

```javascript
// Mélange de styles
function getUserData() { }
const get_user_name = () => { };
var GetUserEmail = function() { };

// Mélange de quotes
const name1 = "John";
const name2 = 'Jane';
const name3 = `Bob`;

// Mélange d'indentation
function test() {
  if (true) {
      console.log('2 espaces');
  }
}

function autre() {
    if (true) {
        console.log('4 espaces');
    }
}
```

#### ✅ Cohérent

```javascript
// Style uniforme camelCase
function getUserData() { }
function getUserName() { }
function getUserEmail() { }

// Quotes uniformes (single quotes)
const name1 = 'John';
const name2 = 'Jane';
const name3 = 'Bob';

// Indentation uniforme (2 espaces partout)
function test() {
  if (true) {
    console.log('Cohérent');
  }
}

function autre() {
  if (true) {
    console.log('Toujours cohérent');
  }
}
```

**Créez un guide de style pour votre projet :**

```javascript
// style-guide.js

/**
 * GUIDE DE STYLE DU PROJET
 *
 * Indentation : 2 espaces
 * Quotes : Single quotes (')
 * Point-virgules : Toujours
 * Nommage fonctions : camelCase
 * Nommage classes : PascalCase
 * Nommage constantes : SCREAMING_SNAKE_CASE
 */
```

### 7. Commentaires intelligents

**Principe :** Le code explique le "comment", les commentaires expliquent le "pourquoi".

#### ❌ Commentaires inutiles

```javascript
// Incrémente i
i++;

// Boucle sur les utilisateurs
users.forEach(user => {
    // Affiche le nom de l'utilisateur
    console.log(user.name);
});

// Déclare une variable
const total = 0;
```

**Ces commentaires ne font que répéter le code. Inutiles !**

#### ❌ Commentaires trompeurs

```javascript
// Divise par 2
const result = value * 3; // ❌ Le commentaire ment !
```

#### ✅ Commentaires utiles

```javascript
// Utilisation de 1.2 au lieu de 1.2066 pour simplifier
// Source : https://www.exemple.com/tax-rates
const TAX_RATE = 1.2;

// HACK : Temporaire jusqu'à ce que l'API soit corrigée
// TODO: Retirer quand bug #1234 sera résolu
if (data === null) {
    data = [];
}

// Cette regex valide les emails selon la RFC 5322
// Format : local-part@domain
const EMAIL_REGEX = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

/**
 * Calcule le prix final avec taxes et réductions
 *
 * Note : L'ordre des opérations est important !
 * La réduction doit être appliquée AVANT les taxes
 * pour respecter la législation française.
 *
 * @param {number} basePrice - Prix de base HT
 * @param {number} discount - Réduction en pourcentage (0-100)
 * @returns {number} Prix final TTC
 */
function calculateFinalPrice(basePrice, discount) {
    const discountedPrice = basePrice * (1 - discount / 100);
    return discountedPrice * 1.2; // TVA 20%
}
```

**Quand commenter :**
- ✅ Expliquer un choix de design non évident
- ✅ Documenter des comportements étranges ou des hacks temporaires
- ✅ Avertir de pièges ou d'effets de bord
- ✅ Expliquer des calculs complexes
- ✅ Fournir des exemples d'utilisation (JSDoc)
- ✅ Lier à de la documentation externe

**Quand NE PAS commenter :**
- ❌ Répéter ce que fait le code
- ❌ Commenter du mauvais code au lieu de le réécrire
- ❌ Laisser du vieux code commenté (utilisez Git !)

---

## Exemples concrets par langage

### HTML propre

#### ❌ HTML sale

```html
<div class="container"><div class="row"><div class="col"><h1>Titre</h1><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p><button onclick="alert('click')">Cliquer</button></div></div></div>
```

#### ✅ HTML propre

```html
<div class="container">
    <div class="row">
        <div class="col">
            <h1>Titre</h1>

            <p>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
            </p>

            <button id="actionBtn" class="btn btn--primary">
                Cliquer
            </button>
        </div>
    </div>
</div>
```

**Principes HTML :**
- ✅ Indentation cohérente
- ✅ Un attribut par ligne si plusieurs (ou tous sur la même si peu)
- ✅ Classes sémantiques et BEM
- ✅ Pas de JavaScript inline
- ✅ Lignes vides entre sections logiques

### CSS propre

#### ❌ CSS sale

```css
.box{background:red;width:200px;height:200px;margin:10px;padding:20px;}
.box p{font-size:14px;color:white;}
.btn{background:blue;color:white;padding:10px;border-radius:5px;}
.btn:hover{background:darkblue;}
```

#### ✅ CSS propre

```css
/* =================================
   COMPOSANT : Box
   ================================= */

.box {
    /* Dimensions */
    width: 200px;
    height: 200px;

    /* Espacements */
    margin: 10px;
    padding: 20px;

    /* Couleurs */
    background: red;
}

.box__text {
    font-size: 14px;
    color: white;
}

/* =================================
   COMPOSANT : Button
   ================================= */

.btn {
    /* Couleurs */
    background: blue;
    color: white;

    /* Espacements */
    padding: 10px;

    /* Forme */
    border-radius: 5px;

    /* Comportement */
    cursor: pointer;
    transition: background 0.3s ease;
}

.btn:hover {
    background: darkblue;
}
```

**Principes CSS :**
- ✅ Propriétés groupées par catégorie
- ✅ Ordre logique (dimensions, espacements, couleurs, etc.)
- ✅ Lignes vides entre sélecteurs
- ✅ Commentaires pour séparer les sections
- ✅ Nommage BEM cohérent

### JavaScript propre

#### ❌ JavaScript sale

```javascript
var x=document.getElementById('btn');x.onclick=function(){var y=document.getElementById('input').value;if(y==''){alert('erreur')}else{var z=[];for(var i=0;i<10;i++){z.push(i*2)}console.log(z)}};
```

#### ✅ JavaScript propre

```javascript
// Configuration
const ELEMENTS = {
    button: document.getElementById('btn'),
    input: document.getElementById('input')
};

// Gestionnaire d'événement principal
function handleButtonClick() {
    const inputValue = ELEMENTS.input.value;

    if (!inputValue) {
        showError('Le champ ne peut pas être vide');
        return;
    }

    const numbers = generateEvenNumbers(10);
    displayResults(numbers);
}

// Génère une liste de nombres pairs
function generateEvenNumbers(count) {
    const numbers = [];

    for (let i = 0; i < count; i++) {
        numbers.push(i * 2);
    }

    return numbers;
}

// Affiche les résultats
function displayResults(numbers) {
    console.log('Nombres générés:', numbers);
}

// Affiche un message d'erreur
function showError(message) {
    alert(message);
}

// Initialisation
ELEMENTS.button.addEventListener('click', handleButtonClick);
```

**Principes JavaScript :**
- ✅ Déclarations séparées
- ✅ Fonctions nommées et focalisées
- ✅ Commentaires de section
- ✅ `const` et `let` au lieu de `var`
- ✅ addEventListener au lieu de onclick
- ✅ Early returns pour la lisibilité
- ✅ Nommage explicite

---

## Outils pour un code propre

### 1. Formatage automatique : Prettier

**Prettier** formate automatiquement votre code selon des règles cohérentes.

**Installation (avec VS Code) :**
1. Installer l'extension "Prettier - Code formatter"
2. Configurer comme formateur par défaut
3. Activer "Format On Save"

**Configuration `.prettierrc` :**
```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80,
  "arrowParens": "avoid"
}
```

**Avant Prettier :**
```javascript
const user={name:'John',age:30,email:'john@example.com'};
function getUser(){return user;}
```

**Après Prettier :**
```javascript
const user = {
  name: 'John',
  age: 30,
  email: 'john@example.com',
};

function getUser() {
  return user;
}
```

### 2. Linting : ESLint

**ESLint** détecte les erreurs et les mauvaises pratiques.

**Installation basique :**
```bash
npm install --save-dev eslint
npx eslint --init
```

**Configuration `.eslintrc.json` :**
```json
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "es2021": true
  },
  "rules": {
    "no-unused-vars": "warn",
    "no-console": "off",
    "prefer-const": "error"
  }
}
```

**Exemples d'erreurs détectées :**
```javascript
// ❌ Variable non utilisée
const unusedVar = 42;

// ❌ Should use const
let neverReassigned = 'value';

// ❌ Fonction jamais appelée
function neverUsed() { }
```

### 3. Extensions VS Code utiles

**EditorConfig :**
Assure une configuration cohérente entre développeurs.

**Fichier `.editorconfig` :**
```ini
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false
```

**Autres extensions recommandées :**
- **Auto Rename Tag** : Renomme les balises HTML en paire
- **Bracket Pair Colorizer** : Colore les paires de parenthèses
- **Indent Rainbow** : Colore l'indentation
- **Better Comments** : Améliore les commentaires

---

## Checklist du code propre

Avant de considérer votre code comme "terminé", passez cette checklist :

### Structure et organisation
- [ ] Le code est bien indenté (2 ou 4 espaces cohérents)
- [ ] Les lignes ne dépassent pas 80-100 caractères
- [ ] Les sections logiques sont séparées par des lignes vides
- [ ] Les imports/includes sont en haut du fichier

### Nommage
- [ ] Les noms de variables sont descriptifs
- [ ] Les noms de fonctions décrivent l'action
- [ ] Les conventions de nommage sont respectées
- [ ] Pas d'abréviations cryptiques

### Fonctions
- [ ] Chaque fonction fait une seule chose
- [ ] Les fonctions sont courtes (< 20 lignes idéalement)
- [ ] Les paramètres sont limités (< 4 idéalement)
- [ ] Les noms de fonctions sont des verbes

### Complexité
- [ ] Pas de conditions imbriquées sur plus de 3 niveaux
- [ ] Utilisation d'early returns pour simplifier
- [ ] Pas de code dupliqué
- [ ] Les valeurs magiques sont dans des constantes

### Commentaires
- [ ] Les commentaires expliquent le "pourquoi", pas le "quoi"
- [ ] Pas de code commenté (utiliser Git)
- [ ] Les commentaires sont à jour
- [ ] Les TODOs sont documentés

### Tests visuels
- [ ] Le code est agréable à regarder
- [ ] On peut suivre la logique facilement
- [ ] L'indentation révèle la structure
- [ ] Cohérence visuelle sur tout le fichier

---

## Erreurs courantes à éviter

### 1. Variables mal nommées

```javascript
// ❌ MAUVAIS
const d = new Date();
const x = users.length;
const tmp = getData();
const data = processData(tmp);

// ✅ BON
const currentDate = new Date();
const userCount = users.length;
const rawData = getData();
const processedData = processData(rawData);
```

### 2. Fonctions trop longues

```javascript
// ❌ MAUVAIS : Une fonction de 100 lignes qui fait tout

// ✅ BON : Diviser en petites fonctions focalisées
```

### 3. Magic numbers

```javascript
// ❌ MAUVAIS
if (user.age > 18) { }
setTimeout(doSomething, 5000);

// ✅ BON
const LEGAL_AGE = 18;
const TIMEOUT_DURATION = 5000;

if (user.age > LEGAL_AGE) { }
setTimeout(doSomething, TIMEOUT_DURATION);
```

### 4. Conditions négatives

```javascript
// ❌ MAUVAIS : Double négation confuse
if (!user.isNotLoggedIn) { }

// ✅ BON : Positif et clair
if (user.isLoggedIn) { }
```

### 5. Code dupliqué

```javascript
// ❌ MAUVAIS
function processAdminUser(user) {
    user.validate();
    user.sanitize();
    user.save();
    sendEmail(user.email);
}

function processRegularUser(user) {
    user.validate();
    user.sanitize();
    user.save();
    sendEmail(user.email);
}

// ✅ BON : DRY (Don't Repeat Yourself)
function processUser(user) {
    user.validate();
    user.sanitize();
    user.save();
    sendEmail(user.email);
}
```

### 6. Pas de gestion d'erreur

```javascript
// ❌ MAUVAIS
function getUser(id) {
    return users.find(u => u.id === id).name;
}

// ✅ BON
function getUser(id) {
    const user = users.find(u => u.id === id);

    if (!user) {
        console.error(`User with id ${id} not found`);
        return null;
    }

    return user.name;
}
```

---

## Avant / Après : Refactoring complet

### ❌ Code sale

```javascript
var btn=document.getElementById('btn');
btn.onclick=function(){
var n=document.getElementById('name').value;
var e=document.getElementById('email').value;
var p=document.getElementById('phone').value;
if(n==''||e==''||p==''){alert('remplir tous les champs');return;}
if(e.indexOf('@')==-1){alert('email invalide');return;}
var u={n:n,e:e,p:p,d:new Date()};
var us=localStorage.getItem('users');
if(us){us=JSON.parse(us);}else{us=[];}
us.push(u);
localStorage.setItem('users',JSON.stringify(us));
alert('utilisateur enregistré');
document.getElementById('name').value='';
document.getElementById('email').value='';
document.getElementById('phone').value='';
};
```

### ✅ Code propre

```javascript
// ============================================
// CONFIGURATION
// ============================================

const STORAGE_KEY = 'users';

const FORM_FIELDS = {
    name: document.getElementById('name'),
    email: document.getElementById('email'),
    phone: document.getElementById('phone')
};

const submitButton = document.getElementById('btn');

// ============================================
// GESTION DU FORMULAIRE
// ============================================

/**
 * Récupère les valeurs du formulaire
 * @returns {Object} Les données du formulaire
 */
function getFormData() {
    return {
        name: FORM_FIELDS.name.value.trim(),
        email: FORM_FIELDS.email.value.trim(),
        phone: FORM_FIELDS.phone.value.trim(),
        createdAt: new Date()
    };
}

/**
 * Réinitialise le formulaire
 */
function resetForm() {
    FORM_FIELDS.name.value = '';
    FORM_FIELDS.email.value = '';
    FORM_FIELDS.phone.value = '';
}

// ============================================
// VALIDATION
// ============================================

/**
 * Valide que tous les champs sont remplis
 * @param {Object} data - Les données à valider
 * @returns {boolean} True si valide
 */
function validateRequiredFields(data) {
    return data.name && data.email && data.phone;
}

/**
 * Valide le format de l'email
 * @param {string} email - L'email à valider
 * @returns {boolean} True si valide
 */
function validateEmail(email) {
    return email.includes('@');
}

/**
 * Valide les données du formulaire
 * @param {Object} data - Les données à valider
 * @returns {Object} { isValid, error }
 */
function validateFormData(data) {
    if (!validateRequiredFields(data)) {
        return {
            isValid: false,
            error: 'Veuillez remplir tous les champs'
        };
    }

    if (!validateEmail(data.email)) {
        return {
            isValid: false,
            error: 'Email invalide'
        };
    }

    return { isValid: true };
}

// ============================================
// STOCKAGE
// ============================================

/**
 * Récupère la liste des utilisateurs
 * @returns {Array} Liste des utilisateurs
 */
function getUsers() {
    const usersJson = localStorage.getItem(STORAGE_KEY);
    return usersJson ? JSON.parse(usersJson) : [];
}

/**
 * Sauvegarde la liste des utilisateurs
 * @param {Array} users - Liste des utilisateurs
 */
function saveUsers(users) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(users));
}

/**
 * Ajoute un utilisateur
 * @param {Object} user - L'utilisateur à ajouter
 */
function addUser(user) {
    const users = getUsers();
    users.push(user);
    saveUsers(users);
}

// ============================================
// GESTIONNAIRE D'ÉVÉNEMENT PRINCIPAL
// ============================================

/**
 * Gère la soumission du formulaire
 */
function handleFormSubmit() {
    const formData = getFormData();
    const validation = validateFormData(formData);

    if (!validation.isValid) {
        alert(validation.error);
        return;
    }

    addUser(formData);
    resetForm();
    alert('Utilisateur enregistré avec succès');
}

// ============================================
// INITIALISATION
// ============================================

submitButton.addEventListener('click', handleFormSubmit);
```

**Ce qui a changé :**
1. ✅ **Structure claire** : Sections logiques
2. ✅ **Nommage explicite** : Plus de variables `n`, `e`, `p`
3. ✅ **Fonctions focalisées** : Une responsabilité par fonction
4. ✅ **Documentation** : JSDoc pour chaque fonction
5. ✅ **Validation séparée** : Facile à tester et réutiliser
6. ✅ **Constantes** : `STORAGE_KEY` au lieu de la chaîne en dur
7. ✅ **Lisibilité** : On comprend en un coup d'œil

---

## Résumé

### Les 7 principes du code propre

1. **Lisibilité** : Le code se lit comme un livre
2. **Indentation** : Structure visible et cohérente
3. **Nommage** : Noms explicites qui révèlent l'intention
4. **Fonctions courtes** : Une fonction = une responsabilité
5. **Simplicité** : Le plus simple qui fonctionne
6. **Cohérence** : Un style unique dans tout le projet
7. **Commentaires** : Expliquer le "pourquoi", pas le "quoi"

### Citation célèbre

> *"Any fool can write code that a computer can understand. Good programmers write code that humans can understand."*
>
> — Martin Fowler

### Règle d'or

**Le code est écrit une fois, mais lu des dizaines de fois.**

Investissez du temps dans la propreté du code dès le début. Vous (et vos collègues) vous en remercierez plus tard !

### Pour aller plus loin

Dans les prochaines sections :
- **6.2.2** - Conventions de nommage (détails approfondis)
- **6.2.3** - Commentaires et documentation
- **6.2.4** - Indentation et formatage
- **6.2.5** - Principe DRY (Don't Repeat Yourself)

**Ressources recommandées :**
- *Clean Code* par Robert C. Martin
- *The Art of Readable Code* par Dustin Boswell
- Airbnb JavaScript Style Guide
- Google HTML/CSS Style Guide

---

Le code propre n'est pas une destination, c'est un voyage continu. Chaque ligne que vous écrivez est une opportunité d'améliorer vos compétences. Bon code ! 🚀

⏭️ [Conventions de nommage](/06-integration-html-css-javascript/02-bonnes-pratiques/02-conventions-nommage.md)
