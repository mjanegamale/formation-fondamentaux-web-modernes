🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.2 - Expression de fonction

## Introduction

Dans la section précédente, vous avez appris la **déclaration de fonction classique**. Il existe une autre façon de créer des fonctions en JavaScript : l'**expression de fonction**.

Une expression de fonction consiste à **assigner une fonction à une variable**, exactement comme vous assigneriez un nombre ou une chaîne de caractères.

## Rappel : déclaration classique

Avant d'aller plus loin, rappelons la syntaxe de déclaration classique :

```javascript
function direBonjour() {
  console.log("Bonjour !");
}
```

## Qu'est-ce qu'une expression de fonction ?

Une expression de fonction crée une fonction et l'assigne à une variable :

```javascript
const direBonjour = function() {
  console.log("Bonjour !");
};
```

**Remarquez les différences :**

1. On utilise `const` (ou `let`) pour déclarer une variable
2. Le nom de la fonction après `function` est absent (fonction **anonyme**)
3. On termine par un **point-virgule** `;` (comme toute assignation de variable)

## Syntaxe de base

```javascript
const nomVariable = function() {
  // Code à exécuter
};
```

**Éléments de la syntaxe :**

- `const nomVariable` : Déclaration de variable (préférez `const`)
- `=` : Opérateur d'assignation
- `function()` : Fonction anonyme (sans nom après `function`)
- `{ }` : Corps de la fonction
- `;` : Point-virgule de fin (important !)

## Appeler une expression de fonction

L'appel se fait exactement comme avec une déclaration classique :

```javascript
const saluer = function() {
  console.log("Salut tout le monde !");
};

saluer(); // Affiche : "Salut tout le monde !"
```

**Important :** Vous utilisez le **nom de la variable**, pas un nom de fonction.

## Exemples avec paramètres

Les expressions de fonction acceptent des paramètres normalement :

### Exemple simple

```javascript
const direBonjour = function(prenom) {
  console.log("Bonjour " + prenom + " !");
};

direBonjour("Marie");  // Affiche : "Bonjour Marie !"
direBonjour("Lucas");  // Affiche : "Bonjour Lucas !"
```

### Exemple avec plusieurs paramètres et return

```javascript
const additionner = function(a, b) {
  return a + b;
};

const resultat = additionner(10, 5);
console.log(resultat); // Affiche : 15

const somme = additionner(7, 3);
console.log(somme); // Affiche : 10
```

### Exemple pratique : calculer une remise

```javascript
const calculerPrixFinal = function(prixInitial, pourcentageRemise) {
  const remise = prixInitial * (pourcentageRemise / 100);
  const prixFinal = prixInitial - remise;
  return prixFinal;
};

console.log(calculerPrixFinal(100, 20)); // Affiche : 80
console.log(calculerPrixFinal(50, 10));  // Affiche : 45
```

## Différence majeure : pas de hoisting !

C'est la **différence cruciale** entre déclaration et expression de fonction.

### Avec une déclaration classique (hoisting = ✅)

```javascript
// Ceci fonctionne ! ✅
direBonjour();

function direBonjour() {
  console.log("Bonjour !");
}
```

### Avec une expression de fonction (pas de hoisting = ❌)

```javascript
// Ceci NE fonctionne PAS ! ❌
direBonjour(); // ❌ Erreur : Cannot access 'direBonjour' before initialization

const direBonjour = function() {
  console.log("Bonjour !");
};
```

**Explication :** Les variables déclarées avec `const` et `let` ne sont pas "remontées" (hoisting) de la même manière que les déclarations de fonction classiques.

### Règle d'or

Avec les expressions de fonction, vous **devez déclarer la fonction AVANT de l'appeler** :

```javascript
// ✅ Correct : déclaration puis appel
const direBonjour = function() {
  console.log("Bonjour !");
};

direBonjour(); // Fonctionne !
```

## Fonction anonyme vs fonction nommée

### Fonction anonyme (le plus courant)

```javascript
const calculer = function(x, y) {
  return x + y;
};
```

La fonction n'a pas de nom après le mot-clé `function`.

### Fonction nommée dans une expression

On peut aussi donner un nom à la fonction dans l'expression :

```javascript
const calculer = function addition(x, y) {
  return x + y;
};
```

**Quand utiliser un nom ?**

Le nom n'est utile que pour :
- Le **débogage** : le nom apparaît dans les messages d'erreur
- La **récursivité** : la fonction peut s'appeler elle-même

Dans la plupart des cas, une fonction anonyme suffit.

### Exemple avec récursivité

```javascript
const factorielle = function fact(n) {
  if (n <= 1) {
    return 1;
  }
  return n * fact(n - 1); // La fonction s'appelle elle-même
};

console.log(factorielle(5)); // Affiche : 120
```

## Les fonctions sont des valeurs

En JavaScript, les fonctions sont des **citoyens de première classe** (*first-class citizens*). Cela signifie qu'on peut les traiter comme n'importe quelle autre valeur.

### Assigner à plusieurs variables

```javascript
const saluer = function(nom) {
  return "Bonjour " + nom;
};

const direHello = saluer; // Copie la référence de la fonction

console.log(saluer("Alice"));    // Affiche : "Bonjour Alice"
console.log(direHello("Bob"));   // Affiche : "Bonjour Bob"
```

### Passer une fonction en argument

Les expressions de fonction sont particulièrement utiles pour passer des fonctions à d'autres fonctions :

```javascript
const afficher = function(message) {
  console.log(message);
};

const executer = function(fn, texte) {
  fn(texte); // Appelle la fonction passée en paramètre
};

executer(afficher, "Hello world !"); // Affiche : "Hello world !"
```

Cet exemple peut sembler complexe maintenant, mais c'est un pattern très courant en JavaScript (callbacks, que vous verrez plus tard).

### Retourner une fonction

Une fonction peut même retourner une autre fonction :

```javascript
const creerSalutation = function(salut) {
  return function(nom) {
    return salut + " " + nom;
  };
};

const direBonjour = creerSalutation("Bonjour");
const direHello = creerSalutation("Hello");

console.log(direBonjour("Marie")); // Affiche : "Bonjour Marie"
console.log(direHello("John"));    // Affiche : "Hello John"
```

Ne vous inquiétez pas si cet exemple semble avancé, nous reviendrons sur ce concept plus tard.

## const vs let pour les fonctions

### Utilisez const (recommandé)

```javascript
const calculer = function(x) {
  return x * 2;
};

// calculer = function() { }; // ❌ Erreur : impossible de réassigner
```

`const` empêche la réassignation accidentelle de la fonction.

### let (moins recommandé)

```javascript
let calculer = function(x) {
  return x * 2;
};

calculer = function(x) { // ✅ Autorisé mais déconseillé
  return x * 3;
};
```

**Bonne pratique :** Utilisez toujours `const` pour vos expressions de fonction, sauf si vous avez une raison spécifique de vouloir réassigner la fonction.

## Comparaison : déclaration vs expression

| Aspect | Déclaration classique | Expression de fonction |
|--------|----------------------|------------------------|
| **Syntaxe** | `function nom() { }` | `const nom = function() { };` |
| **Hoisting** | ✅ Oui | ❌ Non |
| **Peut être appelée avant déclaration** | ✅ Oui | ❌ Non |
| **Nom de fonction** | Obligatoire | Facultatif (anonyme) |
| **Point-virgule** | Non | Oui |
| **Assignation à variable** | Non directement | Oui |
| **Utilisation moderne** | Très courant | Très courant |

## Exemples pratiques complets

### Exemple 1 : Convertisseur de devises

```javascript
const convertirEuroVersUSD = function(montantEuros) {
  const tauxChange = 1.10; // Exemple de taux
  return montantEuros * tauxChange;
};

const montantUSD = convertirEuroVersUSD(100);
console.log(montantUSD + " USD"); // Affiche : "110 USD"
```

### Exemple 2 : Validateur d'email simple

```javascript
const estEmailValide = function(email) {
  return email.includes("@") && email.includes(".");
};

console.log(estEmailValide("user@example.com")); // Affiche : true
console.log(estEmailValide("userexample.com"));  // Affiche : false
console.log(estEmailValide("user@example"));     // Affiche : false
```

### Exemple 3 : Calculateur de prix TTC

```javascript
const calculerPrixTTC = function(prixHT, tauxTVA) {
  const montantTVA = prixHT * (tauxTVA / 100);
  const prixTTC = prixHT + montantTVA;
  return prixTTC;
};

console.log(calculerPrixTTC(100, 20));  // Affiche : 120
console.log(calculerPrixTTC(50, 5.5));  // Affiche : 52.75
```

### Exemple 4 : Formateur de message

```javascript
const formaterMessage = function(prenom, age, ville) {
  return "Bonjour, je suis " + prenom + ", j'ai " + age + " ans et j'habite à " + ville + ".";
};

const message1 = formaterMessage("Sophie", 28, "Lyon");
console.log(message1);
// Affiche : "Bonjour, je suis Sophie, j'ai 28 ans et j'habite à Lyon."

const message2 = formaterMessage("Thomas", 35, "Marseille");
console.log(message2);
// Affiche : "Bonjour, je suis Thomas, j'ai 35 ans et j'habite à Marseille."
```

## Quand utiliser une expression de fonction ?

Utilisez une expression de fonction quand :

- ✅ Vous voulez **éviter le hoisting** et forcer une déclaration avant utilisation
- ✅ Vous souhaitez **passer une fonction en argument** à une autre fonction
- ✅ Vous voulez **créer des fonctions anonymes** (sans nom)
- ✅ Vous travaillez dans un **contexte où une valeur est attendue**
- ✅ Vous suivez un **style de code cohérent** avec `const`/`let`

## Utilisations courantes dans le code moderne

### Dans les méthodes de tableau

```javascript
const nombres = [1, 2, 3, 4, 5];

// La fonction est passée directement
const doubles = nombres.map(function(nombre) {
  return nombre * 2;
});

console.log(doubles); // Affiche : [2, 4, 6, 8, 10]
```

### Dans les événements (que vous verrez plus tard)

```javascript
const bouton = document.querySelector("button");

bouton.addEventListener("click", function() {
  console.log("Bouton cliqué !");
});
```

### Dans les callbacks (que vous verrez plus tard)

```javascript
setTimeout(function() {
  console.log("Exécuté après 2 secondes");
}, 2000);
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier le point-virgule

```javascript
const calculer = function(x) {
  return x * 2;
} // ❌ Point-virgule manquant

// Devrait être :
const calculer = function(x) {
  return x * 2;
}; // ✅
```

### ❌ Erreur 2 : Appeler avant de déclarer

```javascript
calculer(); // ❌ Erreur !

const calculer = function() {
  return 42;
};

// Correct :
const calculer = function() {
  return 42;
};
calculer(); // ✅
```

### ❌ Erreur 3 : Confondre déclaration et expression

```javascript
// Ce n'est pas une expression de fonction :
function calculer() { } // C'est une déclaration

// Ceci est une expression de fonction :
const calculer = function() { }; // ✅
```

## Points clés à retenir

1. **Expression de fonction** : assigner une fonction à une variable avec `const` ou `let`

2. **Syntaxe** :
   ```javascript
   const nomVariable = function(paramètres) {
     // code
     return valeur;
   };
   ```

3. **Pas de hoisting** : vous devez déclarer avant d'appeler

4. **Fonction anonyme** : le nom après `function` est optionnel

5. **Point-virgule** : ne l'oubliez pas à la fin !

6. **const recommandé** : empêche la réassignation accidentelle

7. **Fonctions = valeurs** : peuvent être assignées, passées en argument, retournées

8. **Très utilisé** : notamment pour les callbacks, méthodes de tableau, événements

## Prochaines étapes

Maintenant que vous maîtrisez les expressions de fonction, vous êtes prêt pour :

- Les **fonctions fléchées (arrow functions)** - la syntaxe moderne et concise d'ES6+ (5.6.3)
- Les **callbacks** - passer des fonctions en argument (5.6.10)
- Les **paramètres par défaut** (5.6.5)

Dans la section suivante, vous découvrirez les **arrow functions**, une syntaxe moderne et encore plus concise pour créer des expressions de fonction !

---

**Note :** Les expressions de fonction sont fondamentales en JavaScript moderne. Elles sont particulièrement importantes pour comprendre les concepts plus avancés comme les callbacks, les closures, et la programmation fonctionnelle que vous rencontrerez plus tard dans votre apprentissage.

⏭️ [Fonctions fléchées (Arrow functions) : syntaxe et différences](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/03-arrow-functions.md)
