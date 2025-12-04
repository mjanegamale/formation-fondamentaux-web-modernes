🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.1.3 Sélecteurs simples : élément, classe, ID, attribut

## Introduction

Les **sélecteurs CSS** sont les outils qui vous permettent de **cibler précisément les éléments HTML** que vous voulez styliser. C'est la première partie de toute règle CSS, celle qui détermine "à qui" les styles vont s'appliquer.

Dans cette section, nous allons découvrir les quatre types de sélecteurs simples les plus utilisés :
1. **Sélecteur d'élément** (type)
2. **Sélecteur de classe** (`.classe`)
3. **Sélecteur d'ID** (`#id`)
4. **Sélecteur d'attribut** (`[attribut]`)

Comprendre ces sélecteurs est **essentiel** car vous les utiliserez dans chaque ligne de CSS que vous écrirez !

---

## 1. Sélecteur d'élément (Type Selector)

### Qu'est-ce qu'un sélecteur d'élément ?

Le sélecteur d'élément cible **tous les éléments HTML d'un type donné** en utilisant simplement le **nom de la balise**.

### Syntaxe

```css
nom-de-balise {
  propriété: valeur;
}
```

### Exemples

**Cibler tous les paragraphes :**
```css
p {
  color: blue;
  font-size: 16px;
}
```

**HTML correspondant :**
```html
<p>Ce paragraphe sera bleu.</p>
<p>Celui-ci aussi sera bleu.</p>
<p>Et celui-là également !</p>
```

**Résultat :** Tous les `<p>` de la page seront en bleu, taille 16px.

### Autres exemples courants

**Styliser tous les titres h1 :**
```css
h1 {
  color: navy;
  font-size: 32px;
  text-align: center;
}
```

**Styliser tous les liens :**
```css
a {
  color: #0066cc;
  text-decoration: none;
}
```

**Styliser tous les éléments div :**
```css
div {
  margin: 20px;
  padding: 15px;
  border: 1px solid #ccc;
}
```

**Styliser le body (élément racine du contenu) :**
```css
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
  margin: 0;
  padding: 0;
}
```

### Caractéristiques

**Points positifs :**
- ✅ **Simple** à utiliser
- ✅ **Universel** : affecte tous les éléments du type
- ✅ Pratique pour les **styles globaux**

**Points négatifs :**
- ⚠️ **Trop large** : affecte TOUS les éléments du type
- ⚠️ **Manque de précision** : difficile de cibler un élément spécifique

### Quand l'utiliser ?

Utilisez le sélecteur d'élément pour :
- Définir des **styles de base** pour tout le site
- Appliquer une **apparence cohérente** à tous les éléments d'un type
- Réinitialiser ou normaliser les styles

**Exemple de styles globaux :**
```css
/* Styles de base pour tout le site */
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
}

h1, h2, h3, h4, h5, h6 {
  font-weight: bold;
  margin-bottom: 15px;
}

p {
  margin-bottom: 10px;
}

a {
  color: blue;
  text-decoration: none;
}
```

### Problème : trop générique

**Scénario problématique :**
```html
<style>
  p {
    color: blue;
  }
</style>

<p>Ce paragraphe sera bleu.</p>
<p>Celui-ci aussi, mais je voulais qu'il soit rouge !</p>
<p>Et celui-là aussi est bleu...</p>
```

**Solution :** Utiliser des classes ou des IDs pour plus de précision !

---

## 2. Sélecteur de classe (Class Selector) ✅ **LE PLUS UTILISÉ**

### Qu'est-ce qu'un sélecteur de classe ?

Le sélecteur de classe cible les éléments qui ont un **attribut `class` spécifique**. C'est le sélecteur **le plus flexible et le plus utilisé** en développement web moderne.

### Syntaxe

**En CSS :**
```css
.nom-de-classe {
  propriété: valeur;
}
```

**En HTML :**
```html
<balise class="nom-de-classe">Contenu</balise>
```

**⚠️ Important :**
- En CSS, le nom de classe commence par un **point** `.`
- En HTML, pas de point, juste le nom de la classe

### Exemples

**CSS :**
```css
.intro {
  font-size: 18px;
  font-weight: bold;
  color: navy;
}
```

**HTML :**
```html
<p class="intro">Ce paragraphe a la classe "intro".</p>
<p>Ce paragraphe n'a pas de classe.</p>
<p class="intro">Celui-ci aussi a la classe "intro".</p>
```

**Résultat :**
- Les paragraphes avec `class="intro"` seront en navy, gras, 18px
- Le paragraphe sans classe gardera le style par défaut

### Réutilisation des classes

**Le grand avantage :** Une classe peut être **appliquée à plusieurs éléments**, même de types différents !

**CSS :**
```css
.highlight {
  background-color: yellow;
  font-weight: bold;
}
```

**HTML :**
```html
<p class="highlight">Paragraphe important</p>
<span class="highlight">Texte important</span>
<div class="highlight">Bloc important</div>
```

**Résultat :** Tous les éléments avec `class="highlight"` auront le fond jaune et seront en gras, quel que soit le type d'élément.

### Plusieurs classes sur un même élément

Un élément peut avoir **plusieurs classes** séparées par des espaces :

**HTML :**
```html
<p class="intro highlight center">Texte avec 3 classes</p>
```

**CSS :**
```css
.intro {
  font-size: 18px;
}

.highlight {
  background-color: yellow;
}

.center {
  text-align: center;
}
```

**Résultat :** Le paragraphe aura :
- Une taille de 18px (de `.intro`)
- Un fond jaune (de `.highlight`)
- Un alignement centré (de `.center`)

### Conventions de nommage

**✅ Bonnes pratiques :**
```css
.button-primary        /* Kebab-case (recommandé) */
.card-header
.menu-item-active
```

**⚠️ Acceptable mais moins courant :**
```css
.buttonPrimary         /* CamelCase */
.button_primary        /* Snake_case */
```

**❌ À éviter :**
```css
.Button                /* Majuscule au début */
.123button             /* Commence par un chiffre */
.mon bouton            /* Espace */
.bouton!               /* Caractère spécial */
```

**Règles de nommage :**
- Commencer par une lettre
- Utiliser lettres, chiffres, tirets `-` et underscores `_`
- Préférer le kebab-case (tirets)
- Choisir des noms **descriptifs** et **significatifs**

### Exemples de classes bien nommées

**Par fonction :**
```css
.button { }
.button-primary { }
.button-secondary { }
.card { }
.card-header { }
.card-body { }
.card-footer { }
```

**Par apparence :**
```css
.text-center { }
.text-bold { }
.bg-blue { }
.border-solid { }
```

**Par état :**
```css
.is-active { }
.is-hidden { }
.is-loading { }
.has-error { }
```

### Pourquoi les classes sont-elles si populaires ?

**1. Réutilisables :**
```html
<button class="btn">Bouton 1</button>
<button class="btn">Bouton 2</button>
<button class="btn">Bouton 3</button>
```

**2. Modulaires :**
```html
<button class="btn btn-large btn-primary">Grand bouton bleu</button>
<button class="btn btn-small btn-secondary">Petit bouton gris</button>
```

**3. Faciles à maintenir :**
```css
/* Changer tous les boutons primaires en changeant une seule règle */
.btn-primary {
  background: blue; /* Changé de red à blue → tous les boutons sont mis à jour */
}
```

**4. Sémantiquement claires :**
```html
<article class="blog-post">
  <h2 class="post-title">Mon Article</h2>
  <p class="post-excerpt">Résumé...</p>
  <a href="#" class="read-more">Lire la suite</a>
</article>
```

---

## 3. Sélecteur d'ID (ID Selector)

### Qu'est-ce qu'un sélecteur d'ID ?

Le sélecteur d'ID cible un élément qui a un **attribut `id` spécifique**. Un ID doit être **unique** dans la page.

### Syntaxe

**En CSS :**
```css
#nom-id {
  propriété: valeur;
}
```

**En HTML :**
```html
<balise id="nom-id">Contenu</balise>
```

**⚠️ Important :**
- En CSS, le nom d'ID commence par un **dièse** `#`
- En HTML, pas de dièse, juste le nom de l'ID
- **Un ID doit être unique** : un seul élément par page peut avoir cet ID

### Exemples

**CSS :**
```css
#header {
  background: navy;
  color: white;
  padding: 20px;
}
```

**HTML :**
```html
<header id="header">
  <h1>Mon Site</h1>
</header>
```

**Autre exemple :**
```css
#logo {
  width: 150px;
  height: auto;
}

#main-content {
  max-width: 1200px;
  margin: 0 auto;
}

#footer {
  background: #333;
  color: white;
  text-align: center;
}
```

**HTML correspondant :**
```html
<img id="logo" src="logo.png" alt="Logo">

<main id="main-content">
  <p>Contenu principal...</p>
</main>

<footer id="footer">
  <p>&copy; 2025</p>
</footer>
```

### Règle d'unicité

**❌ ERREUR - Deux éléments avec le même ID :**
```html
<div id="box">Première boîte</div>
<div id="box">Deuxième boîte</div>  <!-- ERREUR : ID dupliqué ! -->
```

**✅ CORRECT - Utiliser des classes pour plusieurs éléments :**
```html
<div class="box">Première boîte</div>
<div class="box">Deuxième boîte</div>
```

### Classe vs ID : Quand utiliser quoi ?

| Critère | Classe `.class` | ID `#id` |
|---------|----------------|----------|
| **Unicité** | Réutilisable | Unique par page |
| **Nombre** | Plusieurs par élément | Un seul par élément |
| **Usage** | Styles répétés | Élément unique |
| **Spécificité** | Basse | Haute |
| **JavaScript** | Possible | Pratique |
| **Ancres** | Non | Oui (`<a href="#section">`) |
| **Recommandation** | ✅ Privilégier | ⚠️ Utiliser avec parcimonie |

### Pourquoi préférer les classes aux IDs ?

**Raison 1 : Réutilisabilité**
```html
<!-- ❌ Avec ID : non réutilisable -->
<button id="primary-button">Bouton 1</button>
<button id="primary-button-2">Bouton 2</button>  <!-- Doit changer l'ID -->

<!-- ✅ Avec classe : réutilisable -->
<button class="primary-button">Bouton 1</button>
<button class="primary-button">Bouton 2</button>  <!-- Même classe -->
```

**Raison 2 : Spécificité (nous verrons cela en détail plus tard)**

Les IDs ont une spécificité plus élevée, ce qui peut rendre le CSS difficile à surcharger :

```css
#title {
  color: blue;
}

.title-red {
  color: red;  /* Ne fonctionnera PAS si l'élément a aussi un ID ! */
}
```

**Raison 3 : Bonnes pratiques modernes**

Le consensus actuel dans la communauté web est de **privilégier les classes pour le CSS** et de réserver les IDs pour :
- JavaScript (ciblage d'éléments)
- Ancres de navigation (`<a href="#section">`)
- Labels de formulaires (`<label for="email">`)

### Cas d'usage légitime des IDs

**1. JavaScript :**
```html
<button id="submit-button">Envoyer</button>

<script>
  document.getElementById('submit-button').addEventListener('click', ...);
</script>
```

**2. Ancres de navigation :**
```html
<nav>
  <a href="#about">À propos</a>
  <a href="#services">Services</a>
  <a href="#contact">Contact</a>
</nav>

<section id="about">...</section>
<section id="services">...</section>
<section id="contact">...</section>
```

**3. Labels de formulaires :**
```html
<label for="email">Email :</label>
<input type="email" id="email" name="email">
```

### Recommandation moderne

**🎯 Pour le CSS : utilisez principalement des CLASSES**

```css
/* ✅ Recommandé : classes */
.header { }
.main-content { }
.footer { }

/* ⚠️ Éviter : IDs pour le style */
#header { }
#main-content { }
#footer { }
```

---

## 4. Sélecteur d'attribut (Attribute Selector)

### Qu'est-ce qu'un sélecteur d'attribut ?

Le sélecteur d'attribut cible les éléments en fonction de leurs **attributs HTML** ou de leurs valeurs d'attributs.

### Syntaxe de base

**Élément avec un attribut spécifique :**
```css
[attribut] {
  propriété: valeur;
}
```

### Exemples simples

**Cibler tous les éléments avec un attribut `title` :**
```css
[title] {
  border-bottom: 1px dotted blue;
  cursor: help;
}
```

**HTML correspondant :**
```html
<p title="Information supplémentaire">Texte avec un title</p>
<span title="Note">Autre élément</span>
```

**Cibler tous les liens avec un attribut `target` :**
```css
a[target] {
  background: yellow;
}
```

**HTML :**
```html
<a href="page.html">Lien normal</a>
<a href="externe.html" target="_blank">Lien externe</a>  <!-- Sera en jaune -->
```

### Sélecteurs d'attribut avec valeur

CSS offre plusieurs façons de cibler des attributs selon leur valeur :

#### 1. Égalité exacte `[attr="valeur"]`

```css
[type="text"] {
  border: 2px solid blue;
}
```

**HTML :**
```html
<input type="text">      <!-- Ciblé -->
<input type="email">     <!-- Pas ciblé -->
<input type="password">  <!-- Pas ciblé -->
```

**Exemple pratique :**
```css
/* Styliser différemment les types d'inputs */
input[type="text"] {
  border: 1px solid gray;
}

input[type="email"] {
  border: 1px solid blue;
}

input[type="password"] {
  border: 1px solid red;
}
```

#### 2. Contient un mot `[attr~="valeur"]`

Cible les éléments dont l'attribut contient le mot exact parmi une liste de mots séparés par des espaces.

```css
[class~="important"] {
  font-weight: bold;
}
```

**HTML :**
```html
<p class="important">Ciblé</p>
<p class="very important">Ciblé (contient le mot "important")</p>
<p class="importance">Pas ciblé (ce n'est pas le mot exact)</p>
```

#### 3. Commence par `[attr^="valeur"]`

```css
[href^="https"] {
  color: green;
}
```

**HTML :**
```html
<a href="https://site.com">Lien HTTPS</a>       <!-- Vert -->
<a href="http://site.com">Lien HTTP</a>         <!-- Pas vert -->
```

**Exemple pratique : Icônes selon le type de lien**
```css
/* Liens externes (commencent par http) */
a[href^="http"]::after {
  content: " 🔗";
}

/* Liens vers des PDFs */
a[href^="download/"]::after {
  content: " 📄";
}

/* Liens mailto */
a[href^="mailto:"]::before {
  content: "✉️ ";
}
```

#### 4. Se termine par `[attr$="valeur"]`

```css
[href$=".pdf"] {
  color: red;
}
```

**HTML :**
```html
<a href="document.pdf">PDF</a>        <!-- Rouge -->
<a href="document.doc">DOC</a>        <!-- Pas rouge -->
```

**Exemple pratique : Icônes selon l'extension**
```css
/* Fichiers PDF */
a[href$=".pdf"]::after {
  content: " 📄";
}

/* Fichiers ZIP */
a[href$=".zip"]::after {
  content: " 📦";
}

/* Images */
a[href$=".jpg"]::after,
a[href$=".png"]::after {
  content: " 🖼️";
}
```

#### 5. Contient la sous-chaîne `[attr*="valeur"]`

```css
[href*="youtube"] {
  color: red;
}
```

**HTML :**
```html
<a href="https://www.youtube.com/watch">YouTube</a>     <!-- Rouge -->
<a href="https://youtu.be/abc123">YouTube court</a>     <!-- Rouge -->
<a href="https://vimeo.com/video">Vimeo</a>             <!-- Pas rouge -->
```

#### 6. Commence par (avec tiret optionnel) `[attr|="valeur"]`

Utilisé principalement pour les codes de langue.

```css
[lang|="fr"] {
  color: blue;
}
```

**HTML :**
```html
<p lang="fr">Texte en français</p>           <!-- Bleu -->
<p lang="fr-FR">Texte en français (France)</p> <!-- Bleu -->
<p lang="en">Texte en anglais</p>            <!-- Pas bleu -->
```

### Récapitulatif des sélecteurs d'attribut

| Syntaxe | Description | Exemple |
|---------|-------------|---------|
| `[attr]` | Attribut présent | `[title]` |
| `[attr="valeur"]` | Égalité exacte | `[type="text"]` |
| `[attr~="valeur"]` | Contient le mot | `[class~="important"]` |
| `[attr^="valeur"]` | Commence par | `[href^="https"]` |
| `[attr$="valeur"]` | Se termine par | `[href$=".pdf"]` |
| `[attr*="valeur"]` | Contient la sous-chaîne | `[href*="youtube"]` |
| `[attr|="valeur"]` | Commence par (avec `-`) | `[lang|="fr"]` |

### Exemples pratiques

**1. Styliser les liens externes :**
```css
/* Liens qui commencent par http (externes) */
a[href^="http"] {
  color: orange;
}

a[href^="http"]::after {
  content: " ↗";
  font-size: 0.8em;
}
```

**2. Différencier les types de fichiers :**
```css
/* PDFs */
a[href$=".pdf"] {
  background: url('icons/pdf.png') no-repeat left center;
  padding-left: 20px;
}

/* Documents Word */
a[href$=".doc"],
a[href$=".docx"] {
  background: url('icons/word.png') no-repeat left center;
  padding-left: 20px;
}
```

**3. Styliser les champs requis :**
```css
input[required] {
  border-left: 3px solid red;
}
```

**4. Désactiver visuellement les éléments disabled :**
```css
input[disabled],
button[disabled] {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Combinaison avec d'autres sélecteurs

Les sélecteurs d'attribut peuvent être combinés avec d'autres sélecteurs :

```css
/* Seulement les inputs de type text */
input[type="text"] {
  border: 1px solid gray;
}

/* Seulement les divs avec l'attribut data-role */
div[data-role="banner"] {
  background: yellow;
}

/* Seulement les liens de classe "button" qui sont externes */
a.button[href^="http"] {
  border: 2px solid orange;
}
```

---

## Comparaison des quatre sélecteurs simples

| Sélecteur | Syntaxe | Cible | Usage | Spécificité |
|-----------|---------|-------|-------|-------------|
| **Élément** | `p` | Tous les `<p>` | Styles globaux | Basse |
| **Classe** | `.intro` | `class="intro"` | ✅ Le plus utilisé | Moyenne |
| **ID** | `#header` | `id="header"` | Élément unique | Haute |
| **Attribut** | `[type="text"]` | Attribut spécifique | Cas spécifiques | Moyenne |

### Ordre de priorité (spécificité)

Si plusieurs règles ciblent le même élément, l'ordre de priorité est :

**ID > Classe/Attribut > Élément**

**Exemple :**
```html
<p id="special" class="intro">Quelle couleur ?</p>
```

```css
p {
  color: blue;        /* Spécificité : 1 */
}

.intro {
  color: green;       /* Spécificité : 10 */
}

#special {
  color: red;         /* Spécificité : 100 - GAGNE */
}
```

**Résultat :** Le paragraphe sera **rouge** (l'ID a la priorité la plus haute).

*Note : Nous verrons la spécificité en détail dans la section 4.1.7.*

---

## Bonnes pratiques

### ✅ À FAIRE

**1. Privilégier les classes pour le CSS**
```css
/* ✅ Recommandé */
.header { }
.button { }
.card { }
```

**2. Utiliser des noms de classes descriptifs**
```css
/* ✅ Clair et compréhensible */
.product-card { }
.user-profile { }
.navigation-menu { }

/* ❌ Vague et confus */
.box1 { }
.thing { }
.temp { }
```

**3. Utiliser le kebab-case**
```css
/* ✅ Cohérent */
.main-navigation { }
.card-title { }
.button-primary { }
```

**4. Être spécifique mais pas trop**
```css
/* ✅ Bon équilibre */
.blog-post { }
.blog-post-title { }
.blog-post-meta { }

/* ❌ Trop spécifique */
.homepage-main-section-blog-posts-container-item-title { }
```

**5. Utiliser les sélecteurs d'attribut pour les cas spécifiques**
```css
/* ✅ Pratique pour les formulaires */
input[type="email"] { }
input[required] { }
a[href^="http"] { }
```

### ❌ À ÉVITER

**1. Éviter les IDs pour le style**
```css
/* ❌ À éviter */
#header { }
#main { }
#footer { }

/* ✅ Préférer */
.header { }
.main { }
.footer { }
```

**2. Éviter les noms génériques**
```css
/* ❌ Trop vague */
.text { }
.box { }
.item { }

/* ✅ Plus descriptif */
.article-text { }
.product-box { }
.menu-item { }
```

**3. Éviter les noms basés sur l'apparence**
```css
/* ❌ Que se passe-t-il si vous changez la couleur ? */
.blue-text { }
.big-title { }

/* ✅ Basé sur la fonction/sémantique */
.primary-text { }
.page-title { }
```

**4. Ne pas surcharger avec trop de classes**
```html
<!-- ❌ Trop de classes -->
<button class="btn btn-primary btn-large btn-rounded btn-shadow btn-hover btn-animated">
  Cliquez
</button>

<!-- ✅ Classes essentielles seulement -->
<button class="btn btn-primary btn-large">
  Cliquez
</button>
```

---

## Exemples pratiques complets

### Exemple 1 : Card (Carte) de produit

**HTML :**
```html
<article class="product-card">
  <img src="produit.jpg" alt="Produit" class="product-image">
  <h3 class="product-title">Nom du Produit</h3>
  <p class="product-price">29.99€</p>
  <button class="btn btn-primary">Acheter</button>
</article>
```

**CSS :**
```css
/* Card principale */
.product-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  background: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* Image du produit */
.product-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 4px;
}

/* Titre du produit */
.product-title {
  font-size: 18px;
  color: #333;
  margin: 15px 0 10px;
}

/* Prix */
.product-price {
  font-size: 24px;
  color: #e74c3c;
  font-weight: bold;
  margin-bottom: 15px;
}

/* Bouton générique */
.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

/* Bouton primaire */
.btn-primary {
  background: #3498db;
  color: white;
}

.btn-primary:hover {
  background: #2980b9;
}
```

### Exemple 2 : Formulaire

**HTML :**
```html
<form class="contact-form">
  <div class="form-group">
    <label for="name">Nom :</label>
    <input type="text" id="name" class="form-input" required>
  </div>

  <div class="form-group">
    <label for="email">Email :</label>
    <input type="email" id="email" class="form-input" required>
  </div>

  <button type="submit" class="btn btn-submit">Envoyer</button>
</form>
```

**CSS :**
```css
/* Formulaire */
.contact-form {
  max-width: 500px;
  margin: 0 auto;
}

/* Groupe de champs */
.form-group {
  margin-bottom: 20px;
}

/* Labels */
.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #333;
}

/* Inputs */
.form-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
}

/* Inputs au focus */
.form-input:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 5px rgba(52, 152, 219, 0.3);
}

/* Inputs requis avec une bordure spéciale */
.form-input[required] {
  border-left: 3px solid #e74c3c;
}

/* Bouton de soumission */
.btn-submit {
  background: #27ae60;
  color: white;
  padding: 12px 30px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  width: 100%;
}

.btn-submit:hover {
  background: #229954;
}
```

### Exemple 3 : Navigation avec liens externes

**HTML :**
```html
<nav class="main-nav">
  <a href="index.html" class="nav-link">Accueil</a>
  <a href="about.html" class="nav-link">À propos</a>
  <a href="https://blog.example.com" class="nav-link">Blog</a>
  <a href="contact.html" class="nav-link">Contact</a>
</nav>
```

**CSS :**
```css
/* Navigation */
.main-nav {
  background: #2c3e50;
  padding: 15px;
}

/* Liens de navigation */
.nav-link {
  color: white;
  text-decoration: none;
  padding: 10px 15px;
  margin: 0 5px;
  border-radius: 4px;
  transition: background 0.3s;
}

.nav-link:hover {
  background: #34495e;
}

/* Liens externes (commencent par http) */
.nav-link[href^="http"] {
  position: relative;
}

.nav-link[href^="http"]::after {
  content: " ↗";
  font-size: 0.8em;
  margin-left: 3px;
}
```

---

## Résumé

### Les quatre sélecteurs simples

**1. Sélecteur d'élément :**
```css
p { color: blue; }          /* Tous les <p> */
```

**2. Sélecteur de classe ✅ LE PLUS UTILISÉ :**
```css
.intro { color: blue; }     /* class="intro" */
```

**3. Sélecteur d'ID :**
```css
#header { color: blue; }    /* id="header" */
```

**4. Sélecteur d'attribut :**
```css
[type="text"] { border: 1px solid gray; }
```

### Points clés à retenir

- 📌 **Privilégiez les classes** pour vos styles CSS
- 📌 **Les IDs sont uniques** - un seul par page
- 📌 **Les classes sont réutilisables** - plusieurs fois
- 📌 **Utilisez des noms descriptifs** et cohérents
- 📌 **Le kebab-case est recommandé** pour les classes
- 📌 **Les sélecteurs d'attribut** sont puissants pour les cas spécifiques
- 📌 **Un élément peut avoir plusieurs classes**
- 📌 **Spécificité : ID > Classe > Élément**

### Checklist de bonnes pratiques

- ✅ Utiliser principalement des **classes** pour le CSS
- ✅ Réserver les **IDs** pour JavaScript et les ancres
- ✅ Choisir des **noms descriptifs** et significatifs
- ✅ Utiliser le **kebab-case** : `.my-class`
- ✅ Être **cohérent** dans le nommage
- ✅ Utiliser les **sélecteurs d'attribut** pour les formulaires
- ✅ Éviter les noms basés sur l'apparence
- ✅ Garder les sélecteurs **simples et maintenables**

---

## Prochaine étape

Vous maîtrisez maintenant les quatre sélecteurs simples de base ! Dans la section suivante (4.1.4), nous découvrirons les **combinateurs CSS**, qui permettent de cibler des éléments en fonction de leur **relation avec d'autres éléments** (parent, enfant, frère, etc.).

Les combinateurs vous donneront encore plus de précision et de puissance dans votre ciblage d'éléments !

---

**Navigation :**

- ➡️ Section suivante : [4.1.4 Combinateurs](./04-combinateurs.md)
- 🏠 Retour à la [Table des matières](../../SOMMAIRE.md)

⏭️ [Combinateurs : descendant, enfant direct, frère adjacent](/04-css3-styles-et-mise-en-page/01-syntaxe-et-selecteurs/04-combinateurs.md)
