🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.1.6 Pseudo-éléments (::before, ::after)

## Introduction

Les **pseudo-éléments** sont des sélecteurs CSS spéciaux qui permettent de **créer et styliser des éléments virtuels** dans le DOM sans modifier le HTML. Ils ajoutent du contenu purement décoratif ou informatif directement via CSS.

À la différence des pseudo-classes (un seul `:`) qui ciblent des états, les pseudo-éléments (deux `::`) créent ou ciblent des parties spécifiques d'éléments existants.

Dans cette section, nous allons découvrir :
1. **`::before`** : ajoute du contenu avant un élément
2. **`::after`** : ajoute du contenu après un élément
3. **`::first-letter`** : stylise la première lettre
4. **`::first-line`** : stylise la première ligne
5. **`::selection`** : stylise le texte sélectionné

---

## Syntaxe : Double deux-points `::`

### Notation moderne vs ancienne

**Notation moderne (CSS3) - Recommandée :**
```css
élément::pseudo-élément {
  propriété: valeur;
}
```

**Notation ancienne (CSS2) - Toujours supportée :**
```css
élément:pseudo-élément {
  propriété: valeur;
}
```

**✅ Utilisez toujours la double notation `::` pour les pseudo-éléments :**
```css
p::before { }     /* ✅ Recommandé */
p::after { }      /* ✅ Recommandé */
```

**⚠️ La simple notation `:` fonctionne mais est obsolète :**
```css
p:before { }      /* ⚠️ Ancienne syntaxe */
p:after { }       /* ⚠️ Ancienne syntaxe */
```

### Différence pseudo-classe vs pseudo-élément

**Pseudo-classe (un `:`)** : cible un **état** ou une **condition**
```css
a:hover { }           /* État : survol */
p:first-child { }     /* Condition : position */
```

**Pseudo-élément (deux `::`)** : crée ou cible une **partie** d'un élément
```css
p::before { }         /* Crée du contenu avant */
p::first-letter { }   /* Cible une partie (première lettre) */
```

---

## 1. `::before` - Avant l'élément

### Qu'est-ce que `::before` ?

Le pseudo-élément `::before` crée un **élément virtuel** qui sera inséré **avant le contenu** de l'élément ciblé, en tant que premier enfant.

### Syntaxe

```css
sélecteur::before {
  content: "contenu";  /* Propriété OBLIGATOIRE */
  /* autres propriétés */
}
```

**⚠️ Important :** La propriété `content` est **obligatoire**, même si elle est vide (`content: "";`).

### Structure dans le DOM

```html
<p>Mon texte</p>
```

```css
p::before {
  content: "→ ";
}
```

**Rendu conceptuel :**
```html
<p>
  ::before → Mon texte
</p>
```

Le navigateur affichera : **→ Mon texte**

### Exemples simples

**1. Ajouter un symbole avant les titres :**
```css
h2::before {
  content: "★ ";
  color: gold;
}
```

**HTML :**
```html
<h2>Titre important</h2>
```

**Résultat :** ★ Titre important

**2. Ajouter du texte avant les liens externes :**
```css
a[href^="http"]::before {
  content: "🔗 ";
}
```

**HTML :**
```html
<a href="https://example.com">Lien externe</a>
```

**Résultat :** 🔗 Lien externe

**3. Numérotation automatique :**
```css
.chapter::before {
  content: "Chapitre " counter(chapter) " - ";
  font-weight: bold;
}
```

### La propriété `content`

La propriété `content` peut contenir différents types de valeurs :

#### 1. Texte simple

```css
p::before {
  content: "Note : ";
}
```

#### 2. Chaîne vide (pour élément purement décoratif)

```css
.box::before {
  content: "";
  display: block;
  width: 50px;
  height: 50px;
  background: blue;
}
```

#### 3. Caractères spéciaux / Emojis

```css
.important::before {
  content: "⚠️ ";
}

.success::before {
  content: "✓ ";
  color: green;
}
```

#### 4. Valeur d'attribut

```css
a::before {
  content: attr(href);
}
```

**HTML :**
```html
<a href="page.html">Lien</a>
```

**Résultat :** page.html Lien

**Usage typique - Afficher l'URL en impression :**
```css
@media print {
  a::after {
    content: " (" attr(href) ")";
  }
}
```

#### 5. URL d'image

```css
.icon::before {
  content: url('icon.png');
  margin-right: 5px;
}
```

#### 6. Guillemets typographiques

```css
q::before {
  content: "« ";
}

q::after {
  content: " »";
}
```

#### 7. Compteurs CSS

```css
h2 {
  counter-increment: section;
}

h2::before {
  content: counter(section) ". ";
}
```

---

## 2. `::after` - Après l'élément

### Qu'est-ce que `::after` ?

Le pseudo-élément `::after` crée un **élément virtuel** qui sera inséré **après le contenu** de l'élément ciblé, en tant que dernier enfant.

### Syntaxe

```css
sélecteur::after {
  content: "contenu";  /* Propriété OBLIGATOIRE */
  /* autres propriétés */
}
```

### Structure dans le DOM

```html
<p>Mon texte</p>
```

```css
p::after {
  content: " ✓";
}
```

**Rendu conceptuel :**
```html
<p>
  Mon texte ✓ ::after
</p>
```

Le navigateur affichera : **Mon texte ✓**

### Exemples simples

**1. Ajouter une flèche après les liens :**
```css
a::after {
  content: " →";
  color: blue;
}
```

**2. Badge "NEW" sur les nouveaux articles :**
```css
.new::after {
  content: "NEW";
  background: red;
  color: white;
  padding: 2px 6px;
  margin-left: 10px;
  font-size: 0.7em;
  border-radius: 3px;
}
```

**HTML :**
```html
<h3 class="new">Article récent</h3>
```

**Résultat :** Article récent **[NEW]** (en rouge)

**3. Indicateur de liens externes :**
```css
a[href^="http"]::after {
  content: " ↗";
  font-size: 0.8em;
  vertical-align: super;
}
```

---

## Combiner `::before` et `::after`

Vous pouvez utiliser les deux pseudo-éléments sur le même élément.

**Exemple - Guillemets décoratifs :**
```css
blockquote::before {
  content: """;
  font-size: 3em;
  color: #ccc;
}

blockquote::after {
  content: """;
  font-size: 3em;
  color: #ccc;
}
```

**HTML :**
```html
<blockquote>
  Une citation inspirante
</blockquote>
```

---

## Cas d'usage pratiques

### 1. Icônes et symboles décoratifs

**Ajouter des icônes sans images :**
```css
.email::before {
  content: "✉️ ";
  margin-right: 5px;
}

.phone::before {
  content: "📞 ";
  margin-right: 5px;
}

.location::before {
  content: "📍 ";
  margin-right: 5px;
}
```

**HTML :**
```html
<p class="email">contact@example.com</p>
<p class="phone">01 23 45 67 89</p>
<p class="location">Paris, France</p>
```

### 2. Effets de survol sur boutons

**Bouton avec animation de flèche :**
```css
.button {
  position: relative;
  padding: 10px 40px 10px 20px;
  background: blue;
  color: white;
  border: none;
  cursor: pointer;
}

.button::after {
  content: "→";
  position: absolute;
  right: 15px;
  top: 50%;
  transform: translateY(-50%);
  transition: right 0.3s;
}

.button:hover::after {
  right: 10px;
}
```

### 3. Lignes décoratives

**Titre avec lignes de part et d'autre :**
```css
.title-decorated {
  display: flex;
  align-items: center;
  text-align: center;
}

.title-decorated::before,
.title-decorated::after {
  content: "";
  flex: 1;
  height: 1px;
  background: #ddd;
}

.title-decorated::before {
  margin-right: 20px;
}

.title-decorated::after {
  margin-left: 20px;
}
```

**HTML :**
```html
<h2 class="title-decorated">Mon Titre</h2>
```

**Résultat :** ─────── Mon Titre ───────

### 4. Compteurs automatiques

**Liste numérotée personnalisée :**
```css
.custom-list {
  counter-reset: item;
  list-style: none;
  padding: 0;
}

.custom-list li {
  counter-increment: item;
  padding: 10px;
  position: relative;
  padding-left: 50px;
}

.custom-list li::before {
  content: counter(item);
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 35px;
  height: 35px;
  background: blue;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  font-weight: bold;
}
```

**HTML :**
```html
<ul class="custom-list">
  <li>Premier élément</li>
  <li>Deuxième élément</li>
  <li>Troisième élément</li>
</ul>
```

### 5. Tooltips (info-bulles) CSS

**Tooltip qui apparaît au survol :**
```css
.tooltip {
  position: relative;
  cursor: help;
  border-bottom: 1px dotted blue;
}

.tooltip::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  white-space: nowrap;
  font-size: 14px;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s;
  margin-bottom: 5px;
}

.tooltip::before {
  content: "";
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  border: 5px solid transparent;
  border-top-color: #333;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover::after,
.tooltip:hover::before {
  opacity: 1;
}
```

**HTML :**
```html
<span class="tooltip" data-tooltip="Ceci est une info-bulle">
  Survolez-moi
</span>
```

### 6. Badges et étiquettes

**Badge de notification :**
```css
.notification-icon {
  position: relative;
  display: inline-block;
  padding: 10px;
}

.notification-icon::after {
  content: attr(data-count);
  position: absolute;
  top: 0;
  right: 0;
  background: red;
  color: white;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: bold;
}
```

**HTML :**
```html
<span class="notification-icon" data-count="5">
  🔔
</span>
```

### 7. Clearfix (technique classique)

**Résoudre les problèmes de float :**
```css
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

### 8. Overlay sur images

**Effet d'overlay au survol d'image :**
```css
.image-overlay {
  position: relative;
  display: inline-block;
}

.image-overlay img {
  display: block;
  width: 100%;
}

.image-overlay::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  opacity: 0;
  transition: opacity 0.3s;
}

.image-overlay:hover::after {
  opacity: 1;
}
```

---

## 3. `::first-letter` - Première lettre

### Qu'est-ce que `::first-letter` ?

Le pseudo-élément `::first-letter` cible la **première lettre** d'un élément de type bloc.

### Syntaxe

```css
sélecteur::first-letter {
  propriété: valeur;
}
```

### Exemple - Lettrine (Drop cap)

**CSS :**
```css
p::first-letter {
  font-size: 3em;
  font-weight: bold;
  float: left;
  line-height: 1;
  margin-right: 5px;
  color: #8b0000;
}
```

**HTML :**
```html
<p>Il était une fois, dans un royaume lointain, une princesse...</p>
```

**Résultat :** La lettre **I** sera grande, en gras et rouge, comme dans les livres anciens.

### Propriétés applicables

Vous pouvez modifier :
- Propriétés de police : `font-size`, `font-weight`, `font-family`, `color`
- Marges et padding
- Bordures
- `float`, `text-transform`
- Propriétés de fond

**⚠️ Limitation :** Ne fonctionne que sur les éléments de type bloc.

---

## 4. `::first-line` - Première ligne

### Qu'est-ce que `::first-line` ?

Le pseudo-élément `::first-line` cible la **première ligne** d'un élément de type bloc.

**⚠️ Important :** La "première ligne" dépend de la **largeur de l'élément** et change dynamiquement si la fenêtre est redimensionnée.

### Syntaxe

```css
sélecteur::first-line {
  propriété: valeur;
}
```

### Exemple

**CSS :**
```css
p::first-line {
  font-weight: bold;
  text-transform: uppercase;
  color: navy;
}
```

**HTML :**
```html
<p>
  Cette première ligne sera en gras et en majuscules.
  Le reste du paragraphe aura un style normal même si
  le texte continue sur plusieurs lignes.
</p>
```

### Propriétés applicables

Moins de propriétés sont disponibles que pour `::first-letter` :
- Propriétés de police et de couleur
- `background`
- `text-decoration`, `text-transform`
- `line-height`, `letter-spacing`, `word-spacing`

**❌ Ne fonctionne PAS avec :** `margin`, `padding`, `border`, `width`, `height`

---

## 5. `::selection` - Texte sélectionné

### Qu'est-ce que `::selection` ?

Le pseudo-élément `::selection` permet de styliser le texte **sélectionné par l'utilisateur** (surligné en bleu par défaut).

### Syntaxe

```css
::selection {
  background: couleur;
  color: couleur;
}
```

### Exemple

**CSS :**
```css
::selection {
  background: #ffeb3b;
  color: #000;
}
```

**Résultat :** Quand vous sélectionnez du texte, il sera surligné en jaune avec du texte noir.

### Sélection spécifique à un élément

```css
p::selection {
  background: lightblue;
  color: darkblue;
}

code::selection {
  background: #2c3e50;
  color: #ecf0f1;
}
```

### Propriétés applicables

**Très limitées :**
- ✅ `color`
- ✅ `background-color`
- ✅ `cursor`
- ✅ `text-shadow`

**❌ La plupart des autres propriétés ne fonctionnent pas.**

### Préfixe pour Firefox (ancien)

```css
::selection {
  background: yellow;
}

/* Pour anciennes versions de Firefox */
::-moz-selection {
  background: yellow;
}
```

---

## Exemples pratiques complets

### Exemple 1 : Card avec coin décoratif

**HTML :**
```html
<div class="card">
  <h3>Titre de la card</h3>
  <p>Contenu de la card...</p>
</div>
```

**CSS :**
```css
.card {
  position: relative;
  padding: 20px;
  border: 2px solid #ddd;
  border-radius: 8px;
  background: white;
}

/* Coin décoratif en haut à droite */
.card::before {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 50px 50px 0;
  border-color: transparent #3498db transparent transparent;
}

/* Icône dans le coin */
.card::after {
  content: "★";
  position: absolute;
  top: 5px;
  right: 5px;
  color: white;
  font-size: 20px;
}
```

### Exemple 2 : Timeline verticale

**HTML :**
```html
<div class="timeline">
  <div class="timeline-item">
    <h4>2020</h4>
    <p>Événement 1</p>
  </div>
  <div class="timeline-item">
    <h4>2021</h4>
    <p>Événement 2</p>
  </div>
  <div class="timeline-item">
    <h4>2022</h4>
    <p>Événement 3</p>
  </div>
</div>
```

**CSS :**
```css
.timeline {
  position: relative;
  padding-left: 40px;
}

/* Ligne verticale */
.timeline::before {
  content: "";
  position: absolute;
  left: 15px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: #3498db;
}

.timeline-item {
  position: relative;
  margin-bottom: 30px;
  padding: 15px;
  background: white;
  border: 1px solid #ddd;
  border-radius: 8px;
}

/* Point sur la timeline */
.timeline-item::before {
  content: "";
  position: absolute;
  left: -31px;
  top: 20px;
  width: 12px;
  height: 12px;
  background: white;
  border: 3px solid #3498db;
  border-radius: 50%;
}
```

### Exemple 3 : Blockquote stylisée

**HTML :**
```html
<blockquote class="fancy-quote">
  Le succès n'est pas final, l'échec n'est pas fatal :
  c'est le courage de continuer qui compte.
</blockquote>
```

**CSS :**
```css
.fancy-quote {
  position: relative;
  padding: 30px 40px;
  background: #f9f9f9;
  border-left: 4px solid #3498db;
  font-style: italic;
  font-size: 1.2em;
}

/* Guillemet ouvrant */
.fancy-quote::before {
  content: """;
  position: absolute;
  top: -10px;
  left: 10px;
  font-size: 4em;
  color: #3498db;
  opacity: 0.3;
  font-family: Georgia, serif;
}

/* Guillemet fermant */
.fancy-quote::after {
  content: """;
  position: absolute;
  bottom: -40px;
  right: 10px;
  font-size: 4em;
  color: #3498db;
  opacity: 0.3;
  font-family: Georgia, serif;
}
```

### Exemple 4 : Breadcrumb (fil d'Ariane)

**HTML :**
```html
<nav class="breadcrumb">
  <a href="#">Accueil</a>
  <a href="#">Catégorie</a>
  <a href="#">Sous-catégorie</a>
  <span>Page actuelle</span>
</nav>
```

**CSS :**
```css
.breadcrumb {
  display: flex;
  align-items: center;
}

.breadcrumb a,
.breadcrumb span {
  padding: 5px 10px;
  color: #333;
  text-decoration: none;
}

/* Séparateur après chaque élément sauf le dernier */
.breadcrumb a::after {
  content: "›";
  margin: 0 10px;
  color: #999;
}

.breadcrumb span {
  font-weight: bold;
}
```

### Exemple 5 : Boutons avec icônes

**HTML :**
```html
<button class="btn-download">Télécharger</button>
<button class="btn-play">Lire</button>
<button class="btn-delete">Supprimer</button>
```

**CSS :**
```css
.btn-download,
.btn-play,
.btn-delete {
  padding: 10px 20px 10px 45px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  font-size: 16px;
}

/* Icône téléchargement */
.btn-download {
  background: #3498db;
  color: white;
}

.btn-download::before {
  content: "⬇";
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 20px;
}

/* Icône lecture */
.btn-play {
  background: #2ecc71;
  color: white;
}

.btn-play::before {
  content: "▶";
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 16px;
}

/* Icône suppression */
.btn-delete {
  background: #e74c3c;
  color: white;
}

.btn-delete::before {
  content: "✕";
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 20px;
}
```

---

## Limitations et contraintes

### 1. Propriété `content` obligatoire pour ::before et ::after

**❌ Ne fonctionnera PAS :**
```css
p::before {
  background: blue;
  /* Manque content ! */
}
```

**✅ Correct :**
```css
p::before {
  content: "";  /* Vide mais présent */
  background: blue;
  display: block;
  width: 50px;
  height: 50px;
}
```

### 2. Les pseudo-éléments ne sont pas dans le DOM

Les pseudo-éléments ne peuvent pas :
- Être ciblés par JavaScript directement
- Recevoir d'événements (pas de `addEventListener`)
- Être inspectés facilement (mais visibles dans DevTools)

**Workaround pour JavaScript :**
```javascript
// ❌ Ne fonctionne pas directement
document.querySelector('p::before');

// ✅ Modifier via les propriétés CSS
element.style.setProperty('--custom-content', '"Nouveau texte"');
```

```css
p::before {
  content: var(--custom-content, "Défaut");
}
```

### 3. Un seul ::before et un seul ::after par élément

Vous ne pouvez pas avoir plusieurs `::before` ou `::after` sur le même élément.

**❌ Impossible :**
```css
p::before {
  content: "1";
}

p::before {  /* Écrase le précédent */
  content: "2";
}
```

**✅ Solution : utiliser les deux :**
```css
p::before {
  content: "1";
}

p::after {
  content: "2";
}
```

### 4. Éléments remplacés

Les pseudo-éléments `::before` et `::after` ne fonctionnent **pas** sur les éléments remplacés :

**❌ Ne fonctionne PAS sur :**
- `<img>`
- `<input>`
- `<textarea>`
- `<video>`
- `<iframe>`

**Solution :** Envelopper dans un conteneur :
```html
<div class="input-wrapper">
  <input type="text">
</div>
```

```css
.input-wrapper::before {
  content: "✓";
}
```

### 5. Accessibilité

Les pseudo-éléments **ne sont pas lus par les lecteurs d'écran**.

**⚠️ Ne mettez pas de contenu important dans `content` :**
```css
/* ❌ Le lecteur d'écran ne lira pas "Important :" */
.warning::before {
  content: "Important : ";
}
```

**✅ Mieux : utiliser des attributs ARIA ou du texte visible :**
```html
<div class="warning" aria-label="Important">
  Message d'avertissement
</div>
```

---

## Bonnes pratiques

### ✅ À FAIRE

**1. Utiliser pour du contenu purement décoratif :**
```css
.card::before {
  content: "";
  display: block;
  width: 100%;
  height: 5px;
  background: linear-gradient(to right, blue, purple);
}
```

**2. Toujours inclure `content`, même vide :**
```css
.element::before {
  content: "";  /* Obligatoire */
  /* ... autres styles */
}
```

**3. Utiliser `attr()` pour du contenu dynamique :**
```css
.label::before {
  content: attr(data-label) ": ";
}
```

**4. Penser responsive :**
```css
.card::before {
  content: "Desktop";
}

@media (max-width: 768px) {
  .card::before {
    content: "Mobile";
  }
}
```

**5. Utiliser des variables CSS pour la réutilisation :**
```css
:root {
  --icon-size: 20px;
}

.icon::before {
  content: "";
  width: var(--icon-size);
  height: var(--icon-size);
}
```

### ❌ À ÉVITER

**1. Ne pas mettre de contenu essentiel :**
```css
/* ❌ Contenu important, devrait être dans le HTML */
.product::after {
  content: "Prix : 29.99€";
}
```

**2. Ne pas abuser des pseudo-éléments :**
```css
/* ❌ Trop de pseudo-éléments, HTML serait plus clair */
.element::before { /* ... */ }
.element::after { /* ... */ }
.element span::before { /* ... */ }
.element span::after { /* ... */ }
```

**3. Ne pas oublier les contraintes d'accessibilité :**
```css
/* ❌ Le lecteur d'écran ne dira pas "Erreur" */
.error::before {
  content: "Erreur: ";
}

/* ✅ Utiliser aria-label à la place */
```

**4. Ne pas utiliser pour remplacer des images importantes :**
```css
/* ❌ Une vraie image serait mieux */
.logo::before {
  content: url('logo.png');
}

/* ✅ Utiliser <img> avec alt */
```

---

## Tableau récapitulatif

| Pseudo-élément | Fonction | Propriété `content` | Exemples d'usage |
|----------------|----------|---------------------|------------------|
| `::before` | Ajoute du contenu avant | Obligatoire | Icônes, décorations, compteurs |
| `::after` | Ajoute du contenu après | Obligatoire | Flèches, badges, clearfix |
| `::first-letter` | Première lettre | Non utilisée | Lettrines, effets typographiques |
| `::first-line` | Première ligne | Non utilisée | Mise en avant, chapô |
| `::selection` | Texte sélectionné | Non utilisée | Personnalisation de sélection |

---

## Résumé

### Points clés à retenir

- 📌 **Double deux-points `::` pour les pseudo-éléments** (notation moderne)
- 📌 **`content` est obligatoire** pour `::before` et `::after`, même vide
- 📌 **Un seul `::before` et un seul `::after`** par élément
- 📌 **Pseudo-éléments = contenu décoratif**, pas de contenu essentiel
- 📌 **Ne fonctionnent pas sur les éléments remplacés** (`<img>`, `<input>`)
- 📌 **Non accessibles par les lecteurs d'écran** (problème d'accessibilité)
- 📌 **Très puissants pour les effets visuels** sans alourdir le HTML
- 📌 **Peuvent être animés** avec CSS transitions/animations

### Cas d'usage principaux

- **Décorations** : lignes, formes, coins
- **Icônes** : symboles avant/après du texte
- **Effets interactifs** : overlays, tooltips
- **Typographie** : lettrines, guillemets
- **Compteurs** : numérotation automatique
- **Séparateurs** : breadcrumbs, listes
- **Clearfix** : résolution des floats

---

## Prochaine étape

Vous maîtrisez maintenant les pseudo-éléments qui permettent d'ajouter du contenu décoratif et des effets visuels sans modifier le HTML ! Dans la section suivante (4.1.7), nous découvrirons la **spécificité et la cascade CSS**, concepts fondamentaux pour comprendre quelles règles CSS s'appliquent quand plusieurs règles ciblent le même élément.

Comprendre la spécificité est essentiel pour éviter les conflits CSS et écrire du code maintenable !

---

**Navigation :**

- ➡️ Section suivante : [4.1.7 Spécificité et cascade](./07-specificite-et-cascade.md)
- 🏠 Retour à la [Table des matières](../../SOMMAIRE.md)

⏭️ [Spécificité et cascade CSS](/04-css3-styles-et-mise-en-page/01-syntaxe-et-selecteurs/07-specificite-et-cascade.md)
