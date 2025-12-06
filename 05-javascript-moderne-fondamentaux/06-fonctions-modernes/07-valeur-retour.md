🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.7 - Valeur de retour (return)

## Introduction

Le mot-clé **`return`** est l'un des concepts les plus importants des fonctions en JavaScript. Il permet à une fonction de **renvoyer** une valeur à l'endroit où elle a été appelée, permettant ainsi d'utiliser le résultat du calcul ou du traitement effectué par la fonction.

Comprendre `return` est essentiel pour écrire des fonctions utiles et réutilisables.

## Qu'est-ce que `return` ?

Le mot-clé `return` fait **deux choses** :

1. **Renvoie une valeur** à l'endroit où la fonction a été appelée
2. **Termine immédiatement** l'exécution de la fonction

### Syntaxe

```javascript
function nomFonction() {
  // Code...
  return valeur;  // Renvoie la valeur et termine la fonction
}
```

## Premier exemple simple

```javascript
function additionner(a, b) {
  return a + b;
}

const resultat = additionner(5, 3);
console.log(resultat);  // Affiche : 8
```

**Ce qui se passe :**
1. La fonction `additionner` calcule `5 + 3`
2. Le `return` renvoie le résultat `8`
3. Cette valeur est stockée dans la variable `resultat`
4. On peut ensuite utiliser `resultat` ailleurs dans le code

## Return vs console.log : différence cruciale

C'est une source de confusion fréquente pour les débutants !

### console.log : AFFICHER

`console.log` affiche quelque chose dans la console, mais **ne renvoie rien** d'utilisable.

```javascript
function afficherSomme(a, b) {
  console.log(a + b);
  // Pas de return !
}

const resultat = afficherSomme(5, 3);  // Affiche : 8 dans la console
console.log(resultat);                 // Affiche : undefined
console.log(resultat * 2);             // NaN (on ne peut pas utiliser undefined)
```

### return : RENVOYER

`return` renvoie une valeur **utilisable** dans le code.

```javascript
function calculerSomme(a, b) {
  return a + b;
  // Pas de console.log !
}

const resultat = calculerSomme(5, 3);  // Rien ne s'affiche dans la console
console.log(resultat);                 // Affiche : 8
console.log(resultat * 2);             // Affiche : 16 (on peut utiliser la valeur)
```

### Comparaison côte à côte

```javascript
// ❌ Mauvais : utilise console.log au lieu de return
function calculer(x) {
  console.log(x * 2);
}

const a = calculer(5);        // Affiche : 10
const b = a + 10;             // b = undefined + 10 = NaN
console.log(b);               // NaN ❌

// ✅ Bon : utilise return
function calculer(x) {
  return x * 2;
}

const a = calculer(5);        // Ne affiche rien
const b = a + 10;             // b = 10 + 10 = 20
console.log(b);               // 20 ✅
```

**Règle d'or :** Utilisez `return` pour renvoyer des valeurs, `console.log` uniquement pour le débogage.

## Return termine l'exécution

Le code **après** un `return` n'est **jamais exécuté** (on parle de "code mort" ou *dead code*).

```javascript
function exemple() {
  console.log("Ceci s'exécute");
  return 42;
  console.log("Ceci ne s'exécute JAMAIS");  // ← Code mort !
  return 100;  // Jamais atteint
}

const resultat = exemple();
// Affiche seulement : "Ceci s'exécute"
console.log(resultat);  // Affiche : 42
```

### Utilisation pratique : sortir d'une fonction

Vous pouvez utiliser `return` pour sortir d'une fonction plus tôt :

```javascript
function verifierAge(age) {
  if (age < 0) {
    console.log("Âge invalide");
    return;  // Sort de la fonction immédiatement
  }

  if (age < 18) {
    return "Mineur";
  }

  return "Majeur";
}

console.log(verifierAge(-5));   // Affiche "Âge invalide", retourne undefined
console.log(verifierAge(15));   // "Mineur"
console.log(verifierAge(25));   // "Majeur"
```

## Return sans valeur

Si vous utilisez `return` sans valeur, la fonction retourne `undefined` :

```javascript
function direBonjour(nom) {
  if (nom === undefined) {
    return;  // Return sans valeur = return undefined
  }

  console.log("Bonjour " + nom);
}

const resultat1 = direBonjour("Alice");
// Affiche : "Bonjour Alice"
console.log(resultat1);  // undefined

const resultat2 = direBonjour();
// N'affiche rien
console.log(resultat2);  // undefined
```

### Fonction sans return = undefined

Une fonction qui n'a **aucun** `return` retourne automatiquement `undefined` :

```javascript
function afficher(message) {
  console.log(message);
  // Pas de return
}

const resultat = afficher("Hello");
console.log(resultat);  // undefined
```

## Types de valeurs retournées

Une fonction peut retourner **n'importe quel type** de valeur JavaScript.

### Nombres

```javascript
const calculer = (x) => x * 2;
console.log(calculer(5));  // 10
```

### Strings

```javascript
const saluer = (nom) => "Bonjour " + nom;
console.log(saluer("Alice"));  // "Bonjour Alice"
```

### Booléens

```javascript
const estPair = (n) => n % 2 === 0;
console.log(estPair(4));   // true
console.log(estPair(7));   // false
```

### Tableaux

```javascript
const creerTableau = (a, b, c) => [a, b, c];
const nombres = creerTableau(1, 2, 3);
console.log(nombres);  // [1, 2, 3]
```

### Objets

```javascript
const creerPersonne = (nom, age) => {
  return {
    nom: nom,
    age: age,
    majeur: age >= 18
  };
};

const alice = creerPersonne("Alice", 25);
console.log(alice);
// { nom: "Alice", age: 25, majeur: true }
```

Ou avec la syntaxe raccourcie :

```javascript
const creerPersonne = (nom, age) => ({
  nom,
  age,
  majeur: age >= 18
});
```

### Fonctions

Une fonction peut même retourner une autre fonction !

```javascript
function creerMultiplicateur(facteur) {
  return function(nombre) {
    return nombre * facteur;
  };
}

const doubler = creerMultiplicateur(2);
const tripler = creerMultiplicateur(3);

console.log(doubler(5));   // 10
console.log(tripler(5));   // 15
```

## Multiples returns dans une fonction

Une fonction peut avoir **plusieurs instructions** `return` (mais un seul sera exécuté) :

```javascript
function categoriserAge(age) {
  if (age < 0) {
    return "Âge invalide";
  }

  if (age < 13) {
    return "Enfant";
  }

  if (age < 18) {
    return "Adolescent";
  }

  if (age < 60) {
    return "Adulte";
  }

  return "Senior";
}

console.log(categoriserAge(10));   // "Enfant"
console.log(categoriserAge(15));   // "Adolescent"
console.log(categoriserAge(30));   // "Adulte"
console.log(categoriserAge(70));   // "Senior"
```

**Important :** Dès qu'un `return` est exécuté, la fonction se termine. Les autres `return` ne seront pas atteints.

## Pattern "Early Return" (retour anticipé)

C'est une bonne pratique de gérer les cas spéciaux **en premier** avec des returns anticipés :

### Sans early return (moins lisible)

```javascript
function calculerRemise(prix, estMembre) {
  let prixFinal;

  if (prix > 0) {
    if (estMembre) {
      prixFinal = prix * 0.9;  // 10% de réduction
    } else {
      prixFinal = prix;
    }
  } else {
    prixFinal = 0;
  }

  return prixFinal;
}
```

### Avec early return (plus lisible) ✅

```javascript
function calculerRemise(prix, estMembre) {
  // Gérer les cas invalides en premier
  if (prix <= 0) {
    return 0;
  }

  // Cas normal
  if (estMembre) {
    return prix * 0.9;  // 10% de réduction
  }

  return prix;
}
```

**Avantages :**
- Plus lisible et moins d'imbrication
- Les cas spéciaux sont immédiatement visibles
- Moins de variables temporaires

### Autre exemple : validation

```javascript
function diviser(a, b) {
  // Valider les entrées en premier
  if (typeof a !== "number" || typeof b !== "number") {
    return "Erreur : arguments doivent être des nombres";
  }

  if (b === 0) {
    return "Erreur : division par zéro impossible";
  }

  // Cas normal
  return a / b;
}

console.log(diviser(10, 2));      // 5
console.log(diviser(10, 0));      // "Erreur : division par zéro impossible"
console.log(diviser(10, "a"));    // "Erreur : arguments doivent être des nombres"
```

## Return dans les boucles

Vous pouvez utiliser `return` dans une boucle pour sortir de la fonction :

```javascript
function trouverPremierPair(nombres) {
  for (let i = 0; i < nombres.length; i++) {
    if (nombres[i] % 2 === 0) {
      return nombres[i];  // Trouve le premier pair et sort immédiatement
    }
  }

  return null;  // Aucun nombre pair trouvé
}

console.log(trouverPremierPair([1, 3, 5, 8, 9, 10]));  // 8
console.log(trouverPremierPair([1, 3, 5, 7]));         // null
```

**Note :** `return` termine la fonction ET la boucle. Si vous voulez seulement sortir de la boucle, utilisez `break`.

## Exemples pratiques complets

### Exemple 1 : Calculateur d'IMC

```javascript
function calculerIMC(poids, taille) {
  // Validation
  if (poids <= 0 || taille <= 0) {
    return "Erreur : valeurs invalides";
  }

  // Calcul
  const imc = poids / (taille * taille);

  // Arrondir à 2 décimales
  return Math.round(imc * 100) / 100;
}

console.log(calculerIMC(70, 1.75));   // 22.86
console.log(calculerIMC(-70, 1.75));  // "Erreur : valeurs invalides"
```

### Exemple 2 : Vérificateur de mot de passe

```javascript
function verifierMotDePasse(mdp) {
  // Vérifications avec early returns
  if (mdp.length < 8) {
    return {
      valide: false,
      message: "Le mot de passe doit contenir au moins 8 caractères"
    };
  }

  if (!/[A-Z]/.test(mdp)) {
    return {
      valide: false,
      message: "Le mot de passe doit contenir au moins une majuscule"
    };
  }

  if (!/[0-9]/.test(mdp)) {
    return {
      valide: false,
      message: "Le mot de passe doit contenir au moins un chiffre"
    };
  }

  // Tout est ok
  return {
    valide: true,
    message: "Mot de passe valide"
  };
}

console.log(verifierMotDePasse("abc"));
// { valide: false, message: "Le mot de passe doit contenir au moins 8 caractères" }

console.log(verifierMotDePasse("abcdefgh"));
// { valide: false, message: "Le mot de passe doit contenir au moins une majuscule" }

console.log(verifierMotDePasse("Abcdefgh"));
// { valide: false, message: "Le mot de passe doit contenir au moins un chiffre" }

console.log(verifierMotDePasse("Abcdefgh1"));
// { valide: true, message: "Mot de passe valide" }
```

### Exemple 3 : Convertisseur de notes

```javascript
function noteEnLettre(note) {
  if (note < 0 || note > 20) {
    return "Note invalide";
  }

  if (note >= 16) return "A";
  if (note >= 14) return "B";
  if (note >= 12) return "C";
  if (note >= 10) return "D";
  return "E";
}

console.log(noteEnLettre(18));   // "A"
console.log(noteEnLettre(13));   // "C"
console.log(noteEnLettre(8));    // "E"
console.log(noteEnLettre(-5));   // "Note invalide"
```

### Exemple 4 : Formateur de prix

```javascript
function formaterPrix(prix, devise = "EUR") {
  if (typeof prix !== "number") {
    return "Erreur : prix doit être un nombre";
  }

  const prixFormate = prix.toFixed(2);

  switch (devise) {
    case "EUR":
      return prixFormate + " €";
    case "USD":
      return "$" + prixFormate;
    case "GBP":
      return "£" + prixFormate;
    default:
      return prixFormate + " " + devise;
  }
}

console.log(formaterPrix(19.99));            // "19.99 €"
console.log(formaterPrix(29.5, "USD"));      // "$29.50"
console.log(formaterPrix(39.99, "GBP"));     // "£39.99"
console.log(formaterPrix("abc"));            // "Erreur : prix doit être un nombre"
```

### Exemple 5 : Recherche dans un tableau

```javascript
function trouverUtilisateur(users, id) {
  for (let user of users) {
    if (user.id === id) {
      return user;  // Utilisateur trouvé, retourne immédiatement
    }
  }

  // Si on arrive ici, l'utilisateur n'a pas été trouvé
  return null;
}

const utilisateurs = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" },
  { id: 3, nom: "Charlie" }
];

console.log(trouverUtilisateur(utilisateurs, 2));
// { id: 2, nom: "Bob" }

console.log(trouverUtilisateur(utilisateurs, 99));
// null
```

### Exemple 6 : Calculateur de réduction

```javascript
function calculerPrixFinal(prixInitial, codePromo) {
  // Validation
  if (prixInitial <= 0) {
    return { erreur: "Prix invalide" };
  }

  // Codes promo
  const promos = {
    "NOEL25": 0.25,
    "ETE15": 0.15,
    "NOUVEAU10": 0.10
  };

  // Vérifier le code promo
  const reduction = promos[codePromo] || 0;

  // Calcul
  const montantReduction = prixInitial * reduction;
  const prixFinal = prixInitial - montantReduction;

  return {
    prixInitial: prixInitial,
    reduction: reduction * 100 + "%",
    montantReduction: montantReduction.toFixed(2),
    prixFinal: prixFinal.toFixed(2)
  };
}

console.log(calculerPrixFinal(100, "NOEL25"));
// {
//   prixInitial: 100,
//   reduction: "25%",
//   montantReduction: "25.00",
//   prixFinal: "75.00"
// }

console.log(calculerPrixFinal(100, "INVALID"));
// {
//   prixInitial: 100,
//   reduction: "0%",
//   montantReduction: "0.00",
//   prixFinal: "100.00"
// }
```

## Return dans les arrow functions

### Avec accolades : return obligatoire

```javascript
const doubler = (x) => {
  return x * 2;
};
```

### Sans accolades : return implicite

```javascript
const doubler = (x) => x * 2;
```

### Attention aux objets littéraux

Pour retourner un objet avec la syntaxe concise, utilisez des parenthèses :

```javascript
// ❌ Ne fonctionne pas
const creer = (nom) => { nom: nom };  // JavaScript pense que {} est un bloc !

// ✅ Correct avec parenthèses
const creer = (nom) => ({ nom: nom });

// ✅ Ou avec accolades et return
const creer = (nom) => {
  return { nom: nom };
};
```

## Chaîner des fonctions (function chaining)

Quand une fonction retourne une valeur, vous pouvez immédiatement appeler une méthode sur cette valeur :

```javascript
function obtenirTexte() {
  return "  Bonjour le monde  ";
}

// Chaîner les méthodes
const resultat = obtenirTexte().trim().toUpperCase();
console.log(resultat);  // "BONJOUR LE MONDE"
```

### Exemple avec vos propres fonctions

```javascript
const additionner = (a, b) => a + b;
const multiplier = (x, facteur) => x * facteur;

const resultat = multiplier(additionner(3, 4), 2);
console.log(resultat);  // (3 + 4) * 2 = 14
```

## Stocker vs utiliser directement

Vous pouvez soit stocker la valeur retournée, soit l'utiliser directement :

### Stocker dans une variable

```javascript
function calculer(x) {
  return x * 2 + 5;
}

const resultat = calculer(10);
console.log(resultat);           // 25
console.log(resultat + 10);      // 35
```

### Utiliser directement

```javascript
function calculer(x) {
  return x * 2 + 5;
}

console.log(calculer(10));       // 25
console.log(calculer(10) + 10);  // 35

if (calculer(10) > 20) {
  console.log("Plus grand que 20");
}
```

## Bonnes pratiques

### 1. Une fonction devrait avoir un seul type de retour

```javascript
// ❌ Mauvais : retourne différents types
function exemple(x) {
  if (x > 0) {
    return "positif";  // String
  }
  return 0;  // Number
}

// ✅ Bon : retourne toujours le même type
function exemple(x) {
  if (x > 0) {
    return "positif";
  }
  return "non-positif";  // Toujours string
}
```

### 2. Être cohérent avec les valeurs de retour d'erreur

```javascript
// ✅ Bon : cohérent
function trouver(id) {
  // ... recherche ...
  if (trouve) {
    return objet;
  }
  return null;  // Toujours retourner null si non trouvé
}

// ✅ Bon : autre approche cohérente
function trouver(id) {
  // ... recherche ...
  return {
    trouve: true/false,
    data: objet ou null
  };
}
```

### 3. Documenter ce qui est retourné

```javascript
/**
 * Calcule l'aire d'un rectangle
 * @param {number} longueur - Longueur du rectangle
 * @param {number} largeur - Largeur du rectangle
 * @returns {number} L'aire du rectangle
 */
function calculerAire(longueur, largeur) {
  return longueur * largeur;
}
```

### 4. Éviter les fonctions trop longues

```javascript
// ❌ Mauvais : fonction trop longue avec trop de logique
function traiterDonnees(data) {
  // 50 lignes de code...
  return resultat;
}

// ✅ Bon : décomposer en petites fonctions
function valider(data) {
  // ...
  return valide;
}

function transformer(data) {
  // ...
  return transforme;
}

function traiterDonnees(data) {
  if (!valider(data)) {
    return null;
  }
  return transformer(data);
}
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier le return

```javascript
// ❌ Oubli du return
function doubler(x) {
  x * 2;  // Pas de return !
}

const resultat = doubler(5);
console.log(resultat);  // undefined

// ✅ Correct
function doubler(x) {
  return x * 2;
}
```

### ❌ Erreur 2 : Code après return

```javascript
// ❌ Code mort après return
function calculer(x) {
  return x * 2;
  console.log("Ceci ne s'exécute jamais");  // Dead code
  return x * 3;  // Jamais atteint
}
```

### ❌ Erreur 3 : Confondre return et console.log

```javascript
// ❌ Utilise console.log au lieu de return
function additionner(a, b) {
  console.log(a + b);
}

const resultat = additionner(5, 3);  // Affiche 8
const double = resultat * 2;         // NaN !

// ✅ Correct
function additionner(a, b) {
  return a + b;
}
```

### ❌ Erreur 4 : Return avec accolades dans arrow function concise

```javascript
// ❌ Erreur : accolades mais pas de return
const doubler = (x) => {
  x * 2;  // Retourne undefined !
};

// ✅ Correct : avec return
const doubler = (x) => {
  return x * 2;
};

// ✅ Correct : sans accolades (return implicite)
const doubler = (x) => x * 2;
```

## Points clés à retenir

1. **`return` fait deux choses** : renvoie une valeur ET termine la fonction

2. **Return ≠ console.log** :
   - `return` = renvoyer une valeur utilisable
   - `console.log` = afficher pour le débogage

3. **Code après return** : jamais exécuté (dead code)

4. **Sans return** : la fonction retourne `undefined`

5. **Multiples returns** : possibles, mais un seul sera exécuté

6. **Early return** : bonne pratique pour gérer les cas spéciaux en premier

7. **Type de retour** : peut être n'importe quel type JavaScript

8. **Arrow functions** : return implicite sans accolades

## Prochaines étapes

Maintenant que vous maîtrisez `return`, vous êtes prêt pour :

- La **portée et le scope** (5.6.8) - où les variables sont accessibles
- Le **hoisting** (5.6.9) - comment JavaScript "remonte" les déclarations
- Les **callbacks** (5.6.10) - passer des fonctions qui retournent des valeurs

Le mot-clé `return` est fondamental en programmation. C'est ce qui rend les fonctions réellement utiles en permettant de récupérer et réutiliser les résultats de leurs calculs !

---

**Note :** Comprendre la différence entre `return` et `console.log` est crucial pour les débutants. `console.log` est un outil de débogage, tandis que `return` est la façon dont les fonctions communiquent leurs résultats au reste du programme. Utilisez toujours `return` pour renvoyer des valeurs que vous voulez utiliser dans votre code.

⏭️ [Portée : scope de bloc (let/const) vs scope de fonction](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/08-portee-scope.md)
