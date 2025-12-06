🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.1 - Création et initialisation des tableaux

## Qu'est-ce qu'un tableau ?

Un **tableau** (ou *array* en anglais) est une structure de données qui permet de stocker **plusieurs valeurs** dans une seule variable. C'est comme une liste ordonnée où chaque élément a une position numérotée (appelée **index**).

### Pourquoi utiliser des tableaux ?

Au lieu de créer plusieurs variables individuelles :

```javascript
const fruit1 = "pomme";
const fruit2 = "banane";
const fruit3 = "orange";
```

On peut regrouper toutes ces valeurs dans un seul tableau :

```javascript
const fruits = ["pomme", "banane", "orange"];
```

---

## Création d'un tableau vide

Il existe deux syntaxes pour créer un tableau vide en JavaScript.

### Syntaxe moderne recommandée : les crochets `[]`

```javascript
const monTableau = [];
```

Cette syntaxe est **la plus courante et la plus recommandée** en JavaScript moderne.

### Syntaxe avec le constructeur `Array()`

```javascript
const monTableau = new Array();
```

Cette syntaxe fonctionne également, mais elle est **moins utilisée** car les crochets sont plus simples et plus lisibles.

> 💡 **Bonne pratique** : Privilégiez toujours la syntaxe avec les crochets `[]`.

---

## Création d'un tableau avec des valeurs initiales

La plupart du temps, vous créerez des tableaux directement avec des valeurs à l'intérieur.

### Syntaxe de base

```javascript
const fruits = ["pomme", "banane", "orange"];
```

Les éléments du tableau sont :
- Séparés par des **virgules** `,`
- Entourés de **crochets** `[]`

### Tableaux avec différents types de données

Un tableau peut contenir n'importe quel type de données JavaScript.

#### Tableau de nombres

```javascript
const notes = [15, 18, 12, 14, 16];
```

#### Tableau de chaînes de caractères

```javascript
const prenoms = ["Alice", "Bob", "Charlie"];
```

#### Tableau de booléens

```javascript
const reponses = [true, false, true, true];
```

#### Tableau mixte (plusieurs types)

JavaScript permet de mélanger différents types dans un même tableau :

```javascript
const donneesMelangees = ["Alice", 25, true, "Développeuse"];
```

> ⚠️ **Attention** : Bien que possible, mélanger les types dans un tableau est souvent déconseillé car cela rend le code plus difficile à comprendre. Essayez de garder des tableaux homogènes (avec des éléments du même type).

---

## Tableaux contenant d'autres tableaux

Un tableau peut contenir d'autres tableaux ! On appelle cela un **tableau multidimensionnel** ou **tableau de tableaux**.

### Tableau à deux dimensions (comme une grille)

```javascript
const grille = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
```

Cela ressemble à un tableau avec 3 lignes et 3 colonnes.

### Exemple pratique : liste de courses par catégorie

```javascript
const courses = [
  ["pommes", "bananes", "oranges"],      // Fruits
  ["carottes", "salade", "tomates"],     // Légumes
  ["pain", "croissants", "baguette"]     // Boulangerie
];
```

---

## Création avec le constructeur `Array()` et une taille

Vous pouvez créer un tableau avec une taille prédéfinie, mais vide :

```javascript
const tableauVide = new Array(5);
console.log(tableauVide);  // [ <5 empty items> ]
console.log(tableauVide.length);  // 5
```

Ce tableau contient 5 emplacements vides (non définis).

> 💡 **Note** : Cette syntaxe est rarement utilisée en pratique. Il est plus courant de créer un tableau vide `[]` et d'ajouter des éléments au fur et à mesure.

---

## Création avec `Array.of()`

La méthode `Array.of()` permet de créer un tableau avec les valeurs passées en paramètres :

```javascript
const nombres = Array.of(1, 2, 3, 4, 5);
console.log(nombres);  // [1, 2, 3, 4, 5]
```

C'est équivalent à :

```javascript
const nombres = [1, 2, 3, 4, 5];
```

> 💡 **Bonne pratique** : La syntaxe avec les crochets `[]` est plus simple et plus lisible. `Array.of()` est rarement nécessaire.

---

## Longueur d'un tableau dès la création

Dès qu'un tableau est créé, vous pouvez connaître sa longueur avec la propriété `.length` :

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits.length);  // 3
```

Un tableau vide a une longueur de `0` :

```javascript
const vide = [];
console.log(vide.length);  // 0
```

---

## Déclaration moderne : `const` ou `let` ?

### Utiliser `const` (recommandé)

Dans la plupart des cas, déclarez vos tableaux avec `const` :

```javascript
const fruits = ["pomme", "banane"];
```

Même avec `const`, vous pouvez **modifier le contenu** du tableau :

```javascript
const fruits = ["pomme", "banane"];
fruits.push("orange");  // ✅ Fonctionne
console.log(fruits);  // ["pomme", "banane", "orange"]
```

Ce qui est interdit, c'est de **réassigner** complètement le tableau :

```javascript
const fruits = ["pomme", "banane"];
fruits = ["kiwi"];  // ❌ Erreur ! Impossible avec const
```

### Utiliser `let` (cas particuliers)

Utilisez `let` seulement si vous devez réassigner complètement le tableau :

```javascript
let fruits = ["pomme"];
fruits = ["banane", "orange"];  // ✅ Possible avec let
```

> 💡 **Bonne pratique** : Préférez toujours `const` sauf si vous avez une raison spécifique d'utiliser `let`.

---

## Exemples pratiques

### Exemple 1 : Liste de tâches

```javascript
const taches = [
  "Faire les courses",
  "Répondre aux emails",
  "Terminer le projet"
];

console.log(taches);
// ["Faire les courses", "Répondre aux emails", "Terminer le projet"]
```

### Exemple 2 : Statistiques d'un jeu

```javascript
const scores = [1250, 980, 1500, 750, 2100];
console.log(scores.length);  // 5 joueurs
```

### Exemple 3 : Configuration d'une application

```javascript
const config = [true, false, true, false];
// [notifications, modeNuit, sauvegardeAuto, sons]
```

---

## Points clés à retenir

- ✅ Un tableau permet de stocker plusieurs valeurs dans une seule variable
- ✅ Créer un tableau avec la syntaxe des crochets : `const tab = []`
- ✅ Initialiser un tableau avec des valeurs : `const tab = [1, 2, 3]`
- ✅ Les éléments sont séparés par des virgules
- ✅ Un tableau peut contenir n'importe quel type de données
- ✅ Utiliser `const` pour déclarer les tableaux (sauf cas particuliers)
- ✅ La propriété `.length` donne le nombre d'éléments

---

## Pour aller plus loin

Dans les prochaines sections, vous apprendrez à :
- Accéder aux éléments d'un tableau avec les index
- Modifier les valeurs d'un tableau
- Ajouter et supprimer des éléments
- Parcourir les tableaux avec des boucles
- Utiliser les méthodes modernes de manipulation de tableaux

---


⏭️ [Accès et modification d'éléments](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/02-acces-modification.md)
