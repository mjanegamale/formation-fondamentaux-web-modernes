🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.10 - Insertion d'éléments : appendChild, append, insertBefore, insertAdjacentHTML

## Introduction

Dans la section précédente, vous avez appris à **créer** des éléments HTML avec JavaScript. Maintenant, découvrez comment les **insérer dans le DOM** pour qu'ils deviennent visibles sur votre page !

JavaScript offre plusieurs méthodes pour ajouter des éléments :
- 📌 **À la fin** d'un parent
- 📌 **Au début** d'un parent
- 📌 **Avant ou après** un élément spécifique
- 📌 À une **position précise**

> **Note importante :** Un élément ne peut être qu'à **un seul endroit** dans le DOM. Si vous "ajoutez" un élément qui existe déjà ailleurs, il sera **déplacé** (pas copié).

---

## appendChild() - La méthode classique

### Qu'est-ce que appendChild ?

**`appendChild()`** est la méthode traditionnelle pour ajouter un élément **enfant à la fin** d'un élément parent.

### Syntaxe

```javascript
elementParent.appendChild(elementEnfant);
```

### Exemple basique

**HTML initial :**
```html
<div id="container">
    <p>Paragraphe existant</p>
</div>
```

**JavaScript :**
```javascript
// Créer un nouvel élément
let nouveauParagraphe = document.createElement('p');
nouveauParagraphe.textContent = 'Nouveau paragraphe';

// L'ajouter au container
let container = document.getElementById('container');
container.appendChild(nouveauParagraphe);
```

**Résultat :**
```html
<div id="container">
    <p>Paragraphe existant</p>
    <p>Nouveau paragraphe</p>
</div>
```

Le nouveau paragraphe est ajouté **à la fin**, après les enfants existants.

### Exemple pratique : Ajouter des éléments de liste

**HTML :**
```html
<ul id="fruits-list">
    <li>Pomme</li>
    <li>Banane</li>
</ul>
<button id="add-fruit">Ajouter un fruit</button>
```

**JavaScript :**
```javascript
let liste = document.getElementById('fruits-list');
let button = document.getElementById('add-fruit');

button.addEventListener('click', function() {
    // Créer un nouvel élément
    let item = document.createElement('li');
    item.textContent = 'Orange';

    // L'ajouter à la liste
    liste.appendChild(item);
});
```

**Résultat après clic :**
```html
<ul id="fruits-list">
    <li>Pomme</li>
    <li>Banane</li>
    <li>Orange</li>
</ul>
```

### Retour de appendChild

`appendChild()` retourne l'élément qui a été ajouté :

```javascript
let container = document.getElementById('container');
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Mon texte';

let elementAjoute = container.appendChild(paragraphe);
console.log(elementAjoute);  // <p>Mon texte</p>
```

### appendChild déplace les éléments existants

**Important :** Si l'élément existe déjà dans le DOM, `appendChild()` le **déplace** !

```html
<div id="zone1">
    <p id="mobile">Je vais bouger</p>
</div>
<div id="zone2"></div>
```

```javascript
let zone2 = document.getElementById('zone2');
let paragraphe = document.getElementById('mobile');

// Déplace le paragraphe de zone1 vers zone2
zone2.appendChild(paragraphe);
```

**Résultat :**
```html
<div id="zone1">
    <!-- Le paragraphe n'est plus ici -->
</div>
<div id="zone2">
    <p id="mobile">Je vais bouger</p>
</div>
```

---

## append() - La méthode moderne 🆕

### Qu'est-ce que append ?

**`append()`** est la version **moderne** de `appendChild()`, avec des fonctionnalités supplémentaires.

### Syntaxe

```javascript
elementParent.append(element1, element2, ...);
```

### Avantages de append sur appendChild

1. **Plusieurs éléments à la fois**
2. **Accepte du texte directement**
3. **Pas de valeur de retour** (retourne `undefined`)

### Exemple 1 : Ajouter un seul élément

```javascript
let container = document.getElementById('container');
let paragraphe = document.createElement('p');
paragraphe.textContent = 'Nouveau paragraphe';

// Avec append (moderne)
container.append(paragraphe);

// Équivalent à appendChild
// container.appendChild(paragraphe);
```

### Exemple 2 : Ajouter plusieurs éléments à la fois

**Avec append (moderne) :**
```javascript
let container = document.getElementById('container');

let titre = document.createElement('h2');
titre.textContent = 'Mon titre';

let paragraphe = document.createElement('p');
paragraphe.textContent = 'Mon paragraphe';

let image = document.createElement('img');
image.src = 'photo.jpg';

// Ajouter les trois d'un coup !
container.append(titre, paragraphe, image);
```

**Avec appendChild (ancien) :**
```javascript
// Il faut appeler la méthode trois fois
container.appendChild(titre);
container.appendChild(paragraphe);
container.appendChild(image);
```

### Exemple 3 : Ajouter du texte directement

**Avec append (moderne) :**
```javascript
let container = document.getElementById('container');

// Ajouter du texte directement, sans createElement
container.append('Ceci est du texte simple');

// Mélanger éléments et texte
let strong = document.createElement('strong');
strong.textContent = 'Texte en gras';

container.append('Début ', strong, ' Fin');
```

**Résultat :**
```html
<div id="container">
    Début <strong>Texte en gras</strong> Fin
</div>
```

**Avec appendChild (ancien) :**
```javascript
// Il faut créer un nœud de texte explicitement
let texte = document.createTextNode('Ceci est du texte simple');
container.appendChild(texte);
```

### append vs appendChild : Tableau comparatif

| Caractéristique | appendChild | append |
|----------------|-------------|---------|
| **Année** | Ancien (DOM Level 1) | Moderne (DOM Living Standard) |
| **Plusieurs éléments** | ❌ Un seul | ✅ Plusieurs |
| **Texte direct** | ❌ Non | ✅ Oui |
| **Valeur de retour** | L'élément ajouté | undefined |
| **Compatibilité** | Tous navigateurs | Navigateurs modernes |

### Quelle méthode utiliser ?

**Pour les nouveaux projets :**
- ✅ Utilisez **`append()`** (plus flexible et moderne)

**Pour les anciens projets ou compatibilité maximale :**
- ✅ Utilisez **`appendChild()`** (fonctionne partout)

---

## prepend() - Ajouter au début 🆕

### Qu'est-ce que prepend ?

**`prepend()`** est le pendant de `append()`, mais ajoute les éléments **au début** (avant les enfants existants).

### Syntaxe

```javascript
elementParent.prepend(element1, element2, ...);
```

### Exemple

**HTML initial :**
```html
<ul id="liste">
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

**JavaScript :**
```javascript
let liste = document.getElementById('liste');
let premier = document.createElement('li');
premier.textContent = 'Item 1';

// Ajouter au début
liste.prepend(premier);
```

**Résultat :**
```html
<ul id="liste">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

### Exemple avec plusieurs éléments

```javascript
let container = document.getElementById('container');

let titre = document.createElement('h1');
titre.textContent = 'Titre principal';

let sousTitre = document.createElement('h2');
sousTitre.textContent = 'Sous-titre';

// Ajouter les deux au début
container.prepend(titre, sousTitre);
```

---

## insertBefore() - Insérer avant un élément

### Qu'est-ce que insertBefore ?

**`insertBefore()`** permet d'insérer un élément **avant** un autre élément spécifique.

### Syntaxe

```javascript
elementParent.insertBefore(nouvelElement, elementReference);
```

- **nouvelElement** : L'élément à insérer
- **elementReference** : L'élément devant lequel insérer

### Exemple basique

**HTML initial :**
```html
<ul id="liste">
    <li id="item1">Item 1</li>
    <li id="item3">Item 3</li>
</ul>
```

**JavaScript :**
```javascript
let liste = document.getElementById('liste');
let item3 = document.getElementById('item3');

// Créer le nouvel élément
let item2 = document.createElement('li');
item2.textContent = 'Item 2';

// Insérer avant item3
liste.insertBefore(item2, item3);
```

**Résultat :**
```html
<ul id="liste">
    <li id="item1">Item 1</li>
    <li>Item 2</li>
    <li id="item3">Item 3</li>
</ul>
```

### Insérer en première position

Pour insérer au début, utilisez `firstChild` comme référence :

```javascript
let liste = document.getElementById('liste');
let premier = document.createElement('li');
premier.textContent = 'Premier item';

// Insérer avant le premier enfant
liste.insertBefore(premier, liste.firstChild);
```

**Note :** Avec les méthodes modernes, `prepend()` est plus simple pour ajouter au début !

### Si l'élément de référence est null

Si le deuxième paramètre est `null`, `insertBefore()` se comporte comme `appendChild()` :

```javascript
let liste = document.getElementById('liste');
let dernier = document.createElement('li');
dernier.textContent = 'Dernier';

// Équivalent à appendChild
liste.insertBefore(dernier, null);
```

---

## before() et after() - Méthodes modernes 🆕

### before() - Insérer avant l'élément

**`before()`** insère des éléments **avant** l'élément ciblé (comme frère, pas comme enfant).

### Syntaxe

```javascript
element.before(element1, element2, ...);
```

### Exemple

**HTML initial :**
```html
<div id="container">
    <p id="milieu">Paragraphe du milieu</p>
</div>
```

**JavaScript :**
```javascript
let milieu = document.getElementById('milieu');

let avant = document.createElement('p');
avant.textContent = 'Paragraphe avant';

// Insérer avant le paragraphe milieu
milieu.before(avant);
```

**Résultat :**
```html
<div id="container">
    <p>Paragraphe avant</p>
    <p id="milieu">Paragraphe du milieu</p>
</div>
```

### after() - Insérer après l'élément

**`after()`** insère des éléments **après** l'élément ciblé.

### Syntaxe

```javascript
element.after(element1, element2, ...);
```

### Exemple

```javascript
let milieu = document.getElementById('milieu');

let apres = document.createElement('p');
apres.textContent = 'Paragraphe après';

// Insérer après le paragraphe milieu
milieu.after(apres);
```

**Résultat :**
```html
<div id="container">
    <p id="milieu">Paragraphe du milieu</p>
    <p>Paragraphe après</p>
</div>
```

### Différence avec insertBefore

**`insertBefore()`** :
- Appelé sur le **parent**
- Insère comme **enfant** du parent

**`before()`** :
- Appelé sur **l'élément de référence**
- Insère comme **frère**

```javascript
// insertBefore - appelé sur le parent
parent.insertBefore(nouvel, reference);

// before - appelé sur l'élément de référence
reference.before(nouvel);
```

---

## insertAdjacentHTML() - Insérer du HTML

### Qu'est-ce que insertAdjacentHTML ?

**`insertAdjacentHTML()`** permet d'insérer du **code HTML** (sous forme de chaîne) à différentes positions.

### Syntaxe

```javascript
element.insertAdjacentHTML(position, htmlString);
```

### Les 4 positions possibles

```
<!-- beforebegin -->
<div id="target">
    <!-- afterbegin -->
    Contenu existant
    <!-- beforeend -->
</div>
<!-- afterend -->
```

- **`'beforebegin'`** : Avant l'élément (comme frère précédent)
- **`'afterbegin'`** : À l'intérieur, avant le premier enfant
- **`'beforeend'`** : À l'intérieur, après le dernier enfant
- **`'afterend'`** : Après l'élément (comme frère suivant)

### Exemple avec les 4 positions

**HTML initial :**
```html
<div id="container">
    <p>Contenu existant</p>
</div>
```

**JavaScript :**
```javascript
let container = document.getElementById('container');

// beforebegin - avant le container
container.insertAdjacentHTML('beforebegin', '<h1>Titre avant le container</h1>');

// afterbegin - début du container
container.insertAdjacentHTML('afterbegin', '<p>Au début du container</p>');

// beforeend - fin du container
container.insertAdjacentHTML('beforeend', '<p>À la fin du container</p>');

// afterend - après le container
container.insertAdjacentHTML('afterend', '<footer>Après le container</footer>');
```

**Résultat :**
```html
<h1>Titre avant le container</h1>
<div id="container">
    <p>Au début du container</p>
    <p>Contenu existant</p>
    <p>À la fin du container</p>
</div>
<footer>Après le container</footer>
```

### Exemple pratique : Ajouter des commentaires

```html
<div id="comments"></div>
<button id="add-comment">Ajouter un commentaire</button>
```

```javascript
let comments = document.getElementById('comments');
let button = document.getElementById('add-comment');
let compteur = 1;

button.addEventListener('click', function() {
    let html = `
        <div class="comment">
            <strong>Utilisateur ${compteur}</strong>
            <p>Ceci est le commentaire numéro ${compteur}</p>
            <span class="date">${new Date().toLocaleString()}</span>
        </div>
    `;

    // Ajouter à la fin
    comments.insertAdjacentHTML('beforeend', html);
    compteur++;
});
```

### ⚠️ Attention avec insertAdjacentHTML

**Risques de sécurité (XSS) :**

```javascript
// ❌ DANGER : Ne jamais faire ça avec du contenu utilisateur
let userComment = getUserInput();
element.insertAdjacentHTML('beforeend', userComment);  // Risque XSS !
```

**Solution sûre :**
```javascript
// ✅ Utiliser createElement et textContent
let div = document.createElement('div');
div.textContent = getUserInput();  // Sécurisé
element.append(div);
```

### insertAdjacentElement() et insertAdjacentText()

Il existe aussi des variantes plus sûres :

**insertAdjacentElement() :**
```javascript
let nouvel = document.createElement('p');
nouvel.textContent = 'Nouveau paragraphe';

element.insertAdjacentElement('beforeend', nouvel);
```

**insertAdjacentText() :**
```javascript
// Ajoute du texte brut (sécurisé)
element.insertAdjacentText('beforeend', 'Texte simple et sûr');
```

---

## Assembler des éléments complexes

### Créer puis assembler

La stratégie recommandée :
1. **Créer** tous les éléments
2. Les **configurer** (contenu, classes, événements)
3. Les **assembler** en structure
4. **Insérer** le tout dans le DOM

### Exemple : Carte de produit complète

```javascript
function creerCarteProduit(produit) {
    // 1. Créer tous les éléments
    let carte = document.createElement('div');
    carte.classList.add('product-card');

    let image = document.createElement('img');
    image.src = produit.image;
    image.alt = produit.nom;

    let info = document.createElement('div');
    info.classList.add('product-info');

    let titre = document.createElement('h3');
    titre.textContent = produit.nom;

    let description = document.createElement('p');
    description.textContent = produit.description;

    let prix = document.createElement('span');
    prix.textContent = `${produit.prix}€`;
    prix.classList.add('price');

    let bouton = document.createElement('button');
    bouton.textContent = 'Acheter';
    bouton.classList.add('btn-buy');

    // 2. Assembler la structure
    info.append(titre, description, prix, bouton);
    carte.append(image, info);

    // 3. Retourner la carte assemblée
    return carte;
}

// Utilisation
let produit = {
    nom: 'Ordinateur portable',
    description: 'Un excellent ordinateur',
    prix: 899,
    image: 'laptop.jpg'
};

let carte = creerCarteProduit(produit);

// 4. Insérer dans le DOM
let container = document.getElementById('products');
container.append(carte);
```

### Exemple : Liste de tâches

```javascript
function creerTache(texte, estComplete = false) {
    // Créer la structure
    let tache = document.createElement('div');
    tache.classList.add('task');
    if (estComplete) {
        tache.classList.add('completed');
    }

    let checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.checked = estComplete;

    let label = document.createElement('label');
    label.textContent = texte;

    let btnSupprimer = document.createElement('button');
    btnSupprimer.textContent = '✕';
    btnSupprimer.classList.add('btn-delete');

    // Événements
    checkbox.addEventListener('change', function() {
        tache.classList.toggle('completed');
    });

    btnSupprimer.addEventListener('click', function() {
        tache.remove();
    });

    // Assembler
    tache.append(checkbox, label, btnSupprimer);

    return tache;
}

// Utilisation
let listeTaches = document.getElementById('tasks');

let tache1 = creerTache('Faire les courses');
let tache2 = creerTache('Lire un livre', true);
let tache3 = creerTache('Faire du sport');

listeTaches.append(tache1, tache2, tache3);
```

---

## DocumentFragment - Optimisation des performances

### Qu'est-ce qu'un DocumentFragment ?

Quand vous ajoutez beaucoup d'éléments au DOM, chaque ajout peut déclencher un **recalcul du rendu**. Un **DocumentFragment** permet d'assembler tous les éléments hors du DOM, puis de les insérer **en une seule fois**.

### Syntaxe

```javascript
let fragment = document.createDocumentFragment();
```

### Exemple sans fragment (moins performant)

```javascript
let liste = document.getElementById('liste');

// Chaque ajout provoque un recalcul
for (let i = 1; i <= 100; i++) {
    let item = document.createElement('li');
    item.textContent = `Item ${i}`;
    liste.appendChild(item);  // 100 modifications du DOM !
}
```

### Exemple avec fragment (plus performant)

```javascript
let liste = document.getElementById('liste');
let fragment = document.createDocumentFragment();

// Assembler dans le fragment
for (let i = 1; i <= 100; i++) {
    let item = document.createElement('li');
    item.textContent = `Item ${i}`;
    fragment.appendChild(item);  // Pas dans le DOM
}

// Une seule insertion dans le DOM
liste.appendChild(fragment);  // 1 seule modification !
```

### Exemple pratique : Créer une galerie

```javascript
function creerGalerie(images) {
    let galerie = document.getElementById('galerie');
    let fragment = document.createDocumentFragment();

    images.forEach(img => {
        let figure = document.createElement('figure');

        let image = document.createElement('img');
        image.src = img.url;
        image.alt = img.titre;

        let caption = document.createElement('figcaption');
        caption.textContent = img.titre;

        figure.append(image, caption);
        fragment.appendChild(figure);
    });

    // Une seule insertion
    galerie.appendChild(fragment);
}

// Utilisation
let photos = [
    { url: 'photo1.jpg', titre: 'Photo 1' },
    { url: 'photo2.jpg', titre: 'Photo 2' },
    { url: 'photo3.jpg', titre: 'Photo 3' }
    // ... 100 photos
];

creerGalerie(photos);
```

**Avantage :** Beaucoup plus rapide pour de grandes listes !

---

## Exemples pratiques complets

### Exemple 1 : Système de notifications

```javascript
function ajouterNotification(message, type = 'info') {
    // Créer la notification
    let notif = document.createElement('div');
    notif.classList.add('notification', `notification-${type}`);

    let texte = document.createElement('p');
    texte.textContent = message;

    let btnFermer = document.createElement('button');
    btnFermer.textContent = '×';
    btnFermer.classList.add('btn-close');

    // Événement pour fermer
    btnFermer.addEventListener('click', function() {
        notif.remove();
    });

    // Assembler
    notif.append(texte, btnFermer);

    // Insérer en haut de la zone de notifications
    let container = document.getElementById('notifications');
    container.prepend(notif);

    // Auto-suppression après 5 secondes
    setTimeout(() => {
        notif.remove();
    }, 5000);
}

// Utilisation
ajouterNotification('Opération réussie !', 'success');
ajouterNotification('Attention aux données', 'warning');
ajouterNotification('Une erreur est survenue', 'error');
```

### Exemple 2 : Fil de discussion

```html
<div id="chat">
    <div id="messages"></div>
    <input type="text" id="message-input" placeholder="Tapez votre message...">
    <button id="send-btn">Envoyer</button>
</div>
```

```javascript
let messagesDiv = document.getElementById('messages');
let input = document.getElementById('message-input');
let sendBtn = document.getElementById('send-btn');

function ajouterMessage(texte, auteur, estMoi = false) {
    let message = document.createElement('div');
    message.classList.add('message');
    if (estMoi) {
        message.classList.add('message-mine');
    }

    let nomAuteur = document.createElement('strong');
    nomAuteur.textContent = auteur;

    let texteMessage = document.createElement('p');
    texteMessage.textContent = texte;

    let heure = document.createElement('span');
    heure.textContent = new Date().toLocaleTimeString();
    heure.classList.add('time');

    message.append(nomAuteur, texteMessage, heure);

    // Ajouter à la fin et scroller
    messagesDiv.append(message);
    messagesDiv.scrollTop = messagesDiv.scrollHeight;
}

sendBtn.addEventListener('click', function() {
    let texte = input.value.trim();
    if (texte) {
        ajouterMessage(texte, 'Moi', true);
        input.value = '';
    }
});

// Simuler des messages reçus
setTimeout(() => ajouterMessage('Salut !', 'Alice'), 1000);
setTimeout(() => ajouterMessage('Comment ça va ?', 'Alice'), 2000);
```

### Exemple 3 : Menu de navigation dynamique

```javascript
function creerMenu(items) {
    let nav = document.createElement('nav');
    let ul = document.createElement('ul');
    ul.classList.add('menu');

    items.forEach(item => {
        let li = document.createElement('li');
        let a = document.createElement('a');

        a.href = item.url;
        a.textContent = item.titre;

        if (item.actif) {
            li.classList.add('active');
        }

        if (item.sousMenu) {
            li.classList.add('has-submenu');
            let sousUl = document.createElement('ul');
            sousUl.classList.add('submenu');

            item.sousMenu.forEach(sousItem => {
                let sousLi = document.createElement('li');
                let sousA = document.createElement('a');
                sousA.href = sousItem.url;
                sousA.textContent = sousItem.titre;
                sousLi.appendChild(sousA);
                sousUl.appendChild(sousLi);
            });

            li.append(a, sousUl);
        } else {
            li.appendChild(a);
        }

        ul.appendChild(li);
    });

    nav.appendChild(ul);
    return nav;
}

// Utilisation
let menuData = [
    { titre: 'Accueil', url: '/', actif: true },
    { titre: 'À propos', url: '/about' },
    {
        titre: 'Produits',
        url: '/products',
        sousMenu: [
            { titre: 'Catégorie 1', url: '/products/cat1' },
            { titre: 'Catégorie 2', url: '/products/cat2' }
        ]
    },
    { titre: 'Contact', url: '/contact' }
];

let menu = creerMenu(menuData);
document.getElementById('header').prepend(menu);
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Créer et configurer complètement avant d'insérer
let element = document.createElement('div');
element.classList.add('card');
element.textContent = 'Contenu';
element.addEventListener('click', handleClick);
container.append(element);  // ✅ Une seule insertion

// Utiliser append pour plusieurs éléments
container.append(elem1, elem2, elem3);  // ✅ Moderne et efficace

// Utiliser DocumentFragment pour beaucoup d'éléments
let fragment = document.createDocumentFragment();
// ... ajouter beaucoup d'éléments au fragment
container.appendChild(fragment);  // ✅ Performant

// Créer des fonctions réutilisables
function creerElement(texte) {
    let elem = document.createElement('p');
    elem.textContent = texte;
    return elem;
}

// Utiliser textContent pour du contenu utilisateur
element.textContent = userInput;  // ✅ Sûr
```

### ❌ À éviter

```javascript
// Ne pas insérer dans une boucle sans fragment
for (let i = 0; i < 1000; i++) {
    let item = document.createElement('li');
    liste.appendChild(item);  // ❌ 1000 modifications du DOM !
}

// Ne pas utiliser innerHTML avec du contenu utilisateur
container.innerHTML = userInput;  // ❌ Risque XSS

// Ne pas oublier d'insérer l'élément
let element = document.createElement('div');
element.textContent = 'Texte';
// ❌ Oubli : jamais ajouté au DOM !

// Ne pas créer inutilement des éléments complexes
// si innerHTML suffit pour du contenu statique
```

---

## Résumé des méthodes d'insertion

| Méthode | Position | Moderne | Multiple | Texte direct |
|---------|----------|---------|----------|--------------|
| **appendChild()** | Fin (enfant) | ❌ | ❌ | ❌ |
| **append()** | Fin (enfant) | ✅ | ✅ | ✅ |
| **prepend()** | Début (enfant) | ✅ | ✅ | ✅ |
| **insertBefore()** | Avant (enfant) | ❌ | ❌ | ❌ |
| **before()** | Avant (frère) | ✅ | ✅ | ✅ |
| **after()** | Après (frère) | ✅ | ✅ | ✅ |
| **insertAdjacentHTML()** | 4 positions | ❌ | ❌ | HTML uniquement |

---

## Points clés à retenir

✅ **`appendChild()`** ajoute un enfant à la fin (méthode classique)

✅ **`append()`** est la version moderne (plusieurs éléments, texte direct) 🆕

✅ **`prepend()`** ajoute au début 🆕

✅ **`insertBefore()`** insère avant un élément de référence

✅ **`before()`** et **`after()`** insèrent comme frères 🆕

✅ **`insertAdjacentHTML()`** insère du HTML à 4 positions (⚠️ attention XSS)

✅ Un élément ne peut être qu'à **un seul endroit** (déplacement automatique)

✅ **DocumentFragment** optimise les insertions multiples

✅ **Assembler hors du DOM** puis insérer en une fois

✅ Préférer **`createElement` + `textContent`** à `innerHTML` pour du contenu utilisateur

---

## Ce qui vient ensuite

Vous savez maintenant créer et insérer des éléments ! La prochaine étape logique : apprendre à **supprimer** des éléments du DOM.

Vous découvrirez :
- `remove()` - Supprimer un élément 🆕
- `removeChild()` - Méthode classique
- Comment vider un conteneur
- Remplacer des éléments

---

## Ressources supplémentaires

- 📖 [MDN - Node.appendChild()](https://developer.mozilla.org/fr/docs/Web/API/Node/appendChild)
- 📖 [MDN - Element.append()](https://developer.mozilla.org/fr/docs/Web/API/Element/append)
- 📖 [MDN - Element.prepend()](https://developer.mozilla.org/fr/docs/Web/API/Element/prepend)
- 📖 [MDN - Element.insertAdjacentHTML()](https://developer.mozilla.org/fr/docs/Web/API/Element/insertAdjacentHTML)
- 📖 [MDN - DocumentFragment](https://developer.mozilla.org/fr/docs/Web/API/DocumentFragment)

---


⏭️ [Suppression d'éléments : remove, removeChild](/05-javascript-moderne-fondamentaux/09-manipulation-dom/11-suppression-elements.md)
