🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.12.5 Debugging : console.log, console.table, console.error

## Introduction

La console du navigateur est votre meilleur ami pour déboguer votre code JavaScript. Elle vous permet d'afficher des informations, de tracer l'exécution de votre programme et de détecter les problèmes. Maîtriser les différentes méthodes de `console` vous fera gagner énormément de temps !

> 💡 **Important** : Ouvrez toujours la console du navigateur (F12 ou Ctrl+Shift+I / Cmd+Option+I) quand vous développez en JavaScript.

---

## L'objet console

L'objet `console` est disponible partout dans votre code JavaScript. Il offre de nombreuses méthodes pour afficher des informations de différentes manières.

```javascript
// Accessible partout
console.log("La console est disponible !");
```

---

## console.log() - La méthode de base

### Qu'est-ce que c'est ?

`console.log()` est la méthode la plus utilisée. Elle affiche des messages dans la console du navigateur.

### Syntaxe

```javascript
console.log(message1, message2, ..., messageN);
```

### Exemples de base

```javascript
// Message simple
console.log("Bonjour !");

// Variable
const nom = "Alice";
console.log(nom);

// Plusieurs valeurs
console.log("Nom:", nom, "Âge:", 25);

// Expression
console.log(5 + 3);  // Affiche 8
```

### Afficher des variables

```javascript
const prenom = "Bob";
const age = 30;
const ville = "Paris";

// ❌ Pas très clair
console.log(prenom);
console.log(age);
console.log(ville);

// ✅ Mieux - avec étiquettes
console.log("Prénom:", prenom);
console.log("Âge:", age);
console.log("Ville:", ville);

// ✅ Encore mieux - tout en une fois
console.log("Prénom:", prenom, "Âge:", age, "Ville:", ville);
```

### Afficher des objets

```javascript
const utilisateur = {
    nom: "Dupont",
    prenom: "Marie",
    age: 28,
    ville: "Lyon"
};

// La console affiche l'objet de manière interactive
console.log(utilisateur);

// Avec un label
console.log("Utilisateur:", utilisateur);
```

### Afficher des tableaux

```javascript
const fruits = ["Pomme", "Banane", "Orange", "Kiwi"];

console.log(fruits);
// Affiche : ["Pomme", "Banane", "Orange", "Kiwi"]

// Avec index et longueur
console.log("Fruits:", fruits, "Nombre:", fruits.length);
```

### Template literals dans console.log

```javascript
const nom = "Alice";
const score = 95;

// ✅ Utilisation de template literals pour plus de clarté
console.log(`${nom} a obtenu un score de ${score}`);
```

---

## console.error() - Afficher des erreurs

### Qu'est-ce que c'est ?

`console.error()` affiche un message d'erreur dans la console, généralement en rouge et avec une icône d'erreur.

### Syntaxe

```javascript
console.error(message1, message2, ..., messageN);
```

### Utilisation

```javascript
// Message d'erreur simple
console.error("Une erreur s'est produite !");

// Avec contexte
const userId = 123;
console.error("Impossible de charger l'utilisateur", userId);

// Afficher un objet Error
try {
    throw new Error("Quelque chose a mal tourné");
} catch (erreur) {
    console.error(erreur);
}
```

### Différence visuelle avec log

```javascript
console.log("Ceci est un message normal");        // Texte noir
console.error("Ceci est un message d'erreur");    // Texte rouge avec ❌
```

### Cas d'usage pratiques

```javascript
function diviser(a, b) {
    if (b === 0) {
        console.error("Erreur: Division par zéro !");
        return null;
    }
    return a / b;
}

function chargerUtilisateur(id) {
    if (!id) {
        console.error("Erreur: ID utilisateur manquant");
        return null;
    }
    // Chargement...
}
```

---

## console.warn() - Afficher des avertissements

### Qu'est-ce que c'est ?

`console.warn()` affiche un message d'avertissement, généralement en jaune/orange.

### Utilisation

```javascript
// Avertissement simple
console.warn("Attention : Cette fonctionnalité est dépréciée");

// Avertissement avec contexte
const age = 17;
if (age < 18) {
    console.warn("L'utilisateur est mineur");
}
```

### Différence avec error et log

```javascript
console.log("Information normale");        // Noir
console.warn("Avertissement");            // Orange/Jaune avec ⚠️
console.error("Erreur critique");         // Rouge avec ❌
```

---

## console.table() - Afficher des tableaux structurés

### Qu'est-ce que c'est ?

`console.table()` affiche les données sous forme de tableau, ce qui est très pratique pour visualiser des tableaux d'objets ou des objets complexes.

### Syntaxe

```javascript
console.table(data);
console.table(data, columns);  // Optionnel : spécifier les colonnes
```

### Tableau d'objets

```javascript
const utilisateurs = [
    { id: 1, nom: "Dupont", prenom: "Alice", age: 25 },
    { id: 2, nom: "Martin", prenom: "Bob", age: 30 },
    { id: 3, nom: "Durand", prenom: "Claire", age: 28 }
];

console.table(utilisateurs);
```

**Résultat dans la console :**
```
┌─────────┬────┬──────────┬─────────┬─────┐
│ (index) │ id │   nom    │ prenom  │ age │
├─────────┼────┼──────────┼─────────┼─────┤
│    0    │ 1  │ 'Dupont' │ 'Alice' │ 25  │
│    1    │ 2  │ 'Martin' │  'Bob'  │ 30  │
│    2    │ 3  │ 'Durand' │'Claire' │ 28  │
└─────────┴────┴──────────┴─────────┴─────┘
```

### Tableau simple

```javascript
const nombres = [10, 20, 30, 40, 50];
console.table(nombres);

const fruits = ["Pomme", "Banane", "Orange"];
console.table(fruits);
```

### Objet simple

```javascript
const personne = {
    nom: "Dupont",
    prenom: "Alice",
    age: 25,
    ville: "Paris"
};

console.table(personne);
```

**Résultat :**
```
┌─────────┬──────────┐
│ (index) │  Values  │
├─────────┼──────────┤
│   nom   │ 'Dupont' │
│ prenom  │ 'Alice'  │
│   age   │    25    │
│  ville  │ 'Paris'  │
└─────────┴──────────┘
```

### Spécifier les colonnes

```javascript
const produits = [
    { id: 1, nom: "Laptop", prix: 999, stock: 5, categorie: "Informatique" },
    { id: 2, nom: "Souris", prix: 25, stock: 50, categorie: "Accessoires" },
    { id: 3, nom: "Clavier", prix: 79, stock: 20, categorie: "Accessoires" }
];

// Afficher seulement certaines colonnes
console.table(produits, ["nom", "prix"]);
```

### Quand utiliser console.table ?

- ✅ Visualiser des tableaux d'objets
- ✅ Comparer rapidement des données structurées
- ✅ Déboguer des résultats de requêtes API
- ✅ Examiner des données JSON

---

## console.dir() - Explorer les objets en profondeur

### Qu'est-ce que c'est ?

`console.dir()` affiche un objet sous forme d'arborescence interactive, idéal pour explorer des objets complexes ou des éléments DOM.

### Utilisation

```javascript
const objet = {
    nom: "Test",
    donnees: {
        valeur1: 10,
        valeur2: 20,
        nested: {
            deep: "valeur profonde"
        }
    }
};

console.dir(objet);
```

### Différence avec console.log

```javascript
const element = document.querySelector('body');

console.log(element);   // Affiche l'élément HTML
console.dir(element);   // Affiche l'objet JavaScript avec toutes ses propriétés
```

---

## console.clear() - Nettoyer la console

### Qu'est-ce que c'est ?

`console.clear()` efface tout le contenu de la console.

### Utilisation

```javascript
console.log("Message 1");
console.log("Message 2");
console.log("Message 3");

console.clear();  // Efface tout

console.log("Nouvelle session");
```

---

## console.group() et console.groupEnd() - Grouper les messages

### Qu'est-ce que c'est ?

Ces méthodes permettent de créer des groupes de messages pliables dans la console.

### Syntaxe

```javascript
console.group(label);
// Messages à grouper
console.groupEnd();
```

### Exemple simple

```javascript
console.group("Informations utilisateur");
console.log("Nom: Alice");
console.log("Âge: 25");
console.log("Ville: Paris");
console.groupEnd();

console.group("Produits");
console.log("Laptop - 999€");
console.log("Souris - 25€");
console.groupEnd();
```

### Groupes imbriqués

```javascript
console.group("Application");
    console.log("Version: 1.0.0");

    console.group("Configuration");
        console.log("API URL: https://api.example.com");
        console.log("Timeout: 5000ms");
    console.groupEnd();

    console.group("Utilisateur");
        console.log("ID: 123");
        console.log("Role: Admin");
    console.groupEnd();
console.groupEnd();
```

### console.groupCollapsed()

Comme `group()` mais le groupe est replié par défaut.

```javascript
console.groupCollapsed("Détails techniques");
console.log("Info 1");
console.log("Info 2");
console.log("Info 3");
console.groupEnd();
```

---

## console.count() - Compter les appels

### Qu'est-ce que c'est ?

`console.count()` compte le nombre de fois qu'une ligne est exécutée.

### Utilisation

```javascript
function traiterItem(item) {
    console.count("Fonction appelée");
    // Traitement...
}

traiterItem("A");  // Fonction appelée: 1
traiterItem("B");  // Fonction appelée: 2
traiterItem("C");  // Fonction appelée: 3
```

### Avec des labels différents

```javascript
function processus(type) {
    if (type === "A") {
        console.count("Type A");
    } else {
        console.count("Type B");
    }
}

processus("A");  // Type A: 1
processus("A");  // Type A: 2
processus("B");  // Type B: 1
processus("A");  // Type A: 3
```

### console.countReset()

```javascript
console.count("Compteur");  // Compteur: 1
console.count("Compteur");  // Compteur: 2
console.countReset("Compteur");
console.count("Compteur");  // Compteur: 1
```

---

## console.time() et console.timeEnd() - Mesurer le temps

### Qu'est-ce que c'est ?

Ces méthodes permettent de mesurer le temps d'exécution d'un bout de code.

### Syntaxe

```javascript
console.time(label);
// Code à mesurer
console.timeEnd(label);
```

### Exemple simple

```javascript
console.time("Calcul");

let total = 0;
for (let i = 0; i < 1000000; i++) {
    total += i;
}

console.timeEnd("Calcul");
// Affiche : Calcul: 5.234ms
```

### Plusieurs timers en parallèle

```javascript
console.time("Opération A");
console.time("Opération B");

// Opération A
setTimeout(() => {
    console.timeEnd("Opération A");
}, 1000);

// Opération B
setTimeout(() => {
    console.timeEnd("Opération B");
}, 500);
```

### Mesurer des performances

```javascript
function comparerMethodes() {
    const tableau = Array.from({ length: 100000 }, (_, i) => i);

    // Méthode 1 : boucle for
    console.time("Boucle for");
    let somme1 = 0;
    for (let i = 0; i < tableau.length; i++) {
        somme1 += tableau[i];
    }
    console.timeEnd("Boucle for");

    // Méthode 2 : reduce
    console.time("Reduce");
    const somme2 = tableau.reduce((acc, val) => acc + val, 0);
    console.timeEnd("Reduce");
}

comparerMethodes();
```

---

## console.assert() - Assertions

### Qu'est-ce que c'est ?

`console.assert()` affiche un message d'erreur si une condition est fausse.

### Syntaxe

```javascript
console.assert(condition, message);
```

### Utilisation

```javascript
const age = 15;

console.assert(age >= 18, "L'utilisateur doit être majeur");
// Affiche une erreur car la condition est fausse

console.assert(age >= 0, "L'âge doit être positif");
// N'affiche rien car la condition est vraie
```

### Exemple pratique

```javascript
function diviser(a, b) {
    console.assert(b !== 0, "Division par zéro impossible");
    return a / b;
}

diviser(10, 2);  // Pas d'erreur
diviser(10, 0);  // Affiche l'assertion
```

---

## console.trace() - Afficher la pile d'appels

### Qu'est-ce que c'est ?

`console.trace()` affiche la pile d'appels (stack trace) pour savoir comment on est arrivé à un certain point du code.

### Utilisation

```javascript
function fonctionA() {
    fonctionB();
}

function fonctionB() {
    fonctionC();
}

function fonctionC() {
    console.trace("Comment sommes-nous arrivés ici ?");
}

fonctionA();
```

**Résultat :**
```
Comment sommes-nous arrivés ici ?
    fonctionC @ script.js:10
    fonctionB @ script.js:6
    fonctionA @ script.js:2
```

---

## Techniques de debugging avancées

### 1. Débogage d'objets avec des labels

```javascript
const user1 = { nom: "Alice", age: 25 };
const user2 = { nom: "Bob", age: 30 };

// ❌ Pas clair
console.log(user1);
console.log(user2);

// ✅ Mieux
console.log("User 1:", user1);
console.log("User 2:", user2);

// ✅ Encore mieux - astuce avec accolades
console.log({ user1, user2 });
// Affiche : { user1: {...}, user2: {...} }
```

### 2. Utiliser %c pour styler les messages

```javascript
console.log(
    "%cMessage Important",
    "color: red; font-size: 20px; font-weight: bold"
);

console.log(
    "%cSuccès%c Opération terminée",
    "color: green; font-weight: bold",
    "color: black"
);
```

### 3. Debugging conditionnel

```javascript
const DEBUG = true;

function debugLog(...args) {
    if (DEBUG) {
        console.log(...args);
    }
}

debugLog("Ce message s'affiche seulement en mode debug");
```

### 4. Afficher le type d'une variable

```javascript
function afficherType(variable) {
    console.log(
        "Valeur:", variable,
        "Type:", typeof variable,
        "Constructeur:", variable?.constructor?.name
    );
}

afficherType(42);
afficherType("texte");
afficherType([1, 2, 3]);
afficherType({ nom: "Alice" });
```

### 5. Déboguer des boucles

```javascript
const produits = [
    { id: 1, nom: "Laptop", prix: 999 },
    { id: 2, nom: "Souris", prix: 25 },
    { id: 3, nom: "Clavier", prix: 79 }
];

console.group("Traitement des produits");
produits.forEach((produit, index) => {
    console.log(`Produit ${index + 1}:`, produit.nom, "-", produit.prix + "€");
});
console.groupEnd();
```

---

## Tableau récapitulatif des méthodes

| Méthode | Usage | Quand l'utiliser ? |
|---------|-------|-------------------|
| `console.log()` | Message général | Débuggage courant |
| `console.error()` | Message d'erreur | Erreurs et exceptions |
| `console.warn()` | Avertissement | Situations à surveiller |
| `console.table()` | Tableau structuré | Tableaux d'objets |
| `console.dir()` | Exploration d'objet | Objets complexes, DOM |
| `console.group()` | Grouper messages | Organiser les logs |
| `console.count()` | Compter appels | Suivre nombre d'exécutions |
| `console.time()` | Mesurer temps | Optimisation performance |
| `console.assert()` | Vérifier condition | Tests simples |
| `console.trace()` | Pile d'appels | Tracer le flux d'exécution |
| `console.clear()` | Nettoyer console | Commencer une nouvelle session |

---

## Bonnes pratiques

### ✅ À faire

**1. Utiliser des messages descriptifs**

```javascript
// ✅ Bon
console.log("Chargement de l'utilisateur ID:", userId);

// ❌ Mauvais
console.log(userId);
```

**2. Grouper les logs liés**

```javascript
// ✅ Bon
console.group("Validation du formulaire");
console.log("Nom:", nom);
console.log("Email:", email);
console.log("Âge:", age);
console.groupEnd();
```

**3. Utiliser le bon niveau de log**

```javascript
// ✅ Bon
console.log("Information générale");
console.warn("Attention: paramètre déprécié");
console.error("Erreur critique: connexion échouée");
```

**4. Utiliser console.table pour les données structurées**

```javascript
// ✅ Bon
console.table(utilisateurs);

// ❌ Moins lisible
console.log(utilisateurs);
```

### ❌ À éviter

**1. Trop de console.log**

```javascript
// ❌ Mauvais - pollution de la console
console.log("1");
console.log("2");
console.log("3");
// ...

// ✅ Mieux
console.log("Étapes:", 1, 2, 3);
```

**2. Laisser des console.log en production**

```javascript
// ❌ À retirer avant déploiement
console.log("Debug: valeur de x =", x);

// ✅ Utiliser une fonction de debug conditionnelle
if (process.env.NODE_ENV === 'development') {
    console.log("Debug: valeur de x =", x);
}
```

**3. Console.log dans des boucles massives**

```javascript
// ❌ Très mauvais - ralentit l'application
for (let i = 0; i < 100000; i++) {
    console.log(i);
}

// ✅ Mieux - log seulement ce qui est nécessaire
console.log("Début de la boucle");
for (let i = 0; i < 100000; i++) {
    // Traitement...
}
console.log("Fin de la boucle");
```

---

## Astuces pratiques

### 1. Raccourci pour console.log

```javascript
// Créer un alias court
const c = console.log;
c("Message rapide");
```

### 2. Afficher plusieurs variables avec leurs noms

```javascript
const nom = "Alice";
const age = 25;
const ville = "Paris";

// ✅ Astuce : utiliser un objet
console.log({ nom, age, ville });
// Affiche : { nom: "Alice", age: 25, ville: "Paris" }
```

### 3. Console.log qui retourne la valeur

```javascript
// Astuce pour déboguer dans une chaîne
const resultat = calculComplexe(
    console.log(valeur1) || valeur1,
    console.log(valeur2) || valeur2
);
```

### 4. Copier un objet depuis la console

Dans la console du navigateur, vous pouvez :
```javascript
// 1. Afficher l'objet
console.log(monObjet);

// 2. Clic droit sur l'objet dans la console
// 3. "Copy object" ou "Store as global variable"
```

---

## Exemple complet de debugging

```javascript
function traiterCommande(commande) {
    console.group("🛒 Traitement de la commande");
    console.time("Durée totale");

    // Vérification de la commande
    console.log("📦 Commande reçue:", commande);
    console.assert(commande, "La commande ne peut pas être vide");

    // Validation
    console.group("✅ Validation");
    const valide = validerCommande(commande);
    console.log("Résultat:", valide ? "✓ Valide" : "✗ Invalide");
    console.groupEnd();

    if (!valide) {
        console.error("❌ Commande invalide, arrêt du traitement");
        console.groupEnd();
        return false;
    }

    // Traitement des articles
    console.group("📋 Articles");
    console.table(commande.articles, ["nom", "quantite", "prix"]);
    console.groupEnd();

    // Calcul du total
    console.time("Calcul du total");
    const total = calculerTotal(commande.articles);
    console.timeEnd("Calcul du total");
    console.log("💰 Total:", total + "€");

    // Fin
    console.timeEnd("Durée totale");
    console.groupEnd();

    return true;
}

function validerCommande(commande) {
    return commande && commande.articles && commande.articles.length > 0;
}

function calculerTotal(articles) {
    return articles.reduce((total, article) => {
        return total + (article.prix * article.quantite);
    }, 0);
}

// Test
const commande = {
    id: 123,
    client: "Alice",
    articles: [
        { nom: "Laptop", quantite: 1, prix: 999 },
        { nom: "Souris", quantite: 2, prix: 25 }
    ]
};

traiterCommande(commande);
```

---

## Points clés à retenir

1. **console.log()** est votre outil de base pour le debugging quotidien

2. **console.error()** pour les erreurs et **console.warn()** pour les avertissements

3. **console.table()** est parfait pour visualiser des tableaux d'objets

4. **console.group()** aide à organiser les messages liés

5. **console.time()** mesure les performances

6. **Utilisez des messages clairs** avec du contexte

7. **Retirez les console.log** avant de mettre en production

8. **La console est interactive** - explorez les objets en cliquant dessus

---

## Prochaines étapes

Dans la prochaine section, vous apprendrez :
- Comment utiliser les breakpoints dans les DevTools
- Le debugging pas à pas
- L'inspection des variables en temps réel
- Les techniques avancées de debugging

> 💡 **Conseil** : Prenez l'habitude d'utiliser `console.table()` pour les tableaux d'objets et `console.group()` pour organiser vos messages. Votre debugging sera beaucoup plus clair et efficace !

⏭️ [Utilisation des breakpoints dans DevTools](/05-javascript-moderne-fondamentaux/12-gestion-erreurs/06-breakpoints-devtools.md)
