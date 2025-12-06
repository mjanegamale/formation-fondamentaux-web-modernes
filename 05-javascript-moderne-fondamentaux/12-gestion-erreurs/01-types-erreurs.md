🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.12.1 Types d'erreurs courantes

## Introduction

Lorsque vous écrivez du code JavaScript, il est inévitable de rencontrer des erreurs. Comprendre les différents types d'erreurs vous aidera à les identifier rapidement et à les corriger efficacement. Voyons ensemble les erreurs les plus courantes que vous rencontrerez.

---

## Qu'est-ce qu'une erreur en JavaScript ?

Une **erreur** est un problème qui empêche votre code de s'exécuter correctement. Lorsqu'une erreur se produit, JavaScript :
- Arrête l'exécution du code
- Affiche un message d'erreur dans la console
- Indique le type d'erreur et où elle s'est produite

> 💡 **Bon à savoir** : Les erreurs ne sont pas forcément "mauvaises". Elles sont comme des panneaux indicateurs qui vous aident à trouver et corriger les problèmes dans votre code.

---

## Les principaux types d'erreurs

### 1. SyntaxError (Erreur de syntaxe)

**Qu'est-ce que c'est ?**
Une `SyntaxError` se produit quand vous écrivez du code qui ne respecte pas les règles de syntaxe de JavaScript. C'est comme faire une faute de grammaire en français.

**Causes courantes :**
- Oubli d'une parenthèse, d'un crochet ou d'une accolade
- Virgule manquante ou en trop
- Utilisation incorrecte des guillemets
- Mot-clé mal écrit

**Exemples :**

```javascript
// ❌ Parenthèse fermante manquante
console.log("Bonjour";

// ❌ Accolade ouvrante manquante
function direBonjour()
    console.log("Bonjour");
}

// ❌ Guillemet non fermé
const message = "Bonjour tout le monde;

// ❌ Virgule en trop
const nombres = [1, 2, 3,];  // Peut causer une erreur dans certains cas
```

**Message d'erreur typique :**
```
Uncaught SyntaxError: Unexpected token '}'
Uncaught SyntaxError: missing ) after argument list
```

**Comment la corriger ?**
Vérifiez attentivement votre code ligne par ligne. Les éditeurs modernes comme VS Code vous aident souvent en soulignant les erreurs de syntaxe en rouge.

---

### 2. ReferenceError (Erreur de référence)

**Qu'est-ce que c'est ?**
Une `ReferenceError` se produit quand vous essayez d'utiliser une variable ou une fonction qui n'existe pas ou qui n'est pas accessible.

**Causes courantes :**
- Utilisation d'une variable non déclarée
- Faute de frappe dans le nom d'une variable
- Tentative d'accès à une variable en dehors de sa portée (scope)
- Utilisation d'une variable avant sa déclaration (avec `let` ou `const`)

**Exemples :**

```javascript
// ❌ Variable non déclarée
console.log(prenom);  // ReferenceError: prenom is not defined

// ❌ Faute de frappe
const message = "Bonjour";
console.log(mesage);  // ReferenceError: mesage is not defined

// ❌ Variable utilisée avant déclaration
console.log(age);  // ReferenceError
let age = 25;

// ❌ Variable en dehors de sa portée
if (true) {
    let ville = "Paris";
}
console.log(ville);  // ReferenceError: ville is not defined
```

**Message d'erreur typique :**
```
Uncaught ReferenceError: prenom is not defined
```

**Comment la corriger ?**
- Vérifiez l'orthographe de vos variables
- Assurez-vous que la variable est déclarée avant de l'utiliser
- Vérifiez que vous êtes dans la bonne portée (scope)

---

### 3. TypeError (Erreur de type)

**Qu'est-ce que c'est ?**
Une `TypeError` se produit quand vous essayez d'effectuer une opération sur une valeur d'un type inapproprié.

**Causes courantes :**
- Appeler quelque chose qui n'est pas une fonction
- Accéder à une propriété de `null` ou `undefined`
- Modifier une constante
- Utiliser une méthode sur le mauvais type de données

**Exemples :**

```javascript
// ❌ Appeler une variable comme une fonction
const nombre = 42;
nombre();  // TypeError: nombre is not a function

// ❌ Accéder à une propriété de null
const utilisateur = null;
console.log(utilisateur.nom);  // TypeError: Cannot read property 'nom' of null

// ❌ Accéder à une propriété de undefined
let personne;
console.log(personne.age);  // TypeError: Cannot read property 'age' of undefined

// ❌ Modifier une constante
const PI = 3.14;
PI = 3.14159;  // TypeError: Assignment to constant variable

// ❌ Utiliser une méthode de string sur un nombre
const age = 25;
age.toUpperCase();  // TypeError: age.toUpperCase is not a function
```

**Message d'erreur typique :**
```
Uncaught TypeError: Cannot read property 'nom' of null
Uncaught TypeError: nombre is not a function
```

**Comment la corriger ?**
- Vérifiez le type de vos variables avant de les utiliser
- Utilisez des conditions pour vérifier si une valeur existe
- Assurez-vous d'utiliser les bonnes méthodes pour le bon type de données

---

### 4. RangeError (Erreur de plage)

**Qu'est-ce que c'est ?**
Une `RangeError` se produit quand vous utilisez une valeur en dehors de sa plage autorisée.

**Causes courantes :**
- Créer un tableau avec une taille négative ou trop grande
- Utiliser des fonctions de conversion avec des valeurs invalides
- Récursion infinie (trop d'appels de fonction)

**Exemples :**

```javascript
// ❌ Tableau avec une taille négative
const tableau = new Array(-1);  // RangeError: Invalid array length

// ❌ toFixed avec trop de décimales
const nombre = 3.14159;
nombre.toFixed(101);  // RangeError: toFixed() digits argument must be between 0 and 100

// ❌ Récursion infinie
function boucleInfinie() {
    boucleInfinie();  // RangeError: Maximum call stack size exceeded
}
boucleInfinie();
```

**Message d'erreur typique :**
```
Uncaught RangeError: Invalid array length
Uncaught RangeError: Maximum call stack size exceeded
```

**Comment la corriger ?**
- Vérifiez les valeurs que vous passez aux fonctions
- Assurez-vous que vos boucles et récursions ont une condition d'arrêt

---

## Autres erreurs courantes

### URIError

Se produit lors de l'utilisation incorrecte de fonctions globales de manipulation d'URI comme `encodeURI()` ou `decodeURI()`.

```javascript
// ❌ URI mal formée
decodeURIComponent('%');  // URIError: URI malformed
```

### EvalError

Historiquement liée à la fonction `eval()`, cette erreur est rare dans le JavaScript moderne.

---

## Comment lire un message d'erreur

Prenons un exemple de message d'erreur complet :

```
Uncaught TypeError: Cannot read property 'nom' of null
    at getUserName (script.js:15)
    at displayProfile (script.js:28)
    at HTMLButtonElement.<anonymous> (script.js:42)
```

**Décortiquons ce message :**

1. **`Uncaught`** : L'erreur n'a pas été interceptée (nous verrons comment faire dans les prochaines sections)

2. **`TypeError`** : Le type d'erreur

3. **`Cannot read property 'nom' of null`** : La description du problème

4. **`at getUserName (script.js:15)`** :
   - L'erreur s'est produite dans la fonction `getUserName`
   - Dans le fichier `script.js`
   - À la ligne 15

5. **Les lignes suivantes** : La pile d'appels (call stack) qui montre comment on est arrivé à cette erreur

---

## Conseils pratiques pour éviter les erreurs

### 1. Utilisez un éditeur avec coloration syntaxique
VS Code et autres éditeurs modernes détectent automatiquement beaucoup d'erreurs de syntaxe.

### 2. Déclarez toujours vos variables
```javascript
// ✅ Bon
const nom = "Alice";

// ❌ Mauvais (mode non-strict uniquement)
nom = "Alice";  // Crée une variable globale accidentellement
```

### 3. Vérifiez les valeurs avant de les utiliser
```javascript
// ✅ Bon
const utilisateur = getUser();
if (utilisateur) {
    console.log(utilisateur.nom);
}

// ❌ Risqué
const utilisateur = getUser();
console.log(utilisateur.nom);  // Erreur si utilisateur est null
```

### 4. Utilisez le mode strict
```javascript
'use strict';

// Aide à détecter plus d'erreurs
x = 10;  // ReferenceError en mode strict
```

### 5. Faites attention aux fautes de frappe
```javascript
const message = "Bonjour";
console.log(mesage);  // ReferenceError à cause de la faute
```

---

## Tableau récapitulatif

| Type d'erreur | Quand elle se produit | Exemple courant |
|---------------|----------------------|-----------------|
| **SyntaxError** | Code mal écrit syntaxiquement | Parenthèse manquante |
| **ReferenceError** | Variable inexistante ou inaccessible | Faute de frappe dans un nom |
| **TypeError** | Opération sur un mauvais type | Appeler `null.propriete` |
| **RangeError** | Valeur hors limites | Tableau de taille négative |

---

## Points clés à retenir

1. **Les erreurs sont normales** : Même les développeurs expérimentés en rencontrent quotidiennement

2. **Lisez les messages d'erreur** : Ils contiennent des informations précieuses sur le problème et sa localisation

3. **La console est votre amie** : Ouvrez-la toujours (F12) pour voir les erreurs en temps réel

4. **Prévention > Correction** : Un code bien écrit et vérifié génère moins d'erreurs

5. **Apprenez à déboguer** : Savoir identifier et corriger les erreurs est une compétence essentielle

---

## Prochaines étapes

Maintenant que vous connaissez les types d'erreurs, vous allez apprendre dans les prochaines sections :
- Comment intercepter et gérer les erreurs avec `try...catch`
- Comment créer vos propres erreurs personnalisées
- Comment utiliser les outils de debugging du navigateur

> 💡 **Astuce ** : Ne vous découragez pas face aux erreurs ! Chaque erreur résolue vous rend meilleur en programmation. C'est en comprenant et en corrigeant les erreurs qu'on apprend vraiment à coder.

⏭️ [Structure try...catch...finally](/05-javascript-moderne-fondamentaux/12-gestion-erreurs/02-try-catch-finally.md)
