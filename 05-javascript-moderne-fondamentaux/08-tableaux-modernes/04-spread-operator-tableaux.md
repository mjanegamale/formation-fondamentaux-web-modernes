🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.4 - Spread operator pour les tableaux 🆕

## Qu'est-ce que le spread operator ?

Le **spread operator** (opérateur de décomposition) est représenté par **trois points** : `...`

Il permet de "décomposer" un tableau en ses éléments individuels. C'est une fonctionnalité moderne introduite avec **ES6**.

### Visualisation du concept

Imaginez un tableau comme une boîte contenant des éléments :

```javascript
const fruits = ["pomme", "banane", "orange"];
```

Le spread operator "ouvre" la boîte et expose les éléments :

```javascript
...fruits  // équivaut à : "pomme", "banane", "orange"
```

---

## Syntaxe de base

Le spread operator s'écrit avec **trois points** devant un tableau :

```javascript
...nomDuTableau
```

Il ne peut pas être utilisé seul, mais doit être dans un contexte approprié (nouveau tableau, appel de fonction, etc.).

---

## Copier un tableau

### Le problème : copie par référence

En JavaScript, si vous assignez un tableau à une autre variable, vous créez une **référence**, pas une copie :

```javascript
const original = [1, 2, 3];
const copie = original;

copie[0] = 999;

console.log(original);  // [999, 2, 3] ⚠️ Original modifié !
console.log(copie);     // [999, 2, 3]
```

Les deux variables pointent vers le **même tableau en mémoire**.

### La solution : spread operator

Le spread operator crée une **vraie copie** :

```javascript
const original = [1, 2, 3];
const copie = [...original];

copie[0] = 999;

console.log(original);  // [1, 2, 3] ✅ Original intact
console.log(copie);     // [999, 2, 3]
```

### Comparaison visuelle

```javascript
const fruits = ["pomme", "banane", "orange"];

// ❌ Pas une vraie copie (référence)
const ref = fruits;

// ✅ Vraie copie avec spread
const copie = [...fruits];
```

---

## Fusionner des tableaux

Le spread operator permet de combiner plusieurs tableaux facilement.

### Fusionner deux tableaux

```javascript
const fruits = ["pomme", "banane"];
const legumes = ["carotte", "salade"];

const nourriture = [...fruits, ...legumes];

console.log(nourriture);
// ["pomme", "banane", "carotte", "salade"]
```

### Fusionner trois tableaux ou plus

```javascript
const matin = ["café", "croissant"];
const midi = ["salade", "pâtes"];
const soir = ["soupe", "pain"];

const repas = [...matin, ...midi, ...soir];

console.log(repas);
// ["café", "croissant", "salade", "pâtes", "soupe", "pain"]
```

### Comparaison avec concat()

**Méthode classique avec concat()** :

```javascript
const tab1 = [1, 2];
const tab2 = [3, 4];

const fusion = tab1.concat(tab2);
```

**Méthode moderne avec spread** :

```javascript
const tab1 = [1, 2];
const tab2 = [3, 4];

const fusion = [...tab1, ...tab2];
```

Les deux méthodes fonctionnent, mais le spread est souvent préféré pour sa lisibilité. 💡

---

## Ajouter des éléments

Le spread operator permet d'ajouter des éléments tout en copiant un tableau.

### Ajouter au début

```javascript
const nombres = [2, 3, 4];
const nouveau = [1, ...nombres];

console.log(nouveau);  // [1, 2, 3, 4]
```

### Ajouter à la fin

```javascript
const nombres = [1, 2, 3];
const nouveau = [...nombres, 4, 5];

console.log(nouveau);  // [1, 2, 3, 4, 5]
```

### Ajouter au milieu

```javascript
const nombres = [1, 2, 5];
const nouveau = [...nombres.slice(0, 2), 3, 4, ...nombres.slice(2)];

console.log(nouveau);  // [1, 2, 3, 4, 5]
```

### Ajouter plusieurs éléments à différents endroits

```javascript
const base = [3, 4];
const complet = [1, 2, ...base, 5, 6];

console.log(complet);  // [1, 2, 3, 4, 5, 6]
```

---

## Insérer un tableau dans un autre

Vous pouvez insérer un tableau au milieu d'un autre :

```javascript
const debut = ["a", "b"];
const milieu = ["c", "d", "e"];
const fin = ["f", "g"];

const resultat = [...debut, ...milieu, ...fin];

console.log(resultat);
// ["a", "b", "c", "d", "e", "f", "g"]
```

### Exemple pratique : menu de restaurant

```javascript
const entrees = ["Salade", "Soupe"];
const plats = ["Poulet", "Poisson", "Végétarien"];
const desserts = ["Tarte", "Glace"];

const menuComplet = [
  "=== ENTRÉES ===",
  ...entrees,
  "=== PLATS ===",
  ...plats,
  "=== DESSERTS ===",
  ...desserts
];

console.log(menuComplet);
```

---

## Utiliser avec des fonctions

Le spread operator peut "décomposer" un tableau en arguments individuels pour une fonction.

### Math.max() et Math.min()

Ces fonctions prennent des arguments séparés, pas un tableau :

```javascript
// ❌ Ne fonctionne pas
const nombres = [5, 12, 8, 3, 20];
console.log(Math.max(nombres));  // NaN

// ✅ Solution avec spread
console.log(Math.max(...nombres));  // 20
console.log(Math.min(...nombres));  // 3
```

Le spread "décompose" `[5, 12, 8, 3, 20]` en `5, 12, 8, 3, 20`.

### Fonction personnalisée

```javascript
function addition(a, b, c) {
  return a + b + c;
}

const nombres = [10, 20, 30];

// ❌ Ne fonctionne pas (passe le tableau entier)
console.log(addition(nombres));  // NaN

// ✅ Avec spread
console.log(addition(...nombres));  // 60
```

### console.log() avec plusieurs valeurs

```javascript
const infos = ["Alice", 25, "Paris"];

// Au lieu de :
console.log(infos[0], infos[1], infos[2]);

// Plus simple avec spread :
console.log(...infos);  // Alice 25 Paris
```

---

## Convertir d'autres structures en tableaux

Le spread fonctionne avec tout ce qui est "itérable".

### Convertir une chaîne en tableau de caractères

```javascript
const mot = "Hello";
const lettres = [...mot];

console.log(lettres);  // ["H", "e", "l", "l", "o"]
```

### Exemple : compter les voyelles

```javascript
const texte = "Bonjour";
const caracteres = [...texte.toLowerCase()];
const voyelles = ["a", "e", "i", "o", "u", "y"];

const nbVoyelles = caracteres.filter(c => voyelles.includes(c)).length;
console.log(nbVoyelles);  // 3 (o, o, u)
```

### Copier un Set en tableau

```javascript
const ensemble = new Set([1, 2, 3, 3, 4]);  // Set supprime les doublons
const tableau = [...ensemble];

console.log(tableau);  // [1, 2, 3, 4]
```

---

## Supprimer les doublons d'un tableau

Combinaison puissante : `Set` + spread operator

```javascript
const nombres = [1, 2, 2, 3, 4, 4, 5];

const sansDoublons = [...new Set(nombres)];

console.log(sansDoublons);  // [1, 2, 3, 4, 5]
```

**Comment ça marche ?**
1. `new Set(nombres)` crée un Set (collection sans doublons)
2. `...` décompose le Set en éléments individuels
3. `[...]` crée un nouveau tableau avec ces éléments

---

## Copie superficielle vs profonde

⚠️ **Important** : Le spread operator crée une **copie superficielle** (shallow copy).

### Avec des tableaux simples (OK)

```javascript
const original = [1, 2, 3];
const copie = [...original];

copie[0] = 999;
console.log(original);  // [1, 2, 3] ✅ Original intact
```

### Avec des tableaux imbriqués (problème)

```javascript
const original = [1, [2, 3], 4];
const copie = [...original];

copie[1][0] = 999;

console.log(original);  // [1, [999, 3], 4] ⚠️ Original modifié !
console.log(copie);     // [1, [999, 3], 4]
```

Le tableau interne `[2, 3]` n'est pas copié, seulement sa référence.

### Solution pour copie profonde

Pour les tableaux simples imbriqués :

```javascript
const original = [1, [2, 3], 4];
const copie = [...original].map(item =>
  Array.isArray(item) ? [...item] : item
);

copie[1][0] = 999;
console.log(original);  // [1, [2, 3], 4] ✅ Original intact
```

Pour des structures complexes, utilisez `structuredClone()` (moderne) :

```javascript
const original = [1, [2, [3, 4]], 5];
const copie = structuredClone(original);

copie[1][1][0] = 999;
console.log(original);  // [1, [2, [3, 4]], 5] ✅ Original intact
```

---

## Exemples pratiques complets

### Exemple 1 : Gestion d'un panier d'achat

```javascript
const panier = ["pommes", "pain"];

// Ajouter un article
const nouveauPanier = [...panier, "lait"];
console.log(nouveauPanier);  // ["pommes", "pain", "lait"]

// Fusionner avec une liste de courses
const courses = ["beurre", "œufs"];
const total = [...nouveauPanier, ...courses];
console.log(total);
// ["pommes", "pain", "lait", "beurre", "œufs"]
```

### Exemple 2 : Historique d'actions (undo/redo)

```javascript
const historique = ["action1", "action2"];

// Ajouter une nouvelle action
const nouvelHistorique = [...historique, "action3"];

// Annuler (retirer la dernière action)
const apresAnnulation = nouvelHistorique.slice(0, -1);

console.log(apresAnnulation);  // ["action1", "action2"]
```

### Exemple 3 : Fusion de résultats de recherche

```javascript
const resultatsGoogle = ["résultat1", "résultat2"];
const resultatsBing = ["résultat3", "résultat4"];
const resultatsYahoo = ["résultat5"];

const tousResultats = [
  ...resultatsGoogle,
  ...resultatsBing,
  ...resultatsYahoo
];

console.log(tousResultats);
// ["résultat1", "résultat2", "résultat3", "résultat4", "résultat5"]
```

### Exemple 4 : Rotation de tableau (déplacer premier élément à la fin)

```javascript
const file = ["Alice", "Bob", "Charlie", "David"];

// Retirer le premier et l'ajouter à la fin
const [premier, ...reste] = file;
const nouvelleFile = [...reste, premier];

console.log(nouvelleFile);
// ["Bob", "Charlie", "David", "Alice"]
```

### Exemple 5 : Trouver max/min avec contexte

```javascript
const notes = [15, 18, 12, 16, 14];

const meilleure = Math.max(...notes);
const pire = Math.min(...notes);
const moyenne = notes.reduce((a, b) => a + b) / notes.length;

console.log(`Meilleure: ${meilleure}, Pire: ${pire}, Moyenne: ${moyenne}`);
// "Meilleure: 18, Pire: 12, Moyenne: 15"
```

---

## Combinaison avec d'autres fonctionnalités

### Spread + Destructuring

```javascript
const nombres = [1, 2, 3, 4, 5];

const [premier, deuxieme, ...reste] = nombres;

console.log(premier);   // 1
console.log(deuxieme);  // 2
console.log(reste);     // [3, 4, 5]

// Créer un nouveau tableau sans le premier élément
const sansPremier = [...reste];
console.log(sansPremier);  // [3, 4, 5]
```

### Spread + filter() + map()

```javascript
const nombres = [1, 2, 3, 4, 5, 6];

// Doubler tous les nombres pairs
const pairs = nombres.filter(n => n % 2 === 0);
const doubles = [...pairs].map(n => n * 2);

console.log(doubles);  // [4, 8, 12]
```

---

## Erreurs courantes à éviter

### ❌ Utiliser spread seul

```javascript
const nombres = [1, 2, 3];
...nombres;  // ❌ Erreur de syntaxe
```

Le spread doit toujours être dans un contexte (tableau, fonction, objet).

### ❌ Oublier les crochets pour créer un tableau

```javascript
const tab1 = [1, 2];
const tab2 = [3, 4];

const fusion = ...tab1, ...tab2;  // ❌ Erreur
const fusion = [...tab1, ...tab2];  // ✅ Correct
```

### ❌ Confondre spread et rest

```javascript
// Rest : dans le destructuring (collecte)
const [premier, ...reste] = [1, 2, 3];

// Spread : dans un tableau/fonction (décompose)
const nouveau = [...reste, 4];
```

Même syntaxe (`...`) mais utilisations différentes !

---

## Performances

Le spread operator est très performant pour des tableaux de taille petite à moyenne (< 10,000 éléments).

Pour des tableaux très grands, les méthodes natives comme `concat()` peuvent être légèrement plus rapides, mais la différence est négligeable dans la plupart des cas.

> 💡 **Conseil** : Privilégiez la lisibilité avec le spread operator. L'optimisation prématurée n'est pas nécessaire.

---

## Points clés à retenir

- ✅ Syntaxe : `...tableau` pour "décomposer" un tableau
- ✅ Crée des **vraies copies** de tableaux (superficielles)
- ✅ Permet de **fusionner** des tableaux facilement
- ✅ Permet d'**ajouter** des éléments en créant un nouveau tableau
- ✅ Utile pour passer un tableau comme **arguments de fonction**
- ✅ Peut convertir des **chaînes** et **Sets** en tableaux
- ✅ Attention : copie **superficielle** uniquement (shallow copy)
- ✅ Ne pas confondre avec **rest operator** (même syntaxe, usage différent)

---

## Quand utiliser le spread operator ?

- ✅ **Copier** un tableau sans affecter l'original
- ✅ **Fusionner** plusieurs tableaux
- ✅ **Ajouter** des éléments à un tableau existant
- ✅ **Passer** un tableau comme arguments de fonction
- ✅ **Supprimer les doublons** (avec Set)
- ✅ Préférer **spread** à `concat()` pour la lisibilité

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez la propriété `length` et comment l'utiliser pour manipuler la taille des tableaux.

---


⏭️ [Propriété length](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/05-propriete-length.md)
