🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.10 - Méthodes de transformation : map, filter, reduce 🆕

## Introduction

Les méthodes `map()`, `filter()` et `reduce()` sont **trois des méthodes les plus puissantes** en JavaScript. Elles permettent de transformer des tableaux de manière **élégante et fonctionnelle**.

### Programmation fonctionnelle

Ces méthodes suivent les principes de la **programmation fonctionnelle** :
- ✅ **Immutabilité** : ne modifient pas le tableau original
- ✅ **Pureté** : retournent toujours un nouveau résultat
- ✅ **Composition** : peuvent être chaînées ensemble

### Vue d'ensemble

| Méthode   | Action                          | Retourne                    |
|-----------|---------------------------------|-----------------------------|
| `map()`   | Transforme chaque élément       | Nouveau tableau (même taille) |
| `filter()`| Sélectionne certains éléments   | Nouveau tableau (taille ≤)  |
| `reduce()`| Agrège tous les éléments        | Une seule valeur            |

---

## map() - Transformer chaque élément 🆕

La méthode `map()` **transforme** chaque élément d'un tableau en appliquant une fonction, et retourne un **nouveau tableau** avec les résultats.

### Syntaxe

```javascript
const nouveauTableau = tableau.map((element, index, tableau) => {
  // Retourner la valeur transformée
  return valeurTransformee;
});
```

**Paramètres de la fonction de rappel** :
- `element` : L'élément en cours de traitement
- `index` : L'index de l'élément (optionnel)
- `tableau` : Le tableau complet (optionnel)

**Retour** : Un **nouveau tableau** de la même longueur

### Exemple simple : doubler des nombres

```javascript
const nombres = [1, 2, 3, 4, 5];

const doubles = nombres.map(n => n * 2);

console.log(nombres);  // [1, 2, 3, 4, 5] (original intact)
console.log(doubles);  // [2, 4, 6, 8, 10]
```

### Visualisation

```
Entrée:  [1,    2,    3,    4,    5]
          ↓     ↓     ↓     ↓     ↓
       (×2)  (×2)  (×2)  (×2)  (×2)
          ↓     ↓     ↓     ↓     ↓
Sortie:  [2,    4,    6,    8,   10]
```

### Transformer des chaînes

```javascript
const prenoms = ["alice", "bob", "charlie"];

const majuscules = prenoms.map(nom => nom.toUpperCase());

console.log(majuscules);  // ["ALICE", "BOB", "CHARLIE"]
```

### Extraire des propriétés d'objets

```javascript
const utilisateurs = [
  { id: 1, nom: "Alice", age: 25 },
  { id: 2, nom: "Bob", age: 30 },
  { id: 3, nom: "Charlie", age: 35 }
];

// Extraire seulement les noms
const noms = utilisateurs.map(user => user.nom);
console.log(noms);  // ["Alice", "Bob", "Charlie"]

// Extraire seulement les âges
const ages = utilisateurs.map(user => user.age);
console.log(ages);  // [25, 30, 35]
```

### Créer de nouveaux objets

```javascript
const produits = [
  { nom: "Laptop", prix: 1000 },
  { nom: "Souris", prix: 25 },
  { nom: "Clavier", prix: 75 }
];

// Appliquer une réduction de 10%
const enPromo = produits.map(p => ({
  nom: p.nom,
  prixOriginal: p.prix,
  prixPromo: p.prix * 0.9
}));

console.log(enPromo);
// [
//   { nom: "Laptop", prixOriginal: 1000, prixPromo: 900 },
//   { nom: "Souris", prixOriginal: 25, prixPromo: 22.5 },
//   { nom: "Clavier", prixOriginal: 75, prixPromo: 67.5 }
// ]
```

### Utiliser l'index

```javascript
const lettres = ["a", "b", "c"];

const avecIndex = lettres.map((lettre, index) => `${index}: ${lettre}`);

console.log(avecIndex);  // ["0: a", "1: b", "2: c"]
```

### Comparaison avec une boucle for

**Avec boucle for (ancien style)** :
```javascript
const nombres = [1, 2, 3, 4, 5];
const doubles = [];

for (let i = 0; i < nombres.length; i++) {
  doubles.push(nombres[i] * 2);
}

console.log(doubles);  // [2, 4, 6, 8, 10]
```

**Avec map() (moderne)** :
```javascript
const nombres = [1, 2, 3, 4, 5];

const doubles = nombres.map(n => n * 2);

console.log(doubles);  // [2, 4, 6, 8, 10]
```

✅ Plus court, plus lisible, plus expressif !

---

## filter() - Sélectionner des éléments 🆕

La méthode `filter()` crée un **nouveau tableau** contenant uniquement les éléments qui **passent un test** (fonction qui retourne `true` ou `false`).

### Syntaxe

```javascript
const nouveauTableau = tableau.filter((element, index, tableau) => {
  // Retourner true pour garder l'élément, false pour l'exclure
  return condition;
});
```

**Retour** : Un **nouveau tableau** avec les éléments filtrés (peut être vide)

### Exemple simple : nombres pairs

```javascript
const nombres = [1, 2, 3, 4, 5, 6];

const pairs = nombres.filter(n => n % 2 === 0);

console.log(nombres);  // [1, 2, 3, 4, 5, 6] (original intact)
console.log(pairs);    // [2, 4, 6]
```

### Visualisation

```
Entrée:  [1,    2,    3,    4,    5,    6]
          ↓     ↓     ↓     ↓     ↓     ↓
     (pair?) (pair?) (pair?) (pair?) (pair?) (pair?)
        ❌     ✅    ❌     ✅    ❌     ✅
               ↓           ↓           ↓
Sortie:       [2,          4,          6]
```

### Filtrer par condition

```javascript
const ages = [15, 22, 17, 30, 12, 25];

// Garder seulement les majeurs
const majeurs = ages.filter(age => age >= 18);

console.log(majeurs);  // [22, 30, 25]
```

### Filtrer des objets

```javascript
const produits = [
  { nom: "Laptop", prix: 1000, stock: 5 },
  { nom: "Souris", prix: 25, stock: 0 },
  { nom: "Clavier", prix: 75, stock: 10 },
  { nom: "Écran", prix: 300, stock: 0 }
];

// Garder seulement les produits en stock
const disponibles = produits.filter(p => p.stock > 0);

console.log(disponibles);
// [
//   { nom: "Laptop", prix: 1000, stock: 5 },
//   { nom: "Clavier", prix: 75, stock: 10 }
// ]
```

### Conditions complexes

```javascript
const produits = [
  { nom: "Laptop", prix: 1000, stock: 5 },
  { nom: "Souris", prix: 25, stock: 10 },
  { nom: "Clavier", prix: 75, stock: 0 }
];

// Produits disponibles ET abordables (< 100€)
const selection = produits.filter(p => p.stock > 0 && p.prix < 100);

console.log(selection);
// [{ nom: "Souris", prix: 25, stock: 10 }]
```

### Filtrer par type

```javascript
const melange = [1, "deux", 3, "quatre", 5, null, 7, undefined, 9];

// Garder seulement les nombres
const nombres = melange.filter(item => typeof item === "number");

console.log(nombres);  // [1, 3, 5, 7, 9]
```

### Supprimer les valeurs falsy

```javascript
const valeurs = [0, 1, false, 2, "", 3, null, undefined, 4];

// Garder seulement les valeurs truthy
const valides = valeurs.filter(Boolean);

console.log(valides);  // [1, 2, 3, 4]
```

> 💡 **Astuce** : `filter(Boolean)` est un raccourci pour `filter(v => Boolean(v))`

### Supprimer les doublons

```javascript
const nombres = [1, 2, 2, 3, 4, 4, 5];

const uniques = nombres.filter((n, index, arr) => arr.indexOf(n) === index);

console.log(uniques);  // [1, 2, 3, 4, 5]
```

### Comparaison avec une boucle for

**Avec boucle for (ancien style)** :
```javascript
const nombres = [1, 2, 3, 4, 5, 6];
const pairs = [];

for (let i = 0; i < nombres.length; i++) {
  if (nombres[i] % 2 === 0) {
    pairs.push(nombres[i]);
  }
}

console.log(pairs);  // [2, 4, 6]
```

**Avec filter() (moderne)** :
```javascript
const nombres = [1, 2, 3, 4, 5, 6];

const pairs = nombres.filter(n => n % 2 === 0);

console.log(pairs);  // [2, 4, 6]
```

---

## reduce() - Réduire à une seule valeur 🆕

La méthode `reduce()` **réduit** un tableau à **une seule valeur** en appliquant une fonction qui accumule un résultat.

### Syntaxe

```javascript
const resultat = tableau.reduce((accumulateur, element, index, tableau) => {
  // Retourner la nouvelle valeur de l'accumulateur
  return nouvelAccumulateur;
}, valeurInitiale);
```

**Paramètres de la fonction de rappel** :
- `accumulateur` : La valeur accumulée (résultat des itérations précédentes)
- `element` : L'élément en cours de traitement
- `index` : L'index de l'élément (optionnel)
- `tableau` : Le tableau complet (optionnel)

**Paramètre supplémentaire** :
- `valeurInitiale` : Valeur de départ de l'accumulateur (optionnel mais recommandé)

### Exemple simple : somme de nombres

```javascript
const nombres = [1, 2, 3, 4, 5];

const somme = nombres.reduce((total, n) => total + n, 0);

console.log(somme);  // 15
```

### Visualisation étape par étape

```javascript
const nombres = [1, 2, 3, 4, 5];
const somme = nombres.reduce((total, n) => total + n, 0);
```

| Itération | total (accumulateur) | n (élément) | Retour |
|-----------|---------------------|-------------|--------|
| Initial   | 0                   | -           | -      |
| 1         | 0                   | 1           | 1      |
| 2         | 1                   | 2           | 3      |
| 3         | 3                   | 3           | 6      |
| 4         | 6                   | 4           | 10     |
| 5         | 10                  | 5           | 15     |

**Résultat final** : `15`

### Produit de nombres

```javascript
const nombres = [2, 3, 4];

const produit = nombres.reduce((resultat, n) => resultat * n, 1);

console.log(produit);  // 24 (2 × 3 × 4)
```

### Trouver le maximum

```javascript
const nombres = [5, 12, 8, 130, 44];

const max = nombres.reduce((maximum, n) => {
  return n > maximum ? n : maximum;
}, nombres[0]);

console.log(max);  // 130
```

Ou plus simplement :
```javascript
const max = nombres.reduce((max, n) => Math.max(max, n), -Infinity);
```

### Compter les occurrences

```javascript
const fruits = ["pomme", "banane", "pomme", "orange", "banane", "pomme"];

const compteur = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});

console.log(compteur);
// { pomme: 3, banane: 2, orange: 1 }
```

### Aplatir un tableau (flatten)

```javascript
const tableaux = [[1, 2], [3, 4], [5, 6]];

const aplati = tableaux.reduce((acc, arr) => acc.concat(arr), []);

console.log(aplati);  // [1, 2, 3, 4, 5, 6]
```

### Grouper par propriété

```javascript
const personnes = [
  { nom: "Alice", age: 25, ville: "Paris" },
  { nom: "Bob", age: 30, ville: "Lyon" },
  { nom: "Charlie", age: 35, ville: "Paris" },
  { nom: "David", age: 28, ville: "Lyon" }
];

const parVille = personnes.reduce((acc, p) => {
  if (!acc[p.ville]) {
    acc[p.ville] = [];
  }
  acc[p.ville].push(p);
  return acc;
}, {});

console.log(parVille);
// {
//   Paris: [
//     { nom: "Alice", age: 25, ville: "Paris" },
//     { nom: "Charlie", age: 35, ville: "Paris" }
//   ],
//   Lyon: [
//     { nom: "Bob", age: 30, ville: "Lyon" },
//     { nom: "David", age: 28, ville: "Lyon" }
//   ]
// }
```

### Calculer une moyenne

```javascript
const notes = [15, 18, 12, 16, 14];

const moyenne = notes.reduce((total, note, index, arr) => {
  total += note;
  // Si c'est le dernier élément, diviser par la longueur
  if (index === arr.length - 1) {
    return total / arr.length;
  }
  return total;
}, 0);

console.log(moyenne);  // 15
```

Ou plus simplement :
```javascript
const moyenne = notes.reduce((sum, note) => sum + note, 0) / notes.length;
```

### Créer un objet depuis un tableau

```javascript
const paires = [["nom", "Alice"], ["age", 25], ["ville", "Paris"]];

const objet = paires.reduce((acc, [cle, valeur]) => {
  acc[cle] = valeur;
  return acc;
}, {});

console.log(objet);
// { nom: "Alice", age: 25, ville: "Paris" }
```

### Comparaison avec une boucle for

**Avec boucle for (ancien style)** :
```javascript
const nombres = [1, 2, 3, 4, 5];
let somme = 0;

for (let i = 0; i < nombres.length; i++) {
  somme += nombres[i];
}

console.log(somme);  // 15
```

**Avec reduce() (moderne)** :
```javascript
const nombres = [1, 2, 3, 4, 5];

const somme = nombres.reduce((total, n) => total + n, 0);

console.log(somme);  // 15
```

---

## Chaîner les méthodes

L'un des grands avantages de ces méthodes est qu'elles peuvent être **chaînées** pour créer des transformations complexes.

### Exemple 1 : Filtrer puis transformer

```javascript
const nombres = [1, 2, 3, 4, 5, 6];

// Garder les pairs, puis les doubler
const resultat = nombres
  .filter(n => n % 2 === 0)
  .map(n => n * 2);

console.log(resultat);  // [4, 8, 12]
```

### Exemple 2 : Transformer puis filtrer

```javascript
const mots = ["hello", "world", "javascript", "code"];

// Mettre en majuscules, puis garder les mots > 5 lettres
const resultat = mots
  .map(mot => mot.toUpperCase())
  .filter(mot => mot.length > 5);

console.log(resultat);  // ["JAVASCRIPT"]
```

### Exemple 3 : Pipeline complet

```javascript
const produits = [
  { nom: "Laptop", prix: 1000, stock: 5 },
  { nom: "Souris", prix: 25, stock: 0 },
  { nom: "Clavier", prix: 75, stock: 10 },
  { nom: "Écran", prix: 300, stock: 3 }
];

// 1. Garder les produits en stock
// 2. Appliquer une réduction de 10%
// 3. Calculer le prix total

const total = produits
  .filter(p => p.stock > 0)
  .map(p => p.prix * 0.9)
  .reduce((sum, prix) => sum + prix, 0);

console.log(total);  // 1237.5
```

### Exemple 4 : Traitement de données complexe

```javascript
const utilisateurs = [
  { nom: "Alice", age: 25, actif: true, commandes: 5 },
  { nom: "Bob", age: 17, actif: false, commandes: 2 },
  { nom: "Charlie", age: 30, actif: true, commandes: 8 },
  { nom: "David", age: 22, actif: true, commandes: 3 }
];

// Trouver le nombre total de commandes des utilisateurs actifs majeurs
const totalCommandes = utilisateurs
  .filter(u => u.actif && u.age >= 18)
  .map(u => u.commandes)
  .reduce((total, nb) => total + nb, 0);

console.log(totalCommandes);  // 16 (5 + 8 + 3)
```

---

## Exemples pratiques complets

### Exemple 1 : Traitement de notes

```javascript
const etudiants = [
  { nom: "Alice", notes: [15, 18, 16] },
  { nom: "Bob", notes: [12, 10, 14] },
  { nom: "Charlie", notes: [18, 20, 19] }
];

// Calculer la moyenne de chaque étudiant
const moyennes = etudiants.map(e => ({
  nom: e.nom,
  moyenne: e.notes.reduce((sum, n) => sum + n, 0) / e.notes.length
}));

console.log(moyennes);
// [
//   { nom: "Alice", moyenne: 16.33 },
//   { nom: "Bob", moyenne: 12 },
//   { nom: "Charlie", moyenne: 19 }
// ]

// Garder seulement ceux qui ont la moyenne
const admis = moyennes.filter(e => e.moyenne >= 10);

console.log(admis);  // Tous sont admis
```

### Exemple 2 : Statistiques de ventes

```javascript
const ventes = [
  { produit: "Laptop", quantite: 2, prix: 1000 },
  { produit: "Souris", quantite: 10, prix: 25 },
  { produit: "Clavier", quantite: 5, prix: 75 }
];

// Calculer le chiffre d'affaires total
const CA = ventes.reduce((total, v) => {
  return total + (v.quantite * v.prix);
}, 0);

console.log(`Chiffre d'affaires : ${CA}€`);  // 2625€
```

### Exemple 3 : Transformation de données API

```javascript
const apiResponse = [
  { user_id: 1, user_name: "Alice", user_email: "alice@example.com" },
  { user_id: 2, user_name: "Bob", user_email: "bob@example.com" }
];

// Transformer en format plus propre
const users = apiResponse.map(u => ({
  id: u.user_id,
  name: u.user_name,
  email: u.user_email
}));

console.log(users);
// [
//   { id: 1, name: "Alice", email: "alice@example.com" },
//   { id: 2, name: "Bob", email: "bob@example.com" }
// ]
```

### Exemple 4 : Validation de formulaire

```javascript
const champs = [
  { nom: "email", valeur: "alice@example.com", requis: true },
  { nom: "tel", valeur: "", requis: false },
  { nom: "nom", valeur: "Alice", requis: true }
];

// Vérifier si tous les champs requis sont remplis
const formulaireValide = champs
  .filter(c => c.requis)
  .every(c => c.valeur.trim() !== "");

console.log(formulaireValide);  // true
```

### Exemple 5 : Panier d'achat

```javascript
const panier = [
  { nom: "Laptop", prix: 1000, quantite: 1 },
  { nom: "Souris", prix: 25, quantite: 2 },
  { nom: "Clavier", prix: 75, quantite: 1 }
];

// Calculer le sous-total pour chaque ligne
const lignesAvecTotal = panier.map(item => ({
  ...item,
  sousTotal: item.prix * item.quantite
}));

// Calculer le total général
const totalGeneral = lignesAvecTotal.reduce((sum, item) => {
  return sum + item.sousTotal;
}, 0);

console.log(`Total : ${totalGeneral}€`);  // 1125€
```

---

## Erreurs courantes et pièges

### ❌ Oublier le return dans map/filter

```javascript
const nombres = [1, 2, 3];

// ❌ Pas de return
const doubles = nombres.map(n => {
  n * 2;  // Oubli du return !
});
console.log(doubles);  // [undefined, undefined, undefined]

// ✅ Avec return
const doubles = nombres.map(n => {
  return n * 2;
});
console.log(doubles);  // [2, 4, 6]

// ✅ Ou arrow function implicite
const doubles = nombres.map(n => n * 2);
console.log(doubles);  // [2, 4, 6]
```

### ❌ Modifier le tableau original

```javascript
const objets = [{ valeur: 1 }, { valeur: 2 }];

// ❌ Modifie les objets originaux !
const doubles = objets.map(obj => {
  obj.valeur *= 2;
  return obj;
});

console.log(objets);  // [{ valeur: 2 }, { valeur: 4 }] ⚠️

// ✅ Créer de nouveaux objets
const doubles = objets.map(obj => ({
  valeur: obj.valeur * 2
}));

console.log(objets);  // [{ valeur: 1 }, { valeur: 2 }] ✅
```

### ❌ Oublier la valeur initiale dans reduce()

```javascript
const nombres = [1, 2, 3];

// ⚠️ Sans valeur initiale (fonctionne mais peut causer des bugs)
const somme = nombres.reduce((total, n) => total + n);

// Sur un tableau vide : ERREUR !
const vide = [];
const somme = vide.reduce((total, n) => total + n);  // ❌ TypeError!

// ✅ Avec valeur initiale (recommandé)
const somme = nombres.reduce((total, n) => total + n, 0);
const sommeVide = vide.reduce((total, n) => total + n, 0);  // 0 ✅
```

### ❌ Confondre map() et forEach()

```javascript
// forEach() ne retourne rien !
const nombres = [1, 2, 3];
const resultat = nombres.forEach(n => n * 2);
console.log(resultat);  // undefined ❌

// map() retourne un nouveau tableau
const doubles = nombres.map(n => n * 2);
console.log(doubles);  // [2, 4, 6] ✅
```

### ❌ Utiliser map() quand filter() est plus approprié

```javascript
const nombres = [1, 2, 3, 4, 5, 6];

// ❌ Utiliser map() pour filtrer (inefficace)
const pairs = nombres.map(n => {
  if (n % 2 === 0) return n;
}).filter(n => n !== undefined);

// ✅ Utiliser directement filter()
const pairs = nombres.filter(n => n % 2 === 0);
```

---

## Performances

### map(), filter(), reduce() sont rapides

Ces méthodes sont **optimisées** par les moteurs JavaScript modernes.

### Chaînage vs boucle unique

Le chaînage est très lisible mais parcourt le tableau plusieurs fois :

```javascript
// Chaînage : 2 parcours
const resultat = tableau
  .filter(condition)   // Parcours 1
  .map(transformation); // Parcours 2

// Boucle unique : 1 parcours
const resultat = [];
for (const item of tableau) {
  if (condition(item)) {
    resultat.push(transformation(item));
  }
}
```

> 💡 **Conseil** : Pour la plupart des cas, privilégiez la lisibilité avec le chaînage. L'optimisation n'est nécessaire que pour de très grands tableaux (> 10,000 éléments).

---

## Quand utiliser chaque méthode ?

### Utilisez map() quand :

- ✅ Vous voulez **transformer** chaque élément
- ✅ Le tableau de sortie a la **même taille** que l'entrée
- ✅ Vous créez un nouveau tableau basé sur l'ancien

**Exemples** : doubler des nombres, extraire des propriétés, formatter des données

### Utilisez filter() quand :

- ✅ Vous voulez **sélectionner** certains éléments
- ✅ Le tableau de sortie peut être **plus petit**
- ✅ Vous testez une condition booléenne

**Exemples** : garder les majeurs, produits en stock, valeurs valides

### Utilisez reduce() quand :

- ✅ Vous voulez **agréger** en **une seule valeur**
- ✅ Vous calculez une somme, moyenne, maximum
- ✅ Vous transformez un tableau en objet
- ✅ Vous combinez tous les éléments

**Exemples** : calculer un total, compter, grouper, aplatir

---

## Points clés à retenir

- ✅ **map()** : transforme chaque élément → nouveau tableau (même taille)
- ✅ **filter()** : sélectionne des éléments → nouveau tableau (taille ≤)
- ✅ **reduce()** : réduit à une valeur → valeur unique
- ✅ Ces méthodes **ne modifient pas** le tableau original (immutabilité)
- ✅ Elles utilisent des **fonctions de rappel** (callbacks)
- ✅ Elles peuvent être **chaînées** ensemble
- ✅ Toujours **retourner** une valeur dans les callbacks
- ✅ reduce() : toujours fournir une **valeur initiale**
- ✅ Plus **lisibles** que les boucles for pour des transformations
- ✅ Au cœur de la **programmation fonctionnelle** en JavaScript

---

## Bonnes pratiques

- ✅ Utilisez des **arrow functions** pour les callbacks simples
- ✅ Nommez clairement vos callbacks pour des logiques complexes
- ✅ Privilégiez l'**immutabilité** : ne modifiez pas les objets originaux
- ✅ Fournissez toujours une **valeur initiale** à reduce()
- ✅ Chaînez les méthodes pour plus de **lisibilité**
- ✅ Utilisez le **destructuring** dans les paramètres si pertinent
- ✅ Commentez les transformations complexes
- ✅ Préférez ces méthodes aux boucles for pour les transformations

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez d'autres méthodes utiles des tableaux : `forEach()`, `some()`, et `every()`.

---


⏭️ [Autres méthodes : forEach, some, every](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/11-foreach-some-every.md)
