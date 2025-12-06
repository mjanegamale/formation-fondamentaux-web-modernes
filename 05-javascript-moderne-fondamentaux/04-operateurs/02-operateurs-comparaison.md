🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4.2 - Opérateurs de comparaison (=== vs ==)

## Introduction

Les **opérateurs de comparaison** permettent de comparer deux valeurs et retournent toujours un résultat **booléen** : `true` (vrai) ou `false` (faux).

Ces opérateurs sont essentiels pour :
- Prendre des décisions avec `if`
- Créer des boucles conditionnelles
- Filtrer des données
- Valider des entrées utilisateur

JavaScript offre plusieurs opérateurs de comparaison, mais **un point crucial** : la différence entre `==` et `===` est source de nombreux bugs pour les débutants !

---

## Vue d'ensemble des opérateurs

| Opérateur | Nom | Description | Recommandation |
|-----------|-----|-------------|----------------|
| `===` | Égalité stricte | Valeur ET type identiques | ✅ **À UTILISER** |
| `!==` | Inégalité stricte | Valeur OU type différents | ✅ **À UTILISER** |
| `==` | Égalité faible | Valeur égale (avec conversion) | ⚠️ **À ÉVITER** |
| `!=` | Inégalité faible | Valeur différente (avec conversion) | ⚠️ **À ÉVITER** |
| `>` | Supérieur à | Plus grand que | ✅ OK |
| `<` | Inférieur à | Plus petit que | ✅ OK |
| `>=` | Supérieur ou égal | Plus grand ou égal | ✅ OK |
| `<=` | Inférieur ou égal | Plus petit ou égal | ✅ OK |

---

## === (Égalité stricte) - L'opérateur recommandé ✅

L'opérateur `===` vérifie que deux valeurs sont identiques **en valeur ET en type**.

### Syntaxe

```javascript
valeur1 === valeur2
```

### Retourne

- `true` si les valeurs ET les types sont identiques
- `false` sinon

### Exemples de base

```javascript
// Comparaison de nombres
console.log(5 === 5);        // true
console.log(10 === 5);       // false

// Comparaison de strings
console.log("hello" === "hello");  // true
console.log("Hello" === "hello");  // false (casse différente)

// Comparaison de booléens
console.log(true === true);   // true
console.log(true === false);  // false
```

### Vérification du type

**Point crucial** : `===` vérifie également le **type** :

```javascript
console.log(5 === 5);        // true (même valeur, même type)
console.log(5 === "5");      // false (même valeur, types différents)
console.log(0 === false);    // false (types différents)
console.log("" === false);   // false (types différents)
console.log(null === undefined); // false (types différents)
```

### Pourquoi utiliser === ?

#### ✅ Avantage 1 : Comportement prévisible

```javascript
const age = 18;
const input = "18";

// ✅ Avec === (clair et sans surprise)
if (age === input) {
    console.log("Égaux");
} else {
    console.log("Différents"); // Ce bloc s'exécute
}
```

#### ✅ Avantage 2 : Évite les bugs subtils

```javascript
const userInput = "0";

// ❌ Avec == (comportement surprenant)
if (userInput == false) {
    console.log("C'est égal !"); // S'exécute (wtf?)
}

// ✅ Avec === (comportement logique)
if (userInput === false) {
    console.log("C'est égal !"); // Ne s'exécute PAS
}
```

#### ✅ Avantage 3 : Code plus maintenable

Les autres développeurs comprennent immédiatement votre intention.

### Cas d'usage pratiques

#### Validation de formulaire

```javascript
const motDePasse = "secret123";
const confirmation = "secret123";

if (motDePasse === confirmation) {
    console.log("✅ Les mots de passe correspondent");
} else {
    console.log("❌ Les mots de passe ne correspondent pas");
}
```

#### Vérification de rôle utilisateur

```javascript
const roleUtilisateur = "admin";

if (roleUtilisateur === "admin") {
    console.log("Accès autorisé à l'administration");
}
```

#### Comparaison de choix

```javascript
const choixUtilisateur = "oui";

if (choixUtilisateur === "oui") {
    console.log("L'utilisateur a accepté");
} else if (choixUtilisateur === "non") {
    console.log("L'utilisateur a refusé");
}
```

---

## == (Égalité faible) - À éviter ⚠️

L'opérateur `==` compare les valeurs **après conversion de type** (coercition). C'est source de confusion et de bugs !

### Syntaxe

```javascript
valeur1 == valeur2
```

### Le problème avec ==

JavaScript **convertit automatiquement** les types avant de comparer :

```javascript
// Conversions surprenantes
console.log(5 == "5");       // true (string converti en nombre)
console.log(0 == false);     // true (false converti en 0)
console.log("" == false);    // true (string vide converti en 0)
console.log(null == undefined); // true (considérés équivalents)
console.log(" \t\n" == 0);   // true (wtf?)
```

### Exemples qui démontrent le problème

#### Exemple 1 : Validation trompeuse

```javascript
const inputAge = "18";
const ageMinimum = 18;

// ❌ Avec == (semble fonctionner mais c'est trompeur)
if (inputAge == ageMinimum) {
    console.log("Âge valide"); // S'exécute grâce à la conversion
}

// ✅ Avec === (force à être explicite)
if (Number(inputAge) === ageMinimum) {
    console.log("Âge valide"); // Conversion explicite, intention claire
}
```

#### Exemple 2 : Validation de checkbox

```javascript
const isChecked = "false"; // Valeur venant d'un formulaire

// ❌ DANGER avec ==
if (isChecked == false) {
    console.log("Pas coché"); // Ne s'exécute PAS ! "false" != false
}

// ✅ Correct avec ===
if (isChecked === "false") {
    console.log("Pas coché"); // S'exécute correctement
}
```

#### Exemple 3 : Tableau des surprises

```javascript
// Comportements contre-intuitifs de ==
console.log([] == false);      // true (!)
console.log([] == 0);          // true (!)
console.log("0" == false);     // true (!)
console.log(null == 0);        // false (!)
console.log(null == undefined); // true (!)
```

**Pourquoi ces résultats ?** À cause de règles de conversion complexes que même les développeurs expérimentés ont du mal à retenir !

### Pourquoi == existe-t-il encore ?

C'est un **héritage historique** de JavaScript. Dans les années 90, cela semblait pratique, mais l'expérience a montré que c'est source d'erreurs.

**Recommandation moderne** : N'utilisez **JAMAIS** `==` dans du nouveau code. Utilisez toujours `===`.

---

## !== (Inégalité stricte) - Recommandé ✅

L'opérateur `!==` vérifie que deux valeurs sont **différentes** en valeur OU en type.

### Syntaxe

```javascript
valeur1 !== valeur2
```

### Retourne

- `true` si les valeurs OU les types sont différents
- `false` si identiques en valeur ET type

### Exemples de base

```javascript
console.log(5 !== 3);        // true (valeurs différentes)
console.log(5 !== 5);        // false (identiques)
console.log(5 !== "5");      // true (types différents)
console.log("hello" !== "Hello"); // true (casse différente)
```

### Cas d'usage pratiques

#### Validation de saisie

```javascript
const nom = "";

if (nom !== "") {
    console.log(`Bonjour ${nom}`);
} else {
    console.log("Veuillez entrer votre nom");
}
```

#### Vérification d'erreur

```javascript
const resultat = faireQuelqueChose();

if (resultat !== null) {
    console.log("Opération réussie");
} else {
    console.log("Erreur détectée");
}
```

#### Filtrage de données

```javascript
const utilisateurs = [
    { nom: "Alice", role: "admin" },
    { nom: "Bob", role: "user" },
    { nom: "Charlie", role: "admin" }
];

const nonAdmins = utilisateurs.filter(u => u.role !== "admin");
console.log(nonAdmins); // [{ nom: "Bob", role: "user" }]
```

---

## != (Inégalité faible) - À éviter ⚠️

Comme `==`, l'opérateur `!=` effectue une conversion de type. Même problèmes, même recommandation : **ne l'utilisez pas**.

```javascript
// Comportements surprenants
console.log(5 != "5");       // false (convertis en même valeur)
console.log(0 != false);     // false
console.log("" != false);    // false

// ✅ Utilisez !== à la place
console.log(5 !== "5");      // true
console.log(0 !== false);    // true
console.log("" !== false);   // true
```

---

## Comparaison : === vs ==

### Tableau comparatif détaillé

| Comparaison | `==` (faible) | `===` (strict) |
|-------------|---------------|----------------|
| `5 == 5` | `true` | `true` |
| `5 == "5"` | `true` ⚠️ | `false` ✅ |
| `0 == false` | `true` ⚠️ | `false` ✅ |
| `"" == false` | `true` ⚠️ | `false` ✅ |
| `null == undefined` | `true` ⚠️ | `false` ✅ |
| `[] == false` | `true` ⚠️ | `false` ✅ |
| `"0" == false` | `true` ⚠️ | `false` ✅ |

### Quiz : Devinez le résultat

Testez votre compréhension :

```javascript
// Avec ==
console.log("1" == 1);           // true (conversion)
console.log(true == 1);          // true (true → 1)
console.log(false == 0);         // true (false → 0)
console.log(" " == 0);           // true (espace → 0)

// Avec ===
console.log("1" === 1);          // false (types différents)
console.log(true === 1);         // false (types différents)
console.log(false === 0);        // false (types différents)
console.log(" " === 0);          // false (types différents)
```

---

## > (Supérieur à)

Vérifie si la valeur de gauche est **strictement supérieure** à celle de droite.

### Syntaxe

```javascript
valeur1 > valeur2
```

### Exemples avec nombres

```javascript
console.log(10 > 5);     // true
console.log(5 > 10);     // false
console.log(5 > 5);      // false (pas strictement supérieur)
console.log(-5 > -10);   // true
console.log(3.5 > 3);    // true
```

### Comparaison de strings

Les strings sont comparées **alphabétiquement** (ordre lexicographique) :

```javascript
console.log("b" > "a");     // true
console.log("z" > "a");     // true
console.log("abc" > "aba"); // true

// Attention à la casse !
console.log("A" > "a");     // false (majuscule < minuscule en Unicode)
console.log("B" > "a");     // false
```

### Cas d'usage pratiques

#### Validation d'âge

```javascript
const age = 25;
const ageMinimum = 18;

if (age > ageMinimum) {
    console.log("Accès autorisé");
}
```

#### Vérification de stock

```javascript
const stock = 15;
const seuilAlerte = 10;

if (stock > seuilAlerte) {
    console.log("Stock suffisant");
} else {
    console.log("⚠️ Stock faible, réapprovisionner");
}
```

#### Comparaison de scores

```javascript
const scoreJoueur1 = 450;
const scoreJoueur2 = 380;

if (scoreJoueur1 > scoreJoueur2) {
    console.log("Joueur 1 gagne !");
}
```

---

## < (Inférieur à)

Vérifie si la valeur de gauche est **strictement inférieure** à celle de droite.

### Syntaxe

```javascript
valeur1 < valeur2
```

### Exemples

```javascript
console.log(5 < 10);     // true
console.log(10 < 5);     // false
console.log(5 < 5);      // false (pas strictement inférieur)
console.log(-10 < -5);   // true
```

### Cas d'usage pratiques

#### Limitation de caractères

```javascript
const message = "Bonjour";
const maxLength = 100;

if (message.length < maxLength) {
    console.log("Message valide");
}
```

#### Vérification de température

```javascript
const temperature = 15;
const seuilFroid = 18;

if (temperature < seuilFroid) {
    console.log("🥶 Il fait froid, mettez un pull");
}
```

---

## >= (Supérieur ou égal)

Vérifie si la valeur de gauche est **supérieure ou égale** à celle de droite.

### Syntaxe

```javascript
valeur1 >= valeur2
```

### Exemples

```javascript
console.log(10 >= 5);    // true
console.log(5 >= 5);     // true (égal compte)
console.log(3 >= 5);     // false
```

### Cas d'usage pratiques

#### Validation d'âge minimum

```javascript
const age = 18;
const ageMinimum = 18;

if (age >= ageMinimum) {
    console.log("✅ Vous pouvez vous inscrire");
} else {
    console.log("❌ Vous devez avoir au moins 18 ans");
}
```

#### Vérification de note

```javascript
const note = 12;
const notePassage = 10;

if (note >= notePassage) {
    console.log("✅ Examen réussi");
} else {
    console.log("❌ Examen échoué");
}
```

#### Système de réduction

```javascript
const montantAchat = 50;
const seuilReduction = 50;

if (montantAchat >= seuilReduction) {
    console.log("🎉 Vous bénéficiez de 10% de réduction !");
}
```

---

## <= (Inférieur ou égal)

Vérifie si la valeur de gauche est **inférieure ou égale** à celle de droite.

### Syntaxe

```javascript
valeur1 <= valeur2
```

### Exemples

```javascript
console.log(5 <= 10);    // true
console.log(5 <= 5);     // true (égal compte)
console.log(10 <= 5);    // false
```

### Cas d'usage pratiques

#### Limitation de prix

```javascript
const prix = 25;
const budgetMax = 30;

if (prix <= budgetMax) {
    console.log("✅ Dans le budget");
}
```

#### Validation de longueur

```javascript
const username = "alice";
const maxLength = 20;

if (username.length <= maxLength) {
    console.log("✅ Nom d'utilisateur valide");
}
```

---

## Comparaison de différents types

### Nombres vs Strings

Avec les opérateurs `>`, `<`, `>=`, `<=`, JavaScript **convertit** les strings en nombres :

```javascript
console.log("10" > 5);       // true (string converti en nombre)
console.log("10" < 20);      // true
console.log("abc" > 5);      // false (NaN)
```

**Bonne pratique** : Convertissez explicitement pour éviter les surprises :

```javascript
const input = "25";

// ✅ Conversion explicite
if (Number(input) > 18) {
    console.log("Valide");
}
```

### Null et Undefined

```javascript
// null
console.log(null === null);        // true
console.log(null === undefined);   // false
console.log(null == undefined);    // true (piège !)

// undefined
console.log(undefined === undefined); // true
console.log(undefined > 0);        // false
console.log(undefined < 0);        // false
```

**Conseil** : Toujours vérifier explicitement :

```javascript
// ✅ Vérification explicite
if (valeur !== null && valeur !== undefined) {
    // valeur existe
}

// Ou plus court
if (valeur != null) { // Seul cas où == est utile !
    // null et undefined sont exclus
}
```

---

## Comparaison de strings

### Ordre alphabétique

Les strings sont comparées caractère par caractère selon leur code Unicode :

```javascript
console.log("a" < "b");         // true
console.log("abc" < "abd");     // true
console.log("JavaScript" < "Java"); // false
```

### Sensibilité à la casse

Les majuscules ont des codes plus petits que les minuscules :

```javascript
console.log("A" < "a");         // true
console.log("Z" < "a");         // true (toutes majuscules < minuscules)
```

### Comparaison insensible à la casse

```javascript
const str1 = "JavaScript";
const str2 = "javascript";

// ❌ Sensible à la casse
console.log(str1 === str2);     // false

// ✅ Insensible à la casse
console.log(str1.toLowerCase() === str2.toLowerCase()); // true
```

### Ordre naturel vs alphabétique

```javascript
// Attention avec les nombres en strings !
console.log("10" < "2");        // true (!)
// Explication : "1" < "2" en ordre alphabétique

// Solution : convertir en nombres
console.log(Number("10") < Number("2")); // false
```

---

## Chaîner les comparaisons

En JavaScript, vous **ne pouvez pas** chaîner les comparaisons comme en mathématiques :

```javascript
const age = 25;

// ❌ NE FONCTIONNE PAS comme attendu
if (18 < age < 30) {
    // Évalué comme : (18 < age) < 30
    // (18 < 25) < 30
    // true < 30
    // 1 < 30 → true (toujours vrai !)
}

// ✅ Utilisez des opérateurs logiques
if (age > 18 && age < 30) {
    console.log("Âge entre 18 et 30");
}
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Utiliser == au lieu de ===

```javascript
const userInput = "0";

// ❌ Comportement inattendu
if (userInput == 0) {
    console.log("Zéro détecté"); // S'exécute (conversion)
}

// ✅ Comportement prévisible
if (userInput === "0") {
    console.log("String '0' détectée");
}
```

### ❌ Erreur 2 : Confondre = et ===

```javascript
const age = 18;

// ❌ ERREUR : affectation au lieu de comparaison
if (age = 25) {  // age devient 25, condition toujours true
    console.log("Ceci s'exécute toujours");
}

// ✅ Comparaison correcte
if (age === 25) {
    console.log("L'âge est 25");
}
```

**Note** : Certains linters détectent cette erreur automatiquement.

### ❌ Erreur 3 : Comparer des objets ou tableaux

```javascript
const arr1 = [1, 2, 3];
const arr2 = [1, 2, 3];

// ❌ Compare les références, pas le contenu
console.log(arr1 === arr2);  // false (!)

const obj1 = { a: 1 };
const obj2 = { a: 1 };
console.log(obj1 === obj2);  // false (!)

// ✅ Pour comparer le contenu, convertir en JSON
console.log(JSON.stringify(arr1) === JSON.stringify(arr2)); // true
```

### ❌ Erreur 4 : Oublier la sensibilité à la casse

```javascript
const input = "Admin";

// ❌ Ne trouve pas
if (input === "admin") {
    console.log("Admin détecté"); // Ne s'exécute pas
}

// ✅ Normaliser d'abord
if (input.toLowerCase() === "admin") {
    console.log("Admin détecté"); // S'exécute
}
```

---

## Bonnes pratiques

### ✅ Toujours utiliser === et !==

```javascript
// ✅ À FAIRE
if (valeur === 5) { }
if (valeur !== null) { }

// ❌ À ÉVITER
if (valeur == 5) { }
if (valeur != null) { } // Exception : acceptable pour vérifier null ET undefined
```

### ✅ Convertir explicitement les types

```javascript
const input = "25";

// ❌ Conversion implicite
if (input > 18) { }

// ✅ Conversion explicite
if (Number(input) > 18) { }
```

### ✅ Normaliser avant de comparer des strings

```javascript
const userInput = "  JavaScript  ";
const expected = "javascript";

// ✅ Nettoyer et normaliser
if (userInput.trim().toLowerCase() === expected) {
    console.log("Correspondance trouvée");
}
```

### ✅ Utiliser des variables pour la lisibilité

```javascript
// ❌ Difficile à lire
if (user.age >= 18 && user.age <= 65 && user.country === "FR") { }

// ✅ Plus clair
const estAdulte = user.age >= 18 && user.age <= 65;
const estFrancais = user.country === "FR";

if (estAdulte && estFrancais) { }
```

---

## Cas pratiques complets

### 1. Validation de formulaire d'inscription

```javascript
function validerInscription(username, email, age, password, confirmation) {
    // Vérification du nom d'utilisateur
    if (username.length < 3) {
        return "Le nom d'utilisateur doit contenir au moins 3 caractères";
    }

    // Vérification de l'email
    if (!email.includes("@")) {
        return "Email invalide";
    }

    // Vérification de l'âge
    if (age < 18) {
        return "Vous devez avoir au moins 18 ans";
    }

    // Vérification du mot de passe
    if (password.length < 8) {
        return "Le mot de passe doit contenir au moins 8 caractères";
    }

    // Vérification de la confirmation
    if (password !== confirmation) {
        return "Les mots de passe ne correspondent pas";
    }

    return "✅ Inscription valide";
}

console.log(validerInscription("alice", "alice@example.com", 25, "secret123", "secret123"));
// ✅ Inscription valide
```

### 2. Système de tarification

```javascript
function calculerTarif(age, estEtudiant, nombreBillets) {
    const prixBase = 15;
    let prixUnitaire = prixBase;

    // Réductions selon l'âge
    if (age < 12) {
        prixUnitaire = prixBase * 0.5; // -50%
    } else if (age >= 65) {
        prixUnitaire = prixBase * 0.7; // -30%
    }

    // Réduction étudiant
    if (estEtudiant && age >= 18 && age <= 25) {
        prixUnitaire = prixUnitaire * 0.8; // -20%
    }

    // Réduction groupe
    let total = prixUnitaire * nombreBillets;
    if (nombreBillets >= 5) {
        total = total * 0.9; // -10%
    }

    return total.toFixed(2);
}

console.log(calculerTarif(20, true, 6));
// Calcul : 15 * 0.8 (étudiant) * 6 billets * 0.9 (groupe) = 64.80
```

### 3. Authentification simple

```javascript
function authentifier(usernameInput, passwordInput) {
    // Base de données simulée
    const utilisateurs = [
        { username: "alice", password: "pass123", role: "admin" },
        { username: "bob", password: "secret", role: "user" }
    ];

    // Recherche de l'utilisateur
    const user = utilisateurs.find(u =>
        u.username.toLowerCase() === usernameInput.toLowerCase()
    );

    // Vérifications
    if (!user) {
        return "❌ Utilisateur inconnu";
    }

    if (user.password !== passwordInput) {
        return "❌ Mot de passe incorrect";
    }

    return `✅ Bienvenue ${user.username} (${user.role})`;
}

console.log(authentifier("Alice", "pass123"));
// ✅ Bienvenue alice (admin)
```

---

## Points clés à retenir

✅ **Utilisez TOUJOURS `===` et `!==`** (égalité stricte)

❌ **N'utilisez JAMAIS `==` et `!=`** (égalité faible) sauf cas très spécifique

✅ **`===` vérifie la valeur ET le type**

✅ **`>`, `<`, `>=`, `<=`** pour comparer des nombres

✅ **Convertissez explicitement** les types avant de comparer

✅ **Normalisez les strings** (trim, toLowerCase) avant comparaison

⚠️ **Ne confondez pas `=` (affectation) et `===` (comparaison)**

⚠️ **Les objets et tableaux** se comparent par référence, pas par contenu

⚠️ **Les strings sont sensibles à la casse** par défaut

---

## Tableau récapitulatif

| Opération | ❌ À éviter | ✅ Recommandé |
|-----------|-------------|---------------|
| Égalité | `valeur == 5` | `valeur === 5` |
| Inégalité | `valeur != 5` | `valeur !== 5` |
| Avec conversion | `"5" == 5` → true | `Number("5") === 5` → true |
| String vs nombre | `age == "18"` | `age === 18` |
| Null/undefined | `val == null` (OK) | `val === null \|\| val === undefined` |

---

## Dans la prochaine section

Dans la section **5.4.3 - Opérateurs logiques**, nous découvrirons comment combiner plusieurs conditions avec `&&` (ET), `||` (OU) et `!` (NON) pour créer des tests plus complexes.

---


⏭️ [Opérateurs logiques](/05-javascript-moderne-fondamentaux/04-operateurs/03-operateurs-logiques.md)
