🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.5 - Modification du contenu : innerHTML, textContent, innerText

## Introduction

Maintenant que vous savez **sélectionner** des éléments dans le DOM, il est temps d'apprendre à **modifier leur contenu** ! JavaScript vous offre plusieurs propriétés pour lire et changer le contenu des éléments HTML.

Les trois principales propriétés sont :
- **`innerHTML`** - Pour manipuler le HTML complet
- **`textContent`** - Pour manipuler uniquement le texte
- **`innerText`** - Similaire à textContent avec quelques différences

> Chacune a ses avantages et ses cas d'usage spécifiques. Comprendre leurs différences vous aidera à choisir la bonne méthode !

---

## Vue d'ensemble des trois propriétés

Avant de les détailler, voici un aperçu rapide :

**Exemple HTML :**
```html
<div id="contenu">
    <p>Ceci est du <strong>texte</strong> formaté</p>
</div>
```

**JavaScript :**
```javascript
let element = document.getElementById('contenu');

console.log(element.innerHTML);
// "<p>Ceci est du <strong>texte</strong> formaté</p>"

console.log(element.textContent);
// "Ceci est du texte formaté"

console.log(element.innerText);
// "Ceci est du texte formaté"
```

Voyons maintenant chacune en détail !

---

## 1. innerHTML - Manipuler le HTML complet

### Qu'est-ce que innerHTML ?

**`innerHTML`** est une propriété qui vous permet de **lire** ou **modifier** le contenu HTML d'un élément, balises comprises.

### Lire le contenu HTML

**Exemple HTML :**
```html
<div id="box">
    <h2>Titre</h2>
    <p>Un paragraphe avec du <em>texte en italique</em>.</p>
</div>
```

**JavaScript :**
```javascript
let box = document.getElementById('box');
console.log(box.innerHTML);

// Affiche :
// <h2>Titre</h2>
// <p>Un paragraphe avec du <em>texte en italique</em>.</p>
```

**Note :** `innerHTML` retourne **tout le HTML** à l'intérieur de l'élément, y compris les balises et l'indentation.

### Modifier le contenu HTML

Vous pouvez aussi **assigner** du nouveau HTML à `innerHTML` :

```javascript
let box = document.getElementById('box');

// Remplacer tout le contenu
box.innerHTML = '<h3>Nouveau titre</h3><p>Nouveau paragraphe</p>';
```

**Résultat dans le navigateur :**
```html
<div id="box">
    <h3>Nouveau titre</h3>
    <p>Nouveau paragraphe</p>
</div>
```

### Ajouter du contenu (sans tout remplacer)

Si vous voulez **ajouter** du contenu sans effacer l'existant, utilisez `+=` :

```javascript
let box = document.getElementById('box');

// Ajouter à la fin
box.innerHTML += '<p>Paragraphe ajouté</p>';
```

**⚠️ Attention :** Utiliser `+=` recrée tout le contenu, ce qui peut avoir des effets de bord (événements perdus, animations réinitialisées). Pour un ajout propre, préférez `appendChild()` (que nous verrons plus tard).

### Vider un élément

Pour supprimer tout le contenu d'un élément :

```javascript
let box = document.getElementById('box');

// Vider complètement
box.innerHTML = '';
```

### Exemples pratiques avec innerHTML

#### Exemple 1 : Afficher une liste dynamique

```html
<div id="fruits"></div>

<script>
    let fruits = ['Pomme', 'Banane', 'Orange', 'Fraise'];
    let container = document.getElementById('fruits');

    // Créer une liste HTML
    let html = '<ul>';
    fruits.forEach(fruit => {
        html += `<li>${fruit}</li>`;
    });
    html += '</ul>';

    // Insérer dans le DOM
    container.innerHTML = html;
</script>
```

**Résultat affiché :**
- Pomme
- Banane
- Orange
- Fraise

#### Exemple 2 : Créer une carte de produit

```html
<div id="product-card"></div>

<script>
    let produit = {
        nom: 'Ordinateur portable',
        prix: 899,
        description: 'Un excellent ordinateur pour le travail'
    };

    let card = document.getElementById('product-card');

    card.innerHTML = `
        <div class="card">
            <h3>${produit.nom}</h3>
            <p class="price">${produit.prix}€</p>
            <p>${produit.description}</p>
            <button>Acheter</button>
        </div>
    `;
</script>
```

### ⚠️ Risques de sécurité avec innerHTML

**ATTENTION** : `innerHTML` peut être **dangereux** si vous insérez du contenu venant d'utilisateurs !

#### Problème : Injection de code (XSS)

```javascript
// ❌ DANGER : Ne jamais faire ça avec du contenu utilisateur
let commentaire = '<script>alert("Attaque !");</script>';
element.innerHTML = commentaire;  // ❌ Le script pourrait s'exécuter !
```

#### Solution : Échapper le contenu ou utiliser textContent

```javascript
// ✅ SÛRE : utiliser textContent pour du contenu utilisateur
let commentaire = userInput;
element.textContent = commentaire;  // Le code est affiché comme du texte, pas exécuté
```

**Règle d'or :**
- ✅ Utilisez `innerHTML` avec du contenu que **vous** contrôlez
- ❌ N'utilisez **jamais** `innerHTML` avec du contenu venant directement des utilisateurs

---

## 2. textContent - Manipuler uniquement le texte

### Qu'est-ce que textContent ?

**`textContent`** est une propriété qui vous permet de **lire** ou **modifier** uniquement le **texte** d'un élément, sans les balises HTML.

### Lire le texte

**Exemple HTML :**
```html
<div id="box">
    <h2>Titre</h2>
    <p>Un paragraphe avec du <strong>texte en gras</strong>.</p>
</div>
```

**JavaScript :**
```javascript
let box = document.getElementById('box');
console.log(box.textContent);

// Affiche :
// Titre
// Un paragraphe avec du texte en gras.
```

**Résultat :** Tout le texte, sans les balises HTML !

### Modifier le texte

```javascript
let titre = document.querySelector('h1');

// Remplacer le texte
titre.textContent = 'Nouveau titre';
```

**Important :** Si vous mettez du HTML dans `textContent`, il sera affiché **comme du texte**, pas interprété :

```javascript
let element = document.getElementById('test');

element.textContent = '<strong>Gras</strong>';
// Affiche littéralement : <strong>Gras</strong>
// Pas en gras !

element.innerHTML = '<strong>Gras</strong>';
// Affiche : Gras (en gras)
```

### Pourquoi utiliser textContent ?

#### ✅ Avantages

1. **Sécurité** : Pas de risque d'injection de code
2. **Performance** : Plus rapide que innerHTML
3. **Simplicité** : Pour du texte simple, c'est plus clair

#### 📝 Cas d'usage typiques

```javascript
// Changer le texte d'un titre
document.querySelector('h1').textContent = 'Bienvenue sur mon site';

// Afficher un compteur
let compteur = document.getElementById('counter');
compteur.textContent = count;

// Afficher un message d'erreur
let erreur = document.querySelector('.error-message');
erreur.textContent = 'Veuillez remplir tous les champs';

// Afficher du contenu utilisateur de façon sûre
let commentaire = document.querySelector('.comment');
commentaire.textContent = userInput;  // ✅ Sûr, pas d'injection XSS
```

### Vider un élément avec textContent

```javascript
let element = document.getElementById('content');

// Vider le contenu
element.textContent = '';
```

---

## 3. innerText - Une alternative à textContent

### Qu'est-ce que innerText ?

**`innerText`** est très similaire à `textContent`, mais avec quelques différences subtiles. C'est une propriété plus ancienne, créée par Internet Explorer.

### Différence principale : le rendu visuel

**`innerText`** prend en compte le **rendu CSS**, tandis que **`textContent`** retourne tout le texte brut.

**Exemple HTML :**
```html
<div id="test">
    Texte visible
    <span style="display: none;">Texte caché</span>
    Encore du texte
</div>
```

**JavaScript :**
```javascript
let element = document.getElementById('test');

console.log(element.textContent);
// "Texte visible Texte caché Encore du texte"
// ↑ Récupère TOUT le texte, même caché

console.log(element.innerText);
// "Texte visible Encore du texte"
// ↑ Ne récupère que le texte VISIBLE
```

### Autres différences

#### Gestion des espaces et sauts de ligne

```html
<div id="test">
    Ligne 1

    Ligne 2
</div>
```

```javascript
let element = document.getElementById('test');

console.log(element.textContent);
// "    Ligne 1

//     Ligne 2"
// ↑ Conserve tous les espaces et sauts de ligne

console.log(element.innerText);
// "Ligne 1
// Ligne 2"
// ↑ Normalise les espaces
```

### Performance

**`textContent`** est généralement **plus rapide** car il ne calcule pas le rendu CSS.

---

## Tableau comparatif : innerHTML vs textContent vs innerText

| Critère | innerHTML | textContent | innerText |
|---------|-----------|-------------|-----------|
| **Retourne** | HTML complet avec balises | Texte brut uniquement | Texte visible uniquement |
| **Insère** | Interprète le HTML | Texte brut (échappé) | Texte brut (échappé) |
| **Sécurité** | ⚠️ Risque XSS | ✅ Sûr | ✅ Sûr |
| **Performance** | Plus lent | Rapide | Moyen (calcule le CSS) |
| **Éléments cachés (CSS)** | Inclus | Inclus | Exclus |
| **Espaces/sauts ligne** | Conservés | Conservés | Normalisés |
| **Compatibilité** | ✅ Tous navigateurs | ✅ Tous navigateurs | ✅ Tous navigateurs modernes |
| **Cas d'usage** | Insérer/lire du HTML | Texte simple/sécurisé | Texte visible seulement |

---

## Quelle propriété utiliser ?

Voici un guide pour choisir la bonne propriété selon votre besoin :

### Utilisez `innerHTML` quand :

- ✅ Vous devez **insérer du HTML** (balises, structure)
- ✅ Vous créez du contenu **riche** (listes, liens, images...)
- ✅ Le contenu vient de **votre code** (pas d'utilisateurs)
- ✅ Vous avez besoin de **formatage HTML**

**Exemples :**
```javascript
// Créer une liste
element.innerHTML = '<ul><li>Item 1</li><li>Item 2</li></ul>';

// Ajouter un lien
element.innerHTML = 'Visitez <a href="#">notre site</a>';

// Créer une structure complexe
element.innerHTML = `
    <div class="card">
        <img src="photo.jpg" alt="Photo">
        <h3>Titre</h3>
    </div>
`;
```

### Utilisez `textContent` quand :

- ✅ Vous travaillez avec du **texte simple**
- ✅ Vous affichez du **contenu utilisateur** (sécurité)
- ✅ Vous voulez la **meilleure performance**
- ✅ Vous voulez **échapper le HTML**

**Exemples :**
```javascript
// Afficher un nom d'utilisateur
username.textContent = user.name;

// Afficher un compteur
counter.textContent = count;

// Afficher un message
message.textContent = 'Opération réussie !';

// Sécuriser du contenu utilisateur
comment.textContent = userComment;  // ✅ Sûr
```

### Utilisez `innerText` quand :

- ✅ Vous avez besoin du texte **tel qu'affiché** (sans éléments cachés)
- ✅ Vous voulez que les **sauts de ligne soient normalisés**
- ✅ Vous travaillez avec des **anciennes bases de code**

**Note :** En pratique, `textContent` est généralement préféré à `innerText` pour sa meilleure performance.

---

## Exemples pratiques complets

### Exemple 1 : Compteur de clics

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Compteur</title>
</head>
<body>
    <h1>Compteur de clics</h1>
    <p>Nombre de clics : <span id="count">0</span></p>
    <button id="btn">Cliquez-moi !</button>

    <script>
        let count = 0;
        let countElement = document.getElementById('count');
        let button = document.getElementById('btn');

        button.addEventListener('click', function() {
            count++;
            // textContent pour afficher un nombre
            countElement.textContent = count;
        });
    </script>
</body>
</html>
```

### Exemple 2 : Afficher des informations dynamiques

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Profil utilisateur</title>
</head>
<body>
    <div id="profile"></div>

    <script>
        let user = {
            nom: 'Marie Dupont',
            email: 'marie@example.com',
            bio: 'Développeuse passionnée par le web'
        };

        let profile = document.getElementById('profile');

        // innerHTML pour créer une structure HTML
        profile.innerHTML = `
            <div class="user-card">
                <h2>${user.nom}</h2>
                <p><strong>Email :</strong> ${user.email}</p>
                <p><strong>Bio :</strong> ${user.bio}</p>
            </div>
        `;
    </script>
</body>
</html>
```

### Exemple 3 : Formulaire sécurisé avec textContent

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Commentaires</title>
</head>
<body>
    <h1>Ajouter un commentaire</h1>
    <textarea id="comment-input" placeholder="Votre commentaire"></textarea>
    <button id="submit">Publier</button>

    <div id="comments"></div>

    <script>
        let submitBtn = document.getElementById('submit');
        let commentInput = document.getElementById('comment-input');
        let commentsDiv = document.getElementById('comments');

        submitBtn.addEventListener('click', function() {
            let text = commentInput.value;

            if (text.trim() !== '') {
                // Créer un nouvel élément
                let commentDiv = document.createElement('div');
                commentDiv.className = 'comment';

                // ✅ Utiliser textContent pour du contenu utilisateur (SÛRE)
                commentDiv.textContent = text;

                // Ajouter au DOM
                commentsDiv.appendChild(commentDiv);

                // Vider le champ
                commentInput.value = '';
            }
        });
    </script>
</body>
</html>
```

### Exemple 4 : Basculer entre innerHTML et textContent

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Comparaison innerHTML vs textContent</title>
</head>
<body>
    <div id="output"></div>
    <button id="html-btn">Afficher avec innerHTML</button>
    <button id="text-btn">Afficher avec textContent</button>

    <script>
        let output = document.getElementById('output');
        let htmlBtn = document.getElementById('html-btn');
        let textBtn = document.getElementById('text-btn');

        let content = '<h2>Titre</h2><p>Paragraphe avec <strong>gras</strong></p>';

        htmlBtn.addEventListener('click', function() {
            // innerHTML : interprète le HTML
            output.innerHTML = content;
        });

        textBtn.addEventListener('click', function() {
            // textContent : affiche le HTML comme du texte
            output.textContent = content;
        });
    </script>
</body>
</html>
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Utiliser textContent pour du texte simple
element.textContent = 'Mon texte';

// Utiliser innerHTML pour du HTML contrôlé
element.innerHTML = '<strong>Important</strong>';

// Vérifier qu'un élément existe
let element = document.getElementById('mon-id');
if (element) {
    element.textContent = 'Nouveau texte';
}

// Sécuriser le contenu utilisateur
commentElement.textContent = userInput;  // ✅

// Utiliser les template literals avec innerHTML
element.innerHTML = `
    <div class="card">
        <h3>${titre}</h3>
        <p>${description}</p>
    </div>
`;
```

### ❌ À éviter

```javascript
// Ne jamais mettre du contenu utilisateur dans innerHTML
element.innerHTML = userInput;  // ❌ DANGER XSS !

// Ne pas utiliser innerHTML pour du texte simple
element.innerHTML = 'Simple texte';  // ❌ Moins performant
element.textContent = 'Simple texte';  // ✅ Mieux

// Ne pas oublier de vérifier l'existence
element.textContent = 'Texte';  // ❌ Si element est null, erreur !

// Éviter les += avec innerHTML (recrée tout)
element.innerHTML += '<p>Nouveau</p>';  // ❌ Peut causer des problèmes
```

---

## Pièges courants

### Piège 1 : Perdre les événements avec innerHTML

```javascript
let button = document.createElement('button');
button.textContent = 'Cliquez';
button.addEventListener('click', () => alert('Cliqué !'));

let container = document.getElementById('container');
container.innerHTML = '';  // ❌ Supprime le bouton ET son événement
container.appendChild(button);  // ✅ Préserve l'événement
```

### Piège 2 : innerHTML ne met pas à jour automatiquement

```javascript
let count = 0;
let element = document.getElementById('counter');

element.innerHTML = count;  // 0

count++;  // La variable change...
// Mais l'affichage ne change pas automatiquement !

element.innerHTML = count;  // Il faut le refaire manuellement
```

### Piège 3 : textContent ignore le HTML

```javascript
let element = document.getElementById('content');

element.textContent = '<strong>Gras</strong>';
// Affiche littéralement : <strong>Gras</strong>
// Pas en gras !
```

---

## Récupérer vs Définir

Ces propriétés fonctionnent dans les deux sens :

### Récupérer (getter)

```javascript
let element = document.getElementById('content');

// Lire le contenu
let htmlContent = element.innerHTML;
let textContent = element.textContent;
let innerContent = element.innerText;

console.log(htmlContent);
console.log(textContent);
console.log(innerContent);
```

### Définir (setter)

```javascript
let element = document.getElementById('content');

// Modifier le contenu
element.innerHTML = '<p>Nouveau HTML</p>';
element.textContent = 'Nouveau texte';
element.innerText = 'Nouveau texte aussi';
```

---

## Astuces avancées

### Vider plusieurs éléments

```javascript
let elements = document.querySelectorAll('.reset');

elements.forEach(element => {
    element.textContent = '';  // Vider chaque élément
});
```

### Échapper du HTML dans une fonction

```javascript
function escapeHTML(text) {
    let div = document.createElement('div');
    div.textContent = text;  // textContent échappe automatiquement
    return div.innerHTML;
}

let userInput = '<script>alert("XSS")</script>';
let safe = escapeHTML(userInput);
console.log(safe);
// "&lt;script&gt;alert("XSS")&lt;/script&gt;"
```

### Préserver les sauts de ligne

```javascript
let textarea = document.getElementById('textarea');
let display = document.getElementById('display');

// Conserver les sauts de ligne avec CSS
display.style.whiteSpace = 'pre-wrap';
display.textContent = textarea.value;
```

---

## Points clés à retenir

✅ **`innerHTML`** manipule le HTML complet (balises incluses)

✅ **`textContent`** manipule uniquement le texte (ignore les balises)

✅ **`innerText`** similaire à textContent mais considère le rendu CSS

✅ `innerHTML` avec du contenu utilisateur = **DANGER** (XSS)

✅ `textContent` est **sûr** pour le contenu utilisateur

✅ `textContent` est plus **performant** que innerHTML

✅ Pour du texte simple, **préférez textContent**

✅ Pour du HTML structuré, **utilisez innerHTML** (avec précaution)

✅ Ces propriétés fonctionnent en **lecture et écriture**

✅ Assigner une valeur **remplace** tout le contenu existant

---

## Ce qui vient ensuite

Maintenant que vous savez modifier le contenu des éléments, vous allez apprendre à :

1. **Modifier les attributs** HTML (src, href, id, class...)
2. **Manipuler les styles** CSS directement en JavaScript
3. **Travailler avec les classes** CSS (ajouter, supprimer, basculer)
4. **Créer de nouveaux éléments** dynamiquement
5. **Insérer et supprimer** des éléments du DOM

La manipulation du contenu est une compétence fondamentale pour rendre vos pages interactives !

---

## Ressources supplémentaires

- 📖 [MDN - innerHTML](https://developer.mozilla.org/fr/docs/Web/API/Element/innerHTML)
- 📖 [MDN - textContent](https://developer.mozilla.org/fr/docs/Web/API/Node/textContent)
- 📖 [MDN - innerText](https://developer.mozilla.org/fr/docs/Web/API/HTMLElement/innerText)
- 🔒 [OWASP - XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

---


⏭️ [Modification des attributs : getAttribute, setAttribute, dataset](/05-javascript-moderne-fondamentaux/09-manipulation-dom/06-modification-attributs.md)
