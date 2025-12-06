🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.3 - Accès aux propriétés : notation point vs crochets

## Introduction

Maintenant que vous savez créer des objets, il est temps d'apprendre à **accéder** à leurs propriétés et à les **modifier**. JavaScript propose deux méthodes principales pour accéder aux propriétés d'un objet :

1. **La notation point** (dot notation) : `objet.propriete`
2. **La notation crochets** (bracket notation) : `objet["propriete"]`

Chacune a ses avantages et ses cas d'usage spécifiques. Comprendre quand utiliser l'une ou l'autre est essentiel en JavaScript.

## 1. La notation point (Dot Notation)

### Syntaxe

La notation point est la plus courante et la plus simple :

```javascript
objet.propriete
```

### Lecture de propriétés

```javascript
const personne = {
  nom: "Alice",
  age: 28,
  ville: "Paris"
};

// Accès avec la notation point
console.log(personne.nom);    // "Alice"
console.log(personne.age);    // 28
console.log(personne.ville);  // "Paris"
```

### Utilisation dans des expressions

```javascript
const utilisateur = {
  prenom: "Bob",
  nom: "Martin",
  age: 32
};

// Dans des chaînes de caractères
console.log(`Bonjour ${utilisateur.prenom} !`);
// "Bonjour Bob !"

// Dans des calculs
const anneeNaissance = 2024 - utilisateur.age;
console.log(anneeNaissance);  // 1992

// Dans des conditions
if (utilisateur.age >= 18) {
  console.log("Majeur");
}
```

### Modification de propriétés

On peut modifier une propriété existante :

```javascript
const produit = {
  nom: "Ordinateur",
  prix: 899,
  stock: 10
};

console.log(produit.prix);  // 899

// Modification
produit.prix = 799;
console.log(produit.prix);  // 799

// Modification avec calcul
produit.stock = produit.stock - 1;
// ou plus court :
produit.stock--;
console.log(produit.stock);  // 9
```

### Ajout de nouvelles propriétés

On peut ajouter une propriété qui n'existait pas :

```javascript
const voiture = {
  marque: "Peugeot",
  modele: "308"
};

console.log(voiture);
// { marque: "Peugeot", modele: "308" }

// Ajout d'une nouvelle propriété
voiture.annee = 2023;
voiture.couleur = "bleu";

console.log(voiture);
// {
//   marque: "Peugeot",
//   modele: "308",
//   annee: 2023,
//   couleur: "bleu"
// }
```

## 2. La notation crochets (Bracket Notation)

### Syntaxe

La notation crochets utilise des crochets `[]` avec le nom de la propriété **entre guillemets** :

```javascript
objet["propriete"]
```

### Lecture de propriétés

```javascript
const personne = {
  nom: "Alice",
  age: 28,
  ville: "Paris"
};

// Accès avec la notation crochets
console.log(personne["nom"]);    // "Alice"
console.log(personne["age"]);    // 28
console.log(personne["ville"]);  // "Paris"
```

**Important :** Le nom de la propriété doit être une **chaîne de caractères** (entre guillemets).

### Modification avec la notation crochets

```javascript
const produit = {
  nom: "Clavier",
  prix: 49.99
};

// Modification
produit["prix"] = 39.99;
console.log(produit["prix"]);  // 39.99

// Ajout
produit["stock"] = 50;
console.log(produit);
// { nom: "Clavier", prix: 39.99, stock: 50 }
```

## 3. Quand utiliser quelle notation ?

### Notation point : Usage par défaut ✅

**Utilisez la notation point** dans la plupart des cas :

```javascript
const user = {
  nom: "Sophie",
  email: "sophie@example.com"
};

// ✅ Préférez la notation point
console.log(user.nom);
console.log(user.email);
```

**Avantages :**
- Plus courte et lisible
- Plus rapide à écrire
- Standard en JavaScript

### Notation crochets : Cas spécifiques 🔧

**Utilisez la notation crochets** dans ces situations :

#### Cas 1 : Propriétés avec espaces ou caractères spéciaux

```javascript
const config = {
  "couleur de fond": "blanc",
  "taille-police": "16px",
  "data-id": "123"
};

// ❌ ERREUR avec notation point
// console.log(config.couleur de fond);  // Syntaxe invalide

// ✅ OK avec notation crochets
console.log(config["couleur de fond"]);  // "blanc"
console.log(config["taille-police"]);     // "16px"
console.log(config["data-id"]);           // "123"
```

**Note :** Évitez de créer des propriétés avec espaces. Utilisez plutôt le camelCase : `couleurDeFond`.

#### Cas 2 : Nom de propriété dans une variable

C'est le cas d'usage le plus important de la notation crochets :

```javascript
const utilisateur = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com"
};

// Le nom de la propriété est stocké dans une variable
const propriete = "nom";

// ❌ Ne fonctionne pas avec notation point
console.log(utilisateur.propriete);  // undefined (cherche une propriété nommée "propriete")

// ✅ Fonctionne avec notation crochets
console.log(utilisateur[propriete]);  // "Alice"
```

**Exemple pratique :**

```javascript
function afficherPropriete(objet, nomPropriete) {
  return objet[nomPropriete];
}

const produit = {
  nom: "Souris",
  prix: 29.99,
  stock: 100
};

console.log(afficherPropriete(produit, "nom"));    // "Souris"
console.log(afficherPropriete(produit, "prix"));   // 29.99
console.log(afficherPropriete(produit, "stock"));  // 100
```

#### Cas 3 : Noms de propriétés dynamiques

```javascript
const stats = {
  visites: 1000,
  clics: 250,
  conversions: 50
};

// Parcourir dynamiquement les propriétés
const metriques = ["visites", "clics", "conversions"];

metriques.forEach(metrique => {
  console.log(`${metrique}: ${stats[metrique]}`);
});
// visites: 1000
// clics: 250
// conversions: 50
```

#### Cas 4 : Noms de propriétés calculés

```javascript
const formulaire = {
  nom: "Alice",
  email: "alice@example.com"
};

const prefixe = "email";

// Calcul du nom de la propriété
console.log(formulaire[prefixe]);  // "alice@example.com"

// Avec concaténation
const index = 1;
const objet = {
  champ1: "valeur1",
  champ2: "valeur2"
};

console.log(objet["champ" + index]);  // "valeur1"
```

## 4. Propriétés inexistantes

### Que se passe-t-il ?

Quand on accède à une propriété qui n'existe pas, JavaScript renvoie `undefined` :

```javascript
const personne = {
  nom: "Alice",
  age: 28
};

console.log(personne.ville);     // undefined
console.log(personne["email"]);  // undefined
```

**Important :** Pas d'erreur, juste `undefined`.

### Vérifier l'existence d'une propriété

#### Méthode 1 : Vérification simple

```javascript
const user = {
  nom: "Bob",
  email: "bob@example.com"
};

if (user.email) {
  console.log("Email trouvé:", user.email);
} else {
  console.log("Pas d'email");
}
```

**Attention :** Cette méthode ne fonctionne pas si la valeur est `false`, `0`, ou `""`.

#### Méthode 2 : Opérateur `in`

```javascript
const config = {
  theme: "sombre",
  notifications: false
};

console.log("theme" in config);          // true
console.log("notifications" in config);  // true (même si false)
console.log("langue" in config);         // false

if ("notifications" in config) {
  console.log("Paramètre notifications existe");
}
```

#### Méthode 3 : `hasOwnProperty()`

```javascript
const objet = {
  nom: "test",
  valeur: 0
};

console.log(objet.hasOwnProperty("nom"));      // true
console.log(objet.hasOwnProperty("valeur"));   // true
console.log(objet.hasOwnProperty("inexistant")); // false
```

## 5. Objets imbriqués (Nested Objects)

### Accès aux propriétés imbriquées

Les objets peuvent contenir d'autres objets. On accède aux propriétés en chaînant les notations :

```javascript
const utilisateur = {
  nom: "Alice",
  adresse: {
    rue: "10 rue de la Paix",
    ville: "Paris",
    codePostal: "75001"
  },
  contact: {
    email: "alice@example.com",
    telephone: "0123456789"
  }
};

// Accès aux propriétés imbriquées avec notation point
console.log(utilisateur.adresse.ville);      // "Paris"
console.log(utilisateur.contact.email);      // "alice@example.com"
console.log(utilisateur.adresse.codePostal); // "75001"
```

### Mélanger les notations

On peut combiner notation point et crochets :

```javascript
const entreprise = {
  nom: "TechCorp",
  employes: {
    direction: {
      "chef d'entreprise": "Marie Dubois",
      "directeur technique": "Jean Martin"
    }
  }
};

// Mélange des deux notations
console.log(entreprise.employes.direction["chef d'entreprise"]);
// "Marie Dubois"

console.log(entreprise["employes"]["direction"]["directeur technique"]);
// "Jean Martin"
```

### Modification de propriétés imbriquées

```javascript
const profil = {
  utilisateur: {
    nom: "Bob",
    preferences: {
      theme: "clair",
      langue: "fr"
    }
  }
};

// Modification
profil.utilisateur.preferences.theme = "sombre";
console.log(profil.utilisateur.preferences.theme);  // "sombre"

// Ajout
profil.utilisateur.preferences.notifications = true;
console.log(profil.utilisateur.preferences);
// { theme: "sombre", langue: "fr", notifications: true }
```

### Attention aux propriétés `undefined`

Chaîner l'accès peut causer des erreurs si une propriété intermédiaire n'existe pas :

```javascript
const data = {
  user: {
    nom: "Alice"
  }
};

// ✅ OK
console.log(data.user.nom);  // "Alice"

// ❌ ERREUR : adresse n'existe pas
// console.log(data.user.adresse.ville);
// TypeError: Cannot read property 'ville' of undefined
```

**Solution : Vérification avant accès**

```javascript
if (data.user && data.user.adresse) {
  console.log(data.user.adresse.ville);
} else {
  console.log("Adresse non définie");
}
```

**Solution moderne : Optional Chaining (voir section 5.4.5)**

```javascript
// Avec optional chaining (?.)
console.log(data.user?.adresse?.ville);  // undefined (pas d'erreur)
```

## 6. Exemples pratiques complets

### Exemple 1 : Gestion de configuration

```javascript
const config = {
  app: {
    nom: "MonApp",
    version: "1.0.0"
  },
  utilisateur: {
    theme: "sombre",
    langue: "fr"
  }
};

// Lecture
console.log("Application:", config.app.nom);
console.log("Thème:", config.utilisateur.theme);

// Modification
config.utilisateur.theme = "clair";
config.app.version = "1.0.1";

console.log("Nouvelle version:", config.app.version);
```

### Exemple 2 : Traitement de données dynamique

```javascript
const produits = {
  livre: {
    prix: 15.99,
    stock: 50
  },
  stylo: {
    prix: 2.49,
    stock: 200
  },
  cahier: {
    prix: 3.99,
    stock: 100
  }
};

function afficherProduit(nomProduit) {
  if (nomProduit in produits) {
    const produit = produits[nomProduit];
    console.log(`${nomProduit}: ${produit.prix}€ (stock: ${produit.stock})`);
  } else {
    console.log("Produit non trouvé");
  }
}

afficherProduit("livre");   // "livre: 15.99€ (stock: 50)"
afficherProduit("stylo");   // "stylo: 2.49€ (stock: 200)"
afficherProduit("crayon");  // "Produit non trouvé"
```

### Exemple 3 : Mise à jour de formulaire

```javascript
const formulaire = {
  champs: {
    nom: "",
    email: "",
    message: ""
  },
  valide: false
};

// Fonction pour mettre à jour un champ
function mettreAJourChamp(nomChamp, valeur) {
  if (nomChamp in formulaire.champs) {
    formulaire.champs[nomChamp] = valeur;
    console.log(`${nomChamp} mis à jour: ${valeur}`);
  }
}

mettreAJourChamp("nom", "Alice");
mettreAJourChamp("email", "alice@example.com");
mettreAJourChamp("message", "Bonjour !");

console.log(formulaire.champs);
// {
//   nom: "Alice",
//   email: "alice@example.com",
//   message: "Bonjour !"
// }
```

### Exemple 4 : Statistiques avec clés dynamiques

```javascript
const statistiques = {
  janvier: { ventes: 1000, revenus: 50000 },
  fevrier: { ventes: 1200, revenus: 60000 },
  mars: { ventes: 1500, revenus: 75000 }
};

function afficherStats(mois, metrique) {
  const moisData = statistiques[mois];

  if (moisData) {
    console.log(`${mois} - ${metrique}: ${moisData[metrique]}`);
  } else {
    console.log("Mois non trouvé");
  }
}

afficherStats("janvier", "ventes");   // "janvier - ventes: 1000"
afficherStats("fevrier", "revenus");  // "fevrier - revenus: 60000"
afficherStats("mars", "ventes");      // "mars - ventes: 1500"
```

## 7. Suppression de propriétés

On peut supprimer une propriété avec l'opérateur `delete` :

```javascript
const utilisateur = {
  nom: "Bob",
  age: 30,
  email: "bob@example.com",
  temporaire: "valeur"
};

console.log(utilisateur);
// { nom: "Bob", age: 30, email: "bob@example.com", temporaire: "valeur" }

// Suppression avec notation point
delete utilisateur.temporaire;

console.log(utilisateur);
// { nom: "Bob", age: 30, email: "bob@example.com" }

// Suppression avec notation crochets
delete utilisateur["email"];

console.log(utilisateur);
// { nom: "Bob", age: 30 }
```

## 8. Comparaison des deux notations

### Tableau récapitulatif

| Critère | Notation point | Notation crochets |
|---------|---------------|-------------------|
| **Syntaxe** | `objet.propriete` | `objet["propriete"]` |
| **Lisibilité** | ✅ Plus claire | ❌ Moins claire |
| **Vitesse d'écriture** | ✅ Plus rapide | ❌ Plus longue |
| **Propriétés avec espaces** | ❌ Impossible | ✅ Possible |
| **Propriétés dynamiques** | ❌ Impossible | ✅ Possible |
| **Noms dans variables** | ❌ Impossible | ✅ Possible |
| **Usage recommandé** | Par défaut | Cas spéciaux |

### Règle générale

```javascript
const data = {
  nom: "Alice",
  age: 28,
  "code postal": "75001"
};

// ✅ Notation point par défaut (si possible)
console.log(data.nom);
console.log(data.age);

// ✅ Notation crochets quand nécessaire
console.log(data["code postal"]);

// ✅ Notation crochets pour accès dynamique
const prop = "nom";
console.log(data[prop]);
```

## 9. Erreurs courantes

### Erreur 1 : Oublier les guillemets avec notation crochets

```javascript
const personne = {
  nom: "Alice"
};

// ❌ ERREUR : nom n'est pas entre guillemets
// console.log(personne[nom]);  // ReferenceError: nom is not defined

// ✅ CORRECT
console.log(personne["nom"]);  // "Alice"

// ✅ OU si nom est une variable
const propriete = "nom";
console.log(personne[propriete]);  // "Alice"
```

### Erreur 2 : Utiliser notation point avec espaces

```javascript
const config = {
  "couleur fond": "blanc"
};

// ❌ ERREUR : Syntaxe invalide
// console.log(config.couleur fond);

// ✅ CORRECT
console.log(config["couleur fond"]);  // "blanc"
```

### Erreur 3 : Chaîner sur undefined

```javascript
const data = {
  user: {
    nom: "Alice"
  }
};

// ❌ ERREUR : adresse n'existe pas
// console.log(data.user.adresse.ville);
// TypeError

// ✅ Vérifier d'abord
if (data.user.adresse) {
  console.log(data.user.adresse.ville);
}

// ✅ Ou utiliser optional chaining
console.log(data.user.adresse?.ville);  // undefined
```

## 10. Bonnes pratiques

### 1. Préférez la notation point par défaut

```javascript
// ✅ Préférez ceci
const user = { nom: "Alice", age: 28 };
console.log(user.nom);
console.log(user.age);

// ❌ Évitez ceci (sauf si nécessaire)
console.log(user["nom"]);
console.log(user["age"]);
```

### 2. Utilisez des noms de propriétés simples

```javascript
// ✅ Bon : pas d'espaces, notation point possible
const config = {
  couleurFond: "blanc",
  taillePolice: 16
};

// ❌ À éviter : espaces, force notation crochets
const config = {
  "couleur fond": "blanc",
  "taille police": 16
};
```

### 3. Soyez cohérent

```javascript
// ✅ Cohérent : toujours la même notation
const data = { a: 1, b: 2, c: 3 };
console.log(data.a);
console.log(data.b);
console.log(data.c);

// ❌ Incohérent : mélange inutile
console.log(data.a);
console.log(data["b"]);
console.log(data.c);
```

### 4. Commentez les accès dynamiques

```javascript
const stats = {
  visites: 1000,
  clics: 250
};

const metriques = ["visites", "clics"];

// Accès dynamique pour parcourir toutes les métriques
metriques.forEach(metrique => {
  console.log(`${metrique}: ${stats[metrique]}`);
});
```

## Points clés à retenir

1. **Notation point** `objet.propriete` : usage par défaut, plus lisible
2. **Notation crochets** `objet["propriete"]` : pour cas spéciaux (espaces, variables, dynamique)
3. **Les deux notations** permettent de lire, modifier et ajouter des propriétés
4. **Propriété inexistante** → renvoie `undefined` (pas d'erreur)
5. **Objets imbriqués** : chaîner les accès avec `.` ou `[]`
6. **Optional chaining** `?.` évite les erreurs sur propriétés undefined
7. **Suppression** : opérateur `delete`

## Ce qui vient ensuite

Maintenant que vous maîtrisez l'accès aux propriétés, vous allez découvrir :
- Le destructuring d'objets (extraction élégante de propriétés)
- Le spread operator (copier et fusionner des objets)
- Les méthodes d'objets et le mot-clé `this`
- Les constructeurs et les classes

L'accès aux propriétés est une compétence fondamentale que vous utiliserez constamment en JavaScript !

⏭️ [Destructuring d'objets](/05-javascript-moderne-fondamentaux/07-objets-modernes/04-destructuring-objets.md)
