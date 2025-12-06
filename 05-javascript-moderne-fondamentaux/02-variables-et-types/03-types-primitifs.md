🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.2.3 - Types primitifs : string, number, boolean

## Introduction

Maintenant que vous savez déclarer des variables avec `const` et `let`, une question se pose : **quel type de valeur** pouvez-vous stocker dans ces variables ?

JavaScript est un langage **dynamiquement typé**, ce qui signifie que vous n'avez pas besoin de spécifier le type de données lors de la déclaration. JavaScript le devine automatiquement !

Dans cette section, nous allons découvrir les **trois types primitifs fondamentaux** :
- 📝 **String** (chaîne de caractères) : pour le texte
- 🔢 **Number** (nombre) : pour les valeurs numériques
- ✅ **Boolean** (booléen) : pour vrai ou faux

> 💡 **Note** : Il existe d'autres types primitifs (undefined, null, Symbol, BigInt) que nous verrons dans la section suivante. Concentrons-nous d'abord sur ces trois types essentiels.

## Qu'est-ce qu'un type de données ?

### Analogie avec la vie réelle

Imaginez que vous rangez des objets dans des boîtes :
- 📦 Une boîte pour les livres (texte)
- 📦 Une boîte pour les chiffres (comptes, mesures)
- 📦 Une boîte pour les réponses oui/non (décisions)

En programmation, c'est pareil ! Chaque type de données a ses propres caractéristiques et opérations possibles.

### Type = Nature de la donnée

Le **type** définit :
- Ce que la donnée représente
- Quelles opérations on peut faire avec
- Comment elle est stockée en mémoire

```javascript
const prenom = "Alice";      // Type : string (texte)
const age = 25;              // Type : number (nombre)
const estMajeur = true;      // Type : boolean (vrai/faux)
```

## 1. String (Chaîne de caractères) 📝

### Qu'est-ce qu'un string ?

Un **string** (chaîne de caractères) est une séquence de caractères utilisée pour représenter du **texte**.

### Créer un string

Il existe **trois façons** de créer des strings en JavaScript :

#### 1. Guillemets doubles " "

```javascript
const prenom = "Alice";
const message = "Bonjour le monde !";
const phrase = "J'aime le JavaScript";
```

#### 2. Guillemets simples ' '

```javascript
const nom = 'Dupont';
const ville = 'Paris';
const citation = 'Il a dit "bonjour"';  // Guillemets doubles à l'intérieur
```

#### 3. Backticks ` ` (Template literals - Moderne) 🆕

```javascript
const prenom = `Alice`;
const salutation = `Bonjour !`;
```

> 💡 **Quelle syntaxe choisir ?** Les trois fonctionnent, mais les **backticks** sont les plus modernes et offrent des fonctionnalités supplémentaires (nous les verrons en détail dans une section dédiée).

### Strings vides

```javascript
const texteVide = "";      // String vide
const espaces = "   ";     // String avec des espaces
const rien = "";           // Vraiment vide
```

### Caractères spéciaux (échappement)

Pour inclure des caractères spéciaux, utilisez le **backslash** `\` :

```javascript
// Guillemets dans un string
const citation1 = "Il a dit \"bonjour\"";
const citation2 = 'Il a dit "bonjour"';  // Plus simple

// Apostrophe
const phrase1 = 'C\'est génial !';
const phrase2 = "C'est génial !";  // Plus simple

// Saut de ligne
const texte = "Ligne 1\nLigne 2\nLigne 3";

// Tabulation
const tableau = "Nom\tPrénom\tÂge";

// Backslash lui-même
const chemin = "C:\\Users\\Alice\\Documents";
```

**Caractères spéciaux courants :**

| Séquence | Signification |
|----------|---------------|
| `\n` | Saut de ligne (new line) |
| `\t` | Tabulation (tab) |
| `\'` | Apostrophe |
| `\"` | Guillemet double |
| `\\` | Backslash |

### Concaténation (assembler des strings)

#### Avec l'opérateur + (classique)

```javascript
const prenom = "Alice";
const nom = "Dupont";

const nomComplet = prenom + " " + nom;
console.log(nomComplet);  // "Alice Dupont"

const salutation = "Bonjour " + prenom + " !";
console.log(salutation);  // "Bonjour Alice !"
```

#### Avec les template literals (moderne) 🆕

```javascript
const prenom = "Alice";
const age = 25;

// Interpolation avec ${}
const message = `Bonjour, je m'appelle ${prenom} et j'ai ${age} ans.`;
console.log(message);  // "Bonjour, je m'appelle Alice et j'ai 25 ans."

// On peut mettre des expressions
const prix = 50;
const total = `Le total est : ${prix * 2} euros`;
console.log(total);  // "Le total est : 100 euros"
```

> 💡 **Conseil moderne** : Préférez les template literals avec backticks pour plus de lisibilité !

### Exemples pratiques avec strings

```javascript
// Informations personnelles
const prenom = "Alice";
const nom = "Dupont";
const email = "alice.dupont@example.com";

// Messages
const bienvenue = `Bienvenue ${prenom} !`;
const confirmation = `Un email a été envoyé à ${email}`;

// Adresses et chemins
const adresse = "123 rue de la Paix, 75001 Paris";
const url = "https://www.example.com";

// Descriptions
const description = "Développeuse web passionnée par JavaScript";
```

## 2. Number (Nombre) 🔢

### Qu'est-ce qu'un number ?

Un **number** représente une valeur numérique. JavaScript n'a qu'**un seul type** pour tous les nombres (entiers et décimaux).

### Créer un number

```javascript
// Nombres entiers
const age = 25;
const annee = 2025;
const temperature = -5;

// Nombres décimaux (flottants)
const prix = 19.99;
const pi = 3.14159;
const pourcentage = 0.75;

// Nombres négatifs
const dette = -500;
const temperatureFroide = -15.5;

// Zéro
const zero = 0;
```

> ⚡ **Important** : En JavaScript, on utilise le **point** (.) comme séparateur décimal, pas la virgule !

### Nombres spéciaux

```javascript
// Infinity (infini)
const infini = Infinity;
const divisionParZero = 10 / 0;  // Infinity

// -Infinity (infini négatif)
const infiniNegatif = -Infinity;

// NaN (Not a Number - Pas un nombre)
const pasUnNombre = "texte" * 5;  // NaN
const invalide = 0 / 0;           // NaN
```

### Opérations arithmétiques de base

#### Addition (+)

```javascript
const a = 10;
const b = 5;
const somme = a + b;
console.log(somme);  // 15

const prix1 = 20.50;
const prix2 = 15.75;
const total = prix1 + prix2;
console.log(total);  // 36.25
```

#### Soustraction (-)

```javascript
const a = 10;
const b = 3;
const difference = a - b;
console.log(difference);  // 7

const solde = 100;
const depense = 25;
const reste = solde - depense;
console.log(reste);  // 75
```

#### Multiplication (*)

```javascript
const a = 5;
const b = 4;
const produit = a * b;
console.log(produit);  // 20

const prixUnitaire = 10;
const quantite = 3;
const total = prixUnitaire * quantite;
console.log(total);  // 30
```

#### Division (/)

```javascript
const a = 20;
const b = 4;
const quotient = a / b;
console.log(quotient);  // 5

const total = 100;
const personnes = 4;
const partParPersonne = total / personnes;
console.log(partParPersonne);  // 25
```

#### Modulo (%) - Reste de la division

```javascript
const a = 10;
const b = 3;
const reste = a % b;
console.log(reste);  // 1 (car 10 = 3 * 3 + 1)

// Vérifier si un nombre est pair ou impair
const nombre = 7;
const estPair = nombre % 2;
console.log(estPair);  // 1 (impair)
// Si le résultat est 0, le nombre est pair
```

#### Exponentiation (**) - Puissance 🆕

```javascript
const base = 2;
const exposant = 3;
const resultat = base ** exposant;  // 2³ = 8
console.log(resultat);  // 8

const carre = 5 ** 2;      // 5² = 25
const cube = 3 ** 3;       // 3³ = 27
```

### Ordre des opérations

JavaScript suit les règles mathématiques standards (PEMDAS) :

```javascript
const resultat1 = 2 + 3 * 4;        // 14 (multiplication d'abord)
const resultat2 = (2 + 3) * 4;      // 20 (parenthèses d'abord)

const calcul = 10 + 5 * 2 - 3 / 3;
// Ordre : 5 * 2 = 10, 3 / 3 = 1, puis 10 + 10 - 1 = 19
console.log(calcul);  // 19
```

**Ordre de priorité :**
1. Parenthèses `( )`
2. Exponentiation `**`
3. Multiplication `*`, Division `/`, Modulo `%`
4. Addition `+`, Soustraction `-`

### Nombres et précision

⚠️ **Attention** : JavaScript utilise des nombres à virgule flottante, ce qui peut causer des problèmes de précision :

```javascript
const a = 0.1;
const b = 0.2;
const somme = a + b;
console.log(somme);  // 0.30000000000000004 ⚠️ (pas exactement 0.3 !)

// Solution : arrondir
const sommeArrondie = Math.round((a + b) * 100) / 100;
console.log(sommeArrondie);  // 0.3 ✅
```

### Exemples pratiques avec numbers

```javascript
// Calculs de prix
const prixHT = 100;
const tauxTVA = 0.20;
const montantTVA = prixHT * tauxTVA;      // 20
const prixTTC = prixHT + montantTVA;      // 120

// Moyennes
const note1 = 15;
const note2 = 12;
const note3 = 18;
const moyenne = (note1 + note2 + note3) / 3;  // 15

// Conversions
const euros = 50;
const tauxConversion = 1.10;
const dollars = euros * tauxConversion;  // 55

// Calculs d'âge
const anneeNaissance = 1995;
const anneeActuelle = 2025;
const age = anneeActuelle - anneeNaissance;  // 30
```

## 3. Boolean (Booléen) ✅

### Qu'est-ce qu'un boolean ?

Un **boolean** (booléen) est un type de données qui ne peut avoir que **deux valeurs** :
- `true` (vrai)
- `false` (faux)

C'est le type utilisé pour les **décisions** et la **logique** en programmation.

### Créer un boolean

```javascript
const estMajeur = true;
const estConnecte = false;
const aPaye = true;
const estVIP = false;
```

> ⚡ **Important** : `true` et `false` s'écrivent en minuscules, sans guillemets !

```javascript
// ✅ Correct
const vrai = true;
const faux = false;

// ❌ Incorrect
const vrai = True;     // Erreur : True n'existe pas
const faux = "false";  // C'est un string, pas un boolean !
```

### Comparaisons qui retournent des booleans

#### Égalité stricte (===)

```javascript
const age = 18;
const estAdulte = age === 18;
console.log(estAdulte);  // true

const prenom = "Alice";
const estAlice = prenom === "Alice";
console.log(estAlice);  // true

const nombre = 5;
const estDix = nombre === 10;
console.log(estDix);  // false
```

#### Différence stricte (!==)

```javascript
const age = 15;
const estAdulte = age !== 18;
console.log(estAdulte);  // true (15 est différent de 18)

const langue = "fr";
const estAnglais = langue !== "en";
console.log(estAnglais);  // true
```

#### Comparaisons numériques

```javascript
const age = 25;

// Supérieur à
const estMajeur = age > 18;
console.log(estMajeur);  // true

// Supérieur ou égal à
const peutVoter = age >= 18;
console.log(peutVoter);  // true

// Inférieur à
const estEnfant = age < 12;
console.log(estEnfant);  // false

// Inférieur ou égal à
const estAdo = age <= 19;
console.log(estAdo);  // false
```

**Tableau des opérateurs de comparaison :**

| Opérateur | Signification | Exemple | Résultat |
|-----------|---------------|---------|----------|
| `===` | Égal à | `5 === 5` | `true` |
| `!==` | Différent de | `5 !== 3` | `true` |
| `>` | Supérieur à | `10 > 5` | `true` |
| `<` | Inférieur à | `3 < 8` | `true` |
| `>=` | Supérieur ou égal | `5 >= 5` | `true` |
| `<=` | Inférieur ou égal | `4 <= 4` | `true` |

### Opérateurs logiques

#### ET logique (&&)

Les deux conditions doivent être vraies :

```javascript
const age = 25;
const aPermis = true;

const peutConduire = age >= 18 && aPermis;
console.log(peutConduire);  // true (les deux sont vrais)

const age2 = 16;
const aPermis2 = true;
const peutConduire2 = age2 >= 18 && aPermis2;
console.log(peutConduire2);  // false (age < 18)
```

#### OU logique (||)

Au moins une condition doit être vraie :

```javascript
const estWeekend = true;
const estVacances = false;

const peutSeReposer = estWeekend || estVacances;
console.log(peutSeReposer);  // true (weekend est vrai)

const pluie = false;
const neige = false;
const mauvaisTemps = pluie || neige;
console.log(mauvaisTemps);  // false (aucun des deux)
```

#### NON logique (!)

Inverse la valeur :

```javascript
const estConnecte = true;
const estDeconnecte = !estConnecte;
console.log(estDeconnecte);  // false

const estMajeur = false;
const estMineur = !estMajeur;
console.log(estMineur);  // true
```

**Table de vérité :**

| A | B | A && B | A \|\| B | !A |
|---|---|--------|----------|-----|
| true | true | true | true | false |
| true | false | false | true | false |
| false | true | false | true | true |
| false | false | false | false | true |

### Exemples pratiques avec booleans

```javascript
// Vérification d'accès
const age = 20;
const aCarteEtudiant = true;
const peutEntrer = age >= 18 && aCarteEtudiant;
console.log("Accès autorisé:", peutEntrer);  // true

// Conditions de réduction
const estEtudiant = true;
const estSenior = false;
const aReduction = estEtudiant || estSenior;
console.log("A droit à une réduction:", aReduction);  // true

// Validation de formulaire
const nomRempli = true;
const emailRempli = true;
const champsObligatoires = nomRempli && emailRempli;
console.log("Formulaire complet:", champsObligatoires);  // true

// États de l'application
const estCharge = true;
const aErreur = false;
const peutAfficher = estCharge && !aErreur;
console.log("Peut afficher:", peutAfficher);  // true
```

## Valeurs "truthy" et "falsy"

En JavaScript, certaines valeurs sont considérées comme "fausses" (`falsy`) ou "vraies" (`truthy`) dans un contexte boolean.

### Valeurs falsy (considérées comme false)

```javascript
// Ces valeurs sont traitées comme false dans un contexte boolean
false        // Boolean false
0            // Zéro
""           // String vide
null         // Null
undefined    // Undefined
NaN          // Not a Number
```

### Valeurs truthy (considérées comme true)

```javascript
// Tout le reste est truthy !
true         // Boolean true
1            // Tout nombre différent de 0
"hello"      // Tout string non-vide
" "          // Même un espace
[]           // Tableau vide
{}           // Objet vide
```

### Exemple pratique

```javascript
const nom = "Alice";

// Dans une condition, un string non-vide est truthy
if (nom) {
    console.log("Nom fourni !");  // Ceci s'affichera
}

const nomVide = "";

// Un string vide est falsy
if (nomVide) {
    console.log("Ceci ne s'affichera pas");
}
```

## Vérifier le type d'une variable : typeof

L'opérateur `typeof` permet de connaître le type d'une valeur :

```javascript
// Strings
console.log(typeof "Alice");        // "string"
console.log(typeof 'Bob');          // "string"
console.log(typeof `Charlie`);      // "string"

// Numbers
console.log(typeof 42);             // "number"
console.log(typeof 3.14);           // "number"
console.log(typeof -10);            // "number"
console.log(typeof Infinity);       // "number"
console.log(typeof NaN);            // "number" (même si c'est Not a Number !)

// Booleans
console.log(typeof true);           // "boolean"
console.log(typeof false);          // "boolean"

// Avec des variables
const prenom = "Alice";
const age = 25;
const estMajeur = true;

console.log(typeof prenom);         // "string"
console.log(typeof age);            // "number"
console.log(typeof estMajeur);      // "boolean"
```

## Mélanger les types (attention !)

### Addition avec strings (concaténation)

Quand vous utilisez `+` avec un string, JavaScript convertit tout en string :

```javascript
const nombre = 5;
const texte = "10";

// ⚠️ Concaténation, pas addition !
const resultat = nombre + texte;
console.log(resultat);  // "510" (string)
console.log(typeof resultat);  // "string"

// Exemples surprenants
console.log("3" + 4);      // "34" (string)
console.log(3 + "4");      // "34" (string)
console.log("3" + "4");    // "34" (string)
```

### Autres opérateurs (conversion en number)

Avec `-`, `*`, `/`, JavaScript convertit en number :

```javascript
const texte = "10";
const nombre = 5;

console.log(texte - nombre);  // 5 (number)
console.log(texte * nombre);  // 50 (number)
console.log(texte / nombre);  // 2 (number)

// Exemples
console.log("10" - "3");      // 7 (number)
console.log("10" * "2");      // 20 (number)
```

### Cas problématiques

```javascript
// Conversions invalides donnent NaN
console.log("hello" - 5);     // NaN
console.log("abc" * 2);       // NaN

// Boolean converti en number
console.log(true + 1);        // 2 (true = 1)
console.log(false + 5);       // 5 (false = 0)
```

> 🐛 **Piège courant** : Faites attention au `+` avec les strings ! Utilisez des parenthèses si nécessaire.

```javascript
const a = 5;
const b = 10;
const texte = "Le résultat est : " + a + b;
console.log(texte);  // "Le résultat est : 510" ⚠️

// Solution
const texte2 = "Le résultat est : " + (a + b);
console.log(texte2);  // "Le résultat est : 15" ✅
```

## Conversion explicite de types

### String vers Number

```javascript
// Avec Number()
const texte = "42";
const nombre = Number(texte);
console.log(nombre);        // 42 (number)
console.log(typeof nombre); // "number"

// Avec parseInt() (entiers)
const texte2 = "42.7";
const entier = parseInt(texte2);
console.log(entier);        // 42

// Avec parseFloat() (décimaux)
const decimal = parseFloat(texte2);
console.log(decimal);       // 42.7

// Avec l'opérateur + unaire (astuce)
const nombre2 = +"123";
console.log(nombre2);       // 123 (number)
```

### Number vers String

```javascript
// Avec String()
const nombre = 42;
const texte = String(nombre);
console.log(texte);         // "42" (string)
console.log(typeof texte);  // "string"

// Avec .toString()
const nombre2 = 99;
const texte2 = nombre2.toString();
console.log(texte2);        // "99" (string)

// Avec concaténation (astuce)
const texte3 = nombre + "";
console.log(texte3);        // "42" (string)
```

### Vers Boolean

```javascript
// Avec Boolean()
const nombre = 1;
const bool = Boolean(nombre);
console.log(bool);          // true

console.log(Boolean(0));    // false
console.log(Boolean(""));   // false
console.log(Boolean("hi")); // true

// Avec double négation (astuce)
const bool2 = !!"hello";
console.log(bool2);         // true
```

## Exemples pratiques complets

### Exemple 1 : Calcul de prix avec TVA

```javascript
// Données
const prixHT = 100;           // number
const tauxTVA = 20;           // number (pourcentage)
const nomProduit = "Clavier"; // string

// Calculs
const montantTVA = prixHT * (tauxTVA / 100);  // 20
const prixTTC = prixHT + montantTVA;          // 120

// Affichage
const message = `Le ${nomProduit} coûte ${prixTTC}€ TTC`;
console.log(message);
// "Le Clavier coûte 120€ TTC"
```

### Exemple 2 : Vérification d'accès

```javascript
// Données utilisateur
const age = 20;               // number
const aCarteEtudiant = true;  // boolean
const nom = "Alice";          // string

// Vérifications
const estMajeur = age >= 18;                    // true
const peutEntrer = estMajeur && aCarteEtudiant; // true

// Message
if (peutEntrer) {
    console.log(`Bienvenue ${nom} !`);
} else {
    console.log("Accès refusé");
}
```

### Exemple 3 : Panier d'achat

```javascript
// Produits
const prixProduit1 = 29.99;
const prixProduit2 = 15.50;
const prixProduit3 = 8.00;

// Calcul
const sousTotal = prixProduit1 + prixProduit2 + prixProduit3;  // 53.49
const fraisLivraison = sousTotal >= 50 ? 0 : 5.90;
const total = sousTotal + fraisLivraison;

// Informations
const livraisonGratuite = fraisLivraison === 0;  // boolean

console.log(`Sous-total: ${sousTotal.toFixed(2)}€`);
console.log(`Frais de livraison: ${fraisLivraison.toFixed(2)}€`);
console.log(`Total: ${total.toFixed(2)}€`);
console.log(`Livraison gratuite: ${livraisonGratuite}`);
```

## Récapitulatif des types primitifs

| Type | Usage | Exemples | Opérations courantes |
|------|-------|----------|---------------------|
| **String** | Texte | `"Alice"`, `'Hello'`, `` `Salut` `` | Concaténation (+), longueur, méthodes |
| **Number** | Nombres | `42`, `3.14`, `-10` | +, -, *, /, %, ** |
| **Boolean** | Vrai/Faux | `true`, `false` | &&, \|\|, !, comparaisons |

## Bonnes pratiques

### ✅ À faire

1. **Utilisez des noms de variables descriptifs**
   ```javascript
   const prixUnitaire = 10;     // ✅ Clair
   const p = 10;                // ❌ Pas clair
   ```

2. **Utilisez template literals pour les strings**
   ```javascript
   const nom = "Alice";
   const message = `Bonjour ${nom} !`;  // ✅ Moderne
   const message2 = "Bonjour " + nom + " !";  // ⚠️ Ancien
   ```

3. **Utilisez === et !== (égalité stricte)**
   ```javascript
   const age = 18;
   if (age === 18) { }  // ✅ Strict
   if (age == 18) { }   // ⚠️ Non strict (éviter)
   ```

4. **Commentez les nombres "magiques"**
   ```javascript
   const TAUX_TVA = 0.20;  // 20% de TVA
   const prix = 100 * (1 + TAUX_TVA);
   ```

### ❌ À éviter

1. **Mélanger les types sans le vouloir**
   ```javascript
   const resultat = "5" + 3;  // ⚠️ "53" (string)
   ```

2. **Utiliser des valeurs "magiques" sans explication**
   ```javascript
   const prix = montant * 1.2;  // ❌ Que représente 1.2 ?
   ```

3. **Comparer avec == au lieu de ===**
   ```javascript
   console.log(5 == "5");   // true (⚠️ conversion implicite)
   console.log(5 === "5");  // false (✅ types différents)
   ```

## En résumé

### Les 3 types primitifs essentiels

#### String 📝
```javascript
const nom = "Alice";
const message = `Bonjour ${nom} !`;
```
- Représente du texte
- Guillemets doubles, simples ou backticks
- Concaténation avec +

#### Number 🔢
```javascript
const age = 25;
const prix = 19.99;
```
- Représente des nombres (entiers et décimaux)
- Opérations : +, -, *, /, %, **
- Attention à la précision des flottants

#### Boolean ✅
```javascript
const estMajeur = true;
const peutEntrer = age >= 18;
```
- Représente vrai ou faux
- Résultat de comparaisons
- Opérateurs logiques : &&, ||, !

> 🎯 **À retenir** : Ces trois types sont les briques de base de tout programme JavaScript. Maîtrisez-les bien, car vous les utiliserez constamment !

## Prochaine étape

Dans la section suivante, nous découvrirons les **types spéciaux** : `undefined`, `null`, et `Symbol`, qui complètent l'arsenal des types primitifs en JavaScript.

---


💡 **Citation** : "Les données sont le nouveau pétrole" - comprendre les types de données est fondamental en programmation !

⏭️ [Types spéciaux : undefined, null, Symbol](/05-javascript-moderne-fondamentaux/02-variables-et-types/04-types-speciaux.md)
