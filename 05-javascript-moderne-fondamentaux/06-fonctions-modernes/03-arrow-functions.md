🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.3 - Fonctions fléchées (Arrow Functions) 🆕

## Introduction

Les **fonctions fléchées** (*arrow functions*) sont une syntaxe moderne introduite avec **ES6** (ECMAScript 2015) pour créer des fonctions de manière plus concise et élégante.

Elles utilisent la notation `=>` (qui ressemble à une flèche, d'où leur nom) et sont devenues **la façon standard** d'écrire des fonctions en JavaScript moderne.

## Pourquoi les arrow functions ?

Les fonctions fléchées offrent plusieurs avantages :

- ✅ **Syntaxe plus courte** : moins de code à écrire
- ✅ **Plus lisibles** : surtout pour les fonctions simples
- ✅ **Comportement prévisible** : pas de binding de `this` (nous y reviendrons)
- ✅ **Standard moderne** : utilisées partout dans le code JavaScript actuel

## Évolution des syntaxes

Voyons comment la même fonction peut s'écrire avec les trois syntaxes :

### Déclaration classique

```javascript
function additionner(a, b) {
  return a + b;
}
```

### Expression de fonction

```javascript
const additionner = function(a, b) {
  return a + b;
};
```

### Arrow function (moderne) 🆕

```javascript
const additionner = (a, b) => {
  return a + b;
};
```

Encore plus court avec la syntaxe concise :

```javascript
const additionner = (a, b) => a + b;
```

**Impressionnant, non ?** Une seule ligne au lieu de trois !

## Syntaxe de base

La syntaxe de base d'une arrow function :

```javascript
const nomFonction = (paramètres) => {
  // Code à exécuter
  return valeur;
};
```

**Éléments de la syntaxe :**

- `const nomFonction` : Déclaration de variable
- `=` : Opérateur d'assignation
- `(paramètres)` : Paramètres entre parenthèses
- `=>` : La "flèche" qui définit la fonction
- `{ }` : Corps de la fonction (accolades)
- `return` : Retour de valeur

## Exemples simples

### Fonction sans paramètre

```javascript
const direBonjour = () => {
  console.log("Bonjour !");
};

direBonjour(); // Affiche : "Bonjour !"
```

**Note :** Les parenthèses vides `()` sont **obligatoires** quand il n'y a pas de paramètre.

### Fonction avec un seul paramètre

```javascript
const doubler = (nombre) => {
  return nombre * 2;
};

console.log(doubler(5));  // Affiche : 10
console.log(doubler(8));  // Affiche : 16
```

### Fonction avec plusieurs paramètres

```javascript
const multiplier = (a, b) => {
  return a * b;
};

console.log(multiplier(3, 4));  // Affiche : 12
console.log(multiplier(7, 2));  // Affiche : 14
```

## Syntaxe concise (sans accolades)

C'est là que les arrow functions deviennent vraiment puissantes ! Pour les fonctions simples qui ne font qu'une seule chose, vous pouvez utiliser une **syntaxe ultra-concise**.

### Règle du return implicite

Si votre fonction :
- Ne contient qu'**une seule expression**
- Retourne directement le résultat

Vous pouvez :
- **Supprimer les accolades** `{ }`
- **Supprimer le mot-clé** `return`

### Exemples de syntaxe concise

#### Avant (avec accolades et return)

```javascript
const doubler = (nombre) => {
  return nombre * 2;
};
```

#### Après (syntaxe concise) ⚡

```javascript
const doubler = (nombre) => nombre * 2;
```

#### Plus d'exemples

```javascript
// Addition
const additionner = (a, b) => a + b;

// Carré d'un nombre
const carre = (x) => x * x;

// Créer un message
const saluer = (nom) => "Bonjour " + nom + " !";

// Test de condition
const estMajeur = (age) => age >= 18;
```

#### Utilisation

```javascript
console.log(additionner(5, 3));     // Affiche : 8
console.log(carre(4));              // Affiche : 16
console.log(saluer("Alice"));       // Affiche : "Bonjour Alice !"
console.log(estMajeur(25));         // Affiche : true
console.log(estMajeur(15));         // Affiche : false
```

## Simplification des parenthèses

### Un seul paramètre : parenthèses optionnelles

Quand votre fonction n'a **qu'un seul paramètre**, vous pouvez omettre les parenthèses :

```javascript
// Avec parenthèses (valide)
const doubler = (nombre) => nombre * 2;

// Sans parenthèses (aussi valide) ✨
const doubler = nombre => nombre * 2;
```

**C'est encore plus court !**

### Plusieurs paramètres ou zéro : parenthèses obligatoires

```javascript
// Zéro paramètre : parenthèses OBLIGATOIRES
const direBonjour = () => "Bonjour !";

// Deux paramètres ou plus : parenthèses OBLIGATOIRES
const additionner = (a, b) => a + b;
```

## Quand utiliser les accolades ?

### Sans accolades : une seule expression

```javascript
const calculer = (x) => x * 2 + 5;
```

Le résultat de l'expression est automatiquement retourné.

### Avec accolades : code sur plusieurs lignes

Si votre fonction contient **plusieurs instructions**, utilisez les accolades et `return` :

```javascript
const calculerSurfaceCircle = (rayon) => {
  const pi = 3.14159;
  const surface = pi * rayon * rayon;
  return surface;
};

console.log(calculerSurfaceCircle(5)); // Affiche : 78.53975
```

**⚠️ Important :** Avec les accolades, le `return` redevient **obligatoire** !

```javascript
// ❌ Erreur : pas de return avec accolades
const doubler = (x) => {
  x * 2;  // Retourne undefined !
};

// ✅ Correct
const doubler = (x) => {
  return x * 2;
};
```

## Retourner un objet littéral

Petite subtilité : pour retourner un objet avec la syntaxe concise, entourez-le de **parenthèses** :

### ❌ Sans parenthèses (ne fonctionne pas)

```javascript
// JavaScript pense que { } sont les accolades de la fonction !
const creerPersonne = (nom, age) => { nom: nom, age: age };
```

### ✅ Avec parenthèses (correct)

```javascript
const creerPersonne = (nom, age) => ({ nom: nom, age: age });

const alice = creerPersonne("Alice", 30);
console.log(alice); // Affiche : { nom: "Alice", age: 30 }
```

Encore plus court avec la syntaxe ES6 :

```javascript
const creerPersonne = (nom, age) => ({ nom, age });
```

## Exemples pratiques complets

### Exemple 1 : Conversions de température

```javascript
const celsiusVersFahrenheit = celsius => (celsius * 9/5) + 32;
const fahrenheitVersCelsius = fahrenheit => (fahrenheit - 32) * 5/9;

console.log(celsiusVersFahrenheit(0));    // Affiche : 32
console.log(celsiusVersFahrenheit(100));  // Affiche : 212
console.log(fahrenheitVersCelsius(32));   // Affiche : 0
```

### Exemple 2 : Manipulations de strings

```javascript
const majuscule = texte => texte.toUpperCase();
const minuscule = texte => texte.toLowerCase();
const longueur = texte => texte.length;
const inverser = texte => texte.split("").reverse().join("");

console.log(majuscule("hello"));    // Affiche : "HELLO"
console.log(minuscule("WORLD"));    // Affiche : "world"
console.log(longueur("JavaScript")); // Affiche : 10
console.log(inverser("hello"));     // Affiche : "olleh"
```

### Exemple 3 : Validations

```javascript
const estEmailValide = email => email.includes("@") && email.includes(".");
const estMotDePasseSecurise = mdp => mdp.length >= 8;
const estNombrePositif = n => n > 0;
const estPair = n => n % 2 === 0;

console.log(estEmailValide("user@example.com")); // Affiche : true
console.log(estMotDePasseSecurise("abc123"));    // Affiche : false
console.log(estNombrePositif(-5));               // Affiche : false
console.log(estPair(4));                         // Affiche : true
```

### Exemple 4 : Calculs mathématiques

```javascript
const perimetre = rayon => 2 * Math.PI * rayon;
const aire = rayon => Math.PI * rayon * rayon;
const hypotenuse = (a, b) => Math.sqrt(a * a + b * b);

console.log(perimetre(5));      // Affiche : 31.41592653589793
console.log(aire(5));           // Affiche : 78.53981633974483
console.log(hypotenuse(3, 4));  // Affiche : 5
```

## Arrow functions avec les méthodes de tableau

Les arrow functions brillent particulièrement avec les **méthodes de tableau** (que vous verrez en détail plus tard) :

### Méthode map()

```javascript
const nombres = [1, 2, 3, 4, 5];

// Avant ES6 (expression de fonction)
const doubles = nombres.map(function(n) {
  return n * 2;
});

// Avec arrow function 🆕
const doubles = nombres.map(n => n * 2);

console.log(doubles); // Affiche : [2, 4, 6, 8, 10]
```

### Méthode filter()

```javascript
const nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Filtrer les nombres pairs
const pairs = nombres.filter(n => n % 2 === 0);

console.log(pairs); // Affiche : [2, 4, 6, 8, 10]
```

### Méthode reduce()

```javascript
const nombres = [1, 2, 3, 4, 5];

// Calculer la somme
const somme = nombres.reduce((acc, n) => acc + n, 0);

console.log(somme); // Affiche : 15
```

**Ces exemples sont spectaculairement plus courts et lisibles !**

## Arrow functions et le mot-clé `this`

C'est la **différence fondamentale** entre les fonctions classiques et les arrow functions.

### Fonctions classiques : `this` dynamique

Les fonctions classiques ont leur propre `this` qui change selon le contexte d'appel :

```javascript
const personne = {
  nom: "Alice",
  direBonjour: function() {
    console.log("Bonjour, je suis " + this.nom);
  }
};

personne.direBonjour(); // Affiche : "Bonjour, je suis Alice"
```

### Arrow functions : `this` lexical

Les arrow functions **n'ont pas leur propre** `this`. Elles héritent du `this` du contexte parent :

```javascript
const personne = {
  nom: "Alice",
  direBonjour: () => {
    console.log("Bonjour, je suis " + this.nom); // this ne pointe pas vers personne !
  }
};

personne.direBonjour(); // Affiche : "Bonjour, je suis undefined"
```

### Exemple pratique : setTimeout

C'est particulièrement utile avec des callbacks comme `setTimeout` :

#### Problème avec fonction classique

```javascript
const personne = {
  nom: "Alice",
  direBonjour: function() {
    setTimeout(function() {
      console.log("Bonjour, je suis " + this.nom); // this est perdu !
    }, 1000);
  }
};

personne.direBonjour(); // Affiche : "Bonjour, je suis undefined"
```

#### Solution avec arrow function ✅

```javascript
const personne = {
  nom: "Alice",
  direBonjour: function() {
    setTimeout(() => {
      console.log("Bonjour, je suis " + this.nom); // this est préservé !
    }, 1000);
  }
};

personne.direBonjour(); // Affiche : "Bonjour, je suis Alice"
```

### Règle simple pour `this`

- **Méthodes d'objet** : utilisez une fonction classique
- **Callbacks** : utilisez une arrow function

```javascript
const objet = {
  propriete: "valeur",

  // Méthode : fonction classique
  methode: function() {
    console.log(this.propriete);

    // Callback : arrow function
    setTimeout(() => {
      console.log(this.propriete); // this est préservé
    }, 1000);
  }
};
```

## Arrow functions : ce qu'elles n'ont pas

Les arrow functions **ne peuvent pas** :

- ❌ Être utilisées comme **constructeurs** (pas de `new`)
- ❌ Avoir leur propre objet **`arguments`**
- ❌ Être utilisées comme **méthodes de générateur** (`yield`)

```javascript
// ❌ Ne fonctionne pas
const Personne = (nom) => {
  this.nom = nom;
};
const alice = new Personne("Alice"); // Erreur !

// ❌ Ne fonctionne pas
const maFonction = () => {
  console.log(arguments); // arguments n'existe pas
};
```

**Mais honnêtement**, ces limitations sont rarement un problème dans le code moderne !

## Comparaison des trois syntaxes

| Aspect | Déclaration | Expression | Arrow Function |
|--------|-------------|------------|----------------|
| **Syntaxe** | `function f() {}` | `const f = function() {}` | `const f = () => {}` |
| **Hoisting** | ✅ Oui | ❌ Non | ❌ Non |
| **Syntaxe concise** | ❌ Non | ❌ Non | ✅ Oui |
| **`this` propre** | ✅ Oui | ✅ Oui | ❌ Non (lexical) |
| **Constructeur (new)** | ✅ Oui | ✅ Oui | ❌ Non |
| **Objet arguments** | ✅ Oui | ✅ Oui | ❌ Non |
| **Usage moderne** | Courant | Courant | **Très courant** |

## Quand utiliser les arrow functions ?

### ✅ Utilisez des arrow functions pour :

- Les **fonctions courtes et simples**
- Les **callbacks** (map, filter, reduce, setTimeout, etc.)
- Les **fonctions dans les fonctions**
- Quand vous voulez **préserver** le `this` du contexte parent
- La plupart de votre **code moderne**

### ❌ Évitez les arrow functions pour :

- Les **méthodes d'objet** (utilisez une fonction classique)
- Les **constructeurs**
- Quand vous avez besoin de `this` dynamique
- Quand vous avez besoin de l'objet `arguments`

## Exemples de choix de syntaxe

```javascript
// Objet avec méthodes
const utilisateur = {
  nom: "Alice",

  // Méthode d'objet : fonction classique (pour avoir `this`)
  saluer: function() {
    console.log("Bonjour, je suis " + this.nom);

    // Callback : arrow function (pour préserver `this`)
    setTimeout(() => {
      console.log("Je suis toujours " + this.nom);
    }, 1000);
  }
};

// Fonction utilitaire : arrow function
const doubler = x => x * 2;

// Transformation de tableau : arrow function
const nombres = [1, 2, 3, 4, 5];
const doubles = nombres.map(n => n * 2);

// Fonction avec logique complexe : fonction classique ou expression
function calculComplexe(a, b, c) {
  const etape1 = a + b;
  const etape2 = etape1 * c;
  const etape3 = Math.sqrt(etape2);
  return etape3;
}
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier les parenthèses pour retourner un objet

```javascript
// ❌ Incorrect
const creerPersonne = (nom, age) => { nom: nom, age: age };

// ✅ Correct
const creerPersonne = (nom, age) => ({ nom: nom, age: age });
```

### ❌ Erreur 2 : Utiliser `return` sans accolades

```javascript
// ❌ Erreur de syntaxe
const doubler = x => return x * 2;

// ✅ Correct (sans accolades)
const doubler = x => x * 2;

// ✅ Correct (avec accolades)
const doubler = x => {
  return x * 2;
};
```

### ❌ Erreur 3 : Oublier le `return` avec des accolades

```javascript
// ❌ Retourne undefined
const doubler = x => {
  x * 2;
};

// ✅ Correct
const doubler = x => {
  return x * 2;
};

// ✅ Ou mieux : sans accolades
const doubler = x => x * 2;
```

### ❌ Erreur 4 : Utiliser arrow function comme méthode d'objet

```javascript
// ❌ `this` ne pointe pas vers l'objet
const personne = {
  nom: "Alice",
  saluer: () => {
    console.log("Bonjour " + this.nom); // undefined !
  }
};

// ✅ Correct
const personne = {
  nom: "Alice",
  saluer: function() {
    console.log("Bonjour " + this.nom);
  }
};

// ✅ Ou encore mieux (syntaxe ES6)
const personne = {
  nom: "Alice",
  saluer() {
    console.log("Bonjour " + this.nom);
  }
};
```

## Points clés à retenir

1. **Arrow functions** : syntaxe moderne et concise avec `=>`

2. **Syntaxe de base** :
   ```javascript
   const f = (params) => { return valeur; };
   ```

3. **Syntaxe concise** : pas d'accolades ni de `return` pour une seule expression
   ```javascript
   const f = (params) => valeur;
   ```

4. **Parenthèses optionnelles** : pour un seul paramètre
   ```javascript
   const f = param => valeur;
   ```

5. **Objet littéral** : entourez-le de parenthèses
   ```javascript
   const f = () => ({ prop: valeur });
   ```

6. **`this` lexical** : hérite du contexte parent (pas de `this` propre)

7. **Idéales pour** : callbacks, fonctions courtes, méthodes de tableau

8. **À éviter pour** : méthodes d'objet, constructeurs

## Prochaines étapes

Maintenant que vous maîtrisez les arrow functions, vous êtes prêt pour :

- Les **paramètres et arguments** en détail (5.6.4)
- Les **paramètres par défaut** (5.6.5)
- Les **rest parameters** avec `...args` (5.6.6)
- Les **méthodes de tableau** modernes (Section 5.8)

Les arrow functions sont **omniprésentes** dans le JavaScript moderne. Vous les verrez et utiliserez constamment dans votre code et dans tout le code que vous lirez. Maîtriser leur syntaxe et leurs subtilités est essentiel pour devenir un développeur JavaScript moderne !

---

**Note :** Les arrow functions sont l'une des fonctionnalités ES6+ les plus populaires et les plus utilisées. Elles rendent le code JavaScript beaucoup plus lisible et concis. Dans le développement moderne, elles sont devenues la norme pour écrire la plupart des fonctions, particulièrement dans les contextes de callbacks et de programmation fonctionnelle.

⏭️ [Paramètres et arguments](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/04-parametres-arguments.md)
