🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.4.3 - Git : notions avancées et collaboration

## Introduction

**Git** est le système de gestion de versions le plus utilisé au monde. Si vous savez déjà faire des commits et des push basiques, ce tutoriel vous aidera à maîtriser les fonctionnalités plus avancées de Git et à collaborer efficacement en équipe.

### Pourquoi aller au-delà des bases ?

Les bases de Git (commit, push, pull) suffisent pour des projets personnels simples. Mais dès que vous :
- Travaillez en équipe
- Développez plusieurs fonctionnalités en parallèle
- Devez revenir en arrière sur certains changements
- Contribuez à des projets open source

Vous avez besoin de maîtriser les **branches**, les **merges**, la **résolution de conflits** et les **workflows collaboratifs**.

> 💡 **Analogie** : Git basique, c'est comme conduire en ligne droite. Git avancé, c'est apprendre à faire des manœuvres, changer de voie, gérer les intersections et conduire avec d'autres voitures autour de vous.

---

## Rappel des bases Git

### Installation et configuration

**Vérifier l'installation** :
```bash
git --version
```

**Configuration initiale** (si pas déjà fait) :
```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

### Commandes de base (révision rapide)

| Commande | Action |
|----------|--------|
| `git init` | Initialise un dépôt Git |
| `git add fichier.txt` | Ajoute un fichier au staging |
| `git add .` | Ajoute tous les fichiers modifiés |
| `git commit -m "message"` | Crée un commit |
| `git status` | Affiche l'état des fichiers |
| `git log` | Affiche l'historique des commits |
| `git push` | Envoie les commits vers le remote |
| `git pull` | Récupère les changements du remote |

---

## Les branches Git

### Qu'est-ce qu'une branche ?

Une **branche** est une ligne de développement indépendante. C'est comme une version parallèle de votre projet.

**Analogie** : Imaginez un document Word. Au lieu de créer "Document_v1.docx", "Document_v2.docx", etc., Git vous permet de travailler sur plusieurs versions en même temps, puis de les fusionner intelligemment.

### Pourquoi utiliser des branches ?

- ✅ **Développer des fonctionnalités isolément** : Ne pas perturber le code principal
- ✅ **Expérimenter sans risque** : Tester des idées sans casser ce qui fonctionne
- ✅ **Collaborer efficacement** : Chacun travaille sur sa branche
- ✅ **Organiser le travail** : Une branche par fonctionnalité ou bug fix

### Visualisation des branches

```
main    : A---B---C---D---E---F
                   \         /
feature :           G---H---I
```

- **main** : La branche principale (production)
- **feature** : Une branche pour développer une nouvelle fonctionnalité
- Le point C : Moment où on crée la branche
- Le point F : Moment où on fusionne la branche

### Commandes de base pour les branches

#### Voir les branches existantes
```bash
git branch
```

Le `*` indique la branche actuelle.

#### Créer une nouvelle branche
```bash
git branch nom-de-la-branche
```

**Convention de nommage** :
- `feature/nouvelle-fonctionnalite`
- `bugfix/correction-menu`
- `hotfix/securite-critique`

#### Changer de branche
```bash
git checkout nom-de-la-branche
```

**Ou avec Git moderne (2.23+)** :
```bash
git switch nom-de-la-branche
```

#### Créer ET changer de branche en une commande
```bash
git checkout -b nom-de-la-branche
```

**Ou** :
```bash
git switch -c nom-de-la-branche
```

#### Supprimer une branche
```bash
git branch -d nom-de-la-branche
```

**Force delete** (si la branche n'est pas mergée) :
```bash
git branch -D nom-de-la-branche
```

---

## Workflow typique avec branches

### Scénario : Ajouter une nouvelle fonctionnalité

**Étape 1 : Partir de la branche principale**
```bash
git checkout main
git pull  # S'assurer d'avoir la dernière version
```

**Étape 2 : Créer une branche pour la fonctionnalité**
```bash
git checkout -b feature/ajout-formulaire-contact
```

**Étape 3 : Développer**
```bash
# Modifier des fichiers
git add .
git commit -m "feat: ajoute la structure HTML du formulaire"

# Continuer à développer
git add .
git commit -m "feat: ajoute le style CSS du formulaire"

git add .
git commit -m "feat: ajoute la validation JavaScript"
```

**Étape 4 : Pousser la branche vers GitHub**
```bash
git push origin feature/ajout-formulaire-contact
```

**Étape 5 : Fusionner dans main (une fois terminé)**
```bash
git checkout main
git merge feature/ajout-formulaire-contact
git push origin main
```

**Étape 6 : Supprimer la branche (optionnel)**
```bash
git branch -d feature/ajout-formulaire-contact
git push origin --delete feature/ajout-formulaire-contact
```

---

## Merge : Fusionner des branches

### Types de merge

#### 1. Fast-Forward Merge (le plus simple)

**Situation** : Aucun commit n'a été fait sur `main` pendant que vous travailliez sur la branche.

```
Avant merge :
main   : A---B---C
              \
feature:       D---E

Après merge (fast-forward) :
main   : A---B---C---D---E
```

**Commande** :
```bash
git checkout main
git merge feature/ma-fonctionnalite
```

Git déplace simplement le pointeur `main` vers le dernier commit de la branche.

#### 2. Three-Way Merge (fusion à 3 points)

**Situation** : Des commits ont été faits sur `main` ET sur la branche.

```
Avant merge :
main   : A---B---C---F
              \
feature:       D---E

Après merge (three-way) :
main   : A---B---C---F---M
              \         /
feature:       D---E---
```

M = commit de merge qui combine les deux branches.

**Commande** :
```bash
git checkout main
git merge feature/ma-fonctionnalite
```

Git crée automatiquement un **commit de merge**.

---

## Conflits de merge

### Qu'est-ce qu'un conflit ?

Un **conflit** survient quand Git ne peut pas fusionner automatiquement parce que le même code a été modifié différemment dans les deux branches.

**Exemple de situation conflictuelle** :

**Branche main** :
```html
<h1>Bienvenue sur notre site</h1>
```

**Branche feature** :
```html
<h1>Bienvenue sur MonSite.com</h1>
```

Git ne sait pas quelle version garder !

### Identifier un conflit

Quand vous tentez un merge et qu'il y a un conflit :

```bash
git merge feature/ma-branche

Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

### Voir les fichiers en conflit

```bash
git status
```

Affiche :
```
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.html
```

### Résoudre un conflit

**1. Ouvrir le fichier en conflit**

Git ajoute des marqueurs dans le fichier :

```html
<h1>
<<<<<<< HEAD
Bienvenue sur notre site
=======
Bienvenue sur MonSite.com
>>>>>>> feature/ma-branche
</h1>
```

**Explication des marqueurs** :
- `<<<<<<< HEAD` : Version de la branche actuelle (main)
- `=======` : Séparateur
- `>>>>>>> feature/ma-branche` : Version de la branche à merger

**2. Choisir la bonne version**

**Option A** : Garder la version de main
```html
<h1>Bienvenue sur notre site</h1>
```

**Option B** : Garder la version de la branche feature
```html
<h1>Bienvenue sur MonSite.com</h1>
```

**Option C** : Combiner les deux
```html
<h1>Bienvenue sur notre site - MonSite.com</h1>
```

**Option D** : Écrire quelque chose de complètement nouveau
```html
<h1>Bienvenue sur MonSite - Votre partenaire web</h1>
```

**3. Supprimer les marqueurs de conflit**

Assurez-vous de supprimer :
- `<<<<<<< HEAD`
- `=======`
- `>>>>>>> nom-de-la-branche`

**4. Marquer le conflit comme résolu**

```bash
git add index.html
```

**5. Finaliser le merge**

```bash
git commit -m "merge: résout le conflit dans index.html"
```

Ou simplement :
```bash
git commit
```

Git ouvrira un éditeur avec un message de merge par défaut.

### Annuler un merge en cours

Si vous êtes perdu dans la résolution de conflits :

```bash
git merge --abort
```

Cela annule le merge et revient à l'état d'avant.

---

## Collaboration avec GitHub

### Remote : Le dépôt distant

**Remote** = La version de votre projet hébergée sur GitHub (ou GitLab, Bitbucket, etc.)

#### Voir les remotes configurés
```bash
git remote -v
```

Affiche :
```
origin  https://github.com/username/mon-projet.git (fetch)
origin  https://github.com/username/mon-projet.git (push)
```

**origin** = nom par défaut du remote principal

#### Ajouter un remote
```bash
git remote add origin https://github.com/username/mon-projet.git
```

#### Changer l'URL d'un remote
```bash
git remote set-url origin https://github.com/username/nouveau-nom.git
```

### Push : Envoyer vos changements

**Push vers la branche actuelle** :
```bash
git push
```

**Push et créer la branche sur le remote** :
```bash
git push -u origin nom-de-la-branche
```

Le `-u` (ou `--set-upstream`) configure le tracking.

**Force push** (⚠️ Danger) :
```bash
git push --force
```

**⚠️ N'utilisez jamais `--force` sur une branche partagée !** Cela peut écraser le travail des autres.

### Pull : Récupérer les changements

**Pull = Fetch + Merge**

```bash
git pull
```

Équivaut à :
```bash
git fetch
git merge origin/nom-de-la-branche
```

#### Fetch : Récupérer sans fusionner

```bash
git fetch
```

Télécharge les changements mais ne les fusionne pas. Utile pour voir ce qui a changé avant de merger.

**Voir les différences** :
```bash
git diff main origin/main
```

---

## Pull Requests (GitHub)

### Qu'est-ce qu'une Pull Request ?

Une **Pull Request** (PR) est une demande de fusion de votre branche dans une autre branche (généralement `main`).

**Pourquoi utiliser des PRs ?**

- ✅ **Revue de code** : Les autres peuvent commenter et suggérer des améliorations
- ✅ **Discussion** : Échange sur les choix techniques
- ✅ **Validation** : Quelqu'un d'autre approuve avant la fusion
- ✅ **Historique** : Traçabilité des décisions

### Créer une Pull Request

**Étape 1 : Pousser votre branche**
```bash
git push origin feature/ma-fonctionnalite
```

**Étape 2 : Sur GitHub**
1. Allez sur votre repository
2. GitHub affiche souvent un bouton "Compare & pull request"
3. Sinon, allez dans l'onglet "Pull requests" > "New pull request"

**Étape 3 : Configurer la PR**
- **Base** : La branche cible (généralement `main`)
- **Compare** : Votre branche (`feature/ma-fonctionnalite`)
- **Titre** : Description courte (ex: "Ajoute le formulaire de contact")
- **Description** : Explication détaillée des changements

**Exemple de description de PR** :
```markdown
## Description
Ajoute un formulaire de contact avec validation côté client.

## Changements
- [x] Structure HTML du formulaire
- [x] Styles CSS responsive
- [x] Validation JavaScript
- [x] Tests sur Chrome, Firefox, Safari

## Screenshots
![Formulaire desktop](url-screenshot.png)
![Formulaire mobile](url-screenshot-mobile.png)

## À tester
1. Remplir le formulaire avec des données invalides
2. Vérifier que les messages d'erreur s'affichent
3. Soumettre avec des données valides
```

**Étape 4 : Créer la PR**
Cliquez sur "Create pull request"

### Revue et merge d'une PR

**Rôle du reviewer** :
1. Lire le code
2. Tester localement si nécessaire
3. Commenter ou demander des changements
4. Approuver si tout est bon

**Merge de la PR** :
1. Bouton "Merge pull request" sur GitHub
2. Choisir le type de merge :
   - **Create a merge commit** : Garde tout l'historique
   - **Squash and merge** : Combine tous les commits en un seul
   - **Rebase and merge** : Réécriture linéaire de l'historique

**Après le merge** :
```bash
# Localement, revenir sur main et pull
git checkout main
git pull

# Supprimer la branche locale
git branch -d feature/ma-fonctionnalite
```

---

## Workflows Git courants

### 1. GitHub Flow (Simple et efficace)

**Principe** : Une seule branche principale (`main`), toujours déployable.

```
main : Toujours stable et déployable

Workflow :
1. Créer une branche depuis main
2. Développer
3. Ouvrir une Pull Request
4. Revue de code
5. Merge dans main
6. Déployer immédiatement
```

**Avantages** :
- ✅ Simple
- ✅ Rapide
- ✅ Adapté au déploiement continu

**Inconvénients** :
- ⚠️ Pas de version stable "release"

**Idéal pour** : Applications web modernes, SaaS

---

### 2. Git Flow (Plus complexe, plus structuré)

**Principe** : Plusieurs branches avec des rôles définis.

**Branches principales** :
- **main** : Code en production
- **develop** : Code en développement

**Branches temporaires** :
- **feature/** : Nouvelles fonctionnalités
- **release/** : Préparation d'une release
- **hotfix/** : Corrections urgentes en production

```
main     : v1.0 -------- v1.1 -------- v2.0
                \       /      \       /
develop  : ------D------E-------F------G
            \   / \    /  \    /
feature  :   F1    F2     F3
```

**Workflow** :
1. Feature branchée depuis `develop`
2. Développement
3. Merge dans `develop`
4. Quand prêt, créer une branche `release`
5. Tests finaux sur `release`
6. Merge `release` dans `main` ET `develop`
7. Tag la version (v1.0, v1.1, etc.)

**Avantages** :
- ✅ Très structuré
- ✅ Séparation claire dev/prod
- ✅ Gestion de versions multiples

**Inconvénients** :
- ⚠️ Complexe
- ⚠️ Peut ralentir

**Idéal pour** : Logiciels avec versions planifiées

---

### 3. Trunk-Based Development

**Principe** : Tout le monde travaille sur `main` (ou fait des branches très courtes).

**Caractéristiques** :
- Commits fréquents sur `main`
- Feature flags pour cacher le code incomplet
- Tests automatisés très robustes

**Avantages** :
- ✅ Intégration continue maximale
- ✅ Évite les gros merges complexes

**Inconvénients** :
- ⚠️ Nécessite une discipline rigoureuse
- ⚠️ Tests automatisés indispensables

**Idéal pour** : Équipes matures avec CI/CD solide

---

## Commandes Git avancées

### 1. Stash : Mettre de côté des changements

**Situation** : Vous travaillez sur quelque chose, mais devez changer de branche d'urgence.

```bash
# Mettre de côté les changements non commités
git stash

# Changer de branche et travailler
git checkout autre-branche

# Revenir et récupérer les changements
git checkout ma-branche
git stash pop
```

**Autres commandes stash** :
```bash
git stash list          # Voir tous les stashs
git stash apply         # Appliquer sans supprimer
git stash drop          # Supprimer le dernier stash
git stash clear         # Supprimer tous les stashs
```

---

### 2. Rebase : Réécrire l'historique

**Rebase** réapplique vos commits sur une autre base.

**Exemple** :
```
Avant rebase :
main   : A---B---C---D
              \
feature:       E---F

Après rebase :
main   : A---B---C---D
                      \
feature:               E'---F'
```

**Commande** :
```bash
git checkout feature/ma-branche
git rebase main
```

**Utilité** :
- ✅ Historique linéaire et propre
- ✅ Évite les commits de merge
- ✅ Facilite la lecture de l'historique

**⚠️ Règle d'or** : Ne jamais rebase des commits déjà pushés et partagés !

#### Rebase interactif

**Réécrire les derniers commits** :
```bash
git rebase -i HEAD~3  # Les 3 derniers commits
```

**Options disponibles** :
- `pick` : Garder le commit tel quel
- `reword` : Changer le message
- `edit` : Modifier le commit
- `squash` : Fusionner avec le commit précédent
- `drop` : Supprimer le commit

**Exemple d'utilisation** :
```
pick abc1234 feat: ajoute formulaire
squash def5678 fix: corrige validation
squash ghi9012 fix: typo dans le formulaire
```

Résultat : Les 3 commits deviennent 1 seul commit propre.

---

### 3. Cherry-pick : Récupérer un commit spécifique

**Situation** : Vous voulez appliquer UN commit d'une branche dans une autre.

```bash
# Sur la branche où vous voulez appliquer le commit
git checkout main
git cherry-pick abc1234
```

**Utilité** :
- Appliquer un bugfix d'une branche à une autre
- Récupérer un commit utile sans merger toute la branche

---

### 4. Reset : Annuler des commits

**⚠️ Attention : reset réécrit l'historique !**

#### Soft reset (garde les changements)
```bash
git reset --soft HEAD~1
```

Les changements du dernier commit reviennent dans le staging.

#### Mixed reset (par défaut)
```bash
git reset HEAD~1
```

Les changements reviennent dans le working directory (non stagés).

#### Hard reset (supprime tout)
```bash
git reset --hard HEAD~1
```

**⚠️ Danger** : Supprime définitivement les changements !

**Usage** : Annuler le dernier commit en local (avant push).

---

### 5. Revert : Annuler un commit en créant un nouveau commit

**Contrairement à reset**, revert crée un nouveau commit qui annule les changements.

```bash
git revert abc1234
```

**Avantages** :
- ✅ N'efface pas l'historique
- ✅ Safe pour les commits déjà pushés
- ✅ Traçable (on voit qu'un commit a été annulé)

---

### 6. Reflog : L'historique des historiques

**reflog** enregistre TOUTES les modifications des branches (même les suppressions).

```bash
git reflog
```

**Utilité** : Récupérer des commits "perdus" après un reset ou une suppression.

**Exemple de récupération** :
```bash
# Vous avez fait un reset --hard par erreur
git reflog
# Vous voyez : abc1234 HEAD@{1}: commit: message important

# Récupérer ce commit
git reset --hard abc1234
```

---

## Le fichier .gitignore

### Qu'est-ce que .gitignore ?

Un fichier `.gitignore` indique à Git quels fichiers/dossiers **ne pas** tracker.

### Pourquoi ignorer des fichiers ?

**Fichiers à ignorer** :
- ✅ Fichiers générés (node_modules, dist, build)
- ✅ Fichiers de configuration locaux (.env, config.local.js)
- ✅ Fichiers système (.DS_Store, Thumbs.db)
- ✅ Logs et caches
- ✅ Fichiers sensibles (clés API, mots de passe)

### Créer un .gitignore

**À la racine du projet**, créez un fichier `.gitignore` :

```
# Dépendances
node_modules/
vendor/

# Fichiers de build
dist/
build/
*.min.js
*.min.css

# Fichiers de configuration
.env
.env.local
config.local.js

# Logs
logs/
*.log

# Fichiers système
.DS_Store
Thumbs.db
desktop.ini

# Éditeurs
.vscode/
.idea/
*.swp
*.swo

# Fichiers temporaires
tmp/
temp/
*.tmp
```

### Ignorer un fichier déjà tracké

Si vous avez déjà commité un fichier que vous voulez maintenant ignorer :

```bash
# Retirer du tracking sans supprimer
git rm --cached fichier.txt

# Ajouter à .gitignore
echo "fichier.txt" >> .gitignore

# Commit
git add .gitignore
git commit -m "chore: ajoute fichier.txt au gitignore"
```

### Templates .gitignore

GitHub propose des templates pour différents langages :
https://github.com/github/gitignore

**Exemple pour Node.js** :
```bash
curl https://raw.githubusercontent.com/github/gitignore/main/Node.gitignore > .gitignore
```

---

## Bonnes pratiques Git

### 1. Messages de commit clairs

**❌ Mauvais messages** :
```bash
git commit -m "fix"
git commit -m "mise à jour"
git commit -m "ça marche maintenant"
```

**✅ Bons messages** :
```bash
git commit -m "feat: ajoute le formulaire de contact avec validation"
git commit -m "fix: corrige le bug d'affichage du menu mobile"
git commit -m "refactor: simplifie la fonction de tri des produits"
```

#### Convention Conventional Commits

**Format** :
```
<type>(<scope>): <description>

[corps optionnel]

[footer optionnel]
```

**Types courants** :
- `feat`: Nouvelle fonctionnalité
- `fix`: Correction de bug
- `docs`: Documentation
- `style`: Formatage, style (pas de changement de code)
- `refactor`: Refactorisation
- `test`: Ajout/modification de tests
- `chore`: Tâches de maintenance

**Exemples** :
```bash
feat(auth): ajoute la connexion avec Google OAuth
fix(cart): corrige le calcul du total avec remise
docs(readme): ajoute les instructions d'installation
style(header): améliore l'espacement du menu
refactor(api): simplifie la gestion des erreurs
test(login): ajoute des tests pour le formulaire de login
chore(deps): met à jour les dépendances npm
```

---

### 2. Commits atomiques

**Un commit = Une modification logique**

**❌ Mauvais** :
```bash
git commit -m "fix: corrige plein de trucs"
```

Contient : 3 bugs fixés + 1 nouvelle fonctionnalité + du refactoring

**✅ Bon** :
```bash
git commit -m "fix: corrige le bug du menu mobile"
git commit -m "fix: corrige le calcul du prix total"
git commit -m "fix: corrige l'affichage des images sur Safari"
git commit -m "feat: ajoute le filtre par catégorie"
git commit -m "refactor: simplifie la fonction de tri"
```

**Avantages** :
- Plus facile de comprendre les changements
- Plus facile de revert un commit spécifique
- Meilleure traçabilité

---

### 3. Tirer (pull) avant de pousser (push)

**Toujours** récupérer les dernières modifications avant de pusher :

```bash
git pull
git push
```

Évite les conflits et les problèmes de synchronisation.

---

### 4. Ne pas commiter de secrets

**❌ JAMAIS commiter** :
- Clés API
- Mots de passe
- Tokens d'accès
- Certificats

**✅ À la place** :
- Variables d'environnement (fichier `.env`)
- Fichiers de configuration ignorés par Git
- Services de gestion de secrets (Vault, AWS Secrets Manager)

**Si vous avez commité un secret par erreur** :
1. Changer immédiatement le secret (régénérer la clé API)
2. Nettoyer l'historique Git (complexe, cherchez "git filter-branch")
3. Force push (si le repo est privé et que vous êtes seul)

---

### 5. Branches éphémères

**Supprimez les branches** une fois mergées :

```bash
# Localement
git branch -d feature/ma-branche

# Sur le remote
git push origin --delete feature/ma-branche
```

Garde le repository propre et lisible.

---

### 6. Utiliser des tags pour les versions

**Tags** = Marqueurs pour des points importants de l'historique (releases).

```bash
# Créer un tag
git tag v1.0.0

# Tag annoté (recommandé)
git tag -a v1.0.0 -m "Version 1.0.0 - Première release"

# Pousser les tags
git push origin v1.0.0
# Ou tous les tags
git push origin --tags

# Lister les tags
git tag

# Checkout un tag
git checkout v1.0.0
```

---

## Résolution de problèmes courants

### Problème 1 : J'ai commité sur la mauvaise branche

**Solution** :

```bash
# Noter le hash du commit (ex: abc1234)
git log

# Revenir en arrière sur cette branche
git reset --hard HEAD~1

# Aller sur la bonne branche
git checkout bonne-branche

# Appliquer le commit
git cherry-pick abc1234
```

---

### Problème 2 : J'ai fait un commit trop tôt

**Solution 1 : Ajouter des changements au dernier commit**
```bash
# Faire vos modifications
git add .
git commit --amend --no-edit
```

Le `--no-edit` garde le même message de commit.

**Solution 2 : Changer le message du dernier commit**
```bash
git commit --amend -m "Nouveau message"
```

**⚠️ Attention** : N'amend que si vous n'avez pas encore pushé !

---

### Problème 3 : Conflit complexe, je suis perdu

**Solutions** :

**Option 1 : Annuler le merge**
```bash
git merge --abort
```

**Option 2 : Utiliser un outil visuel**

```bash
git mergetool
```

Ouvre un éditeur visuel de résolution de conflits.

**Option 3 : Garder une version complète**

```bash
# Garder la version de main
git checkout --ours fichier.txt

# Garder la version de la branche
git checkout --theirs fichier.txt

# Puis
git add fichier.txt
git commit
```

---

### Problème 4 : J'ai pushé par erreur

**Si personne n'a encore pullé** :

```bash
git reset --hard HEAD~1
git push --force
```

**⚠️ Très dangereux si d'autres ont déjà pullé !**

**Solution safe** :
```bash
git revert HEAD
git push
```

Crée un commit qui annule le précédent.

---

### Problème 5 : Mon dépôt est devenu énorme

**Causes** :
- Gros fichiers binaires commités
- Historique très long

**Solutions** :

```bash
# Voir les gros fichiers
git rev-list --objects --all | sort -k 2 > allfileshas.txt

# Nettoyer les gros fichiers (avancé)
git filter-branch --tree-filter 'rm -rf gros-dossier' HEAD
```

**Mieux** : Utiliser Git LFS (Large File Storage) pour les gros fichiers.

---

## Outils et interfaces graphiques

### Interfaces en ligne de commande améliorées

#### 1. tig
Terminal interface pour Git. Navigation intuitive dans l'historique.

```bash
brew install tig  # Mac
apt install tig   # Linux
```

#### 2. lazygit
Interface terminale très visuelle et interactive.

```bash
brew install lazygit
```

---

### Interfaces graphiques (GUI)

#### 1. GitKraken
- Interface moderne et intuitive
- Visualisation claire des branches
- Gratuit pour usage non-commercial

#### 2. SourceTree
- Par Atlassian (créateurs de Bitbucket)
- Gratuit
- Windows et Mac

#### 3. GitHub Desktop
- Officiel GitHub
- Simple et épuré
- Idéal pour débutants

#### 4. VS Code (intégré)
- Extension Git Graph (très recommandée)
- Interface Git native de VS Code
- Source Control panel

**Recommandation** : Apprenez d'abord la ligne de commande, puis utilisez une GUI pour visualiser.

---

## Collaborer efficacement

### 1. Communication claire

**Dans les Pull Requests** :
- Description détaillée
- Screenshots si UI
- Liste de ce qui a été fait
- Liste de ce qui reste à faire

**Dans les commits** :
- Messages clairs et explicites
- Références aux issues (#42, closes #15)

---

### 2. Revue de code constructive

**En tant que reviewer** :
- Soyez respectueux et constructif
- Expliquez le "pourquoi" de vos suggestions
- Reconnaissez le bon travail

**Exemple de bon commentaire** :
```
Bonne idée d'extraire cette logique dans une fonction séparée !
Pour encore améliorer la lisibilité, que penses-tu de renommer
`data` en `userProfile` ? Ça rendrait l'intention plus claire.
```

**Exemple de mauvais commentaire** :
```
Ce code est nul, refais-le.
```

---

### 3. Gestion des issues

**Lier commits et issues** :
```bash
git commit -m "fix: corrige le bug de connexion (fixes #42)"
```

Quand le commit est mergé dans main, l'issue #42 se ferme automatiquement.

**Mots-clés GitHub** :
- `fixes #42`
- `closes #42`
- `resolves #42`

---

### 4. Templates de Pull Request

Créez un fichier `.github/PULL_REQUEST_TEMPLATE.md` :

```markdown
## Description
<!-- Décrivez vos changements -->

## Type de changement
- [ ] Bug fix
- [ ] Nouvelle fonctionnalité
- [ ] Breaking change
- [ ] Documentation

## Checklist
- [ ] Mon code suit le style du projet
- [ ] J'ai commenté les parties complexes
- [ ] J'ai testé mes changements
- [ ] J'ai mis à jour la documentation
- [ ] Aucune nouvelle alerte ESLint

## Screenshots
<!-- Si pertinent -->
```

GitHub l'utilisera automatiquement lors de la création de PR.

---

## Récapitulatif : Workflow complet d'équipe

### Jour 1 : Nouvelle fonctionnalité

```bash
# 1. Synchroniser avec main
git checkout main
git pull origin main

# 2. Créer une branche
git checkout -b feature/ajout-panier

# 3. Développer
# ... modifications ...
git add .
git commit -m "feat(cart): ajoute la structure du panier"

# ... modifications ...
git add .
git commit -m "feat(cart): ajoute l'ajout de produits"

# ... modifications ...
git add .
git commit -m "feat(cart): ajoute le calcul du total"

# 4. Pousser régulièrement
git push -u origin feature/ajout-panier
```

### Jour 2 : Finalisation et PR

```bash
# 5. Synchroniser avec main (au cas où)
git checkout main
git pull origin main
git checkout feature/ajout-panier
git merge main
# Résoudre les conflits si nécessaire

# 6. Derniers commits
git add .
git commit -m "feat(cart): ajoute le bouton de suppression"

git push origin feature/ajout-panier

# 7. Sur GitHub : Créer la Pull Request
# ... revue par l'équipe ...
```

### Jour 3 : Après approbation

```bash
# 8. Merge de la PR sur GitHub

# 9. Localement : Nettoyer
git checkout main
git pull origin main
git branch -d feature/ajout-panier

# 10. Passer à la prochaine fonctionnalité
git checkout -b feature/page-commande
```

---

## Ressources et aide

### Documentation officielle
- **Git Book** : https://git-scm.com/book/fr/v2
- **GitHub Docs** : https://docs.github.com/

### Apprendre de manière interactive
- **Learn Git Branching** : https://learngitbranching.js.org/?locale=fr_FR (très recommandé !)
- **GitHub Skills** : https://skills.github.com/

### Cheat sheets
- **Git Cheat Sheet officiel** : https://training.github.com/downloads/github-git-cheat-sheet/
- **Atlassian Git Cheatsheet** : https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet

### Aide communautaire
- **Stack Overflow** : Tag [git]
- **Reddit** : r/git
- **Discord** : Serveurs de développeurs

### En cas de problème
**Site : Oh Shit, Git!?!** : https://ohshitgit.com/
Solutions aux erreurs Git courantes en langage simple.

---

## Conclusion

Git est un outil puissant qui peut sembler complexe au début, mais qui devient indispensable une fois maîtrisé.

**Les points clés à retenir** :

- ✅ **Branches** : Développez chaque fonctionnalité sur une branche séparée
- ✅ **Commits atomiques** : Un commit = une modification logique
- ✅ **Messages clairs** : Utilisez la convention Conventional Commits
- ✅ **Pull Requests** : Revue de code systématique avant merge
- ✅ **Synchronisation** : Pull régulièrement pour éviter les conflits
- ✅ **Gitignore** : Ne commitez jamais de fichiers sensibles ou générés

**Progression recommandée** :

1. **Semaine 1-2** : Maîtriser les branches et les merges basiques
2. **Semaine 3-4** : Créer des Pull Requests, participer à des revues
3. **Mois 2** : Gérer les conflits avec confiance
4. **Mois 3+** : Utiliser rebase, cherry-pick, stash selon les besoins

**Conseil final** : La meilleure façon d'apprendre Git est de l'utiliser dans de vrais projets. Commencez petit, expérimentez, faites des erreurs (c'est pour ça que Git existe !), et vous progresserez rapidement.

Git est comme la conduite : au début, vous devez penser à chaque commande. Après quelques semaines, ça devient naturel. Vous ne pensez plus "je vais créer une branche, faire un commit, pousser", vous le faites automatiquement. 🚀

---


⏭️ [Écosystème JavaScript Moderne](/08-ecosysteme-javascript-moderne/README.md)
