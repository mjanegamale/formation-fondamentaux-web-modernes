🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.5 - Spread operator (...) pour copier et fusionner 🆕

## Introduction

Le **spread operator** (opérateur de décomposition) `...` est une fonctionnalité ES6 qui permet de "décomposer" un objet ou un tableau en ses éléments individuels. Pour les objets, il est principalement utilisé pour :

1. **Copier** des objets
2. **Fusionner** (merger) plusieurs objets
3. Ajouter ou modifier des propriétés tout en gardant les autres

C'est l'une des fonctionnalités les plus pratiques et les plus utilisées du JavaScript moderne.

### Syntaxe de base

Le spread operator s'écrit avec **trois points** `...` devant un objet :

```javascript
const copie = { ...objetOriginal };
```

## 1. Copier un objet

### Le problème : la référence

En JavaScript, les objets sont des **références**. Quand on assigne un objet à une nouvelle variable, on ne crée pas une copie, on crée juste une nouvelle référence vers le même objet :

```javascript
const utilisateur1 = {
  nom: "Alice",
  age: 28
};

// ❌ Ceci ne crée PAS une copie
const utilisateur2 = utilisateur1;

// Modification de utilisateur2
utilisateur2.age = 30;

// ⚠️ utilisateur1 est aussi modifié !
console.log(utilisateur1.age);  // 30
console.log(utilisateur2.age);  // 30

// Les deux variables pointent vers le même objet
console.log(utilisateur1 === utilisateur2);  // true
```

### La solution : le spread operator

Le spread operator crée une **vraie copie** de l'objet :

```javascript
const utilisateur1 = {
  nom: "Alice",
  age: 28
};

// ✅ Copie avec le spread operator
const utilisateur2 = { ...utilisateur1 };

// Modification de utilisateur2
utilisateur2.age = 30;

// ✅ utilisateur1 n'est PAS modifié
console.log(utilisateur1.age);  // 28
console.log(utilisateur2.age);  // 30

// Ce sont deux objets différents
console.log(utilisateur1 === utilisateur2);  // false
```

### Exemples de copie

```javascript
const produit = {
  nom: "Ordinateur",
  prix: 899,
  stock: 15
};

// Copie complète
const copieProduit = { ...produit };

console.log(copieProduit);
// { nom: "Ordinateur", prix: 899, stock: 15 }

// Modifier la copie n'affecte pas l'original
copieProduit.prix = 799;

console.log(produit.prix);       // 899 (inchangé)
console.log(copieProduit.prix);  // 799
```

## 2. Copier et modifier en même temps

On peut copier un objet et **modifier/ajouter des propriétés** en une seule opération :

### Syntaxe

```javascript
const nouvelObjet = {
  ...objetOriginal,
  proprieteModifiee: nouvelleValeur,
  nouvellePropriete: valeur
};
```

### Exemples

```javascript
const utilisateur = {
  nom: "Bob",
  age: 30,
  ville: "Paris"
};

// Copier et modifier "age"
const utilisateurModifie = {
  ...utilisateur,
  age: 31
};

console.log(utilisateur.age);         // 30 (original inchangé)
console.log(utilisateurModifie.age);  // 31

// Copier et ajouter une nouvelle propriété
const utilisateurAvecEmail = {
  ...utilisateur,
  email: "bob@example.com"
};

console.log(utilisateurAvecEmail);
// {
//   nom: "Bob",
//   age: 30,
//   ville: "Paris",
//   email: "bob@example.com"
// }
```

### Ordre important : écrasement des propriétés

L'ordre des propriétés est important. Les propriétés qui viennent **après** écrasent celles d'avant :

```javascript
const config = {
  theme: "clair",
  langue: "fr",
  notifications: true
};

// ✅ Le spread avant : on peut écraser
const config1 = {
  ...config,
  theme: "sombre"  // Écrase theme
};
console.log(config1.theme);  // "sombre"

// ❌ Le spread après : les modifications sont écrasées
const config2 = {
  theme: "sombre",
  ...config  // Écrase tout avec les valeurs originales
};
console.log(config2.theme);  // "clair" (valeur originale)
```

**Règle :** Mettez le spread operator **avant** les propriétés que vous voulez modifier.

## 3. Fusionner plusieurs objets

Le spread operator permet de **fusionner** (merger) plusieurs objets :

### Syntaxe

```javascript
const fusion = { ...objet1, ...objet2, ...objet3 };
```

### Exemple de fusion

```javascript
const infoBase = {
  nom: "Alice",
  age: 28
};

const contact = {
  email: "alice@example.com",
  telephone: "0123456789"
};

const adresse = {
  ville: "Paris",
  pays: "France"
};

// Fusionner les trois objets
const profilComplet = {
  ...infoBase,
  ...contact,
  ...adresse
};

console.log(profilComplet);
// {
//   nom: "Alice",
//   age: 28,
//   email: "alice@example.com",
//   telephone: "0123456789",
//   ville: "Paris",
//   pays: "France"
// }
```

### Fusion avec propriétés en commun

Si deux objets ont des propriétés avec le **même nom**, celui qui vient **en dernier** gagne :

```javascript
const defaults = {
  theme: "clair",
  langue: "en",
  notifications: true
};

const userPrefs = {
  langue: "fr",
  notifications: false
};

// Fusion : userPrefs écrase defaults
const config = {
  ...defaults,
  ...userPrefs
};

console.log(config);
// {
//   theme: "clair",        // de defaults
//   langue: "fr",          // écrasé par userPrefs
//   notifications: false   // écrasé par userPrefs
// }
```

### Cas d'usage : options par défaut

C'est très utile pour gérer des options avec valeurs par défaut :

```javascript
function creerUtilisateur(options) {
  const defaults = {
    role: "user",
    actif: true,
    notifications: true
  };

  // Fusionner les defaults avec les options fournies
  const config = { ...defaults, ...options };

  return {
    id: Math.random(),
    ...config,
    dateCreation: new Date()
  };
}

// Utilisation avec options partielles
const user1 = creerUtilisateur({
  nom: "Alice",
  email: "alice@example.com"
});

console.log(user1);
// {
//   id: 0.123...,
//   role: "user",          // valeur par défaut
//   actif: true,           // valeur par défaut
//   notifications: true,   // valeur par défaut
//   nom: "Alice",
//   email: "alice@example.com",
//   dateCreation: ...
// }

const user2 = creerUtilisateur({
  nom: "Bob",
  email: "bob@example.com",
  role: "admin",           // Écrase la valeur par défaut
  actif: false
});

console.log(user2.role);  // "admin"
console.log(user2.actif); // false
```

## 4. Exemples pratiques complets

### Exemple 1 : Mise à jour immutable d'état

En React et autres frameworks modernes, on ne modifie jamais l'état directement, on crée une nouvelle version :

```javascript
let etatApp = {
  utilisateur: {
    nom: "Alice",
    score: 100
  },
  theme: "clair",
  notifications: true
};

// ❌ Mauvaise pratique : modification directe
// etatApp.theme = "sombre";

// ✅ Bonne pratique : créer un nouvel état
etatApp = {
  ...etatApp,
  theme: "sombre"
};

// Incrémenter le score sans modifier directement
etatApp = {
  ...etatApp,
  utilisateur: {
    ...etatApp.utilisateur,
    score: etatApp.utilisateur.score + 10
  }
};

console.log(etatApp.utilisateur.score);  // 110
```

### Exemple 2 : Gestion de formulaire

```javascript
let formulaire = {
  nom: "",
  email: "",
  message: "",
  accepterCGU: false
};

// Simuler la saisie utilisateur
function mettreAJourChamp(champ, valeur) {
  formulaire = {
    ...formulaire,
    [champ]: valeur  // Notation avec crochets pour clé dynamique
  };
}

mettreAJourChamp("nom", "Alice");
mettreAJourChamp("email", "alice@example.com");
mettreAJourChamp("message", "Bonjour !");
mettreAJourChamp("accepterCGU", true);

console.log(formulaire);
// {
//   nom: "Alice",
//   email: "alice@example.com",
//   message: "Bonjour !",
//   accepterCGU: true
// }
```

### Exemple 3 : Configuration d'API

```javascript
const configBase = {
  baseURL: "https://api.example.com",
  timeout: 5000,
  headers: {
    "Content-Type": "application/json"
  }
};

// Configuration pour requête authentifiée
function creerConfigAuth(token) {
  return {
    ...configBase,
    headers: {
      ...configBase.headers,
      "Authorization": `Bearer ${token}`
    }
  };
}

const configAuth = creerConfigAuth("abc123xyz");
console.log(configAuth);
// {
//   baseURL: "https://api.example.com",
//   timeout: 5000,
//   headers: {
//     "Content-Type": "application/json",
//     "Authorization": "Bearer abc123xyz"
//   }
// }
```

### Exemple 4 : Gestion de produits

```javascript
const produitBase = {
  id: 1001,
  nom: "Ordinateur portable",
  prix: 899,
  stock: 15
};

// Appliquer une réduction
function appliquerReduction(produit, pourcentage) {
  const reduction = produit.prix * (pourcentage / 100);

  return {
    ...produit,
    prixOriginal: produit.prix,
    prix: produit.prix - reduction,
    enPromotion: true
  };
}

const produitEnPromo = appliquerReduction(produitBase, 10);

console.log(produitBase.prix);        // 899 (inchangé)
console.log(produitEnPromo.prix);     // 809.1
console.log(produitEnPromo.enPromotion);  // true
```

### Exemple 5 : Fusionner des configurations

```javascript
const configDev = {
  apiUrl: "http://localhost:3000",
  debug: true,
  logLevel: "verbose"
};

const configProd = {
  apiUrl: "https://api.production.com",
  debug: false,
  logLevel: "error"
};

const configCommune = {
  timeout: 5000,
  retries: 3,
  cache: true
};

// Choisir la configuration selon l'environnement
const environnement = "development";

const config = {
  ...configCommune,
  ...(environnement === "development" ? configDev : configProd)
};

console.log(config);
// {
//   timeout: 5000,
//   retries: 3,
//   cache: true,
//   apiUrl: "http://localhost:3000",
//   debug: true,
//   logLevel: "verbose"
// }
```

## 5. Copie superficielle vs copie profonde

### Important : copie superficielle (shallow copy)

Le spread operator fait une **copie superficielle** : seul le premier niveau est copié. Les objets imbriqués restent des références :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  adresse: {
    ville: "Paris",
    codePostal: "75001"
  }
};

// Copie avec spread operator
const copie = { ...utilisateur };

// Modifier une propriété de premier niveau : OK
copie.age = 30;
console.log(utilisateur.age);  // 28 (inchangé) ✅

// Modifier une propriété imbriquée : ATTENTION !
copie.adresse.ville = "Lyon";
console.log(utilisateur.adresse.ville);  // "Lyon" (modifié aussi!) ⚠️

// adresse est toujours une référence partagée
console.log(utilisateur.adresse === copie.adresse);  // true
```

### Solution : copier les objets imbriqués aussi

Pour une vraie copie indépendante, il faut copier aussi les objets imbriqués :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  adresse: {
    ville: "Paris",
    codePostal: "75001"
  }
};

// Copie profonde manuelle du premier niveau
const copie = {
  ...utilisateur,
  adresse: { ...utilisateur.adresse }  // Copier l'objet imbriqué
};

// Maintenant c'est vraiment indépendant
copie.adresse.ville = "Lyon";
console.log(utilisateur.adresse.ville);  // "Paris" (inchangé) ✅
console.log(copie.adresse.ville);        // "Lyon"

console.log(utilisateur.adresse === copie.adresse);  // false
```

### Exemple avec plusieurs niveaux

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

// Copie profonde manuelle
const copieEntreprise = {
  ...entreprise,
  employes: {
    ...entreprise.employes,
    direction: {
      ...entreprise.employes.direction
    }
  }
};

// Modification de la copie
copieEntreprise.employes.direction.ceo = "Sophie";

console.log(entreprise.employes.direction.ceo);      // "Marie" (inchangé)
console.log(copieEntreprise.employes.direction.ceo); // "Sophie"
```

### Pour des copies vraiment profondes

Pour des objets très imbriqués, utilisez :

```javascript
// Méthode 1 : JSON (simple mais limitations)
const copieProfonde1 = JSON.parse(JSON.stringify(objetOriginal));

// Méthode 2 : structuredClone (moderne, navigateurs récents)
const copieProfonde2 = structuredClone(objetOriginal);

// Méthode 3 : Bibliothèque comme Lodash
// const copieProfonde3 = _.cloneDeep(objetOriginal);
```

**Note :** Pour la plupart des cas simples, le spread operator suffit.

## 6. Comparaison avant/après ES6

### Copier un objet

```javascript
const original = { nom: "Alice", age: 28 };

// ❌ AVANT ES6 : Object.assign()
const copie1 = Object.assign({}, original);

// ✅ AVEC ES6 : Spread operator
const copie2 = { ...original };
```

### Fusionner des objets

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };

// ❌ AVANT ES6 : Object.assign()
const fusion1 = Object.assign({}, obj1, obj2);

// ✅ AVEC ES6 : Spread operator
const fusion2 = { ...obj1, ...obj2 };
```

### Copier et modifier

```javascript
const utilisateur = { nom: "Bob", age: 30 };

// ❌ AVANT ES6
const modifie1 = Object.assign({}, utilisateur, { age: 31 });

// ✅ AVEC ES6
const modifie2 = { ...utilisateur, age: 31 };
```

**Le spread operator est plus court, plus lisible et plus intuitif.**

## 7. Utilisation avec des tableaux (aperçu)

Le spread operator fonctionne aussi avec les tableaux (nous verrons cela en détail dans la section 5.8.4) :

```javascript
const nombres1 = [1, 2, 3];
const nombres2 = [4, 5, 6];

// Copier un tableau
const copie = [...nombres1];

// Fusionner des tableaux
const fusion = [...nombres1, ...nombres2];
console.log(fusion);  // [1, 2, 3, 4, 5, 6]

// Ajouter des éléments
const nouveaux = [...nombres1, 7, 8, 9];
console.log(nouveaux);  // [1, 2, 3, 7, 8, 9]
```

## 8. Pièges à éviter

### Piège 1 : Croire que c'est une copie profonde

```javascript
const data = {
  user: {
    nom: "Alice"
  }
};

const copie = { ...data };
copie.user.nom = "Bob";

// ⚠️ L'original est modifié aussi !
console.log(data.user.nom);  // "Bob"

// ✅ Solution : copier aussi les objets imbriqués
const vraieCopie = {
  ...data,
  user: { ...data.user }
};
```

### Piège 2 : Ordre de priorité

```javascript
const defaults = { a: 1, b: 2, c: 3 };
const custom = { b: 20 };

// ✅ custom écrase defaults
const result1 = { ...defaults, ...custom };
console.log(result1.b);  // 20

// ❌ defaults écrase custom
const result2 = { ...custom, ...defaults };
console.log(result2.b);  // 2

// L'ordre compte !
```

### Piège 3 : Performance avec de gros objets

Le spread operator crée une nouvelle copie complète. Pour de très gros objets, cela peut être coûteux :

```javascript
// Si l'objet a 10000 propriétés
const grosObjet = { /* ... beaucoup de propriétés ... */ };

// Ceci copie tout
const copie = { ...grosObjet };

// Si vous ne modifiez qu'une propriété, c'est inefficace
```

**Dans la plupart des cas, ce n'est pas un problème.**

## 9. Cas d'usage avancés

### Composition d'objets

```javascript
const avecNom = (nom) => ({ nom });
const avecAge = (age) => ({ age });
const avecEmail = (email) => ({ email });

const utilisateur = {
  ...avecNom("Alice"),
  ...avecAge(28),
  ...avecEmail("alice@example.com"),
  id: 123
};

console.log(utilisateur);
// { nom: "Alice", age: 28, email: "alice@example.com", id: 123 }
```

### Supprimer des propriétés

Combiné avec le destructuring :

```javascript
const utilisateur = {
  id: 123,
  nom: "Alice",
  motDePasse: "secret",
  email: "alice@example.com"
};

// Extraire motDePasse et garder le reste
const { motDePasse, ...utilisateurSansMotDePasse } = utilisateur;

console.log(utilisateurSansMotDePasse);
// { id: 123, nom: "Alice", email: "alice@example.com" }
```

### Conditions avec spread

```javascript
function creerProfil(nom, options = {}) {
  return {
    nom,
    dateCreation: new Date(),
    // Ajouter conditionnellement des propriétés
    ...(options.premium && { badge: "Premium" }),
    ...(options.admin && { role: "admin" }),
    ...options
  };
}

const profil1 = creerProfil("Alice", { premium: true });
console.log(profil1.badge);  // "Premium"

const profil2 = creerProfil("Bob", { admin: true });
console.log(profil2.role);  // "admin"
```

## 10. Bonnes pratiques

### 1. Utilisez le spread pour l'immutabilité

```javascript
// ✅ Bon : ne modifie pas l'original
const nouveauConfig = { ...config, theme: "sombre" };

// ❌ Éviter : modifie l'original
config.theme = "sombre";
```

### 2. Spread avant modifications

```javascript
// ✅ Bon : le spread d'abord
const result = {
  ...defaults,
  option: "nouvelle valeur"
};

// ❌ Moins clair
const result = {
  option: "nouvelle valeur",
  ...defaults  // Écrase option
};
```

### 3. Commentez les spreads complexes

```javascript
const config = {
  ...baseConfig,
  ...environmentConfig,  // Écrase avec config environnement
  ...userPreferences,    // Priorité aux préférences utilisateur
  version: "2.0"         // Version toujours fixe
};
```

### 4. Ne pas abuser des niveaux

```javascript
// ⚠️ Difficile à lire
const result = {
  ...obj1,
  nested: {
    ...obj1.nested,
    deep: {
      ...obj1.nested.deep,
      veryDeep: {
        ...obj1.nested.deep.veryDeep,
        value: "new"
      }
    }
  }
};

// ✅ Mieux : extraire dans des fonctions
function updateDeepValue(obj, value) {
  return {
    ...obj,
    nested: {
      ...obj.nested,
      deep: {
        ...obj.nested.deep,
        veryDeep: {
          ...obj.nested.deep.veryDeep,
          value
        }
      }
    }
  };
}
```

## Points clés à retenir

1. **Spread operator** `...` décompose un objet en ses propriétés
2. **Copier** : `const copie = { ...original }`
3. **Fusionner** : `const fusion = { ...obj1, ...obj2 }`
4. **Modifier** : `const modifie = { ...original, prop: nouvelleValeur }`
5. **L'ordre compte** : les propriétés suivantes écrasent les précédentes
6. **Copie superficielle** : les objets imbriqués restent des références
7. **Plus lisible** que `Object.assign()`
8. **Immutabilité** : ne modifie jamais l'original

## Tableau récapitulatif

| Opération | Syntaxe | Résultat |
|-----------|---------|----------|
| Copier | `{ ...obj }` | Nouvelle copie indépendante |
| Fusionner | `{ ...obj1, ...obj2 }` | Toutes les propriétés combinées |
| Modifier | `{ ...obj, prop: val }` | Copie avec prop modifiée |
| Ajouter | `{ ...obj, newProp: val }` | Copie avec nouvelle propriété |
| Défauts | `{ ...defaults, ...custom }` | custom écrase defaults |

## Ce qui vient ensuite

Le spread operator fonctionne aussi avec les tableaux (section 5.8.4). Vous allez découvrir comment :
- Copier et fusionner des tableaux
- Ajouter des éléments
- Passer des arguments à des fonctions
- Convertir des structures de données

Le spread operator est **indispensable** en JavaScript moderne, surtout avec React, Vue et les autres frameworks qui privilégient l'immutabilité !

⏭️ [Ajout et suppression de propriétés](/05-javascript-moderne-fondamentaux/07-objets-modernes/06-ajout-suppression-proprietes.md)
