🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.1 - Comprendre le DOM

## Introduction

Vous avez appris à écrire du HTML pour structurer vos pages web et du CSS pour les styliser. Maintenant, avec JavaScript, vous allez pouvoir rendre vos pages **interactives** et **dynamiques**. Pour cela, vous devez comprendre un concept fondamental : le **DOM**.

---

## Qu'est-ce que le DOM ?

Le **DOM** (Document Object Model, ou Modèle d'Objet de Document en français) est une représentation de votre page HTML que JavaScript peut comprendre et manipuler.

### Définition simple

> Le DOM est comme une carte détaillée de votre page web que JavaScript peut lire et modifier en temps réel.

Quand vous chargez une page HTML dans votre navigateur, celui-ci ne se contente pas d'afficher le code. Il **transforme** votre HTML en une structure organisée appelée le DOM, que JavaScript peut ensuite manipuler.

---

## Pourquoi le DOM est-il nécessaire ?

Sans le DOM, JavaScript ne pourrait pas interagir avec votre page web. Voici quelques exemples de ce que vous pouvez faire grâce au DOM :

- ✅ Changer le texte d'un élément après un clic
- ✅ Ajouter ou supprimer des éléments de la page
- ✅ Modifier les styles CSS dynamiquement
- ✅ Réagir aux actions de l'utilisateur (clics, saisies, survols...)
- ✅ Créer des animations et des effets interactifs
- ✅ Valider des formulaires avant soumission

**En résumé :** Le DOM est le pont entre votre HTML et JavaScript.

---

## Comment fonctionne le DOM ?

### 1. Le navigateur crée le DOM

Lorsque votre navigateur charge une page HTML, il suit ces étapes :

1. **Lecture du code HTML** - Le navigateur lit votre fichier HTML ligne par ligne
2. **Parsing** - Il analyse et comprend la structure du code
3. **Construction du DOM** - Il crée une représentation en mémoire sous forme d'arbre
4. **Affichage** - Il utilise ce DOM pour afficher la page à l'écran

### 2. JavaScript accède au DOM

Une fois le DOM créé, JavaScript peut :
- Le **lire** (récupérer des informations)
- Le **modifier** (changer du contenu)
- **Écouter** les événements (réagir aux actions utilisateur)

---

## La structure en arbre du DOM

Le DOM organise votre page HTML comme un **arbre généalogique**. C'est une analogie très importante à comprendre !

### Exemple de code HTML simple

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Ma page</title>
  </head>
  <body>
    <h1>Bienvenue</h1>
    <p>Ceci est un paragraphe.</p>
  </body>
</html>
```

### Représentation en arbre

Voici comment le navigateur voit cette structure :

```
Document
  └── html
       ├── head
       │    └── title
       │         └── "Ma page"
       └── body
            ├── h1
            │    └── "Bienvenue"
            └── p
                 └── "Ceci est un paragraphe."
```

### Vocabulaire de l'arbre DOM

Pour parler du DOM, on utilise un vocabulaire inspiré des arbres généalogiques :

- **Nœud (Node)** : Chaque élément de l'arbre (balise HTML, texte, commentaire...)
- **Nœud parent** : L'élément qui en contient d'autres
- **Nœud enfant** : Un élément contenu dans un autre
- **Nœuds frères (siblings)** : Éléments au même niveau, ayant le même parent
- **Nœud racine** : L'élément `<html>`, tout en haut de l'arbre

### Exemple avec relations familiales

```html
<div id="parent">
  <p>Premier paragraphe</p>
  <p>Deuxième paragraphe</p>
</div>
```

Dans cet exemple :
- Le `<div>` est le **parent**
- Les deux `<p>` sont les **enfants** du `<div>`
- Les deux `<p>` sont **frères** entre eux

---

## Types de nœuds dans le DOM

Le DOM contient différents types de nœuds. Les plus courants sont :

### 1. Nœuds d'éléments (Element nodes)

Ce sont les balises HTML elles-mêmes : `<div>`, `<p>`, `<h1>`, `<img>`, etc.

```html
<h1>Titre</h1>  <!-- Nœud d'élément -->
```

### 2. Nœuds de texte (Text nodes)

Le contenu textuel à l'intérieur des éléments :

```html
<p>Ceci est du texte</p>  <!-- "Ceci est du texte" est un nœud de texte -->
```

**Important :** Le texte à l'intérieur d'une balise est considéré comme un enfant de cette balise !

### 3. Nœuds de commentaires

Les commentaires HTML font aussi partie du DOM :

```html
<!-- Ceci est un commentaire -->  <!-- Nœud de commentaire -->
```

### 4. Le nœud Document

C'est le point d'entrée de tout le DOM. En JavaScript, on y accède via l'objet `document`.

---

## L'objet `document` : votre porte d'entrée

En JavaScript, vous interagissez avec le DOM via l'objet global **`document`**.

### Essayez dans la console !

Ouvrez la console de votre navigateur (F12) et tapez :

```javascript
console.log(document);
```

Vous verrez l'intégralité de votre page HTML sous forme d'objet JavaScript !

### Autres propriétés utiles

```javascript
// Récupérer le titre de la page
console.log(document.title);

// Récupérer l'URL de la page
console.log(document.URL);

// Récupérer l'élément <body>
console.log(document.body);

// Récupérer l'élément <html>
console.log(document.documentElement);
```

---

## Visualiser le DOM dans les DevTools

Les DevTools de votre navigateur vous permettent de voir le DOM en temps réel.

### Comment accéder à l'inspecteur DOM :

1. **Clic droit** sur n'importe quel élément de la page
2. Sélectionnez **"Inspecter"** ou **"Inspecter l'élément"**
3. L'onglet **"Éléments"** (Chrome/Edge) ou **"Inspecteur"** (Firefox) s'ouvre

### Ce que vous pouvez faire :

- 🔍 **Explorer** la structure en arbre du DOM
- 📝 **Modifier** le HTML et le CSS en direct (temporairement)
- 👁️ **Voir** les styles CSS appliqués à chaque élément
- 🎯 **Survoler** un élément dans le DOM pour le mettre en évidence sur la page
- ❌ **Supprimer** temporairement des éléments pour tester

**Astuce :** Toutes les modifications dans l'inspecteur sont temporaires. Rafraîchir la page annule tout.

---

## DOM vs HTML : quelle est la différence ?

C'est une question importante que se posent souvent les débutants !

### Le code HTML
- C'est le **code source** que vous écrivez
- C'est un fichier texte statique
- Il ne change pas (sauf si vous le modifiez manuellement)

### Le DOM
- C'est la **représentation en mémoire** créée par le navigateur
- C'est une structure dynamique et interactive
- JavaScript peut le modifier à tout moment
- Il peut être différent du HTML initial

### Exemple concret

**HTML initial :**
```html
<div id="message">Bonjour</div>
```

**JavaScript modifie le DOM :**
```javascript
document.getElementById('message').textContent = 'Hello';
```

**Résultat affiché :** "Hello"

➡️ Le fichier HTML n'a pas changé, mais le DOM (et donc ce que vous voyez) a été modifié !

---

## Le DOM est dynamique et "vivant"

Une caractéristique essentielle du DOM : il est **vivant** (live).

### Qu'est-ce que cela signifie ?

Quand vous récupérez une collection d'éléments via le DOM, cette collection se met à jour automatiquement si le DOM change.

### Exemple conceptuel

Imaginez que vous récupérez tous les paragraphes de la page :

```javascript
// On récupère tous les <p>
let paragraphes = document.getElementsByTagName('p');
console.log(paragraphes.length); // Affiche : 3

// JavaScript ajoute un nouveau paragraphe
// ...

console.log(paragraphes.length); // Affiche maintenant : 4
```

La collection `paragraphes` s'est mise à jour automatiquement !

---

## Analogie pour mieux comprendre

Imaginez le DOM comme un **immeuble** :

- 🏢 **L'immeuble entier** = Le document HTML complet
- 🚪 **Chaque appartement** = Un élément HTML (div, p, h1...)
- 👨‍👩‍👧‍👦 **Les habitants** = Le contenu (texte, images...)
- 🔑 **Vous avez les clés** = JavaScript peut accéder à tout
- 🔨 **Vous pouvez rénover** = Modifier la structure, ajouter/supprimer des pièces
- 📋 **Le plan de l'immeuble** = La structure en arbre du DOM

---

## Points clés à retenir

✅ Le **DOM** est une représentation de votre HTML que JavaScript peut manipuler

✅ Le navigateur **crée automatiquement** le DOM quand il charge une page

✅ Le DOM est structuré comme un **arbre** avec des relations parent-enfant

✅ L'objet **`document`** est votre point d'entrée pour accéder au DOM

✅ Le DOM est **dynamique** : vous pouvez le modifier en temps réel avec JavaScript

✅ Le **HTML** est le code source, le **DOM** est sa représentation vivante en mémoire

✅ Les **DevTools** vous permettent d'explorer et de manipuler le DOM visuellement

---

## Ce qui vient ensuite

Maintenant que vous comprenez ce qu'est le DOM, vous allez apprendre à :

1. **Sélectionner** des éléments dans le DOM
2. **Lire** leur contenu et leurs attributs
3. **Modifier** leur contenu, leurs styles et leurs attributs
4. **Créer** de nouveaux éléments
5. **Supprimer** des éléments existants
6. **Naviguer** entre les éléments (parents, enfants, frères)

Le DOM est la fondation de toute interaction JavaScript avec vos pages web. Une fois que vous maîtriserez sa manipulation, vous pourrez créer des expériences web vraiment interactives et dynamiques !

---

## Ressources supplémentaires

Pour aller plus loin dans votre compréhension du DOM :

- 📖 [MDN - Introduction au DOM](https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model/Introduction)
- 🎥 Visualisez le DOM dans les DevTools de votre navigateur
- 🔍 Explorez `console.dir(document)` pour voir toutes les propriétés disponibles

---


⏭️ [L'objet document](/05-javascript-moderne-fondamentaux/09-manipulation-dom/02-objet-document.md)
