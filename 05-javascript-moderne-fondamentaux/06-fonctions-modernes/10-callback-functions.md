🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.10 - Callback Functions

## Introduction

Une **callback function** (fonction de rappel) est une fonction qui est **passée en argument** à une autre fonction, et qui sera **exécutée plus tard** par cette fonction.

Les callbacks sont **omniprésents** en JavaScript : manipulation de tableaux, gestion d'événements, requêtes HTTP, timers... C'est un concept fondamental à maîtriser absolument.

## Qu'est-ce qu'un callback ?

En JavaScript, les fonctions sont des **valeurs** (on dit que ce sont des "first-class citizens"). Cela signifie qu'on peut :
- Les assigner à des variables
- Les passer en argument à d'autres fonctions ← **C'est un callback !**
- Les retourner depuis des fonctions

### Analogie simple

Imaginez que vous appelez un plombier :
- Vous lui donnez votre **numéro de téléphone** (le callback)
- Vous lui demandez de vous **rappeler** quand le travail est terminé
- Le plombier fait son travail (fonction principale)
- Puis il vous **rappelle** (exécute le callback)

## Premier exemple simple

### Sans callback : exécution immédiate

```javascript
function direBonjour() {
  console.log("Bonjour !");
}

direBonjour();  // Appel immédiat
// Affiche : "Bonjour !"
```

### Avec callback : exécution différée

```javascript
function direBonjour() {
  console.log("Bonjour !");
}

function executerCallback(callback) {
  console.log("Avant le callback");
  callback();  // Exécute la fonction passée en paramètre
  console.log("Après le callback");
}

executerCallback(direBonjour);
// Affiche :
// Avant le callback
// Bonjour !
// Après le callback
```

**Points importants :**
- `direBonjour` est passée **sans parenthèses** (on passe la fonction, on ne l'appelle pas)
- `executerCallback` décide **quand** exécuter le callback

## Syntaxe et décortication

### Passer une fonction nommée

```javascript
function traiter(nombre) {
  console.log("Le nombre est :", nombre);
}

function executerAvec10(callback) {
  callback(10);  // Appelle callback avec l'argument 10
}

executerAvec10(traiter);
// Affiche : "Le nombre est : 10"
```

### Passer une fonction anonyme

```javascript
executerAvec10(function(nombre) {
  console.log("Le nombre est :", nombre);
});
// Affiche : "Le nombre est : 10"
```

### Passer une arrow function (moderne) ✅

```javascript
executerAvec10((nombre) => {
  console.log("Le nombre est :", nombre);
});

// Ou version ultra-concise
executerAvec10(nombre => console.log("Le nombre est :", nombre));
```

## Pourquoi utiliser des callbacks ?

### 1. Réutilisation et flexibilité

Une fonction peut avoir différents comportements selon le callback passé :

```javascript
function appliquerOperation(a, b, operation) {
  return operation(a, b);
}

const additionner = (x, y) => x + y;
const multiplier = (x, y) => x * y;
const soustraire = (x, y) => x - y;

console.log(appliquerOperation(5, 3, additionner));  // 8
console.log(appliquerOperation(5, 3, multiplier));   // 15
console.log(appliquerOperation(5, 3, soustraire));   // 2
```

### 2. Traitement asynchrone

Les callbacks permettent de gérer des opérations qui prennent du temps :

```javascript
function simulerChargement(callback) {
  console.log("Chargement en cours...");

  // Simule un délai
  setTimeout(() => {
    console.log("Chargement terminé !");
    callback();
  }, 2000);
}

simulerChargement(() => {
  console.log("Callback exécuté !");
});

// Affiche :
// Chargement en cours...
// (2 secondes d'attente)
// Chargement terminé !
// Callback exécuté !
```

### 3. Personnalisation du comportement

```javascript
function repeter(n, action) {
  for (let i = 0; i < n; i++) {
    action(i);
  }
}

// Différentes actions
repeter(3, i => console.log("Itération", i));
// Itération 0
// Itération 1
// Itération 2

repeter(3, i => console.log(i * 2));
// 0
// 2
// 4
```

## Callbacks synchrones

Les **callbacks synchrones** sont exécutés immédiatement, dans l'ordre du code.

### Exemple de callback synchrone

```javascript
function traiterTableau(tableau, callback) {
  console.log("Début du traitement");

  for (let element of tableau) {
    callback(element);  // Exécuté immédiatement
  }

  console.log("Fin du traitement");
}

traiterTableau([1, 2, 3], nombre => {
  console.log("Nombre :", nombre);
});

// Affiche :
// Début du traitement
// Nombre : 1
// Nombre : 2
// Nombre : 3
// Fin du traitement
```

### Méthodes de tableau avec callbacks

Les méthodes de tableau en JavaScript utilisent massivement les callbacks :

#### forEach

```javascript
const fruits = ["pomme", "banane", "orange"];

fruits.forEach(fruit => {
  console.log("J'aime les", fruit + "s");
});

// J'aime les pommes
// J'aime les bananes
// J'aime les oranges
```

#### map

```javascript
const nombres = [1, 2, 3, 4, 5];

const doubles = nombres.map(n => n * 2);
console.log(doubles);  // [2, 4, 6, 8, 10]
```

#### filter

```javascript
const ages = [12, 15, 18, 21, 25, 30];

const majeurs = ages.filter(age => age >= 18);
console.log(majeurs);  // [18, 21, 25, 30]
```

#### find

```javascript
const utilisateurs = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" },
  { id: 3, nom: "Charlie" }
];

const utilisateur = utilisateurs.find(u => u.id === 2);
console.log(utilisateur);  // { id: 2, nom: "Bob" }
```

## Callbacks asynchrones

Les **callbacks asynchrones** sont exécutés plus tard, après une opération asynchrone.

### setTimeout : callback après un délai

```javascript
console.log("Début");

setTimeout(() => {
  console.log("2 secondes écoulées");
}, 2000);

console.log("Fin");

// Affiche :
// Début
// Fin
// (2 secondes d'attente)
// 2 secondes écoulées
```

**Important :** Le code continue de s'exécuter pendant l'attente !

### setInterval : callback répété

```javascript
let compteur = 0;

const intervalId = setInterval(() => {
  compteur++;
  console.log("Compteur :", compteur);

  if (compteur === 3) {
    clearInterval(intervalId);  // Arrête l'intervalle
    console.log("Terminé !");
  }
}, 1000);

// Affiche (chaque seconde) :
// Compteur : 1
// Compteur : 2
// Compteur : 3
// Terminé !
```

### Événements (aperçu)

```javascript
// Dans le navigateur
const bouton = document.querySelector("button");

bouton.addEventListener("click", () => {
  console.log("Bouton cliqué !");
});

// Le callback est exécuté chaque fois que le bouton est cliqué
```

## Callbacks avec paramètres

Un callback peut recevoir des paramètres de la fonction qui l'appelle.

### Exemple simple

```javascript
function saluer(nom, callback) {
  const message = "Bonjour " + nom;
  callback(message);  // Passe le message au callback
}

saluer("Alice", (msg) => {
  console.log(msg);  // "Bonjour Alice"
});
```

### Exemple avec plusieurs paramètres

```javascript
function calculer(a, b, callback) {
  const somme = a + b;
  const produit = a * b;
  callback(somme, produit);  // Passe deux résultats
}

calculer(5, 3, (somme, produit) => {
  console.log("Somme :", somme);      // 8
  console.log("Produit :", produit);  // 15
});
```

### Pattern erreur en premier (Node.js)

Conventionnellement en Node.js, le premier paramètre est l'erreur :

```javascript
function lireFichier(nomFichier, callback) {
  // Simule une lecture de fichier
  const erreur = null;
  const contenu = "Contenu du fichier";

  callback(erreur, contenu);
}

lireFichier("data.txt", (err, data) => {
  if (err) {
    console.error("Erreur :", err);
    return;
  }

  console.log("Données :", data);
});
```

## Exemples pratiques complets

### Exemple 1 : Traitement de données avec callback

```javascript
function traiterDonnees(donnees, transformateur, afficheur) {
  console.log("Données originales :", donnees);

  const resultat = transformateur(donnees);

  afficheur(resultat);
}

const nombres = [1, 2, 3, 4, 5];

traiterDonnees(
  nombres,
  arr => arr.map(n => n * 2),        // Transformateur : double les valeurs
  result => console.log("Résultat :", result)  // Afficheur
);

// Données originales : [1, 2, 3, 4, 5]
// Résultat : [2, 4, 6, 8, 10]
```

### Exemple 2 : Système de notification

```javascript
function envoyerNotification(message, onSuccess, onError) {
  console.log("Envoi de :", message);

  // Simule un envoi
  const reussi = Math.random() > 0.3;  // 70% de chance de réussite

  setTimeout(() => {
    if (reussi) {
      onSuccess("Notification envoyée avec succès");
    } else {
      onError("Échec de l'envoi");
    }
  }, 1000);
}

envoyerNotification(
  "Bonjour !",
  (message) => console.log("✅", message),
  (erreur) => console.log("❌", erreur)
);
```

### Exemple 3 : Filtre personnalisé

```javascript
function filtrer(tableau, condition) {
  const resultat = [];

  for (let element of tableau) {
    if (condition(element)) {
      resultat.push(element);
    }
  }

  return resultat;
}

const produits = [
  { nom: "Laptop", prix: 1000 },
  { nom: "Souris", prix: 20 },
  { nom: "Clavier", prix: 50 },
  { nom: "Écran", prix: 300 }
];

// Produits à moins de 100€
const abordables = filtrer(produits, p => p.prix < 100);
console.log(abordables);
// [{ nom: "Souris", prix: 20 }, { nom: "Clavier", prix: 50 }]

// Produits dont le nom commence par "C"
const commencantParC = filtrer(produits, p => p.nom.startsWith("C"));
console.log(commencantParC);
// [{ nom: "Clavier", prix: 50 }]
```

### Exemple 4 : Animation avec callback

```javascript
function animer(element, duree, onComplete) {
  console.log("Animation de", element, "pendant", duree, "ms");

  setTimeout(() => {
    console.log("Animation terminée");
    onComplete();
  }, duree);
}

animer("boîte", 1000, () => {
  console.log("Callback : afficher le message de fin");
});

// Animation de boîte pendant 1000 ms
// (1 seconde d'attente)
// Animation terminée
// Callback : afficher le message de fin
```

### Exemple 5 : Validation de formulaire

```javascript
function validerChamp(valeur, validateurs, onSuccess, onError) {
  for (let validateur of validateurs) {
    const erreur = validateur(valeur);
    if (erreur) {
      onError(erreur);
      return;
    }
  }

  onSuccess("Validation réussie");
}

const email = "alice@example.com";

const validateurs = [
  (val) => val.length === 0 ? "Le champ est vide" : null,
  (val) => !val.includes("@") ? "Email invalide" : null,
  (val) => val.length < 5 ? "Email trop court" : null
];

validerChamp(
  email,
  validateurs,
  (msg) => console.log("✅", msg),
  (err) => console.log("❌", err)
);
```

### Exemple 6 : Tri personnalisé

```javascript
function trierTableau(tableau, comparateur) {
  return tableau.sort(comparateur);
}

const personnes = [
  { nom: "Charlie", age: 30 },
  { nom: "Alice", age: 25 },
  { nom: "Bob", age: 35 }
];

// Trier par âge croissant
const parAge = trierTableau([...personnes], (a, b) => a.age - b.age);
console.log(parAge);

// Trier par nom alphabétique
const parNom = trierTableau([...personnes], (a, b) => {
  return a.nom.localeCompare(b.nom);
});
console.log(parNom);
```

## Callbacks nommés vs anonymes

### Callback anonyme (inline)

```javascript
setTimeout(() => {
  console.log("Hello");
}, 1000);
```

**Avantages :**
- ✅ Concis
- ✅ Code visible au point d'utilisation

**Inconvénients :**
- ❌ Difficile à réutiliser
- ❌ Difficile à tester
- ❌ Peut devenir illisible si complexe

### Callback nommé (fonction séparée)

```javascript
function afficherHello() {
  console.log("Hello");
}

setTimeout(afficherHello, 1000);
```

**Avantages :**
- ✅ Réutilisable
- ✅ Facile à tester
- ✅ Nom descriptif
- ✅ Plus lisible si complexe

**Inconvénients :**
- ❌ Plus verbeux pour des opérations simples

### Quand utiliser quoi ?

```javascript
// ✅ Anonyme : opération simple et unique
nombres.map(n => n * 2);

// ✅ Nommé : logique complexe ou réutilisable
function validerEmail(email) {
  return email.includes("@") && email.includes(".");
}

emails.filter(validerEmail);
```

## Retourner des valeurs depuis les callbacks

Les callbacks peuvent retourner des valeurs qui seront utilisées par la fonction principale.

### Exemple avec map

```javascript
const nombres = [1, 2, 3, 4, 5];

const carres = nombres.map(n => {
  return n * n;  // La valeur retournée est ajoutée au nouveau tableau
});

console.log(carres);  // [1, 4, 9, 16, 25]
```

### Exemple avec reduce

```javascript
const nombres = [1, 2, 3, 4, 5];

const somme = nombres.reduce((acc, n) => {
  return acc + n;  // Retourne l'accumulateur mis à jour
}, 0);

console.log(somme);  // 15
```

### Exemple personnalisé

```javascript
function transformer(valeur, transformateurs) {
  let resultat = valeur;

  for (let transformateur of transformateurs) {
    resultat = transformateur(resultat);  // Utilise la valeur retournée
  }

  return resultat;
}

const doubler = x => x * 2;
const ajouter10 = x => x + 10;
const carre = x => x * x;

console.log(transformer(5, [doubler, ajouter10, carre]));
// ((5 * 2) + 10)² = 400
```

## Callbacks et portée (scope)

Les callbacks ont accès aux variables de leur portée (closure).

### Exemple de closure avec callback

```javascript
function creerCompteur() {
  let compte = 0;  // Variable privée

  return function() {
    compte++;  // Le callback accède à compte
    console.log("Compte :", compte);
  };
}

const compteur = creerCompteur();

compteur();  // Compte : 1
compteur();  // Compte : 2
compteur();  // Compte : 3
```

### Utilisation pratique

```javascript
function genererValidateur(min, max) {
  // min et max sont capturés par le callback
  return function(valeur) {
    return valeur >= min && valeur <= max;
  };
}

const validerAge = genererValidateur(0, 120);
const validerNote = genererValidateur(0, 20);

console.log(validerAge(25));   // true
console.log(validerAge(150));  // false
console.log(validerNote(15));  // true
console.log(validerNote(25));  // false
```

## Chaînage de callbacks

Vous pouvez enchaîner plusieurs callbacks (attention à la lisibilité !) :

```javascript
function etape1(callback) {
  console.log("Étape 1");
  setTimeout(() => callback("Résultat 1"), 1000);
}

function etape2(donnees, callback) {
  console.log("Étape 2, données :", donnees);
  setTimeout(() => callback("Résultat 2"), 1000);
}

function etape3(donnees, callback) {
  console.log("Étape 3, données :", donnees);
  setTimeout(() => callback("Résultat final"), 1000);
}

// Chaînage
etape1((res1) => {
  etape2(res1, (res2) => {
    etape3(res2, (resultatFinal) => {
      console.log("Terminé :", resultatFinal);
    });
  });
});
```

**Note :** Ce type de chaînage peut devenir difficile à lire ("callback hell"). Les Promises et async/await (que vous verrez plus tard) résolvent ce problème.

## Bonnes pratiques

### 1. Nommez vos callbacks de manière descriptive

```javascript
// ❌ Nom vague
bouton.addEventListener("click", function(e) { });

// ✅ Nom descriptif
bouton.addEventListener("click", function gererClicBouton(e) {
  // ...
});

// Ou avec arrow function + variable nommée
const gererClicBouton = (e) => {
  // ...
};
bouton.addEventListener("click", gererClicBouton);
```

### 2. Gardez les callbacks simples

```javascript
// ❌ Callback trop complexe
nombres.map(n => {
  const double = n * 2;
  const carre = double * double;
  const result = carre + 10;
  return result > 100 ? result : 0;
});

// ✅ Extraire la logique dans une fonction séparée
function transformer(n) {
  const double = n * 2;
  const carre = double * double;
  const result = carre + 10;
  return result > 100 ? result : 0;
}

nombres.map(transformer);
```

### 3. Gérez les erreurs

```javascript
function chargerDonnees(url, onSuccess, onError) {
  // Toujours prévoir un callback d'erreur
  fetch(url)
    .then(response => response.json())
    .then(onSuccess)
    .catch(onError);
}

chargerDonnees(
  "https://api.example.com/data",
  (data) => console.log("Données :", data),
  (error) => console.error("Erreur :", error)
);
```

### 4. Documentez vos callbacks

```javascript
/**
 * Applique une opération sur deux nombres
 * @param {number} a - Premier nombre
 * @param {number} b - Deuxième nombre
 * @param {Function} operation - Callback qui prend deux nombres et retourne un résultat
 * @returns {number} Le résultat de l'opération
 */
function appliquer(a, b, operation) {
  return operation(a, b);
}
```

### 5. Évitez les callbacks trop imbriqués

```javascript
// ❌ Difficile à lire
fonction1(param1, (res1) => {
  fonction2(res1, (res2) => {
    fonction3(res2, (res3) => {
      fonction4(res3, (res4) => {
        console.log(res4);
      });
    });
  });
});

// ✅ Mieux : décomposer
function traiterRes1(res1) {
  fonction2(res1, traiterRes2);
}

function traiterRes2(res2) {
  fonction3(res2, traiterRes3);
}

// Ou mieux : utiliser Promises/async-await (section 5.11)
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Appeler le callback au lieu de le passer

```javascript
// ❌ Mauvais : on appelle la fonction
setTimeout(direBonjour(), 1000);  // Exécute immédiatement !

// ✅ Bon : on passe la fonction
setTimeout(direBonjour, 1000);
```

### ❌ Erreur 2 : Oublier de retourner dans un callback

```javascript
// ❌ Mauvais : pas de return
const doubles = [1, 2, 3].map(n => {
  n * 2;  // Oups, pas de return !
});
console.log(doubles);  // [undefined, undefined, undefined]

// ✅ Bon
const doubles = [1, 2, 3].map(n => {
  return n * 2;
});

// ✅ Ou avec return implicite
const doubles = [1, 2, 3].map(n => n * 2);
```

### ❌ Erreur 3 : Ne pas gérer les erreurs

```javascript
// ❌ Pas de gestion d'erreur
function charger(callback) {
  // Si ça échoue, le callback ne sera jamais appelé
  donneesDangereuses.load(callback);
}

// ✅ Avec gestion d'erreur
function charger(onSuccess, onError) {
  try {
    donneesDangereuses.load(onSuccess);
  } catch (error) {
    onError(error);
  }
}
```

### ❌ Erreur 4 : Modifier l'objet original sans le vouloir

```javascript
const original = [1, 2, 3];

// ❌ forEach modifie le comportement externe
original.forEach((n, i, arr) => {
  arr[i] = n * 2;  // Modifie le tableau original !
});

console.log(original);  // [2, 4, 6] - Modifié !

// ✅ Utiliser map pour créer un nouveau tableau
const original = [1, 2, 3];
const double = original.map(n => n * 2);
console.log(original);  // [1, 2, 3] - Inchangé
console.log(double);    // [2, 4, 6] - Nouveau
```

## Points clés à retenir

1. **Callback** = fonction passée en argument à une autre fonction

2. **Passer sans parenthèses** : `fonction(callback)` et non `fonction(callback())`

3. **Deux types** :
   - Synchrones : exécutés immédiatement
   - Asynchrones : exécutés plus tard

4. **Omniprésents** : méthodes de tableau, événements, timers, APIs

5. **Flexibilité** : permettent de personnaliser le comportement

6. **Closures** : les callbacks ont accès aux variables de leur portée

7. **Nommage** : fonctions nommées pour la complexité, anonymes pour la simplicité

8. **Attention** : callbacks imbriqués peuvent devenir difficiles à lire

## Prochaines étapes

Maintenant que vous maîtrisez les callbacks, vous êtes prêt pour :

- Les **méthodes de tableau modernes** (Section 5.8) - map, filter, reduce en détail
- La **programmation asynchrone** (Section 5.11) - Promises et async/await
- Le **callback hell** (5.11.3) - problème et solutions
- Les **closures** (5.13.1) - comprendre la capture de portée

Les callbacks sont un concept fondamental en JavaScript. Ils sont la base de la programmation asynchrone et sont utilisés partout dans l'écosystème JavaScript. Prenez le temps de bien les maîtriser !

---

**Note :** Les callbacks sont au cœur de JavaScript et de sa nature asynchrone. Bien qu'ils puissent sembler déroutants au début, ils deviennent naturels avec la pratique. Dans le JavaScript moderne, les Promises et async/await (que vous verrez dans la section 5.11) offrent une syntaxe plus claire pour gérer l'asynchrone, mais ils sont construits sur le concept de callbacks. Comprendre les callbacks est donc essentiel pour maîtriser JavaScript.

⏭️ [Objets modernes](/05-javascript-moderne-fondamentaux/07-objets-modernes/README.md)
