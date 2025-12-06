🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.7 - Méthodes de manipulation : splice, slice

## Introduction

Les méthodes `splice()` et `slice()` sont deux méthodes puissantes pour manipuler les tableaux, mais elles ont des **comportements très différents** :

| Méthode   | Modifie l'original ? | Action principale           |
|-----------|----------------------|-----------------------------|
| `splice()` | ✅ OUI (mutable)    | Ajouter/supprimer/remplacer |
| `slice()`  | ❌ NON (immutable)  | Extraire une copie partielle |

⚠️ **Attention** : Leurs noms se ressemblent, mais ne les confondez pas !

---

## splice() - Modifier le tableau original

La méthode `splice()` permet de **modifier** un tableau en :
- Supprimant des éléments
- Ajoutant des éléments
- Remplaçant des éléments

### Syntaxe

```javascript
tableau.splice(indexDebut, nombreASupprimer, element1, element2, ...)
```

**Paramètres** :
- `indexDebut` : Position où commencer la modification
- `nombreASupprimer` : Nombre d'éléments à supprimer (peut être 0)
- `element1, element2, ...` : Éléments à ajouter (optionnel)

**Valeur de retour** : Tableau contenant les éléments supprimés

---

## splice() - Supprimer des éléments

### Supprimer un seul élément

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];

// Supprimer 1 élément à l'index 2
fruits.splice(2, 1);

console.log(fruits);  // ["pomme", "banane", "kiwi"]
// "orange" a été supprimé
```

### Supprimer plusieurs éléments

```javascript
const nombres = [1, 2, 3, 4, 5, 6];

// Supprimer 3 éléments à partir de l'index 2
nombres.splice(2, 3);

console.log(nombres);  // [1, 2, 6]
// 3, 4, 5 ont été supprimés
```

### Récupérer les éléments supprimés

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];

const supprimes = fruits.splice(1, 2);

console.log(supprimes);  // ["banane", "orange"]
console.log(fruits);     // ["pomme", "kiwi"]
```

### Supprimer depuis la fin

Utilisez des index négatifs pour compter depuis la fin :

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];

// Supprimer 1 élément à partir de l'avant-dernier
fruits.splice(-2, 1);

console.log(fruits);  // ["pomme", "banane", "kiwi"]
// "orange" a été supprimé
```

### Supprimer tous les éléments après un index

Omettez le deuxième paramètre pour supprimer jusqu'à la fin :

```javascript
const nombres = [1, 2, 3, 4, 5];

// Supprimer tous les éléments à partir de l'index 2
nombres.splice(2);

console.log(nombres);  // [1, 2]
```

---

## splice() - Ajouter des éléments

### Ajouter sans supprimer

Pour ajouter des éléments sans en supprimer, mettez `0` comme deuxième paramètre :

```javascript
const fruits = ["pomme", "orange"];

// Ajouter "banane" à l'index 1, sans rien supprimer
fruits.splice(1, 0, "banane");

console.log(fruits);  // ["pomme", "banane", "orange"]
```

### Ajouter plusieurs éléments

```javascript
const nombres = [1, 5];

// Ajouter 2, 3, 4 à l'index 1
nombres.splice(1, 0, 2, 3, 4);

console.log(nombres);  // [1, 2, 3, 4, 5]
```

### Ajouter au début

```javascript
const fruits = ["banane", "orange"];

fruits.splice(0, 0, "pomme");

console.log(fruits);  // ["pomme", "banane", "orange"]
```

### Ajouter à la fin

```javascript
const fruits = ["pomme", "banane"];

fruits.splice(fruits.length, 0, "orange", "kiwi");

console.log(fruits);  // ["pomme", "banane", "orange", "kiwi"]
```

> 💡 **Note** : Pour ajouter à la fin, `push()` est plus simple et plus lisible.

---

## splice() - Remplacer des éléments

Combinez suppression et ajout pour remplacer :

### Remplacer un élément

```javascript
const fruits = ["pomme", "banane", "orange"];

// Remplacer l'élément à l'index 1
fruits.splice(1, 1, "fraise");

console.log(fruits);  // ["pomme", "fraise", "orange"]
```

### Remplacer plusieurs éléments

```javascript
const nombres = [1, 2, 3, 4, 5];

// Remplacer 3 éléments à partir de l'index 1
nombres.splice(1, 3, 10, 20);

console.log(nombres);  // [1, 10, 20, 5]
// 2, 3, 4 ont été remplacés par 10, 20
```

### Remplacer par plus d'éléments

```javascript
const lettres = ["a", "b", "c"];

// Remplacer 1 élément par 3 éléments
lettres.splice(1, 1, "x", "y", "z");

console.log(lettres);  // ["a", "x", "y", "z", "c"]
```

---

## splice() - Exemples pratiques

### Exemple 1 : Retirer un élément spécifique

```javascript
const taches = ["Courses", "Ménage", "Appeler", "Cuisiner"];

// Retirer "Ménage" (index 1)
taches.splice(1, 1);

console.log(taches);  // ["Courses", "Appeler", "Cuisiner"]
```

### Exemple 2 : Insérer un élément au milieu

```javascript
const etapes = ["Début", "Fin"];

// Insérer "Milieu" entre les deux
etapes.splice(1, 0, "Milieu");

console.log(etapes);  // ["Début", "Milieu", "Fin"]
```

### Exemple 3 : Remplacer un élément défectueux

```javascript
const produits = ["Livre", "Stylo cassé", "Cahier"];

// Remplacer le stylo cassé
produits.splice(1, 1, "Stylo neuf");

console.log(produits);  // ["Livre", "Stylo neuf", "Cahier"]
```

### Exemple 4 : Réorganiser un tableau

```javascript
const ordre = ["Premier", "Troisième", "Deuxième", "Quatrième"];

// Déplacer "Deuxième" à sa place
const element = ordre.splice(2, 1)[0];  // Retirer
ordre.splice(1, 0, element);            // Réinsérer

console.log(ordre);  // ["Premier", "Deuxième", "Troisième", "Quatrième"]
```

### Exemple 5 : Vider une partie du tableau

```javascript
const donnees = [1, 2, 3, 4, 5, 6, 7, 8];

// Vider du milieu (index 2 à 5)
donnees.splice(2, 4);

console.log(donnees);  // [1, 2, 7, 8]
```

---

## slice() - Extraire une copie partielle

La méthode `slice()` crée un **nouveau tableau** contenant une portion du tableau original, **sans modifier l'original**.

### Syntaxe

```javascript
tableau.slice(indexDebut, indexFin)
```

**Paramètres** :
- `indexDebut` : Index de début (inclus)
- `indexFin` : Index de fin (exclus) - optionnel

**Valeur de retour** : Nouveau tableau contenant les éléments extraits

⚠️ **Important** : L'index de fin est **EXCLUS** (non inclus).

---

## slice() - Extraire des portions

### Extraire du milieu

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi", "mangue"];

// Extraire de l'index 1 à 3 (3 exclus)
const milieu = fruits.slice(1, 3);

console.log(milieu);  // ["banane", "orange"]
console.log(fruits);  // ["pomme", "banane", "orange", "kiwi", "mangue"] (intact)
```

### Visualisation des index

```javascript
const arr = ["a", "b", "c", "d", "e"];
//           0    1    2    3    4

arr.slice(1, 3);  // ["b", "c"]
//        ↑   ↑
//     inclus  exclus
```

### Extraire depuis un index jusqu'à la fin

Omettez le deuxième paramètre :

```javascript
const nombres = [1, 2, 3, 4, 5];

const fin = nombres.slice(2);

console.log(fin);  // [3, 4, 5]
```

### Extraire depuis le début

Utilisez `0` comme premier paramètre :

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];

const debut = fruits.slice(0, 2);

console.log(debut);  // ["pomme", "banane"]
```

---

## slice() - Index négatifs

Les index négatifs comptent depuis la fin du tableau :

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi", "mangue"];
//             0        1         2         3       4
//            -5       -4        -3        -2      -1

// Extraire les 2 derniers éléments
const derniers = fruits.slice(-2);
console.log(derniers);  // ["kiwi", "mangue"]

// Extraire du 2e élément en partant de la fin jusqu'au dernier (exclus)
const selection = fruits.slice(-3, -1);
console.log(selection);  // ["orange", "kiwi"]
```

---

## slice() - Cas particuliers

### Copier tout le tableau

Sans paramètres, `slice()` copie tout le tableau :

```javascript
const original = [1, 2, 3, 4, 5];
const copie = original.slice();

copie[0] = 999;

console.log(original);  // [1, 2, 3, 4, 5] (intact)
console.log(copie);     // [999, 2, 3, 4, 5]
```

C'est équivalent à :

```javascript
const copie = [...original];  // Spread operator (plus moderne)
```

### Index de fin plus petit que début

Si l'index de fin est plus petit que le début, retourne un tableau vide :

```javascript
const nombres = [1, 2, 3, 4, 5];

const resultat = nombres.slice(3, 1);

console.log(resultat);  // []
```

### Index hors limites

Si les index dépassent la taille du tableau, JavaScript ajuste automatiquement :

```javascript
const nombres = [1, 2, 3];

console.log(nombres.slice(0, 100));  // [1, 2, 3]
console.log(nombres.slice(10, 20));  // []
```

---

## slice() - Exemples pratiques

### Exemple 1 : Pagination

```javascript
const articles = ["A1", "A2", "A3", "A4", "A5", "A6", "A7", "A8"];
const articlesParPage = 3;

// Page 1 (articles 0-2)
const page1 = articles.slice(0, 3);
console.log(page1);  // ["A1", "A2", "A3"]

// Page 2 (articles 3-5)
const page2 = articles.slice(3, 6);
console.log(page2);  // ["A4", "A5", "A6"]

// Page 3 (articles 6-8)
const page3 = articles.slice(6, 9);
console.log(page3);  // ["A7", "A8"]
```

### Exemple 2 : Obtenir les N premiers éléments

```javascript
const scores = [95, 87, 92, 78, 88, 85, 90];

// Top 3 scores
const top3 = scores.slice(0, 3);
console.log(top3);  // [95, 87, 92]
```

### Exemple 3 : Obtenir les N derniers éléments

```javascript
const historique = ["Action 1", "Action 2", "Action 3", "Action 4", "Action 5"];

// 3 dernières actions
const dernieres = historique.slice(-3);
console.log(dernieres);  // ["Action 3", "Action 4", "Action 5"]
```

### Exemple 4 : Exclure les extrémités

```javascript
const donnees = [0, 1, 2, 3, 4, 5, 6];

// Exclure le premier et le dernier
const milieu = donnees.slice(1, -1);
console.log(milieu);  // [1, 2, 3, 4, 5]
```

### Exemple 5 : Créer des sections

```javascript
const menu = ["🏠 Accueil", "📧 Contact", "📱 Services", "ℹ️ À propos", "🔒 Connexion"];

// Navigation principale (3 premiers)
const navPrincipale = menu.slice(0, 3);
console.log(navPrincipale);  // ["🏠 Accueil", "📧 Contact", "📱 Services"]

// Navigation secondaire (reste)
const navSecondaire = menu.slice(3);
console.log(navSecondaire);  // ["ℹ️ À propos", "🔒 Connexion"]
```

---

## Comparaison : splice() vs slice()

### Tableau comparatif

| Critère               | splice()                    | slice()                      |
|-----------------------|-----------------------------|------------------------------|
| Modifie l'original ?  | ✅ OUI                      | ❌ NON                       |
| Action                | Supprimer/ajouter/remplacer | Extraire une copie           |
| Paramètres            | (début, nbSuppr, ...ajouts) | (début, fin)                 |
| Retourne              | Éléments supprimés          | Nouvelle portion du tableau  |
| Mutation              | Mutable                     | Immutable                    |
| Index de fin          | Compte (nombre à supprimer) | Position (exclus)            |

### Exemple côte à côte

```javascript
// SPLICE - Modifie l'original
const arr1 = [1, 2, 3, 4, 5];
const supprimes = arr1.splice(1, 2);
console.log(arr1);        // [1, 4, 5] (modifié !)
console.log(supprimes);   // [2, 3]

// SLICE - Original intact
const arr2 = [1, 2, 3, 4, 5];
const extraits = arr2.slice(1, 3);
console.log(arr2);        // [1, 2, 3, 4, 5] (intact)
console.log(extraits);    // [2, 3]
```

### Mnémotechnique

- **spliCe** : **C**hange (modifie) le tableau
- **sliCe** : **C**opie (crée un nouveau tableau)

---

## Erreurs courantes et pièges

### ❌ Confondre splice et slice

```javascript
const fruits = ["pomme", "banane", "orange"];

// Vouloir copier, mais utiliser splice par erreur
const copie = fruits.splice(0, 2);  // ❌ Modifie fruits !
console.log(fruits);  // ["orange"] (détruit !)
console.log(copie);   // ["pomme", "banane"]

// Solution : utiliser slice
const fruits2 = ["pomme", "banane", "orange"];
const copie2 = fruits2.slice(0, 2);  // ✅ Correct
console.log(fruits2);  // ["pomme", "banane", "orange"] (intact)
console.log(copie2);   // ["pomme", "banane"]
```

### ❌ Oublier que splice modifie l'original

```javascript
const original = [1, 2, 3, 4, 5];
const copie = original;  // ⚠️ Pas une vraie copie !

copie.splice(2, 1);

console.log(original);  // [1, 2, 4, 5] (modifié !)
console.log(copie);     // [1, 2, 4, 5]
```

### ❌ Confondre les paramètres de splice

```javascript
const nombres = [1, 2, 3, 4, 5];

// splice(début, NOMBRE À SUPPRIMER, éléments à ajouter)
nombres.splice(1, 3);  // Supprime 3 éléments à partir de l'index 1

// slice(début, INDEX DE FIN exclus)
const copie = nombres.slice(1, 3);  // Copie de l'index 1 à 2
```

### ❌ Index de fin inclusif dans slice

```javascript
const fruits = ["a", "b", "c", "d"];

// Vouloir extraire "b" et "c"
const mauvais = fruits.slice(1, 2);  // ❌ Seulement ["b"]
const correct = fruits.slice(1, 3);  // ✅ ["b", "c"]
//                             ↑ 3 est exclus, donc arrête à l'index 2
```

---

## Cas d'usage : Quand utiliser quoi ?

### Utilisez splice() quand :

- ✅ Vous voulez **supprimer** des éléments du tableau
- ✅ Vous voulez **ajouter** des éléments au milieu du tableau
- ✅ Vous voulez **remplacer** des éléments
- ✅ Vous voulez **modifier le tableau original** directement

### Utilisez slice() quand :

- ✅ Vous voulez **extraire** une portion sans modifier l'original
- ✅ Vous voulez **copier** le tableau (ou une partie)
- ✅ Vous voulez **créer un nouveau tableau** à partir d'une sélection
- ✅ Vous voulez **préserver le tableau original** (approche immutable)

---

## Alternatives modernes

### Alternative à splice() pour l'immutabilité

Si vous voulez éviter de modifier l'original avec splice() :

```javascript
const original = [1, 2, 3, 4, 5];

// Supprimer l'élément à l'index 2 sans modifier original
const nouveau = [
  ...original.slice(0, 2),
  ...original.slice(3)
];

console.log(original);  // [1, 2, 3, 4, 5] (intact)
console.log(nouveau);   // [1, 2, 4, 5]
```

### Alternative avec filter()

Pour supprimer par condition plutôt que par index :

```javascript
const nombres = [1, 2, 3, 4, 5];

// Supprimer tous les nombres pairs
const impairs = nombres.filter(n => n % 2 !== 0);

console.log(nombres);  // [1, 2, 3, 4, 5] (intact)
console.log(impairs);  // [1, 3, 5]
```

---

## Combinaison des deux méthodes

Vous pouvez combiner `slice()` et `splice()` pour des opérations complexes :

### Exemple : Dupliquer et modifier

```javascript
const original = [1, 2, 3, 4, 5];

// Créer une copie et la modifier
const copie = original.slice();  // Copier
copie.splice(2, 1);              // Modifier la copie

console.log(original);  // [1, 2, 3, 4, 5] (intact)
console.log(copie);     // [1, 2, 4, 5]
```

### Exemple : Insérer une portion dans un autre tableau

```javascript
const arr1 = [1, 2, 7, 8];
const arr2 = [3, 4, 5, 6];

// Insérer arr2 au milieu de arr1
const portion = arr2.slice();  // Copier arr2
arr1.splice(2, 0, ...portion); // Insérer dans arr1

console.log(arr1);  // [1, 2, 3, 4, 5, 6, 7, 8]
```

---

## Performances

### splice()
- Complexité : O(n) - doit déplacer les éléments après la modification
- Plus lent sur de grands tableaux
- Rapide pour les opérations à la fin

### slice()
- Complexité : O(n) - doit copier les éléments
- Performant pour des petites portions
- Copie superficielle (références pour les objets)

> 💡 **Conseil** : Pour des opérations fréquentes au milieu de très grands tableaux, envisagez des structures de données différentes (listes chaînées, etc.).

---

## Points clés à retenir

- ✅ **splice()** modifie le tableau original (mutable)
- ✅ **slice()** crée un nouveau tableau (immutable)
- ✅ splice() : `(début, nombre, ...ajouts)`
- ✅ slice() : `(début, fin)` où fin est **exclus**
- ✅ splice() retourne les éléments supprimés
- ✅ slice() retourne une copie partielle
- ✅ Index négatifs comptent depuis la fin
- ✅ slice() sans paramètres copie tout le tableau
- ✅ Ne confondez pas ces deux méthodes !

---

## Aide-mémoire visuel

```javascript
const arr = [1, 2, 3, 4, 5];

// SPLICE - Modifier l'original
arr.splice(2, 1);        // Supprime à l'index 2
// arr est maintenant [1, 2, 4, 5] ⚠️

// SLICE - Copier une portion
const nouveau = arr.slice(1, 3);  // Copie index 1-2
// arr reste [1, 2, 3, 4, 5] ✅
// nouveau = [2, 3]
```

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez les méthodes modernes de recherche dans les tableaux : `find()`, `findIndex()` et `includes()`.

---


⏭️ [Méthodes modernes de recherche : find, findIndex, includes](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/08-recherche-moderne.md)
