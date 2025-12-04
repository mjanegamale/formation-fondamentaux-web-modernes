🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.1.4 - Chemins relatifs et absolus

## Introduction

Imaginez que vous donnez une adresse à quelqu'un :

**Adresse absolue :** "123 Rue de la Paix, 75001 Paris, France"
→ Complète, précise, fonctionne depuis n'importe où dans le monde

**Adresse relative :** "Deux rues plus loin, puis à gauche"
→ Dépend d'où vous êtes, simple mais contextuelle

C'est exactement la même chose en développement web ! Les **chemins** (ou *paths*) vous permettent de dire au navigateur où trouver vos fichiers CSS, JavaScript, images, etc. Et il existe deux façons de le faire : **absolue** ou **relative**.

Comprendre les chemins est **crucial** car c'est l'une des sources d'erreurs les plus fréquentes pour les débutants. Un chemin incorrect = fichier non trouvé = site cassé.

---

## Qu'est-ce qu'un chemin ?

### Définition simple

> Un **chemin** (ou *path*) est l'adresse qui indique où se trouve un fichier dans votre système de fichiers.

Quand vous écrivez :
```html
<link rel="stylesheet" href="style.css">
```

Le `href="style.css"` est un **chemin** qui dit au navigateur : "Charge le fichier `style.css`".

### Anatomie d'un chemin

Un chemin peut contenir plusieurs éléments :

```
../assets/images/logo.png
│  │      │      └─ Nom du fichier
│  │      └─ Nom du dossier
│  └─ Nom du dossier parent
└─ Remonter d'un niveau
```

### Les caractères spéciaux

- `.` (point) = Le répertoire **courant** (actuel)
- `..` (deux points) = Le répertoire **parent** (un niveau au-dessus)
- `/` (slash) = Séparateur de dossiers

---

## Les chemins relatifs

### Définition

> Un **chemin relatif** indique l'emplacement d'un fichier **par rapport à** l'emplacement du fichier actuel.

C'est comme dire : "Va dans la pièce d'à côté" plutôt que de donner l'adresse complète.

### Exemple de base

```
mon-site/
├── index.html
└── style.css
```

Dans `index.html`, pour lier `style.css` :

```html
<!-- Chemin relatif : même dossier -->
<link rel="stylesheet" href="style.css">
```

Le navigateur comprend : "Cherche `style.css` dans le **même dossier** que `index.html`".

### Navigation dans les dossiers

#### Cas 1 : Fichier dans un sous-dossier

```
mon-site/
├── index.html
└── css/
    └── style.css
```

Dans `index.html` :
```html
<!-- Aller DANS le dossier css/ -->
<link rel="stylesheet" href="css/style.css">
```

**Explication :**
1. Départ : on est dans le dossier de `index.html` (racine)
2. `css/` = entre dans le dossier `css`
3. `style.css` = sélectionne le fichier

#### Cas 2 : Fichier dans un dossier parent

```
mon-site/
├── pages/
│   └── about.html
└── css/
    └── style.css
```

Dans `about.html`, pour lier `style.css` :
```html
<!-- Remonter d'un niveau (..), puis aller dans css/ -->
<link rel="stylesheet" href="../css/style.css">
```

**Explication :**
1. Départ : on est dans `pages/`
2. `../` = remonte d'un niveau (vers `mon-site/`)
3. `css/` = entre dans le dossier `css`
4. `style.css` = sélectionne le fichier

#### Cas 3 : Remonter plusieurs niveaux

```
mon-site/
├── pages/
│   └── blog/
│       └── article.html
└── css/
    └── style.css
```

Dans `article.html` :
```html
<!-- Remonter de 2 niveaux, puis aller dans css/ -->
<link rel="stylesheet" href="../../css/style.css">
```

**Explication :**
1. Départ : on est dans `pages/blog/`
2. `../` = remonte dans `pages/`
3. `../` = remonte dans `mon-site/`
4. `css/` = entre dans `css/`
5. `style.css` = sélectionne le fichier

### Le point (.) : répertoire courant

Le point `.` représente le dossier actuel. Ces deux écritures sont équivalentes :

```html
<!-- Sans le point (implicite) -->
<link rel="stylesheet" href="style.css">

<!-- Avec le point (explicite) -->
<link rel="stylesheet" href="./style.css">
```

**Conseil :** Utilisez `./` pour être **explicite** et éviter la confusion, surtout avec les modules JavaScript :

```javascript
// ✅ Explicite et clair
import { formatDate } from './utils.js';

// ❌ Ambigu (peut être confondu avec un package npm)
import { formatDate } from 'utils.js';
```

---

## Les chemins absolus

### Définition

> Un **chemin absolu** indique l'emplacement d'un fichier depuis la **racine** du site web.

C'est comme donner une adresse complète qui fonctionne depuis n'importe où.

### Chemins absolus locaux

Un chemin absolu local commence par `/` et part de la **racine du serveur** :

```
mon-site/
├── index.html
├── pages/
│   └── about.html
└── css/
    └── style.css
```

**Depuis n'importe quel fichier HTML :**
```html
<!-- Chemin absolu depuis la racine -->
<link rel="stylesheet" href="/css/style.css">
```

**Avantages :**
- Fonctionne depuis n'importe quel fichier
- Pas besoin de compter les `../`
- Plus simple pour des structures complexes

**Inconvénients :**
- Ne fonctionne pas en local (`file://`)
- Nécessite un serveur web
- Moins portable (dépend de la racine du serveur)

### Chemins absolus externes (URLs complètes)

Pour des fichiers sur d'autres serveurs :

```html
<!-- URL complète -->
<link rel="stylesheet" href="https://example.com/css/style.css">

<!-- Image hébergée ailleurs -->
<img src="https://images.example.com/logo.png" alt="Logo">

<!-- CDN externe -->
<script src="https://cdn.jsdelivr.net/npm/vue@3/dist/vue.global.js"></script>
```

---

## Comparaison : Relatif vs Absolu

### Tableau récapitulatif

| Aspect | Chemin relatif | Chemin absolu |
|--------|---------------|---------------|
| **Syntaxe** | `../css/style.css` | `/css/style.css` |
| **Point de départ** | Fichier actuel | Racine du serveur |
| **Portable** | ✅ Oui | ❌ Dépend du serveur |
| **Fonctionne en local** | ✅ Oui (`file://`) | ❌ Non |
| **Complexité** | Peut être complexe | Simple |
| **Maintenance** | Difficile si restructuration | Facile |
| **Utilisation recommandée** | Projets simples, développement local | Projets en production sur serveur |

### Quand utiliser quoi ?

#### Utilisez les chemins relatifs :
- ✅ En développement local (ouvrir `index.html` directement)
- ✅ Pour des projets simples
- ✅ Quand vous voulez un projet portable
- ✅ Pour les images, CSS, JS dans votre propre projet

#### Utilisez les chemins absolus :
- ✅ Sur un serveur en production
- ✅ Pour des ressources externes (CDN, APIs)
- ✅ Dans des projets complexes avec beaucoup de niveaux
- ✅ Quand la structure du site est stable

---

## Exemples pratiques complets

### Exemple 1 : Site simple

```
mon-site-simple/
├── index.html
├── about.html
├── contact.html
├── style.css
├── script.js
└── logo.png
```

**Tous les fichiers sont au même niveau, c'est facile :**

**index.html :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Accueil</title>
    <!-- ✅ Même dossier -->
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <img src="logo.png" alt="Logo">

    <nav>
        <!-- ✅ Même dossier -->
        <a href="index.html">Accueil</a>
        <a href="about.html">À propos</a>
        <a href="contact.html">Contact</a>
    </nav>

    <!-- ✅ Même dossier -->
    <script src="script.js"></script>
</body>
</html>
```

### Exemple 2 : Site organisé avec dossiers

```
mon-site-organise/
├── index.html
├── pages/
│   ├── about.html
│   └── contact.html
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   └── images/
│       └── logo.png
```

**index.html (à la racine) :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Accueil</title>
    <!-- ✅ Descendre dans assets/css/ -->
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>
    <!-- ✅ Descendre dans assets/images/ -->
    <img src="assets/images/logo.png" alt="Logo">

    <nav>
        <!-- ✅ Même niveau -->
        <a href="index.html">Accueil</a>
        <!-- ✅ Descendre dans pages/ -->
        <a href="pages/about.html">À propos</a>
        <a href="pages/contact.html">Contact</a>
    </nav>

    <!-- ✅ Descendre dans assets/js/ -->
    <script src="assets/js/main.js"></script>
</body>
</html>
```

**pages/about.html :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>À propos</title>
    <!-- ✅ Remonter (..), puis descendre dans assets/css/ -->
    <link rel="stylesheet" href="../assets/css/style.css">
</head>
<body>
    <!-- ✅ Remonter, descendre dans assets/images/ -->
    <img src="../assets/images/logo.png" alt="Logo">

    <nav>
        <!-- ✅ Remonter pour aller à la racine -->
        <a href="../index.html">Accueil</a>
        <!-- ✅ Même dossier -->
        <a href="about.html">À propos</a>
        <a href="contact.html">Contact</a>
    </nav>

    <!-- ✅ Remonter, descendre dans assets/js/ -->
    <script src="../assets/js/main.js"></script>
</body>
</html>
```

### Exemple 3 : Structure professionnelle

```
projet-pro/
├── index.html
├── pages/
│   ├── blog/
│   │   ├── index.html
│   │   └── article-1.html
│   └── about.html
└── assets/
    ├── css/
    │   └── style.css
    ├── js/
    │   └── main.js
    └── images/
        └── logo.png
```

**pages/blog/article-1.html :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Article</title>
    <!-- ✅ Remonter de 2 niveaux, descendre dans assets/css/ -->
    <link rel="stylesheet" href="../../assets/css/style.css">
</head>
<body>
    <!-- ✅ Remonter 2x, descendre dans assets/images/ -->
    <img src="../../assets/images/logo.png" alt="Logo">

    <nav>
        <!-- Navigation vers différents niveaux -->
        <a href="../../index.html">Accueil</a>
        <a href="../about.html">À propos</a>
        <a href="index.html">Blog</a>
        <a href="article-1.html">Article 1</a>
    </nav>

    <script src="../../assets/js/main.js"></script>
</body>
</html>
```

**Visualisation du chemin :**
```
article-1.html
    │
    ├── ../           (remonte dans pages/blog/)
    │   └── ../       (remonte dans pages/)
    │       └── ../   (remonte dans projet-pro/)
    │           └── assets/css/style.css  ✓
```

---

## Cas particulier : Les modules JavaScript

### Rappel important

Avec les modules JavaScript (`type="module"`), vous **devez** :
1. ✅ Toujours inclure l'extension `.js`
2. ✅ Utiliser des chemins relatifs ou absolus explicites

```javascript
// ✅ BON : Chemin relatif explicite avec extension
import { formatDate } from './utils.js';
import Slider from './components/Slider.js';
import api from '../services/api.js';

// ❌ MAUVAIS : Sans extension
import { formatDate } from './utils';

// ❌ MAUVAIS : Sans ./
import { formatDate } from 'utils.js';
```

### Structure de modules

```
projet/
├── index.html
└── js/
    ├── main.js
    ├── components/
    │   ├── Slider.js
    │   └── Modal.js
    └── utils/
        └── helpers.js
```

**index.html :**
```html
<script type="module" src="js/main.js"></script>
```

**js/main.js :**
```javascript
// ✅ Depuis main.js vers components/Slider.js
import Slider from './components/Slider.js';

// ✅ Depuis main.js vers utils/helpers.js
import { formatDate } from './utils/helpers.js';
```

**js/components/Slider.js :**
```javascript
// ✅ Depuis components/Slider.js vers utils/helpers.js
import { debounce } from '../utils/helpers.js';

export default class Slider {
    // ...
}
```

---

## Erreurs courantes et solutions

### Erreur 1 : Fichier non trouvé (404)

**Symptômes :**
```
GET http://localhost:8000/css/style.css 404 (Not Found)
```

**Causes possibles :**

#### a) Mauvais nombre de `../`

```
mon-site/
├── pages/
│   └── about.html
└── css/
    └── style.css
```

```html
<!-- ❌ ERREUR : pas assez de ../ -->
<link rel="stylesheet" href="css/style.css">
<!-- Le navigateur cherche pages/css/style.css -->

<!-- ✅ CORRECT -->
<link rel="stylesheet" href="../css/style.css">
```

#### b) Mauvais nom de fichier/dossier

```html
<!-- ❌ ERREUR : faute de frappe -->
<link rel="stylesheet" href="assets/css/stlye.css">
<!--                                        └─ "stlye" au lieu de "style" -->

<!-- ✅ CORRECT -->
<link rel="stylesheet" href="assets/css/style.css">
```

#### c) Casse incorrecte (majuscules/minuscules)

Sur certains systèmes (Linux, serveurs), la casse est importante :

```html
<!-- ❌ Peut ne pas fonctionner si le fichier s'appelle "Style.css" -->
<link rel="stylesheet" href="assets/css/style.css">

<!-- ✅ Respecter exactement la casse -->
<link rel="stylesheet" href="assets/css/Style.css">
```

**Bonne pratique :** Toujours utiliser des **minuscules** pour éviter ce problème.

### Erreur 2 : Chemin absolu en local

```html
<!-- ❌ Ne fonctionne pas avec file:// -->
<link rel="stylesheet" href="/css/style.css">
```

**Solution :** Utilisez un serveur local ou des chemins relatifs :

```html
<!-- ✅ Fonctionne partout -->
<link rel="stylesheet" href="./css/style.css">
```

### Erreur 3 : Oublier l'extension .js dans les modules

```javascript
// ❌ ERREUR dans les modules
import Slider from './Slider';

// ✅ CORRECT
import Slider from './Slider.js';
```

### Erreur 4 : Mélanger / et \

Sur Windows, les chemins utilisent `\`, mais sur le web, on utilise **toujours** `/` :

```html
<!-- ❌ ERREUR : backslash Windows -->
<link rel="stylesheet" href="assets\css\style.css">

<!-- ✅ CORRECT : forward slash -->
<link rel="stylesheet" href="assets/css/style.css">
```

---

## Techniques de débogage

### 1. Vérifier dans l'onglet Network des DevTools

**Ouvrez les DevTools** (F12) → Onglet **Network** :

- ✅ **Statut 200** : Fichier chargé avec succès
- ❌ **Statut 404** : Fichier non trouvé
- ❌ **Statut 0 ou CORS error** : Problème de sécurité/serveur

**Astuce :** Cliquez sur une requête échouée pour voir le chemin exact que le navigateur a essayé d'accéder.

### 2. Vérifier le chemin complet

Dans la console, vous pouvez voir le chemin complet :

```javascript
// Dans la console
console.log(window.location.href);
// Résultat : http://localhost:8000/pages/about.html

// Le navigateur résout les chemins relatifs depuis cette URL
```

### 3. Tester étape par étape

Si `../../assets/css/style.css` ne fonctionne pas, testez :

```html
<!-- Trop de ../ ? -->
<link rel="stylesheet" href="../assets/css/style.css">

<!-- Pas assez de ../ ? -->
<link rel="stylesheet" href="../../../assets/css/style.css">

<!-- Nom du dossier incorrect ? -->
<link rel="stylesheet" href="../../asset/css/style.css">
```

### 4. Utiliser l'inspecteur d'éléments

Cliquez droit sur un élément → **Inspecter** → Regardez l'attribut `href` ou `src` :

```html
<!-- Si le lien est souligné en rouge dans DevTools, il est cassé -->
<link rel="stylesheet" href="CHEMIN_CASSÉ">
```

### 5. Afficher visuellement l'arborescence

Créez un fichier `structure.txt` à la racine :

```
mon-site/
├── index.html          ← Je suis ici
├── pages/
│   └── about.html      ← Je veux aller là
└── assets/
    └── css/
        └── style.css   ← Je cherche ce fichier
```

Puis comptez les `../` nécessaires :
- De `index.html` vers `style.css` : `assets/css/style.css`
- De `about.html` vers `style.css` : `../assets/css/style.css`

---

## Bonnes pratiques

### 1. Soyez cohérent

Choisissez une approche et tenez-vous-y dans tout le projet :

```html
<!-- ✅ BON : Cohérent avec ./ partout -->
<link rel="stylesheet" href="./assets/css/style.css">
<script src="./assets/js/main.js"></script>

<!-- ❌ MAUVAIS : Incohérent -->
<link rel="stylesheet" href="assets/css/style.css">
<script src="./assets/js/main.js"></script>
```

### 2. Privilégiez les chemins relatifs en développement

En développement local, les chemins relatifs sont plus flexibles :

```html
<!-- ✅ Fonctionne partout -->
<link rel="stylesheet" href="./css/style.css">

<!-- ❌ Nécessite un serveur -->
<link rel="stylesheet" href="/css/style.css">
```

### 3. Nommez clairement vos dossiers

```
✅ BON : Noms explicites
assets/
├── css/
├── js/
└── images/

❌ MAUVAIS : Noms ambigus
stuff/
├── s/
├── j/
└── i/
```

### 4. Évitez les structures trop profondes

```
❌ MAUVAIS : Trop profond
assets/ui/components/buttons/primary/large/blue/button.css

✅ BON : Maximum 3-4 niveaux
assets/css/components/button-primary.css
```

### 5. Testez sur un serveur local

Avant de déployer, testez toujours avec un serveur local :

```bash
# Python 3
python -m http.server 8000

# Node.js
npx http-server

# VS Code Extension "Live Server"
```

### 6. Documentez votre structure

Ajoutez un fichier `README.md` à la racine :

```markdown
# Structure du projet

```
mon-site/
├── index.html          ← Page d'accueil
├── pages/              ← Autres pages
└── assets/             ← Ressources statiques
    ├── css/            ← Feuilles de style
    ├── js/             ← Scripts JavaScript
    └── images/         ← Images
```

## Comment lier les fichiers
- Depuis la racine : `assets/css/style.css`
- Depuis pages/ : `../assets/css/style.css`
```

---

## Cas d'usage avancés

### 1. Base URL avec `<base>`

Vous pouvez définir une base pour tous les chemins relatifs :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <base href="https://example.com/">
    <!-- Tous les chemins relatifs partent de cette base -->
    <link rel="stylesheet" href="css/style.css">
    <!-- Résolu comme : https://example.com/css/style.css -->
</head>
<body>
    <img src="images/logo.png" alt="Logo">
    <!-- Résolu comme : https://example.com/images/logo.png -->
</body>
</html>
```

**Attention :** `<base>` affecte aussi les liens internes !

### 2. Protocol-relative URLs

Pour des ressources externes, vous pouvez omettre le protocole :

```html
<!-- S'adapte automatiquement à http:// ou https:// -->
<script src="//cdn.example.com/library.js"></script>

<!-- Équivalent à : -->
<script src="https://cdn.example.com/library.js"></script>
<!-- ou -->
<script src="http://cdn.example.com/library.js"></script>
```

### 3. Chemins dans les CSS

Les chemins dans le CSS sont relatifs **au fichier CSS**, pas au HTML :

```
mon-site/
├── index.html
├── assets/
│   ├── css/
│   │   └── style.css
│   └── images/
│       └── bg.jpg
```

**style.css :**
```css
body {
    /* Relatif à style.css, pas à index.html */
    background-image: url('../images/bg.jpg');
    /*                     └─ Remonte de css/ vers assets/
                              puis descend dans images/ */
}
```

**index.html :**
```html
<link rel="stylesheet" href="assets/css/style.css">
```

---

## Aide-mémoire visuel

### Symboles des chemins

```
Symbole  │ Signification           │ Exemple
─────────┼─────────────────────────┼──────────────────────
.        │ Dossier courant         │ ./style.css
..       │ Dossier parent          │ ../css/style.css
/        │ Racine (absolu)         │ /css/style.css
nom/     │ Entrer dans un dossier  │ assets/css/style.css
```

### Compter les niveaux

```
Fichier A              Fichier B            Chemin de A vers B
─────────────────────  ───────────────────  ────────────────────
index.html         →   style.css            style.css
index.html         →   css/style.css        css/style.css
pages/about.html   →   css/style.css        ../css/style.css
pages/blog/post.html → css/style.css        ../../css/style.css
```

**Formule :**
1. Comptez combien de niveaux il faut **remonter** depuis A pour arriver au point commun
2. Chaque niveau = un `../`
3. Ajoutez le chemin **descendant** vers B

---

## Checklist de vérification

Avant de déclarer qu'un chemin ne fonctionne pas, vérifiez :

- [ ] L'extension du fichier est correcte (`.css`, `.js`, `.png`, etc.)
- [ ] Le nom du fichier est exact (pas de faute de frappe)
- [ ] La casse est respectée (majuscules/minuscules)
- [ ] Les slashes sont des `/` et non des `\`
- [ ] Le nombre de `../` est correct
- [ ] Le fichier existe bien à l'endroit indiqué
- [ ] Si module JS : l'extension `.js` est présente
- [ ] Si chemin absolu : un serveur local est en cours d'exécution
- [ ] L'onglet Network des DevTools montre le chemin exact testé

---

## Résumé

### Les deux types de chemins

**Chemins relatifs :**
```html
<!-- Depuis le fichier actuel -->
<link href="./style.css">           <!-- Même dossier -->
<link href="./css/style.css">       <!-- Sous-dossier -->
<link href="../css/style.css">      <!-- Dossier parent puis sous-dossier -->
<link href="../../css/style.css">   <!-- 2 niveaux au-dessus puis sous-dossier -->
```

**Chemins absolus :**
```html
<!-- Depuis la racine du serveur -->
<link href="/css/style.css">

<!-- URL complète -->
<link href="https://example.com/css/style.css">
```

### Règles d'or

1. ✅ **En développement** : utilisez des chemins relatifs
2. ✅ **En production** : les deux approches sont valides
3. ✅ **Pour les modules** : toujours avec `./` et extension `.js`
4. ✅ **Testez** toujours sur un serveur local
5. ✅ **Soyez cohérent** dans tout votre projet
6. ✅ **Tout en minuscules** pour éviter les problèmes de casse

### Formule pour calculer un chemin relatif

```
1. Trouvez le point commun entre les deux fichiers
2. Comptez les niveaux à remonter depuis le fichier source
3. Chaque niveau = un ../
4. Ajoutez le chemin descendant vers le fichier cible
```

### Dépannage rapide

```
Problème : 404 Not Found
→ Vérifier le chemin dans Network (DevTools)
→ Comparer avec la structure réelle des fichiers
→ Vérifier la casse et l'orthographe

Problème : Fonctionne en local mais pas en ligne
→ Passer d'absolus (/) à relatifs (./)
→ Ou configurer le serveur correctement

Problème : Module import ne fonctionne pas
→ Ajouter l'extension .js
→ Utiliser ./ explicitement
→ Vérifier le serveur local (pas file://)
```

---

## Pour aller plus loin

Maintenant que vous maîtrisez les chemins, la prochaine section vous montrera :
- **6.1.5** - Ordre de chargement des ressources pour optimiser les performances

Les chemins peuvent sembler techniques au début, mais avec un peu de pratique, ils deviennent une seconde nature. L'important est de **visualiser** mentalement votre structure de fichiers ! 🗂️

**Astuce finale :** Dessinez votre arborescence sur papier quand vous êtes bloqué. Ça aide vraiment ! 📝

⏭️ [Ordre de chargement des ressources](/06-integration-html-css-javascript/01-architecture-projet-moderne/05-ordre-chargement.md)
