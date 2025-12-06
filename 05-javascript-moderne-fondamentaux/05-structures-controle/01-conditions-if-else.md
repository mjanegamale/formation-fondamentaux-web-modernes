🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.1 - Conditions : if, else if, else

## Introduction

Les structures conditionnelles permettent à votre programme de prendre des décisions et d'exécuter différents blocs de code selon que certaines conditions sont vraies ou fausses. C'est un concept fondamental en programmation qui rend votre code dynamique et intelligent.

Imaginez un feu de circulation : si le feu est vert, on avance ; si le feu est orange, on ralentit ; si le feu est rouge, on s'arrête. C'est exactement ce que font les conditions en JavaScript !

---

## La structure `if` (si)

La structure la plus simple est le `if`, qui signifie "si" en français. Elle permet d'exécuter un bloc de code uniquement si une condition est vraie.

### Syntaxe de base

```javascript
if (condition) {
  // Code exécuté si la condition est vraie
}
```

### Exemple simple

```javascript
const age = 20;

if (age >= 18) {
  console.log("Vous êtes majeur");
}
// Affiche : "Vous êtes majeur"
```

**Explication :**
- La condition `age >= 18` est évaluée
- Elle retourne `true` (car 20 est supérieur ou égal à 18)
- Le code entre les accolades `{}` est donc exécuté

### Points importants

1. **Les parenthèses** autour de la condition sont obligatoires
2. **Les accolades** `{}` délimitent le bloc de code à exécuter
3. La condition doit retourner une valeur **booléenne** (`true` ou `false`)

### Exemples variés

```javascript
const temperature = 25;

if (temperature > 30) {
  console.log("Il fait chaud !");
}

const estConnecte = true;

if (estConnecte) {
  console.log("Bienvenue sur votre compte");
}

const nom = "Alice";

if (nom === "Alice") {
  console.log("Bonjour Alice !");
}
```

---

## La structure `if...else` (si...sinon)

Souvent, on veut exécuter un code si la condition est vraie, et un autre code si elle est fausse. C'est là qu'intervient `else` (sinon).

### Syntaxe

```javascript
if (condition) {
  // Code exécuté si la condition est vraie
} else {
  // Code exécuté si la condition est fausse
}
```

### Exemple

```javascript
const age = 15;

if (age >= 18) {
  console.log("Vous êtes majeur");
} else {
  console.log("Vous êtes mineur");
}
// Affiche : "Vous êtes mineur"
```

**Explication :**
- La condition `age >= 18` est évaluée
- Elle retourne `false` (car 15 est inférieur à 18)
- Le code dans le bloc `else` est donc exécuté

### Exemple avec une interaction utilisateur

```javascript
const motDePasse = "secret123";

if (motDePasse === "secret123") {
  console.log("✅ Accès autorisé");
} else {
  console.log("❌ Mot de passe incorrect");
}
```

---

## La structure `if...else if...else` (si...sinon si...sinon)

Lorsqu'on a plus de deux possibilités, on utilise `else if` pour tester plusieurs conditions successives.

### Syntaxe

```javascript
if (condition1) {
  // Code exécuté si condition1 est vraie
} else if (condition2) {
  // Code exécuté si condition1 est fausse ET condition2 est vraie
} else if (condition3) {
  // Code exécuté si condition1 et condition2 sont fausses ET condition3 est vraie
} else {
  // Code exécuté si toutes les conditions précédentes sont fausses
}
```

### Exemple : système de notes

```javascript
const note = 14;

if (note >= 16) {
  console.log("Excellent ! 🌟");
} else if (note >= 14) {
  console.log("Très bien ! 👍");
} else if (note >= 12) {
  console.log("Bien");
} else if (note >= 10) {
  console.log("Passable");
} else {
  console.log("Insuffisant");
}
// Affiche : "Très bien ! 👍"
```

**Comment ça fonctionne :**
1. JavaScript teste `note >= 16` → faux (14 < 16)
2. Ensuite, il teste `note >= 14` → vrai ! (14 >= 14)
3. Le code correspondant est exécuté
4. Les autres conditions ne sont **pas testées**

### Exemple : météo

```javascript
const temperature = 18;

if (temperature >= 30) {
  console.log("☀️ Il fait très chaud, hydratez-vous !");
} else if (temperature >= 20) {
  console.log("🌤️ Temps agréable");
} else if (temperature >= 10) {
  console.log("🌥️ Un peu frais, prenez une veste");
} else {
  console.log("🥶 Il fait froid !");
}
// Affiche : "🌥️ Un peu frais, prenez une veste"
```

---

## Ordre d'évaluation

⚠️ **Important :** L'ordre des conditions est crucial !

### Exemple incorrect

```javascript
const age = 25;

if (age >= 0) {
  console.log("Vous avez un âge valide");
} else if (age >= 18) {
  console.log("Vous êtes majeur");  // Cette ligne ne sera JAMAIS exécutée
}
// Affiche : "Vous avez un âge valide"
```

**Problème :** La première condition `age >= 0` est toujours vraie pour les âges positifs, donc la seconde condition n'est jamais testée.

### Exemple correct

```javascript
const age = 25;

if (age >= 18) {
  console.log("Vous êtes majeur");
} else if (age >= 0) {
  console.log("Vous êtes mineur");
}
// Affiche : "Vous êtes majeur"
```

**Règle :** Placez toujours les conditions les plus **spécifiques** en premier, et les plus **générales** en dernier.

---

## Conditions complexes

Vous pouvez combiner plusieurs conditions avec les opérateurs logiques :

### Opérateur AND (&&) - ET

Les **deux** conditions doivent être vraies.

```javascript
const age = 20;
const aPermis = true;

if (age >= 18 && aPermis) {
  console.log("Vous pouvez conduire");
} else {
  console.log("Vous ne pouvez pas conduire");
}
// Affiche : "Vous pouvez conduire"
```

### Opérateur OR (||) - OU

Au moins **une** des conditions doit être vraie.

```javascript
const jour = "samedi";

if (jour === "samedi" || jour === "dimanche") {
  console.log("C'est le week-end ! 🎉");
} else {
  console.log("C'est un jour de semaine");
}
// Affiche : "C'est le week-end ! 🎉"
```

### Opérateur NOT (!) - NON

Inverse une condition.

```javascript
const estConnecte = false;

if (!estConnecte) {
  console.log("Veuillez vous connecter");
}
// Affiche : "Veuillez vous connecter"
```

### Conditions combinées complexes

```javascript
const age = 25;
const estEtudiant = true;
const aCarteReduction = false;

if ((age < 26 && estEtudiant) || aCarteReduction) {
  console.log("Vous bénéficiez d'une réduction");
} else {
  console.log("Tarif plein");
}
// Affiche : "Vous bénéficiez d'une réduction"
```

---

## Le bloc `else` est optionnel

Vous n'êtes pas obligé d'ajouter un `else` si vous n'en avez pas besoin.

```javascript
const stock = 5;

if (stock === 0) {
  console.log("⚠️ Produit en rupture de stock");
}
// Si stock n'est pas 0, rien ne se passe
```

---

## Conditions imbriquées

On peut placer des conditions à l'intérieur d'autres conditions (mais attention à la lisibilité !).

```javascript
const age = 25;
const pays = "France";

if (age >= 18) {
  console.log("Vous êtes majeur");

  if (pays === "France") {
    console.log("Vous pouvez voter en France");
  } else {
    console.log("Vous êtes majeur mais pas en France");
  }
} else {
  console.log("Vous êtes mineur");
}
```

**Conseil :** Si vos conditions deviennent trop imbriquées, envisagez de refactoriser votre code pour le rendre plus lisible.

---

## Valeurs truthy et falsy

JavaScript évalue certaines valeurs comme "vraies" ou "fausses" dans un contexte booléen.

### Valeurs **falsy** (considérées comme fausses)

```javascript
if (false) { }        // false
if (0) { }            // 0
if ("") { }           // chaîne vide
if (null) { }         // null
if (undefined) { }    // undefined
if (NaN) { }          // Not a Number
```

### Valeurs **truthy** (considérées comme vraies)

Toutes les autres valeurs sont truthy :

```javascript
if (true) { }         // true
if (42) { }           // tout nombre sauf 0
if ("hello") { }      // toute chaîne non vide
if ([]) { }           // tableau (même vide)
if ({}) { }           // objet (même vide)
```

### Exemple pratique

```javascript
const nom = "Alice";

// Vérifie si la variable contient une valeur
if (nom) {
  console.log(`Bonjour ${nom}`);
} else {
  console.log("Nom non défini");
}
// Affiche : "Bonjour Alice"
```

---

## Bonnes pratiques

### ✅ Utilisez des accolades même pour une seule ligne

```javascript
// ❌ Évitez (moins lisible, risque d'erreurs)
if (age >= 18)
  console.log("Majeur");

// ✅ Préférez
if (age >= 18) {
  console.log("Majeur");
}
```

### ✅ Utilisez des comparaisons strictes (===)

```javascript
// ❌ Évitez
if (age == 18) { }

// ✅ Préférez
if (age === 18) { }
```

### ✅ Nommez vos conditions pour plus de clarté

```javascript
const age = 20;
const aPermis = true;

// ✅ Lisible
const peutConduire = age >= 18 && aPermis;
if (peutConduire) {
  console.log("Vous pouvez conduire");
}
```

### ✅ Évitez les conditions trop complexes

```javascript
// ❌ Difficile à lire
if ((age >= 18 && pays === "France" && aPermis) || (age >= 16 && formation && supervision)) {
  // ...
}

// ✅ Plus clair
const estMajeurEnFrance = age >= 18 && pays === "France" && aPermis;
const estMineurAvecFormation = age >= 16 && formation && supervision;

if (estMajeurEnFrance || estMineurAvecFormation) {
  // ...
}
```

---

## Comparaison avec l'opérateur ternaire

Pour des conditions simples, vous pouvez aussi utiliser l'opérateur ternaire (nous le verrons en détail plus tard) :

```javascript
// Avec if...else
let message;
if (age >= 18) {
  message = "Majeur";
} else {
  message = "Mineur";
}

// Avec opérateur ternaire (même résultat)
const message = age >= 18 ? "Majeur" : "Mineur";
```

---

## Exemples récapitulatifs

### Exemple 1 : Connexion utilisateur

```javascript
const username = "alice";
const password = "secret123";

if (username === "" || password === "") {
  console.log("❌ Veuillez remplir tous les champs");
} else if (username === "alice" && password === "secret123") {
  console.log("✅ Connexion réussie");
} else {
  console.log("❌ Identifiants incorrects");
}
```

### Exemple 2 : Calcul de réduction

```javascript
const montant = 150;
let remise = 0;

if (montant >= 200) {
  remise = 0.20; // 20% de réduction
} else if (montant >= 100) {
  remise = 0.10; // 10% de réduction
} else if (montant >= 50) {
  remise = 0.05; // 5% de réduction
}

const prixFinal = montant * (1 - remise);
console.log(`Prix final : ${prixFinal}€`);
// Affiche : "Prix final : 135€"
```

### Exemple 3 : Validation de formulaire

```javascript
const email = "alice@example.com";
const age = 25;
const accepteConditions = true;

if (email === "") {
  console.log("❌ Email requis");
} else if (!email.includes("@")) {
  console.log("❌ Email invalide");
} else if (age < 18) {
  console.log("❌ Vous devez avoir au moins 18 ans");
} else if (!accepteConditions) {
  console.log("❌ Vous devez accepter les conditions");
} else {
  console.log("✅ Formulaire valide");
}
```

---

## Résumé

- **`if`** : exécute du code si une condition est vraie
- **`else`** : exécute du code si la condition précédente est fausse
- **`else if`** : teste une nouvelle condition si les précédentes sont fausses
- L'ordre des conditions est important : du plus spécifique au plus général
- Utilisez `&&` (ET), `||` (OU) et `!` (NON) pour combiner des conditions
- Privilégiez la lisibilité : accolades, comparaisons strictes (===), noms de variables clairs

Les conditions sont essentielles en JavaScript et vous les utiliserez constamment. Prenez le temps de bien comprendre leur fonctionnement, cela vous servira tout au long de votre parcours de développeur ! 🚀

⏭️ [Switch et case](/05-javascript-moderne-fondamentaux/05-structures-controle/02-switch-case.md)
