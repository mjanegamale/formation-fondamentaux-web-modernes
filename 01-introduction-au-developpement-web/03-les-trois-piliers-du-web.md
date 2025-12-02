🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 1.3 - Les trois piliers du web : HTML, CSS, JavaScript

## Introduction

Imaginez que vous construisez une maison. Vous avez besoin de trois éléments essentiels :
- **La structure** : les murs, le toit, les fondations
- **La décoration** : la peinture, le mobilier, les couleurs
- **La fonctionnalité** : l'électricité, la plomberie, les systèmes automatisés

Le développement web fonctionne exactement de la même manière, avec trois technologies fondamentales qui travaillent ensemble pour créer des sites web :

- **HTML** = La structure (les murs de la maison)
- **CSS** = La présentation (la décoration)
- **JavaScript** = L'interactivité (les systèmes fonctionnels)

Ces trois technologies sont présentes sur **absolument tous les sites web** que vous visitez. Maîtriser ces trois piliers, c'est maîtriser le développement front-end.

## HTML : La structure et le contenu

### Qu'est-ce que HTML ?

**HTML** signifie **H**yper**T**ext **M**arkup **L**anguage (Langage de Balisage Hypertexte).

**Ce n'est PAS un langage de programmation**, mais un **langage de balisage**. La différence ? HTML décrit la structure et le contenu, mais ne contient pas de logique ou d'instructions à exécuter.

### Le rôle de HTML

HTML définit **quoi afficher** et **comment organiser le contenu** :
- Les titres et sous-titres
- Les paragraphes de texte
- Les images
- Les liens hypertextes
- Les listes (à puces ou numérotées)
- Les formulaires
- Les tableaux
- Les vidéos et audios
- Et bien plus encore...

### Comment ça marche ?

HTML utilise des **balises** (tags en anglais) pour structurer le contenu. Les balises sont comme des étiquettes qui disent au navigateur "ceci est un titre", "ceci est un paragraphe", etc.

**Syntaxe de base** :
```html
<balise>Contenu</balise>
```

**Exemples concrets** :

```html
<h1>Bienvenue sur mon site</h1>
<p>Ceci est un paragraphe de texte.</p>
<a href="https://www.example.com">Cliquez ici</a>
<img src="photo.jpg" alt="Une belle photo">
```

**Décryptage** :
- `<h1>...</h1>` : Un titre de niveau 1 (le plus important)
- `<p>...</p>` : Un paragraphe
- `<a>...</a>` : Un lien hypertexte
- `<img>` : Une image (notez qu'elle n'a pas de balise fermante)

### Structure de base d'un document HTML

Voici à quoi ressemble un document HTML minimal :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Ma première page</title>
</head>
<body>
    <h1>Bonjour le monde !</h1>
    <p>Ceci est ma première page web.</p>
</body>
</html>
```

**Explication** :
- `<!DOCTYPE html>` : Indique que c'est un document HTML5
- `<html>` : La racine du document, contient tout le reste
- `<head>` : Les métadonnées (informations sur la page, non visibles)
- `<title>` : Le titre qui apparaît dans l'onglet du navigateur
- `<body>` : Le corps du document, tout ce qui sera visible

### L'importance de la sémantique

HTML5 a introduit des balises **sémantiques** qui donnent du sens au contenu :

```html
<header>En-tête de la page</header>
<nav>Menu de navigation</nav>
<main>
    <article>
        <h1>Titre de l'article</h1>
        <p>Contenu de l'article...</p>
    </article>
</main>
<aside>Barre latérale</aside>
<footer>Pied de page</footer>
```

**Pourquoi c'est important ?**
- **Accessibilité** : Les lecteurs d'écran comprennent mieux la structure
- **SEO** : Les moteurs de recherche comprennent mieux votre contenu
- **Maintenance** : Le code est plus lisible et compréhensible

### HTML seul : Fonctionnel mais basique

Voici à quoi ressemble une page **uniquement HTML** (sans CSS ni JavaScript) :

- Fond blanc
- Texte noir
- Police de base (généralement Times New Roman)
- Pas de mise en page sophistiquée
- Éléments empilés verticalement
- Aucune animation
- Aucune interactivité (sauf les liens)

**C'est fonctionnel, mais pas très attrayant !** C'est là que CSS entre en jeu.

## CSS : Le style et la présentation

### Qu'est-ce que CSS ?

**CSS** signifie **C**ascading **S**tyle **S**heets (Feuilles de Style en Cascade).

CSS est le langage qui **contrôle l'apparence visuelle** de votre page web. Si HTML est le squelette, CSS est la peau, les vêtements et le maquillage.

### Le rôle de CSS

CSS permet de contrôler :
- **Les couleurs** : texte, arrière-plans, bordures
- **Les polices** : type, taille, épaisseur, style
- **La mise en page** : positionnement, alignement, espacement
- **Les dimensions** : largeur, hauteur, marges, padding
- **Les animations** : transitions, transformations
- **Le responsive design** : adaptation aux différentes tailles d'écran
- **Et bien plus encore...**

### Comment ça marche ?

CSS fonctionne avec des **règles** composées de :
1. Un **sélecteur** (qui cibler ?)
2. Des **propriétés** (quoi modifier ?)
3. Des **valeurs** (comment modifier ?)

**Syntaxe de base** :
```css
sélecteur {
    propriété: valeur;
    autre-propriété: autre-valeur;
}
```

**Exemples concrets** :

```css
/* Tous les titres h1 en bleu */
h1 {
    color: blue;
    font-size: 32px;
}

/* Tous les paragraphes avec un fond gris clair */
p {
    background-color: #f0f0f0;
    padding: 15px;
    line-height: 1.6;
}

/* Les liens en rouge sans soulignement */
a {
    color: red;
    text-decoration: none;
}
```

### Les trois façons d'intégrer CSS

#### 1. CSS inline (dans la balise HTML)
```html
<p style="color: blue; font-size: 18px;">Texte en bleu</p>
```
**❌ À éviter** : Mélange structure et style, difficile à maintenir.

#### 2. CSS interne (dans la balise `<style>`)
```html
<head>
    <style>
        p {
            color: blue;
            font-size: 18px;
        }
    </style>
</head>
```
**⚠️ Acceptable pour de petits projets** ou des tests rapides.

#### 3. CSS externe (fichier séparé)
```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```
**✅ Méthode recommandée** : Sépare structure et style, réutilisable, plus propre.

### La puissance des sélecteurs CSS

CSS offre de nombreux moyens de cibler précisément les éléments :

```css
/* Par balise */
p { color: black; }

/* Par classe (réutilisable) */
.important { font-weight: bold; }

/* Par ID (unique) */
#header { background: blue; }

/* Combinaisons */
nav a { color: white; }

/* Pseudo-classes */
a:hover { color: red; }

/* Et bien plus encore... */
```

### CSS moderne : Flexbox et Grid

Les technologies modernes comme **Flexbox** et **CSS Grid** ont révolutionné la mise en page web :

**Avant** : On utilisait des techniques complexes et fragiles (float, tables)

**Aujourd'hui** : Des systèmes puissants et intuitifs pour créer n'importe quelle mise en page

```css
/* Container flexible qui centre son contenu */
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}

/* Grille responsive automatique */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
```

Nous explorerons ces concepts en détail dans le chapitre 4 de cette formation.

### CSS transforme tout !

Grâce à CSS, une simple page HTML peut devenir :
- Un site moderne et élégant
- Une application mobile-friendly
- Une présentation animée
- Un portfolio artistique
- Et bien plus encore...

**Le même HTML avec différents CSS = Des sites complètement différents !**

C'est la magie de la séparation entre structure (HTML) et présentation (CSS).

## JavaScript : L'interactivité et la logique

### Qu'est-ce que JavaScript ?

**JavaScript** (souvent abrégé JS) est un **véritable langage de programmation** qui s'exécute dans le navigateur.

**Attention** : JavaScript n'a **RIEN à voir** avec Java ! Ce sont deux langages complètement différents. Le nom a été choisi pour des raisons marketing à l'époque.

### Le rôle de JavaScript

JavaScript permet de rendre les pages web **interactives et dynamiques** :

- **Réagir aux actions de l'utilisateur** : clics, survols, saisies clavier
- **Modifier le contenu dynamiquement** : sans recharger la page
- **Valider les formulaires** : avant envoi au serveur
- **Créer des animations complexes**
- **Communiquer avec des serveurs** : charger des données (AJAX)
- **Créer des applications web complètes** : Gmail, Facebook, etc.
- **Et infiniment plus...**

### Comment ça marche ?

JavaScript utilise une syntaxe de programmation avec :
- **Variables** : stocker des données
- **Fonctions** : groupes d'instructions réutilisables
- **Conditions** : prendre des décisions (if/else)
- **Boucles** : répéter des actions
- **Événements** : réagir aux actions utilisateur
- **Objets** : structurer des données complexes

**Exemples concrets** :

```javascript
// Afficher un message dans la console
console.log("Bonjour le monde !");

// Stocker une valeur dans une variable
let nom = "Alice";
let age = 25;

// Une fonction qui calcule
function calculerDouble(nombre) {
    return nombre * 2;
}

// Réagir à un clic
document.querySelector('button').addEventListener('click', function() {
    alert('Vous avez cliqué sur le bouton !');
});

// Modifier le contenu de la page
document.querySelector('h1').textContent = "Nouveau titre !";
```

### Les trois façons d'intégrer JavaScript

#### 1. JavaScript inline (dans la balise HTML)
```html
<button onclick="alert('Clic !')">Cliquez-moi</button>
```
**❌ À éviter** : Mélange structure et comportement, déprécié.

#### 2. JavaScript interne (dans la balise `<script>`)
```html
<script>
    console.log('Hello World');
</script>
```
**⚠️ Acceptable pour de petits scripts** ou des tests.

#### 3. JavaScript externe (fichier séparé)
```html
<script src="script.js"></script>
```
**✅ Méthode recommandée** : Code organisé, réutilisable, maintenable.

### La manipulation du DOM

Le **DOM** (Document Object Model) est la représentation de votre page HTML que JavaScript peut manipuler.

**Imaginez le DOM comme une arborescence** :

```
document
  └── html
      ├── head
      │   ├── title
      │   └── meta
      └── body
          ├── header
          ├── main
          │   ├── h1
          │   └── p
          └── footer
```

JavaScript peut :
- **Sélectionner** n'importe quel élément
- **Modifier** son contenu, ses attributs, son style
- **Créer** de nouveaux éléments
- **Supprimer** des éléments
- **Réagir** aux événements (clics, soumissions, etc.)

**Exemple pratique** :

```javascript
// Sélectionner un élément
let titre = document.querySelector('h1');

// Modifier son contenu
titre.textContent = "Nouveau titre dynamique !";

// Modifier son style
titre.style.color = "red";

// Ajouter une classe CSS
titre.classList.add('important');

// Créer un nouvel élément
let nouveauParagraphe = document.createElement('p');
nouveauParagraphe.textContent = "Paragraphe créé dynamiquement";
document.body.appendChild(nouveauParagraphe);
```

### JavaScript moderne (ES6+)

Depuis 2015, JavaScript a connu d'énormes évolutions avec **ES6** (ECMAScript 2015) et les versions suivantes :

**Nouvelles fonctionnalités importantes** :
- `let` et `const` au lieu de `var`
- Arrow functions `() =>`
- Template literals `` `Hello ${nom}` ``
- Destructuring
- Modules (import/export)
- Promises et async/await
- Et bien plus...

**Cette formation se concentre sur le JavaScript moderne** utilisé en 2024-2025, pas sur les anciennes pratiques.

### L'écosystème JavaScript

JavaScript ne se limite pas au navigateur :

**Côté client (navigateur)** :
- JavaScript vanilla (pur)
- Frameworks : React, Vue.js, Angular
- Librairies : jQuery (legacy), Lodash, etc.

**Côté serveur** :
- Node.js : JavaScript côté serveur
- Express.js, Nest.js : frameworks serveur

**Mobile** :
- React Native, Ionic : applications mobiles

**Desktop** :
- Electron : applications desktop (VS Code, Slack, Discord)

JavaScript est devenu un langage **universel** et **incontournable** du développement moderne.

## Comment les trois technologies travaillent ensemble

### La séparation des préoccupations

Chaque technologie a son rôle bien défini :

```
┌──────────────────────────────────────┐
│           NAVIGATEUR                 │
│                                      │
│  ┌────────────────────────────────┐  │
│  │   HTML : Structure / Contenu   │  │
│  │   "Quoi afficher ?"            │  │
│  └────────────────────────────────┘  │
│              ↓                       │
│  ┌────────────────────────────────┐  │
│  │   CSS : Style / Présentation   │  │
│  │   "Comment l'afficher ?"       │  │
│  └────────────────────────────────┘  │
│              ↓                       │
│  ┌────────────────────────────────┐  │
│  │   JS : Comportement / Logique  │  │
│  │   "Que faire avec ?"           │  │
│  └────────────────────────────────┘  │
│              ↓                       │
│       PAGE WEB FINALE                │
└──────────────────────────────────────┘
```

### Exemple concret : Un bouton interactif

Voyons comment les trois technologies collaborent pour créer un simple bouton :

**HTML (structure)** :
```html
<button class="btn-primary" id="monBouton">
    Cliquez-moi !
</button>
<p id="message"></p>
```

**CSS (style)** :
```css
.btn-primary {
    background-color: #007bff;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.btn-primary:hover {
    background-color: #0056b3;
}
```

**JavaScript (comportement)** :
```javascript
const bouton = document.getElementById('monBouton');
const message = document.getElementById('message');

let compteur = 0;

bouton.addEventListener('click', function() {
    compteur++;
    message.textContent = `Vous avez cliqué ${compteur} fois !`;
});
```

**Résultat** : Un bouton stylé qui compte les clics et affiche le résultat !

### Exemple concret : Un formulaire de contact

**HTML (structure)** :
```html
<form id="contactForm">
    <label for="nom">Nom :</label>
    <input type="text" id="nom" required>

    <label for="email">Email :</label>
    <input type="email" id="email" required>

    <button type="submit">Envoyer</button>
</form>
<div id="resultat"></div>
```

**CSS (style)** :
```css
form {
    max-width: 400px;
    padding: 20px;
    background: #f5f5f5;
    border-radius: 8px;
}

input {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ddd;
    border-radius: 4px;
}

button {
    background: #28a745;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background: #218838;
}
```

**JavaScript (validation et comportement)** :
```javascript
const form = document.getElementById('contactForm');
const resultat = document.getElementById('resultat');

form.addEventListener('submit', function(e) {
    e.preventDefault(); // Empêche l'envoi classique

    const nom = document.getElementById('nom').value;
    const email = document.getElementById('email').value;

    // Validation personnalisée
    if (nom.length < 2) {
        resultat.textContent = "Le nom doit contenir au moins 2 caractères";
        resultat.style.color = "red";
        return;
    }

    // Afficher le résultat
    resultat.textContent = `Merci ${nom} ! Nous vous contacterons à ${email}`;
    resultat.style.color = "green";

    // Réinitialiser le formulaire
    form.reset();
});
```

**Résultat** : Un formulaire stylé avec validation personnalisée et feedback immédiat !

## L'évolution des standards web

### HTML : De HTML à HTML5

**HTML 1.0 (1991)** : Très basique, juste du texte et des liens

**HTML 4 (1997)** : Tables pour la mise en page, frames

**XHTML (2000)** : HTML avec syntaxe XML stricte

**HTML5 (2014)** : Moderne, sémantique, multimédia natif
- Nouvelles balises sémantiques (`<header>`, `<nav>`, `<article>`)
- Vidéo et audio natifs (`<video>`, `<audio>`)
- Canvas pour le dessin
- APIs JavaScript puissantes
- Support mobile optimisé

### CSS : De CSS à CSS3

**CSS 1 (1996)** : Styles de base (couleurs, polices)

**CSS 2 (1998)** : Positionnement, z-index

**CSS 3 (2011+)** : Révolution visuelle
- Coins arrondis (`border-radius`)
- Ombres (`box-shadow`, `text-shadow`)
- Transitions et animations
- Transformations 2D et 3D
- Flexbox (2012)
- Grid Layout (2017)
- Variables CSS
- Et bien plus...

**CSS continue d'évoluer** avec de nouvelles fonctionnalités chaque année !

### JavaScript : De ES5 à ES6+

**JavaScript (1995)** : Langage basique créé en 10 jours !

**ES3 (1999)** : Standardisation

**ES5 (2009)** : `"use strict"`, méthodes Array modernes

**ES6 / ES2015 (2015)** : RÉVOLUTION
- `let` et `const`
- Arrow functions
- Classes
- Modules
- Promises
- Template literals
- Destructuring
- Et bien plus...

**ES2016 à ES2024** : Nouvelles fonctionnalités chaque année
- Async/await (ES2017)
- Optional chaining `?.` (ES2020)
- Nullish coalescing `??` (ES2020)
- Et la liste continue...

## Pourquoi apprendre ces trois technologies ?

### 1. Elles sont universelles

**100% des sites web** utilisent HTML, CSS et JavaScript. Quelle que soit la technologie ou le framework utilisé, tout repose sur ces trois piliers.

### 2. Elles sont incontournables

Même si vous utilisez un framework comme React ou Vue.js plus tard, vous devez **d'abord maîtriser les bases** : HTML, CSS et JavaScript vanilla (pur).

### 3. Elles évoluent ensemble

Les trois technologies progressent en harmonie pour offrir de nouvelles possibilités :
- HTML5 + CSS3 = Sites modernes et responsives
- JavaScript moderne + HTML5 = Applications web puissantes
- CSS Grid/Flexbox + JavaScript = Mises en page dynamiques

### 4. Elles ouvrent des portes

Maîtriser ces trois piliers vous permet d'accéder à :
- **Frameworks front-end** : React, Vue.js, Angular
- **Développement mobile** : React Native, Ionic
- **Développement serveur** : Node.js
- **Développement desktop** : Electron
- **Et bien plus encore...**

### 5. Le marché les demande

Les compétences en HTML, CSS et JavaScript sont parmi **les plus demandées** sur le marché du travail. C'est un investissement rentable pour votre carrière.

## Les outils pour développer

Pour travailler avec HTML, CSS et JavaScript, vous avez besoin de :

### 1. Un éditeur de code
- **Visual Studio Code** (recommandé, gratuit)
- Sublime Text, Atom, WebStorm...

### 2. Un navigateur web
- **Chrome** (avec DevTools excellents)
- Firefox, Safari, Edge...

### 3. Optionnel mais utile
- Git (gestion de versions)
- Node.js (pour les outils modernes)
- Extensions VS Code

Nous verrons comment installer et configurer tout cela dans le chapitre 2.

## Les mythes à déconstruire

### ❌ "HTML et CSS ne sont pas de la vraie programmation"

**Faux** : Bien que HTML et CSS ne soient pas des langages de programmation au sens strict, la **maîtrise de ces technologies est complexe et technique**. Créer des interfaces modernes, accessibles et performantes demande de réelles compétences.

### ❌ "JavaScript, c'est juste pour les animations"

**Faux** : JavaScript est un langage de programmation complet qui permet de créer des applications web complexes, des serveurs, des applications mobiles et desktop.

### ❌ "Il faut connaître tous les frameworks"

**Faux** : Concentrez-vous d'abord sur les **fondamentaux** (HTML, CSS, JS vanilla). Les frameworks viennent naturellement après et sont plus faciles à apprendre avec une base solide.

### ❌ "Il y a trop à apprendre, je n'y arriverai jamais"

**Faux** : Personne ne connaît tout ! Même les développeurs seniors cherchent régulièrement sur Google. L'important est de **maîtriser les fondamentaux** et de savoir où chercher l'information.

## Votre parcours d'apprentissage

### Phase 1 : Les bases (vous êtes ici !)
- Comprendre les concepts fondamentaux
- Installer les outils
- Premiers pas en HTML, CSS et JavaScript

### Phase 2 : La pratique
- Créer des pages simples
- Appliquer du style avec CSS
- Ajouter de l'interactivité avec JavaScript

### Phase 3 : La maîtrise
- Concepts avancés
- Bonnes pratiques
- Responsive design
- Performances

### Phase 4 : L'écosystème
- Frameworks et librairies
- Build tools
- Workflow professionnel

**Cette formation couvre les phases 1, 2 et 3** en détail, et introduit la phase 4.

## Points clés à retenir

✅ **HTML structure le contenu** : "Quoi afficher ?"

✅ **CSS gère la présentation** : "Comment l'afficher ?"

✅ **JavaScript ajoute l'interactivité** : "Que faire avec ?"

✅ **Les trois technologies sont complémentaires** et travaillent ensemble

✅ **Elles évoluent constamment** : HTML5, CSS3, ES6+

✅ **Maîtriser les fondamentaux est essentiel** avant d'aller vers les frameworks

✅ **Ces compétences sont universelles** et très demandées

✅ **La séparation des préoccupations est importante** : un fichier par technologie

✅ **Tout le monde peut apprendre** avec de la pratique et de la patience

## L'analogie finale : La voiture

Pour résumer les trois piliers :

**HTML = La carrosserie et la structure**
- Les portes, les fenêtres, les sièges
- La forme générale
- Les éléments structurels

**CSS = La peinture et les finitions**
- La couleur de la voiture
- Le design des jantes
- L'intérieur luxueux ou sportif
- Les décalcomanies

**JavaScript = Le moteur et l'électronique**
- Le moteur qui fait avancer la voiture
- Les systèmes électroniques
- La climatisation automatique
- L'ordinateur de bord

**Ensemble**, ils créent une voiture fonctionnelle, belle et intelligente !

---

**Prochaine étape** : [1.4 - Évolution du web : du statique au dynamique](./04-evolution-du-web-du-statique-au-dynamique.md)

Maintenant que vous connaissez les trois piliers fondamentaux du web, découvrons comment le web a évolué depuis sa création et vers quoi il se dirige.

⏭️ [Évolution du web : du statique au dynamique](/01-introduction-au-developpement-web/04-evolution-du-web-du-statique-au-dynamique.md)
