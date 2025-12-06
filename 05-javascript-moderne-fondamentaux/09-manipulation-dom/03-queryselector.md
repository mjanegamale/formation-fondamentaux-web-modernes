🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.3 - Sélection moderne : querySelector et querySelectorAll 🆕

## Introduction

Dans les sections précédentes, vous avez appris ce qu'est le DOM et comment utiliser l'objet `document`. Maintenant, vous allez découvrir **les méthodes modernes** pour sélectionner des éléments HTML dans votre page : **`querySelector()`** et **`querySelectorAll()`**.

> Ces deux méthodes sont **la façon moderne et recommandée** de sélectionner des éléments en JavaScript. Elles utilisent la même syntaxe que CSS, ce qui les rend très intuitives !

---

## Pourquoi des méthodes "modernes" ?

Historiquement, JavaScript proposait plusieurs méthodes pour sélectionner des éléments :
- `getElementById()`
- `getElementsByClassName()`
- `getElementsByTagName()`

Ces méthodes fonctionnent toujours, mais elles ont des limitations. Les méthodes **`querySelector()`** et **`querySelectorAll()`** sont plus récentes (ES6+) et offrent :

- ✅ **Une syntaxe unifiée** : une seule méthode pour tout sélectionner
- ✅ **La puissance du CSS** : utilisez vos sélecteurs CSS familiers
- ✅ **Plus de flexibilité** : sélections complexes facilitées
- ✅ **Plus moderne** : c'est la norme actuelle du développement web

---

## querySelector() - Sélectionner UN élément

### Syntaxe de base

```javascript
document.querySelector('sélecteur-css');
```

La méthode `querySelector()` recherche et renvoie **le premier élément** qui correspond au sélecteur CSS fourni.

### Comment ça fonctionne ?

**Exemple HTML :**
```html
<div class="container">
    <h1 id="titre">Mon titre</h1>
    <p class="intro">Premier paragraphe</p>
    <p class="intro">Deuxième paragraphe</p>
</div>
```

**JavaScript :**
```javascript
// Sélectionner par ID
let titre = document.querySelector('#titre');
console.log(titre);  // <h1 id="titre">Mon titre</h1>

// Sélectionner par classe
let paragraphe = document.querySelector('.intro');
console.log(paragraphe);  // <p class="intro">Premier paragraphe</p>
// ⚠️ Renvoie seulement le PREMIER élément trouvé !

// Sélectionner par balise
let div = document.querySelector('div');
console.log(div);  // <div class="container">...</div>
```

### Point important : UN seul élément

`querySelector()` renvoie **uniquement le premier élément** qui correspond, même s'il y en a plusieurs dans la page.

```javascript
let p = document.querySelector('.intro');
// Renvoie SEULEMENT le premier <p class="intro">
// Pas le deuxième !
```

### Que se passe-t-il si aucun élément n'est trouvé ?

Si aucun élément ne correspond au sélecteur, `querySelector()` renvoie **`null`**.

```javascript
let inexistant = document.querySelector('#nexistepas');
console.log(inexistant);  // null
```

**⚠️ Important :** Vérifiez toujours qu'un élément existe avant de le manipuler !

```javascript
let element = document.querySelector('.ma-classe');

if (element) {
    // L'élément existe, on peut le manipuler
    element.style.color = 'red';
} else {
    console.log("Élément non trouvé");
}
```

---

## querySelectorAll() - Sélectionner PLUSIEURS éléments

### Syntaxe de base

```javascript
document.querySelectorAll('sélecteur-css');
```

La méthode `querySelectorAll()` recherche et renvoie **tous les éléments** qui correspondent au sélecteur CSS, sous forme de **NodeList**.

### Comment ça fonctionne ?

**Exemple HTML :**
```html
<ul>
    <li class="item">Item 1</li>
    <li class="item">Item 2</li>
    <li class="item">Item 3</li>
    <li class="item active">Item 4</li>
</ul>
```

**JavaScript :**
```javascript
// Sélectionner tous les éléments avec la classe "item"
let items = document.querySelectorAll('.item');
console.log(items);  // NodeList(4) [li.item, li.item, li.item, li.item.active]
console.log(items.length);  // 4
```

### Qu'est-ce qu'une NodeList ?

Une **NodeList** est une collection d'éléments, similaire à un tableau (array), mais ce n'est pas exactement la même chose.

**Ce que vous pouvez faire avec une NodeList :**

```javascript
let paragraphes = document.querySelectorAll('p');

// Accéder à un élément par son index (comme un tableau)
console.log(paragraphes[0]);  // Premier paragraphe
console.log(paragraphes[1]);  // Deuxième paragraphe

// Connaître le nombre d'éléments
console.log(paragraphes.length);  // Nombre de paragraphes

// Parcourir avec forEach (méthode moderne)
paragraphes.forEach(function(p) {
    console.log(p.textContent);
});
```

### Parcourir une NodeList

Il existe plusieurs façons de parcourir tous les éléments d'une NodeList :

#### Méthode 1 : forEach() (moderne et recommandée)

```javascript
let items = document.querySelectorAll('.item');

items.forEach(function(item) {
    console.log(item.textContent);
    item.style.color = 'blue';
});
```

**Avec une fonction fléchée (encore plus moderne) :**

```javascript
items.forEach(item => {
    console.log(item.textContent);
});
```

#### Méthode 2 : Boucle for classique

```javascript
let items = document.querySelectorAll('.item');

for (let i = 0; i < items.length; i++) {
    console.log(items[i].textContent);
}
```

#### Méthode 3 : Boucle for...of (moderne)

```javascript
let items = document.querySelectorAll('.item');

for (let item of items) {
    console.log(item.textContent);
}
```

### Que se passe-t-il si aucun élément n'est trouvé ?

Si aucun élément ne correspond, `querySelectorAll()` renvoie une **NodeList vide** (pas `null`).

```javascript
let inexistants = document.querySelectorAll('.nexistepas');
console.log(inexistants);  // NodeList [] (vide)
console.log(inexistants.length);  // 0
```

---

## Les sélecteurs CSS que vous pouvez utiliser

La grande force de `querySelector()` et `querySelectorAll()` est qu'ils acceptent **tous les sélecteurs CSS** !

### 1. Sélecteurs de base

#### Par balise
```javascript
document.querySelector('p');           // Premier <p>
document.querySelectorAll('div');      // Tous les <div>
```

#### Par ID (#)
```javascript
document.querySelector('#mon-id');     // Élément avec id="mon-id"
```

**Note :** Pour les ID, pas besoin de `querySelectorAll()` car un ID est unique.

#### Par classe (.)
```javascript
document.querySelector('.ma-classe');      // Premier élément avec class="ma-classe"
document.querySelectorAll('.ma-classe');   // Tous les éléments avec cette classe
```

#### Par attribut
```javascript
document.querySelector('[type="text"]');       // Premier input de type text
document.querySelectorAll('[disabled]');       // Tous les éléments disabled
document.querySelector('a[target="_blank"]');  // Premier lien s'ouvrant dans un nouvel onglet
```

### 2. Sélecteurs combinés

#### Combinaison de sélecteurs
```javascript
// Balise ET classe
document.querySelector('p.intro');  // <p> avec class="intro"

// ID ET classe
document.querySelector('#content.active');  // Élément avec cet id ET cette classe

// Plusieurs classes
document.querySelector('.btn.primary');  // Élément avec les deux classes
```

#### Descendant (espace)
```javascript
// Tous les <p> DANS un <div>
document.querySelectorAll('div p');

// Tous les liens dans un <nav>
document.querySelectorAll('nav a');
```

#### Enfant direct (>)
```javascript
// Les <li> qui sont enfants DIRECTS d'un <ul>
document.querySelectorAll('ul > li');

// Les <p> enfants directs de <div class="container">
document.querySelectorAll('.container > p');
```

#### Frère adjacent (+)
```javascript
// Le <p> qui suit immédiatement un <h2>
document.querySelector('h2 + p');
```

### 3. Pseudo-classes

Les pseudo-classes CSS fonctionnent aussi !

```javascript
// Premier enfant
document.querySelector('li:first-child');

// Dernier enfant
document.querySelector('li:last-child');

// N-ième enfant
document.querySelectorAll('li:nth-child(odd)');  // Éléments impairs
document.querySelectorAll('li:nth-child(2n)');   // Éléments pairs

// Element non vide
document.querySelectorAll('p:not(.intro)');  // Tous les <p> SAUF ceux avec class="intro"
```

### 4. Sélecteurs multiples (,)

Vous pouvez sélectionner plusieurs types d'éléments en même temps avec une virgule :

```javascript
// Tous les h1, h2 et h3
document.querySelectorAll('h1, h2, h3');

// Tous les éléments avec class="error" OU "warning"
document.querySelectorAll('.error, .warning');

// Tous les paragraphes et tous les spans
document.querySelectorAll('p, span');
```

---

## Exemples pratiques complets

### Exemple 1 : Modifier tous les titres

```html
<h1>Titre 1</h1>
<h2>Sous-titre 1</h2>
<h2>Sous-titre 2</h2>
<h3>Sous-sous-titre</h3>
```

```javascript
// Sélectionner tous les h2
let sousTitres = document.querySelectorAll('h2');

// Changer leur couleur
sousTitres.forEach(titre => {
    titre.style.color = 'blue';
});
```

### Exemple 2 : Ajouter une classe aux éléments

```html
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

```javascript
// Sélectionner tous les li
let items = document.querySelectorAll('li');

// Ajouter une classe à chacun
items.forEach(item => {
    item.classList.add('list-item');
});
```

### Exemple 3 : Sélection complexe

```html
<div class="container">
    <nav>
        <a href="#" class="active">Accueil</a>
        <a href="#">À propos</a>
        <a href="#">Contact</a>
    </nav>
    <main>
        <p class="intro">Introduction</p>
        <p>Contenu normal</p>
    </main>
</div>
```

```javascript
// Sélectionner le lien actif dans le nav
let lienActif = document.querySelector('nav a.active');
console.log(lienActif.textContent);  // "Accueil"

// Sélectionner tous les liens du nav
let liens = document.querySelectorAll('nav a');
console.log(liens.length);  // 3

// Sélectionner le paragraphe intro dans main
let intro = document.querySelector('main p.intro');
console.log(intro.textContent);  // "Introduction"

// Sélectionner tous les paragraphes dans le container
let paragraphes = document.querySelectorAll('.container p');
console.log(paragraphes.length);  // 2
```

### Exemple 4 : Compter les éléments

```javascript
// Combien de liens sur la page ?
let totalLiens = document.querySelectorAll('a').length;
console.log(`Il y a ${totalLiens} liens sur la page`);

// Combien d'images ?
let totalImages = document.querySelectorAll('img').length;
console.log(`Il y a ${totalImages} images sur la page`);

// Combien d'éléments avec la classe "active" ?
let elementsActifs = document.querySelectorAll('.active').length;
console.log(`${elementsActifs} éléments sont actifs`);
```

---

## Différences clés : querySelector vs querySelectorAll

| Critère | querySelector() | querySelectorAll() |
|---------|----------------|-------------------|
| **Résultat** | UN seul élément (le premier trouvé) | TOUS les éléments correspondants |
| **Type retourné** | Element ou null | NodeList (peut être vide) |
| **Si rien trouvé** | Retourne `null` | Retourne NodeList vide `[]` |
| **Usage typique** | Sélection unique (ID, premier élément) | Sélection multiple (classe, balise) |

### Quel méthode choisir ?

**Utilisez `querySelector()` quand :**
- ✅ Vous cherchez UN élément spécifique (souvent par ID)
- ✅ Vous voulez uniquement le premier élément d'une liste
- ✅ Vous êtes sûr qu'il n'y en a qu'un

**Utilisez `querySelectorAll()` quand :**
- ✅ Vous voulez travailler avec PLUSIEURS éléments
- ✅ Vous devez appliquer le même traitement à tous les éléments correspondants
- ✅ Vous voulez compter les éléments

---

## Conseils et bonnes pratiques

### ✅ Bonnes pratiques

#### 1. Stocker les sélections dans des variables

```javascript
// ✅ Bien : stocker dans une variable
let menu = document.querySelector('#menu');
menu.style.display = 'none';
menu.classList.add('hidden');

// ❌ Moins bien : chercher plusieurs fois
document.querySelector('#menu').style.display = 'none';
document.querySelector('#menu').classList.add('hidden');
```

#### 2. Vérifier l'existence

```javascript
// ✅ Toujours vérifier avant de manipuler
let element = document.querySelector('.optional');
if (element) {
    element.style.color = 'red';
}
```

#### 3. Utiliser des sélecteurs spécifiques

```javascript
// ✅ Spécifique et rapide
let bouton = document.querySelector('#submit-btn');

// ❌ Trop général
let bouton = document.querySelector('button');  // Lequel ?
```

#### 4. Nommer vos variables clairement

```javascript
// ✅ Noms descriptifs
let boutonSubmit = document.querySelector('#submit');
let listItems = document.querySelectorAll('.item');

// ❌ Noms vagues
let btn = document.querySelector('#submit');
let items = document.querySelectorAll('.item');
```

### ⚠️ Pièges à éviter

#### 1. Oublier les guillemets

```javascript
// ❌ Erreur : pas de guillemets
let element = document.querySelector(#titre);

// ✅ Correct
let element = document.querySelector('#titre');
```

#### 2. Oublier le # ou le .

```javascript
// ❌ Erreur : cherche une balise <titre>
let element = document.querySelector('titre');

// ✅ Correct : cherche id="titre"
let element = document.querySelector('#titre');
```

#### 3. Traiter querySelectorAll() comme un élément unique

```javascript
let items = document.querySelectorAll('.item');

// ❌ Ne fonctionne pas : items est une NodeList, pas un élément
items.style.color = 'red';

// ✅ Correct : parcourir la NodeList
items.forEach(item => {
    item.style.color = 'red';
});
```

#### 4. Ne pas vérifier si l'élément existe

```javascript
// ❌ Risqué : crash si l'élément n'existe pas
let element = document.querySelector('.inexistant');
element.textContent = 'Texte';  // ❌ Erreur !

// ✅ Toujours vérifier
let element = document.querySelector('.inexistant');
if (element) {
    element.textContent = 'Texte';
}
```

---

## Sélection limitée à une partie de la page

Vous pouvez aussi appeler `querySelector()` et `querySelectorAll()` sur un élément spécifique, pas seulement sur `document` !

### Pourquoi faire ça ?

C'est plus rapide et plus précis de chercher dans une partie de la page plutôt que dans toute la page.

### Exemple

```html
<div id="sidebar">
    <a href="#">Lien sidebar 1</a>
    <a href="#">Lien sidebar 2</a>
</div>

<main>
    <a href="#">Lien main 1</a>
    <a href="#">Lien main 2</a>
</main>
```

```javascript
// Sélectionner le container
let sidebar = document.querySelector('#sidebar');

// Chercher seulement dans ce container
let liensSidebar = sidebar.querySelectorAll('a');
console.log(liensSidebar.length);  // 2 (seulement ceux du sidebar)

// Comparaison avec recherche globale
let tousLesLiens = document.querySelectorAll('a');
console.log(tousLesLiens.length);  // 4 (tous les liens de la page)
```

**Avantage :** Performance et précision améliorées !

---

## Comparaison avec les anciennes méthodes

Voici pourquoi `querySelector()` et `querySelectorAll()` sont préférables :

### getElementById() vs querySelector()

```javascript
// Ancienne méthode
let element = document.getElementById('titre');

// Méthode moderne (équivalent)
let element = document.querySelector('#titre');
```

**Avantage de querySelector :** Syntaxe unifiée, peut faire plus que les ID.

### getElementsByClassName() vs querySelectorAll()

```javascript
// Ancienne méthode
let elements = document.getElementsByClassName('item');

// Méthode moderne (équivalent)
let elements = document.querySelectorAll('.item');
```

**Avantages de querySelectorAll :**
- Syntaxe CSS familière
- Peut combiner plusieurs critères
- Plus flexible

### getElementsByTagName() vs querySelectorAll()

```javascript
// Ancienne méthode
let paragraphes = document.getElementsByTagName('p');

// Méthode moderne (équivalent)
let paragraphes = document.querySelectorAll('p');
```

**Note :** Les anciennes méthodes retournent des **HTMLCollection** (vivantes), tandis que `querySelectorAll()` retourne des **NodeList** (statiques). Pour débuter, cette différence n'est pas critique.

---

## Tableau récapitulatif des sélecteurs

| Sélecteur | Exemple | Description |
|-----------|---------|-------------|
| `#id` | `#header` | Élément avec id="header" |
| `.classe` | `.btn` | Éléments avec class="btn" |
| `balise` | `p` | Tous les éléments `<p>` |
| `[attribut]` | `[disabled]` | Éléments avec l'attribut disabled |
| `[attribut="valeur"]` | `[type="text"]` | Attribut avec valeur exacte |
| `selecteur1 selecteur2` | `div p` | `<p>` descendants de `<div>` |
| `selecteur1 > selecteur2` | `ul > li` | `<li>` enfants directs de `<ul>` |
| `selecteur1 + selecteur2` | `h2 + p` | `<p>` juste après un `<h2>` |
| `selecteur1, selecteur2` | `h1, h2` | Tous les `<h1>` et `<h2>` |
| `:first-child` | `li:first-child` | Premier enfant |
| `:last-child` | `li:last-child` | Dernier enfant |
| `:nth-child(n)` | `li:nth-child(2)` | N-ième enfant |
| `:not(selecteur)` | `p:not(.intro)` | Négation |

---

## Points clés à retenir

✅ **`querySelector()`** sélectionne le **premier** élément correspondant

✅ **`querySelectorAll()`** sélectionne **tous** les éléments correspondants (NodeList)

✅ Ils utilisent la **syntaxe CSS** : `#id`, `.classe`, `balise`, `[attribut]`, etc.

✅ Ce sont les **méthodes modernes recommandées** pour sélectionner des éléments

✅ `querySelector()` retourne **`null`** si rien n'est trouvé

✅ `querySelectorAll()` retourne une **NodeList vide** si rien n'est trouvé

✅ Toujours **vérifier l'existence** d'un élément avant de le manipuler

✅ Utilisez **`forEach()`** pour parcourir une NodeList (méthode moderne)

✅ Les **sélecteurs peuvent être complexes** : descendant, enfant direct, combinaisons...

---

## Exemple de mini-projet

Voici un exemple qui montre la puissance de ces méthodes :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Gestionnaire de tâches</title>
    <style>
        .completed { text-decoration: line-through; color: gray; }
        .important { font-weight: bold; color: red; }
    </style>
</head>
<body>
    <h1>Ma liste de tâches</h1>
    <ul id="task-list">
        <li class="task">Faire les courses</li>
        <li class="task completed">Lire un livre</li>
        <li class="task important">Appeler le médecin</li>
        <li class="task">Faire du sport</li>
        <li class="task completed important">Payer les factures</li>
    </ul>

    <script>
        // Compter les tâches
        let totalTaches = document.querySelectorAll('.task').length;
        console.log(`Total de tâches : ${totalTaches}`);

        // Compter les tâches terminées
        let tachesTerminees = document.querySelectorAll('.task.completed').length;
        console.log(`Tâches terminées : ${tachesTerminees}`);

        // Compter les tâches importantes
        let tachesImportantes = document.querySelectorAll('.task.important').length;
        console.log(`Tâches importantes : ${tachesImportantes}`);

        // Afficher toutes les tâches importantes non terminées
        console.log('Tâches importantes en attente :');
        let tachesImportantesEnAttente = document.querySelectorAll('.task.important:not(.completed)');
        tachesImportantesEnAttente.forEach(tache => {
            console.log('- ' + tache.textContent);
        });

        // Ajouter un effet au survol (on verra les événements plus tard)
        let toutesLesTaches = document.querySelectorAll('.task');
        toutesLesTaches.forEach(tache => {
            tache.style.cursor = 'pointer';
        });
    </script>
</body>
</html>
```

**Ce code :**
1. Compte différents types de tâches
2. Utilise des sélecteurs combinés (`.task.completed`, `.task.important:not(.completed)`)
3. Parcourt et manipule plusieurs éléments
4. Montre la puissance et la flexibilité des sélecteurs modernes

---

## Ce qui vient ensuite

Maintenant que vous savez **sélectionner** des éléments avec précision, vous allez apprendre à :

1. **Lire** le contenu des éléments
2. **Modifier** leur contenu et leurs attributs
3. **Changer** leurs styles
4. **Créer** de nouveaux éléments
5. Les **ajouter** ou les **supprimer** du DOM

Les méthodes `querySelector()` et `querySelectorAll()` seront vos outils de base pour toute manipulation du DOM !

---

## Ressources supplémentaires

- 📖 [MDN - querySelector](https://developer.mozilla.org/fr/docs/Web/API/Document/querySelector)
- 📖 [MDN - querySelectorAll](https://developer.mozilla.org/fr/docs/Web/API/Document/querySelectorAll)
- 🎓 [Référence des sélecteurs CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Selectors)
- 🔍 Pratiquez dans la console de votre navigateur sur n'importe quel site !

---


⏭️ [Sélection classique : getElementById, getElementsByClassName, getElementsByTagName](/05-javascript-moderne-fondamentaux/09-manipulation-dom/04-selection-classique.md)
