🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.7 - Instructions break et continue

## Introduction

Les instructions `break` et `continue` sont des outils de **contrôle de flux** qui permettent de modifier le comportement normal d'une boucle. Elles sont utilisées pour optimiser le code et éviter d'exécuter des instructions inutiles.

**En résumé :**
- **`break`** : Sort complètement de la boucle
- **`continue`** : Passe directement à l'itération suivante

**Analogie :** Imaginez que vous cherchez vos clés dans différentes pièces de votre maison :
- **`break`** : Vous trouvez vos clés → Vous arrêtez immédiatement de chercher
- **`continue`** : Une pièce est fermée → Vous passez directement à la suivante sans perdre de temps

---

## L'instruction `break`

### Qu'est-ce que `break` ?

L'instruction `break` permet de **sortir immédiatement** d'une boucle, quel que soit l'état de la condition. Quand JavaScript rencontre `break`, il arrête la boucle et continue l'exécution du code après la boucle.

### Syntaxe

```javascript
for (let i = 0; i < 10; i++) {
  if (condition) {
    break; // Sort de la boucle
  }
  // Code normal
}
// Le code continue ici après le break
```

---

## `break` avec différentes boucles

### Avec la boucle `for`

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    console.log("On arrête à 5 !");
    break;
  }
  console.log(i);
}
console.log("Boucle terminée");
```

**Résultat :**
```
0
1
2
3
4
On arrête à 5 !
Boucle terminée
```

**Explication :** Quand `i` atteint 5, le `break` est exécuté et on sort immédiatement de la boucle.

### Avec la boucle `while`

```javascript
let compteur = 0;

while (compteur < 100) {
  console.log(compteur);
  compteur++;

  if (compteur === 5) {
    console.log("Interruption à 5");
    break;
  }
}
console.log("Boucle terminée");
```

**Résultat :**
```
0
1
2
3
4
Interruption à 5
Boucle terminée
```

### Avec la boucle `for...of`

```javascript
const fruits = ["pomme", "banane", "orange", "fraise", "kiwi"];

for (const fruit of fruits) {
  if (fruit === "orange") {
    console.log(`Trouvé ${fruit}, on arrête !`);
    break;
  }
  console.log(fruit);
}
```

**Résultat :**
```
pomme
banane
Trouvé orange, on arrête !
```

### Avec la boucle `do-while`

```javascript
let i = 0;

do {
  console.log(i);
  i++;

  if (i === 3) {
    break;
  }
} while (i < 10);

console.log("Fin");
```

**Résultat :**
```
0
1
2
Fin
```

---

## Cas d'usage de `break`

### Exemple 1 : Rechercher un élément dans un tableau

```javascript
const etudiants = ["Alice", "Bob", "Charlie", "Diana", "Eve"];
const nomRecherche = "Charlie";
let trouve = false;

for (let i = 0; i < etudiants.length; i++) {
  if (etudiants[i] === nomRecherche) {
    console.log(`✅ ${nomRecherche} trouvé à l'index ${i}`);
    trouve = true;
    break; // Plus besoin de continuer
  }
}

if (!trouve) {
  console.log(`❌ ${nomRecherche} non trouvé`);
}
```

**Avantage :** On évite de parcourir inutilement le reste du tableau une fois l'élément trouvé.

### Exemple 2 : Valider un formulaire

```javascript
const formulaire = {
  nom: "Dupont",
  email: "dupont@email.com",
  age: "",
  telephone: "0612345678"
};

const champs = Object.keys(formulaire);
let valide = true;

for (const champ of champs) {
  if (formulaire[champ] === "") {
    console.log(`❌ Le champ "${champ}" est vide`);
    valide = false;
    break; // Inutile de vérifier les autres champs
  }
}

if (valide) {
  console.log("✅ Formulaire valide");
}
```

### Exemple 3 : Limite de tentatives

```javascript
const motDePasseCorrect = "secret123";
const tentativesMax = 3;

const tentatives = ["abc", "def", "secret123"];

for (let i = 0; i < tentativesMax; i++) {
  const saisie = tentatives[i];
  console.log(`Tentative ${i + 1} : ${saisie}`);

  if (saisie === motDePasseCorrect) {
    console.log("✅ Accès autorisé !");
    break;
  }

  if (i === tentativesMax - 1) {
    console.log("❌ Compte bloqué après 3 tentatives");
  }
}
```

### Exemple 4 : Trouver le premier nombre supérieur à un seuil

```javascript
const nombres = [5, 12, 8, 45, 23, 67, 34];
const seuil = 40;

for (const nombre of nombres) {
  if (nombre > seuil) {
    console.log(`Premier nombre > ${seuil} : ${nombre}`);
    break;
  }
}
```

---

## L'instruction `continue`

### Qu'est-ce que `continue` ?

L'instruction `continue` permet de **sauter l'itération actuelle** et de passer directement à la suivante. Le code après `continue` dans la boucle n'est pas exécuté pour cette itération, mais la boucle continue normalement.

### Syntaxe

```javascript
for (let i = 0; i < 10; i++) {
  if (condition) {
    continue; // Passe à l'itération suivante
  }
  // Ce code est sauté si continue est exécuté
}
```

---

## `continue` avec différentes boucles

### Avec la boucle `for`

```javascript
for (let i = 0; i < 10; i++) {
  if (i % 2 !== 0) {
    continue; // Saute les nombres impairs
  }
  console.log(i);
}
```

**Résultat :**
```
0
2
4
6
8
```

**Explication :** Quand `i` est impair, `continue` est exécuté et le `console.log` est sauté. La boucle passe directement à `i++`.

### Avec la boucle `while`

```javascript
let compteur = 0;

while (compteur < 10) {
  compteur++;

  if (compteur % 2 !== 0) {
    continue; // Saute les nombres impairs
  }

  console.log(compteur);
}
```

**Résultat :**
```
2
4
6
8
10
```

**⚠️ Important :** Notez que `compteur++` est **avant** le `continue`. Si c'était après, on aurait une boucle infinie !

### Avec la boucle `for...of`

```javascript
const mots = ["bonjour", "le", "monde", "est", "beau"];

for (const mot of mots) {
  if (mot.length <= 2) {
    continue; // Ignore les mots de 2 lettres ou moins
  }
  console.log(mot);
}
```

**Résultat :**
```
bonjour
monde
beau
```

---

## Cas d'usage de `continue`

### Exemple 1 : Filtrer des éléments

```javascript
const nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

console.log("Nombres pairs :");
for (const nombre of nombres) {
  if (nombre % 2 !== 0) {
    continue; // Ignore les impairs
  }
  console.log(nombre);
}
```

### Exemple 2 : Ignorer des valeurs invalides

```javascript
const temperatures = [18, -999, 22, 25, -999, 30, 19];
let somme = 0;
let compteur = 0;

for (const temp of temperatures) {
  if (temp === -999) {
    continue; // Ignore les valeurs d'erreur
  }

  somme += temp;
  compteur++;
}

const moyenne = somme / compteur;
console.log(`Température moyenne : ${moyenne.toFixed(1)}°C`);
// Température moyenne : 22.8°C
```

### Exemple 3 : Traiter uniquement certains éléments

```javascript
const produits = [
  { nom: "Ordinateur", prix: 899, enStock: true },
  { nom: "Souris", prix: 25, enStock: false },
  { nom: "Clavier", prix: 75, enStock: true },
  { nom: "Écran", prix: 299, enStock: false }
];

console.log("Produits en stock :");
for (const produit of produits) {
  if (!produit.enStock) {
    continue; // Ignore les produits en rupture
  }
  console.log(`- ${produit.nom} : ${produit.prix}€`);
}
```

**Résultat :**
```
Produits en stock :
- Ordinateur : 899€
- Clavier : 75€
```

### Exemple 4 : Éviter les divisions par zéro

```javascript
const dividendes = [10, 20, 30, 40];
const diviseurs = [2, 0, 5, 0];

console.log("Résultats des divisions :");
for (let i = 0; i < dividendes.length; i++) {
  if (diviseurs[i] === 0) {
    console.log(`Division ${i + 1} : impossible (division par zéro)`);
    continue;
  }

  const resultat = dividendes[i] / diviseurs[i];
  console.log(`Division ${i + 1} : ${dividendes[i]} / ${diviseurs[i]} = ${resultat}`);
}
```

---

## `break` vs `continue` : Quelle est la différence ?

### Comparaison directe

```javascript
console.log("=== Avec BREAK ===");
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    console.log("Break à 5");
    break; // SORT de la boucle
  }
  console.log(i);
}

console.log("\n=== Avec CONTINUE ===");
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    console.log("Continue à 5");
    continue; // SAUTE l'itération 5
  }
  console.log(i);
}
```

**Résultat :**
```
=== Avec BREAK ===
0
1
2
3
4
Break à 5

=== Avec CONTINUE ===
0
1
2
3
4
Continue à 5
6
7
8
9
```

### Tableau récapitulatif

| Instruction | Action | La boucle continue ? | Code après l'instruction |
|-------------|--------|----------------------|-------------------------|
| `break` | Sort de la boucle | ❌ Non | Non exécuté |
| `continue` | Passe à l'itération suivante | ✅ Oui | Non exécuté (pour cette itération) |

---

## Combiner `break` et `continue`

Vous pouvez utiliser les deux dans la même boucle (mais sur des conditions différentes).

### Exemple : Recherche avec filtrage

```javascript
const nombres = [5, 12, -3, 8, 45, -7, 23, 67, 34];

console.log("Recherche du premier nombre > 40 (nombres négatifs ignorés) :");
for (const nombre of nombres) {
  if (nombre < 0) {
    console.log(`${nombre} est négatif, on l'ignore`);
    continue; // Ignore les négatifs
  }

  console.log(`Vérification de ${nombre}...`);

  if (nombre > 40) {
    console.log(`✅ Trouvé : ${nombre}`);
    break; // On a trouvé, on arrête
  }
}
```

**Résultat :**
```
Vérification de 5...
Vérification de 12...
-3 est négatif, on l'ignore
Vérification de 8...
✅ Trouvé : 45
```

---

## Boucles imbriquées : `break` et `continue`

### `break` dans une boucle imbriquée

⚠️ **Important :** `break` ne sort que de la boucle **la plus proche** (celle où il se trouve).

```javascript
console.log("=== Boucles imbriquées avec break ===");

for (let i = 1; i <= 3; i++) {
  console.log(`\nBoucle externe i = ${i}`);

  for (let j = 1; j <= 5; j++) {
    if (j === 3) {
      console.log("  Break à j = 3");
      break; // Sort uniquement de la boucle interne
    }
    console.log(`  Boucle interne j = ${j}`);
  }

  console.log("  Retour à la boucle externe");
}
```

**Résultat :**
```
=== Boucles imbriquées avec break ===

Boucle externe i = 1
  Boucle interne j = 1
  Boucle interne j = 2
  Break à j = 3
  Retour à la boucle externe

Boucle externe i = 2
  Boucle interne j = 1
  Boucle interne j = 2
  Break à j = 3
  Retour à la boucle externe

Boucle externe i = 3
  Boucle interne j = 1
  Boucle interne j = 2
  Break à j = 3
  Retour à la boucle externe
```

### `continue` dans une boucle imbriquée

```javascript
for (let i = 1; i <= 3; i++) {
  console.log(`\nLigne ${i} :`);

  for (let j = 1; j <= 5; j++) {
    if (j === 3) {
      continue; // Saute j = 3
    }
    console.log(`  ${i}-${j}`);
  }
}
```

**Résultat :**
```
Ligne 1 :
  1-1
  1-2
  1-4
  1-5

Ligne 2 :
  2-1
  2-2
  2-4
  2-5

Ligne 3 :
  3-1
  3-2
  3-4
  3-5
```

### Sortir de plusieurs boucles imbriquées (avec labels)

Si vous devez sortir de plusieurs boucles à la fois, vous pouvez utiliser des **labels** (rarement utilisé, mais possible).

```javascript
boucleExterne: // Label
for (let i = 1; i <= 5; i++) {
  for (let j = 1; j <= 5; j++) {
    if (i * j > 10) {
      console.log(`i=${i}, j=${j}, produit=${i*j} > 10`);
      break boucleExterne; // Sort de TOUTES les boucles
    }
    console.log(`${i} × ${j} = ${i * j}`);
  }
}

console.log("Toutes les boucles terminées");
```

**Résultat :**
```
1 × 1 = 1
1 × 2 = 2
1 × 3 = 3
1 × 4 = 4
1 × 5 = 5
2 × 1 = 2
2 × 2 = 4
2 × 3 = 6
2 × 4 = 8
2 × 5 = 10
3 × 1 = 3
3 × 2 = 6
3 × 3 = 9
i=3, j=4, produit=12 > 10
Toutes les boucles terminées
```

---

## ⚠️ Pièges et erreurs courantes

### Erreur 1 : `continue` avec `while` (placement de l'incrémentation)

```javascript
// ❌ ATTENTION : Boucle infinie possible !
let i = 0;
while (i < 10) {
  if (i % 2 !== 0) {
    continue; // Si i est impair, on ne fait jamais i++
  }
  console.log(i);
  i++; // Cette ligne n'est jamais atteinte pour les impairs !
}
```

**✅ Solution : Incrémenter AVANT le continue**

```javascript
let i = 0;
while (i < 10) {
  i++; // ✅ Incrémenter en premier

  if (i % 2 !== 0) {
    continue;
  }
  console.log(i);
}
```

### Erreur 2 : Utiliser `break` en dehors d'une boucle

```javascript
// ❌ Erreur de syntaxe
if (condition) {
  break; // Erreur : break doit être dans une boucle ou switch
}
```

### Erreur 3 : Code inaccessible après `break` ou `continue`

```javascript
for (let i = 0; i < 5; i++) {
  break;
  console.log(i); // ⚠️ Ce code ne sera jamais exécuté
}
```

**Attention :** Les éditeurs modernes vous avertiront souvent de ce problème ("unreachable code").

---

## Quand utiliser `break` et `continue` ?

### ✅ Utilisez `break` quand :

- Vous cherchez un élément et **voulez arrêter** dès que vous le trouvez
- Une **condition d'erreur** nécessite l'arrêt de la boucle
- Vous avez atteint une **limite** (tentatives, temps, etc.)
- Continuer la boucle serait **inutile** ou **inefficace**

### ✅ Utilisez `continue` quand :

- Vous voulez **ignorer certains éléments** sans arrêter la boucle
- Vous devez **filtrer** des valeurs invalides
- Certaines conditions rendent le **traitement inutile** pour cette itération
- Vous voulez **éviter l'imbrication excessive** de conditions

### ❌ Évitez d'utiliser si :

- Une **méthode de tableau** moderne fait mieux le travail (`filter`, `find`, `some`, etc.)
- Cela rend le code **moins lisible**
- Une simple **condition if** suffirait

---

## Alternatives modernes

Dans de nombreux cas, les méthodes de tableaux modernes sont plus claires que `break` et `continue`.

### Alternative à `break` : `find()`

```javascript
// Avec for + break
const nombres = [5, 12, 8, 45, 23, 67];
let resultat;

for (const nombre of nombres) {
  if (nombre > 40) {
    resultat = nombre;
    break;
  }
}

console.log(resultat); // 45

// ✅ Plus moderne avec find()
const resultat2 = nombres.find(n => n > 40);
console.log(resultat2); // 45
```

### Alternative à `continue` : `filter()`

```javascript
const nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Avec for + continue
const pairs = [];
for (const nombre of nombres) {
  if (nombre % 2 !== 0) {
    continue;
  }
  pairs.push(nombre);
}

console.log(pairs); // [2, 4, 6, 8, 10]

// ✅ Plus moderne avec filter()
const pairs2 = nombres.filter(n => n % 2 === 0);
console.log(pairs2); // [2, 4, 6, 8, 10]
```

### Alternative : `some()` pour vérifier l'existence

```javascript
const nombres = [5, 12, 8, 45, 23];

// Avec for + break
let aTrouveGrand = false;
for (const nombre of nombres) {
  if (nombre > 40) {
    aTrouveGrand = true;
    break;
  }
}

console.log(aTrouveGrand); // true

// ✅ Plus moderne avec some()
const aTrouveGrand2 = nombres.some(n => n > 40);
console.log(aTrouveGrand2); // true
```

---

## Exemples pratiques complets

### Exemple 1 : Validation de mot de passe

```javascript
function validerMotDePasse(motDePasse) {
  const regles = [
    { test: (mp) => mp.length >= 8, message: "au moins 8 caractères" },
    { test: (mp) => /[A-Z]/.test(mp), message: "une majuscule" },
    { test: (mp) => /[a-z]/.test(mp), message: "une minuscule" },
    { test: (mp) => /[0-9]/.test(mp), message: "un chiffre" },
    { test: (mp) => /[!@#$%^&*]/.test(mp), message: "un caractère spécial" }
  ];

  for (const regle of regles) {
    if (!regle.test(motDePasse)) {
      console.log(`❌ Le mot de passe doit contenir ${regle.message}`);
      return false; // Équivalent à break + return
    }
  }

  console.log("✅ Mot de passe valide");
  return true;
}

validerMotDePasse("Pass123!"); // ✅ Mot de passe valide
validerMotDePasse("pass123!");  // ❌ Le mot de passe doit contenir une majuscule
```

### Exemple 2 : Traiter un fichier ligne par ligne

```javascript
const lignes = [
  "# Ceci est un commentaire",
  "Alice,25,Paris",
  "",
  "Bob,30,Lyon",
  "# Un autre commentaire",
  "Charlie,28,Marseille"
];

const utilisateurs = [];

for (const ligne of lignes) {
  // Ignorer les lignes vides
  if (ligne.trim() === "") {
    continue;
  }

  // Ignorer les commentaires
  if (ligne.startsWith("#")) {
    continue;
  }

  const [nom, age, ville] = ligne.split(",");
  utilisateurs.push({ nom, age: parseInt(age), ville });
}

console.log(utilisateurs);
// [
//   { nom: "Alice", age: 25, ville: "Paris" },
//   { nom: "Bob", age: 30, ville: "Lyon" },
//   { nom: "Charlie", age: 28, ville: "Marseille" }
// ]
```

### Exemple 3 : Jeu du plus ou moins

```javascript
function jeuPlusOuMoins() {
  const nombreSecret = 42;
  const tentativesMax = 5;
  const propositions = [50, 30, 40, 42, 45]; // Simulations

  for (let i = 0; i < tentativesMax; i++) {
    const proposition = propositions[i];
    console.log(`\nTentative ${i + 1} : ${proposition}`);

    if (proposition === nombreSecret) {
      console.log(`🎉 Bravo ! Trouvé en ${i + 1} tentatives !`);
      break; // Jeu terminé
    }

    if (proposition < nombreSecret) {
      console.log("↗️  C'est plus !");
    } else {
      console.log("↘️  C'est moins !");
    }

    if (i === tentativesMax - 1) {
      console.log(`\n😞 Perdu ! Le nombre était ${nombreSecret}`);
    }
  }
}

jeuPlusOuMoins();
```

---

## Bonnes pratiques

### ✅ Privilégiez la clarté

```javascript
// ❌ Peu clair
for (let i = 0; i < arr.length; i++) {
  if (arr[i] < 0) continue;
  if (arr[i] > 100) break;
  process(arr[i]);
}

// ✅ Plus clair avec des commentaires
for (let i = 0; i < arr.length; i++) {
  // Ignorer les valeurs négatives
  if (arr[i] < 0) {
    continue;
  }

  // Arrêter si on dépasse 100
  if (arr[i] > 100) {
    break;
  }

  process(arr[i]);
}
```

### ✅ Évitez l'usage excessif

```javascript
// ❌ Trop de break/continue rend le code confus
for (let i = 0; i < n; i++) {
  if (cond1) continue;
  if (cond2) break;
  if (cond3) continue;
  if (cond4) break;
  // ...
}

// ✅ Mieux : restructurer la logique
for (let i = 0; i < n; i++) {
  if (shouldProcess(i)) {
    process(i);
  }
  if (shouldStop(i)) {
    break;
  }
}
```

### ✅ Documentez l'intention

```javascript
// ✅ Bon
for (const user of users) {
  // On ignore les utilisateurs inactifs
  if (!user.isActive) {
    continue;
  }

  // On arrête dès qu'on trouve un admin
  if (user.isAdmin) {
    return user;
  }

  processUser(user);
}
```

---

## Résumé

### Points clés à retenir

- **`break`** : Sort **complètement** de la boucle
- **`continue`** : Passe à l'**itération suivante**
- `break` et `continue` fonctionnent avec `for`, `while`, `do-while`, `for...of`, `for...in`
- Dans les boucles imbriquées, ils n'affectent que la boucle **la plus proche**
- Utilisez des **labels** pour sortir de plusieurs boucles (rare)
- ⚠️ Attention au placement de l'incrémentation avec `continue` dans `while`
- Les **méthodes de tableaux** modernes (`find`, `filter`, `some`) sont souvent plus claires

### Aide-mémoire

```javascript
// break : SORTIR
for (const item of items) {
  if (conditionTrouvee) {
    break; // ← Sort de la boucle
  }
}
// Code continue ici après break

// continue : SAUTER
for (const item of items) {
  if (devraitIgnorer) {
    continue; // ← Passe à l'itération suivante
  }
  traiter(item);
}
```

### Quand les utiliser ?

| Situation | Utilisez | Alternative moderne |
|-----------|----------|---------------------|
| Chercher un élément | `break` | `find()`, `findIndex()` |
| Filtrer des éléments | `continue` | `filter()` |
| Vérifier existence | `break` | `some()` |
| Arrêt sur erreur | `break` | `try-catch` |

Les instructions `break` et `continue` sont des outils puissants pour contrôler le flux d'exécution de vos boucles. Utilisez-les judicieusement pour rendre votre code plus efficace et plus lisible ! 🎯

⏭️ [Fonctions modernes](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/README.md)
