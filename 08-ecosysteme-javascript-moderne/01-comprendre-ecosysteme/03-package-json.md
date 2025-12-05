🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.1.3 package.json et dépendances 🆕

## Introduction

Si votre projet JavaScript est une maison, alors le fichier **package.json** en est le **plan d'architecte**. Il contient toutes les informations essentielles sur votre projet : son nom, sa version, ses dépendances, ses scripts, et bien plus encore.

Ce fichier est le **cœur de tout projet JavaScript moderne**. Comprendre sa structure et son utilisation est absolument essentiel pour tout développeur web.

---

## Qu'est-ce que package.json ?

### Définition

**package.json** est un fichier de configuration JSON qui décrit votre projet JavaScript. Il contient :
- 📝 Les **métadonnées** du projet (nom, version, description...)
- 📦 Les **dépendances** (bibliothèques nécessaires)
- ⚙️ Les **scripts** (commandes automatisées)
- 🔧 La **configuration** de divers outils

### Format JSON

Le fichier est au format JSON (JavaScript Object Notation) :

```json
{
  "nom": "valeur",
  "liste": ["élément1", "élément2"],
  "objet": {
    "propriété": "valeur"
  }
}
```

**Important :** JSON est strict !
- Guillemets doubles obligatoires : `"clé"` ✅, `'clé'` ❌
- Pas de virgule après le dernier élément
- Pas de commentaires (contrairement à JavaScript)

---

## Créer un package.json

### Méthode 1 : npm init (interactif)

```bash
npm init
```

npm vous pose des questions :

```
package name: (mon-projet)         # Nom du projet
version: (1.0.0)                   # Version initiale
description:                       # Description courte
entry point: (index.js)            # Fichier principal
test command:                      # Commande de test
git repository:                    # URL du repo Git
keywords:                          # Mots-clés pour npmjs.com
author:                            # Votre nom
license: (ISC)                     # Type de licence
```

### Méthode 2 : npm init -y (rapide)

```bash
npm init -y
```

Crée un package.json avec des valeurs par défaut :

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

### Méthode 3 : Avec un outil (Vite, Create React App...)

```bash
npm create vite@latest mon-projet
```

Crée automatiquement un package.json adapté au type de projet.

---

## Anatomie complète d'un package.json

Voici un exemple complet avec tous les champs importants :

```json
{
  "name": "mon-super-projet",
  "version": "1.2.3",
  "description": "Une application web moderne et performante",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint .",
    "format": "prettier --write .",
    "test": "jest"
  },
  "keywords": ["web", "javascript", "moderne"],
  "author": "Votre Nom <email@example.com>",
  "license": "MIT",
  "repository": {
    "type": "git",
    "url": "https://github.com/username/mon-projet.git"
  },
  "bugs": {
    "url": "https://github.com/username/mon-projet/issues"
  },
  "homepage": "https://mon-projet.com",
  "dependencies": {
    "axios": "^1.6.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.2.0",
    "eslint": "^8.55.0",
    "prettier": "^3.1.0",
    "vite": "^5.0.0"
  },
  "engines": {
    "node": ">=18.0.0",
    "npm": ">=9.0.0"
  },
  "browserslist": [
    ">0.2%",
    "not dead",
    "not op_mini all"
  ]
}
```

Décortiquons chaque section ! 👇

---

## Métadonnées de base

### name (obligatoire)

Le nom de votre projet.

```json
{
  "name": "mon-projet"
}
```

**Règles :**
- Tout en minuscules
- Pas d'espaces (utilisez `-` ou `_`)
- Maximum 214 caractères
- Évitez les caractères spéciaux

**Exemples valides :**
```json
"name": "mon-super-projet"      ✅
"name": "my-awesome-app"        ✅
"name": "projet_web"            ✅
```

**Exemples invalides :**
```json
"name": "Mon Projet"            ❌ (espaces et majuscules)
"name": "mon@projet"            ❌ (caractère spécial)
```

### version (obligatoire)

La version de votre projet, au format **sémantique** (SemVer).

```json
{
  "version": "1.2.3"
}
```

**Format : MAJEUR.MINEUR.PATCH**

```
  1   .   2   .   3
  ↓       ↓       ↓
MAJEUR MINEUR PATCH

MAJEUR : Changements incompatibles (breaking changes)
MINEUR : Nouvelles fonctionnalités (rétrocompatibles)
PATCH  : Corrections de bugs
```

**Exemples d'évolution :**
```
1.0.0 → Première version stable
1.0.1 → Correction d'un bug
1.1.0 → Ajout d'une nouvelle fonctionnalité
2.0.0 → Refonte majeure (breaking changes)
```

### description

Une courte description de votre projet.

```json
{
  "description": "Une application de gestion de tâches moderne et intuitive"
}
```

**Utilité :**
- Apparaît sur npmjs.com si vous publiez
- Aide à comprendre rapidement le projet
- Utile pour la recherche

### keywords

Mots-clés pour faciliter la recherche de votre package.

```json
{
  "keywords": ["todo", "tasks", "productivity", "react"]
}
```

### author

Informations sur l'auteur.

```json
{
  "author": "Jean Dupont <jean.dupont@email.com> (https://jeandupont.com)"
}
```

**Format alternatif (objet) :**
```json
{
  "author": {
    "name": "Jean Dupont",
    "email": "jean.dupont@email.com",
    "url": "https://jeandupont.com"
  }
}
```

### license

Type de licence du projet.

```json
{
  "license": "MIT"
}
```

**Licences courantes :**
- `MIT` : Très permissive, la plus utilisée
- `ISC` : Similaire à MIT
- `Apache-2.0` : Permissive avec protection de brevet
- `GPL-3.0` : Copyleft (modifications doivent rester open-source)
- `UNLICENSED` : Propriétaire, pas de licence

### repository

Lien vers le dépôt Git.

```json
{
  "repository": {
    "type": "git",
    "url": "https://github.com/username/mon-projet.git"
  }
}
```

**Format court :**
```json
{
  "repository": "github:username/mon-projet"
}
```

### bugs

URL pour signaler des bugs.

```json
{
  "bugs": {
    "url": "https://github.com/username/mon-projet/issues",
    "email": "support@mon-projet.com"
  }
}
```

### homepage

URL du site web du projet.

```json
{
  "homepage": "https://mon-projet.com"
}
```

---

## Champs techniques

### main

Le fichier d'entrée principal de votre projet.

```json
{
  "main": "index.js"
}
```

**Utilité :** Quand quelqu'un fait `import monProjet from 'mon-projet'`, Node.js charge ce fichier.

### type

Définit le système de modules utilisé.

```json
{
  "type": "module"
}
```

**Valeurs possibles :**
- `"commonjs"` (par défaut) : Utilise `require()` et `module.exports`
- `"module"` : Utilise `import` et `export` (ES Modules)

**Différence :**

```javascript
// CommonJS (type: "commonjs")
const axios = require('axios');
module.exports = maFonction;

// ES Modules (type: "module")
import axios from 'axios';
export default maFonction;
```

### engines

Spécifie les versions de Node.js et npm requises.

```json
{
  "engines": {
    "node": ">=18.0.0",
    "npm": ">=9.0.0"
  }
}
```

**Opérateurs :**
- `>=18.0.0` : Version 18 ou supérieure
- `^18.0.0` : Compatible avec 18.x.x
- `18.x` : Toute version 18
- `18.0.0 - 20.0.0` : Entre 18 et 20

### browserslist

Liste des navigateurs ciblés (pour Babel, Autoprefixer...).

```json
{
  "browserslist": [
    ">0.2%",
    "not dead",
    "not op_mini all"
  ]
}
```

**Signification :**
- `>0.2%` : Navigateurs avec plus de 0.2% de part de marché
- `not dead` : Navigateurs encore maintenus
- `not op_mini all` : Exclut Opera Mini

---

## Scripts npm

### Qu'est-ce qu'un script ?

Les scripts sont des **commandes personnalisées** que vous pouvez exécuter avec `npm run`.

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

**Exécution :**
```bash
npm run dev     # Lance "vite"
npm run build   # Lance "vite build"
npm run preview # Lance "vite preview"
```

### Scripts spéciaux (sans "run")

Certains scripts peuvent être lancés sans `npm run` :

```json
{
  "scripts": {
    "start": "node index.js",
    "test": "jest",
    "preinstall": "echo 'Installation en cours...'",
    "postinstall": "echo 'Installation terminée !'"
  }
}
```

**Exécution :**
```bash
npm start       # Au lieu de "npm run start"
npm test        # Au lieu de "npm run test"
```

### Scripts du cycle de vie

npm exécute automatiquement certains scripts à des moments précis :

| Script | Moment d'exécution |
|--------|-------------------|
| `preinstall` | Avant `npm install` |
| `install` / `postinstall` | Après `npm install` |
| `preuninstall` | Avant `npm uninstall` |
| `postuninstall` | Après `npm uninstall` |
| `pretest` | Avant `npm test` |
| `test` | Lors de `npm test` |
| `posttest` | Après `npm test` |

**Exemple pratique :**

```json
{
  "scripts": {
    "prebuild": "npm run lint",
    "build": "vite build",
    "postbuild": "echo 'Build terminé ! ✅'"
  }
}
```

Quand vous faites `npm run build`, npm exécute automatiquement :
1. `prebuild` (lint)
2. `build` (build)
3. `postbuild` (message)

### Scripts courants dans un projet moderne

```json
{
  "scripts": {
    "dev": "vite",                              // Serveur de développement
    "build": "vite build",                      // Build de production
    "preview": "vite preview",                  // Prévisualiser le build
    "lint": "eslint . --ext js,jsx",           // Vérification du code
    "lint:fix": "eslint . --ext js,jsx --fix", // Correction auto
    "format": "prettier --write .",             // Formatage
    "format:check": "prettier --check .",       // Vérif formatage
    "test": "jest",                             // Tests unitaires
    "test:watch": "jest --watch",               // Tests en continu
    "test:coverage": "jest --coverage",         // Couverture de tests
    "clean": "rm -rf dist node_modules",        // Nettoyage
    "typecheck": "tsc --noEmit"                 // Vérif TypeScript
  }
}
```

### Enchaîner plusieurs commandes

**Séquentiel (l'une après l'autre) :**

```json
{
  "scripts": {
    "build": "npm run lint && npm run test && vite build"
  }
}
```

`&&` : La suivante s'exécute **seulement si** la précédente réussit.

**Parallèle (en même temps) :**

```json
{
  "scripts": {
    "watch": "npm run watch:css & npm run watch:js"
  }
}
```

`&` : Les commandes s'exécutent en parallèle.

### Passer des arguments

```bash
npm run dev -- --port 8080
```

Tout après `--` est passé au script.

---

## Dépendances (dependencies)

### Qu'est-ce qu'une dépendance ?

Une **dépendance** est une bibliothèque externe dont votre projet a **besoin pour fonctionner**.

```json
{
  "dependencies": {
    "axios": "^1.6.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "lodash": "^4.17.21"
  }
}
```

### Quand utiliser dependencies ?

Pour les packages **nécessaires en production** :
- Frameworks (React, Vue, Angular)
- Bibliothèques utilitaires (Lodash, date-fns)
- Clients HTTP (Axios, Fetch)
- Bibliothèques de composants (Material-UI, Bootstrap)

**Principe :** Si le code ne fonctionne pas sans ce package, c'est une **dependency**.

### Installer une dependency

```bash
npm install axios
# ou
npm install axios react react-dom
```

npm l'ajoute automatiquement à `dependencies` dans package.json.

---

## Dépendances de développement (devDependencies)

### Qu'est-ce qu'une devDependency ?

Une **devDependency** est un outil nécessaire **uniquement pendant le développement**, pas en production.

```json
{
  "devDependencies": {
    "vite": "^5.0.0",
    "eslint": "^8.55.0",
    "prettier": "^3.1.0",
    "jest": "^29.7.0",
    "@vitejs/plugin-react": "^4.2.0"
  }
}
```

### Quand utiliser devDependencies ?

Pour les outils de **développement** :
- Build tools (Vite, Webpack, Parcel)
- Linters (ESLint)
- Formatters (Prettier)
- Frameworks de test (Jest, Vitest)
- Transpilateurs (Babel, TypeScript)
- Plugins et extensions

**Principe :** Si c'est un **outil** et pas du code qui tourne dans l'application finale, c'est une **devDependency**.

### Installer une devDependency

```bash
npm install --save-dev eslint
# ou forme courte
npm install -D eslint

# Plusieurs à la fois
npm install -D eslint prettier jest
```

### Importance de la distinction

En production, vous n'installez que les **dependencies** :

```bash
npm install --production
# ou
npm install --omit=dev
```

**Avantages :**
- ✅ Déploiement plus rapide (moins de packages)
- ✅ Taille réduite (node_modules plus léger)
- ✅ Surface d'attaque réduite (moins de vulnérabilités potentielles)

---

## Versions et spécificateurs

### Format de version

```json
{
  "dependencies": {
    "axios": "^1.6.0"
  }
}
```

Le symbole `^` est un **spécificateur de version**.

### Symboles de version

| Symbole | Nom | Signification | Exemple | Versions acceptées |
|---------|-----|---------------|---------|-------------------|
| Aucun | Exacte | Version exacte seulement | `1.2.3` | 1.2.3 uniquement |
| `^` | Caret | Compatible MINEUR | `^1.2.3` | ≥1.2.3 et <2.0.0 |
| `~` | Tilde | Compatible PATCH | `~1.2.3` | ≥1.2.3 et <1.3.0 |
| `*` | Wildcard | Toute version | `*` | N'importe quelle version |
| `>=` | Supérieur ou égal | Version minimale | `>=1.2.3` | 1.2.3 et supérieur |
| `<` | Inférieur | Version maximale | `<2.0.0` | Inférieur à 2.0.0 |
| `||` | OU logique | L'une ou l'autre | `^1.0.0 || ^2.0.0` | 1.x ou 2.x |

### Exemples détaillés

**^ (Caret) - Le plus utilisé**

```json
{
  "dependencies": {
    "axios": "^1.6.0"
  }
}
```

Accepte :
- ✅ 1.6.0
- ✅ 1.6.1 (patch)
- ✅ 1.7.0 (mineur)
- ✅ 1.99.99 (mineur)
- ❌ 2.0.0 (majeur)

**~ (Tilde) - Plus restrictif**

```json
{
  "dependencies": {
    "react": "~18.2.0"
  }
}
```

Accepte :
- ✅ 18.2.0
- ✅ 18.2.1 (patch)
- ✅ 18.2.99 (patch)
- ❌ 18.3.0 (mineur)
- ❌ 19.0.0 (majeur)

**Version exacte - Le plus stable**

```json
{
  "dependencies": {
    "lodash": "4.17.21"
  }
}
```

Accepte :
- ✅ 4.17.21 uniquement
- ❌ Toute autre version

### Quelle stratégie choisir ?

| Situation | Recommandation | Raison |
|-----------|----------------|--------|
| **Développement** | `^` (caret) | Profiter des mises à jour compatibles |
| **Production critique** | Version exacte | Stabilité maximale |
| **Applications** | `^` ou `~` | Équilibre entre stabilité et mises à jour |
| **Bibliothèques** | `^` | Compatibilité large |

**En pratique :** npm utilise `^` par défaut, c'est un bon choix.

---

## Autres types de dépendances

### peerDependencies

Spécifie qu'un package nécessite qu'un autre package soit installé **par l'utilisateur**.

```json
{
  "peerDependencies": {
    "react": "^18.0.0"
  }
}
```

**Cas d'usage :** Plugins et extensions.

**Exemple :** Un plugin React nécessite que React soit déjà installé, mais ne l'installe pas lui-même.

### optionalDependencies

Dépendances facultatives qui ne bloquent pas l'installation si elles échouent.

```json
{
  "optionalDependencies": {
    "fsevents": "^2.3.0"
  }
}
```

**Cas d'usage :** Optimisations spécifiques à un OS (ex: fsevents pour macOS).

### bundledDependencies

Packages inclus directement dans votre tarball npm.

```json
{
  "bundledDependencies": ["package-a", "package-b"]
}
```

**Cas d'usage :** Très rare, pour des cas spécifiques.

---

## Configuration d'outils externes

Certains outils peuvent être configurés directement dans package.json :

### ESLint

```json
{
  "eslintConfig": {
    "extends": ["eslint:recommended"],
    "env": {
      "browser": true,
      "es2021": true
    }
  }
}
```

### Prettier

```json
{
  "prettier": {
    "semi": true,
    "singleQuote": true,
    "tabWidth": 2
  }
}
```

### Babel

```json
{
  "babel": {
    "presets": ["@babel/preset-env", "@babel/preset-react"]
  }
}
```

### Jest

```json
{
  "jest": {
    "testEnvironment": "jsdom",
    "collectCoverage": true
  }
}
```

**Note :** Souvent, ces configurations sont placées dans des fichiers dédiés (`.eslintrc.js`, `.prettierrc`, etc.) pour plus de lisibilité.

---

## Bonnes pratiques

### ✅ À faire

1. **Versionner package.json**
   ```bash
   git add package.json package-lock.json
   git commit -m "Update dependencies"
   ```

2. **Documenter les scripts dans le README**
   ```markdown
   ## Scripts disponibles

   - `npm run dev` : Lance le serveur de développement
   - `npm run build` : Compile pour la production
   - `npm test` : Lance les tests
   ```

3. **Garder les dépendances à jour**
   ```bash
   npm outdated
   npm update
   ```

4. **Vérifier la sécurité**
   ```bash
   npm audit
   npm audit fix
   ```

5. **Utiliser des versions précises pour la production**
   ```json
   {
     "dependencies": {
       "react": "18.2.0"  // Pas de ^
     }
   }
   ```

6. **Bien séparer dependencies et devDependencies**
   - Production → dependencies
   - Développement uniquement → devDependencies

### ❌ À éviter

1. **Ne pas modifier package.json manuellement pour ajouter des dépendances**
   - Utilisez `npm install` qui gère tout automatiquement

2. **Ne pas utiliser `*` comme version**
   ```json
   {
     "dependencies": {
       "axios": "*"  // ❌ Trop risqué !
     }
   }
   ```

3. **Ne pas ignorer les avertissements npm**
   ```bash
   npm WARN deprecated package@1.0.0
   # Mettez à jour le package !
   ```

4. **Ne pas mélanger les gestionnaires de paquets**
   - Choisissez npm OU yarn OU pnpm
   - Ne mélangez pas dans le même projet

5. **Ne pas commiter node_modules**
   - Uniquement package.json et package-lock.json

---

## Exemple complet d'un projet réel

Voici un package.json complet pour un projet React avec Vite :

```json
{
  "name": "my-react-app",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "description": "Une application React moderne avec Vite",
  "author": "Jean Dupont <jean@example.com>",
  "license": "MIT",
  "keywords": ["react", "vite", "web-app"],
  "repository": {
    "type": "git",
    "url": "https://github.com/username/my-react-app.git"
  },
  "bugs": {
    "url": "https://github.com/username/my-react-app/issues"
  },
  "homepage": "https://github.com/username/my-react-app#readme",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "lint:fix": "eslint . --ext js,jsx --fix",
    "format": "prettier --write \"src/**/*.{js,jsx,css}\"",
    "format:check": "prettier --check \"src/**/*.{js,jsx,css}\"",
    "test": "vitest",
    "test:ui": "vitest --ui",
    "test:coverage": "vitest --coverage"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.20.0",
    "axios": "^1.6.2"
  },
  "devDependencies": {
    "@types/react": "^18.2.43",
    "@types/react-dom": "^18.2.17",
    "@vitejs/plugin-react": "^4.2.1",
    "eslint": "^8.55.0",
    "eslint-plugin-react": "^7.33.2",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.5",
    "prettier": "^3.1.1",
    "vite": "^5.0.8",
    "vitest": "^1.0.4"
  },
  "engines": {
    "node": ">=18.0.0",
    "npm": ">=9.0.0"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

---

## Commandes utiles

### Voir les informations

```bash
# Afficher le contenu de package.json
cat package.json

# Afficher les dépendances installées
npm list --depth=0

# Voir les infos d'un package
npm view axios

# Voir toutes les versions disponibles
npm view axios versions
```

### Mettre à jour package.json

```bash
# Mettre à jour un package
npm update axios

# Mettre à jour tous les packages
npm update

# Vérifier les packages obsolètes
npm outdated

# Installer une version spécifique
npm install axios@1.6.0
```

### Nettoyage

```bash
# Supprimer un package
npm uninstall axios

# Nettoyer les dépendances inutilisées
npm prune

# Réinstaller tous les packages
rm -rf node_modules package-lock.json
npm install
```

---

## Ce qu'il faut retenir

### ✅ Points essentiels

1. **package.json est le cœur du projet**
   - Décrit tout ce dont le projet a besoin
   - Permet de recréer l'environnement sur n'importe quelle machine

2. **Deux types principaux de dépendances**
   - `dependencies` : Nécessaires en production
   - `devDependencies` : Uniquement pour le développement

3. **Les scripts automatisent les tâches**
   ```bash
   npm run dev     # Développement
   npm run build   # Production
   npm test        # Tests
   ```

4. **Le versionning est important**
   - `^1.2.3` : Accepte les mises à jour mineures (recommandé)
   - `~1.2.3` : Accepte uniquement les patches
   - `1.2.3` : Version exacte (production critique)

5. **À versionner dans Git**
   - ✅ package.json
   - ✅ package-lock.json
   - ❌ node_modules/

### 🎯 En pratique

Quand vous clonez un projet :
```bash
git clone https://github.com/user/projet.git
cd projet
npm install      # Installe tout depuis package.json
npm run dev      # Lance le projet
```

C'est aussi simple que ça ! Le fichier package.json contient tout ce qu'il faut savoir.

---

## FAQ - Questions fréquentes

**Q : Puis-je modifier package.json manuellement ?**
R : Oui pour les métadonnées (name, description, scripts...). Non pour les dépendances (utilisez npm install).

**Q : Que faire si package.json est corrompu ?**
R : Restaurez depuis Git, ou recréez-le avec `npm init` et réinstallez les dépendances.

**Q : Comment changer la version de mon projet ?**
R : Manuellement dans package.json, ou avec `npm version patch|minor|major`.

**Q : Quelle est la différence entre package.json et package-lock.json ?**
R : package.json liste les dépendances avec des versions flexibles. package-lock.json liste les versions EXACTES installées.

**Q : Faut-il commiter package-lock.json ?**
R : OUI ! C'est essentiel pour garantir que tout le monde a les mêmes versions.

**Q : Comment publier mon package sur npm ?**
R :
```bash
npm login
npm publish
```

**Q : Que signifie "private": true ?**
R : Empêche la publication accidentelle sur npm. Utilisé pour les applications (pas les bibliothèques).

```json
{
  "private": true
}
```

---


⏭️ [Build tools et bundlers](/08-ecosysteme-javascript-moderne/02-build-tools-bundlers/README.md)
