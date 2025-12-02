🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Annexe C - Checklist des Bonnes Pratiques

Cette checklist regroupe les bonnes pratiques essentielles à suivre pour développer des sites web de qualité professionnelle. Utilisez-la comme guide de révision avant de livrer votre travail ou comme référence pendant le développement.

**💡 Comment utiliser cette checklist :**
- Passez en revue chaque section pertinente à votre projet
- Cochez les éléments au fur et à mesure
- Ne vous découragez pas si vous ne pouvez pas tout respecter immédiatement
- Revenez régulièrement pour intégrer progressivement ces pratiques

---

## 📋 Sommaire

1. [Structure de Projet et Organisation](#1-structure-de-projet-et-organisation)
2. [HTML - Structure et Sémantique](#2-html---structure-et-s%C3%A9mantique)
3. [CSS - Styles et Mise en Page](#3-css---styles-et-mise-en-page)
4. [JavaScript - Code et Logique](#4-javascript---code-et-logique)
5. [Responsive Design et Accessibilité](#5-responsive-design-et-accessibilit%C3%A9)
6. [Performance et Optimisation](#6-performance-et-optimisation)
7. [Sécurité](#7-s%C3%A9curit%C3%A9)
8. [Qualité du Code](#8-qualit%C3%A9-du-code)
9. [Git et Gestion de Versions](#9-git-et-gestion-de-versions)
10. [Avant la Mise en Ligne](#10-avant-la-mise-en-ligne)

---

## 1. Structure de Projet et Organisation

### Organisation des fichiers

- [ ] Structure de dossiers claire et cohérente
  ```
  mon-projet/
  ├── index.html
  ├── css/
  │   ├── style.css
  │   └── reset.css
  ├── js/
  │   ├── main.js
  │   └── utils.js
  ├── images/
  │   ├── logo.png
  │   └── photos/
  └── assets/
      ├── fonts/
      └── icons/
  ```

- [ ] Séparation claire entre HTML, CSS et JavaScript
- [ ] Un fichier par fonctionnalité (éviter les fichiers trop longs)
- [ ] Noms de fichiers en minuscules avec tirets (`mon-fichier.css`)
- [ ] Pas d'espaces dans les noms de fichiers

### Conventions de nommage

- [ ] **Fichiers** : kebab-case (`header-navigation.js`)
- [ ] **Classes CSS** : kebab-case (`.menu-principal`)
- [ ] **IDs HTML** : kebab-case (`#section-contact`)
- [ ] **Variables JavaScript** : camelCase (`monUtilisateur`)
- [ ] **Constantes JavaScript** : UPPER_SNAKE_CASE (`API_URL`)
- [ ] **Fonctions JavaScript** : camelCase (`calculerTotal()`)
- [ ] **Classes JavaScript** : PascalCase (`class Utilisateur {}`)

### Documentation

- [ ] README.md présent à la racine du projet
- [ ] Description claire du projet dans le README
- [ ] Instructions d'installation et d'utilisation
- [ ] Liste des dépendances et technologies utilisées

---

## 2. HTML - Structure et Sémantique

### Structure de base

- [ ] DOCTYPE HTML5 présent : `<!DOCTYPE html>`
- [ ] Attribut `lang` sur la balise `<html>` : `<html lang="fr">`
- [ ] Encodage UTF-8 déclaré : `<meta charset="UTF-8">`
- [ ] Meta viewport pour le responsive :
  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  ```
- [ ] Titre de page descriptif et unique : `<title>Mon Site | Page d'accueil</title>`
- [ ] Meta description présente pour le SEO

### Sémantique HTML5

- [ ] Utilisation de balises sémantiques appropriées :
  - [ ] `<header>` pour l'en-tête
  - [ ] `<nav>` pour la navigation
  - [ ] `<main>` pour le contenu principal (une seule par page)
  - [ ] `<article>` pour les contenus autonomes
  - [ ] `<section>` pour les sections thématiques
  - [ ] `<aside>` pour les contenus annexes
  - [ ] `<footer>` pour le pied de page

- [ ] Hiérarchie des titres respectée (h1 → h2 → h3, sans sauts)
- [ ] Un seul `<h1>` par page
- [ ] Éviter les `<div>` et `<span>` quand une balise sémantique existe

### Images et médias

- [ ] Attribut `alt` présent sur toutes les images
  ```html
  <img src="photo.jpg" alt="Description claire de l'image">
  ```
- [ ] Alt vide pour les images décoratives : `alt=""`
- [ ] Attributs `width` et `height` pour éviter les décalages de page
- [ ] Formats d'images optimisés (WebP, AVIF pour les modernes)
- [ ] Images responsives avec `srcset` si nécessaire
- [ ] Vidéos avec sous-titres et contrôles

### Formulaires

- [ ] Chaque `<input>` associé à un `<label>` :
  ```html
  <label for="email">Email :</label>
  <input type="email" id="email" name="email">
  ```
- [ ] Types d'inputs appropriés (`email`, `tel`, `number`, `date`, etc.)
- [ ] Attributs `required` pour les champs obligatoires
- [ ] Attributs `placeholder` informatifs mais pas en remplacement du label
- [ ] Messages d'erreur clairs et accessibles
- [ ] Boutons avec type explicite : `<button type="submit">Envoyer</button>`

### Liens

- [ ] Liens externes avec `target="_blank"` et `rel="noopener noreferrer"` :
  ```html
  <a href="https://exemple.com" target="_blank" rel="noopener noreferrer">
    Lien externe
  </a>
  ```
- [ ] Textes de liens descriptifs (éviter "cliquez ici")
- [ ] Navigation avec une liste `<ul>` dans `<nav>`

### Validation

- [ ] Code HTML valide (test avec https://validator.w3.org/)
- [ ] Pas de balises obsolètes (`<center>`, `<font>`, `<marquee>`)
- [ ] Toutes les balises correctement fermées
- [ ] Attributs entre guillemets

---

## 3. CSS - Styles et Mise en Page

### Organisation du CSS

- [ ] CSS externe dans un fichier séparé (pas de CSS inline sauf exception)
- [ ] Structure logique du fichier CSS :
  ```css
  /* 1. Variables CSS */
  /* 2. Reset/Normalize */
  /* 3. Styles généraux */
  /* 4. Layout */
  /* 5. Composants */
  /* 6. Utilitaires */
  /* 7. Media queries */
  ```
- [ ] Commentaires pour organiser les sections
- [ ] Un seul fichier CSS ou regroupement logique

### Sélecteurs

- [ ] Préférer les classes aux IDs pour le style
- [ ] Sélecteurs simples et peu profonds (éviter `.parent .enfant .petit-enfant .arriere-petit-enfant`)
- [ ] Éviter `!important` (sauf cas exceptionnels)
- [ ] Utiliser des noms de classes descriptifs (`.btn-primary`, `.card-header`)
- [ ] Éviter les sélecteurs d'éléments génériques pour les styles spécifiques

### Propriétés et valeurs

- [ ] Utiliser des variables CSS pour les valeurs répétées :
  ```css
  :root {
    --color-primary: #3498db;
    --spacing-unit: 8px;
    --font-main: 'Arial', sans-serif;
  }
  ```
- [ ] Préfixer les couleurs hexadécimales avec `#`
- [ ] Utiliser des unités relatives (`rem`, `em`, `%`, `vw`, `vh`)
- [ ] Éviter les valeurs magiques (ajouter un commentaire si nécessaire)
- [ ] Shorthand properties quand approprié :
  ```css
  /* Au lieu de */
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 10px;
  margin-left: 20px;

  /* Utiliser */
  margin: 10px 20px;
  ```

### Mise en page moderne

- [ ] **Flexbox** pour les layouts unidimensionnels
- [ ] **Grid** pour les layouts bidimensionnels
- [ ] ❌ Éviter `float` pour le layout (legacy)
- [ ] `box-sizing: border-box` globalement :
  ```css
  *, *::before, *::after {
    box-sizing: border-box;
  }
  ```

### Responsive Design

- [ ] Approche mobile-first :
  ```css
  /* Mobile par défaut */
  .container { width: 100%; }

  /* Puis adaptations croissantes */
  @media (min-width: 768px) {
    .container { width: 750px; }
  }
  ```
- [ ] Media queries pour les breakpoints standards (768px, 1024px, 1200px)
- [ ] Unités relatives plutôt que pixels fixes
- [ ] Testez sur différentes tailles d'écran
- [ ] Images et vidéos responsives (`max-width: 100%`)

### Performance CSS

- [ ] Minimiser le nombre de propriétés par règle
- [ ] Éviter les sélecteurs universels (`*`) dans les règles spécifiques
- [ ] Regrouper les media queries par breakpoint
- [ ] Supprimer le CSS inutilisé

### Validation

- [ ] Code CSS valide (test avec https://jigsaw.w3.org/css-validator/)
- [ ] Compatibilité navigateur vérifiée (Can I Use)
- [ ] Pas de propriétés obsolètes ou non standard sans préfixes

---

## 4. JavaScript - Code et Logique

### Syntaxe moderne (ES6+)

- [ ] ✅ Utiliser `const` par défaut, `let` si réassignation nécessaire
- [ ] ❌ Ne JAMAIS utiliser `var` (legacy)
- [ ] Utiliser les arrow functions quand approprié :
  ```javascript
  // Au lieu de
  function addition(a, b) {
    return a + b;
  }

  // Utiliser
  const addition = (a, b) => a + b;
  ```
- [ ] Template literals pour la concaténation :
  ```javascript
  // Au lieu de
  const message = 'Bonjour ' + nom + ' !';

  // Utiliser
  const message = `Bonjour ${nom} !`;
  ```
- [ ] Destructuring pour extraire des valeurs :
  ```javascript
  const { nom, age } = utilisateur;
  const [premier, deuxieme] = tableau;
  ```
- [ ] Spread operator pour copier/fusionner :
  ```javascript
  const nouveauTableau = [...ancienTableau, nouvelElement];
  const nouvelObjet = { ...ancienObjet, nouvelleProp: 'valeur' };
  ```

### Déclarations et fonctions

- [ ] Fonctions déclarées en haut du fichier ou avant leur utilisation
- [ ] Noms de fonctions descriptifs et verbeux
- [ ] Fonctions courtes (principe de responsabilité unique)
- [ ] Paramètres par défaut quand approprié :
  ```javascript
  function saluer(nom = 'Invité') {
    return `Bonjour ${nom}`;
  }
  ```
- [ ] Éviter les fonctions avec trop de paramètres (max 3-4)

### Manipulation du DOM

- [ ] ✅ Utiliser `querySelector` / `querySelectorAll` (moderne)
- [ ] ❌ Éviter `getElementById`, `getElementsByClassName` (moins flexibles)
- [ ] Cacher le DOM avant les modifications multiples
- [ ] Utiliser `classList` pour les classes CSS :
  ```javascript
  element.classList.add('active');
  element.classList.remove('hidden');
  element.classList.toggle('open');
  ```
- [ ] Éviter `innerHTML` avec du contenu utilisateur (risque XSS)

### Événements

- [ ] ✅ Utiliser `addEventListener` (moderne)
- [ ] ❌ Éviter les attributs `onclick` dans le HTML
- [ ] Un seul listener par élément (ou utiliser la délégation)
- [ ] Délégation d'événements pour les éléments dynamiques :
  ```javascript
  // Sur le parent
  document.querySelector('.liste').addEventListener('click', (e) => {
    if (e.target.matches('.item')) {
      // Traitement
    }
  });
  ```
- [ ] `removeEventListener` quand nécessaire (éviter les fuites mémoire)
- [ ] `preventDefault()` utilisé correctement

### Asynchrone

- [ ] ✅ Préférer `async/await` aux Promises `.then()` :
  ```javascript
  // Au lieu de
  fetch(url)
    .then(response => response.json())
    .then(data => console.log(data));

  // Utiliser
  async function recupererDonnees() {
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
  }
  ```
- [ ] Gestion des erreurs avec `try...catch` :
  ```javascript
  try {
    const data = await fetch(url);
  } catch (error) {
    console.error('Erreur:', error);
  }
  ```
- [ ] Fetch API plutôt que XMLHttpRequest (legacy)

### Gestion des erreurs

- [ ] `try...catch` pour le code susceptible d'échouer
- [ ] Messages d'erreur clairs et informatifs
- [ ] Console.error() pour les erreurs, console.log() pour l'info
- [ ] Validation des données avant traitement

### Modules

- [ ] Code organisé en modules ES6 :
  ```javascript
  // utils.js
  export function addition(a, b) {
    return a + b;
  }

  // main.js
  import { addition } from './utils.js';
  ```
- [ ] `type="module"` dans la balise `<script>` :
  ```html
  <script type="module" src="main.js"></script>
  ```
- [ ] Éviter les variables globales

### Sécurité

- [ ] Validation et nettoyage des entrées utilisateur
- [ ] Éviter `eval()` (dangereux)
- [ ] Utiliser `textContent` plutôt que `innerHTML` quand possible
- [ ] Échapper les données utilisateur avant insertion dans le DOM

### Performance

- [ ] Éviter les boucles sur de très gros tableaux dans le code synchrone
- [ ] Utiliser `debounce` ou `throttle` pour les événements fréquents (scroll, resize)
- [ ] Minimiser les accès au DOM dans les boucles
- [ ] Préférer les méthodes natives (map, filter, reduce) aux boucles for

### Code propre

- [ ] Pas de `console.log()` oublié en production
- [ ] Pas de code commenté (supprimer ou utiliser Git)
- [ ] Pas de code mort (code jamais exécuté)
- [ ] Comparaisons strictes : `===` et `!==` (pas `==` ou `!=`)
- [ ] Variables déclarées au plus proche de leur utilisation

---

## 5. Responsive Design et Accessibilité

### Responsive Design

- [ ] Meta viewport configuré
- [ ] Design mobile-first
- [ ] Breakpoints cohérents :
  - [ ] Mobile : < 768px
  - [ ] Tablette : 768px - 1023px
  - [ ] Desktop : ≥ 1024px
- [ ] Tests sur différentes résolutions :
  - [ ] Mobile (320px, 375px, 414px)
  - [ ] Tablette (768px, 1024px)
  - [ ] Desktop (1280px, 1920px)
- [ ] Images responsives (srcset ou picture)
- [ ] Pas de scroll horizontal non intentionnel
- [ ] Texte lisible sans zoom
- [ ] Zones cliquables assez grandes sur mobile (min 44x44px)

### Accessibilité (a11y)

#### Sémantique et structure

- [ ] HTML sémantique utilisé correctement
- [ ] Hiérarchie des titres logique (h1 → h2 → h3)
- [ ] Landmarks ARIA si nécessaire (`role="banner"`, `role="main"`)
- [ ] Langue du document déclarée (`lang="fr"`)
- [ ] Changements de langue signalés : `<span lang="en">Hello</span>`

#### Images et médias

- [ ] Attributs `alt` descriptifs sur les images informatives
- [ ] `alt=""` sur les images décoratives
- [ ] Transcriptions pour l'audio
- [ ] Sous-titres pour les vidéos
- [ ] Pas d'information véhiculée uniquement par la couleur

#### Navigation au clavier

- [ ] Navigation au clavier possible (Tab, Shift+Tab, Enter, Espace)
- [ ] Ordre de tabulation logique
- [ ] Focus visible sur tous les éléments interactifs :
  ```css
  button:focus {
    outline: 2px solid blue;
  }
  ```
- [ ] Pas de piège au clavier (on peut sortir de tous les éléments)
- [ ] Skip links pour aller au contenu principal :
  ```html
  <a href="#main-content" class="skip-link">Aller au contenu principal</a>
  ```

#### Formulaires

- [ ] Labels associés aux champs
- [ ] Messages d'erreur explicites et accessibles
- [ ] Instructions claires
- [ ] Attribut `aria-describedby` pour les descriptions
- [ ] Groupes de champs avec `<fieldset>` et `<legend>`

#### Contrastes et lisibilité

- [ ] Ratio de contraste suffisant (4.5:1 pour le texte normal, 3:1 pour le texte large)
- [ ] Vérifier avec un outil : https://webaim.org/resources/contrastchecker/
- [ ] Texte redimensionnable jusqu'à 200% sans perte de contenu
- [ ] Pas d'informations transmises uniquement par la couleur

#### ARIA (si nécessaire)

- [ ] `aria-label` pour les boutons sans texte :
  ```html
  <button aria-label="Fermer la fenêtre">✕</button>
  ```
- [ ] `aria-hidden="true"` pour cacher des éléments décoratifs
- [ ] `aria-live` pour les mises à jour dynamiques importantes
- [ ] Ne pas surcharger avec ARIA (HTML sémantique d'abord)

#### Tests d'accessibilité

- [ ] Test au clavier complet
- [ ] Test avec un lecteur d'écran (NVDA, JAWS, VoiceOver)
- [ ] Lighthouse audit (accessibilité)
- [ ] Extension axe DevTools ou WAVE

---

## 6. Performance et Optimisation

### Chargement et ressources

- [ ] Images optimisées (compression, formats modernes)
- [ ] Taille des images adaptée à l'usage (pas de 4K pour une miniature)
- [ ] Lazy loading pour les images hors écran :
  ```html
  <img src="image.jpg" loading="lazy" alt="Description">
  ```
- [ ] CSS et JS minifiés pour la production
- [ ] Fichiers regroupés (bundling) si possible
- [ ] Polices web optimisées (woff2, preload)
- [ ] Icônes en SVG ou font icons

### Ordre de chargement

- [ ] CSS dans le `<head>`
- [ ] JavaScript avant la fermeture du `</body>` ou avec `defer` :
  ```html
  <script src="script.js" defer></script>
  ```
- [ ] Scripts critiques inline si très petits
- [ ] Preload pour les ressources critiques :
  ```html
  <link rel="preload" href="font.woff2" as="font" crossorigin>
  ```

### Performance JavaScript

- [ ] Éviter les manipulations DOM dans les boucles
- [ ] Debounce/Throttle pour les événements fréquents
- [ ] Web Workers pour les calculs lourds (si applicable)
- [ ] Pagination ou lazy loading pour les grandes listes

### Cache et réseau

- [ ] Headers de cache configurés (si contrôle du serveur)
- [ ] Service Workers pour le cache (PWA)
- [ ] CDN pour les bibliothèques externes
- [ ] Compression Gzip/Brotli activée (serveur)

### Mesure de performance

- [ ] Test Lighthouse dans Chrome DevTools
- [ ] Score Lighthouse > 90 (objectif)
- [ ] Temps de chargement < 3 secondes
- [ ] First Contentful Paint < 1.8s
- [ ] PageSpeed Insights : https://pagespeed.web.dev/

---

## 7. Sécurité

### Bonnes pratiques générales

- [ ] Validation des entrées utilisateur côté client ET serveur
- [ ] Échappement des données avant affichage
- [ ] Pas de données sensibles dans le code source
- [ ] HTTPS utilisé (production)
- [ ] Headers de sécurité configurés (si contrôle du serveur)

### JavaScript

- [ ] Éviter `eval()` et `Function()` avec du contenu utilisateur
- [ ] Utiliser `textContent` plutôt que `innerHTML` quand possible
- [ ] Valider les URLs avant redirection
- [ ] Sanitize les données avant insertion dans le DOM

### Liens externes

- [ ] `rel="noopener noreferrer"` sur les liens `target="_blank"` :
  ```html
  <a href="https://externe.com" target="_blank" rel="noopener noreferrer">
    Lien
  </a>
  ```

### Formulaires

- [ ] Protection CSRF (si backend)
- [ ] Validation côté serveur (ne jamais faire confiance au client)
- [ ] Rate limiting sur les soumissions (si backend)

### Dépendances

- [ ] Dépendances npm à jour (pas de vulnérabilités connues)
- [ ] `npm audit` exécuté régulièrement
- [ ] Sources des CDN fiables

---

## 8. Qualité du Code

### Lisibilité

- [ ] Indentation cohérente (2 ou 4 espaces)
- [ ] Lignes de code < 80-100 caractères
- [ ] Espaces autour des opérateurs : `a + b` pas `a+b`
- [ ] Accolades sur la même ligne (JavaScript) :
  ```javascript
  if (condition) {
    // code
  }
  ```
- [ ] Noms de variables descriptifs (pas de `x`, `data`, `temp`)

### Commentaires

- [ ] Commentaires pour expliquer le "pourquoi", pas le "quoi"
- [ ] Code complexe commenté
- [ ] Pas de code commenté (supprimer ou utiliser Git)
- [ ] Commentaires à jour avec le code
- [ ] JSDoc pour les fonctions importantes :
  ```javascript
  /**
   * Calcule la somme de deux nombres
   * @param {number} a - Premier nombre
   * @param {number} b - Deuxième nombre
   * @returns {number} La somme de a et b
   */
  function addition(a, b) {
    return a + b;
  }
  ```

### Organisation

- [ ] Principe DRY respecté (Don't Repeat Yourself)
- [ ] Fonctions courtes (une responsabilité)
- [ ] Pas de "code spaghetti"
- [ ] Séparation des préoccupations (HTML / CSS / JS)
- [ ] Code groupé par fonctionnalité

### Outils de qualité

- [ ] ESLint configuré et sans erreurs :
  ```bash
  npm run lint
  ```
- [ ] Prettier pour le formatage automatique
- [ ] Validation HTML/CSS avant commit
- [ ] EditorConfig pour la cohérence d'équipe

---

## 9. Git et Gestion de Versions

### Configuration initiale

- [ ] `.gitignore` configuré correctement :
  ```
  node_modules/
  .env
  .DS_Store
  dist/
  *.log
  ```
- [ ] README.md à jour
- [ ] LICENSE si projet open source

### Commits

- [ ] Commits atomiques (une fonctionnalité = un commit)
- [ ] Messages de commit clairs et descriptifs :
  ```
  ✅ Bon : "Ajouter validation du formulaire de contact"
  ❌ Mauvais : "fix", "update", "modif"
  ```
- [ ] Convention de commit (optionnel mais recommandé) :
  ```
  feat: Nouvelle fonctionnalité
  fix: Correction de bug
  docs: Documentation
  style: Formatage
  refactor: Refactorisation
  test: Tests
  ```
- [ ] Commits réguliers (pas tout en un seul gros commit)

### Branches

- [ ] Branche `main` ou `master` toujours fonctionnelle
- [ ] Branches de feature pour les nouvelles fonctionnalités :
  ```bash
  git checkout -b feature/login-form
  ```
- [ ] Fusion via pull request si en équipe
- [ ] Branches supprimées après fusion

### Bonnes pratiques

- [ ] Ne jamais commiter de fichiers générés (`node_modules`, `dist`)
- [ ] Ne jamais commiter de secrets (API keys, mots de passe)
- [ ] Pull régulier si travail en équipe
- [ ] Résolution des conflits avant push

---

## 10. Avant la Mise en Ligne

### Tests finaux

#### Tests fonctionnels

- [ ] Tous les liens fonctionnent (pas de 404)
- [ ] Tous les formulaires fonctionnent et valident correctement
- [ ] Toutes les images s'affichent
- [ ] Toutes les fonctionnalités JavaScript opérationnelles
- [ ] Navigation complète du site testée

#### Tests de compatibilité

- [ ] Test sur Chrome
- [ ] Test sur Firefox
- [ ] Test sur Safari (si possible)
- [ ] Test sur Edge
- [ ] Test sur mobile (iOS et Android)
- [ ] Test sur tablette

#### Tests de résolution

- [ ] Mobile : 320px, 375px, 414px
- [ ] Tablette : 768px, 1024px
- [ ] Desktop : 1280px, 1920px
- [ ] Pas de débordement horizontal

### Validations

- [ ] HTML validé : https://validator.w3.org/
- [ ] CSS validé : https://jigsaw.w3.org/css-validator/
- [ ] Pas d'erreurs JavaScript dans la console
- [ ] Lighthouse audit passé (score > 90)
- [ ] Test d'accessibilité (axe ou WAVE)

### Optimisation finale

- [ ] Images optimisées et compressées
- [ ] CSS minifié
- [ ] JavaScript minifié
- [ ] Fichiers inutiles supprimés
- [ ] Console.log() supprimés
- [ ] Commentaires de debug supprimés

### SEO et Métadonnées

- [ ] Balises `<title>` uniques et descriptives sur chaque page
- [ ] Meta description sur chaque page
- [ ] Meta Open Graph pour les réseaux sociaux :
  ```html
  <meta property="og:title" content="Titre de la page">
  <meta property="og:description" content="Description">
  <meta property="og:image" content="image-preview.jpg">
  ```
- [ ] Favicon présent :
  ```html
  <link rel="icon" type="image/png" href="favicon.png">
  ```
- [ ] robots.txt configuré (si nécessaire)
- [ ] sitemap.xml créé (si applicable)

### Sécurité finale

- [ ] Pas de données sensibles dans le code
- [ ] Variables d'environnement pour les secrets (si backend)
- [ ] HTTPS configuré (en production)
- [ ] Headers de sécurité (si contrôle du serveur)

### Documentation

- [ ] README.md complet avec :
  - [ ] Description du projet
  - [ ] Instructions d'installation
  - [ ] Technologies utilisées
  - [ ] Comment lancer le projet
  - [ ] Crédits et licences
- [ ] Commentaires dans le code à jour
- [ ] Documentation technique si projet complexe

### Déploiement

- [ ] Fichiers de build générés (si applicable)
- [ ] Variables d'environnement configurées (production)
- [ ] Tests en environnement de staging avant production
- [ ] Plan de rollback en cas de problème
- [ ] Monitoring configuré (erreurs, performances)

---

## 📊 Scores à Viser

### Lighthouse (Chrome DevTools)

- **Performance** : > 90 🟢
- **Accessibilité** : > 90 🟢
- **Bonnes pratiques** : > 90 🟢
- **SEO** : > 90 🟢

### Validation

- **HTML** : 0 erreurs ✅
- **CSS** : 0 erreurs ✅
- **JavaScript** : 0 erreurs console ✅

### Compatibilité

- **Navigateurs modernes** : 100% fonctionnel ✅
- **Mobile** : 100% fonctionnel ✅
- **IE11** : ⚠️ Dégradation gracieuse acceptable (si support nécessaire)

---

## 🎯 Checklist par Niveau de Compétence

### 🌱 Débutant (Prioritaire)

Les éléments essentiels à maîtriser en premier :

- [ ] Structure HTML5 correcte (DOCTYPE, lang, charset, viewport)
- [ ] HTML sémantique de base (header, nav, main, footer)
- [ ] Validation HTML et CSS
- [ ] CSS externe (pas inline)
- [ ] `const` et `let` (jamais `var`)
- [ ] `querySelector` et `addEventListener`
- [ ] Noms de fichiers et variables cohérents
- [ ] Git avec commits clairs
- [ ] Tests sur différents navigateurs
- [ ] Meta viewport pour le responsive

### 🌿 Intermédiaire (Important)

Quand vous êtes à l'aise avec les bases :

- [ ] Variables CSS et organisation
- [ ] Flexbox et Grid
- [ ] Mobile-first et media queries
- [ ] Arrow functions et template literals
- [ ] Async/await
- [ ] Modules ES6
- [ ] Accessibilité de base (alt, labels, contrastes)
- [ ] Optimisation des images
- [ ] Commentaires pertinents
- [ ] ESLint et Prettier

### 🌳 Avancé (Optimisation)

Pour aller plus loin :

- [ ] Performance avancée (lazy loading, preload)
- [ ] Accessibilité complète (ARIA, lecteurs d'écran)
- [ ] Sécurité (CSP, sanitization)
- [ ] PWA et Service Workers
- [ ] Tests automatisés
- [ ] CI/CD
- [ ] Monitoring et analytics
- [ ] SEO avancé

---

## 💡 Conseils d'Utilisation

### Avant de commencer un projet

1. Créez une copie de cette checklist pour votre projet
2. Cochez au fur et à mesure du développement
3. Révisez la checklist régulièrement

### Pendant le développement

- Consultez la section pertinente quand vous travaillez sur un aspect spécifique
- Cochez les éléments au fur et à mesure
- Ne vous bloquez pas : tout ne doit pas être parfait du premier coup

### Avant de livrer

- Passez en revue toute la checklist
- Priorités : validation, tests, accessibilité de base
- Documentez ce qui n'a pas pu être fait (dette technique)

### Pour progresser

- Chaque projet, ajoutez 2-3 nouveaux points à respecter
- Revoyez régulièrement les points que vous oubliez
- Partagez avec votre équipe ou mentor

---

## 🔧 Outils Recommandés

### Validation et Tests

- **HTML Validator** : https://validator.w3.org/
- **CSS Validator** : https://jigsaw.w3.org/css-validator/
- **Lighthouse** : Intégré à Chrome DevTools
- **PageSpeed Insights** : https://pagespeed.web.dev/
- **Can I Use** : https://caniuse.com/

### Accessibilité

- **axe DevTools** : Extension navigateur
- **WAVE** : https://wave.webaim.org/
- **Contrast Checker** : https://webaim.org/resources/contrastchecker/

### Qualité de Code

- **ESLint** : https://eslint.org/
- **Prettier** : https://prettier.io/
- **Stylelint** : https://stylelint.io/

### Performance

- **TinyPNG** : Compression d'images https://tinypng.com/
- **Squoosh** : Optimisation d'images https://squoosh.app/
- **WebPageTest** : Tests de performance détaillés https://www.webpagetest.org/

---

## 📚 Ressources Complémentaires

- **MDN Web Docs** : Documentation de référence
- **Web.dev** : Guides de bonnes pratiques par Google
- **A11y Project** : Guide d'accessibilité
- **CSS-Tricks** : Articles et tutoriels CSS
- **JavaScript.info** : Tutoriel JavaScript moderne

---

## ✅ Résumé : Top 10 des Erreurs à Éviter

1. ❌ Oublier le meta viewport (site non responsive)
2. ❌ Utiliser `var` au lieu de `const`/`let`
3. ❌ Pas d'attributs `alt` sur les images
4. ❌ CSS inline ou dans des attributs `style`
5. ❌ `onclick` dans le HTML au lieu de `addEventListener`
6. ❌ Pas de validation HTML/CSS
7. ❌ Images non optimisées (plusieurs Mo)
8. ❌ Pas de tests sur mobile
9. ❌ Console.log() oubliés en production
10. ❌ Commits Git non descriptifs ("fix", "update")

---

## 🎓 Conclusion

Cette checklist n'est pas une liste rigide à suivre aveuglément. C'est un guide pour vous aider à développer de meilleures habitudes et à produire un code de qualité professionnelle.

**Rappelez-vous :**
- La perfection n'existe pas, visez le progrès continu
- Chaque projet est une opportunité d'apprendre
- Les bonnes pratiques deviennent naturelles avec l'expérience
- N'hésitez pas à adapter cette checklist à vos besoins

**Prochaines étapes :**
1. Sauvegardez cette checklist dans vos favoris
2. Utilisez-la sur votre prochain projet
3. Ajoutez vos propres points au fil de votre expérience
4. Partagez avec d'autres développeurs

Bon développement ! 🚀

---

**Dernière mise à jour :** Décembre 2025

⏭️ Annexe D. [Configuration d'environnement complète](/annexes/D-configuration-environnement.md)
