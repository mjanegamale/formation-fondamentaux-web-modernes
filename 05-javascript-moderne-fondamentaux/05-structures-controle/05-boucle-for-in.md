🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.5 - Boucle for...in (pour les objets)

## Introduction

La boucle `for...in` est spécialement conçue pour parcourir les **propriétés** (clés) d'un objet. Contrairement à `for...of` qui parcourt les valeurs d'un tableau, `for...in` parcourt les **noms des propriétés** d'un objet.

**En résumé :** `for...in` permet d'itérer sur les **clés** d'un objet, pas sur ses valeurs directement.

---

## Syntaxe de base

```javascript
for (const cle in objet) {
  // Code à exécuter pour chaque propriété
  console.log(cle);           // Nom de la propriété
  console.log(objet[cle]);    // Valeur de la propriété
}
```

### Les éléments clés

- **`const cle`** : Variable qui contient le nom de la propriété actuelle
- **`in`** : Mot-clé qui signifie "dans"
- **`objet`** : L'objet dont on veut parcourir les propriétés

---

## Premier exemple simple

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Paris"
};

for (const propriete in personne) {
  console.log(propriete);
}
```

**Résultat :**
```
nom
age
ville
```

**Explication :** La boucle parcourt les **noms des propriétés**, pas leurs valeurs.

---

## Accéder aux valeurs

Pour accéder à la valeur, utilisez la notation entre crochets `objet[cle]`.

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Paris"
};

for (const propriete in personne) {
  console.log(`${propriete} : ${personne[propriete]}`);
}
```

**Résultat :**
```
nom : Alice
age : 25
ville : Paris
```

**Important :** On utilise `personne[propriete]` (notation entre crochets), pas `personne.propriete`.

### Pourquoi la notation entre crochets ?

```javascript
const personne = { nom: "Alice", age: 25 };

for (const prop in personne) {
  // ❌ Incorrect : cherche littéralement une propriété nommée "prop"
  console.log(personne.prop);

  // ✅ Correct : utilise la valeur de la variable prop
  console.log(personne[prop]);
}
```

---

## `for...in` vs `for...of` : La différence cruciale ⚠️

C'est une source fréquente de confusion pour les débutants. Voyons la différence :

### `for...in` → Objets (les CLÉS)

```javascript
const personne = {
  nom: "Alice",
  age: 25
};

for (const cle in personne) {
  console.log(cle);
}
// Affiche : nom, age
```

### `for...of` → Tableaux (les VALEURS)

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
// Affiche : pomme, banane, orange
```

### Tableau récapitulatif

| Boucle | Pour | Donne accès à | Exemple |
|--------|------|---------------|---------|
| `for...in` | Objets | **Clés/Propriétés** | `"nom"`, `"age"` |
| `for...of` | Tableaux, Strings, etc. | **Valeurs** | `"pomme"`, `"banane"` |

**Règle simple :**
- **IN** → **I**nfo sur l'objet (clés) → **Objets**
- **OF** → **O**ne item at a time (valeurs) → **Tableaux**

---

## Exemples pratiques avec des objets

### Exemple 1 : Afficher les informations d'un utilisateur

```javascript
const utilisateur = {
  prenom: "Bob",
  nom: "Martin",
  email: "bob.martin@email.com",
  age: 30,
  ville: "Lyon"
};

console.log("Informations de l'utilisateur :");
for (const cle in utilisateur) {
  console.log(`- ${cle} : ${utilisateur[cle]}`);
}
```

**Résultat :**
```
Informations de l'utilisateur :
- prenom : Bob
- nom : Martin
- email : bob.martin@email.com
- age : 30
- ville : Lyon
```

### Exemple 2 : Compter les propriétés

```javascript
const produit = {
  nom: "Ordinateur portable",
  marque: "TechBrand",
  prix: 899,
  enStock: true
};

let nombreProprietes = 0;

for (const prop in produit) {
  nombreProprietes++;
}

console.log(`Le produit a ${nombreProprietes} propriétés`);
// Le produit a 4 propriétés
```

**Alternative moderne :** `Object.keys(produit).length`

### Exemple 3 : Vérifier si une propriété existe

```javascript
const voiture = {
  marque: "Renault",
  modele: "Clio",
  annee: 2020
};

const proprieteRecherchee = "couleur";
let trouve = false;

for (const prop in voiture) {
  if (prop === proprieteRecherchee) {
    trouve = true;
    break;
  }
}

if (trouve) {
  console.log(`✅ La propriété "${proprieteRecherchee}" existe`);
} else {
  console.log(`❌ La propriété "${proprieteRecherchee}" n'existe pas`);
}
```

**Alternative moderne :** `"couleur" in voiture` ou `voiture.hasOwnProperty("couleur")`

---

## Créer un nouvel objet basé sur un existant

### Exemple : Filtrer les propriétés

```javascript
const employe = {
  nom: "Dupont",
  prenom: "Marie",
  age: 28,
  salaire: 35000,
  departement: "IT"
};

// Créer un objet sans la propriété "salaire"
const employePublic = {};

for (const prop in employe) {
  if (prop !== "salaire") {
    employePublic[prop] = employe[prop];
  }
}

console.log(employePublic);
// { nom: "Dupont", prenom: "Marie", age: 28, departement: "IT" }
```

### Exemple : Transformer les valeurs

```javascript
const prix = {
  ordinateur: 899,
  souris: 25,
  clavier: 75
};

const prixAvecTVA = {};

for (const produit in prix) {
  prixAvecTVA[produit] = prix[produit] * 1.20; // +20% de TVA
}

console.log(prixAvecTVA);
// { ordinateur: 1078.8, souris: 30, clavier: 90 }
```

---

## Parcourir plusieurs objets

### Exemple : Comparer deux objets

```javascript
const config1 = {
  theme: "dark",
  langue: "fr",
  notifications: true
};

const config2 = {
  theme: "light",
  langue: "fr",
  notifications: false
};

console.log("Différences :");
for (const cle in config1) {
  if (config1[cle] !== config2[cle]) {
    console.log(`${cle} : ${config1[cle]} → ${config2[cle]}`);
  }
}
```

**Résultat :**
```
Différences :
theme : dark → light
notifications : true → false
```

---

## ⚠️ Attention avec les tableaux !

Techniquement, `for...in` fonctionne avec les tableaux, mais **il ne faut pas l'utiliser** pour parcourir des tableaux.

### ❌ Pourquoi c'est une mauvaise idée

```javascript
const fruits = ["pomme", "banane", "orange"];

// ❌ Ne faites PAS ceci
for (const index in fruits) {
  console.log(typeof index); // "string" (pas "number" !)
  console.log(index);        // Affiche "0", "1", "2" (en string)
  console.log(fruits[index]); // Fonctionne mais pas recommandé
}
```

**Problèmes :**
1. Les indices sont des **strings**, pas des nombres
2. `for...in` peut parcourir des propriétés ajoutées au prototype
3. L'ordre n'est pas garanti (même si en pratique il l'est souvent)

### ✅ Solution : Utilisez `for...of` pour les tableaux

```javascript
const fruits = ["pomme", "banane", "orange"];

// ✅ Correct pour les tableaux
for (const fruit of fruits) {
  console.log(fruit);
}
```

---

## Propriétés héritées et `hasOwnProperty()`

Par défaut, `for...in` parcourt aussi les propriétés héritées du prototype (concept avancé). Pour ne parcourir que les propriétés propres à l'objet, utilisez `hasOwnProperty()`.

### Sans vérification

```javascript
const animal = {
  type: "mammifère",
  respire: true
};

for (const prop in animal) {
  console.log(prop);
}
// Affiche : type, respire (+ éventuellement des propriétés héritées)
```

### Avec `hasOwnProperty()`

```javascript
const animal = {
  type: "mammifère",
  respire: true
};

for (const prop in animal) {
  if (animal.hasOwnProperty(prop)) {
    console.log(`${prop} : ${animal[prop]}`);
  }
}
```

**Note :** Pour les objets simples créés avec `{}`, cette vérification n'est généralement pas nécessaire, mais c'est une bonne pratique pour du code robuste.

---

## Méthodes modernes alternatives

JavaScript moderne offre des alternatives souvent plus claires que `for...in`.

### `Object.keys()` : Obtenir un tableau des clés

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Paris"
};

const cles = Object.keys(personne);
console.log(cles); // ["nom", "age", "ville"]

// Puis utiliser for...of ou forEach
for (const cle of cles) {
  console.log(`${cle} : ${personne[cle]}`);
}
```

### `Object.values()` : Obtenir un tableau des valeurs

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Paris"
};

const valeurs = Object.values(personne);
console.log(valeurs); // ["Alice", 25, "Paris"]

for (const valeur of valeurs) {
  console.log(valeur);
}
```

### `Object.entries()` : Obtenir un tableau de paires [clé, valeur]

```javascript
const personne = {
  nom: "Alice",
  age: 25,
  ville: "Paris"
};

const entrees = Object.entries(personne);
console.log(entrees);
// [["nom", "Alice"], ["age", 25], ["ville", "Paris"]]

for (const [cle, valeur] of entrees) {
  console.log(`${cle} : ${valeur}`);
}
```

**Avantage :** Plus moderne et plus clair !

---

## Exemples pratiques avancés

### Exemple 1 : Convertir un objet en chaîne de requête URL

```javascript
const parametres = {
  page: 1,
  limite: 10,
  tri: "date",
  ordre: "desc"
};

let queryString = "?";

for (const param in parametres) {
  queryString += `${param}=${parametres[param]}&`;
}

// Retirer le dernier "&"
queryString = queryString.slice(0, -1);

console.log(queryString);
// ?page=1&limite=10&tri=date&ordre=desc
```

**Alternative moderne :** `new URLSearchParams(parametres).toString()`

### Exemple 2 : Créer un résumé d'inventaire

```javascript
const inventaire = {
  pommes: 50,
  bananes: 30,
  oranges: 40,
  fraises: 20
};

let total = 0;
let details = "Inventaire :\n";

for (const fruit in inventaire) {
  const quantite = inventaire[fruit];
  details += `- ${fruit} : ${quantite}\n`;
  total += quantite;
}

details += `\nTotal : ${total} fruits`;
console.log(details);
```

**Résultat :**
```
Inventaire :
- pommes : 50
- bananes : 30
- oranges : 40
- fraises : 20

Total : 140 fruits
```

### Exemple 3 : Valider un formulaire

```javascript
const formulaire = {
  nom: "Dupont",
  email: "dupont@email.com",
  age: "",
  telephone: ""
};

const champsObligatoires = ["nom", "email", "age"];
const erreurs = [];

for (const champ of champsObligatoires) {
  if (formulaire[champ] === "") {
    erreurs.push(`Le champ "${champ}" est obligatoire`);
  }
}

if (erreurs.length > 0) {
  console.log("❌ Erreurs de validation :");
  for (const erreur of erreurs) {
    console.log(`- ${erreur}`);
  }
} else {
  console.log("✅ Formulaire valide");
}
```

### Exemple 4 : Fusionner deux objets (approche simple)

```javascript
const defaut = {
  theme: "light",
  langue: "en",
  notifications: true,
  volume: 50
};

const personnalise = {
  theme: "dark",
  volume: 80
};

// Fusionner personnalise dans defaut
const config = {};

// D'abord copier les valeurs par défaut
for (const cle in defaut) {
  config[cle] = defaut[cle];
}

// Puis écraser avec les valeurs personnalisées
for (const cle in personnalise) {
  config[cle] = personnalise[cle];
}

console.log(config);
// { theme: "dark", langue: "en", notifications: true, volume: 80 }
```

**Alternative moderne :** `const config = { ...defaut, ...personnalise };`

### Exemple 5 : Recherche case-insensitive dans un objet

```javascript
const traductions = {
  Bonjour: "Hello",
  Merci: "Thank you",
  AuRevoir: "Goodbye"
};

function trouverTraduction(mot) {
  const motLower = mot.toLowerCase();

  for (const cle in traductions) {
    if (cle.toLowerCase() === motLower) {
      return traductions[cle];
    }
  }

  return "Traduction non trouvée";
}

console.log(trouverTraduction("bonjour"));  // "Hello"
console.log(trouverTraduction("MERCI"));    // "Thank you"
console.log(trouverTraduction("Salut"));    // "Traduction non trouvée"
```

---

## Objets imbriqués

Vous pouvez utiliser `for...in` pour parcourir des objets imbriqués.

### Exemple simple

```javascript
const entreprise = {
  nom: "TechCorp",
  employes: {
    developpeurs: 10,
    designers: 5,
    managers: 3
  },
  adresse: {
    rue: "123 rue Tech",
    ville: "Paris",
    codePostal: "75001"
  }
};

console.log("Informations de l'entreprise :");
for (const cle in entreprise) {
  const valeur = entreprise[cle];

  if (typeof valeur === "object" && valeur !== null) {
    console.log(`${cle} :`);
    for (const sousCle in valeur) {
      console.log(`  - ${sousCle} : ${valeur[sousCle]}`);
    }
  } else {
    console.log(`${cle} : ${valeur}`);
  }
}
```

**Résultat :**
```
Informations de l'entreprise :
nom : TechCorp
employes :
  - developpeurs : 10
  - designers : 5
  - managers : 3
adresse :
  - rue : 123 rue Tech
  - ville : Paris
  - codePostal : 75001
```

---

## Modifier un objet pendant le parcours

### ⚠️ Attention aux modifications

Modifier un objet pendant qu'on le parcourt peut causer des comportements inattendus.

```javascript
const scores = {
  alice: 100,
  bob: 50,
  charlie: 75
};

// ❌ Risqué : ajouter des propriétés pendant le parcours
for (const joueur in scores) {
  if (scores[joueur] >= 75) {
    scores[joueur + "_bonus"] = scores[joueur] + 10; // Peut causer des problèmes
  }
}
```

### ✅ Solution : Créer un nouvel objet

```javascript
const scores = {
  alice: 100,
  bob: 50,
  charlie: 75
};

const nouveauxScores = {};

for (const joueur in scores) {
  nouveauxScores[joueur] = scores[joueur];

  if (scores[joueur] >= 75) {
    nouveauxScores[joueur + "_bonus"] = scores[joueur] + 10;
  }
}

console.log(nouveauxScores);
// { alice: 100, alice_bonus: 110, bob: 50, charlie: 75, charlie_bonus: 85 }
```

---

## Performances et bonnes pratiques

### ✅ Utilisez `const` pour la variable de boucle

```javascript
// ✅ Recommandé
for (const cle in objet) {
  console.log(cle);
}

// Moins courant (seulement si vous modifiez la variable)
for (let cle in objet) {
  cle = cle.toUpperCase();
  console.log(cle);
}
```

### ✅ Préférez les méthodes modernes quand c'est possible

```javascript
const personne = { nom: "Alice", age: 25 };

// ✅ Plus moderne et clair
Object.entries(personne).forEach(([cle, valeur]) => {
  console.log(`${cle} : ${valeur}`);
});

// vs

// Classique mais verbeux
for (const cle in personne) {
  console.log(`${cle} : ${personne[cle]}`);
}
```

### ✅ Utilisez des noms de variables explicites

```javascript
// ❌ Peu clair
for (const k in obj) {
  console.log(obj[k]);
}

// ✅ Plus clair
for (const propriete in utilisateur) {
  console.log(utilisateur[propriete]);
}
```

---

## Cas d'usage : Quand utiliser `for...in` ?

### ✅ Utilisez `for...in` quand :

- Vous devez parcourir les **propriétés d'un objet**
- Vous ne connaissez pas les noms des propriétés à l'avance
- Vous avez besoin d'un traitement pour chaque propriété
- Vous travaillez avec du code legacy qui l'utilise

### ❌ N'utilisez PAS `for...in` quand :

- Vous parcourez un **tableau** (utilisez `for...of` ou `forEach`)
- Vous pouvez utiliser une méthode moderne plus claire (`Object.keys()`, `Object.entries()`)
- L'ordre est important (l'ordre n'est pas garanti, même si souvent respecté)

---

## Résumé

### Points clés à retenir

- **`for...in`** parcourt les **clés/propriétés** d'un objet, pas les valeurs
- Utilisez `objet[cle]` pour accéder aux valeurs (notation entre crochets)
- Ne confondez pas avec **`for...of`** qui est pour les tableaux (valeurs)
- **Évitez** `for...in` avec les tableaux (utilisez `for...of`)
- Utilisez `hasOwnProperty()` pour éviter les propriétés héritées (cas avancés)
- Les méthodes modernes (`Object.keys()`, `Object.values()`, `Object.entries()`) sont souvent plus claires

### Aide-mémoire

```javascript
// Pour les OBJETS : for...in (les CLÉS)
const objet = { nom: "Alice", age: 25 };
for (const cle in objet) {
  console.log(cle, objet[cle]);
}

// Pour les TABLEAUX : for...of (les VALEURS)
const tableau = ["a", "b", "c"];
for (const valeur of tableau) {
  console.log(valeur);
}

// Moderne : Object.entries() + for...of
for (const [cle, valeur] of Object.entries(objet)) {
  console.log(cle, valeur);
}
```

La boucle `for...in` est un outil essentiel pour travailler avec les objets JavaScript. Bien comprendre quand l'utiliser (et quand ne pas l'utiliser !) vous évitera de nombreuses erreurs ! 🎯

⏭️ [Boucle while et do-while](/05-javascript-moderne-fondamentaux/05-structures-controle/06-while-do-while.md)
