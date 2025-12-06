🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.2 - addEventListener : la méthode moderne 🆕

## Introduction

Maintenant que vous comprenez le principe des événements, il est temps d'apprendre **comment** les gérer concrètement en JavaScript. Il existe plusieurs façons de le faire, mais **`addEventListener()`** est la méthode moderne et recommandée.

> **Important** : Les anciennes méthodes (`onclick`, `onmouseover`, etc.) sont aujourd'hui considérées comme obsolètes. Nous les aborderons pour que vous puissiez les reconnaître dans du code ancien, mais vous devez **toujours** utiliser `addEventListener()` dans vos projets.

## Syntaxe de addEventListener()

La syntaxe de base est simple et se compose de trois parties :

```javascript
element.addEventListener(typeEvenement, fonctionGestionnaire);
```

### Décomposition :

1. **`element`** : l'élément HTML que vous voulez surveiller
2. **`typeEvenement`** : le nom de l'événement (entre guillemets)
3. **`fonctionGestionnaire`** : la fonction à exécuter quand l'événement se produit

## Premier exemple simple

Créons un bouton qui affiche une alerte quand on clique dessus.

### HTML
```html
<button id="monBouton">Cliquez-moi !</button>
```

### JavaScript
```javascript
// 1. Sélectionner l'élément
const bouton = document.getElementById('monBouton');

// 2. Définir la fonction qui sera exécutée
function afficherAlerte() {
    alert('Vous avez cliqué sur le bouton !');
}

// 3. Attacher l'événement
bouton.addEventListener('click', afficherAlerte);
```

### ⚠️ Points importants :
- Le nom de l'événement est **entre guillemets** : `'click'`
- Le nom de la fonction est **sans parenthèses** : `afficherAlerte` (pas `afficherAlerte()`)
- Si vous mettez les parenthèses, la fonction s'exécutera immédiatement !

## Les anciennes méthodes (à éviter)

Avant `addEventListener()`, on utilisait deux méthodes aujourd'hui dépréciées.

### ❌ Méthode 1 : Attribut HTML onclick (très déconseillé)

```html
<!-- NE FAITES PAS ÇA -->
<button onclick="alert('Clic!')">Cliquez-moi</button>
```

**Pourquoi c'est mauvais :**
- Mélange HTML et JavaScript (violation de la séparation des préoccupations)
- Difficile à maintenir
- Code JavaScript dans le HTML = mauvaise pratique

### ❌ Méthode 2 : Propriété onclick en JavaScript (déprécié)

```javascript
// NE FAITES PAS ÇA
const bouton = document.getElementById('monBouton');
bouton.onclick = function() {
    alert('Clic!');
};
```

**Pourquoi c'est mauvais :**
- On ne peut attacher qu'**un seul** gestionnaire d'événement
- Si vous en ajoutez un second, il écrase le premier

```javascript
// Le deuxième écrase le premier !
bouton.onclick = fonction1;  // ← sera écrasé
bouton.onclick = fonction2;  // ← seul celui-ci restera
```

## Pourquoi addEventListener() est meilleur ?

### ✅ Avantage 1 : Plusieurs gestionnaires sur le même élément

Vous pouvez attacher plusieurs fonctions au même événement :

```javascript
const bouton = document.getElementById('monBouton');

function fonction1() {
    console.log('Première fonction');
}

function fonction2() {
    console.log('Deuxième fonction');
}

// Les DEUX fonctions seront exécutées
bouton.addEventListener('click', fonction1);
bouton.addEventListener('click', fonction2);
```

**Résultat au clic :**
```
Première fonction
Deuxième fonction
```

### ✅ Avantage 2 : Séparation HTML/JavaScript

Le HTML reste propre, tout le JavaScript est dans un fichier séparé :

```html
<!-- HTML propre, sans JavaScript -->
<button id="monBouton">Cliquez-moi</button>
```

```javascript
// Tout le JavaScript dans un fichier .js
const bouton = document.getElementById('monBouton');
bouton.addEventListener('click', maFonction);
```

### ✅ Avantage 3 : Possibilité de retirer l'événement

Vous pouvez retirer un gestionnaire d'événement avec `removeEventListener()` :

```javascript
function direBonjour() {
    console.log('Bonjour !');
}

// Ajouter
bouton.addEventListener('click', direBonjour);

// Retirer plus tard
bouton.removeEventListener('click', direBonjour);
```

### ✅ Avantage 4 : Options avancées

`addEventListener()` permet de passer un troisième paramètre optionnel pour des comportements avancés (nous verrons ça plus tard).

## Différentes façons d'écrire la fonction gestionnaire

Il existe plusieurs syntaxes pour définir la fonction qui sera exécutée.

### 1. Fonction nommée (recommandé pour la réutilisabilité)

```javascript
const bouton = document.getElementById('monBouton');

function afficherMessage() {
    console.log('Bouton cliqué !');
}

bouton.addEventListener('click', afficherMessage);
```

**Avantage** : La fonction peut être réutilisée et facilement retirée.

### 2. Fonction anonyme

```javascript
const bouton = document.getElementById('monBouton');

bouton.addEventListener('click', function() {
    console.log('Bouton cliqué !');
});
```

**Inconvénient** : Impossible de retirer l'événement plus tard car la fonction n'a pas de nom.

### 3. Fonction fléchée (syntaxe moderne ES6)

```javascript
const bouton = document.getElementById('monBouton');

bouton.addEventListener('click', () => {
    console.log('Bouton cliqué !');
});
```

**Note** : Les fonctions fléchées ont un comportement différent avec le mot-clé `this` (nous verrons ça plus tard).

## Exemples pratiques courants

### Exemple 1 : Changer le texte d'un élément

```html
<button id="btnChanger">Changer le texte</button>
<p id="texte">Texte original</p>
```

```javascript
const bouton = document.getElementById('btnChanger');
const paragraphe = document.getElementById('texte');

bouton.addEventListener('click', () => {
    paragraphe.textContent = 'Le texte a changé !';
});
```

### Exemple 2 : Ajouter/retirer une classe CSS

```html
<button id="btnToggle">Basculer la couleur</button>
<div id="boite" class="boite">Ma boîte</div>
```

```css
.boite {
    background-color: lightblue;
    padding: 20px;
}

.rouge {
    background-color: lightcoral;
}
```

```javascript
const bouton = document.getElementById('btnToggle');
const boite = document.getElementById('boite');

bouton.addEventListener('click', () => {
    boite.classList.toggle('rouge');
});
```

### Exemple 3 : Compter les clics

```html
<button id="btnCompter">Cliquez-moi</button>
<p>Nombre de clics : <span id="compteur">0</span></p>
```

```javascript
const bouton = document.getElementById('btnCompter');
const compteur = document.getElementById('compteur');
let nombreClics = 0;

bouton.addEventListener('click', () => {
    nombreClics++;
    compteur.textContent = nombreClics;
});
```

### Exemple 4 : Plusieurs éléments, même événement

```html
<button class="btn">Bouton 1</button>
<button class="btn">Bouton 2</button>
<button class="btn">Bouton 3</button>
```

```javascript
// Sélectionner tous les boutons
const boutons = document.querySelectorAll('.btn');

// Fonction à exécuter
function direBonjour() {
    console.log('Bonjour !');
}

// Attacher l'événement à chaque bouton
boutons.forEach(bouton => {
    bouton.addEventListener('click', direBonjour);
});
```

## L'objet Event

Quand un événement se déclenche, JavaScript crée automatiquement un **objet Event** qui contient des informations sur l'événement. Vous pouvez y accéder en l'acceptant comme paramètre dans votre fonction :

```javascript
const bouton = document.getElementById('monBouton');

bouton.addEventListener('click', function(event) {
    console.log(event); // Affiche l'objet Event
    console.log(event.type); // Affiche "click"
    console.log(event.target); // Affiche l'élément cliqué
});
```

### Avec une fonction fléchée :

```javascript
bouton.addEventListener('click', (event) => {
    console.log('Type d\'événement :', event.type);
    console.log('Élément cliqué :', event.target);
});
```

> **Note** : Par convention, on appelle souvent ce paramètre `event`, `e`, ou `evt`. Tous ces noms sont valides.

## Noms d'événements courants

Voici les événements que vous utiliserez le plus souvent avec `addEventListener()` :

### Événements de souris
```javascript
element.addEventListener('click', fonction);        // Clic
element.addEventListener('dblclick', fonction);     // Double-clic
element.addEventListener('mouseenter', fonction);   // Souris entre
element.addEventListener('mouseleave', fonction);   // Souris sort
element.addEventListener('mousemove', fonction);    // Souris bouge
```

### Événements de clavier
```javascript
element.addEventListener('keydown', fonction);      // Touche enfoncée
element.addEventListener('keyup', fonction);        // Touche relâchée
```

### Événements de formulaire
```javascript
element.addEventListener('submit', fonction);       // Formulaire soumis
element.addEventListener('input', fonction);        // Valeur change
element.addEventListener('change', fonction);       // Change + perd focus
element.addEventListener('focus', fonction);        // Reçoit le focus
element.addEventListener('blur', fonction);         // Perd le focus
```

### Événements de document/fenêtre
```javascript
document.addEventListener('DOMContentLoaded', fonction); // DOM chargé
window.addEventListener('load', fonction);               // Page chargée
window.addEventListener('scroll', fonction);             // Défilement
window.addEventListener('resize', fonction);             // Redimensionnement
```

## Erreurs fréquentes à éviter

### ❌ Erreur 1 : Mettre des parenthèses après le nom de fonction

```javascript
// FAUX - la fonction s'exécute immédiatement
bouton.addEventListener('click', maFonction());

// CORRECT - on passe la référence de la fonction
bouton.addEventListener('click', maFonction);
```

### ❌ Erreur 2 : Oublier les guillemets autour du type d'événement

```javascript
// FAUX
bouton.addEventListener(click, maFonction);

// CORRECT
bouton.addEventListener('click', maFonction);
```

### ❌ Erreur 3 : Essayer d'attacher un événement avant que l'élément existe

```javascript
// FAUX - le bouton n'existe pas encore dans le DOM
const bouton = document.getElementById('monBouton');
bouton.addEventListener('click', maFonction);
```

**Solutions :**
1. Mettre votre script à la fin du `<body>`
2. Ou utiliser `DOMContentLoaded` :

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const bouton = document.getElementById('monBouton');
    bouton.addEventListener('click', maFonction);
});
```

### ❌ Erreur 4 : Utiliser les anciennes méthodes

```javascript
// FAUX - méthode dépréciée
bouton.onclick = maFonction;

// CORRECT - méthode moderne
bouton.addEventListener('click', maFonction);
```

## Bonnes pratiques

### ✅ 1. Toujours utiliser addEventListener()

```javascript
// ✅ BIEN
bouton.addEventListener('click', maFonction);

// ❌ ÉVITER
bouton.onclick = maFonction;
```

### ✅ 2. Utiliser des fonctions nommées pour les gestionnaires réutilisables

```javascript
// ✅ BIEN - fonction nommée, réutilisable
function validerFormulaire() {
    // Code de validation
}
formulaire.addEventListener('submit', validerFormulaire);

// ✅ ACCEPTABLE - fonction anonyme pour du code simple et unique
bouton.addEventListener('click', () => {
    console.log('Clic unique');
});
```

### ✅ 3. Regrouper les événements dans une fonction d'initialisation

```javascript
function initialiserEvenements() {
    const bouton1 = document.getElementById('btn1');
    const bouton2 = document.getElementById('btn2');

    bouton1.addEventListener('click', fonction1);
    bouton2.addEventListener('click', fonction2);
}

// Appeler quand le DOM est prêt
document.addEventListener('DOMContentLoaded', initialiserEvenements);
```

### ✅ 4. Vérifier que l'élément existe avant d'attacher un événement

```javascript
const bouton = document.getElementById('monBouton');

if (bouton) {
    bouton.addEventListener('click', maFonction);
} else {
    console.error('Le bouton n\'existe pas !');
}
```

## Tableau récapitulatif : Anciennes VS nouvelles méthodes

| Critère | onclick (❌ déprécié) | addEventListener() (✅ moderne) |
|---------|----------------------|--------------------------------|
| **Plusieurs gestionnaires** | Non (écrasement) | Oui |
| **Retrait possible** | Difficile | Facile avec `removeEventListener()` |
| **Séparation HTML/JS** | Non | Oui |
| **Options avancées** | Non | Oui |
| **Compatibilité** | Anciens navigateurs | Tous les navigateurs modernes |
| **Recommandé en 2025** | ❌ Non | ✅ Oui |

## Ce qu'il faut retenir

✅ **`addEventListener()`** est la méthode moderne pour gérer les événements

✅ **Syntaxe** : `element.addEventListener('typeEvenement', fonctionGestionnaire)`

✅ **Ne pas mettre de parenthèses** après le nom de fonction : `maFonction` et non `maFonction()`

✅ **Plusieurs gestionnaires possibles** sur le même élément avec addEventListener()

✅ **Les anciennes méthodes** (onclick, onmouseover, etc.) sont dépréciées

✅ **L'objet Event** est automatiquement passé à la fonction gestionnaire

✅ **Vérifier que l'élément existe** avant d'attacher un événement

## Dans la prochaine leçon

Maintenant que vous savez utiliser `addEventListener()`, nous allons explorer en détail les **événements de souris** : click, dblclick, mouseover, mouseout, et bien d'autres.

Vous découvrirez :
- Les différents types d'événements de souris
- Comment détecter la position de la souris
- Les différences entre mouseover/mouseout et mouseenter/mouseleave
- Des exemples pratiques d'interactions

---


⏭️ [Événements de souris : click, dblclick, mouseover, mouseout, mouseenter, mouseleave](/05-javascript-moderne-fondamentaux/10-evenements/03-evenements-souris.md)
