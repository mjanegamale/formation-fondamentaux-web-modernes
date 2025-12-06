🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6 - Fonctions modernes

## Introduction

Les **fonctions** sont l'un des concepts les plus importants et les plus puissants en JavaScript. Elles sont au cœur de presque tout ce que vous ferez en programmation : organiser votre code, réutiliser des opérations, gérer les événements, manipuler des données, et bien plus encore.

Cette section vous guidera à travers tous les aspects des fonctions en JavaScript moderne, des bases fondamentales aux concepts avancés comme les callbacks et les paramètres rest. Vous apprendrez non seulement les différentes façons de créer des fonctions, mais aussi quand et comment utiliser chacune d'elles.

## Pourquoi les fonctions sont essentielles

### 1. Réutilisabilité du code

Au lieu de répéter le même code plusieurs fois, vous l'écrivez une fois dans une fonction et l'appelez quand vous en avez besoin.

```javascript
// Sans fonction : répétition
console.log("Prix avec TVA :", 100 * 1.2);
console.log("Prix avec TVA :", 50 * 1.2);
console.log("Prix avec TVA :", 75 * 1.2);

// Avec fonction : réutilisable
const calculerTTC = (prixHT) => prixHT * 1.2;
console.log("Prix avec TVA :", calculerTTC(100));
console.log("Prix avec TVA :", calculerTTC(50));
console.log("Prix avec TVA :", calculerTTC(75));
```

### 2. Organisation et lisibilité

Les fonctions permettent de découper un programme complexe en petites parties compréhensibles, chacune avec un nom qui décrit ce qu'elle fait.

```javascript
// Code organisé avec des fonctions bien nommées
function traiterCommande(commande) {
  validerCommande(commande);
  calculerTotal(commande);
  appliquerRemises(commande);
  enregistrerCommande(commande);
  envoyerConfirmation(commande);
}
```

### 3. Abstraction

Les fonctions cachent la complexité et vous permettent de penser à un niveau plus élevé.

```javascript
// Vous n'avez pas besoin de savoir comment fonctionne fetch en interne
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data));
```

### 4. Facilitation des tests

Des fonctions bien conçues sont plus faciles à tester et à déboguer.

```javascript
// Fonction testable
function estEmailValide(email) {
  return email.includes("@") && email.includes(".");
}

// Facile à tester
console.log(estEmailValide("test@example.com")); // true
console.log(estEmailValide("invalid"));          // false
```

## Approche moderne : ES6 et au-delà 🆕

Cette section met l'accent sur les **pratiques modernes** introduites avec ES6 (ECMAScript 2015) et les versions ultérieures. Vous apprendrez :

- Les **arrow functions** (`=>`) - la syntaxe concise moderne
- Les **paramètres par défaut** - rendre vos fonctions plus flexibles
- Les **rest parameters** (`...args`) - gérer un nombre variable d'arguments
- Le **scope de bloc** avec `let` et `const` - éviter les pièges de `var`
- Et bien plus encore !

### Concepts anciens à connaître ⚠️

Nous aborderons aussi quelques concepts plus anciens (comme `var` et l'objet `arguments`) **uniquement pour que vous puissiez les reconnaître** dans du code existant, mais nous vous apprendrons à utiliser les alternatives modernes qui sont plus sûres et plus claires.

## Ce que vous allez apprendre

Cette section est organisée de manière progressive, du plus simple au plus avancé. Voici le parcours complet :

### Les bases (5.6.1 - 5.6.3)

**5.6.1 - Déclaration de fonction classique**
- Comment créer votre première fonction
- Paramètres et arguments
- Le mot-clé `return`
- Quand et pourquoi utiliser cette syntaxe

**5.6.2 - Expression de fonction**
- Assigner des fonctions à des variables
- Fonctions anonymes
- Différence avec les déclarations
- Le problème du hoisting

**5.6.3 - Fonctions fléchées (Arrow functions)** 🆕
- La syntaxe moderne et concise
- Return implicite
- Différences de comportement avec `this`
- Quand utiliser les arrow functions

### Paramètres avancés (5.6.4 - 5.6.6)

**5.6.4 - Paramètres et arguments**
- Comprendre la différence
- Passage par valeur vs par référence
- Nombre variable d'arguments
- Bonnes pratiques de paramètres

**5.6.5 - Paramètres par défaut** 🆕
- Donner des valeurs par défaut aux paramètres
- Rendre vos fonctions plus robustes
- Éviter les vérifications manuelles
- Expressions par défaut dynamiques

**5.6.6 - Rest parameters (...args)** 🆕
- Capturer un nombre indéfini d'arguments
- Remplacer l'ancien objet `arguments`
- Combiner avec des paramètres normaux
- Différence avec le spread operator

### Concepts fondamentaux (5.6.7 - 5.6.9)

**5.6.7 - Valeur de retour (return)**
- Comment renvoyer des résultats
- Différence entre `return` et `console.log`
- Multiples `return` dans une fonction
- Pattern "early return"

**5.6.8 - Portée (scope)**
- Scope de bloc avec `let`/`const` 🆕
- Scope de fonction avec `var` ⚠️
- Portées imbriquées
- Variables globales vs locales

**5.6.9 - Hoisting**
- Comment JavaScript "remonte" les déclarations
- Différences entre `var`, `let`, `const` et fonctions
- Zone Morte Temporelle (TDZ)
- Éviter les pièges du hoisting

### Callbacks (5.6.10)

**5.6.10 - Callback functions**
- Passer des fonctions en arguments
- Callbacks synchrones vs asynchrones
- Utilisation avec les méthodes de tableau
- Introduction à la programmation asynchrone

## Progression pédagogique

Cette section est conçue pour être suivie **dans l'ordre**. Chaque chapitre s'appuie sur les précédents :

```
Déclaration classique
    ↓
Expression de fonction
    ↓
Arrow functions (syntaxe moderne) ✨
    ↓
Paramètres et arguments (fondamentaux)
    ↓
Paramètres par défaut (ES6+)
    ↓
Rest parameters (ES6+)
    ↓
Return (utilisation des résultats)
    ↓
Scope (où les variables existent)
    ↓
Hoisting (comportement de JavaScript)
    ↓
Callbacks (fonctions en arguments) ✨
```

## Syntaxes modernes vs anciennes

Tout au long de cette section, vous verrez des comparaisons entre :

### ✅ Approche moderne (recommandée)

```javascript
// Arrow function avec const
const calculer = (x, y = 10) => x + y;

// Rest parameters
const additionner = (...nombres) => {
  return nombres.reduce((acc, n) => acc + n, 0);
};

// Scope de bloc avec let
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

### ⚠️ Approche ancienne (à éviter, mais à connaître)

```javascript
// Expression de fonction avec var
var calculer = function(x, y) {
  y = y || 10;  // Ancienne façon de gérer les défauts
  return x + y;
};

// Objet arguments
function additionner() {
  var somme = 0;
  for (var i = 0; i < arguments.length; i++) {
    somme += arguments[i];
  }
  return somme;
};

// var a un scope de fonction, pas de bloc
for (var i = 0; i < 3; i++) {
  console.log(i);
}
console.log(i);  // 3 - i existe encore !
```

**Notre recommandation :** Apprenez et utilisez les syntaxes modernes. Connaissez les anciennes uniquement pour lire du code existant.

## Concepts clés à retenir

Au fil de cette section, vous rencontrerez ces concepts essentiels :

### 1. Les fonctions sont des valeurs

En JavaScript, les fonctions sont des "citoyens de première classe" (*first-class citizens*) :

```javascript
// Assigner à une variable
const maFonction = () => console.log("Hello");

// Passer en argument
setTimeout(() => console.log("Delayed"), 1000);

// Retourner depuis une fonction
const creer = () => () => console.log("Nested");
```

### 2. Différentes syntaxes, même résultat

Il existe plusieurs façons de créer des fonctions, chacune avec ses avantages :

```javascript
// Déclaration
function calculer(x) { return x * 2; }

// Expression
const calculer = function(x) { return x * 2; };

// Arrow function
const calculer = (x) => x * 2;
```

### 3. Le scope est crucial

Comprendre où vos variables sont accessibles est fondamental :

```javascript
const global = "accessible partout";

function exemple() {
  const local = "accessible uniquement ici";

  if (true) {
    const bloc = "accessible uniquement dans ce bloc";
  }
}
```

### 4. Les callbacks sont partout

Passer des fonctions en arguments est un pattern omniprésent en JavaScript :

```javascript
// Méthodes de tableau
[1, 2, 3].map(n => n * 2);

// Événements
bouton.addEventListener("click", () => alert("Cliqué"));

// Timers
setTimeout(() => console.log("Later"), 1000);
```

## Comment utiliser cette section

### Pour les débutants complets

Si vous découvrez les fonctions :

1. **Suivez l'ordre** : Commencez par 5.6.1 et progressez séquentiellement
2. **Pratiquez** : Essayez les exemples dans votre console ou éditeur
3. **Prenez votre temps** : Les fonctions sont fondamentales, ne vous précipitez pas
4. **Revenez si nécessaire** : N'hésitez pas à relire les sections précédentes

### Pour ceux qui ont des bases

Si vous connaissez déjà les fonctions :

1. **Concentrez-vous sur les nouveautés** : Sections marquées 🆕
2. **Comparez** : Regardez les différences entre ancien et moderne
3. **Approfondissez** : Hoisting, scope, callbacks sont souvent mal compris
4. **Modernisez** : Apprenez les patterns ES6+ pour améliorer votre code

### Pour ceux qui viennent d'autres langages

Si vous programmez déjà :

1. **Attention aux différences** : JavaScript a des particularités (hoisting, scope, `this`)
2. **Callbacks** : Concept central en JavaScript, prenez le temps de bien comprendre
3. **Arrow functions** : Similaires aux lambdas, mais avec des différences subtiles
4. **Asynchrone** : JavaScript est mono-thread mais non-bloquant

## Liens avec d'autres sections

Les fonctions sont connectées à de nombreux autres concepts JavaScript :

### Sections précédentes utilisées

- **Variables (5.2)** : `const` et `let` pour déclarer des fonctions
- **Opérateurs (5.4)** : Utilisés dans les fonctions
- **Structures de contrôle (5.5)** : `if`, boucles dans les fonctions

### Sections suivantes qui utilisent les fonctions

- **Objets (5.7)** : Méthodes d'objets sont des fonctions
- **Tableaux (5.8)** : Méthodes avec callbacks (map, filter, reduce)
- **DOM (5.9)** : Manipulation via des fonctions
- **Événements (5.10)** : Callbacks pour gérer les interactions
- **Asynchrone (5.11)** : Callbacks, Promises, async/await
- **Closures (5.13.1)** : Concept avancé de portée

## Ressources complémentaires

Après avoir complété cette section, vous pourrez explorer :

- **MDN Web Docs** : Documentation de référence sur les fonctions
- **JavaScript.info** : Tutoriels détaillés sur les fonctions
- **Eloquent JavaScript** : Chapitre sur les fonctions (gratuit en ligne)

## Objectifs d'apprentissage

À la fin de cette section, vous serez capable de :

- ✅ Créer des fonctions avec différentes syntaxes (déclaration, expression, arrow)
- ✅ Utiliser les paramètres et arguments efficacement
- ✅ Comprendre et utiliser les paramètres par défaut et rest parameters
- ✅ Retourner des valeurs et les utiliser dans votre code
- ✅ Comprendre le scope (portée) et éviter les bugs liés aux variables
- ✅ Expliquer le hoisting et ses implications
- ✅ Utiliser les callbacks pour la programmation asynchrone et les méthodes de tableau
- ✅ Choisir la syntaxe appropriée selon le contexte
- ✅ Écrire du code JavaScript moderne et idiomatique

## Conseils avant de commencer

### 1. Expérimentez

Les fonctions s'apprennent en les utilisant. Créez des exemples, modifiez-les, cassez-les pour comprendre comment ils fonctionnent.

```javascript
// Essayez différentes variantes
const test1 = () => console.log("Version 1");
const test2 = (x) => x * 2;
const test3 = (x, y = 10) => x + y;
```

### 2. Utilisez la console

La console du navigateur (F12) est votre amie pour tester rapidement :

```javascript
// Testez directement
const doubler = x => x * 2;
console.log(doubler(5));  // 10
```

### 3. Lisez les messages d'erreur

Les erreurs vous apprennent beaucoup. Ne les ignorez pas, essayez de les comprendre.

```javascript
// Cette erreur vous apprend quelque chose !
const x = () => return 5;  // SyntaxError
```

### 4. Comparez les syntaxes

Pour chaque concept, comparez l'ancienne et la nouvelle façon de faire :

```javascript
// Ancien
var maFonction = function(x, y) {
  y = y || 10;
  return x + y;
};

// Moderne
const maFonction = (x, y = 10) => x + y;
```

## Prêt à commencer ?

Les fonctions sont le cœur de JavaScript. Maîtriser les fonctions, c'est maîtriser JavaScript.

Cette section vous donnera toutes les connaissances nécessaires pour créer des fonctions efficaces, lisibles et modernes. Que vous soyez débutant ou que vous cherchiez à moderniser vos connaissances, vous trouverez ici tout ce qu'il faut savoir.

**Commençons par les bases avec la déclaration de fonction classique ! →**

---

*Note : Les sections marquées 🆕 indiquent des fonctionnalités modernes ES6+. Les sections marquées ⚠️ indiquent des concepts anciens à connaître mais à éviter dans votre code.*

⏭️ [Déclaration de fonction classique](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/01-declaration-classique.md)
