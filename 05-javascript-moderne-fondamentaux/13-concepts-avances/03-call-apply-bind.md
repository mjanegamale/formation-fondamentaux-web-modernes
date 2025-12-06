🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.13.3 - Méthodes call, apply, bind

## Introduction

Les méthodes `call()`, `apply()` et `bind()` sont des outils puissants en JavaScript qui permettent de **contrôler le contexte d'exécution** d'une fonction, c'est-à-dire de décider ce que représente le mot-clé `this`.

> 💡 **En résumé** : Ces méthodes vous permettent de "prêter" une fonction à un objet et de décider quel objet sera `this` lors de l'exécution.

---

## Rappel : Le problème de `this`

Avant de plonger dans ces méthodes, rappelons rapidement le problème qu'elles résolvent.

### Comportement par défaut de `this`

```javascript
const personne = {
  nom: "Alice",
  saluer: function() {
    console.log(`Bonjour, je suis ${this.nom}`);
  }
};

personne.saluer(); // "Bonjour, je suis Alice" ✅
```

Ça fonctionne bien ! Mais regardez ce qui se passe ici :

```javascript
const personne = {
  nom: "Alice",
  saluer: function() {
    console.log(`Bonjour, je suis ${this.nom}`);
  }
};

const direBonjour = personne.saluer;
direBonjour(); // "Bonjour, je suis undefined" ❌
```

**Pourquoi ?** Parce que `this` dépend de **comment la fonction est appelée**, pas de où elle est définie.

C'est là que `call`, `apply` et `bind` entrent en jeu ! 🎯

---

## 1. La méthode `call()`

### Définition

`call()` permet d'**appeler une fonction** en spécifiant explicitement ce que sera `this`.

### Syntaxe

```javascript
fonction.call(objetPourThis, arg1, arg2, arg3, ...)
```

- **Premier paramètre** : L'objet qui sera `this`
- **Paramètres suivants** : Les arguments de la fonction

### Exemple de base

```javascript
function saluer() {
  console.log(`Bonjour, je suis ${this.nom}`);
}

const alice = { nom: "Alice" };
const bob = { nom: "Bob" };

saluer.call(alice); // "Bonjour, je suis Alice"
saluer.call(bob);   // "Bonjour, je suis Bob"
```

**Explication :**
- `call()` exécute `saluer` immédiatement
- Le premier argument devient `this` dans la fonction
- On peut "prêter" la même fonction à différents objets

### Avec des arguments

```javascript
function presenter(age, ville) {
  console.log(`Je suis ${this.nom}, j'ai ${age} ans et j'habite à ${ville}`);
}

const personne = { nom: "Alice" };

presenter.call(personne, 25, "Paris");
// "Je suis Alice, j'ai 25 ans et j'habite à Paris"
```

### Cas d'usage pratique : Emprunter une méthode

```javascript
const chien = {
  nom: "Rex",
  parler: function() {
    console.log(`${this.nom} dit: Ouaf !`);
  }
};

const chat = { nom: "Minou" };

// Le chat "emprunte" la méthode parler du chien
chien.parler.call(chat); // "Minou dit: Ouaf !"
```

---

## 2. La méthode `apply()`

### Définition

`apply()` fonctionne **exactement comme `call()`**, mais les arguments sont passés dans un **tableau**.

### Syntaxe

```javascript
fonction.apply(objetPourThis, [arg1, arg2, arg3, ...])
```

- **Premier paramètre** : L'objet qui sera `this`
- **Deuxième paramètre** : Un **tableau** contenant les arguments

### Exemple de base

```javascript
function presenter(age, ville) {
  console.log(`Je suis ${this.nom}, j'ai ${age} ans et j'habite à ${ville}`);
}

const personne = { nom: "Alice" };

// Avec call (arguments séparés)
presenter.call(personne, 25, "Paris");

// Avec apply (arguments dans un tableau)
presenter.apply(personne, [25, "Paris"]);

// Les deux affichent :
// "Je suis Alice, j'ai 25 ans et j'habite à Paris"
```

### Cas d'usage : Quand utiliser `apply()` ?

Quand vous avez **déjà un tableau** d'arguments :

```javascript
function addition(a, b, c) {
  return a + b + c;
}

const nombres = [5, 10, 15];

// ❌ Pas pratique avec call
const resultat1 = addition.call(null, nombres[0], nombres[1], nombres[2]);

// ✅ Plus simple avec apply
const resultat2 = addition.apply(null, nombres);

console.log(resultat2); // 30
```

> 💡 **Note moderne** : Avec ES6, on peut aussi utiliser le spread operator :
> ```javascript
> const resultat = addition(...nombres); // Plus moderne
> ```

### Exemple pratique : Trouver le maximum d'un tableau

```javascript
const nombres = [5, 10, 2, 25, 8];

// Math.max() ne prend pas de tableau, mais des arguments séparés
// Math.max(5, 10, 2, 25, 8) ✅
// Math.max([5, 10, 2, 25, 8]) ❌

// Solution avec apply
const maximum = Math.max.apply(null, nombres);
console.log(maximum); // 25

// OU solution moderne avec spread
const maximum2 = Math.max(...nombres);
console.log(maximum2); // 25
```

---

## 3. La méthode `bind()`

### Définition

`bind()` **ne lance pas la fonction** immédiatement. Au lieu de cela, elle **crée une nouvelle fonction** avec `this` fixé définitivement.

### Syntaxe

```javascript
const nouvelleFonction = fonction.bind(objetPourThis, arg1, arg2, ...)
```

- **Retourne** : Une nouvelle fonction
- **Ne s'exécute pas** immédiatement

### Exemple de base

```javascript
function saluer() {
  console.log(`Bonjour, je suis ${this.nom}`);
}

const alice = { nom: "Alice" };

// bind() crée une NOUVELLE fonction
const saluerAlice = saluer.bind(alice);

// On peut l'appeler plus tard
saluerAlice(); // "Bonjour, je suis Alice"
saluerAlice(); // "Bonjour, je suis Alice"
```

### Différence clé : `call/apply` vs `bind`

```javascript
const personne = { nom: "Alice" };

function direBonjour() {
  console.log(`Bonjour ${this.nom}`);
}

// call() : exécution IMMÉDIATE
direBonjour.call(personne); // Affiche tout de suite

// bind() : crée une fonction, exécution PLUS TARD
const bonjourAlice = direBonjour.bind(personne);
bonjourAlice(); // On choisit quand l'exécuter
```

### Cas d'usage pratique 1 : Gestionnaires d'événements

**❌ Problème sans bind :**
```javascript
const bouton = {
  texte: "Cliquez-moi",

  handleClick: function() {
    console.log(`Bouton cliqué: ${this.texte}`);
  }
};

document.getElementById('monBouton')
  .addEventListener('click', bouton.handleClick);

// Clic → "Bouton cliqué: undefined" ❌
// Pourquoi ? this devient l'élément DOM, pas l'objet bouton
```

**✅ Solution avec bind :**
```javascript
const bouton = {
  texte: "Cliquez-moi",

  handleClick: function() {
    console.log(`Bouton cliqué: ${this.texte}`);
  }
};

document.getElementById('monBouton')
  .addEventListener('click', bouton.handleClick.bind(bouton));

// Clic → "Bouton cliqué: Cliquez-moi" ✅
```

### Cas d'usage pratique 2 : Arguments pré-remplis (Currying partiel)

```javascript
function multiplier(a, b) {
  return a * b;
}

// Créer une fonction "doubler"
const doubler = multiplier.bind(null, 2);

console.log(doubler(5));  // 10 (2 × 5)
console.log(doubler(10)); // 20 (2 × 10)

// Créer une fonction "tripler"
const tripler = multiplier.bind(null, 3);

console.log(tripler(5));  // 15 (3 × 5)
console.log(tripler(10)); // 30 (3 × 10)
```

**Explication :**
- `bind()` peut pré-remplir des arguments
- `multiplier.bind(null, 2)` crée une fonction où `a = 2` est déjà fixé
- On n'a plus qu'à fournir `b`

---

## Comparaison : call vs apply vs bind

| Méthode | Exécution | Arguments | Retourne |
|---------|-----------|-----------|----------|
| **call()** | Immédiate | Séparés : `func.call(obj, a, b, c)` | Le résultat de la fonction |
| **apply()** | Immédiate | Tableau : `func.apply(obj, [a, b, c])` | Le résultat de la fonction |
| **bind()** | Plus tard | Séparés : `func.bind(obj, a, b)` | Une nouvelle fonction |

### Exemple comparatif

```javascript
function presenter(age, ville) {
  return `${this.nom}, ${age} ans, ${ville}`;
}

const personne = { nom: "Alice" };

// call : exécution immédiate, arguments séparés
const resultat1 = presenter.call(personne, 25, "Paris");
console.log(resultat1); // "Alice, 25 ans, Paris"

// apply : exécution immédiate, arguments en tableau
const resultat2 = presenter.apply(personne, [25, "Paris"]);
console.log(resultat2); // "Alice, 25 ans, Paris"

// bind : retourne une fonction
const presenterAlice = presenter.bind(personne, 25, "Paris");
const resultat3 = presenterAlice(); // On l'appelle plus tard
console.log(resultat3); // "Alice, 25 ans, Paris"
```

---

## Exemples pratiques détaillés

### Exemple 1 : Réutiliser une méthode

```javascript
const utilisateur1 = {
  nom: "Alice",
  email: "alice@example.com",
  afficherInfos: function() {
    console.log(`${this.nom} - ${this.email}`);
  }
};

const utilisateur2 = {
  nom: "Bob",
  email: "bob@example.com"
  // Pas de méthode afficherInfos
};

// Bob "emprunte" la méthode d'Alice
utilisateur1.afficherInfos.call(utilisateur2);
// "Bob - bob@example.com"
```

### Exemple 2 : Chaînage de constructeurs

```javascript
function Personne(nom, age) {
  this.nom = nom;
  this.age = age;
}

function Etudiant(nom, age, ecole) {
  // Appeler le constructeur Personne avec le contexte Etudiant
  Personne.call(this, nom, age);
  this.ecole = ecole;
}

const etudiant = new Etudiant("Alice", 20, "Sorbonne");
console.log(etudiant);
// { nom: "Alice", age: 20, ecole: "Sorbonne" }
```

### Exemple 3 : Conversion array-like en tableau

```javascript
function exemple() {
  // arguments est "array-like" mais pas un vrai tableau
  console.log(arguments); // Objet arguments

  // Utiliser slice pour convertir en tableau
  const args = Array.prototype.slice.call(arguments);
  console.log(args); // Vrai tableau

  // Maintenant on peut utiliser les méthodes de tableau
  args.forEach(arg => console.log(arg));
}

exemple(1, 2, 3, 4);

// OU version moderne avec spread
function exempleModerne() {
  const args = [...arguments];
  console.log(args);
}
```

### Exemple 4 : Délai avec contexte préservé

```javascript
const timer = {
  secondes: 0,

  demarrer: function() {
    setInterval(function() {
      this.secondes++; // ❌ this est undefined ou window
      console.log(this.secondes);
    }, 1000);
  }
};

// ✅ Solution avec bind
const timerCorrige = {
  secondes: 0,

  demarrer: function() {
    setInterval(function() {
      this.secondes++;
      console.log(this.secondes);
    }.bind(this), 1000); // bind(this) fixe le contexte
  }
};

timerCorrige.demarrer(); // 1, 2, 3, 4...
```

### Exemple 5 : Méthode d'extraction personnalisée

```javascript
const nombres = [1, 2, 3, 4, 5];

// Utiliser join (méthode des tableaux) sur un objet arguments
function afficherArgs() {
  const resultat = Array.prototype.join.call(arguments, ' - ');
  console.log(resultat);
}

afficherArgs('Alice', 'Bob', 'Charlie');
// "Alice - Bob - Charlie"
```

---

## bind() et les arguments partiels

`bind()` permet de créer des fonctions avec des arguments pré-remplis :

```javascript
function calculer(operation, a, b) {
  if (operation === 'addition') return a + b;
  if (operation === 'multiplication') return a * b;
}

// Créer des fonctions spécialisées
const additionner = calculer.bind(null, 'addition');
const multiplier = calculer.bind(null, 'multiplication');

console.log(additionner(5, 3));  // 8
console.log(multiplier(5, 3));   // 15

// On peut même pré-remplir plus d'arguments
const ajouter10 = calculer.bind(null, 'addition', 10);
console.log(ajouter10(5)); // 15 (10 + 5)
```

---

## Différence avec les Arrow Functions

⚠️ **Important** : Les arrow functions ne peuvent pas changer leur `this` avec `call`, `apply` ou `bind`.

```javascript
const personne = {
  nom: "Alice",

  // Fonction normale
  saluerNormal: function() {
    console.log(`Bonjour ${this.nom}`);
  },

  // Arrow function
  saluerArrow: () => {
    console.log(`Bonjour ${this.nom}`);
  }
};

const bob = { nom: "Bob" };

// Avec fonction normale : ✅ fonctionne
personne.saluerNormal.call(bob); // "Bonjour Bob"

// Avec arrow function : ❌ this ne change pas
personne.saluerArrow.call(bob); // "Bonjour undefined"
```

**Pourquoi ?** Les arrow functions ont un `this` lexical (fixé à la création).

### Quand utiliser quoi ?

```javascript
const compteur = {
  compte: 0,

  // ✅ Méthode normale : this peut être contrôlé
  incrementer: function() {
    this.compte++;
  },

  // ✅ Arrow pour callbacks : this automatique
  demarrer: function() {
    setInterval(() => {
      this.compte++; // this = compteur automatiquement
      console.log(this.compte);
    }, 1000);
  }
};
```

---

## Pièges à éviter

### 1. Utiliser `call/apply` sur une arrow function

```javascript
const obj = { nom: "Alice" };

const direNom = () => {
  console.log(this.nom);
};

direNom.call(obj); // ❌ Ne change pas this
```

### 2. Oublier de retourner avec `bind`

```javascript
const obj = { valeur: 42 };

function getValue() {
  return this.valeur;
}

// ❌ Oubli de bind
setTimeout(getValue, 1000); // undefined

// ✅ Avec bind
setTimeout(getValue.bind(obj), 1000); // 42
```

### 3. Chaîner plusieurs `bind`

```javascript
function afficher() {
  console.log(this.nom);
}

const obj1 = { nom: "Alice" };
const obj2 = { nom: "Bob" };

const func = afficher.bind(obj1).bind(obj2);
func(); // "Alice" (le premier bind gagne toujours)
```

**Règle** : Une fois `bind()` appliqué, `this` est fixé définitivement.

---

## Cas d'usage modernes

### 1. Avec les classes ES6

```javascript
class Compteur {
  constructor() {
    this.count = 0;
    // Bind dans le constructeur pour les événements
    this.incrementer = this.incrementer.bind(this);
  }

  incrementer() {
    this.count++;
    console.log(this.count);
  }
}

const compteur = new Compteur();

// Sans bind, this serait l'élément bouton
document.getElementById('btn')
  .addEventListener('click', compteur.incrementer);
```

### 2. Callbacks et API asynchrones

```javascript
class UtilisateurService {
  constructor() {
    this.utilisateurs = [];
  }

  charger() {
    fetch('/api/users')
      .then(function(response) {
        return response.json();
      }.bind(this)) // Nécessaire pour fonction normale
      .then(function(data) {
        this.utilisateurs = data;
      }.bind(this));

    // OU avec arrow functions (plus moderne)
    fetch('/api/users')
      .then(response => response.json())
      .then(data => {
        this.utilisateurs = data; // this automatique
      });
  }
}
```

### 3. Méthodes utilitaires réutilisables

```javascript
const mathUtils = {
  additionner: function(a, b) {
    return a + b;
  },

  creerAdditionneur: function(valeur) {
    return this.additionner.bind(this, valeur);
  }
};

const ajouter5 = mathUtils.creerAdditionneur(5);
console.log(ajouter5(10)); // 15
console.log(ajouter5(20)); // 25
```

---

## Alternatives modernes

Avec JavaScript moderne, certains usages de `call/apply/bind` peuvent être remplacés :

### Spread operator au lieu d'`apply`

```javascript
const nombres = [5, 10, 2, 25, 8];

// Ancien (apply)
const max1 = Math.max.apply(null, nombres);

// Moderne (spread)
const max2 = Math.max(...nombres);
```

### Arrow functions au lieu de `bind`

```javascript
class Component {
  constructor() {
    this.data = [];
  }

  // Ancien
  charger_ancien() {
    fetch('/api/data')
      .then(function(res) { return res.json(); }.bind(this))
      .then(function(data) { this.data = data; }.bind(this));
  }

  // Moderne
  charger_moderne() {
    fetch('/api/data')
      .then(res => res.json())
      .then(data => this.data = data);
  }
}
```

---

## Résumé visuel

```javascript
const objet = { valeur: 42 };

function afficher(a, b) {
  console.log(this.valeur, a, b);
}

// ═══════════════════════════════════════
// CALL : Exécution immédiate, args séparés
// ═══════════════════════════════════════
afficher.call(objet, 1, 2);
// Résultat : 42 1 2 (exécuté tout de suite)

// ═══════════════════════════════════════
// APPLY : Exécution immédiate, args en tableau
// ═══════════════════════════════════════
afficher.apply(objet, [1, 2]);
// Résultat : 42 1 2 (exécuté tout de suite)

// ═══════════════════════════════════════
// BIND : Retourne une fonction
// ═══════════════════════════════════════
const fonctionLiee = afficher.bind(objet, 1, 2);
fonctionLiee();
// Résultat : 42 1 2 (exécuté quand on appelle)
```

---

## Points clés à retenir

✅ **call()** : Exécute immédiatement avec `this` personnalisé, arguments séparés

✅ **apply()** : Comme `call()` mais arguments dans un tableau

✅ **bind()** : Crée une nouvelle fonction avec `this` fixé (pas d'exécution immédiate)

✅ **Utile pour** :
   - Emprunter des méthodes entre objets
   - Préserver le contexte dans les callbacks
   - Créer des fonctions partiellement appliquées
   - Héritage de constructeur

⚠️ **Ne fonctionne pas avec les arrow functions** (elles ont un `this` lexical)

⚠️ **bind() est permanent** : impossible de re-bind une fonction déjà bindée

---

## Quand les utiliser en pratique ?

### Utilisez `call()`
- Emprunter une méthode une fois
- Chaîner des constructeurs
- Contexte ponctuel

### Utilisez `apply()`
- Quand vous avez déjà un tableau d'arguments
- Fonctions variadiques (Math.max, Math.min...)

### Utilisez `bind()`
- Gestionnaires d'événements
- Callbacks setTimeout/setInterval
- Créer des fonctions configurées
- Méthodes de classe pour événements

### Préférez les alternatives modernes
- Arrow functions pour callbacks simples
- Spread operator au lieu d'apply
- Classes avec class fields pour auto-bind

---

## Conclusion

`call()`, `apply()` et `bind()` sont des outils essentiels pour maîtriser `this` en JavaScript. Bien qu'ils puissent sembler complexes au début, ils sont extrêmement utiles pour :

- Contrôler précisément le contexte d'exécution
- Réutiliser du code de manière flexible
- Résoudre des problèmes de `this` dans les callbacks

Avec JavaScript moderne (ES6+), certains de leurs usages peuvent être remplacés par des arrow functions ou le spread operator, mais ils restent fondamentaux pour comprendre le fonctionnement en profondeur de JavaScript ! 🎯

⏭️ [Import/Export de modules (ES6)](/05-javascript-moderne-fondamentaux/13-concepts-avances/04-import-export-modules.md)
