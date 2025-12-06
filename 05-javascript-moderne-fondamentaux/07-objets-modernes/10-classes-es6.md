🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.10 - Classes ES6 (introduction simple) 🆕

## Introduction

Les **classes** ont été introduites en ES6 (2015) pour offrir une syntaxe plus claire et plus moderne pour créer des objets. Elles font la même chose que les constructeurs traditionnels, mais avec une syntaxe beaucoup plus lisible et proche de la programmation orientée objet classique (Java, Python, C++).

### Pourquoi les classes ?

Les constructeurs fonctionnent, mais leur syntaxe peut être confuse :

```javascript
// ❌ Constructeur classique : syntaxe dispersée
function Personne(nom, age) {
  this.nom = nom;
  this.age = age;
}
Personne.prototype.saluer = function() {
  return `Bonjour, je suis ${this.nom}`;
};
```

Les classes rendent tout plus clair et organisé :

```javascript
// ✅ Classe ES6 : syntaxe claire et groupée
class Personne {
  constructor(nom, age) {
    this.nom = nom;
    this.age = age;
  }

  saluer() {
    return `Bonjour, je suis ${this.nom}`;
  }
}
```

**Important :** Les classes sont du "sucre syntaxique" (syntactic sugar) autour des constructeurs. En interne, JavaScript utilise toujours les prototypes, mais la syntaxe est beaucoup plus agréable.

## 1. Syntaxe de base

### Créer une classe

```javascript
class NomDeLaClasse {
  constructor(parametres) {
    // Initialisation
  }

  methode1() {
    // Code
  }

  methode2() {
    // Code
  }
}
```

### Premier exemple

```javascript
class Utilisateur {
  constructor(nom, email) {
    this.nom = nom;
    this.email = email;
  }

  sePresenter() {
    return `Je suis ${this.nom} (${this.email})`;
  }
}

// Créer des instances avec new
const alice = new Utilisateur("Alice", "alice@example.com");
const bob = new Utilisateur("Bob", "bob@example.com");

console.log(alice.sePresenter());
// "Je suis Alice (alice@example.com)"

console.log(bob.sePresenter());
// "Je suis Bob (bob@example.com)"
```

**À noter :**
- Le mot-clé `class` pour définir une classe
- Le `constructor` pour initialiser l'objet
- Les méthodes s'écrivent directement (syntaxe raccourcie automatique)
- On utilise toujours `new` pour créer une instance

## 2. Le constructor

Le **constructor** est une méthode spéciale qui est appelée automatiquement quand on crée un nouvel objet avec `new`.

### Rôle du constructor

```javascript
class Voiture {
  constructor(marque, modele, annee) {
    // Initialiser les propriétés
    this.marque = marque;
    this.modele = modele;
    this.annee = annee;
    this.kilometrage = 0;  // Valeur par défaut

    console.log("Nouvelle voiture créée !");
  }
}

const voiture = new Voiture("Peugeot", "308", 2023);
// Affiche : "Nouvelle voiture créée !"

console.log(voiture.marque);       // "Peugeot"
console.log(voiture.kilometrage);  // 0
```

### Constructor avec valeurs par défaut

```javascript
class Produit {
  constructor(nom, prix = 0, stock = 0) {
    this.nom = nom;
    this.prix = prix;
    this.stock = stock;
    this.id = Math.random().toString(36).substr(2, 9);
  }
}

const produit1 = new Produit("Livre", 15.99, 50);
const produit2 = new Produit("Article gratuit");  // Utilise les valeurs par défaut

console.log(produit1.prix);   // 15.99
console.log(produit2.prix);   // 0
console.log(produit2.stock);  // 0
```

### Constructor optionnel

Si vous n'avez pas besoin d'initialiser des propriétés, vous pouvez omettre le constructor :

```javascript
class Compteur {
  // Pas de constructor nécessaire

  incrementer() {
    console.log("Incrémenté !");
  }
}

const compteur = new Compteur();
compteur.incrementer();  // "Incrémenté !"
```

## 3. Méthodes de classe

Les méthodes sont définies directement dans la classe, sans le mot-clé `function` :

```javascript
class Rectangle {
  constructor(largeur, hauteur) {
    this.largeur = largeur;
    this.hauteur = hauteur;
  }

  // Méthodes (pas de "function", pas de virgule entre elles)
  calculerAire() {
    return this.largeur * this.hauteur;
  }

  calculerPerimetre() {
    return 2 * (this.largeur + this.hauteur);
  }

  estCarre() {
    return this.largeur === this.hauteur;
  }

  agrandir(facteur) {
    this.largeur *= facteur;
    this.hauteur *= facteur;
  }

  afficher() {
    console.log(`Rectangle ${this.largeur}x${this.hauteur}`);
  }
}

const rect = new Rectangle(10, 5);

console.log(rect.calculerAire());       // 50
console.log(rect.calculerPerimetre());  // 30
console.log(rect.estCarre());           // false

rect.agrandir(2);
rect.afficher();  // "Rectangle 20x10"
```

### Méthodes qui s'appellent entre elles

```javascript
class CompteBancaire {
  constructor(titulaire, soldeInitial = 0) {
    this.titulaire = titulaire;
    this.solde = soldeInitial;
    this.historique = [];
  }

  deposer(montant) {
    if (montant <= 0) return false;

    this.solde += montant;
    this.ajouterTransaction("Dépôt", montant);
    return true;
  }

  retirer(montant) {
    if (montant <= 0 || montant > this.solde) return false;

    this.solde -= montant;
    this.ajouterTransaction("Retrait", montant);
    return true;
  }

  // Méthode utilisée par les autres
  ajouterTransaction(type, montant) {
    this.historique.push({
      type: type,
      montant: montant,
      date: new Date(),
      solde: this.solde
    });
  }

  afficherSolde() {
    console.log(`Solde de ${this.titulaire}: ${this.solde}€`);
  }
}

const compte = new CompteBancaire("Alice", 1000);
compte.deposer(500);
compte.retirer(200);
compte.afficherSolde();  // "Solde de Alice: 1300€"
```

## 4. Getters et Setters

Les **getters** et **setters** permettent de définir des propriétés calculées ou contrôlées.

### Getters (lecture)

Un getter permet d'accéder à une propriété calculée comme si c'était une propriété normale :

```javascript
class Personne {
  constructor(prenom, nom) {
    this.prenom = prenom;
    this.nom = nom;
  }

  // Getter : s'utilise comme une propriété
  get nomComplet() {
    return `${this.prenom} ${this.nom}`;
  }

  get initiales() {
    return `${this.prenom[0]}.${this.nom[0]}.`;
  }
}

const personne = new Personne("Alice", "Martin");

// Utilisation sans parenthèses (comme une propriété)
console.log(personne.nomComplet);  // "Alice Martin"
console.log(personne.initiales);   // "A.M."
```

### Setters (écriture)

Un setter permet de contrôler comment une propriété est modifiée :

```javascript
class Temperature {
  constructor(celsius) {
    this._celsius = celsius;
  }

  // Getter pour lire
  get celsius() {
    return this._celsius;
  }

  // Setter pour modifier avec validation
  set celsius(valeur) {
    if (valeur < -273.15) {
      console.log("Température invalide (en dessous du zéro absolu)");
      return;
    }
    this._celsius = valeur;
  }

  // Propriété calculée
  get fahrenheit() {
    return (this._celsius * 9/5) + 32;
  }

  set fahrenheit(valeur) {
    this._celsius = (valeur - 32) * 5/9;
  }
}

const temp = new Temperature(25);

console.log(temp.celsius);     // 25
console.log(temp.fahrenheit);  // 77

// Utiliser le setter
temp.celsius = 30;
console.log(temp.celsius);     // 30

temp.fahrenheit = 86;
console.log(temp.celsius);     // 30
```

**Note :** Le préfixe `_` est une convention pour indiquer une propriété "privée" (même si elle reste accessible).

## 5. Exemples pratiques complets

### Exemple 1 : Gestionnaire de tâches

```javascript
class GestionnaireTaches {
  constructor(nom) {
    this.nom = nom;
    this.taches = [];
    this.prochainId = 1;
  }

  ajouter(titre, priorite = "normale") {
    const tache = {
      id: this.prochainId++,
      titre: titre,
      priorite: priorite,
      terminee: false,
      dateCreation: new Date()
    };

    this.taches.push(tache);
    console.log(`✓ Tâche ajoutée: ${titre}`);
    return tache.id;
  }

  terminer(id) {
    const tache = this.taches.find(t => t.id === id);

    if (!tache) {
      console.log("✗ Tâche non trouvée");
      return false;
    }

    tache.terminee = true;
    console.log(`✓ Tâche terminée: ${tache.titre}`);
    return true;
  }

  supprimer(id) {
    const index = this.taches.findIndex(t => t.id === id);

    if (index === -1) {
      console.log("✗ Tâche non trouvée");
      return false;
    }

    const tache = this.taches.splice(index, 1)[0];
    console.log(`✓ Tâche supprimée: ${tache.titre}`);
    return true;
  }

  lister() {
    console.log(`\n=== ${this.nom} ===`);

    if (this.taches.length === 0) {
      console.log("Aucune tâche");
      return;
    }

    this.taches.forEach(tache => {
      const statut = tache.terminee ? "✓" : "○";
      console.log(`${statut} [${tache.priorite}] ${tache.titre}`);
    });
  }

  get nombreTotal() {
    return this.taches.length;
  }

  get nombreTerminees() {
    return this.taches.filter(t => t.terminee).length;
  }

  get nombreEnCours() {
    return this.nombreTotal - this.nombreTerminees;
  }

  afficherStatistiques() {
    console.log(`\n=== Statistiques de ${this.nom} ===`);
    console.log(`Total: ${this.nombreTotal}`);
    console.log(`Terminées: ${this.nombreTerminees}`);
    console.log(`En cours: ${this.nombreEnCours}`);
  }
}

// Utilisation
const gestionnaire = new GestionnaireTaches("Ma liste");

gestionnaire.ajouter("Faire les courses", "haute");
gestionnaire.ajouter("Apprendre JavaScript");
gestionnaire.ajouter("Appeler le dentiste", "haute");
gestionnaire.ajouter("Lire un livre");

gestionnaire.lister();

gestionnaire.terminer(1);
gestionnaire.terminer(3);

gestionnaire.lister();
gestionnaire.afficherStatistiques();
```

### Exemple 2 : Produit e-commerce

```javascript
class Produit {
  constructor(nom, prix, stock) {
    this.id = Date.now() + Math.random();
    this.nom = nom;
    this.prix = prix;
    this.stock = stock;
    this.enPromotion = false;
    this.pourcentageReduction = 0;
  }

  get disponible() {
    return this.stock > 0;
  }

  get prixFinal() {
    if (this.enPromotion) {
      return this.prix * (1 - this.pourcentageReduction / 100);
    }
    return this.prix;
  }

  appliquerReduction(pourcentage) {
    if (pourcentage < 0 || pourcentage > 100) {
      console.log("Pourcentage invalide");
      return false;
    }

    this.enPromotion = true;
    this.pourcentageReduction = pourcentage;
    console.log(`Réduction de ${pourcentage}% appliquée à ${this.nom}`);
    return true;
  }

  retirerReduction() {
    this.enPromotion = false;
    this.pourcentageReduction = 0;
    console.log(`Réduction retirée de ${this.nom}`);
  }

  ajusterStock(quantite) {
    this.stock += quantite;
    console.log(`Stock de ${this.nom}: ${this.stock}`);
  }

  acheter(quantite = 1) {
    if (quantite <= 0) {
      console.log("Quantité invalide");
      return false;
    }

    if (quantite > this.stock) {
      console.log("Stock insuffisant");
      return false;
    }

    this.stock -= quantite;
    const total = this.prixFinal * quantite;
    console.log(`Achat de ${quantite} ${this.nom}: ${total.toFixed(2)}€`);
    return true;
  }

  afficher() {
    const dispo = this.disponible ? "En stock" : "Rupture";
    const promo = this.enPromotion
      ? ` (${this.prix.toFixed(2)}€ → ${this.prixFinal.toFixed(2)}€, -${this.pourcentageReduction}%)`
      : ``;

    console.log(`${this.nom} - ${this.prixFinal.toFixed(2)}€${promo} [${dispo}]`);
  }
}

// Utilisation
const produit1 = new Produit("Ordinateur portable", 899, 15);
const produit2 = new Produit("Souris", 29.99, 50);

produit1.afficher();
// "Ordinateur portable - 899.00€ [En stock]"

produit1.appliquerReduction(10);
produit1.afficher();
// "Ordinateur portable - 809.10€ (899.00€ → 809.10€, -10%) [En stock]"

produit1.acheter(2);
// "Achat de 2 Ordinateur portable: 1618.20€"

produit2.acheter(5);
// "Achat de 5 Souris: 149.95€"
```

### Exemple 3 : Minuteur

```javascript
class Minuteur {
  constructor(nom) {
    this.nom = nom;
    this.secondes = 0;
    this.enMarche = false;
    this.intervalId = null;
  }

  demarrer() {
    if (this.enMarche) {
      console.log(`${this.nom} est déjà en marche`);
      return;
    }

    this.enMarche = true;
    console.log(`⏱️  ${this.nom} démarré`);

    this.intervalId = setInterval(() => {
      this.secondes++;
      this.afficherTemps();
    }, 1000);
  }

  arreter() {
    if (!this.enMarche) {
      console.log(`${this.nom} est déjà arrêté`);
      return;
    }

    clearInterval(this.intervalId);
    this.enMarche = false;
    console.log(`⏸️  ${this.nom} arrêté à ${this.tempsFormate}`);
  }

  reinitialiser() {
    this.arreter();
    this.secondes = 0;
    console.log(`🔄 ${this.nom} réinitialisé`);
  }

  get tempsFormate() {
    const heures = Math.floor(this.secondes / 3600);
    const minutes = Math.floor((this.secondes % 3600) / 60);
    const secondes = this.secondes % 60;

    return `${String(heures).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(secondes).padStart(2, '0')}`;
  }

  afficherTemps() {
    console.log(`${this.nom}: ${this.tempsFormate}`);
  }
}

// Utilisation
const timer = new Minuteur("Timer principal");

// timer.demarrer();
// Attend quelques secondes...
// timer.arreter();
// timer.reinitialiser();
```

### Exemple 4 : Panier d'achat

```javascript
class Panier {
  constructor(proprietaire) {
    this.proprietaire = proprietaire;
    this.articles = [];
  }

  ajouter(nom, prix, quantite = 1) {
    const articleExistant = this.articles.find(a => a.nom === nom);

    if (articleExistant) {
      articleExistant.quantite += quantite;
      console.log(`Quantité mise à jour: ${nom} (×${articleExistant.quantite})`);
    } else {
      this.articles.push({ nom, prix, quantite });
      console.log(`Article ajouté: ${nom}`);
    }
  }

  retirer(nom) {
    const index = this.articles.findIndex(a => a.nom === nom);

    if (index === -1) {
      console.log("Article non trouvé");
      return false;
    }

    this.articles.splice(index, 1);
    console.log(`Article retiré: ${nom}`);
    return true;
  }

  modifierQuantite(nom, nouvelleQuantite) {
    const article = this.articles.find(a => a.nom === nom);

    if (!article) {
      console.log("Article non trouvé");
      return false;
    }

    if (nouvelleQuantite <= 0) {
      return this.retirer(nom);
    }

    article.quantite = nouvelleQuantite;
    console.log(`Quantité modifiée: ${nom} (×${nouvelleQuantite})`);
    return true;
  }

  get total() {
    return this.articles.reduce((sum, article) => {
      return sum + (article.prix * article.quantite);
    }, 0);
  }

  get nombreArticles() {
    return this.articles.reduce((sum, article) => {
      return sum + article.quantite;
    }, 0);
  }

  get estVide() {
    return this.articles.length === 0;
  }

  afficher() {
    console.log(`\n=== Panier de ${this.proprietaire} ===`);

    if (this.estVide) {
      console.log("Panier vide");
      return;
    }

    this.articles.forEach(article => {
      const sousTotal = article.prix * article.quantite;
      console.log(`${article.nom} - ${article.prix.toFixed(2)}€ ×${article.quantite} = ${sousTotal.toFixed(2)}€`);
    });

    console.log("---");
    console.log(`Total: ${this.total.toFixed(2)}€`);
    console.log(`Articles: ${this.nombreArticles}`);
  }

  vider() {
    this.articles = [];
    console.log("Panier vidé");
  }
}

// Utilisation
const panier = new Panier("Alice");

panier.ajouter("Livre", 15.99, 2);
panier.ajouter("Stylo", 2.50, 5);
panier.ajouter("Cahier", 3.99, 3);

panier.afficher();

panier.modifierQuantite("Stylo", 3);
panier.retirer("Cahier");

panier.afficher();
```

## 6. Héritage avec `extends` (aperçu simple)

Les classes peuvent **hériter** d'autres classes avec le mot-clé `extends` :

```javascript
// Classe de base
class Animal {
  constructor(nom) {
    this.nom = nom;
  }

  parler() {
    console.log(`${this.nom} fait du bruit`);
  }
}

// Classe qui hérite de Animal
class Chien extends Animal {
  constructor(nom, race) {
    super(nom);  // Appelle le constructor de Animal
    this.race = race;
  }

  // Surcharge de la méthode parler
  parler() {
    console.log(`${this.nom} aboie: Wouf wouf !`);
  }

  // Nouvelle méthode
  sePresenter() {
    console.log(`Je suis ${this.nom}, un ${this.race}`);
  }
}

const animal = new Animal("Créature");
animal.parler();  // "Créature fait du bruit"

const chien = new Chien("Rex", "Labrador");
chien.parler();        // "Rex aboie: Wouf wouf !"
chien.sePresenter();   // "Je suis Rex, un Labrador"
```

**Note :** L'héritage est un sujet avancé que nous approfondirons dans des sections ultérieures.

## 7. Propriétés statiques (aperçu)

Les **propriétés et méthodes statiques** appartiennent à la classe elle-même, pas aux instances :

```javascript
class MathUtils {
  static PI = 3.14159;

  static carre(x) {
    return x * x;
  }

  static aire Cercle(rayon) {
    return this.PI * this.carre(rayon);
  }
}

// Utilisation directe sur la classe
console.log(MathUtils.PI);              // 3.14159
console.log(MathUtils.carre(5));        // 25
console.log(MathUtils.aireCercle(10));  // 314.159

// ❌ Ne fonctionne pas sur les instances
const util = new MathUtils();
// console.log(util.PI);  // undefined
```

### Exemple pratique : compteur global

```javascript
class Utilisateur {
  static compteur = 0;

  constructor(nom) {
    this.nom = nom;
    this.id = ++Utilisateur.compteur;
  }

  static obtenirNombreUtilisateurs() {
    return Utilisateur.compteur;
  }
}

const user1 = new Utilisateur("Alice");
const user2 = new Utilisateur("Bob");
const user3 = new Utilisateur("Charlie");

console.log(user1.id);  // 1
console.log(user2.id);  // 2
console.log(user3.id);  // 3

console.log(Utilisateur.obtenirNombreUtilisateurs());  // 3
```

## 8. Comparaison : Classes vs Constructeurs

### Même fonctionnalité, syntaxe différente

```javascript
// ❌ Constructeur classique
function PersonneConstructeur(nom, age) {
  this.nom = nom;
  this.age = age;
}
PersonneConstructeur.prototype.saluer = function() {
  return `Bonjour, je suis ${this.nom}`;
};

// ✅ Classe ES6
class PersonneClasse {
  constructor(nom, age) {
    this.nom = nom;
    this.age = age;
  }

  saluer() {
    return `Bonjour, je suis ${this.nom}`;
  }
}

// Utilisation identique
const p1 = new PersonneConstructeur("Alice", 28);
const p2 = new PersonneClasse("Bob", 32);

console.log(p1.saluer());  // "Bonjour, je suis Alice"
console.log(p2.saluer());  // "Bonjour, je suis Bob"
```

### Avantages des classes

| Aspect | Constructeur | Classe ES6 |
|--------|-------------|-----------|
| Syntaxe | Dispersée | Groupée et claire |
| Lisibilité | Moyenne | Excellente |
| Méthodes | `prototype.` | Directement dans la classe |
| Héritage | Complexe | Simple avec `extends` |
| Standard moderne | Non | Oui |

## 9. Vérification de type

```javascript
class Utilisateur {
  constructor(nom) {
    this.nom = nom;
  }
}

const user = new Utilisateur("Alice");
const objet = { nom: "Bob" };

console.log(user instanceof Utilisateur);   // true
console.log(objet instanceof Utilisateur);  // false

console.log(typeof user);   // "object"
console.log(typeof objet);  // "object"

// Pour vérifier si c'est vraiment une instance d'Utilisateur
console.log(user.constructor.name);  // "Utilisateur"
```

## 10. Bonnes pratiques

### 1. Nommage en PascalCase

```javascript
// ✅ Bon : PascalCase pour les classes
class GestionnaireTaches {}
class CompteBancaire {}
class UtilisateurPremium {}

// ❌ Mauvais : camelCase
class gestionnaireTaches {}
class compteBancaire {}
```

### 2. Un fichier par classe (organisation)

```javascript
// fichier: Utilisateur.js
class Utilisateur {
  // ...
}
export default Utilisateur;

// fichier: CompteBancaire.js
class CompteBancaire {
  // ...
}
export default CompteBancaire;
```

### 3. Valider dans le constructor

```javascript
class Utilisateur {
  constructor(nom, age) {
    if (!nom || typeof nom !== 'string') {
      throw new Error("Nom invalide");
    }

    if (age < 0 || age > 150) {
      throw new Error("Âge invalide");
    }

    this.nom = nom;
    this.age = age;
  }
}
```

### 4. Utiliser des getters pour les propriétés calculées

```javascript
// ✅ Bon : propriété calculée avec getter
class Rectangle {
  constructor(largeur, hauteur) {
    this.largeur = largeur;
    this.hauteur = hauteur;
  }

  get aire() {
    return this.largeur * this.hauteur;
  }
}

const rect = new Rectangle(10, 5);
console.log(rect.aire);  // 50 (pas de parenthèses)

// ❌ Moins élégant : méthode
class Rectangle {
  constructor(largeur, hauteur) {
    this.largeur = largeur;
    this.hauteur = hauteur;
  }

  calculerAire() {
    return this.largeur * this.hauteur;
  }
}

const rect = new Rectangle(10, 5);
console.log(rect.calculerAire());  // 50 (avec parenthèses)
```

### 5. Documenter les classes

```javascript
/**
 * Représente un compte bancaire
 * @class
 */
class CompteBancaire {
  /**
   * Crée un nouveau compte bancaire
   * @param {string} titulaire - Nom du titulaire
   * @param {number} soldeInitial - Solde de départ (défaut: 0)
   */
  constructor(titulaire, soldeInitial = 0) {
    this.titulaire = titulaire;
    this.solde = soldeInitial;
  }

  /**
   * Dépose de l'argent sur le compte
   * @param {number} montant - Montant à déposer
   * @returns {boolean} true si réussi, false sinon
   */
  deposer(montant) {
    // ...
  }
}
```

## 11. Pièges à éviter

### Piège 1 : Oublier `new`

```javascript
class Utilisateur {
  constructor(nom) {
    this.nom = nom;
  }
}

// ❌ Sans new : erreur
// const user = Utilisateur("Alice");  // TypeError

// ✅ Avec new
const user = new Utilisateur("Alice");
```

**Heureusement,** les classes génèrent une erreur si on oublie `new` (contrairement aux constructeurs).

### Piège 2 : Arrow functions comme méthodes

```javascript
class Compteur {
  valeur = 0;

  // ❌ Arrow function : problèmes potentiels
  incrementer = () => {
    this.valeur++;
  }

  // ✅ Méthode normale
  incrementer() {
    this.valeur++;
  }
}
```

**Note :** Les arrow functions comme méthodes fonctionnent, mais peuvent causer des problèmes avec l'héritage.

### Piège 3 : Virgules entre les méthodes

```javascript
class Personne {
  constructor(nom) {
    this.nom = nom;
  }

  // ❌ Pas de virgule entre les méthodes !
  saluer() {
    return "Bonjour";
  }  // Pas de virgule ici

  partir() {
    return "Au revoir";
  }
}
```

### Piège 4 : Oublier `this`

```javascript
class Compteur {
  constructor() {
    this.valeur = 0;
  }

  incrementer() {
    // ❌ Oubli de this
    // valeur++;  // Erreur

    // ✅ Avec this
    this.valeur++;
  }
}
```

## 12. Classes vs Objets littéraux : quand utiliser quoi ?

### Utilisez des classes pour :

```javascript
// ✅ Créer plusieurs instances similaires
class Utilisateur {
  constructor(nom, email) {
    this.nom = nom;
    this.email = email;
  }
}

const users = [
  new Utilisateur("Alice", "alice@example.com"),
  new Utilisateur("Bob", "bob@example.com"),
  new Utilisateur("Charlie", "charlie@example.com")
];
```

### Utilisez des objets littéraux pour :

```javascript
// ✅ Configuration unique
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000,
  retries: 3
};

// ✅ Regroupement de fonctions utilitaires
const MathUtils = {
  carre: (x) => x * x,
  cube: (x) => x * x * x,
  racine: (x) => Math.sqrt(x)
};
```

## Points clés à retenir

1. **Classes ES6** = syntaxe moderne et claire pour créer des objets
2. **`constructor`** = méthode spéciale pour initialiser l'objet
3. **Méthodes** = définies directement dans la classe
4. **`get`/`set`** = propriétés calculées ou contrôlées
5. **`extends`** = héritage entre classes
6. **`static`** = propriétés/méthodes de la classe elle-même
7. **`new`** obligatoire pour créer une instance
8. **Classes ≠ constructeurs** en interne, mais syntaxe beaucoup plus claire
9. **PascalCase** pour nommer les classes
10. **Classes pour plusieurs objets**, objets littéraux pour singleton

## Comparaison finale

```javascript
// AVANT : Constructeur classique
function Voiture(marque, modele) {
  this.marque = marque;
  this.modele = modele;
}
Voiture.prototype.afficher = function() {
  console.log(`${this.marque} ${this.modele}`);
};

// MAINTENANT : Classe ES6
class Voiture {
  constructor(marque, modele) {
    this.marque = marque;
    this.modele = modele;
  }

  afficher() {
    console.log(`${this.marque} ${this.modele}`);
  }
}

// Utilisation identique
const voiture = new Voiture("Peugeot", "308");
voiture.afficher();
```

**Les classes ES6 sont la façon moderne et recommandée de créer des objets en JavaScript !**

## Ce qui vient ensuite

Vous avez maintenant terminé le chapitre sur les objets modernes ! Vous avez appris :
- Créer des objets littéraux
- Utiliser la syntaxe raccourcie ES6
- Accéder et modifier les propriétés
- Le destructuring
- Le spread operator
- Les méthodes d'objets
- Le mot-clé `this`
- Les constructeurs
- Les classes ES6

**Prochaines étapes :**
- Approfondir l'héritage et la POO
- Les prototypes en détail
- Les design patterns
- La programmation fonctionnelle avec les objets

Les classes sont un pilier de JavaScript moderne et vous les utiliserez constamment, surtout avec React, Vue, et autres frameworks !

⏭️ [Tableaux modernes (Arrays)](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/README.md)
