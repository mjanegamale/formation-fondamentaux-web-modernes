🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.8 - Portée : scope de bloc (let/const) vs scope de fonction

## Introduction

La **portée** (ou **scope** en anglais) détermine **où** dans votre code une variable est accessible et utilisable. C'est l'un des concepts les plus importants à comprendre en JavaScript, car il affecte directement comment vos variables se comportent.

Avec l'introduction d'ES6, JavaScript a deux types principaux de portée :
- **Scope de bloc** (avec `let` et `const`) 🆕
- **Scope de fonction** (avec `var` et les fonctions) ⚠️

## Qu'est-ce que la portée ?

La portée définit la **zone de visibilité** d'une variable. Une variable n'est accessible que dans sa portée.

### Analogie simple

Imaginez des pièces dans une maison :
- Une variable dans une pièce (portée) n'est visible que dans cette pièce
- Pour qu'elle soit visible ailleurs, elle doit être dans une pièce "parente" ou "commune"

## Les trois types de portée

### 1. Portée globale

Les variables déclarées **en dehors** de toute fonction ou bloc sont dans la portée **globale** : accessibles partout.

```javascript
const nom = "Alice";  // Variable globale

function afficher() {
  console.log(nom);  // ✅ Accessible ici
}

afficher();  // Affiche : "Alice"
console.log(nom);  // ✅ Accessible ici aussi
```

### 2. Portée de fonction

Les variables déclarées **dans une fonction** ne sont accessibles que dans cette fonction.

```javascript
function exemple() {
  const message = "Hello";  // Variable locale à la fonction
  console.log(message);  // ✅ Accessible ici
}

exemple();  // Affiche : "Hello"
console.log(message);  // ❌ Erreur : message is not defined
```

### 3. Portée de bloc (ES6+)

Les variables `let` et `const` déclarées dans un **bloc** `{ }` ne sont accessibles que dans ce bloc.

```javascript
{
  const message = "Hello";  // Variable de bloc
  console.log(message);  // ✅ Accessible ici
}

console.log(message);  // ❌ Erreur : message is not defined
```

## Scope de bloc avec let et const 🆕

### Définition

Un **bloc** est délimité par des accolades `{ }` :
- Blocs `if`, `else`
- Blocs `for`, `while`
- Blocs de fonction
- Blocs indépendants

Les variables déclarées avec `let` ou `const` dans un bloc sont **limitées à ce bloc**.

### Exemple avec if

```javascript
const age = 25;

if (age >= 18) {
  const message = "Vous êtes majeur";  // Scope du bloc if
  console.log(message);  // ✅ Accessible ici
}

console.log(message);  // ❌ Erreur : message is not defined
```

### Exemple avec for

```javascript
for (let i = 0; i < 3; i++) {
  console.log(i);  // ✅ i est accessible ici
}

console.log(i);  // ❌ Erreur : i is not defined
```

**C'est très utile !** La variable `i` n'existe que dans la boucle, évitant les conflits.

### Exemple avec bloc indépendant

```javascript
{
  const x = 10;
  console.log(x);  // ✅ 10
}

{
  const x = 20;  // Nouvelle variable x dans un autre bloc
  console.log(x);  // ✅ 20
}

console.log(x);  // ❌ Erreur : x is not defined
```

### let vs const : même portée de bloc

```javascript
if (true) {
  let a = 10;     // Scope de bloc
  const b = 20;   // Scope de bloc
}

console.log(a);  // ❌ Erreur
console.log(b);  // ❌ Erreur
```

**Les deux** `let` et `const` ont un scope de bloc. La seule différence est que `const` ne peut pas être réassigné.

## Scope de fonction avec var ⚠️

### var : portée de fonction (pas de bloc)

`var` est l'ancienne façon de déclarer des variables (avant ES6). Elle a un **scope de fonction**, pas de bloc.

```javascript
function exemple() {
  var x = 10;  // Scope de fonction
  console.log(x);  // ✅ 10
}

exemple();
console.log(x);  // ❌ Erreur : x is not defined
```

### var ignore les blocs !

C'est là que ça devient problématique :

```javascript
if (true) {
  var message = "Hello";  // var ignore le bloc if !
}

console.log(message);  // ✅ "Hello" - Accessible en dehors du bloc ! 😱
```

### Exemple problématique avec for

```javascript
for (var i = 0; i < 3; i++) {
  console.log(i);
}

console.log(i);  // ✅ 3 - i existe encore en dehors de la boucle ! 😱
```

**Problème :** La variable `i` "fuit" hors de la boucle et peut causer des bugs.

### Comparaison let vs var dans une boucle

```javascript
// Avec let (moderne) ✅
for (let i = 0; i < 3; i++) {
  console.log(i);  // 0, 1, 2
}
console.log(i);  // ❌ Erreur : i is not defined (c'est bien !)

// Avec var (ancien) ⚠️
for (var j = 0; j < 3; j++) {
  console.log(j);  // 0, 1, 2
}
console.log(j);  // ✅ 3 (j existe toujours, problème potentiel !)
```

## Portée imbriquée (nested scope)

Les portées peuvent être **imbriquées** : une portée intérieure peut accéder aux variables d'une portée extérieure, mais pas l'inverse.

### Règle de base

Une fonction **interne** peut accéder aux variables de la fonction **externe** :

```javascript
function externe() {
  const x = 10;  // Portée de externe

  function interne() {
    console.log(x);  // ✅ Peut accéder à x
  }

  interne();  // Affiche : 10
}

externe();
```

### L'inverse ne fonctionne pas

```javascript
function externe() {
  function interne() {
    const y = 20;  // Portée de interne
  }

  interne();
  console.log(y);  // ❌ Erreur : y is not defined
}

externe();
```

### Plusieurs niveaux

```javascript
const global = "global";  // Niveau 1 : global

function niveau1() {
  const var1 = "niveau1";  // Niveau 2 : fonction niveau1

  function niveau2() {
    const var2 = "niveau2";  // Niveau 3 : fonction niveau2

    console.log(global);  // ✅ Accessible
    console.log(var1);    // ✅ Accessible
    console.log(var2);    // ✅ Accessible
  }

  niveau2();
  console.log(var2);  // ❌ Erreur : var2 n'est pas accessible ici
}

niveau1();
```

**Règle :** Une portée interne accède aux portées externes, mais pas l'inverse.

### Exemple pratique : compteur

```javascript
function creerCompteur() {
  let compte = 0;  // Variable privée dans la portée de creerCompteur

  return function() {
    compte++;  // La fonction interne accède à compte
    return compte;
  };
}

const compteur = creerCompteur();
console.log(compteur());  // 1
console.log(compteur());  // 2
console.log(compteur());  // 3
console.log(compte);      // ❌ Erreur : compte n'est pas accessible ici
```

## Masquage de variables (shadowing)

Quand une variable interne a le **même nom** qu'une variable externe, elle **masque** (shadow) la variable externe.

### Exemple de shadowing

```javascript
const x = "global";

function exemple() {
  const x = "local";  // Masque la variable globale x
  console.log(x);     // "local" - utilise la variable locale
}

exemple();
console.log(x);  // "global" - la variable globale n'a pas changé
```

### Shadowing avec let dans un bloc

```javascript
const nom = "Alice";

if (true) {
  const nom = "Bob";  // Masque la variable externe
  console.log(nom);   // "Bob"
}

console.log(nom);  // "Alice"
```

### Attention aux confusions

```javascript
let resultat = 10;

function calculer() {
  let resultat = 20;  // Variable différente, même nom
  resultat = resultat + 5;
  console.log(resultat);  // 25 (variable locale)
}

calculer();
console.log(resultat);  // 10 (variable globale inchangée)
```

**Bonne pratique :** Évitez de réutiliser les mêmes noms de variables pour éviter la confusion.

## Exemples pratiques complets

### Exemple 1 : Validation de formulaire

```javascript
function validerFormulaire(email, motDePasse) {
  // Variables locales à la fonction
  const emailValide = email.includes("@");

  if (emailValide) {
    const message = "Email valide";  // Scope du bloc if
    console.log(message);
  } else {
    const message = "Email invalide";  // Différente variable message
    console.log(message);
  }

  // message n'existe plus ici

  if (motDePasse.length >= 8) {
    return "Formulaire valide";
  }

  return "Mot de passe trop court";
}

console.log(validerFormulaire("test@mail.com", "12345678"));
```

### Exemple 2 : Boucles imbriquées

```javascript
function tableauMultiplication(max) {
  for (let i = 1; i <= max; i++) {
    // i est dans le scope de cette boucle

    for (let j = 1; j <= max; j++) {
      // j est dans le scope de cette boucle interne
      console.log(i + " x " + j + " = " + (i * j));
    }

    // j n'existe plus ici
  }

  // i et j n'existent plus ici
}

tableauMultiplication(3);
```

### Exemple 3 : Configuration avec portées

```javascript
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000
};

function faireFetch(endpoint) {
  // config est accessible (portée globale)
  const url = config.apiUrl + endpoint;  // Variable locale

  if (config.timeout > 0) {
    const message = "Timeout configuré";  // Scope du bloc if
    console.log(message);
  }

  console.log("Appel à:", url);
  return url;
}

faireFetch("/users");
```

### Exemple 4 : Scope dans des conditions

```javascript
function categoriserScore(score) {
  if (score >= 90) {
    const grade = "A";
    const message = "Excellent !";
    return { grade, message };
  } else if (score >= 70) {
    const grade = "B";  // Nouvelle variable grade (différente portée)
    const message = "Bien !";
    return { grade, message };
  } else {
    const grade = "C";  // Encore une autre variable grade
    const message = "Peut mieux faire";
    return { grade, message };
  }

  // Aucune des variables ci-dessus n'existe ici
}

console.log(categoriserScore(85));  // { grade: "B", message: "Bien !" }
```

### Exemple 5 : Compteurs multiples

```javascript
function creerGestionnaireCompteurs() {
  let compteur1 = 0;  // Portée de creerGestionnaireCompteurs
  let compteur2 = 0;

  return {
    incrementer1: function() {
      compteur1++;
      return compteur1;
    },
    incrementer2: function() {
      compteur2++;
      return compteur2;
    },
    obtenir: function() {
      return { compteur1, compteur2 };
    }
  };
}

const gestionnaire = creerGestionnaireCompteurs();
console.log(gestionnaire.incrementer1());  // 1
console.log(gestionnaire.incrementer1());  // 2
console.log(gestionnaire.incrementer2());  // 1
console.log(gestionnaire.obtenir());       // { compteur1: 2, compteur2: 1 }
```

## Portée dans les arrow functions

Les arrow functions se comportent exactement comme les fonctions classiques pour la portée des variables (mais différemment pour `this`, vu dans une autre section).

```javascript
const x = "global";

const exemple = () => {
  const y = "local";
  console.log(x);  // ✅ Accessible
  console.log(y);  // ✅ Accessible
};

exemple();
console.log(y);  // ❌ Erreur
```

## Variables globales : à éviter

### Pourquoi éviter les variables globales ?

1. **Pollution de l'espace global** : risque de conflits de noms
2. **Difficiles à déboguer** : peuvent être modifiées de n'importe où
3. **Couplage fort** : rendent le code moins modulaire
4. **Problèmes de maintenance** : difficile de savoir qui utilise quoi

### Mauvais exemple

```javascript
// ❌ Trop de variables globales
let utilisateur = null;
let score = 0;
let niveau = 1;
let temps = 0;

function jouer() {
  score += 10;
  temps++;
  // ...
}

function sauvegarder() {
  // ...
}
```

### Bon exemple : encapsulation

```javascript
// ✅ Encapsuler dans un objet ou une fonction
const jeu = {
  utilisateur: null,
  score: 0,
  niveau: 1,
  temps: 0,

  jouer() {
    this.score += 10;
    this.temps++;
  },

  sauvegarder() {
    // ...
  }
};
```

Ou avec une fonction :

```javascript
function creerJeu() {
  let score = 0;  // Variable privée
  let niveau = 1;

  return {
    jouer() {
      score += 10;
    },
    obtenirScore() {
      return score;
    }
  };
}

const jeu = creerJeu();
```

## Différence let/const vs var : résumé

| Aspect | let / const | var |
|--------|-------------|-----|
| **Portée** | Bloc `{ }` | Fonction |
| **Redéclaration** | ❌ Non | ✅ Oui (problématique) |
| **Hoisting** | Oui mais zone morte | Oui, initialisé à undefined |
| **Global scope** | N'attache pas à window | Attache à window (navigateur) |
| **Usage moderne** | ✅ Recommandé | ⚠️ Éviter |

### Redéclaration avec var (problématique)

```javascript
var x = 10;
var x = 20;  // ✅ Autorisé (mais confus !)
console.log(x);  // 20

let y = 10;
let y = 20;  // ❌ Erreur : Identifier 'y' has already been declared
```

### var crée des propriétés globales

```javascript
var x = 10;
console.log(window.x);  // 10 (dans un navigateur) - Pollution !

let y = 20;
console.log(window.y);  // undefined - Mieux !
```

## Bonnes pratiques

### 1. Utilisez toujours let ou const (jamais var)

```javascript
// ✅ Moderne
const MAX = 100;
let compteur = 0;

// ❌ Ancien, à éviter
var ancienneVariable = "non";
```

### 2. Préférez const par défaut

```javascript
// ✅ Utilisez const si la variable ne change pas
const nom = "Alice";
const utilisateurs = [];  // Le tableau peut être modifié, mais pas la référence

// Utilisez let seulement si nécessaire
let compteur = 0;
compteur++;
```

### 3. Déclarez les variables au plus près de leur utilisation

```javascript
// ❌ Déclaration loin de l'usage
function exemple() {
  let x, y, z;

  // 50 lignes de code...

  x = 10;
  y = 20;
  z = x + y;
}

// ✅ Déclaration proche de l'usage
function exemple() {
  // Code...

  const x = 10;
  const y = 20;
  const z = x + y;
}
```

### 4. Limitez la portée des variables

```javascript
// ❌ Variable dans une portée trop large
function traiter() {
  let resultat;

  if (condition1) {
    resultat = calcul1();
  }

  if (condition2) {
    resultat = calcul2();
  }

  return resultat;
}

// ✅ Variables dans des portées limitées
function traiter() {
  if (condition1) {
    const resultat = calcul1();
    return resultat;
  }

  if (condition2) {
    const resultat = calcul2();
    return resultat;
  }
}
```

### 5. Évitez le shadowing sauf si intentionnel

```javascript
// ❌ Shadowing confus
const nom = "Alice";

function afficher() {
  const nom = "Bob";  // Confusion possible
  console.log(nom);
}

// ✅ Noms distincts
const nomGlobal = "Alice";

function afficher() {
  const nomLocal = "Bob";
  console.log(nomLocal);
}
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier de déclarer une variable

```javascript
function exemple() {
  x = 10;  // ❌ Crée une variable globale accidentellement !
}

exemple();
console.log(x);  // 10 (variable globale par erreur)

// ✅ Correct : toujours déclarer
function exemple() {
  const x = 10;  // Variable locale
}
```

### ❌ Erreur 2 : Accéder à une variable hors de sa portée

```javascript
if (true) {
  const message = "Hello";
}

console.log(message);  // ❌ Erreur : message is not defined

// ✅ Correct : déclarer dans la bonne portée
const message = "Hello";

if (true) {
  console.log(message);  // ✅ Accessible
}
```

### ❌ Erreur 3 : Utiliser var dans des boucles

```javascript
// ❌ Problème classique avec var
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);  // Affiche : 3, 3, 3 (pas 0, 1, 2 !)
  }, 100);
}

// ✅ Correct avec let
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);  // Affiche : 0, 1, 2 ✅
  }, 100);
}
```

### ❌ Erreur 4 : Modifier une variable externe involontairement

```javascript
let total = 0;

function ajouter(valeur) {
  total = total + valeur;  // ❌ Modifie la variable globale
}

ajouter(10);
console.log(total);  // 10 (modifié !)

// ✅ Mieux : retourner une nouvelle valeur
let total = 0;

function ajouter(valeur) {
  return total + valeur;  // Ne modifie pas total
}

total = ajouter(10);  // Assignation explicite
```

## Visualisation de la portée

```javascript
// NIVEAU 1 : Portée globale
const global = "Je suis global";

function fonction1() {
  // NIVEAU 2 : Portée de fonction1
  const local1 = "Je suis dans fonction1";

  if (true) {
    // NIVEAU 3 : Portée du bloc if
    const bloc1 = "Je suis dans le bloc if";

    console.log(global);  // ✅ Accessible (niveau 1)
    console.log(local1);  // ✅ Accessible (niveau 2)
    console.log(bloc1);   // ✅ Accessible (niveau 3)
  }

  console.log(global);  // ✅ Accessible
  console.log(local1);  // ✅ Accessible
  console.log(bloc1);   // ❌ Erreur : hors de portée
}

function fonction2() {
  // NIVEAU 2 : Portée de fonction2 (différente de fonction1)
  console.log(global);  // ✅ Accessible
  console.log(local1);  // ❌ Erreur : dans une autre fonction
}

console.log(global);  // ✅ Accessible
console.log(local1);  // ❌ Erreur : dans une fonction
```

## Points clés à retenir

1. **Trois types de portée** : globale, fonction, bloc

2. **let/const** : portée de bloc `{ }` (moderne, recommandé)

3. **var** : portée de fonction (ancien, éviter)

4. **Règle d'accès** : de l'intérieur vers l'extérieur (jamais l'inverse)

5. **Shadowing** : variable interne masque l'externe du même nom

6. **Variables globales** : à minimiser autant que possible

7. **const par défaut** : utilisez const, let si nécessaire, jamais var

8. **Portée limitée** : déclarez les variables dans la portée la plus petite possible

## Prochaines étapes

Maintenant que vous comprenez la portée, vous êtes prêt pour :

- Le **hoisting** (5.6.9) - comment JavaScript "remonte" les déclarations
- Les **closures** (5.13.1) - fonctions qui "capturent" leur environnement
- Les **callbacks** (5.6.10) - fonctions passées en argument

Comprendre la portée est fondamental pour éviter les bugs et écrire du code propre. C'est un concept qui reviendra constamment dans votre apprentissage de JavaScript !

---

**Note :** La portée est l'un des concepts les plus importants en JavaScript. Les différences entre `var`, `let`, et `const` sont cruciales à comprendre. En JavaScript moderne, utilisez toujours `let` ou `const` (préférez `const` par défaut), et n'utilisez jamais `var`. Cela vous évitera de nombreux bugs liés à la portée.

⏭️ [Hoisting : différences entre var, let, const et fonctions](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/09-hoisting.md)
