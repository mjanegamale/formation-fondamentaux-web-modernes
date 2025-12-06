🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.2 - Accès et modification d'éléments

## Comprendre les index

Dans un tableau, chaque élément a une **position** appelée **index**. C'est comme les numéros de siège dans un cinéma ou les cases d'un casier.

### Les index commencent à 0

⚠️ **Point crucial** : En JavaScript (et dans la plupart des langages de programmation), les index commencent à **0**, pas à 1 !

```javascript
const fruits = ["pomme", "banane", "orange"];
//              index 0   index 1    index 2
```

| Élément  | Index |
|----------|-------|
| "pomme"  | 0     |
| "banane" | 1     |
| "orange" | 2     |

Le premier élément est à l'index `0`, le deuxième à l'index `1`, et ainsi de suite.

---

## Accéder à un élément du tableau

Pour accéder à un élément spécifique, utilisez les **crochets** avec l'index :

### Syntaxe

```javascript
nomDuTableau[index]
```

### Exemples

```javascript
const fruits = ["pomme", "banane", "orange"];

console.log(fruits[0]);  // "pomme"
console.log(fruits[1]);  // "banane"
console.log(fruits[2]);  // "orange"
```

### Utiliser une variable comme index

L'index peut être une variable :

```javascript
const fruits = ["pomme", "banane", "orange"];
const position = 1;

console.log(fruits[position]);  // "banane"
```

---

## Accéder au premier et au dernier élément

### Premier élément

Le premier élément est toujours à l'index `0` :

```javascript
const fruits = ["pomme", "banane", "orange"];
const premier = fruits[0];
console.log(premier);  // "pomme"
```

### Dernier élément

Pour accéder au dernier élément, utilisez `length - 1` :

```javascript
const fruits = ["pomme", "banane", "orange"];
const dernier = fruits[fruits.length - 1];
console.log(dernier);  // "orange"
```

**Pourquoi `length - 1` ?**

Parce que les index commencent à 0 :
- Un tableau de 3 éléments a les index : 0, 1, 2
- Le dernier index est donc 3 - 1 = 2

```javascript
const notes = [15, 18, 12, 14, 16];
console.log(notes.length);        // 5 éléments
console.log(notes[4]);            // 16 (dernier élément, index 4)
console.log(notes[notes.length - 1]);  // 16 (même résultat)
```

### Avant-dernier élément

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];
const avantDernier = fruits[fruits.length - 2];
console.log(avantDernier);  // "orange"
```

---

## Modifier un élément existant

Pour modifier la valeur d'un élément, utilisez l'opérateur d'affectation `=` :

### Syntaxe

```javascript
nomDuTableau[index] = nouvelleValeur;
```

### Exemples

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits);  // ["pomme", "banane", "orange"]

// Modifier le deuxième élément (index 1)
fruits[1] = "fraise";
console.log(fruits);  // ["pomme", "fraise", "orange"]
```

```javascript
const scores = [10, 20, 30];
scores[0] = 15;      // Modifier le premier élément
scores[2] = 35;      // Modifier le troisième élément
console.log(scores); // [15, 20, 35]
```

### Modifier avec `const`

Même si le tableau est déclaré avec `const`, vous pouvez modifier ses éléments :

```javascript
const nombres = [1, 2, 3];
nombres[0] = 10;     // ✅ Autorisé
console.log(nombres); // [10, 2, 3]
```

Ce qui est interdit, c'est de réassigner complètement le tableau :

```javascript
const nombres = [1, 2, 3];
nombres = [4, 5, 6]; // ❌ Erreur avec const !
```

---

## Que se passe-t-il avec un index invalide ?

### Index trop grand (hors limites)

Si vous essayez d'accéder à un index qui n'existe pas, JavaScript retourne `undefined` :

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits[10]);  // undefined (pas d'erreur)
```

### Modifier un index hors limites

Vous pouvez créer des "trous" dans un tableau :

```javascript
const fruits = ["pomme", "banane"];
console.log(fruits.length);  // 2

fruits[5] = "orange";
console.log(fruits);  // ["pomme", "banane", <3 empty items>, "orange"]
console.log(fruits.length);  // 6
```

Les index 2, 3 et 4 sont maintenant des emplacements vides (`undefined`).

> ⚠️ **Attention** : Évitez de créer des trous dans vos tableaux. Utilisez plutôt les méthodes d'ajout comme `push()` que vous verrez plus tard.

### Index négatif

JavaScript ne supporte **pas** les index négatifs comme certains langages (Python par exemple) :

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits[-1]);  // undefined (pas "orange")
```

Pour accéder aux éléments en partant de la fin, utilisez toujours `length - 1`, `length - 2`, etc.

---

## Accès dans les tableaux multidimensionnels

Pour accéder aux éléments d'un tableau contenu dans un autre tableau, utilisez plusieurs paires de crochets :

### Syntaxe

```javascript
tableau[indexLigne][indexColonne]
```

### Exemple : grille de jeu

```javascript
const grille = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

console.log(grille[0]);     // [1, 2, 3] - première ligne
console.log(grille[0][0]);  // 1 - ligne 0, colonne 0
console.log(grille[1][2]);  // 6 - ligne 1, colonne 2
console.log(grille[2][1]);  // 8 - ligne 2, colonne 1
```

Visualisation :

```
     Col 0  Col 1  Col 2
Ligne 0: 1     2     3
Ligne 1: 4     5     6
Ligne 2: 7     8     9
```

### Modifier dans un tableau multidimensionnel

```javascript
const grille = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

grille[1][1] = 50;  // Modifier le centre
console.log(grille);
// [[1, 2, 3], [4, 50, 6], [7, 8, 9]]
```

### Exemple pratique : emploi du temps

```javascript
const emploiDuTemps = [
  ["Maths", "Français", "Sport"],      // Lundi
  ["Anglais", "Histoire", "Sciences"], // Mardi
  ["Art", "Maths", "Informatique"]     // Mercredi
];

// Quel cours le mardi (index 1) à la 3e heure (index 2) ?
console.log(emploiDuTemps[1][2]);  // "Sciences"

// Changer le cours du mercredi matin
emploiDuTemps[2][0] = "Musique";
console.log(emploiDuTemps[2]);  // ["Musique", "Maths", "Informatique"]
```

---

## Utiliser les valeurs d'un tableau

Une fois récupérée, une valeur de tableau peut être utilisée comme n'importe quelle variable :

### Dans des calculs

```javascript
const notes = [15, 18, 12];
const moyenne = (notes[0] + notes[1] + notes[2]) / 3;
console.log(moyenne);  // 15
```

### Dans des conditions

```javascript
const temperatures = [18, 22, 15, 25];

if (temperatures[3] > 20) {
  console.log("Il fait chaud !");  // Sera affiché
}
```

### Dans des chaînes de caractères

```javascript
const prenoms = ["Alice", "Bob", "Charlie"];
console.log("Bonjour " + prenoms[0]);  // "Bonjour Alice"

// Avec template literals (moderne)
console.log(`Bonjour ${prenoms[0]} !`);  // "Bonjour Alice !"
```

### Assigner à d'autres variables

```javascript
const fruits = ["pomme", "banane", "orange"];
const fruitPrefere = fruits[1];
console.log(fruitPrefere);  // "banane"
```

---

## Exemples pratiques complets

### Exemple 1 : Gestion d'un inventaire

```javascript
const stock = [50, 30, 20, 15];
// [ordinateurs, claviers, souris, écrans]

console.log("Ordinateurs en stock :", stock[0]);  // 50

// Vente de 5 ordinateurs
stock[0] = stock[0] - 5;
console.log("Après vente :", stock[0]);  // 45

// Réapprovisionnement de 10 écrans
stock[3] = stock[3] + 10;
console.log("Écrans après réappro :", stock[3]);  // 25
```

### Exemple 2 : Podium d'une course

```javascript
const coureurs = ["Marie", "Lucas", "Sophie", "Tom"];

const premier = coureurs[0];
const deuxieme = coureurs[1];
const troisieme = coureurs[2];

console.log("🥇 1er :", premier);   // Marie
console.log("🥈 2e :", deuxieme);   // Lucas
console.log("🥉 3e :", troisieme);  // Sophie
```

### Exemple 3 : Modification de configuration

```javascript
const parametres = [true, false, "français", 100];
// [notifications, modeNuit, langue, volume]

console.log("Notifications :", parametres[0]);  // true

// Activer le mode nuit
parametres[1] = true;

// Baisser le volume
parametres[3] = 50;

console.log(parametres);
// [true, true, "français", 50]
```

---

## Erreurs courantes à éviter

### ❌ Oublier que les index commencent à 0

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits[1]);  // Pas "pomme" mais "banane" !
```

### ❌ Utiliser `length` comme index

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits[fruits.length]);  // undefined !
// Il faut fruits[fruits.length - 1] pour le dernier
```

### ❌ Confondre parenthèses et crochets

```javascript
const fruits = ["pomme", "banane", "orange"];
console.log(fruits(0));  // ❌ Erreur !
console.log(fruits[0]);  // ✅ Correct
```

---

## Points clés à retenir

- ✅ Les index commencent toujours à **0**
- ✅ Syntaxe d'accès : `tableau[index]`
- ✅ Premier élément : `tableau[0]`
- ✅ Dernier élément : `tableau[tableau.length - 1]`
- ✅ Modification : `tableau[index] = nouvelleValeur`
- ✅ Index invalide retourne `undefined` (pas d'erreur)
- ✅ Tableaux 2D : `tableau[ligne][colonne]`
- ✅ On peut modifier un tableau déclaré avec `const`

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez le **destructuring**, une syntaxe moderne qui simplifie l'extraction de valeurs des tableaux.

---


⏭️ [Destructuring de tableaux](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/03-destructuring-tableaux.md)
