🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.9 - Constructeurs et new (introduction)

## Introduction

Jusqu'à présent, nous avons créé des objets avec la syntaxe d'**objets littéraux** `{}`. Cette méthode fonctionne bien pour créer un ou quelques objets, mais que faire si on veut créer **des dizaines ou des centaines d'objets similaires** ?

Les **constructeurs** sont des fonctions spéciales qui servent de "moules" ou de "blueprints" pour créer des objets. Ils permettent de créer facilement plusieurs objets avec la même structure.

### Analogie

Pensez à un moule à gâteau :
- Le **moule** = le constructeur
- Chaque **gâteau** produit = un objet créé avec le constructeur
- Tous les gâteaux ont la **même forme** mais peuvent avoir des **ingrédients différents**

## 1. Le problème : créer plusieurs objets similaires

Imaginons qu'on veuille créer plusieurs utilisateurs :

```javascript
// ❌ Répétitif : créer chaque objet manuellement
const utilisateur1 = {
  nom: "Alice",
  age: 28,
  email: "alice@example.com",
  sePresenter() {
    return `Je suis ${this.nom}, ${this.age} ans`;
  }
};

const utilisateur2 = {
  nom: "Bob",
  age: 32,
  email: "bob@example.com",
  sePresenter() {
    return `Je suis ${this.nom}, ${this.age} ans`;
  }
};

const utilisateur3 = {
  nom: "Charlie",
  age: 25,
  email: "charlie@example.com",
  sePresenter() {
    return `Je suis ${this.nom}, ${this.age} ans`;
  }
};

// ... et ainsi de suite pour 100 utilisateurs ?
```

**Problèmes :**
- Code répétitif (violation du principe DRY)
- Erreurs faciles si on oublie une propriété
- Difficile à maintenir

## 2. La solution : les constructeurs

Un **constructeur** est une fonction qui crée et initialise des objets. Par convention, son nom commence par une **majuscule**.

### Syntaxe de base

```javascript
// Définir un constructeur
function Utilisateur(nom, age, email) {
  this.nom = nom;
  this.age = age;
  this.email = email;
  this.sePresenter = function() {
    return `Je suis ${this.nom}, ${this.age} ans`;
  };
}

// Créer des objets avec le constructeur
const utilisateur1 = new Utilisateur("Alice", 28, "alice@example.com");
const utilisateur2 = new Utilisateur("Bob", 32, "bob@example.com");
const utilisateur3 = new Utilisateur("Charlie", 25, "charlie@example.com");

console.log(utilisateur1.nom);           // "Alice"
console.log(utilisateur2.sePresenter()); // "Je suis Bob, 32 ans"
```

**Beaucoup plus simple !** On a défini la structure une seule fois et on peut créer autant d'objets qu'on veut.

## 3. Le mot-clé `new`

Le mot-clé `new` est **essentiel** pour créer un objet avec un constructeur. Il fait quatre choses automatiquement :

1. **Crée** un nouvel objet vide `{}`
2. **Lie** cet objet à `this` dans le constructeur
3. **Exécute** le code du constructeur (qui ajoute propriétés et méthodes)
4. **Retourne** automatiquement le nouvel objet

### Avec et sans `new`

```javascript
function Voiture(marque, modele) {
  this.marque = marque;
  this.modele = modele;
}

// ✅ Avec new : fonctionne correctement
const voiture1 = new Voiture("Peugeot", "308");
console.log(voiture1);  // Voiture { marque: "Peugeot", modele: "308" }

// ❌ Sans new : ne crée pas d'objet
const voiture2 = Voiture("Renault", "Clio");
console.log(voiture2);  // undefined
```

**Important :** Oubliez jamais le mot-clé `new` !

## 4. Comment fonctionne `this` dans les constructeurs

Dans un constructeur, `this` fait référence au **nouvel objet en cours de création**.

### Visualisation

```javascript
function Personne(nom, age) {
  // À ce moment, new a créé un objet vide : {}
  // this pointe vers cet objet

  this.nom = nom;      // Ajoute la propriété nom
  this.age = age;      // Ajoute la propriété age

  // À la fin, l'objet est automatiquement retourné
}

const alice = new Personne("Alice", 28);
// alice = { nom: "Alice", age: 28 }
```

### Étape par étape

```javascript
function Produit(nom, prix) {
  console.log("1. this au début:", this);  // {}

  this.nom = nom;
  console.log("2. Après ajout de nom:", this);  // { nom: "..." }

  this.prix = prix;
  console.log("3. Après ajout de prix:", this);  // { nom: "...", prix: ... }

  // Pas besoin de return, c'est automatique
}

const produit = new Produit("Ordinateur", 899);
console.log("4. Objet final:", produit);
// { nom: "Ordinateur", prix: 899 }
```

## 5. Convention de nommage

Par convention, les constructeurs commencent par une **majuscule** :

```javascript
// ✅ Bon : majuscule pour les constructeurs
function Utilisateur(nom) {
  this.nom = nom;
}

function Voiture(marque) {
  this.marque = marque;
}

function CompteBancaire(titulaire) {
  this.titulaire = titulaire;
}

// ❌ À éviter : minuscule (confusion avec fonction normale)
function utilisateur(nom) {
  this.nom = nom;
}
```

**Pourquoi ?** Cela aide à identifier immédiatement qu'une fonction est un constructeur.

## 6. Ajouter des méthodes dans le constructeur

On peut ajouter des méthodes directement dans le constructeur :

```javascript
function Rectangle(largeur, hauteur) {
  // Propriétés
  this.largeur = largeur;
  this.hauteur = hauteur;

  // Méthodes
  this.calculerAire = function() {
    return this.largeur * this.hauteur;
  };

  this.calculerPerimetre = function() {
    return 2 * (this.largeur + this.hauteur);
  };

  this.estCarre = function() {
    return this.largeur === this.hauteur;
  };
}

const rect1 = new Rectangle(10, 5);
console.log(rect1.calculerAire());      // 50
console.log(rect1.calculerPerimetre()); // 30
console.log(rect1.estCarre());          // false

const rect2 = new Rectangle(8, 8);
console.log(rect2.estCarre());          // true
```

## 7. Exemples pratiques

### Exemple 1 : Gestionnaire de tâches

```javascript
function Tache(titre, priorite = "normale") {
  this.id = Math.random().toString(36).substr(2, 9);
  this.titre = titre;
  this.priorite = priorite;
  this.terminee = false;
  this.dateCreation = new Date();

  this.terminer = function() {
    this.terminee = true;
    console.log(`Tâche terminée: ${this.titre}`);
  };

  this.afficher = function() {
    const statut = this.terminee ? "✓" : "○";
    console.log(`${statut} [${this.priorite}] ${this.titre}`);
  };
}

// Créer plusieurs tâches
const tache1 = new Tache("Faire les courses", "haute");
const tache2 = new Tache("Apprendre JavaScript");
const tache3 = new Tache("Appeler le dentiste", "haute");

tache1.afficher();  // "○ [haute] Faire les courses"
tache2.afficher();  // "○ [normale] Apprendre JavaScript"

tache1.terminer();  // "Tâche terminée: Faire les courses"
tache1.afficher();  // "✓ [haute] Faire les courses"
```

### Exemple 2 : Compte bancaire

```javascript
function CompteBancaire(titulaire, soldeInitial = 0) {
  this.titulaire = titulaire;
  this.solde = soldeInitial;
  this.historique = [];

  this.deposer = function(montant) {
    if (montant <= 0) {
      console.log("Montant invalide");
      return false;
    }

    this.solde += montant;
    this.historique.push({
      type: "dépôt",
      montant: montant,
      date: new Date()
    });
    console.log(`Dépôt de ${montant}€ effectué`);
    return true;
  };

  this.retirer = function(montant) {
    if (montant <= 0) {
      console.log("Montant invalide");
      return false;
    }

    if (montant > this.solde) {
      console.log("Solde insuffisant");
      return false;
    }

    this.solde -= montant;
    this.historique.push({
      type: "retrait",
      montant: montant,
      date: new Date()
    });
    console.log(`Retrait de ${montant}€ effectué`);
    return true;
  };

  this.afficherSolde = function() {
    console.log(`Compte de ${this.titulaire}: ${this.solde}€`);
  };
}

// Créer plusieurs comptes
const compteAlice = new CompteBancaire("Alice Martin", 1000);
const compteBob = new CompteBancaire("Bob Dupont", 500);

compteAlice.afficherSolde();  // "Compte de Alice Martin: 1000€"
compteAlice.deposer(500);     // "Dépôt de 500€ effectué"
compteAlice.retirer(200);     // "Retrait de 200€ effectué"
compteAlice.afficherSolde();  // "Compte de Alice Martin: 1300€"

compteBob.afficherSolde();    // "Compte de Bob Dupont: 500€"
```

### Exemple 3 : Produit e-commerce

```javascript
function Produit(nom, prix, stock) {
  this.id = Date.now() + Math.random();
  this.nom = nom;
  this.prix = prix;
  this.stock = stock;

  this.estDisponible = function() {
    return this.stock > 0;
  };

  this.appliquerReduction = function(pourcentage) {
    if (pourcentage < 0 || pourcentage > 100) {
      console.log("Pourcentage invalide");
      return false;
    }

    this.prix *= (1 - pourcentage / 100);
    console.log(`Réduction de ${pourcentage}% appliquée`);
    return true;
  };

  this.ajusterStock = function(quantite) {
    this.stock += quantite;
    console.log(`Stock ajusté: ${this.stock}`);
  };

  this.afficher = function() {
    const dispo = this.estDisponible() ? "En stock" : "Rupture";
    console.log(`${this.nom} - ${this.prix.toFixed(2)}€ (${dispo})`);
  };
}

const produit1 = new Produit("Ordinateur portable", 899, 15);
const produit2 = new Produit("Souris", 29.99, 0);

produit1.afficher();  // "Ordinateur portable - 899.00€ (En stock)"
produit2.afficher();  // "Souris - 29.99€ (Rupture)"

produit1.appliquerReduction(10);
produit1.afficher();  // "Ordinateur portable - 809.10€ (En stock)"
```

### Exemple 4 : Minuteur

```javascript
function Minuteur(nom) {
  this.nom = nom;
  this.secondes = 0;
  this.enMarche = false;
  this.intervalId = null;

  this.demarrer = function() {
    if (this.enMarche) {
      console.log(`${this.nom} déjà en marche`);
      return;
    }

    this.enMarche = true;
    console.log(`${this.nom} démarré`);

    // Utiliser une arrow function pour garder le contexte
    this.intervalId = setInterval(() => {
      this.secondes++;
      console.log(`${this.nom}: ${this.secondes}s`);
    }, 1000);
  };

  this.arreter = function() {
    if (!this.enMarche) {
      console.log(`${this.nom} déjà arrêté`);
      return;
    }

    clearInterval(this.intervalId);
    this.enMarche = false;
    console.log(`${this.nom} arrêté à ${this.secondes}s`);
  };

  this.reinitialiser = function() {
    this.arreter();
    this.secondes = 0;
    console.log(`${this.nom} réinitialisé`);
  };
}

const timer1 = new Minuteur("Timer principal");
const timer2 = new Minuteur("Timer secondaire");

// timer1.demarrer();
// Après quelques secondes...
// timer1.arreter();
// timer1.reinitialiser();
```

## 8. Vérifier le type d'un objet

On peut vérifier si un objet a été créé par un constructeur spécifique avec `instanceof` :

```javascript
function Personne(nom) {
  this.nom = nom;
}

function Voiture(marque) {
  this.marque = marque;
}

const alice = new Personne("Alice");
const voiture = new Voiture("Peugeot");

console.log(alice instanceof Personne);    // true
console.log(alice instanceof Voiture);     // false
console.log(voiture instanceof Voiture);   // true
console.log(voiture instanceof Personne);  // false
```

### Exemple pratique

```javascript
function validerUtilisateur(obj) {
  if (obj instanceof Utilisateur) {
    console.log("C'est bien un utilisateur");
    return true;
  } else {
    console.log("Ce n'est pas un utilisateur");
    return false;
  }
}

function Utilisateur(nom) {
  this.nom = nom;
}

const user = new Utilisateur("Alice");
const objet = { nom: "Bob" };

validerUtilisateur(user);   // "C'est bien un utilisateur"
validerUtilisateur(objet);  // "Ce n'est pas un utilisateur"
```

## 9. Propriétés par défaut

On peut définir des valeurs par défaut dans le constructeur :

```javascript
function Configuration(options = {}) {
  this.theme = options.theme || "clair";
  this.langue = options.langue || "fr";
  this.notifications = options.notifications !== undefined
    ? options.notifications
    : true;
  this.volume = options.volume || 50;
}

// Avec toutes les options
const config1 = new Configuration({
  theme: "sombre",
  langue: "en",
  notifications: false,
  volume: 75
});

// Avec options partielles (valeurs par défaut utilisées)
const config2 = new Configuration({
  theme: "sombre"
});

console.log(config2.langue);         // "fr" (valeur par défaut)
console.log(config2.notifications);  // true (valeur par défaut)
```

## 10. Le problème de duplication des méthodes

Chaque objet créé a sa **propre copie** des méthodes, ce qui peut gaspiller de la mémoire :

```javascript
function Personne(nom) {
  this.nom = nom;

  this.saluer = function() {
    return `Bonjour, je suis ${this.nom}`;
  };
}

const alice = new Personne("Alice");
const bob = new Personne("Bob");

// Chaque objet a SA PROPRE copie de la méthode saluer
console.log(alice.saluer === bob.saluer);  // false

// Si on crée 1000 personnes, on a 1000 copies de la même méthode !
```

### Solution : le prototype (aperçu)

On peut partager les méthodes entre tous les objets via le **prototype** :

```javascript
function Personne(nom) {
  this.nom = nom;
}

// Ajouter la méthode au prototype
Personne.prototype.saluer = function() {
  return `Bonjour, je suis ${this.nom}`;
};

const alice = new Personne("Alice");
const bob = new Personne("Bob");

// Maintenant ils partagent la même méthode
console.log(alice.saluer === bob.saluer);  // true

// Mais chaque objet a toujours ses propres propriétés
console.log(alice.nom);  // "Alice"
console.log(bob.nom);    // "Bob"
```

**Note :** Nous verrons le prototype plus en détail dans des sections avancées. Les classes ES6 (section suivante) gèrent cela automatiquement.

## 11. Constructeurs vs Objets littéraux

### Quand utiliser un constructeur ?

```javascript
// ✅ Constructeur : créer PLUSIEURS objets similaires
function Utilisateur(nom, email) {
  this.nom = nom;
  this.email = email;
}

const users = [
  new Utilisateur("Alice", "alice@example.com"),
  new Utilisateur("Bob", "bob@example.com"),
  new Utilisateur("Charlie", "charlie@example.com")
];
```

### Quand utiliser un objet littéral ?

```javascript
// ✅ Objet littéral : créer UN objet unique
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000,
  retries: 3
};

const singleton = {
  instance: null,
  getInstance() {
    // ...
  }
};
```

### Tableau comparatif

| Critère | Objet littéral | Constructeur |
|---------|----------------|--------------|
| Syntaxe | `const obj = {}` | `function Obj() {}` + `new` |
| Usage | Objet unique | Plusieurs objets similaires |
| Réutilisation | Difficile | Facile |
| Mémoire | Efficace | Peut gaspiller (méthodes dupliquées) |
| Lisibilité | Simple | Plus formel |

## 12. Retourner explicitement un objet

Par défaut, un constructeur retourne automatiquement `this`. Mais on peut retourner un autre objet :

```javascript
function Personne(nom) {
  this.nom = nom;

  // ⚠️ Retourner explicitement un autre objet
  return {
    prenom: nom,
    age: 25
  };
}

const personne = new Personne("Alice");
console.log(personne);  // { prenom: "Alice", age: 25 }
console.log(personne.nom);  // undefined
```

**Note :** C'est rare et généralement déconseillé. Laissez le constructeur retourner automatiquement `this`.

## 13. Bonnes pratiques

### 1. Majuscule pour les constructeurs

```javascript
// ✅ Bon
function Utilisateur(nom) {
  this.nom = nom;
}

// ❌ Mauvais
function utilisateur(nom) {
  this.nom = nom;
}
```

### 2. Toujours utiliser `new`

```javascript
// ✅ Bon
const user = new Utilisateur("Alice");

// ❌ Oubli de new
const user = Utilisateur("Alice");  // undefined
```

### 3. Valider les paramètres

```javascript
function Utilisateur(nom, age) {
  if (!nom || typeof nom !== 'string') {
    throw new Error("Nom invalide");
  }

  if (age < 0 || age > 150) {
    throw new Error("Âge invalide");
  }

  this.nom = nom;
  this.age = age;
}
```

### 4. Utiliser des valeurs par défaut

```javascript
function Produit(nom, prix = 0, stock = 0) {
  this.nom = nom;
  this.prix = prix;
  this.stock = stock;
}

const prod = new Produit("Article");
console.log(prod.prix);   // 0
console.log(prod.stock);  // 0
```

### 5. Documenter le constructeur

```javascript
/**
 * Crée un nouveau compte bancaire
 * @param {string} titulaire - Nom du titulaire
 * @param {number} soldeInitial - Solde de départ (défaut: 0)
 */
function CompteBancaire(titulaire, soldeInitial = 0) {
  this.titulaire = titulaire;
  this.solde = soldeInitial;
}
```

## 14. Pièges à éviter

### Piège 1 : Oublier `new`

```javascript
function Voiture(marque) {
  this.marque = marque;
}

// ❌ Sans new
const voiture = Voiture("Peugeot");
console.log(voiture);  // undefined

// ✅ Avec new
const voiture = new Voiture("Peugeot");
console.log(voiture);  // Voiture { marque: "Peugeot" }
```

### Piège 2 : Arrow function comme constructeur

```javascript
// ❌ Les arrow functions ne peuvent PAS être des constructeurs
const Personne = (nom) => {
  this.nom = nom;
};

// const alice = new Personne("Alice");  // TypeError

// ✅ Utiliser une fonction normale
function Personne(nom) {
  this.nom = nom;
}
```

### Piège 3 : Méthodes dupliquées

```javascript
// ⚠️ Chaque objet a sa propre copie des méthodes
function Personne(nom) {
  this.nom = nom;
  this.saluer = function() {
    return `Bonjour ${this.nom}`;
  };
}

// ✅ Mieux : utiliser le prototype (ou les classes ES6)
function Personne(nom) {
  this.nom = nom;
}
Personne.prototype.saluer = function() {
  return `Bonjour ${this.nom}`;
};
```

### Piège 4 : Confusion avec les fonctions normales

```javascript
// Fonction normale
function calculer(a, b) {
  return a + b;
}
const resultat = calculer(5, 3);  // Pas de new

// Constructeur
function Calculatrice() {
  this.total = 0;
}
const calc = new Calculatrice();  // Avec new
```

## 15. Protection contre l'oubli de `new`

On peut protéger un constructeur contre l'oubli de `new` :

```javascript
function Utilisateur(nom) {
  // Vérifier si appelé avec new
  if (!(this instanceof Utilisateur)) {
    return new Utilisateur(nom);
  }

  this.nom = nom;
}

// Fonctionne même sans new
const user1 = new Utilisateur("Alice");    // Avec new
const user2 = Utilisateur("Bob");          // Sans new (corrigé automatiquement)

console.log(user1 instanceof Utilisateur);  // true
console.log(user2 instanceof Utilisateur);  // true
```

## 16. Exemple complet : Application de gestion

```javascript
function GestionnaireTaches() {
  this.taches = [];
  this.prochainId = 1;

  this.ajouter = function(titre, priorite) {
    const tache = {
      id: this.prochainId++,
      titre: titre,
      priorite: priorite || "normale",
      terminee: false
    };

    this.taches.push(tache);
    console.log(`Tâche ajoutée: ${titre}`);
    return tache.id;
  };

  this.terminer = function(id) {
    const tache = this.taches.find(t => t.id === id);

    if (tache) {
      tache.terminee = true;
      console.log(`Tâche terminée: ${tache.titre}`);
      return true;
    }

    console.log("Tâche non trouvée");
    return false;
  };

  this.lister = function() {
    console.log("=== Liste des tâches ===");
    this.taches.forEach(tache => {
      const statut = tache.terminee ? "✓" : "○";
      console.log(`${statut} [${tache.priorite}] ${tache.titre}`);
    });
  };

  this.statistiques = function() {
    const total = this.taches.length;
    const terminees = this.taches.filter(t => t.terminee).length;

    return {
      total: total,
      terminees: terminees,
      enCours: total - terminees
    };
  };
}

// Utilisation
const gestionnaire = new GestionnaireTaches();

gestionnaire.ajouter("Faire les courses", "haute");
gestionnaire.ajouter("Apprendre JavaScript");
gestionnaire.ajouter("Appeler le dentiste", "haute");

gestionnaire.lister();

gestionnaire.terminer(1);
gestionnaire.terminer(3);

gestionnaire.lister();

const stats = gestionnaire.statistiques();
console.log(stats);
// { total: 3, terminees: 2, enCours: 1 }
```

## 17. Différence avec les classes ES6

Les constructeurs sont l'ancienne façon de créer des objets en JavaScript. ES6 a introduit les **classes**, qui sont une syntaxe plus moderne et plus claire :

```javascript
// Constructeur classique
function Personne(nom, age) {
  this.nom = nom;
  this.age = age;
}
Personne.prototype.saluer = function() {
  return `Bonjour, je suis ${this.nom}`;
};

// Classe ES6 (équivalent moderne)
class Personne {
  constructor(nom, age) {
    this.nom = nom;
    this.age = age;
  }

  saluer() {
    return `Bonjour, je suis ${this.nom}`;
  }
}

// Utilisation identique
const alice = new Personne("Alice", 28);
```

**Les classes ES6 sont plus claires et recommandées en JavaScript moderne.** Nous les verrons dans la section suivante.

## Points clés à retenir

1. **Constructeur** = fonction qui crée des objets (commence par une majuscule)
2. **`new`** est obligatoire pour créer un objet avec un constructeur
3. **`this`** dans un constructeur = le nouvel objet en cours de création
4. **Constructeurs** = idéal pour créer plusieurs objets similaires
5. **Objets littéraux** = idéal pour un objet unique
6. **`instanceof`** vérifie si un objet a été créé par un constructeur
7. **Méthodes dans le constructeur** = dupliquées pour chaque objet
8. **Prototype** = permet de partager les méthodes (plus efficace)
9. **Classes ES6** = syntaxe moderne recommandée

## Schéma mental

```
AVANT (objets littéraux)
const obj1 = { nom: "Alice", ... }
const obj2 = { nom: "Bob", ... }
const obj3 = { nom: "Charlie", ... }
❌ Répétitif

APRÈS (constructeur)
function Personne(nom) {
  this.nom = nom;
}
const obj1 = new Personne("Alice");
const obj2 = new Personne("Bob");
const obj3 = new Personne("Charlie");
✅ DRY (Don't Repeat Yourself)
```

## Ce qui vient ensuite

Dans la prochaine section, vous découvrirez les **classes ES6**, qui sont :
- Une syntaxe plus moderne et plus claire
- La façon recommandée de créer des objets en JavaScript moderne
- Plus proches de la POO traditionnelle (Java, C++, Python)
- Basées sur les constructeurs et prototypes, mais beaucoup plus lisibles

Les constructeurs sont la base, mais les classes ES6 sont l'avenir en JavaScript !

⏭️ [Classes ES6 (introduction simple)](/05-javascript-moderne-fondamentaux/07-objets-modernes/10-classes-es6.md)
