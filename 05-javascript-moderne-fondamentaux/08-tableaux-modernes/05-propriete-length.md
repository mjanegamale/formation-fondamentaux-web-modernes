🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.5 - Propriété length

## Qu'est-ce que la propriété length ?

La propriété **`length`** d'un tableau indique le **nombre d'éléments** qu'il contient. C'est l'une des propriétés les plus utilisées en JavaScript.

### Syntaxe

```javascript
tableau.length
```

C'est une **propriété**, pas une méthode, donc **pas de parenthèses** `()`.

---

## Obtenir le nombre d'éléments

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits.length);  // 3
```

### Tableau vide

Un tableau vide a une longueur de `0` :

```javascript
const vide = [];
console.log(vide.length);  // 0
```

### Tableaux de différentes tailles

```javascript
const petitTableau = [1, 2];
console.log(petitTableau.length);  // 2

const grandTableau = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log(grandTableau.length);  // 10
```

---

## length représente le plus grand index + 1

⚠️ **Point important** : `length` n'est pas exactement le "nombre d'éléments", mais **le plus grand index + 1**.

### Exemple normal

```javascript
const nombres = [10, 20, 30];
// Index:      0   1   2
// length = 2 + 1 = 3 ✅
console.log(nombres.length);  // 3
```

### Exemple avec un tableau creux

```javascript
const tableauCreux = [];
tableauCreux[0] = "a";
tableauCreux[5] = "b";

console.log(tableauCreux);
// ["a", <4 empty items>, "b"]

console.log(tableauCreux.length);  // 6 (pas 2 !)
// Car le plus grand index est 5, donc length = 5 + 1 = 6
```

Dans la pratique, vous travaillerez rarement avec des tableaux creux, donc `length` correspondra au nombre d'éléments.

---

## Utiliser length avec les index

### Accéder au dernier élément

Puisque les index commencent à 0, le dernier élément est à l'index `length - 1` :

```javascript
const fruits = ["pomme", "banane", "orange"];

const dernier = fruits[fruits.length - 1];
console.log(dernier);  // "orange"
```

**Pourquoi `-1` ?**
- Tableau de 3 éléments : index 0, 1, 2
- `length` = 3
- Dernier index = 3 - 1 = 2 ✅

### Accéder à l'avant-dernier élément

```javascript
const nombres = [10, 20, 30, 40, 50];

const avantDernier = nombres[nombres.length - 2];
console.log(avantDernier);  // 40
```

### Parcourir un tableau avec length

```javascript
const fruits = ["pomme", "banane", "orange"];

for (let i = 0; i < fruits.length; i++) {
  console.log(`Fruit ${i + 1}: ${fruits[i]}`);
}
// Fruit 1: pomme
// Fruit 2: banane
// Fruit 3: orange
```

La condition `i < fruits.length` garantit qu'on ne dépasse pas le tableau.

---

## Vérifier si un tableau est vide

Utilisez `length` pour tester si un tableau contient des éléments :

```javascript
const panier = [];

if (panier.length === 0) {
  console.log("Le panier est vide");
} else {
  console.log(`Le panier contient ${panier.length} articles`);
}
```

### Avec un opérateur logique

```javascript
const taches = ["Faire les courses", "Appeler le médecin"];

if (taches.length > 0) {
  console.log("Il y a des tâches à faire !");
}
```

### Forme courte (truthy/falsy)

Comme `0` est falsy en JavaScript, vous pouvez écrire :

```javascript
const panier = [];

if (panier.length) {
  console.log("Le panier contient des articles");
} else {
  console.log("Le panier est vide");
}
```

> 💡 **Note** : Cette forme est concise, mais `length === 0` est plus explicite et lisible.

---

## Modifier la propriété length

⚠️ **Caractéristique unique** : Contrairement à beaucoup de propriétés, vous pouvez **modifier** `length` directement !

### Réduire la taille d'un tableau

Si vous réduisez `length`, les éléments en fin de tableau sont **supprimés** :

```javascript
const nombres = [1, 2, 3, 4, 5];
console.log(nombres);  // [1, 2, 3, 4, 5]

nombres.length = 3;  // Réduire à 3 éléments

console.log(nombres);  // [1, 2, 3]
// Les éléments 4 et 5 ont été supprimés !
```

### Vider complètement un tableau

Pour supprimer tous les éléments, définissez `length` à `0` :

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.length = 0;

console.log(fruits);  // []
console.log(fruits.length);  // 0
```

### Augmenter la taille d'un tableau

Si vous augmentez `length`, des emplacements vides sont ajoutés :

```javascript
const nombres = [1, 2, 3];
console.log(nombres);  // [1, 2, 3]

nombres.length = 5;

console.log(nombres);  // [1, 2, 3, <2 empty items>]
console.log(nombres[3]);  // undefined
console.log(nombres[4]);  // undefined
```

> ⚠️ **Attention** : Cette pratique crée des tableaux creux et est généralement déconseillée.

---

## Exemples pratiques

### Exemple 1 : Afficher le nombre d'éléments

```javascript
const participants = ["Alice", "Bob", "Charlie", "David"];

console.log(`Il y a ${participants.length} participants`);
// "Il y a 4 participants"
```

### Exemple 2 : Limiter la taille d'un historique

```javascript
const historique = [];

function ajouterAction(action) {
  historique.push(action);

  // Garder seulement les 10 dernières actions
  if (historique.length > 10) {
    historique.shift();  // Retirer la plus ancienne
  }
}

ajouterAction("Ouvrir fichier");
ajouterAction("Modifier texte");
// ... etc
```

### Exemple 3 : Vérifier qu'un tableau n'est pas vide avant traitement

```javascript
const notes = [15, 18, 12, 16];

if (notes.length > 0) {
  const somme = notes.reduce((total, note) => total + note, 0);
  const moyenne = somme / notes.length;
  console.log(`Moyenne: ${moyenne}`);
} else {
  console.log("Aucune note à calculer");
}
```

### Exemple 4 : Créer un tableau de taille fixe

Bien que peu utilisé, vous pouvez créer un tableau d'une certaine taille :

```javascript
const scores = new Array(5);
console.log(scores.length);  // 5
console.log(scores);  // [<5 empty items>]

// Remplir avec des valeurs par défaut
scores.fill(0);
console.log(scores);  // [0, 0, 0, 0, 0]
```

### Exemple 5 : Pagination

```javascript
const articles = ["Article 1", "Article 2", "Article 3", "Article 4", "Article 5"];
const articlesParPage = 2;

const nombreDePages = Math.ceil(articles.length / articlesParPage);
console.log(`Nombre de pages: ${nombreDePages}`);  // 3

// Page 1: articles 0-1
// Page 2: articles 2-3
// Page 3: article 4
```

### Exemple 6 : Cloner un tableau avec la bonne taille

```javascript
const original = [1, 2, 3, 4, 5];

// Créer un nouveau tableau de la même taille
const copie = new Array(original.length);

// Copier les valeurs
for (let i = 0; i < original.length; i++) {
  copie[i] = original[i];
}

console.log(copie);  // [1, 2, 3, 4, 5]
```

> 💡 **Note moderne** : Utilisez plutôt le spread operator : `const copie = [...original]`

---

## length change automatiquement

Lorsque vous ajoutez ou retirez des éléments, `length` se met à jour automatiquement :

### Ajout d'éléments

```javascript
const fruits = ["pomme"];
console.log(fruits.length);  // 1

fruits.push("banane");
console.log(fruits.length);  // 2

fruits.push("orange", "kiwi");
console.log(fruits.length);  // 4
```

### Suppression d'éléments

```javascript
const nombres = [1, 2, 3, 4, 5];
console.log(nombres.length);  // 5

nombres.pop();  // Retire le dernier
console.log(nombres.length);  // 4

nombres.shift();  // Retire le premier
console.log(nombres.length);  // 3
```

### Avec splice()

```javascript
const lettres = ["a", "b", "c", "d", "e"];
console.log(lettres.length);  // 5

lettres.splice(1, 2);  // Retire 2 éléments à partir de l'index 1
console.log(lettres);  // ["a", "d", "e"]
console.log(lettres.length);  // 3
```

---

## Comparaison avec les objets

Les tableaux sont des objets spéciaux, et `length` est une propriété spéciale :

```javascript
// Tableau
const tableau = [1, 2, 3];
console.log(tableau.length);  // 3

// Objet ordinaire (pas de length)
const objet = { a: 1, b: 2, c: 3 };
console.log(objet.length);  // undefined

// Pour compter les propriétés d'un objet :
console.log(Object.keys(objet).length);  // 3
```

---

## length et les méthodes de tableau

Beaucoup de méthodes utilisent `length` en interne :

### forEach()

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.forEach((fruit, index) => {
  console.log(`${index}/${fruits.length - 1}: ${fruit}`);
});
// 0/2: pomme
// 1/2: banane
// 2/2: orange
```

### map()

```javascript
const nombres = [1, 2, 3, 4, 5];

const doubles = nombres.map(n => n * 2);
console.log(doubles.length);  // 5 (même longueur que l'original)
```

### filter()

```javascript
const nombres = [1, 2, 3, 4, 5];

const pairs = nombres.filter(n => n % 2 === 0);
console.log(pairs.length);  // 2 (peut être différent de l'original)
```

---

## Performances

Accéder à `length` est une opération très rapide (O(1) - temps constant).

N'ayez **pas peur** de l'utiliser dans des boucles :

```javascript
// ✅ Performant (length est mis en cache par les moteurs JS modernes)
for (let i = 0; i < tableau.length; i++) {
  // ...
}

// Pas nécessaire d'optimiser comme ça :
const len = tableau.length;
for (let i = 0; i < len; i++) {
  // ...
}
```

Les moteurs JavaScript modernes optimisent automatiquement l'accès à `length`.

---

## Erreurs courantes à éviter

### ❌ Utiliser length avec des parenthèses

```javascript
const fruits = ["pomme", "banane"];
console.log(fruits.length());  // ❌ Erreur ! length n'est pas une fonction
console.log(fruits.length);    // ✅ Correct
```

### ❌ Confondre length et le dernier index

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits[fruits.length]);  // undefined (index 3 n'existe pas)
console.log(fruits[fruits.length - 1]);  // ✅ "orange"
```

### ❌ Modifier length sans comprendre les conséquences

```javascript
const notes = [15, 18, 12, 16, 14];
notes.length = 2;  // ⚠️ Supprime les 3 dernières notes !
console.log(notes);  // [15, 18]
```

### ❌ Créer des trous intentionnellement

```javascript
const fruits = ["pomme", "banane"];
fruits.length = 10;  // ⚠️ Crée 8 emplacements vides
// Évitez cette pratique
```

---

## Cas d'usage avancés

### Limiter dynamiquement un tableau

```javascript
const messageLogs = [];

function ajouterLog(message) {
  messageLogs.push(message);

  // Garder seulement les 100 derniers messages
  if (messageLogs.length > 100) {
    messageLogs.length = 100;
  }
}
```

### Vérifier la cohérence entre deux tableaux

```javascript
const prenoms = ["Alice", "Bob", "Charlie"];
const ages = [25, 30];

if (prenoms.length !== ages.length) {
  console.log("Attention: nombre de prénoms et d'âges différent !");
}
```

### Calculer un pourcentage

```javascript
const taches = [
  { nom: "Tâche 1", terminee: true },
  { nom: "Tâche 2", terminee: false },
  { nom: "Tâche 3", terminee: true },
  { nom: "Tâche 4", terminee: true }
];

const tachesTerminees = taches.filter(t => t.terminee).length;
const pourcentage = (tachesTerminees / taches.length) * 100;

console.log(`Progression: ${pourcentage}%`);  // "Progression: 75%"
```

---

## Points clés à retenir

- ✅ `length` indique le nombre d'éléments dans un tableau
- ✅ Syntaxe : `tableau.length` (pas de parenthèses !)
- ✅ Valeur : plus grand index + 1
- ✅ Dernier élément : `tableau[tableau.length - 1]`
- ✅ Se met à jour automatiquement lors d'ajouts/suppressions
- ✅ Peut être **modifié** directement (rare mais possible)
- ✅ Réduire `length` supprime des éléments
- ✅ `length === 0` pour tester si un tableau est vide
- ✅ Accès très rapide (performances optimales)

---

## Bonnes pratiques

- ✅ Utilisez `length` pour parcourir les tableaux avec `for`
- ✅ Vérifiez `length > 0` avant de traiter un tableau
- ✅ Utilisez `length === 0` plutôt que `!length` pour plus de clarté
- ✅ Ne modifiez `length` que si vous comprenez les conséquences
- ✅ Privilégiez les méthodes comme `pop()`, `splice()` plutôt que de modifier `length` directement

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez les méthodes d'ajout et de suppression d'éléments : `push()`, `pop()`, `shift()` et `unshift()`.

---


⏭️ [Méthodes d'ajout/suppression : push, pop, shift, unshift](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/06-ajout-suppression.md)
