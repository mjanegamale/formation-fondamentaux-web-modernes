🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.2.2 Vite : le bundler moderne 🆕

## Introduction

Si vous avez déjà utilisé des outils comme Create React App ou Webpack, vous connaissez peut-être cette frustration : **attendre plusieurs secondes** (parfois minutes !) à chaque fois que vous démarrez votre serveur de développement ou que vous faites une modification.

**Vite** (prononcé "vite", comme le mot français) est arrivé en 2020 pour révolutionner cela. Son créateur, Evan You (également créateur de Vue.js), s'est dit : "Et si on pouvait avoir un outil de build **instantané** ?"

Le résultat ? Un outil ultra-rapide qui change complètement l'expérience de développement. ⚡

---

## Qu'est-ce que Vite ?

### Définition simple

**Vite** est un **outil de build** (build tool) moderne qui :
- ⚡ Démarre votre serveur de développement **instantanément**
- 🔥 Actualise vos modifications **en temps réel**
- 📦 Optimise votre code pour la production
- 🎯 Nécessite **très peu de configuration**

### Vite en chiffres

```
Temps de démarrage (projet moyen)
───────────────────────────────────

Webpack          : ~15-30 secondes
Create React App : ~10-20 secondes
Vite             : ~0.5-2 secondes ⚡

Mise à jour après modification
───────────────────────────────────

Webpack          : 1-3 secondes
Create React App : 1-2 secondes
Vite             : <100ms ⚡⚡⚡
```

**C'est 10 à 30 fois plus rapide !**

### Le nom "Vite"

Le mot "vite" en français signifie "rapide" - et c'est exactement ce que cet outil est ! 🇫🇷⚡

---

## Pourquoi Vite est si rapide ?

### Approche traditionnelle (Webpack, Create React App)

Les outils traditionnels fonctionnent comme ceci :

```
Au démarrage :
┌────────────────────────────────────────────┐
│  1. Lire TOUS les fichiers du projet       │
│     (peut être des milliers)               │
│          ↓                                 │
│  2. Transformer tout le code               │
│     (JSX → JS, TypeScript → JS, etc.)      │
│          ↓                                 │
│  3. Bundler tout ensemble                  │
│     (créer un gros fichier)                │
│          ↓                                 │
│  4. ENFIN démarrer le serveur              │
└────────────────────────────────────────────┘
     Temps total : 10-30 secondes 😴
```

**Problème :** Même si vous n'utilisez qu'une petite partie de votre app, l'outil traite TOUT.

### Approche moderne (Vite)

Vite utilise une approche radicalement différente :

```
Au démarrage :
┌────────────────────────────────────────────┐
│  1. Démarrer le serveur IMMÉDIATEMENT      │
│          ↓                                 │
│  2. Transformer uniquement les fichiers    │
│     demandés par le navigateur             │
│     (à la demande)                         │
└────────────────────────────────────────────┘
     Temps total : <1 seconde ⚡
```

**Analogie du restaurant :**

**Webpack/CRA** (approche traditionnelle) :
- 🍳 Le restaurant prépare **TOUS les plats** du menu avant d'ouvrir
- Vous commandez une salade
- Mais vous attendez que tout soit prêt
- **Temps d'attente : 1 heure**

**Vite** (approche moderne) :
- 🎯 Le restaurant ouvre immédiatement
- Vous commandez une salade
- Le chef prépare **uniquement votre salade**
- **Temps d'attente : 5 minutes**

### Technologies utilisées par Vite

Vite s'appuie sur deux technologies modernes :

**1. ES Modules natifs**
- Les navigateurs modernes comprennent nativement `import/export`
- Pas besoin de bundler en développement !

**2. esbuild**
- Un bundler écrit en Go (très rapide)
- 10-100x plus rapide que les bundlers JavaScript traditionnels

```
Langages de programmation (vitesse) :
────────────────────────────────────
JavaScript  : 🚗 (rapide)
Go         : 🚀 (très rapide)

esbuild est écrit en Go = ultra-rapide !
```

---

## Installation et premier projet

### Créer un nouveau projet avec Vite

C'est extrêmement simple :

```bash
# Créer un nouveau projet
npm create vite@latest mon-projet

# Vite vous pose quelques questions :
? Select a framework: ›
  ❯ Vanilla     # JavaScript pur
    Vue         # Vue.js
    React       # React
    Preact      # Preact
    Lit         # Lit
    Svelte      # Svelte
    Solid       # Solid
    Others      # Autres...

? Select a variant: ›
  ❯ JavaScript  # JavaScript standard
    TypeScript  # TypeScript
```

### Installation complète

```bash
# 1. Créer le projet
npm create vite@latest mon-premier-vite -- --template vanilla

# 2. Naviguer dans le dossier
cd mon-premier-vite

# 3. Installer les dépendances
npm install

# 4. Démarrer le serveur de développement
npm run dev
```

**Et voilà !** En moins de 30 secondes, vous avez un projet fonctionnel qui tourne sur `http://localhost:5173` 🎉

### Structure d'un projet Vite

```
mon-premier-vite/
├── node_modules/          # Dépendances (généré)
├── public/                # Fichiers statiques (favicon, etc.)
│   └── vite.svg
├── src/                   # Votre code source
│   ├── main.js           # Point d'entrée JavaScript
│   ├── style.css         # Styles
│   └── counter.js        # Module exemple
├── index.html            # Point d'entrée HTML
├── package.json          # Configuration npm
└── vite.config.js        # Configuration Vite (optionnel)
```

**Point important :** Le fichier `index.html` est **à la racine**, pas dans un dossier `public/`. C'est une particularité de Vite.

---

## Le fichier index.html

### Structure type

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>

    <!-- Point d'entrée JavaScript -->
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

### Points clés

**1. `type="module"` est essentiel**
```html
<script type="module" src="/src/main.js"></script>
```
- Permet d'utiliser `import/export` ES6
- Vite transforme automatiquement ce script

**2. Les chemins commencent par `/`**
```html
<script type="module" src="/src/main.js"></script>
<!-- Pas "./src/main.js" mais "/src/main.js" -->
```
- Le `/` représente la racine du projet
- Vite gère la résolution des chemins

**3. Pas de balise `<link>` pour le CSS**
```javascript
// Dans main.js
import './style.css';  // Le CSS est importé depuis JavaScript !
```
- Vite injecte automatiquement le CSS dans la page

---

## Les scripts npm avec Vite

### Scripts par défaut

Quand vous créez un projet Vite, le `package.json` contient :

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

### npm run dev - Développement

Lance le serveur de développement.

```bash
npm run dev
```

**Ce qui se passe :**
```
VITE v5.0.8  ready in 127 ms

➜  Local:   http://localhost:5173/
➜  Network: use --host to expose
➜  press h + enter to show help
```

**Fonctionnalités :**
- ⚡ Démarrage instantané
- 🔥 Hot Module Replacement (HMR)
- 🔍 Messages d'erreur clairs
- 📱 Accessible sur le réseau local

**Pendant que le serveur tourne :**
- Modifiez un fichier
- Sauvegardez (Ctrl+S)
- La page se met à jour **instantanément** sans se recharger complètement !

### npm run build - Production

Crée une version optimisée pour la production.

```bash
npm run build
```

**Ce qui se passe :**
```
vite v5.0.8 building for production...
✓ 34 modules transformed.
dist/index.html                   0.45 kB │ gzip:  0.30 kB
dist/assets/index-a1b2c3d4.css    1.23 kB │ gzip:  0.64 kB
dist/assets/index-e5f6g7h8.js    143.42 kB │ gzip: 46.13 kB
✓ built in 1.23s
```

**Résultat :** Un dossier `dist/` contenant votre application prête pour le déploiement.

```
dist/
├── index.html
├── assets/
│   ├── index-a1b2c3d4.css    # CSS minifié
│   └── index-e5f6g7h8.js     # JS minifié et optimisé
└── vite.svg
```

**Ce dossier `dist/` est ce que vous uploadez sur votre serveur.**

### npm run preview - Prévisualisation

Teste le build de production localement.

```bash
npm run build     # D'abord, créer le build
npm run preview   # Ensuite, le prévisualiser
```

**Utile pour :**
- Vérifier que le build fonctionne
- Tester les performances
- Debugger les problèmes de production

---

## Hot Module Replacement (HMR)

### Qu'est-ce que le HMR ?

Le **HMR** (Hot Module Replacement) est une fonctionnalité magique qui met à jour votre page **sans la recharger complètement**.

### Sans HMR (rechargement classique)

```
1. Vous modifiez le code
2. Vous sauvegardez
3. La page se recharge COMPLÈTEMENT
4. Vous perdez l'état de l'application
   (formulaires vidés, position perdue, etc.)
```

**Exemple frustrant :**
Vous testez un formulaire avec 10 champs. Vous modifiez le CSS d'un bouton. La page se recharge et vous devez **reremplir les 10 champs** ! 😤

### Avec HMR (Vite)

```
1. Vous modifiez le code
2. Vous sauvegardez
3. Seul le module modifié se met à jour
4. L'état de l'application est PRÉSERVÉ
   (formulaires remplis, position conservée)
```

**Même exemple avec Vite :**
Vous modifiez le CSS du bouton. **Seul le style change**, les 10 champs restent remplis ! 😊

### Types de HMR dans Vite

**1. CSS Hot Reload**
```css
/* Vous modifiez style.css */
.button {
  background: blue; /* Changement immédiat ! */
}
```
→ Le style se met à jour instantanément, sans recharger la page.

**2. JavaScript Hot Reload**
```javascript
// Vous modifiez counter.js
export function increment() {
  count++; // Mise à jour instantanée !
}
```
→ Le module se met à jour, l'état peut être préservé (selon le code).

**3. Vue/React Fast Refresh**
- Avec Vue ou React, Vite préserve l'état des composants
- Vous pouvez modifier un composant et voir le changement instantanément

---

## Configuration de Vite

### Configuration par défaut

Vite fonctionne **sans configuration** ! C'est sa force.

Mais si besoin, vous pouvez créer un fichier `vite.config.js` :

```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  // Votre configuration ici
});
```

### Configurations courantes

#### Changer le port

Par défaut, Vite utilise le port 5173.

```javascript
// vite.config.js
export default defineConfig({
  server: {
    port: 3000  // Utiliser le port 3000 à la place
  }
});
```

#### Ouvrir le navigateur automatiquement

```javascript
export default defineConfig({
  server: {
    open: true  // Ouvre le navigateur au démarrage
  }
});
```

#### Configurer un proxy (API)

Si votre API backend tourne sur un autre port :

```javascript
export default defineConfig({
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:3001',
        changeOrigin: true
      }
    }
  }
});
```

**Utilisation :**
```javascript
// Votre code fait une requête à /api/users
fetch('/api/users')

// Vite redirige automatiquement vers http://localhost:3001/api/users
```

#### Alias de chemins

Créer des raccourcis pour les imports :

```javascript
import path from 'path';

export default defineConfig({
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
      '@components': path.resolve(__dirname, './src/components')
    }
  }
});
```

**Utilisation :**
```javascript
// Au lieu de :
import Button from '../../../components/Button.js';

// Vous écrivez :
import Button from '@components/Button.js';
```

#### Configuration pour React

```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()]
});
```

#### Configuration pour Vue

```javascript
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
  plugins: [vue()]
});
```

---

## Variables d'environnement

### Créer des fichiers .env

Vite supporte nativement les variables d'environnement.

**Fichiers possibles :**
```
.env                # Dans tous les environnements
.env.local          # Local, non versionné
.env.development    # En développement uniquement
.env.production     # En production uniquement
```

**Exemple de fichier `.env` :**
```bash
# .env
VITE_API_URL=https://api.monapp.com
VITE_APP_TITLE=Mon Application
VITE_ENABLE_DEBUG=true
```

**⚠️ Important :** Les variables doivent commencer par `VITE_` pour être exposées au client.

### Utiliser les variables

```javascript
// Dans votre code JavaScript
const apiUrl = import.meta.env.VITE_API_URL;
const appTitle = import.meta.env.VITE_APP_TITLE;
const isDebug = import.meta.env.VITE_ENABLE_DEBUG === 'true';

console.log(apiUrl); // "https://api.monapp.com"
```

### Variables intégrées

Vite fournit aussi des variables par défaut :

```javascript
import.meta.env.MODE        // 'development' ou 'production'
import.meta.env.BASE_URL    // Base URL de l'app
import.meta.env.PROD        // true en production
import.meta.env.DEV         // true en développement
import.meta.env.SSR         // true si Server-Side Rendering
```

**Utilisation pratique :**
```javascript
if (import.meta.env.DEV) {
  console.log('Mode développement');
  // Afficher des logs de debug
}

if (import.meta.env.PROD) {
  console.log('Mode production');
  // Désactiver les logs
}
```

---

## Importer des ressources

### Importer du CSS

```javascript
// main.js
import './style.css';           // CSS global
import './components/button.css'; // CSS spécifique
```

Vite :
- ✅ Injecte automatiquement le CSS dans la page
- ✅ Applique le HMR (mise à jour instantanée)
- ✅ Minifie en production

### Importer des images

```javascript
// Importer comme module
import logo from './assets/logo.png';

// Utiliser dans le HTML
const img = document.createElement('img');
img.src = logo; // URL optimisée automatiquement
```

**En React :**
```jsx
import logo from './assets/logo.png';

function App() {
  return <img src={logo} alt="Logo" />;
}
```

### Importer du JSON

```javascript
import config from './config.json';

console.log(config.apiUrl);
```

### Importer des fichiers texte

```javascript
import readme from './README.md?raw';

console.log(readme); // Contenu du fichier en texte brut
```

### Importer dynamiquement

```javascript
// Import dynamique (lazy loading)
const loadModule = async () => {
  const module = await import('./heavy-module.js');
  module.doSomething();
};

// Le module n'est chargé que quand la fonction est appelée
```

---

## Build de production

### Optimisations automatiques

Quand vous faites `npm run build`, Vite :

**1. Minification**
```javascript
// Votre code
function calculateSum(a, b) {
  return a + b;
}

// Code minifié
function c(a,b){return a+b}
```

**2. Tree Shaking**
```javascript
// Vous importez
import { add } from './utils.js';

// Seule la fonction add est incluse dans le build
// Les autres fonctions de utils.js sont supprimées
```

**3. Code Splitting**
```javascript
// Routes lazy-loaded
const Home = () => import('./pages/Home.jsx');
const About = () => import('./pages/About.jsx');

// Résultat : plusieurs petits fichiers au lieu d'un gros
```

**4. CSS Optimization**
- Minification du CSS
- Suppression du CSS inutilisé
- Extraction dans des fichiers séparés

**5. Asset Optimization**
- Images optimisées
- Noms de fichiers avec hash (cache busting)
- Compression

### Cache Busting

Vite ajoute automatiquement un hash aux noms de fichiers :

```
assets/index-a1b2c3d4.js
assets/style-e5f6g7h8.css
```

**Avantage :** Quand vous mettez à jour votre site, les navigateurs téléchargent les nouveaux fichiers (le hash change).

### Source Maps

En production, Vite peut générer des source maps pour le debug :

```javascript
// vite.config.js
export default defineConfig({
  build: {
    sourcemap: true  // Générer les source maps
  }
});
```

**Source maps** = fichiers qui permettent de voir votre code original dans les DevTools même s'il est minifié.

---

## Vite vs autres outils

### Vite vs Create React App (CRA)

| Critère | Vite | Create React App |
|---------|------|-----------------|
| **Vitesse dev** | ⚡⚡⚡ Instantané | 🐌 10-30s |
| **HMR** | ⚡⚡⚡ <100ms | 🐌 1-3s |
| **Build production** | ⚡⚡ Rapide | 🐌 Lent |
| **Configuration** | 🎯 Simple | 🔒 Éjection nécessaire |
| **Taille** | 📦 Légère | 📦📦 Lourde |
| **Technologie** | 🆕 Moderne | 🕰️ Ancien |
| **Maintenance** | ✅ Active | ⚠️ Déprécié (2023) |

**Verdict :** Vite est supérieur sur tous les points. CRA n'est plus maintenu.

### Vite vs Webpack

| Critère | Vite | Webpack |
|---------|------|---------|
| **Courbe d'apprentissage** | 🟢 Facile | 🔴 Difficile |
| **Configuration** | 📝 Minimale | 📚 Complexe |
| **Vitesse** | ⚡⚡⚡ Très rapide | 🐌 Lent |
| **Écosystème** | 🌱 Croissant | 🌳 Mature |
| **Flexibilité** | 🎯 Bonnes bases | 🔧 Extrême |

**Verdict :**
- **Débutants et projets modernes** → Vite
- **Projets complexes existants avec besoins très spécifiques** → Webpack

### Vite vs Parcel

| Critère | Vite | Parcel |
|---------|------|--------|
| **Vitesse** | ⚡⚡⚡ Très rapide | ⚡⚡ Rapide |
| **Configuration** | 📝 Minimale | 🎁 Zéro config |
| **Popularité** | 📈 En forte croissance | 📊 Moyenne |
| **Écosystème** | 🌱 Plugins nombreux | 🌿 Plugins limités |

**Verdict :** Vite est devenu plus populaire et plus rapide.

---

## Plugins Vite essentiels

### Plugin React

```bash
npm install -D @vitejs/plugin-react
```

```javascript
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()]
});
```

### Plugin Vue

```bash
npm install -D @vitejs/plugin-vue
```

```javascript
import vue from '@vitejs/plugin-vue';

export default defineConfig({
  plugins: [vue()]
});
```

### Plugin PWA

Pour transformer votre app en Progressive Web App :

```bash
npm install -D vite-plugin-pwa
```

```javascript
import { VitePWA } from 'vite-plugin-pwa';

export default defineConfig({
  plugins: [
    VitePWA({
      registerType: 'autoUpdate',
      manifest: {
        name: 'Mon Application',
        short_name: 'MonApp',
        description: 'Une super application',
        theme_color: '#ffffff'
      }
    })
  ]
});
```

### Plugin de compression

Compresser les fichiers en gzip :

```bash
npm install -D vite-plugin-compression
```

```javascript
import compression from 'vite-plugin-compression';

export default defineConfig({
  plugins: [compression()]
});
```

---

## Cas d'usage pratiques

### Projet React avec Vite

```bash
# Créer le projet
npm create vite@latest mon-app-react -- --template react

# Installer et lancer
cd mon-app-react
npm install
npm run dev
```

### Projet Vue avec Vite

```bash
npm create vite@latest mon-app-vue -- --template vue
cd mon-app-vue
npm install
npm run dev
```

### Projet TypeScript

```bash
npm create vite@latest mon-app-ts -- --template vanilla-ts
cd mon-app-ts
npm install
npm run dev
```

### Projet avec TailwindCSS

```bash
# Créer le projet
npm create vite@latest mon-app

# Installer Tailwind
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Configurer tailwind.config.js
# content: ["./index.html", "./src/**/*.{js,jsx}"]

# Ajouter à votre CSS
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## Déploiement

### Build pour la production

```bash
npm run build
```

Résultat : dossier `dist/` prêt pour le déploiement.

### Déployer sur Vercel

```bash
# Installer Vercel CLI
npm install -g vercel

# Déployer
vercel
```

### Déployer sur Netlify

1. Connectez votre repo GitHub
2. Configuration build :
   - Build command: `npm run build`
   - Publish directory: `dist`

### Déployer sur GitHub Pages

```bash
# Installer gh-pages
npm install -D gh-pages

# Ajouter dans package.json
"scripts": {
  "deploy": "npm run build && gh-pages -d dist"
}

# Déployer
npm run deploy
```

**Configuration vite.config.js pour GitHub Pages :**
```javascript
export default defineConfig({
  base: '/nom-du-repo/'  // Important pour GitHub Pages
});
```

---

## Troubleshooting (Résolution de problèmes)

### Erreur: "Port already in use"

Le port 5173 est déjà utilisé.

**Solution :**
```javascript
// vite.config.js
export default defineConfig({
  server: {
    port: 3000  // Changer le port
  }
});
```

### Erreur: Module not found

```
Error: Cannot find module './Component'
```

**Causes possibles :**
1. Chemin d'import incorrect
2. Extension de fichier manquante
3. Casse incorrecte (Component.jsx vs component.jsx)

**Solution :**
```javascript
// ❌ Mauvais
import Button from './components/button';

// ✅ Correct
import Button from './components/Button.jsx';
```

### HMR ne fonctionne pas

**Solutions :**
1. Redémarrer le serveur : Ctrl+C puis `npm run dev`
2. Vider le cache : `rm -rf node_modules/.vite`
3. Vérifier les erreurs dans la console

### Build échoue

```bash
# Nettoyer et réinstaller
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Import de CSS ne fonctionne pas

Vérifiez que vous importez bien le CSS :

```javascript
// ✅ Correct
import './style.css';

// ❌ Incorrect (syntax HTML)
<link rel="stylesheet" href="./style.css">
```

---

## Bonnes pratiques avec Vite

### ✅ À faire

1. **Utiliser les imports ES6**
```javascript
import { function } from './module.js';
```

2. **Préfixer les variables d'environnement**
```bash
VITE_API_URL=...  # ✅
API_URL=...       # ❌ (non accessible)
```

3. **Organiser le code par fonctionnalité**
```
src/
├── components/
├── utils/
├── pages/
└── assets/
```

4. **Utiliser le lazy loading pour les routes**
```javascript
const About = () => import('./pages/About.jsx');
```

5. **Versionner vite.config.js**
```bash
git add vite.config.js
```

### ❌ À éviter

1. **Ne pas importer de gros fichiers inutilement**
```javascript
// ❌ Import toute la bibliothèque
import _ from 'lodash';

// ✅ Import uniquement ce dont vous avez besoin
import { debounce } from 'lodash-es';
```

2. **Ne pas oublier le préfixe VITE_ pour les variables**

3. **Ne pas commettre .env avec des secrets**
```gitignore
# .gitignore
.env.local
.env.*.local
```

4. **Ne pas ignorer les warnings du build**

5. **Ne pas utiliser des chemins absolus sans alias**
```javascript
// ❌ Difficile à maintenir
import Button from '../../../components/Button.jsx';

// ✅ Avec alias
import Button from '@/components/Button.jsx';
```

---

## Ce qu'il faut retenir

### ✅ Points essentiels

1. **Vite est ultra-rapide**
   - Démarrage instantané (<1s)
   - HMR en moins de 100ms
   - 10-30x plus rapide que les outils traditionnels

2. **Vite est simple**
   - Fonctionne sans configuration
   - Installation en 3 commandes
   - Courbe d'apprentissage faible

3. **Vite est moderne**
   - Utilise les ES Modules natifs
   - Supporte TypeScript, JSX, Vue, React...
   - Optimisations automatiques

4. **Workflow de base**
   ```bash
   npm create vite@latest    # Créer
   npm install               # Installer
   npm run dev               # Développer
   npm run build             # Produire
   ```

5. **Vite est l'avenir**
   - Create React App est déprécié
   - Vite est recommandé officiellement par React et Vue
   - Communauté en forte croissance

### 🎯 Prochaine étape

Vous savez maintenant utiliser Vite ! Dans la section suivante, nous découvrirons **Webpack** - l'ancien standard de l'industrie que vous rencontrerez dans les projets existants.

---

## FAQ - Questions fréquentes

**Q : Vite remplace-t-il npm ?**
R : Non ! Vite est un build tool, npm est un gestionnaire de paquets. Vous utilisez les deux ensemble.

**Q : Puis-je utiliser Vite sans framework ?**
R : Oui ! Avec le template `vanilla` : `npm create vite@latest -- --template vanilla`

**Q : Vite fonctionne-t-il avec tous les navigateurs ?**
R : En développement, il faut un navigateur moderne. En production, le code est compatible avec les vieux navigateurs.

**Q : Dois-je apprendre Webpack si j'utilise Vite ?**
R : Non pour un nouveau projet. Oui si vous devez maintenir un vieux projet Webpack.

**Q : Vite est-il stable pour la production ?**
R : Oui ! Des milliers de sites l'utilisent en production (Notion, Cloudflare, etc.)

**Q : Comment migrer de CRA vers Vite ?**
R : Il existe des guides de migration, mais pour un nouveau projet, commencez directement avec Vite.

**Q : Vite coûte-t-il quelque chose ?**
R : Non, c'est 100% gratuit et open-source !

---


⏭️ [Webpack : aperçu (legacy mais important)](/08-ecosysteme-javascript-moderne/02-build-tools-bundlers/03-webpack-apercu.md)
