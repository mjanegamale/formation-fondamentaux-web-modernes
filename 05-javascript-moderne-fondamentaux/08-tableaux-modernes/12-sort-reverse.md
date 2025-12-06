🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.12 - Méthodes de tri et réorganisation : sort, reverse

## Introduction

Les méthodes `sort()` et `reverse()` permettent de **réorganiser** les éléments d'un tableau.

⚠️ **Attention importante** : Ces deux méthodes **modifient le tableau original** (mutation).

| Méthode    | Action                        | Modifie l'original ? |
|------------|-------------------------------|----------------------|
| `reverse()`| Inverse l'ordre des éléments  | ✅ OUI               |
| `sort()`   | Trie les éléments             | ✅ OUI               |

---

## reverse() - Inverser l'ordre

La méthode `reverse()` **inverse** l'ordre des éléments dans un tableau.

### Syntaxe

```javascript
tableau.reverse()
```

**Retour** : Le tableau inversé (le même tableau, modifié)

### Utilisation de base

```javascript
const nombres = [1, 2, 3, 4, 5];

nombres.reverse();

console.log(nombres);  // [5, 4, 3, 2, 1]
```

### Avec des chaînes

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.reverse();

console.log(fruits);  // ["orange", "banane", "pomme"]
```

### Visualisation

```
Avant:   [1,  2,  3,  4,  5]
          ↓   ↓   ↓   ↓   ↓
Après:   [5,  4,  3,  2,  1]
```

### Modification du tableau original

```javascript
const original = [1, 2, 3];

const resultat = original.reverse();

console.log(original);  // [3, 2, 1] ⚠️ Modifié !
console.log(resultat);  // [3, 2, 1] (même tableau)
console.log(original === resultat);  // true (même référence)
```

### Version immutable (sans modification)

Si vous voulez préserver l'original, créez d'abord une copie :

```javascript
const original = [1, 2, 3];

const inverse = [...original].reverse();

console.log(original);  // [1, 2, 3] ✅ Intact
console.log(inverse);   // [3, 2, 1]
```

Ou utilisez `toReversed()` (ES2023, très récent) :

```javascript
const original = [1, 2, 3];

const inverse = original.toReversed();

console.log(original);  // [1, 2, 3] ✅ Intact
console.log(inverse);   // [3, 2, 1]
```

> 💡 **Note** : `toReversed()` n'est disponible que dans les navigateurs très récents.

---

## sort() - Trier les éléments

La méthode `sort()` **trie** les éléments d'un tableau.

⚠️ **Attention** : Le comportement par défaut peut être surprenant !

### Syntaxe

```javascript
tableau.sort()                    // Tri lexicographique (alphabétique)
tableau.sort(fonctionComparaison) // Tri personnalisé
```

---

## Tri par défaut (lexicographique)

Par défaut, `sort()` convertit les éléments en **chaînes de caractères** et les trie par ordre **alphabétique** (lexicographique).

### Tri de chaînes

Cela fonctionne bien pour les chaînes :

```javascript
const fruits = ["orange", "pomme", "banane", "kiwi"];

fruits.sort();

console.log(fruits);  // ["banane", "kiwi", "orange", "pomme"]
```

### Problème avec les nombres

⚠️ **Piège** : Le tri par défaut ne fonctionne **pas** correctement avec les nombres !

```javascript
const nombres = [10, 2, 5, 1, 20];

nombres.sort();

console.log(nombres);  // [1, 10, 2, 20, 5] ❌
```

**Pourquoi ?** Parce que `sort()` convertit en chaînes :
- `"1"` vient avant `"10"` (compare le premier caractère)
- `"10"` vient avant `"2"` (compare le premier caractère : "1" < "2")
- `"2"` vient avant `"20"`
- `"20"` vient avant `"5"`

Résultat : `["1", "10", "2", "20", "5"]` en ordre alphabétique !

---

## Fonction de comparaison

Pour trier correctement les nombres (ou personnaliser le tri), utilisez une **fonction de comparaison**.

### Syntaxe de la fonction de comparaison

```javascript
tableau.sort((a, b) => {
  // Retourner :
  // - nombre négatif si a doit venir avant b
  // - 0 si a et b sont égaux (même position)
  // - nombre positif si a doit venir après b
});
```

### Règles simples

| Retour de la fonction | Ordre résultant |
|-----------------------|-----------------|
| `< 0` (négatif)       | a avant b       |
| `0`                   | Pas de changement |
| `> 0` (positif)       | b avant a       |

---

## Trier des nombres

### Ordre croissant

```javascript
const nombres = [10, 2, 5, 1, 20];

nombres.sort((a, b) => a - b);

console.log(nombres);  // [1, 2, 5, 10, 20] ✅
```

**Explication** :
- Si `a < b` : `a - b` est négatif → `a` avant `b` ✅
- Si `a > b` : `a - b` est positif → `b` avant `a` ✅
- Si `a === b` : `a - b` est 0 → pas de changement ✅

### Ordre décroissant

```javascript
const nombres = [10, 2, 5, 1, 20];

nombres.sort((a, b) => b - a);

console.log(nombres);  // [20, 10, 5, 2, 1] ✅
```

### Visualisation étape par étape

```javascript
[10, 2, 5, 1, 20].sort((a, b) => a - b)
```

Comparaisons effectuées :
- `10` vs `2` : `10 - 2 = 8` (positif) → `2` avant `10`
- `10` vs `5` : `10 - 5 = 5` (positif) → `5` avant `10`
- `5` vs `2` : `5 - 2 = 3` (positif) → `2` avant `5`
- ... et ainsi de suite

Résultat final : `[1, 2, 5, 10, 20]`

---

## Trier des chaînes (avec accents)

### Tri alphabétique simple

```javascript
const noms = ["Charlie", "Alice", "Bob"];

noms.sort();

console.log(noms);  // ["Alice", "Bob", "Charlie"]
```

### Tri avec accents et casse

Pour un tri correct des accents et insensible à la casse, utilisez `localeCompare()` :

```javascript
const mots = ["éclair", "zèbre", "Éléphant", "avion"];

// ❌ Tri par défaut (problèmes avec accents et casse)
console.log([...mots].sort());
// ["avion", "zèbre", "éclair", "Éléphant"]

// ✅ Tri avec localeCompare (correct)
mots.sort((a, b) => a.localeCompare(b, "fr"));

console.log(mots);
// ["avion", "éclair", "Éléphant", "zèbre"]
```

### Tri insensible à la casse

```javascript
const noms = ["alice", "Bob", "CHARLIE", "david"];

noms.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));

console.log(noms);  // ["alice", "Bob", "CHARLIE", "david"]
```

---

## Trier des objets

Pour trier un tableau d'objets, comparez une propriété spécifique.

### Trier par une propriété numérique

```javascript
const personnes = [
  { nom: "Alice", age: 30 },
  { nom: "Bob", age: 25 },
  { nom: "Charlie", age: 35 }
];

// Trier par âge croissant
personnes.sort((a, b) => a.age - b.age);

console.log(personnes);
// [
//   { nom: "Bob", age: 25 },
//   { nom: "Alice", age: 30 },
//   { nom: "Charlie", age: 35 }
// ]
```

### Trier par une propriété texte

```javascript
const produits = [
  { nom: "Laptop", prix: 1000 },
  { nom: "Souris", prix: 25 },
  { nom: "Clavier", prix: 75 }
];

// Trier par nom alphabétique
produits.sort((a, b) => a.nom.localeCompare(b.nom));

console.log(produits);
// [
//   { nom: "Clavier", prix: 75 },
//   { nom: "Laptop", prix: 1000 },
//   { nom: "Souris", prix: 25 }
// ]
```

### Tri sur plusieurs critères

Trier d'abord par une propriété, puis par une autre en cas d'égalité :

```javascript
const etudiants = [
  { nom: "Alice", classe: "A", note: 15 },
  { nom: "Bob", classe: "B", note: 18 },
  { nom: "Charlie", classe: "A", note: 18 },
  { nom: "David", classe: "B", note: 15 }
];

// Trier par classe, puis par note décroissante
etudiants.sort((a, b) => {
  // D'abord par classe
  if (a.classe !== b.classe) {
    return a.classe.localeCompare(b.classe);
  }
  // Si même classe, par note décroissante
  return b.note - a.note;
});

console.log(etudiants);
// [
//   { nom: "Charlie", classe: "A", note: 18 },
//   { nom: "Alice", classe: "A", note: 15 },
//   { nom: "Bob", classe: "B", note: 18 },
//   { nom: "David", classe: "B", note: 15 }
// ]
```

---

## Tri stable vs instable

Le tri est dit **stable** si l'ordre relatif des éléments égaux est préservé.

### Exemple de tri stable

```javascript
const personnes = [
  { nom: "Alice", age: 30 },
  { nom: "Bob", age: 25 },
  { nom: "Charlie", age: 30 },  // Même âge qu'Alice
  { nom: "David", age: 25 }     // Même âge que Bob
];

// Tri par âge (stable en JavaScript moderne)
personnes.sort((a, b) => a.age - b.age);

console.log(personnes);
// Alice et Charlie gardent leur ordre relatif (Alice avant Charlie)
// Bob et David gardent leur ordre relatif (Bob avant David)
```

> 💡 **Note** : Depuis ES2019, `sort()` est **garanti stable** en JavaScript.

---

## Version immutable (sans modification)

Si vous voulez préserver l'original, créez une copie avant de trier :

```javascript
const original = [3, 1, 4, 1, 5];

const trie = [...original].sort((a, b) => a - b);

console.log(original);  // [3, 1, 4, 1, 5] ✅ Intact
console.log(trie);      // [1, 1, 3, 4, 5]
```

Ou utilisez `toSorted()` (ES2023, très récent) :

```javascript
const original = [3, 1, 4, 1, 5];

const trie = original.toSorted((a, b) => a - b);

console.log(original);  // [3, 1, 4, 1, 5] ✅ Intact
console.log(trie);      // [1, 1, 3, 4, 5]
```

---

## Exemples pratiques complets

### Exemple 1 : Classement de joueurs

```javascript
const joueurs = [
  { nom: "Alice", score: 1250 },
  { nom: "Bob", score: 980 },
  { nom: "Charlie", score: 1500 },
  { nom: "David", score: 750 }
];

// Trier par score décroissant (meilleurs d'abord)
joueurs.sort((a, b) => b.score - a.score);

console.log("=== CLASSEMENT ===");
joueurs.forEach((j, index) => {
  console.log(`${index + 1}. ${j.nom} - ${j.score} points`);
});
// === CLASSEMENT ===
// 1. Charlie - 1500 points
// 2. Alice - 1250 points
// 3. Bob - 980 points
// 4. David - 750 points
```

### Exemple 2 : Tri de produits par prix

```javascript
const produits = [
  { nom: "Laptop", prix: 1000, categorie: "Électronique" },
  { nom: "Souris", prix: 25, categorie: "Électronique" },
  { nom: "Bureau", prix: 300, categorie: "Mobilier" },
  { nom: "Chaise", prix: 150, categorie: "Mobilier" }
];

// Créer une copie triée par prix croissant
const parPrix = [...produits].sort((a, b) => a.prix - b.prix);

console.log("Du moins cher au plus cher :");
parPrix.forEach(p => console.log(`${p.nom} : ${p.prix}€`));
// Souris : 25€
// Chaise : 150€
// Bureau : 300€
// Laptop : 1000€

// Trier par catégorie puis par prix
const parCatPrix = [...produits].sort((a, b) => {
  if (a.categorie !== b.categorie) {
    return a.categorie.localeCompare(b.categorie);
  }
  return a.prix - b.prix;
});

console.log("\nPar catégorie puis prix :");
parCatPrix.forEach(p =>
  console.log(`[${p.categorie}] ${p.nom} : ${p.prix}€`)
);
```

### Exemple 3 : Tri de dates

```javascript
const evenements = [
  { nom: "Réunion", date: new Date("2025-03-15") },
  { nom: "Conférence", date: new Date("2025-01-10") },
  { nom: "Formation", date: new Date("2025-02-20") }
];

// Trier par date (plus récent d'abord)
evenements.sort((a, b) => b.date - a.date);

evenements.forEach(e => {
  console.log(`${e.nom} : ${e.date.toLocaleDateString("fr-FR")}`);
});
// Réunion : 15/03/2025
// Formation : 20/02/2025
// Conférence : 10/01/2025
```

### Exemple 4 : Tri alphanumérique

```javascript
const versions = ["v1.10", "v1.2", "v1.1", "v2.0", "v1.20"];

// Tri naturel (alphanumérique)
versions.sort((a, b) => {
  return a.localeCompare(b, undefined, { numeric: true });
});

console.log(versions);
// ["v1.1", "v1.2", "v1.10", "v1.20", "v2.0"]
```

### Exemple 5 : Mélanger un tableau (shuffle)

```javascript
const cartes = ["As", "Roi", "Dame", "Valet", "10", "9", "8", "7"];

// Mélanger aléatoirement
const melange = [...cartes].sort(() => Math.random() - 0.5);

console.log(melange);
// Ordre aléatoire à chaque exécution
```

> ⚠️ **Note** : Cette méthode n'est pas parfaitement aléatoire. Pour un vrai mélange, utilisez l'algorithme de Fisher-Yates.

### Exemple 6 : Afficher dans l'ordre inverse

```javascript
const taches = [
  "Réviser le code",
  "Écrire les tests",
  "Déployer",
  "Documenter"
];

// Afficher dans l'ordre inverse sans modifier l'original
console.log("Ordre inverse :");
[...taches].reverse().forEach((t, i) => {
  console.log(`${i + 1}. ${t}`);
});

console.log("\nOrdre original intact :");
taches.forEach((t, i) => {
  console.log(`${i + 1}. ${t}`);
});
```

---

## Chaîner sort() et reverse()

Vous pouvez combiner ces méthodes :

```javascript
const nombres = [3, 1, 4, 1, 5, 9, 2, 6];

// Trier par ordre croissant, puis inverser
const decroissant = [...nombres]
  .sort((a, b) => a - b)
  .reverse();

console.log(decroissant);  // [9, 6, 5, 4, 3, 2, 1, 1]
```

Mais c'est plus simple de trier directement en décroissant :

```javascript
const decroissant = [...nombres].sort((a, b) => b - a);
```

---

## Erreurs courantes et pièges

### ❌ Oublier la fonction de comparaison pour les nombres

```javascript
const nombres = [10, 2, 5, 1, 20];

// ❌ Tri alphabétique
nombres.sort();
console.log(nombres);  // [1, 10, 2, 20, 5]

// ✅ Tri numérique
nombres.sort((a, b) => a - b);
console.log(nombres);  // [1, 2, 5, 10, 20]
```

### ❌ Oublier que sort() modifie l'original

```javascript
const original = [3, 1, 2];

const trie = original.sort((a, b) => a - b);

console.log(original);  // [1, 2, 3] ⚠️ Modifié !
console.log(trie);      // [1, 2, 3]

// ✅ Créer une copie d'abord
const original2 = [3, 1, 2];
const trie2 = [...original2].sort((a, b) => a - b);
console.log(original2);  // [3, 1, 2] ✅ Intact
```

### ❌ Fonction de comparaison incorrecte

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Retourne booléen au lieu de nombre
nombres.sort((a, b) => a > b);  // Comportement imprévisible

// ✅ Retourner un nombre
nombres.sort((a, b) => a - b);
```

### ❌ Modifier les éléments pendant le tri

```javascript
const objets = [{ val: 3 }, { val: 1 }, { val: 2 }];

// ❌ Ne pas modifier pendant le tri
objets.sort((a, b) => {
  a.val += 10;  // ⚠️ Modification pendant le tri !
  return a.val - b.val;
});

// ✅ Juste comparer
objets.sort((a, b) => a.val - b.val);
```

### ❌ Comparer des valeurs null/undefined

```javascript
const valeurs = [3, null, 1, undefined, 2];

// ❌ Crash potentiel
valeurs.sort((a, b) => a - b);  // NaN - NaN

// ✅ Gérer les valeurs spéciales
valeurs.sort((a, b) => {
  if (a == null) return 1;   // null/undefined à la fin
  if (b == null) return -1;
  return a - b;
});
```

---

## Performances

### Complexité algorithmique

Les moteurs JavaScript modernes utilisent des algorithmes efficaces :
- **Complexité** : O(n log n) en moyenne
- **Algorithme** : Généralement Timsort (hybride)

### sort() est optimisé

Ne vous inquiétez pas trop des performances de `sort()` pour des tableaux de taille raisonnable (< 10,000 éléments).

```javascript
const grand = Array(10000).fill(0).map(() => Math.random());

console.time("sort");
grand.sort((a, b) => a - b);
console.timeEnd("sort");  // Très rapide (quelques ms)
```

---

## Alternatives et méthodes connexes

### Tri partiel (top N)

Si vous n'avez besoin que des N premiers éléments triés :

```javascript
const nombres = [10, 2, 5, 1, 20, 15, 8];

// Top 3 uniquement
const top3 = nombres
  .sort((a, b) => b - a)
  .slice(0, 3);

console.log(top3);  // [20, 15, 10]
```

### Lodash sortBy

La bibliothèque Lodash offre une méthode plus simple :

```javascript
// Avec Lodash
const trie = _.sortBy(personnes, ["age", "nom"]);

// Sans Lodash (équivalent)
const trie = [...personnes].sort((a, b) => {
  if (a.age !== b.age) return a.age - b.age;
  return a.nom.localeCompare(b.nom);
});
```

---

## Méthodes récentes (ES2023)

### toSorted() et toReversed()

Ces nouvelles méthodes retournent un **nouveau tableau** sans modifier l'original :

```javascript
const original = [3, 1, 2];

// Méthodes immutables (ES2023)
const trie = original.toSorted((a, b) => a - b);
const inverse = original.toReversed();

console.log(original);  // [3, 1, 2] ✅ Intact
console.log(trie);      // [1, 2, 3]
console.log(inverse);   // [2, 1, 3]
```

> ⚠️ **Compatibilité** : Vérifiez le support navigateur. Utilisez un polyfill si nécessaire.

---

## Points clés à retenir

- ✅ **reverse()** : inverse l'ordre → modifie l'original
- ✅ **sort()** : trie les éléments → modifie l'original
- ✅ sort() par défaut = tri **lexicographique** (alphabétique)
- ✅ Pour trier des nombres : `sort((a, b) => a - b)`
- ✅ Fonction de comparaison : retourner négatif, 0, ou positif
- ✅ Ordre croissant : `a - b`, décroissant : `b - a`
- ✅ Pour objets : comparer une propriété spécifique
- ✅ Créer une copie avec `[...tableau]` pour éviter mutation
- ✅ sort() est **stable** depuis ES2019
- ✅ Nouvelles méthodes immutables : `toSorted()`, `toReversed()` (ES2023)

---

## Bonnes pratiques

- ✅ Créez une **copie** si vous voulez préserver l'original
- ✅ Utilisez toujours une **fonction de comparaison** pour les nombres
- ✅ Pour les chaînes avec accents, utilisez **localeCompare()**
- ✅ Pour trier sur plusieurs critères, testez d'abord le premier, puis le suivant
- ✅ Nommez clairement vos fonctions de tri complexes
- ✅ Testez vos tris avec des cas limites (null, undefined, égalités)
- ✅ Documentez les tris complexes avec des commentaires

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez les méthodes de combinaison : `concat()` et `join()`, pour fusionner et convertir des tableaux.

---


⏭️ [Méthodes de combinaison : concat, join](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/13-concat-join.md)
