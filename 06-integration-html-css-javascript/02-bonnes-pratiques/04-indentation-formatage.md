🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.2.4 - Indentation et formatage

## Introduction

Lisez ces deux textes :

**Texte 1 (sans formatage) :**
```
cetexteestdifficilealiresansespacesniponctuation
ilestimpossibledecomprendrerapidementlesens
votrecervaudoittravailler10foispluspourdechiffrer
```

**Texte 2 (avec formatage) :**
```
Ce texte est facile à lire avec des espaces et de la ponctuation.
Il est immédiatement compréhensible.
Votre cerveau traite l'information naturellement.
```

**La différence saute aux yeux, non ?**

C'est exactement pareil avec le code ! L'**indentation** et le **formatage** ne sont pas que cosmétiques. Ils sont essentiels pour :
- 📖 **Comprendre** la structure du code
- 🔍 **Repérer** les erreurs visuellement
- 🤝 **Collaborer** efficacement
- ⚡ **Maintenir** le code sur le long terme

Un code bien indenté et formaté se lit comme un livre bien structuré.

---

## Qu'est-ce que l'indentation ?

### Définition simple

> **L'indentation** est l'espace (blanc) ajouté au début d'une ligne pour montrer sa position dans la hiérarchie du code.

### Analogie : Le plan d'un livre

```
Livre                           Code
─────                           ────
Chapitre 1                      <div>
  Section 1.1                     <header>
    Paragraphe                       <h1>Titre</h1>
    Paragraphe                       <p>Texte</p>
  Section 1.2                     </header>
    Paragraphe                     <main>
Chapitre 2                          ...
  Section 2.1                     </main>
    Paragraphe                   </div>
```

L'indentation **révèle la structure** du contenu.

---

## Pourquoi l'indentation est cruciale ?

### 1. Révéler la structure

#### ❌ Sans indentation

```html
<div>
<header>
<h1>Titre</h1>
<nav>
<ul>
<li>Item 1</li>
<li>Item 2</li>
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

#### ✅ Avec indentation

```html
<div>
    <header>
        <h1>Titre</h1>
        <nav>
            <ul>
                <li>Item 1</li>
                <li>Item 2</li>
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

**La structure est évidente !**

### 2. Repérer les erreurs

#### ❌ Erreur cachée par une mauvaise indentation

```javascript
if (user.isLoggedIn) {
console.log('Bienvenue');
} else {
console.log('Connectez-vous');
    updateUI();  // Bug ! S'exécute toujours, même si loggedIn !
}
```

**L'indentation ment ! `updateUI()` semble dans le `else` mais n'y est pas.**

#### ✅ L'indentation révèle le bug

```javascript
if (user.isLoggedIn) {
    console.log('Bienvenue');
} else {
    console.log('Connectez-vous');
}
updateUI();  // Clairement en dehors du if/else
```

**Le problème devient évident !**

### 3. Gagner du temps

Études montrent qu'un code bien formaté est :
- **30-40% plus rapide** à lire
- **50% moins de bugs** détectés tardivement
- **Réduction de 25%** du temps de code review

---

## Espaces vs Tabs : Le grand débat

### Les deux camps

**Team Espaces** 🟦🟦🟦🟦
- Utilise 2 ou 4 espaces
- Rendu identique partout
- Standard dans beaucoup de projets

**Team Tabs** ⭾⭾
- Utilise le caractère Tab (\t)
- Chacun choisit sa largeur
- Fichiers légèrement plus petits

### Le verdict

**Il n'y a pas de "meilleur" choix absolu.**

**Mais voici les recommendations :**

```javascript
✅ Espaces (2 ou 4) :
- Rendu cohérent sur tous les éditeurs
- Standard pour HTML, CSS, JavaScript moderne
- Utilisé par Google, Airbnb, et la plupart des entreprises

⚠️ Tabs :
- Peut causer des problèmes de différence de rendu
- Peut se mélanger accidentellement avec des espaces
- Moins standard dans le web moderne
```

**Notre recommandation : Espaces (2 ou 4)**

### Choisir entre 2 ou 4 espaces

**2 espaces :**
- ✅ Économise de l'espace horizontal
- ✅ Moins de scrolling horizontal
- ✅ Standard pour HTML, CSS
- ❌ Peut être difficile à voir pour certains

**4 espaces :**
- ✅ Plus visible
- ✅ Standard pour Python, Java
- ❌ Prend plus de place
- ❌ Code très imbriqué = beaucoup de scrolling

**Recommandation web :** **2 espaces** (standard HTML/CSS/JS)

### L'essentiel : LA COHÉRENCE

```
❌ PIRE QUE TOUT : Mélanger espaces et tabs

function test() {
⭾ if (true) {        // Tab
    console.log();   // 4 espaces
⭾⭾ return;          // 2 tabs
}                    // Cauchemar !
}

✅ COHÉRENT : Tout en espaces (2)

function test() {
  if (true) {
    console.log();
    return;
  }
}
```

---

## Règles d'indentation par langage

### HTML : Chaque niveau = +1 indentation

#### Principe de base

Chaque élément enfant est indenté d'un niveau de plus que son parent.

```html
<!-- Niveau 0 -->
<body>
    <!-- Niveau 1 : enfant de body -->
    <div class="container">
        <!-- Niveau 2 : enfant de container -->
        <header>
            <!-- Niveau 3 : enfant de header -->
            <h1>Titre</h1>
            <nav>
                <!-- Niveau 4 : enfant de nav -->
                <ul>
                    <!-- Niveau 5 : enfant de ul -->
                    <li>Item 1</li>
                    <li>Item 2</li>
                </ul>
            </nav>
        </header>
    </div>
</body>
```

#### Éléments inline

Les éléments inline courts peuvent rester sur une ligne :

```html
✅ BON : Inline court
<p>Texte avec un <strong>mot important</strong> dedans.</p>

✅ BON : Inline long sur plusieurs lignes
<p>
    Texte avec un
    <strong>mot important</strong>
    et un <a href="#">lien</a>.
</p>

❌ MAUVAIS : Inline court cassé inutilement
<p>
    Texte avec un
    <strong>
        mot
    </strong>
    dedans.
</p>
```

#### Balises auto-fermantes

```html
✅ BON : Sur une ligne
<img src="image.jpg" alt="Description">
<input type="text" name="username" required>

✅ BON : Attributs multiples sur plusieurs lignes
<img
    src="image.jpg"
    alt="Description très longue qui explique l'image"
    width="800"
    height="600"
>
```

#### Commenter les fermetures complexes

```html
<div class="wrapper">
    <div class="container">
        <div class="row">
            <div class="col">
                <!-- Beaucoup de contenu imbriqué... -->
            </div> <!-- .col -->
        </div> <!-- .row -->
    </div> <!-- .container -->
</div> <!-- .wrapper -->
```

### CSS : Règles et propriétés

#### Une propriété par ligne

```css
/* ❌ MAUVAIS : Tout sur une ligne */
.btn { background: blue; color: white; padding: 10px; border-radius: 4px; }

/* ✅ BON : Une propriété par ligne */
.btn {
    background: blue;
    color: white;
    padding: 10px;
    border-radius: 4px;
}
```

#### Groupement logique des propriétés

```css
.card {
    /* Positionnement */
    position: relative;
    top: 0;
    left: 0;

    /* Box model */
    display: flex;
    width: 300px;
    height: 400px;
    padding: 20px;
    margin: 10px;

    /* Bordures */
    border: 1px solid #ddd;
    border-radius: 8px;

    /* Couleurs */
    background: white;
    color: #333;

    /* Typographie */
    font-size: 16px;
    line-height: 1.6;

    /* Effets */
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
}
```

#### Sélecteurs multiples

```css
/* ✅ BON : Un sélecteur par ligne */
.btn,
.button,
.action-button {
    padding: 10px 20px;
    background: blue;
}

/* ❌ MAUVAIS : Tout sur une ligne */
.btn, .button, .action-button { padding: 10px 20px; }
```

#### Media queries

```css
.container {
    width: 100%;
    max-width: 1200px;
}

/* Indentation du contenu des media queries */
@media (max-width: 768px) {
    .container {
        max-width: 100%;
        padding: 0 15px;
    }

    .sidebar {
        display: none;
    }
}
```

### JavaScript : Blocs et instructions

#### Accolades et indentation

```javascript
// ✅ Style K&R (le plus courant en JS)
function example() {
    if (condition) {
        doSomething();
    } else {
        doSomethingElse();
    }
}

// ✅ Style Allman (moins courant en JS)
function example()
{
    if (condition)
    {
        doSomething();
    }
    else
    {
        doSomethingElse();
    }
}

// ⚠️ Choisissez un style et restez cohérent !
```

#### Objets et tableaux

```javascript
// ✅ BON : Objet multi-lignes
const user = {
    name: 'John',
    age: 30,
    email: 'john@example.com',
    address: {
        street: '123 Main St',
        city: 'Paris',
        country: 'France'
    }
};

// ✅ BON : Tableau multi-lignes
const colors = [
    '#ff0000',
    '#00ff00',
    '#0000ff',
    '#ffff00'
];

// ✅ OK : Court sur une ligne
const point = { x: 10, y: 20 };
const rgb = [255, 0, 0];

// ❌ MAUVAIS : Long sur une ligne
const user = { name: 'John', age: 30, email: 'john@example.com', address: { street: '123 Main St', city: 'Paris' } };
```

#### Chaînage de méthodes

```javascript
// ✅ BON : Une méthode par ligne
users
    .filter(user => user.isActive)
    .map(user => user.name)
    .sort()
    .forEach(name => console.log(name));

// ❌ MAUVAIS : Tout sur une ligne
users.filter(user => user.isActive).map(user => user.name).sort().forEach(name => console.log(name));
```

#### Fonctions fléchées

```javascript
// ✅ BON : Corps simple sur une ligne
const double = n => n * 2;

// ✅ BON : Corps complexe multi-lignes
const processUser = user => {
    const validated = validate(user);
    const transformed = transform(validated);
    return save(transformed);
};

// ✅ BON : Objet retourné avec parenthèses
const createPoint = (x, y) => ({
    x: x,
    y: y
});
```

#### Conditions

```javascript
// ✅ BON : Conditions simples
if (isLoggedIn) {
    showDashboard();
}

// ✅ BON : Conditions complexes alignées
if (
    user.isLoggedIn &&
    user.hasPermission('admin') &&
    !user.isBlocked
) {
    showAdminPanel();
}

// ✅ BON : Ternaire simple
const status = isActive ? 'active' : 'inactive';

// ✅ BON : Ternaire complexe multi-lignes
const message = isLoggedIn
    ? 'Bienvenue, ' + userName
    : 'Veuillez vous connecter';
```

---

## Règles de formatage

### 1. Espaces autour des opérateurs

```javascript
// ✅ BON : Espaces autour des opérateurs
const sum = a + b;
const product = x * y;
const isEqual = value === expected;

// ❌ MAUVAIS : Pas d'espaces
const sum=a+b;
const product=x*y;
const isEqual=value===expected;
```

### 2. Espaces après les virgules

```javascript
// ✅ BON
function example(a, b, c) {
    return [a, b, c];
}

const obj = { name: 'John', age: 30, city: 'Paris' };

// ❌ MAUVAIS
function example(a,b,c) {
    return [a,b,c];
}

const obj = { name:'John',age:30,city:'Paris' };
```

### 3. Espaces dans les structures de contrôle

```javascript
// ✅ BON : Espaces après les mots-clés
if (condition) { }
for (let i = 0; i < 10; i++) { }
while (running) { }

// ❌ MAUVAIS : Pas d'espaces
if(condition){ }
for(let i=0;i<10;i++){ }
while(running){ }
```

### 4. Pas d'espace avant les parenthèses de fonction

```javascript
// ✅ BON : Pas d'espace après le nom
function myFunction() { }
const result = calculate(x, y);

// ❌ MAUVAIS : Espace avant la parenthèse
function myFunction () { }
const result = calculate (x, y);
```

### 5. Point-virgules

```javascript
// ✅ BON : Point-virgule à la fin
const x = 5;
doSomething();

// ⚠️ Sans point-virgule (possible mais déconseillé)
const x = 5
doSomething()
```

**Recommandation : Toujours mettre des point-virgules** (évite des bugs subtils)

### 6. Lignes vides pour la lisibilité

```javascript
// ✅ BON : Sections séparées par des lignes vides
function processOrder(order) {
    // Validation
    validateOrder(order);

    // Calculs
    const subtotal = calculateSubtotal(order);
    const tax = calculateTax(subtotal);
    const total = subtotal + tax;

    // Sauvegarde
    saveOrder(order, total);

    // Notification
    sendConfirmation(order.email);

    return total;
}

// ❌ MAUVAIS : Tout collé
function processOrder(order) {
    validateOrder(order);
    const subtotal = calculateSubtotal(order);
    const tax = calculateTax(subtotal);
    const total = subtotal + tax;
    saveOrder(order, total);
    sendConfirmation(order.email);
    return total;
}
```

### 7. Longueur des lignes

**Recommandation : Maximum 80-100 caractères par ligne**

```javascript
// ❌ MAUVAIS : Ligne trop longue (120+ caractères)
function calculateFinalPriceWithTaxesAndDiscounts(basePrice, discountPercentage, taxRate, shippingCost) {
    return (basePrice * (1 - discountPercentage / 100)) * (1 + taxRate) + shippingCost;
}

// ✅ BON : Lignes courtes
function calculateFinalPrice(
    basePrice,
    discountPercentage,
    taxRate,
    shippingCost
) {
    const discountedPrice = basePrice * (1 - discountPercentage / 100);
    const priceWithTax = discountedPrice * (1 + taxRate);
    return priceWithTax + shippingCost;
}
```

---

## Outils d'automatisation

### Prettier : Le formateur automatique

**Prettier** est l'outil de référence pour formater automatiquement votre code.

#### Installation (VS Code)

1. Installer l'extension "Prettier - Code formatter"
2. Paramètres → "Format On Save" → ✅ Activer
3. Paramètres → "Default Formatter" → Prettier

#### Configuration `.prettierrc`

```json
{
    "semi": true,
    "singleQuote": true,
    "tabWidth": 2,
    "useTabs": false,
    "trailingComma": "es5",
    "printWidth": 80,
    "bracketSpacing": true,
    "arrowParens": "avoid"
}
```

#### Avant/Après Prettier

**Avant :**
```javascript
function example(a,b,c){
const result=a+b+c
const obj={name:"John",age:30,email:"john@example.com"}
return obj
}
```

**Après (automatique) :**
```javascript
function example(a, b, c) {
  const result = a + b + c;
  const obj = {
    name: 'John',
    age: 30,
    email: 'john@example.com',
  };
  return obj;
}
```

**Magique ! ✨**

### EditorConfig : Cohérence entre éditeurs

Assure que tous les développeurs utilisent les mêmes paramètres.

**Fichier `.editorconfig` :**
```ini
# EditorConfig is awesome: https://EditorConfig.org

# Configuration racine
root = true

# Tous les fichiers
[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true

# Fichiers web (HTML, CSS, JS)
[*.{html,css,js,json}]
indent_style = space
indent_size = 2

# Markdown (espaces en fin de ligne significatifs)
[*.md]
trim_trailing_whitespace = false

# Python (4 espaces standard)
[*.py]
indent_size = 4
```

### ESLint : Règles de formatage JavaScript

```json
// .eslintrc.json
{
    "extends": ["eslint:recommended", "prettier"],
    "rules": {
        "indent": ["error", 2],
        "quotes": ["error", "single"],
        "semi": ["error", "always"],
        "comma-spacing": ["error", { "before": false, "after": true }],
        "space-before-function-paren": ["error", "never"],
        "object-curly-spacing": ["error", "always"]
    }
}
```

---

## Exemples complets : Avant/Après

### Exemple 1 : HTML mal formaté → bien formaté

#### ❌ Avant (cauchemar)

```html
<div class="container"><header><h1>Mon Site</h1><nav><ul><li><a href="#home">Accueil</a></li><li><a href="#about">À propos</a></li><li><a href="#contact">Contact</a></li></ul></nav></header><main><article><h2>Article principal</h2><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p><img src="image.jpg" alt="Image"><p>Suite du texte...</p></article><aside><h3>Barre latérale</h3><ul><li>Item 1</li><li>Item 2</li></ul></aside></main><footer><p>&copy; 2025 Mon Site</p></footer></div>
```

#### ✅ Après (lisible)

```html
<div class="container">
    <header>
        <h1>Mon Site</h1>
        <nav>
            <ul>
                <li><a href="#home">Accueil</a></li>
                <li><a href="#about">À propos</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2>Article principal</h2>
            <p>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
            </p>
            <img src="image.jpg" alt="Image">
            <p>Suite du texte...</p>
        </article>

        <aside>
            <h3>Barre latérale</h3>
            <ul>
                <li>Item 1</li>
                <li>Item 2</li>
            </ul>
        </aside>
    </main>

    <footer>
        <p>&copy; 2025 Mon Site</p>
    </footer>
</div>
```

### Exemple 2 : CSS mal formaté → bien formaté

#### ❌ Avant

```css
.container{max-width:1200px;margin:0 auto;padding:0 20px}.header{background:#333;color:white;padding:20px 0}.header h1{margin:0;font-size:24px}.nav ul{list-style:none;margin:0;padding:0;display:flex}.nav li{margin-right:20px}.nav a{color:white;text-decoration:none}.btn{background:blue;color:white;padding:10px 20px;border:none;border-radius:4px;cursor:pointer}.btn:hover{background:darkblue}
```

#### ✅ Après

```css
/* =================================
   Layout Principal
   ================================= */

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* =================================
   Header
   ================================= */

.header {
    background: #333;
    color: white;
    padding: 20px 0;
}

.header h1 {
    margin: 0;
    font-size: 24px;
}

/* =================================
   Navigation
   ================================= */

.nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
}

.nav li {
    margin-right: 20px;
}

.nav a {
    color: white;
    text-decoration: none;
}

/* =================================
   Boutons
   ================================= */

.btn {
    background: blue;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background 0.3s ease;
}

.btn:hover {
    background: darkblue;
}
```

### Exemple 3 : JavaScript mal formaté → bien formaté

#### ❌ Avant

```javascript
function processUser(user){if(!user){return null}const{name,email,age}=user
if(!name||!email){throw new Error('Missing required fields')}const processed={fullName:name.trim().toUpperCase(),emailLower:email.toLowerCase(),isAdult:age>=18,createdAt:new Date()}
const saved=saveToDatabase(processed)
if(saved){sendWelcomeEmail(processed.emailLower)}return processed}
```

#### ✅ Après

```javascript
/**
 * Traite les données d'un utilisateur
 * @param {Object} user - Les données utilisateur
 * @returns {Object} Les données traitées
 */
function processUser(user) {
    // Validation initiale
    if (!user) {
        return null;
    }

    // Extraction des données
    const { name, email, age } = user;

    // Validation des champs requis
    if (!name || !email) {
        throw new Error('Missing required fields');
    }

    // Transformation des données
    const processed = {
        fullName: name.trim().toUpperCase(),
        emailLower: email.toLowerCase(),
        isAdult: age >= 18,
        createdAt: new Date()
    };

    // Sauvegarde
    const saved = saveToDatabase(processed);

    // Notification
    if (saved) {
        sendWelcomeEmail(processed.emailLower);
    }

    return processed;
}
```

---

## Erreurs courantes d'indentation

### 1. Indentation incohérente

```javascript
// ❌ MAUVAIS : Mélange de 2 et 4 espaces
function example() {
  if (true) {      // 2 espaces
      console.log('A');  // 4 espaces
    console.log('B');    // 3 espaces ??
  }
}

// ✅ BON : Cohérent (2 espaces partout)
function example() {
  if (true) {
    console.log('A');
    console.log('B');
  }
}
```

### 2. Oublier d'indenter les enfants

```html
<!-- ❌ MAUVAIS -->
<div>
<p>Texte</p>
<p>Texte</p>
</div>

<!-- ✅ BON -->
<div>
    <p>Texte</p>
    <p>Texte</p>
</div>
```

### 3. Sur-indenter

```javascript
// ❌ MAUVAIS : Trop d'indentation inutile
function example() {
        if (true) {
                console.log('A');
        }
}

// ✅ BON : Indentation normale
function example() {
    if (true) {
        console.log('A');
    }
}
```

### 4. Ne pas aligner les éléments similaires

```css
/* ❌ MAUVAIS : Désaligné */
.btn {
    background: blue;
    color:white;
    padding:   10px;
}

/* ✅ BON : Aligné et cohérent */
.btn {
    background: blue;
    color: white;
    padding: 10px;
}
```

### 5. Lignes trop longues non cassées

```javascript
// ❌ MAUVAIS : Ligne de 150 caractères
const result = calculateVeryComplexOperation(parameter1, parameter2, parameter3, parameter4, parameter5, parameter6, parameter7);

// ✅ BON : Cassé sur plusieurs lignes
const result = calculateVeryComplexOperation(
    parameter1,
    parameter2,
    parameter3,
    parameter4,
    parameter5,
    parameter6,
    parameter7
);
```

---

## Guide de style complet

Voici un guide complet que vous pouvez adopter :

```javascript
/**
 * GUIDE DE FORMATAGE
 * ==================
 */

// ====================================
// INDENTATION
// ====================================

// ✅ 2 espaces (pas de tabs)
function example() {
  if (true) {
    console.log('Hello');
  }
}

// ====================================
// ESPACES
// ====================================

// ✅ Autour des opérateurs
const sum = a + b;
const isEqual = x === y;

// ✅ Après les virgules
function test(a, b, c) { }
const arr = [1, 2, 3];

// ✅ Après les mots-clés
if (condition) { }
for (let i = 0; i < 10; i++) { }

// ❌ Avant les parenthèses de fonction
function myFunc() { }  // ✅
function myFunc () { } // ❌

// ====================================
// ACCOLADES
// ====================================

// ✅ Style K&R (ouvrante sur même ligne)
if (condition) {
  doSomething();
}

// ====================================
// LIGNES VIDES
// ====================================

// ✅ Entre les sections logiques
function processData() {
  // Section 1
  const data = getData();

  // Section 2
  const validated = validate(data);

  // Section 3
  return save(validated);
}

// ====================================
// LONGUEUR DES LIGNES
// ====================================

// ✅ Maximum 80 caractères
// Si plus long, casser sur plusieurs lignes

// ====================================
// OBJETS ET TABLEAUX
// ====================================

// ✅ Court sur une ligne
const point = { x: 10, y: 20 };

// ✅ Long sur plusieurs lignes
const user = {
  name: 'John',
  email: 'john@example.com',
  age: 30
};

// ====================================
// POINT-VIRGULES
// ====================================

// ✅ Toujours mettre des point-virgules
const x = 5;
doSomething();
```

---

## Checklist de formatage

Avant de valider votre code, vérifiez :

### HTML
- [ ] Chaque niveau enfant est indenté
- [ ] Les balises fermantes sont alignées avec les ouvrantes
- [ ] Pas de lignes trop longues (> 100 caractères)
- [ ] Attributs multiples sur plusieurs lignes si nécessaire
- [ ] Lignes vides entre les sections principales

### CSS
- [ ] Une propriété par ligne
- [ ] Espaces après les deux-points
- [ ] Ligne vide entre chaque règle
- [ ] Sélecteurs multiples sur des lignes séparées
- [ ] Propriétés groupées logiquement

### JavaScript
- [ ] Indentation cohérente (2 ou 4 espaces partout)
- [ ] Espaces autour des opérateurs
- [ ] Espaces après les virgules
- [ ] Accolades style cohérent
- [ ] Point-virgules partout
- [ ] Lignes vides entre les sections
- [ ] Pas de lignes > 80-100 caractères

---

## Résumé

### Les 3 piliers du formatage

1. **INDENTATION**
   - Révèle la structure
   - Aide à repérer les erreurs
   - Facilite la lecture

2. **ESPACEMENT**
   - Autour des opérateurs
   - Après les virgules
   - Entre les sections

3. **COHÉRENCE**
   - Un seul style dans tout le projet
   - Outils automatiques (Prettier)
   - Configuration partagée (EditorConfig)

### Choix recommandés

```
Indentation    → 2 espaces (web standard)
Style accolades → K&R (ouvrante même ligne)
Point-virgules  → Toujours
Longueur ligne  → Max 80-100 caractères
Outil          → Prettier (automatique)
```

### Citation inspirante

> *"Any fool can write code that a computer can understand. Good programmers write code that humans can understand."*
>
> — Martin Fowler

Le formatage ne change pas ce que fait votre code, mais change **radicalement** sa lisibilité.

### La règle d'or

**Si vous devez choisir entre :**
- ✅ Formatage automatique (Prettier) avec configuration par défaut
- ❌ Formatage manuel incohérent

**Choisissez TOUJOURS l'automatique !**

---

## Pour aller plus loin

Dans la prochaine section :
- **6.2.5** - Principe DRY (Don't Repeat Yourself)

**Ressources :**
- [Prettier Playground](https://prettier.io/playground/)
- [EditorConfig](https://editorconfig.org/)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)

---

**Le code bien formaté est comme une maison bien rangée : on s'y sent bien et on trouve tout facilement ! 🏠✨**

**Investissez 5 minutes pour configurer Prettier, économisez 100 heures de formatage manuel ! ⏰💎**

⏭️ [DRY (Don't Repeat Yourself)](/06-integration-html-css-javascript/02-bonnes-pratiques/05-dry-principe.md)
