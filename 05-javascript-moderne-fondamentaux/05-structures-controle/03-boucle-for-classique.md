🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.3 - Boucle for classique

## Introduction

La boucle `for` est l'une des structures de répétition les plus utilisées en programmation. Elle permet d'exécuter un bloc de code un nombre déterminé de fois, ce qui évite de répéter le même code manuellement.

Imaginez que vous devez compter de 1 à 100. Sans boucle, vous devriez écrire 100 lignes de code ! Avec une boucle `for`, vous n'en écrivez qu'une seule. 🚀

---

## Pourquoi utiliser des boucles ?

### Sans boucle (répétitif et peu pratique)

```javascript
console.log("Ligne 1");
console.log("Ligne 2");
console.log("Ligne 3");
console.log("Ligne 4");
console.log("Ligne 5");
// Et ainsi de suite... 😰
```

### Avec une boucle (élégant et efficace)

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(`Ligne ${i}`);
}
```

**Résultat :**
```
Ligne 1
Ligne 2
Ligne 3
Ligne 4
Ligne 5
```

---

## Syntaxe de la boucle `for`

```javascript
for (initialisation; condition; incrémentation) {
  // Code à répéter
}
```

### Les trois parties essentielles

1. **Initialisation** : Définit la variable de compteur (exécutée une seule fois au début)
2. **Condition** : Détermine si la boucle continue (testée avant chaque itération)
3. **Incrémentation** : Modifie le compteur après chaque itération

### Schéma de fonctionnement

```
1. Initialisation (i = 0)
     ↓
2. Test de condition (i < 5) → Vrai ?
     ↓ OUI
3. Exécution du code dans les accolades
     ↓
4. Incrémentation (i++)
     ↓
   Retour à l'étape 2

Quand la condition devient FAUSSE → La boucle s'arrête
```

---

## Premier exemple simple

```javascript
for (let i = 0; i < 5; i++) {
  console.log(`Itération numéro ${i}`);
}
```

**Résultat :**
```
Itération numéro 0
Itération numéro 1
Itération numéro 2
Itération numéro 3
Itération numéro 4
```

### Décortiquons ce code

- **`let i = 0`** : On crée une variable `i` qui commence à 0
- **`i < 5`** : La boucle continue tant que `i` est inférieur à 5
- **`i++`** : À la fin de chaque tour, on augmente `i` de 1
- La boucle s'exécute **5 fois** (pour i = 0, 1, 2, 3, 4)

---

## Compter de 1 à 10

```javascript
for (let i = 1; i <= 10; i++) {
  console.log(i);
}
```

**Résultat :**
```
1
2
3
4
5
6
7
8
9
10
```

**Note :** On commence à 1 et on utilise `<=` pour inclure 10.

---

## Différentes façons d'incrémenter

### Incrémenter de 1 en 1 (classique)

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
// 0, 1, 2, 3, 4
```

### Incrémenter de 2 en 2

```javascript
for (let i = 0; i < 10; i += 2) {
  console.log(i);
}
// 0, 2, 4, 6, 8
```

### Incrémenter de 10 en 10

```javascript
for (let i = 0; i <= 100; i += 10) {
  console.log(i);
}
// 0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100
```

### Décrémenter (compter à rebours)

```javascript
for (let i = 5; i >= 1; i--) {
  console.log(i);
}
console.log("🚀 Décollage !");
```

**Résultat :**
```
5
4
3
2
1
🚀 Décollage !
```

---

## Parcourir un tableau

L'une des utilisations les plus courantes de la boucle `for` est de parcourir les éléments d'un tableau.

### Exemple avec un tableau de fruits

```javascript
const fruits = ["pomme", "banane", "orange", "fraise", "kiwi"];

for (let i = 0; i < fruits.length; i++) {
  console.log(`Fruit ${i + 1} : ${fruits[i]}`);
}
```

**Résultat :**
```
Fruit 1 : pomme
Fruit 2 : banane
Fruit 3 : orange
Fruit 4 : fraise
Fruit 5 : kiwi
```

**Explication :**
- `fruits.length` retourne 5 (le nombre d'éléments)
- `i` va de 0 à 4 (indices valides pour un tableau de 5 éléments)
- `fruits[i]` accède à chaque élément du tableau

### Exemple avec un tableau de nombres

```javascript
const notes = [15, 12, 18, 10, 14];
let somme = 0;

for (let i = 0; i < notes.length; i++) {
  somme += notes[i];
}

const moyenne = somme / notes.length;
console.log(`Moyenne : ${moyenne}`);
// Affiche : "Moyenne : 13.8"
```

---

## Créer un tableau avec une boucle

On peut utiliser une boucle `for` pour remplir un tableau.

### Créer un tableau de nombres

```javascript
const nombres = [];

for (let i = 1; i <= 10; i++) {
  nombres.push(i);
}

console.log(nombres);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Créer un tableau de carrés

```javascript
const carres = [];

for (let i = 1; i <= 5; i++) {
  carres.push(i * i);
}

console.log(carres);
// [1, 4, 9, 16, 25]
```

---

## Boucles avec conditions

On peut combiner des boucles avec des conditions `if`.

### Afficher uniquement les nombres pairs

```javascript
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) {
    console.log(`${i} est pair`);
  }
}
```

**Résultat :**
```
2 est pair
4 est pair
6 est pair
8 est pair
10 est pair
```

### Filtrer des éléments d'un tableau

```javascript
const temperatures = [18, 25, 30, 15, 28, 22];
const joursChauds = [];

for (let i = 0; i < temperatures.length; i++) {
  if (temperatures[i] >= 25) {
    joursChauds.push(temperatures[i]);
  }
}

console.log("Températures ≥ 25°C :", joursChauds);
// [25, 30, 28]
```

---

## Boucles imbriquées

On peut placer une boucle à l'intérieur d'une autre boucle.

### Table de multiplication

```javascript
for (let i = 1; i <= 3; i++) {
  console.log(`Table de ${i} :`);

  for (let j = 1; j <= 5; j++) {
    console.log(`  ${i} × ${j} = ${i * j}`);
  }

  console.log(""); // Ligne vide pour la lisibilité
}
```

**Résultat :**
```
Table de 1 :
  1 × 1 = 1
  1 × 2 = 2
  1 × 3 = 3
  1 × 4 = 4
  1 × 5 = 5

Table de 2 :
  2 × 1 = 2
  2 × 2 = 4
  2 × 3 = 6
  2 × 4 = 8
  2 × 5 = 10

Table de 3 :
  3 × 1 = 3
  3 × 2 = 6
  3 × 3 = 9
  3 × 4 = 12
  3 × 5 = 15
```

### Créer une grille

```javascript
let grille = "";

for (let ligne = 0; ligne < 3; ligne++) {
  for (let colonne = 0; colonne < 5; colonne++) {
    grille += "* ";
  }
  grille += "\n"; // Saut de ligne
}

console.log(grille);
```

**Résultat :**
```
* * * * *
* * * * *
* * * * *
```

---

## Contrôle de flux : `break` et `continue`

### `break` : Sortir de la boucle

Le mot-clé `break` arrête immédiatement la boucle.

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    console.log("On s'arrête à 5 !");
    break; // Sort de la boucle
  }
  console.log(i);
}
```

**Résultat :**
```
1
2
3
4
On s'arrête à 5 !
```

### Rechercher un élément dans un tableau

```javascript
const fruits = ["pomme", "banane", "orange", "fraise"];
const recherche = "orange";
let trouve = false;

for (let i = 0; i < fruits.length; i++) {
  if (fruits[i] === recherche) {
    console.log(`✅ ${recherche} trouvé à l'index ${i}`);
    trouve = true;
    break; // On arrête dès qu'on l'a trouvé
  }
}

if (!trouve) {
  console.log(`❌ ${recherche} non trouvé`);
}
```

### `continue` : Passer à l'itération suivante

Le mot-clé `continue` saute l'itération actuelle et passe à la suivante.

```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) {
    continue; // Saute l'itération quand i = 3
  }
  console.log(i);
}
```

**Résultat :**
```
1
2
4
5
```

**Note :** Le 3 n'est pas affiché car `continue` a été exécuté.

### Ignorer les nombres impairs

```javascript
for (let i = 1; i <= 10; i++) {
  if (i % 2 !== 0) {
    continue; // Saute les nombres impairs
  }
  console.log(i);
}
// Affiche : 2, 4, 6, 8, 10
```

---

## Exemples pratiques

### Exemple 1 : Calculer une somme

```javascript
let somme = 0;

for (let i = 1; i <= 100; i++) {
  somme += i;
}

console.log(`La somme de 1 à 100 est : ${somme}`);
// Affiche : "La somme de 1 à 100 est : 5050"
```

### Exemple 2 : Construire une chaîne HTML

```javascript
const prenoms = ["Alice", "Bob", "Charlie", "Diana"];
let listeHTML = "<ul>";

for (let i = 0; i < prenoms.length; i++) {
  listeHTML += `<li>${prenoms[i]}</li>`;
}

listeHTML += "</ul>";

console.log(listeHTML);
```

**Résultat :**
```html
<ul><li>Alice</li><li>Bob</li><li>Charlie</li><li>Diana</li></ul>
```

### Exemple 3 : Compter les voyelles

```javascript
const phrase = "Bonjour le monde";
const voyelles = "aeiouAEIOU";
let compteur = 0;

for (let i = 0; i < phrase.length; i++) {
  if (voyelles.includes(phrase[i])) {
    compteur++;
  }
}

console.log(`Nombre de voyelles : ${compteur}`);
// Affiche : "Nombre de voyelles : 6"
```

### Exemple 4 : Inverser un tableau

```javascript
const nombres = [1, 2, 3, 4, 5];
const inverse = [];

for (let i = nombres.length - 1; i >= 0; i--) {
  inverse.push(nombres[i]);
}

console.log("Original :", nombres);
console.log("Inversé :", inverse);
// Original : [1, 2, 3, 4, 5]
// Inversé : [5, 4, 3, 2, 1]
```

### Exemple 5 : Générer une table d'étoiles

```javascript
for (let i = 1; i <= 5; i++) {
  let ligne = "";
  for (let j = 0; j < i; j++) {
    ligne += "⭐";
  }
  console.log(ligne);
}
```

**Résultat :**
```
⭐
⭐⭐
⭐⭐⭐
⭐⭐⭐⭐
⭐⭐⭐⭐⭐
```

### Exemple 6 : Trouver le plus grand nombre

```javascript
const nombres = [45, 78, 12, 99, 34, 56];
let plusGrand = nombres[0]; // On suppose que le premier est le plus grand

for (let i = 1; i < nombres.length; i++) {
  if (nombres[i] > plusGrand) {
    plusGrand = nombres[i];
  }
}

console.log(`Le plus grand nombre est : ${plusGrand}`);
// Affiche : "Le plus grand nombre est : 99"
```

---

## Portée de la variable de boucle

La variable déclarée avec `let` dans la boucle `for` n'existe que dans la boucle.

```javascript
for (let i = 0; i < 3; i++) {
  console.log(`Dans la boucle : ${i}`);
}

// console.log(i); // ❌ Erreur : i n'est pas défini ici
```

Si vous avez besoin de la variable après la boucle, déclarez-la avant :

```javascript
let i;

for (i = 0; i < 3; i++) {
  console.log(`Dans la boucle : ${i}`);
}

console.log(`Après la boucle : ${i}`); // ✅ Fonctionne, i vaut 3
```

---

## Erreurs courantes

### ❌ Erreur 1 : Boucle infinie

```javascript
// ❌ ATTENTION : Boucle infinie !
for (let i = 0; i < 5; i--) {
  console.log(i);
}
```

**Problème :** `i` décrémente au lieu d'incrémenter, donc `i < 5` reste toujours vrai. La boucle ne s'arrête jamais !

**Solution :** Vérifiez que votre incrémentation va dans le bon sens par rapport à votre condition.

### ❌ Erreur 2 : Mauvaise condition

```javascript
const tableau = [1, 2, 3];

// ❌ Erreur : on dépasse la longueur du tableau
for (let i = 0; i <= tableau.length; i++) {
  console.log(tableau[i]);
}
// Affiche : 1, 2, 3, undefined
```

**Problème :** `i <= tableau.length` va jusqu'à 3, mais le dernier index valide est 2.

**Solution :** Utilisez `i < tableau.length` (sans le `=`).

### ❌ Erreur 3 : Oublier d'incrémenter

```javascript
// ❌ ATTENTION : Boucle infinie !
for (let i = 0; i < 5;) {
  console.log(i);
  // Oubli de i++
}
```

**Solution :** N'oubliez jamais la partie incrémentation.

### ❌ Erreur 4 : Modifier le tableau pendant le parcours

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Comportement imprévisible
for (let i = 0; i < nombres.length; i++) {
  nombres.push(i); // Ajoute des éléments pendant la boucle
}
```

**Problème :** La taille du tableau change pendant qu'on le parcourt, ce qui peut causer une boucle infinie ou des résultats inattendus.

**Solution :** Stockez la longueur dans une variable avant la boucle :

```javascript
const longueur = nombres.length;
for (let i = 0; i < longueur; i++) {
  // ...
}
```

---

## Comparaison avec d'autres types de boucles

### Boucle `for` classique

```javascript
const fruits = ["pomme", "banane", "orange"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

**Avantages :**
- Contrôle total sur l'index
- Peut parcourir dans n'importe quel ordre
- Peut sauter des éléments

**Inconvénients :**
- Plus verbeux
- Risque d'erreurs avec les indices

### Boucle `for...of` (moderne)

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

**Avantages :**
- Plus simple et lisible
- Pas de gestion d'index
- Moderne (ES6+)

**Inconvénients :**
- Pas d'accès direct à l'index (sauf avec `entries()`)

---

## Optimisation et bonnes pratiques

### ✅ Stocker la longueur du tableau

```javascript
const tableau = [1, 2, 3, 4, 5];

// ✅ Bon (plus performant pour de grands tableaux)
const longueur = tableau.length;
for (let i = 0; i < longueur; i++) {
  console.log(tableau[i]);
}
```

**Pourquoi ?** Évite de recalculer `tableau.length` à chaque itération.

### ✅ Utiliser des noms de variables descriptifs

```javascript
// ❌ Peu clair
for (let i = 0; i < t.length; i++) {
  console.log(t[i]);
}

// ✅ Plus clair
for (let index = 0; index < etudiants.length; index++) {
  console.log(etudiants[index]);
}
```

### ✅ Commenter les boucles complexes

```javascript
// Parcourt tous les produits et applique une remise de 10% si le prix > 100€
for (let i = 0; i < produits.length; i++) {
  if (produits[i].prix > 100) {
    produits[i].prix *= 0.9;
  }
}
```

### ✅ Éviter les boucles trop imbriquées

```javascript
// ❌ Difficile à comprendre
for (let i = 0; i < tableau1.length; i++) {
  for (let j = 0; j < tableau2.length; j++) {
    for (let k = 0; k < tableau3.length; k++) {
      // Trop de niveaux !
    }
  }
}

// ✅ Mieux : extraire dans des fonctions
function traiterLigne(ligne) {
  // ...
}

for (let i = 0; i < tableau.length; i++) {
  traiterLigne(tableau[i]);
}
```

---

## Quand utiliser la boucle `for` classique ?

### ✅ Utilisez `for` classique quand :

- Vous avez besoin de l'**index** de l'élément
- Vous devez parcourir le tableau dans un **ordre spécifique** (à l'envers, de 2 en 2, etc.)
- Vous devez **modifier le tableau** pendant le parcours
- Vous travaillez avec des **nombres** (de 1 à 100, etc.)

### ✅ Préférez `for...of` quand :

- Vous voulez juste **lire les valeurs**
- L'ordre n'a pas d'importance
- Vous voulez un code **plus simple et lisible**

---

## Résumé

- La boucle `for` permet de **répéter du code** un nombre déterminé de fois
- Elle se compose de **trois parties** : initialisation, condition, incrémentation
- Très utile pour **parcourir des tableaux** avec l'index
- On peut utiliser `break` pour **sortir** de la boucle
- On peut utiliser `continue` pour **sauter** une itération
- Attention aux **boucles infinies** (vérifiez toujours votre condition et incrémentation)
- Utilisez `let` pour déclarer la variable de boucle
- Pour des cas simples, préférez les méthodes modernes (`for...of`, `forEach`, `map`, etc.)

La boucle `for` classique est un outil fondamental en JavaScript. Bien la maîtriser vous permettra d'écrire du code plus efficace et de comprendre comment fonctionnent les structures de répétition ! 🎯

⏭️ [Boucle for...of (moderne, pour les tableaux)](/05-javascript-moderne-fondamentaux/05-structures-controle/04-boucle-for-of.md)
