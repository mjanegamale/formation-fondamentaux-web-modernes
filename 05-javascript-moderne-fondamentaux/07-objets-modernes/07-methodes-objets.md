🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.7 - Méthodes d'objets

## Introduction

Une **méthode** est une fonction qui appartient à un objet. C'est simplement une propriété d'objet dont la valeur est une fonction. Les méthodes permettent aux objets d'avoir des **comportements** en plus de leurs données.

En d'autres termes :
- **Propriétés** = les données de l'objet (ce qu'il **a**)
- **Méthodes** = les actions de l'objet (ce qu'il **fait**)

### Analogie du monde réel

Pensez à une voiture :
- **Propriétés** : couleur, marque, vitesse, carburant
- **Méthodes** : démarrer(), accélérer(), freiner(), tourner()

## 1. Créer des méthodes

### Syntaxe classique (avant ES6)

```javascript
const personne = {
  nom: "Alice",
  age: 28,

  // Méthode avec syntaxe classique
  saluer: function() {
    console.log("Bonjour !");
  }
};

// Appel de la méthode
personne.saluer();  // "Bonjour !"
```

### Syntaxe raccourcie ES6 (recommandée)

```javascript
const personne = {
  nom: "Alice",
  age: 28,

  // Méthode avec syntaxe raccourcie (sans "function" ni ":")
  saluer() {
    console.log("Bonjour !");
  }
};

// Appel de la méthode
personne.saluer();  // "Bonjour !"
```

**Recommandation :** Utilisez toujours la syntaxe raccourcie ES6 pour les méthodes.

### Différence avec une fonction normale

```javascript
// Fonction indépendante
function saluer() {
  console.log("Bonjour !");
}
saluer();

// Méthode d'objet
const personne = {
  saluer() {
    console.log("Bonjour !");
  }
};
personne.saluer();  // Notez la notation point
```

## 2. Appeler une méthode

Pour appeler une méthode, on utilise la notation point suivie de parenthèses :

```javascript
const calculatrice = {
  marque: "Casio",

  afficherMarque() {
    console.log("Calculatrice Casio");
  }
};

// ✅ Appel correct avec parenthèses
calculatrice.afficherMarque();  // "Calculatrice Casio"

// ⚠️ Sans parenthèses : renvoie la fonction elle-même
console.log(calculatrice.afficherMarque);
// [Function: afficherMarque]
```

**Important :** Les parenthèses `()` sont obligatoires pour **exécuter** la méthode.

## 3. Méthodes avec paramètres

Les méthodes peuvent accepter des paramètres comme les fonctions normales :

```javascript
const calculatrice = {
  marque: "Casio",

  additionner(a, b) {
    return a + b;
  },

  soustraire(a, b) {
    return a - b;
  },

  multiplier(a, b) {
    return a * b;
  }
};

console.log(calculatrice.additionner(5, 3));   // 8
console.log(calculatrice.soustraire(10, 4));   // 6
console.log(calculatrice.multiplier(7, 6));    // 42
```

### Avec plusieurs paramètres

```javascript
const utilisateur = {
  nom: "Alice",

  sePresenter(titre, ville) {
    console.log(`Je suis ${titre} ${this.nom}, je vis à ${ville}`);
  },

  creerMessage(destinataire, message) {
    return `De: ${this.nom}\nÀ: ${destinataire}\nMessage: ${message}`;
  }
};

utilisateur.sePresenter("Madame", "Paris");
// "Je suis Madame Alice, je vis à Paris"

const msg = utilisateur.creerMessage("Bob", "Bonjour !");
console.log(msg);
// "De: Alice
// À: Bob
// Message: Bonjour !"
```

## 4. Méthodes avec valeur de retour

Les méthodes peuvent retourner des valeurs avec `return` :

```javascript
const rectangle = {
  largeur: 10,
  hauteur: 5,

  calculerAire() {
    return this.largeur * this.hauteur;
  },

  calculerPerimetre() {
    return 2 * (this.largeur + this.hauteur);
  },

  estCarre() {
    return this.largeur === this.hauteur;
  }
};

const aire = rectangle.calculerAire();
console.log(aire);  // 50

const perimetre = rectangle.calculerPerimetre();
console.log(perimetre);  // 30

console.log(rectangle.estCarre());  // false
```

### Méthodes qui ne retournent rien

Certaines méthodes ne retournent rien (`undefined` par défaut) :

```javascript
const logger = {
  messages: [],

  ajouter(message) {
    this.messages.push(message);
    console.log("Message ajouté:", message);
    // Pas de return
  },

  afficherTous() {
    this.messages.forEach(msg => console.log(msg));
    // Pas de return
  }
};

logger.ajouter("Premier message");
logger.ajouter("Deuxième message");
logger.afficherTous();
```

## 5. Le mot-clé `this`

Dans une méthode, `this` fait référence à **l'objet lui-même**. Cela permet d'accéder aux autres propriétés et méthodes de l'objet.

### Accéder aux propriétés avec `this`

```javascript
const personne = {
  prenom: "Alice",
  nom: "Martin",
  age: 28,

  // Utiliser this pour accéder aux propriétés
  nomComplet() {
    return `${this.prenom} ${this.nom}`;
  },

  sePresenter() {
    return `Je suis ${this.nomComplet()}, j'ai ${this.age} ans`;
  }
};

console.log(personne.nomComplet());
// "Alice Martin"

console.log(personne.sePresenter());
// "Je suis Alice Martin, j'ai 28 ans"
```

### Sans `this` : erreur !

```javascript
const voiture = {
  marque: "Peugeot",
  modele: "308",

  // ❌ Sans this : ne fonctionne pas
  afficherMauvais() {
    return marque + " " + modele;
    // ReferenceError: marque is not defined
  },

  // ✅ Avec this : fonctionne
  afficherBon() {
    return this.marque + " " + this.modele;
  }
};

console.log(voiture.afficherBon());  // "Peugeot 308"
```

### Modifier les propriétés avec `this`

```javascript
const compteur = {
  valeur: 0,

  incrementer() {
    this.valeur++;
  },

  decrementer() {
    this.valeur--;
  },

  ajouter(nombre) {
    this.valeur += nombre;
  },

  reinitialiser() {
    this.valeur = 0;
  },

  afficher() {
    console.log(`Compteur: ${this.valeur}`);
  }
};

compteur.incrementer();
compteur.incrementer();
compteur.afficher();  // "Compteur: 2"

compteur.ajouter(5);
compteur.afficher();  // "Compteur: 7"

compteur.reinitialiser();
compteur.afficher();  // "Compteur: 0"
```

## 6. Appeler une méthode depuis une autre méthode

Les méthodes peuvent s'appeler entre elles avec `this` :

```javascript
const calculatrice = {
  historique: [],

  additionner(a, b) {
    const resultat = a + b;
    this.ajouterAHistorique(`${a} + ${b} = ${resultat}`);
    return resultat;
  },

  soustraire(a, b) {
    const resultat = a - b;
    this.ajouterAHistorique(`${a} - ${b} = ${resultat}`);
    return resultat;
  },

  ajouterAHistorique(operation) {
    this.historique.push(operation);
  },

  afficherHistorique() {
    console.log("=== Historique ===");
    this.historique.forEach(op => console.log(op));
  }
};

calculatrice.additionner(5, 3);
calculatrice.soustraire(10, 4);
calculatrice.additionner(7, 2);

calculatrice.afficherHistorique();
// === Historique ===
// 5 + 3 = 8
// 10 - 4 = 6
// 7 + 2 = 9
```

## 7. Exemples pratiques complets

### Exemple 1 : Compte bancaire

```javascript
const compteBancaire = {
  titulaire: "Alice Martin",
  solde: 1000,
  devise: "EUR",
  historique: [],

  deposer(montant) {
    if (montant <= 0) {
      console.log("Montant invalide");
      return false;
    }

    this.solde += montant;
    this.ajouterTransaction("Dépôt", montant);
    console.log(`Dépôt de ${montant}${this.devise} effectué`);
    return true;
  },

  retirer(montant) {
    if (montant <= 0) {
      console.log("Montant invalide");
      return false;
    }

    if (montant > this.solde) {
      console.log("Solde insuffisant");
      return false;
    }

    this.solde -= montant;
    this.ajouterTransaction("Retrait", montant);
    console.log(`Retrait de ${montant}${this.devise} effectué`);
    return true;
  },

  ajouterTransaction(type, montant) {
    this.historique.push({
      type: type,
      montant: montant,
      date: new Date(),
      soldeApres: this.solde
    });
  },

  afficherSolde() {
    console.log(`Solde de ${this.titulaire}: ${this.solde}${this.devise}`);
  },

  afficherHistorique() {
    console.log(`=== Historique de ${this.titulaire} ===`);
    this.historique.forEach(transaction => {
      console.log(`${transaction.type}: ${transaction.montant}${this.devise} (Solde: ${transaction.soldeApres}${this.devise})`);
    });
  }
};

// Utilisation
compteBancaire.afficherSolde();
// "Solde de Alice Martin: 1000EUR"

compteBancaire.deposer(500);
// "Dépôt de 500EUR effectué"

compteBancaire.retirer(200);
// "Retrait de 200EUR effectué"

compteBancaire.retirer(2000);
// "Solde insuffisant"

compteBancaire.afficherSolde();
// "Solde de Alice Martin: 1300EUR"

compteBancaire.afficherHistorique();
```

### Exemple 2 : Gestion de tâches

```javascript
const gestionnaireTaches = {
  taches: [],
  prochainId: 1,

  ajouter(titre, priorite = "normale") {
    const tache = {
      id: this.prochainId++,
      titre: titre,
      priorite: priorite,
      terminee: false,
      dateCreation: new Date()
    };

    this.taches.push(tache);
    console.log(`Tâche ajoutée: ${titre}`);
    return tache.id;
  },

  terminer(id) {
    const tache = this.taches.find(t => t.id === id);

    if (!tache) {
      console.log("Tâche non trouvée");
      return false;
    }

    tache.terminee = true;
    console.log(`Tâche terminée: ${tache.titre}`);
    return true;
  },

  supprimer(id) {
    const index = this.taches.findIndex(t => t.id === id);

    if (index === -1) {
      console.log("Tâche non trouvée");
      return false;
    }

    const tache = this.taches.splice(index, 1)[0];
    console.log(`Tâche supprimée: ${tache.titre}`);
    return true;
  },

  listerTout() {
    console.log("=== Toutes les tâches ===");
    this.taches.forEach(tache => {
      const statut = tache.terminee ? "✓" : "○";
      console.log(`${statut} [${tache.priorite}] ${tache.titre}`);
    });
  },

  listerNonTerminees() {
    console.log("=== Tâches non terminées ===");
    const nonTerminees = this.taches.filter(t => !t.terminee);

    if (nonTerminees.length === 0) {
      console.log("Aucune tâche en cours");
      return;
    }

    nonTerminees.forEach(tache => {
      console.log(`[${tache.priorite}] ${tache.titre}`);
    });
  },

  compter() {
    const total = this.taches.length;
    const terminees = this.taches.filter(t => t.terminee).length;
    const enCours = total - terminees;

    return {
      total: total,
      terminees: terminees,
      enCours: enCours
    };
  },

  afficherStatistiques() {
    const stats = this.compter();
    console.log("=== Statistiques ===");
    console.log(`Total: ${stats.total}`);
    console.log(`Terminées: ${stats.terminees}`);
    console.log(`En cours: ${stats.enCours}`);
  }
};

// Utilisation
gestionnaireTaches.ajouter("Faire les courses", "haute");
gestionnaireTaches.ajouter("Apprendre JavaScript");
gestionnaireTaches.ajouter("Appeler le dentiste", "haute");
gestionnaireTaches.ajouter("Lire un livre");

gestionnaireTaches.listerTout();

gestionnaireTaches.terminer(1);
gestionnaireTaches.terminer(3);

gestionnaireTaches.listerNonTerminees();
gestionnaireTaches.afficherStatistiques();
```

### Exemple 3 : Panier d'achat

```javascript
const panier = {
  articles: [],

  ajouter(nom, prix, quantite = 1) {
    // Vérifier si l'article existe déjà
    const articleExistant = this.articles.find(a => a.nom === nom);

    if (articleExistant) {
      articleExistant.quantite += quantite;
      console.log(`Quantité mise à jour: ${nom} (${articleExistant.quantite})`);
    } else {
      this.articles.push({
        nom: nom,
        prix: prix,
        quantite: quantite
      });
      console.log(`Article ajouté: ${nom}`);
    }
  },

  retirer(nom) {
    const index = this.articles.findIndex(a => a.nom === nom);

    if (index === -1) {
      console.log("Article non trouvé");
      return false;
    }

    this.articles.splice(index, 1);
    console.log(`Article retiré: ${nom}`);
    return true;
  },

  modifierQuantite(nom, nouvelleQuantite) {
    const article = this.articles.find(a => a.nom === nom);

    if (!article) {
      console.log("Article non trouvé");
      return false;
    }

    if (nouvelleQuantite <= 0) {
      this.retirer(nom);
    } else {
      article.quantite = nouvelleQuantite;
      console.log(`Quantité modifiée: ${nom} (${nouvelleQuantite})`);
    }

    return true;
  },

  calculerTotal() {
    return this.articles.reduce((total, article) => {
      return total + (article.prix * article.quantite);
    }, 0);
  },

  calculerNbArticles() {
    return this.articles.reduce((total, article) => {
      return total + article.quantite;
    }, 0);
  },

  afficher() {
    console.log("=== Panier ===");

    if (this.articles.length === 0) {
      console.log("Panier vide");
      return;
    }

    this.articles.forEach(article => {
      const sousTotal = article.prix * article.quantite;
      console.log(`${article.nom} - ${article.prix}€ x ${article.quantite} = ${sousTotal.toFixed(2)}€`);
    });

    console.log("---");
    console.log(`Total: ${this.calculerTotal().toFixed(2)}€`);
    console.log(`Articles: ${this.calculerNbArticles()}`);
  },

  vider() {
    this.articles = [];
    console.log("Panier vidé");
  },

  obtenirResume() {
    return {
      nbArticles: this.calculerNbArticles(),
      total: this.calculerTotal(),
      articles: this.articles.length
    };
  }
};

// Utilisation
panier.ajouter("Livre", 15.99, 2);
panier.ajouter("Stylo", 2.50, 5);
panier.ajouter("Cahier", 3.99, 3);

panier.afficher();

panier.modifierQuantite("Stylo", 3);
panier.retirer("Cahier");

panier.afficher();

const resume = panier.obtenirResume();
console.log(resume);
```

### Exemple 4 : Chronomètre

```javascript
const chronometre = {
  secondes: 0,
  intervalId: null,
  enMarche: false,

  demarrer() {
    if (this.enMarche) {
      console.log("Chronomètre déjà en marche");
      return;
    }

    this.enMarche = true;
    this.intervalId = setInterval(() => {
      this.secondes++;
      this.afficher();
    }, 1000);

    console.log("Chronomètre démarré");
  },

  arreter() {
    if (!this.enMarche) {
      console.log("Chronomètre déjà arrêté");
      return;
    }

    clearInterval(this.intervalId);
    this.enMarche = false;
    console.log("Chronomètre arrêté");
  },

  reinitialiser() {
    this.arreter();
    this.secondes = 0;
    console.log("Chronomètre réinitialisé");
  },

  afficher() {
    const heures = Math.floor(this.secondes / 3600);
    const minutes = Math.floor((this.secondes % 3600) / 60);
    const secondes = this.secondes % 60;

    const format = `${String(heures).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(secondes).padStart(2, '0')}`;
    console.log(format);
  },

  obtenirTemps() {
    return this.secondes;
  }
};

// Utilisation
// chronometre.demarrer();
// ... attend quelques secondes ...
// chronometre.arreter();
// chronometre.afficher();
// chronometre.reinitialiser();
```

## 8. Méthodes et propriétés privées (convention)

JavaScript n'a pas de vraies propriétés privées (avant ES2022), mais on utilise la convention du préfixe `_` :

```javascript
const compteur = {
  _valeur: 0,  // Convention : propriété "privée"

  // Méthodes publiques
  incrementer() {
    this._valeur++;
  },

  obtenir() {
    return this._valeur;
  },

  // Méthode "privée" (par convention)
  _valider(nombre) {
    return typeof nombre === 'number' && !isNaN(nombre);
  },

  definir(nouvelleValeur) {
    if (this._valider(nouvelleValeur)) {
      this._valeur = nouvelleValeur;
      return true;
    }
    console.log("Valeur invalide");
    return false;
  }
};

// Utilisation
compteur.incrementer();
console.log(compteur.obtenir());  // 1

compteur.definir(10);
console.log(compteur.obtenir());  // 10

// ⚠️ On peut toujours accéder à _valeur, mais par convention on ne devrait pas
console.log(compteur._valeur);  // 10 (fonctionne mais déconseillé)
```

## 9. Getters et Setters

JavaScript permet de créer des propriétés calculées avec `get` et `set` :

### Getter (lecture)

```javascript
const personne = {
  prenom: "Alice",
  nom: "Martin",

  // Getter : appelé comme une propriété, pas comme une méthode
  get nomComplet() {
    return `${this.prenom} ${this.nom}`;
  }
};

// Utilisation : pas de parenthèses !
console.log(personne.nomComplet);  // "Alice Martin"
```

### Setter (écriture)

```javascript
const personne = {
  prenom: "Alice",
  nom: "Martin",

  get nomComplet() {
    return `${this.prenom} ${this.nom}`;
  },

  // Setter : permet de modifier via une propriété
  set nomComplet(valeur) {
    const parties = valeur.split(" ");
    this.prenom = parties[0];
    this.nom = parties[1];
  }
};

// Lecture avec getter
console.log(personne.nomComplet);  // "Alice Martin"

// Écriture avec setter
personne.nomComplet = "Bob Dupont";

console.log(personne.prenom);  // "Bob"
console.log(personne.nom);     // "Dupont"
console.log(personne.nomComplet);  // "Bob Dupont"
```

### Exemple pratique avec getters

```javascript
const rectangle = {
  largeur: 10,
  hauteur: 5,

  get aire() {
    return this.largeur * this.hauteur;
  },

  get perimetre() {
    return 2 * (this.largeur + this.hauteur);
  },

  get estCarre() {
    return this.largeur === this.hauteur;
  }
};

// Utilisation comme des propriétés
console.log(rectangle.aire);       // 50
console.log(rectangle.perimetre);  // 30
console.log(rectangle.estCarre);   // false

// Modification des dimensions
rectangle.largeur = 5;
console.log(rectangle.aire);       // 25
console.log(rectangle.estCarre);   // true
```

## 10. Chaînage de méthodes

On peut chaîner des méthodes en retournant `this` :

```javascript
const calculatrice = {
  valeur: 0,

  ajouter(nombre) {
    this.valeur += nombre;
    return this;  // Retourne l'objet lui-même
  },

  soustraire(nombre) {
    this.valeur -= nombre;
    return this;
  },

  multiplier(nombre) {
    this.valeur *= nombre;
    return this;
  },

  diviser(nombre) {
    this.valeur /= nombre;
    return this;
  },

  afficher() {
    console.log(this.valeur);
    return this;
  },

  reinitialiser() {
    this.valeur = 0;
    return this;
  }
};

// Chaînage de méthodes
calculatrice
  .ajouter(10)
  .multiplier(2)
  .soustraire(5)
  .afficher()      // 15
  .diviser(3)
  .afficher();     // 5

// Réinitialiser et nouveau calcul
calculatrice
  .reinitialiser()
  .ajouter(100)
  .diviser(4)
  .afficher();     // 25
```

## 11. Bonnes pratiques

### 1. Nommage descriptif

```javascript
// ✅ Bon : noms clairs et descriptifs
const utilisateur = {
  calculerAge() { /* ... */ },
  verifierAcces() { /* ... */ },
  sauvegarderDonnees() { /* ... */ }
};

// ❌ À éviter : noms vagues
const utilisateur = {
  calc() { /* ... */ },
  check() { /* ... */ },
  save() { /* ... */ }
};
```

### 2. Une méthode = une responsabilité

```javascript
// ✅ Bon : méthodes spécifiques
const produit = {
  calculerPrixTTC() {
    return this.prix * 1.20;
  },

  verifierStock() {
    return this.stock > 0;
  },

  appliquerReduction(pourcentage) {
    this.prix *= (1 - pourcentage / 100);
  }
};

// ❌ À éviter : méthode qui fait trop de choses
const produit = {
  traiter() {
    // Calcule le prix
    // Vérifie le stock
    // Applique une réduction
    // Sauvegarde
    // Envoie un email
    // ...
  }
};
```

### 3. Utiliser `this` pour accéder aux propriétés

```javascript
// ✅ Bon
const personne = {
  nom: "Alice",
  saluer() {
    return `Bonjour, je suis ${this.nom}`;
  }
};

// ❌ Mauvais : impossible sans this
const personne = {
  nom: "Alice",
  saluer() {
    return `Bonjour, je suis ${nom}`;  // Erreur !
  }
};
```

### 4. Retourner des valeurs quand c'est utile

```javascript
// ✅ Bon : retourne le résultat
const calculatrice = {
  additionner(a, b) {
    return a + b;
  }
};

const resultat = calculatrice.additionner(5, 3);
console.log(resultat);

// ⚠️ Moins flexible : ne retourne rien
const calculatrice = {
  additionner(a, b) {
    console.log(a + b);  // Affiche directement
  }
};
```

### 5. Valider les paramètres

```javascript
const compteBancaire = {
  solde: 1000,

  retirer(montant) {
    // Validation
    if (typeof montant !== 'number' || montant <= 0) {
      console.log("Montant invalide");
      return false;
    }

    if (montant > this.solde) {
      console.log("Solde insuffisant");
      return false;
    }

    // Action
    this.solde -= montant;
    return true;
  }
};
```

## 12. Différences importantes

### Méthode vs Fonction

| Aspect | Fonction | Méthode |
|--------|----------|---------|
| Localisation | Indépendante | Dans un objet |
| Appel | `fonction()` | `objet.methode()` |
| `this` | Dépend du contexte | Pointe vers l'objet |
| Usage | Tâches générales | Actions d'un objet |

### Méthode vs Propriété

```javascript
const personne = {
  nom: "Alice",              // Propriété (donnée)
  age: 28,                   // Propriété (donnée)

  saluer() {                 // Méthode (action)
    return `Bonjour !`;
  },

  get nomMajuscules() {      // Getter (propriété calculée)
    return this.nom.toUpperCase();
  }
};

console.log(personne.nom);           // Propriété : pas de ()
console.log(personne.saluer());      // Méthode : avec ()
console.log(personne.nomMajuscules); // Getter : pas de ()
```

## 13. Pièges à éviter

### Piège 1 : Oublier `this`

```javascript
const compteur = {
  valeur: 0,

  // ❌ Erreur : pas de this
  incrementer() {
    valeur++;  // ReferenceError
  },

  // ✅ Correct : avec this
  incrementer() {
    this.valeur++;
  }
};
```

### Piège 2 : Oublier les parenthèses

```javascript
const personne = {
  saluer() {
    return "Bonjour !";
  }
};

// ❌ Sans () : renvoie la fonction
console.log(personne.saluer);
// [Function: saluer]

// ✅ Avec () : exécute la fonction
console.log(personne.saluer());
// "Bonjour !"
```

### Piège 3 : Arrow function et `this`

```javascript
const personne = {
  nom: "Alice",

  // ❌ Arrow function : this ne fonctionne pas correctement
  saluer: () => {
    return `Bonjour, je suis ${this.nom}`;  // undefined
  },

  // ✅ Méthode normale : this fonctionne
  saluerCorrect() {
    return `Bonjour, je suis ${this.nom}`;
  }
};
```

**Important :** N'utilisez **jamais** d'arrow functions pour les méthodes d'objets.

## Points clés à retenir

1. **Méthode** = fonction dans un objet
2. **Syntaxe ES6** : `nomMethode() { }` (sans `function` ni `:`)
3. **Appel** : `objet.methode()` avec parenthèses
4. **`this`** fait référence à l'objet lui-même
5. **Paramètres et `return`** fonctionnent comme les fonctions normales
6. **Getters/Setters** : `get` et `set` pour propriétés calculées
7. **Chaînage** : retourner `this` permet de chaîner les méthodes
8. **Pas d'arrow functions** pour les méthodes d'objets

## Ce qui vient ensuite

Dans la prochaine section, vous allez approfondir votre compréhension de `this` avec :
- Les différents contextes d'exécution
- Le comportement de `this` avec les arrow functions
- Les méthodes `bind`, `call`, et `apply`

Les méthodes sont essentielles pour créer des objets avec comportements. Elles sont la base de la programmation orientée objet en JavaScript !

⏭️ [Le mot-clé this et arrow functions](/05-javascript-moderne-fondamentaux/07-objets-modernes/08-this-et-arrow-functions.md)
