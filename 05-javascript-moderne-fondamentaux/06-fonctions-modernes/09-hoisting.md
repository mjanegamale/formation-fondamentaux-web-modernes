🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.9 - Hoisting : différences entre var, let, const et fonctions

## Introduction

Le **hoisting** (qui signifie "hisser" ou "remonter" en anglais) est un comportement de JavaScript où les **déclarations** de variables et de fonctions sont "remontées" en haut de leur portée avant l'exécution du code.

C'est un concept important à comprendre, même si en JavaScript moderne, nous utilisons des pratiques qui minimisent ses effets potentiellement déroutants.

## Qu'est-ce que le hoisting ?

Avant d'exécuter votre code, JavaScript parcourt votre code et "remonte" toutes les déclarations en haut de leur portée. Cela signifie que vous pouvez parfois utiliser des variables ou des fonctions avant leur déclaration dans le code.

### Analogie simple

Imaginez que vous préparez une recette :
- **Sans hoisting** : vous lisez la recette ligne par ligne et utilisez les ingrédients au fur et à mesure
- **Avec hoisting** : avant de commencer, JavaScript "sort tous les ingrédients (déclarations) sur le plan de travail" et ensuite exécute la recette

## Hoisting des fonctions (déclarations)

Les **déclarations de fonction** sont **complètement** hoistées : déclaration ET définition.

### Vous pouvez appeler avant de déclarer

```javascript
// ✅ Ceci fonctionne !
direBonjour();  // Affiche : "Bonjour !"

function direBonjour() {
  console.log("Bonjour !");
}
```

**Pourquoi ça marche ?** JavaScript "remonte" la fonction complète avant d'exécuter le code.

### Ce qui se passe en réalité

JavaScript traite le code comme s'il était écrit ainsi :

```javascript
// Ce que JavaScript "voit" :
function direBonjour() {
  console.log("Bonjour !");
}

direBonjour();  // Maintenant c'est logique !
```

### Exemple avec plusieurs fonctions

```javascript
calculer();  // ✅ Fonctionne

function calculer() {
  const resultat = additionner(5, 3);
  console.log(resultat);  // 8
}

function additionner(a, b) {
  return a + b;
}
```

Toutes les déclarations de fonction sont remontées, donc l'ordre dans le code source n'a pas d'importance.

## Hoisting de var ⚠️

Avec `var`, seule la **déclaration** est remontée, pas l'**initialisation** (la valeur).

### Comportement de var

```javascript
console.log(x);  // undefined (pas d'erreur, mais pas la valeur attendue)
var x = 10;
console.log(x);  // 10
```

### Ce qui se passe réellement

JavaScript traite le code comme ceci :

```javascript
var x;  // Déclaration remontée
console.log(x);  // undefined (déclaré mais pas encore initialisé)
x = 10;  // Initialisation reste à sa place
console.log(x);  // 10
```

### Exemple plus complexe

```javascript
function exemple() {
  console.log(nom);  // undefined
  var nom = "Alice";
  console.log(nom);  // "Alice"
}

exemple();
```

Équivalent à :

```javascript
function exemple() {
  var nom;  // Déclaration remontée
  console.log(nom);  // undefined
  nom = "Alice";  // Initialisation
  console.log(nom);  // "Alice"
}
```

### Le problème avec var

Ce comportement peut créer des bugs difficiles à détecter :

```javascript
var x = "global";

function test() {
  console.log(x);  // undefined (pas "global" !)
  var x = "local";
  console.log(x);  // "local"
}

test();
```

**Pourquoi `undefined` et non `"global"` ?**

Parce que JavaScript voit :

```javascript
var x = "global";

function test() {
  var x;  // Déclaration locale remontée, masque la variable globale
  console.log(x);  // undefined
  x = "local";
  console.log(x);  // "local"
}
```

## Hoisting de let et const 🆕

Avec `let` et `const`, les déclarations sont techniquement remontées, mais elles sont placées dans une **zone morte temporelle** (TDZ - Temporal Dead Zone).

### Zone Morte Temporelle (TDZ)

Entre le début du bloc et la déclaration, la variable est dans la TDZ : elle existe mais **n'est pas accessible**.

```javascript
console.log(x);  // ❌ ReferenceError: Cannot access 'x' before initialization
let x = 10;
console.log(x);  // 10
```

**Différence importante :** Avec `var`, vous obtenez `undefined`. Avec `let`/`const`, vous obtenez une **erreur**.

### const se comporte pareil

```javascript
console.log(y);  // ❌ ReferenceError: Cannot access 'y' before initialization
const y = 20;
console.log(y);  // 20
```

### Visualisation de la TDZ

```javascript
// Début de la portée
// |
// | <- Zone Morte Temporelle (TDZ)
// | Variables existent mais ne sont pas accessibles
// |
// v
console.log(x);  // ❌ Erreur : dans la TDZ
let x = 10;  // <- Fin de la TDZ pour x
console.log(x);  // ✅ Accessible
```

### Exemple dans un bloc

```javascript
{
  // TDZ commence ici pour x
  console.log(x);  // ❌ ReferenceError
  let x = 5;  // TDZ se termine ici
  console.log(x);  // ✅ 5
}
```

### let/const protègent contre les erreurs

C'est en fait une **bonne chose** ! L'erreur vous alerte immédiatement du problème :

```javascript
// ❌ Avec var : bug silencieux
console.log(utilisateur);  // undefined (on ne voit pas le problème)
var utilisateur = "Alice";

// ✅ Avec let : erreur claire
console.log(utilisateur);  // Erreur claire !
let utilisateur = "Alice";
```

## Expressions de fonction : PAS de hoisting

Les **expressions de fonction** (assignées à des variables) ne sont PAS hoistées comme les déclarations de fonction.

### Avec var

```javascript
direBonjour();  // ❌ TypeError: direBonjour is not a function

var direBonjour = function() {
  console.log("Bonjour !");
};
```

**Ce qui se passe :**

```javascript
var direBonjour;  // Seule la déclaration de la variable est remontée
direBonjour();  // undefined() -> Erreur !
direBonjour = function() {
  console.log("Bonjour !");
};
```

### Avec let/const

```javascript
direBonjour();  // ❌ ReferenceError: Cannot access 'direBonjour' before initialization

const direBonjour = function() {
  console.log("Bonjour !");
};
```

### Arrow functions : même chose

```javascript
saluer();  // ❌ ReferenceError

const saluer = () => {
  console.log("Salut !");
};
```

## Comparaison des quatre cas

| Type | Hoisting | Accessible avant déclaration ? | Valeur avant déclaration |
|------|----------|-------------------------------|--------------------------|
| **Déclaration de fonction** | ✅ Complet | ✅ Oui | La fonction elle-même |
| **var** | ⚠️ Partiel | ⚠️ Oui (mais undefined) | `undefined` |
| **let** | 🔒 TDZ | ❌ Non (erreur) | ReferenceError |
| **const** | 🔒 TDZ | ❌ Non (erreur) | ReferenceError |

### Exemples comparatifs

```javascript
// DÉCLARATION DE FONCTION
console.log(fonc);  // ✅ [Function: fonc]
fonc();            // ✅ "Fonctionne"
function fonc() {
  console.log("Fonctionne");
}

// VAR
console.log(varVar);  // ⚠️ undefined
var varVar = "value";

// LET
console.log(letVar);  // ❌ ReferenceError
let letVar = "value";

// CONST
console.log(constVar);  // ❌ ReferenceError
const constVar = "value";
```

## Exemples pratiques complets

### Exemple 1 : Ordre d'appel des fonctions

```javascript
// ✅ Fonctionne grâce au hoisting
afficherResultat();

function afficherResultat() {
  const resultat = calculer(10, 20);
  console.log("Résultat :", resultat);
}

function calculer(a, b) {
  return a + b;
}
```

### Exemple 2 : Problème classique avec var

```javascript
// ❌ Bug potentiel avec var
function compterAvecVar() {
  console.log(i);  // undefined (on ne voit pas le problème facilement)

  for (var i = 0; i < 3; i++) {
    console.log(i);
  }

  console.log(i);  // 3 (i existe encore ici !)
}

compterAvecVar();
```

### Exemple 3 : Protection avec let

```javascript
// ✅ Erreur claire avec let
function compterAvecLet() {
  console.log(i);  // ❌ ReferenceError (le problème est immédiatement visible)

  for (let i = 0; i < 3; i++) {
    console.log(i);
  }

  console.log(i);  // ❌ ReferenceError (i n'existe pas ici)
}
```

### Exemple 4 : Initialisation conditionnelle

```javascript
function exempleConditionnelle(condition) {
  if (condition) {
    var x = "var dans if";
    let y = "let dans if";
  }

  console.log(x);  // undefined (si condition est false) ou "var dans if"
  console.log(y);  // ❌ ReferenceError (y n'existe pas hors du bloc)
}
```

### Exemple 5 : Fonction vs expression

```javascript
// ✅ Déclaration : hoistée
calculer1();  // Fonctionne

function calculer1() {
  console.log("Fonction déclarée");
}

// ❌ Expression : pas hoistée
calculer2();  // Erreur

const calculer2 = function() {
  console.log("Expression de fonction");
};
```

### Exemple 6 : Shadowing avec hoisting

```javascript
var nom = "Global";

function afficher() {
  console.log(nom);  // undefined (pas "Global" !)

  if (true) {
    var nom = "Local";  // Déclaration remontée en haut de la fonction
  }

  console.log(nom);  // "Local"
}

afficher();
```

Équivalent à :

```javascript
var nom = "Global";

function afficher() {
  var nom;  // Remontée ici !
  console.log(nom);  // undefined

  if (true) {
    nom = "Local";
  }

  console.log(nom);  // "Local"
}
```

## Hoisting dans différentes portées

### Portée globale

```javascript
console.log(x);  // undefined
var x = 10;

console.log(y);  // ReferenceError
let y = 20;
```

### Portée de fonction

```javascript
function exemple() {
  console.log(a);  // undefined
  var a = 1;

  console.log(b);  // ReferenceError
  let b = 2;
}
```

### Portée de bloc

```javascript
{
  console.log(x);  // ReferenceError
  let x = 1;
}

if (true) {
  console.log(y);  // ReferenceError
  const y = 2;
}
```

## Pourquoi le hoisting existe-t-il ?

Le hoisting est un détail d'implémentation de JavaScript qui permet certains patterns utiles :

### 1. Définir les fonctions utilitaires en bas

```javascript
// Code principal lisible en haut
function main() {
  const resultat1 = calculer(5, 3);
  const resultat2 = formater(resultat1);
  afficher(resultat2);
}

main();

// Fonctions utilitaires en bas (plus facile à lire)
function calculer(a, b) {
  return a + b;
}

function formater(valeur) {
  return "Résultat : " + valeur;
}

function afficher(texte) {
  console.log(texte);
}
```

### 2. Récursion mutuelle

```javascript
// Deux fonctions qui s'appellent l'une l'autre
function estPair(n) {
  if (n === 0) return true;
  return estImpair(n - 1);
}

function estImpair(n) {
  if (n === 0) return false;
  return estPair(n - 1);
}

console.log(estPair(4));   // true
console.log(estImpair(5)); // true
```

Sans hoisting, la seconde fonction ne serait pas accessible dans la première.

## Bonnes pratiques pour éviter les problèmes

### 1. N'utilisez jamais var

```javascript
// ❌ Éviter
var x = 10;

// ✅ Utiliser
const x = 10;
// ou
let y = 20;
```

### 2. Déclarez les variables en haut de leur portée

```javascript
// ✅ Bon
function calculer() {
  const a = 10;
  const b = 20;
  const resultat = a + b;

  console.log(resultat);
}

// Moins bon (mais fonctionne)
function calculer() {
  console.log(resultat);  // Utilise avant...

  const resultat = 10 + 20;  // ...de déclarer
}
```

### 3. Déclarez les fonctions avant de les utiliser

Même si le hoisting permet de faire autrement, c'est plus lisible :

```javascript
// ✅ Plus lisible
function helper() {
  return 42;
}

function main() {
  const x = helper();
}

main();
```

### 4. Utilisez les expressions de fonction pour éviter le hoisting

Si vous voulez forcer une erreur en cas d'utilisation prématurée :

```javascript
// ✅ Erreur claire si utilisé trop tôt
const maFonction = () => {
  console.log("Hello");
};
```

### 5. Utilisez const par défaut

```javascript
// ✅ const empêche la réassignation et force une initialisation
const config = {
  api: "https://api.example.com"
};

// ❌ Erreur si on essaie de réassigner
config = {};  // TypeError
```

## Debugging et hoisting

### Comprendre les messages d'erreur

```javascript
// ReferenceError: Cannot access 'x' before initialization
// -> x est dans la TDZ

console.log(x);
let x = 10;
```

```javascript
// ReferenceError: x is not defined
// -> x n'existe nulle part

console.log(x);
```

```javascript
// TypeError: x is not a function
// -> x existe mais n'est pas une fonction

var x = 10;
x();
```

### Utiliser "use strict"

Le mode strict rend certaines erreurs plus évidentes :

```javascript
"use strict";

x = 10;  // ReferenceError: x is not defined
// Sans strict mode : crée une variable globale
```

## Cas particuliers

### Hoisting dans les boucles

```javascript
// Problème classique avec var
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);  // 3, 3, 3 (pas 0, 1, 2)
  }, 100);
}

// ✅ Solution avec let (pas de hoisting problématique)
for (let j = 0; j < 3; j++) {
  setTimeout(() => {
    console.log(j);  // 0, 1, 2
  }, 100);
}
```

### Hoisting et closures

```javascript
function creerFonctions() {
  var fonctions = [];

  for (var i = 0; i < 3; i++) {
    fonctions.push(function() {
      console.log(i);
    });
  }

  return fonctions;
}

const fns = creerFonctions();
fns[0]();  // 3 (pas 0)
fns[1]();  // 3 (pas 1)
fns[2]();  // 3 (pas 2)

// ✅ Avec let, chaque itération a son propre i
function creerFonctionsLet() {
  const fonctions = [];

  for (let i = 0; i < 3; i++) {
    fonctions.push(function() {
      console.log(i);
    });
  }

  return fonctions;
}

const fnsLet = creerFonctionsLet();
fnsLet[0]();  // 0
fnsLet[1]();  // 1
fnsLet[2]();  // 2
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Compter sur le hoisting de var

```javascript
// ❌ Code difficile à comprendre
function mauvais() {
  resultat = calcul * 2;
  var calcul = 10;
  var resultat;
  return resultat;
}

// ✅ Code clair
function bon() {
  const calcul = 10;
  const resultat = calcul * 2;
  return resultat;
}
```

### ❌ Erreur 2 : Redéclarer avec var

```javascript
// ❌ var permet la redéclaration (confus)
var x = 10;
var x = 20;  // Pas d'erreur !
console.log(x);  // 20

// ✅ let/const empêchent la redéclaration
let y = 10;
let y = 20;  // SyntaxError: Identifier 'y' has already been declared
```

### ❌ Erreur 3 : Utiliser une variable dans sa propre initialisation

```javascript
// ❌ Ne fonctionne pas
let x = x + 1;  // ReferenceError: Cannot access 'x' before initialization

// ✅ Correct
let x = 10;
x = x + 1;
```

### ❌ Erreur 4 : Mélanger déclarations et expressions

```javascript
// Peut créer de la confusion
maFonction();  // Fonctionne

function maFonction() {
  autreFunction();  // Erreur !

  const autreFunction = function() {
    console.log("Hello");
  };
}
```

## Résumé visuel

```javascript
// AVANT EXÉCUTION : Ce que JavaScript fait

// Code écrit :
console.log(a);
var a = 1;
console.log(b);
let b = 2;
direBonjour();
function direBonjour() {}

// Code "transformé" par le hoisting :
function direBonjour() {}  // Fonction complète remontée
var a;                      // Déclaration var remontée
// let b;                   // let en TDZ, pas accessible

console.log(a);             // undefined
a = 1;                      // Initialisation reste ici
console.log(b);             // ReferenceError (TDZ)
let b = 2;                  // Fin de TDZ
direBonjour();              // Fonctionne
```

## Points clés à retenir

1. **Hoisting** = les déclarations sont "remontées" avant l'exécution

2. **Déclarations de fonction** : hoisting complet (déclaration + définition)

3. **var** : seule la déclaration est remontée (initialisation = `undefined`)

4. **let/const** : déclaration remontée mais TDZ (erreur si accès prématuré)

5. **Expressions de fonction** : pas de hoisting (se comportent comme des variables)

6. **TDZ** = protection contre l'utilisation prématurée (bonne chose !)

7. **Bonne pratique** : utilisez `const`/`let`, déclarez avant d'utiliser

8. **Ne jamais utiliser** `var` en JavaScript moderne

## Prochaines étapes

Maintenant que vous comprenez le hoisting, vous êtes prêt pour :

- Les **callbacks** (5.6.10) - passer des fonctions en arguments
- Les **closures** (5.13.1) - fonctions qui capturent leur environnement
- Les **modules ES6** (5.13.4) - organiser et partager du code

Le hoisting est un concept important à comprendre, mais en suivant les bonnes pratiques modernes (utiliser `const`/`let`, déclarer avant d'utiliser), vous éviterez la plupart de ses pièges !

---

**Note :** Le hoisting est souvent source de confusion pour les débutants. La bonne nouvelle est qu'en JavaScript moderne, avec `const` et `let`, les comportements surprenants du hoisting sont largement éliminés. La règle simple : déclarez toujours vos variables et fonctions avant de les utiliser, et n'utilisez jamais `var`. Cette approche rend votre code prévisible et facile à comprendre.

⏭️ [Callback functions](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/10-callback-functions.md)
