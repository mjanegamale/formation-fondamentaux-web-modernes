🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.9 - indexOf et lastIndexOf (legacy mais toujours utilisé)

## Introduction

Les méthodes `indexOf()` et `lastIndexOf()` sont des **méthodes classiques** de recherche dans les tableaux. Bien qu'elles existent depuis longtemps (avant ES6), elles restent **largement utilisées** et parfaitement valides.

### Pourquoi "legacy" ?

Ces méthodes sont considérées comme "legacy" (anciennes) car :
- Elles ont été introduites avant ES6
- Les nouvelles méthodes comme `includes()`, `find()`, et `findIndex()` sont souvent plus puissantes
- Elles ont quelques limitations (ne trouvent pas `NaN`, pas de recherche par condition)

### Pourquoi toujours utilisées ?

Malgré cela, elles restent très populaires car :
- ✅ Elles sont simples et rapides
- ✅ Parfaites pour des recherches de valeurs exactes
- ✅ Compatibles avec tous les navigateurs (même très anciens)
- ✅ Moins de code pour des cas simples

---

## indexOf() - Trouver la première occurrence

La méthode `indexOf()` retourne l'**index de la première occurrence** d'une valeur dans un tableau.

### Syntaxe

```javascript
tableau.indexOf(valeurCherchee, indexDebut)
```

**Paramètres** :
- `valeurCherchee` : La valeur à rechercher
- `indexDebut` : Position de départ (optionnel, défaut : 0)

**Retour** : L'index de l'élément trouvé, ou `-1` si non trouvé

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];

console.log(fruits.indexOf("orange"));  // 2
console.log(fruits.indexOf("mangue"));  // -1 (non trouvé)
```

### Avec différents types de données

```javascript
const nombres = [10, 20, 30, 40, 50];
console.log(nombres.indexOf(30));  // 2
console.log(nombres.indexOf(100)); // -1

const booleens = [true, false, true, false];
console.log(booleens.indexOf(false));  // 1
```

### Avec un index de départ

```javascript
const lettres = ["a", "b", "c", "b", "d"];

// Chercher "b" depuis le début
console.log(lettres.indexOf("b"));     // 1

// Chercher "b" à partir de l'index 2
console.log(lettres.indexOf("b", 2));  // 3
```

### Avec des index négatifs

Les index négatifs comptent depuis la fin :

```javascript
const nombres = [1, 2, 3, 4, 5];

// Chercher 4 en commençant 2 positions avant la fin
console.log(nombres.indexOf(4, -2));  // 3
```

---

## lastIndexOf() - Trouver la dernière occurrence

La méthode `lastIndexOf()` retourne l'**index de la dernière occurrence** d'une valeur dans un tableau. Elle effectue la recherche **de la fin vers le début**.

### Syntaxe

```javascript
tableau.lastIndexOf(valeurCherchee, indexDebut)
```

**Paramètres** :
- `valeurCherchee` : La valeur à rechercher
- `indexDebut` : Position de départ (depuis la fin, optionnel, défaut : longueur-1)

**Retour** : L'index de l'élément trouvé, ou `-1` si non trouvé

### Utilisation de base

```javascript
const lettres = ["a", "b", "c", "b", "d"];

console.log(lettres.lastIndexOf("b"));  // 3 (dernière occurrence)
console.log(lettres.indexOf("b"));      // 1 (première occurrence)
```

### Différence avec indexOf()

```javascript
const nombres = [5, 10, 15, 10, 20, 10];

console.log(nombres.indexOf(10));      // 1 (premier 10)
console.log(nombres.lastIndexOf(10));  // 5 (dernier 10)
```

### Avec un index de départ

Le deuxième paramètre définit où **arrêter** la recherche (en partant de la fin) :

```javascript
const lettres = ["a", "b", "c", "b", "d", "b"];
//              0    1    2    3    4    5

// Chercher "b" en partant de la fin jusqu'à l'index 3 (inclus)
console.log(lettres.lastIndexOf("b", 3));  // 3

// Chercher "b" en partant de la fin jusqu'à l'index 2 (inclus)
console.log(lettres.lastIndexOf("b", 2));  // 1
```

### Recherche de la fin vers le début

```javascript
const nombres = [1, 2, 3, 2, 1];

// lastIndexOf cherche de droite à gauche
console.log(nombres.lastIndexOf(2));  // 3 (le dernier 2)
console.log(nombres.lastIndexOf(1));  // 4 (le dernier 1)
```

---

## Vérifier la présence d'un élément

### Méthode classique avec indexOf()

```javascript
const fruits = ["pomme", "banane", "orange"];

// Vérifier si "banane" existe
if (fruits.indexOf("banane") !== -1) {
  console.log("Banane trouvée !");
}

// Vérifier si "kiwi" n'existe pas
if (fruits.indexOf("kiwi") === -1) {
  console.log("Pas de kiwi");
}
```

### Comparaison avec includes() (moderne)

```javascript
const fruits = ["pomme", "banane", "orange"];

// Méthode classique
if (fruits.indexOf("banane") !== -1) {
  console.log("Banane trouvée !");
}

// Méthode moderne (plus lisible)
if (fruits.includes("banane")) {
  console.log("Banane trouvée !");
}
```

> 💡 **Conseil** : Pour simplement vérifier l'existence, préférez `includes()` qui est plus explicite.

---

## Cas d'usage pratiques

### Exemple 1 : Supprimer un élément spécifique

```javascript
const taches = ["Courses", "Ménage", "Cuisine", "Lessive"];

const aSuppprimer = "Ménage";
const index = taches.indexOf(aSuppprimer);

if (index !== -1) {
  taches.splice(index, 1);
}

console.log(taches);  // ["Courses", "Cuisine", "Lessive"]
```

### Exemple 2 : Compter les occurrences

```javascript
const notes = [4, 5, 4, 3, 5, 4, 2];

function compterOccurrences(tableau, valeur) {
  let count = 0;
  let index = tableau.indexOf(valeur);

  while (index !== -1) {
    count++;
    index = tableau.indexOf(valeur, index + 1);
  }

  return count;
}

console.log(compterOccurrences(notes, 4));  // 3
console.log(compterOccurrences(notes, 5));  // 2
```

### Exemple 3 : Trouver tous les index d'une valeur

```javascript
const lettres = ["a", "b", "c", "b", "d", "b"];

function trouverTousLesIndex(tableau, valeur) {
  const indexes = [];
  let index = tableau.indexOf(valeur);

  while (index !== -1) {
    indexes.push(index);
    index = tableau.indexOf(valeur, index + 1);
  }

  return indexes;
}

console.log(trouverTousLesIndex(lettres, "b"));  // [1, 3, 5]
```

### Exemple 4 : Vérifier l'ordre d'apparition

```javascript
const etapes = ["Connexion", "Navigation", "Achat", "Paiement"];

const indexNavigation = etapes.indexOf("Navigation");
const indexAchat = etapes.indexOf("Achat");

if (indexNavigation < indexAchat) {
  console.log("L'utilisateur a navigué avant d'acheter");
}
```

### Exemple 5 : Détecter les doublons

```javascript
const ids = [101, 102, 103, 104, 102];

function aDesDoublons(tableau) {
  for (let i = 0; i < tableau.length; i++) {
    // Si indexOf trouve l'élément à un index différent, c'est un doublon
    if (tableau.indexOf(tableau[i]) !== i) {
      return true;
    }
  }
  return false;
}

console.log(aDesDoublons(ids));  // true (102 apparaît deux fois)
```

### Exemple 6 : Remplacer toutes les occurrences

```javascript
const fruits = ["pomme", "banane", "pomme", "orange", "pomme"];

function remplacerTous(tableau, ancienne, nouvelle) {
  let index = tableau.indexOf(ancienne);

  while (index !== -1) {
    tableau[index] = nouvelle;
    index = tableau.indexOf(ancienne, index + 1);
  }
}

remplacerTous(fruits, "pomme", "poire");
console.log(fruits);
// ["poire", "banane", "poire", "orange", "poire"]
```

---

## Comparaison stricte (===)

Les deux méthodes utilisent une **comparaison stricte** (`===`) :

```javascript
const nombres = [1, 2, 3, 4, 5];

console.log(nombres.indexOf(3));    // 2 (trouvé)
console.log(nombres.indexOf("3"));  // -1 (type différent)

const melange = [1, "2", 3];
console.log(melange.indexOf(2));    // -1 (cherche number, trouve string)
console.log(melange.indexOf("2"));  // 1 (cherche string, trouve string)
```

---

## Limitations importantes

### 1. Ne trouve pas NaN

⚠️ **Problème majeur** : `indexOf()` ne peut pas détecter `NaN` :

```javascript
const valeurs = [1, 2, NaN, 4];

console.log(valeurs.indexOf(NaN));      // -1 ❌ (ne trouve pas)
console.log(valeurs.includes(NaN));     // true ✅ (trouve)
```

**Pourquoi ?** Parce que `NaN === NaN` retourne `false` en JavaScript.

### 2. Pas de recherche par condition

Vous ne pouvez chercher que des **valeurs exactes**, pas par condition :

```javascript
const nombres = [5, 12, 8, 130, 44];

// ❌ Impossible avec indexOf()
// Chercher le premier nombre > 10

// ✅ Utilisez find() ou findIndex()
const resultat = nombres.find(n => n > 10);       // 12
const index = nombres.findIndex(n => n > 10);     // 1
```

### 3. Pas pratique pour les objets

Pour chercher dans un tableau d'objets, `indexOf()` n'est pas adapté :

```javascript
const users = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" }
];

// ❌ Ne fonctionne pas (comparaison par référence)
const bob = { id: 2, nom: "Bob" };
console.log(users.indexOf(bob));  // -1 (objet différent en mémoire)

// ✅ Utilisez find() ou findIndex()
const index = users.findIndex(u => u.id === 2);  // 1
```

---

## Comparaison avec les méthodes modernes

### indexOf() vs includes()

| Critère          | indexOf()              | includes()            |
|------------------|------------------------|-----------------------|
| Retourne         | Index ou `-1`          | `true` ou `false`     |
| Intention        | Trouver la position    | Vérifier l'existence  |
| Lisibilité       | Moins claire           | Plus claire           |
| Détecte NaN      | ❌ Non                  | ✅ Oui                |
| Support          | Très ancien            | ES7 (2016)            |

```javascript
const fruits = ["pomme", "banane", "orange"];

// indexOf() - si vous avez besoin de la position
const position = fruits.indexOf("banane");
if (position !== -1) {
  console.log(`Trouvé à l'index ${position}`);
}

// includes() - si vous voulez juste vérifier
if (fruits.includes("banane")) {
  console.log("Banane disponible");
}
```

### indexOf() vs findIndex()

| Critère          | indexOf()              | findIndex()           |
|------------------|------------------------|-----------------------|
| Recherche        | Valeur exacte          | Par condition         |
| Flexibilité      | Limitée                | Très flexible         |
| Avec objets      | Difficile              | Facile                |
| Performance      | Plus rapide (simple)   | Légèrement plus lent  |

```javascript
const nombres = [5, 12, 8, 130, 44];

// indexOf() - valeur exacte uniquement
console.log(nombres.indexOf(12));  // 1

// findIndex() - recherche par condition
console.log(nombres.findIndex(n => n > 10));  // 1 (trouve 12)
console.log(nombres.findIndex(n => n > 100)); // 3 (trouve 130)
```

---

## Quand utiliser indexOf() et lastIndexOf() ?

### ✅ Utilisez indexOf() et lastIndexOf() quand :

- Vous cherchez une **valeur exacte** (nombre, chaîne, booléen)
- Vous avez besoin de la **position** de l'élément
- Vous voulez **compter les occurrences**
- Vous travaillez avec des **tableaux simples** (pas d'objets)
- Vous avez besoin d'une **compatibilité maximale** avec de vieux navigateurs
- Les performances sont critiques (plus rapides que find/findIndex)

### ❌ Évitez-les quand :

- Vous cherchez `NaN` → utilisez `includes()`
- Vous voulez juste vérifier l'existence → utilisez `includes()`
- Vous cherchez par condition → utilisez `find()` ou `findIndex()`
- Vous travaillez avec des objets → utilisez `find()` ou `findIndex()`

---

## Exemples de migration vers les méthodes modernes

### Vérification d'existence

**Ancien style** :
```javascript
if (tableau.indexOf(valeur) !== -1) {
  // Trouvé
}
```

**Style moderne** :
```javascript
if (tableau.includes(valeur)) {
  // Trouvé
}
```

### Recherche dans des objets

**Ancien style** (compliqué) :
```javascript
const users = [{ id: 1 }, { id: 2 }, { id: 3 }];

let index = -1;
for (let i = 0; i < users.length; i++) {
  if (users[i].id === 2) {
    index = i;
    break;
  }
}
```

**Style moderne** (simple) :
```javascript
const users = [{ id: 1 }, { id: 2 }, { id: 3 }];

const index = users.findIndex(u => u.id === 2);
```

---

## Erreurs courantes et pièges

### ❌ Oublier de vérifier -1

```javascript
const fruits = ["pomme", "banane"];

const index = fruits.indexOf("orange");
console.log(fruits[index]);  // undefined (index = -1)

// ✅ Vérifier d'abord
if (index !== -1) {
  console.log(fruits[index]);
}
```

### ❌ Utiliser if (index) au lieu de if (index !== -1)

```javascript
const fruits = ["pomme", "banane", "orange"];

const index = fruits.indexOf("pomme");  // 0

// ❌ Mauvais : 0 est falsy !
if (index) {
  console.log("Trouvé");  // Ne s'exécute pas !
}

// ✅ Correct
if (index !== -1) {
  console.log("Trouvé");  // S'exécute
}
```

### ❌ Confusion entre indexOf() et includes()

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Erreur : indexOf() retourne un nombre, pas un booléen
if (nombres.indexOf(3)) {  // 2 (truthy) ✅ mais logique floue
  console.log("Trouvé");
}

if (nombres.indexOf(1)) {  // 0 (falsy) ❌ faux négatif !
  console.log("Trouvé");   // Ne s'exécute pas !
}

// ✅ Correct avec includes()
if (nombres.includes(3)) {
  console.log("Trouvé");
}
```

### ❌ Chercher des objets par référence

```javascript
const objets = [{ id: 1 }, { id: 2 }];

console.log(objets.indexOf({ id: 1 }));  // -1 ❌
// Chaque {} crée un nouvel objet en mémoire

// ✅ Solution : findIndex()
console.log(objets.findIndex(obj => obj.id === 1));  // 0
```

---

## Performances

### indexOf() et lastIndexOf() sont rapides

Ces méthodes sont **optimisées** dans les moteurs JavaScript modernes :

```javascript
const grand = Array(1000000).fill(0).map((_, i) => i);

console.time("indexOf");
grand.indexOf(999999);
console.timeEnd("indexOf");  // Très rapide (< 1ms)
```

### Comparaison de performance

Pour des recherches simples de valeurs :
1. **indexOf()** : Le plus rapide ⚡
2. **includes()** : Légèrement plus lent
3. **findIndex()** : Plus lent (fonction callback)

> 💡 **Conseil** : La différence est négligeable dans la plupart des cas. Privilégiez la lisibilité !

---

## Points clés à retenir

- ✅ **indexOf()** : trouve la **première** occurrence → retourne l'index ou `-1`
- ✅ **lastIndexOf()** : trouve la **dernière** occurrence → retourne l'index ou `-1`
- ✅ Les deux utilisent une **comparaison stricte** (`===`)
- ✅ Retournent `-1` si l'élément n'est **pas trouvé**
- ✅ Ne peuvent **pas détecter** `NaN`
- ✅ Ne permettent **pas** de recherche par condition
- ✅ Toujours vérifier que l'index `!== -1` avant utilisation
- ✅ Méthodes **classiques** mais toujours **valides et utiles**
- ✅ Pour vérifier l'existence seulement, préférez `includes()`
- ✅ Pour chercher par condition, préférez `find()` ou `findIndex()`

---

## Bonnes pratiques

- ✅ Utilisez `indexOf()` pour trouver la position d'une valeur exacte
- ✅ Vérifiez toujours le résultat avec `!== -1` (pas juste `if (index)`)
- ✅ Pour vérifier l'existence, préférez `includes()` (plus lisible)
- ✅ Pour des objets, utilisez `findIndex()` avec une condition
- ✅ `lastIndexOf()` est utile pour trouver la dernière occurrence
- ✅ Ces méthodes restent parfaitement valides dans du code moderne

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez les **méthodes de transformation** puissantes : `map()`, `filter()` et `reduce()`, qui sont au cœur de la programmation fonctionnelle moderne en JavaScript.

---


⏭️ [Méthodes de transformation : map, filter, reduce](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/10-map-filter-reduce.md)
