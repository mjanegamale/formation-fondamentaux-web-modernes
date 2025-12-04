🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.1.5 Pseudo-classes (:hover, :focus, :nth-child)

## Introduction

Les **pseudo-classes** sont des mots-clés spéciaux qui permettent de cibler des éléments selon leur **état** ou leur **position** dans le document, sans avoir besoin d'ajouter des classes supplémentaires dans le HTML.

Une pseudo-classe s'ajoute à un sélecteur avec le symbole **deux-points** `:` et permet de styliser :
- Des **états interactifs** (survol, focus, clic)
- Des **positions** dans la structure (premier, dernier, nième enfant)
- Des **états de formulaire** (validé, désactivé, coché)

Dans cette section, nous allons découvrir les pseudo-classes les plus utilisées et essentielles pour créer des interfaces web modernes et interactives.

---

## Syntaxe générale

```css
sélecteur:pseudo-classe {
  propriété: valeur;
}
```

**Exemple :**
```css
a:hover {
  color: red;
}
```

**⚠️ Important :** Pas d'espace entre le sélecteur et les deux-points !

**✅ Correct :**
```css
a:hover { }
.button:hover { }
```

**❌ Incorrect :**
```css
a :hover { }      /* L'espace change complètement le sens ! */
```

---

## Pseudo-classes d'état interactif

Ces pseudo-classes ciblent les éléments selon leur interaction avec l'utilisateur.

### 1. `:hover` - Au survol

Cible un élément lorsque le **curseur de la souris** le survole.

**Syntaxe :**
```css
sélecteur:hover {
  propriété: valeur;
}
```

**Exemple simple :**
```css
a:hover {
  color: red;
  text-decoration: underline;
}
```

**HTML :**
```html
<a href="#">Survolez-moi</a>
```

**Résultat :** Quand vous passez la souris sur le lien, il devient rouge et souligné.

#### Exemples pratiques

**1. Bouton avec effet au survol :**
```css
.button {
  background: blue;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  transition: background 0.3s;
}

.button:hover {
  background: darkblue;
}
```

**2. Image avec zoom au survol :**
```css
.image-container img {
  width: 300px;
  transition: transform 0.3s;
}

.image-container img:hover {
  transform: scale(1.1);
}
```

**3. Card avec élévation au survol :**
```css
.card {
  padding: 20px;
  border: 1px solid #ddd;
  transition: box-shadow 0.3s;
}

.card:hover {
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}
```

**4. Navigation avec changement de fond :**
```css
nav a {
  display: inline-block;
  padding: 15px 20px;
  color: white;
  text-decoration: none;
  transition: background 0.3s;
}

nav a:hover {
  background: rgba(255,255,255,0.1);
}
```

#### Combiner avec d'autres sélecteurs

```css
/* Hover sur un élément dans un conteneur */
.gallery img:hover {
  opacity: 0.8;
}

/* Hover sur un élément avec une classe */
.menu-item:hover {
  background: lightgray;
}

/* Hover avec enfant */
.card:hover .card-title {
  color: blue;
}
```

**Exemple du dernier cas :**
```html
<div class="card">
  <h3 class="card-title">Titre</h3>
  <p>Contenu</p>
</div>
```

Quand on survole la card, le titre devient bleu.

#### ⚠️ Note sur les appareils tactiles

`:hover` ne fonctionne pas bien sur mobile/tablette (pas de souris). Utilisez-le comme **amélioration progressive**, pas comme fonctionnalité essentielle.

---

### 2. `:active` - Au clic

Cible un élément pendant qu'il est **activé** (bouton de souris enfoncé).

**Exemple :**
```css
.button:active {
  transform: scale(0.95);
  background: navy;
}
```

**Utilisation typique - effet de "pression" :**
```css
button {
  background: blue;
  border: none;
  padding: 10px 20px;
  color: white;
  cursor: pointer;
}

button:hover {
  background: darkblue;
}

button:active {
  background: navy;
  transform: translateY(2px);
}
```

**Résultat :** Le bouton change de couleur au survol, et "s'enfonce" quand on clique.

---

### 3. `:focus` - Au focus

Cible un élément qui a le **focus** (généralement via clavier ou clic dans un champ).

**Particulièrement important pour :**
- Les champs de formulaire (`<input>`, `<textarea>`, `<select>`)
- Les liens et boutons (navigation au clavier)
- L'accessibilité

**Exemple - Champs de formulaire :**
```css
input:focus {
  outline: none;
  border: 2px solid blue;
  box-shadow: 0 0 5px rgba(0,0,255,0.3);
}
```

**HTML :**
```html
<input type="text" placeholder="Cliquez ici">
```

**Résultat :** Quand l'input a le focus, il a une bordure bleue et une ombre.

#### Exemples pratiques

**1. Formulaire avec feedback visuel :**
```css
.form-input {
  padding: 10px;
  border: 1px solid #ddd;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.form-input:focus {
  border-color: #3498db;
  box-shadow: 0 0 8px rgba(52, 152, 219, 0.3);
  outline: none;
}
```

**2. Navigation accessible au clavier :**
```css
a {
  color: blue;
  text-decoration: none;
}

a:focus {
  outline: 2px solid orange;
  outline-offset: 2px;
}
```

**3. Bouton avec état focus :**
```css
button:focus {
  outline: 2px solid blue;
  outline-offset: 3px;
}

button:focus:not(:focus-visible) {
  outline: none;  /* Retire l'outline au clic, garde pour clavier */
}
```

#### ⚠️ Attention : Ne jamais supprimer le focus sans alternative

**❌ Mauvaise pratique :**
```css
*:focus {
  outline: none;  /* Rend la navigation au clavier impossible ! */
}
```

**✅ Bonne pratique :**
```css
input:focus {
  outline: none;  /* On retire l'outline par défaut */
  border: 2px solid blue;  /* Mais on fournit une alternative visible */
}
```

---

### 4. `:visited` - Lien visité

Cible les liens (`<a>`) qui ont déjà été **visités** par l'utilisateur.

**Exemple :**
```css
a {
  color: blue;
}

a:visited {
  color: purple;
}
```

**⚠️ Limitations de sécurité :**
Pour des raisons de confidentialité, vous ne pouvez changer que certaines propriétés sur `:visited` :
- ✅ `color`, `background-color`, `border-color`
- ❌ Pas de `font-size`, `padding`, `margin`, etc.

---

### 5. `:link` - Lien non visité

Cible les liens (`<a>` avec `href`) qui n'ont **pas encore été visités**.

**Exemple :**
```css
a:link {
  color: blue;
}

a:visited {
  color: purple;
}
```

---

### Ordre LVHA pour les liens

Pour les liens, il est important de définir les pseudo-classes dans cet ordre (mnémotechnique : **L**o**V**e **HA**te) :

```css
/* 1. Link (non visité) */
a:link {
  color: blue;
}

/* 2. Visited (visité) */
a:visited {
  color: purple;
}

/* 3. Hover (survol) */
a:hover {
  color: red;
}

/* 4. Active (clic) */
a:active {
  color: darkred;
}
```

**Pourquoi cet ordre ?** À cause de la spécificité CSS. Si vous mettez `:hover` avant `:link`, le hover ne fonctionnera pas sur les liens non visités.

---

## Pseudo-classes de formulaire

Ces pseudo-classes ciblent les éléments de formulaire selon leur état.

### 1. `:disabled` - Élément désactivé

Cible les éléments de formulaire avec l'attribut `disabled`.

**Exemple :**
```css
input:disabled {
  background: #f0f0f0;
  cursor: not-allowed;
  opacity: 0.6;
}
```

**HTML :**
```html
<input type="text" value="Non modifiable" disabled>
```

### 2. `:enabled` - Élément activé

Cible les éléments de formulaire qui sont **actifs** (par défaut).

```css
input:enabled {
  background: white;
}
```

### 3. `:checked` - Case cochée

Cible les checkboxes et radio buttons qui sont **cochés**.

**Exemple pratique - Checkbox personnalisée :**
```css
/* Cacher la checkbox native */
input[type="checkbox"] {
  display: none;
}

/* Label stylisé */
input[type="checkbox"] + label {
  position: relative;
  padding-left: 30px;
  cursor: pointer;
}

/* Créer une fausse checkbox */
input[type="checkbox"] + label::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 20px;
  height: 20px;
  border: 2px solid #ddd;
  background: white;
}

/* Quand cochée, changer l'apparence */
input[type="checkbox"]:checked + label::before {
  background: blue;
  border-color: blue;
}

/* Ajouter un checkmark */
input[type="checkbox"]:checked + label::after {
  content: "✓";
  position: absolute;
  left: 5px;
  top: -2px;
  color: white;
  font-weight: bold;
}
```

**HTML :**
```html
<input type="checkbox" id="terms">
<label for="terms">J'accepte les conditions</label>
```

### 4. `:required` - Champ requis

Cible les champs avec l'attribut `required`.

```css
input:required {
  border-left: 3px solid red;
}
```

### 5. `:optional` - Champ optionnel

Cible les champs **sans** l'attribut `required`.

```css
input:optional {
  border-left: 3px solid gray;
}
```

### 6. `:valid` et `:invalid` - Validation

Ciblent les champs selon leur état de validation HTML5.

**Exemple :**
```css
/* Champ valide */
input:valid {
  border-color: green;
}

/* Champ invalide */
input:invalid {
  border-color: red;
}

/* Pour éviter l'effet au chargement, combiner avec :not(:placeholder-shown) */
input:invalid:not(:placeholder-shown) {
  border-color: red;
}
```

**HTML :**
```html
<input type="email" placeholder="votre@email.com" required>
```

---

## Pseudo-classes structurelles

Ces pseudo-classes ciblent les éléments selon leur **position** dans la structure HTML.

### 1. `:first-child` - Premier enfant

Cible un élément qui est le **premier enfant** de son parent.

**Exemple :**
```css
p:first-child {
  font-weight: bold;
}
```

**HTML :**
```html
<div>
  <p>Je serai en gras (premier enfant)</p>
  <p>Je ne serai pas en gras</p>
</div>
```

**⚠️ Important :** L'élément doit être le premier enfant **de n'importe quel type**.

**Exemple qui ne fonctionne PAS :**
```html
<div>
  <h2>Titre</h2>       <!-- h2 est le premier enfant -->
  <p>Paragraphe</p>    <!-- p n'est PAS le premier enfant -->
</div>
```

```css
p:first-child {
  /* Ne s'appliquera PAS au paragraphe ci-dessus */
}
```

### 2. `:last-child` - Dernier enfant

Cible un élément qui est le **dernier enfant** de son parent.

**Exemple :**
```css
li:last-child {
  border-bottom: none;
}
```

**HTML :**
```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>  <!-- Pas de bordure en bas -->
</ul>
```

### 3. `:nth-child(n)` - Nième enfant

Cible un élément selon sa **position numérique** parmi les enfants de son parent.

**Syntaxe de base :**
```css
élément:nth-child(nombre) { }
```

#### Exemples avec nombres

**1. Cibler le 3ème élément :**
```css
li:nth-child(3) {
  color: red;
}
```

**HTML :**
```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>  <!-- Rouge -->
  <li>4</li>
</ul>
```

**2. Cibler plusieurs éléments spécifiques :**
```css
tr:nth-child(2),
tr:nth-child(4),
tr:nth-child(6) {
  background: #f0f0f0;
}
```

#### Utiliser des mots-clés

**1. `:nth-child(odd)` - Éléments impairs (1, 3, 5, ...) :**
```css
tr:nth-child(odd) {
  background: #f9f9f9;
}
```

**2. `:nth-child(even)` - Éléments pairs (2, 4, 6, ...) :**
```css
tr:nth-child(even) {
  background: white;
}
```

**Exemple - Tableau avec lignes alternées :**
```css
table tr:nth-child(odd) {
  background: #f0f0f0;
}

table tr:nth-child(even) {
  background: white;
}
```

#### Utiliser des formules : `nth-child(an+b)`

La notation `an+b` permet de créer des patterns complexes :
- `a` : le coefficient (intervalle)
- `n` : compteur (commence à 0)
- `b` : décalage (offset)

**Exemples de formules :**

**1. `2n` - Tous les éléments pairs :**
```css
li:nth-child(2n) {
  /* n=0: 2×0=0 (aucun)
     n=1: 2×1=2 (2ème)
     n=2: 2×2=4 (4ème)
     n=3: 2×3=6 (6ème) */
}
```

**2. `2n+1` - Tous les éléments impairs :**
```css
li:nth-child(2n+1) {
  /* n=0: 2×0+1=1 (1er)
     n=1: 2×1+1=3 (3ème)
     n=2: 2×2+1=5 (5ème) */
}
```

**3. `3n` - Chaque 3ème élément (3, 6, 9, ...) :**
```css
div:nth-child(3n) {
  background: yellow;
}
```

**4. `3n+1` - 1er, 4ème, 7ème, 10ème, ... :**
```css
li:nth-child(3n+1) {
  font-weight: bold;
}
```

**5. `n+3` - À partir du 3ème :**
```css
p:nth-child(n+3) {
  /* 3ème, 4ème, 5ème, ... tous les suivants */
  margin-top: 20px;
}
```

**6. `-n+3` - Les 3 premiers uniquement :**
```css
li:nth-child(-n+3) {
  /* 1er, 2ème, 3ème seulement */
  color: red;
}
```

#### Exemples pratiques

**1. Galerie avec 3 colonnes :**
```css
.gallery-item:nth-child(3n+1) {
  clear: left;  /* Force un retour à la ligne tous les 3 éléments */
}
```

**2. Cibler les 5 premiers éléments :**
```css
.list-item:nth-child(-n+5) {
  font-size: 18px;
}
```

**3. Tous les éléments sauf les 3 premiers :**
```css
article:nth-child(n+4) {
  opacity: 0.7;
}
```

### 4. `:nth-last-child(n)` - Nième enfant depuis la fin

Fonctionne comme `:nth-child()` mais compte **depuis la fin**.

**Exemple :**
```css
/* Les 2 derniers éléments */
li:nth-last-child(-n+2) {
  color: red;
}
```

### 5. `:first-of-type` - Premier du type

Cible le **premier élément d'un type** parmi ses frères.

**Différence avec `:first-child` :**

```html
<article>
  <h2>Titre</h2>       <!-- :first-child mais pas p:first-child -->
  <p>Paragraphe 1</p>  <!-- p:first-of-type ✅ -->
  <p>Paragraphe 2</p>
</article>
```

```css
/* Ne cible rien (h2 est le premier enfant) */
p:first-child {
  color: red;
}

/* Cible "Paragraphe 1" */
p:first-of-type {
  color: red;
}
```

### 6. `:last-of-type` - Dernier du type

Cible le **dernier élément d'un type** parmi ses frères.

```css
p:last-of-type {
  margin-bottom: 0;
}
```

### 7. `:nth-of-type(n)` - Nième du type

Comme `:nth-child()` mais ne compte que les éléments **du même type**.

**Exemple :**
```css
/* Tous les paragraphes impairs */
p:nth-of-type(odd) {
  background: #f0f0f0;
}
```

**HTML :**
```html
<article>
  <h2>Titre</h2>
  <p>P1 (1er p - impair) - fond gris</p>
  <p>P2 (2ème p - pair) - fond normal</p>
  <div>Division</div>
  <p>P3 (3ème p - impair) - fond gris</p>
</article>
```

### 8. `:only-child` - Enfant unique

Cible un élément qui est le **seul enfant** de son parent.

```css
p:only-child {
  text-align: center;
}
```

**HTML :**
```html
<div>
  <p>Je suis seul - je serai centré</p>
</div>

<div>
  <p>Je ne suis pas seul</p>
  <p>Car nous sommes deux</p>
</div>
```

### 9. `:only-of-type` - Seul de son type

Cible un élément qui est le **seul de son type** parmi ses frères.

```css
p:only-of-type {
  font-weight: bold;
}
```

**HTML :**
```html
<article>
  <h2>Titre</h2>
  <p>Je suis le seul paragraphe - je serai en gras</p>
  <div>Division</div>
</article>
```

### 10. `:empty` - Élément vide

Cible les éléments qui n'ont **aucun enfant** (pas même du texte).

```css
.message:empty {
  display: none;
}
```

**HTML :**
```html
<div class="message"></div>  <!-- Caché -->
<div class="message">Texte</div>  <!-- Visible -->
```

---

## Pseudo-classes de négation

### `:not()` - Négation

Cible les éléments qui **ne correspondent pas** au sélecteur spécifié.

**Syntaxe :**
```css
élément:not(sélecteur) {
  propriété: valeur;
}
```

**Exemples :**

**1. Tous les paragraphes sauf ceux avec une classe :**
```css
p:not(.intro) {
  color: gray;
}
```

**HTML :**
```html
<p class="intro">Pas gris</p>
<p>Gris</p>
<p>Gris aussi</p>
```

**2. Tous les inputs sauf les checkboxes :**
```css
input:not([type="checkbox"]) {
  border: 1px solid #ddd;
}
```

**3. Liens sans classe :**
```css
a:not([class]) {
  color: blue;
}
```

**4. Tous les éléments sauf le dernier :**
```css
li:not(:last-child) {
  border-bottom: 1px solid #ddd;
}
```

**5. Combiner plusieurs conditions (CSS moderne) :**
```css
/* Tous les inputs sauf checkbox et radio */
input:not([type="checkbox"], [type="radio"]) {
  display: block;
  margin-bottom: 10px;
}
```

---

## Pseudo-classes de ciblage

### `:target` - Élément ciblé par l'URL

Cible un élément dont l'ID correspond à l'**ancre de l'URL**.

**Exemple :**
```css
section:target {
  background: yellow;
  border: 2px solid orange;
}
```

**HTML :**
```html
<nav>
  <a href="#section1">Section 1</a>
  <a href="#section2">Section 2</a>
</nav>

<section id="section1">
  <h2>Section 1</h2>
  <p>Contenu...</p>
</section>

<section id="section2">
  <h2>Section 2</h2>
  <p>Contenu...</p>
</section>
```

Quand l'URL est `page.html#section1`, la section 1 aura un fond jaune.

**Cas d'usage - Onglets sans JavaScript :**
```css
.tab-content {
  display: none;
}

.tab-content:target {
  display: block;
}
```

---

## Combinaisons de pseudo-classes

Vous pouvez **combiner plusieurs pseudo-classes** sur le même élément.

**Exemples :**

**1. Lien visité au survol :**
```css
a:visited:hover {
  color: darkpurple;
}
```

**2. Input requis au focus :**
```css
input:required:focus {
  border-color: red;
}
```

**3. Bouton désactivé au survol (pas d'effet) :**
```css
button:disabled:hover {
  cursor: not-allowed;
}
```

**4. Checkbox cochée et désactivée :**
```css
input:checked:disabled {
  opacity: 0.5;
}
```

**5. Premier enfant au survol :**
```css
li:first-child:hover {
  background: lightblue;
}
```

---

## Exemples pratiques complets

### Exemple 1 : Navigation interactive

**HTML :**
```html
<nav class="main-nav">
  <a href="#" class="active">Accueil</a>
  <a href="#">Services</a>
  <a href="#">Portfolio</a>
  <a href="#">Contact</a>
</nav>
```

**CSS :**
```css
.main-nav {
  background: #333;
  padding: 0;
}

.main-nav a {
  display: inline-block;
  color: white;
  text-decoration: none;
  padding: 15px 20px;
  transition: background 0.3s;
}

/* Survol */
.main-nav a:hover {
  background: #555;
}

/* Actif (clic) */
.main-nav a:active {
  background: #222;
}

/* Lien actif (page courante) */
.main-nav a.active {
  background: #0066cc;
}

/* Focus (clavier) */
.main-nav a:focus {
  outline: 2px solid orange;
  outline-offset: -2px;
}
```

### Exemple 2 : Liste de prix avec distinction visuelle

**HTML :**
```html
<div class="pricing-container">
  <div class="pricing-card">
    <h3>Basic</h3>
    <p class="price">9€/mois</p>
    <button>Choisir</button>
  </div>
  <div class="pricing-card featured">
    <h3>Pro</h3>
    <p class="price">29€/mois</p>
    <button>Choisir</button>
  </div>
  <div class="pricing-card">
    <h3>Enterprise</h3>
    <p class="price">99€/mois</p>
    <button>Choisir</button>
  </div>
</div>
```

**CSS :**
```css
.pricing-card {
  border: 2px solid #ddd;
  padding: 30px;
  text-align: center;
  transition: transform 0.3s, box-shadow 0.3s;
}

/* Première carte (Basic) */
.pricing-card:first-child {
  border-color: #3498db;
}

/* Dernière carte (Enterprise) */
.pricing-card:last-child {
  border-color: #e74c3c;
}

/* Card du milieu (carte "featured") */
.pricing-card:nth-child(2) {
  transform: scale(1.05);
  border-color: #2ecc71;
  box-shadow: 0 5px 20px rgba(0,0,0,0.2);
}

/* Hover sur toutes les cards */
.pricing-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(0,0,0,0.15);
}

/* Hover sur la card featured (plus d'effet) */
.pricing-card:nth-child(2):hover {
  transform: translateY(-8px) scale(1.08);
  box-shadow: 0 15px 30px rgba(0,0,0,0.3);
}
```

### Exemple 3 : Formulaire avec validation visuelle

**HTML :**
```html
<form class="contact-form">
  <div class="form-group">
    <label for="name">Nom *</label>
    <input type="text" id="name" required>
  </div>

  <div class="form-group">
    <label for="email">Email *</label>
    <input type="email" id="email" required>
  </div>

  <div class="form-group">
    <label for="message">Message</label>
    <textarea id="message"></textarea>
  </div>

  <button type="submit">Envoyer</button>
</form>
```

**CSS :**
```css
/* Tous les champs */
.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 4px;
  transition: border-color 0.3s, box-shadow 0.3s;
}

/* Focus sur un champ */
.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 8px rgba(52, 152, 219, 0.3);
}

/* Champs requis avec bordure spéciale */
.contact-form input:required {
  border-left-width: 4px;
  border-left-color: #e74c3c;
}

/* Champ valide (rempli correctement) */
.contact-form input:valid:not(:placeholder-shown) {
  border-color: #2ecc71;
  border-left-color: #2ecc71;
}

/* Champ invalide (erreur) */
.contact-form input:invalid:not(:placeholder-shown) {
  border-color: #e74c3c;
  background: #ffe6e6;
}

/* Bouton */
.contact-form button {
  background: #3498db;
  color: white;
  padding: 12px 30px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background 0.3s, transform 0.1s;
}

.contact-form button:hover {
  background: #2980b9;
}

.contact-form button:active {
  transform: scale(0.98);
}

.contact-form button:disabled {
  background: #bdc3c7;
  cursor: not-allowed;
}
```

### Exemple 4 : Tableau avec lignes alternées et hover

**HTML :**
```html
<table class="data-table">
  <thead>
    <tr>
      <th>Nom</th>
      <th>Email</th>
      <th>Statut</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Jean Dupont</td>
      <td>jean@email.com</td>
      <td>Actif</td>
    </tr>
    <tr>
      <td>Marie Martin</td>
      <td>marie@email.com</td>
      <td>Actif</td>
    </tr>
    <tr>
      <td>Pierre Durand</td>
      <td>pierre@email.com</td>
      <td>Inactif</td>
    </tr>
  </tbody>
</table>
```

**CSS :**
```css
.data-table {
  width: 100%;
  border-collapse: collapse;
}

.data-table th,
.data-table td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

/* En-tête */
.data-table thead tr {
  background: #34495e;
  color: white;
}

/* Lignes impaires */
.data-table tbody tr:nth-child(odd) {
  background: #f9f9f9;
}

/* Lignes paires */
.data-table tbody tr:nth-child(even) {
  background: white;
}

/* Hover sur les lignes */
.data-table tbody tr:hover {
  background: #e8f4f8;
  cursor: pointer;
}

/* Première colonne en gras */
.data-table td:first-child {
  font-weight: bold;
}

/* Dernière ligne avec bordure spéciale */
.data-table tbody tr:last-child td {
  border-bottom: 2px solid #34495e;
}
```

---

## Tableau récapitulatif

### Pseudo-classes d'état

| Pseudo-classe | Cible | Exemple |
|---------------|-------|---------|
| `:hover` | Survol souris | `a:hover` |
| `:active` | Clic actif | `button:active` |
| `:focus` | Focus | `input:focus` |
| `:visited` | Lien visité | `a:visited` |
| `:link` | Lien non visité | `a:link` |

### Pseudo-classes de formulaire

| Pseudo-classe | Cible | Exemple |
|---------------|-------|---------|
| `:disabled` | Élément désactivé | `input:disabled` |
| `:enabled` | Élément activé | `input:enabled` |
| `:checked` | Case cochée | `input:checked` |
| `:required` | Champ requis | `input:required` |
| `:optional` | Champ optionnel | `input:optional` |
| `:valid` | Validation réussie | `input:valid` |
| `:invalid` | Validation échouée | `input:invalid` |

### Pseudo-classes structurelles

| Pseudo-classe | Cible | Exemple |
|---------------|-------|---------|
| `:first-child` | Premier enfant | `p:first-child` |
| `:last-child` | Dernier enfant | `li:last-child` |
| `:nth-child(n)` | Nième enfant | `tr:nth-child(2)` |
| `:nth-child(odd)` | Enfants impairs | `tr:nth-child(odd)` |
| `:nth-child(even)` | Enfants pairs | `tr:nth-child(even)` |
| `:first-of-type` | Premier du type | `p:first-of-type` |
| `:last-of-type` | Dernier du type | `p:last-of-type` |
| `:nth-of-type(n)` | Nième du type | `p:nth-of-type(2)` |
| `:only-child` | Enfant unique | `p:only-child` |
| `:only-of-type` | Seul de son type | `p:only-of-type` |
| `:empty` | Élément vide | `div:empty` |

### Autres pseudo-classes

| Pseudo-classe | Cible | Exemple |
|---------------|-------|---------|
| `:not()` | Négation | `p:not(.intro)` |
| `:target` | Ancre ciblée | `section:target` |

---

## Bonnes pratiques

### ✅ À FAIRE

**1. Utiliser les transitions pour des effets fluides :**
```css
a {
  color: blue;
  transition: color 0.3s;
}

a:hover {
  color: red;
}
```

**2. Toujours fournir un feedback visuel au focus :**
```css
button:focus {
  outline: 2px solid blue;
  outline-offset: 2px;
}
```

**3. Respecter l'ordre LVHA pour les liens :**
```css
a:link { }
a:visited { }
a:hover { }
a:active { }
```

**4. Utiliser `:not()` pour simplifier le code :**
```css
/* ✅ Au lieu de répéter les styles */
li:not(:last-child) {
  border-bottom: 1px solid #ddd;
}
```

**5. Combiner pseudo-classes pour plus de précision :**
```css
input:required:invalid:not(:placeholder-shown) {
  border-color: red;
}
```

### ❌ À ÉVITER

**1. Ne pas supprimer le focus sans alternative :**
```css
/* ❌ Mauvais pour l'accessibilité */
*:focus {
  outline: none;
}
```

**2. Éviter les effets :hover sur mobile :**
```css
/* ⚠️ Peut poser problème sur tactile */
.card:hover {
  display: none;  /* Ne pas cacher au hover ! */
}
```

**3. Ne pas abuser de :nth-child() complexe :**
```css
/* ❌ Difficile à comprendre et maintenir */
div:nth-child(3n+2):not(:nth-child(5)):nth-of-type(odd) {
  /* Trop complexe ! */
}

/* ✅ Utiliser une classe à la place */
.special-item {
  /* Plus clair */
}
```

---

## Résumé

### Points clés à retenir

- 📌 **Les pseudo-classes ciblent des états ou positions** sans modifier le HTML
- 📌 **`:hover`, `:focus`, `:active`** : interactions utilisateur essentielles
- 📌 **`:nth-child()`** : puissant pour les patterns (odd, even, formules)
- 📌 **`:first-child` vs `:first-of-type`** : comprendre la différence
- 📌 **`:not()`** : inverse la sélection
- 📌 **Combiner plusieurs pseudo-classes** : `input:required:focus`
- 📌 **Toujours penser à l'accessibilité** : focus, clavier, lecteurs d'écran
- 📌 **Utiliser les transitions** pour des effets fluides

### Pseudo-classes les plus utilisées

Les plus courantes que vous utiliserez régulièrement :
- `:hover` - Survol
- `:focus` - Focus
- `:active` - Clic
- `:first-child` / `:last-child` - Premier/Dernier
- `:nth-child(odd)` / `:nth-child(even)` - Alternance
- `:disabled` - Éléments désactivés
- `:checked` - Cases cochées
- `:not()` - Négation

---

## Prochaine étape

Vous maîtrisez maintenant les pseudo-classes qui permettent de cibler des éléments selon leur état ou position ! Dans la section suivante (4.1.6), nous découvrirons les **pseudo-éléments** (`::before`, `::after`) qui permettent de créer et styliser du contenu généré par CSS.

Ces pseudo-éléments sont extrêmement puissants pour ajouter des éléments décoratifs sans alourdir le HTML !

---

**Navigation :**

- ➡️ Section suivante : [4.1.6 Pseudo-éléments](./06-pseudo-elements.md)
- 🏠 Retour à la [Table des matières](../../SOMMAIRE.md)

⏭️ [Pseudo-éléments (::before, ::after)](/04-css3-styles-et-mise-en-page/01-syntaxe-et-selecteurs/06-pseudo-elements.md)
