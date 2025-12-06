🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.1 - Création d'objets littéraux

## Introduction

Les objets sont l'un des concepts les plus fondamentaux et les plus puissants de JavaScript. Un **objet** est une structure de données qui permet de regrouper plusieurs valeurs et fonctionnalités liées ensemble. Contrairement aux types primitifs (string, number, boolean), les objets peuvent contenir plusieurs informations organisées.

Pensez à un objet comme à un **conteneur** qui peut stocker différentes informations connexes. Par exemple, au lieu d'avoir des variables séparées pour stocker les informations d'une personne, on peut tout regrouper dans un seul objet.

## Qu'est-ce qu'un objet littéral ?

Un **objet littéral** est la façon la plus simple et la plus courante de créer un objet en JavaScript. On l'appelle "littéral" car on écrit directement sa structure dans le code, entre accolades `{}`.

### Analogie du monde réel

Imaginez une fiche d'identité :
- **Nom** : Martin
- **Prénom** : Sophie
- **Âge** : 28
- **Ville** : Paris

En JavaScript, cela devient un objet qui regroupe toutes ces informations.

## Syntaxe de base

### Objet vide

La forme la plus simple d'un objet est un objet vide :

```javascript
const objetVide = {};
```

Cet objet existe, mais ne contient aucune information pour le moment.

### Objet avec des propriétés

Un objet contient des **propriétés**. Chaque propriété est composée d'une **clé** (le nom) et d'une **valeur** :

```javascript
const personne = {
  nom: "Martin",
  prenom: "Sophie",
  age: 28
};
```

**Structure d'une propriété :**
- `nom` → clé (aussi appelée "propriété")
- `"Martin"` → valeur
- `:` → sépare la clé de sa valeur
- `,` → sépare les différentes propriétés

## Les règles de syntaxe

### 1. Les accolades `{}`

Un objet est toujours délimité par des accolades :

```javascript
const monObjet = {
  // propriétés ici
};
```

### 2. Les paires clé-valeur

Chaque propriété suit le format `cle: valeur` :

```javascript
const livre = {
  titre: "Le Petit Prince",
  auteur: "Antoine de Saint-Exupéry",
  pages: 96
};
```

### 3. Les virgules

Les propriétés sont séparées par des virgules. La dernière virgule est optionnelle (mais recommandée en JavaScript moderne) :

```javascript
const film = {
  titre: "Inception",
  annee: 2010,
  realisateur: "Christopher Nolan", // virgule optionnelle sur la dernière ligne
};
```

### 4. Noms de propriétés

Les noms de propriétés (clés) peuvent être :
- Sans guillemets si ce sont des identifiants valides
- Avec guillemets si nécessaire (espaces, caractères spéciaux, etc.)

```javascript
const config = {
  // Sans guillemets (recommandé)
  couleur: "bleu",
  taille: 42,

  // Avec guillemets (si nécessaire)
  "couleur de fond": "blanc",
  "data-id": "123"
};
```

**Bonne pratique :** Utilisez des noms simples sans espaces ni caractères spéciaux pour éviter les guillemets.

## Types de valeurs dans un objet

Un objet peut contenir **n'importe quel type de valeur** JavaScript :

### Strings (chaînes de caractères)

```javascript
const utilisateur = {
  nom: "Dupont",
  email: "dupont@example.com",
  ville: "Lyon"
};
```

### Numbers (nombres)

```javascript
const produit = {
  prix: 29.99,
  stock: 150,
  reduction: 0.15
};
```

### Booleans (booléens)

```javascript
const compte = {
  actif: true,
  premium: false,
  emailVerifie: true
};
```

### Null et undefined

```javascript
const profil = {
  avatar: null,           // Pas encore d'avatar
  dernierLogin: undefined // Jamais connecté
};
```

### Tableaux

```javascript
const etudiant = {
  nom: "Alice",
  notes: [15, 18, 12, 16],
  matieres: ["Math", "Physique", "Français"]
};
```

### Autres objets (objets imbriqués)

Un objet peut contenir d'autres objets :

```javascript
const entreprise = {
  nom: "TechCorp",
  adresse: {
    rue: "12 rue de la Paix",
    ville: "Paris",
    codePostal: "75001"
  },
  contact: {
    email: "contact@techcorp.fr",
    telephone: "01 23 45 67 89"
  }
};
```

### Fonctions (méthodes)

Un objet peut contenir des fonctions, qu'on appelle alors des **méthodes** :

```javascript
const calculatrice = {
  marque: "Casio",
  additionner: function(a, b) {
    return a + b;
  }
};
```

> **Note :** Nous verrons une syntaxe plus moderne pour les méthodes dans la section suivante (5.7.2).

## Exemples concrets

### Exemple 1 : Carte d'identité

```javascript
const personne = {
  nom: "Dubois",
  prenom: "Marie",
  age: 32,
  nationalite: "Française",
  permis: true
};
```

### Exemple 2 : Produit e-commerce

```javascript
const article = {
  id: 1001,
  nom: "Chaussures de running",
  marque: "Nike",
  prix: 89.99,
  couleurs: ["noir", "blanc", "rouge"],
  tailles: [38, 39, 40, 41, 42],
  enStock: true,
  promotion: false
};
```

### Exemple 3 : Configuration d'application

```javascript
const config = {
  langue: "fr",
  theme: "sombre",
  notifications: true,
  volume: 75,
  qualite: "HD"
};
```

### Exemple 4 : Données utilisateur complexes

```javascript
const utilisateur = {
  id: 42,
  pseudo: "codeur_pro",
  email: "codeur@example.com",
  dateInscription: "2024-01-15",
  profil: {
    avatar: "avatar.jpg",
    bio: "Développeur passionné",
    localisation: "France"
  },
  preferences: {
    theme: "clair",
    notifications: true,
    langue: "fr"
  },
  statistiques: {
    publications: 127,
    abonnes: 1542,
    abonnements: 89
  }
};
```

## Pourquoi utiliser des objets ?

### 1. Organisation du code

Au lieu de :
```javascript
const nomUtilisateur = "Alice";
const ageUtilisateur = 25;
const emailUtilisateur = "alice@example.com";
const villeUtilisateur = "Paris";
```

On peut écrire :
```javascript
const utilisateur = {
  nom: "Alice",
  age: 25,
  email: "alice@example.com",
  ville: "Paris"
};
```

**Avantages :**
- Plus lisible
- Plus facile à maintenir
- Logiquement regroupé

### 2. Passage de données

Les objets facilitent le passage de plusieurs informations à une fonction :

```javascript
function afficherProfil(utilisateur) {
  console.log(`${utilisateur.nom}, ${utilisateur.age} ans`);
  console.log(`Email: ${utilisateur.email}`);
}

const user = {
  nom: "Bob",
  age: 30,
  email: "bob@example.com"
};

afficherProfil(user);
```

### 3. Représentation de données réelles

Les objets permettent de modéliser des entités du monde réel de façon naturelle :

```javascript
const voiture = {
  marque: "Peugeot",
  modele: "308",
  annee: 2022,
  couleur: "bleu",
  kilometrage: 15000,
  carburant: "essence"
};
```

## Objets et variables

### Déclaration avec const (recommandé)

```javascript
const utilisateur = {
  nom: "Alice",
  age: 25
};
```

**Important :** Même si on utilise `const`, on peut modifier les propriétés de l'objet (nous verrons cela dans les prochaines sections). Le `const` empêche seulement de réaffecter complètement l'objet.

### Déclaration avec let

```javascript
let config = {
  mode: "production"
};

// Plus tard, on peut réaffecter complètement l'objet
config = {
  mode: "development"
};
```

## Bonnes pratiques

### 1. Nommage cohérent

```javascript
// ✅ Bon : nom descriptif au singulier
const utilisateur = {
  nom: "Alice",
  email: "alice@example.com"
};

// ❌ Éviter : nom vague
const data = {
  nom: "Alice",
  email: "alice@example.com"
};
```

### 2. Indentation et lisibilité

```javascript
// ✅ Bon : bien indenté et aéré
const produit = {
  nom: "Ordinateur portable",
  prix: 899,
  specifications: {
    processeur: "Intel i7",
    ram: "16 GB",
    stockage: "512 GB SSD"
  }
};

// ❌ Difficile à lire
const produit = {nom: "Ordinateur portable", prix: 899, specifications: {processeur: "Intel i7", ram: "16 GB", stockage: "512 GB SSD"}};
```

### 3. Regroupement logique

Regroupez les propriétés liées ensemble :

```javascript
const employe = {
  // Informations personnelles
  nom: "Martin",
  prenom: "Sophie",
  age: 32,

  // Informations professionnelles
  poste: "Développeuse",
  service: "IT",
  salaire: 45000,

  // Contact
  email: "s.martin@entreprise.fr",
  telephone: "01 23 45 67 89"
};
```

### 4. Virgule finale (trailing comma)

En JavaScript moderne, il est recommandé d'ajouter une virgule après la dernière propriété :

```javascript
const config = {
  option1: true,
  option2: false,
  option3: "valeur", // ✅ Virgule finale
};
```

**Avantage :** Facilite l'ajout de nouvelles propriétés et rend les diffs Git plus propres.

## Points clés à retenir

1. **Un objet littéral** se crée avec des accolades `{}`
2. **Les propriétés** sont des paires clé-valeur séparées par `:`
3. **Plusieurs propriétés** sont séparées par des virgules
4. **Les valeurs** peuvent être de n'importe quel type JavaScript
5. **Les objets** peuvent être **imbriqués** (contenir d'autres objets)
6. **Utilisez `const`** pour déclarer vos objets par défaut
7. **Les objets** permettent de regrouper logiquement des données liées

## Ce qui vient ensuite

Maintenant que vous savez créer des objets littéraux, les prochaines sections vous apprendront à :
- Utiliser la syntaxe raccourcie ES6 pour créer des objets plus rapidement
- Accéder aux propriétés d'un objet et les modifier
- Utiliser le destructuring pour extraire des propriétés
- Créer des méthodes (fonctions dans les objets)
- Comprendre le mot-clé `this`

Les objets sont au cœur de JavaScript. Maîtriser leur création est la première étape vers une programmation orientée objet efficace !

⏭️ [Syntaxe raccourcie pour propriétés et méthodes (ES6)](/05-javascript-moderne-fondamentaux/07-objets-modernes/02-syntaxe-raccourcie.md)
