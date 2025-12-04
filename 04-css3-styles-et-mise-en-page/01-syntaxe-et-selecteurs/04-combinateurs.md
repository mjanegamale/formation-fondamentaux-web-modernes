🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.1.4 Combinateurs : descendant, enfant direct, frère adjacent

## Introduction

Les **combinateurs CSS** sont des symboles qui permettent de créer des **relations entre les sélecteurs**. Ils vous permettent de cibler des éléments non pas isolément, mais en fonction de leur **position dans l'arbre HTML** par rapport à d'autres éléments.

Au lieu de cibler "tous les paragraphes", vous pourrez cibler "les paragraphes qui sont à l'intérieur d'un article" ou "le paragraphe qui suit directement un titre".

Dans cette section, nous allons découvrir les quatre combinateurs principaux :
1. **Combinateur descendant** (espace ` `)
2. **Combinateur enfant direct** (`>`)
3. **Combinateur frère adjacent** (`+`)
4. **Combinateur frère général** (`~`)

---

## Comprendre l'arbre HTML

Avant d'étudier les combinateurs, il est essentiel de comprendre la notion de **hiérarchie HTML**.

### Structure arborescente

Le HTML fonctionne comme un arbre généalogique :

```html
<article>                    <!-- Parent/Ancêtre -->
  <h2>Titre</h2>            <!-- Enfant de article -->
  <div>                     <!-- Enfant de article, Parent de p -->
    <p>Paragraphe 1</p>     <!-- Enfant de div, Descendant de article -->
    <p>Paragraphe 2</p>     <!-- Frère de p précédent -->
  </div>
  <footer>                  <!-- Enfant de article, Frère de div -->
    <span>Info</span>       <!-- Enfant de footer -->
  </footer>
</article>
```

### Vocabulaire important

**Parent** : élément qui contient directement un autre élément
```html
<div>              <!-- div est le parent de p -->
  <p>Texte</p>     <!-- p est l'enfant de div -->
</div>
```

**Enfant** : élément directement contenu dans un autre élément

**Descendant** : élément contenu dans un autre, directement ou non
```html
<article>          <!-- article est l'ancêtre de span -->
  <div>            <!-- div est entre les deux -->
    <span>Texte</span>  <!-- span est le descendant de article -->
  </div>
</article>
```

**Frère (sibling)** : éléments qui partagent le même parent
```html
<div>
  <p>Paragraphe 1</p>    <!-- Frère de p suivant -->
  <p>Paragraphe 2</p>    <!-- Frère de p précédent -->
</div>
```

**Visualisation :**
```
article
├── h2 (enfant direct)
├── div (enfant direct, frère de h2 et footer)
│   ├── p (enfant de div, descendant de article)
│   └── p (enfant de div, frère du p précédent)
└── footer (enfant direct, frère de h2 et div)
    └── span (enfant de footer, descendant de article)
```

---

## 1. Combinateur descendant (espace ` `)

### Syntaxe

```css
sélecteur1 sélecteur2 {
  propriété: valeur;
}
```

Le combinateur descendant utilise simplement un **espace** entre deux sélecteurs.

### Signification

Cible **tous les éléments** correspondant à `sélecteur2` qui sont **à l'intérieur** de `sélecteur1`, peu importe le niveau de profondeur.

### Exemple simple

**CSS :**
```css
article p {
  color: blue;
}
```

**HTML :**
```html
<article>
  <p>Je serai bleu</p>          <!-- ✅ Ciblé : p dans article -->
  <div>
    <p>Je serai bleu aussi</p>   <!-- ✅ Ciblé : p dans div dans article -->
  </div>
</article>

<p>Je ne serai pas bleu</p>     <!-- ❌ Pas ciblé : p hors de article -->
```

**Tous les paragraphes à l'intérieur d'un `<article>` seront bleus**, qu'ils soient enfants directs ou plus profondément imbriqués.

### Exemples pratiques

**1. Cibler les liens dans la navigation :**
```css
nav a {
  color: white;
  text-decoration: none;
}
```

**HTML correspondant :**
```html
<nav>
  <a href="#">Lien 1</a>        <!-- ✅ Ciblé -->
  <ul>
    <li><a href="#">Lien 2</a></li>  <!-- ✅ Ciblé aussi -->
  </ul>
</nav>

<a href="#">Lien hors nav</a>   <!-- ❌ Pas ciblé -->
```

**2. Styliser les paragraphes dans un article :**
```css
.blog-post p {
  line-height: 1.8;
  margin-bottom: 15px;
}
```

**3. Cibler plusieurs niveaux :**
```css
header nav ul li a {
  color: white;
}
```

**HTML :**
```html
<header>
  <nav>
    <ul>
      <li>
        <a href="#">Ce lien sera blanc</a>
      </li>
    </ul>
  </nav>
</header>
```

### Profondeur illimitée

Le combinateur descendant fonctionne à **n'importe quelle profondeur** :

**CSS :**
```css
div span {
  color: red;
}
```

**HTML :**
```html
<div>
  <span>Rouge - niveau 1</span>                    <!-- ✅ -->
  <p>
    <span>Rouge - niveau 2</span>                  <!-- ✅ -->
    <strong>
      <span>Rouge - niveau 3</span>                <!-- ✅ -->
    </strong>
  </p>
</div>
```

**Tous les `<span>` à l'intérieur du `<div>` seront rouges**, peu importe le nombre de niveaux.

### ⚠️ Attention à la sur-qualification

**❌ Éviter les chaînes trop longues :**
```css
body div.container main article.post div.content p.text {
  color: blue;
}
```

**Problèmes :**
- Difficile à lire
- Haute spécificité (difficile à surcharger)
- Rigide (peu réutilisable)

**✅ Préférer des sélecteurs plus simples :**
```css
.post-content p {
  color: blue;
}
```

---

## 2. Combinateur enfant direct (`>`)

### Syntaxe

```css
sélecteur1 > sélecteur2 {
  propriété: valeur;
}
```

### Signification

Cible **uniquement les éléments** correspondant à `sélecteur2` qui sont des **enfants directs** (premier niveau) de `sélecteur1`.

### Différence avec le descendant

**Combinateur descendant (espace) :** tous les niveaux
**Combinateur enfant direct (`>`) :** seulement le premier niveau

### Exemple comparatif

**CSS :**
```css
/* Descendant : tous les p dans article */
article p {
  color: blue;
}

/* Enfant direct : seulement les p directement dans article */
article > p {
  color: red;
}
```

**HTML :**
```html
<article>
  <p>Je serai ROUGE (enfant direct)</p>

  <div>
    <p>Je serai BLEU (descendant mais pas enfant direct)</p>
  </div>

  <p>Je serai ROUGE (enfant direct)</p>
</article>
```

**Résultat :**
- Les `<p>` enfants directs de `<article>` → rouges (règle plus spécifique)
- Les `<p>` plus profonds → bleus (règle descendant)

### Exemples pratiques

**1. Menu de navigation avec sous-menus :**
```css
/* Seulement les li de premier niveau */
nav > ul > li {
  display: inline-block;
  margin: 0 10px;
}

/* Les li des sous-menus */
nav ul ul li {
  display: block;
  margin: 5px 0;
}
```

**HTML :**
```html
<nav>
  <ul>
    <li>Menu 1</li>              <!-- Style premier niveau -->
    <li>Menu 2
      <ul>
        <li>Sous-menu</li>       <!-- Style sous-menu -->
      </ul>
    </li>
  </ul>
</nav>
```

**2. Styliser uniquement les enfants directs d'un conteneur :**
```css
.container > div {
  padding: 20px;
  border: 1px solid #ddd;
}
```

**HTML :**
```html
<div class="container">
  <div>Sera stylisé</div>        <!-- ✅ Enfant direct -->

  <section>
    <div>Ne sera PAS stylisé</div>  <!-- ❌ Pas enfant direct -->
  </section>
</div>
```

**3. Cards avec sections :**
```css
.card > header {
  background: navy;
  color: white;
  padding: 15px;
}

.card > footer {
  background: #f4f4f4;
  padding: 10px;
  text-align: center;
}
```

### Cas d'usage typiques

Le combinateur enfant direct est particulièrement utile pour :
- **Menus à plusieurs niveaux** (différencier les niveaux)
- **Grilles et layouts** (cibler seulement les enfants directs)
- **Composants structurés** (header, body, footer d'une card)
- **Éviter les effets en cascade** non désirés

---

## 3. Combinateur frère adjacent (`+`)

### Syntaxe

```css
sélecteur1 + sélecteur2 {
  propriété: valeur;
}
```

### Signification

Cible **l'élément** correspondant à `sélecteur2` qui **suit immédiatement** un élément correspondant à `sélecteur1`, au même niveau dans l'arbre HTML.

**Conditions :**
- Les deux éléments doivent avoir le **même parent**
- `sélecteur2` doit venir **juste après** `sélecteur1`
- Cible **uniquement le premier** élément qui suit

### Exemple simple

**CSS :**
```css
h2 + p {
  font-size: 18px;
  font-weight: bold;
}
```

**HTML :**
```html
<h2>Titre</h2>
<p>Ce paragraphe suit directement h2 → sera stylisé</p>
<p>Ce paragraphe ne suit pas directement h2 → pas stylisé</p>
```

**Seul le premier paragraphe après le `<h2>` sera stylisé.**

### Visualisation

```html
<div>
  <h2>Titre</h2>         ← élément de référence
  <p>Ciblé ✅</p>        ← suit immédiatement (frère adjacent)
  <p>Pas ciblé ❌</p>    ← ne suit pas immédiatement
</div>
```

### Exemples pratiques

**1. Paragraphe d'introduction après un titre :**
```css
h1 + p {
  font-size: 20px;
  color: #666;
  font-style: italic;
}
```

**HTML :**
```html
<article>
  <h1>Mon Article</h1>
  <p>Premier paragraphe (intro) - sera stylisé</p>
  <p>Deuxième paragraphe - style normal</p>
</article>
```

**2. Espacement après un élément spécifique :**
```css
.alert + .content {
  margin-top: 30px;
}
```

**HTML :**
```html
<div class="alert">Message d'alerte</div>
<div class="content">Contenu qui suit - aura une marge de 30px</div>
```

**3. Checkbox personnalisée :**
```css
/* Styliser le label qui suit immédiatement un checkbox */
input[type="checkbox"] + label {
  padding-left: 25px;
  cursor: pointer;
}
```

**HTML :**
```html
<input type="checkbox" id="terms">
<label for="terms">J'accepte les conditions</label>
```

**4. Supprimer la bordure entre éléments adjacents :**
```css
.list-item {
  border-bottom: 1px solid #ddd;
}

.list-item + .list-item {
  border-top: none;  /* Évite la double bordure */
}
```

### ⚠️ Important : suit IMMÉDIATEMENT

Le combinateur `+` est très strict. Il faut que l'élément suive **directement** :

```html
<style>
  h2 + p {
    color: red;
  }
</style>

<h2>Titre</h2>
<p>Rouge ✅</p>

<h2>Autre Titre</h2>
<div></div>           <!-- Élément intermédiaire ! -->
<p>Pas rouge ❌</p>   <!-- Ne suit pas DIRECTEMENT h2 -->
```

---

## 4. Combinateur frère général (`~`)

### Syntaxe

```css
sélecteur1 ~ sélecteur2 {
  propriété: valeur;
}
```

### Signification

Cible **tous les éléments** correspondant à `sélecteur2` qui **suivent** (pas nécessairement immédiatement) un élément correspondant à `sélecteur1`, au même niveau.

### Différence avec le frère adjacent (`+`)

**Frère adjacent (`+`) :** seulement le premier élément qui suit **immédiatement**
**Frère général (`~`) :** tous les éléments qui suivent (même s'il y a d'autres éléments entre)

### Exemple comparatif

**CSS :**
```css
/* Frère adjacent : seulement le p qui suit immédiatement */
h2 + p {
  color: red;
}

/* Frère général : tous les p qui suivent */
h2 ~ p {
  color: blue;
}
```

**HTML :**
```html
<div>
  <h2>Titre</h2>
  <p>Rouge (adjacent) et Bleu (général)</p>
  <div>Élément intermédiaire</div>
  <p>Bleu (général, pas adjacent car div entre les deux)</p>
  <p>Bleu (général)</p>
</div>
```

### Exemples pratiques

**1. Styliser tous les paragraphes après un titre :**
```css
h2 ~ p {
  margin-left: 20px;
}
```

**HTML :**
```html
<article>
  <p>Pas affecté (avant h2)</p>

  <h2>Section</h2>
  <p>Marge de 20px</p>
  <blockquote>Citation</blockquote>
  <p>Marge de 20px aussi</p>
</article>
```

**2. Afficher/masquer du contenu :**
```css
/* Au clic sur le checkbox, afficher les éléments suivants */
#toggle:checked ~ .content {
  display: block;
}
```

**HTML :**
```html
<input type="checkbox" id="toggle">
<label for="toggle">Afficher plus</label>
<div class="content" style="display: none;">
  Contenu caché
</div>
```

**3. Effet sur tous les éléments après le survol :**
```css
.item:hover ~ .item {
  opacity: 0.5;
}
```

**HTML :**
```html
<div>
  <div class="item">1</div>
  <div class="item">2</div>  <!-- Au survol de 1, 2 et 3 deviennent semi-transparents -->
  <div class="item">3</div>
</div>
```

---

## Comparaison des quatre combinateurs

| Combinateur | Syntaxe | Cible | Exemple |
|-------------|---------|-------|---------|
| **Descendant** | `A B` | Tous les B dans A (tous niveaux) | `article p` |
| **Enfant direct** | `A > B` | Seulement les B enfants directs de A | `article > p` |
| **Frère adjacent** | `A + B` | Le B qui suit immédiatement A | `h2 + p` |
| **Frère général** | `A ~ B` | Tous les B qui suivent A | `h2 ~ p` |

### Visualisation complète

```html
<article>              <!-- Ancêtre -->
  <h2>Titre</h2>       <!-- Référence pour frères -->
  <p>P1</p>            <!-- Enfant direct + Frère adjacent de h2 -->
  <div>                <!-- Enfant direct -->
    <p>P2</p>          <!-- Descendant (pas enfant direct) -->
  </div>
  <p>P3</p>            <!-- Enfant direct + Frère général de h2 -->
  <p>P4</p>            <!-- Enfant direct + Frère général de h2 -->
</article>
```

**Règles CSS :**
```css
article p        { }  /* P1, P2, P3, P4 (tous les p dans article) */
article > p      { }  /* P1, P3, P4 (seulement enfants directs) */
h2 + p           { }  /* P1 (seulement le p adjacent à h2) */
h2 ~ p           { }  /* P1, P3, P4 (tous les p après h2, même niveau) */
```

---

## Combinaison de combinateurs

Vous pouvez **combiner plusieurs combinateurs** pour des sélections très précises :

### Exemples

**1. Paragraphe qui suit un titre dans un article :**
```css
article h2 + p {
  font-style: italic;
}
```

**2. Liens dans les li enfants directs d'une nav :**
```css
nav > ul > li > a {
  color: white;
}
```

**3. Span dans les paragraphes d'une section :**
```css
section.intro p > span {
  font-weight: bold;
}
```

**4. Élément avec classe après un titre :**
```css
h2 + .highlight {
  background: yellow;
}
```

### ⚠️ Attention à la complexité

**Éviter les sélecteurs trop complexes :**
```css
/* ❌ Trop complexe et difficile à maintenir */
body > main > article > section > div > ul > li > a:hover {
  color: red;
}

/* ✅ Plus simple et maintenable */
.article-link:hover {
  color: red;
}
```

---

## Cas pratiques complets

### Exemple 1 : Article de blog

**HTML :**
```html
<article class="blog-post">
  <h1>Titre de l'article</h1>
  <p class="intro">Paragraphe d'introduction</p>

  <h2>Première section</h2>
  <p>Contenu de la première section</p>
  <p>Suite du contenu</p>

  <h2>Deuxième section</h2>
  <p>Contenu de la deuxième section</p>
</article>
```

**CSS :**
```css
/* Tous les paragraphes de l'article */
.blog-post p {
  line-height: 1.8;
  margin-bottom: 15px;
}

/* Premier paragraphe après le titre principal (intro) */
.blog-post h1 + p {
  font-size: 18px;
  color: #666;
  font-style: italic;
}

/* Premier paragraphe après chaque h2 */
.blog-post h2 + p {
  font-weight: bold;
}

/* Tous les h2 (sauf le premier) */
.blog-post h2 ~ h2 {
  margin-top: 40px;
}
```

### Exemple 2 : Navigation à deux niveaux

**HTML :**
```html
<nav class="main-nav">
  <ul>
    <li><a href="#">Accueil</a></li>
    <li>
      <a href="#">Services</a>
      <ul>
        <li><a href="#">Service 1</a></li>
        <li><a href="#">Service 2</a></li>
      </ul>
    </li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

**CSS :**
```css
/* Menu de premier niveau */
.main-nav > ul > li {
  display: inline-block;
  position: relative;
}

/* Liens de premier niveau */
.main-nav > ul > li > a {
  padding: 15px 20px;
  color: white;
  background: navy;
  display: block;
}

/* Sous-menus (cachés par défaut) */
.main-nav ul ul {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
}

/* Afficher le sous-menu au survol du parent */
.main-nav > ul > li:hover > ul {
  display: block;
}

/* Liens du sous-menu */
.main-nav ul ul li a {
  padding: 10px 15px;
  background: #444;
  color: white;
  display: block;
  white-space: nowrap;
}

/* Liens du sous-menu au survol */
.main-nav ul ul li a:hover {
  background: #666;
}
```

### Exemple 3 : Formulaire avec validation visuelle

**HTML :**
```html
<form class="contact-form">
  <div>
    <label for="name">Nom :</label>
    <input type="text" id="name" required>
  </div>

  <div>
    <label for="email">Email :</label>
    <input type="email" id="email" required>
  </div>

  <button type="submit">Envoyer</button>
</form>
```

**CSS :**
```css
/* Tous les inputs du formulaire */
.contact-form input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
}

/* Input qui suit directement un label */
.contact-form label + input {
  margin-top: 5px;
}

/* Input valide */
.contact-form input:valid {
  border-color: green;
}

/* Input invalide qui a été modifié */
.contact-form input:invalid:not(:placeholder-shown) {
  border-color: red;
}

/* Div qui suit une div dans le formulaire */
.contact-form div + div {
  margin-top: 20px;
}

/* Bouton qui suit les divs */
.contact-form div ~ button {
  margin-top: 25px;
}
```

### Exemple 4 : Liste avec séparateurs

**HTML :**
```html
<ul class="breadcrumb">
  <li><a href="#">Accueil</a></li>
  <li><a href="#">Catégorie</a></li>
  <li><a href="#">Sous-catégorie</a></li>
  <li>Page actuelle</li>
</ul>
```

**CSS :**
```css
/* Liste horizontale */
.breadcrumb {
  list-style: none;
  display: flex;
}

/* Éléments de la liste */
.breadcrumb li {
  color: #666;
}

/* Ajouter un séparateur après chaque li */
.breadcrumb li + li::before {
  content: " / ";
  margin: 0 10px;
  color: #999;
}

/* Dernier élément en gras */
.breadcrumb li:last-child {
  font-weight: bold;
  color: #333;
}
```

---

## Erreurs courantes à éviter

### 1. Confondre descendant et enfant direct

**❌ Erreur :**
```css
/* Voulait cibler seulement les enfants directs */
nav ul li {
  display: inline-block;
}
```

**Problème :** Cible aussi les `<li>` des sous-menus !

**✅ Solution :**
```css
nav > ul > li {
  display: inline-block;
}
```

### 2. Oublier que les frères doivent être au même niveau

**❌ Ne fonctionnera pas :**
```html
<div>
  <h2>Titre</h2>
</div>
<p>Paragraphe</p>  <!-- Pas au même niveau que h2 ! -->
```

```css
h2 + p {
  color: red;  /* Ne fonctionnera PAS */
}
```

### 3. Chaînes de sélecteurs trop longues

**❌ Trop spécifique :**
```css
body > main > section > article > div > p {
  color: blue;
}
```

**✅ Plus simple :**
```css
.article-content p {
  color: blue;
}
```

### 4. Utiliser `+` au lieu de `~`

**Si vous voulez cibler plusieurs éléments :**
```css
/* ❌ Cible seulement le premier */
h2 + p {
  margin-left: 20px;
}

/* ✅ Cible tous les p après h2 */
h2 ~ p {
  margin-left: 20px;
}
```

---

## Performance et bonnes pratiques

### Conseils de performance

**1. Les navigateurs lisent les sélecteurs de droite à gauche**

```css
/* Le navigateur trouve d'abord TOUS les p, puis filtre ceux dans article */
article p { }

/* Mieux : commence par .article-text (plus spécifique) */
.article-text { }
```

**2. Éviter les sélecteurs universels dans les combinateurs**

```css
/* ❌ Très lent : vérifie tous les éléments */
div * {
  margin: 0;
}

/* ✅ Mieux : cibler spécifiquement */
div > p,
div > h2 {
  margin: 0;
}
```

**3. Limiter la profondeur**

```css
/* ❌ Trop profond */
body main section article div p span { }

/* ✅ Maximum 3-4 niveaux */
.article p span { }
```

### Bonnes pratiques

**✅ À FAIRE :**

1. **Utiliser des classes quand c'est pertinent**
```css
/* ✅ Clair et efficace */
.intro-paragraph { }

/* Au lieu de */
article > h1 + p { }
```

2. **Combiner classes et combinateurs**
```css
.nav > .nav-item > .nav-link { }
```

3. **Commenter les sélecteurs complexes**
```css
/* Premier paragraphe de chaque section */
.article h2 + p {
  font-weight: bold;
}
```

**❌ À ÉVITER :**

1. **Sélecteurs trop génériques**
```css
/* ❌ Affecte tous les p partout */
div p { }
```

2. **Chaînes inutilement longues**
```css
/* ❌ Trop spécifique */
html body div.container main article p { }

/* ✅ Suffisant */
.container p { }
```

3. **Répétition de styles**
```css
/* ❌ Répétitif */
h2 + p { font-weight: bold; }
h3 + p { font-weight: bold; }
h4 + p { font-weight: bold; }

/* ✅ Groupé */
h2 + p,
h3 + p,
h4 + p {
  font-weight: bold;
}
```

---

## Résumé

### Les quatre combinateurs

**1. Descendant (espace)** : `A B`
- Tous les B dans A, tous niveaux
- Le plus large

**2. Enfant direct** : `A > B`
- Seulement les B enfants directs de A
- Premier niveau uniquement

**3. Frère adjacent** : `A + B`
- Le B qui suit immédiatement A
- Même parent, immédiatement après

**4. Frère général** : `A ~ B`
- Tous les B qui suivent A
- Même parent, après (pas forcément immédiatement)

### Tableau récapitulatif

| Combinateur | Relation | Exemple | Cible |
|-------------|----------|---------|-------|
| ` ` (espace) | Descendant | `div p` | Tous les `<p>` dans `<div>` |
| `>` | Enfant direct | `div > p` | `<p>` enfants directs de `<div>` |
| `+` | Frère adjacent | `h2 + p` | `<p>` juste après `<h2>` |
| `~` | Frère général | `h2 ~ p` | Tous `<p>` après `<h2>` |

### Points clés à retenir

- 📌 **Les combinateurs créent des relations** entre sélecteurs
- 📌 **L'espace est un combinateur** (descendant)
- 📌 **`>` cible seulement les enfants directs**, pas les descendants
- 📌 **`+` cible UN élément** qui suit immédiatement
- 📌 **`~` cible TOUS les éléments** qui suivent
- 📌 **Les frères doivent avoir le même parent**
- 📌 **Éviter les chaînes trop longues** (max 3-4 niveaux)
- 📌 **Combiner avec des classes** pour plus de clarté

### Checklist d'utilisation

- ✅ Ai-je besoin de tous les niveaux ? → **espace**
- ✅ Seulement le premier niveau ? → **`>`**
- ✅ L'élément qui suit immédiatement ? → **`+`**
- ✅ Tous les éléments qui suivent ? → **`~`**
- ✅ Mon sélecteur est-il trop long ? → Simplifier avec des classes
- ✅ Est-ce que c'est lisible ? → Ajouter des commentaires

---

## Prochaine étape

Vous maîtrisez maintenant les combinateurs qui permettent de créer des relations entre éléments ! Dans la section suivante (4.1.5), nous découvrirons les **pseudo-classes** comme `:hover`, `:focus`, `:nth-child`, qui permettent de cibler des éléments selon leur **état** ou leur **position**.

Ces pseudo-classes vont encore élargir vos possibilités de ciblage et vous permettre de créer des interactions dynamiques !

---

**Navigation :**

- ➡️ Section suivante : [4.1.5 Pseudo-classes](./05-pseudo-classes.md)
- 🏠 Retour à la [Table des matières](../../SOMMAIRE.md)

⏭️ [Pseudo-classes (:hover, :focus, :nth-child)](/04-css3-styles-et-mise-en-page/01-syntaxe-et-selecteurs/05-pseudo-classes.md)
