🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.3.2 - ESLint pour JavaScript

## Introduction

**ESLint** est un outil d'analyse statique de code JavaScript qui détecte les erreurs, les problèmes de style et les mauvaises pratiques dans votre code **avant même de l'exécuter**. C'est comme un correcteur orthographique et grammatical, mais pour le code !

### Qu'est-ce que l'analyse statique ?

L'**analyse statique** signifie que ESLint examine votre code sans l'exécuter. Il lit simplement vos fichiers JavaScript et cherche :
- ✅ Les erreurs de syntaxe
- ✅ Les variables non utilisées
- ✅ Les problèmes de style (espaces, indentation, etc.)
- ✅ Les pratiques déconseillées
- ✅ Les bugs potentiels

### Pourquoi utiliser ESLint ?

1. **Détecter les erreurs tôt** : Trouvez les problèmes avant de lancer votre code
2. **Améliorer la qualité** : Adoptez les bonnes pratiques JavaScript
3. **Uniformiser le code** : Maintenez un style cohérent dans tout le projet
4. **Apprendre** : ESLint vous enseigne les bonnes pratiques en les suggérant
5. **Gagner du temps** : Moins de bugs = moins de débogage

> 💡 **Analogie** : ESLint est comme un professeur qui relit vos devoirs et vous signale les fautes avant de les rendre. C'est toujours mieux de corriger les erreurs avant que quelqu'un d'autre ne les découvre !

---

## Installation d'ESLint

### Prérequis : Node.js et npm

ESLint nécessite **Node.js** (qui inclut npm, le gestionnaire de paquets).

**Vérifier si Node.js est installé** :
```bash
node --version
```

Si vous voyez un numéro de version (ex: `v18.17.0`), Node.js est installé. Sinon, téléchargez-le sur https://nodejs.org/

### Méthode 1 : Installation globale (Simple pour débuter)

Cette méthode installe ESLint une seule fois sur votre ordinateur, utilisable pour tous vos projets.

**Commande** :
```bash
npm install -g eslint
```

**Vérifier l'installation** :
```bash
eslint --version
```

**Avantages** :
- ✅ Installation unique
- ✅ Disponible partout
- ✅ Simple pour les débutants

**Inconvénients** :
- ⚠️ Même version pour tous les projets
- ⚠️ Peut créer des conflits dans des équipes

### Méthode 2 : Installation locale (Recommandée pour les projets)

Cette méthode installe ESLint dans un projet spécifique.

**Étapes** :

1. **Créer un projet npm** (si pas déjà fait) :
```bash
npm init -y
```

Cela crée un fichier `package.json` dans votre dossier.

2. **Installer ESLint** :
```bash
npm install eslint --save-dev
```

Le `--save-dev` indique que ESLint est un outil de développement.

**Avantages** :
- ✅ Version spécifique au projet
- ✅ Partageable avec l'équipe
- ✅ Configuration indépendante par projet

---

## Configuration d'ESLint

### Initialisation rapide

ESLint propose un assistant de configuration interactif :

```bash
npx eslint --init
```

ou si installé globalement :

```bash
eslint --init
```

### Questions de l'assistant

L'assistant vous posera plusieurs questions. Voici les réponses recommandées pour débuter :

#### 1. How would you like to use ESLint?
**Choix recommandé** : `To check syntax, find problems, and enforce code style`

Cela active toutes les fonctionnalités d'ESLint.

#### 2. What type of modules does your project use?
**Choix** :
- `JavaScript modules (import/export)` → Si vous utilisez des modules ES6
- `CommonJS (require/exports)` → Si vous utilisez Node.js classique
- `None of these` → Si vous n'utilisez pas de modules

**Pour débuter** : Choisissez `JavaScript modules (import/export)`

#### 3. Which framework does your project use?
**Choix** :
- `React` → Si vous faites du React
- `Vue.js` → Si vous faites du Vue
- `None of these` → Pour du JavaScript vanilla

**Pour débuter** : Choisissez `None of these`

#### 4. Does your project use TypeScript?
**Choix** : `No` (sauf si vous utilisez TypeScript)

#### 5. Where does your code run?
**Choix** :
- `Browser` → Pour du JavaScript qui s'exécute dans le navigateur
- `Node` → Pour du JavaScript côté serveur

**Pour débuter** : Cochez `Browser` (utilisez la barre d'espace pour cocher)

#### 6. How would you like to define a style for your project?
**Choix recommandé** : `Use a popular style guide`

Cela vous permet d'utiliser des configurations pré-établies par la communauté.

#### 7. Which style guide do you want to follow?
**Choix recommandé** : `Standard` ou `Airbnb`

- **Standard** : Moins strict, bon pour débuter
- **Airbnb** : Plus strict, très populaire dans l'industrie

#### 8. What format do you want your config file to be in?
**Choix recommandé** : `JavaScript`

Les autres options (YAML, JSON) fonctionnent aussi, mais JavaScript est le plus flexible.

#### 9. Installation des dépendances
ESLint vous demandera d'installer les dépendances nécessaires. Répondez `Yes`.

### Fichier de configuration généré

Après l'assistant, un fichier `.eslintrc.js` (ou `.eslintrc.json`) est créé :

**Exemple de `.eslintrc.js`** :
```javascript
module.exports = {
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": "standard",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
  }
}
```

---

## Utilisation d'ESLint

### En ligne de commande

#### Analyser un fichier
```bash
eslint monFichier.js
```

#### Analyser tous les fichiers JS d'un dossier
```bash
eslint src/
```

#### Analyser avec correction automatique
```bash
eslint monFichier.js --fix
```

Le flag `--fix` corrige automatiquement les problèmes simples (espaces, virgules, etc.).

### Dans VS Code (Recommandé)

#### Installation de l'extension ESLint

1. Ouvrez VS Code
2. Allez dans Extensions (Ctrl+Shift+X)
3. Recherchez "ESLint"
4. Installez l'extension officielle "ESLint" par Microsoft

#### Configuration dans VS Code

Une fois l'extension installée :

**Avantages** :
- ✅ Les erreurs apparaissent directement dans l'éditeur (soulignements rouges/jaunes)
- ✅ Correction automatique à la sauvegarde (optionnel)
- ✅ Suggestions de correction en temps réel

**Activer la correction automatique à la sauvegarde** :

1. Ouvrez les paramètres VS Code (Ctrl+,)
2. Cherchez "eslint"
3. Cochez "ESLint: Auto Fix On Save" ou ajoutez dans `settings.json` :

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

---

## Comprendre les messages d'ESLint

### Structure d'un message d'erreur

Quand ESLint détecte un problème, il affiche :

```
/chemin/vers/fichier.js
  5:10  error    'utilisateur' is defined but never used  no-unused-vars
  8:1   warning  Unexpected console statement             no-console
```

**Décomposition** :
- `5:10` → Ligne 5, colonne 10
- `error` ou `warning` → Niveau de gravité
- Message descriptif → Explication du problème
- `no-unused-vars` → Nom de la règle ESLint concernée

### Niveaux de gravité

ESLint utilise trois niveaux :

| Niveau | Symbole | Signification |
|--------|---------|---------------|
| **off** (0) | - | La règle est désactivée |
| **warn** (1) | ⚠️ | Avertissement (n'empêche pas l'exécution) |
| **error** (2) | ❌ | Erreur (doit être corrigée) |

---

## Règles ESLint courantes

### Règles de base

#### 1. `no-unused-vars` - Variables non utilisées

**Problème** :
```javascript
const nom = 'Jean';  // ❌ Erreur : variable déclarée mais jamais utilisée
const age = 25;
console.log(age);
```

**Solution** :
```javascript
const age = 25;  // ✅ Correct
console.log(age);
```

**Pourquoi** : Les variables inutilisées encombrent le code et peuvent indiquer une erreur logique.

---

#### 2. `no-undef` - Variables non définies

**Problème** :
```javascript
console.log(utilisateur);  // ❌ Erreur : 'utilisateur' n'est pas défini
```

**Solution** :
```javascript
const utilisateur = 'Jean';  // ✅ Définir la variable d'abord
console.log(utilisateur);
```

**Pourquoi** : Utiliser une variable non définie cause une erreur d'exécution.

---

#### 3. `no-console` - Utilisation de console

**Problème** :
```javascript
console.log('Debug');  // ⚠️ Avertissement
```

**Pourquoi** : Les `console.log` sont utiles en développement mais doivent être retirés en production.

**Solutions** :
1. Retirer les console.log avant la mise en production
2. Utiliser des outils de logging appropriés
3. Désactiver la règle pour le développement (voir section Configuration)

---

#### 4. `semi` - Points-virgules

**Problème** (avec règle activée) :
```javascript
const nom = 'Jean'  // ❌ Point-virgule manquant
```

**Solution** :
```javascript
const nom = 'Jean';  // ✅ Correct
```

**Note** : Certains styles (comme Standard) n'utilisent PAS de points-virgules. Cela dépend de votre configuration.

---

#### 5. `quotes` - Type de guillemets

**Configuration possible** : `"quotes": ["error", "single"]`

**Problème** :
```javascript
const nom = "Jean";  // ❌ Utilise des guillemets doubles
```

**Solution** :
```javascript
const nom = 'Jean';  // ✅ Utilise des guillemets simples
```

**Note** : Le choix entre `'` et `"` est une question de style. L'important est d'être cohérent.

---

#### 6. `eqeqeq` - Égalité stricte

**Problème** :
```javascript
if (age == 25) {  // ❌ Utilise == au lieu de ===
  console.log('25 ans');
}
```

**Solution** :
```javascript
if (age === 25) {  // ✅ Utilise === (égalité stricte)
  console.log('25 ans');
}
```

**Pourquoi** : `===` évite les conversions de type implicites et les bugs associés.

---

#### 7. `no-var` - Interdire var

**Problème** :
```javascript
var nom = 'Jean';  // ❌ var est déconseillé
```

**Solution** :
```javascript
const nom = 'Jean';  // ✅ Utiliser const ou let
```

**Pourquoi** : `const` et `let` ont une portée de bloc plus prévisible que `var`.

---

#### 8. `prefer-const` - Préférer const

**Problème** :
```javascript
let nom = 'Jean';  // ⚠️ Variable jamais réassignée
console.log(nom);
```

**Solution** :
```javascript
const nom = 'Jean';  // ✅ Utiliser const si la valeur ne change pas
console.log(nom);
```

**Pourquoi** : `const` indique clairement que la valeur ne sera pas modifiée.

---

#### 9. `indent` - Indentation

**Configuration** : `"indent": ["error", 2]` (2 espaces)

**Problème** :
```javascript
function saluer() {
console.log('Bonjour');  // ❌ Pas d'indentation
}
```

**Solution** :
```javascript
function saluer() {
  console.log('Bonjour');  // ✅ Indenté avec 2 espaces
}
```

---

#### 10. `space-before-function-paren` - Espace avant les parenthèses

**Problème** :
```javascript
function saluer() {  // ⚠️ Selon configuration
  console.log('Bonjour');
}
```

**Cela dépend du style guide choisi**. Certains requièrent un espace, d'autres non.

---

## Configuration des règles

### Modifier les règles dans `.eslintrc.js`

Vous pouvez personnaliser les règles dans la section `"rules"` :

```javascript
module.exports = {
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": "standard",
  "rules": {
    // Désactiver une règle
    "no-console": "off",

    // Passer en warning au lieu d'error
    "no-unused-vars": "warn",

    // Configurer une règle avec options
    "quotes": ["error", "single"],
    "indent": ["error", 2],

    // Activer une règle désactivée par défaut
    "eqeqeq": "error"
  }
}
```

### Format des règles

```javascript
"nom-de-la-regle": "off" | "warn" | "error"
```

ou avec options :

```javascript
"nom-de-la-regle": ["error", option1, option2]
```

**Exemples** :
```javascript
"quotes": ["error", "single"]  // Guillemets simples obligatoires
"indent": ["error", 2]         // Indentation de 2 espaces
"semi": ["error", "always"]    // Points-virgules obligatoires
```

---

## Ignorer des fichiers ou lignes

### Ignorer des fichiers entiers

Créez un fichier `.eslintignore` à la racine de votre projet :

```
# Fichiers à ignorer
node_modules/
dist/
build/
*.min.js
vendor/
```

**Similaire à `.gitignore`** : Chaque ligne représente un pattern de fichiers à ignorer.

### Ignorer une ligne spécifique

**Ignorer la ligne suivante** :
```javascript
// eslint-disable-next-line
console.log('Ce console.log ne sera pas signalé');
```

**Ignorer une règle spécifique** :
```javascript
// eslint-disable-next-line no-console
console.log('Seule la règle no-console est ignorée ici');
```

### Ignorer une section de code

**Désactiver temporairement ESLint** :
```javascript
/* eslint-disable */
console.log('ESLint est désactivé ici');
var ancien = 'code legacy';
/* eslint-enable */
```

**Désactiver une règle spécifique** :
```javascript
/* eslint-disable no-console */
console.log('Debug 1');
console.log('Debug 2');
/* eslint-enable no-console */
```

**⚠️ Attention** : N'abusez pas des commentaires d'ignore. Si vous devez ignorer beaucoup de règles, questionnez-vous sur votre code ou votre configuration ESLint.

---

## Styles guides populaires

### 1. Standard

**Installation** :
```bash
npm install --save-dev eslint-config-standard
```

**Configuration** :
```javascript
{
  "extends": "standard"
}
```

**Caractéristiques** :
- ✅ Pas de points-virgules
- ✅ 2 espaces d'indentation
- ✅ Guillemets simples
- ✅ Espace avant les parenthèses de fonction

**Avantages** :
- Simple et permissif
- Bon pour débuter
- Configuration minimale

---

### 2. Airbnb

**Installation** :
```bash
npm install --save-dev eslint-config-airbnb-base
```

**Configuration** :
```javascript
{
  "extends": "airbnb-base"
}
```

**Caractéristiques** :
- ✅ Points-virgules obligatoires
- ✅ 2 espaces d'indentation
- ✅ Guillemets simples
- ✅ Règles strictes

**Avantages** :
- Très populaire dans l'industrie
- Encourage les meilleures pratiques
- Documentation complète

**Inconvénients** :
- Peut sembler strict pour les débutants
- Plus d'erreurs à corriger au début

---

### 3. Google

**Installation** :
```bash
npm install --save-dev eslint-config-google
```

**Configuration** :
```javascript
{
  "extends": "google"
}
```

**Caractéristiques** :
- ✅ Points-virgules obligatoires
- ✅ 2 espaces d'indentation
- ✅ Guillemets simples

---

## ESLint et les éditeurs

### Intégration avec d'autres éditeurs

#### Sublime Text
Extension : `SublimeLinter-eslint`

#### Atom
Extension : `linter-eslint`

#### WebStorm / IntelliJ
ESLint intégré nativement. À activer dans :
`Preferences > Languages & Frameworks > JavaScript > Code Quality Tools > ESLint`

---

## Commandes utiles

### Analyser tout le projet
```bash
eslint .
```

### Analyser et corriger automatiquement
```bash
eslint . --fix
```

### Analyser un type de fichier spécifique
```bash
eslint "src/**/*.js"
```

### Voir la configuration actuelle
```bash
eslint --print-config fichier.js
```

### Créer un rapport HTML
```bash
eslint . -f html -o rapport.html
```

---

## Intégration dans package.json

Ajoutez des scripts dans votre `package.json` pour faciliter l'utilisation :

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "lint:report": "eslint . -f html -o eslint-report.html"
  }
}
```

**Utilisation** :
```bash
npm run lint        # Analyser le code
npm run lint:fix    # Analyser et corriger
npm run lint:report # Générer un rapport
```

---

## Dépannage

### Problème : ESLint ne fonctionne pas dans VS Code

**Solutions** :
1. Vérifiez que l'extension ESLint est installée
2. Rechargez la fenêtre VS Code (Ctrl+Shift+P > "Reload Window")
3. Vérifiez que le fichier `.eslintrc.js` existe à la racine du projet
4. Regardez la console de sortie ESLint (View > Output > ESLint)

### Problème : Trop d'erreurs

**Solutions** :
1. Corrigez les erreurs une par une, en commençant par les premières
2. Utilisez `--fix` pour corriger automatiquement les problèmes simples
3. Ajustez les règles dans `.eslintrc.js` pour être moins strict au début
4. Ignorez temporairement les fichiers legacy avec `.eslintignore`

### Problème : Conflit entre ESLint et Prettier

Si vous utilisez **Prettier** (formateur de code) en plus d'ESLint :

**Installation** :
```bash
npm install --save-dev eslint-config-prettier
```

**Configuration** :
```javascript
{
  "extends": ["standard", "prettier"]
}
```

Cela désactive les règles ESLint qui entrent en conflit avec Prettier.

---

## Bonnes pratiques

### 1. Commencer avec un style guide populaire

Ne créez pas votre propre configuration au début :
- ✅ Utilisez Standard ou Airbnb
- ✅ Apprenez les conventions
- ✅ Personnalisez progressivement

### 2. Corriger régulièrement

N'attendez pas d'avoir 1000 erreurs :
- ✅ Lancez ESLint après chaque fonctionnalité
- ✅ Activez la correction automatique dans VS Code
- ✅ Intégrez ESLint dans votre workflow

### 3. Comprendre avant de désactiver

Avant de désactiver une règle :
- ✅ Comprenez pourquoi elle existe
- ✅ Cherchez la bonne façon de corriger
- ✅ Désactivez en dernier recours

### 4. Collaborer avec l'équipe

Si vous travaillez en équipe :
- ✅ Partagez le fichier `.eslintrc.js` via Git
- ✅ Documentez les règles personnalisées
- ✅ Discutez des modifications de configuration

### 5. Ne pas sur-optimiser

ESLint est un outil, pas une fin en soi :
- ✅ Concentrez-vous sur les erreurs critiques
- ✅ Les warnings peuvent être corrigés progressivement
- ✅ Le code qui fonctionne > le code parfait

---

## Exemple de configuration complète

Voici une configuration recommandée pour débuter :

```javascript
module.exports = {
  // Environnement d'exécution
  env: {
    browser: true,      // Code qui tourne dans le navigateur
    es2021: true,       // Fonctionnalités ES2021
    node: true          // Si vous utilisez Node.js
  },

  // Style guide de base
  extends: [
    'standard'          // Ou 'airbnb-base'
  ],

  // Configuration du parseur
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module'
  },

  // Règles personnalisées
  rules: {
    // Permettre console.log en développement
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'warn',

    // Avertissement pour les variables non utilisées
    'no-unused-vars': 'warn',

    // Exiger === au lieu de ==
    'eqeqeq': 'error',

    // Préférer const quand c'est possible
    'prefer-const': 'error',

    // Interdire var
    'no-var': 'error',

    // Indentation de 2 espaces
    'indent': ['error', 2],

    // Guillemets simples
    'quotes': ['error', 'single'],

    // Points-virgules (ajustez selon votre préférence)
    'semi': ['error', 'never']  // ou 'always'
  }
}
```

---

## Conclusion

ESLint est un **outil indispensable** pour tout développeur JavaScript moderne. Il vous aide à :

- ✅ Écrire du code de meilleure qualité
- ✅ Éviter les bugs courants
- ✅ Apprendre les bonnes pratiques
- ✅ Maintenir un code cohérent
- ✅ Gagner du temps sur le débogage

**Conseil final** : Au début, ESLint peut sembler contraignant avec toutes ses règles. Mais très vite, vous comprendrez la valeur de ces garde-fous. Avec le temps, vous écrirez naturellement du code qui respecte ces règles, et ESLint deviendra simplement une vérification de sécurité plutôt qu'un correcteur permanent.

**Commencez simple** : Installez ESLint, choisissez un style guide (Standard est parfait pour débuter), et laissez-le vous guider. Vous progresserez rapidement !

---

## Ressources

- **Site officiel ESLint** : https://eslint.org/
- **Liste complète des règles** : https://eslint.org/docs/rules/
- **ESLint dans VS Code** : https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint
- **Standard JS** : https://standardjs.com/
- **Airbnb Style Guide** : https://github.com/airbnb/javascript
- **Documentation npm** : https://docs.npmjs.com/

---


⏭️ [Tests de compatibilité navigateur (Can I Use)](/07-debugging-et-outils-avances/03-validation-qualite/03-compatibilite-navigateur.md)
