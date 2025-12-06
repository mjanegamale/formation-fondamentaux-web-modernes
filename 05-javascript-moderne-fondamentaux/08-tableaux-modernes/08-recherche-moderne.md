🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.8 - Méthodes modernes de recherche : find, findIndex, includes 🆕

## Introduction

JavaScript propose des **méthodes modernes** (ES6+) pour rechercher des éléments dans un tableau de manière plus puissante et lisible que les méthodes classiques.

### Les trois méthodes principales

| Méthode       | Retourne                              | Utile pour                          |
|---------------|---------------------------------------|-------------------------------------|
| `includes()`  | `true` ou `false`                     | Vérifier si une valeur existe       |
| `find()`      | Le premier élément trouvé ou `undefined` | Trouver un élément par condition |
| `findIndex()` | L'index du premier élément ou `-1`    | Trouver la position d'un élément    |

Ces méthodes sont **plus puissantes** que `indexOf()` car elles permettent de rechercher selon des **conditions complexes**.

---

## includes() - Vérifier la présence d'une valeur 🆕

La méthode `includes()` vérifie si un tableau contient une valeur spécifique. Elle retourne `true` ou `false`.

### Syntaxe

```javascript
tableau.includes(valeurCherchee, indexDebut)
```

**Paramètres** :
- `valeurCherchee` : La valeur à rechercher
- `indexDebut` : Position de départ (optionnel, défaut : 0)

**Retour** : `true` si trouvé, `false` sinon

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];

console.log(fruits.includes("banane"));  // true
console.log(fruits.includes("kiwi"));    // false
```

### Avec différents types

```javascript
const nombres = [1, 2, 3, 4, 5];
console.log(nombres.includes(3));  // true
console.log(nombres.includes(10)); // false

const booleens = [true, false, true];
console.log(booleens.includes(false));  // true
```

### Avec un index de départ

```javascript
const lettres = ["a", "b", "c", "d", "e"];

// Chercher "c" à partir de l'index 2
console.log(lettres.includes("c", 2));  // true

// Chercher "b" à partir de l'index 2
console.log(lettres.includes("b", 2));  // false (b est avant l'index 2)
```

### Avec des index négatifs

Les index négatifs comptent depuis la fin :

```javascript
const nombres = [1, 2, 3, 4, 5];

// Chercher dans les 2 derniers éléments
console.log(nombres.includes(4, -2));  // true (4 est dans les 2 derniers)
console.log(nombres.includes(2, -2));  // false (2 n'est pas dans les 2 derniers)
```

### Cas particuliers

#### NaN (Not a Number)

Contrairement à `indexOf()`, `includes()` peut détecter `NaN` :

```javascript
const valeurs = [1, 2, NaN, 4];

console.log(valeurs.includes(NaN));  // true ✅
console.log(valeurs.indexOf(NaN));   // -1 ❌ (ne trouve pas NaN)
```

#### Comparaison stricte

`includes()` utilise une comparaison **similaire** à `===`, mais avec une exception pour `NaN` :

```javascript
const nombres = [1, 2, 3];

console.log(nombres.includes(2));    // true
console.log(nombres.includes("2"));  // false (type différent)
```

---

## find() - Trouver un élément par condition 🆕

La méthode `find()` retourne le **premier élément** qui satisfait une condition (fonction de test).

### Syntaxe

```javascript
tableau.find(fonction)
tableau.find((element, index, tableau) => {
  // Condition de recherche
  return condition;
})
```

**Paramètres de la fonction de rappel** :
- `element` : L'élément en cours de traitement
- `index` : L'index de l'élément (optionnel)
- `tableau` : Le tableau complet (optionnel)

**Retour** : Le premier élément trouvé, ou `undefined` si aucun

### Recherche simple

```javascript
const nombres = [5, 12, 8, 130, 44];

// Trouver le premier nombre supérieur à 10
const resultat = nombres.find(nombre => nombre > 10);

console.log(resultat);  // 12
```

### Recherche dans un tableau d'objets

C'est là que `find()` brille vraiment :

```javascript
const utilisateurs = [
  { id: 1, nom: "Alice", age: 25 },
  { id: 2, nom: "Bob", age: 30 },
  { id: 3, nom: "Charlie", age: 35 }
];

// Trouver l'utilisateur avec l'id 2
const utilisateur = utilisateurs.find(user => user.id === 2);

console.log(utilisateur);  // { id: 2, nom: "Bob", age: 30 }
console.log(utilisateur.nom);  // "Bob"
```

### Conditions complexes

```javascript
const produits = [
  { nom: "Laptop", prix: 1000, stock: 5 },
  { nom: "Souris", prix: 25, stock: 0 },
  { nom: "Clavier", prix: 75, stock: 10 }
];

// Trouver le premier produit en stock et abordable
const produit = produits.find(p => p.stock > 0 && p.prix < 100);

console.log(produit);  // { nom: "Clavier", prix: 75, stock: 10 }
```

### Si aucun élément n'est trouvé

```javascript
const nombres = [1, 2, 3, 4, 5];

const resultat = nombres.find(n => n > 10);

console.log(resultat);  // undefined
```

### Utiliser l'index dans la fonction

```javascript
const nombres = [10, 20, 30, 40, 50];

// Trouver le premier élément dont l'index est pair
const resultat = nombres.find((element, index) => index % 2 === 0);

console.log(resultat);  // 10 (index 0)
```

### Syntaxe avec fonction nommée

```javascript
const nombres = [1, 3, 5, 8, 10, 12];

function estPair(nombre) {
  return nombre % 2 === 0;
}

const premierPair = nombres.find(estPair);
console.log(premierPair);  // 8
```

---

## findIndex() - Trouver l'index d'un élément 🆕

La méthode `findIndex()` retourne l'**index du premier élément** qui satisfait une condition.

### Syntaxe

```javascript
tableau.findIndex(fonction)
tableau.findIndex((element, index, tableau) => {
  // Condition de recherche
  return condition;
})
```

**Retour** : L'index du premier élément trouvé, ou `-1` si aucun

### Utilisation de base

```javascript
const nombres = [5, 12, 8, 130, 44];

// Trouver l'index du premier nombre supérieur à 10
const index = nombres.findIndex(nombre => nombre > 10);

console.log(index);  // 1 (12 est à l'index 1)
```

### Recherche dans un tableau d'objets

```javascript
const utilisateurs = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" },
  { id: 3, nom: "Charlie" }
];

// Trouver l'index de Bob
const index = utilisateurs.findIndex(user => user.nom === "Bob");

console.log(index);  // 1
```

### Si aucun élément n'est trouvé

```javascript
const nombres = [1, 2, 3, 4, 5];

const index = nombres.findIndex(n => n > 10);

console.log(index);  // -1
```

### Utilisation après avoir trouvé l'index

```javascript
const taches = [
  { id: 1, texte: "Faire courses", termine: false },
  { id: 2, texte: "Appeler médecin", termine: false },
  { id: 3, texte: "Lire email", termine: true }
];

// Trouver l'index de la première tâche non terminée
const index = taches.findIndex(t => !t.termine);

if (index !== -1) {
  console.log(`Prochaine tâche : ${taches[index].texte}`);
  // "Prochaine tâche : Faire courses"
}
```

### Supprimer un élément après l'avoir trouvé

```javascript
const produits = [
  { id: 1, nom: "Laptop" },
  { id: 2, nom: "Souris" },
  { id: 3, nom: "Clavier" }
];

// Trouver et supprimer le produit avec id 2
const index = produits.findIndex(p => p.id === 2);

if (index !== -1) {
  produits.splice(index, 1);
}

console.log(produits);
// [{ id: 1, nom: "Laptop" }, { id: 3, nom: "Clavier" }]
```

---

## Comparaison avec les méthodes classiques

### includes() vs indexOf()

**Méthode moderne (includes)** :

```javascript
const fruits = ["pomme", "banane", "orange"];

if (fruits.includes("banane")) {
  console.log("On a des bananes !");
}
```

**Méthode classique (indexOf)** :

```javascript
const fruits = ["pomme", "banane", "orange"];

if (fruits.indexOf("banane") !== -1) {
  console.log("On a des bananes !");
}
```

✅ `includes()` est plus lisible et son intention est plus claire.

### find() vs boucle for

**Méthode moderne (find)** :

```javascript
const users = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" },
  { id: 3, nom: "Charlie" }
];

const user = users.find(u => u.id === 2);
```

**Méthode classique (boucle)** :

```javascript
const users = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" },
  { id: 3, nom: "Charlie" }
];

let user;
for (let i = 0; i < users.length; i++) {
  if (users[i].id === 2) {
    user = users[i];
    break;
  }
}
```

✅ `find()` est beaucoup plus concis et expressif.

### Tableau comparatif complet

| Méthode       | Moderne | Recherche        | Retourne              | Avec condition ? |
|---------------|---------|------------------|-----------------------|------------------|
| `includes()`  | ✅ ES7   | Valeur exacte    | `true`/`false`        | ❌                |
| `indexOf()`   | ⚠️ Ancien | Valeur exacte   | Index ou `-1`         | ❌                |
| `find()`      | ✅ ES6   | Par condition    | Élément ou `undefined`| ✅                |
| `findIndex()` | ✅ ES6   | Par condition    | Index ou `-1`         | ✅                |

---

## Exemples pratiques complets

### Exemple 1 : Vérifier les permissions

```javascript
const permissions = ["read", "write", "delete"];

if (permissions.includes("delete")) {
  console.log("⚠️ Attention : permission de suppression active");
} else {
  console.log("✅ Pas de permission de suppression");
}
```

### Exemple 2 : Trouver un produit par code

```javascript
const inventaire = [
  { code: "A123", nom: "Chaise", stock: 15 },
  { code: "B456", nom: "Table", stock: 8 },
  { code: "C789", nom: "Lampe", stock: 0 }
];

const codeCherche = "B456";
const produit = inventaire.find(p => p.code === codeCherche);

if (produit) {
  console.log(`${produit.nom} - Stock: ${produit.stock}`);
} else {
  console.log("Produit non trouvé");
}
```

### Exemple 3 : Trouver le premier disponible

```javascript
const serveurs = [
  { nom: "Serveur 1", actif: false },
  { nom: "Serveur 2", actif: true },
  { nom: "Serveur 3", actif: true }
];

const serveurDispo = serveurs.find(s => s.actif);
console.log(`Connexion à : ${serveurDispo.nom}`);
// "Connexion à : Serveur 2"
```

### Exemple 4 : Modifier un élément spécifique

```javascript
const etudiants = [
  { id: 1, nom: "Alice", note: 15 },
  { id: 2, nom: "Bob", note: 12 },
  { id: 3, nom: "Charlie", note: 18 }
];

// Trouver et modifier la note de Bob
const index = etudiants.findIndex(e => e.nom === "Bob");

if (index !== -1) {
  etudiants[index].note = 14;
  console.log("Note mise à jour");
}

console.log(etudiants);
```

### Exemple 5 : Validation de formulaire

```javascript
const champs = [
  { nom: "email", valeur: "alice@example.com", valide: true },
  { nom: "password", valeur: "", valide: false },
  { nom: "nom", valeur: "Alice", valide: true }
];

// Vérifier si tous les champs sont valides
const champInvalide = champs.find(c => !c.valide);

if (champInvalide) {
  console.log(`Erreur : ${champInvalide.nom} est invalide`);
} else {
  console.log("Formulaire valide !");
}
```

### Exemple 6 : Système de notifications

```javascript
const notifications = [
  { id: 1, message: "Nouveau message", lu: true },
  { id: 2, message: "Mise à jour", lu: false },
  { id: 3, message: "Rappel", lu: false }
];

// Trouver la première notification non lue
const nonLue = notifications.find(n => !n.lu);

if (nonLue) {
  console.log(`📬 ${nonLue.message}`);
}

// Compter les notifications non lues
const nbNonLues = notifications.filter(n => !n.lu).length;
console.log(`${nbNonLues} notifications non lues`);
```

### Exemple 7 : Recherche d'âge

```javascript
const personnes = [
  { nom: "Alice", age: 17 },
  { nom: "Bob", age: 25 },
  { nom: "Charlie", age: 15 }
];

// Trouver le premier majeur
const majeur = personnes.find(p => p.age >= 18);

if (majeur) {
  console.log(`${majeur.nom} est majeur(e)`);
} else {
  console.log("Aucun majeur trouvé");
}
```

---

## Cas d'usage : Quelle méthode choisir ?

### Utilisez includes() quand :

- ✅ Vous voulez juste vérifier si une **valeur existe**
- ✅ Vous travaillez avec des **valeurs simples** (nombres, chaînes, booléens)
- ✅ Vous avez besoin d'un résultat **booléen**

```javascript
const tags = ["javascript", "react", "node"];

if (tags.includes("react")) {
  // ...
}
```

### Utilisez find() quand :

- ✅ Vous voulez **récupérer l'élément complet**
- ✅ Vous recherchez selon une **condition complexe**
- ✅ Vous travaillez avec des **objets**

```javascript
const users = [{ id: 1, nom: "Alice" }, { id: 2, nom: "Bob" }];

const user = users.find(u => u.id === 2);
console.log(user.nom);  // Besoin de l'objet complet
```

### Utilisez findIndex() quand :

- ✅ Vous avez besoin de la **position** de l'élément
- ✅ Vous voulez **modifier** ou **supprimer** l'élément après
- ✅ Vous voulez effectuer des opérations basées sur l'**index**

```javascript
const taches = [{ id: 1, texte: "..." }, { id: 2, texte: "..." }];

const index = taches.findIndex(t => t.id === 2);
taches.splice(index, 1);  // Supprimer la tâche
```

---

## Chaîner avec d'autres méthodes

### find() avec déstructuration

```javascript
const produits = [
  { id: 1, nom: "Laptop", prix: 1000 },
  { id: 2, nom: "Souris", prix: 25 }
];

const { nom, prix } = produits.find(p => p.id === 2) || {};
console.log(nom);  // "Souris"
```

### Avec optional chaining (?.)

```javascript
const users = [{ id: 1, nom: "Alice" }];

const userName = users.find(u => u.id === 2)?.nom || "Inconnu";
console.log(userName);  // "Inconnu"
```

---

## Gestion des cas "non trouvé"

### Avec includes()

```javascript
const fruits = ["pomme", "banane"];

if (!fruits.includes("orange")) {
  console.log("Pas d'oranges");
}
```

### Avec find()

```javascript
const users = [{ id: 1, nom: "Alice" }];

const user = users.find(u => u.id === 2);

if (user) {
  console.log(user.nom);
} else {
  console.log("Utilisateur non trouvé");
}

// Ou avec une valeur par défaut
const userName = (users.find(u => u.id === 2) || { nom: "Invité" }).nom;
```

### Avec findIndex()

```javascript
const taches = [{ id: 1 }, { id: 2 }];

const index = taches.findIndex(t => t.id === 3);

if (index !== -1) {
  console.log(`Trouvé à l'index ${index}`);
} else {
  console.log("Non trouvé");
}
```

---

## Performances

### includes()
- Complexité : O(n) - parcourt le tableau jusqu'à trouver
- Rapide pour les tableaux courts
- Arrête dès que l'élément est trouvé

### find() et findIndex()
- Complexité : O(n) - parcourt jusqu'à trouver
- Arrêtent dès que la condition est vraie
- Efficaces car ne parcourent pas tout le tableau si trouvé tôt

> 💡 **Optimisation** : Pour des recherches répétées dans de grands tableaux, envisagez d'utiliser un `Set` ou un objet/Map pour des recherches en O(1).

---

## Erreurs courantes et pièges

### ❌ Oublier que find() retourne undefined

```javascript
const users = [{ id: 1, nom: "Alice" }];

const user = users.find(u => u.id === 2);
console.log(user.nom);  // ❌ Erreur ! Cannot read property 'nom' of undefined

// ✅ Vérifier d'abord
if (user) {
  console.log(user.nom);
}

// ✅ Ou utiliser optional chaining
console.log(user?.nom);
```

### ❌ Confondre find() et filter()

```javascript
const nombres = [1, 2, 3, 4, 5];

// find() - retourne LE PREMIER élément
const premier = nombres.find(n => n > 2);
console.log(premier);  // 3

// filter() - retourne TOUS les éléments correspondants
const tous = nombres.filter(n => n > 2);
console.log(tous);  // [3, 4, 5]
```

### ❌ Oublier le return dans la fonction

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Pas de return
const resultat = nombres.find(n => {
  n > 3;  // Cette ligne ne retourne rien !
});
console.log(resultat);  // undefined

// ✅ Avec return
const correct = nombres.find(n => {
  return n > 3;
});
console.log(correct);  // 4

// ✅ Ou avec arrow function implicite
const correct2 = nombres.find(n => n > 3);
console.log(correct2);  // 4
```

### ❌ Utiliser == au lieu de ===

```javascript
const nombres = [1, 2, 3];

// ⚠️ Mauvais : comparaison non stricte
const resultat = nombres.find(n => n == "2");
console.log(resultat);  // 2 (trouve à cause de ==)

// ✅ Bon : comparaison stricte
const correct = nombres.find(n => n === "2");
console.log(correct);  // undefined (comme attendu)
```

---

## Points clés à retenir

- ✅ **includes()** : vérifie si une valeur existe → retourne booléen
- ✅ **find()** : trouve le premier élément → retourne l'élément ou `undefined`
- ✅ **findIndex()** : trouve l'index → retourne l'index ou `-1`
- ✅ find() et findIndex() utilisent des **fonctions de condition**
- ✅ Ces méthodes sont **plus puissantes** qu'indexOf()
- ✅ Elles **arrêtent** dès qu'un élément est trouvé
- ✅ includes() peut détecter `NaN` (contrairement à indexOf)
- ✅ Toujours **vérifier** que find() n'a pas retourné `undefined`
- ✅ Ne pas confondre find() (un élément) et filter() (tous les éléments)

---

## Bonnes pratiques

- ✅ Utilisez `includes()` pour les vérifications simples d'existence
- ✅ Utilisez `find()` quand vous avez besoin de l'objet complet
- ✅ Utilisez `findIndex()` quand vous devez modifier/supprimer l'élément
- ✅ Vérifiez toujours le résultat de `find()` avant de l'utiliser
- ✅ Préférez `===` à `==` dans vos conditions
- ✅ Utilisez arrow functions pour des conditions simples
- ✅ Nommez clairement vos fonctions de recherche pour des conditions complexes

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez `indexOf()` et `lastIndexOf()`, les méthodes classiques de recherche qui restent utiles dans certains cas.

---


⏭️ [indexOf et lastIndexOf (legacy mais toujours utilisé)](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/09-indexof-lastindexof.md)
