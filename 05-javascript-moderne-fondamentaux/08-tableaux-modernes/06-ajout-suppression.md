🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.6 - Méthodes d'ajout/suppression : push, pop, shift, unshift

## Introduction

JavaScript propose **quatre méthodes essentielles** pour ajouter ou retirer des éléments aux extrémités d'un tableau :

| Méthode     | Action                        | Extrémité |
|-------------|-------------------------------|-----------|
| `push()`    | Ajoute un ou plusieurs éléments | Fin       |
| `pop()`     | Retire le dernier élément      | Fin       |
| `unshift()` | Ajoute un ou plusieurs éléments | Début     |
| `shift()`   | Retire le premier élément      | Début     |

⚠️ **Important** : Ces méthodes **modifient le tableau original** (mutation).

---

## push() - Ajouter à la fin

La méthode `push()` ajoute un ou plusieurs éléments **à la fin** du tableau.

### Syntaxe

```javascript
tableau.push(element1, element2, ..., elementN)
```

### Ajouter un élément

```javascript
const fruits = ["pomme", "banane"];

fruits.push("orange");

console.log(fruits);  // ["pomme", "banane", "orange"]
```

### Ajouter plusieurs éléments

```javascript
const nombres = [1, 2, 3];

nombres.push(4, 5, 6);

console.log(nombres);  // [1, 2, 3, 4, 5, 6]
```

### Valeur de retour

`push()` retourne la **nouvelle longueur** du tableau :

```javascript
const fruits = ["pomme", "banane"];

const nouvelleLongueur = fruits.push("orange");

console.log(nouvelleLongueur);  // 3
console.log(fruits.length);     // 3
console.log(fruits);            // ["pomme", "banane", "orange"]
```

### Visualisation

```
Avant:  ["pomme", "banane"]
                            ← push("orange")
Après:  ["pomme", "banane", "orange"]
```

---

## pop() - Retirer de la fin

La méthode `pop()` retire et retourne le **dernier élément** du tableau.

### Syntaxe

```javascript
tableau.pop()
```

Pas de paramètres (retire toujours le dernier élément).

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.pop();

console.log(fruits);  // ["pomme", "banane"]
```

### Valeur de retour

`pop()` retourne l'**élément retiré** :

```javascript
const fruits = ["pomme", "banane", "orange"];

const dernierFruit = fruits.pop();

console.log(dernierFruit);  // "orange"
console.log(fruits);        // ["pomme", "banane"]
```

### Sur un tableau vide

Si le tableau est vide, `pop()` retourne `undefined` :

```javascript
const vide = [];
const resultat = vide.pop();

console.log(resultat);  // undefined
console.log(vide);      // []
```

### Visualisation

```
Avant:  ["pomme", "banane", "orange"]
                            pop() → retire "orange"
Après:  ["pomme", "banane"]
```

---

## unshift() - Ajouter au début

La méthode `unshift()` ajoute un ou plusieurs éléments **au début** du tableau.

### Syntaxe

```javascript
tableau.unshift(element1, element2, ..., elementN)
```

### Ajouter un élément

```javascript
const fruits = ["banane", "orange"];

fruits.unshift("pomme");

console.log(fruits);  // ["pomme", "banane", "orange"]
```

### Ajouter plusieurs éléments

```javascript
const nombres = [3, 4, 5];

nombres.unshift(1, 2);

console.log(nombres);  // [1, 2, 3, 4, 5]
```

L'ordre des éléments ajoutés est préservé.

### Valeur de retour

`unshift()` retourne la **nouvelle longueur** du tableau :

```javascript
const fruits = ["banane", "orange"];

const nouvelleLongueur = fruits.unshift("pomme");

console.log(nouvelleLongueur);  // 3
console.log(fruits);            // ["pomme", "banane", "orange"]
```

### Visualisation

```
              unshift("pomme") ↓
Avant:        ["banane", "orange"]
Après:  ["pomme", "banane", "orange"]
```

---

## shift() - Retirer du début

La méthode `shift()` retire et retourne le **premier élément** du tableau.

### Syntaxe

```javascript
tableau.shift()
```

Pas de paramètres (retire toujours le premier élément).

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.shift();

console.log(fruits);  // ["banane", "orange"]
```

### Valeur de retour

`shift()` retourne l'**élément retiré** :

```javascript
const fruits = ["pomme", "banane", "orange"];

const premierFruit = fruits.shift();

console.log(premierFruit);  // "pomme"
console.log(fruits);        // ["banane", "orange"]
```

### Sur un tableau vide

Si le tableau est vide, `shift()` retourne `undefined` :

```javascript
const vide = [];
const resultat = vide.shift();

console.log(resultat);  // undefined
console.log(vide);      // []
```

### Visualisation

```
Avant:  ["pomme", "banane", "orange"]
         shift() → retire "pomme"
Après:          ["banane", "orange"]
```

---

## Tableau récapitulatif

| Méthode     | Action          | Position | Retourne              | Paramètres          |
|-------------|-----------------|----------|-----------------------|---------------------|
| `push()`    | Ajoute          | Fin      | Nouvelle longueur     | 1+ éléments         |
| `pop()`     | Retire          | Fin      | Élément retiré        | Aucun               |
| `unshift()` | Ajoute          | Début    | Nouvelle longueur     | 1+ éléments         |
| `shift()`   | Retire          | Début    | Élément retiré        | Aucun               |

### Mnémotechnique

- **push** / **pop** : actions sur la **fin** (comme une pile - stack)
- **unshift** / **shift** : actions sur le **début** (comme une file - queue)

```
    shift()  →  [1, 2, 3]  ← push()
                     ↑
                  pop()
```

---

## Mutation du tableau original

⚠️ **Attention** : Ces quatre méthodes **modifient directement** le tableau original.

```javascript
const nombres = [1, 2, 3];

nombres.push(4);      // Modifie nombres
nombres.pop();        // Modifie nombres
nombres.unshift(0);   // Modifie nombres
nombres.shift();      // Modifie nombres

console.log(nombres);  // [1, 2, 3]
```

### Éviter la mutation (si nécessaire)

Si vous voulez créer un nouveau tableau sans modifier l'original, utilisez le spread operator :

```javascript
const original = [1, 2, 3];

// Ajouter à la fin sans mutation
const avecElementFin = [...original, 4];
console.log(original);       // [1, 2, 3] (intact)
console.log(avecElementFin); // [1, 2, 3, 4]

// Ajouter au début sans mutation
const avecElementDebut = [0, ...original];
console.log(original);          // [1, 2, 3] (intact)
console.log(avecElementDebut);  // [0, 1, 2, 3]

// Retirer le dernier sans mutation
const sansDernier = original.slice(0, -1);
console.log(original);      // [1, 2, 3] (intact)
console.log(sansDernier);   // [1, 2]

// Retirer le premier sans mutation
const sansPremier = original.slice(1);
console.log(original);     // [1, 2, 3] (intact)
console.log(sansPremier);  // [2, 3]
```

---

## Combinaisons de méthodes

### Ajouter et récupérer

```javascript
const fruits = ["pomme", "banane"];

// Ajouter "orange" et récupérer la nouvelle longueur
const longueur = fruits.push("orange");
console.log(`Le tableau contient maintenant ${longueur} fruits`);
// "Le tableau contient maintenant 3 fruits"
```

### Retirer et utiliser l'élément

```javascript
const taches = ["Tâche 1", "Tâche 2", "Tâche 3"];

// Retirer et traiter la première tâche
const tacheEnCours = taches.shift();
console.log(`En cours : ${tacheEnCours}`);
console.log(`Tâches restantes : ${taches.length}`);
// "En cours : Tâche 1"
// "Tâches restantes : 2"
```

### Chaîner les méthodes

Vous pouvez enchaîner plusieurs opérations :

```javascript
const nombres = [2, 3, 4];

nombres.unshift(1);  // [1, 2, 3, 4]
nombres.push(5);     // [1, 2, 3, 4, 5]
nombres.shift();     // [2, 3, 4, 5]
nombres.pop();       // [2, 3, 4]

console.log(nombres);  // [2, 3, 4]
```

---

## Exemples pratiques

### Exemple 1 : Pile (Stack) - LIFO (Last In, First Out)

Une pile fonctionne comme une pile d'assiettes : la dernière ajoutée est la première retirée.

```javascript
const pile = [];

// Empiler (ajouter)
pile.push("Assiette 1");
pile.push("Assiette 2");
pile.push("Assiette 3");
console.log(pile);  // ["Assiette 1", "Assiette 2", "Assiette 3"]

// Dépiler (retirer)
const derniere = pile.pop();
console.log(derniere);  // "Assiette 3"
console.log(pile);      // ["Assiette 1", "Assiette 2"]
```

### Exemple 2 : File (Queue) - FIFO (First In, First Out)

Une file fonctionne comme une file d'attente : le premier arrivé est le premier servi.

```javascript
const file = [];

// Ajouter à la file (à la fin)
file.push("Personne 1");
file.push("Personne 2");
file.push("Personne 3");
console.log(file);  // ["Personne 1", "Personne 2", "Personne 3"]

// Servir (retirer du début)
const suivant = file.shift();
console.log(`${suivant} est servie`);  // "Personne 1 est servie"
console.log(file);  // ["Personne 2", "Personne 3"]
```

### Exemple 3 : Historique de navigation

```javascript
const historique = [];
let positionActuelle = -1;

function naviguerVers(page) {
  // Supprimer les pages après la position actuelle
  historique.length = positionActuelle + 1;

  // Ajouter la nouvelle page
  historique.push(page);
  positionActuelle++;

  console.log(`Vous êtes sur : ${page}`);
}

naviguerVers("Accueil");
naviguerVers("Produits");
naviguerVers("Contact");

console.log(historique);
// ["Accueil", "Produits", "Contact"]
```

### Exemple 4 : Gestion d'une playlist

```javascript
const playlist = ["Chanson 1", "Chanson 2", "Chanson 3"];

// Ajouter une chanson à la fin
playlist.push("Chanson 4");
console.log("Playlist :", playlist);

// Jouer et retirer la première chanson
const enCours = playlist.shift();
console.log(`En cours : ${enCours}`);
console.log("Suivantes :", playlist);

// Ajouter une chanson en priorité (au début)
playlist.unshift("Chanson urgente");
console.log("Playlist mise à jour :", playlist);
```

### Exemple 5 : Système de notifications

```javascript
const notifications = [];

function ajouterNotification(message) {
  notifications.push({
    message: message,
    timestamp: new Date()
  });

  // Limiter à 5 notifications
  if (notifications.length > 5) {
    notifications.shift();  // Retirer la plus ancienne
  }
}

ajouterNotification("Nouveau message");
ajouterNotification("Mise à jour disponible");
ajouterNotification("Connexion réussie");
// ... etc
```

### Exemple 6 : Panier d'achat

```javascript
const panier = [];

function ajouterArticle(article) {
  panier.push(article);
  console.log(`${article} ajouté au panier`);
  console.log(`Total: ${panier.length} articles`);
}

function retirerDernierArticle() {
  if (panier.length > 0) {
    const article = panier.pop();
    console.log(`${article} retiré du panier`);
    return article;
  } else {
    console.log("Le panier est vide");
  }
}

ajouterArticle("Pommes");
ajouterArticle("Pain");
ajouterArticle("Lait");
retirerDernierArticle();  // Retire "Lait"
```

---

## Performances

### push() et pop() - Rapides ⚡

Ajouter ou retirer à la fin est **très rapide** (O(1) - temps constant) :

```javascript
const tableau = [1, 2, 3, 4, 5];
tableau.push(6);  // ⚡ Rapide
tableau.pop();    // ⚡ Rapide
```

Pas besoin de déplacer d'autres éléments.

### shift() et unshift() - Plus lents 🐢

Ajouter ou retirer au début est **plus lent** (O(n) - temps linéaire) :

```javascript
const tableau = [1, 2, 3, 4, 5];
tableau.shift();    // 🐢 Plus lent (doit réindexer tous les éléments)
tableau.unshift(0); // 🐢 Plus lent (doit décaler tous les éléments)
```

Tous les éléments doivent être "décalés" pour réindexer le tableau.

### Recommandation

- ✅ Privilégiez `push()` et `pop()` quand possible
- ⚠️ Utilisez `shift()` et `unshift()` avec modération sur de grands tableaux

Pour de grands volumes de données avec beaucoup d'opérations au début, envisagez une structure de données différente (comme une liste chaînée).

---

## Utilisation avec const

Même si un tableau est déclaré avec `const`, vous pouvez utiliser ces méthodes :

```javascript
const fruits = ["pomme", "banane"];

// ✅ Autorisé : modification du contenu
fruits.push("orange");
fruits.pop();
fruits.shift();
fruits.unshift("kiwi");

console.log(fruits);  // ["kiwi", "banane"]

// ❌ Interdit : réassignation complète
fruits = ["nouvelle", "liste"];  // Erreur !
```

`const` empêche la réassignation, pas la mutation.

---

## Différences avec d'autres méthodes

### push() vs concat()

```javascript
const arr1 = [1, 2];

// push() - modifie l'original
arr1.push(3, 4);
console.log(arr1);  // [1, 2, 3, 4]

// concat() - crée un nouveau tableau
const arr2 = [1, 2];
const arr3 = arr2.concat(3, 4);
console.log(arr2);  // [1, 2] (original intact)
console.log(arr3);  // [1, 2, 3, 4]
```

### shift() vs slice()

```javascript
const arr1 = [1, 2, 3];

// shift() - modifie l'original, retourne l'élément
const premier = arr1.shift();
console.log(premier);  // 1
console.log(arr1);     // [2, 3]

// slice() - crée un nouveau tableau
const arr2 = [1, 2, 3];
const sansPremier = arr2.slice(1);
console.log(arr2);          // [1, 2, 3] (original intact)
console.log(sansPremier);   // [2, 3]
```

---

## Cas d'erreurs et pièges

### Oublier que les méthodes modifient le tableau

```javascript
const original = [1, 2, 3];
const copie = original;  // ⚠️ Pas une vraie copie !

copie.push(4);

console.log(original);  // [1, 2, 3, 4] ⚠️ Original modifié !
console.log(copie);     // [1, 2, 3, 4]
```

Solution : créer une vraie copie

```javascript
const original = [1, 2, 3];
const copie = [...original];  // ✅ Vraie copie

copie.push(4);

console.log(original);  // [1, 2, 3] ✅ Original intact
console.log(copie);     // [1, 2, 3, 4]
```

### Utiliser la valeur de retour incorrectement

```javascript
const nombres = [1, 2, 3];

// ❌ push() retourne la longueur, pas le tableau
const resultat = nombres.push(4);
console.log(resultat);  // 4 (longueur, pas le tableau)

// ✅ Le tableau est dans la variable originale
console.log(nombres);  // [1, 2, 3, 4]
```

### pop() ou shift() sur un tableau vide

```javascript
const vide = [];

const element = vide.pop();
console.log(element);  // undefined (pas d'erreur)

// Vérification avant d'utiliser
if (vide.length > 0) {
  const element = vide.pop();
  // Utiliser element en toute sécurité
}
```

---

## Alternatives modernes

### Avec le spread operator (immutable)

Si vous voulez éviter la mutation :

```javascript
const original = [1, 2, 3];

// Équivalent à push()
const avecNouveau = [...original, 4];

// Équivalent à unshift()
const avecNouveauDebut = [0, ...original];

// Équivalent à pop() (sans l'élément retiré)
const sansDernier = original.slice(0, -1);

// Équivalent à shift() (sans l'élément retiré)
const sansPremier = original.slice(1);
```

---

## Points clés à retenir

- ✅ **push()** : ajoute à la fin, retourne la nouvelle longueur
- ✅ **pop()** : retire de la fin, retourne l'élément retiré
- ✅ **unshift()** : ajoute au début, retourne la nouvelle longueur
- ✅ **shift()** : retire du début, retourne l'élément retiré
- ✅ Ces méthodes **modifient le tableau original** (mutation)
- ✅ push() et pop() sont **plus rapides** que shift() et unshift()
- ✅ Utilisables avec des tableaux déclarés en `const`
- ✅ Sur tableau vide : pop() et shift() retournent `undefined`

---

## Bonnes pratiques

- ✅ Utilisez `push()` et `pop()` pour les performances
- ✅ Vérifiez `length > 0` avant `pop()` ou `shift()` si nécessaire
- ✅ Si vous ne voulez pas modifier l'original, utilisez le spread operator
- ✅ Pour une pile (stack) : `push()` + `pop()`
- ✅ Pour une file (queue) : `push()` + `shift()`
- ✅ Documentez votre code si vous utilisez ces méthodes pour des structures de données spécifiques

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez `splice()` et `slice()`, des méthodes plus puissantes pour manipuler les tableaux à n'importe quelle position.

---


⏭️ [Méthodes de manipulation : splice, slice](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/07-splice-slice.md)
