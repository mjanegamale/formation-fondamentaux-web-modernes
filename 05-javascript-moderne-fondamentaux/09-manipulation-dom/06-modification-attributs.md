🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.6 - Modification des attributs : getAttribute, setAttribute, dataset

## Introduction

Vous savez maintenant modifier le **contenu** des éléments HTML. Il est temps d'apprendre à manipuler leurs **attributs** ! Les attributs sont les informations supplémentaires que vous ajoutez aux balises HTML, comme `id`, `class`, `src`, `href`, etc.

JavaScript vous permet de **lire**, **modifier**, **ajouter** et **supprimer** ces attributs dynamiquement.

> **Exemples d'attributs :** `id="header"`, `class="active"`, `src="image.jpg"`, `href="page.html"`, `data-id="123"`

---

## Qu'est-ce qu'un attribut HTML ?

### Rappel HTML

Les attributs sont des informations ajoutées aux balises HTML :

```html
<img src="photo.jpg" alt="Une photo" width="300">
<a href="https://example.com" target="_blank">Lien</a>
<input type="text" id="username" placeholder="Nom d'utilisateur" required>
<div class="container" data-theme="dark">Contenu</div>
```

Dans ces exemples :
- `src`, `alt`, `width` sont des attributs de `<img>`
- `href`, `target` sont des attributs de `<a>`
- `type`, `id`, `placeholder`, `required` sont des attributs de `<input>`
- `class`, `data-theme` sont des attributs de `<div>`

### Pourquoi manipuler les attributs en JavaScript ?

Modifier les attributs vous permet de :
- ✅ Changer la source d'une image
- ✅ Modifier le lien d'un élément `<a>`
- ✅ Activer/désactiver un champ de formulaire
- ✅ Ajouter ou retirer des classes CSS
- ✅ Stocker des données personnalisées
- ✅ Rendre votre site interactif

---

## Les trois façons de manipuler les attributs

JavaScript offre trois approches principales :

1. **Méthodes `getAttribute()` et `setAttribute()`** - Approche universelle
2. **Propriétés directes** - Approche simplifiée (ex: `element.id`, `element.src`)
3. **Dataset** - Pour les attributs `data-*` personnalisés

Nous allons voir chacune en détail !

---

## 1. getAttribute() - Lire un attribut

### Syntaxe

```javascript
element.getAttribute('nom-attribut');
```

Cette méthode retourne la **valeur** de l'attribut spécifié, ou **`null`** si l'attribut n'existe pas.

### Exemples basiques

**HTML :**
```html
<img id="photo" src="chat.jpg" alt="Mon chat" width="400">
<a id="lien" href="https://example.com" target="_blank">Visitez</a>
```

**JavaScript :**
```javascript
// Récupérer l'élément
let image = document.getElementById('photo');

// Lire les attributs
console.log(image.getAttribute('src'));      // "chat.jpg"
console.log(image.getAttribute('alt'));      // "Mon chat"
console.log(image.getAttribute('width'));    // "400"

// Récupérer le lien
let lien = document.getElementById('lien');
console.log(lien.getAttribute('href'));      // "https://example.com"
console.log(lien.getAttribute('target'));    // "_blank"
```

### Si l'attribut n'existe pas

```javascript
let image = document.getElementById('photo');

console.log(image.getAttribute('title'));  // null (l'attribut n'existe pas)
```

**Note :** `getAttribute()` retourne **`null`** (pas `undefined`) si l'attribut est absent.

### Vérifier l'existence d'un attribut

```javascript
let image = document.getElementById('photo');

if (image.getAttribute('alt')) {
    console.log('L\'image a un texte alternatif');
} else {
    console.log('L\'image n\'a pas de texte alternatif');
}
```

---

## 2. setAttribute() - Modifier ou ajouter un attribut

### Syntaxe

```javascript
element.setAttribute('nom-attribut', 'valeur');
```

Cette méthode **modifie** un attribut existant ou **l'ajoute** s'il n'existe pas.

### Modifier un attribut existant

**HTML :**
```html
<img id="photo" src="chat.jpg" alt="Mon chat">
```

**JavaScript :**
```javascript
let image = document.getElementById('photo');

// Changer la source de l'image
image.setAttribute('src', 'chien.jpg');

// Changer le texte alternatif
image.setAttribute('alt', 'Mon chien');

// Résultat : l'image affiche maintenant chien.jpg
```

### Ajouter un nouvel attribut

```javascript
let image = document.getElementById('photo');

// Ajouter un attribut qui n'existait pas
image.setAttribute('title', 'Cliquez pour agrandir');
image.setAttribute('width', '500');

// L'image a maintenant ces nouveaux attributs
```

### Exemples pratiques

#### Exemple 1 : Changer le lien d'un bouton

```html
<a id="download-btn" href="file-v1.pdf">Télécharger</a>

<script>
    let button = document.getElementById('download-btn');

    // Changer le fichier à télécharger
    button.setAttribute('href', 'file-v2.pdf');
</script>
```

#### Exemple 2 : Activer/Désactiver un champ

```html
<input type="text" id="email" placeholder="Email">
<button id="toggle">Activer/Désactiver</button>

<script>
    let input = document.getElementById('email');
    let button = document.getElementById('toggle');

    button.addEventListener('click', function() {
        // Vérifier si le champ est désactivé
        if (input.getAttribute('disabled') !== null) {
            // Activer (retirer l'attribut)
            input.removeAttribute('disabled');
        } else {
            // Désactiver (ajouter l'attribut)
            input.setAttribute('disabled', 'disabled');
        }
    });
</script>
```

#### Exemple 3 : Galerie d'images

```html
<img id="main-image" src="image1.jpg" alt="Image 1">
<button onclick="changeImage('image1.jpg')">Image 1</button>
<button onclick="changeImage('image2.jpg')">Image 2</button>
<button onclick="changeImage('image3.jpg')">Image 3</button>

<script>
    function changeImage(imageSrc) {
        let image = document.getElementById('main-image');
        image.setAttribute('src', imageSrc);
    }
</script>
```

---

## 3. removeAttribute() - Supprimer un attribut

### Syntaxe

```javascript
element.removeAttribute('nom-attribut');
```

Cette méthode **supprime complètement** un attribut d'un élément.

### Exemples

```javascript
let image = document.getElementById('photo');

// Supprimer l'attribut width
image.removeAttribute('width');

// L'image n'a plus de largeur définie
```

**Cas d'usage typique :** Retirer l'attribut `disabled` pour réactiver un champ :

```javascript
let input = document.getElementById('email');

// Désactiver
input.setAttribute('disabled', 'disabled');

// Réactiver
input.removeAttribute('disabled');
```

---

## 4. hasAttribute() - Vérifier l'existence d'un attribut

### Syntaxe

```javascript
element.hasAttribute('nom-attribut');
```

Cette méthode retourne **`true`** si l'attribut existe, **`false`** sinon.

### Exemples

```html
<input type="text" id="username" required>
```

```javascript
let input = document.getElementById('username');

console.log(input.hasAttribute('required'));  // true
console.log(input.hasAttribute('disabled'));  // false

// Utilisation dans une condition
if (input.hasAttribute('required')) {
    console.log('Ce champ est obligatoire');
}
```

---

## Propriétés directes vs méthodes getAttribute/setAttribute

JavaScript offre souvent **deux façons** d'accéder aux attributs :

### Approche 1 : Méthodes (getAttribute/setAttribute)

```javascript
let image = document.getElementById('photo');

// Lecture
let src = image.getAttribute('src');

// Modification
image.setAttribute('src', 'nouvelle-image.jpg');
```

### Approche 2 : Propriétés directes

```javascript
let image = document.getElementById('photo');

// Lecture
let src = image.src;

// Modification
image.src = 'nouvelle-image.jpg';
```

**Les deux fonctionnent !** Mais il y a des différences subtiles.

### Comparaison

```javascript
let image = document.getElementById('photo');

// getAttribute retourne la valeur exacte dans le HTML
console.log(image.getAttribute('src'));  // "chat.jpg"

// La propriété directe peut retourner une URL complète
console.log(image.src);  // "http://localhost:3000/chat.jpg"
```

### Propriétés directes disponibles

Voici les attributs HTML courants accessibles directement :

```javascript
let element = document.querySelector('element');

// Attributs communs
element.id           // id="..."
element.className    // class="..." (⚠️ className, pas class)
element.title        // title="..."

// Images
element.src          // src="..."
element.alt          // alt="..."

// Liens
element.href         // href="..."
element.target       // target="..."

// Inputs
element.type         // type="..."
element.value        // value="..."
element.placeholder  // placeholder="..."
element.disabled     // disabled (booléen)
element.required     // required (booléen)
element.checked      // checked (booléen pour checkbox/radio)

// Autres
element.style        // Objet de styles CSS
```

### Quelle approche utiliser ?

**Utilisez les propriétés directes** pour les attributs standard :
```javascript
// ✅ Plus simple et lisible
image.src = 'nouvelle-image.jpg';
input.disabled = true;
```

**Utilisez getAttribute/setAttribute** pour :
- Les attributs personnalisés (`data-*`)
- Les attributs moins courants
- Quand vous avez besoin de la valeur exacte du HTML

```javascript
// ✅ Pour les attributs personnalisés
element.getAttribute('data-id');
element.setAttribute('data-theme', 'dark');
```

---

## Attributs data-* et dataset

### Qu'est-ce que les attributs data-* ?

Les attributs `data-*` sont des **attributs personnalisés** que vous pouvez créer pour stocker des informations supplémentaires.

**Exemple HTML :**
```html
<div id="user-card"
     data-user-id="42"
     data-username="alice"
     data-role="admin">
    Carte utilisateur
</div>
```

### Pourquoi utiliser data-* ?

- ✅ **Stockage de données** : Garder des infos dans le HTML
- ✅ **Séparation** : Ne pas mélanger données et présentation
- ✅ **Accessibilité JS** : Facile à récupérer en JavaScript
- ✅ **Validité HTML** : Standard HTML5 valide

### Accéder aux attributs data-* avec getAttribute

```javascript
let card = document.getElementById('user-card');

// Lecture avec getAttribute
let userId = card.getAttribute('data-user-id');
console.log(userId);  // "42"

// Modification avec setAttribute
card.setAttribute('data-user-id', '100');
```

### L'objet dataset (approche moderne 🆕)

JavaScript offre un moyen **plus élégant** d'accéder aux attributs `data-*` : la propriété **`dataset`** !

#### Syntaxe

```javascript
element.dataset.nomAttribut
```

**Important :** Le préfixe `data-` est automatiquement retiré et le nom est converti en camelCase.

#### Conversion du nom

```
HTML                    →    JavaScript
data-user-id           →    dataset.userId
data-username          →    dataset.username
data-birth-date        →    dataset.birthDate
data-is-active         →    dataset.isActive
```

### Exemples avec dataset

**HTML :**
```html
<div id="user-card"
     data-user-id="42"
     data-username="alice"
     data-role="admin"
     data-is-premium="true">
    Carte utilisateur
</div>
```

**JavaScript :**
```javascript
let card = document.getElementById('user-card');

// Lecture (plus simple !)
console.log(card.dataset.userId);      // "42"
console.log(card.dataset.username);    // "alice"
console.log(card.dataset.role);        // "admin"
console.log(card.dataset.isPremium);   // "true"

// Modification
card.dataset.userId = '100';
card.dataset.username = 'bob';

// Ajout d'un nouvel attribut data-*
card.dataset.level = '5';
// Ajoute data-level="5" dans le HTML

// Suppression
delete card.dataset.role;
// Supprime data-role du HTML
```

### Exemple pratique : Système d'onglets

```html
<div class="tabs">
    <button class="tab-btn active" data-tab="home">Accueil</button>
    <button class="tab-btn" data-tab="profile">Profil</button>
    <button class="tab-btn" data-tab="settings">Paramètres</button>
</div>

<div id="home" class="tab-content">Contenu Accueil</div>
<div id="profile" class="tab-content" style="display:none;">Contenu Profil</div>
<div id="settings" class="tab-content" style="display:none;">Contenu Paramètres</div>

<script>
    let tabButtons = document.querySelectorAll('.tab-btn');

    tabButtons.forEach(button => {
        button.addEventListener('click', function() {
            // Récupérer le nom de l'onglet via dataset
            let tabName = this.dataset.tab;

            // Masquer tous les contenus
            let allContents = document.querySelectorAll('.tab-content');
            allContents.forEach(content => {
                content.style.display = 'none';
            });

            // Afficher le contenu sélectionné
            let targetContent = document.getElementById(tabName);
            targetContent.style.display = 'block';

            // Gérer la classe active
            tabButtons.forEach(btn => btn.classList.remove('active'));
            this.classList.add('active');
        });
    });
</script>
```

---

## Exemples pratiques complets

### Exemple 1 : Galerie d'images interactive

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Galerie</title>
    <style>
        .thumbnail {
            width: 100px;
            height: 100px;
            cursor: pointer;
            margin: 5px;
            border: 2px solid transparent;
        }
        .thumbnail:hover {
            border-color: blue;
        }
    </style>
</head>
<body>
    <h1>Ma galerie</h1>
    <img id="main-image" src="image1.jpg" alt="Image principale" width="500">

    <div id="thumbnails">
        <img class="thumbnail" src="thumb1.jpg" data-full="image1.jpg" alt="Image 1">
        <img class="thumbnail" src="thumb2.jpg" data-full="image2.jpg" alt="Image 2">
        <img class="thumbnail" src="thumb3.jpg" data-full="image3.jpg" alt="Image 3">
    </div>

    <script>
        let mainImage = document.getElementById('main-image');
        let thumbnails = document.querySelectorAll('.thumbnail');

        thumbnails.forEach(thumb => {
            thumb.addEventListener('click', function() {
                // Récupérer l'URL de l'image complète via dataset
                let fullImageUrl = this.dataset.full;

                // Changer l'image principale
                mainImage.setAttribute('src', fullImageUrl);
                // Ou : mainImage.src = fullImageUrl;
            });
        });
    </script>
</body>
</html>
```

### Exemple 2 : Formulaire avec validation

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Formulaire</title>
</head>
<body>
    <form id="signup-form">
        <input type="text" id="username" placeholder="Nom d'utilisateur">
        <input type="email" id="email" placeholder="Email">
        <input type="password" id="password" placeholder="Mot de passe">
        <button type="submit" id="submit-btn" disabled>S'inscrire</button>
    </form>

    <script>
        let form = document.getElementById('signup-form');
        let inputs = form.querySelectorAll('input');
        let submitBtn = document.getElementById('submit-btn');

        // Vérifier si tous les champs sont remplis
        function checkForm() {
            let allFilled = true;

            inputs.forEach(input => {
                if (input.value.trim() === '') {
                    allFilled = false;
                }
            });

            // Activer/désactiver le bouton
            if (allFilled) {
                submitBtn.removeAttribute('disabled');
                submitBtn.style.opacity = '1';
            } else {
                submitBtn.setAttribute('disabled', 'disabled');
                submitBtn.style.opacity = '0.5';
            }
        }

        // Vérifier à chaque saisie
        inputs.forEach(input => {
            input.addEventListener('input', checkForm);
        });

        // Empêcher la soumission réelle (pour démo)
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            alert('Formulaire soumis !');
        });
    </script>
</body>
</html>
```

### Exemple 3 : Système de notation avec étoiles

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Notation</title>
    <style>
        .star {
            font-size: 30px;
            color: gray;
            cursor: pointer;
        }
        .star.filled {
            color: gold;
        }
    </style>
</head>
<body>
    <h2>Notez ce produit</h2>
    <div id="rating">
        <span class="star" data-rating="1">★</span>
        <span class="star" data-rating="2">★</span>
        <span class="star" data-rating="3">★</span>
        <span class="star" data-rating="4">★</span>
        <span class="star" data-rating="5">★</span>
    </div>
    <p>Votre note : <span id="rating-value">0</span>/5</p>

    <script>
        let stars = document.querySelectorAll('.star');
        let ratingValue = document.getElementById('rating-value');
        let currentRating = 0;

        stars.forEach(star => {
            // Au survol
            star.addEventListener('mouseenter', function() {
                let rating = parseInt(this.dataset.rating);
                highlightStars(rating);
            });

            // Au clic
            star.addEventListener('click', function() {
                currentRating = parseInt(this.dataset.rating);
                ratingValue.textContent = currentRating;
            });
        });

        // Quand on quitte la zone
        document.getElementById('rating').addEventListener('mouseleave', function() {
            highlightStars(currentRating);
        });

        function highlightStars(rating) {
            stars.forEach(star => {
                let starRating = parseInt(star.dataset.rating);
                if (starRating <= rating) {
                    star.classList.add('filled');
                } else {
                    star.classList.remove('filled');
                }
            });
        }
    </script>
</body>
</html>
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Utiliser dataset pour les attributs data-*
let id = element.dataset.userId;  // ✅

// Vérifier l'existence avant de lire
if (element.hasAttribute('data-id')) {
    let id = element.dataset.id;
}

// Utiliser les propriétés directes pour les attributs standard
image.src = 'photo.jpg';  // ✅ Plus simple
input.disabled = true;    // ✅

// Nommer les attributs data-* en kebab-case
<div data-user-name="Alice">  <!-- ✅ -->

// Stocker des données simples dans data-*
<button data-action="delete" data-id="123">
```

### ❌ À éviter

```javascript
// Ne pas utiliser getAttribute pour les attributs standard simples
let src = image.getAttribute('src');  // ❌ Moins pratique
let src = image.src;                  // ✅ Mieux

// Ne pas stocker d'objets complexes dans data-*
<div data-user='{"name":"Alice","age":30}'>  <!-- ❌ -->

// Ne pas oublier le camelCase avec dataset
element.dataset['user-id'];  // ❌ Incorrect
element.dataset.userId;      // ✅ Correct

// Ne pas utiliser data-* pour des informations sensibles
<div data-password="secret123">  <!-- ❌ Visible par tous ! -->
```

---

## Attributs booléens

Certains attributs sont **booléens** : leur présence signifie `true`, leur absence signifie `false`.

**Exemples :** `disabled`, `required`, `checked`, `readonly`, `hidden`

### Avec les méthodes

```javascript
let input = document.getElementById('email');

// Vérifier
if (input.hasAttribute('disabled')) {
    console.log('Le champ est désactivé');
}

// Activer
input.removeAttribute('disabled');

// Désactiver
input.setAttribute('disabled', '');
// Ou
input.setAttribute('disabled', 'disabled');
```

### Avec les propriétés directes (plus simple)

```javascript
let input = document.getElementById('email');

// Vérifier
if (input.disabled) {
    console.log('Le champ est désactivé');
}

// Activer
input.disabled = false;

// Désactiver
input.disabled = true;
```

**Préférez les propriétés directes** pour les attributs booléens : c'est plus lisible !

---

## Tableau récapitulatif

| Besoin | Méthode | Exemple |
|--------|---------|---------|
| **Lire un attribut** | `getAttribute()` | `element.getAttribute('src')` |
| **Modifier un attribut** | `setAttribute()` | `element.setAttribute('src', 'image.jpg')` |
| **Supprimer un attribut** | `removeAttribute()` | `element.removeAttribute('width')` |
| **Vérifier existence** | `hasAttribute()` | `element.hasAttribute('required')` |
| **Propriété directe** | `.propriété` | `element.src = 'image.jpg'` |
| **Lire data-*** | `dataset` | `element.dataset.userId` |
| **Modifier data-*** | `dataset` | `element.dataset.userId = '42'` |
| **Supprimer data-*** | `delete` | `delete element.dataset.userId` |

---

## Différence entre attribut et propriété

C'est une nuance importante à comprendre :

### Attribut

- Défini dans le **HTML**
- Valeur **initiale**
- Accessible via `getAttribute()`

### Propriété

- Propriété de l'**objet JavaScript**
- Valeur **actuelle**
- Accessible via `.propriété`

### Exemple avec un input

```html
<input type="text" id="username" value="Alice">
```

```javascript
let input = document.getElementById('username');

// Attribut (valeur initiale dans le HTML)
console.log(input.getAttribute('value'));  // "Alice"

// Propriété (valeur actuelle)
console.log(input.value);  // "Alice"

// L'utilisateur tape "Bob" dans le champ

// L'attribut ne change PAS
console.log(input.getAttribute('value'));  // Toujours "Alice"

// Mais la propriété est mise à jour
console.log(input.value);  // "Bob"
```

**En résumé :**
- **Attribut** = Ce qui est écrit dans le HTML
- **Propriété** = L'état actuel de l'élément

---

## Points clés à retenir

✅ **`getAttribute()`** lit un attribut, retourne `null` si absent

✅ **`setAttribute()`** modifie ou ajoute un attribut

✅ **`removeAttribute()`** supprime un attribut

✅ **`hasAttribute()`** vérifie l'existence d'un attribut

✅ **Propriétés directes** (`.src`, `.id`, `.disabled`) sont plus simples pour les attributs standard

✅ **`dataset`** est l'approche moderne pour les attributs `data-*`

✅ Conversion automatique : `data-user-id` → `dataset.userId`

✅ Les attributs `data-*` sont parfaits pour stocker des infos personnalisées

✅ **Attribut ≠ Propriété** : l'attribut est la valeur initiale, la propriété est l'état actuel

✅ Pour les booléens (`disabled`, `checked`), préférez les propriétés directes

---

## Ce qui vient ensuite

Maintenant que vous savez manipuler le contenu et les attributs, vous allez apprendre à :

1. **Modifier les styles CSS** directement en JavaScript
2. **Travailler avec les classes CSS** (add, remove, toggle)
3. **Créer de nouveaux éléments** dynamiquement
4. **Insérer et supprimer** des éléments du DOM

La manipulation des attributs est essentielle pour rendre vos applications web réellement interactives !

---

## Ressources supplémentaires

- 📖 [MDN - getAttribute](https://developer.mozilla.org/fr/docs/Web/API/Element/getAttribute)
- 📖 [MDN - setAttribute](https://developer.mozilla.org/fr/docs/Web/API/Element/setAttribute)
- 📖 [MDN - dataset](https://developer.mozilla.org/fr/docs/Web/API/HTMLElement/dataset)
- 📖 [MDN - Attributs data-*](https://developer.mozilla.org/fr/docs/Learn/HTML/Howto/Use_data_attributes)

---


⏭️ [Manipulation du style en ligne](/05-javascript-moderne-fondamentaux/09-manipulation-dom/07-manipulation-style.md)
