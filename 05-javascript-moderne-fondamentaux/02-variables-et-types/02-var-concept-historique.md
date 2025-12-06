🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.2.2 - ⚠️ var : pourquoi on ne l'utilise plus (concept historique)

## Introduction

Dans la section précédente, vous avez appris à déclarer des variables avec `const` et `let`, les méthodes **modernes** introduites en ES6 (2015). Mais si vous lisez du code JavaScript plus ancien ou si vous cherchez des tutoriels sur Internet, vous rencontrerez inévitablement `var`.

Cette section explique ce qu'est `var`, pourquoi il a été la seule façon de déclarer des variables pendant 20 ans, et surtout **pourquoi vous ne devez plus l'utiliser** dans vos nouveaux projets.

> ⚠️ **Important** : Cette section est à titre **informatif uniquement**. Vous devez comprendre `var` pour lire du vieux code, mais **n'utilisez jamais `var` dans du nouveau code** ! Utilisez toujours `const` ou `let`.

## Qu'est-ce que var ?

### Un peu d'histoire 📚

`var` (pour "variable") était la **seule façon** de déclarer des variables en JavaScript de 1995 à 2015. Pendant 20 ans, tous les développeurs JavaScript l'utilisaient quotidiennement.

```javascript
// De 1995 à 2015, on écrivait comme ça :
var nom = "Alice";
var age = 25;
var estConnecte = true;
```

En 2015, avec l'arrivée d'**ES6**, JavaScript a introduit `let` et `const` pour corriger les nombreux problèmes de `var`.

### Syntaxe de var

```javascript
var nomDeVariable = valeur;
```

À première vue, ça ressemble beaucoup à `let` :

```javascript
// Avec var (ancien)
var prenom = "Alice";
var age = 25;
age = 26;  // On peut modifier la valeur

// Avec let (moderne)
let prenom = "Alice";
let age = 25;
age = 26;  // Même comportement de base
```

Alors, quel est le problème ? 🤔

## Les 5 problèmes majeurs de var

### Problème 1 : Scope de fonction au lieu de scope de bloc 🚨

C'est le **problème le plus grave** de `var`.

#### Qu'est-ce que le scope ?

Le **scope** (ou portée) définit où une variable est accessible dans votre code.

#### Comportement de let (scope de bloc) ✅

```javascript
{
    let x = 10;
    console.log(x);  // 10 - OK, x existe dans ce bloc
}

console.log(x);  // ❌ ReferenceError: x is not defined
// x n'existe que dans le bloc { }
```

Les **accolades** `{ }` créent un bloc. Avec `let`, la variable n'existe que dans son bloc.

#### Comportement de var (scope de fonction) ⚠️

```javascript
{
    var x = 10;
    console.log(x);  // 10 - OK
}

console.log(x);  // 10 - ⚠️ x existe toujours !
// var ignore les blocs, la variable "fuite" !
```

Avec `var`, les accolades sont **ignorées** ! La variable est accessible partout dans la fonction (ou globalement si hors d'une fonction).

#### Exemple concret du problème

**Avec var (problématique) :**

```javascript
function compter() {
    var resultat = [];

    for (var i = 0; i < 3; i++) {
        resultat.push(function() {
            console.log(i);
        });
    }

    // Quel devrait être i maintenant ?
    console.log(i);  // 3 - ⚠️ i existe encore ici !

    // Qu'affichent ces fonctions ?
    resultat[0]();  // 3 (on attendait 0 !)
    resultat[1]();  // 3 (on attendait 1 !)
    resultat[2]();  // 3 (on attendait 2 !)
}

compter();
```

**Avec let (correct) :**

```javascript
function compter() {
    const resultat = [];

    for (let i = 0; i < 3; i++) {
        resultat.push(function() {
            console.log(i);
        });
    }

    // console.log(i);  // ❌ ReferenceError - i n'existe plus ici

    resultat[0]();  // 0 ✅
    resultat[1]();  // 1 ✅
    resultat[2]();  // 2 ✅
}

compter();
```

#### Comparaison scope : var vs let

```javascript
// Exemple avec if
if (true) {
    var x = 10;
    let y = 20;
}

console.log(x);  // 10 - var fuite du bloc if
console.log(y);  // ❌ ReferenceError - let reste dans le bloc

// Exemple avec boucle for
for (var i = 0; i < 3; i++) {
    // ...
}
console.log(i);  // 3 - ⚠️ i existe encore !

for (let j = 0; j < 3; j++) {
    // ...
}
console.log(j);  // ❌ ReferenceError - ✅ j n'existe plus
```

### Problème 2 : Peut être redéclaré 🔄

#### Comportement de let/const (protection) ✅

```javascript
let nom = "Alice";
let nom = "Bob";  // ❌ SyntaxError: Identifier 'nom' has already been declared
// JavaScript vous protège contre les redéclarations accidentelles
```

#### Comportement de var (pas de protection) ⚠️

```javascript
var nom = "Alice";
console.log(nom);  // "Alice"

var nom = "Bob";  // ⚠️ Aucune erreur !
console.log(nom);  // "Bob"

// Plus tard dans le code...
var nom = "Charlie";  // ⚠️ Toujours aucune erreur !
console.log(nom);  // "Charlie"
```

**Pourquoi c'est problématique ?**

Dans un gros projet, vous pouvez accidentellement réutiliser le même nom de variable et écraser une valeur importante sans le savoir !

```javascript
var compteur = 0;
// ... 500 lignes de code ...
var compteur = 10;  // ⚠️ Oups ! J'ai écrasé l'ancien compteur par erreur
// Le premier compteur est perdu, et c'est difficile à déboguer
```

### Problème 3 : Hoisting bizarre 👻

Le **hoisting** (levage) est un comportement de JavaScript où les déclarations sont "remontées" en haut de leur scope.

#### Comportement de let/const (Temporal Dead Zone) ✅

```javascript
console.log(nom);  // ❌ ReferenceError: Cannot access 'nom' before initialization
let nom = "Alice";
// JavaScript vous empêche d'utiliser la variable avant sa déclaration
```

#### Comportement de var (hoisting confus) ⚠️

```javascript
console.log(nom);  // undefined - ⚠️ Pas d'erreur mais valeur bizarre
var nom = "Alice";
console.log(nom);  // "Alice"
```

**Ce que JavaScript fait en réalité :**

```javascript
// JavaScript "remonte" la déclaration mais pas l'initialisation
var nom;  // Déclaration remontée (= undefined)
console.log(nom);  // undefined
nom = "Alice";  // Initialisation à sa place originale
console.log(nom);  // "Alice"
```

**Exemple plus complexe :**

```javascript
function tester() {
    console.log(x);  // undefined - ⚠️ Pas d'erreur !

    if (false) {
        var x = 10;  // Ce code ne s'exécute jamais
    }

    console.log(x);  // undefined - x existe quand même !
}

tester();
```

Avec `let`, ce serait une erreur claire au lieu d'un `undefined` mystérieux.

### Problème 4 : Variables globales accidentelles 🌍

Sans strict mode, oublier `var` crée une variable **globale** silencieusement.

```javascript
function calculer() {
    resultat = 10 * 5;  // ⚠️ Oubli de var
    return resultat;
}

calculer();
console.log(resultat);  // 50 - ⚠️ Variable globale créée !
console.log(window.resultat);  // 50 - Accessible partout !
```

Même avec `var`, c'est facile de polluer le scope global :

```javascript
var nom = "Alice";  // Variable globale
console.log(window.nom);  // "Alice" - Attachée à l'objet global !
```

Avec `let` et `const`, ce problème est beaucoup moins présent.

### Problème 5 : Pas de constantes 📌

Avec `var`, **tout** peut être modifié. Il n'y a aucun moyen de protéger une valeur constante.

```javascript
var PI = 3.14159;
// ... Plus tard dans le code ...
PI = 3.14;  // ⚠️ Aucune erreur, la "constante" est modifiée !

var API_URL = "https://api.example.com";
API_URL = "https://autre.com";  // ⚠️ Modifié accidentellement
```

Avec `const`, vous avez une vraie protection :

```javascript
const PI = 3.14159;
PI = 3.14;  // ❌ TypeError: Assignment to constant variable
```

## Tableau comparatif : var vs let vs const

| Caractéristique | var ⚠️ | let ✅ | const ✅ |
|----------------|--------|--------|----------|
| **Scope** | Fonction | Bloc | Bloc |
| **Redéclaration** | ✅ Autorisée | ❌ Interdite | ❌ Interdite |
| **Hoisting** | Oui (undefined) | Oui (TDZ) | Oui (TDZ) |
| **Réaffectation** | ✅ Oui | ✅ Oui | ❌ Non |
| **Temporal Dead Zone** | ❌ Non | ✅ Oui | ✅ Oui |
| **Variable globale** | Attachée à window | Non attachée | Non attachée |
| **Usage moderne** | ⚠️ Déprécié | ✅ Standard | ✅ Standard |

**TDZ (Temporal Dead Zone)** : Zone où la variable existe mais ne peut pas être accédée avant sa déclaration.

## Exemples de problèmes réels avec var

### Exemple 1 : Bug de boucle classique

```javascript
// Code qui devrait afficher 0, 1, 2, 3, 4 avec un délai
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log(i);  // Affiche : 5, 5, 5, 5, 5 ⚠️
    }, 1000);
}

// Pourquoi ? Car var n'a qu'une seule instance de i
// Quand setTimeout s'exécute, i vaut déjà 5

// Solution avec let :
for (let i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log(i);  // Affiche : 0, 1, 2, 3, 4 ✅
    }, 1000);
}

// let crée une nouvelle instance de i pour chaque itération
```

### Exemple 2 : Conflit de noms

```javascript
var nom = "Alice";
console.log(nom);  // "Alice"

// ... 200 lignes de code plus loin ...

function traiterUtilisateur() {
    var nom = "Bob";  // ⚠️ Même nom !
    console.log(nom);  // "Bob"
}

traiterUtilisateur();
console.log(nom);  // "Alice" - OK ici, mais confus
```

Si ces deux `var nom` étaient au même niveau, le deuxième écraserait le premier sans avertissement.

### Exemple 3 : Variable qui "fuite" d'un if

```javascript
function verifierAge(age) {
    if (age >= 18) {
        var message = "Vous êtes majeur";
        console.log(message);
    }

    // ⚠️ message existe toujours ici !
    console.log(message);  // "Vous êtes majeur" (si age >= 18)
                           // undefined (si age < 18)
}

verifierAge(20);

// Avec let :
function verifierAge(age) {
    if (age >= 18) {
        let message = "Vous êtes majeur";
        console.log(message);
    }

    console.log(message);  // ❌ ReferenceError - beaucoup plus clair !
}
```

## Quand peut-on encore voir var ?

Vous rencontrerez `var` dans :

### 1. Code ancien (pré-2015)

```javascript
// Ancien code JavaScript
var $ = jQuery;
var App = {};
var config = {
    api: "https://api.example.com"
};
```

### 2. Tutoriels obsolètes

Malheureusement, beaucoup de tutoriels sur Internet n'ont pas été mis à jour et enseignent encore `var`.

> 💡 **Conseil** : Si un tutoriel utilise `var`, remplacez-le mentalement par `let` ou `const`. Le reste du tutoriel reste valable.

### 3. Bibliothèques anciennes

Certaines bibliothèques JavaScript créées avant 2015 utilisent `var` dans leur code source.

```javascript
// Code interne d'une vieille bibliothèque
(function() {
    var version = "1.0.0";
    var settings = {};
    // ...
})();
```

### 4. Support de navigateurs très anciens

Si vous devez supporter Internet Explorer 10 ou antérieur (ce qui est rare aujourd'hui), vous devrez peut-être utiliser `var` ou transpiler votre code avec Babel.

## Migration de var vers let/const

Si vous devez moderniser du vieux code, voici comment procéder :

### Règle simple de migration

```javascript
// ❌ Ancien code avec var
var nom = "Alice";
var age = 25;
var PI = 3.14159;

// ✅ Code moderne
const nom = "Alice";    // Ne change pas → const
let age = 25;           // Peut changer → let
const PI = 3.14159;     // Constante → const
```

### Processus de migration

1. **Remplacez `var` par `const` par défaut**
   ```javascript
   var nom = "Alice";  →  const nom = "Alice";
   ```

2. **Si une erreur apparaît (réaffectation), utilisez `let`**
   ```javascript
   const compteur = 0;
   compteur++;  // ❌ Erreur

   // → Changez en let
   let compteur = 0;
   compteur++;  // ✅ OK
   ```

3. **Vérifiez les problèmes de scope**
   ```javascript
   for (var i = 0; i < 10; i++) { }
   console.log(i);  // Fonctionne avec var

   for (let i = 0; i < 10; i++) { }
   console.log(i);  // ❌ Erreur avec let (c'est mieux !)
   ```

## Pourquoi var existe-t-il encore ?

Vous vous demandez peut-être : "Si var est si problématique, pourquoi JavaScript ne l'a-t-il pas supprimé ?"

### Compatibilité ascendante 🔄

JavaScript suit un principe strict : **"Ne jamais casser le web"**.

Des millions de sites web utilisent encore `var` dans leur code. Si JavaScript supprimait `var`, tous ces sites cesseraient de fonctionner du jour au lendemain !

Au lieu de cela, JavaScript a :
- ✅ Gardé `var` (pour ne pas casser le code existant)
- ✅ Ajouté `let` et `const` (pour le nouveau code)
- ✅ Encouragé les développeurs à migrer progressivement

C'est ce qu'on appelle la **rétrocompatibilité**.

## Ce que vous devez retenir

### ✅ À faire

1. **Utilisez `const` par défaut** dans tout nouveau code
2. **Utilisez `let`** quand la valeur change
3. **Ne jamais utiliser `var`** dans du nouveau code
4. **Comprenez `var`** pour lire du vieux code
5. **Remplacez `var` par `const`/`let`** lors de refactoring

### ❌ À éviter

1. ❌ N'utilisez pas `var` dans les nouveaux projets
2. ❌ Ne copiez pas du code avec `var` sans le moderniser
3. ❌ N'apprenez pas en profondeur `var` (comprendre suffit)

## Comparaison finale

```javascript
// ❌ ANCIEN STYLE (ne plus utiliser)
var prenom = "Alice";
var age = 25;
var ville = "Paris";

// ✅ STYLE MODERNE (à utiliser)
const prenom = "Alice";  // Ne change pas
let age = 25;            // Peut changer
const ville = "Paris";   // Ne change pas
```

## Questions fréquentes

### "Puis-je mélanger var, let et const ?"

**Non recommandé !** Utilisez uniquement `let` et `const` pour la cohérence.

```javascript
// ❌ Éviter le mélange
var x = 10;
let y = 20;
const z = 30;

// ✅ Cohérent et moderne
const x = 10;
let y = 20;
const z = 30;
```

### "Et si je vois var dans un tutoriel ?"

Remplacez mentalement `var` par `const` ou `let`. Le reste du tutoriel reste valable.

```javascript
// Tutoriel dit :
var nom = "Alice";

// Vous écrivez :
const nom = "Alice";
```

### "Dois-je comprendre var en profondeur ?"

**Non.** Comprenez juste :
- Ce que c'est (ancienne façon de déclarer)
- Pourquoi on ne l'utilise plus (scope, hoisting, etc.)
- Comment le remplacer par `const`/`let`

Vous n'avez pas besoin de devenir expert en `var` !

## En résumé

### var - L'ancienne méthode ⚠️

```javascript
var nom = "Alice";  // Ne plus utiliser !
```

**Problèmes :**
- Scope de fonction (pas de scope de bloc)
- Peut être redéclaré sans erreur
- Hoisting confus
- Crée des variables globales facilement
- Pas de protection pour les constantes

### let et const - Les méthodes modernes ✅

```javascript
const nom = "Alice";  // Préférer const
let age = 25;         // Utiliser let si change
```

**Avantages :**
- Scope de bloc (plus intuitif)
- Pas de redéclaration accidentelle
- Temporal Dead Zone (protection)
- Pas de pollution globale
- `const` protège les valeurs constantes

> 🎯 **À retenir** : `var` est un vestige du passé de JavaScript. Dans tout nouveau code, utilisez exclusivement `const` et `let`. Votre code sera plus sûr, plus clair et plus facile à maintenir !

## Prochaine étape

Maintenant que vous comprenez pourquoi on n'utilise plus `var`, nous allons explorer les **types de données primitifs** en JavaScript : les chaînes de caractères (strings), les nombres (numbers) et les booléens (booleans).

---


⚠️ **Historique** : Cette section explique un concept legacy. Utilisez toujours `const` et `let` dans vos projets !

⏭️ [Types primitifs : string, number, boolean](/05-javascript-moderne-fondamentaux/02-variables-et-types/03-types-primitifs.md)
