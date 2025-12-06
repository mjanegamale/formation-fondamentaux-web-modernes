🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.2 - L'objet document

## Introduction

Dans la section précédente, vous avez découvert le DOM et compris qu'il représente votre page HTML sous forme d'arbre. Maintenant, nous allons explorer **l'objet `document`**, qui est votre outil principal pour interagir avec ce DOM en JavaScript.

> **`document`** est l'objet JavaScript qui représente l'intégralité de votre page web et vous permet de la manipuler.

---

## Qu'est-ce que l'objet document ?

L'objet **`document`** est un objet global automatiquement créé par le navigateur. Il est disponible partout dans votre code JavaScript, sans avoir besoin de l'importer ou de le créer.

### Analogie simple

Imaginez que votre page web est une **bibliothèque** :
- 📚 Le **DOM** = Tous les livres et leur organisation
- 🔑 L'objet **`document`** = Le catalogue qui vous permet de trouver et manipuler n'importe quel livre

### Pourquoi est-il important ?

L'objet `document` est le **point d'entrée** pour :
- ✅ Sélectionner des éléments HTML
- ✅ Créer de nouveaux éléments
- ✅ Modifier le contenu de la page
- ✅ Accéder aux informations sur la page
- ✅ Écouter et réagir aux événements

Sans `document`, vous ne pourriez pas interagir avec votre page web !

---

## Accéder à l'objet document

L'objet `document` est **toujours disponible**. Vous pouvez l'utiliser directement dans votre code JavaScript.

### Explorer l'objet document

Ouvrez la console de votre navigateur (F12) et tapez :

```javascript
console.log(document);
```

Vous verrez la représentation complète de votre page HTML.

### Voir toutes les propriétés et méthodes

Pour voir tout ce que `document` peut faire :

```javascript
console.dir(document);
```

La méthode `console.dir()` affiche l'objet sous forme d'une liste de propriétés et méthodes. C'est très utile pour explorer !

---

## Propriétés principales de document

L'objet `document` possède de nombreuses propriétés qui vous donnent des informations sur votre page.

### 1. Informations sur la page

#### `document.title`
Récupère ou modifie le titre de la page (ce qui s'affiche dans l'onglet du navigateur).

```javascript
// Lire le titre
console.log(document.title);  // "Ma superbe page"

// Modifier le titre
document.title = "Nouveau titre";
```

**Résultat :** Le titre dans l'onglet change immédiatement !

#### `document.URL`
L'URL complète de la page actuelle.

```javascript
console.log(document.URL);
// "https://www.monsite.com/page.html"
```

**Note :** Cette propriété est en **lecture seule**, vous ne pouvez pas la modifier.

#### `document.domain`
Le nom de domaine du site.

```javascript
console.log(document.domain);
// "www.monsite.com"
```

#### `document.characterSet`
L'encodage des caractères utilisé (généralement UTF-8).

```javascript
console.log(document.characterSet);
// "UTF-8"
```

### 2. Accès aux éléments principaux

#### `document.documentElement`
Représente l'élément `<html>`, la racine de votre document.

```javascript
console.log(document.documentElement);
// Affiche : <html>...</html>
```

#### `document.head`
Représente l'élément `<head>` de votre page.

```javascript
console.log(document.head);
// Affiche : <head>...</head>
```

#### `document.body`
Représente l'élément `<body>` de votre page.

```javascript
console.log(document.body);
// Affiche : <body>...</body>
```

**Exemple pratique :** Changer la couleur de fond de toute la page

```javascript
document.body.style.backgroundColor = "lightblue";
```

### 3. Collections d'éléments

#### `document.images`
Une collection de toutes les images (`<img>`) de la page.

```javascript
console.log(document.images);
console.log(document.images.length);  // Nombre d'images
```

#### `document.links`
Une collection de tous les liens (`<a>` avec attribut `href`) de la page.

```javascript
console.log(document.links);
console.log(document.links.length);  // Nombre de liens
```

#### `document.forms`
Une collection de tous les formulaires (`<form>`) de la page.

```javascript
console.log(document.forms);
console.log(document.forms.length);  // Nombre de formulaires
```

#### `document.scripts`
Une collection de tous les scripts (`<script>`) de la page.

```javascript
console.log(document.scripts);
console.log(document.scripts.length);  // Nombre de scripts
```

**Astuce :** Ces collections sont **dynamiques**. Si vous ajoutez une image à la page, `document.images` sera automatiquement mis à jour !

### 4. Informations sur l'état de la page

#### `document.readyState`
Indique l'état de chargement du document.

```javascript
console.log(document.readyState);
// Valeurs possibles : "loading", "interactive", "complete"
```

- **`"loading"`** : Le document est en cours de chargement
- **`"interactive"`** : Le document est chargé mais les ressources (images, CSS) ne le sont pas encore
- **`"complete"`** : Tout est chargé

#### `document.lastModified`
La date de dernière modification du document.

```javascript
console.log(document.lastModified);
// "12/05/2025 14:30:25"
```

---

## Méthodes principales de document

Les méthodes de `document` vous permettent d'**agir** sur la page. Voici un aperçu des plus importantes (elles seront détaillées dans les prochaines sections).

### 1. Sélectionner des éléments

Ces méthodes permettent de trouver et récupérer des éléments HTML.

#### `document.getElementById()`
Récupère un élément par son attribut `id`.

```javascript
let titre = document.getElementById('mon-titre');
console.log(titre);
```

#### `document.querySelector()`
Récupère le **premier** élément correspondant à un sélecteur CSS.

```javascript
let paragraphe = document.querySelector('.intro');
console.log(paragraphe);
```

#### `document.querySelectorAll()`
Récupère **tous** les éléments correspondant à un sélecteur CSS.

```javascript
let tousLesParagraphes = document.querySelectorAll('p');
console.log(tousLesParagraphes);
```

**Note :** Ces méthodes seront expliquées en détail dans les sections suivantes. Pour l'instant, retenez qu'elles servent à **sélectionner** des éléments.

### 2. Créer des éléments

#### `document.createElement()`
Crée un nouvel élément HTML.

```javascript
let nouveauParagraphe = document.createElement('p');
console.log(nouveauParagraphe);  // <p></p>
```

#### `document.createTextNode()`
Crée un nœud de texte.

```javascript
let texte = document.createTextNode('Bonjour le monde !');
console.log(texte);
```

### 3. Écrire dans le document

#### `document.write()`
Écrit directement dans le document HTML.

```javascript
document.write('<h1>Titre ajouté</h1>');
```

**⚠️ Attention :** Cette méthode est **déconseillée** car elle peut effacer tout le contenu de la page si elle est appelée après le chargement. Préférez les méthodes modernes de manipulation du DOM.

---

## Explorer document dans la console

La meilleure façon de comprendre `document` est de l'explorer vous-même !

### Exercice d'exploration (à faire dans la console)

1. **Ouvrez n'importe quelle page web**
2. **Ouvrez la console** (F12)
3. **Tapez les commandes suivantes** :

```javascript
// Voir le document complet
console.log(document);

// Voir toutes les propriétés
console.dir(document);

// Tester les propriétés
console.log(document.title);
console.log(document.URL);
console.log(document.body);

// Compter les éléments
console.log("Nombre d'images :", document.images.length);
console.log("Nombre de liens :", document.links.length);
console.log("Nombre de formulaires :", document.forms.length);

// Modifier le titre
document.title = "J'ai modifié le titre !";
```

### Conseils pour l'exploration

🔍 **Astuce 1 :** Tapez `document.` dans la console puis appuyez sur **Tab**. Vous verrez toutes les propriétés et méthodes disponibles grâce à l'auto-complétion !

🔍 **Astuce 2 :** Pour développer un objet dans la console, cliquez sur le petit triangle ▶ à côté.

🔍 **Astuce 3 :** Utilisez `console.dir()` plutôt que `console.log()` pour voir la structure d'un objet en détail.

---

## Exemple pratique complet

Voici un exemple qui utilise plusieurs propriétés de `document` :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Ma page</title>
</head>
<body>
    <h1 id="titre">Bienvenue</h1>
    <p>Ceci est une page de démonstration.</p>
    <img src="photo.jpg" alt="Photo">
    <a href="https://example.com">Lien externe</a>

    <script>
        // Afficher des informations sur la page
        console.log("=== Informations sur la page ===");
        console.log("Titre :", document.title);
        console.log("URL :", document.URL);
        console.log("Encodage :", document.characterSet);
        console.log("État :", document.readyState);

        console.log("=== Statistiques ===");
        console.log("Nombre d'images :", document.images.length);
        console.log("Nombre de liens :", document.links.length);

        // Modifier le titre
        document.title = "Page modifiée !";

        // Changer la couleur de fond
        document.body.style.backgroundColor = "#f0f0f0";

        // Récupérer le titre h1
        let titre = document.getElementById('titre');
        console.log("Contenu du H1 :", titre.textContent);
    </script>
</body>
</html>
```

**Ce que fait ce code :**
1. Affiche des informations sur la page dans la console
2. Compte les images et les liens
3. Modifie le titre de la page
4. Change la couleur de fond du body
5. Récupère et affiche le contenu du `<h1>`

---

## document vs window : quelle différence ?

Vous entendrez peut-être parler de l'objet **`window`**. Voici la différence :

### L'objet `window`
- Représente la **fenêtre du navigateur**
- Contient tout : le document, l'historique, la barre d'adresse, etc.
- C'est l'objet **global** de JavaScript dans le navigateur

### L'objet `document`
- Représente uniquement le **contenu de la page** (le DOM)
- Est une propriété de `window` : `window.document`
- Spécifique au contenu HTML

### Relation entre les deux

```javascript
console.log(window.document === document);  // true
```

Ils pointent vers le même objet ! En pratique, on écrit simplement `document` au lieu de `window.document`.

**Analogie :**
- 🪟 **`window`** = La fenêtre complète de votre maison (cadre, vitre, poignée...)
- 📄 **`document`** = Ce que vous voyez à travers la fenêtre (le paysage)

---

## Bonnes pratiques avec document

### ✅ À faire

```javascript
// Utiliser les sélecteurs modernes
let element = document.querySelector('#mon-id');

// Stocker les éléments dans des variables
let body = document.body;
body.style.margin = '0';

// Vérifier l'existence d'un élément
let titre = document.getElementById('titre');
if (titre) {
    titre.textContent = 'Nouveau titre';
}
```

### ❌ À éviter

```javascript
// Ne pas utiliser document.write() (obsolète)
document.write('<p>Mauvaise pratique</p>');  // ❌

// Ne pas accéder au DOM avant son chargement
// (Mettre les scripts en fin de body ou utiliser DOMContentLoaded)
```

### Attendre le chargement du DOM

Si votre script se trouve dans le `<head>`, le DOM n'est pas encore chargé. Utilisez l'événement `DOMContentLoaded` :

```javascript
document.addEventListener('DOMContentLoaded', function() {
    // Le DOM est maintenant complètement chargé
    console.log('DOM prêt !');

    // Vous pouvez manipuler les éléments ici
    let titre = document.getElementById('titre');
    console.log(titre);
});
```

**Alternative simple :** Placer vos balises `<script>` juste avant la fermeture de `</body>`.

---

## Les propriétés moins connues mais utiles

### `document.cookie`
Accède aux cookies de la page.

```javascript
console.log(document.cookie);
```

### `document.referrer`
L'URL de la page d'où vient l'utilisateur.

```javascript
console.log(document.referrer);
```

### `document.hidden`
Indique si l'onglet est visible ou caché.

```javascript
console.log(document.hidden);  // false si l'onglet est actif
```

---

## Points clés à retenir

✅ **`document`** est l'objet principal pour interagir avec le DOM

✅ Il est **automatiquement disponible** dans tout code JavaScript du navigateur

✅ Il possède de nombreuses **propriétés** (title, URL, body...) et **méthodes** (getElementById, querySelector...)

✅ Les **collections** (images, links, forms) sont **dynamiques** et se mettent à jour automatiquement

✅ Utilisez **`console.dir(document)`** pour explorer toutes ses capacités

✅ **`document`** est une propriété de **`window`**, mais on l'utilise directement

✅ Assurez-vous que le DOM est chargé avant de manipuler des éléments

---

## Résumé visuel

```
window (fenêtre du navigateur)
  │
  ├── document (contenu de la page)
  │     │
  │     ├── documentElement (<html>)
  │     │     │
  │     │     ├── head (<head>)
  │     │     │
  │     │     └── body (<body>)
  │     │           │
  │     │           ├── Éléments HTML
  │     │           ├── Textes
  │     │           └── Commentaires
  │     │
  │     ├── Propriétés (title, URL, images...)
  │     └── Méthodes (getElementById, querySelector...)
  │
  └── Autres propriétés (history, location...)
```

---

## Ce qui vient ensuite

Maintenant que vous connaissez l'objet `document` et ses capacités, vous allez apprendre à :

1. **Sélectionner** des éléments spécifiques avec précision
2. **Modifier** leur contenu et leurs attributs
3. **Créer** de nouveaux éléments dynamiquement
4. **Naviguer** entre les éléments du DOM

L'objet `document` sera votre compagnon constant dans la manipulation du DOM !

---

## Ressources supplémentaires

- 📖 [MDN - L'objet Document](https://developer.mozilla.org/fr/docs/Web/API/Document)
- 🔍 Explorez `document` dans la console de n'importe quelle page web
- 💡 Testez les différentes propriétés sur des sites réels pour voir leur comportement

---


⏭️ [Sélection moderne : querySelector et querySelectorAll](/05-javascript-moderne-fondamentaux/09-manipulation-dom/03-queryselector.md)
