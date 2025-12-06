🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.6 - Ajout et suppression de propriétés

## Introduction

En JavaScript, les objets sont **dynamiques** : on peut ajouter, modifier et supprimer des propriétés à tout moment, même après la création de l'objet. Cette flexibilité est l'une des forces de JavaScript.

Dans cette section, nous allons apprendre à :
1. **Ajouter** de nouvelles propriétés
2. **Modifier** des propriétés existantes
3. **Supprimer** des propriétés
4. **Vérifier** l'existence de propriétés

## 1. Ajouter des propriétés

### Méthode 1 : Notation point

La façon la plus simple et la plus courante d'ajouter une propriété :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28
};

console.log(utilisateur);
// { nom: "Alice", age: 28 }

// Ajout d'une nouvelle propriété
utilisateur.email = "alice@example.com";
utilisateur.ville = "Paris";

console.log(utilisateur);
// {
//   nom: "Alice",
//   age: 28,
//   email: "alice@example.com",
//   ville: "Paris"
// }
```

### Méthode 2 : Notation crochets

Utile pour les noms de propriétés dynamiques ou avec caractères spéciaux :

```javascript
const produit = {
  nom: "Ordinateur",
  prix: 899
};

// Ajout avec notation crochets
produit["stock"] = 15;
produit["en promotion"] = true;

console.log(produit);
// {
//   nom: "Ordinateur",
//   prix: 899,
//   stock: 15,
//   "en promotion": true
// }
```

### Ajout dynamique

Quand le nom de la propriété est dans une variable :

```javascript
const voiture = {
  marque: "Peugeot",
  modele: "308"
};

const nouvellePropriete = "annee";
const valeur = 2023;

// Utiliser la notation crochets avec une variable
voiture[nouvellePropriete] = valeur;

console.log(voiture);
// { marque: "Peugeot", modele: "308", annee: 2023 }
```

### Exemple pratique : Enrichir un objet

```javascript
function enrichirProduit(produit) {
  // Ajouter des propriétés calculées
  produit.id = Math.random().toString(36).substr(2, 9);
  produit.dateAjout = new Date();
  produit.disponible = produit.stock > 0;
  produit.prixTTC = produit.prix * 1.20;

  return produit;
}

const article = {
  nom: "Clavier",
  prix: 49.99,
  stock: 10
};

enrichirProduit(article);

console.log(article);
// {
//   nom: "Clavier",
//   prix: 49.99,
//   stock: 10,
//   id: "kx7j9m2p8",
//   dateAjout: 2024-12-05T...,
//   disponible: true,
//   prixTTC: 59.988
// }
```

## 2. Modifier des propriétés existantes

Modifier une propriété fonctionne exactement comme l'ajout :

### Avec notation point

```javascript
const utilisateur = {
  nom: "Bob",
  age: 30,
  email: "bob@old-email.com"
};

// Modification
utilisateur.age = 31;
utilisateur.email = "bob@new-email.com";

console.log(utilisateur);
// {
//   nom: "Bob",
//   age: 31,
//   email: "bob@new-email.com"
// }
```

### Avec notation crochets

```javascript
const config = {
  theme: "clair",
  langue: "en"
};

const propriete = "theme";
config[propriete] = "sombre";

console.log(config.theme);  // "sombre"
```

### Modifications basées sur l'ancienne valeur

```javascript
const compteur = {
  valeur: 10,
  nom: "Compteur principal"
};

// Incrémenter
compteur.valeur = compteur.valeur + 1;
// ou plus court :
compteur.valeur++;

console.log(compteur.valeur);  // 11

// Doubler la valeur
compteur.valeur *= 2;
console.log(compteur.valeur);  // 22
```

### Exemple : Mise à jour de panier

```javascript
const panier = {
  articles: [],
  total: 0,
  nbArticles: 0
};

function ajouterArticle(panier, article) {
  panier.articles.push(article);
  panier.nbArticles++;
  panier.total += article.prix;
}

ajouterArticle(panier, { nom: "Livre", prix: 15.99 });
ajouterArticle(panier, { nom: "Stylo", prix: 2.50 });

console.log(panier);
// {
//   articles: [
//     { nom: "Livre", prix: 15.99 },
//     { nom: "Stylo", prix: 2.50 }
//   ],
//   total: 18.49,
//   nbArticles: 2
// }
```

## 3. Supprimer des propriétés

### L'opérateur `delete`

Pour supprimer une propriété, on utilise l'opérateur `delete` :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com",
  temporaire: "à supprimer"
};

console.log(utilisateur);
// { nom: "Alice", age: 28, email: "alice@example.com", temporaire: "à supprimer" }

// Suppression avec notation point
delete utilisateur.temporaire;

console.log(utilisateur);
// { nom: "Alice", age: 28, email: "alice@example.com" }

// Suppression avec notation crochets
delete utilisateur["email"];

console.log(utilisateur);
// { nom: "Alice", age: 28 }
```

### `delete` retourne un booléen

```javascript
const objet = {
  prop1: "valeur1",
  prop2: "valeur2"
};

const resultat1 = delete objet.prop1;
console.log(resultat1);  // true (suppression réussie)

const resultat2 = delete objet.propInexistante;
console.log(resultat2);  // true (pas d'erreur même si inexistante)
```

### Supprimer dynamiquement

```javascript
const config = {
  option1: true,
  option2: false,
  option3: true,
  option4: false
};

// Supprimer une propriété dont le nom est dans une variable
const aSuppprimer = "option2";
delete config[aSuppprimer];

console.log(config);
// { option1: true, option3: true, option4: false }
```

### Attention : `delete` vs `undefined`

Il y a une différence entre supprimer et mettre à `undefined` :

```javascript
const personne = {
  nom: "Bob",
  age: 30,
  ville: "Paris"
};

// Mettre à undefined (la propriété existe toujours)
personne.age = undefined;
console.log("age" in personne);  // true (la propriété existe)

// Supprimer (la propriété n'existe plus)
delete personne.ville;
console.log("ville" in personne);  // false (la propriété n'existe pas)

console.log(personne);
// { nom: "Bob", age: undefined }
```

**Recommandation :** Utilisez `delete` pour vraiment supprimer une propriété.

## 4. Vérifier l'existence d'une propriété

Avant d'ajouter ou de modifier, on peut vérifier si une propriété existe :

### Méthode 1 : Opérateur `in`

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  actif: false
};

console.log("nom" in utilisateur);      // true
console.log("email" in utilisateur);    // false
console.log("actif" in utilisateur);    // true (même si false)
```

### Méthode 2 : `hasOwnProperty()`

```javascript
const config = {
  theme: "sombre",
  notifications: true
};

console.log(config.hasOwnProperty("theme"));          // true
console.log(config.hasOwnProperty("langue"));         // false
console.log(config.hasOwnProperty("notifications")); // true
```

### Méthode 3 : Vérification directe

```javascript
const data = {
  valeur: 0,
  texte: ""
};

// ⚠️ Attention : 0 et "" sont falsy
if (data.valeur) {
  console.log("Existe");  // Ne s'exécute pas car 0 est falsy
}

// ✅ Mieux : vérifier avec !== undefined
if (data.valeur !== undefined) {
  console.log("Existe");  // S'exécute correctement
}

// ✅ Ou utiliser "in"
if ("valeur" in data) {
  console.log("Existe");  // S'exécute correctement
}
```

### Exemple : Ajouter seulement si inexistant

```javascript
function ajouterParDefaut(objet, propriete, valeur) {
  if (!(propriete in objet)) {
    objet[propriete] = valeur;
  }
}

const config = {
  theme: "sombre"
};

ajouterParDefaut(config, "theme", "clair");      // N'ajoute pas (existe déjà)
ajouterParDefaut(config, "langue", "fr");        // Ajoute
ajouterParDefaut(config, "notifications", true); // Ajoute

console.log(config);
// { theme: "sombre", langue: "fr", notifications: true }
```

## 5. Approches modernes avec le spread operator

### Ajouter des propriétés (immutable)

Au lieu de modifier l'objet original, on peut créer un nouveau objet avec les propriétés ajoutées :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28
};

// ❌ Modification directe (mutable)
utilisateur.email = "alice@example.com";

// ✅ Création d'un nouvel objet (immutable)
const utilisateurAvecEmail = {
  ...utilisateur,
  email: "alice@example.com",
  ville: "Paris"
};

console.log(utilisateur);
// { nom: "Alice", age: 28 } (inchangé)

console.log(utilisateurAvecEmail);
// { nom: "Alice", age: 28, email: "alice@example.com", ville: "Paris" }
```

### Supprimer des propriétés (immutable)

Avec le destructuring et le rest operator :

```javascript
const utilisateur = {
  id: 123,
  nom: "Bob",
  motDePasse: "secret",
  email: "bob@example.com",
  role: "user"
};

// Extraire motDePasse et garder le reste
const { motDePasse, ...utilisateurPublic } = utilisateur;

console.log(utilisateurPublic);
// {
//   id: 123,
//   nom: "Bob",
//   email: "bob@example.com",
//   role: "user"
// }

// L'original est inchangé
console.log(utilisateur.motDePasse);  // "secret"
```

### Supprimer plusieurs propriétés

```javascript
const produit = {
  id: 101,
  nom: "Ordinateur",
  prix: 899,
  stock: 15,
  _internal: "donnée interne",
  _debug: true
};

// Supprimer les propriétés privées (commençant par _)
const { _internal, _debug, ...produitPublic } = produit;

console.log(produitPublic);
// {
//   id: 101,
//   nom: "Ordinateur",
//   prix: 899,
//   stock: 15
// }
```

### Fonction de suppression générique

```javascript
function supprimerProprietes(objet, ...proprietes) {
  const resultat = { ...objet };

  proprietes.forEach(prop => {
    delete resultat[prop];
  });

  return resultat;
}

const data = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  e: 5
};

const filtre = supprimerProprietes(data, "b", "d");
console.log(filtre);
// { a: 1, c: 3, e: 5 }

console.log(data);
// { a: 1, b: 2, c: 3, d: 4, e: 5 } (inchangé)
```

## 6. Exemples pratiques complets

### Exemple 1 : Gestion de formulaire

```javascript
const formulaire = {
  nom: "",
  prenom: "",
  email: ""
};

function remplirChamp(champ, valeur) {
  formulaire[champ] = valeur;
  console.log(`${champ} mis à jour: ${valeur}`);
}

function ajouterChamp(champ, valeur) {
  if (champ in formulaire) {
    console.log(`Le champ ${champ} existe déjà`);
  } else {
    formulaire[champ] = valeur;
    console.log(`Champ ${champ} ajouté`);
  }
}

function supprimerChamp(champ) {
  if (champ in formulaire) {
    delete formulaire[champ];
    console.log(`Champ ${champ} supprimé`);
  } else {
    console.log(`Le champ ${champ} n'existe pas`);
  }
}

remplirChamp("nom", "Dupont");
remplirChamp("prenom", "Marie");
ajouterChamp("telephone", "0123456789");
supprimerChamp("email");

console.log(formulaire);
// {
//   nom: "Dupont",
//   prenom: "Marie",
//   telephone: "0123456789"
// }
```

### Exemple 2 : Système de cache

```javascript
const cache = {
  data: {},

  ajouter(cle, valeur, duree = 3600) {
    this.data[cle] = {
      valeur: valeur,
      expiration: Date.now() + (duree * 1000)
    };
    console.log(`Cache ajouté: ${cle}`);
  },

  obtenir(cle) {
    const entree = this.data[cle];

    if (!entree) {
      console.log(`Cache manqué: ${cle}`);
      return null;
    }

    // Vérifier l'expiration
    if (Date.now() > entree.expiration) {
      delete this.data[cle];
      console.log(`Cache expiré: ${cle}`);
      return null;
    }

    console.log(`Cache trouvé: ${cle}`);
    return entree.valeur;
  },

  supprimer(cle) {
    if (cle in this.data) {
      delete this.data[cle];
      console.log(`Cache supprimé: ${cle}`);
    }
  },

  vider() {
    this.data = {};
    console.log("Cache vidé");
  }
};

cache.ajouter("utilisateur", { nom: "Alice" }, 10);
cache.ajouter("config", { theme: "sombre" });

console.log(cache.obtenir("utilisateur"));
// { nom: "Alice" }

cache.supprimer("config");
console.log(cache.obtenir("config"));
// null
```

### Exemple 3 : Enrichissement progressif d'objet

```javascript
function creerUtilisateur(donnees) {
  const utilisateur = {
    nom: donnees.nom,
    email: donnees.email
  };

  // Ajouter l'ID
  utilisateur.id = Math.random().toString(36).substr(2, 9);

  // Ajouter la date de création
  utilisateur.dateCreation = new Date();

  // Ajouter le rôle si fourni
  if (donnees.role) {
    utilisateur.role = donnees.role;
  } else {
    utilisateur.role = "user"; // Par défaut
  }

  // Ajouter le statut
  utilisateur.actif = donnees.actif !== undefined ? donnees.actif : true;

  // Ajouter les préférences si fournies
  if (donnees.preferences) {
    utilisateur.preferences = donnees.preferences;
  }

  return utilisateur;
}

const user1 = creerUtilisateur({
  nom: "Alice",
  email: "alice@example.com"
});

const user2 = creerUtilisateur({
  nom: "Bob",
  email: "bob@example.com",
  role: "admin",
  preferences: { theme: "sombre" }
});

console.log(user1);
// {
//   nom: "Alice",
//   email: "alice@example.com",
//   id: "x7k9m2p1s",
//   dateCreation: ...,
//   role: "user",
//   actif: true
// }

console.log(user2);
// {
//   nom: "Bob",
//   email: "bob@example.com",
//   id: "a3j8n5q2w",
//   dateCreation: ...,
//   role: "admin",
//   actif: true,
//   preferences: { theme: "sombre" }
// }
```

### Exemple 4 : Nettoyage de données

```javascript
function nettoyerObjet(objet) {
  const nettoye = { ...objet };

  // Supprimer les propriétés undefined
  for (const cle in nettoye) {
    if (nettoye[cle] === undefined) {
      delete nettoye[cle];
    }
  }

  // Supprimer les propriétés null
  for (const cle in nettoye) {
    if (nettoye[cle] === null) {
      delete nettoye[cle];
    }
  }

  // Supprimer les chaînes vides
  for (const cle in nettoye) {
    if (nettoye[cle] === "") {
      delete nettoye[cle];
    }
  }

  return nettoye;
}

const donneesSales = {
  nom: "Alice",
  age: 28,
  email: "",
  ville: null,
  pays: undefined,
  actif: true
};

const donneesPropres = nettoyerObjet(donneesSales);

console.log(donneesPropres);
// { nom: "Alice", age: 28, actif: true }
```

### Exemple 5 : Mise à jour conditionnelle

```javascript
function mettreAJourSiDifferent(objet, propriete, nouvelleValeur) {
  if (!(propriete in objet)) {
    console.log(`Ajout de ${propriete}`);
    objet[propriete] = nouvelleValeur;
    return true;
  }

  if (objet[propriete] !== nouvelleValeur) {
    console.log(`Modification de ${propriete}: ${objet[propriete]} → ${nouvelleValeur}`);
    objet[propriete] = nouvelleValeur;
    return true;
  }

  console.log(`${propriete} inchangé`);
  return false;
}

const config = {
  theme: "clair",
  langue: "fr"
};

mettreAJourSiDifferent(config, "theme", "clair");      // Inchangé
mettreAJourSiDifferent(config, "theme", "sombre");     // Modifié
mettreAJourSiDifferent(config, "notifications", true); // Ajouté

console.log(config);
// {
//   theme: "sombre",
//   langue: "fr",
//   notifications: true
// }
```

## 7. Objets imbriqués

### Ajouter des propriétés imbriquées

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28
};

// Ajouter un objet imbriqué
utilisateur.adresse = {
  rue: "10 rue de la Paix",
  ville: "Paris"
};

// Ajouter une propriété à l'objet imbriqué
utilisateur.adresse.codePostal = "75001";

console.log(utilisateur);
// {
//   nom: "Alice",
//   age: 28,
//   adresse: {
//     rue: "10 rue de la Paix",
//     ville: "Paris",
//     codePostal: "75001"
//   }
// }
```

### Vérifier avant d'ajouter dans un objet imbriqué

```javascript
const config = {
  app: {
    nom: "MonApp"
  }
};

// ❌ ERREUR si config.utilisateur n'existe pas
// config.utilisateur.theme = "sombre";  // TypeError

// ✅ Vérifier d'abord
if (!config.utilisateur) {
  config.utilisateur = {};
}
config.utilisateur.theme = "sombre";

console.log(config);
// {
//   app: { nom: "MonApp" },
//   utilisateur: { theme: "sombre" }
// }
```

### Supprimer des propriétés imbriquées

```javascript
const entreprise = {
  nom: "TechCorp",
  employes: {
    direction: {
      ceo: "Marie",
      cto: "Jean"
    },
    effectif: 150
  }
};

// Supprimer une propriété imbriquée
delete entreprise.employes.direction.cto;

console.log(entreprise.employes.direction);
// { ceo: "Marie" }

// Supprimer tout l'objet imbriqué
delete entreprise.employes;

console.log(entreprise);
// { nom: "TechCorp" }
```

## 8. Approche immutable vs mutable

### Approche mutable (modification directe)

```javascript
const utilisateur = {
  nom: "Alice",
  score: 100
};

// ❌ Modification directe
utilisateur.score = 150;
utilisateur.niveau = 5;
delete utilisateur.nom;

// L'objet original est modifié
```

**Avantages :**
- Plus simple
- Plus performant (pas de copie)

**Inconvénients :**
- Peut causer des bugs difficiles à trouver
- Problématique en programmation fonctionnelle
- Difficile de suivre l'historique des changements

### Approche immutable (création de nouveaux objets)

```javascript
const utilisateur = {
  nom: "Alice",
  score: 100
};

// ✅ Création de nouveaux objets
const utilisateur2 = { ...utilisateur, score: 150 };
const utilisateur3 = { ...utilisateur2, niveau: 5 };
const { nom, ...utilisateur4 } = utilisateur3;

// L'objet original est inchangé
console.log(utilisateur);
// { nom: "Alice", score: 100 }
```

**Avantages :**
- Prévisible et sûr
- Facilite le debugging
- Recommandé avec React, Redux, etc.

**Inconvénients :**
- Plus verbeux
- Légèrement moins performant

### Quand utiliser quelle approche ?

```javascript
// ✅ Mutable : objet local, usage interne
function calculerStatistiques(data) {
  const stats = {};

  stats.total = data.length;
  stats.moyenne = data.reduce((a, b) => a + b, 0) / data.length;
  stats.max = Math.max(...data);

  return stats;
}

// ✅ Immutable : objet partagé, état d'application
let etatApp = {
  utilisateur: { nom: "Alice" },
  theme: "clair"
};

function changerTheme(theme) {
  // Ne pas modifier etatApp directement
  etatApp = {
    ...etatApp,
    theme
  };
}
```

## 9. Bonnes pratiques

### 1. Préférez l'ajout explicite

```javascript
// ✅ Bon : clair et explicite
utilisateur.email = "alice@example.com";

// ❌ À éviter : trop générique
Object.assign(utilisateur, donnees);
```

### 2. Vérifiez avant de supprimer

```javascript
// ✅ Bon : vérification avant suppression
if ("tempData" in objet) {
  delete objet.tempData;
}

// ⚠️ OK mais moins précis
delete objet.tempData;  // Pas d'erreur même si inexistant
```

### 3. Documentez les modifications dynamiques

```javascript
// ✅ Bon : commenté
function enrichirProduit(produit, options) {
  // Ajout d'ID unique
  produit.id = generateId();

  // Ajout de timestamp
  produit.timestamp = Date.now();

  // Ajout optionnel des métadonnées
  if (options.metadata) {
    produit.metadata = options.metadata;
  }
}
```

### 4. Utilisez l'immutabilité pour l'état partagé

```javascript
// ✅ Bon : création de nouveaux objets
function mettreAJourConfig(config, cle, valeur) {
  return {
    ...config,
    [cle]: valeur
  };
}

// ❌ Risqué : modification directe
function mettreAJourConfigMutable(config, cle, valeur) {
  config[cle] = valeur;
  return config;
}
```

### 5. Nettoyez les données sensibles

```javascript
function envoyerAuClient(utilisateur) {
  const { motDePasse, tokenSession, ...utilisateurPublic } = utilisateur;

  return utilisateurPublic;
}
```

## 10. Pièges à éviter

### Piège 1 : Oublier que les objets sont des références

```javascript
const config1 = { theme: "clair" };
const config2 = config1;  // Même référence !

config2.theme = "sombre";
console.log(config1.theme);  // "sombre" (modifié aussi !)

// ✅ Solution : copier avec spread
const config3 = { ...config1 };
```

### Piège 2 : delete sur des propriétés non-configurables

```javascript
const objet = {};
Object.defineProperty(objet, "constante", {
  value: 42,
  writable: false,
  configurable: false
});

delete objet.constante;  // Ne fait rien en mode non-strict
console.log(objet.constante);  // 42 (toujours là)
```

### Piège 3 : Modifications pendant l'itération

```javascript
const objet = { a: 1, b: 2, c: 3 };

// ⚠️ Risqué : modifier pendant l'itération
for (const cle in objet) {
  if (objet[cle] === 2) {
    delete objet[cle];  // Peut causer des comportements imprévisibles
  }
}

// ✅ Mieux : collecter d'abord, supprimer ensuite
const aSuppprimer = [];
for (const cle in objet) {
  if (objet[cle] === 2) {
    aSuppprimer.push(cle);
  }
}
aSuppprimer.forEach(cle => delete objet[cle]);
```

## Points clés à retenir

1. **Ajouter** : `objet.nouvelleProp = valeur` ou `objet["nouvelleProp"] = valeur`
2. **Modifier** : Même syntaxe que l'ajout
3. **Supprimer** : `delete objet.propriete`
4. **Vérifier** : `"propriete" in objet` ou `objet.hasOwnProperty("propriete")`
5. **Immutable** : Utiliser le spread operator `{ ...objet, nouvelleProp: valeur }`
6. **delete vs undefined** : `delete` supprime vraiment la propriété
7. **Les objets sont des références** : Attention aux modifications non intentionnelles
8. **Approche immutable** recommandée pour l'état partagé

## Tableau récapitulatif

| Opération | Syntaxe mutable | Syntaxe immutable |
|-----------|----------------|-------------------|
| Ajouter | `obj.prop = val` | `{ ...obj, prop: val }` |
| Modifier | `obj.prop = newVal` | `{ ...obj, prop: newVal }` |
| Supprimer | `delete obj.prop` | `const { prop, ...rest } = obj` |
| Vérifier | `"prop" in obj` | `"prop" in obj` |

## Ce qui vient ensuite

Maintenant que vous savez manipuler les propriétés d'objets, vous allez découvrir :
- Les méthodes d'objets (fonctions dans les objets)
- Le mot-clé `this` et son fonctionnement
- Les constructeurs pour créer des objets
- Les classes ES6 pour une programmation orientée objet moderne

La capacité à ajouter et supprimer dynamiquement des propriétés est une caractéristique fondamentale de JavaScript qui le rend très flexible !

⏭️ [Méthodes d'objets](/05-javascript-moderne-fondamentaux/07-objets-modernes/07-methodes-objets.md)
