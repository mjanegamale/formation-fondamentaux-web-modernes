🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.4 - Boucle for...of (moderne, pour les tableaux) 🆕

## Introduction

La boucle `for...of` est une fonctionnalité moderne introduite avec ES6 (2015) qui simplifie grandement le parcours de tableaux et d'autres structures de données. Elle est plus lisible et moins sujette aux erreurs que la boucle `for` classique.

**En résumé :** `for...of` permet de parcourir directement les **valeurs** d'un tableau, sans se soucier des indices.

---

## Comparaison : `for` classique vs `for...of`

### Avec la boucle `for` classique

```javascript
const fruits = ["pomme", "banane", "orange"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

**Inconvénients :**
- Besoin de gérer l'index `i`
- Risque d'erreur avec `fruits.length`
- Plus verbeux

### Avec la boucle `for...of` (moderne) 🆕

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

**Avantages :**
- ✅ Plus simple et lisible
- ✅ Pas de gestion d'index
- ✅ Moins de risque d'erreurs
- ✅ Code plus moderne

**Résultat (identique) :**
```
pomme
banane
orange
```

---

## Syntaxe de base

```javascript
for (const element of tableau) {
  // Code à exécuter pour chaque élément
}
```

### Les éléments clés

- **`const element`** : Variable qui contient la valeur actuelle (vous pouvez la nommer comme vous voulez)
- **`of`** : Mot-clé qui signifie "dans" ou "de"
- **`tableau`** : Le tableau à parcourir

**Note :** Utilisez `const` si vous ne modifiez pas la variable, `let` si vous devez la modifier.

---

## Exemples de base

### Parcourir un tableau de nombres

```javascript
const nombres = [10, 20, 30, 40, 50];

for (const nombre of nombres) {
  console.log(nombre);
}
```

**Résultat :**
```
10
20
30
40
50
```

### Parcourir un tableau de strings

```javascript
const villes = ["Paris", "Lyon", "Marseille", "Toulouse"];

for (const ville of villes) {
  console.log(`J'aime ${ville}`);
}
```

**Résultat :**
```
J'aime Paris
J'aime Lyon
J'aime Marseille
J'aime Toulouse
```

### Parcourir un tableau d'objets

```javascript
const etudiants = [
  { nom: "Alice", age: 20 },
  { nom: "Bob", age: 22 },
  { nom: "Charlie", age: 21 }
];

for (const etudiant of etudiants) {
  console.log(`${etudiant.nom} a ${etudiant.age} ans`);
}
```

**Résultat :**
```
Alice a 20 ans
Bob a 22 ans
Charlie a 21 ans
```

---

## Utiliser `const` vs `let`

### Avec `const` (recommandé si vous ne modifiez pas la variable)

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const fruit of fruits) {
  console.log(fruit.toUpperCase());
}
// POMME, BANANE, ORANGE
```

### Avec `let` (si vous devez modifier la variable)

```javascript
const nombres = [1, 2, 3, 4, 5];

for (let nombre of nombres) {
  nombre = nombre * 2; // Modification locale
  console.log(nombre);
}
// 2, 4, 6, 8, 10

// Note : le tableau original n'est pas modifié !
console.log(nombres); // [1, 2, 3, 4, 5]
```

**Important :** Modifier la variable de boucle ne modifie **pas** le tableau original. Pour modifier le tableau, utilisez la méthode `map()` ou une boucle `for` classique avec l'index.

---

## Calculer avec `for...of`

### Calculer une somme

```javascript
const prix = [15.99, 22.50, 8.75, 12.00];
let total = 0;

for (const p of prix) {
  total += p;
}

console.log(`Total : ${total.toFixed(2)}€`);
// Total : 59.24€
```

### Trouver le maximum

```javascript
const temperatures = [18, 25, 22, 30, 19, 28];
let max = temperatures[0];

for (const temp of temperatures) {
  if (temp > max) {
    max = temp;
  }
}

console.log(`Température maximale : ${max}°C`);
// Température maximale : 30°C
```

### Compter des éléments spécifiques

```javascript
const notes = [12, 15, 8, 18, 10, 16, 14];
let bonnesNotes = 0;

for (const note of notes) {
  if (note >= 15) {
    bonnesNotes++;
  }
}

console.log(`Nombre de notes ≥ 15 : ${bonnesNotes}`);
// Nombre de notes ≥ 15 : 3
```

---

## Créer un nouveau tableau

Pour créer un nouveau tableau basé sur un existant, vous pouvez combiner `for...of` avec `push()`.

### Transformer des valeurs

```javascript
const prenoms = ["alice", "bob", "charlie"];
const prenomsCapitalises = [];

for (const prenom of prenoms) {
  const capitalise = prenom[0].toUpperCase() + prenom.slice(1);
  prenomsCapitalises.push(capitalise);
}

console.log(prenomsCapitalises);
// ["Alice", "Bob", "Charlie"]
```

**Note moderne :** Pour ce genre de transformation, la méthode `map()` est encore plus appropriée (nous la verrons plus tard).

### Filtrer des éléments

```javascript
const nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const pairs = [];

for (const nombre of nombres) {
  if (nombre % 2 === 0) {
    pairs.push(nombre);
  }
}

console.log(pairs);
// [2, 4, 6, 8, 10]
```

**Note moderne :** Pour le filtrage, la méthode `filter()` est plus appropriée.

---

## Parcourir d'autres structures itérables

### Parcourir une chaîne de caractères (string)

Oui, `for...of` fonctionne aussi avec les strings ! Chaque caractère devient une valeur.

```javascript
const mot = "Bonjour";

for (const lettre of mot) {
  console.log(lettre);
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

### Compter les voyelles dans une chaîne

```javascript
const phrase = "JavaScript est génial";
const voyelles = "aeiouAEIOU";
let compteur = 0;

for (const caractere of phrase) {
  if (voyelles.includes(caractere)) {
    compteur++;
  }
}

console.log(`Nombre de voyelles : ${compteur}`);
// Nombre de voyelles : 8
```

### Parcourir un Set (ensemble)

```javascript
const couleurs = new Set(["rouge", "bleu", "vert", "rouge", "jaune"]);

for (const couleur of couleurs) {
  console.log(couleur);
}
```

**Résultat :**
```
rouge
bleu
vert
jaune
```

**Note :** Le Set élimine automatiquement les doublons.

### Parcourir une Map (dictionnaire)

```javascript
const ages = new Map([
  ["Alice", 25],
  ["Bob", 30],
  ["Charlie", 28]
]);

for (const [nom, age] of ages) {
  console.log(`${nom} : ${age} ans`);
}
```

**Résultat :**
```
Alice : 25 ans
Bob : 30 ans
Charlie : 28 ans
```

---

## Contrôle de flux : `break` et `continue`

Comme avec la boucle `for` classique, vous pouvez utiliser `break` et `continue`.

### `break` : Sortir de la boucle

```javascript
const nombres = [5, 12, 8, 130, 44];

for (const nombre of nombres) {
  if (nombre > 100) {
    console.log(`Trouvé un nombre > 100 : ${nombre}`);
    break; // On arrête la boucle
  }
}
// Trouvé un nombre > 100 : 130
```

### Rechercher un élément

```javascript
const produits = ["ordinateur", "souris", "clavier", "écran"];
const recherche = "clavier";
let trouve = false;

for (const produit of produits) {
  if (produit === recherche) {
    console.log(`✅ ${recherche} trouvé`);
    trouve = true;
    break;
  }
}

if (!trouve) {
  console.log(`❌ ${recherche} non trouvé`);
}
```

### `continue` : Passer à l'itération suivante

```javascript
const nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

for (const nombre of nombres) {
  if (nombre % 2 !== 0) {
    continue; // Saute les nombres impairs
  }
  console.log(nombre);
}
// Affiche : 2, 4, 6, 8, 10
```

---

## Obtenir l'index avec `for...of`

Si vous avez besoin de l'index, vous pouvez utiliser la méthode `entries()`.

### Avec `entries()`

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const [index, fruit] of fruits.entries()) {
  console.log(`${index} : ${fruit}`);
}
```

**Résultat :**
```
0 : pomme
1 : banane
2 : orange
```

**Explication :** `entries()` retourne des paires `[index, valeur]` que l'on déstructure.

### Exemple avec numérotation à partir de 1

```javascript
const taches = ["Faire les courses", "Laver la voiture", "Étudier JavaScript"];

for (const [index, tache] of taches.entries()) {
  console.log(`${index + 1}. ${tache}`);
}
```

**Résultat :**
```
1. Faire les courses
2. Laver la voiture
3. Étudier JavaScript
```

---

## Quand utiliser `for...of` ?

### ✅ Utilisez `for...of` quand :

- Vous voulez **parcourir toutes les valeurs** d'un tableau
- Vous n'avez **pas besoin de l'index**
- Vous voulez un code **simple et lisible**
- Vous travaillez avec des **strings, Sets, ou Maps**

### ❌ N'utilisez PAS `for...of` quand :

- Vous devez **modifier le tableau** en place (utilisez `for` classique)
- Vous avez besoin de l'index pour des calculs complexes
- Vous voulez parcourir dans un ordre personnalisé (à l'envers, de 2 en 2, etc.)

---

## `for...of` vs `for...in` : Attention à la confusion ! ⚠️

### `for...of` : Pour les valeurs (tableaux, strings, etc.)

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
// pomme, banane, orange
```

### `for...in` : Pour les clés/propriétés (objets)

```javascript
const personne = { nom: "Alice", age: 25, ville: "Paris" };

for (const cle in personne) {
  console.log(`${cle} : ${personne[cle]}`);
}
// nom : Alice
// age : 25
// ville : Paris
```

### ⚠️ Erreur fréquente : Utiliser `for...in` sur un tableau

```javascript
const fruits = ["pomme", "banane", "orange"];

// ❌ Évitez ceci avec les tableaux
for (const index in fruits) {
  console.log(index); // Affiche 0, 1, 2 (les indices, pas les valeurs !)
}

// ✅ Préférez ceci
for (const fruit of fruits) {
  console.log(fruit); // Affiche pomme, banane, orange
}
```

**Règle simple :**
- **`for...of`** → Tableaux, strings, Sets, Maps (les **valeurs**)
- **`for...in`** → Objets (les **clés**)

---

## Exemples pratiques

### Exemple 1 : Validation de formulaire

```javascript
const champsSaisis = ["alice@email.com", "secret123", "", "Paris"];
const nomsChamps = ["Email", "Mot de passe", "Téléphone", "Ville"];
let tousRemplis = true;

for (const [index, valeur] of champsSaisis.entries()) {
  if (valeur === "") {
    console.log(`❌ Le champ "${nomsChamps[index]}" est vide`);
    tousRemplis = false;
  }
}

if (tousRemplis) {
  console.log("✅ Tous les champs sont remplis");
}
```

### Exemple 2 : Calcul de statistiques

```javascript
const notes = [15, 12, 18, 10, 16, 14, 17];
let somme = 0;
let min = notes[0];
let max = notes[0];

for (const note of notes) {
  somme += note;
  if (note < min) min = note;
  if (note > max) max = note;
}

const moyenne = somme / notes.length;

console.log(`Moyenne : ${moyenne.toFixed(2)}`);
console.log(`Note minimum : ${min}`);
console.log(`Note maximum : ${max}`);
```

**Résultat :**
```
Moyenne : 14.57
Note minimum : 10
Note maximum : 18
```

### Exemple 3 : Génération de liste HTML

```javascript
const produits = [
  { nom: "Ordinateur", prix: 899 },
  { nom: "Souris", prix: 25 },
  { nom: "Clavier", prix: 75 }
];

let html = "<ul>";

for (const produit of produits) {
  html += `<li>${produit.nom} - ${produit.prix}€</li>`;
}

html += "</ul>";

console.log(html);
```

**Résultat :**
```html
<ul><li>Ordinateur - 899€</li><li>Souris - 25€</li><li>Clavier - 75€</li></ul>
```

### Exemple 4 : Nettoyage de données

```javascript
const emails = [
  "  alice@email.com  ",
  "BOB@EMAIL.COM",
  "  charlie@email.com"
];
const emailsNettoyes = [];

for (const email of emails) {
  const nettoye = email.trim().toLowerCase();
  emailsNettoyes.push(nettoye);
}

console.log(emailsNettoyes);
// ["alice@email.com", "bob@email.com", "charlie@email.com"]
```

### Exemple 5 : Vérification de présence

```javascript
const motsCles = ["JavaScript", "Python", "HTML", "CSS"];
const technologies = ["React", "JavaScript", "Node.js"];
const competencesCorrespondantes = [];

for (const motCle of motsCles) {
  for (const tech of technologies) {
    if (tech.toLowerCase().includes(motCle.toLowerCase())) {
      competencesCorrespondantes.push(motCle);
      break; // On sort de la boucle interne
    }
  }
}

console.log("Compétences trouvées :", competencesCorrespondantes);
// Compétences trouvées : ["JavaScript"]
```

---

## Boucles imbriquées avec `for...of`

Vous pouvez imbriquer des boucles `for...of`.

### Exemple : Parcourir un tableau 2D (matrice)

```javascript
const grille = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

for (const ligne of grille) {
  for (const nombre of ligne) {
    console.log(nombre);
  }
}
// Affiche : 1, 2, 3, 4, 5, 6, 7, 8, 9
```

### Afficher une grille formatée

```javascript
const grille = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

for (const ligne of grille) {
  let ligneStr = "";
  for (const nombre of ligne) {
    ligneStr += nombre + " ";
  }
  console.log(ligneStr);
}
```

**Résultat :**
```
1 2 3
4 5 6
7 8 9
```

---

## Performance : `for...of` vs `for` classique

Pour la plupart des cas, la différence de performance est **négligeable**. Privilégiez la **lisibilité** !

### Cas où `for` classique est plus rapide (rare)

```javascript
// Pour des tableaux TRÈS grands (millions d'éléments)
// et des opérations critiques en performance
const hugeArray = new Array(10000000);

// for classique : légèrement plus rapide
for (let i = 0; i < hugeArray.length; i++) {
  // ...
}

// for...of : légèrement plus lent mais plus lisible
for (const item of hugeArray) {
  // ...
}
```

**Conseil :** Ne vous préoccupez de la performance que si vous avez un problème de performance réel. La lisibilité prime !

---

## Méthodes modernes alternatives

Pour certaines opérations, JavaScript propose des méthodes encore plus expressives que `for...of`.

### `forEach()` : Parcourir avec une fonction

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.forEach(fruit => {
  console.log(fruit);
});
```

### `map()` : Transformer chaque élément

```javascript
const nombres = [1, 2, 3, 4, 5];
const doubles = nombres.map(n => n * 2);
console.log(doubles); // [2, 4, 6, 8, 10]
```

### `filter()` : Filtrer des éléments

```javascript
const nombres = [1, 2, 3, 4, 5, 6];
const pairs = nombres.filter(n => n % 2 === 0);
console.log(pairs); // [2, 4, 6]
```

**Note :** Nous verrons ces méthodes en détail dans une section ultérieure. Pour l'instant, retenez que `for...of` est un excellent choix général !

---

## Résumé

### Points clés à retenir

- **`for...of`** est une boucle **moderne** (ES6+) pour parcourir des tableaux
- Elle donne accès directement aux **valeurs**, pas aux indices
- Plus **simple** et **lisible** que `for` classique
- Fonctionne avec les **tableaux**, **strings**, **Sets**, **Maps** et autres itérables
- Utilisez `const` sauf si vous devez modifier la variable
- Utilisez `.entries()` si vous avez besoin de l'index
- Ne confondez pas avec `for...in` (qui est pour les objets)

### Quand l'utiliser

✅ **Utilisez `for...of` quand :**
- Vous parcourez un tableau du début à la fin
- Vous n'avez pas besoin de l'index (ou utilisez `.entries()`)
- Vous voulez un code simple et lisible

❌ **Utilisez `for` classique quand :**
- Vous devez modifier le tableau en place
- Vous avez besoin de contrôle précis sur l'index
- Vous parcourez dans un ordre non-standard

### Tableau récapitulatif

| Boucle | Usage | Donne accès à |
|--------|-------|---------------|
| `for` classique | Contrôle total | Index + Valeur |
| `for...of` 🆕 | Parcours simple | Valeur |
| `for...in` | Objets | Clé/Propriété |
| `forEach()` | Fonctionnel | Valeur + Index + Tableau |

La boucle `for...of` est l'une des améliorations les plus appréciées d'ES6. Elle rend le code JavaScript plus moderne, plus propre et plus agréable à lire ! 🚀

⏭️ [Boucle for...in (pour les objets)](/05-javascript-moderne-fondamentaux/05-structures-controle/05-boucle-for-in.md)
