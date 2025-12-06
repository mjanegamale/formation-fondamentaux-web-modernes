🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.6 - Rest Parameters (...args) 🆕

## Introduction

Les **rest parameters** (paramètres rest ou paramètres de reste) sont une fonctionnalité ES6 qui permet à une fonction d'accepter un **nombre indéfini d'arguments** et de les regrouper dans un tableau.

La syntaxe utilise trois points `...` suivis d'un nom de paramètre : `...args`

C'est extrêmement utile quand vous ne savez pas à l'avance combien d'arguments seront passés à votre fonction.

## Le problème à résoudre

Imaginez que vous voulez créer une fonction qui additionne des nombres, mais vous ne savez pas combien de nombres l'utilisateur va fournir :

```javascript
additionner(1, 2);           // 2 nombres
additionner(5, 10, 15);      // 3 nombres
additionner(1, 2, 3, 4, 5);  // 5 nombres
```

Comment gérer cela avec une seule fonction ?

## Syntaxe des rest parameters

```javascript
function nomFonction(...nomTableau) {
  // nomTableau est un tableau contenant tous les arguments
}
```

### Éléments de la syntaxe

- `...` : Les trois points (rest operator)
- `nomTableau` : Le nom que vous donnez au tableau (souvent `args`, `params`, `values`, etc.)
- Le résultat est un **vrai tableau** JavaScript

## Premier exemple simple

```javascript
function additionner(...nombres) {
  console.log(nombres);  // C'est un tableau !

  let somme = 0;
  for (let i = 0; i < nombres.length; i++) {
    somme += nombres[i];
  }
  return somme;
}

console.log(additionner(1, 2));              // Affiche : 3
console.log(additionner(5, 10, 15));         // Affiche : 30
console.log(additionner(1, 2, 3, 4, 5));     // Affiche : 15
console.log(additionner(10, 20, 30, 40, 50, 60)); // Affiche : 210
```

**Magie !** Peu importe le nombre d'arguments, ils sont tous capturés dans le tableau `nombres`.

## Rest parameters avec arrow functions

Cela fonctionne parfaitement avec les arrow functions :

```javascript
const additionner = (...nombres) => {
  let somme = 0;
  for (let nombre of nombres) {
    somme += nombre;
  }
  return somme;
};

console.log(additionner(1, 2, 3, 4)); // Affiche : 10
```

Ou avec `reduce` (méthode moderne de tableau) :

```javascript
const additionner = (...nombres) => nombres.reduce((acc, n) => acc + n, 0);

console.log(additionner(1, 2, 3, 4)); // Affiche : 10
```

## Combiner avec des paramètres normaux

Vous pouvez avoir des paramètres normaux **avant** le rest parameter :

```javascript
function saluer(salutation, ...noms) {
  console.log(salutation + " " + noms.join(", ") + " !");
}

saluer("Bonjour", "Alice");
// Affiche : "Bonjour Alice !"

saluer("Bonjour", "Alice", "Bob");
// Affiche : "Bonjour Alice, Bob !"

saluer("Bonjour", "Alice", "Bob", "Charlie");
// Affiche : "Bonjour Alice, Bob, Charlie !"
```

**Explication :**
- `salutation` capture le premier argument
- `...noms` capture **tous les arguments restants** dans un tableau

### Exemple avec calcul de moyenne

```javascript
function calculerMoyenne(matiere, ...notes) {
  console.log("Matière :", matiere);
  console.log("Notes :", notes);

  const somme = notes.reduce((acc, note) => acc + note, 0);
  const moyenne = somme / notes.length;

  return moyenne;
}

console.log(calculerMoyenne("Mathématiques", 15, 12, 18));
// Matière : Mathématiques
// Notes : [15, 12, 18]
// Retourne : 15

console.log(calculerMoyenne("Histoire", 14, 16, 13, 17, 15));
// Matière : Histoire
// Notes : [14, 16, 13, 17, 15]
// Retourne : 15
```

## Règles importantes

### 1. Le rest parameter doit être le DERNIER paramètre

```javascript
// ✅ Correct
function exemple(a, b, ...reste) { }

// ❌ Erreur : rest parameter doit être le dernier
function exemple(a, ...reste, b) { }  // SyntaxError!
```

### 2. Il ne peut y avoir qu'UN SEUL rest parameter

```javascript
// ❌ Erreur : un seul rest parameter autorisé
function exemple(...args1, ...args2) { }  // SyntaxError!

// ✅ Correct : un seul rest parameter
function exemple(...args) { }
```

### 3. Le rest parameter capture TOUS les arguments restants

```javascript
function exemple(a, b, ...reste) {
  console.log("a:", a);
  console.log("b:", b);
  console.log("reste:", reste);
}

exemple(1, 2, 3, 4, 5, 6);
// a: 1
// b: 2
// reste: [3, 4, 5, 6]
```

## Exemples pratiques complets

### Exemple 1 : Fonction de multiplication

```javascript
const multiplier = (...nombres) => {
  if (nombres.length === 0) {
    return 0;
  }

  let resultat = 1;
  for (let nombre of nombres) {
    resultat *= nombre;
  }
  return resultat;
};

console.log(multiplier(2, 3));           // 6
console.log(multiplier(2, 3, 4));        // 24
console.log(multiplier(5, 2, 10, 2));    // 200
console.log(multiplier());               // 0
```

### Exemple 2 : Trouver le maximum

```javascript
const trouverMax = (...nombres) => {
  if (nombres.length === 0) {
    return null;
  }

  let max = nombres[0];
  for (let nombre of nombres) {
    if (nombre > max) {
      max = nombre;
    }
  }
  return max;
};

console.log(trouverMax(5, 2, 9, 1, 7));      // 9
console.log(trouverMax(15, 8, 23, 4, 16));   // 23
console.log(trouverMax(100));                // 100

// Ou plus simplement avec Math.max et spread
const trouverMax2 = (...nombres) => Math.max(...nombres);
```

### Exemple 3 : Créer une liste HTML

```javascript
function creerListe(titre, ...elements) {
  let html = "<h3>" + titre + "</h3>";
  html += "<ul>";

  for (let element of elements) {
    html += "<li>" + element + "</li>";
  }

  html += "</ul>";
  return html;
}

console.log(creerListe("Courses"));
// <h3>Courses</h3><ul></ul>

console.log(creerListe("Courses", "Pain", "Lait"));
// <h3>Courses</h3><ul><li>Pain</li><li>Lait</li></ul>

console.log(creerListe("Tâches", "Étudier", "Coder", "Faire du sport", "Lire"));
// <h3>Tâches</h3><ul><li>Étudier</li><li>Coder</li><li>Faire du sport</li><li>Lire</li></ul>
```

### Exemple 4 : Logger avec timestamp

```javascript
function log(niveau, ...messages) {
  const timestamp = new Date().toLocaleTimeString();
  console.log("[" + timestamp + "] [" + niveau + "]", ...messages);
}

log("INFO", "Application démarrée");
// [14:30:25] [INFO] Application démarrée

log("ERROR", "Échec de connexion", "Code: 500", "Serveur indisponible");
// [14:30:26] [ERROR] Échec de connexion Code: 500 Serveur indisponible

log("DEBUG", "Variable x:", 42, "Variable y:", 100);
// [14:30:27] [DEBUG] Variable x: 42 Variable y: 100
```

### Exemple 5 : Concaténer des strings

```javascript
const concatener = (separateur, ...mots) => {
  return mots.join(separateur);
};

console.log(concatener(" ", "Bonjour", "le", "monde"));
// "Bonjour le monde"

console.log(concatener("-", "2025", "12", "05"));
// "2025-12-05"

console.log(concatener(", ", "Alice", "Bob", "Charlie", "David"));
// "Alice, Bob, Charlie, David"
```

### Exemple 6 : Filtrer des valeurs

```javascript
const garderPositifs = (...nombres) => {
  return nombres.filter(n => n > 0);
};

console.log(garderPositifs(5, -3, 10, -1, 0, 8));
// [5, 10, 8]

console.log(garderPositifs(-5, -10, -2));
// []

console.log(garderPositifs(1, 2, 3, 4, 5));
// [1, 2, 3, 4, 5]
```

## Rest parameters vs l'objet arguments (ancien)

Avant ES6, JavaScript fournissait un objet spécial appelé `arguments` disponible dans toutes les fonctions.

### L'ancien objet arguments (à éviter)

```javascript
function somme() {
  console.log(arguments);  // Ressemble à un tableau mais n'en est pas un !

  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(somme(1, 2, 3, 4)); // 10
```

**Problèmes avec `arguments` :**
- ❌ Ce n'est **pas un vrai tableau** (pas de méthodes comme `map`, `filter`, `reduce`)
- ❌ Ne fonctionne **pas avec les arrow functions**
- ❌ Moins lisible (on ne voit pas dans la signature qu'il accepte plusieurs arguments)
- ❌ Comportement parfois surprenant

### Rest parameters (moderne) ✅

```javascript
const somme = (...nombres) => {
  return nombres.reduce((acc, n) => acc + n, 0);
};

console.log(somme(1, 2, 3, 4)); // 10
```

**Avantages des rest parameters :**
- ✅ **Vrai tableau** JavaScript avec toutes les méthodes
- ✅ Fonctionne avec **arrow functions**
- ✅ **Lisible** : on voit dans la signature que la fonction accepte plusieurs arguments
- ✅ Peut être combiné avec des paramètres normaux
- ✅ Plus moderne et recommandé

### Comparaison côte à côte

```javascript
// ❌ Ancien : avec arguments
function ancienMax() {
  // Convertir arguments en tableau
  const nombres = Array.from(arguments);
  return Math.max(...nombres);
}

// ✅ Moderne : avec rest parameters
const nouveauMax = (...nombres) => Math.max(...nombres);
```

## Rest parameters vs Spread operator

Ne confondez pas les rest parameters (`...` dans les paramètres) avec le spread operator (`...` dans les appels) :

### Rest parameters : RASSEMBLER

Transforme plusieurs arguments en un seul tableau :

```javascript
function exemple(...args) {
  // args est un TABLEAU contenant tous les arguments
  console.log(args);
}

exemple(1, 2, 3); // [1, 2, 3]
```

### Spread operator : DISPERSER

Transforme un tableau en arguments individuels :

```javascript
const nombres = [1, 2, 3];

// Spread : disperse le tableau en arguments individuels
console.log(Math.max(...nombres)); // Équivalent à Math.max(1, 2, 3)
```

### Utilisation combinée

Vous pouvez utiliser les deux ensemble :

```javascript
// Rest : rassemble les arguments en tableau
const additionner = (...nombres) => {
  return nombres.reduce((acc, n) => acc + n, 0);
};

const liste1 = [1, 2, 3];
const liste2 = [4, 5, 6];

// Spread : disperse les tableaux en arguments individuels
console.log(additionner(...liste1));              // 6
console.log(additionner(...liste2));              // 15
console.log(additionner(...liste1, ...liste2));   // 21
```

### Mémo visuel

```javascript
// REST : plusieurs → un (tableau)
function func(...args) { }  // ← Rassemble les arguments
func(1, 2, 3);             // args = [1, 2, 3]

// SPREAD : un (tableau) → plusieurs
const arr = [1, 2, 3];
func(...arr);              // ← Disperse le tableau
// Équivalent à : func(1, 2, 3)
```

## Cas d'usage pratiques

### 1. Fonctions mathématiques flexibles

```javascript
const stats = (...nombres) => {
  const somme = nombres.reduce((acc, n) => acc + n, 0);
  const moyenne = somme / nombres.length;
  const min = Math.min(...nombres);
  const max = Math.max(...nombres);

  return { somme, moyenne, min, max };
};

console.log(stats(10, 20, 30, 40, 50));
// { somme: 150, moyenne: 30, min: 10, max: 50 }
```

### 2. Wrapper de console.log

```javascript
const debug = (...args) => {
  console.log("[DEBUG]", new Date().toISOString(), ...args);
};

debug("User logged in", { id: 123, name: "Alice" });
// [DEBUG] 2025-12-05T14:30:00.000Z User logged in { id: 123, name: 'Alice' }
```

### 3. Validation de formulaire

```javascript
const validerChamps = (formulaire, ...champsRequis) => {
  const champsManquants = [];

  for (let champ of champsRequis) {
    if (!formulaire[champ]) {
      champsManquants.push(champ);
    }
  }

  return {
    valide: champsManquants.length === 0,
    champsManquants: champsManquants
  };
};

const form = { nom: "Alice", email: "alice@test.com" };

console.log(validerChamps(form, "nom", "email"));
// { valide: true, champsManquants: [] }

console.log(validerChamps(form, "nom", "email", "telephone"));
// { valide: false, champsManquants: ["telephone"] }
```

### 4. Créateur de requête SQL

```javascript
const creerRequete = (table, ...colonnes) => {
  const cols = colonnes.length > 0 ? colonnes.join(", ") : "*";
  return "SELECT " + cols + " FROM " + table;
};

console.log(creerRequete("users"));
// "SELECT * FROM users"

console.log(creerRequete("users", "id", "nom", "email"));
// "SELECT id, nom, email FROM users"
```

### 5. Fonction de composition

```javascript
const composer = (...fonctions) => {
  return (valeur) => {
    return fonctions.reduceRight((acc, fn) => fn(acc), valeur);
  };
};

const doubler = x => x * 2;
const ajouter10 = x => x + 10;
const carre = x => x * x;

const calcul = composer(carre, ajouter10, doubler);
console.log(calcul(5));  // ((5 * 2) + 10)² = 400
```

## Avec la déstructuration

Vous pouvez combiner rest parameters avec la déstructuration :

```javascript
const afficherPremierEtReste = (premier, ...reste) => {
  console.log("Premier :", premier);
  console.log("Reste :", reste);
};

afficherPremierEtReste(1, 2, 3, 4, 5);
// Premier : 1
// Reste : [2, 3, 4, 5]

// Avec déstructuration de tableau
const [premier, deuxieme, ...reste] = [10, 20, 30, 40, 50];
console.log(premier);   // 10
console.log(deuxieme);  // 20
console.log(reste);     // [30, 40, 50]
```

## Bonnes pratiques

### 1. Nommage significatif

```javascript
// ❌ Nom générique
function faire(...args) { }

// ✅ Nom descriptif
function additionnerNombres(...nombres) { }
function afficherMessages(...messages) { }
function creerElements(...elements) { }
```

### 2. Validation des arguments

```javascript
const additionner = (...nombres) => {
  // Vérifier que tous les arguments sont bien des nombres
  if (!nombres.every(n => typeof n === "number")) {
    throw new Error("Tous les arguments doivent être des nombres");
  }

  return nombres.reduce((acc, n) => acc + n, 0);
};

console.log(additionner(1, 2, 3));      // 6
// console.log(additionner(1, "2", 3)); // Erreur !
```

### 3. Gérer le cas vide

```javascript
const calculerMoyenne = (...notes) => {
  if (notes.length === 0) {
    return 0;  // ou null, ou throw une erreur
  }

  const somme = notes.reduce((acc, n) => acc + n, 0);
  return somme / notes.length;
};

console.log(calculerMoyenne());          // 0 (cas géré)
console.log(calculerMoyenne(15, 12, 18)); // 15
```

### 4. Documentation claire

```javascript
/**
 * Additionne tous les nombres passés en arguments
 * @param {...number} nombres - Les nombres à additionner
 * @returns {number} La somme de tous les nombres
 * @example
 * additionner(1, 2, 3) // retourne 6
 * additionner(10, 20) // retourne 30
 */
const additionner = (...nombres) => {
  return nombres.reduce((acc, n) => acc + n, 0);
};
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Rest parameter pas en dernière position

```javascript
// ❌ Erreur de syntaxe
function exemple(...args, dernierParam) { }

// ✅ Correct
function exemple(dernierParam, ...args) { }
```

### ❌ Erreur 2 : Plusieurs rest parameters

```javascript
// ❌ Erreur de syntaxe
function exemple(...args1, ...args2) { }

// ✅ Un seul suffit
function exemple(...args) { }
```

### ❌ Erreur 3 : Confondre rest et spread

```javascript
// Rest : dans les PARAMÈTRES (rassemble)
function func(...args) { }

// Spread : dans les APPELS (disperse)
const arr = [1, 2, 3];
func(...arr);
```

### ❌ Erreur 4 : Oublier que c'est un tableau

```javascript
const afficher = (...items) => {
  // ❌ Oublier que items est un tableau
  console.log(items.toUpperCase());  // Erreur ! Pas de méthode toUpperCase sur les tableaux

  // ✅ Correct : itérer sur le tableau
  items.forEach(item => console.log(item.toUpperCase()));
};
```

## Points clés à retenir

1. **Syntaxe** : `...nomParametre` - les trois points avant le nom

2. **Position** : Doit être le **dernier paramètre**

3. **Résultat** : Un **vrai tableau** JavaScript

4. **Usage** : Capturer un nombre **indéfini d'arguments**

5. **Différence avec arguments** : Plus moderne, plus propre, vrai tableau

6. **Différence avec spread** :
   - Rest = **rassembler** (dans les paramètres)
   - Spread = **disperser** (dans les appels)

7. **Combinaison** : Peut être combiné avec des paramètres normaux

8. **Arrow functions** : Fonctionne parfaitement (contrairement à `arguments`)

## Prochaines étapes

Maintenant que vous maîtrisez les rest parameters, vous êtes prêt pour :

- La **valeur de retour** avec `return` (5.6.7)
- La **portée et le scope** (5.6.8)
- Le **hoisting** (5.6.9)
- Les **callbacks** (5.6.10)

Les rest parameters sont une fonctionnalité ES6 puissante qui rend vos fonctions beaucoup plus flexibles. Vous les verrez fréquemment dans le code JavaScript moderne, notamment dans les bibliothèques et frameworks.

---

**Note :** Les rest parameters sont l'une des améliorations majeures d'ES6 pour les fonctions. Ils remplacent complètement l'ancien objet `arguments` et offrent une solution plus élégante et plus puissante pour gérer un nombre variable d'arguments. Dans le développement moderne, utilisez toujours les rest parameters plutôt que `arguments`.

⏭️ [Valeur de retour (return)](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/07-valeur-retour.md)
