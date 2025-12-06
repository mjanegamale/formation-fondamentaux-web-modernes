🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.11 - Autres méthodes : forEach, some, every

## Introduction

En plus de `map()`, `filter()` et `reduce()`, JavaScript propose d'autres méthodes très utiles pour travailler avec les tableaux :

| Méthode     | Action                                  | Retourne           |
|-------------|-----------------------------------------|--------------------|
| `forEach()` | Exécute une action pour chaque élément  | `undefined`        |
| `some()`    | Teste si **au moins un** élément passe  | `true` ou `false`  |
| `every()`   | Teste si **tous** les éléments passent  | `true` ou `false`  |

Ces méthodes sont complémentaires et couvrent des besoins différents.

---

## forEach() - Exécuter une action pour chaque élément

La méthode `forEach()` **exécute une fonction** pour chaque élément du tableau. Elle est utilisée pour les **effets de bord** (affichage, modification, etc.) plutôt que pour transformer le tableau.

### Syntaxe

```javascript
tableau.forEach((element, index, tableau) => {
  // Code à exécuter pour chaque élément
});
```

**Paramètres de la fonction de rappel** :
- `element` : L'élément en cours de traitement
- `index` : L'index de l'élément (optionnel)
- `tableau` : Le tableau complet (optionnel)

**Retour** : `undefined` (ne retourne rien)

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.forEach(fruit => {
  console.log(fruit);
});
// Affiche :
// pomme
// banane
// orange
```

### Avec l'index

```javascript
const couleurs = ["rouge", "vert", "bleu"];

couleurs.forEach((couleur, index) => {
  console.log(`${index + 1}. ${couleur}`);
});
// Affiche :
// 1. rouge
// 2. vert
// 3. bleu
```

### Effectuer des actions

```javascript
const nombres = [1, 2, 3, 4, 5];

// Afficher chaque nombre au carré
nombres.forEach(n => {
  const carre = n * n;
  console.log(`${n}² = ${carre}`);
});
// Affiche :
// 1² = 1
// 2² = 4
// 3² = 9
// ...
```

### Modifier des éléments externes

```javascript
const produits = [
  { nom: "Laptop", prix: 1000 },
  { nom: "Souris", prix: 25 },
  { nom: "Clavier", prix: 75 }
];

let total = 0;

produits.forEach(p => {
  total += p.prix;
  console.log(`Ajout de ${p.nom} : ${p.prix}€`);
});

console.log(`Total : ${total}€`);
// Total : 1100€
```

### Manipulation du DOM

```javascript
const taches = ["Faire courses", "Appeler médecin", "Lire emails"];

// Créer un élément li pour chaque tâche
taches.forEach(tache => {
  const li = document.createElement("li");
  li.textContent = tache;
  document.querySelector("ul").appendChild(li);
});
```

---

## forEach() vs map()

Ces deux méthodes se ressemblent mais ont des **usages différents** :

### Différences principales

| Critère           | forEach()                  | map()                        |
|-------------------|----------------------------|------------------------------|
| Retourne          | `undefined`                | Nouveau tableau              |
| Usage principal   | Effets de bord             | Transformation               |
| Créer tableau     | ❌ Non                      | ✅ Oui                       |
| Chaînable         | ❌ Non                      | ✅ Oui                       |

### Exemple comparatif

```javascript
const nombres = [1, 2, 3, 4, 5];

// forEach() - juste afficher
nombres.forEach(n => {
  console.log(n * 2);
});
// Affiche : 2, 4, 6, 8, 10
// Ne retourne rien

// map() - créer un nouveau tableau
const doubles = nombres.map(n => n * 2);
console.log(doubles);  // [2, 4, 6, 8, 10]
```

### Quand utiliser quoi ?

**Utilisez forEach() quand** :
- ✅ Vous voulez **afficher** des éléments
- ✅ Vous effectuez des **actions** (modification du DOM, appels API, etc.)
- ✅ Vous **ne voulez pas** créer de nouveau tableau
- ✅ Vous modifiez une variable externe

**Utilisez map() quand** :
- ✅ Vous voulez **transformer** et **créer un nouveau tableau**
- ✅ Vous voulez **chaîner** d'autres méthodes après
- ✅ Vous suivez une approche **fonctionnelle**

### Erreur courante : utiliser forEach() comme map()

```javascript
const nombres = [1, 2, 3];

// ❌ Ne fonctionne pas
const doubles = nombres.forEach(n => n * 2);
console.log(doubles);  // undefined

// ✅ Utilisez map()
const doubles = nombres.map(n => n * 2);
console.log(doubles);  // [2, 4, 6]
```

---

## Limitations de forEach()

### 1. Impossible d'arrêter la boucle

Contrairement à une boucle `for`, vous **ne pouvez pas** utiliser `break` ou `continue` avec `forEach()` :

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Ne fonctionne pas
nombres.forEach(n => {
  if (n === 3) break;  // SyntaxError!
  console.log(n);
});

// ✅ Utilisez une boucle for si besoin d'arrêter
for (const n of nombres) {
  if (n === 3) break;
  console.log(n);
}
// Affiche : 1, 2
```

### 2. Return n'arrête pas la boucle

Le `return` dans `forEach()` passe simplement à l'itération suivante :

```javascript
const nombres = [1, 2, 3, 4, 5];

nombres.forEach(n => {
  if (n === 3) return;  // Passe à l'élément suivant
  console.log(n);
});
// Affiche : 1, 2, 4, 5 (3 est sauté)
```

### 3. Pas de valeur de retour

`forEach()` retourne toujours `undefined`, vous ne pouvez pas l'utiliser pour construire une valeur :

```javascript
const nombres = [1, 2, 3];

const resultat = nombres.forEach(n => n * 2);
console.log(resultat);  // undefined
```

---

## some() - Au moins un élément satisfait la condition

La méthode `some()` teste si **au moins un élément** du tableau passe un test (fonction qui retourne `true` ou `false`).

### Syntaxe

```javascript
const resultat = tableau.some((element, index, tableau) => {
  // Retourner true ou false
  return condition;
});
```

**Retour** : `true` si au moins un élément satisfait la condition, `false` sinon

### Utilisation de base

```javascript
const nombres = [1, 2, 3, 4, 5];

// Y a-t-il au moins un nombre pair ?
const aDesPairs = nombres.some(n => n % 2 === 0);
console.log(aDesPairs);  // true (2 et 4 sont pairs)

// Y a-t-il au moins un nombre > 10 ?
const aGrandNombre = nombres.some(n => n > 10);
console.log(aGrandNombre);  // false
```

### Vérifier des conditions

```javascript
const ages = [15, 17, 20, 16];

// Y a-t-il au moins un majeur ?
const aUnMajeur = ages.some(age => age >= 18);
console.log(aUnMajeur);  // true (20 >= 18)
```

### Avec des objets

```javascript
const produits = [
  { nom: "Laptop", stock: 0 },
  { nom: "Souris", stock: 5 },
  { nom: "Clavier", stock: 0 }
];

// Y a-t-il au moins un produit en stock ?
const aProduitsDispo = produits.some(p => p.stock > 0);
console.log(aProduitsDispo);  // true (Souris a du stock)
```

### Court-circuit

`some()` **arrête dès** qu'un élément satisfait la condition :

```javascript
const nombres = [1, 2, 3, 4, 5];

const resultat = nombres.some(n => {
  console.log(`Test de ${n}`);
  return n > 2;
});
// Affiche :
// Test de 1
// Test de 2
// Test de 3
// (s'arrête car 3 > 2 est vrai)

console.log(resultat);  // true
```

---

## every() - Tous les éléments satisfont la condition

La méthode `every()` teste si **tous les éléments** du tableau passent un test (fonction qui retourne `true` ou `false`).

### Syntaxe

```javascript
const resultat = tableau.every((element, index, tableau) => {
  // Retourner true ou false
  return condition;
});
```

**Retour** : `true` si **tous** les éléments satisfont la condition, `false` sinon

### Utilisation de base

```javascript
const nombres = [2, 4, 6, 8, 10];

// Tous les nombres sont-ils pairs ?
const tousPairs = nombres.every(n => n % 2 === 0);
console.log(tousPairs);  // true

// Tous les nombres sont-ils > 5 ?
const tousGrands = nombres.every(n => n > 5);
console.log(tousGrands);  // false (2 et 4 ne sont pas > 5)
```

### Validation de données

```javascript
const utilisateurs = [
  { nom: "Alice", age: 25, email: "alice@example.com" },
  { nom: "Bob", age: 30, email: "bob@example.com" },
  { nom: "Charlie", age: 35, email: "charlie@example.com" }
];

// Tous les utilisateurs ont-ils un email ?
const tousOntEmail = utilisateurs.every(u => u.email && u.email.includes("@"));
console.log(tousOntEmail);  // true

// Tous les utilisateurs sont-ils majeurs ?
const tousMajeurs = utilisateurs.every(u => u.age >= 18);
console.log(tousMajeurs);  // true
```

### Vérifier un formulaire

```javascript
const champs = [
  { nom: "email", valeur: "test@example.com", valide: true },
  { nom: "password", valeur: "123456", valide: true },
  { nom: "nom", valeur: "Alice", valide: true }
];

// Tous les champs sont-ils valides ?
const formulaireValide = champs.every(c => c.valide);
console.log(formulaireValide);  // true
```

### Court-circuit

`every()` **arrête dès** qu'un élément ne satisfait pas la condition :

```javascript
const nombres = [2, 4, 5, 8, 10];

const resultat = nombres.every(n => {
  console.log(`Test de ${n}`);
  return n % 2 === 0;
});
// Affiche :
// Test de 2
// Test de 4
// Test de 5
// (s'arrête car 5 n'est pas pair)

console.log(resultat);  // false
```

---

## some() vs every()

### Différence logique

| Méthode  | Logique                        | Retourne true si...        |
|----------|--------------------------------|----------------------------|
| `some()` | **OU logique** (OR)            | Au moins un satisfait      |
| `every()`| **ET logique** (AND)           | Tous satisfont             |

### Exemple comparatif

```javascript
const notes = [15, 18, 12, 16, 8];

// some() - Au moins une note >= 10 ?
const auMoinsUneMoyenne = notes.some(n => n >= 10);
console.log(auMoinsUneMoyenne);  // true (15, 18, 12, 16 >= 10)

// every() - Toutes les notes >= 10 ?
const toutesLaNoyenne = notes.every(n => n >= 10);
console.log(toutesLaNoyenne);  // false (8 < 10)
```

### Tableau vide

Comportement particulier avec les tableaux vides :

```javascript
const vide = [];

console.log(vide.some(n => n > 0));   // false (aucun élément ne satisfait)
console.log(vide.every(n => n > 0));  // true (vacuité logique)
```

> 💡 **Note** : `every()` retourne `true` pour un tableau vide car il n'y a aucun élément qui contredit la condition (principe de vacuité en logique).

---

## Exemples pratiques complets

### Exemple 1 : Affichage de liste avec forEach()

```javascript
const etudiants = [
  { nom: "Alice", note: 15 },
  { nom: "Bob", note: 12 },
  { nom: "Charlie", note: 18 }
];

console.log("=== RÉSULTATS ===");
etudiants.forEach((e, index) => {
  const mention = e.note >= 16 ? "Très bien" :
                  e.note >= 14 ? "Bien" :
                  e.note >= 12 ? "Assez bien" : "Passable";

  console.log(`${index + 1}. ${e.nom} : ${e.note}/20 - ${mention}`);
});
// === RÉSULTATS ===
// 1. Alice : 15/20 - Bien
// 2. Bob : 12/20 - Assez bien
// 3. Charlie : 18/20 - Très bien
```

### Exemple 2 : Validation avec some()

```javascript
const commande = {
  articles: [
    { nom: "Laptop", stock: 5 },
    { nom: "Souris", stock: 0 },
    { nom: "Clavier", stock: 10 }
  ]
};

// Y a-t-il des articles en rupture ?
const aRupture = commande.articles.some(a => a.stock === 0);

if (aRupture) {
  console.log("⚠️ Attention : certains articles sont en rupture de stock");

  // Afficher lesquels
  commande.articles.forEach(a => {
    if (a.stock === 0) {
      console.log(`  - ${a.nom} (rupture)`);
    }
  });
}
```

### Exemple 3 : Vérification complète avec every()

```javascript
const utilisateur = {
  nom: "Alice",
  age: 25,
  email: "alice@example.com",
  cgv: true,
  newsletter: false
};

const champsObligatoires = [
  { cle: "nom", valeur: utilisateur.nom },
  { cle: "email", valeur: utilisateur.email },
  { cle: "cgv", valeur: utilisateur.cgv }
];

// Tous les champs obligatoires sont-ils remplis ?
const inscriptionValide = champsObligatoires.every(champ => {
  if (typeof champ.valeur === "boolean") {
    return champ.valeur === true;
  }
  return champ.valeur && champ.valeur.trim() !== "";
});

if (inscriptionValide) {
  console.log("✅ Inscription valide");
} else {
  console.log("❌ Veuillez remplir tous les champs obligatoires");
}
```

### Exemple 4 : Permissions utilisateur

```javascript
const utilisateur = {
  nom: "Alice",
  role: "admin",
  permissions: ["read", "write", "delete", "manage_users"]
};

// Vérifier si l'utilisateur peut effectuer une action
function peutEffectuer(action) {
  return utilisateur.permissions.some(p => p === action);
}

console.log(peutEffectuer("write"));   // true
console.log(peutEffectuer("execute")); // false

// Vérifier si l'utilisateur a toutes les permissions d'admin
const permissionsAdmin = ["read", "write", "delete"];
const estAdmin = permissionsAdmin.every(p =>
  utilisateur.permissions.includes(p)
);

console.log(`Est admin : ${estAdmin}`);  // true
```

### Exemple 5 : Vérification de stock

```javascript
const panier = [
  { article: "Laptop", quantite: 1, stock: 5 },
  { article: "Souris", quantite: 2, stock: 10 },
  { article: "Clavier", quantite: 1, stock: 3 }
];

// Tous les articles sont-ils disponibles en quantité suffisante ?
const tousDisponibles = panier.every(item => item.stock >= item.quantite);

if (tousDisponibles) {
  console.log("✅ Tous les articles sont disponibles");
  console.log("Vous pouvez procéder au paiement");
} else {
  console.log("❌ Certains articles ne sont pas disponibles en quantité suffisante");

  // Afficher les problèmes
  panier.forEach(item => {
    if (item.stock < item.quantite) {
      console.log(`  ⚠️ ${item.article} : demandé ${item.quantite}, disponible ${item.stock}`);
    }
  });
}
```

### Exemple 6 : Vérification d'âge pour un groupe

```javascript
const groupe = [
  { nom: "Alice", age: 25 },
  { nom: "Bob", age: 17 },
  { nom: "Charlie", age: 30 },
  { nom: "David", age: 22 }
];

// Y a-t-il des mineurs dans le groupe ?
const aDesMineurs = groupe.some(p => p.age < 18);

if (aDesMineurs) {
  console.log("⚠️ Le groupe contient des mineurs");
  console.log("Certaines activités seront restreintes");
} else {
  console.log("✅ Tous les participants sont majeurs");
}

// Tout le monde peut-il conduire une voiture de location ?
const tousConduire = groupe.every(p => p.age >= 21);

if (tousConduire) {
  console.log("✅ Tout le monde peut conduire");
} else {
  console.log("⚠️ Certains participants ne peuvent pas conduire (< 21 ans)");
}
```

---

## Comparaison avec filter()

### some() vs filter()

```javascript
const nombres = [1, 2, 3, 4, 5];

// some() - Y a-t-il au moins un pair ?
const aUnPair = nombres.some(n => n % 2 === 0);
console.log(aUnPair);  // true (juste un booléen)

// filter() - Quels sont les pairs ?
const pairs = nombres.filter(n => n % 2 === 0);
console.log(pairs);  // [2, 4] (les valeurs)
```

**Quand utiliser quoi ?**
- `some()` : Vous voulez juste savoir **SI** (question oui/non)
- `filter()` : Vous voulez savoir **LESQUELS** (obtenir les valeurs)

### every() vs filter()

```javascript
const notes = [15, 18, 12, 16, 14];

// every() - Tous >= 10 ?
const tousLaNoyenne = notes.every(n => n >= 10);
console.log(tousLaNoyenne);  // true (juste un booléen)

// filter() - Lesquels >= 10 ?
const notesCorrectes = notes.filter(n => n >= 10);
console.log(notesCorrectes);  // [15, 18, 12, 16, 14] (les valeurs)
```

---

## Performances et optimisations

### Court-circuit de some() et every()

Ces méthodes sont optimisées car elles s'**arrêtent dès que possible** :

```javascript
const grand = Array(1000000).fill(1);
grand[500000] = 2;

// some() trouve rapidement
console.time("some");
const resultat = grand.some(n => n === 2);
console.timeEnd("some");  // Très rapide (s'arrête à 500000)

// filter() doit tout parcourir
console.time("filter");
const resultats = grand.filter(n => n === 2);
console.timeEnd("filter");  // Plus lent (parcourt tout)
```

### forEach() vs boucle for

Pour des performances critiques, une boucle `for` classique peut être légèrement plus rapide :

```javascript
const grand = Array(1000000).fill(1);

// forEach() - élégant mais légèrement plus lent
console.time("forEach");
grand.forEach(n => n * 2);
console.timeEnd("forEach");

// for - plus rapide
console.time("for");
for (let i = 0; i < grand.length; i++) {
  grand[i] * 2;
}
console.timeEnd("for");
```

> 💡 **Conseil** : La différence est négligeable dans 99% des cas. Privilégiez la lisibilité !

---

## Erreurs courantes et pièges

### ❌ Essayer d'utiliser break dans forEach()

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Ne fonctionne pas
nombres.forEach(n => {
  if (n === 3) break;  // SyntaxError!
  console.log(n);
});

// ✅ Utilisez some() qui peut s'arrêter
nombres.some(n => {
  console.log(n);
  return n === 3;  // Arrête quand retourne true
});
```

### ❌ Confondre some() et every()

```javascript
const ages = [15, 25, 30];

// Question : "Y a-t-il des majeurs ?"
const bonneReponse = ages.some(age => age >= 18);   // true ✅
const mauvaiseReponse = ages.every(age => age >= 18);  // false ❌

// Question : "Sont-ils tous majeurs ?"
const bonneReponse = ages.every(age => age >= 18);  // false ✅
const mauvaiseReponse = ages.some(age => age >= 18);   // true ❌
```

### ❌ Oublier le return dans some()/every()

```javascript
const nombres = [1, 2, 3, 4, 5];

// ❌ Pas de return
const resultat = nombres.some(n => {
  n > 3;  // Cette ligne ne retourne rien !
});
console.log(resultat);  // false (toutes les conditions sont undefined = falsy)

// ✅ Avec return
const resultat = nombres.some(n => {
  return n > 3;
});
console.log(resultat);  // true

// ✅ Ou arrow function implicite
const resultat = nombres.some(n => n > 3);
console.log(resultat);  // true
```

### ❌ Utiliser forEach() pour créer un tableau

```javascript
// ❌ Compliqué et inefficace
const doubles = [];
[1, 2, 3].forEach(n => {
  doubles.push(n * 2);
});

// ✅ Utilisez map()
const doubles = [1, 2, 3].map(n => n * 2);
```

---

## Points clés à retenir

- ✅ **forEach()** : exécute une action pour chaque élément → retourne `undefined`
- ✅ **some()** : au moins un satisfait → retourne booléen
- ✅ **every()** : tous satisfont → retourne booléen
- ✅ forEach() est pour les **effets de bord**, pas pour transformer
- ✅ some() et every() utilisent le **court-circuit** (optimisé)
- ✅ some() = **OU logique**, every() = **ET logique**
- ✅ Pas de `break` dans forEach() (utilisez une boucle for si besoin)
- ✅ every() retourne `true` pour un **tableau vide**
- ✅ Ces méthodes ne modifient **pas le tableau original**

---

## Bonnes pratiques

- ✅ Utilisez **forEach()** pour afficher ou effectuer des actions
- ✅ Utilisez **some()** pour des questions "Y a-t-il au moins... ?"
- ✅ Utilisez **every()** pour des validations "Tous sont... ?"
- ✅ Préférez **map()** à forEach() si vous créez un tableau
- ✅ Utilisez **filter()** si vous voulez les valeurs, pas juste un booléen
- ✅ Nommez clairement vos variables de résultat (`aDesMineurs`, `tousMajeurs`)
- ✅ Combinez avec d'autres méthodes pour des vérifications complexes

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez les méthodes de tri et de réorganisation : `sort()` et `reverse()`.

---


⏭️ [Méthodes de tri et réorganisation : sort, reverse](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/12-sort-reverse.md)
