🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.1.1 - Organisation des fichiers et dossiers

## Introduction

Imaginez que vous déménagez dans un nouvel appartement. Vous pourriez jeter toutes vos affaires en vrac dans le salon, mais ce ne serait pas très pratique ! Vous organisez plutôt : vêtements dans la chambre, ustensiles dans la cuisine, etc.

C'est exactement la même chose avec vos projets web. Une bonne organisation de fichiers et dossiers est **essentielle** pour :

- 🔍 **Retrouver rapidement** ce que vous cherchez
- 🚀 **Travailler plus efficacement**
- 👥 **Collaborer** facilement avec d'autres développeurs
- 🔧 **Maintenir** votre code sur le long terme
- 📈 **Faire évoluer** votre projet sans tout casser

Dans ce chapitre, nous allons voir comment passer d'un simple fichier HTML à une structure de projet professionnelle, étape par étape.

---

## Le problème du fichier unique

### La tentation du débutant

Quand on débute, on a souvent tendance à tout mettre dans un seul fichier :

```html
<!-- page.html - MAUVAISE PRATIQUE -->
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon site</title>
    <style>
        body { background: #f0f0f0; }
        .header { color: blue; }
        .content { padding: 20px; }
        /* 200 lignes de CSS... */
    </style>
</head>
<body>
    <div class="header">Mon site</div>
    <div class="content">
        <!-- 500 lignes de HTML... -->
    </div>

    <script>
        function maFonction() {
            // ...
        }
        // 300 lignes de JavaScript...
    </script>
</body>
</html>
```

### Pourquoi c'est problématique ?

❌ **Difficile à naviguer** : vous devez scroller pendant des heures pour trouver ce que vous cherchez

❌ **Impossible à réutiliser** : vous ne pouvez pas utiliser le même CSS sur plusieurs pages

❌ **Difficile à déboguer** : tout est mélangé, on ne sait plus où est le problème

❌ **Performance** : le navigateur doit tout recharger à chaque page

❌ **Collaboration impossible** : deux personnes ne peuvent pas travailler en même temps

---

## Étape 1 : Séparation basique (projet débutant)

### Structure minimale

La première étape est de séparer HTML, CSS et JavaScript dans des fichiers distincts :

```
mon-premier-site/
│
├── index.html
├── style.css
└── script.js
```

### Exemple concret

**📄 index.html**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon Premier Site</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Bienvenue sur mon site</h1>
        <nav>
            <a href="#accueil">Accueil</a>
            <a href="#about">À propos</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <main>
        <section id="accueil">
            <h2>Accueil</h2>
            <p>Contenu de la page d'accueil...</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2025 Mon Site</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>
```

**🎨 style.css**
```css
/* Reset basique */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
}

header {
    background: #333;
    color: white;
    padding: 1rem;
}

/* Reste du CSS... */
```

**⚡ script.js**
```javascript
// Votre code JavaScript
console.log('Le site est chargé !');

// Exemple d'interactivité
document.addEventListener('DOMContentLoaded', () => {
    console.log('Le DOM est prêt');
});
```

### Avantages de cette structure

✅ **Séparation claire** : HTML, CSS et JS sont séparés

✅ **Réutilisable** : le même CSS peut être utilisé sur plusieurs pages HTML

✅ **Mise en cache** : le navigateur peut garder style.css et script.js en cache

✅ **Facile à comprendre** : parfait pour débuter

### Limites

Cette structure fonctionne pour des projets très simples (1-3 pages), mais devient vite ingérable quand le projet grandit.

---

## Étape 2 : Organisation par type (projet intermédiaire)

### Structure avec dossiers

Quand votre projet grandit, créez des dossiers pour chaque type de ressource :

```
mon-site/
│
├── index.html
├── about.html
├── contact.html
│
├── css/
│   ├── style.css
│   ├── responsive.css
│   └── animations.css
│
├── js/
│   ├── app.js
│   ├── utils.js
│   └── form-validation.js
│
└── images/
    ├── logo.png
    ├── hero-banner.jpg
    └── icons/
        ├── facebook.svg
        └── twitter.svg
```

### Détail de la structure

#### 📁 Dossier `css/`
Contient tous vos fichiers de styles :
- **style.css** : styles principaux
- **responsive.css** : media queries pour le responsive
- **animations.css** : animations et transitions
- **reset.css** : reset CSS (optionnel)

#### 📁 Dossier `js/`
Contient tous vos scripts JavaScript :
- **app.js** : script principal de votre application
- **utils.js** : fonctions utilitaires réutilisables
- **form-validation.js** : validation de formulaires
- etc.

#### 📁 Dossier `images/`
Contient toutes vos images :
- Organisées par type ou par page
- Sous-dossiers pour les icônes, illustrations, photos...

### Exemple d'intégration dans le HTML

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon Site</title>

    <!-- Multiples fichiers CSS -->
    <link rel="stylesheet" href="css/style.css">
    <link rel="stylesheet" href="css/responsive.css">
    <link rel="stylesheet" href="css/animations.css">
</head>
<body>
    <header>
        <img src="images/logo.png" alt="Logo">
        <nav>
            <a href="index.html">Accueil</a>
            <a href="about.html">À propos</a>
            <a href="contact.html">Contact</a>
        </nav>
    </header>

    <main>
        <!-- Contenu -->
    </main>

    <!-- Multiples fichiers JavaScript -->
    <script src="js/utils.js"></script>
    <script src="js/app.js"></script>
</body>
</html>
```

### Avantages

✅ **Organisation logique** : chaque type de fichier a sa place

✅ **Scalabilité** : on peut ajouter facilement de nouveaux fichiers

✅ **Collaboration** : plusieurs développeurs peuvent travailler sur différents fichiers

✅ **Maintenance** : facile de retrouver un fichier spécifique

---

## Étape 3 : Structure professionnelle (projet avancé)

### Organisation complète

Pour un projet professionnel, on va encore plus loin dans l'organisation :

```
mon-projet-pro/
│
├── index.html
├── about.html
├── contact.html
│
├── assets/                    # Toutes les ressources statiques
│   ├── css/
│   │   ├── base/             # Styles de base
│   │   │   ├── reset.css
│   │   │   ├── typography.css
│   │   │   └── variables.css
│   │   ├── components/       # Styles de composants
│   │   │   ├── buttons.css
│   │   │   ├── cards.css
│   │   │   └── navbar.css
│   │   ├── layout/           # Mise en page
│   │   │   ├── header.css
│   │   │   ├── footer.css
│   │   │   └── grid.css
│   │   └── pages/            # Styles spécifiques aux pages
│   │       ├── home.css
│   │       └── contact.css
│   │
│   ├── js/
│   │   ├── main.js           # Point d'entrée principal
│   │   ├── modules/          # Modules JavaScript
│   │   │   ├── slider.js
│   │   │   ├── form.js
│   │   │   └── modal.js
│   │   └── utils/            # Fonctions utilitaires
│   │       ├── helpers.js
│   │       └── api.js
│   │
│   ├── images/
│   │   ├── logo/
│   │   │   ├── logo.svg
│   │   │   └── logo-white.svg
│   │   ├── icons/
│   │   │   └── ...
│   │   ├── photos/
│   │   │   └── ...
│   │   └── backgrounds/
│   │       └── ...
│   │
│   ├── fonts/                # Polices personnalisées
│   │   ├── Roboto-Regular.woff2
│   │   └── Roboto-Bold.woff2
│   │
│   └── videos/               # Vidéos (si nécessaire)
│       └── demo.mp4
│
├── docs/                     # Documentation du projet
│   ├── README.md
│   └── CONTRIBUTING.md
│
└── .gitignore               # Fichiers à ignorer par Git
```

### Explications détaillées

#### 📂 Le dossier `assets/`

C'est le conteneur principal de toutes vos ressources statiques. On le nomme souvent `assets/`, `static/` ou `public/`.

**Pourquoi un dossier `assets/` ?**
- Regroupe toutes les ressources au même endroit
- Facilite la configuration des serveurs web
- Clarifie ce qui est statique vs dynamique

#### 🎨 Organisation du CSS

##### `base/` - Fondations
Contient les styles de base qui s'appliquent globalement :

**reset.css**
```css
/* Normalisation des styles par défaut du navigateur */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    font-size: 16px;
}
```

**variables.css**
```css
/* Variables CSS pour la cohérence */
:root {
    /* Couleurs */
    --color-primary: #007bff;
    --color-secondary: #6c757d;
    --color-success: #28a745;
    --color-danger: #dc3545;

    /* Espacements */
    --spacing-xs: 0.25rem;
    --spacing-sm: 0.5rem;
    --spacing-md: 1rem;
    --spacing-lg: 2rem;
    --spacing-xl: 4rem;

    /* Typographie */
    --font-primary: 'Roboto', sans-serif;
    --font-secondary: 'Georgia', serif;
}
```

**typography.css**
```css
/* Styles typographiques globaux */
body {
    font-family: var(--font-primary);
    font-size: 1rem;
    line-height: 1.6;
    color: #333;
}

h1, h2, h3, h4, h5, h6 {
    margin-bottom: 1rem;
    font-weight: 600;
    line-height: 1.2;
}
```

##### `components/` - Composants réutilisables
Chaque composant UI a son propre fichier :

**buttons.css**
```css
/* Tous les styles de boutons */
.btn {
    display: inline-block;
    padding: 0.75rem 1.5rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.btn-primary {
    background-color: var(--color-primary);
    color: white;
}

.btn-primary:hover {
    background-color: #0056b3;
}
```

**cards.css**
```css
/* Styles pour les cartes */
.card {
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    padding: 1.5rem;
}
```

##### `layout/` - Structure des pages
Styles pour la structure générale :

**header.css**
```css
.header {
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    position: sticky;
    top: 0;
    z-index: 1000;
}
```

##### `pages/` - Styles spécifiques à certaines pages
Styles qui ne concernent qu'une page particulière :

**home.css**
```css
/* Styles uniquement pour la page d'accueil */
.hero-section {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

#### ⚡ Organisation du JavaScript

##### `main.js` - Point d'entrée
```javascript
// Importation des modules nécessaires
import Slider from './modules/slider.js';
import Form from './modules/form.js';
import Modal from './modules/modal.js';

// Initialisation de l'application
document.addEventListener('DOMContentLoaded', () => {
    // Initialiser le slider
    const slider = new Slider('.slider');

    // Initialiser le formulaire de contact
    const contactForm = new Form('#contact-form');

    // Initialiser les modales
    const modal = new Modal('.modal');

    console.log('Application initialisée');
});
```

##### `modules/` - Modules fonctionnels
Chaque fonctionnalité majeure a son module :

**slider.js**
```javascript
// Module pour gérer un slider d'images
export default class Slider {
    constructor(selector) {
        this.slider = document.querySelector(selector);
        this.currentSlide = 0;
        this.init();
    }

    init() {
        // Logique d'initialisation
        this.setupEventListeners();
    }

    setupEventListeners() {
        // Gestion des événements
    }

    nextSlide() {
        // Passer à la slide suivante
    }

    previousSlide() {
        // Revenir à la slide précédente
    }
}
```

##### `utils/` - Fonctions utilitaires
Fonctions réutilisables dans tout le projet :

**helpers.js**
```javascript
// Fonctions utilitaires diverses
export function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

export function formatDate(date) {
    // Formater une date
    return new Date(date).toLocaleDateString('fr-FR');
}

export function slugify(text) {
    // Transformer un texte en slug URL-friendly
    return text
        .toLowerCase()
        .replace(/[^\w ]+/g, '')
        .replace(/ +/g, '-');
}
```

**api.js**
```javascript
// Fonctions pour les appels API
export async function fetchData(url) {
    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error('Erreur réseau');
        }
        return await response.json();
    } catch (error) {
        console.error('Erreur lors du fetch:', error);
        throw error;
    }
}

export async function postData(url, data) {
    try {
        const response = await fetch(url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        });
        return await response.json();
    } catch (error) {
        console.error('Erreur lors du POST:', error);
        throw error;
    }
}
```

#### 🖼️ Organisation des images

Organisez vos images par catégorie :

```
images/
├── logo/           # Logos du site (versions claires/sombres)
├── icons/          # Icônes (SVG de préférence)
├── photos/         # Photos de contenu
├── backgrounds/    # Images de fond
├── products/       # Photos de produits (si e-commerce)
└── team/           # Photos d'équipe
```

**Bonnes pratiques pour les images :**
- Utilisez des noms descriptifs : `hero-banner.jpg` plutôt que `img1.jpg`
- Optimisez les tailles : ne chargez pas une image de 5Mo
- Utilisez les bons formats :
  - **JPEG** pour les photos
  - **PNG** pour les images avec transparence
  - **SVG** pour les logos et icônes
  - **WebP** pour la meilleure compression (moderne)

### Intégration dans le HTML

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon Projet Pro</title>

    <!-- Ordre d'importance des CSS -->
    <link rel="stylesheet" href="assets/css/base/reset.css">
    <link rel="stylesheet" href="assets/css/base/variables.css">
    <link rel="stylesheet" href="assets/css/base/typography.css">
    <link rel="stylesheet" href="assets/css/layout/header.css">
    <link rel="stylesheet" href="assets/css/layout/footer.css">
    <link rel="stylesheet" href="assets/css/components/buttons.css">
    <link rel="stylesheet" href="assets/css/components/cards.css">
    <link rel="stylesheet" href="assets/css/pages/home.css">
</head>
<body>
    <!-- Contenu -->

    <!-- Module ES6 -->
    <script type="module" src="assets/js/main.js"></script>
</body>
</html>
```

### Avantages de cette structure

✅ **Maintenabilité maximale** : chaque fichier a un rôle précis

✅ **Scalabilité** : facile d'ajouter de nouveaux composants

✅ **Réutilisabilité** : les composants peuvent être réutilisés

✅ **Collaboration** : plusieurs développeurs peuvent travailler sans conflit

✅ **Performance** : on charge uniquement ce dont on a besoin

✅ **Professionnalisme** : structure reconnue dans l'industrie

---

## Conventions de nommage

### Pour les fichiers et dossiers

#### ✅ Bonnes pratiques

```
✓ index.html
✓ about.html
✓ style.css
✓ main.js
✓ user-profile.html
✓ contact-form.js
```

**Règles :**
- Tout en **minuscules**
- Utilisez des **tirets** pour séparer les mots (kebab-case)
- Noms **descriptifs** et **explicites**
- Extensions appropriées (`.html`, `.css`, `.js`)

#### ❌ À éviter

```
✗ MyFile.html              (majuscules)
✗ my_file.html             (underscores - sauf cas spéciaux)
✗ monfichier.html          (pas d'espace, difficile à lire)
✗ fichier 1.html           (espaces)
✗ page_2_temp_final.html   (nom non descriptif)
```

### Pour les dossiers

```
✓ assets/
✓ css/
✓ js/
✓ images/
✓ components/
✓ user-profiles/

✗ Assets/              (majuscule)
✗ CSS_Files/           (underscores et majuscules)
✗ mes images/          (espaces)
```

---

## Cas pratiques : différents types de projets

### Projet 1 : Site vitrine simple

Pour un site vitrine de 3-5 pages :

```
site-vitrine/
├── index.html
├── services.html
├── portfolio.html
├── contact.html
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   └── images/
│       ├── logo.svg
│       └── photos/
└── README.md
```

### Projet 2 : Application web interactive

Pour une application avec beaucoup de JavaScript :

```
app-web/
├── index.html
├── assets/
│   ├── css/
│   │   ├── style.css
│   │   └── components/
│   ├── js/
│   │   ├── app.js
│   │   ├── components/
│   │   │   ├── navbar.js
│   │   │   ├── sidebar.js
│   │   │   └── modal.js
│   │   ├── services/
│   │   │   ├── auth.js
│   │   │   └── api.js
│   │   └── utils/
│   │       └── helpers.js
│   └── images/
└── data/
    └── config.json
```

### Projet 3 : Portfolio personnel

Pour un portfolio de développeur :

```
portfolio/
├── index.html
├── projects.html
├── blog.html
├── contact.html
├── assets/
│   ├── css/
│   │   ├── base/
│   │   ├── components/
│   │   └── pages/
│   ├── js/
│   │   ├── main.js
│   │   └── modules/
│   ├── images/
│   │   ├── profile.jpg
│   │   ├── projects/
│   │   └── blog/
│   └── documents/
│       └── cv.pdf
└── README.md
```

---

## Fichiers spéciaux à connaître

### README.md

Un fichier qui explique votre projet :

```markdown
# Mon Projet Web

## Description
Une brève description de votre projet.

## Technologies utilisées
- HTML5
- CSS3
- JavaScript ES6+

## Structure du projet
Explication de l'organisation des dossiers.

## Comment utiliser
Instructions pour lancer le projet localement.

## Auteur
Votre nom
```

### .gitignore

Pour Git, liste les fichiers à ne pas versionner :

```
# Fichiers système
.DS_Store
Thumbs.db

# Fichiers temporaires
*.tmp
*.log

# Dépendances
node_modules/

# Configuration locale
.env
config.local.js
```

---

## Conseils pratiques

### 1. Commencez simple

Ne créez pas une structure complexe dès le début. Commencez avec une structure simple et **évoluez** selon vos besoins.

**Pour débuter :**
```
projet/
├── index.html
├── style.css
└── script.js
```

**Quand ça grandit :**
```
projet/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── script.js
└── images/
```

### 2. Restez cohérent

Une fois que vous avez choisi une structure, **tenez-vous-y**. La cohérence est plus importante que la perfection.

### 3. Documentez

Ajoutez un fichier README.md qui explique :
- Ce que fait le projet
- Comment il est organisé
- Comment l'installer/utiliser

### 4. Pensez à l'avenir

Organisez vos fichiers en pensant que le projet va grandir. Mieux vaut avoir quelques dossiers vides au début que de devoir tout réorganiser plus tard.

### 5. Inspirez-vous

Regardez comment sont organisés les projets open source sur GitHub. Vous y trouverez d'excellents exemples.

---

## Pièges à éviter

### ❌ Trop de profondeur

Évitez une structure trop profonde :

```
assets/css/components/buttons/primary/large/blue/button.css  ❌ TROP PROFOND
```

3-4 niveaux maximum sont généralement suffisants.

### ❌ Fichiers fourre-tout

Ne créez pas de fichiers comme `old-stuff.js` ou `temp-test.css`. Supprimez ce qui ne sert plus.

### ❌ Duplication

```
assets/images/logo.png
images/logo-copy.png
assets/img/logo-final.png  ❌ DUPLICATION
```

Choisissez UN emplacement et une version.

### ❌ Noms génériques

```
file1.js
page2.html
style-new.css  ❌ PAS DESCRIPTIF
```

Utilisez des noms qui décrivent le contenu :
```
slider.js
contact.html
header-navigation.css  ✓ DESCRIPTIF
```

---

## Outils pour vous aider

### VS Code : Explorateur de fichiers

L'explorateur de fichiers de VS Code vous permet de :
- Créer des dossiers et fichiers facilement
- Glisser-déposer pour réorganiser
- Voir la structure en arborescence

**Raccourcis utiles :**
- `Ctrl+N` : Nouveau fichier
- Clic droit > "New Folder" : Nouveau dossier
- `F2` : Renommer

### Extensions VS Code recommandées

**File Utils**
- Facilite la création et la gestion de fichiers
- Permet de dupliquer, déplacer, renommer facilement

**Project Manager**
- Gérer plusieurs projets
- Passer rapidement d'un projet à l'autre

**Path Intellisense**
- Auto-complétion des chemins de fichiers
- Évite les erreurs de chemins

---

## Checklist : Est-ce que mon projet est bien organisé ?

Posez-vous ces questions :

✓ Mes fichiers HTML, CSS et JS sont-ils séparés ?

✓ Mes ressources sont-elles dans des dossiers logiques ?

✓ Mes noms de fichiers sont-ils descriptifs et cohérents ?

✓ Puis-je retrouver facilement n'importe quel fichier ?

✓ Un autre développeur pourrait-il comprendre ma structure ?

✓ Y a-t-il de la duplication inutile ?

✓ Ai-je documenté mon organisation (README.md) ?

✓ Ma structure permet-elle de faire évoluer le projet ?

Si vous répondez "oui" à la plupart de ces questions, vous êtes sur la bonne voie ! 🎉

---

## Résumé

**L'organisation de fichiers et dossiers, c'est :**

1. 🗂️ **Séparer** HTML, CSS et JavaScript
2. 📁 **Créer des dossiers** logiques par type de ressource
3. 🏗️ **Structurer** selon la complexité du projet
4. 📝 **Nommer** de façon cohérente et descriptive
5. 🔄 **Évoluer** la structure selon les besoins
6. 📚 **Documenter** l'organisation choisie

**Règle d'or :** Une bonne organisation doit être **intuitive**. Si vous devez réfléchir 5 minutes pour savoir où mettre un fichier, c'est que votre structure doit être améliorée.

**Progression naturelle :**
```
Débutant    → 1 fichier de chaque type
Intermédiaire → Dossiers par type (css/, js/, images/)
Avancé      → Structure professionnelle complète (assets/, modules, etc.)
```

Commencez simple, et évoluez au fur et à mesure que votre projet grandit ! 🚀

---

## Pour aller plus loin

Dans les prochaines sections, nous verrons :
- **6.1.2** - Séparation des préoccupations (détails avancés)
- **6.1.3** - Modules JavaScript et type="module"
- **6.1.4** - Chemins relatifs vs absolus
- **6.1.5** - Ordre de chargement des ressources

Ces notions s'appuieront sur la structure que vous avez appris à créer ici.

⏭️ [Séparation des préoccupations](/06-integration-html-css-javascript/01-architecture-projet-moderne/02-separation-preoccupations.md)
