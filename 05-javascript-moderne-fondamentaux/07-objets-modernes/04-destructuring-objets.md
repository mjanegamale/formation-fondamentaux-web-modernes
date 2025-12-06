🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.4 - Destructuring d'objets 🆕

## Introduction

Le **destructuring** (ou déstructuration en français) est une fonctionnalité ES6 qui permet d'**extraire** des propriétés d'un objet et de les assigner directement à des variables, en une seule ligne de code.

C'est l'une des fonctionnalités les plus pratiques et les plus utilisées du JavaScript moderne. Elle rend le code plus court, plus lisible et plus élégant.

### Le problème avant ES6

Avant ES6, pour extraire des propriétés d'un objet, il fallait créer une variable pour chaque propriété :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com"
};

// ❌ Approche ancienne : répétitif et verbeux
const nom = utilisateur.nom;
const age = utilisateur.age;
const email = utilisateur.email;

console.log(nom);    // "Alice"
console.log(age);    // 28
console.log(email);  // "alice@example.com"
```

### La solution ES6 : Destructuring

Avec le destructuring, on peut faire la même chose en **une seule ligne** :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com"
};

// ✅ Destructuring ES6 : concis et élégant
const { nom, age, email } = utilisateur;

console.log(nom);    // "Alice"
console.log(age);    // 28
console.log(email);  // "alice@example.com"
```

**Magie !** En une ligne, on a créé trois variables qui contiennent les valeurs des propriétés correspondantes.

## 1. Syntaxe de base

### Structure générale

```javascript
const { propriete1, propriete2, propriete3 } = objet;
```

Les accolades `{}` à gauche du `=` indiquent qu'on fait du destructuring.

### Exemple simple

```javascript
const personne = {
  prenom: "Bob",
  age: 32,
  ville: "Lyon"
};

// Extraction de propriétés
const { prenom, ville } = personne;

console.log(prenom);  // "Bob"
console.log(ville);   // "Lyon"
```

**Note :** On n'est pas obligé d'extraire toutes les propriétés. Ici, on n'a pas extrait `age`.

### Comment ça fonctionne ?

JavaScript cherche dans l'objet des propriétés qui ont les **mêmes noms** que les variables entre accolades, et assigne leurs valeurs :

```javascript
const produit = {
  nom: "Ordinateur",
  prix: 899,
  stock: 15
};

// JavaScript fait automatiquement :
// const nom = produit.nom;
// const prix = produit.prix;
const { nom, prix } = produit;

console.log(nom);   // "Ordinateur"
console.log(prix);  // 899
```

## 2. Extraire seulement ce dont on a besoin

On peut choisir de n'extraire que certaines propriétés :

```javascript
const config = {
  theme: "sombre",
  langue: "fr",
  notifications: true,
  volume: 75,
  qualite: "HD"
};

// On extrait seulement theme et langue
const { theme, langue } = config;

console.log(theme);   // "sombre"
console.log(langue);  // "fr"

// Les autres propriétés sont toujours dans config
console.log(config.notifications);  // true
```

## 3. Renommer les variables

Parfois, on veut extraire une propriété mais lui donner un **nom différent** en tant que variable :

### Syntaxe de renommage

```javascript
const { proprieteOriginale: nouveauNom } = objet;
```

### Exemple

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com"
};

// Renommer "nom" en "nomUtilisateur"
const { nom: nomUtilisateur, age: ageUtilisateur } = utilisateur;

console.log(nomUtilisateur);  // "Alice"
console.log(ageUtilisateur);  // 28

// ⚠️ La variable "nom" n'existe pas
// console.log(nom);  // ReferenceError
```

### Cas d'usage pratique

```javascript
const reponseAPI = {
  data: {
    user_name: "bob_martin",    // format snake_case de l'API
    user_email: "bob@example.com",
    user_age: 30
  }
};

// Renommer en camelCase (convention JavaScript)
const {
  user_name: userName,
  user_email: userEmail,
  user_age: userAge
} = reponseAPI.data;

console.log(userName);   // "bob_martin"
console.log(userEmail);  // "bob@example.com"
```

## 4. Valeurs par défaut

Si une propriété n'existe pas dans l'objet, on peut définir une **valeur par défaut** :

### Syntaxe

```javascript
const { propriete = valeurParDefaut } = objet;
```

### Exemple

```javascript
const config = {
  theme: "sombre",
  langue: "fr"
};

// "notifications" n'existe pas, on utilise la valeur par défaut
const { theme, langue, notifications = true } = config;

console.log(theme);          // "sombre"
console.log(langue);         // "fr"
console.log(notifications);  // true (valeur par défaut)
```

### Avec et sans valeur par défaut

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28
};

// Sans valeur par défaut
const { nom, email } = utilisateur;
console.log(email);  // undefined

// Avec valeur par défaut
const { nom: nom2, email: email2 = "non défini" } = utilisateur;
console.log(email2);  // "non défini"
```

### Combiner renommage et valeur par défaut

```javascript
const produit = {
  nom: "Clavier",
  prix: 49.99
};

// Extraire "stock" qui n'existe pas, avec valeur par défaut
const { nom, prix, stock: quantite = 0 } = produit;

console.log(nom);       // "Clavier"
console.log(prix);      // 49.99
console.log(quantite);  // 0
```

## 5. Destructuring d'objets imbriqués

On peut destructurer des objets qui contiennent d'autres objets :

### Exemple simple

```javascript
const utilisateur = {
  nom: "Alice",
  adresse: {
    rue: "10 rue de la Paix",
    ville: "Paris",
    codePostal: "75001"
  }
};

// Destructuring imbriqué
const {
  nom,
  adresse: { ville, codePostal }
} = utilisateur;

console.log(nom);        // "Alice"
console.log(ville);      // "Paris"
console.log(codePostal); // "75001"

// ⚠️ La variable "adresse" n'existe pas
// console.log(adresse);  // ReferenceError
```

**Important :** Quand on fait un destructuring imbriqué, on crée des variables pour les propriétés imbriquées, **pas** pour l'objet parent.

### Si on veut aussi l'objet parent

```javascript
const utilisateur = {
  nom: "Bob",
  adresse: {
    rue: "5 avenue des Champs",
    ville: "Lyon"
  }
};

// Extraire à la fois l'objet adresse ET ses propriétés
const {
  nom,
  adresse,                    // L'objet complet
  adresse: { ville }          // Une propriété de l'objet
} = utilisateur;

console.log(nom);      // "Bob"
console.log(adresse);  // { rue: "5 avenue des Champs", ville: "Lyon" }
console.log(ville);    // "Lyon"
```

### Exemple plus complexe

```javascript
const entreprise = {
  nom: "TechCorp",
  employes: {
    direction: {
      ceo: "Marie Dubois",
      cto: "Jean Martin"
    },
    effectif: 150
  },
  adresse: {
    ville: "Paris",
    pays: "France"
  }
};

// Destructuring profond
const {
  nom: nomEntreprise,
  employes: {
    direction: { ceo },
    effectif
  },
  adresse: { ville }
} = entreprise;

console.log(nomEntreprise);  // "TechCorp"
console.log(ceo);            // "Marie Dubois"
console.log(effectif);       // 150
console.log(ville);          // "Paris"
```

### Avec valeurs par défaut imbriquées

```javascript
const config = {
  app: {
    nom: "MonApp"
    // version manquante
  }
};

const {
  app: {
    nom,
    version = "1.0.0"  // valeur par défaut
  }
} = config;

console.log(nom);      // "MonApp"
console.log(version);  // "1.0.0"
```

## 6. Destructuring dans les paramètres de fonction

C'est l'un des usages les plus courants et les plus pratiques du destructuring.

### Avant ES6

```javascript
// ❌ Approche ancienne
function afficherUtilisateur(utilisateur) {
  console.log("Nom:", utilisateur.nom);
  console.log("Age:", utilisateur.age);
  console.log("Email:", utilisateur.email);
}

const user = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com"
};

afficherUtilisateur(user);
```

### Avec destructuring ES6

```javascript
// ✅ Destructuring directement dans les paramètres
function afficherUtilisateur({ nom, age, email }) {
  console.log("Nom:", nom);
  console.log("Age:", age);
  console.log("Email:", email);
}

const user = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com"
};

afficherUtilisateur(user);
```

**Avantage :** On voit immédiatement quelles propriétés la fonction utilise.

### Avec valeurs par défaut

```javascript
function creerProfil({
  nom,
  age,
  ville = "Non spécifié",
  actif = true
}) {
  return {
    nom,
    age,
    ville,
    actif,
    dateCreation: new Date()
  };
}

const profil1 = creerProfil({
  nom: "Bob",
  age: 30,
  ville: "Paris"
});

const profil2 = creerProfil({
  nom: "Alice",
  age: 25
  // ville et actif utiliseront les valeurs par défaut
});

console.log(profil2);
// {
//   nom: "Alice",
//   age: 25,
//   ville: "Non spécifié",
//   actif: true,
//   dateCreation: ...
// }
```

### Extraire seulement ce dont on a besoin

```javascript
// La fonction ne prend que ce qui l'intéresse
function calculerPrixTotal({ prix, quantite }) {
  return prix * quantite;
}

const produit = {
  id: 101,
  nom: "Clavier",
  prix: 49.99,
  quantite: 3,
  categorie: "Électronique",
  description: "Clavier mécanique RGB"
};

const total = calculerPrixTotal(produit);
console.log(total);  // 149.97
```

### Destructuring imbriqué dans les paramètres

```javascript
function afficherAdresse({
  nom,
  adresse: { ville, codePostal }
}) {
  console.log(`${nom} habite à ${ville} (${codePostal})`);
}

const personne = {
  nom: "Sophie",
  age: 32,
  adresse: {
    rue: "12 rue Victor Hugo",
    ville: "Lyon",
    codePostal: "69001"
  }
};

afficherAdresse(personne);
// "Sophie habite à Lyon (69001)"
```

## 7. Rest dans le destructuring

On peut capturer les propriétés restantes avec l'opérateur `...` (rest) :

### Syntaxe

```javascript
const { prop1, prop2, ...reste } = objet;
```

### Exemple

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com",
  ville: "Paris",
  pays: "France"
};

// Extraire nom et age, mettre le reste dans "autres"
const { nom, age, ...autres } = utilisateur;

console.log(nom);     // "Alice"
console.log(age);     // 28
console.log(autres);
// { email: "alice@example.com", ville: "Paris", pays: "France" }
```

### Cas d'usage : Séparer des propriétés

```javascript
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000,
  retry: 3,
  cache: true,
  debug: false
};

// Séparer les paramètres réseau du reste
const { apiUrl, timeout, ...autresOptions } = config;

console.log("URL:", apiUrl);
console.log("Timeout:", timeout);
console.log("Autres options:", autresOptions);
// { retry: 3, cache: true, debug: false }
```

### Dans les paramètres de fonction

```javascript
function traiterUtilisateur({ id, nom, ...details }) {
  console.log(`Traitement de l'utilisateur ${id}: ${nom}`);
  console.log("Détails supplémentaires:", details);
}

const user = {
  id: 42,
  nom: "Bob",
  email: "bob@example.com",
  age: 30,
  actif: true
};

traiterUtilisateur(user);
// Traitement de l'utilisateur 42: Bob
// Détails supplémentaires: { email: "bob@example.com", age: 30, actif: true }
```

## 8. Exemples pratiques complets

### Exemple 1 : Traitement de données API

```javascript
// Réponse d'une API
const reponseAPI = {
  status: 200,
  data: {
    user: {
      id: 123,
      username: "alice_dev",
      email: "alice@example.com",
      profile: {
        firstName: "Alice",
        lastName: "Martin",
        age: 28
      }
    },
    token: "abc123xyz",
    expiresIn: 3600
  }
};

// Destructuring pour extraire ce qui nous intéresse
const {
  data: {
    user: {
      username,
      profile: { firstName, lastName }
    },
    token
  }
} = reponseAPI;

console.log(`Bienvenue ${firstName} ${lastName} (@${username})`);
console.log(`Token: ${token}`);
```

### Exemple 2 : Configuration d'application

```javascript
function initialiserApp({
  theme = "clair",
  langue = "fr",
  notifications = true,
  autoSave = false,
  ...autresOptions
}) {
  console.log("=== Configuration de l'application ===");
  console.log(`Thème: ${theme}`);
  console.log(`Langue: ${langue}`);
  console.log(`Notifications: ${notifications ? "activées" : "désactivées"}`);
  console.log(`Sauvegarde auto: ${autoSave ? "activée" : "désactivée"}`);

  if (Object.keys(autresOptions).length > 0) {
    console.log("Options supplémentaires:", autresOptions);
  }
}

// Appel avec configuration partielle
initialiserApp({
  theme: "sombre",
  notifications: false,
  qualite: "HD",
  fps: 60
});
```

### Exemple 3 : Gestion de formulaires

```javascript
function validerFormulaire({
  nom,
  email,
  motDePasse,
  confirmerMotDePasse,
  accepterCGU = false
}) {
  const erreurs = [];

  if (!nom || nom.length < 2) {
    erreurs.push("Le nom doit contenir au moins 2 caractères");
  }

  if (!email || !email.includes("@")) {
    erreurs.push("Email invalide");
  }

  if (motDePasse !== confirmerMotDePasse) {
    erreurs.push("Les mots de passe ne correspondent pas");
  }

  if (!accepterCGU) {
    erreurs.push("Vous devez accepter les CGU");
  }

  return {
    valide: erreurs.length === 0,
    erreurs
  };
}

const donnees = {
  nom: "Alice",
  email: "alice@example.com",
  motDePasse: "secret123",
  confirmerMotDePasse: "secret123",
  accepterCGU: true
};

const resultat = validerFormulaire(donnees);
console.log(resultat);
// { valide: true, erreurs: [] }
```

### Exemple 4 : Transformation de données

```javascript
function transformerProduit({
  id,
  name: nom,           // Renommage
  price: prix,
  stock: {
    quantity: quantite,
    warehouse: entrepot = "Principal"
  },
  discount = 0
}) {
  const prixFinal = prix * (1 - discount);

  return {
    id,
    nom,
    prixOriginal: prix,
    prixFinal,
    quantite,
    entrepot,
    disponible: quantite > 0
  };
}

const produitAPI = {
  id: 1001,
  name: "Ordinateur Portable",
  price: 899,
  stock: {
    quantity: 15,
    warehouse: "Entrepôt A"
  },
  discount: 0.1
};

const produitTransforme = transformerProduit(produitAPI);
console.log(produitTransforme);
// {
//   id: 1001,
//   nom: "Ordinateur Portable",
//   prixOriginal: 899,
//   prixFinal: 809.1,
//   quantite: 15,
//   entrepot: "Entrepôt A",
//   disponible: true
// }
```

## 9. Destructuring avec `let` et `const`

Le destructuring fonctionne avec `const` et `let` :

```javascript
const utilisateur = {
  nom: "Alice",
  score: 100
};

// Avec const (ne peut pas être réassigné)
const { nom } = utilisateur;
// nom = "Bob";  // ❌ Erreur

// Avec let (peut être réassigné)
let { score } = utilisateur;
score = 150;  // ✅ OK
console.log(score);  // 150
```

## 10. Pièges à éviter

### Piège 1 : Destructuring sans déclaration

```javascript
const utilisateur = { nom: "Alice", age: 28 };

// ❌ ERREUR : Doit commencer par let, const ou var
// { nom, age } = utilisateur;  // SyntaxError

// ✅ CORRECT
const { nom, age } = utilisateur;

// ✅ OU avec parenthèses pour réassigner des variables existantes
let nom2, age2;
({ nom: nom2, age: age2 } = utilisateur);
```

### Piège 2 : Objet undefined ou null

```javascript
const data = null;

// ❌ ERREUR
// const { nom } = data;  // TypeError: Cannot destructure property 'nom' of 'null'

// ✅ Solution : vérifier d'abord
if (data) {
  const { nom } = data;
}

// ✅ Ou utiliser une valeur par défaut
const { nom } = data || {};
console.log(nom);  // undefined (pas d'erreur)
```

### Piège 3 : Confusion entre destructuring et objet littéral

```javascript
// ❌ Objet littéral
const personne = { nom: "Alice" };

// ✅ Destructuring
const { nom } = personne;

// Les accolades à gauche = destructuring
// Les accolades à droite = objet littéral
```

## 11. Avantages du destructuring

### 1. Code plus court

```javascript
// Avant
const nom = utilisateur.nom;
const age = utilisateur.age;
const email = utilisateur.email;

// Après
const { nom, age, email } = utilisateur;
```

### 2. Code plus lisible

```javascript
// Moins lisible
function afficher(user) {
  return `${user.prenom} ${user.nom} - ${user.ville}`;
}

// Plus lisible
function afficher({ prenom, nom, ville }) {
  return `${prenom} ${nom} - ${ville}`;
}
```

### 3. Évite les répétitions

```javascript
// Répétitif
console.log(config.theme);
console.log(config.langue);
console.log(config.notifications);

// Concis
const { theme, langue, notifications } = config;
console.log(theme);
console.log(langue);
console.log(notifications);
```

### 4. Paramètres de fonction explicites

```javascript
// Pas clair quelles propriétés sont utilisées
function traiter(data) {
  // ...
}

// Clair dès la signature
function traiter({ nom, email, actif }) {
  // ...
}
```

## Points clés à retenir

1. **Destructuring** = extraire des propriétés d'un objet en variables
2. **Syntaxe** : `const { prop1, prop2 } = objet`
3. **Renommage** : `const { ancien: nouveau } = objet`
4. **Valeurs par défaut** : `const { prop = valeur } = objet`
5. **Destructuring imbriqué** : possible mais attention à la lisibilité
6. **Dans les paramètres** : très utile pour les fonctions
7. **Rest operator** : `const { a, b, ...reste } = objet`
8. **Toujours déclarer** avec `const` ou `let`

## Comparaison avant/après ES6

```javascript
const utilisateur = {
  id: 42,
  nom: "Alice",
  email: "alice@example.com",
  preferences: {
    theme: "sombre",
    langue: "fr"
  }
};

// ❌ AVANT ES6 : verbeux
const id = utilisateur.id;
const nom = utilisateur.nom;
const email = utilisateur.email;
const theme = utilisateur.preferences.theme;
const langue = utilisateur.preferences.langue;

// ✅ AVEC ES6 : élégant
const {
  id,
  nom,
  email,
  preferences: { theme, langue }
} = utilisateur;
```

## Ce qui vient ensuite

Maintenant que vous maîtrisez le destructuring d'objets, vous allez découvrir :
- Le spread operator pour copier et fusionner des objets
- Le destructuring de tableaux (similaire mais pour les arrays)
- Les méthodes d'objets et `this`
- Les classes ES6

Le destructuring est une fonctionnalité **essentielle** du JavaScript moderne. Vous la verrez et l'utiliserez constamment dans le code professionnel !

⏭️ [Spread operator (...) pour copier et fusionner](/05-javascript-moderne-fondamentaux/07-objets-modernes/05-spread-operator.md)
