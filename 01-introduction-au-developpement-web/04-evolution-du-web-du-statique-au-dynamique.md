🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 1.4 - Évolution du web : du statique au dynamique

## Introduction

Le web que nous connaissons aujourd'hui - avec ses applications interactives, ses vidéos en streaming, ses réseaux sociaux - est radicalement différent du web de 1991. En à peine 30 ans, le web a connu une transformation spectaculaire qui continue encore aujourd'hui.

Comprendre cette évolution vous aidera à :
- Apprécier les technologies modernes que nous utilisons
- Comprendre pourquoi certaines pratiques sont obsolètes
- Anticiper les tendances futures
- Faire les bons choix techniques dans vos projets

Voyageons dans le temps pour découvrir cette fascinante histoire !

## 1991-1999 : Le Web 1.0 - L'ère statique

### Les débuts du World Wide Web

**1991** : Tim Berners-Lee, chercheur au CERN, crée le World Wide Web. Son objectif ? Permettre aux scientifiques de partager facilement des documents.

**Les premières pages web** :
- Uniquement du texte
- Quelques liens hypertextes
- Pas d'images (au début)
- Pas de style, juste du contenu brut
- Fond gris par défaut

**Analogie** : C'était comme lire un document Word très basique affiché dans une fenêtre. Pas de couleurs, pas de mise en page sophistiquée, juste de l'information.

### Caractéristiques du Web 1.0

#### Pages statiques

Les pages étaient **codées en dur** en HTML. Pour changer le contenu, il fallait :
1. Modifier le fichier HTML sur son ordinateur
2. Le télécharger sur le serveur via FTP
3. Le contenu était identique pour tous les visiteurs

**Exemple de page Web 1.0** :
```html
<html>
<head>
<title>Bienvenue sur mon site</title>
</head>
<body>
<h1>Mon site personnel</h1>
<p>Voici quelques liens intéressants :</p>
<ul>
<li><a href="page2.html">Ma page 2</a></li>
<li><a href="page3.html">Ma page 3</a></li>
</ul>
<p>Dernière mise à jour : 15 mars 1997</p>
</body>
</html>
```

Pas de CSS, pas de JavaScript, juste du HTML pur.

#### Contenu unidirectionnel

**Le site vous parle, vous écoutez** :
- Pas de commentaires
- Pas d'interaction
- Pas de comptes utilisateurs
- Juste de la lecture

C'était essentiellement une **brochure en ligne**.

#### Technologies limitées

**HTML 2.0 et 3.2** :
- Balises très limitées
- Tableaux pour la mise en page (!)
- Pas de multimedia natif
- Images GIF pixelisées

**Navigateurs primitifs** :
- Netscape Navigator
- Internet Explorer 3-4
- Différences d'affichage importantes

#### Connexions lentes

**Modems 56K** : Télécharger une image prenait plusieurs secondes !
- Les développeurs optimisaient chaque pixel
- Les images étaient compressées au maximum
- Les sites étaient volontairement minimalistes

### Ce qui était possible

Malgré les limitations, le Web 1.0 permettait :
- **Sites vitrines** : Présenter une entreprise, un CV
- **Annuaires** : Yahoo! était essentiellement un annuaire géant
- **Pages personnelles** : "Home pages" sur GeoCities
- **Documentation** : Manuels techniques, guides
- **Actualités** : Journaux en ligne (sans commentaires)

### L'expérience utilisateur

**Points positifs** :
- Simple et facile à comprendre
- Pas de publicités intrusives
- Pages légères qui chargeaient vite (malgré les modems lents)

**Points négatifs** :
- Aucune personnalisation
- Aucune interactivité
- Design très basique
- Pas de mises à jour en temps réel

## 2000-2004 : La transition - Les prémices du dynamisme

### L'arrivée des technologies dynamiques

Cette période marque une **révolution technologique** avec l'introduction de langages côté serveur :

#### PHP, ASP, JSP

Ces langages permettent de **générer du HTML dynamiquement** :

```php
<!-- Avant (statique) -->
<p>Bonjour visiteur</p>

<!-- Après (dynamique) -->
<p>Bonjour <?php echo $nom_utilisateur; ?></p>
```

Le serveur exécute le code et envoie du HTML personnalisé à chaque visiteur.

#### Bases de données

**MySQL, PostgreSQL** : Stockage de données structurées
- Contenu des articles
- Informations des utilisateurs
- Commentaires
- Produits et commandes

**Exemple** : Un blog peut maintenant stocker 1000 articles dans une base de données au lieu d'avoir 1000 fichiers HTML.

#### Les premières applications web

**Nouvelles possibilités** :
- Forums de discussion (phpBB, vBulletin)
- Systèmes de gestion de contenu (CMS)
- E-commerce basique
- Webmails

**Sites emblématiques** :
- Amazon (e-commerce)
- eBay (enchères en ligne)
- Blogger (blogs)

### JavaScript commence à briller

**JavaScript** existait depuis 1995, mais était peu utilisé. Puis :

**1999** : Internet Explorer 5 introduit **XMLHttpRequest**
- Permet de charger des données sans recharger la page
- Base de ce qu'on appellera AJAX

**Utilisations** :
- Validation de formulaires
- Menus déroulants
- Galeries d'images
- Petites animations

**Mais** : JavaScript était encore considéré comme "pas sérieux" et mal standardisé entre navigateurs.

### CSS arrive timidement

**CSS 1 (1996) et CSS 2 (1998)** commencent à être adoptés :

```css
/* Séparation du style et du contenu ! */
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
}

h1 {
    color: navy;
    text-align: center;
}
```

**Révolution** : On peut maintenant changer l'apparence de tout un site en modifiant un seul fichier CSS !

**Problème** : Incompatibilités entre navigateurs. Les développeurs devaient créer des CSS différents pour IE et les autres.

### La guerre des navigateurs

**Internet Explorer vs Netscape** : Bataille acharnée pour la dominance
- Standards non respectés
- Fonctionnalités propriétaires
- Cauchemar pour les développeurs

**Conséquences** :
- Sites avec "Optimisé pour Internet Explorer 6"
- Code avec détection du navigateur
- Frustration généralisée

## 2005-2010 : Le Web 2.0 - L'ère de la participation

### Qu'est-ce que le Web 2.0 ?

Le terme **Web 2.0**, popularisé en 2004, désigne un web où **les utilisateurs deviennent acteurs** et non plus simples lecteurs.

### Les piliers du Web 2.0

#### 1. Contenu généré par les utilisateurs

**Avant** : Les webmasters créaient tout le contenu
**Maintenant** : Les utilisateurs créent le contenu

**Exemples** :
- **Blogs** : WordPress, Blogger (tout le monde peut publier)
- **Wikis** : Wikipédia (encyclopédie collaborative)
- **Partage de vidéos** : YouTube (2005)
- **Réseaux sociaux** : Facebook (2004), Twitter (2006)

#### 2. L'interactivité

**AJAX** (Asynchronous JavaScript and XML) révolutionne l'expérience :

**Avant AJAX** :
```
Clic sur "Soumettre"
→ Page blanche pendant le chargement
→ Toute la page se recharge
```

**Avec AJAX** :
```
Clic sur "J'aime"
→ Mise à jour instantanée
→ Pas de rechargement
```

**Google Maps (2005)** : L'exemple parfait
- Carte interactive et fluide
- Déplacement sans rechargement
- Démonstration de la puissance d'AJAX

#### 3. Les interfaces riches (RIA)

**Rich Internet Applications** : Applications web qui rivalisent avec les logiciels desktop

**Technologies** :
- **Flash** : Animations, vidéos, jeux (RIP 2020)
- **Silverlight** : Alternative Microsoft (abandonné)
- **JavaScript** : Devient sérieux avec des frameworks

#### 4. Le social et le partage

**Fonctionnalités sociales** omniprésentes :
- Boutons de partage (Facebook, Twitter)
- Commentaires sur tous les sites
- Likes et réactions
- Profils utilisateurs
- Flux d'activités

**Le contenu devient viral** : Un article peut être partagé des millions de fois.

### L'émergence des frameworks JavaScript

JavaScript gagne ses lettres de noblesse avec des **librairies puissantes** :

#### jQuery (2006)

**Révolution** : Simplifie énormément JavaScript

**Avant jQuery** :
```javascript
// Code complexe et verbeux
var element = document.getElementById('monDiv');
element.style.display = 'none';
```

**Avec jQuery** :
```javascript
// Code simple et élégant
$('#monDiv').hide();
```

**Impact** : jQuery devient **omniprésent**. À son apogée, 70% des sites l'utilisaient.

#### Autres librairies importantes

- **Prototype** : Une des premières
- **MooTools** : Animations et effets
- **Dojo** : Pour les applications complexes

### CSS 3 arrive

**CSS 3** (à partir de 2011) apporte des fonctionnalités visuelles révolutionnaires :

```css
/* Coins arrondis (sans images !) */
.box {
    border-radius: 10px;
}

/* Ombres */
.card {
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

/* Transitions */
button {
    transition: all 0.3s ease;
}

button:hover {
    background-color: blue;
    transform: scale(1.1);
}

/* Gradients */
.header {
    background: linear-gradient(to right, #667eea, #764ba2);
}
```

**Plus besoin d'images** pour les effets visuels de base !

### HTML5 en préparation

**HTML5** commence à émerger avec des promesses excitantes :
- Vidéo et audio natifs (bye bye Flash !)
- Canvas pour le dessin
- Géolocalisation
- Stockage local
- WebSockets pour le temps réel

### L'expérience utilisateur s'améliore

**Sites Web 2.0** :
- ✅ Interactifs et fluides
- ✅ Visuellement attrayants
- ✅ Personnalisés
- ✅ Sociaux et collaboratifs
- ✅ Application-like

**Mais aussi** :
- ⚠️ Plus lourds et lents
- ⚠️ Dépendance à JavaScript
- ⚠️ Compatibilité navigateur encore problématique

## 2011-2015 : Le Web Mobile et Responsive

### La révolution mobile

**2007** : iPhone lancé
**2008** : Android lancé
**Conséquence** : Le web doit s'adapter aux smartphones et tablettes

### Le problème

Les sites desktop ne fonctionnent **pas du tout** sur mobile :
- Texte trop petit
- Boutons impossibles à cliquer
- Mise en page cassée
- Trop lourd à charger

**Première solution** : Créer des versions séparées
- `www.example.com` pour desktop
- `m.example.com` pour mobile
- **Problème** : Double maintenance, contenu différent

### Le Responsive Web Design (2010)

**Ethan Marcotte** introduit le concept de **Responsive Design** :
> "Un seul site qui s'adapte à toutes les tailles d'écran"

**Les trois ingrédients** :

#### 1. Grilles fluides
```css
.container {
    width: 90%; /* Pourcentages au lieu de pixels */
    max-width: 1200px;
}
```

#### 2. Images flexibles
```css
img {
    max-width: 100%;
    height: auto;
}
```

#### 3. Media queries
```css
/* Styles par défaut (mobile first) */
.menu {
    display: block;
}

/* Sur écran large */
@media (min-width: 768px) {
    .menu {
        display: flex;
    }
}
```

**Résultat** : Un site unique qui **s'adapte intelligemment** à toutes les tailles.

### HTML5 et CSS3 matures

**HTML5 finalisé en 2014** :
- `<video>` et `<audio>` natifs
- Balises sémantiques (`<header>`, `<nav>`, `<article>`)
- APIs JavaScript puissantes
- Formulaires améliorés

**La mort de Flash** : HTML5 offre tout ce que Flash faisait, en mieux et en standard.

### L'essor des frameworks CSS

**Bootstrap (2011)** : Le framework qui change tout

**Avantages** :
- Grille responsive prête à l'emploi
- Composants réutilisables
- Design professionnel par défaut
- Compatible tous navigateurs

**Impact** : Démocratisation du responsive design

**Autres frameworks** :
- Foundation
- Semantic UI
- Material Design (Google)

### Les Single Page Applications (SPA)

**Concept** : L'application entière tient dans une page HTML

**Comment ça marche ?**
1. Le navigateur charge une page HTML minimale
2. JavaScript charge et affiche dynamiquement le contenu
3. Navigation sans rechargement de page
4. Expérience ultra-fluide

**Frameworks émergents** :
- **AngularJS (2010)** : Framework complet de Google
- **Backbone.js (2010)** : Structure pour applications complexes
- **Ember.js (2011)** : Convention over configuration

### L'expérience mobile-first

**Nouveau paradigme** : Concevoir d'abord pour mobile, puis adapter au desktop

**Pourquoi ?**
- Plus de trafic mobile que desktop (depuis 2016)
- Contraintes mobile forcent à se concentrer sur l'essentiel
- Montée en puissance plus facile que descente

## 2016-2020 : Le Web Moderne - React, Vue, et l'écosystème JavaScript

### La révolution React

**React (2013, populaire en 2016)** : Facebook change la donne

**Concept révolutionnaire** : Component-based architecture

```jsx
// Un composant React
function Bouton({ texte, onClick }) {
    return (
        <button onClick={onClick} className="btn">
            {texte}
        </button>
    );
}

// Réutilisable partout !
<Bouton texte="Cliquez" onClick={handleClick} />
```

**Avantages** :
- Code réutilisable
- Maintenance facilitée
- Performance optimale (Virtual DOM)
- Écosystème riche

**Impact** : Devient rapidement le framework le plus populaire.

### Vue.js et Angular 2+

**Vue.js (2014)** : L'alternative progressive
- Plus simple que React
- Courbe d'apprentissage douce
- Très apprécié en Europe et Asie

**Angular 2+ (2016)** : Réécriture complète
- Framework complet "batteries included"
- TypeScript par défaut
- Surtout utilisé en entreprise

### L'explosion de l'écosystème JavaScript

#### npm et les build tools

**npm** : Des millions de packages réutilisables
- Lodash (utilitaires)
- Moment.js (dates)
- Axios (requêtes HTTP)
- Et des milliers d'autres...

**Build tools** :
- **Webpack** : Bundle les fichiers
- **Babel** : Transpile ES6+ pour anciens navigateurs
- **Grunt/Gulp** : Automatisation des tâches

#### ES6/ES2015 et après

**JavaScript moderne** avec de nouvelles fonctionnalités chaque année :

```javascript
// Arrow functions
const double = x => x * 2;

// Destructuring
const { nom, age } = utilisateur;

// Template literals
const message = `Bonjour ${nom}`;

// Async/await
const data = await fetch(url);

// Modules
import { Component } from 'react';
```

### CSS se modernise encore

#### Flexbox (2012) et Grid (2017)

**Révolution de la mise en page** :

```css
/* Flexbox : Alignement facile */
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}

/* Grid : Layouts complexes */
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

**Fini les hacks** avec float et position !

#### Preprocesseurs CSS

**SASS/SCSS, LESS** : CSS avec des superpuissances

```scss
// Variables
$primary-color: #3498db;

// Nesting
.nav {
    ul {
        list-style: none;
    }

    li {
        display: inline;
    }
}

// Mixins
@mixin button-style {
    padding: 10px 20px;
    border-radius: 5px;
}
```

### Progressive Web Apps (PWA)

**Concept** : Applications web qui se comportent comme des apps natives

**Fonctionnalités** :
- Installation sur l'écran d'accueil
- Fonctionnement offline
- Notifications push
- Performance native

**Exemples** :
- Twitter Lite
- Spotify Web
- Pinterest

### JAMstack

**J**avaScript + **A**PIs + **M**arkup

**Nouvelle architecture** :
- Sites statiques ultra-rapides
- Données via APIs
- JavaScript pour l'interactivité
- Déploiement sur CDN

**Générateurs** :
- Gatsby (React)
- Next.js (React)
- Nuxt.js (Vue)
- Jekyll, Hugo (statiques)

### Performance et accessibilité

**Google Core Web Vitals** : La performance devient essentielle
- LCP (Largest Contentful Paint)
- FID (First Input Delay)
- CLS (Cumulative Layout Shift)

**Accessibilité (a11y)** : Focus accru sur l'inclusion
- ARIA attributes
- Navigation au clavier
- Contraste des couleurs
- Screen readers

## 2021-Aujourd'hui : Le Web du Futur

### Les tendances actuelles

#### 1. TypeScript partout

**TypeScript** : JavaScript typé
- Moins d'erreurs
- Meilleure autocomplétion
- Code plus maintenable

**Adoption massive** : La plupart des nouveaux projets utilisent TypeScript.

#### 2. Meta-frameworks

**Frameworks de frameworks** :
- **Next.js** : React avec SSR, SSG, routing...
- **Nuxt** : Vue avec SSR, SSG...
- **SvelteKit** : Svelte avec fonctionnalités complètes
- **Remix** : React avec focus sur les standards web

**Avantages** : Tout est configuré, optimisé, prêt à l'emploi.

#### 3. Serverless et Edge Computing

**Nouvelle architecture** :
- Fonctions à la demande
- Pas de serveur à gérer
- Exécution au plus près de l'utilisateur
- Coûts optimisés

**Plateformes** :
- Vercel
- Netlify
- Cloudflare Workers
- AWS Lambda

#### 4. Web Components

**Standards natifs** pour créer des composants réutilisables :

```javascript
// Custom element natif
class MonBouton extends HTMLElement {
    connectedCallback() {
        this.innerHTML = `<button>Clic</button>`;
    }
}

customElements.define('mon-bouton', MonBouton);
```

Utilisable dans n'importe quel framework ou sans framework.

#### 5. WebAssembly (WASM)

**Révolution performance** : Code compilé qui tourne dans le navigateur
- Performances quasi-natives
- Réutilisation de code C/C++/Rust
- Jeux, traitement d'image, calculs lourds

**Exemples** :
- Figma (éditeur graphique)
- AutoCAD Web
- Google Earth

#### 6. IA et Machine Learning

**TensorFlow.js** : Machine learning dans le navigateur
- Reconnaissance d'images
- Traitement du langage naturel
- Prédictions en temps réel

**ChatGPT et IA génératives** : Nouvelle façon d'interagir avec le web

### Les technologies émergentes

#### WebGL et WebGPU

**Graphismes 3D** dans le navigateur :
- Jeux complexes
- Visualisations 3D
- Réalité augmentée
- Applications créatives

#### WebRTC

**Communication temps réel** :
- Visioconférence (Zoom, Google Meet)
- Partage d'écran
- Streaming pair-à-pair

#### API modernes

Le navigateur devient une **plateforme complète** :
- File System Access API
- Web Bluetooth
- Web USB
- Geolocation
- Payment Request API
- Web Share API
- Et des dizaines d'autres...

### Les défis actuels

#### 1. La complexité croissante

**Le paradoxe** : Plus d'outils = plus de complexité
- Fatigue JavaScript (trop de choix)
- Courbe d'apprentissage élevée
- Dépendances sur dépendances

**Solutions** :
- Retour aux fondamentaux
- Outils mieux intégrés
- Conventions partagées

#### 2. La sur-ingénierie

**Tentation** : Utiliser les dernières technologies pour tout
**Réalité** : Un simple site vitrine n'a pas besoin de React !

**Principe** : Choisir la techno adaptée au besoin.

#### 3. La performance

**Paradoxe** : Connexions plus rapides, mais sites plus lourds
- JavaScript trop volumineux
- Images non optimisées
- Animations gourmandes

**Solutions** :
- Code splitting
- Lazy loading
- Optimisation d'images
- Critical CSS

#### 4. La vie privée

**Préoccupation grandissante** :
- RGPD en Europe
- Cookies tiers bloqués
- Tracking limité

**Conséquences** : Nouvelles façons de faire de l'analytics et de la publicité.

### Le Web 3.0 ?

**Vision** : Un web décentralisé basé sur la blockchain
- Pas d'intermédiaires
- Propriété des données
- Crypto-monnaies
- NFTs

**État actuel** : Très controversé, peu adopté, avenir incertain.

## Tableau récapitulatif de l'évolution

| Période | Nom | Caractéristiques | Technologies |
|---------|-----|------------------|--------------|
| **1991-1999** | Web 1.0 | Statique, lecture seule | HTML, tables |
| **2000-2004** | Transition | Premiers CMS, forums | PHP, MySQL, CSS |
| **2005-2010** | Web 2.0 | Social, interactif | AJAX, jQuery, Flash |
| **2011-2015** | Mobile & Responsive | Multi-écrans | HTML5, CSS3, Bootstrap |
| **2016-2020** | Moderne | SPAs, composants | React, Vue, ES6+ |
| **2021-aujourd'hui** | Futur | Edge, IA, WebAssembly | Next.js, TypeScript, WASM |

## Les leçons de cette évolution

### 1. Le changement est constant

**Le web évolue vite** : Ce qui est moderne aujourd'hui sera obsolète demain.

**Conséquence** : L'apprentissage continu est essentiel.

### 2. Les fondamentaux restent

**HTML, CSS, JavaScript** : Toujours présents malgré les frameworks.

**Conseil** : Maîtrisez d'abord les bases avant les outils.

### 3. La simplicité revient toujours

**Cycle** : Complexité → Frustration → Retour à la simplicité

**Exemples** :
- Tables → Divs → Flexbox/Grid (plus simple)
- Callbacks → Promises → Async/await (plus simple)
- Classes → Hooks (plus simple)

### 4. L'expérience utilisateur prime

**Fil conducteur** : Rendre le web plus utilisable, accessible, rapide

**Toute innovation** doit servir l'utilisateur final.

### 5. Les standards gagnent à long terme

**Flash, Silverlight** : Technologies propriétaires disparues

**HTML5, CSS3, JavaScript** : Standards ouverts qui perdurent

## Où en sommes-nous aujourd'hui ?

### Le web moderne en 2024-2025

**Caractéristiques** :
- ✅ **Rapide** : Optimisations poussées, Edge computing
- ✅ **Réactif** : Interfaces fluides et dynamiques
- ✅ **Responsive** : Fonctionne partout
- ✅ **Riche** : Applications complexes dans le navigateur
- ✅ **Accessible** : Focus sur l'inclusion
- ✅ **Sécurisé** : HTTPS partout, sécurité renforcée

**Mais aussi** :
- ⚠️ **Complexe** : Beaucoup de technologies à maîtriser
- ⚠️ **Fragmenté** : Nombreux frameworks et outils
- ⚠️ **Énergivore** : Impact écologique des sites lourds

### Quel développeur web en 2024 ?

**Compétences essentielles** :
1. **Fondamentaux solides** : HTML, CSS, JavaScript moderne
2. **Un framework front-end** : React, Vue, ou Angular
3. **Build tools** : npm, Webpack/Vite
4. **Git** : Gestion de versions
5. **APIs et async** : Fetch, Promises, async/await
6. **Responsive design** : Mobile-first
7. **Performance** : Optimisation et bonnes pratiques
8. **Accessibilité** : Inclusion et standards

**Et continuez d'apprendre !**

## Vers où allons-nous ?

### Tendances probables

**Court terme (2025-2027)** :
- Consolidation des outils (moins de fragmentation)
- IA intégrée partout
- WebAssembly plus répandu
- Performance encore plus critique

**Moyen terme (2028-2030)** :
- Interfaces vocales et gestuelles
- Réalité augmentée dans le navigateur
- Web spatial (Apple Vision Pro, etc.)
- Intégration IoT plus poussée

**Long terme (2030+)** :
- Interfaces cerveau-ordinateur ?
- Web quantique ?
- L'imagination est la limite !

### Ce qui ne changera pas

**Les principes fondamentaux** :
- L'utilisateur au centre
- Performance et accessibilité
- HTML, CSS, JavaScript (sous une forme ou une autre)
- Le besoin de créer et partager

## Points clés à retenir

✅ **Le web est passé du statique au dynamique** en 30 ans

✅ **Web 1.0** : Pages statiques, lecture seule

✅ **Web 2.0** : Interactif, social, AJAX, contenu généré par utilisateurs

✅ **Mobile** : Responsive design devient essentiel

✅ **Moderne** : SPAs, frameworks, écosystème JavaScript riche

✅ **Futur** : Edge computing, WebAssembly, IA, performance

✅ **Les fondamentaux persistent** : HTML, CSS, JS restent la base

✅ **L'apprentissage est continu** : Le web évolue constamment

✅ **La simplicité revient** : Cycles de complexification/simplification

✅ **L'expérience utilisateur guide tout** : Rapidité, accessibilité, utilisabilité

## L'analogie finale : L'évolution des transports

L'évolution du web ressemble à celle des transports :

**Web 1.0 = Calèche** : Fonctionnelle mais basique

**Web 2.0 = Automobile** : Plus rapide, plus interactive

**Mobile & Responsive = 4x4** : S'adapte à tous les terrains

**Web Moderne = Voiture électrique connectée** : Performante, intelligente, écologique

**Web du Futur = ?** : Voiture autonome ? Vaisseau spatial ? L'avenir nous le dira !

Chaque étape apporte son lot d'innovations tout en gardant le but principal : **aller d'un point A à un point B** (ou dans le cas du web : **transmettre de l'information**).

---

**Prochaine étape** : [1.5 - Présentation de l'écosystème et des outils](./05-presentation-de-lecosysteme-et-des-outils.md)

Maintenant que vous comprenez l'histoire et l'évolution du web, découvrons l'écosystème actuel et les outils que nous allons utiliser dans cette formation.

⏭️ [Présentation de l'écosystème et des outils](/01-introduction-au-developpement-web/05-presentation-de-lecosysteme-et-des-outils.md)
