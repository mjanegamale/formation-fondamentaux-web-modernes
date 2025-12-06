🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.1 - Principe des événements

## Introduction

Les **événements** sont au cœur de l'interactivité sur le web. Sans événements, une page web serait complètement statique : impossible de cliquer sur un bouton, de remplir un formulaire, ou de faire défiler une galerie d'images.

Un événement est simplement **quelque chose qui se passe** dans le navigateur ou sur la page web. Cela peut être une action de l'utilisateur (clic, frappe au clavier) ou un événement du navigateur lui-même (page chargée, image affichée).

## Qu'est-ce qu'un événement ?

Un événement est un **signal** que quelque chose s'est produit. Voici quelques exemples d'événements courants :

- **L'utilisateur clique** sur un bouton → événement `click`
- **L'utilisateur tape** au clavier → événement `keydown` ou `keyup`
- **La souris passe** au-dessus d'un élément → événement `mouseover`
- **Un formulaire est soumis** → événement `submit`
- **La page a fini de charger** → événement `load`

### Exemple du monde réel

Pensez à une sonnette de porte :
1. **L'événement** : quelqu'un appuie sur le bouton
2. **La réaction** : la sonnette produit un son

En JavaScript, c'est exactement le même principe :
1. **L'événement** : l'utilisateur clique sur un bouton
2. **La réaction** : on exécute du code JavaScript

## Le modèle événementiel

Le fonctionnement des événements repose sur un modèle simple en trois parties :

### 1. La cible (target)

C'est **l'élément HTML** sur lequel l'événement se produit. Par exemple :
- Un bouton qu'on clique
- Une zone de texte dans laquelle on tape
- Une image sur laquelle on passe la souris

### 2. Le type d'événement

C'est **le nom de l'événement** qui nous intéresse :
- `click` pour un clic
- `keydown` pour une touche enfoncée
- `submit` pour la soumission d'un formulaire
- etc.

### 3. Le gestionnaire d'événement (event handler)

C'est **la fonction JavaScript** qui sera exécutée quand l'événement se produit. On l'appelle aussi "écouteur d'événement" (event listener).

## Schéma conceptuel

```

  UTILISATEUR
  ↓
  Action (clic, frappe clavier, etc.)
  ↓
  NAVIGATEUR détecte l'événement
  ↓
  Déclenche le GESTIONNAIRE D'ÉVÉNEMENT
  ↓
  FONCTION JAVASCRIPT s'exécute
  ↓
  RÉACTION visible (changement de couleur, etc.)

```

## Exemple simple et concret

Imaginons qu'on veuille afficher un message quand l'utilisateur clique sur un bouton.

### Le HTML
```html
<button id="monBouton">Cliquez-moi !</button>
<p id="message"></p>
```

### Le JavaScript (on verra la syntaxe exacte dans les prochaines leçons)
```javascript
// 1. On sélectionne le bouton (la cible)
const bouton = document.getElementById('monBouton');

// 2. On définit ce qui doit se passer (le gestionnaire)
function afficherMessage() {
    const paragraphe = document.getElementById('message');
    paragraphe.textContent = 'Vous avez cliqué sur le bouton !';
}

// 3. On "écoute" l'événement click sur le bouton
bouton.addEventListener('click', afficherMessage);
```

### Ce qui se passe :
1. JavaScript surveille le bouton
2. Quand l'utilisateur clique (événement `click`)
3. La fonction `afficherMessage` s'exécute automatiquement
4. Le message apparaît dans le paragraphe

## Pourquoi c'est puissant ?

Les événements permettent de créer des **interactions riches** :

### Pages statiques VS pages interactives

**Sans événements (page statique)** :
- Le contenu ne change jamais
- Aucune réaction aux actions de l'utilisateur
- Expérience limitée

**Avec événements (page interactive)** :
- Menus qui s'ouvrent au clic
- Formulaires qui valident les données en temps réel
- Galeries d'images qui changent
- Animations déclenchées par l'utilisateur
- Et bien plus encore !

## Types d'événements principaux

Voici les grandes familles d'événements que vous rencontrerez :

### Événements de souris
- `click` : clic sur un élément
- `dblclick` : double-clic
- `mouseover` : souris entre dans un élément
- `mouseout` : souris sort d'un élément
- `mousemove` : souris bouge sur un élément

### Événements de clavier
- `keydown` : touche enfoncée
- `keyup` : touche relâchée
- `keypress` : touche pressée (déprécié, utilisez `keydown`)

### Événements de formulaire
- `submit` : formulaire soumis
- `input` : valeur d'un champ modifiée
- `change` : valeur d'un champ modifiée et élément perd le focus
- `focus` : champ reçoit le focus
- `blur` : champ perd le focus

### Événements de document
- `DOMContentLoaded` : le HTML est chargé et analysé
- `load` : toute la page (images incluses) est chargée
- `scroll` : l'utilisateur fait défiler la page
- `resize` : la fenêtre du navigateur est redimensionnée

## Le cycle de vie d'un événement

Voici ce qui se passe dans le navigateur quand un événement est déclenché :

```
1. L'utilisateur effectue une action
   ↓
2. Le navigateur crée un "objet Event"
   (contient toutes les infos sur l'événement)
   ↓
3. Le navigateur cherche s'il y a un gestionnaire d'événement
   ↓
4. Si oui, il exécute la fonction associée
   ↓
5. La fonction peut accéder à l'objet Event
   pour avoir des détails (position de la souris, touche pressée, etc.)
```

## Programmation événementielle

Cette façon de programmer s'appelle la **programmation événementielle** ou **event-driven programming** :

- On ne contrôle pas l'ordre exact d'exécution du code
- On **réagit** aux actions de l'utilisateur
- Le code attend passivement qu'un événement se produise
- C'est le navigateur qui décide **quand** exécuter nos fonctions

### Analogie
C'est comme un gardien de but au football :
- Il ne sait pas **quand** le ballon va arriver
- Il ne sait pas **d'où** il va venir
- Mais il est **prêt à réagir** dès que ça arrive

En JavaScript :
- Vous ne savez pas **quand** l'utilisateur va cliquer
- Vous ne savez pas **sur quoi** exactement
- Mais votre code est **prêt à réagir** grâce aux événements

## Vocabulaire important

Avant de continuer, assurons-nous de bien comprendre ces termes :

| Terme | Définition | Exemple |
|-------|------------|---------|
| **Événement** | Signal qu'quelque chose s'est produit | Un clic de souris |
| **Gestionnaire d'événement** | Fonction qui s'exécute quand l'événement se produit | `function onClick() { ... }` |
| **Écouteur d'événement** | Mécanisme qui surveille un événement | `addEventListener()` |
| **Cible (target)** | L'élément sur lequel l'événement s'est produit | Le bouton cliqué |
| **Type d'événement** | Le nom de l'événement | `click`, `keydown`, etc. |

## Avantages des événements

### 1. Séparation des préoccupations
Le HTML reste du HTML, le JavaScript reste du JavaScript. On ne mélange pas tout.

### 2. Réutilisabilité
Une même fonction peut gérer plusieurs événements sur plusieurs éléments.

### 3. Flexibilité
On peut ajouter ou retirer des écouteurs d'événements dynamiquement.

### 4. Performance
Le code ne s'exécute que quand nécessaire (quand l'événement se produit).

## Ce qu'il faut retenir

✅ **Un événement est un signal** que quelque chose s'est produit dans le navigateur

✅ **Les événements rendent les pages interactives** en permettant de réagir aux actions de l'utilisateur

✅ **On utilise des gestionnaires d'événements** (fonctions JavaScript) pour définir ce qui doit se passer

✅ **La programmation événementielle** signifie que notre code réagit aux événements plutôt que de s'exécuter de manière linéaire

✅ **Il existe de nombreux types d'événements** : souris, clavier, formulaire, document, etc.

## Dans la prochaine leçon

Maintenant que vous comprenez le **principe** des événements, nous allons voir dans la leçon suivante comment **concrètement** écouter et gérer les événements avec la méthode moderne `addEventListener()`.

Vous apprendrez :
- La syntaxe exacte pour attacher un événement
- Comment passer des paramètres
- Pourquoi `addEventListener` est meilleur que les anciennes méthodes
- Des exemples pratiques complets

---


⏭️ [addEventListener : la méthode moderne (onclick déprécié)](/05-javascript-moderne-fondamentaux/10-evenements/02-addeventlistener.md)
