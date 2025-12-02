🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Annexe B - Glossaire des Termes Techniques

Ce glossaire regroupe les termes techniques essentiels du développement web moderne. Chaque terme est expliqué de manière simple et accessible, avec des exemples concrets pour faciliter la compréhension.

**💡 Conseil de lecture :** Ne cherchez pas à tout mémoriser d'un coup ! Revenez consulter ce glossaire chaque fois que vous rencontrez un terme inconnu.

---

## A

### API (Application Programming Interface)
**Interface de Programmation d'Application**

Une API est un ensemble de règles et de protocoles qui permet à différents logiciels de communiquer entre eux.

**Exemple concret :**
```javascript
// API Fetch pour récupérer des données
fetch('https://api.exemple.com/data')
  .then(response => response.json())
  .then(data => console.log(data));
```

**APIs web courantes :** Fetch API, DOM API, Geolocation API, LocalStorage API

### Accessibilité (a11y)
La capacité d'un site web à être utilisé par tous, y compris les personnes en situation de handicap (visuel, auditif, moteur, cognitif).

**Pourquoi "a11y" ?**
- **a** = première lettre
- **11** = nombre de lettres entre "a" et "y"
- **y** = dernière lettre

**Exemple :**
```html
<!-- ❌ Pas accessible -->
<div onclick="submit()">Envoyer</div>

<!-- ✅ Accessible -->
<button type="submit">Envoyer</button>
```

### Argument
Valeur passée à une fonction lors de son appel.

**Exemple :**
```javascript
function saluer(nom) { // nom = paramètre
  console.log('Bonjour ' + nom);
}

saluer('Marie'); // 'Marie' = argument
```

### Arrow Function (Fonction Fléchée)
Syntaxe moderne et concise pour écrire des fonctions en JavaScript (ES6+).

**Exemple :**
```javascript
// Fonction classique
function addition(a, b) {
  return a + b;
}

// Arrow function
const addition = (a, b) => a + b;
```

### Asynchrone
Se dit d'une opération qui ne bloque pas l'exécution du code. Le programme continue pendant que l'opération se termine en arrière-plan.

**Exemple :**
```javascript
console.log('1');
setTimeout(() => console.log('2'), 1000);
console.log('3');
// Affiche : 1, 3, 2 (le 2 arrive après car asynchrone)
```

### Async/Await
Syntaxe moderne pour gérer le code asynchrone de manière plus lisible.

**Exemple :**
```javascript
async function recupererDonnees() {
  const response = await fetch('https://api.exemple.com');
  const data = await response.json();
  return data;
}
```

### Attribut
Information supplémentaire donnée à une balise HTML.

**Exemple :**
```html
<img src="photo.jpg" alt="Ma photo" width="500">
<!--  └── attributs: src, alt, width -->
```

---

## B

### Babel
Outil de transpilation qui convertit le JavaScript moderne (ES6+) en JavaScript compatible avec les anciens navigateurs.

### Backend (Arrière-plan)
Partie d'une application web qui s'exécute sur le serveur. Gère la logique métier, les bases de données, l'authentification.

**Technologies backend courantes :** Node.js, PHP, Python, Ruby, Java

### Balise (Tag)
Élément de base du HTML qui structure le contenu. Les balises sont entourées de chevrons `< >`.

**Types de balises :**
```html
<!-- Balise avec ouverture et fermeture -->
<p>Contenu</p>

<!-- Balise auto-fermante -->
<img src="photo.jpg" />
<br />
```

### Block-level Element
Élément HTML qui occupe toute la largeur disponible et commence sur une nouvelle ligne.

**Exemples :** `<div>`, `<p>`, `<h1>`, `<section>`, `<ul>`

### Box Model (Modèle de boîte)
Concept CSS qui définit comment est calculée la taille totale d'un élément.

**Composants :**
```
┌───────────────────────────┐
│       MARGIN              │
│  ┌────────────────────┐   │
│  │    BORDER          │   │
│  │  ┌─────────────┐   │   │
│  │  │  PADDING    │   │   │
│  │  │  ┌───────┐  │   │   │
│  │  │  │CONTENT│  │   │   │
│  │  │  └───────┘  │   │   │
│  │  └─────────────┘   │   │
│  └────────────────────┘   │
└───────────────────────────┘
```

### Breakpoint
Point de rupture en design responsive où la mise en page change pour s'adapter à différentes tailles d'écran.

**Exemple :**
```css
/* Mobile par défaut */
.container { width: 100%; }

/* Tablette à partir de 768px */
@media (min-width: 768px) {
  .container { width: 750px; }
}

/* Desktop à partir de 1024px */
@media (min-width: 1024px) {
  .container { width: 1000px; }
}
```

### Browser (Navigateur)
Logiciel permettant de consulter le web.

**Navigateurs modernes :** Chrome, Firefox, Safari, Edge, Brave

### Bubbling (Bouillonnement)
Mécanisme de propagation des événements qui remontent des éléments enfants vers les parents.

**Exemple :**
```html
<div onclick="alert('div')">
  <button onclick="alert('button')">Cliquez</button>
</div>
<!-- Clic sur le bouton → affiche "button" puis "div" -->
```

### Bug
Erreur dans le code qui cause un comportement inattendu ou incorrect.

### Bundler
Outil qui regroupe plusieurs fichiers JavaScript/CSS en un ou quelques fichiers optimisés.

**Exemples populaires :** Vite, Webpack, Rollup, Parcel

---

## C

### Callback
Fonction passée en argument à une autre fonction, qui sera exécutée plus tard.

**Exemple :**
```javascript
function traiterDonnees(callback) {
  const resultat = 42;
  callback(resultat);
}

traiterDonnees(function(resultat) {
  console.log(resultat); // 42
});
```

### Callback Hell
Situation où plusieurs callbacks sont imbriqués, rendant le code difficile à lire et maintenir.

**Exemple du problème :**
```javascript
getData(function(a) {
  getMoreData(a, function(b) {
    getMoreData(b, function(c) {
      getMoreData(c, function(d) {
        // 😱 Pyramide de la mort
      });
    });
  });
});
```

**Solution moderne :** Utiliser Promises ou async/await

### Cascade (CSS)
Mécanisme qui détermine quel style appliquer lorsque plusieurs règles CSS ciblent le même élément.

**Ordre de priorité (du plus fort au plus faible) :**
1. `!important`
2. Styles inline (`style=""`)
3. ID (`#monId`)
4. Classes, attributs, pseudo-classes (`.maClasse`, `[type="text"]`, `:hover`)
5. Éléments et pseudo-éléments (`p`, `::before`)

### CDN (Content Delivery Network)
Réseau de serveurs distribués géographiquement qui délivre du contenu web rapidement.

**Exemple d'utilisation :**
```html
<!-- Charger une bibliothèque depuis un CDN -->
<script src="https://cdn.jsdelivr.net/npm/library@1.0.0/dist/library.min.js"></script>
```

### Cheatsheet (Antisèche)
Document de référence rapide qui résume les commandes et syntaxes essentielles d'une technologie.

### Client-side (Côté client)
Code qui s'exécute dans le navigateur de l'utilisateur (HTML, CSS, JavaScript).

### Closure (Fermeture)
Fonction qui a accès aux variables de sa portée parent, même après que la fonction parent ait terminé son exécution.

**Exemple :**
```javascript
function compteur() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}

const incrementer = compteur();
console.log(incrementer()); // 1
console.log(incrementer()); // 2
```

### Code Source
Ensemble des fichiers texte contenant le code d'un programme (HTML, CSS, JavaScript).

### Commentaire
Texte dans le code source qui n'est pas exécuté, utilisé pour documenter et expliquer.

**Exemples :**
```html
<!-- Commentaire HTML -->
```

```css
/* Commentaire CSS */
```

```javascript
// Commentaire JavaScript sur une ligne
/* Commentaire JavaScript
   sur plusieurs lignes */
```

### Compilation
Processus de transformation du code source en code exécutable.

### Composant
Élément réutilisable et indépendant d'une interface utilisateur (concept des frameworks comme React, Vue).

### const
Mot-clé moderne pour déclarer une constante (variable dont la valeur ne peut pas être réassignée).

**Exemple :**
```javascript
const PI = 3.14159;
const utilisateur = { nom: 'Alice' };

// ❌ Erreur : on ne peut pas réassigner
PI = 3.14;

// ✅ OK : on peut modifier les propriétés d'un objet
utilisateur.nom = 'Bob';
```

### CSS (Cascading Style Sheets)
Langage qui décrit la présentation et le style des documents HTML.

### CSS Grid
Système de mise en page CSS bidimensionnel (lignes et colonnes).

**Exemple :**
```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
}
```

---

## D

### Debugging (Débogage)
Processus de recherche et correction des bugs dans le code.

**Outils :** Console, breakpoints, DevTools

### Déclaration
Instruction qui crée une variable, une fonction ou toute autre entité.

**Exemple :**
```javascript
const nom = 'Alice'; // Déclaration de variable
function saluer() {} // Déclaration de fonction
```

### Destructuring (Déstructuration)
Syntaxe permettant d'extraire des valeurs d'objets ou de tableaux.

**Exemple :**
```javascript
// Objets
const personne = { nom: 'Alice', age: 30 };
const { nom, age } = personne;

// Tableaux
const nombres = [1, 2, 3];
const [premier, deuxieme] = nombres;
```

### DevTools (Outils de Développement)
Ensemble d'outils intégrés aux navigateurs pour inspecter, déboguer et optimiser les sites web.

**Onglets principaux :**
- Elements : Inspecter HTML/CSS
- Console : Exécuter JavaScript
- Sources : Déboguer le code
- Network : Analyser les requêtes
- Performance : Mesurer les performances

### DOM (Document Object Model)
Représentation en arbre du document HTML, que JavaScript peut manipuler.

**Exemple :**
```javascript
// Accéder au DOM
document.querySelector('h1').textContent = 'Nouveau titre';
```

### DRY (Don't Repeat Yourself)
Principe qui consiste à éviter la duplication de code.

**Exemple :**
```javascript
// ❌ Code répété
const prix1 = 100 * 1.20;
const prix2 = 200 * 1.20;
const prix3 = 150 * 1.20;

// ✅ DRY : fonction réutilisable
function calculerPrixTTC(prixHT) {
  return prixHT * 1.20;
}
```

---

## E

### Élément
Instance d'une balise HTML dans le document.

**Exemple :** `<p>` est une balise, `<p>Texte</p>` est un élément

### Encapsulation
Regroupement de données et méthodes dans une unité (objet, classe, module).

### ES6 (ECMAScript 2015)
Version majeure de JavaScript introduisant de nombreuses fonctionnalités modernes : `let`, `const`, arrow functions, classes, modules, etc.

### Event (Événement)
Action détectée par le navigateur : clic, saisie clavier, chargement de page, etc.

**Exemple :**
```javascript
document.querySelector('button').addEventListener('click', function(event) {
  console.log('Bouton cliqué !', event);
});
```

### Event Listener (Écouteur d'événement)
Fonction qui attend qu'un événement se produise pour s'exécuter.

### Expression
Morceau de code qui produit une valeur.

**Exemples :**
```javascript
5 + 3          // Expression arithmétique
'Hello'        // Expression littérale
function() {}  // Expression de fonction
```

---

## F

### Fetch API
API moderne pour effectuer des requêtes HTTP.

**Exemple :**
```javascript
fetch('https://api.exemple.com/users')
  .then(response => response.json())
  .then(users => console.log(users))
  .catch(error => console.error(error));
```

### Flexbox
Système de mise en page CSS unidimensionnel (ligne ou colonne).

**Exemple :**
```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

### Float (Legacy)
⚠️ Ancienne méthode de mise en page CSS, **remplacée par Flexbox/Grid**.

### Framework
Structure logicielle qui fournit des outils et conventions pour développer des applications.

**Frameworks JavaScript populaires :** React, Vue.js, Angular, Svelte

### Frontend (Interface utilisateur)
Partie d'une application web visible et interactive dans le navigateur.

**Technologies frontend :** HTML, CSS, JavaScript

### Fonction
Bloc de code réutilisable qui effectue une tâche spécifique.

**Exemple :**
```javascript
function addition(a, b) {
  return a + b;
}

const resultat = addition(5, 3); // 8
```

---

## G

### GET
Méthode HTTP pour récupérer des données depuis un serveur.

**Exemple :**
```javascript
fetch('https://api.exemple.com/users', {
  method: 'GET'
});
```

### Git
Système de gestion de versions qui permet de suivre les modifications du code.

**Commandes de base :**
```bash
git init        # Initialiser un dépôt
git add .       # Ajouter les fichiers
git commit -m "Message"  # Enregistrer les modifications
git push        # Envoyer vers le serveur distant
```

### GitHub
Plateforme web pour héberger et collaborer sur des projets Git.

### Grid (CSS Grid)
Voir **CSS Grid**

---

## H

### Hoisting (Hissage)
Comportement JavaScript qui "remonte" les déclarations de variables et fonctions en haut de leur portée.

**Exemple :**
```javascript
console.log(x); // undefined (hoisting de var)
var x = 5;

// let et const ne sont PAS hissées de la même manière
console.log(y); // ❌ ReferenceError
let y = 10;
```

### HTML (HyperText Markup Language)
Langage de balisage qui structure le contenu des pages web.

### HTTP (HyperText Transfer Protocol)
Protocole de communication entre le client (navigateur) et le serveur.

**Méthodes HTTP courantes :**
- **GET** : Récupérer des données
- **POST** : Envoyer des données
- **PUT** : Mettre à jour des données
- **DELETE** : Supprimer des données

---

## I

### ID (Identifiant)
Attribut HTML unique qui identifie un élément spécifique.

**Exemple :**
```html
<div id="header">En-tête unique</div>
```

```css
#header { background: blue; }
```

**⚠️ Règle importante :** Un ID doit être unique dans toute la page

### IIFE (Immediately Invoked Function Expression)
⚠️ Fonction qui s'exécute immédiatement après sa définition. **Concept legacy**, remplacé par les modules ES6.

**Exemple :**
```javascript
(function() {
  console.log('Exécution immédiate');
})();
```

### Import/Export
Syntaxe moderne (ES6) pour partager du code entre fichiers JavaScript.

**Exemple :**
```javascript
// fichier utils.js
export function addition(a, b) {
  return a + b;
}

// fichier main.js
import { addition } from './utils.js';
```

### Indentation
Décalage du code vers la droite pour améliorer la lisibilité.

**Exemple :**
```javascript
function exemple() {
  if (true) {
    console.log('Indenté');
  }
}
```

### Inline Element
Élément HTML qui n'occupe que l'espace nécessaire à son contenu et ne crée pas de nouvelle ligne.

**Exemples :** `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`

### Instance
Objet créé à partir d'une classe ou d'un constructeur.

**Exemple :**
```javascript
class Voiture {
  constructor(marque) {
    this.marque = marque;
  }
}

const maVoiture = new Voiture('Toyota');
// maVoiture est une instance de Voiture
```

### Itération
Action de répéter une opération (généralement dans une boucle).

---

## J

### JavaScript (JS)
Langage de programmation qui rend les pages web interactives.

### JSON (JavaScript Object Notation)
Format d'échange de données léger et lisible.

**Exemple :**
```json
{
  "nom": "Alice",
  "age": 30,
  "competences": ["HTML", "CSS", "JavaScript"]
}
```

**Conversion :**
```javascript
// Objet → JSON
const json = JSON.stringify(objet);

// JSON → Objet
const objet = JSON.parse(json);
```

---

## K

### Keyword (Mot-clé)
Mot réservé du langage qui a une signification spéciale.

**Exemples JavaScript :** `function`, `const`, `let`, `if`, `return`, `class`, `async`, `await`

---

## L

### Legacy (Héritage/Obsolète)
Se dit d'une technologie ou pratique ancienne, toujours fonctionnelle mais déconseillée.

**Exemples :** `var` (remplacé par `let`/`const`), `float` (remplacé par Flexbox/Grid)

### let
Mot-clé moderne pour déclarer une variable à portée de bloc.

**Exemple :**
```javascript
let age = 25;
age = 26; // OK : on peut réassigner

if (true) {
  let temp = 'local';
} // temp n'existe plus ici (portée de bloc)
```

### Library (Bibliothèque)
Collection de code réutilisable qui facilite des tâches spécifiques.

**Exemples :** jQuery, Lodash, Moment.js, Axios

### Linter
Outil qui analyse le code pour détecter des erreurs et imposer des conventions.

**Exemple :** ESLint pour JavaScript

### LocalStorage
API de stockage permettant de sauvegarder des données dans le navigateur.

**Exemple :**
```javascript
// Sauvegarder
localStorage.setItem('nom', 'Alice');

// Récupérer
const nom = localStorage.getItem('nom');

// Supprimer
localStorage.removeItem('nom');
```

### Loop (Boucle)
Structure qui répète un bloc de code plusieurs fois.

**Types :**
```javascript
// for classique
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// for...of (tableaux)
for (const element of tableau) {
  console.log(element);
}

// while
while (condition) {
  // code
}
```

---

## M

### Media Query
Technique CSS pour appliquer des styles en fonction de caractéristiques de l'appareil (taille d'écran, résolution, orientation).

**Exemple :**
```css
/* Styles pour écrans larges */
@media (min-width: 1024px) {
  .container {
    width: 1000px;
  }
}
```

### Méthode
Fonction associée à un objet.

**Exemple :**
```javascript
const personne = {
  nom: 'Alice',
  saluer() { // méthode
    console.log('Bonjour, je suis ' + this.nom);
  }
};

personne.saluer(); // Appel de méthode
```

### Minification
Processus de réduction de la taille des fichiers en supprimant espaces, commentaires et en raccourcissant les noms.

**Avant :**
```javascript
function calculerSomme(nombre1, nombre2) {
  return nombre1 + nombre2;
}
```

**Après minification :**
```javascript
function c(a,b){return a+b}
```

### Mobile-First
Approche de design responsive qui consiste à concevoir d'abord pour mobile, puis adapter pour les écrans plus grands.

**Exemple :**
```css
/* Mobile par défaut */
.container { width: 100%; }

/* Puis adaptations pour écrans plus grands */
@media (min-width: 768px) {
  .container { width: 750px; }
}
```

### Module
Fichier JavaScript contenant du code qui peut être importé et réutilisé ailleurs.

**Exemple :**
```javascript
// module.js
export const PI = 3.14159;
export function aireCircle(rayon) {
  return PI * rayon * rayon;
}

// main.js
import { PI, aireCircle } from './module.js';
```

---

## N

### Navigateur
Voir **Browser**

### Node.js
Environnement d'exécution JavaScript côté serveur (en dehors du navigateur).

**Utilisation :**
- Créer des serveurs web
- Utiliser npm et les build tools
- Exécuter des scripts JavaScript

### npm (Node Package Manager)
Gestionnaire de paquets JavaScript, le plus grand registre de bibliothèques au monde.

**Commandes courantes :**
```bash
npm init              # Initialiser un projet
npm install library   # Installer une bibliothèque
npm run dev          # Lancer un script
```

### Null
Valeur spéciale représentant l'absence intentionnelle de valeur.

**Exemple :**
```javascript
let utilisateur = null; // Volontairement vide
```

### Nullish Coalescing (??)
Opérateur moderne qui retourne l'opérande de droite si celui de gauche est `null` ou `undefined`.

**Exemple :**
```javascript
const nom = null;
console.log(nom ?? 'Anonyme'); // 'Anonyme'

const age = 0;
console.log(age ?? 18); // 0 (car 0 n'est ni null ni undefined)
```

---

## O

### Objet (Object)
Structure de données contenant des propriétés (paires clé-valeur).

**Exemple :**
```javascript
const voiture = {
  marque: 'Toyota',
  annee: 2024,
  demarrer() {
    console.log('Vroum !');
  }
};
```

### Opérateur
Symbole qui effectue une opération sur des valeurs.

**Types :**
- Arithmétiques : `+`, `-`, `*`, `/`, `%`
- Comparaison : `===`, `!==`, `>`, `<`, `>=`, `<=`
- Logiques : `&&`, `||`, `!`
- Affectation : `=`, `+=`, `-=`

### Optional Chaining (?.)
Opérateur moderne pour accéder aux propriétés d'objets potentiellement `null` ou `undefined` sans erreur.

**Exemple :**
```javascript
const utilisateur = {
  nom: 'Alice',
  adresse: {
    ville: 'Paris'
  }
};

// Sans optional chaining
const pays = utilisateur.adresse && utilisateur.adresse.pays; // undefined

// Avec optional chaining
const pays = utilisateur.adresse?.pays; // undefined (pas d'erreur)
```

---

## P

### Package (Paquet)
Bibliothèque ou module distribué via npm.

### Paramètre
Variable dans la définition d'une fonction qui recevra une valeur lors de l'appel.

**Exemple :**
```javascript
function saluer(nom) { // nom = paramètre
  console.log('Bonjour ' + nom);
}

saluer('Marie'); // 'Marie' = argument
```

### Parsing
Processus d'analyse et d'interprétation du code par le navigateur ou le moteur JavaScript.

### POST
Méthode HTTP pour envoyer des données au serveur.

**Exemple :**
```javascript
fetch('https://api.exemple.com/users', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ nom: 'Alice', age: 30 })
});
```

### Promise
Objet représentant une opération asynchrone qui sera complétée dans le futur.

**Exemple :**
```javascript
const promesse = fetch('https://api.exemple.com/data');

promesse
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

**États d'une Promise :**
- **Pending** : En attente
- **Fulfilled** : Réussie
- **Rejected** : Échouée

### Propriété
Caractéristique d'un objet (paire clé-valeur).

**Exemple :**
```javascript
const voiture = {
  marque: 'Toyota', // propriété
  annee: 2024       // propriété
};
```

### Pseudo-classe
Sélecteur CSS qui cible un état spécial d'un élément.

**Exemples :**
```css
a:hover { color: red; }        /* Survol */
input:focus { border: blue; }  /* Focus */
li:first-child { font-weight: bold; }
li:nth-child(2) { color: green; }
```

### Pseudo-élément
Sélecteur CSS qui cible une partie spécifique d'un élément.

**Exemples :**
```css
p::first-letter { font-size: 2em; } /* Première lettre */
p::before { content: "→ "; }        /* Avant le contenu */
p::after { content: " ←"; }         /* Après le contenu */
```

### PWA (Progressive Web App)
Application web qui se comporte comme une application native (peut fonctionner hors ligne, être installée sur l'écran d'accueil).

---

## Q

### Query (Requête)
Demande d'information, généralement à une base de données ou une API.

### querySelector / querySelectorAll
Méthodes modernes pour sélectionner des éléments du DOM avec des sélecteurs CSS.

**Exemple :**
```javascript
// Sélectionner un élément
const titre = document.querySelector('h1');
const premier = document.querySelector('.classe');

// Sélectionner plusieurs éléments
const paragraphes = document.querySelectorAll('p');
```

---

## R

### React
Bibliothèque JavaScript populaire pour construire des interfaces utilisateurs basées sur des composants.

### Refactoring (Refactorisation)
Processus d'amélioration du code sans changer son comportement externe.

### Rendering (Rendu)
Processus par lequel le navigateur affiche le contenu HTML/CSS à l'écran.

### Repository (Dépôt)
Emplacement de stockage du code source d'un projet (souvent sur GitHub, GitLab).

### Responsive Design
Approche de conception qui permet à un site de s'adapter à différentes tailles d'écran.

**Techniques :**
- Media queries
- Unités relatives (`%`, `em`, `rem`, `vw`, `vh`)
- Flexbox et Grid
- Images responsives

### REST (Representational State Transfer)
Architecture pour créer des APIs web utilisant les méthodes HTTP standard.

### Return
Mot-clé pour retourner une valeur depuis une fonction.

**Exemple :**
```javascript
function addition(a, b) {
  return a + b; // Retourne le résultat
}

const resultat = addition(5, 3); // 8
```

---

## S

### Scope (Portée)
Contexte dans lequel une variable est accessible.

**Types :**
```javascript
// Portée globale
const global = 'accessible partout';

function exemple() {
  // Portée de fonction
  const fonctionScope = 'accessible dans la fonction';

  if (true) {
    // Portée de bloc (let/const)
    const blocScope = 'accessible dans ce bloc';
  }
}
```

### Selector (Sélecteur)
Pattern utilisé en CSS pour cibler des éléments HTML.

**Types :**
```css
p { }              /* Élément */
.classe { }        /* Classe */
#id { }            /* ID */
[type="text"] { }  /* Attribut */
p.classe { }       /* Combinaison */
div > p { }        /* Enfant direct */
div p { }          /* Descendant */
```

### Semantic HTML (HTML Sémantique)
Utilisation de balises HTML qui décrivent clairement leur contenu.

**Exemple :**
```html
<!-- ❌ Non sémantique -->
<div class="header">
  <div class="nav">...</div>
</div>

<!-- ✅ Sémantique -->
<header>
  <nav>...</nav>
</header>
```

### Server (Serveur)
Ordinateur qui héberge et délivre des sites web aux clients (navigateurs).

### SPA (Single Page Application)
Application web qui charge une seule page HTML et met à jour dynamiquement le contenu.

**Exemples :** Gmail, Facebook, Twitter

### Spread Operator (...)
Opérateur moderne pour "étaler" les éléments d'un tableau ou d'un objet.

**Exemple :**
```javascript
// Tableaux
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

// Objets
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }
```

### Statement (Instruction)
Commande complète qui effectue une action.

**Exemples :**
```javascript
let x = 5;           // Instruction de déclaration
if (x > 0) { }       // Instruction conditionnelle
console.log(x);      // Instruction d'appel de fonction
```

### Strict Mode
Mode JavaScript plus strict qui détecte plus d'erreurs.

**Activation :**
```javascript
'use strict';

// Le code ici est en mode strict
```

### String (Chaîne de caractères)
Type de données représentant du texte.

**Exemples :**
```javascript
const simple = 'Texte avec guillemets simples';
const double = "Texte avec guillemets doubles";
const template = `Texte avec backticks et ${variable}`;
```

### Syntax (Syntaxe)
Ensemble de règles qui définissent comment écrire correctement le code.

### Syntactic Sugar (Sucre Syntaxique)
Syntaxe alternative qui rend le code plus facile à lire sans ajouter de fonctionnalité.

**Exemple :**
```javascript
// Sans sucre syntaxique
const addition = function(a, b) {
  return a + b;
};

// Avec sucre syntaxique (arrow function)
const addition = (a, b) => a + b;
```

---

## T

### Tag (Balise)
Voir **Balise**

### Template Literals
Syntaxe moderne (backticks `) pour créer des chaînes de caractères avec interpolation.

**Exemple :**
```javascript
const nom = 'Alice';
const age = 30;

// Ancienne méthode
const texte1 = 'Je m\'appelle ' + nom + ' et j\'ai ' + age + ' ans.';

// Template literals
const texte2 = `Je m'appelle ${nom} et j'ai ${age} ans.`;
```

### Ternary Operator (Opérateur Ternaire)
Forme condensée de `if...else` en une seule ligne.

**Syntaxe :** `condition ? valeurSiVrai : valeurSiFaux`

**Exemple :**
```javascript
const age = 20;
const statut = age >= 18 ? 'majeur' : 'mineur';
```

### this
Mot-clé qui fait référence au contexte d'exécution actuel.

**Exemple :**
```javascript
const personne = {
  nom: 'Alice',
  saluer() {
    console.log('Bonjour, je suis ' + this.nom);
  }
};

personne.saluer(); // "Bonjour, je suis Alice"
```

### Transpilation
Conversion de code d'une version à une autre (ex: ES6+ → ES5 pour compatibilité).

**Outil :** Babel

### try...catch
Structure pour gérer les erreurs.

**Exemple :**
```javascript
try {
  // Code susceptible de générer une erreur
  const resultat = JSON.parse(jsonInvalide);
} catch (error) {
  // Gestion de l'erreur
  console.error('Erreur:', error.message);
} finally {
  // Toujours exécuté
  console.log('Nettoyage');
}
```

### Type
Catégorie de donnée (string, number, boolean, object, etc.).

### TypeScript
Sur-ensemble de JavaScript qui ajoute des types statiques.

**Exemple :**
```typescript
function addition(a: number, b: number): number {
  return a + b;
}
```

---

## U

### Undefined
Valeur par défaut d'une variable déclarée mais non initialisée.

**Exemple :**
```javascript
let x;
console.log(x); // undefined
```

### URL (Uniform Resource Locator)
Adresse d'une ressource sur le web.

**Structure :**
```
https://www.exemple.com:443/page?param=valeur#section
└─┬─┘   └────┬────────┘ └┬┘ └─┬─┘ └─────┬─────┘ └──┬──┘
protocole  domaine     port chemin   query      hash
```

### User Agent
Chaîne de caractères que le navigateur envoie au serveur pour s'identifier.

---

## V

### Validation
Vérification qu'un code ou des données respectent certaines règles.

**Types :**
- Validation HTML (W3C Validator)
- Validation CSS (CSS Validator)
- Validation JavaScript (ESLint)
- Validation de formulaires

### var (Legacy)
⚠️ Ancien mot-clé pour déclarer des variables. **Remplacé par `let` et `const`**.

**Pourquoi ne plus l'utiliser :**
```javascript
// Problème 1: Pas de portée de bloc
if (true) {
  var x = 5;
}
console.log(x); // 5 (fuite de variable)

// Problème 2: Hoisting confus
console.log(y); // undefined (pas d'erreur)
var y = 10;

// ✅ Solution moderne
if (true) {
  let x = 5;
}
console.log(x); // ❌ ReferenceError (attendu)
```

### Variable
Conteneur nommé pour stocker une valeur.

**Déclaration moderne :**
```javascript
const constante = 'ne change pas';
let variable = 'peut changer';
```

### Version Control (Gestion de versions)
Système pour suivre les modifications du code (Git).

### Viewport
Zone visible de la page web dans le navigateur.

**Meta viewport :**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Virtual DOM
Représentation en mémoire du DOM réel, utilisée par React et autres frameworks pour optimiser les mises à jour.

### Vite
Bundler moderne ultra-rapide pour le développement web.

### Vue.js
Framework JavaScript progressif pour construire des interfaces utilisateurs.

---

## W

### W3C (World Wide Web Consortium)
Organisation qui développe les standards web (HTML, CSS, etc.).

### Webpack
Bundler JavaScript populaire (plus ancien que Vite).

### Web API
Interface fournie par le navigateur pour interagir avec des fonctionnalités système.

**Exemples :** Fetch API, LocalStorage, Geolocation, Web Audio

### Whitespace (Espace blanc)
Espaces, tabulations et sauts de ligne dans le code.

---

## X

### XML (eXtensible Markup Language)
Langage de balisage pour structurer des données (moins utilisé que JSON aujourd'hui).

### XMLHttpRequest (Legacy)
⚠️ Ancienne API pour les requêtes HTTP. **Remplacée par Fetch API**.

---

## Y

### YAML
Format de sérialisation de données lisible par l'humain, utilisé pour les fichiers de configuration.

**Exemple :**
```yaml
nom: Alice
age: 30
competences:
  - HTML
  - CSS
  - JavaScript
```

---

## Z

### Z-index
Propriété CSS qui contrôle l'ordre d'empilement des éléments positionnés.

**Exemple :**
```css
.element1 {
  position: relative;
  z-index: 1;
}

.element2 {
  position: relative;
  z-index: 10; /* Au-dessus de element1 */
}
```

---

## Symboles et Caractères Spéciaux

### && (ET logique)
Opérateur qui retourne `true` si les deux opérandes sont vraies.

```javascript
if (age >= 18 && hasPermission) {
  console.log('Accès autorisé');
}
```

### || (OU logique)
Opérateur qui retourne `true` si au moins une opérande est vraie.

```javascript
if (isAdmin || isOwner) {
  console.log('Peut modifier');
}
```

### ! (NON logique)
Opérateur qui inverse une valeur booléenne.

```javascript
const isNotConnected = !isConnected;
```

### === (Égalité stricte)
Compare la valeur ET le type.

```javascript
5 === 5      // true
5 === '5'    // false (types différents)
```

### !== (Inégalité stricte)
Compare la valeur ET le type, retourne `true` s'ils sont différents.

### ?? (Nullish Coalescing)
Voir **Nullish Coalescing**

### ?. (Optional Chaining)
Voir **Optional Chaining**

### ... (Spread/Rest Operator)
Voir **Spread Operator**

### => (Arrow Function)
Voir **Arrow Function**

### ${} (Interpolation)
Utilisé dans les template literals pour insérer des variables.

```javascript
const nom = 'Alice';
console.log(`Bonjour ${nom} !`);
```

---

## Acronymes Courants

### AJAX - Asynchronous JavaScript And XML
Technique pour mettre à jour une page web sans la recharger.

### API - Application Programming Interface
Voir **API**

### CDN - Content Delivery Network
Voir **CDN**

### CSS - Cascading Style Sheets
Voir **CSS**

### DOM - Document Object Model
Voir **DOM**

### DRY - Don't Repeat Yourself
Voir **DRY**

### ES6 - ECMAScript 2015
Voir **ES6**

### HTML - HyperText Markup Language
Voir **HTML**

### HTTP - HyperText Transfer Protocol
Voir **HTTP**

### IDE - Integrated Development Environment
Environnement de développement intégré (ex: VS Code, WebStorm).

### IIFE - Immediately Invoked Function Expression
Voir **IIFE**

### JS - JavaScript
Voir **JavaScript**

### JSON - JavaScript Object Notation
Voir **JSON**

### MVC - Model-View-Controller
Architecture logicielle séparant données, interface et logique.

### npm - Node Package Manager
Voir **npm**

### PWA - Progressive Web App
Voir **PWA**

### REST - Representational State Transfer
Voir **REST**

### SPA - Single Page Application
Voir **SPA**

### UI - User Interface
Interface utilisateur (ce que l'utilisateur voit).

### UX - User Experience
Expérience utilisateur (comment l'utilisateur ressent le produit).

### W3C - World Wide Web Consortium
Voir **W3C**

### WYSIWYG - What You See Is What You Get
Éditeur qui affiche le résultat final pendant l'édition.

---

## Conseils d'utilisation de ce glossaire

### 📚 Pour l'apprentissage

1. **Ne pas tout lire d'un coup** : Consultez les termes au fur et à mesure de votre apprentissage
2. **Créez des liens** : Notez les relations entre concepts (ex: Promise → async/await)
3. **Pratiquez** : Testez les exemples de code fournis
4. **Revenez régulièrement** : Relisez les définitions pour renforcer votre compréhension

### 🔍 Pour la référence rapide

1. **Utilisez Ctrl+F** (ou Cmd+F sur Mac) pour rechercher rapidement
2. **Favorisez ce document** pour y accéder facilement
3. **Imprimez les sections importantes** si vous préférez le papier

### ✅ Signes de progression

Vous progressez bien si :
- ✅ Vous comprenez 80% des termes de base (A-E)
- ✅ Vous reconnaissez les termes même sans connaître tous les détails
- ✅ Vous pouvez expliquer les concepts avec vos propres mots
- ✅ Vous identifiez les pratiques legacy vs modernes

### 🎯 Prochaines étapes

Une fois ce glossaire maîtrisé :
1. Explorez des concepts avancés (Performance, Sécurité, Architecture)
2. Approfondissez les frameworks (React, Vue, Angular)
3. Découvrez le backend (Node.js, bases de données)
4. Contribuez à la communauté open source

---

**Note importante :** Ce glossaire évolue avec les technologies web. Les pratiques marquées ⚠️ "Legacy" sont à connaître pour maintenir du code existant, mais ne doivent plus être utilisées dans de nouveaux projets.

---

**Dernière mise à jour :** Décembre 2025

⏭️ Annexe C. [Checklist des bonnes pratiques](/annexes/C-checklist-bonnes-pratiques.md)
