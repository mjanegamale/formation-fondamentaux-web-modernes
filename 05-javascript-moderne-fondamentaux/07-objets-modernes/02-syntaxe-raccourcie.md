🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.2 - Syntaxe raccourcie pour propriétés et méthodes (ES6) 🆕

## Introduction

ES6 (ECMAScript 2015) a introduit des **syntaxes raccourcies** qui rendent la création d'objets plus concise et plus lisible. Ces améliorations permettent d'écrire moins de code tout en restant clair et expressif.

Dans cette section, nous allons découvrir deux simplifications majeures :
1. **La syntaxe raccourcie pour les propriétés** (Property Shorthand)
2. **La syntaxe raccourcie pour les méthodes** (Method Shorthand)

> **Note :** Ces syntaxes sont désormais **standard** en JavaScript moderne et largement utilisées dans le code professionnel.

## 1. Syntaxe raccourcie pour les propriétés

### Le problème avant ES6

Avant ES6, quand on voulait créer un objet à partir de variables existantes, on devait répéter les noms :

```javascript
const nom = "Alice";
const age = 28;
const ville = "Paris";

// Syntaxe classique (avant ES6)
const personne = {
  nom: nom,        // répétition du mot "nom"
  age: age,        // répétition du mot "age"
  ville: ville     // répétition du mot "ville"
};
```

**Problème :** C'est redondant. On écrit deux fois le même mot !

### La solution ES6

Quand le **nom de la variable** est identique au **nom de la propriété**, on peut écrire simplement :

```javascript
const nom = "Alice";
const age = 28;
const ville = "Paris";

// Syntaxe raccourcie ES6 ✨
const personne = {
  nom,    // équivalent à nom: nom
  age,    // équivalent à age: age
  ville   // équivalent à ville: ville
};

console.log(personne);
// { nom: "Alice", age: 28, ville: "Paris" }
```

**Règle simple :** Si `cle: valeur` ont le même nom, écrivez juste le nom une fois !

### Exemples pratiques

#### Exemple 1 : Données de formulaire

```javascript
// Récupération des valeurs d'un formulaire
const email = "user@example.com";
const motDePasse = "secret123";
const seSouvenir = true;

// Création de l'objet de connexion
const donneesCo = {
  email,
  motDePasse,
  seSouvenir
};

console.log(donneesCo);
// {
//   email: "user@example.com",
//   motDePasse: "secret123",
//   seSouvenir: true
// }
```

#### Exemple 2 : Configuration d'API

```javascript
const apiUrl = "https://api.example.com";
const timeout = 5000;
const retry = 3;

const config = {
  apiUrl,
  timeout,
  retry
};
```

#### Exemple 3 : Données de produit

```javascript
const titre = "Ordinateur portable";
const prix = 899;
const stock = 42;
const disponible = true;

const produit = {
  titre,
  prix,
  stock,
  disponible
};
```

### Mélanger syntaxe raccourcie et normale

On peut **combiner** les deux syntaxes dans le même objet :

```javascript
const nom = "Sophie";
const age = 32;

const utilisateur = {
  nom,              // raccourci
  age,              // raccourci
  role: "admin",    // syntaxe normale
  actif: true       // syntaxe normale
};

console.log(utilisateur);
// {
//   nom: "Sophie",
//   age: 32,
//   role: "admin",
//   actif: true
// }
```

### Cas d'usage typiques

#### Retour de fonction

```javascript
function creerUtilisateur(nom, email) {
  const id = Math.random();
  const dateCreation = new Date();

  return {
    id,
    nom,
    email,
    dateCreation
  };
}

const user = creerUtilisateur("Alice", "alice@example.com");
```

#### Passage de paramètres

```javascript
function sauvegarderConfig(theme, langue, notifications) {
  const config = {
    theme,
    langue,
    notifications,
    version: "2.0"
  };

  // Sauvegarder config...
  console.log("Configuration sauvegardée:", config);
}

sauvegarderConfig("sombre", "fr", true);
```

## 2. Syntaxe raccourcie pour les méthodes

### Rappel : méthodes avant ES6

Une **méthode** est une fonction qui appartient à un objet. Avant ES6, on devait écrire le mot-clé `function` :

```javascript
// Syntaxe classique (avant ES6)
const calculatrice = {
  additionner: function(a, b) {
    return a + b;
  },
  soustraire: function(a, b) {
    return a - b;
  }
};

console.log(calculatrice.additionner(5, 3));  // 8
console.log(calculatrice.soustraire(10, 4));  // 6
```

### La syntaxe raccourcie ES6

ES6 permet d'**omettre** le mot-clé `function` et les deux-points `:` :

```javascript
// Syntaxe raccourcie ES6 ✨
const calculatrice = {
  additionner(a, b) {
    return a + b;
  },
  soustraire(a, b) {
    return a - b;
  }
};

console.log(calculatrice.additionner(5, 3));  // 8
console.log(calculatrice.soustraire(10, 4));  // 6
```

**Plus court, plus lisible !**

### Comparaison avant/après

```javascript
// ❌ Avant ES6 : verbeux
const personne = {
  nom: "Alice",
  saluer: function() {
    return `Bonjour, je suis ${this.nom}`;
  },
  sePresenter: function() {
    return `Je m'appelle ${this.nom}`;
  }
};

// ✅ ES6 : concis et moderne
const personne = {
  nom: "Alice",
  saluer() {
    return `Bonjour, je suis ${this.nom}`;
  },
  sePresenter() {
    return `Je m'appelle ${this.nom}`;
  }
};
```

### Exemples pratiques

#### Exemple 1 : Objet utilisateur avec méthodes

```javascript
const utilisateur = {
  nom: "Bob",
  age: 25,
  email: "bob@example.com",

  // Méthodes avec syntaxe raccourcie
  sePresenter() {
    return `Je suis ${this.nom}, ${this.age} ans`;
  },

  obtenirEmail() {
    return this.email;
  },

  estMajeur() {
    return this.age >= 18;
  }
};

console.log(utilisateur.sePresenter());  // "Je suis Bob, 25 ans"
console.log(utilisateur.estMajeur());    // true
```

#### Exemple 2 : Gestionnaire de tâches

```javascript
const gestionnaireTaches = {
  taches: [],

  ajouter(tache) {
    this.taches.push(tache);
    console.log(`Tâche ajoutée: ${tache}`);
  },

  supprimer(index) {
    const tache = this.taches.splice(index, 1);
    console.log(`Tâche supprimée: ${tache}`);
  },

  lister() {
    console.log("Liste des tâches:");
    this.taches.forEach((tache, i) => {
      console.log(`${i + 1}. ${tache}`);
    });
  },

  compter() {
    return this.taches.length;
  }
};

gestionnaireTaches.ajouter("Faire les courses");
gestionnaireTaches.ajouter("Apprendre JavaScript");
gestionnaireTaches.lister();
```

#### Exemple 3 : Compte bancaire

```javascript
const compteBancaire = {
  titulaire: "Marie Dupont",
  solde: 1000,

  deposer(montant) {
    this.solde += montant;
    return `Nouveau solde: ${this.solde}€`;
  },

  retirer(montant) {
    if (montant > this.solde) {
      return "Solde insuffisant";
    }
    this.solde -= montant;
    return `Nouveau solde: ${this.solde}€`;
  },

  afficherSolde() {
    return `Solde de ${this.titulaire}: ${this.solde}€`;
  }
};

console.log(compteBancaire.deposer(500));    // "Nouveau solde: 1500€"
console.log(compteBancaire.retirer(200));    // "Nouveau solde: 1300€"
console.log(compteBancaire.afficherSolde()); // "Solde de Marie Dupont: 1300€"
```

## 3. Combiner les deux syntaxes

On peut utiliser **simultanément** les deux raccourcis dans le même objet :

```javascript
const prenom = "Alice";
const nom = "Martin";
const age = 30;

const personne = {
  // Syntaxe raccourcie pour les propriétés
  prenom,
  nom,
  age,

  // Syntaxe raccourcie pour les méthodes
  nomComplet() {
    return `${this.prenom} ${this.nom}`;
  },

  sePresenter() {
    return `Je suis ${this.nomComplet()}, ${this.age} ans`;
  },

  anniversaire() {
    this.age++;
    return `Joyeux anniversaire ! Vous avez maintenant ${this.age} ans`;
  }
};

console.log(personne.sePresenter());
// "Je suis Alice Martin, 30 ans"

console.log(personne.anniversaire());
// "Joyeux anniversaire ! Vous avez maintenant 31 ans"
```

## 4. Exemple complet : Application de gestion

Voici un exemple qui combine tous les concepts :

```javascript
function creerProduit(nom, prix, quantite) {
  // Variables locales
  const id = Math.random().toString(36).substr(2, 9);
  const dateCreation = new Date();

  // Objet avec syntaxes raccourcies
  return {
    // Propriétés raccourcies
    id,
    nom,
    prix,
    quantite,
    dateCreation,

    // Méthodes raccourcies
    afficherInfos() {
      return `${this.nom} - ${this.prix}€ (Stock: ${this.quantite})`;
    },

    calculerTotal() {
      return this.prix * this.quantite;
    },

    estDisponible() {
      return this.quantite > 0;
    },

    ajusterStock(ajustement) {
      this.quantite += ajustement;
      return `Nouveau stock: ${this.quantite}`;
    },

    appliquerReduction(pourcentage) {
      const reduction = this.prix * (pourcentage / 100);
      this.prix -= reduction;
      return `Nouveau prix après ${pourcentage}% de réduction: ${this.prix.toFixed(2)}€`;
    }
  };
}

// Utilisation
const produit = creerProduit("Clavier mécanique", 89.99, 15);

console.log(produit.afficherInfos());
// "Clavier mécanique - 89.99€ (Stock: 15)"

console.log(produit.calculerTotal());
// 1349.85

console.log(produit.appliquerReduction(10));
// "Nouveau prix après 10% de réduction: 80.99€"

console.log(produit.ajusterStock(-3));
// "Nouveau stock: 12"
```

## 5. Noms calculés de propriétés (Bonus ES6)

ES6 permet aussi d'utiliser des **expressions** comme noms de propriétés avec des crochets `[]` :

```javascript
const prefixe = "user";
const id = 123;

const objet = {
  [prefixe + "Id"]: id,           // userId: 123
  [prefixe + "Name"]: "Alice",    // userName: "Alice"
  [`${prefixe}Active`]: true      // userActive: true
};

console.log(objet);
// {
//   userId: 123,
//   userName: "Alice",
//   userActive: true
// }
```

### Exemple pratique avec noms calculés

```javascript
function creerObjet(cle, valeur) {
  return {
    [cle]: valeur,
    timestamp: Date.now()
  };
}

const config1 = creerObjet("theme", "sombre");
console.log(config1);
// { theme: "sombre", timestamp: 1701878400000 }

const config2 = creerObjet("langue", "fr");
console.log(config2);
// { langue: "fr", timestamp: 1701878401000 }
```

## 6. Quand utiliser ces syntaxes ?

### ✅ À utiliser systématiquement

Les syntaxes raccourcies sont maintenant **standard** et devraient être utilisées par défaut :

```javascript
// ✅ Bon : syntaxe moderne
const nom = "Alice";
const config = {
  nom,
  afficher() {
    console.log(this.nom);
  }
};

// ❌ Éviter : syntaxe ancienne inutilement verbeuse
const nom = "Alice";
const config = {
  nom: nom,
  afficher: function() {
    console.log(this.nom);
  }
};
```

### Avantages

1. **Code plus court** : Moins de répétitions
2. **Plus lisible** : Réduit le bruit visuel
3. **Standard moderne** : Attendu dans le code professionnel
4. **Moins d'erreurs** : Moins de code = moins de fautes de frappe

## 7. Pièges à éviter

### Piège 1 : Arrow functions vs méthodes raccourcies

Les arrow functions ne sont **pas** la même chose que les méthodes raccourcies :

```javascript
const objet = {
  valeur: 42,

  // ✅ Méthode raccourcie : `this` fonctionne correctement
  methode1() {
    console.log(this.valeur);  // 42
  },

  // ❌ Arrow function : `this` ne pointe pas vers l'objet
  methode2: () => {
    console.log(this.valeur);  // undefined
  }
};

objet.methode1();  // 42
objet.methode2();  // undefined
```

**Règle :** Pour les méthodes d'objets, utilisez la syntaxe raccourcie, **pas les arrow functions**.

### Piège 2 : Variables non définies

La syntaxe raccourcie ne fonctionne que si la variable existe :

```javascript
const nom = "Alice";

// ✅ OK : la variable existe
const objet1 = {
  nom
};

// ❌ ERREUR : age n'est pas défini
const objet2 = {
  nom,
  age  // ReferenceError: age is not defined
};
```

## Points clés à retenir

1. **Syntaxe raccourcie pour propriétés** : Si `cle: valeur` ont le même nom, écrivez juste le nom
   ```javascript
   { nom }  // au lieu de { nom: nom }
   ```

2. **Syntaxe raccourcie pour méthodes** : Omettez `function` et `:`
   ```javascript
   { saluer() {} }  // au lieu de { saluer: function() {} }
   ```

3. **Ces syntaxes sont standards** en JavaScript moderne et largement utilisées

4. **On peut mélanger** syntaxes raccourcies et normales dans le même objet

5. **Pour les méthodes**, utilisez la syntaxe raccourcie, **pas les arrow functions** (problème avec `this`)

6. **Les noms calculés** `[expression]` permettent de créer des propriétés dynamiques

## Comparaison récapitulative

```javascript
// ❌ AVANT ES6 : verbeux
function creerPersonne(nom, age) {
  return {
    nom: nom,
    age: age,
    saluer: function() {
      return "Bonjour, je suis " + nom;
    }
  };
}

// ✅ AVEC ES6 : concis et moderne
function creerPersonne(nom, age) {
  return {
    nom,
    age,
    saluer() {
      return `Bonjour, je suis ${nom}`;
    }
  };
}
```

## Ce qui vient ensuite

Maintenant que vous maîtrisez les syntaxes raccourcies ES6, vous êtes prêt pour :
- Accéder et modifier les propriétés d'objets
- Le destructuring d'objets (encore plus de raccourcis !)
- Le spread operator pour copier et fusionner des objets
- Comprendre `this` en profondeur
- Les classes ES6

Ces syntaxes raccourcies sont **essentielles** en JavaScript moderne. Elles rendent votre code plus professionnel et plus agréable à lire !

⏭️ [Accès aux propriétés : notation point vs crochets](/05-javascript-moderne-fondamentaux/07-objets-modernes/03-acces-proprietes.md)
