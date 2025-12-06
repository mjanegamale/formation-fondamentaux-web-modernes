🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.2.1 - Déclaration moderne : const et let 🆕

## Introduction

Bienvenue dans votre première vraie leçon de code JavaScript ! Nous allons apprendre à créer des **variables**, qui sont les briques de base de tout programme informatique.

Une variable, c'est comme une **boîte avec une étiquette** dans laquelle vous pouvez stocker une information (un nombre, un texte, etc.) pour l'utiliser plus tard dans votre programme.

> 💡 **Métaphore** : Imaginez votre code comme une cuisine. Les variables sont comme des bocaux étiquetés où vous stockez des ingrédients (farine, sucre, sel...). Vous pouvez ensuite utiliser ces ingrédients dans vos recettes (fonctions).

## Qu'est-ce qu'une variable ?

### Définition simple

Une **variable** est un espace de stockage nommé qui contient une valeur. Cette valeur peut être :
- Un nombre : `25`, `3.14`, `-10`
- Du texte : `"Bonjour"`, `"Alice"`
- Un booléen (vrai/faux) : `true`, `false`
- Et bien d'autres types que nous verrons plus tard

### Pourquoi avons-nous besoin de variables ?

Sans variables, vous devriez réécrire les mêmes valeurs encore et encore :

```javascript
// Sans variable (répétitif et difficile à maintenir)
console.log("Bonjour Alice !");
console.log("Alice a 25 ans");
console.log("L'email de Alice est alice@example.com");

// Si Alice change de nom, vous devez modifier 3 endroits !
```

Avec des variables, c'est beaucoup plus simple :

```javascript
// Avec variable (facile à maintenir)
let nom = "Alice";
console.log("Bonjour " + nom + " !");
console.log(nom + " a 25 ans");
console.log("L'email de " + nom + " est alice@example.com");

// Si le nom change, vous ne modifiez qu'un seul endroit !
```

## Les deux façons modernes de déclarer des variables : const et let

En JavaScript moderne (ES6+), il existe **deux mots-clés** pour créer des variables :

| Mot-clé | Usage | Peut changer ? |
|---------|-------|----------------|
| **`const`** | Valeur constante | ❌ Non |
| **`let`** | Valeur qui peut changer | ✅ Oui |

> ⚡ **Important** : Oubliez `var` pour le moment ! C'est l'ancienne méthode. Nous verrons pourquoi elle pose problème dans la section suivante, mais dans vos nouveaux projets, utilisez **toujours** `const` ou `let`.

## const - Pour les valeurs constantes 🔒

### Syntaxe

```javascript
const nomDeVariable = valeur;
```

### Qu'est-ce qu'une constante ?

Une **constante** est une variable dont la valeur **ne peut pas être modifiée** après sa création. Une fois qu'elle est définie, elle reste toujours la même.

### Exemples pratiques

```javascript
// Déclarer une constante
const prenom = "Alice";
console.log(prenom);  // Affiche : Alice

// Informations qui ne changent pas
const anneeNaissance = 1995;
const PI = 3.14159;
const EMAIL = "alice@example.com";

console.log(anneeNaissance);  // 1995
console.log(PI);              // 3.14159
```

### Tentative de modification (❌ Erreur !)

```javascript
const age = 25;
console.log(age);  // 25

age = 26;  // ❌ TypeError: Assignment to constant variable
```

Le navigateur vous empêchera de modifier une constante. C'est une protection !

### Pourquoi utiliser const ?

#### 1. Sécurité 🛡️

Si vous savez qu'une valeur ne doit pas changer, `const` vous protège contre les modifications accidentelles :

```javascript
const tauxTVA = 0.20;

// Plus tard dans votre code...
tauxTVA = 0.19;  // ❌ Erreur ! Vous ne pouvez pas modifier accidentellement le taux
```

#### 2. Lisibilité 📖

Quand vous voyez `const`, vous savez immédiatement que cette valeur ne changera pas. Cela rend le code plus facile à comprendre.

```javascript
const URL_API = "https://api.example.com";
const COULEUR_PRIMAIRE = "#3498db";
const MAX_TENTATIVES = 3;

// Un développeur qui lit ce code sait que ces valeurs sont fixes
```

#### 3. Intention claire 💬

Utiliser `const` indique votre **intention** : "Cette valeur est importante et ne doit pas changer."

### Quand utiliser const ?

Utilisez `const` pour :

✅ Les valeurs de configuration
```javascript
const API_KEY = "abc123";
const PORT = 3000;
```

✅ Les constantes mathématiques
```javascript
const PI = 3.14159;
const VITESSE_LUMIERE = 299792458;  // m/s
```

✅ Les valeurs qui ne doivent jamais changer
```javascript
const MON_NOM = "Alice";
const DATE_NAISSANCE = "1995-06-15";
```

✅ Les références aux éléments du DOM
```javascript
const bouton = document.getElementById('mon-bouton');
const titre = document.querySelector('h1');
```

> 🎯 **Règle d'or** : Utilisez `const` **par défaut**. N'utilisez `let` que si vous savez que la valeur changera.

## let - Pour les valeurs qui changent 🔄

### Syntaxe

```javascript
let nomDeVariable = valeur;
```

### Qu'est-ce que let ?

`let` permet de créer une variable dont la valeur **peut être modifiée** après sa création.

### Exemples pratiques

```javascript
// Déclarer une variable
let age = 25;
console.log(age);  // 25

// Modifier sa valeur
age = 26;
console.log(age);  // 26

// Modifier à nouveau
age = 27;
console.log(age);  // 27
```

### Compteur qui augmente

```javascript
let compteur = 0;
console.log(compteur);  // 0

compteur = compteur + 1;  // On peut aussi écrire : compteur++
console.log(compteur);  // 1

compteur = compteur + 1;
console.log(compteur);  // 2
```

### Valeur qui évolue dans le temps

```javascript
let score = 0;
console.log("Score initial:", score);  // 0

// Le joueur marque des points
score = score + 10;
console.log("Après action 1:", score);  // 10

score = score + 25;
console.log("Après action 2:", score);  // 35

score = score - 5;
console.log("Après pénalité:", score);  // 30
```

### Quand utiliser let ?

Utilisez `let` pour :

✅ Les compteurs et boucles
```javascript
let i = 0;
let total = 0;
let nombreTentatives = 0;
```

✅ Les valeurs temporaires qui évoluent
```javascript
let message = "Chargement...";
// Plus tard...
message = "Chargement terminé !";
```

✅ Les accumulations et calculs
```javascript
let somme = 0;
somme = somme + 10;
somme = somme + 20;
somme = somme + 30;
console.log(somme);  // 60
```

✅ Les états qui changent
```javascript
let estConnecte = false;
// Après connexion...
estConnecte = true;
```

## const vs let : Comment choisir ? 🤔

Voici un guide de décision simple :

```
┌─────────────────────────────────────────┐
│  La valeur va-t-elle changer            │
│  dans mon programme ?                   │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴───────┐
       │               │
      OUI             NON
       │               │
       ▼               ▼
    ┌─────┐        ┌──────┐
    │ let │        │ const│
    └─────┘        └──────┘
```

### Exemples de décision

| Situation | Mot-clé | Raison |
|-----------|---------|--------|
| Nom d'utilisateur saisi | `let` | Peut changer si l'utilisateur modifie son profil |
| URL de l'API | `const` | Ne change jamais pendant l'exécution |
| Score d'un jeu | `let` | Augmente ou diminue pendant la partie |
| Taux de TVA | `const` | Fixe pour toute l'application |
| Compteur de boucle | `let` | S'incrémente à chaque itération |
| Nom de l'application | `const` | Reste identique |

### Principe de base : Préférez const

```javascript
// ✅ Bonne pratique : commencez avec const
const nom = "Alice";
const ville = "Paris";

// Si vous réalisez que la valeur doit changer, passez à let
let age = 25;
age = 26;  // OK, je peux le modifier
```

> 💡 **Conseil** : Déclarez toutes vos variables avec `const`. Si le code vous signale une erreur parce que vous essayez de modifier la valeur, changez alors `const` en `let`. C'est mieux que l'inverse !

## Règles de nommage des variables 📝

Pour nommer vos variables, suivez ces règles :

### Règles obligatoires (syntaxe)

✅ **Doit commencer par :**
- Une lettre (a-z, A-Z)
- Un underscore (_)
- Un dollar ($)

```javascript
let nom = "Alice";      // ✅ OK
let _private = true;    // ✅ OK
let $jquery = {};       // ✅ OK
```

❌ **Ne peut pas commencer par :**
- Un chiffre
- Un caractère spécial (sauf _ et $)

```javascript
let 1nom = "Alice";     // ❌ Erreur de syntaxe
let mon-nom = "Alice";  // ❌ Erreur de syntaxe
let @email = "test";    // ❌ Erreur de syntaxe
```

✅ **Peut contenir :**
- Lettres (a-z, A-Z)
- Chiffres (0-9)
- Underscores (_)
- Dollar ($)

```javascript
let nom2 = "Bob";           // ✅ OK
let prix_total = 100;       // ✅ OK
let user123 = "Charlie";    // ✅ OK
```

❌ **Ne peut pas contenir :**
- Espaces
- Tirets (sauf underscore)
- Caractères accentués (à éviter)

```javascript
let mon nom = "Alice";      // ❌ Erreur
let prix-total = 100;       // ❌ Erreur
let prénom = "Alice";       // ⚠️ Fonctionne mais déconseillé
```

### Conventions de nommage (bonnes pratiques)

#### 1. CamelCase pour les variables normales

```javascript
// ✅ Bon : camelCase (première lettre minuscule)
let prenom = "Alice";
let nomComplet = "Alice Dupont";
let ageUtilisateur = 25;
let scoreTotal = 100;

// ❌ Éviter : PascalCase (réservé aux classes)
let Prenom = "Alice";
let NomComplet = "Alice Dupont";
```

**Règle du camelCase :**
- Première lettre en minuscule
- Chaque nouveau mot commence par une majuscule
- Pas d'espaces ni de tirets

#### 2. SCREAMING_SNAKE_CASE pour les constantes "vraies"

```javascript
// ✅ Pour les valeurs qui ne changeront JAMAIS
const PI = 3.14159;
const TAUX_TVA = 0.20;
const URL_API = "https://api.example.com";
const COULEUR_PRIMAIRE = "#3498db";
const MAX_TENTATIVES = 3;
```

#### 3. Noms descriptifs et explicites

```javascript
// ❌ Mauvais : noms trop courts ou cryptiques
let x = "Alice";
let a = 25;
let t = 100;

// ✅ Bon : noms clairs et descriptifs
let nomUtilisateur = "Alice";
let ageUtilisateur = 25;
let scoreTotal = 100;
```

#### 4. Éviter les abréviations obscures

```javascript
// ❌ Difficile à comprendre
let nbUs = 5;
let prixTtc = 120;

// ✅ Plus clair
let nombreUtilisateurs = 5;
let prixTTC = 120;  // OK si l'abréviation est universelle
```

### Mots réservés (interdits)

Certains mots sont **réservés** par JavaScript et ne peuvent pas être utilisés comme noms de variables :

```javascript
// ❌ Interdits (mots-clés JavaScript)
let if = 10;          // Erreur
let function = 5;     // Erreur
let return = true;    // Erreur
let class = "test";   // Erreur
let const = 42;       // Erreur
let let = 10;         // Erreur
```

**Liste des principaux mots réservés :**
`break`, `case`, `catch`, `class`, `const`, `continue`, `debugger`, `default`, `delete`, `do`, `else`, `export`, `extends`, `false`, `finally`, `for`, `function`, `if`, `import`, `in`, `instanceof`, `let`, `new`, `null`, `return`, `super`, `switch`, `this`, `throw`, `true`, `try`, `typeof`, `var`, `void`, `while`, `with`, `yield`

## Initialisation des variables

### Initialisation immédiate (recommandée)

```javascript
// ✅ Déclarer et initialiser en même temps
const nom = "Alice";
let age = 25;
```

### Déclaration sans initialisation

```javascript
// Avec let : possible mais la valeur est undefined
let prenom;
console.log(prenom);  // undefined
prenom = "Bob";
console.log(prenom);  // "Bob"

// Avec const : IMPOSSIBLE !
const nom;  // ❌ SyntaxError: Missing initializer in const declaration
```

> ⚡ **Important** : Une variable déclarée avec `const` **doit** être initialisée immédiatement. Avec `let`, c'est optionnel mais recommandé.

### Déclaration multiple

```javascript
// Déclarer plusieurs variables en une ligne
let a = 1, b = 2, c = 3;

// Mais c'est plus lisible sur plusieurs lignes
let prenom = "Alice";
let nom = "Dupont";
let age = 25;
```

## Exemples pratiques complets

### Exemple 1 : Informations utilisateur

```javascript
// Informations qui ne changent pas
const PRENOM = "Alice";
const NOM = "Dupont";
const DATE_NAISSANCE = "1995-06-15";

// Informations qui peuvent changer
let age = 30;
let ville = "Paris";
let estConnecte = false;

console.log(PRENOM + " " + NOM);  // Alice Dupont
console.log("Âge:", age);          // Âge: 30
console.log("Ville:", ville);      // Ville: Paris

// Simulation : anniversaire !
age = 31;
console.log("Nouvel âge:", age);   // Nouvel âge: 31

// Simulation : déménagement
ville = "Lyon";
console.log("Nouvelle ville:", ville);  // Nouvelle ville: Lyon

// Simulation : connexion
estConnecte = true;
console.log("Connecté ?", estConnecte);  // Connecté ? true
```

### Exemple 2 : Calcul de prix

```javascript
// Configuration fixe
const PRIX_UNITAIRE = 50;
const TAUX_TVA = 0.20;

// Valeurs qui changent selon la commande
let quantite = 3;
let sousTotal = 0;
let totalTTC = 0;

// Calculs
sousTotal = PRIX_UNITAIRE * quantite;
console.log("Sous-total:", sousTotal);  // 150

totalTTC = sousTotal * (1 + TAUX_TVA);
console.log("Total TTC:", totalTTC);    // 180

// Nouvelle commande
quantite = 5;
sousTotal = PRIX_UNITAIRE * quantite;
totalTTC = sousTotal * (1 + TAUX_TVA);
console.log("Nouveau total:", totalTTC);  // 300
```

### Exemple 3 : Compteur simple

```javascript
// État initial
let compteur = 0;
console.log("Compteur initial:", compteur);  // 0

// Incrémenter
compteur = compteur + 1;
console.log("Après +1:", compteur);  // 1

compteur = compteur + 1;
console.log("Après +1:", compteur);  // 2

compteur = compteur + 5;
console.log("Après +5:", compteur);  // 7

// Décrémenter
compteur = compteur - 3;
console.log("Après -3:", compteur);  // 4

// Réinitialiser
compteur = 0;
console.log("Après reset:", compteur);  // 0
```

## Erreurs courantes à éviter 🐛

### 1. Modifier une constante

```javascript
const age = 25;
age = 26;  // ❌ TypeError: Assignment to constant variable
```

**Solution :** Utilisez `let` si la valeur doit changer.

### 2. Oublier de déclarer la variable

```javascript
'use strict';
nom = "Alice";  // ❌ ReferenceError: nom is not defined
```

**Solution :** Utilisez toujours `const` ou `let`.

```javascript
const nom = "Alice";  // ✅ OK
```

### 3. Réutiliser le même nom

```javascript
let prenom = "Alice";
let prenom = "Bob";  // ❌ SyntaxError: Identifier 'prenom' has already been declared
```

**Solution :** Choisissez un nom différent ou réaffectez la valeur.

```javascript
let prenom = "Alice";
prenom = "Bob";  // ✅ OK : réaffectation
```

### 4. Utiliser une variable avant de la déclarer

```javascript
console.log(age);  // ❌ ReferenceError
let age = 25;
```

**Solution :** Déclarez toujours vos variables avant de les utiliser.

```javascript
let age = 25;
console.log(age);  // ✅ OK
```

## Comparaison rapide : const vs let

| Critère | const | let |
|---------|-------|-----|
| **Réaffectation** | ❌ Non | ✅ Oui |
| **Initialisation obligatoire** | ✅ Oui | ❌ Non |
| **Usage recommandé** | Par défaut | Si la valeur change |
| **Sécurité** | ✅ Plus sûr | ⚠️ Moins sûr |
| **Intention** | Valeur fixe | Valeur variable |

## Récapitulatif des bonnes pratiques ✅

1. **Préférez `const` par défaut** : N'utilisez `let` que si nécessaire
2. **Nommez clairement vos variables** : `nombreUtilisateurs` plutôt que `nb`
3. **Utilisez camelCase** : `monNomDeVariable`
4. **MAJUSCULES pour constantes "vraies"** : `const PI = 3.14159`
5. **Initialisez toujours vos variables** : `let age = 25` plutôt que `let age;`
6. **Une déclaration par ligne** pour la lisibilité
7. **Déclarez en haut** de votre bloc de code

## En résumé

### const 🔒
```javascript
const PI = 3.14159;  // Valeur qui ne change JAMAIS
```
- Déclare une **constante**
- La valeur **ne peut pas être modifiée**
- **Doit être initialisée** immédiatement
- À utiliser **par défaut**

### let 🔄
```javascript
let age = 25;   // Valeur qui PEUT changer
age = 26;       // Modification OK
```
- Déclare une **variable**
- La valeur **peut être modifiée**
- Initialisation optionnelle (mais recommandée)
- À utiliser **uniquement si la valeur change**

> 🎯 **À retenir** : En JavaScript moderne, utilisez `const` par défaut et `let` seulement quand la valeur doit changer. N'utilisez jamais `var` dans du nouveau code !

## Prochaine étape

Dans la section suivante, nous verrons pourquoi `var` (l'ancienne façon de déclarer des variables) ne doit plus être utilisé dans du code moderne. Comprendre ses problèmes vous aidera à apprécier les avantages de `const` et `let` !

---


🆕 **Moderne** : `const` et `let` sont les standards ES6+ et doivent être utilisés dans tout nouveau code JavaScript !

⏭️ [ var : pourquoi on ne l'utilise plus (concept historique)](/05-javascript-moderne-fondamentaux/02-variables-et-types/02-var-concept-historique.md)
