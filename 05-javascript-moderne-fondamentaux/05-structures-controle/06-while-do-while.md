🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.6 - Boucle while et do-while

## Introduction

Les boucles `while` et `do-while` sont des structures de répétition utilisées quand on ne sait pas à l'avance **combien de fois** le code doit être exécuté. Contrairement à la boucle `for` qui est idéale pour un nombre d'itérations connu, ces boucles continuent **tant qu'une condition est vraie**.

**Analogie :** Imaginez que vous remplissez un verre d'eau. Vous ne savez pas combien de fois vous allez verser, vous continuez **tant que** le verre n'est pas plein. C'est exactement le principe de `while` !

---

## La boucle `while`

### Syntaxe

```javascript
while (condition) {
  // Code à répéter tant que la condition est vraie
}
```

### Fonctionnement

1. La **condition** est testée
2. Si elle est **vraie** → le code dans les accolades est exécuté
3. On revient à l'étape 1 (test de la condition)
4. Si elle est **fausse** → la boucle s'arrête

### Premier exemple simple

```javascript
let compteur = 0;

while (compteur < 5) {
  console.log(`Compteur : ${compteur}`);
  compteur++;
}

console.log("Boucle terminée !");
```

**Résultat :**
```
Compteur : 0
Compteur : 1
Compteur : 2
Compteur : 3
Compteur : 4
Boucle terminée !
```

**Explication :**
- Au début, `compteur = 0`, donc `compteur < 5` est vrai
- Le code s'exécute et `compteur` devient 1
- On teste à nouveau : `1 < 5` est vrai, on continue
- Quand `compteur = 5`, la condition `5 < 5` est fausse, on sort de la boucle

---

## Différence entre `while` et `for`

Ces deux boucles peuvent souvent faire la même chose, mais leur usage diffère.

### Avec `for` (nombre d'itérations connu)

```javascript
// Je sais que je veux 5 itérations
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

### Avec `while` (condition à surveiller)

```javascript
// Je continue tant qu'une condition est vraie
let compteur = 0;

while (compteur < 5) {
  console.log(compteur);
  compteur++;
}
```

**Quand utiliser quoi ?**
- **`for`** : Quand vous savez combien de tours faire (parcourir un tableau, compter de 1 à 10, etc.)
- **`while`** : Quand vous continuez jusqu'à ce qu'une condition change (attendre une saisie valide, chercher jusqu'à trouver, etc.)

---

## ⚠️ Attention aux boucles infinies !

C'est le piège le plus dangereux avec `while`. Si la condition reste toujours vraie, la boucle ne s'arrête jamais !

### ❌ Boucle infinie (erreur)

```javascript
let compteur = 0;

// ❌ ATTENTION : Boucle infinie !
while (compteur < 5) {
  console.log(compteur);
  // Oubli de compteur++ → la condition reste toujours vraie !
}
```

**Résultat :** Le programme plante ou votre navigateur se fige. 😱

### ✅ Solution : Toujours modifier la variable de condition

```javascript
let compteur = 0;

while (compteur < 5) {
  console.log(compteur);
  compteur++; // ✅ Important : on modifie la variable !
}
```

**Règle d'or :** Assurez-vous que la condition finira par devenir fausse !

---

## Exemples pratiques avec `while`

### Exemple 1 : Demander une saisie valide (simulation)

```javascript
let motDePasse = "";
let tentatives = 0;

// Simulons des saisies
const saisies = ["123", "azerty", "password", "MonMotDePasse123"];
let indexSaisie = 0;

while (motDePasse !== "MonMotDePasse123" && tentatives < 3) {
  motDePasse = saisies[indexSaisie]; // Simulation de saisie
  indexSaisie++;
  tentatives++;

  if (motDePasse === "MonMotDePasse123") {
    console.log("✅ Mot de passe correct !");
  } else {
    console.log(`❌ Incorrect. Tentative ${tentatives}/3`);
  }
}

if (motDePasse !== "MonMotDePasse123") {
  console.log("🔒 Compte bloqué après 3 tentatives");
}
```

### Exemple 2 : Chercher un élément

```javascript
const nombres = [10, 25, 30, 45, 60, 75];
const cible = 45;
let index = 0;
let trouve = false;

while (index < nombres.length && !trouve) {
  if (nombres[index] === cible) {
    console.log(`✅ ${cible} trouvé à l'index ${index}`);
    trouve = true;
  }
  index++;
}

if (!trouve) {
  console.log(`❌ ${cible} non trouvé`);
}
```

### Exemple 3 : Diviser jusqu'à un certain seuil

```javascript
let nombre = 1000;
let divisions = 0;

while (nombre > 1) {
  nombre = nombre / 2;
  divisions++;
  console.log(`Après division ${divisions} : ${nombre}`);
}

console.log(`Il a fallu ${divisions} divisions pour arriver en dessous de 1`);
```

**Résultat :**
```
Après division 1 : 500
Après division 2 : 250
Après division 3 : 125
Après division 4 : 62.5
Après division 5 : 31.25
Après division 6 : 15.625
Après division 7 : 7.8125
Après division 8 : 3.90625
Après division 9 : 1.953125
Après division 10 : 0.9765625
Il a fallu 10 divisions pour arriver en dessous de 1
```

### Exemple 4 : Consommer des éléments d'un tableau

```javascript
const taches = ["Laver la voiture", "Faire les courses", "Étudier JavaScript"];

console.log("Tâches à faire :");
while (taches.length > 0) {
  const tache = taches.shift(); // Retire le premier élément
  console.log(`✓ ${tache}`);
}

console.log("Toutes les tâches sont terminées !");
```

---

## La boucle `do-while`

La boucle `do-while` est similaire à `while`, mais avec une différence cruciale : **le code s'exécute au moins une fois** avant de tester la condition.

### Syntaxe

```javascript
do {
  // Code à exécuter
} while (condition);
```

**Note :** Le point-virgule après la condition est important !

### Fonctionnement

1. Le code dans les accolades est **exécuté une fois**
2. Ensuite, la **condition** est testée
3. Si elle est **vraie** → on recommence à l'étape 1
4. Si elle est **fausse** → on sort de la boucle

---

## Différence entre `while` et `do-while`

### Avec `while` : condition testée AVANT

```javascript
let compteur = 10;

while (compteur < 5) {
  console.log("Ce message ne s'affichera jamais");
  compteur++;
}

console.log("Boucle terminée");
```

**Résultat :**
```
Boucle terminée
```

**Explication :** La condition `10 < 5` est fausse dès le début, donc le code n'est **jamais exécuté**.

### Avec `do-while` : condition testée APRÈS

```javascript
let compteur = 10;

do {
  console.log("Ce message s'affiche au moins une fois");
  compteur++;
} while (compteur < 5);

console.log("Boucle terminée");
```

**Résultat :**
```
Ce message s'affiche au moins une fois
Boucle terminée
```

**Explication :** Le code s'exécute une fois, puis la condition `11 < 5` est testée et est fausse, donc on sort.

---

## Quand utiliser `do-while` ?

Utilisez `do-while` quand vous voulez **garantir au moins une exécution** du code, même si la condition est fausse dès le début.

### Exemple typique : Menu avec saisie utilisateur

```javascript
let choix;
let continuer = true;

do {
  console.log("\n=== MENU ===");
  console.log("1. Option A");
  console.log("2. Option B");
  console.log("3. Quitter");

  // Simulation de saisie
  choix = 1; // On simule que l'utilisateur choisit 1

  switch (choix) {
    case 1:
      console.log("Vous avez choisi l'option A");
      continuer = false; // Pour arrêter l'exemple
      break;
    case 2:
      console.log("Vous avez choisi l'option B");
      continuer = false;
      break;
    case 3:
      console.log("Au revoir !");
      continuer = false;
      break;
    default:
      console.log("Choix invalide, réessayez");
  }
} while (continuer);
```

**Pourquoi `do-while` ici ?** Le menu doit s'afficher **au moins une fois**, même si on ne connaît pas encore le choix de l'utilisateur.

---

## Exemples pratiques avec `do-while`

### Exemple 1 : Validation de données

```javascript
let age;
const agesTest = [-5, 150, 25]; // Simulations de saisies
let tentative = 0;

do {
  age = agesTest[tentative];
  tentative++;

  if (age < 0 || age > 120) {
    console.log(`❌ Âge invalide : ${age}`);
  }
} while ((age < 0 || age > 120) && tentative < agesTest.length);

if (age >= 0 && age <= 120) {
  console.log(`✅ Âge valide : ${age}`);
}
```

### Exemple 2 : Calculer la somme jusqu'à un total

```javascript
let somme = 0;
let nombre = 1;

do {
  somme += nombre;
  console.log(`Ajout de ${nombre}, somme = ${somme}`);
  nombre++;
} while (somme < 100);

console.log(`Somme finale : ${somme}`);
```

**Résultat :**
```
Ajout de 1, somme = 1
Ajout de 2, somme = 3
Ajout de 3, somme = 6
Ajout de 4, somme = 10
...
Ajout de 13, somme = 91
Ajout de 14, somme = 105
Somme finale : 105
```

### Exemple 3 : Générer un nombre aléatoire jusqu'à obtenir une valeur

```javascript
let nombreAleatoire;
let essais = 0;

do {
  nombreAleatoire = Math.floor(Math.random() * 10) + 1; // Entre 1 et 10
  essais++;
  console.log(`Essai ${essais} : ${nombreAleatoire}`);
} while (nombreAleatoire !== 7);

console.log(`✅ Trouvé le 7 en ${essais} essais !`);
```

---

## Contrôle de flux : `break` et `continue`

Comme avec les autres boucles, vous pouvez utiliser `break` et `continue` avec `while` et `do-while`.

### `break` : Sortir immédiatement de la boucle

```javascript
let compteur = 0;

while (compteur < 100) {
  console.log(compteur);
  compteur++;

  if (compteur === 5) {
    console.log("On arrête à 5 !");
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
On arrête à 5 !
Boucle terminée
```

### `continue` : Passer à l'itération suivante

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

### ⚠️ Attention avec `continue` dans `while`

Assurez-vous que la variable de condition est modifiée **avant** le `continue`, sinon vous risquez une boucle infinie !

```javascript
let compteur = 0;

while (compteur < 10) {
  if (compteur % 2 !== 0) {
    continue; // ❌ Boucle infinie si compteur est impair !
  }

  compteur++; // Cette ligne n'est jamais atteinte pour les impairs
  console.log(compteur);
}
```

**✅ Correct :**

```javascript
let compteur = 0;

while (compteur < 10) {
  compteur++; // ✅ Incrémenter AVANT le continue

  if (compteur % 2 !== 0) {
    continue;
  }

  console.log(compteur);
}
```

---

## Boucles imbriquées avec `while`

Vous pouvez imbriquer des boucles `while`, mais c'est moins courant qu'avec `for`.

### Exemple : Table de multiplication

```javascript
let i = 1;

while (i <= 3) {
  console.log(`Table de ${i} :`);

  let j = 1;
  while (j <= 5) {
    console.log(`  ${i} × ${j} = ${i * j}`);
    j++;
  }

  console.log(""); // Ligne vide
  i++;
}
```

---

## Comparaison des trois types de boucles

### Exemple identique avec les trois boucles

#### Avec `for`

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

#### Avec `while`

```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

#### Avec `do-while`

```javascript
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

**Les trois produisent le même résultat :** `0, 1, 2, 3, 4`

---

## Quand utiliser quelle boucle ?

### Utilisez `for` quand :

- ✅ Vous connaissez le **nombre d'itérations** à l'avance
- ✅ Vous parcourez un **tableau** avec un index
- ✅ Vous comptez de X à Y

**Exemple :**
```javascript
for (let i = 0; i < tableau.length; i++) {
  // Parcourir un tableau
}
```

### Utilisez `while` quand :

- ✅ Vous continuez **tant qu'une condition est vraie**
- ✅ Le nombre d'itérations est **inconnu**
- ✅ Vous attendez un **événement** ou une **saisie valide**

**Exemple :**
```javascript
while (!utilisateurConnecte) {
  // Continuer jusqu'à connexion réussie
}
```

### Utilisez `do-while` quand :

- ✅ Le code doit s'exécuter **au moins une fois**
- ✅ Vous affichez un **menu** ou une **interface**
- ✅ Vous demandez une saisie qui doit être **validée**

**Exemple :**
```javascript
do {
  afficherMenu();
  choix = obtenirChoix();
} while (choix !== "quitter");
```

---

## Exemples pratiques avancés

### Exemple 1 : Algorithme de recherche binaire (simplifié)

```javascript
const tableau = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];
const cible = 13;

let debut = 0;
let fin = tableau.length - 1;
let trouve = false;

while (debut <= fin && !trouve) {
  const milieu = Math.floor((debut + fin) / 2);

  console.log(`Recherche entre indices ${debut} et ${fin}, milieu = ${milieu}`);

  if (tableau[milieu] === cible) {
    console.log(`✅ ${cible} trouvé à l'index ${milieu}`);
    trouve = true;
  } else if (tableau[milieu] < cible) {
    debut = milieu + 1; // Chercher dans la moitié droite
  } else {
    fin = milieu - 1; // Chercher dans la moitié gauche
  }
}

if (!trouve) {
  console.log(`❌ ${cible} non trouvé`);
}
```

### Exemple 2 : Calcul du PGCD (Plus Grand Commun Diviseur)

```javascript
let a = 48;
let b = 18;

console.log(`Calcul du PGCD de ${a} et ${b}`);

while (b !== 0) {
  const temp = b;
  b = a % b;
  a = temp;
  console.log(`a = ${a}, b = ${b}`);
}

console.log(`PGCD : ${a}`);
```

### Exemple 3 : Simuler un jeu de devinette

```javascript
const nombreSecret = 42;
const tentativesMax = 5;
let tentatives = 0;
let devine = false;

// Simulations de propositions
const propositions = [50, 30, 40, 42];
let indexProposition = 0;

console.log("Devinez le nombre entre 1 et 100 !");

while (tentatives < tentativesMax && !devine) {
  tentatives++;
  const proposition = propositions[indexProposition++];

  console.log(`\nTentative ${tentatives} : ${proposition}`);

  if (proposition === nombreSecret) {
    console.log(`🎉 Bravo ! Vous avez trouvé en ${tentatives} tentatives !`);
    devine = true;
  } else if (proposition < nombreSecret) {
    console.log("↗️  C'est plus !");
  } else {
    console.log("↘️  C'est moins !");
  }
}

if (!devine) {
  console.log(`\n😞 Perdu ! Le nombre était ${nombreSecret}`);
}
```

### Exemple 4 : Parcourir une liste chaînée (structure avancée)

```javascript
// Simulation d'une liste chaînée simple
const liste = {
  valeur: 10,
  suivant: {
    valeur: 20,
    suivant: {
      valeur: 30,
      suivant: {
        valeur: 40,
        suivant: null
      }
    }
  }
};

let noeudActuel = liste;

console.log("Éléments de la liste :");
while (noeudActuel !== null) {
  console.log(noeudActuel.valeur);
  noeudActuel = noeudActuel.suivant;
}
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier d'incrémenter le compteur

```javascript
let i = 0;

// ❌ Boucle infinie
while (i < 5) {
  console.log(i);
  // Oubli de i++
}
```

### ❌ Erreur 2 : Modifier la mauvaise variable

```javascript
let compteur = 0;
let limite = 5;

// ❌ Modifie limite au lieu de compteur
while (compteur < limite) {
  console.log(compteur);
  limite++; // Erreur : la condition ne change jamais !
}
```

### ❌ Erreur 3 : Condition qui ne peut jamais être fausse

```javascript
let x = 10;

// ❌ x sera toujours positif
while (x > 0) {
  console.log(x);
  x++; // x augmente, donc reste toujours > 0
}
```

### ❌ Erreur 4 : Utiliser `=` au lieu de `==` ou `===`

```javascript
let trouve = false;

// ❌ Boucle infinie : trouve = false (affectation, toujours vraie)
while (trouve = false) {
  console.log("Ceci ne s'arrêtera jamais");
}

// ✅ Correct
while (trouve === false) {
  // ...
}

// ✅ Encore mieux
while (!trouve) {
  // ...
}
```

---

## Bonnes pratiques

### ✅ Toujours prévoir une condition de sortie

```javascript
// ✅ Bon
let tentatives = 0;
const maxTentatives = 100;

while (!trouve && tentatives < maxTentatives) {
  // Recherche
  tentatives++;
}

if (tentatives >= maxTentatives) {
  console.log("⚠️ Nombre maximum de tentatives atteint");
}
```

### ✅ Utiliser des variables booléennes pour la clarté

```javascript
// ✅ Plus clair
let rechercheFinie = false;

while (!rechercheFinie) {
  // ...
  if (conditionTrouvee) {
    rechercheFinie = true;
  }
}
```

### ✅ Limiter la complexité dans la condition

```javascript
// ❌ Trop complexe
while (a > 0 && b < 10 && !c && (d === "ok" || e > 5)) {
  // Difficile à comprendre
}

// ✅ Plus clair
const peutContinuer = a > 0 && b < 10 && !c && (d === "ok" || e > 5);
while (peutContinuer) {
  // ...
  peutContinuer = /* recalculer */;
}
```

---

## Résumé

### Points clés à retenir

- **`while`** : Teste la condition **avant** d'exécuter le code (peut ne jamais s'exécuter)
- **`do-while`** : Exécute le code **au moins une fois**, puis teste la condition
- Utilisez `while` quand le nombre d'itérations est **inconnu**
- Utilisez `do-while` quand vous voulez **garantir une exécution**
- ⚠️ **Attention aux boucles infinies** : assurez-vous que la condition finira par être fausse
- Préférez `for` quand vous connaissez le nombre d'itérations

### Tableau de comparaison

| Boucle | Test de condition | Exécution minimale | Usage typique |
|--------|-------------------|-------------------|---------------|
| `for` | Avant | 0 fois | Nombre d'itérations connu |
| `while` | Avant | 0 fois | Condition à surveiller |
| `do-while` | Après | 1 fois | Menu, validation |

### Aide-mémoire

```javascript
// while : tant que...
while (condition) {
  // Peut ne jamais s'exécuter
}

// do-while : fais... tant que...
do {
  // S'exécute toujours au moins une fois
} while (condition);

// for : pour chaque...
for (let i = 0; i < n; i++) {
  // Nombre d'itérations connu
}
```

Les boucles `while` et `do-while` sont des outils puissants pour gérer des situations où le nombre d'itérations n'est pas connu à l'avance. Maîtrisez-les, mais restez vigilant face aux boucles infinies ! 🔄

⏭️ [Instructions break et continue](/05-javascript-moderne-fondamentaux/05-structures-controle/07-break-continue.md)
