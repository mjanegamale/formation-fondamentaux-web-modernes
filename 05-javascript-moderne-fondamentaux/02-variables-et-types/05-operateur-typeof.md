🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.2.5 - Opérateur typeof

## Introduction

Maintenant que vous connaissez tous les types primitifs de JavaScript (string, number, boolean, undefined, null, Symbol), une question importante se pose : **comment savoir quel est le type d'une variable** ?

C'est là qu'intervient **typeof**, un opérateur qui vous permet de vérifier le type de n'importe quelle valeur en JavaScript.

> 💡 **Pourquoi c'est important** : En JavaScript, le type d'une variable peut changer (typage dynamique). L'opérateur `typeof` vous aide à savoir avec quel type de données vous travaillez, ce qui est essentiel pour éviter les bugs.

## Qu'est-ce que typeof ?

### Définition

**typeof** est un **opérateur** (comme +, -, *, /) qui retourne une **chaîne de caractères** indiquant le type de la valeur évaluée.

### Syntaxe

Il existe deux façons d'utiliser `typeof` :

```javascript
// Syntaxe 1 : Sans parenthèses (recommandée)
typeof valeur

// Syntaxe 2 : Avec parenthèses (fonctionne aussi)
typeof(valeur)
```

> 💡 **Les deux fonctionnent**, mais la syntaxe sans parenthèses est plus courante car `typeof` est un opérateur, pas une fonction.

### Que retourne typeof ?

`typeof` retourne **toujours un string** parmi ces valeurs possibles :

| Valeur retournée | Type de la valeur |
|------------------|-------------------|
| `"string"` | Chaîne de caractères |
| `"number"` | Nombre |
| `"boolean"` | Booléen |
| `"undefined"` | Non défini |
| `"object"` | Objet, tableau, ou null ⚠️ |
| `"function"` | Fonction |
| `"symbol"` | Symbol (ES6+) |
| `"bigint"` | BigInt (ES2020+) |

## typeof avec les types primitifs

### String

```javascript
console.log(typeof "Alice");           // "string"
console.log(typeof 'Bob');             // "string"
console.log(typeof `Charlie`);         // "string"
console.log(typeof "");                // "string"

const prenom = "Alice";
console.log(typeof prenom);            // "string"
```

### Number

```javascript
console.log(typeof 42);                // "number"
console.log(typeof 3.14);              // "number"
console.log(typeof -10);               // "number"
console.log(typeof 0);                 // "number"

// Nombres spéciaux
console.log(typeof Infinity);          // "number"
console.log(typeof -Infinity);         // "number"
console.log(typeof NaN);               // "number" ⚠️ (même si c'est "Not a Number" !)

const age = 25;
console.log(typeof age);               // "number"
```

> ⚠️ **Attention** : `NaN` (Not a Number) a pour type `"number"` ! C'est contre-intuitif mais c'est ainsi en JavaScript.

### Boolean

```javascript
console.log(typeof true);              // "boolean"
console.log(typeof false);             // "boolean"

const estMajeur = true;
console.log(typeof estMajeur);         // "boolean"

const resultat = 5 > 3;
console.log(typeof resultat);          // "boolean"
```

### Undefined

```javascript
console.log(typeof undefined);         // "undefined"

let variable;
console.log(typeof variable);          // "undefined"

let nom;
console.log(typeof nom);               // "undefined"
```

### Symbol

```javascript
console.log(typeof Symbol());          // "symbol"
console.log(typeof Symbol("id"));      // "symbol"

const id = Symbol("identifiant");
console.log(typeof id);                // "symbol"
```

### BigInt (ES2020+)

```javascript
console.log(typeof 123n);              // "bigint"
console.log(typeof BigInt(456));       // "bigint"

const grandNombre = 9007199254740991n;
console.log(typeof grandNombre);       // "bigint"
```

> 💡 **Note** : BigInt est un type pour les très grands entiers, ajouté récemment à JavaScript. Les débutants n'en auront probablement pas besoin tout de suite.

## typeof avec les types complexes

### Object

```javascript
console.log(typeof {});                      // "object"
console.log(typeof { nom: "Alice" });        // "object"

const personne = {
    nom: "Alice",
    age: 25
};
console.log(typeof personne);                // "object"
```

### Array (tableau)

```javascript
// ⚠️ Les tableaux sont aussi des objets !
console.log(typeof []);                      // "object"
console.log(typeof [1, 2, 3]);               // "object"

const fruits = ["Pomme", "Banane"];
console.log(typeof fruits);                  // "object"
```

> 🐛 **Piège** : `typeof` retourne `"object"` pour les tableaux ! Pour vérifier si quelque chose est un tableau, utilisez `Array.isArray()` (nous le verrons plus tard).

### Function

```javascript
console.log(typeof function() {});           // "function"

function saluer() {
    console.log("Bonjour !");
}
console.log(typeof saluer);                  // "function"

const addition = function(a, b) {
    return a + b;
};
console.log(typeof addition);                // "function"

// Arrow function
const multiplier = (a, b) => a * b;
console.log(typeof multiplier);              // "function"
```

> 💡 **Note** : Techniquement, les fonctions sont des objets en JavaScript, mais `typeof` retourne `"function"` pour les distinguer.

### null - Le bug historique 🐛

```javascript
console.log(typeof null);                    // "object" ⚠️

const valeur = null;
console.log(typeof valeur);                  // "object"
```

> ⚠️ **Bug historique** : `typeof null` retourne `"object"` au lieu de `"null"`. C'est une erreur dans la conception originale de JavaScript qui ne peut pas être corrigée pour des raisons de rétrocompatibilité.

**Comment vérifier null correctement :**

```javascript
const valeur = null;

// ❌ Ne fonctionne pas
if (typeof valeur === "null") {
    console.log("C'est null");  // Ne s'exécute jamais !
}

// ✅ Utilisez la comparaison stricte
if (valeur === null) {
    console.log("C'est null");  // Correct !
}
```

## Cas d'usage pratiques de typeof

### 1. Vérifier le type avant d'utiliser une variable

```javascript
function afficherMessage(message) {
    // Vérifier que message est bien un string
    if (typeof message === "string") {
        console.log(message.toUpperCase());
    } else {
        console.log("Erreur : message doit être un string");
    }
}

afficherMessage("Bonjour");  // "BONJOUR"
afficherMessage(123);        // "Erreur : message doit être un string"
```

### 2. Valider des paramètres de fonction

```javascript
function calculerCarre(nombre) {
    // S'assurer que nombre est bien un number
    if (typeof nombre !== "number") {
        console.log("Erreur : un nombre est requis");
        return null;
    }

    return nombre * nombre;
}

console.log(calculerCarre(5));        // 25
console.log(calculerCarre("cinq"));   // "Erreur : un nombre est requis", null
```

### 3. Vérifier si une variable existe

```javascript
// Vérifier si une variable est définie sans provoquer d'erreur
if (typeof maVariable === "undefined") {
    console.log("La variable n'existe pas");
} else {
    console.log("La variable existe");
}

// Sans typeof, ceci provoquerait une erreur si maVariable n'existe pas
// if (maVariable === undefined) { }  // ❌ ReferenceError possible
```

### 4. Détecter les fonctions

```javascript
function executerSiCestUneFonction(fn) {
    if (typeof fn === "function") {
        fn();  // Exécuter la fonction
    } else {
        console.log("Ce n'est pas une fonction");
    }
}

executerSiCestUneFonction(() => console.log("Hello"));  // "Hello"
executerSiCestUneFonction("texte");                     // "Ce n'est pas une fonction"
```

### 5. Gérer différents types d'entrées

```javascript
function traiter(valeur) {
    const type = typeof valeur;

    switch (type) {
        case "string":
            console.log(`String de ${valeur.length} caractères`);
            break;
        case "number":
            console.log(`Nombre : ${valeur}`);
            break;
        case "boolean":
            console.log(`Booléen : ${valeur ? "vrai" : "faux"}`);
            break;
        case "undefined":
            console.log("Valeur non définie");
            break;
        default:
            console.log(`Type : ${type}`);
    }
}

traiter("Alice");      // "String de 5 caractères"
traiter(42);           // "Nombre : 42"
traiter(true);         // "Booléen : vrai"
traiter(undefined);    // "Valeur non définie"
```

## Tableau récapitulatif complet

| Valeur | typeof retourne | Notes |
|--------|----------------|-------|
| `"Alice"` | `"string"` | |
| `42` | `"number"` | |
| `NaN` | `"number"` | ⚠️ Surprenant ! |
| `Infinity` | `"number"` | |
| `true` | `"boolean"` | |
| `undefined` | `"undefined"` | |
| `null` | `"object"` | 🐛 Bug historique |
| `Symbol()` | `"symbol"` | |
| `123n` | `"bigint"` | ES2020+ |
| `{}` | `"object"` | |
| `[]` | `"object"` | ⚠️ Tableaux aussi ! |
| `function() {}` | `"function"` | |
| `class {}` | `"function"` | Les classes aussi |

## Limitations et pièges de typeof

### 1. Ne distingue pas les tableaux des objets

```javascript
const objet = { nom: "Alice" };
const tableau = [1, 2, 3];

console.log(typeof objet);    // "object"
console.log(typeof tableau);  // "object" ⚠️

// Solution : utiliser Array.isArray()
console.log(Array.isArray(objet));   // false
console.log(Array.isArray(tableau)); // true ✅
```

### 2. null est "object"

```javascript
const valeur = null;
console.log(typeof valeur);  // "object" ⚠️

// Solution : comparaison stricte
console.log(valeur === null);  // true ✅
```

### 3. NaN est "number"

```javascript
const resultat = "texte" * 5;
console.log(typeof resultat);  // "number" ⚠️
console.log(resultat);         // NaN

// Solution : utiliser isNaN()
console.log(isNaN(resultat));  // true ✅
```

### 4. Les classes sont "function"

```javascript
class Personne {
    constructor(nom) {
        this.nom = nom;
    }
}

console.log(typeof Personne);  // "function" ⚠️
```

### 5. Ne fonctionne pas avec les types personnalisés

```javascript
const date = new Date();
console.log(typeof date);  // "object" (pas "date")

const regex = /test/;
console.log(typeof regex);  // "object" (pas "regexp")
```

## Alternatives à typeof

Pour des vérifications plus précises, vous pouvez utiliser d'autres méthodes :

### instanceof - Vérifier la classe/constructeur

```javascript
const date = new Date();
console.log(date instanceof Date);     // true

const tableau = [1, 2, 3];
console.log(tableau instanceof Array); // true

const objet = {};
console.log(objet instanceof Object);  // true
```

### Array.isArray() - Vérifier les tableaux

```javascript
console.log(Array.isArray([1, 2, 3]));        // true
console.log(Array.isArray({ nom: "Alice" })); // false
```

### Object.prototype.toString.call() - Type précis

```javascript
function getType(valeur) {
    return Object.prototype.toString.call(valeur).slice(8, -1);
}

console.log(getType([1, 2, 3]));       // "Array"
console.log(getType(new Date()));      // "Date"
console.log(getType(/test/));          // "RegExp"
console.log(getType(null));            // "Null" ✅
console.log(getType(undefined));       // "Undefined"
```

### Number.isNaN() - Vérifier NaN correctement

```javascript
console.log(Number.isNaN(NaN));      // true
console.log(Number.isNaN("texte"));  // false (pas un nombre)
console.log(Number.isNaN(42));       // false

// Attention : isNaN() global est différent
console.log(isNaN("texte"));         // true (convertit puis teste)
console.log(Number.isNaN("texte"));  // false (pas de conversion)
```

## Comparaisons avec typeof

### Vérifier les types primitifs

```javascript
const valeur1 = "Alice";
const valeur2 = 42;
const valeur3 = true;

// Vérification simple
if (typeof valeur1 === "string") {
    console.log("C'est un string");
}

if (typeof valeur2 === "number") {
    console.log("C'est un nombre");
}

if (typeof valeur3 === "boolean") {
    console.log("C'est un booléen");
}
```

### Vérifier plusieurs types

```javascript
function estPrimitif(valeur) {
    const type = typeof valeur;
    return type === "string" ||
           type === "number" ||
           type === "boolean" ||
           type === "undefined" ||
           type === "symbol";
}

console.log(estPrimitif("Alice"));   // true
console.log(estPrimitif(42));        // true
console.log(estPrimitif({}));        // false
console.log(estPrimitif([]));        // false
```

### Vérifier undefined ET null

```javascript
function estVide(valeur) {
    // Méthode 1 : typeof + comparaison
    return typeof valeur === "undefined" || valeur === null;

    // Méthode 2 : avec == (plus court)
    return valeur == null;
}

console.log(estVide(undefined));  // true
console.log(estVide(null));       // true
console.log(estVide(""));         // false
console.log(estVide(0));          // false
```

## Exemples pratiques complets

### Exemple 1 : Validation de formulaire

```javascript
function validerFormulaire(nom, age, email) {
    const erreurs = [];

    // Vérifier que nom est un string
    if (typeof nom !== "string" || nom === "") {
        erreurs.push("Nom invalide");
    }

    // Vérifier que age est un nombre
    if (typeof age !== "number" || age < 0) {
        erreurs.push("Âge invalide");
    }

    // Vérifier que email est un string
    if (typeof email !== "string" || !email.includes("@")) {
        erreurs.push("Email invalide");
    }

    if (erreurs.length > 0) {
        console.log("Erreurs :", erreurs);
        return false;
    }

    console.log("Formulaire valide !");
    return true;
}

validerFormulaire("Alice", 25, "alice@example.com");  // Valide
validerFormulaire("", 25, "alice@example.com");       // Nom invalide
validerFormulaire("Bob", "25", "bob@example.com");    // Âge invalide
```

### Exemple 2 : Fonction polymorphe (accepte plusieurs types)

```javascript
function afficher(valeur) {
    const type = typeof valeur;

    console.log(`Type: ${type}`);

    if (type === "string") {
        console.log(`String: "${valeur}"`);
    } else if (type === "number") {
        console.log(`Number: ${valeur}`);
    } else if (type === "boolean") {
        console.log(`Boolean: ${valeur ? "✓" : "✗"}`);
    } else if (type === "undefined") {
        console.log("Undefined");
    } else if (type === "function") {
        console.log("Function:", valeur.name || "anonyme");
    } else if (type === "object") {
        if (valeur === null) {
            console.log("Null");
        } else if (Array.isArray(valeur)) {
            console.log(`Array de ${valeur.length} éléments`);
        } else {
            console.log("Object:", valeur);
        }
    }
}

afficher("Alice");              // Type: string
afficher(42);                   // Type: number
afficher(true);                 // Type: boolean
afficher(undefined);            // Type: undefined
afficher(null);                 // Type: object (mais détecte null)
afficher([1, 2, 3]);            // Type: object (mais détecte Array)
afficher({ nom: "Bob" });       // Type: object
afficher(function test() {});   // Type: function
```

### Exemple 3 : Debug helper

```javascript
function debug(nom, valeur) {
    const type = typeof valeur;

    console.log("━━━━━━━━━━━━━━━━━━━━");
    console.log(`Variable: ${nom}`);
    console.log(`Type: ${type}`);
    console.log(`Valeur:`, valeur);

    // Informations supplémentaires selon le type
    if (type === "string") {
        console.log(`Longueur: ${valeur.length} caractères`);
    } else if (type === "number") {
        console.log(`Entier: ${Number.isInteger(valeur)}`);
        console.log(`Fini: ${Number.isFinite(valeur)}`);
    } else if (type === "object" && valeur !== null) {
        if (Array.isArray(valeur)) {
            console.log(`Longueur du tableau: ${valeur.length}`);
        } else {
            console.log(`Nombre de propriétés: ${Object.keys(valeur).length}`);
        }
    }

    console.log("━━━━━━━━━━━━━━━━━━━━");
}

debug("prenom", "Alice");
debug("age", 25);
debug("fruits", ["Pomme", "Banane"]);
debug("personne", { nom: "Bob", age: 30 });
```

## Bonnes pratiques avec typeof

### ✅ À faire

1. **Utilisez === pour comparer les types**
   ```javascript
   if (typeof valeur === "string") { }  // ✅ Correct
   ```

2. **Vérifiez les types dans les fonctions**
   ```javascript
   function calculer(a, b) {
       if (typeof a !== "number" || typeof b !== "number") {
           throw new Error("Les deux paramètres doivent être des nombres");
       }
       return a + b;
   }
   ```

3. **Utilisez typeof pour vérifier undefined en toute sécurité**
   ```javascript
   if (typeof maVariable === "undefined") {
       // Pas de ReferenceError même si maVariable n'existe pas
   }
   ```

4. **Combinez typeof avec d'autres vérifications**
   ```javascript
   if (typeof valeur === "object" && valeur !== null && Array.isArray(valeur)) {
       console.log("C'est un tableau");
   }
   ```

### ❌ À éviter

1. **Ne vérifiez pas null avec typeof**
   ```javascript
   if (typeof valeur === "null") { }   // ❌ Ne fonctionne jamais
   if (valeur === null) { }            // ✅ Correct
   ```

2. **N'oubliez pas que les tableaux sont "object"**
   ```javascript
   if (typeof tableau === "array") { }      // ❌ N'existe pas
   if (Array.isArray(tableau)) { }          // ✅ Correct
   ```

3. **Ne comptez pas sur typeof pour des types complexes**
   ```javascript
   const date = new Date();
   if (typeof date === "date") { }          // ❌ Retourne "object"
   if (date instanceof Date) { }            // ✅ Correct
   ```

4. **N'utilisez pas == avec typeof**
   ```javascript
   if (typeof valeur == "string") { }       // ⚠️ Fonctionne mais === est mieux
   if (typeof valeur === "string") { }      // ✅ Préféré
   ```

## En résumé

### typeof en bref

```javascript
typeof valeur  // Retourne un string indiquant le type
```

**Retourne :**
- `"string"`, `"number"`, `"boolean"` pour les types de base
- `"undefined"` pour les variables non définies
- `"object"` pour les objets, tableaux et **null** ⚠️
- `"function"` pour les fonctions
- `"symbol"` pour les Symbols
- `"bigint"` pour les BigInt

### Points clés à retenir

- ✅ **typeof est un opérateur**, pas une fonction
- ✅ **Retourne toujours un string**
- ✅ **Utile pour vérifier les types primitifs**
- ⚠️ **typeof null === "object"** (bug historique)
- ⚠️ **typeof [] === "object"** (utiliser Array.isArray())
- ⚠️ **typeof NaN === "number"** (utiliser Number.isNaN())

### Quand utiliser typeof ?

| Situation | Utiliser |
|-----------|----------|
| Vérifier string, number, boolean | `typeof` ✅ |
| Vérifier undefined | `typeof` ✅ |
| Vérifier null | `=== null` ✅ |
| Vérifier un tableau | `Array.isArray()` ✅ |
| Vérifier une instance | `instanceof` ✅ |
| Vérifier une fonction | `typeof` ✅ |

> 🎯 **À retenir** : `typeof` est votre outil principal pour vérifier les types primitifs en JavaScript. Connaissez ses limitations (null, tableaux) et utilisez des alternatives quand nécessaire !

## Prochaine étape

Maintenant que vous maîtrisez `typeof` et les types de données, nous allons explorer la **conversion et coercition de types** : comment JavaScript convertit automatiquement (ou comment vous pouvez convertir manuellement) entre différents types.

---


💡 **Conseil** : Créez-vous une petite fonction `debug()` qui utilise `typeof` pour inspecter vos variables pendant le développement. C'est très utile pour comprendre ce qui se passe dans votre code !


⏭️ [Conversion et coercition de types](/05-javascript-moderne-fondamentaux/02-variables-et-types/06-conversion-coercition.md)
