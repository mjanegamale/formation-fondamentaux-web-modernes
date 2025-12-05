🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.1.1 Node.js : JavaScript côté serveur 🆕

## Introduction

Jusqu'à présent, vous avez utilisé JavaScript uniquement dans le **navigateur web**. Mais une révolution s'est produite en 2009 : **Node.js** est né, permettant d'exécuter JavaScript **partout** - sur votre ordinateur, sur un serveur, dans des outils de développement, et bien plus encore.

Cette innovation a complètement transformé l'écosystème JavaScript et a ouvert la porte à tout ce que nous allons découvrir dans cette section.

---

## Qu'est-ce que Node.js ?

### Définition simple

**Node.js** est un **environnement d'exécution JavaScript** qui permet de faire tourner du code JavaScript en dehors du navigateur, directement sur votre machine (ordinateur, serveur, etc.).

### Analogie : JavaScript libéré du navigateur

Imaginez que JavaScript est un musicien talentueux :

**AVANT Node.js (depuis 1995)** 🎭
- JavaScript ne pouvait jouer (s'exécuter) **que dans un théâtre** (le navigateur)
- Impossible de jouer dans la rue, chez vous, ou ailleurs
- Limité aux interactions avec les pages web

**APRÈS Node.js (depuis 2009)** 🎸
- JavaScript peut maintenant jouer **partout** !
- Dans la rue (ligne de commande)
- Chez vous (applications de bureau)
- Dans des studios (serveurs web)
- Sur scène (applications mobiles)

---

## Pourquoi Node.js existe-t-il ?

### Le problème à résoudre

Avant Node.js, les développeurs devaient connaître :
- **JavaScript** pour le front-end (côté navigateur)
- **PHP, Python, Ruby, Java...** pour le back-end (côté serveur)

C'était comme devoir parler **deux langues différentes** pour construire un site web complet.

### La solution : un seul langage pour tout

Avec Node.js, vous pouvez utiliser **JavaScript partout** :

```
┌─────────────────────────────────────────┐
│         APPLICATION WEB COMPLÈTE        │
├─────────────────────────────────────────┤
│  FRONT-END (Navigateur)                 │
│  → JavaScript                           │
│  → HTML/CSS                             │
├─────────────────────────────────────────┤
│  BACK-END (Serveur)                     │
│  → JavaScript (grâce à Node.js) ✨      │
│  → Base de données                      │
└─────────────────────────────────────────┘
```

---

## Comment Node.js fonctionne ?

### Le moteur V8

Node.js utilise **V8**, le moteur JavaScript de Google Chrome. C'est le même moteur qui exécute JavaScript dans votre navigateur Chrome !

```
┌──────────────────────────────────────────┐
│         Navigateur Chrome                │
│  ┌────────────────────────────────┐      │
│  │     Moteur V8                  │      │
│  │  (exécute JavaScript)          │      │
│  └────────────────────────────────┘      │
└──────────────────────────────────────────┘

┌──────────────────────────────────────────┐
│           Node.js                        │
│  ┌────────────────────────────────┐      │
│  │     Moteur V8                  │      │
│  │  (exécute JavaScript)          │      │
│  │  + Accès aux fichiers          │      │
│  │  + Accès au réseau             │      │
│  │  + Autres fonctionnalités OS   │      │
│  └────────────────────────────────┘      │
└──────────────────────────────────────────┘
```

### La différence clé

| JavaScript dans le navigateur | JavaScript avec Node.js |
|-------------------------------|-------------------------|
| Accès au DOM (document, window) | ❌ Pas de DOM |
| Peut modifier des pages HTML | ❌ Pas de pages HTML |
| Limité par la sécurité du navigateur | ✅ Accès complet à l'ordinateur |
| Pas d'accès au système de fichiers | ✅ Peut lire/écrire des fichiers |
| Pas de connexion base de données directe | ✅ Peut se connecter aux bases de données |

---

## À quoi sert Node.js ?

### 1. Créer des serveurs web 🌐

Node.js permet de créer des serveurs web qui répondent aux requêtes HTTP.

**Exemple conceptuel :**
```javascript
// Serveur simple avec Node.js (pas besoin de comprendre tout maintenant)
const http = require('http');

const server = http.createServer((requete, reponse) => {
  reponse.write('Bonjour depuis Node.js !');
  reponse.end();
});

server.listen(3000);
console.log('Serveur démarré sur http://localhost:3000');
```

Ce code crée un serveur qui écoute sur le port 3000 et répond "Bonjour depuis Node.js !" à chaque requête.

### 2. Utiliser des outils de développement 🛠️

La plupart des outils modernes de développement web sont construits avec Node.js :

- **Vite** (bundler moderne) → fonctionne avec Node.js
- **Webpack** (bundler) → fonctionne avec Node.js
- **ESLint** (vérification de code) → fonctionne avec Node.js
- **Prettier** (formatage de code) → fonctionne avec Node.js

**Même si vous ne créez pas de serveur, vous utilisez Node.js pour vos outils de développement !**

### 3. Gérer les dépendances avec npm 📦

Node.js est livré avec **npm** (Node Package Manager), qui permet d'installer des milliers de bibliothèques JavaScript.

```bash
# Installer une bibliothèque (ex: lodash)
npm install lodash
```

### 4. Créer des scripts d'automatisation ⚙️

Node.js permet d'écrire des scripts pour automatiser des tâches :

```javascript
// Script qui renomme tous les fichiers d'un dossier
const fs = require('fs');

// Lire le contenu d'un dossier
const fichiers = fs.readdirSync('./images');

// Renommer chaque fichier
fichiers.forEach((fichier, index) => {
  fs.renameSync(
    `./images/${fichier}`,
    `./images/photo-${index + 1}.jpg`
  );
});

console.log('Fichiers renommés !');
```

### 5. Applications diverses

- **Applications de bureau** (avec Electron : VS Code, Slack, Discord)
- **Applications mobiles** (avec React Native)
- **APIs et microservices**
- **Outils en ligne de commande**

---

## Installation de Node.js

### Téléchargement

Rendez-vous sur [nodejs.org](https://nodejs.org) et téléchargez la version **LTS** (Long Term Support).

```
┌──────────────────────────────────────┐
│       nodejs.org                     │
├──────────────────────────────────────┤
│  ✅ Version LTS (ex: 20.x.x)         │
│     → Recommandée pour la plupart    │
│        des utilisateurs              │
│                                      │
│  🚀 Version Current (ex: 21.x.x)     │
│     → Dernières fonctionnalités      │
│     → Pour tester les nouveautés     │
└──────────────────────────────────────┘
```

**Conseil :** Choisissez toujours la version **LTS** pour commencer.

### Vérifier l'installation

Après installation, ouvrez un terminal et tapez :

```bash
node --version
# Devrait afficher : v20.x.x (ou similaire)

npm --version
# Devrait afficher : 10.x.x (ou similaire)
```

Si vous voyez des numéros de version, Node.js est correctement installé ! 🎉

---

## Premier contact avec Node.js

### 1. Exécuter du JavaScript dans le terminal

Créez un fichier `hello.js` :

```javascript
// hello.js
console.log('Bonjour depuis Node.js !');
console.log('JavaScript fonctionne en dehors du navigateur !');

const addition = 5 + 3;
console.log('5 + 3 =', addition);
```

Exécutez-le dans le terminal :

```bash
node hello.js
```

**Résultat :**
```
Bonjour depuis Node.js !
JavaScript fonctionne en dehors du navigateur !
5 + 3 = 8
```

### 2. Mode REPL (interactif)

Node.js possède un mode interactif appelé **REPL** (Read-Eval-Print-Loop) :

```bash
node
# Vous entrez dans le mode interactif
```

Vous pouvez maintenant taper du JavaScript directement :

```javascript
> 2 + 2
4
> const nom = "Alice"
undefined
> `Bonjour ${nom}`
'Bonjour Alice'
> .exit  // Pour quitter le mode REPL
```

---

## Différences importantes à connaître

### Pas de `window` ou `document`

Dans Node.js, il n'y a **pas de navigateur**, donc :

```javascript
// ❌ NE FONCTIONNE PAS dans Node.js
console.log(window);        // Erreur : window n'existe pas
document.getElementById('test'); // Erreur : document n'existe pas

// ✅ FONCTIONNE dans Node.js
console.log(process);       // Objet process disponible
console.log(__dirname);     // Dossier actuel
console.log(__filename);    // Fichier actuel
```

### Nouveaux objets globaux

Node.js fournit des objets spécifiques :

| Objet | Description |
|-------|-------------|
| `process` | Informations sur le processus en cours |
| `__dirname` | Chemin absolu du dossier courant |
| `__filename` | Chemin absolu du fichier courant |
| `global` | Équivalent de `window` (mais différent) |
| `require()` | Importer des modules (ancien système) |
| `module` | Informations sur le module actuel |

### Système de modules

Node.js utilise historiquement **CommonJS** pour les modules :

```javascript
// Ancien système (CommonJS)
const fs = require('fs');      // Importer
module.exports = maFonction;   // Exporter

// Nouveau système (ES Modules) - supporté depuis Node.js 14+
import fs from 'fs';           // Importer
export default maFonction;     // Exporter
```

Nous reviendrons sur les modules dans les sections suivantes.

---

## Cas d'usage concrets pour vous

### En tant que développeur front-end

Même si vous ne créez jamais de serveur avec Node.js, vous l'utiliserez pour :

1. **Installer des packages** avec npm
   ```bash
   npm install jquery
   npm install bootstrap
   ```

2. **Utiliser des outils de build** (Vite, Webpack)
   ```bash
   npm run dev
   npm run build
   ```

3. **Exécuter des linters** (ESLint)
   ```bash
   npm run lint
   ```

4. **Lancer des tests**
   ```bash
   npm test
   ```

### Exemple de workflow moderne

```bash
# 1. Créer un nouveau projet avec Vite
npm create vite@latest mon-projet

# 2. Installer les dépendances
cd mon-projet
npm install

# 3. Lancer le serveur de développement
npm run dev

# 4. Construire pour la production
npm run build
```

Tous ces outils fonctionnent grâce à Node.js !

---

## Concepts importants à retenir

### 1. Node.js ≠ Framework

Node.js n'est **pas** un framework comme React ou Vue. C'est un **environnement d'exécution** - une plateforme qui permet d'exécuter JavaScript.

```
Node.js → La scène de théâtre (la plateforme)
Express → Une pièce de théâtre (un framework pour Node.js)
React → Une autre pièce (un framework côté client)
```

### 2. JavaScript universel (Isomorphic/Universal JavaScript)

Avec Node.js, on peut écrire du code JavaScript qui fonctionne **à la fois** côté client et côté serveur :

```javascript
// Cette fonction fonctionne partout !
function addition(a, b) {
  return a + b;
}

// Navigateur ET Node.js
console.log(addition(5, 3)); // 8
```

### 3. Asynchrone par nature

Node.js est conçu pour être **non-bloquant** et **asynchrone** - parfait pour gérer plusieurs requêtes simultanées.

---

## Node.js dans l'industrie

### Entreprises utilisant Node.js

- **Netflix** - Streaming vidéo
- **PayPal** - Paiements en ligne
- **Uber** - Plateforme de transport
- **LinkedIn** - Réseau professionnel
- **NASA** - Oui, même la NASA !

### Pourquoi ils l'utilisent

1. **Performance** - Gestion efficace de nombreuses requêtes simultanées
2. **Rapidité de développement** - JavaScript partout
3. **Grande communauté** - Des millions de packages npm
4. **Scalabilité** - Facile de gérer la croissance

---

## Versions et évolution

### Node.js suit un cycle de releases

```
Version LTS (Long Term Support)
├── Support pendant 30 mois
├── Mises à jour de sécurité
└── Recommandée pour la production

Version Current
├── Nouvelles fonctionnalités
├── Support court (6 mois)
└── Pour tester les nouveautés
```

### Quelle version utiliser ?

- **Débutant** → Version LTS
- **Production** → Version LTS
- **Expérimentation** → Version Current

---

## Ressources complémentaires

### Documentation officielle

- [nodejs.org/docs](https://nodejs.org/docs) - Documentation complète
- [nodejs.org/api](https://nodejs.org/api) - API Reference

### Tutoriels recommandés

- **Node.js sur MDN** - Excellent point de départ
- **The Node.js Best Practices** - Bonnes pratiques
- **NodeSchool** - Tutoriels interactifs

---

## Ce qu'il faut retenir

### ✅ Points clés

1. **Node.js permet d'exécuter JavaScript en dehors du navigateur**
   - Sur votre ordinateur, sur des serveurs, partout !

2. **Vous utilisez déjà Node.js sans le savoir**
   - Tous les outils modernes (Vite, Webpack, ESLint) fonctionnent avec Node.js

3. **Node.js vient avec npm**
   - Le gestionnaire de packages que nous verrons dans la section suivante

4. **C'est la base de l'écosystème moderne**
   - Sans Node.js, pas d'outils modernes de développement front-end

5. **Vous n'avez pas besoin d'être expert**
   - En tant que développeur front-end, comprendre les bases suffit

### 🎯 Prochaine étape

Maintenant que vous comprenez ce qu'est Node.js, passons à **npm** - le gestionnaire de packages qui va révolutionner votre façon de travailler avec JavaScript.

---

## FAQ - Questions fréquentes

**Q : Dois-je apprendre Node.js pour faire du développement front-end ?**
R : Vous n'avez pas besoin d'être expert en Node.js pour faire du front-end, mais vous devez comprendre les bases car tous les outils modernes l'utilisent.

**Q : Node.js remplace-t-il JavaScript dans le navigateur ?**
R : Non ! Node.js est complémentaire. JavaScript dans le navigateur reste indispensable pour créer des interfaces utilisateur.

**Q : Quelle est la différence entre Node.js et npm ?**
R : Node.js est l'environnement d'exécution JavaScript. npm est le gestionnaire de packages qui est installé avec Node.js.

**Q : Dois-je apprendre à créer des serveurs avec Node.js ?**
R : Pas nécessairement pour débuter en front-end. Concentrez-vous d'abord sur l'utilisation de Node.js pour les outils de développement.

**Q : Express, c'est quoi ?**
R : Express est un framework web pour Node.js. C'est un outil qui facilite la création de serveurs web. Nous n'en aurons pas besoin dans cette formation front-end.

---


⏭️ [npm : gestionnaire de paquets](/08-ecosysteme-javascript-moderne/01-comprendre-ecosysteme/02-npm-gestionnaire-paquets.md)
