🔝 Retour au [Sommaire](/SOMMAIRE.md)

# Annexe D - Configuration d'Environnement Complète

Ce guide vous accompagne pas à pas dans l'installation et la configuration complète de votre environnement de développement web moderne. Que vous soyez sur Windows, macOS ou Linux, vous trouverez ici toutes les instructions nécessaires.

**⏱️ Temps estimé :** 1 à 2 heures pour une installation complète

**💡 Conseil :** Suivez l'ordre des sections et ne sautez pas d'étapes !

---

## 📋 Table des Matières

1. [Prérequis et Vue d'Ensemble](#1-pr%C3%A9requis-et-vue-densemble)
2. [Installation de Visual Studio Code](#2-installation-de-visual-studio-code)
3. [Configuration de VS Code](#3-configuration-de-vs-code)
4. [Installation de Node.js et npm](#4-installation-de-nodejs-et-npm)
5. [Installation et Configuration de Git](#5-installation-et-configuration-de-git)
6. [Navigateurs et Outils de Développement](#6-navigateurs-et-outils-de-d%C3%A9veloppement)
7. [Terminal et Ligne de Commande](#7-terminal-et-ligne-de-commande)
8. [Outils Complémentaires](#8-outils-compl%C3%A9mentaires)
9. [Vérification de l'Installation](#9-v%C3%A9rification-de-linstallation)
10. [Dépannage](#10-d%C3%A9pannage)

---

## 1. Prérequis et Vue d'Ensemble

### Ce dont vous aurez besoin

#### Matériel recommandé
- **Processeur** : Dual-core minimum (Quad-core recommandé)
- **RAM** : 4 GB minimum (8 GB recommandés)
- **Espace disque** : 10 GB libres minimum
- **Connexion Internet** : Pour télécharger les outils

#### Systèmes d'exploitation supportés
- ✅ Windows 10/11
- ✅ macOS 10.14 (Mojave) ou supérieur
- ✅ Linux (Ubuntu, Debian, Fedora, etc.)

### Vue d'ensemble des outils à installer

| Outil | Utilité | Obligatoire |
|-------|---------|-------------|
| **Visual Studio Code** | Éditeur de code principal | ✅ Oui |
| **Node.js & npm** | Runtime JavaScript et gestionnaire de paquets | ✅ Oui |
| **Git** | Gestion de versions | ✅ Oui |
| **Chrome/Firefox** | Navigateurs pour tester et déboguer | ✅ Oui |
| **Extensions VS Code** | Améliorer l'expérience de développement | ✅ Oui |
| **Postman** | Tester les APIs | ⚪ Optionnel |
| **Figma** | Design et maquettes | ⚪ Optionnel |

---

## 2. Installation de Visual Studio Code

Visual Studio Code (VS Code) est l'éditeur de code le plus populaire pour le développement web. Il est gratuit, open source et très extensible.

### 2.1 Téléchargement

**🌐 URL officielle :** https://code.visualstudio.com/

#### Pour Windows

1. Rendez-vous sur https://code.visualstudio.com/
2. Cliquez sur **"Download for Windows"**
3. Téléchargez la version **User Installer** (recommandée) ou **System Installer**
   - **User Installer** : Installation pour votre utilisateur uniquement (pas besoin de droits admin)
   - **System Installer** : Installation pour tous les utilisateurs (nécessite droits admin)

4. **Installation :**
   ```
   1. Double-cliquez sur le fichier téléchargé (VSCodeUserSetup-x64-X.XX.X.exe)
   2. Acceptez les termes de la licence
   3. Choisissez le dossier d'installation (par défaut : C:\Users\VotreNom\AppData\Local\Programs\Microsoft VS Code)
   4. ✅ IMPORTANT : Cochez toutes ces options :
      ☑️ Créer une icône sur le Bureau
      ☑️ Ajouter "Ouvrir avec Code" au menu contextuel
      ☑️ Ajouter à PATH (très important !)
      ☑️ Enregistrer Code comme éditeur par défaut
   5. Cliquez sur "Installer"
   6. Cliquez sur "Terminer" (cochez "Lancer Visual Studio Code")
   ```

#### Pour macOS

1. Rendez-vous sur https://code.visualstudio.com/
2. Cliquez sur **"Download for macOS"**
3. Téléchargez selon votre processeur :
   - **Apple Silicon** (M1, M2, M3) : Version ARM
   - **Intel** : Version Intel

4. **Installation :**
   ```
   1. Ouvrez le fichier .zip téléchargé
   2. Glissez l'application "Visual Studio Code" dans le dossier Applications
   3. Ouvrez Launchpad et cliquez sur VS Code
   4. Si message de sécurité : Système > Confidentialité > Autoriser
   ```

5. **Ajouter VS Code au PATH (important) :**
   ```
   1. Ouvrez VS Code
   2. Appuyez sur Cmd+Shift+P (palette de commandes)
   3. Tapez "shell command"
   4. Sélectionnez "Shell Command: Install 'code' command in PATH"
   5. Redémarrez le terminal
   ```

#### Pour Linux (Ubuntu/Debian)

**Méthode 1 : Via le fichier .deb (recommandée)**

1. Téléchargez le fichier .deb depuis https://code.visualstudio.com/
2. Installation :
   ```bash
   # Via la ligne de commande
   sudo dpkg -i code_X.XX.X_amd64.deb

   # Si erreurs de dépendances
   sudo apt-get install -f
   ```

**Méthode 2 : Via apt repository**

```bash
# 1. Installer les prérequis
sudo apt update
sudo apt install wget gpg

# 2. Ajouter la clé GPG de Microsoft
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

# 3. Ajouter le dépôt
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

# 4. Installer VS Code
sudo apt update
sudo apt install code
```

#### Pour Linux (Fedora/Red Hat)

```bash
# 1. Importer la clé
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# 2. Ajouter le repository
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

# 3. Installer
sudo dnf check-update
sudo dnf install code
```

### 2.2 Premier lancement

1. Lancez VS Code
2. **Choisir le thème :**
   - Thème clair ou sombre selon votre préférence
   - Recommandation : "Dark+ (default dark)" pour commencer

3. **Langue de l'interface :**
   - Par défaut en anglais
   - Pour installer le français :
     ```
     1. Ctrl+Shift+X (Extensions)
     2. Cherchez "French Language Pack"
     3. Cliquez "Install"
     4. Redémarrez VS Code
     ```

---

## 3. Configuration de VS Code

### 3.1 Extensions Essentielles

Les extensions ajoutent des fonctionnalités à VS Code. Voici les indispensables pour le développement web.

**Comment installer une extension :**
```
1. Cliquez sur l'icône Extensions (carré avec 4 petits carrés) dans la barre latérale
   OU appuyez sur Ctrl+Shift+X (Cmd+Shift+X sur Mac)
2. Tapez le nom de l'extension dans la barre de recherche
3. Cliquez sur "Install"
```

#### Extensions pour HTML

**1. HTML CSS Support**
- **ID :** `ecmel.vscode-html-css`
- **Utilité :** Auto-complétion CSS dans HTML
- **Installation :** Cherchez "HTML CSS Support" et installez

**2. Auto Rename Tag**
- **ID :** `formulahendry.auto-rename-tag`
- **Utilité :** Renomme automatiquement la balise fermante
- **Installation :** Cherchez "Auto Rename Tag"

**3. IntelliSense for CSS class names in HTML**
- **ID :** `Zignd.html-css-class-completion`
- **Utilité :** Auto-complétion des noms de classes CSS

#### Extensions pour CSS

**4. CSS Peek**
- **ID :** `pranaygp.vscode-css-peek`
- **Utilité :** Voir rapidement les définitions CSS

**5. Stylelint**
- **ID :** `stylelint.vscode-stylelint`
- **Utilité :** Linter pour CSS/SCSS

#### Extensions pour JavaScript

**6. ESLint** ⭐
- **ID :** `dbaeumer.vscode-eslint`
- **Utilité :** Linter JavaScript (détecte les erreurs)
- **Configuration :**
  ```json
  // Après installation, ajouter dans settings.json :
  "eslint.validate": ["javascript", "javascriptreact"]
  ```

**7. JavaScript (ES6) code snippets**
- **ID :** `xabikos.JavaScriptSnippets`
- **Utilité :** Raccourcis pour le code JavaScript moderne

**8. Quokka.js** (optionnel mais génial)
- **ID :** `WallabyJs.quokka-vscode`
- **Utilité :** Exécuter JavaScript en temps réel dans VS Code

#### Extensions pour Git

**9. GitLens** ⭐
- **ID :** `eamodio.gitlens`
- **Utilité :** Visualiser l'historique Git, auteurs, etc.

**10. Git Graph**
- **ID :** `mhutchie.git-graph`
- **Utilité :** Visualiser l'arbre des commits

#### Extensions générales indispensables

**11. Prettier - Code formatter** ⭐⭐⭐
- **ID :** `esbenp.prettier-vscode`
- **Utilité :** Formateur de code automatique
- **Configuration :**
  ```json
  // Dans settings.json :
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
  ```

**12. Live Server** ⭐⭐⭐
- **ID :** `ritwickdey.LiveServer`
- **Utilité :** Serveur local avec rechargement automatique
- **Usage :** Clic droit sur un fichier HTML > "Open with Live Server"

**13. Path Intellisense**
- **ID :** `christian-kohler.path-intellisense`
- **Utilité :** Auto-complétion des chemins de fichiers

**14. Bracket Pair Colorizer 2** (ou intégré depuis VS Code 1.67)
- **ID :** `CoenraadS.bracket-pair-colorizer-2`
- **Utilité :** Colore les paires de parenthèses/crochets
- **Note :** Fonctionnalité maintenant intégrée nativement dans VS Code

**15. indent-rainbow**
- **ID :** `oderwat.indent-rainbow`
- **Utilité :** Colore les niveaux d'indentation

**16. TODO Highlight**
- **ID :** `wayou.vscode-todo-highlight`
- **Utilité :** Met en évidence les TODO et FIXME dans le code

#### Extensions bonus (optionnelles)

**17. Material Icon Theme**
- **ID :** `PKief.material-icon-theme`
- **Utilité :** Icônes jolies pour les fichiers

**18. Error Lens**
- **ID :** `usernamehw.errorlens`
- **Utilité :** Affiche les erreurs directement dans le code

**19. Color Highlight**
- **ID :** `naumovs.color-highlight`
- **Utilité :** Prévisualise les couleurs dans le code

**20. REST Client**
- **ID :** `humao.rest-client`
- **Utilité :** Tester des APIs directement dans VS Code

### 3.2 Configuration des Paramètres

**Accéder aux paramètres :**
```
Fichier > Préférences > Paramètres
OU
Ctrl+, (Cmd+, sur Mac)
```

**Paramètres recommandés pour débutants :**

```json
{
  // Éditeur
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.wordWrap": "on",
  "editor.minimap.enabled": true,
  "editor.lineNumbers": "on",
  "editor.renderWhitespace": "boundary",
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,

  // Formatage automatique
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  // Suggestions
  "editor.quickSuggestions": {
    "strings": true
  },
  "editor.suggest.insertMode": "replace",

  // Fichiers
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,

  // Terminal intégré
  "terminal.integrated.fontSize": 13,
  "terminal.integrated.fontFamily": "Consolas, 'Courier New', monospace",

  // Emmet (raccourcis HTML/CSS)
  "emmet.triggerExpansionOnTab": true,
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },

  // JavaScript
  "javascript.updateImportsOnFileMove.enabled": "always",
  "javascript.suggest.autoImports": true,

  // Git
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "git.autofetch": true,

  // Live Server
  "liveServer.settings.donotShowInfoMsg": true,
  "liveServer.settings.donotVerifyTags": true,

  // Prettier
  "prettier.singleQuote": true,
  "prettier.semi": true,
  "prettier.trailingComma": "es5",
  "prettier.printWidth": 80,

  // ESLint
  "eslint.validate": [
    "javascript",
    "javascriptreact"
  ],

  // Explorateur de fichiers
  "explorer.confirmDelete": false,
  "explorer.confirmDragAndDrop": false,

  // Interface
  "workbench.colorTheme": "Default Dark+",
  "workbench.iconTheme": "material-icon-theme",
  "workbench.startupEditor": "welcomePage"
}
```

**Comment appliquer ces paramètres :**

1. **Méthode visuelle :**
   - Fichier > Préférences > Paramètres
   - Cherchez chaque paramètre et modifiez-le

2. **Méthode JSON (plus rapide) :**
   ```
   1. Ctrl+Shift+P (palette de commandes)
   2. Tapez "Preferences: Open User Settings (JSON)"
   3. Collez la configuration ci-dessus
   4. Sauvegardez (Ctrl+S)
   ```

### 3.3 Raccourcis Clavier Essentiels

**À mémoriser absolument :**

| Action | Windows/Linux | macOS |
|--------|---------------|-------|
| **Palette de commandes** | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| **Recherche de fichiers** | `Ctrl+P` | `Cmd+P` |
| **Recherche dans fichier** | `Ctrl+F` | `Cmd+F` |
| **Recherche globale** | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| **Terminal intégré** | `Ctrl+ù` | `Ctrl+ù` |
| **Enregistrer** | `Ctrl+S` | `Cmd+S` |
| **Enregistrer tout** | `Ctrl+K S` | `Cmd+K S` |
| **Fermer fichier** | `Ctrl+W` | `Cmd+W` |
| **Dupliquer ligne** | `Shift+Alt+↓` | `Shift+Opt+↓` |
| **Déplacer ligne** | `Alt+↑/↓` | `Opt+↑/↓` |
| **Commenter/Décommenter** | `Ctrl+/` | `Cmd+/` |
| **Multi-curseur** | `Ctrl+Alt+↑/↓` | `Cmd+Opt+↑/↓` |
| **Sélection multi-occurrence** | `Ctrl+D` | `Cmd+D` |
| **Formater le document** | `Shift+Alt+F` | `Shift+Opt+F` |
| **Zen Mode** | `Ctrl+K Z` | `Cmd+K Z` |

### 3.4 Snippets Personnalisés (Optionnel)

Les snippets sont des raccourcis pour générer du code rapidement.

**Créer des snippets HTML :**

```
1. Fichier > Préférences > Extraits utilisateur
2. Sélectionnez "html.json"
3. Ajoutez vos snippets :
```

```json
{
  "HTML5 Boilerplate": {
    "prefix": "html5",
    "body": [
      "<!DOCTYPE html>",
      "<html lang=\"fr\">",
      "<head>",
      "  <meta charset=\"UTF-8\">",
      "  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">",
      "  <title>${1:Titre de la page}</title>",
      "  <link rel=\"stylesheet\" href=\"${2:style.css}\">",
      "</head>",
      "<body>",
      "  $0",
      "  <script src=\"${3:script.js}\"></script>",
      "</body>",
      "</html>"
    ],
    "description": "HTML5 boilerplate complet"
  }
}
```

**Usage :** Tapez `html5` puis Tab dans un fichier HTML

---

## 4. Installation de Node.js et npm

Node.js est un environnement d'exécution JavaScript côté serveur. npm (Node Package Manager) est le gestionnaire de paquets qui vient avec Node.js.

**Pourquoi installer Node.js pour le développement frontend ?**
- Utiliser npm pour installer des outils (Vite, Webpack, etc.)
- Lancer des serveurs de développement
- Utiliser des build tools modernes
- Accéder à l'écosystème JavaScript

### 4.1 Installation

#### Pour Windows

**Méthode recommandée : Installateur officiel**

1. Rendez-vous sur https://nodejs.org/
2. Téléchargez la version **LTS** (Long Term Support) - recommandée
   - Version actuelle LTS : 20.x ou 22.x (décembre 2025)
3. Lancez l'installateur téléchargé (node-vXX.XX.X-x64.msi)
4. Suivez l'assistant d'installation :
   ```
   ☑️ Acceptez les termes de la licence
   ☑️ Installez dans le répertoire par défaut
   ☑️ Cochez "Automatically install the necessary tools" (chocolatey)
   ☑️ Cochez "Add to PATH" (déjà coché par défaut)
   ```
5. Redémarrez votre ordinateur (important !)

**Vérification :**
```bash
# Ouvrez PowerShell ou cmd
node --version    # Devrait afficher v20.x.x ou v22.x.x
npm --version     # Devrait afficher 10.x.x
```

#### Pour macOS

**Méthode 1 : Installateur officiel (recommandée pour débutants)**

1. Rendez-vous sur https://nodejs.org/
2. Téléchargez la version **LTS**
3. Ouvrez le fichier .pkg téléchargé
4. Suivez l'assistant d'installation
5. Entrez votre mot de passe administrateur si demandé

**Méthode 2 : Homebrew (recommandée pour utilisateurs avancés)**

```bash
# 1. Installer Homebrew si pas déjà fait
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. Installer Node.js
brew install node

# 3. Vérifier
node --version
npm --version
```

**Vérification :**
```bash
# Ouvrez le Terminal
node --version
npm --version
```

#### Pour Linux (Ubuntu/Debian)

**Méthode recommandée : NodeSource repository**

```bash
# 1. Télécharger et exécuter le script d'installation pour Node.js 20.x (LTS)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

# 2. Installer Node.js et npm
sudo apt-get install -y nodejs

# 3. Vérifier l'installation
node --version
npm --version
```

**Alternative : Utiliser nvm (Node Version Manager) - recommandé pour gérer plusieurs versions**

```bash
# 1. Installer nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# 2. Recharger le terminal
source ~/.bashrc

# 3. Installer Node.js LTS
nvm install --lts

# 4. Utiliser cette version
nvm use --lts

# 5. Définir comme version par défaut
nvm alias default node

# 6. Vérifier
node --version
npm --version
```

#### Pour Linux (Fedora)

```bash
# Installer Node.js et npm
sudo dnf install nodejs npm

# Vérifier
node --version
npm --version
```

### 4.2 Configuration de npm

**Vérifier la configuration actuelle :**
```bash
npm config list
```

**Configuration recommandée :**

```bash
# 1. Définir le dossier global des packages (optionnel, pour éviter les problèmes de permissions)
# Windows : pas nécessaire
# macOS/Linux :
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'

# Ajouter au PATH (dans ~/.bashrc ou ~/.zshrc)
export PATH=~/.npm-global/bin:$PATH
source ~/.bashrc  # ou source ~/.zshrc

# 2. Définir l'auteur par défaut (pour package.json)
npm config set init-author-name "Votre Nom"
npm config set init-author-email "votre.email@exemple.com"
npm config set init-license "MIT"

# 3. Activer les scripts automatiques (prudent avec les sources inconnues)
npm config set ignore-scripts false
```

### 4.3 Installer des outils globaux utiles

```bash
# 1. Mise à jour de npm lui-même
npm install -g npm@latest

# 2. http-server : serveur HTTP simple
npm install -g http-server

# 3. live-server : serveur avec rechargement automatique
npm install -g live-server

# 4. Vite (optionnel, pour les projets modernes)
npm install -g create-vite

# 5. ESLint (optionnel, pour le linting)
npm install -g eslint

# Vérifier les installations
http-server --version
live-server --version
```

**Usage de http-server :**
```bash
# Dans votre dossier de projet
http-server

# Ouvrir http://localhost:8080 dans le navigateur
```

**Usage de live-server :**
```bash
# Dans votre dossier de projet
live-server

# Ouvre automatiquement le navigateur
```

### 4.4 Créer votre premier projet npm

```bash
# 1. Créer un dossier pour votre projet
mkdir mon-premier-projet
cd mon-premier-projet

# 2. Initialiser un projet npm
npm init -y

# Cela crée un fichier package.json

# 3. Installer une dépendance (exemple)
npm install lodash

# 4. Installer une dépendance de développement (exemple)
npm install --save-dev prettier

# 5. Voir la structure
ls -la
# Vous devriez voir :
# - package.json
# - package-lock.json
# - node_modules/ (dossier)
```

**Comprendre package.json :**

```json
{
  "name": "mon-premier-projet",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "http-server",
    "dev": "live-server"
  },
  "keywords": [],
  "author": "Votre Nom",
  "license": "MIT",
  "dependencies": {
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "prettier": "^3.1.0"
  }
}
```

---

## 5. Installation et Configuration de Git

Git est le système de gestion de versions le plus utilisé. Il permet de suivre les modifications de votre code et de collaborer avec d'autres développeurs.

### 5.1 Installation de Git

#### Pour Windows

**Méthode recommandée : Git for Windows**

1. Téléchargez depuis https://git-scm.com/download/win
2. Lancez l'installateur
3. **Configuration importante :**
   ```
   ☑️ Use Visual Studio Code as Git's default editor
   ☑️ Override the default branch name for new repositories : "main"
   ☑️ Git from the command line and also from 3rd-party software
   ☑️ Use bundled OpenSSH
   ☑️ Use the OpenSSL library
   ☑️ Checkout Windows-style, commit Unix-style line endings
   ☑️ Use MinTTY (the default terminal of MSYS2)
   ☑️ Fast-forward or merge (default)
   ☑️ Git Credential Manager
   ☑️ Enable file system caching
   ☑️ Enable symbolic links
   ```

4. Terminez l'installation
5. Redémarrez VS Code

**Vérification :**
```bash
# Ouvrez PowerShell ou Git Bash
git --version
# Devrait afficher : git version 2.43.0 ou supérieur
```

#### Pour macOS

**Méthode 1 : Installer via Xcode Command Line Tools**

```bash
# Git est généralement pré-installé sur macOS
# Pour installer/mettre à jour :
xcode-select --install
```

**Méthode 2 : Via Homebrew (recommandée)**

```bash
# Installer Git
brew install git

# Vérifier
git --version
```

#### Pour Linux (Ubuntu/Debian)

```bash
# Mettre à jour les paquets
sudo apt update

# Installer Git
sudo apt install git

# Vérifier
git --version
```

#### Pour Linux (Fedora)

```bash
# Installer Git
sudo dnf install git

# Vérifier
git --version
```

### 5.2 Configuration initiale de Git

**Configuration obligatoire (identité) :**

```bash
# Définir votre nom (sera visible dans l'historique des commits)
git config --global user.name "Votre Nom"

# Définir votre email (utilisez le même que sur GitHub/GitLab)
git config --global user.email "votre.email@exemple.com"

# Vérifier la configuration
git config --list
```

**Configuration recommandée :**

```bash
# Définir l'éditeur par défaut (VS Code)
git config --global core.editor "code --wait"

# Nom de la branche principale par défaut
git config --global init.defaultBranch main

# Coloriser la sortie
git config --global color.ui auto

# Configuration des fins de ligne
# Windows :
git config --global core.autocrlf true
# macOS/Linux :
git config --global core.autocrlf input

# Aliases utiles
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --decorate --all'

# Afficher l'historique de manière lisible
git config --global log.abbrevCommit true
```

**Afficher toute la configuration :**
```bash
git config --global --list
```

### 5.3 Configuration SSH pour GitHub/GitLab (Recommandé)

L'authentification SSH est plus sécurisée et pratique que HTTPS.

**Étape 1 : Générer une clé SSH**

```bash
# Générer une nouvelle clé SSH
ssh-keygen -t ed25519 -C "votre.email@exemple.com"

# Si votre système ne supporte pas ed25519, utilisez RSA :
ssh-keygen -t rsa -b 4096 -C "votre.email@exemple.com"

# Quand demandé :
# "Enter file in which to save the key" : Appuyez sur Entrée (utilise le chemin par défaut)
# "Enter passphrase" : Choisissez un mot de passe (optionnel mais recommandé)
```

**Étape 2 : Ajouter la clé à l'agent SSH**

**Windows :**
```bash
# Démarrer l'agent SSH
eval "$(ssh-agent -s)"

# Ajouter la clé
ssh-add ~/.ssh/id_ed25519
```

**macOS :**
```bash
# Démarrer l'agent
eval "$(ssh-agent -s)"

# Ajouter la clé au trousseau macOS
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

# Configurer le fichier SSH config
mkdir -p ~/.ssh
cat >> ~/.ssh/config << EOF
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
EOF
```

**Linux :**
```bash
# Démarrer l'agent
eval "$(ssh-agent -s)"

# Ajouter la clé
ssh-add ~/.ssh/id_ed25519
```

**Étape 3 : Copier la clé publique**

```bash
# Afficher et copier la clé publique
cat ~/.ssh/id_ed25519.pub

# Ou copier directement dans le presse-papiers :
# Windows (Git Bash) :
clip < ~/.ssh/id_ed25519.pub

# macOS :
pbcopy < ~/.ssh/id_ed25519.pub

# Linux (avec xclip) :
xclip -selection clipboard < ~/.ssh/id_ed25519.pub
```

**Étape 4 : Ajouter la clé à GitHub**

1. Allez sur https://github.com/settings/keys
2. Cliquez sur **"New SSH key"**
3. Donnez un titre (ex: "Mon PC portable")
4. Collez la clé publique
5. Cliquez sur **"Add SSH key"**

**Étape 5 : Tester la connexion**

```bash
# Tester la connexion à GitHub
ssh -T git@github.com

# Vous devriez voir :
# "Hi username! You've successfully authenticated..."
```

### 5.4 Créer un fichier .gitignore global

Créer un fichier qui ignore certains fichiers automatiquement dans tous vos projets.

```bash
# Créer le fichier
touch ~/.gitignore_global

# Le configurer dans Git
git config --global core.excludesfile ~/.gitignore_global
```

**Contenu recommandé pour .gitignore_global :**

```
# Systèmes d'exploitation
.DS_Store
Thumbs.db

# Éditeurs
.vscode/
.idea/
*.swp
*.swo
*~

# Node.js
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Logs
logs/
*.log

# Environnement
.env
.env.local
.env.*.local

# Builds
dist/
build/
```

---

## 6. Navigateurs et Outils de Développement

### 6.1 Navigateurs recommandés

**Installer au minimum 2 navigateurs pour tester :**

#### 1. Google Chrome (Recommandé) ⭐

**Pourquoi :** DevTools les plus avancés, grande communauté

- **Téléchargement :** https://www.google.com/chrome/
- **Installation :** Standard, suivez l'assistant
- **Extensions recommandées :**
  - React Developer Tools
  - Redux DevTools
  - Lighthouse
  - JSON Viewer
  - ColorZilla
  - WhatFont

#### 2. Mozilla Firefox Developer Edition ⭐

**Pourquoi :** Outils spécialement conçus pour les développeurs, excellent pour CSS Grid/Flexbox

- **Téléchargement :** https://www.mozilla.org/firefox/developer/
- **Installation :** Standard
- **Extensions recommandées :**
  - React Developer Tools
  - Vue.js devtools
  - Web Developer

#### 3. Microsoft Edge (Recommandé pour Windows)

**Pourquoi :** Basé sur Chromium, intégré à Windows

- **Téléchargement :** Préinstallé sur Windows 10/11, ou https://www.microsoft.com/edge
- **DevTools similaires à Chrome**

#### 4. Safari (Si macOS)

**Pourquoi :** Navigateur par défaut macOS, important pour tester

- **Téléchargement :** Préinstallé sur macOS
- **Activer les outils de développement :**
  ```
  Safari > Préférences > Avancées
  ☑️ Cocher "Afficher le menu Développement dans la barre des menus"
  ```

### 6.2 Ouvrir les DevTools

**Chrome/Edge/Firefox :**
- `F12` ou `Ctrl+Shift+I` (Windows/Linux)
- `Cmd+Opt+I` (macOS)
- Clic droit > Inspecter

**Safari :**
- `Cmd+Opt+I`

### 6.3 Extensions de navigateur utiles

**Pour Chrome/Edge :**

1. **Lighthouse** (audit de performance et accessibilité)
   - Intégré dans Chrome DevTools

2. **React Developer Tools**
   - Si vous utilisez React

3. **Vue.js devtools**
   - Si vous utilisez Vue.js

4. **JSON Viewer**
   - Affiche le JSON de manière lisible

5. **ColorZilla**
   - Pipette à couleurs

6. **WhatFont**
   - Identifier les polices utilisées

7. **Wappalyzer**
   - Détecter les technologies utilisées sur un site

**Installation :**
1. Chrome Web Store : https://chrome.google.com/webstore/
2. Cherchez l'extension
3. Cliquez sur "Ajouter à Chrome"

---

## 7. Terminal et Ligne de Commande

### 7.1 Terminal par défaut

#### Windows

**Options de terminal :**

**1. Windows Terminal (Recommandé) ⭐**
- Modern, onglets multiples, personnalisable
- **Installation :**
  ```
  Microsoft Store > Rechercher "Windows Terminal" > Installer
  ```
- Configuration recommandée :
  ```json
  // Paramètres > Ouvrir le fichier JSON
  {
    "defaultProfile": "{guid-de-powershell}",
    "profiles": {
      "defaults": {
        "fontFace": "Cascadia Code",
        "fontSize": 11
      }
    }
  }
  ```

**2. PowerShell**
- Préinstallé sur Windows
- Plus puissant que cmd

**3. Git Bash**
- Installé avec Git for Windows
- Émule les commandes Unix/Linux

**4. WSL2 (Windows Subsystem for Linux) - Pour utilisateurs avancés**
```bash
# Installer WSL2
wsl --install

# Redémarrer l'ordinateur
# Puis installer Ubuntu depuis le Microsoft Store
```

#### macOS

**Terminal par défaut :**
- Applications > Utilitaires > Terminal

**Alternative recommandée : iTerm2**
- Plus de fonctionnalités
- Téléchargement : https://iterm2.com/
- Configuration :
  ```
  Preferences > Profiles > Colors > Color Presets > Solarized Dark
  Preferences > Profiles > Text > Font > 13pt Monaco
  ```

**Shell recommandé : Zsh (par défaut depuis Catalina)**
- Déjà configuré sur les versions récentes de macOS

#### Linux

**Terminal par défaut :**
- Généralement GNOME Terminal, Konsole, ou xterm
- Raccourci : `Ctrl+Alt+T`

**Alternative : Terminator**
```bash
sudo apt install terminator
```

### 7.2 Commandes de base à connaître

**Navigation :**
```bash
# Afficher le répertoire courant
pwd

# Lister les fichiers
ls          # macOS/Linux
dir         # Windows

# Lister avec détails
ls -la      # macOS/Linux
dir /a      # Windows

# Changer de répertoire
cd chemin/vers/dossier
cd ..       # Remonter d'un niveau
cd ~        # Aller dans le home directory
cd /        # Aller à la racine

# Créer un dossier
mkdir nom-du-dossier
mkdir -p chemin/vers/dossier  # Créer les parents si nécessaire

# Créer un fichier
touch fichier.txt     # macOS/Linux
type nul > fichier.txt  # Windows

# Copier
cp source.txt destination.txt    # macOS/Linux
copy source.txt destination.txt  # Windows

# Déplacer/Renommer
mv ancien.txt nouveau.txt    # macOS/Linux
move ancien.txt nouveau.txt  # Windows

# Supprimer un fichier
rm fichier.txt    # macOS/Linux
del fichier.txt   # Windows

# Supprimer un dossier
rm -rf dossier/    # macOS/Linux
rmdir /s dossier\  # Windows

# Afficher le contenu d'un fichier
cat fichier.txt    # macOS/Linux
type fichier.txt   # Windows

# Éditer un fichier
code fichier.txt   # Ouvre dans VS Code

# Nettoyer le terminal
clear      # macOS/Linux
cls        # Windows
```

**Commandes Git de base :**
```bash
# Initialiser un repo
git init

# Voir le statut
git status

# Ajouter des fichiers
git add .
git add fichier.txt

# Commiter
git commit -m "Message de commit"

# Voir l'historique
git log
git log --oneline

# Créer une branche
git branch nom-branche

# Changer de branche
git checkout nom-branche
git switch nom-branche  # Commande moderne

# Créer et changer de branche
git checkout -b nom-branche

# Fusionner une branche
git merge nom-branche

# Cloner un repo
git clone https://github.com/user/repo.git

# Pousser vers remote
git push origin main

# Tirer depuis remote
git pull origin main
```

**Commandes npm de base :**
```bash
# Initialiser un projet
npm init
npm init -y  # Avec valeurs par défaut

# Installer des dépendances
npm install package-name
npm install -g package-name  # Global
npm install --save-dev package-name  # Dev dependency

# Désinstaller
npm uninstall package-name

# Lancer un script
npm run script-name
npm start
npm test

# Mettre à jour
npm update
npm update package-name

# Vérifier les packages obsolètes
npm outdated

# Audit de sécurité
npm audit
npm audit fix
```

### 7.3 Configuration du terminal dans VS Code

**Choisir votre terminal préféré dans VS Code :**

```
1. Ctrl+ù ou Terminal > Nouveau Terminal
2. Cliquez sur la flèche déroulante à côté du +
3. Choisissez "Sélectionner le profil par défaut"
4. Sélectionnez votre terminal préféré (PowerShell, Git Bash, Bash, etc.)
```

**Configuration du terminal :**
```json
// Dans settings.json
{
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.defaultProfile.osx": "zsh",
  "terminal.integrated.defaultProfile.linux": "bash",
  "terminal.integrated.fontSize": 13,
  "terminal.integrated.fontFamily": "Cascadia Code, Consolas, monospace"
}
```

---

## 8. Outils Complémentaires

### 8.1 Gestionnaire de mots de passe

**Recommandé : Bitwarden (gratuit, open source)**
- https://bitwarden.com/
- Pour stocker vos identifiants GitHub, APIs, etc.

**Alternatives :**
- 1Password
- LastPass
- KeePass

### 8.2 Outils de design

**Figma (recommandé, gratuit)**
- https://www.figma.com/
- Collaboratif, dans le navigateur
- Pour créer des maquettes

**Alternatives :**
- Adobe XD
- Sketch (macOS uniquement)
- Penpot (open source)

### 8.3 Outils de test d'API

**Postman (recommandé)**
- https://www.postman.com/
- Tester des APIs REST
- Gratuit pour usage personnel

**Alternative : Insomnia**
- https://insomnia.rest/

**Alternative : Extension VS Code : REST Client**
- Tester des APIs directement dans VS Code

### 8.4 Capture d'écran et enregistrement

**Windows :**
- **Outil Capture d'écran** (intégré)
- **ShareX** (gratuit, puissant) : https://getsharex.com/

**macOS :**
- **Cmd+Shift+3** : Capture plein écran
- **Cmd+Shift+4** : Capture zone
- **Cmd+Shift+5** : Options avancées

**Linux :**
- **Flameshot** : `sudo apt install flameshot`
- **GNOME Screenshot** (pré-installé sur Ubuntu)

### 8.5 Compression d'images

**En ligne :**
- TinyPNG : https://tinypng.com/
- Squoosh : https://squoosh.app/

**Outil local : ImageOptim (macOS)**
- https://imageoptim.com/

### 8.6 Gestionnaire de base de données (si backend)

**DB Browser for SQLite**
- https://sqlitebrowser.org/
- Gratuit, facile à utiliser

**DBeaver (avancé)**
- https://dbeaver.io/
- Supporte MySQL, PostgreSQL, etc.

### 8.7 Fonts et icônes

**Google Fonts**
- https://fonts.google.com/
- Polices gratuites

**Font Awesome (icônes)**
- https://fontawesome.com/
- Icônes gratuites et payantes

**Heroicons (icônes)**
- https://heroicons.com/
- Icônes SVG gratuites

---

## 9. Vérification de l'Installation

### 9.1 Checklist finale

Vérifiez que tout fonctionne correctement :

```bash
# ✅ Visual Studio Code
code --version

# ✅ Node.js
node --version
# Attendu : v20.x.x ou v22.x.x

# ✅ npm
npm --version
# Attendu : 10.x.x

# ✅ Git
git --version
# Attendu : 2.43.x ou supérieur

# ✅ Git configuration
git config user.name
git config user.email

# ✅ SSH (si configuré)
ssh -T git@github.com
# Attendu : "Hi username! You've successfully authenticated..."
```

### 9.2 Créer un projet de test

Testez votre environnement avec un mini-projet :

```bash
# 1. Créer un dossier de test
mkdir test-env
cd test-env

# 2. Initialiser Git
git init

# 3. Créer un fichier HTML
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Environnement</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>🎉 Mon environnement fonctionne !</h1>
    <p id="message">Cliquez sur le bouton ci-dessous</p>
    <button id="btn">Cliquer ici</button>
    <script src="script.js"></script>
</body>
</html>
EOF

# 4. Créer un fichier CSS
cat > style.css << 'EOF'
body {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    background: white;
    color: #667eea;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 20px;
}

button:hover {
    transform: scale(1.05);
}
EOF

# 5. Créer un fichier JavaScript
cat > script.js << 'EOF'
const btn = document.getElementById('btn');
const message = document.getElementById('message');

btn.addEventListener('click', () => {
    message.textContent = '✨ Environnement configuré avec succès !';
    console.log('Tout fonctionne parfaitement !');
});
EOF

# 6. Ouvrir dans VS Code
code .

# 7. Ouvrir avec Live Server
# Clic droit sur index.html > Open with Live Server
```

**Vérifications à faire :**

- [ ] VS Code s'ouvre correctement
- [ ] Les fichiers s'affichent dans l'explorateur
- [ ] La coloration syntaxique fonctionne
- [ ] Live Server lance le navigateur
- [ ] Le bouton fonctionne
- [ ] DevTools affiche le console.log
- [ ] Prettier formate le code au save

### 9.3 Test des extensions VS Code

```bash
# Liste des extensions installées
code --list-extensions

# Vérifiez que vous avez au minimum :
# - esbenp.prettier-vscode
# - dbaeumer.vscode-eslint
# - ritwickdey.LiveServer
# - eamodio.gitlens
```

---

## 10. Dépannage

### 10.1 Problèmes courants

#### Problème : "command not found" ou "n'est pas reconnu en tant que commande"

**Cause :** La commande n'est pas dans le PATH

**Solution Windows :**
```
1. Panneau de configuration > Système > Paramètres système avancés
2. Variables d'environnement
3. Dans "Variables système", sélectionnez "Path" et cliquez sur Modifier
4. Ajoutez le chemin vers le dossier contenant l'exécutable
   Exemples :
   - Node.js : C:\Program Files\nodejs\
   - Git : C:\Program Files\Git\cmd\
5. Cliquez OK et redémarrez le terminal
```

**Solution macOS/Linux :**
```bash
# Ajouter au PATH dans ~/.bashrc ou ~/.zshrc
echo 'export PATH="$PATH:/chemin/vers/programme"' >> ~/.bashrc
source ~/.bashrc
```

#### Problème : npm ERR! EACCES permission denied

**Solution macOS/Linux :**
```bash
# Changer le propriétaire du dossier npm
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) /usr/local/lib/node_modules

# Ou utiliser nvm pour éviter les problèmes de permissions
```

#### Problème : Git demande un nom d'utilisateur et mot de passe à chaque fois

**Solution :**
```bash
# Utiliser SSH au lieu de HTTPS
# Changer l'URL du remote
git remote set-url origin git@github.com:username/repo.git

# Ou configurer le cache des credentials HTTPS
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'
```

#### Problème : VS Code ne trouve pas Git

**Solution :**
```json
// Dans settings.json
{
  "git.path": "C:\\Program Files\\Git\\cmd\\git.exe"  // Windows
  // ou
  "git.path": "/usr/bin/git"  // macOS/Linux
}
```

#### Problème : Extensions VS Code ne s'installent pas

**Solution :**
```
1. Vérifier la connexion Internet
2. Désactiver le proxy si nécessaire (File > Preferences > Settings > Proxy)
3. Réinstaller VS Code
4. Installer manuellement :
   - Télécharger le .vsix depuis le marketplace
   - Extensions > ... > Install from VSIX
```

#### Problème : Live Server ne se lance pas

**Solution :**
```
1. Vérifier que le port 5500 n'est pas utilisé
2. Changer le port dans les paramètres :
   File > Preferences > Settings > chercher "Live Server"
   Port : 5501 (ou autre)
3. Redémarrer VS Code
```

#### Problème : Prettier ne formate pas automatiquement

**Solution :**
```json
// Vérifier settings.json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

### 10.2 Réinitialiser la configuration

**Réinitialiser VS Code :**
```bash
# Sauvegarder d'abord vos settings
# Puis supprimer les dossiers de configuration :

# Windows :
# %APPDATA%\Code\User\

# macOS :
# ~/Library/Application Support/Code/User/

# Linux :
# ~/.config/Code/User/
```

**Réinitialiser Git :**
```bash
# Supprimer toute la configuration
rm ~/.gitconfig

# Reconfigurer
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@exemple.com"
```

**Réinitialiser npm :**
```bash
# Supprimer le cache
npm cache clean --force

# Supprimer node_modules et réinstaller
rm -rf node_modules package-lock.json
npm install
```

### 10.3 Obtenir de l'aide

**Ressources officielles :**
- VS Code : https://code.visualstudio.com/docs
- Node.js : https://nodejs.org/docs
- Git : https://git-scm.com/doc
- npm : https://docs.npmjs.com/

**Communautés :**
- Stack Overflow : https://stackoverflow.com/
- Reddit r/webdev : https://reddit.com/r/webdev
- Discord servers (cherchez "web dev discord")

**Vérifier les logs :**
```bash
# VS Code : Help > Toggle Developer Tools > Console
# npm : npm-debug.log dans votre dossier de projet
# Git : git --no-pager log
```

---

## 📝 Résumé et Prochaines Étapes

### ✅ Ce que vous devriez avoir maintenant

- [x] Visual Studio Code installé et configuré
- [x] Extensions essentielles installées
- [x] Node.js et npm fonctionnels
- [x] Git configuré avec votre identité
- [x] SSH configuré pour GitHub (recommandé)
- [x] Au moins 2 navigateurs modernes
- [x] Terminal fonctionnel
- [x] Environnement de test créé et vérifié

### 🎯 Vérification finale (5 minutes)

Exécutez ces commandes pour vous assurer que tout fonctionne :

```bash
# 1. Versions
node --version && npm --version && git --version

# 2. Identité Git
git config user.name && git config user.email

# 3. VS Code
code --version

# 4. Test SSH GitHub (si configuré)
ssh -T git@github.com

# Si toutes ces commandes donnent un résultat positif, vous êtes prêt ! 🎉
```

### 🚀 Prochaines étapes

Maintenant que votre environnement est configuré, vous pouvez :

1. **Suivre la formation principale**
   - Commencez par le module 1 : Introduction au Développement Web
   - Pratiquez avec les exemples de code

2. **Créer votre premier projet réel**
   - Portfolio personnel
   - Landing page
   - Mini-application

3. **Rejoindre la communauté**
   - Créer un compte GitHub
   - Rejoindre des Discord/Slack de développeurs
   - Suivre des développeurs sur Twitter/X

4. **Continuer à apprendre**
   - FreeCodeCamp
   - The Odin Project
   - MDN Learning Area

### 📚 Ressources à garder sous la main

- **Documentation officielle :**
  - MDN Web Docs : https://developer.mozilla.org/
  - VS Code Docs : https://code.visualstudio.com/docs

- **Cheatsheets :**
  - Git : https://education.github.com/git-cheat-sheet-education.pdf
  - Terminal : https://github.com/0nn0/terminal-mac-cheatsheet

- **Communautés :**
  - Stack Overflow : https://stackoverflow.com/
  - Dev.to : https://dev.to/
  - GitHub : https://github.com/

---

## 🎓 Félicitations !

Vous avez terminé la configuration complète de votre environnement de développement web moderne. Vous disposez maintenant de tous les outils nécessaires pour créer des sites et applications web professionnels.

**N'oubliez pas :**
- Sauvegardez régulièrement votre travail avec Git
- Prenez l'habitude d'utiliser les raccourcis clavier
- Explorez les fonctionnalités de VS Code progressivement
- Demandez de l'aide quand vous êtes bloqué (c'est normal !)

**Bon développement et bienvenue dans la communauté web ! 🚀**

---

## 📋 Annexe : Configuration complète en une page

### Checklist d'installation rapide

```bash
# ✅ 1. Visual Studio Code
# Télécharger et installer depuis https://code.visualstudio.com/

# ✅ 2. Node.js et npm
# Télécharger version LTS depuis https://nodejs.org/
node --version
npm --version

# ✅ 3. Git
# Télécharger depuis https://git-scm.com/
git --version
git config --global user.name "Votre Nom"
git config --global user.email "votre@email.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"

# ✅ 4. SSH pour GitHub (optionnel mais recommandé)
ssh-keygen -t ed25519 -C "votre@email.com"
cat ~/.ssh/id_ed25519.pub  # Copier et ajouter à GitHub

# ✅ 5. Extensions VS Code essentielles
# - Prettier
# - ESLint
# - Live Server
# - GitLens
# - Auto Rename Tag

# ✅ 6. Navigateurs
# - Chrome : https://www.google.com/chrome/
# - Firefox Developer Edition : https://www.mozilla.org/firefox/developer/

# ✅ 7. Test final
mkdir test-env && cd test-env
git init
npm init -y
code .
```

### Fichier settings.json minimal

```json
{
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "files.autoSave": "afterDelay",
  "terminal.integrated.fontSize": 13,
  "git.enableSmartCommit": true,
  "workbench.colorTheme": "Default Dark+"
}
```

---

**Dernière mise à jour :** Décembre 2025

⏭️ Retour au [Sommaire](/SOMMAIRE.md)
