🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.1.2 npm : gestionnaire de paquets 🆕

## Introduction

Imaginez que vous êtes en train de cuisiner et que vous avez besoin d'ingrédients. Plutôt que de tout faire de zéro (cultiver des tomates, élever des poules...), vous allez au supermarché.

**npm** (Node Package Manager) est comme un **supermarché géant pour le code JavaScript**. Au lieu de réécrire chaque fonctionnalité vous-même, vous pouvez télécharger et utiliser du code créé par d'autres développeurs.

---

## Qu'est-ce que npm ?

### Définition simple

**npm** est un **gestionnaire de paquets** (package manager) qui permet de :
- 📦 **Télécharger** des bibliothèques JavaScript créées par la communauté
- 🔄 **Gérer** les dépendances de votre projet
- 📤 **Partager** votre propre code avec le monde entier
- ⚙️ **Automatiser** des tâches de développement

### npm est installé avec Node.js

Quand vous avez installé Node.js (section précédente), npm a été automatiquement installé avec ! Vous pouvez le vérifier :

```bash
npm --version
# Affiche : 10.x.x (ou similaire)
```

---

## Pourquoi npm est révolutionnaire ?

### Avant npm : le chaos 😰

Avant npm (ou des outils similaires), pour utiliser une bibliothèque JavaScript :

1. Aller sur le site web de la bibliothèque
2. Télécharger un fichier `.js` manuellement
3. Le copier dans votre projet
4. Ajouter une balise `<script>` dans votre HTML
5. Si la bibliothèque est mise à jour, tout recommencer !
6. Si la bibliothèque dépend d'autres bibliothèques, télécharger tout manuellement

**Résultat :** Processus long, fastidieux et source d'erreurs.

### Avec npm : la simplicité 🎉

```bash
# Une seule commande pour installer une bibliothèque
npm install jquery

# C'est tout ! jQuery est installé et prêt à être utilisé.
```

npm s'occupe de :
- ✅ Télécharger la bonne version
- ✅ Installer toutes les dépendances nécessaires
- ✅ Gérer les mises à jour
- ✅ Éviter les conflits de versions

---

## Le registre npm : le plus grand supermarché de code

### Des millions de packages

Le registre npm contient plus de **2 millions de packages** (bibliothèques) gratuits et open-source !

```
┌────────────────────────────────────────┐
│       Registre npm (npmjs.com)         │
├────────────────────────────────────────┤
│  📦 React                              │
│  📦 Vue.js                             │
│  📦 Lodash                             │
│  📦 Axios                              │
│  📦 Express                            │
│  📦 ... et 2 000 000+ autres packages  │
└────────────────────────────────────────┘
```

### Explorer le registre

Visitez [npmjs.com](https://www.npmjs.com) pour :
- Rechercher des packages
- Lire la documentation
- Voir le nombre de téléchargements
- Consulter les versions disponibles

---

## Anatomie d'un package npm

### Qu'est-ce qu'un package ?

Un **package** (ou paquet) est simplement :
- Du code JavaScript réutilisable
- Empaqueté avec des métadonnées (nom, version, auteur...)
- Publié sur le registre npm

### Exemples de packages populaires

| Package | Description | Téléchargements/semaine |
|---------|-------------|-------------------------|
| **React** | Bibliothèque pour créer des interfaces utilisateur | ~20 millions |
| **Lodash** | Utilitaires JavaScript | ~40 millions |
| **Axios** | Client HTTP pour faire des requêtes | ~45 millions |
| **Express** | Framework web pour Node.js | ~25 millions |
| **date-fns** | Manipulation de dates | ~15 millions |

---

## Installer des packages

### Installation locale (dans un projet)

C'est le mode le plus courant. Le package est installé **uniquement dans votre projet**.

```bash
# Syntaxe de base
npm install nom-du-package

# Exemples
npm install lodash
npm install axios
npm install date-fns

# Forme courte (i au lieu de install)
npm i lodash
```

**Résultat :**
- Le package est téléchargé dans le dossier `node_modules/`
- Il est ajouté à votre fichier `package.json`

### Installation globale (sur votre système)

Pour des outils en ligne de commande que vous voulez utiliser partout :

```bash
# Avec le flag -g (global)
npm install -g nom-du-package

# Exemples d'outils globaux
npm install -g http-server    # Serveur web simple
npm install -g create-react-app
npm install -g @vue/cli
```

**Quand utiliser l'installation globale ?**
- Pour des **outils CLI** (Command Line Interface)
- Pour des **utilitaires** que vous utilisez sur tous vos projets
- **Attention :** N'installez PAS les dépendances de vos projets en global !

### Installation de plusieurs packages en une fois

```bash
npm install lodash axios date-fns
# Installe les 3 packages en même temps
```

---

## Le dossier node_modules

### Le mystérieux dossier

Quand vous installez un package, npm crée un dossier `node_modules/` :

```
mon-projet/
├── index.html
├── style.css
├── script.js
├── package.json
└── node_modules/           ⬅️ Créé par npm
    ├── lodash/
    ├── axios/
    └── ... (peut contenir des centaines de dossiers !)
```

### Pourquoi il est si gros ?

Le dossier `node_modules/` peut devenir **énorme** (plusieurs centaines de Mo) parce que :
1. Il contient tous les packages que vous avez installés
2. Il contient aussi toutes les **dépendances des dépendances** !

**Exemple :**
```
Vous installez React
  → React dépend de "loose-envify"
    → loose-envify dépend de "js-tokens"
      → etc.

Résultat : npm installe tout automatiquement !
```

### ⚠️ Ne JAMAIS versionner node_modules

Le dossier `node_modules/` ne doit **jamais** être ajouté à Git !

**Pourquoi ?**
- Trop volumineux (ralentit Git)
- Inutile (peut être recréé avec `npm install`)
- Spécifique à votre système d'exploitation

**Solution :** Ajoutez-le au `.gitignore` :

```gitignore
# .gitignore
node_modules/
```

---

## Les commandes npm essentielles

### npm install (ou npm i)

Installe les packages.

```bash
# Installer un package
npm install lodash

# Installer avec une version spécifique
npm install lodash@4.17.21

# Installer toutes les dépendances listées dans package.json
npm install
```

### npm uninstall (ou npm un)

Désinstalle un package.

```bash
npm uninstall lodash

# Forme courte
npm un lodash
```

### npm update

Met à jour les packages.

```bash
# Mettre à jour tous les packages
npm update

# Mettre à jour un package spécifique
npm update lodash
```

### npm list (ou npm ls)

Liste les packages installés.

```bash
# Liste tous les packages
npm list

# Liste uniquement les dépendances directes (sans les sous-dépendances)
npm list --depth=0

# Vérifier si un package est installé
npm list lodash
```

### npm outdated

Vérifie quels packages ont des mises à jour disponibles.

```bash
npm outdated
```

Affiche un tableau avec :
- Current : version actuelle
- Wanted : version compatible disponible
- Latest : dernière version publiée

### npm search

Recherche des packages dans le registre npm.

```bash
npm search date manipulation
```

---

## Types de dépendances

### dependencies (dépendances de production)

Packages **nécessaires** pour que votre application fonctionne en production.

```bash
npm install lodash
# Ajoute lodash aux "dependencies" de package.json
```

**Exemples :**
- React, Vue.js (frameworks)
- Axios (requêtes HTTP)
- Lodash (utilitaires)

### devDependencies (dépendances de développement)

Packages utilisés **uniquement pendant le développement**, pas en production.

```bash
npm install --save-dev eslint
# ou
npm install -D eslint

# Ajoute eslint aux "devDependencies" de package.json
```

**Exemples :**
- ESLint (vérification de code)
- Prettier (formatage)
- Webpack, Vite (outils de build)
- Jest (tests)

### Pourquoi cette distinction ?

En production, vous n'avez pas besoin des outils de développement :

```bash
# Installation normale (tout)
npm install

# Installation en production (sans devDependencies)
npm install --production
```

Cela réduit la taille du déploiement et améliore la sécurité.

---

## Scripts npm

### Automatisation avec npm scripts

Dans `package.json`, vous pouvez définir des **scripts** - des commandes personnalisées.

**Exemple de package.json :**

```json
{
  "name": "mon-projet",
  "version": "1.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint .",
    "test": "jest"
  }
}
```

### Exécuter des scripts

```bash
# Lancer le script "dev"
npm run dev

# Lancer le script "build"
npm run build

# Scripts spéciaux (pas besoin de "run")
npm start    # Équivalent à "npm run start"
npm test     # Équivalent à "npm run test"
```

### Scripts courants dans les projets modernes

| Script | Fonction typique |
|--------|------------------|
| `dev` ou `start` | Démarrer le serveur de développement |
| `build` | Construire pour la production |
| `preview` | Prévisualiser la version de production |
| `lint` | Vérifier la qualité du code |
| `test` | Lancer les tests |
| `format` | Formater le code |

---

## Versions et versionning sémantique (SemVer)

### Format de version : MAJEUR.MINEUR.PATCH

npm utilise le **versionning sémantique** (Semantic Versioning) :

```
     MAJEUR . MINEUR . PATCH
        ↓       ↓       ↓
       2   .   4   .   1

MAJEUR : Changements incompatibles (breaking changes)
MINEUR : Nouvelles fonctionnalités (compatibles)
PATCH  : Corrections de bugs
```

### Symboles de version dans package.json

```json
{
  "dependencies": {
    "lodash": "4.17.21",      // Version exacte
    "axios": "^1.6.0",        // Compatible avec 1.x.x
    "react": "~18.2.0"        // Compatible avec 18.2.x
  }
}
```

| Symbole | Signification | Exemple | Versions acceptées |
|---------|---------------|---------|-------------------|
| Aucun | Version exacte | `1.2.3` | Seulement 1.2.3 |
| `^` (caret) | Mineur et patch | `^1.2.3` | ≥1.2.3 et <2.0.0 |
| `~` (tilde) | Patch seulement | `~1.2.3` | ≥1.2.3 et <1.3.0 |
| `*` | Toute version | `*` | Toutes versions (⚠️ dangereux) |

**Recommandation :** Le symbole `^` est le plus utilisé et le plus sûr.

---

## npm init : créer un projet

### Initialiser un nouveau projet

```bash
# Mode interactif (pose des questions)
npm init

# Mode rapide (accepte tous les défauts)
npm init -y
```

Cela crée un fichier `package.json` de base :

```json
{
  "name": "mon-projet",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

### Créer un projet avec un template

```bash
# Créer un projet React avec Vite
npm create vite@latest mon-app -- --template react

# Créer un projet Vue
npm create vite@latest mon-app -- --template vue

# Créer un projet Vanilla JS
npm create vite@latest mon-app -- --template vanilla
```

---

## npx : exécuter des packages sans installation

### Qu'est-ce que npx ?

**npx** est livré avec npm et permet d'**exécuter** des packages sans les installer.

```bash
# SANS npx (il faut installer d'abord)
npm install -g create-react-app
create-react-app mon-app

# AVEC npx (exécution directe)
npx create-react-app mon-app
```

### Avantages de npx

1. **Pas d'installation globale** nécessaire
2. **Toujours la dernière version**
3. **Économie d'espace disque**
4. **Parfait pour les outils ponctuels**

### Cas d'usage courants

```bash
# Créer un projet
npx create-react-app mon-app
npx create-vite@latest mon-projet

# Lancer un serveur HTTP simple
npx http-server

# Exécuter un package temporairement
npx cowsay "Hello npm!"
```

---

## Bonnes pratiques npm

### ✅ À faire

1. **Toujours avoir un package.json** dans vos projets
   ```bash
   npm init -y
   ```

2. **Ignorer node_modules dans Git**
   ```gitignore
   node_modules/
   ```

3. **Documenter les scripts** dans le README
   ```markdown
   ## Scripts disponibles
   - `npm run dev` : Lance le serveur de développement
   - `npm run build` : Compile pour la production
   ```

4. **Vérifier les mises à jour régulièrement**
   ```bash
   npm outdated
   npm update
   ```

5. **Utiliser des versions précises en production**
   ```json
   {
     "dependencies": {
       "react": "18.2.0"  // Pas de ^ pour la stabilité
     }
   }
   ```

### ❌ À éviter

1. **Ne jamais modifier directement node_modules**
   - Les changements seront écrasés à la prochaine installation

2. **Ne pas installer tous les packages en global**
   - Préférez les installations locales par projet

3. **Ne pas ignorer les avertissements de sécurité**
   ```bash
   npm audit        # Vérifier les vulnérabilités
   npm audit fix    # Corriger automatiquement
   ```

4. **Ne pas utiliser sudo avec npm** (sur Mac/Linux)
   - Si nécessaire, reconfigurez npm

5. **Ne pas copier node_modules entre projets**
   - Faites toujours `npm install`

---

## npm et la sécurité

### npm audit : vérifier les vulnérabilités

npm intègre un système de vérification de sécurité :

```bash
# Analyser les vulnérabilités
npm audit

# Affiche un rapport avec :
# - Nombre de vulnérabilités
# - Niveau de gravité (low, moderate, high, critical)
# - Packages concernés
```

### Corriger les vulnérabilités

```bash
# Correction automatique (si possible)
npm audit fix

# Correction forcée (peut causer des breaking changes)
npm audit fix --force
```

### Bonnes pratiques de sécurité

1. **Mettre à jour régulièrement**
   ```bash
   npm update
   npm audit fix
   ```

2. **Utiliser des packages populaires et maintenus**
   - Vérifiez les téléchargements/semaine
   - Vérifiez la date de dernière mise à jour

3. **Ne jamais publier vos credentials**
   - Pas de mots de passe dans package.json
   - Utilisez des variables d'environnement

---

## Alternatives à npm

### Yarn

Créé par Facebook, Yarn est une alternative à npm :

```bash
# Installation
npm install -g yarn

# Utilisation (similaire à npm)
yarn add lodash        # équivalent à npm install lodash
yarn remove lodash     # équivalent à npm uninstall lodash
```

**Avantages :**
- Légèrement plus rapide
- Fichier yarn.lock pour la reproductibilité
- Interface utilisateur plus jolie

### pnpm

pnpm (performant npm) est une autre alternative :

```bash
# Installation
npm install -g pnpm

# Utilisation
pnpm add lodash
pnpm remove lodash
```

**Avantages :**
- **Beaucoup plus rapide** que npm
- **Économise beaucoup d'espace disque** (stockage partagé)
- Compatible avec npm

### Lequel choisir ?

| Gestionnaire | Recommandé pour |
|--------------|-----------------|
| **npm** | Débutants, compatibilité maximale |
| **Yarn** | Équipes, projets avec monorepos |
| **pnpm** | Performance, économie d'espace |

**Conseil pour débuter :** Commencez avec **npm**, c'est le standard et il est déjà installé.

---

## Workflow typique avec npm

### 1. Créer un nouveau projet

```bash
# Créer un dossier
mkdir mon-projet
cd mon-projet

# Initialiser npm
npm init -y

# Installer un outil de build (ex: Vite)
npm create vite@latest . -- --template vanilla
npm install
```

### 2. Développer

```bash
# Installer des dépendances au fur et à mesure
npm install axios
npm install -D eslint

# Lancer le serveur de développement
npm run dev
```

### 3. Tester et valider

```bash
# Vérifier la qualité du code
npm run lint

# Vérifier les vulnérabilités
npm audit

# Lancer les tests
npm test
```

### 4. Préparer pour la production

```bash
# Construire pour la production
npm run build

# Le résultat est généralement dans un dossier dist/ ou build/
```

### 5. Partager le projet

**Sur Git :**
```bash
git add .
git commit -m "Initial commit"
git push
```

**Autre développeur qui clone le projet :**
```bash
git clone https://github.com/user/mon-projet.git
cd mon-projet
npm install    # Installe toutes les dépendances
npm run dev    # Lance le projet
```

---

## Comprendre package-lock.json

### Qu'est-ce que c'est ?

Quand vous faites `npm install`, npm crée un fichier `package-lock.json` :

```
mon-projet/
├── package.json           ⬅️ Vos dépendances (versions flexibles)
├── package-lock.json      ⬅️ Versions exactes installées
└── node_modules/
```

### Pourquoi il existe ?

**Problème :**
```json
// package.json
{
  "dependencies": {
    "lodash": "^4.17.0"  // Peut installer 4.17.0, 4.17.21, 4.18.0...
  }
}
```

Sans `package-lock.json`, deux développeurs pourraient avoir des versions différentes !

**Solution :**
```json
// package-lock.json
{
  "dependencies": {
    "lodash": {
      "version": "4.17.21"  // Version EXACTE
    }
  }
}
```

### Faut-il le versionner dans Git ?

**✅ OUI !** Contrairement à `node_modules/`, vous **devez** versionner `package-lock.json`.

**Pourquoi ?**
- Garantit que tous les développeurs ont les mêmes versions
- Garantit que la production a les mêmes versions que le développement
- Évite les bugs "ça marche sur ma machine !"

---

## Ressources et documentation

### Documentation officielle

- [npmjs.com](https://www.npmjs.com) - Registre et recherche de packages
- [docs.npmjs.com](https://docs.npmjs.com) - Documentation complète

### Commandes utiles

```bash
# Aide sur npm
npm help

# Aide sur une commande spécifique
npm help install

# Version de npm
npm --version

# Configuration actuelle
npm config list

# Nettoyer le cache (si problèmes)
npm cache clean --force
```

---

## Ce qu'il faut retenir

### ✅ Points essentiels

1. **npm est le gestionnaire de packages de JavaScript**
   - Plus de 2 millions de packages disponibles
   - Installé automatiquement avec Node.js

2. **npm facilite la gestion des dépendances**
   - Installation en une commande
   - Mise à jour simplifiée
   - Gestion des versions automatique

3. **Les commandes de base à connaître**
   ```bash
   npm init          # Créer un projet
   npm install       # Installer des packages
   npm run           # Exécuter des scripts
   npm update        # Mettre à jour
   npm audit         # Vérifier la sécurité
   ```

4. **node_modules/ ne se versionne pas**
   - Ajoutez-le au .gitignore
   - Il peut être recréé avec `npm install`

5. **package-lock.json se versionne**
   - Garantit la reproductibilité
   - Assure que tout le monde a les mêmes versions

### 🎯 Prochaine étape

Maintenant que vous comprenez npm, découvrons le fichier **package.json** en détail - le cœur de tout projet JavaScript moderne.

---

## FAQ - Questions fréquentes

**Q : Quelle est la différence entre npm et Node.js ?**
R : Node.js est l'environnement d'exécution JavaScript, npm est le gestionnaire de packages qui est installé avec Node.js.

**Q : Faut-il installer npm séparément ?**
R : Non, npm est automatiquement installé avec Node.js.

**Q : Pourquoi node_modules est-il si gros ?**
R : Parce qu'il contient tous les packages et toutes leurs dépendances. C'est normal et nécessaire.

**Q : Puis-je supprimer node_modules ?**
R : Oui ! Vous pouvez le supprimer à tout moment et le recréer avec `npm install`.

**Q : Quelle est la différence entre npm install et npm ci ?**
R : `npm ci` (Clean Install) utilise package-lock.json pour une installation exacte et plus rapide. Utilisé principalement en CI/CD.

**Q : Comment mettre à jour npm lui-même ?**
R : `npm install -g npm@latest`

**Q : Que faire si npm install ne fonctionne pas ?**
R : Essayez :
```bash
rm -rf node_modules
rm package-lock.json
npm cache clean --force
npm install
```

---


⏭️ [package.json et dépendances](/08-ecosysteme-javascript-moderne/01-comprendre-ecosysteme/03-package-json.md)
