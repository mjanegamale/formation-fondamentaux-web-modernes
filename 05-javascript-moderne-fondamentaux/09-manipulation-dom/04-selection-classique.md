🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.4 - Sélection classique : getElementById, getElementsByClassName, getElementsByTagName

## Introduction

Dans la section précédente, vous avez appris les méthodes **modernes** `querySelector()` et `querySelectorAll()`. Maintenant, nous allons découvrir les **méthodes classiques** de sélection d'éléments.

> **Important :** Ces méthodes sont plus anciennes mais **toujours valides** et présentes dans de nombreux projets existants. Il est important de les connaître pour comprendre du code existant, même si les méthodes modernes sont généralement préférables.

---

## Pourquoi apprendre les méthodes classiques ?

Vous vous demandez peut-être : "Pourquoi apprendre ces anciennes méthodes si les nouvelles sont meilleures ?"

**Bonnes raisons de les connaître :**

- ✅ **Code legacy** : Beaucoup de sites existants les utilisent
- ✅ **Compatibilité** : Elles fonctionnent sur tous les navigateurs, même très anciens
- ✅ **Performance** : Pour certaines opérations simples, elles peuvent être légèrement plus rapides
- ✅ **Compréhension** : Comprendre l'évolution de JavaScript
- ✅ **Entretiens** : Questions fréquentes lors d'entretiens techniques

**Note :** Pour vos nouveaux projets, privilégiez `querySelector()` et `querySelectorAll()` !

---

## Les trois méthodes classiques

JavaScript propose trois méthodes principales pour sélectionner des éléments :

1. **`getElementById()`** - Sélectionner par ID
2. **`getElementsByClassName()`** - Sélectionner par classe
3. **`getElementsByTagName()`** - Sélectionner par balise

---

## 1. getElementById() - Sélectionner par ID

### Syntaxe

```javascript
document.getElementById('id-element');
```

Cette méthode recherche et retourne **un seul élément** ayant l'ID spécifié.

### Comment ça fonctionne ?

**Exemple HTML :**
```html
<div id="header">En-tête de la page</div>
<p id="intro">Paragraphe d'introduction</p>
<button id="btn-submit">Envoyer</button>
```

**JavaScript :**
```javascript
// Sélectionner l'élément avec id="header"
let header = document.getElementById('header');
console.log(header);  // <div id="header">En-tête de la page</div>

// Sélectionner le bouton
let bouton = document.getElementById('btn-submit');
console.log(bouton);  // <button id="btn-submit">Envoyer</button>
```

### Points importants

#### ⚠️ Pas de # devant l'ID !

Contrairement à `querySelector()`, on ne met **PAS** le symbole `#` :

```javascript
// ❌ Erreur - Ne fonctionne pas
let element = document.getElementById('#header');

// ✅ Correct
let element = document.getElementById('header');
```

#### Un seul élément

Comme un ID doit être **unique** dans une page HTML, cette méthode retourne :
- **L'élément** s'il est trouvé
- **`null`** si aucun élément n'a cet ID

```javascript
let element = document.getElementById('inexistant');
console.log(element);  // null
```

#### Toujours vérifier

```javascript
let element = document.getElementById('mon-element');

if (element) {
    element.style.color = 'red';
} else {
    console.log("Élément non trouvé");
}
```

### Exemple pratique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>getElementById Example</title>
</head>
<body>
    <h1 id="main-title">Bienvenue</h1>
    <p id="description">Ceci est une description</p>
    <button id="change-title">Changer le titre</button>

    <script>
        // Récupérer les éléments
        let titre = document.getElementById('main-title');
        let description = document.getElementById('description');
        let bouton = document.getElementById('change-title');

        // Afficher leur contenu
        console.log(titre.textContent);        // "Bienvenue"
        console.log(description.textContent);  // "Ceci est une description"

        // Modifier le titre
        titre.textContent = 'Nouveau titre';
        titre.style.color = 'blue';
    </script>
</body>
</html>
```

---

## 2. getElementsByClassName() - Sélectionner par classe

### Syntaxe

```javascript
document.getElementsByClassName('nom-classe');
```

Cette méthode recherche et retourne **tous les éléments** ayant la classe spécifiée.

### Comment ça fonctionne ?

**Exemple HTML :**
```html
<div class="card">Carte 1</div>
<div class="card">Carte 2</div>
<p class="card">Carte 3</p>
<div class="card active">Carte 4</div>
```

**JavaScript :**
```javascript
// Sélectionner tous les éléments avec class="card"
let cartes = document.getElementsByClassName('card');
console.log(cartes);  // HTMLCollection(4) [div.card, div.card, p.card, div.card.active]
console.log(cartes.length);  // 4
```

### Points importants

#### ⚠️ Pas de point (.) devant la classe !

```javascript
// ❌ Erreur - Ne fonctionne pas
let elements = document.getElementsByClassName('.card');

// ✅ Correct
let elements = document.getElementsByClassName('card');
```

#### Retourne une HTMLCollection

Le résultat est une **HTMLCollection**, similaire à un tableau mais avec des différences importantes (nous y reviendrons).

```javascript
let cartes = document.getElementsByClassName('card');

// Accéder à un élément par son index
console.log(cartes[0]);  // Première carte
console.log(cartes[1]);  // Deuxième carte

// Connaître le nombre d'éléments
console.log(cartes.length);  // 4
```

#### Collection vide si rien trouvé

Si aucun élément ne correspond, retourne une **HTMLCollection vide** (pas `null`) :

```javascript
let inexistants = document.getElementsByClassName('inexistant');
console.log(inexistants.length);  // 0
```

### Parcourir une HTMLCollection

Vous ne pouvez **PAS** utiliser `forEach()` directement sur une HTMLCollection (contrairement à NodeList).

#### Méthode 1 : Boucle for classique (la plus compatible)

```javascript
let cartes = document.getElementsByClassName('card');

for (let i = 0; i < cartes.length; i++) {
    console.log(cartes[i].textContent);
    cartes[i].style.backgroundColor = 'lightblue';
}
```

#### Méthode 2 : Boucle for...of

```javascript
let cartes = document.getElementsByClassName('card');

for (let carte of cartes) {
    console.log(carte.textContent);
    carte.style.backgroundColor = 'lightblue';
}
```

#### Méthode 3 : Convertir en tableau puis utiliser forEach

```javascript
let cartes = document.getElementsByClassName('card');

// Convertir en tableau
Array.from(cartes).forEach(carte => {
    console.log(carte.textContent);
});
```

### Exemple pratique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>getElementsByClassName Example</title>
</head>
<body>
    <h2 class="section-title">Section 1</h2>
    <p class="text">Paragraphe 1</p>
    <p class="text">Paragraphe 2</p>

    <h2 class="section-title">Section 2</h2>
    <p class="text">Paragraphe 3</p>
    <p class="text important">Paragraphe important</p>

    <script>
        // Récupérer tous les titres de section
        let titres = document.getElementsByClassName('section-title');
        console.log(`Il y a ${titres.length} sections`);  // 2

        // Changer la couleur de tous les titres
        for (let i = 0; i < titres.length; i++) {
            titres[i].style.color = 'darkblue';
        }

        // Récupérer tous les paragraphes
        let paragraphes = document.getElementsByClassName('text');
        console.log(`Il y a ${paragraphes.length} paragraphes`);  // 4

        // Ajouter une bordure à tous les paragraphes
        for (let p of paragraphes) {
            p.style.border = '1px solid gray';
            p.style.padding = '10px';
        }
    </script>
</body>
</html>
```

---

## 3. getElementsByTagName() - Sélectionner par balise

### Syntaxe

```javascript
document.getElementsByTagName('nom-balise');
```

Cette méthode recherche et retourne **tous les éléments** correspondant au nom de balise spécifié.

### Comment ça fonctionne ?

**Exemple HTML :**
```html
<p>Premier paragraphe</p>
<div>Une div</div>
<p>Deuxième paragraphe</p>
<p>Troisième paragraphe</p>
```

**JavaScript :**
```javascript
// Sélectionner tous les paragraphes
let paragraphes = document.getElementsByTagName('p');
console.log(paragraphes);  // HTMLCollection(3) [p, p, p]
console.log(paragraphes.length);  // 3

// Sélectionner tous les divs
let divs = document.getElementsByTagName('div');
console.log(divs.length);  // 1
```

### Points importants

#### Nom de balise en minuscules

Le nom de la balise est insensible à la casse, mais par convention on utilise des **minuscules** :

```javascript
// Les deux fonctionnent, mais préférez les minuscules
let paragraphes1 = document.getElementsByTagName('p');
let paragraphes2 = document.getElementsByTagName('P');
```

#### Retourne aussi une HTMLCollection

Comme `getElementsByClassName()`, cette méthode retourne une **HTMLCollection**.

```javascript
let paragraphes = document.getElementsByTagName('p');

// Parcourir avec une boucle for
for (let i = 0; i < paragraphes.length; i++) {
    console.log(paragraphes[i].textContent);
}
```

#### Sélectionner TOUS les éléments

Pour sélectionner **tous** les éléments de la page, utilisez `'*'` :

```javascript
let tousLesElements = document.getElementsByTagName('*');
console.log(`Il y a ${tousLesElements.length} éléments dans la page`);
```

### Exemple pratique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>getElementsByTagName Example</title>
</head>
<body>
    <h1>Titre principal</h1>
    <p>Premier paragraphe</p>
    <p>Deuxième paragraphe</p>
    <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>
    <p>Troisième paragraphe</p>

    <script>
        // Compter les éléments
        let paragraphes = document.getElementsByTagName('p');
        let items = document.getElementsByTagName('li');
        let titres = document.getElementsByTagName('h1');

        console.log(`Paragraphes : ${paragraphes.length}`);  // 3
        console.log(`Items de liste : ${items.length}`);      // 3
        console.log(`Titres H1 : ${titres.length}`);          // 1

        // Modifier tous les paragraphes
        for (let p of paragraphes) {
            p.style.fontSize = '18px';
            p.style.lineHeight = '1.6';
        }

        // Numéroter les items de liste
        for (let i = 0; i < items.length; i++) {
            items[i].textContent = `${i + 1}. ${items[i].textContent}`;
        }
    </script>
</body>
</html>
```

---

## HTMLCollection vs NodeList

C'est une différence importante à comprendre !

### HTMLCollection

Retournée par :
- `getElementsByClassName()`
- `getElementsByTagName()`
- Quelques propriétés comme `document.images`, `document.links`

**Caractéristiques :**
- ✅ Collection **vivante** (live) - se met à jour automatiquement
- ❌ **Pas de méthode** `forEach()`
- ✅ Accès par **index** : `collection[0]`
- ✅ Propriété **`length`**

### NodeList

Retournée par :
- `querySelectorAll()`

**Caractéristiques :**
- ✅ Collection **statique** - ne se met pas à jour automatiquement
- ✅ **Méthode** `forEach()` disponible
- ✅ Accès par **index** : `nodeList[0]`
- ✅ Propriété **`length`**

### Comparaison pratique

```html
<div class="item">Item 1</div>
<div class="item">Item 2</div>
```

```javascript
// HTMLCollection (vivante)
let collectionVivante = document.getElementsByClassName('item');
console.log(collectionVivante.length);  // 2

// Ajouter un nouvel élément au DOM
let nouvelItem = document.createElement('div');
nouvelItem.className = 'item';
nouvelItem.textContent = 'Item 3';
document.body.appendChild(nouvelItem);

console.log(collectionVivante.length);  // 3 - Mise à jour automatique !

// NodeList (statique)
let nodeListStatique = document.querySelectorAll('.item');
console.log(nodeListStatique.length);  // 3

// Ajouter encore un élément
let autreItem = document.createElement('div');
autreItem.className = 'item';
autreItem.textContent = 'Item 4';
document.body.appendChild(autreItem);

console.log(collectionVivante.length);  // 4 - Toujours à jour !
console.log(nodeListStatique.length);   // 3 - Pas mis à jour
```

### Tableau comparatif

| Caractéristique | HTMLCollection | NodeList |
|----------------|----------------|----------|
| **Retournée par** | `getElementsBy*()` | `querySelectorAll()` |
| **Vivante (live)** | ✅ Oui | ❌ Non (statique) |
| **Méthode forEach()** | ❌ Non | ✅ Oui |
| **Accès par index []** | ✅ Oui | ✅ Oui |
| **Propriété length** | ✅ Oui | ✅ Oui |
| **Boucle for** | ✅ Oui | ✅ Oui |
| **Boucle for...of** | ✅ Oui | ✅ Oui |

---

## Comparaison avec les méthodes modernes

Voyons comment les méthodes classiques se comparent aux méthodes modernes.

### getElementById vs querySelector

```javascript
// Méthode classique
let element1 = document.getElementById('mon-id');

// Méthode moderne (équivalent)
let element2 = document.querySelector('#mon-id');

// ⚠️ Attention à la syntaxe différente !
// getElementById : pas de #
// querySelector : avec #
```

**Quand utiliser laquelle ?**
- `getElementById()` est **légèrement plus rapide** (négligeable en pratique)
- `querySelector()` offre plus de **flexibilité**

### getElementsByClassName vs querySelectorAll

```javascript
// Méthode classique
let elements1 = document.getElementsByClassName('ma-classe');

// Méthode moderne (équivalent)
let elements2 = document.querySelectorAll('.ma-classe');

// ⚠️ Différence importante :
// getElementsByClassName : HTMLCollection (vivante)
// querySelectorAll : NodeList (statique)
```

**Quand utiliser laquelle ?**
- `getElementsByClassName()` : si vous avez besoin d'une collection **vivante**
- `querySelectorAll()` : plus **flexible** et avec `forEach()`

### getElementsByTagName vs querySelectorAll

```javascript
// Méthode classique
let elements1 = document.getElementsByTagName('p');

// Méthode moderne (équivalent)
let elements2 = document.querySelectorAll('p');
```

---

## Limitations des méthodes classiques

Voici pourquoi les méthodes modernes sont généralement préférables :

### 1. Pas de sélecteurs complexes

```javascript
// ❌ Impossible avec les méthodes classiques :
// - Sélectionner les paragraphes d'une classe spécifique
// - Combiner plusieurs critères
// - Utiliser des pseudo-classes

// ✅ Facile avec querySelector :
let elements = document.querySelectorAll('div.container > p.intro');
```

### 2. Syntaxe différente pour chaque méthode

```javascript
// Méthodes classiques : syntaxe différente pour chaque
document.getElementById('id');           // Pas de #
document.getElementsByClassName('cls');  // Pas de .
document.getElementsByTagName('div');    // Juste le nom

// Méthode moderne : syntaxe unifiée (CSS)
document.querySelector('#id');           // Avec #
document.querySelector('.cls');          // Avec .
document.querySelector('div');           // Pareil
```

### 3. Pas de forEach sur HTMLCollection

```javascript
let elements = document.getElementsByClassName('item');

// ❌ Ne fonctionne pas directement
elements.forEach(item => console.log(item));

// ✅ Il faut convertir en tableau
Array.from(elements).forEach(item => console.log(item));

// Avec querySelectorAll : ✅ forEach fonctionne
let items = document.querySelectorAll('.item');
items.forEach(item => console.log(item));
```

---

## Quand utiliser les méthodes classiques ?

Malgré leurs limitations, il existe des situations où les méthodes classiques sont pertinentes :

### ✅ Utilisez getElementById() quand :
- Vous sélectionnez un élément par son ID unique
- La performance est critique (micro-optimisation)
- Vous travaillez sur du code legacy

### ✅ Utilisez getElementsByClassName() quand :
- Vous avez besoin d'une collection **vivante**
- Sélection simple par classe uniquement
- Compatibilité avec très vieux navigateurs

### ✅ Utilisez getElementsByTagName() quand :
- Vous avez besoin d'une collection **vivante**
- Sélection simple par balise uniquement

### ❌ Préférez querySelector/querySelectorAll quand :
- Vous avez besoin de sélecteurs complexes
- Vous voulez utiliser `forEach()` facilement
- Vous écrivez du nouveau code
- Vous voulez une syntaxe cohérente

---

## Exemples de conversion

Voici comment convertir du code classique en code moderne :

### Exemple 1 : Sélection simple

```javascript
// Ancien code
let titre = document.getElementById('title');
let items = document.getElementsByClassName('item');
let paragraphes = document.getElementsByTagName('p');

// Code moderne équivalent
let titre = document.querySelector('#title');
let items = document.querySelectorAll('.item');
let paragraphes = document.querySelectorAll('p');
```

### Exemple 2 : Parcourir les éléments

```javascript
let items = document.getElementsByClassName('item');

// Ancien : boucle for
for (let i = 0; i < items.length; i++) {
    items[i].style.color = 'red';
}

// Moderne : forEach (après conversion en tableau)
Array.from(items).forEach(item => {
    item.style.color = 'red';
});

// Ou encore mieux avec querySelectorAll
let items = document.querySelectorAll('.item');
items.forEach(item => {
    item.style.color = 'red';
});
```

---

## Exemple complet comparatif

Voici un exemple qui montre les deux approches :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Comparaison des méthodes</title>
</head>
<body>
    <div id="container">
        <h1 id="main-title" class="title">Mon site</h1>
        <p class="text">Paragraphe 1</p>
        <p class="text highlight">Paragraphe 2</p>
        <p class="text">Paragraphe 3</p>
    </div>

    <script>
        console.log("=== MÉTHODES CLASSIQUES ===");

        // getElementById
        let titre = document.getElementById('main-title');
        console.log("Titre :", titre.textContent);

        // getElementsByClassName
        let textes = document.getElementsByClassName('text');
        console.log("Nombre de textes :", textes.length);

        // Parcourir avec for
        for (let i = 0; i < textes.length; i++) {
            console.log(`Texte ${i + 1} :`, textes[i].textContent);
        }

        // getElementsByTagName
        let paragraphes = document.getElementsByTagName('p');
        console.log("Nombre de paragraphes :", paragraphes.length);

        console.log("=== MÉTHODES MODERNES ===");

        // querySelector
        let titre2 = document.querySelector('#main-title');
        console.log("Titre :", titre2.textContent);

        // querySelectorAll
        let textes2 = document.querySelectorAll('.text');
        console.log("Nombre de textes :", textes2.length);

        // Parcourir avec forEach (plus simple)
        textes2.forEach((texte, index) => {
            console.log(`Texte ${index + 1} :`, texte.textContent);
        });

        // Sélection complexe (impossible avec méthodes classiques)
        let texteHighlight = document.querySelector('p.text.highlight');
        console.log("Texte en surbrillance :", texteHighlight.textContent);
    </script>
</body>
</html>
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Vérifier l'existence
let element = document.getElementById('mon-id');
if (element) {
    element.style.color = 'red';
}

// Stocker dans une variable
let items = document.getElementsByClassName('item');
let count = items.length;  // Évite de recalculer à chaque fois

// Utiliser for...of pour parcourir
for (let item of items) {
    console.log(item);
}
```

### ❌ À éviter

```javascript
// Ne pas oublier de vérifier
let element = document.getElementById('inexistant');
element.style.color = 'red';  // ❌ Erreur ! element est null

// Ne pas utiliser forEach directement sur HTMLCollection
let items = document.getElementsByClassName('item');
items.forEach(item => console.log(item));  // ❌ Erreur !

// Ne pas confondre les syntaxes
document.getElementById('#mon-id');  // ❌ Pas de #
document.getElementsByClassName('.ma-classe');  // ❌ Pas de .
```

---

## Points clés à retenir

✅ **Trois méthodes classiques** : `getElementById()`, `getElementsByClassName()`, `getElementsByTagName()`

✅ **Syntaxe sans symboles** : pas de `#` pour ID, pas de `.` pour classe

✅ **getElementById()** retourne **un élément** ou `null`

✅ **getElementsBy*()** retournent une **HTMLCollection**

✅ **HTMLCollection** est **vivante** mais n'a pas de `forEach()`

✅ Pour utiliser `forEach()` : convertir en tableau avec `Array.from()`

✅ Les **méthodes modernes** (`querySelector/querySelectorAll`) sont généralement **préférables**

✅ Les méthodes classiques restent utiles pour :
   - Le code legacy
   - Collections vivantes
   - Performance extrême (rare)

---

## Résumé en tableau

| Méthode | Syntaxe | Retour | Collection | forEach |
|---------|---------|--------|------------|---------|
| `getElementById('id')` | Sans `#` | Un élément ou null | - | - |
| `getElementsByClassName('cls')` | Sans `.` | HTMLCollection | Vivante | ❌ |
| `getElementsByTagName('tag')` | Nom balise | HTMLCollection | Vivante | ❌ |
| `querySelector('#id')` | Avec `#` | Un élément ou null | - | - |
| `querySelectorAll('.cls')` | Avec `.` | NodeList | Statique | ✅ |

---

## Ce qui vient ensuite

Maintenant que vous connaissez toutes les méthodes de sélection (modernes et classiques), vous allez apprendre à :

1. **Lire et modifier** le contenu des éléments
2. **Manipuler** les attributs HTML
3. **Changer** les styles CSS dynamiquement
4. **Travailler** avec les classes CSS

La sélection d'éléments est la première étape. Ensuite vient la manipulation !

---

## Ressources supplémentaires

- 📖 [MDN - getElementById](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById)
- 📖 [MDN - getElementsByClassName](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementsByClassName)
- 📖 [MDN - getElementsByTagName](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementsByTagName)
- 📖 [MDN - HTMLCollection](https://developer.mozilla.org/fr/docs/Web/API/HTMLCollection)

---


⏭️ [Modification du contenu : innerHTML, textContent, innerText](/05-javascript-moderne-fondamentaux/09-manipulation-dom/05-modification-contenu.md)
