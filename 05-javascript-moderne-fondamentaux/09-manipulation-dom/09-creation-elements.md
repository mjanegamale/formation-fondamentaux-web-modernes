🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.9 - Création d'éléments : createElement, createTextNode

## Introduction

Jusqu'à présent, vous avez appris à **manipuler** des éléments HTML existants. Maintenant, vous allez découvrir comment **créer de nouveaux éléments** dynamiquement avec JavaScript !

Créer des éléments en JavaScript permet de :
- 🎨 Construire des interfaces dynamiques
- ➕ Ajouter du contenu sans recharger la page
- 🔄 Créer des listes, des cartes, des menus à la volée
- ⚡ Rendre vos applications interactives et réactives

> **Note :** Les éléments créés en JavaScript existent en mémoire jusqu'à ce que vous les ajoutiez au DOM. Nous verrons comment les insérer dans la page dans la prochaine section.

---

## createElement() - Créer un élément HTML

### Syntaxe

```javascript
document.createElement('nom-balise');
```

Cette méthode crée un **nouvel élément HTML** du type spécifié et le retourne.

### Exemple basique

```javascript
// Créer un paragraphe
let paragraphe = document.createElement('p');
console.log(paragraphe);  // <p></p>

// Créer une div
let div = document.createElement('div');
console.log(div);  // <div></div>

// Créer un bouton
let button = document.createElement('button');
console.log(button);  // <button></button>
```

### L'élément est créé mais pas encore visible

**Important :** L'élément créé existe en mémoire mais **n'est pas encore dans la page** !

```javascript
let titre = document.createElement('h1');
// Le titre existe, mais il n'est pas encore affiché sur la page
```

Pour l'afficher, vous devrez l'**ajouter au DOM** (nous verrons comment dans la section suivante).

---

## Ajouter du contenu à un élément créé

### Méthode 1 : textContent (recommandée)

```javascript
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Ceci est mon paragraphe';
console.log(paragraphe);  // <p>Ceci est mon paragraphe</p>
```

### Méthode 2 : innerHTML

```javascript
let div = document.createElement('div');
div.innerHTML = '<strong>Texte en gras</strong>';
console.log(div);  // <div><strong>Texte en gras</strong></div>
```

**⚠️ Rappel :** Utilisez `textContent` pour du texte simple et sûr, `innerHTML` uniquement pour du HTML que vous contrôlez.

### Exemple complet

```javascript
// Créer un titre
let titre = document.createElement('h2');
titre.textContent = 'Mon nouveau titre';

// Créer un paragraphe
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Ceci est un paragraphe créé dynamiquement.';

// Créer un lien
let lien = document.createElement('a');
lien.textContent = 'Cliquez ici';
lien.href = 'https://example.com';

console.log(titre);      // <h2>Mon nouveau titre</h2>
console.log(paragraphe); // <p>Ceci est un paragraphe créé dynamiquement.</p>
console.log(lien);       // <a href="https://example.com">Cliquez ici</a>
```

---

## Ajouter des attributs à un élément créé

Une fois l'élément créé, vous pouvez lui ajouter des attributs :

### Avec setAttribute()

```javascript
let image = document.createElement('img');
image.setAttribute('src', 'photo.jpg');
image.setAttribute('alt', 'Une belle photo');
image.setAttribute('width', '300');

console.log(image);
// <img src="photo.jpg" alt="Une belle photo" width="300">
```

### Avec les propriétés directes

```javascript
let image = document.createElement('img');
image.src = 'photo.jpg';
image.alt = 'Une belle photo';
image.width = 300;

console.log(image);
// <img src="photo.jpg" alt="Une belle photo" width="300">
```

### Exemple : Créer un bouton complet

```javascript
let button = document.createElement('button');
button.textContent = 'Cliquez-moi !';
button.id = 'mon-bouton';
button.className = 'btn btn-primary';
button.setAttribute('data-action', 'submit');

console.log(button);
// <button id="mon-bouton" class="btn btn-primary" data-action="submit">Cliquez-moi !</button>
```

---

## Ajouter des classes à un élément créé

### Avec classList

```javascript
let div = document.createElement('div');
div.classList.add('card');
div.classList.add('shadow');

console.log(div);
// <div class="card shadow"></div>
```

### Exemple complet : Carte de produit

```javascript
let card = document.createElement('div');
card.classList.add('product-card');

let titre = document.createElement('h3');
titre.textContent = 'Ordinateur portable';

let prix = document.createElement('p');
prix.textContent = '899€';
prix.classList.add('price');

let button = document.createElement('button');
button.textContent = 'Acheter';
button.classList.add('btn', 'btn-primary');

console.log(card);   // <div class="product-card"></div>
console.log(titre);  // <h3>Ordinateur portable</h3>
console.log(prix);   // <p class="price">899€</p>
console.log(button); // <button class="btn btn-primary">Acheter</button>
```

**Note :** Ces éléments sont créés mais séparés. Dans la prochaine section, vous apprendrez à les assembler et à les ajouter au DOM.

---

## createTextNode() - Créer un nœud de texte

### Qu'est-ce qu'un nœud de texte ?

En plus de créer des éléments HTML, vous pouvez créer des **nœuds de texte** purs.

**Rappel :** Dans le DOM, le texte à l'intérieur d'un élément est considéré comme un **nœud enfant** de type texte.

```html
<p>Ceci est du texte</p>
```

Dans cet exemple, "Ceci est du texte" est un **nœud de texte** enfant de l'élément `<p>`.

### Syntaxe

```javascript
document.createTextNode('texte');
```

### Exemple basique

```javascript
let texte = document.createTextNode('Bonjour le monde !');
console.log(texte);  // "Bonjour le monde !"
```

### Différence avec textContent

**Avec createTextNode :**
```javascript
let paragraphe = document.createElement('p');
let texte = document.createTextNode('Mon texte');

// Le texte est créé séparément
console.log(texte);      // "Mon texte" (nœud de texte)
console.log(paragraphe); // <p></p> (vide pour l'instant)

// Il faut ensuite l'ajouter au paragraphe (prochaine section)
```

**Avec textContent (plus simple) :**
```javascript
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Mon texte';

console.log(paragraphe); // <p>Mon texte</p> (déjà rempli)
```

### Quand utiliser createTextNode ?

**En pratique, `textContent` est plus simple et suffisant dans la plupart des cas.**

Utilisez `createTextNode()` quand :
- Vous devez créer du texte que vous ajouterez à plusieurs endroits
- Vous construisez des structures DOM complexes par étapes
- Vous travaillez avec des fragments de document (avancé)

**Pour débuter :** Préférez `textContent`, c'est plus direct !

---

## Exemples pratiques de création d'éléments

### Exemple 1 : Créer un élément de liste

```javascript
// Créer un élément <li>
let item = document.createElement('li');
item.textContent = 'Pomme';
item.classList.add('fruit-item');

console.log(item);
// <li class="fruit-item">Pomme</li>
```

### Exemple 2 : Créer une carte avec image

```javascript
let card = document.createElement('div');
card.classList.add('card');

let image = document.createElement('img');
image.src = 'produit.jpg';
image.alt = 'Photo du produit';

let titre = document.createElement('h3');
titre.textContent = 'Super produit';

let description = document.createElement('p');
description.textContent = 'Une description incroyable';

let prix = document.createElement('span');
prix.textContent = '29.99€';
prix.classList.add('price');

// Pour l'instant, ces éléments sont séparés
// Dans la prochaine section, on les assemblera
```

### Exemple 3 : Créer un formulaire de commentaire

```javascript
// Conteneur
let form = document.createElement('form');
form.id = 'comment-form';

// Label
let label = document.createElement('label');
label.textContent = 'Votre commentaire :';
label.setAttribute('for', 'comment');

// Textarea
let textarea = document.createElement('textarea');
textarea.id = 'comment';
textarea.name = 'comment';
textarea.rows = 4;
textarea.placeholder = 'Écrivez votre commentaire...';

// Bouton
let button = document.createElement('button');
button.textContent = 'Publier';
button.type = 'submit';
button.classList.add('btn-submit');

// Éléments créés, prêts à être assemblés
```

---

## Créer plusieurs éléments en boucle

C'est très utile pour générer des listes dynamiques !

### Exemple : Liste de fruits

```javascript
let fruits = ['Pomme', 'Banane', 'Orange', 'Fraise', 'Kiwi'];
let listItems = [];

// Créer un <li> pour chaque fruit
fruits.forEach(fruit => {
    let item = document.createElement('li');
    item.textContent = fruit;
    item.classList.add('fruit-item');

    listItems.push(item);
});

console.log(listItems);
// [<li>Pomme</li>, <li>Banane</li>, <li>Orange</li>, <li>Fraise</li>, <li>Kiwi</li>]
```

### Exemple : Cartes de produits

```javascript
let produits = [
    { nom: 'Ordinateur', prix: 899, image: 'laptop.jpg' },
    { nom: 'Souris', prix: 29, image: 'mouse.jpg' },
    { nom: 'Clavier', prix: 79, image: 'keyboard.jpg' }
];

let cards = [];

produits.forEach(produit => {
    // Créer la carte
    let card = document.createElement('div');
    card.classList.add('product-card');

    // Créer l'image
    let img = document.createElement('img');
    img.src = produit.image;
    img.alt = produit.nom;

    // Créer le titre
    let titre = document.createElement('h3');
    titre.textContent = produit.nom;

    // Créer le prix
    let prix = document.createElement('p');
    prix.textContent = `${produit.prix}€`;
    prix.classList.add('price');

    // Créer le bouton
    let button = document.createElement('button');
    button.textContent = 'Acheter';

    cards.push({ card, img, titre, prix, button });
});

console.log(cards);
// Tableau d'objets contenant tous les éléments créés
```

---

## Ajouter des événements aux éléments créés

Vous pouvez ajouter des événements aux éléments **avant même** de les ajouter au DOM :

```javascript
let button = document.createElement('button');
button.textContent = 'Cliquez-moi';

// Ajouter un événement
button.addEventListener('click', function() {
    alert('Bouton cliqué !');
});

// L'événement est attaché, même si le bouton n'est pas encore dans la page
```

### Exemple complet

```javascript
let compteur = 0;

let button = document.createElement('button');
button.textContent = 'Compteur : 0';
button.classList.add('btn-counter');

button.addEventListener('click', function() {
    compteur++;
    this.textContent = `Compteur : ${compteur}`;
});

// Le bouton est créé avec son événement
// Quand on l'ajoutera au DOM, il sera fonctionnel
```

---

## Créer des éléments avec des données utilisateur

### Exemple : Ajouter un commentaire

```javascript
function creerCommentaire(auteur, texte) {
    // Créer le conteneur
    let commentaire = document.createElement('div');
    commentaire.classList.add('comment');

    // Créer le nom d'auteur
    let nomAuteur = document.createElement('strong');
    nomAuteur.textContent = auteur;

    // Créer le texte du commentaire
    let texteCommentaire = document.createElement('p');
    texteCommentaire.textContent = texte;

    // Créer la date
    let date = document.createElement('span');
    date.textContent = new Date().toLocaleDateString();
    date.classList.add('comment-date');

    return { commentaire, nomAuteur, texteCommentaire, date };
}

// Utilisation
let nouveauCommentaire = creerCommentaire('Alice', 'Super article !');
console.log(nouveauCommentaire);
```

### Exemple : Créer une tâche

```javascript
function creerTache(texte) {
    let tache = document.createElement('div');
    tache.classList.add('task');

    let checkbox = document.createElement('input');
    checkbox.type = 'checkbox';

    let label = document.createElement('label');
    label.textContent = texte;

    let boutonSupprimer = document.createElement('button');
    boutonSupprimer.textContent = '✕';
    boutonSupprimer.classList.add('btn-delete');

    // Événement pour marquer comme complété
    checkbox.addEventListener('change', function() {
        if (this.checked) {
            tache.classList.add('completed');
        } else {
            tache.classList.remove('completed');
        }
    });

    return { tache, checkbox, label, boutonSupprimer };
}

// Utilisation
let nouvelleTache = creerTache('Faire les courses');
console.log(nouvelleTache);
```

---

## Cloner un élément existant

Au lieu de créer un élément de zéro, vous pouvez aussi **cloner** un élément existant :

### cloneNode()

```javascript
let original = document.getElementById('modele');

// Clonage simple (sans les enfants)
let clone1 = original.cloneNode();

// Clonage profond (avec tous les enfants)
let clone2 = original.cloneNode(true);
```

### Exemple pratique

**HTML :**
```html
<div id="template" class="card" style="display: none;">
    <h3>Titre par défaut</h3>
    <p>Description par défaut</p>
</div>
```

**JavaScript :**
```javascript
let template = document.getElementById('template');

// Cloner le template
let nouvelleCard = template.cloneNode(true);

// Modifier le contenu
nouvelleCard.querySelector('h3').textContent = 'Nouveau titre';
nouvelleCard.querySelector('p').textContent = 'Nouvelle description';
nouvelleCard.style.display = 'block';

// La nouvelle carte est prête à être ajoutée au DOM
```

**Avantage :** Utile quand vous avez un modèle HTML complexe à réutiliser.

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Créer et configurer un élément complètement avant de l'ajouter au DOM
let button = document.createElement('button');
button.textContent = 'Cliquer';
button.classList.add('btn', 'btn-primary');
button.addEventListener('click', handleClick);
// Puis l'ajouter au DOM (prochaine section)

// Utiliser textContent pour du texte simple
element.textContent = 'Mon texte';  // ✅ Sûr

// Créer des fonctions réutilisables
function creerBouton(texte, classe) {
    let btn = document.createElement('button');
    btn.textContent = texte;
    btn.classList.add(classe);
    return btn;
}

// Stocker les éléments dans des variables descriptives
let titreArticle = document.createElement('h2');
let paragrapheIntro = document.createElement('p');
```

### ❌ À éviter

```javascript
// Ne pas oublier d'ajouter l'élément au DOM
let div = document.createElement('div');
div.textContent = 'Texte';
// ❌ Oubli : l'élément n'est jamais ajouté à la page !

// Ne pas utiliser innerHTML avec du contenu utilisateur
let div = document.createElement('div');
div.innerHTML = userInput;  // ❌ Risque XSS
div.textContent = userInput;  // ✅ Sûr

// Ne pas créer trop d'éléments avant de les utiliser
// Cela peut consommer de la mémoire inutilement

// Éviter les noms de variables génériques
let x = document.createElement('div');  // ❌ Pas clair
let carte = document.createElement('div');  // ✅ Descriptif
```

---

## createElement vs innerHTML

### Deux approches pour créer du contenu

**Approche 1 : createElement (recommandée)**
```javascript
let div = document.createElement('div');
let titre = document.createElement('h2');
titre.textContent = 'Mon titre';
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Mon texte';

// Puis assembler (prochaine section)
```

**Avantages :**
- ✅ Plus sûr (pas de XSS)
- ✅ Meilleur pour la performance
- ✅ Plus de contrôle
- ✅ Événements attachés facilement

**Approche 2 : innerHTML**
```javascript
let container = document.getElementById('container');
container.innerHTML = `
    <div>
        <h2>Mon titre</h2>
        <p>Mon texte</p>
    </div>
`;
```

**Avantages :**
- ✅ Plus rapide à écrire
- ✅ Bon pour du HTML statique

**Inconvénients :**
- ❌ Risque XSS avec contenu utilisateur
- ❌ Perd les événements existants
- ❌ Moins performant pour beaucoup d'éléments

### Quelle approche choisir ?

**Utilisez createElement quand :**
- Vous travaillez avec du contenu utilisateur
- Vous créez des éléments complexes avec événements
- Vous construisez des listes ou tableaux dynamiques
- La performance est importante

**Utilisez innerHTML quand :**
- Vous créez du contenu HTML statique simple
- Vous contrôlez totalement le contenu
- La rapidité de développement est prioritaire

---

## Aperçu : Ajouter au DOM (prochaine section)

Les éléments que vous créez existent en mémoire mais ne sont **pas encore visibles**.

**Créer :**
```javascript
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Mon texte';
// Existe en mémoire, mais pas dans la page
```

**Ajouter (prochaine section) :**
```javascript
document.body.appendChild(paragraphe);
// Maintenant visible dans la page !
```

Dans la prochaine section, vous apprendrez toutes les méthodes pour **insérer** ces éléments dans le DOM.

---

## Exemple complet de préparation

Voici un exemple qui crée tous les éléments d'une carte de profil utilisateur :

```javascript
function creerCarteUtilisateur(utilisateur) {
    // Conteneur principal
    let carte = document.createElement('div');
    carte.classList.add('user-card');
    carte.setAttribute('data-user-id', utilisateur.id);

    // Avatar
    let avatar = document.createElement('img');
    avatar.src = utilisateur.photo;
    avatar.alt = utilisateur.nom;
    avatar.classList.add('avatar');

    // Conteneur info
    let info = document.createElement('div');
    info.classList.add('user-info');

    // Nom
    let nom = document.createElement('h3');
    nom.textContent = utilisateur.nom;

    // Email
    let email = document.createElement('p');
    email.textContent = utilisateur.email;
    email.classList.add('email');

    // Rôle
    let role = document.createElement('span');
    role.textContent = utilisateur.role;
    role.classList.add('badge', `badge-${utilisateur.role.toLowerCase()}`);

    // Bouton
    let boutonProfil = document.createElement('button');
    boutonProfil.textContent = 'Voir le profil';
    boutonProfil.classList.add('btn', 'btn-primary');
    boutonProfil.addEventListener('click', function() {
        console.log(`Afficher le profil de ${utilisateur.nom}`);
    });

    // Retourner tous les éléments
    return {
        carte,
        avatar,
        info,
        nom,
        email,
        role,
        boutonProfil
    };
}

// Utilisation
let userData = {
    id: 42,
    nom: 'Alice Dupont',
    email: 'alice@example.com',
    role: 'Admin',
    photo: 'avatar.jpg'
};

let elements = creerCarteUtilisateur(userData);
console.log(elements);
// Tous les éléments sont créés et configurés
// Prêts à être assemblés et ajoutés au DOM !
```

---

## Points clés à retenir

✅ **`createElement()`** crée un nouvel élément HTML

✅ **`createTextNode()`** crée un nœud de texte (mais `textContent` est souvent plus simple)

✅ Les éléments créés existent **en mémoire** mais ne sont **pas encore dans la page**

✅ Configurez complètement l'élément (contenu, classes, attributs, événements) **avant** de l'ajouter au DOM

✅ Utilisez **`textContent`** pour du texte simple (sûr)

✅ Vous pouvez ajouter des **événements** aux éléments avant de les insérer

✅ **`cloneNode()`** permet de copier un élément existant

✅ Préférez `createElement` à `innerHTML` pour du contenu dynamique ou utilisateur

✅ Créer des **fonctions réutilisables** pour les éléments complexes

---

## Ce qui vient ensuite

Maintenant que vous savez **créer** des éléments, la prochaine étape cruciale est d'apprendre à les **insérer dans le DOM** pour qu'ils deviennent visibles dans la page !

Vous découvrirez :
- `appendChild()` - Ajouter un enfant à la fin
- `append()` - Version moderne de appendChild
- `insertBefore()` - Insérer avant un élément
- `insertAdjacentHTML()` - Insérer du HTML
- Et bien d'autres méthodes d'insertion !

---

## Ressources supplémentaires

- 📖 [MDN - document.createElement()](https://developer.mozilla.org/fr/docs/Web/API/Document/createElement)
- 📖 [MDN - document.createTextNode()](https://developer.mozilla.org/fr/docs/Web/API/Document/createTextNode)
- 📖 [MDN - Node.cloneNode()](https://developer.mozilla.org/fr/docs/Web/API/Node/cloneNode)
- 💡 [MDN - Introduction à la création d'éléments](https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model/Introduction)

---


⏭️ [Insertion d'éléments : appendChild, append, insertBefore, insertAdjacentHTML](/05-javascript-moderne-fondamentaux/09-manipulation-dom/10-insertion-elements.md)
