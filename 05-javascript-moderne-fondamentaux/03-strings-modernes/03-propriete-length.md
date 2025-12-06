🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.3 - Propriété length

## Introduction

La propriété **`length`** est l'une des propriétés les plus utilisées avec les strings en JavaScript. Elle permet de connaître le **nombre de caractères** contenus dans une string.

Cette propriété simple mais puissante est essentielle pour de nombreuses opérations courantes : validation de formulaires, limitation de caractères, parcours de strings, et bien plus encore.

---

## Qu'est-ce que la propriété length ?

La propriété `length` retourne un **nombre entier** représentant le nombre de caractères dans une string.

### Syntaxe

```javascript
const nombreDeCaracteres = maString.length;
```

**Important** : Notez qu'il **n'y a pas de parenthèses** après `length`. C'est une **propriété**, pas une **méthode** (nous verrons la différence plus bas).

---

## Utilisation de base

### Exemple simple

```javascript
const mot = "Bonjour";
console.log(mot.length); // Affiche : 7
```

Le mot "Bonjour" contient 7 caractères : B-o-n-j-o-u-r

### Avec des variables

```javascript
const prenom = "Alice";
const longueur = prenom.length;

console.log(longueur); // Affiche : 5
console.log(`Le prénom ${prenom} contient ${longueur} caractères.`);
// Affiche : Le prénom Alice contient 5 caractères.
```

### String vide

```javascript
const stringVide = "";
console.log(stringVide.length); // Affiche : 0
```

Une string vide a une longueur de **0**.

---

## Les espaces comptent !

**Attention** : Les espaces sont des caractères comme les autres et sont donc comptés par `length`.

```javascript
const phrase1 = "Bonjour";
console.log(phrase1.length); // 7

const phrase2 = "Bonjour ";
console.log(phrase2.length); // 8 (espace à la fin)

const phrase3 = " Bonjour ";
console.log(phrase3.length); // 9 (espaces au début et à la fin)

const phrase4 = "Bonjour tout le monde";
console.log(phrase4.length); // 21 (les espaces entre les mots comptent)
```

---

## Caractères spéciaux et length

### Sauts de ligne et tabulations

Les caractères d'échappement comme `\n` (saut de ligne) et `\t` (tabulation) comptent pour **1 caractère chacun** :

```javascript
const texte1 = "Ligne 1\nLigne 2";
console.log(texte1.length); // 15
// L-i-g-n-e- -1-\n-L-i-g-n-e- -2 = 15 caractères

const texte2 = "Nom:\tAlice";
console.log(texte2.length); // 10
// N-o-m-:-\t-A-l-i-c-e = 10 caractères
```

### Caractères échappés

Un caractère échappé compte pour **1 seul caractère** :

```javascript
const texte = "Il a dit \"Bonjour\"";
console.log(texte.length); // 18
// Les \" comptent chacun pour 1 caractère
```

### Emojis et caractères Unicode complexes ⚠️

**Attention** : Certains emojis et caractères spéciaux peuvent compter pour **plus d'un caractère** en raison de leur encodage Unicode :

```javascript
const texte1 = "Hello 😀";
console.log(texte1.length); // 8 (l'emoji compte pour 2)

const texte2 = "👨‍👩‍👧‍👦"; // Famille (emoji composé)
console.log(texte2.length); // 11 (emoji très complexe)
```

**Note pour débutants** : C'est une particularité technique liée à l'encodage UTF-16. Dans la pratique quotidienne, cela n'affecte que rarement vos applications, mais c'est bon à savoir !

---

## Cas d'usage pratiques

### 1. Validation de formulaire

Vérifier qu'un champ respecte une longueur minimale ou maximale :

```javascript
const motDePasse = "abc123";

if (motDePasse.length < 8) {
    console.log("Le mot de passe doit contenir au moins 8 caractères.");
} else {
    console.log("Mot de passe valide.");
}
// Affiche : Le mot de passe doit contenir au moins 8 caractères.
```

### 2. Limitation de caractères (Twitter, SMS)

```javascript
const message = "Ceci est mon message à publier sur les réseaux sociaux.";
const limiteTwitter = 280;

if (message.length > limiteTwitter) {
    console.log(`Message trop long ! (${message.length}/${limiteTwitter} caractères)`);
} else {
    console.log(`Il vous reste ${limiteTwitter - message.length} caractères.`);
}
// Affiche : Il vous reste 223 caractères.
```

### 3. Affichage du compteur de caractères

Créer un compteur en temps réel pour un champ de texte :

```javascript
const commentaire = "Super article !";
const max = 200;

console.log(`${commentaire.length}/${max} caractères`);
// Affiche : 15/200 caractères
```

### 4. Vérifier si une string n'est pas vide

```javascript
const nom = "Alice";

if (nom.length > 0) {
    console.log("Le champ nom est rempli.");
} else {
    console.log("Le champ nom est vide.");
}
```

**Alternative plus idiomatique** :

```javascript
// Une string vide est "falsy" en JavaScript
if (nom) {
    console.log("Le champ nom est rempli.");
}
```

### 5. Troncature de texte

Limiter l'affichage d'un texte long :

```javascript
const description = "Ceci est une très longue description qui pourrait être tronquée pour l'affichage.";
const maxLength = 50;

if (description.length > maxLength) {
    const texteTronque = description.substring(0, maxLength) + "...";
    console.log(texteTronque);
    // Affiche : Ceci est une très longue description qui pourra...
} else {
    console.log(description);
}
```

---

## Accéder au dernier caractère

La propriété `length` est utile pour accéder au **dernier caractère** d'une string :

```javascript
const mot = "JavaScript";

// Le dernier index est length - 1 (car l'indexation commence à 0)
const dernierCaractere = mot[mot.length - 1];
console.log(dernierCaractere); // Affiche : t

// Premier caractère (pour comparaison)
const premierCaractere = mot[0];
console.log(premierCaractere); // Affiche : J
```

**Pourquoi `length - 1` ?**

Parce que l'indexation commence à 0 :
- `"JavaScript"` a 10 caractères (length = 10)
- Les indices vont de 0 à 9
- Le dernier caractère est à l'indice 9, donc `length - 1`

---

## Comparaison de longueurs

Vous pouvez comparer les longueurs de plusieurs strings :

```javascript
const mot1 = "chat";
const mot2 = "chien";
const mot3 = "papillon";

if (mot1.length === mot2.length) {
    console.log("Les deux mots ont la même longueur.");
} else if (mot1.length < mot2.length) {
    console.log(`"${mot1}" est plus court que "${mot2}".`);
} else {
    console.log(`"${mot1}" est plus long que "${mot2}".`);
}
// Affiche : "chat" est plus court que "chien".

// Trouver le mot le plus long
let motLePlusLong = mot1;
if (mot2.length > motLePlusLong.length) {
    motLePlusLong = mot2;
}
if (mot3.length > motLePlusLong.length) {
    motLePlusLong = mot3;
}
console.log(`Le mot le plus long est : ${motLePlusLong}`);
// Affiche : Le mot le plus long est : papillon
```

---

## Propriété vs Méthode

### C'est une PROPRIÉTÉ (pas de parenthèses)

```javascript
const mot = "Bonjour";

// ✅ CORRECT : propriété (sans parenthèses)
console.log(mot.length);

// ❌ ERREUR courante : ajouter des parenthèses
console.log(mot.length());  // TypeError: mot.length is not a function
```

### Différence entre propriété et méthode

| Propriété | Méthode |
|-----------|---------|
| Accès direct à une valeur | Fonction qui effectue une action |
| **Pas de parenthèses** | **Avec parenthèses** |
| `string.length` | `string.toUpperCase()` |
| Retourne une valeur stockée | Retourne le résultat d'un calcul |

**Exemples :**

```javascript
const texte = "Hello";

// Propriété
console.log(texte.length);  // 5

// Méthodes (avec parenthèses)
console.log(texte.toUpperCase());  // "HELLO"
console.log(texte.toLowerCase());  // "hello"
```

---

## La propriété length est en lecture seule

Vous **ne pouvez pas modifier** directement la longueur d'une string :

```javascript
let mot = "Bonjour";
console.log(mot.length); // 7

// ❌ Ceci ne fait RIEN (ignoré silencieusement)
mot.length = 3;
console.log(mot);        // "Bonjour" (inchangé)
console.log(mot.length); // 7 (inchangé)
```

**Rappel** : Les strings sont **immutables** en JavaScript. Pour "modifier" une string, vous devez en créer une nouvelle :

```javascript
let mot = "Bonjour";
mot = mot.substring(0, 3); // Crée une nouvelle string
console.log(mot);        // "Bon"
console.log(mot.length); // 3
```

---

## Boucles avec length

La propriété `length` est très utilisée dans les boucles pour parcourir une string caractère par caractère :

### Boucle for classique

```javascript
const mot = "JavaScript";

for (let i = 0; i < mot.length; i++) {
    console.log(`Caractère ${i} : ${mot[i]}`);
}
```

**Résultat :**
```
Caractère 0 : J
Caractère 1 : a
Caractère 2 : v
Caractère 3 : a
...
```

### Boucle for...of moderne (recommandée)

```javascript
const mot = "Bonjour";

for (const caractere of mot) {
    console.log(caractere);
}
```

**Résultat :**
```
B
o
n
j
o
u
r
```

---

## Exemple complet : validateur de mot de passe

Voici un exemple pratique qui utilise `length` pour valider un mot de passe :

```javascript
const motDePasse = "MonMotDePasse123!";

// Règles de validation
const longueurMin = 8;
const longueurMax = 20;

// Validation de la longueur
if (motDePasse.length < longueurMin) {
    console.log(`❌ Trop court ! Minimum ${longueurMin} caractères requis.`);
} else if (motDePasse.length > longueurMax) {
    console.log(`❌ Trop long ! Maximum ${longueurMax} caractères autorisés.`);
} else {
    console.log(`✅ Longueur valide (${motDePasse.length} caractères).`);
}

// Affichage d'un indicateur de force
let force = "Faible";
if (motDePasse.length >= 12) {
    force = "Moyen";
}
if (motDePasse.length >= 16) {
    force = "Fort";
}
console.log(`Force du mot de passe : ${force}`);
```

---

## Pièges courants

### ❌ Piège 1 : Ajouter des parenthèses

```javascript
const mot = "Bonjour";

// ❌ ERREUR
console.log(mot.length());  // TypeError

// ✅ CORRECT
console.log(mot.length);    // 7
```

### ❌ Piège 2 : Oublier que les espaces comptent

```javascript
const input = "   ";  // Trois espaces
console.log(input.length);  // 3 (pas 0 !)

// Pour vérifier si une string est "vraiment" vide :
if (input.trim().length === 0) {
    console.log("Le champ est vide ou ne contient que des espaces.");
}
```

### ❌ Piège 3 : Confusion avec les tableaux

Les strings et les tableaux ont tous deux une propriété `length`, mais elles se comportent différemment :

```javascript
const string = "abc";
const tableau = ["a", "b", "c"];

console.log(string.length);  // 3 (nombre de caractères)
console.log(tableau.length); // 3 (nombre d'éléments)

// On peut modifier la length d'un tableau (pas d'une string)
tableau.length = 2;
console.log(tableau);  // ["a", "b"] - le tableau est tronqué !
```

---

## Points clés à retenir

✅ **`length`** est une **propriété** (pas de parenthèses !)

✅ Retourne le **nombre de caractères** dans une string

✅ Les **espaces comptent** comme des caractères

✅ Utile pour la **validation** de formulaires

✅ Essentiel pour **parcourir** une string dans une boucle

✅ La propriété length est en **lecture seule** (on ne peut pas la modifier)

✅ `string[string.length - 1]` permet d'accéder au **dernier caractère**

✅ Attention aux **emojis complexes** qui peuvent compter pour plusieurs caractères

---

## Astuces pratiques

### Vérifier si une string n'est pas vide

```javascript
// Méthode 1 : avec length
if (string.length > 0) { /* ... */ }

// Méthode 2 : conversion booléenne (plus idiomatique)
if (string) { /* ... */ }

// Méthode 3 : vérifier après trim (ignorer les espaces)
if (string.trim().length > 0) { /* ... */ }
```

### Calculer le nombre de mots

```javascript
const phrase = "JavaScript est un langage génial";
const nombreDeMots = phrase.split(" ").length;
console.log(nombreDeMots); // 5
```

### Créer une barre de progression

```javascript
const texte = "Bonjour";
const max = 10;
const pourcentage = Math.round((texte.length / max) * 100);

console.log(`Progression : ${pourcentage}%`);
// Affiche : Progression : 70%
```

---

## Dans la prochaine section

Dans la section **5.3.4 - Méthodes de recherche**, nous découvrirons les méthodes modernes pour rechercher du contenu dans une string : `indexOf()`, `includes()`, `startsWith()`, et `endsWith()`.

---


⏭️ [Méthodes de recherche : indexOf, includes, startsWith, endsWith](/05-javascript-moderne-fondamentaux/03-strings-modernes/04-methodes-recherche.md)
