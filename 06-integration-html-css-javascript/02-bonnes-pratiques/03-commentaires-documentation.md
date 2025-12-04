🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.2.3 - Commentaires et documentation

## Introduction

Imaginez deux recettes de cuisine :

**Recette 1 (sans commentaires) :**
```
Mélanger 200g de farine, 100g de sucre, 3 œufs.
Ajouter 50g de beurre fondu.
Mettre au four 180° pendant 30 minutes.
```

**Recette 2 (avec commentaires) :**
```
Mélanger 200g de farine, 100g de sucre, 3 œufs.
// Important : Le beurre doit être fondu mais pas chaud,
// sinon les œufs vont cuire !
Ajouter 50g de beurre fondu tiède.

// Attention : Four traditionnel uniquement.
// Pour un four à chaleur tournante, baisser à 160°
Mettre au four 180° pendant 30 minutes.
```

La deuxième évite des erreurs courantes et explique les subtilités !

**C'est exactement la même chose avec le code.** Les commentaires :
- Expliquent le "pourquoi" (pas le "quoi")
- Avertissent des pièges
- Documentent les choix non évidents
- Facilitent la maintenance

---

## La grande question : Faut-il commenter ?

### Le dilemme du débutant

Beaucoup de débutants oscillent entre deux extrêmes :

**Extrême 1 : Tout commenter**
```javascript
// Déclare une variable x
let x = 5;
// Incrémente x
x++;
// Affiche x
console.log(x);
```

**Extrême 2 : Ne rien commenter**
```javascript
// Code complexe de 500 lignes sans un seul commentaire
function processData(d) {
    // ... magie noire incompréhensible
}
```

**La vérité est entre les deux !**

### Le principe fondamental

> **Le code explique le "COMMENT"**
> **Les commentaires expliquent le "POURQUOI"**

```javascript
// ❌ MAUVAIS : Répète le code
// Incrémente le compteur
counter++;

// ✅ BON : Explique le pourquoi
// On incrémente ici pour éviter de compter deux fois
// le premier élément (bug #1234)
counter++;
```

---

## Quand commenter ?

### ✅ Situations où commenter

#### 1. Choix de conception non évidents

```javascript
// ❌ Sans commentaire : Pourquoi 86400000 ?
const cacheExpiry = 86400000;

// ✅ Avec commentaire : On comprend
// 86400000 ms = 24 heures
// Le cache expire après 1 jour pour respecter
// les conditions de l'API (limite de fraîcheur des données)
const cacheExpiry = 86400000;
```

#### 2. Algorithmes complexes

```javascript
function calculateDiscount(price, userLevel) {
    // Algorithme de réduction progressive :
    // - Bronze (niveau 1) : 5% fixe
    // - Silver (niveau 2) : 10% + 2% par tranche de 100€
    // - Gold (niveau 3) : 15% + bonus si > 500€
    // Ce système encourage les achats importants
    // tout en récompensant la fidélité

    if (userLevel === 1) {
        return price * 0.95;
    } else if (userLevel === 2) {
        const bonus = Math.floor(price / 100) * 0.02;
        return price * (0.9 - bonus);
    } else {
        const baseDiscount = 0.85;
        const extraBonus = price > 500 ? 0.05 : 0;
        return price * (baseDiscount - extraBonus);
    }
}
```

#### 3. Workarounds et hacks temporaires

```javascript
// HACK : Temporaire jusqu'à ce que l'API soit corrigée
// L'API retourne parfois null au lieu d'un tableau vide
// Bug reporté : https://github.com/api-project/issues/1234
// TODO : Retirer ce fix quand la version 2.0 de l'API sortira
if (data === null) {
    data = [];
}
```

#### 4. Comportements contre-intuitifs

```javascript
// ATTENTION : L'ordre est important !
// La réduction DOIT être appliquée AVANT les taxes
// pour respecter la législation française (Article L.123-4)
const discountedPrice = basePrice * (1 - discount);
const finalPrice = discountedPrice * (1 + TAX_RATE);

// ❌ FAUX : Taxes puis réduction (illégal en France)
// const taxedPrice = basePrice * (1 + TAX_RATE);
// const finalPrice = taxedPrice * (1 - discount);
```

#### 5. Décisions qui semblent étranges

```javascript
// On utilise var ici au lieu de let car nous avons besoin
// du hoisting pour cette variable dans le scope global
// (legacy code à maintenir pour compatibilité IE11)
var legacyGlobalConfig = {};
```

#### 6. Références externes

```javascript
// Regex pour valider les emails selon RFC 5322
// Source : https://emailregex.com/
// Note : Volontairement simplifiée pour la lisibilité
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

// Algorithme de tri inspiré de :
// https://stackoverflow.com/questions/12345678
function customSort(array) {
    // ...
}
```

#### 7. Avertissements de sécurité/performance

```javascript
// ATTENTION : Cette fonction est coûteuse en performance
// Ne pas appeler dans une boucle ou à chaque rendu
// Utiliser la version mise en cache si possible
function expensiveCalculation(data) {
    // ...
}

// SÉCURITÉ : Ne jamais exposer cette clé côté client
// Doit rester strictement côté serveur
const API_SECRET_KEY = process.env.SECRET_KEY;
```

### ❌ Situations où NE PAS commenter

#### 1. Code auto-explicatif

```javascript
// ❌ MAUVAIS : Le code est déjà clair
// Ajoute un utilisateur à la liste
function addUserToList(user, list) {
    list.push(user);
}

// ✅ BON : Pas de commentaire nécessaire
function addUserToList(user, list) {
    list.push(user);
}
```

#### 2. Commentaires obsolètes

```javascript
// ❌ MAUVAIS : Commentaire qui ne correspond plus au code
// Calcule la TVA à 19.6%
const totalWithTax = price * 1.20; // TVA est maintenant 20% !

// ✅ BON : Commentaire à jour
// Calcule la TVA à 20% (taux en vigueur depuis 2014)
const totalWithTax = price * 1.20;
```

#### 3. Mauvais code au lieu de le corriger

```javascript
// ❌ MAUVAIS : Commenter du code compliqué
// Cette fonction est compliquée, désolé !
function x(a,b,c){let d=a*b;if(c>10){return d*2}else{return d}}

// ✅ BON : Simplifier le code
function calculatePrice(basePrice, quantity, customerLevel) {
    const subtotal = basePrice * quantity;
    const multiplier = customerLevel > 10 ? 2 : 1;
    return subtotal * multiplier;
}
```

#### 4. Vieux code commenté

```javascript
// ❌ MAUVAIS : Laisser du code commenté "au cas où"
function processData(data) {
    // const oldResult = oldProcessing(data);
    // if (oldResult) {
    //     return oldResult;
    // }
    return newProcessing(data);
}

// ✅ BON : Supprimer et utiliser Git pour l'historique
function processData(data) {
    return newProcessing(data);
}
```

---

## Syntaxe des commentaires par langage

### HTML : `<!-- -->`

```html
<!-- Commentaire simple -->
<div class="container">
    <!-- Section principale du site -->
    <main>
        <!-- Article de blog -->
        <article>
            <h2>Titre</h2>
            <p>Contenu...</p>
        </article>
    </main>
</div>

<!--
    Commentaire multi-lignes
    pour des explications plus longues
    sur plusieurs lignes
-->

<!-- ⚠️ Les commentaires HTML sont VISIBLES dans le code source !
     Ne jamais mettre d'informations sensibles dedans -->
```

**Bonnes pratiques HTML :**
```html
<!-- ✅ BON : Marquer les sections importantes -->
<!-- ============================
     HEADER - Navigation principale
     ============================ -->
<header>
    <!-- ... -->
</header>

<!-- ============================
     MAIN CONTENT
     ============================ -->
<main>
    <!-- ... -->
</main>

<!-- ✅ BON : Commenter les fermetures de divs complexes -->
<div class="wrapper">
    <div class="container">
        <div class="row">
            <div class="col">
                <!-- Beaucoup de contenu... -->
            </div> <!-- .col -->
        </div> <!-- .row -->
    </div> <!-- .container -->
</div> <!-- .wrapper -->

<!-- ❌ MAUVAIS : Commenter chaque élément -->
<!-- div -->
<div>
    <!-- paragraphe -->
    <p>Texte</p>
</div>
```

### CSS : `/* */`

```css
/* Commentaire simple */
.container {
    width: 100%;
}

/*
 * Commentaire multi-lignes
 * pour des explications détaillées
 */

/* =================================
   Section : Navigation
   ================================= */
.nav {
    display: flex;
}

/* Sous-section : Liens de navigation */
.nav__link {
    color: blue;
}
```

**Styles de commentaires CSS :**

```css
/* ========================================
   STRUCTURE GÉNÉRALE
   ======================================== */

/* Reset de base */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

/* ----------------------------------------
   Composant : Boutons
   ---------------------------------------- */

.btn {
    /* Couleurs */
    background: blue;
    color: white;

    /* Espacements */
    padding: 10px 20px;

    /* HACK : Fix pour Safari
       Bug connu : https://bugs.webkit.org/12345
       TODO : Retirer quand Safari 18 sortira */
    -webkit-appearance: none;
}

/* Modificateur : Bouton primaire */
.btn--primary {
    background: #007bff;
}

/* État : Bouton hover */
.btn:hover {
    /* Transition douce pour une meilleure UX */
    background: #0056b3;
    transition: background 0.3s ease;
}
```

### JavaScript : `//` et `/* */`

```javascript
// Commentaire sur une ligne

/* Commentaire sur
   plusieurs lignes */

/**
 * Commentaire de documentation (JSDoc)
 * Utilisé pour générer de la documentation automatique
 */

// ✅ Différents usages

// Explication simple
const TAX_RATE = 0.2;

/*
 * Explication plus longue
 * qui nécessite plusieurs lignes
 */
function complexFunction() {
    // ...
}

/**
 * Documentation formelle
 * avec JSDoc
 */
function documentedFunction() {
    // ...
}
```

---

## JSDoc : Documentation formelle JavaScript

### Qu'est-ce que JSDoc ?

JSDoc est un système de documentation pour JavaScript qui permet :
- De documenter vos fonctions, classes et modules
- De générer une documentation HTML automatique
- D'améliorer l'auto-complétion dans les éditeurs
- De spécifier les types (utile même sans TypeScript)

### Syntaxe de base

```javascript
/**
 * Description courte de la fonction
 *
 * Description longue optionnelle qui explique
 * en détail ce que fait la fonction
 *
 * @param {type} nomParametre - Description du paramètre
 * @returns {type} Description de ce qui est retourné
 */
```

### Exemples concrets

#### Fonction simple

```javascript
/**
 * Calcule la somme de deux nombres
 *
 * @param {number} a - Premier nombre
 * @param {number} b - Deuxième nombre
 * @returns {number} La somme de a et b
 */
function add(a, b) {
    return a + b;
}
```

#### Fonction avec plusieurs paramètres

```javascript
/**
 * Récupère un utilisateur par son ID
 *
 * @param {number} userId - L'identifiant unique de l'utilisateur
 * @param {boolean} [includeDeleted=false] - Inclure les utilisateurs supprimés
 * @returns {Object|null} L'objet utilisateur ou null si non trouvé
 *
 * @example
 * const user = getUserById(123);
 * const userWithDeleted = getUserById(123, true);
 */
function getUserById(userId, includeDeleted = false) {
    // ...
}
```

#### Fonction avec objet en paramètre

```javascript
/**
 * Crée un nouvel utilisateur
 *
 * @param {Object} userData - Les données de l'utilisateur
 * @param {string} userData.name - Nom complet
 * @param {string} userData.email - Adresse email
 * @param {number} [userData.age] - Âge (optionnel)
 * @returns {Object} L'utilisateur créé avec son ID
 *
 * @throws {Error} Si l'email est invalide
 *
 * @example
 * const user = createUser({
 *   name: 'John Doe',
 *   email: 'john@example.com',
 *   age: 30
 * });
 */
function createUser(userData) {
    if (!isValidEmail(userData.email)) {
        throw new Error('Email invalide');
    }
    // ...
}
```

#### Classe documentée

```javascript
/**
 * Représente un panier d'achat
 *
 * @class
 */
class ShoppingCart {
    /**
     * Crée un nouveau panier
     *
     * @param {string} userId - ID de l'utilisateur
     */
    constructor(userId) {
        this.userId = userId;
        this.items = [];
    }

    /**
     * Ajoute un article au panier
     *
     * @param {Object} item - L'article à ajouter
     * @param {number} item.id - ID du produit
     * @param {string} item.name - Nom du produit
     * @param {number} item.price - Prix unitaire
     * @param {number} quantity - Quantité à ajouter
     * @returns {void}
     *
     * @throws {Error} Si la quantité est négative
     */
    addItem(item, quantity) {
        if (quantity < 0) {
            throw new Error('Quantity must be positive');
        }
        this.items.push({ ...item, quantity });
    }

    /**
     * Calcule le total du panier
     *
     * @returns {number} Le prix total
     */
    getTotal() {
        return this.items.reduce((sum, item) => {
            return sum + (item.price * item.quantity);
        }, 0);
    }
}
```

### Tags JSDoc courants

```javascript
/**
 * @param {type} name - Description
 * @returns {type} Description
 * @throws {Error} Description
 * @example Code exemple
 * @deprecated Utiliser newFunction() à la place
 * @see otherFunction
 * @author Nom de l'auteur
 * @version 1.0.0
 * @since 1.0.0
 * @todo Ce qu'il reste à faire
 * @private Méthode privée
 * @readonly Propriété en lecture seule
 */
```

### Types complexes

```javascript
/**
 * @typedef {Object} User
 * @property {number} id - ID unique
 * @property {string} name - Nom complet
 * @property {string} email - Email
 * @property {string[]} roles - Liste des rôles
 */

/**
 * Traite un utilisateur
 *
 * @param {User} user - L'utilisateur à traiter
 * @returns {void}
 */
function processUser(user) {
    // ...
}

/**
 * @callback RequestCallback
 * @param {Error|null} error - Erreur éventuelle
 * @param {Object} response - Réponse de la requête
 */

/**
 * Fait une requête HTTP
 *
 * @param {string} url - URL cible
 * @param {RequestCallback} callback - Fonction de rappel
 */
function makeRequest(url, callback) {
    // ...
}
```

---

## Commentaires spéciaux (Tags de développement)

### TODO

```javascript
// TODO: Implémenter la validation email
function validateUser(user) {
    // Validation temporaire
    return user.name && user.email;
}

// TODO: [John] Optimiser cette boucle pour de meilleures performances
for (let i = 0; i < items.length; i++) {
    // ...
}

// TODO (v2.0): Ajouter le support des images
function uploadFile(file) {
    // ...
}
```

### FIXME

```javascript
// FIXME: Cette fonction retourne parfois undefined
// Bug reporté : #1234
function getData() {
    // ...
}

// FIXME: Memory leak potentiel ici
// À investiguer avec les outils de profiling
let cache = {};
```

### HACK / WORKAROUND

```javascript
// HACK: Fix temporaire pour IE11
// Retirer quand on abandonne le support IE
if (isIE11) {
    element.style.display = 'block';
}

// WORKAROUND: L'API ne gère pas les accents correctement
// En attendant le fix de leur côté, on encode
const encodedName = encodeURIComponent(userName);
```

### NOTE / IMPORTANT

```javascript
// NOTE: Cette valeur doit correspondre à celle dans le CSS
const MOBILE_BREAKPOINT = 768;

// IMPORTANT: Ne pas modifier cette valeur sans consulter l'équipe backend
const API_VERSION = 'v1';
```

### OPTIMIZE

```javascript
// OPTIMIZE: Cette boucle pourrait être remplacée par un .map()
for (let i = 0; i < users.length; i++) {
    users[i].processed = true;
}
```

### DEPRECATED

```javascript
/**
 * @deprecated Utiliser newGetUser() à la place
 * Cette fonction sera retirée en version 3.0
 */
function getUser() {
    console.warn('getUser() is deprecated. Use newGetUser() instead');
    // ...
}
```

### Organisation avec des tags

```javascript
// ============================================
// TODO: Liste des tâches à faire
// ============================================
// - [ ] Ajouter validation des inputs
// - [ ] Implémenter le cache
// - [ ] Optimiser les requêtes
// - [x] Ajouter les tests (fait)

// ============================================
// FIXME: Bugs connus
// ============================================
// - Bug #1234: Crash sur iOS Safari
// - Bug #5678: Problème d'encodage UTF-8
```

---

## Documentation de projet

### README.md

C'est le fichier d'entrée de votre projet. Doit contenir :

```markdown
# Nom du Projet

Description courte du projet en une phrase.

## Description

Description plus détaillée du projet, ce qu'il fait,
pourquoi il existe.

## Installation

```bash
# Cloner le repo
git clone https://github.com/user/projet.git

# Installer les dépendances
npm install

# Lancer le projet
npm start
```

## Utilisation

Exemples d'utilisation basiques :

```javascript
const app = new App();
app.start();
```

## Structure du projet

```
projet/
├── src/
│   ├── components/    # Composants réutilisables
│   ├── utils/         # Fonctions utilitaires
│   └── main.js        # Point d'entrée
├── public/            # Fichiers statiques
└── tests/             # Tests unitaires
```

## Technologies utilisées

- HTML5
- CSS3
- JavaScript ES6+
- [Autre bibliothèque]

## Contribution

Les contributions sont les bienvenues !
Voir [CONTRIBUTING.md](CONTRIBUTING.md)

## Licence

MIT License - voir [LICENSE](LICENSE)

## Auteurs

- Votre Nom - [GitHub](https://github.com/username)

## Remerciements

- Inspiré de [projet X]
- Merci à [contributeur Y]
```

### CONTRIBUTING.md

```markdown
# Guide de contribution

## Comment contribuer ?

1. Forker le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commiter vos changements (`git commit -m 'Add AmazingFeature'`)
4. Pusher vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## Conventions de code

- Indentation : 2 espaces
- Nommage : camelCase pour variables, PascalCase pour classes
- Commentaires : JSDoc pour les fonctions publiques
- Tests : Toute nouvelle feature doit avoir des tests

## Style de commits

```
type(scope): description courte

Description longue optionnelle

Fixes #123
```

Types : feat, fix, docs, style, refactor, test, chore
```

### CHANGELOG.md

```markdown
# Changelog

Tous les changements notables de ce projet seront documentés ici.

## [2.0.0] - 2025-01-15

### Ajouté
- Nouveau système de cache
- Support du mode sombre
- API de recherche avancée

### Modifié
- Amélioration des performances (30% plus rapide)
- Interface utilisateur redessinée

### Corrigé
- Bug de chargement sur Safari (#234)
- Problème d'encodage UTF-8 (#456)

### Supprimé
- Support d'IE11 (obsolète)

## [1.5.0] - 2024-12-01

### Ajouté
- Authentification OAuth
- Export en PDF

### Corrigé
- Memory leak dans le composant Slider (#123)
```

---

## Commentaires dans le code : Exemples complets

### Exemple 1 : Fonction avec contexte métier

```javascript
/**
 * Calcule le prix final d'une commande
 *
 * IMPORTANT : L'ordre des opérations suit la législation fiscale française
 * (Article 278-0 bis du CGI)
 *
 * @param {number} basePrice - Prix de base HT
 * @param {number} discount - Réduction en pourcentage (0-100)
 * @param {string} country - Code pays ISO (ex: 'FR', 'BE')
 * @returns {number} Prix final TTC
 *
 * @example
 * // Client français avec 10% de réduction
 * const finalPrice = calculateFinalPrice(100, 10, 'FR');
 * // => 108 (100 - 10% = 90, puis +20% TVA = 108)
 *
 * @throws {Error} Si le code pays est invalide
 */
function calculateFinalPrice(basePrice, discount, country) {
    // Validation des entrées
    if (!VALID_COUNTRIES.includes(country)) {
        throw new Error(`Invalid country code: ${country}`);
    }

    // 1. Application de la réduction
    // NOTE: La réduction doit être appliquée AVANT les taxes
    // pour respecter la réglementation (Code de commerce L.123-4)
    const discountedPrice = basePrice * (1 - discount / 100);

    // 2. Récupération du taux de TVA selon le pays
    const taxRate = TAX_RATES[country];

    // 3. Application de la TVA
    const finalPrice = discountedPrice * (1 + taxRate);

    // 4. Arrondi à 2 décimales pour éviter les problèmes
    // de précision flottante (ex: 1.1 + 2.2 = 3.3000000000000003)
    return Math.round(finalPrice * 100) / 100;
}

// Configuration des taux de TVA par pays
// Source : Commission Européenne, mis à jour le 2024-01-01
// https://ec.europa.eu/taxation_customs/business/vat/...
const TAX_RATES = {
    'FR': 0.20,  // France : 20%
    'BE': 0.21,  // Belgique : 21%
    'DE': 0.19,  // Allemagne : 19%
    'ES': 0.21   // Espagne : 21%
};

const VALID_COUNTRIES = Object.keys(TAX_RATES);
```

### Exemple 2 : Algorithme complexe

```javascript
/**
 * Algorithme de recherche floue (Fuzzy Search)
 *
 * Utilise l'algorithme de Levenshtein pour trouver
 * les correspondances approximatives
 *
 * @param {string} query - Terme de recherche
 * @param {string[]} items - Liste d'éléments à chercher
 * @param {number} threshold - Seuil de similarité (0-1)
 * @returns {Array<{item: string, score: number}>} Résultats triés
 */
function fuzzySearch(query, items, threshold = 0.6) {
    const results = [];

    for (const item of items) {
        // Calcul de la distance de Levenshtein
        // (nombre minimum d'opérations pour transformer une chaîne en une autre)
        const distance = levenshteinDistance(
            query.toLowerCase(),
            item.toLowerCase()
        );

        // Normalisation du score entre 0 et 1
        // Plus la distance est petite, meilleur est le score
        const maxLength = Math.max(query.length, item.length);
        const score = 1 - (distance / maxLength);

        // Filtrage selon le seuil
        if (score >= threshold) {
            results.push({ item, score });
        }
    }

    // Tri par score décroissant (meilleurs résultats en premier)
    return results.sort((a, b) => b.score - a.score);
}

/**
 * Calcule la distance de Levenshtein entre deux chaînes
 * Implémentation de l'algorithme de programmation dynamique
 *
 * Complexité : O(m * n) où m et n sont les longueurs des chaînes
 *
 * @private
 * @param {string} str1 - Première chaîne
 * @param {string} str2 - Deuxième chaîne
 * @returns {number} Distance de Levenshtein
 */
function levenshteinDistance(str1, str2) {
    // Matrice de programmation dynamique
    const matrix = [];

    // Initialisation de la première ligne et colonne
    for (let i = 0; i <= str1.length; i++) {
        matrix[i] = [i];
    }
    for (let j = 0; j <= str2.length; j++) {
        matrix[0][j] = j;
    }

    // Remplissage de la matrice
    for (let i = 1; i <= str1.length; i++) {
        for (let j = 1; j <= str2.length; j++) {
            if (str1[i - 1] === str2[j - 1]) {
                // Caractères identiques : pas de coût
                matrix[i][j] = matrix[i - 1][j - 1];
            } else {
                // Prendre le minimum des 3 opérations possibles :
                // - Substitution (diagonal)
                // - Insertion (gauche)
                // - Suppression (haut)
                matrix[i][j] = Math.min(
                    matrix[i - 1][j - 1] + 1,  // substitution
                    matrix[i][j - 1] + 1,      // insertion
                    matrix[i - 1][j] + 1       // suppression
                );
            }
        }
    }

    return matrix[str1.length][str2.length];
}
```

---

## Outils et automatisation

### VS Code : Extensions pour commentaires

**Better Comments**
Colore différemment les types de commentaires :

```javascript
// ! Commentaire d'alerte (rouge)
// ? Commentaire de question (bleu)
// TODO: À faire (orange)
// * Commentaire important (vert)
// // Commentaire barré (gris)
```

**Document This**
Génère automatiquement les commentaires JSDoc :
1. Placer le curseur sur une fonction
2. Ctrl+Alt+D deux fois
3. JSDoc généré automatiquement !

### ESLint : Forcer la documentation

```json
// .eslintrc.json
{
    "plugins": ["jsdoc"],
    "rules": {
        "jsdoc/require-jsdoc": ["warn", {
            "require": {
                "FunctionDeclaration": true,
                "MethodDefinition": true,
                "ClassDeclaration": true
            }
        }],
        "jsdoc/require-param": "warn",
        "jsdoc/require-returns": "warn"
    }
}
```

### Générer de la documentation automatique

**JSDoc CLI :**
```bash
# Installation
npm install -g jsdoc

# Générer la documentation
jsdoc src/ -d docs/

# Ouvrir docs/index.html dans le navigateur
```

**Configuration jsdoc.json :**
```json
{
    "source": {
        "include": ["src/"],
        "includePattern": ".+\\.js(doc|x)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
    "opts": {
        "destination": "./docs",
        "recurse": true,
        "readme": "./README.md"
    }
}
```

---

## Erreurs courantes à éviter

### 1. Commentaires mensongers

```javascript
// ❌ Le commentaire ne correspond pas au code
// Ajoute 10 à la valeur
result = value * 2;  // Multiplie par 2, pas ajoute 10 !

// ✅ Commentaire exact
// Double la valeur
result = value * 2;
```

### 2. Trop de commentaires évidents

```javascript
// ❌ Chaque ligne commentée inutilement
// Déclare firstName
let firstName = 'John';
// Déclare lastName
let lastName = 'Doe';
// Concatène firstName et lastName
let fullName = firstName + ' ' + lastName;

// ✅ Code clair sans commentaires inutiles
let firstName = 'John';
let lastName = 'Doe';
let fullName = `${firstName} ${lastName}`;
```

### 3. Commentaires au lieu de refactoring

```javascript
// ❌ Commenter un code mal écrit
// Cette fonction est compliquée car elle fait plusieurs choses
function x(a,b,c,d) {
    // ...100 lignes...
}

// ✅ Refactoriser en fonctions claires
function calculateTotal(items) {
    const subtotal = calculateSubtotal(items);
    const discount = calculateDiscount(subtotal);
    return applyTax(subtotal - discount);
}
```

### 4. Laisser du code mort commenté

```javascript
// ❌ Code commenté qui traîne
function processData(data) {
    // const oldResult = oldProcessing(data);
    // if (oldResult) {
    //     // faire quelque chose
    //     // return oldResult;
    // }

    return newProcessing(data);
}

// ✅ Supprimer (Git garde l'historique)
function processData(data) {
    return newProcessing(data);
}
```

### 5. Commentaires non maintenus

```javascript
// ❌ Commentaire obsolète
// Retourne toujours true
function isValid(data) {
    // Code modifié depuis, peut retourner false
    return data ? data.isValid : false;
}

// ✅ Commentaire à jour ou supprimé
function isValid(data) {
    return data ? data.isValid : false;
}
```

---

## Bonnes pratiques résumées

### Le test du "pourquoi"

Avant d'écrire un commentaire, demandez-vous :
- **Pourquoi** ai-je fait ce choix ?
- **Pourquoi** ce code est-il là ?
- **Pourquoi** pas une autre approche ?

Si la réponse n'est pas évidente en lisant le code → Commentez !

### Les 5 règles d'or

1. **Code clair > Commentaire** : Préférez du code auto-explicatif
2. **Pourquoi > Quoi** : Expliquez le pourquoi, pas le quoi
3. **Mise à jour** : Un commentaire obsolète est pire que pas de commentaire
4. **Concision** : Commentaires courts et précis
5. **Cohérence** : Style uniforme dans tout le projet

### Template de commentaire fonction

```javascript
/**
 * [Verbe d'action] [ce que fait la fonction]
 *
 * [Explication détaillée optionnelle]
 * [Cas particuliers, avertissements]
 *
 * @param {type} nom - Description
 * @returns {type} Description
 *
 * @example
 * [Exemple d'utilisation]
 *
 * @throws {Error} [Quand une erreur est lancée]
 */
function myFunction(param) {
    // Implementation
}
```

---

## Checklist de documentation

### Pour chaque fonction publique
- [ ] JSDoc avec description courte
- [ ] Tous les @param documentés
- [ ] @returns documenté si la fonction retourne quelque chose
- [ ] @throws documenté si la fonction peut lancer des erreurs
- [ ] Au moins un @example pour les fonctions complexes

### Pour chaque classe
- [ ] JSDoc de classe avec description
- [ ] Constructeur documenté
- [ ] Méthodes publiques documentées
- [ ] Propriétés importantes expliquées

### Pour chaque fichier
- [ ] Commentaire d'en-tête expliquant le rôle du fichier
- [ ] Sections importantes marquées
- [ ] Algorithmes complexes expliqués
- [ ] Références externes citées

### Pour le projet
- [ ] README.md complet et à jour
- [ ] CONTRIBUTING.md si open-source
- [ ] CHANGELOG.md tenu à jour
- [ ] Commentaires en-ligne cohérents

---

## Résumé

### Quand commenter ?

```
✅ OUI
- Choix de conception non évidents
- Algorithmes complexes
- Workarounds et hacks
- Comportements contre-intuitifs
- Références externes
- Avertissements importants

❌ NON
- Code auto-explicatif
- Répéter ce que fait le code
- Commenter du mauvais code
- Laisser du code mort
```

### Style par langage

```
HTML    → <!-- Commentaire -->
CSS     → /* Commentaire */
JS      → // Ligne simple
          /* Multi-lignes */
          /** JSDoc */
```

### Principe fondamental

> **Le code dit COMMENT**
> **Les commentaires disent POURQUOI**

### Citation célèbre

> *"Code tells you how; Comments tell you why."*
>
> — Jeff Atwood

---

## Pour aller plus loin

Dans les prochaines sections :
- **6.2.4** - Indentation et formatage
- **6.2.5** - Principe DRY (Don't Repeat Yourself)

**Ressources :**
- [JSDoc Documentation](https://jsdoc.app/)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- *Clean Code* par Robert C. Martin (Chapitre 4 : Comments)

---

**Un bon commentaire vaut mieux que dix lignes de code illisible.**
**Mais dix lignes de code lisible valent mieux qu'un commentaire ! 📝✨**

⏭️ [Indentation et formatage](/06-integration-html-css-javascript/02-bonnes-pratiques/04-indentation-formatage.md)
