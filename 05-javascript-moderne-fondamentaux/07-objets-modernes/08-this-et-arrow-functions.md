🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.7.8 - Le mot-clé this et arrow functions

## Introduction

Le mot-clé `this` est l'un des concepts les plus importants et les plus déroutants de JavaScript. Sa valeur change selon **comment** et **où** une fonction est appelée. Comprendre `this` est essentiel pour travailler avec les objets et la programmation orientée objet.

Les **arrow functions** (fonctions fléchées) ont été introduites en ES6 et ont un comportement spécial avec `this`, différent des fonctions classiques.

Dans cette section, nous allons comprendre :
1. Ce que représente `this`
2. Comment sa valeur est déterminée
3. Le comportement différent des arrow functions
4. Quand utiliser l'une ou l'autre

## 1. Qu'est-ce que `this` ?

`this` est un mot-clé spécial qui fait référence à un **objet**. Mais **quel** objet ? Cela dépend du **contexte d'exécution**.

### Analogie

Imaginez que vous êtes dans une conversation :
- Quand vous dites "moi", cela fait référence à **vous-même**
- Dans une méthode d'objet, `this` fait référence à **l'objet lui-même**

```javascript
const personne = {
  nom: "Alice",

  sePresenter() {
    // "this" = personne (l'objet lui-même)
    console.log(`Je suis ${this.nom}`);
  }
};

personne.sePresenter();  // "Je suis Alice"
```

## 2. `this` dans les méthodes d'objets

Dans une méthode d'objet, `this` pointe vers **l'objet qui contient la méthode** :

```javascript
const voiture = {
  marque: "Peugeot",
  modele: "308",
  annee: 2023,

  afficherInfos() {
    // this = voiture
    console.log(`${this.marque} ${this.modele} (${this.annee})`);
  },

  demarrer() {
    console.log(`La ${this.marque} démarre`);
  }
};

voiture.afficherInfos();  // "Peugeot 308 (2023)"
voiture.demarrer();       // "La Peugeot démarre"
```

### Accéder aux propriétés avec `this`

```javascript
const rectangle = {
  largeur: 10,
  hauteur: 5,

  calculerAire() {
    // this.largeur et this.hauteur font référence aux propriétés
    return this.largeur * this.hauteur;
  },

  agrandir(facteur) {
    this.largeur *= facteur;
    this.hauteur *= facteur;
  }
};

console.log(rectangle.calculerAire());  // 50

rectangle.agrandir(2);
console.log(rectangle.calculerAire());  // 200
```

## 3. Le problème : `this` change selon le contexte

La valeur de `this` dépend de **comment** la fonction est appelée, pas de **où** elle est définie.

### Exemple du problème

```javascript
const personne = {
  nom: "Alice",

  saluer() {
    console.log(`Bonjour, je suis ${this.nom}`);
  }
};

// ✅ Appel direct : this = personne
personne.saluer();  // "Bonjour, je suis Alice"

// ❌ Extraire la méthode : this ne pointe plus vers personne
const saluerSeul = personne.saluer;
saluerSeul();  // "Bonjour, je suis undefined"
```

**Pourquoi ?** Quand on extrait la méthode, elle perd son contexte (son lien avec l'objet).

## 4. `this` dans les fonctions normales

Dans une fonction normale (pas une méthode), la valeur de `this` dépend du mode :

### Mode non-strict (par défaut)

```javascript
function afficherThis() {
  console.log(this);
}

afficherThis();  // Window (dans un navigateur) ou global (Node.js)
```

### Mode strict

```javascript
"use strict";

function afficherThis() {
  console.log(this);
}

afficherThis();  // undefined
```

**Important :** En mode strict, `this` vaut `undefined` dans les fonctions normales.

## 5. Le problème des callbacks

Un problème fréquent survient avec les callbacks :

### Exemple du problème

```javascript
const compteur = {
  valeur: 0,

  incrementer() {
    this.valeur++;
    console.log(this.valeur);
  },

  demarrerTimer() {
    // ❌ Problème : this ne pointe plus vers compteur dans le callback
    setTimeout(function() {
      this.incrementer();  // TypeError: this.incrementer is not a function
    }, 1000);
  }
};

// compteur.demarrerTimer();  // Erreur !
```

**Pourquoi ?** Dans le callback passé à `setTimeout`, `this` ne fait plus référence à `compteur`.

### Solutions classiques (avant ES6)

#### Solution 1 : Variable intermédiaire

```javascript
const compteur = {
  valeur: 0,

  incrementer() {
    this.valeur++;
    console.log(this.valeur);
  },

  demarrerTimer() {
    // Sauvegarder this dans une variable
    const self = this;

    setTimeout(function() {
      self.incrementer();  // ✅ Fonctionne
    }, 1000);
  }
};
```

**Note :** On voit souvent `self`, `that`, ou `_this` comme nom de variable.

#### Solution 2 : `bind()`

```javascript
const compteur = {
  valeur: 0,

  incrementer() {
    this.valeur++;
    console.log(this.valeur);
  },

  demarrerTimer() {
    setTimeout(function() {
      this.incrementer();
    }.bind(this), 1000);  // bind() fixe la valeur de this
  }
};
```

## 6. Les arrow functions : la solution moderne

Les **arrow functions** ont été introduites en ES6 pour résoudre ce problème. Elles ont un comportement spécial avec `this`.

### Règle fondamentale

**Une arrow function n'a PAS son propre `this`.** Elle hérite du `this` du contexte dans lequel elle est définie.

### Comparaison

```javascript
const objet = {
  valeur: 42,

  // Fonction normale : a son propre this
  methodeNormale: function() {
    console.log(this);  // objet
  },

  // Arrow function : hérite du this extérieur
  arrowFunction: () => {
    console.log(this);  // Window ou undefined (pas l'objet !)
  }
};

objet.methodeNormale();   // Affiche objet
objet.arrowFunction();    // N'affiche PAS objet
```

### Solution avec arrow function pour les callbacks

```javascript
const compteur = {
  valeur: 0,

  incrementer() {
    this.valeur++;
    console.log(this.valeur);
  },

  demarrerTimer() {
    // ✅ Arrow function : hérite du this de demarrerTimer
    setTimeout(() => {
      this.incrementer();  // this = compteur
    }, 1000);
  }
};

compteur.demarrerTimer();  // Fonctionne parfaitement !
```

**Pourquoi ça marche ?** L'arrow function hérite du `this` de `demarrerTimer`, qui lui-même a `this = compteur`.

## 7. Visualisation : this dans différents contextes

### Avec une fonction normale

```javascript
const utilisateur = {
  nom: "Alice",
  hobbies: ["lecture", "sport", "cuisine"],

  afficherHobbies() {
    console.log(`Hobbies de ${this.nom}:`);

    // ❌ Problème avec fonction normale
    this.hobbies.forEach(function(hobby) {
      // this ne pointe plus vers utilisateur !
      console.log(`${this.nom} aime ${hobby}`);
      // "undefined aime lecture"
    });
  }
};

utilisateur.afficherHobbies();
```

### Avec une arrow function

```javascript
const utilisateur = {
  nom: "Alice",
  hobbies: ["lecture", "sport", "cuisine"],

  afficherHobbies() {
    console.log(`Hobbies de ${this.nom}:`);

    // ✅ Solution avec arrow function
    this.hobbies.forEach((hobby) => {
      // this hérite du contexte, pointe vers utilisateur
      console.log(`${this.nom} aime ${hobby}`);
    });
  }
};

utilisateur.afficherHobbies();
// "Hobbies de Alice:"
// "Alice aime lecture"
// "Alice aime sport"
// "Alice aime cuisine"
```

## 8. Règle d'or : Quand utiliser quelle fonction ?

### ✅ Utilisez des fonctions normales pour :

#### 1. Les méthodes d'objets

```javascript
const personne = {
  nom: "Bob",

  // ✅ Fonction normale pour méthode
  saluer() {
    return `Bonjour, je suis ${this.nom}`;
  }
};
```

**Pourquoi ?** On veut que `this` pointe vers l'objet.

#### 2. Les constructeurs

```javascript
// ✅ Fonction normale pour constructeur
function Personne(nom) {
  this.nom = nom;
}
```

### ✅ Utilisez des arrow functions pour :

#### 1. Les callbacks dans les méthodes

```javascript
const timer = {
  secondes: 0,

  demarrer() {
    // ✅ Arrow function pour callback
    setInterval(() => {
      this.secondes++;
      console.log(this.secondes);
    }, 1000);
  }
};
```

#### 2. Les callbacks de méthodes de tableaux

```javascript
const liste = {
  nom: "Ma liste",
  items: [1, 2, 3, 4, 5],

  filtrerPairs() {
    // ✅ Arrow function dans filter
    return this.items.filter(item => item % 2 === 0);
  },

  doubler() {
    // ✅ Arrow function dans map
    return this.items.map(item => item * 2);
  }
};
```

#### 3. Fonctions simples sans `this`

```javascript
// ✅ Arrow function pour fonction simple
const double = x => x * 2;
const somme = (a, b) => a + b;
```

## 9. Exemples pratiques complets

### Exemple 1 : Gestionnaire d'événements

```javascript
const bouton = {
  texte: "Cliquez-moi",
  clics: 0,

  afficherStats() {
    console.log(`${this.texte} - Clics: ${this.clics}`);
  },

  configurerEvenement() {
    // Simuler un addEventListener
    const declencherClic = () => {
      // ✅ Arrow function : this = bouton
      this.clics++;
      this.afficherStats();
    };

    // Simulation d'événements
    declencherClic();
    declencherClic();
    declencherClic();
  }
};

bouton.configurerEvenement();
// "Cliquez-moi - Clics: 1"
// "Cliquez-moi - Clics: 2"
// "Cliquez-moi - Clics: 3"
```

### Exemple 2 : Traitement de données

```javascript
const analyseur = {
  nom: "Analyseur de données",
  donnees: [10, 25, 30, 45, 60, 75, 90],
  seuil: 50,

  analyser() {
    console.log(`=== ${this.nom} ===`);

    // ✅ Arrow functions pour garder le contexte
    const superieurs = this.donnees.filter(val => val > this.seuil);
    const inferieurs = this.donnees.filter(val => val <= this.seuil);

    console.log(`Valeurs > ${this.seuil}:`, superieurs);
    console.log(`Valeurs ≤ ${this.seuil}:`, inferieurs);

    // Calcul avec map
    const normalises = this.donnees.map(val => val / 100);
    console.log("Normalisés:", normalises);
  },

  trouverExtremes() {
    // ✅ Arrow function dans reduce
    const max = this.donnees.reduce((max, val) =>
      val > max ? val : max
    , this.donnees[0]);

    const min = this.donnees.reduce((min, val) =>
      val < min ? val : min
    , this.donnees[0]);

    console.log(`Min: ${min}, Max: ${max}`);
  }
};

analyseur.analyser();
analyseur.trouverExtremes();
```

### Exemple 3 : Minuteur avec callbacks

```javascript
const minuteur = {
  nom: "Minuteur principal",
  temps: 0,
  intervalId: null,

  demarrer() {
    console.log(`${this.nom} démarré`);

    // ✅ Arrow function pour conserver this
    this.intervalId = setInterval(() => {
      this.temps++;
      this.afficherTemps();

      if (this.temps >= 5) {
        this.arreter();
      }
    }, 1000);
  },

  arreter() {
    clearInterval(this.intervalId);
    console.log(`${this.nom} arrêté à ${this.temps}s`);
  },

  afficherTemps() {
    console.log(`${this.nom}: ${this.temps}s`);
  }
};

// minuteur.demarrer();
```

### Exemple 4 : Validation de formulaire

```javascript
const formulaire = {
  nom: "Formulaire d'inscription",
  champs: {
    email: "",
    motDePasse: "",
    confirmation: ""
  },
  erreurs: [],

  valider() {
    this.erreurs = [];  // Réinitialiser

    console.log(`Validation de ${this.nom}`);

    // ✅ Arrow function pour garder le contexte
    const regles = [
      {
        nom: "email",
        test: () => this.champs.email.includes("@"),
        message: "Email invalide"
      },
      {
        nom: "motDePasse",
        test: () => this.champs.motDePasse.length >= 8,
        message: "Mot de passe trop court"
      },
      {
        nom: "confirmation",
        test: () => this.champs.motDePasse === this.champs.confirmation,
        message: "Les mots de passe ne correspondent pas"
      }
    ];

    // Valider chaque règle
    regles.forEach(regle => {
      if (!regle.test()) {
        this.erreurs.push(regle.message);
      }
    });

    return this.erreurs.length === 0;
  },

  afficherErreurs() {
    if (this.erreurs.length === 0) {
      console.log("✓ Validation réussie");
    } else {
      console.log("✗ Erreurs:");
      this.erreurs.forEach(erreur => console.log(`  - ${erreur}`));
    }
  },

  remplir(email, motDePasse, confirmation) {
    this.champs.email = email;
    this.champs.motDePasse = motDePasse;
    this.champs.confirmation = confirmation;
  }
};

// Test
formulaire.remplir("alice@example.com", "motdepasse123", "motdepasse123");
formulaire.valider();
formulaire.afficherErreurs();

formulaire.remplir("email-invalide", "court", "different");
formulaire.valider();
formulaire.afficherErreurs();
```

## 10. Cas particuliers et subtilités

### Méthodes avec callbacks multiples

```javascript
const processeur = {
  nom: "Processeur",
  donnees: [1, 2, 3, 4, 5],

  traiter() {
    // ✅ Toutes les arrow functions héritent du même this
    return this.donnees
      .filter(n => n > 2)              // this = processeur
      .map(n => n * 2)                 // this = processeur
      .reduce((sum, n) => sum + n, 0); // this = processeur
  }
};

console.log(processeur.traiter());  // 24
```

### Arrow functions et objets imbriqués

```javascript
const app = {
  nom: "MonApp",
  config: {
    theme: "sombre",

    // ❌ Arrow function comme méthode : ne marche pas
    afficherTheme: () => {
      console.log(this.theme);  // undefined (this ne pointe pas vers config)
    },

    // ✅ Fonction normale : fonctionne
    afficherThemeBon() {
      console.log(this.theme);  // "sombre"
    }
  }
};
```

## 11. Le piège des arrow functions comme méthodes

### ❌ N'utilisez JAMAIS d'arrow functions comme méthodes d'objets

```javascript
const utilisateur = {
  nom: "Alice",

  // ❌ MAUVAIS : arrow function comme méthode
  saluerMauvais: () => {
    console.log(`Bonjour ${this.nom}`);  // undefined !
  },

  // ✅ BON : fonction normale comme méthode
  saluerBon() {
    console.log(`Bonjour ${this.nom}`);  // "Bonjour Alice"
  }
};

utilisateur.saluerMauvais();  // "Bonjour undefined"
utilisateur.saluerBon();      // "Bonjour Alice"
```

**Pourquoi ?** L'arrow function hérite du `this` du contexte extérieur (Window ou global), pas de l'objet.

### Mais utilisez des arrow functions DANS les méthodes

```javascript
const gestionnaire = {
  nom: "Gestionnaire",
  items: [1, 2, 3],

  // ✅ Méthode normale
  traiter() {
    // ✅ Arrow function dans la méthode
    this.items.forEach(item => {
      console.log(`${this.nom} traite ${item}`);
    });
  }
};

gestionnaire.traiter();
// "Gestionnaire traite 1"
// "Gestionnaire traite 2"
// "Gestionnaire traite 3"
```

## 12. Méthodes bind, call et apply

Ces méthodes permettent de contrôler manuellement la valeur de `this` (nous les verrons en détail dans la section 5.13.3).

### Aperçu rapide

```javascript
const personne1 = {
  nom: "Alice"
};

const personne2 = {
  nom: "Bob"
};

function saluer() {
  console.log(`Bonjour, je suis ${this.nom}`);
}

// call : appelle immédiatement avec un this spécifique
saluer.call(personne1);  // "Bonjour, je suis Alice"
saluer.call(personne2);  // "Bonjour, je suis Bob"

// bind : crée une nouvelle fonction avec un this fixe
const saluerAlice = saluer.bind(personne1);
saluerAlice();  // "Bonjour, je suis Alice"
```

## 13. Tableaux récapitulatifs

### Comportement de `this`

| Contexte | Valeur de `this` | Exemple |
|----------|------------------|---------|
| Méthode d'objet | L'objet lui-même | `obj.methode()` |
| Fonction normale (strict) | `undefined` | `function() {}` |
| Fonction normale (non-strict) | `window`/`global` | `function() {}` |
| Arrow function | Hérite du contexte | `() => {}` |
| Callback avec fonction normale | Dépend du contexte | `setTimeout(function() {})` |
| Callback avec arrow function | Hérite de la méthode | `setTimeout(() => {})` |

### Quand utiliser quelle fonction ?

| Situation | Utiliser | Raison |
|-----------|----------|--------|
| Méthode d'objet | Fonction normale | Besoin que `this` = objet |
| Callback dans méthode | Arrow function | Garder le `this` de la méthode |
| Méthode de tableau | Arrow function | Accéder au `this` extérieur |
| Constructeur | Fonction normale | Créer un nouveau contexte |
| Fonction standalone | Arrow function | Plus concis, pas de `this` |

## 14. Bonnes pratiques

### 1. Arrow functions pour les callbacks

```javascript
// ✅ Bon
const timer = {
  secondes: 0,
  demarrer() {
    setInterval(() => {
      this.secondes++;
    }, 1000);
  }
};

// ❌ Éviter (nécessite self/that ou bind)
const timer = {
  secondes: 0,
  demarrer() {
    const self = this;
    setInterval(function() {
      self.secondes++;
    }, 1000);
  }
};
```

### 2. Fonctions normales pour les méthodes

```javascript
// ✅ Bon
const objet = {
  valeur: 42,
  afficher() {
    console.log(this.valeur);
  }
};

// ❌ Mauvais
const objet = {
  valeur: 42,
  afficher: () => {
    console.log(this.valeur);  // undefined
  }
};
```

### 3. Cohérence dans le code

```javascript
// ✅ Cohérent et clair
const collection = {
  items: [1, 2, 3, 4, 5],

  // Méthode normale
  filtrerPairs() {
    // Arrow function dans le callback
    return this.items.filter(n => n % 2 === 0);
  },

  // Méthode normale
  mapper() {
    // Arrow function dans le callback
    return this.items.map(n => n * 2);
  }
};
```

## 15. Pièges courants

### Piège 1 : Arrow function comme méthode

```javascript
const obj = {
  valeur: 42,
  // ❌ Ne fonctionne pas
  methode: () => {
    console.log(this.valeur);  // undefined
  }
};
```

### Piège 2 : Extraire une méthode

```javascript
const compteur = {
  val: 0,
  incrementer() {
    this.val++;
  }
};

// ❌ Perte du contexte
const inc = compteur.incrementer;
inc();  // Erreur ou comportement inattendu

// ✅ Solution : bind
const inc = compteur.incrementer.bind(compteur);
inc();  // Fonctionne
```

### Piège 3 : `this` dans les fonctions imbriquées

```javascript
const objet = {
  nom: "Test",

  methode() {
    console.log(this.nom);  // "Test"

    // ❌ Fonction normale imbriquée : perd this
    function fonctionInterne() {
      console.log(this.nom);  // undefined
    }
    fonctionInterne();

    // ✅ Arrow function : garde this
    const arrowInterne = () => {
      console.log(this.nom);  // "Test"
    };
    arrowInterne();
  }
};
```

## 16. Debugging de `this`

Techniques pour comprendre la valeur de `this` :

```javascript
const objet = {
  nom: "MonObjet",

  debugger() {
    // Afficher this
    console.log("this =", this);

    // Vérifier le type
    console.log("Type de this:", typeof this);

    // Lister les propriétés
    console.log("Propriétés de this:", Object.keys(this));

    // Vérifier l'identité
    console.log("this === objet ?", this === objet);
  }
};

objet.debugger();
```

## Points clés à retenir

1. **`this`** fait référence à un objet selon le **contexte d'appel**
2. Dans une **méthode d'objet**, `this` = l'objet lui-même
3. Les **fonctions normales** ont leur propre `this`
4. Les **arrow functions** héritent du `this` du contexte parent
5. **Utilisez des fonctions normales** pour les méthodes d'objets
6. **Utilisez des arrow functions** pour les callbacks dans les méthodes
7. **JAMAIS** d'arrow function comme méthode d'objet
8. Le problème classique : perte de contexte dans les callbacks

## Schéma mental

```
MÉTHODE D'OBJET
├── Fonction normale → this = objet ✅
└── Arrow function → this ≠ objet ❌

CALLBACK DANS MÉTHODE
├── Fonction normale → this perdu ❌
└── Arrow function → this conservé ✅
```

## Ce qui vient ensuite

Dans les prochaines sections, vous allez découvrir :
- Les constructeurs et le mot-clé `new`
- Les classes ES6 et leur utilisation de `this`
- Les méthodes `bind()`, `call()` et `apply()` en détail
- La programmation orientée objet en JavaScript

Comprendre `this` et les arrow functions est **crucial** pour maîtriser JavaScript. Prenez le temps de bien assimiler ces concepts !

⏭️ [Constructeurs et new (introduction)](/05-javascript-moderne-fondamentaux/07-objets-modernes/09-constructeurs-new.md)
