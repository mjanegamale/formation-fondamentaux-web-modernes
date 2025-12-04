🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.4.2 - De la maquette au code

## Introduction

Passer d'une **maquette** (design visuel) à du **code** (HTML/CSS/JavaScript) est une compétence fondamentale en développement web. C'est le moment où vous transformez une image statique en un site web fonctionnel et interactif.

### Le défi du développeur

Vous avez devant vous un beau design Figma, Photoshop ou même un croquis sur papier. Maintenant, il faut le transformer en code. Par où commencer ?

> 💡 **Analogie** : C'est comme construire un meuble IKEA. Vous avez l'image du meuble fini (la maquette), et vous devez assembler les pièces (HTML) dans le bon ordre, les peindre (CSS) et ajouter les mécanismes (JavaScript). Un bon développeur sait "voir" la structure sous le design.

### Compétences développées

En maîtrisant cette transition maquette → code, vous apprenez à :

- ✅ **Analyser visuellement** un design et identifier ses composants
- ✅ **Structurer sémantiquement** avec HTML
- ✅ **Styliser précisément** avec CSS
- ✅ **Penser responsive** dès le départ
- ✅ **Optimiser** votre processus de développement

---

## Étape 1 : Analyser la maquette

### 1.1 Vue d'ensemble

**Première chose à faire** : Prendre du recul et observer la maquette dans son ensemble.

**Questions à se poser** :

📋 **Structure générale** :
- Combien de sections principales ? (header, hero, features, footer, etc.)
- Y a-t-il une grille visible ?
- Quelle est la largeur maximale du contenu ?

📋 **Hiérarchie visuelle** :
- Quel est l'élément le plus important ?
- Quelle est l'ordre de lecture naturel ?
- Quels éléments attirent l'œil en premier ?

📋 **Répétitions** :
- Y a-t-il des patterns qui se répètent ? (cartes, boutons, etc.)
- Quels composants peuvent être réutilisés ?

### 1.2 Décomposition en zones

**Exercice mental** : Dessinez des rectangles imaginaires autour des différentes zones.

**Exemple de maquette décomposée** :

```
┌─────────────────────────────────────────┐
│ HEADER                                  │ ← Zone 1
│ [Logo]              [Nav Menu]          │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ HERO SECTION                            │ ← Zone 2
│                                         │
│    Titre Principal                      │
│    Sous-titre                           │
│    [CTA Button]                         │
│                                         │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ FEATURES                                │ ← Zone 3
│                                         │
│  ┌────────┐  ┌────────┐  ┌────────┐     │
│  │Feature1│  │Feature2│  │Feature3│     │
│  └────────┘  └────────┘  └────────┘     │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ FOOTER                                  │ ← Zone 4
│ Infos - Liens - Contact                 │
└─────────────────────────────────────────┘
```

**Chaque zone** deviendra une section en HTML.

### 1.3 Identifier les composants réutilisables

**Composants courants** :

| Composant | Utilisation | Exemples |
|-----------|-------------|----------|
| **Bouton** | CTA, actions | Bouton "En savoir plus", "Acheter" |
| **Carte** | Afficher des éléments similaires | Cartes de produits, articles de blog |
| **Icône + texte** | Features, avantages | Icône check + description |
| **Image + overlay** | Hero, bannières | Image avec texte par-dessus |
| **Formulaire** | Contact, inscription | Input + label + bouton submit |

**Principe DRY** (Don't Repeat Yourself) : Un composant = une classe CSS réutilisable.

---

## Étape 2 : Préparer les ressources

### 2.1 Extraire les informations du design

**Ce dont vous avez besoin** :

#### Couleurs
```css
/* Notez toutes les couleurs utilisées */
Primary: #3498db
Secondary: #2ecc71
Accent: #e74c3c
Text dark: #2c3e50
Text light: #7f8c8d
Background: #ecf0f1
```

**Astuce** : Utilisez un color picker (extensions Chrome) pour extraire les couleurs directement de la maquette.

#### Typographies
```css
/* Police principale */
font-family: 'Roboto', sans-serif;

/* Tailles */
h1: 48px / 3rem
h2: 36px / 2.25rem
h3: 24px / 1.5rem
p: 16px / 1rem
small: 14px / 0.875rem

/* Poids */
Titres: 700 (bold)
Sous-titres: 500 (medium)
Texte: 400 (regular)
```

#### Espacements
```css
/* Marges et paddings récurrents */
Small: 8px
Medium: 16px
Large: 32px
XLarge: 64px

/* Largeur maximale du contenu */
max-width: 1200px
```

#### Bordures et ombres
```css
/* Arrondis */
border-radius: 8px (boutons, cartes)

/* Ombres */
box-shadow: 0 2px 8px rgba(0,0,0,0.1)
```

### 2.2 Télécharger les assets

**Images** :
- Exportez toutes les images nécessaires
- Format WebP pour les photos (avec fallback JPG)
- SVG pour les icônes et logos
- PNG pour les images nécessitant la transparence

**Icônes** :
- Utilisez une bibliothèque d'icônes (Font Awesome, Feather Icons, etc.)
- Ou exportez les icônes en SVG depuis la maquette

**Polices** :
- Google Fonts pour les polices web
- Ou fichiers de police locaux si fournis

---

## Étape 3 : Structure HTML sémantique

### 3.1 Penser sémantique d'abord

**Avant de coder**, réfléchissez à la sémantique HTML appropriée.

**Exemple de réflexion** :

```
Maquette: "Titre principal de la page avec logo entreprise"
↓
Question: Est-ce le titre principal du site ou de la page ?
↓
Réponse: Si c'est le titre principal → <h1>
         Si c'est le nom de l'entreprise → <header> avec logo
```

### 3.2 Squelette HTML

**Commencez par le squelette** sans les détails.

**Exemple progressif** :

#### Niveau 1 : Structure de base
```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Site</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header></header>
  <main></main>
  <footer></footer>
</body>
</html>
```

#### Niveau 2 : Sections principales
```html
<body>
  <header>
    <!-- Navigation -->
  </header>

  <main>
    <section class="hero">
      <!-- Section héro -->
    </section>

    <section class="features">
      <!-- Section fonctionnalités -->
    </section>

    <section class="about">
      <!-- Section à propos -->
    </section>
  </main>

  <footer>
    <!-- Pied de page -->
  </footer>
</body>
```

#### Niveau 3 : Contenu détaillé
```html
<header class="site-header">
  <div class="container">
    <div class="logo">
      <img src="logo.svg" alt="Logo MonSite">
    </div>
    <nav class="main-nav">
      <ul>
        <li><a href="#accueil">Accueil</a></li>
        <li><a href="#services">Services</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </div>
</header>
```

### 3.3 Correspondance maquette → balises HTML

**Guide de correspondance** :

| Élément maquette | Balise HTML | Commentaire |
|------------------|-------------|-------------|
| En-tête de site | `<header>` | Contient logo et navigation |
| Menu de navigation | `<nav>` | Liste `<ul><li>` pour les liens |
| Titre principal | `<h1>` | Un seul par page |
| Sous-titres | `<h2>`, `<h3>` | Hiérarchie logique |
| Paragraphe | `<p>` | Blocs de texte |
| Bouton d'action | `<button>` ou `<a>` | Selon l'action |
| Carte de contenu | `<article>` ou `<div>` | `<article>` si autonome |
| Image décorative | `<img>` | Avec alt="" si décorative |
| Image de contenu | `<img>` | Avec alt descriptif |
| Liste à puces | `<ul><li>` | Liste non ordonnée |
| Section de contenu | `<section>` | Avec heading associé |
| Pied de page | `<footer>` | Infos de bas de page |

**Exemple d'analyse** :

```
Maquette montre:
┌──────────────────┐
│ [Icône Check]    │
│ Livraison rapide │
│ En 24h partout   │
└──────────────────┘

↓ Devient en HTML ↓

<div class="feature-card">
  <img src="icon-check.svg" alt="" class="feature-icon">
  <h3 class="feature-title">Livraison rapide</h3>
  <p class="feature-description">En 24h partout</p>
</div>
```

---

## Étape 4 : CSS progressif

### 4.1 Stratégie de développement CSS

**Ordre recommandé** :

1. ✅ **Reset/Normalize** CSS
2. ✅ **Variables CSS** (couleurs, espacements)
3. ✅ **Styles globaux** (body, liens, titres)
4. ✅ **Layout** (positionnement des grandes sections)
5. ✅ **Composants** (boutons, cartes, etc.)
6. ✅ **Responsive** (media queries)
7. ✅ **Animations** (si présentes dans la maquette)

### 4.2 Mettre en place les bases

#### Reset CSS simple
```css
/* reset.css ou début de style.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Roboto', sans-serif;
  line-height: 1.6;
  color: #2c3e50;
}

img {
  max-width: 100%;
  height: auto;
  display: block;
}

a {
  text-decoration: none;
  color: inherit;
}

ul {
  list-style: none;
}
```

#### Variables CSS
```css
:root {
  /* Couleurs */
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --text-dark: #2c3e50;
  --text-light: #7f8c8d;
  --bg-light: #ecf0f1;

  /* Espacements */
  --spacing-xs: 8px;
  --spacing-sm: 16px;
  --spacing-md: 32px;
  --spacing-lg: 64px;

  /* Typographie */
  --font-size-base: 16px;
  --font-size-lg: 24px;
  --font-size-xl: 36px;

  /* Conteneur */
  --container-max-width: 1200px;
}
```

### 4.3 Structure layout

**Container réutilisable** :

```css
.container {
  width: 100%;
  max-width: var(--container-max-width);
  margin: 0 auto;
  padding: 0 var(--spacing-sm);
}

/* Pour grands écrans */
@media (min-width: 1024px) {
  .container {
    padding: 0 var(--spacing-md);
  }
}
```

**Sections** :

```css
section {
  padding: var(--spacing-lg) 0;
}

/* Alternance de backgrounds */
section:nth-child(even) {
  background-color: var(--bg-light);
}
```

### 4.4 Technique de développement : De l'extérieur vers l'intérieur

**Approche recommandée** : Styliser les conteneurs parents avant les enfants.

**Exemple** :

```css
/* 1. Structure générale */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* 2. Container interne */
.hero .container {
  text-align: center;
}

/* 3. Éléments internes */
.hero-title {
  font-size: var(--font-size-xl);
  color: white;
  margin-bottom: var(--spacing-sm);
}

.hero-subtitle {
  font-size: var(--font-size-lg);
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: var(--spacing-md);
}
```

---

## Étape 5 : Cas pratiques

### Cas 1 : Header avec navigation

**Maquette** :
```
┌────────────────────────────────────────┐
│ [Logo]        Accueil Services Contact │
└────────────────────────────────────────┘
```

**HTML** :
```html
<header class="site-header">
  <div class="container">
    <a href="/" class="logo">
      <img src="logo.svg" alt="MonSite">
    </a>
    <nav class="main-nav">
      <ul class="nav-list">
        <li><a href="#accueil" class="nav-link">Accueil</a></li>
        <li><a href="#services" class="nav-link">Services</a></li>
        <li><a href="#contact" class="nav-link">Contact</a></li>
      </ul>
    </nav>
    <button class="mobile-menu-btn">☰</button>
  </div>
</header>
```

**CSS** :
```css
.site-header {
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  position: sticky;
  top: 0;
  z-index: 100;
}

.site-header .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: var(--spacing-sm);
  padding-bottom: var(--spacing-sm);
}

.logo img {
  height: 40px;
}

.nav-list {
  display: flex;
  gap: var(--spacing-md);
}

.nav-link {
  color: var(--text-dark);
  font-weight: 500;
  transition: color 0.3s;
}

.nav-link:hover {
  color: var(--primary-color);
}

/* Mobile */
.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
}

@media (max-width: 768px) {
  .main-nav {
    display: none; /* À rendre visible avec JS */
  }

  .mobile-menu-btn {
    display: block;
  }
}
```

---

### Cas 2 : Hero section avec image de fond

**Maquette** :
```
┌────────────────────────────────────────┐
│         [Image de fond]                │
│                                        │
│        Bienvenue sur MonSite           │
│      Nous créons des expériences       │
│            [Bouton CTA]                │
│                                        │
└────────────────────────────────────────┘
```

**HTML** :
```html
<section class="hero">
  <div class="hero-overlay"></div>
  <div class="container hero-content">
    <h1 class="hero-title">Bienvenue sur MonSite</h1>
    <p class="hero-subtitle">Nous créons des expériences</p>
    <a href="#contact" class="btn btn-primary">Commencer</a>
  </div>
</section>
```

**CSS** :
```css
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url('hero-bg.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed; /* Effet parallax */
}

/* Overlay pour assombrir l'image */
.hero-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
}

.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
  color: white;
}

.hero-title {
  font-size: clamp(32px, 5vw, 56px); /* Responsive typography */
  margin-bottom: var(--spacing-sm);
  animation: fadeInUp 1s ease;
}

.hero-subtitle {
  font-size: clamp(18px, 3vw, 24px);
  margin-bottom: var(--spacing-md);
  opacity: 0.9;
  animation: fadeInUp 1s ease 0.2s backwards;
}

/* Animation */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

### Cas 3 : Grille de cartes

**Maquette** :
```
┌──────────┐ ┌──────────┐ ┌──────────┐
│ [Image]  │ │ [Image]  │ │ [Image]  │
│ Titre 1  │ │ Titre 2  │ │ Titre 3  │
│ Desc...  │ │ Desc...  │ │ Desc...  │
│ [Lien]   │ │ [Lien]   │ │ [Lien]   │
└──────────┘ └──────────┘ └──────────┘
```

**HTML** :
```html
<section class="features">
  <div class="container">
    <h2 class="section-title">Nos Services</h2>

    <div class="cards-grid">
      <article class="card">
        <img src="service1.jpg" alt="Service 1" class="card-image">
        <div class="card-content">
          <h3 class="card-title">Développement Web</h3>
          <p class="card-description">
            Création de sites web modernes et responsives.
          </p>
          <a href="#" class="card-link">En savoir plus →</a>
        </div>
      </article>

      <article class="card">
        <img src="service2.jpg" alt="Service 2" class="card-image">
        <div class="card-content">
          <h3 class="card-title">Design UI/UX</h3>
          <p class="card-description">
            Interfaces utilisateur intuitives et esthétiques.
          </p>
          <a href="#" class="card-link">En savoir plus →</a>
        </div>
      </article>

      <article class="card">
        <img src="service3.jpg" alt="Service 3" class="card-image">
        <div class="card-content">
          <h3 class="card-title">SEO</h3>
          <p class="card-description">
            Optimisation pour les moteurs de recherche.
          </p>
          <a href="#" class="card-link">En savoir plus →</a>
        </div>
      </article>
    </div>
  </div>
</section>
```

**CSS** :
```css
.section-title {
  text-align: center;
  font-size: var(--font-size-xl);
  margin-bottom: var(--spacing-lg);
}

/* Grille CSS */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-md);
}

/* Carte */
.card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s, box-shadow 0.3s;
}

.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.15);
}

.card-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card-content {
  padding: var(--spacing-md);
}

.card-title {
  font-size: var(--font-size-lg);
  margin-bottom: var(--spacing-sm);
  color: var(--text-dark);
}

.card-description {
  color: var(--text-light);
  margin-bottom: var(--spacing-sm);
  line-height: 1.6;
}

.card-link {
  color: var(--primary-color);
  font-weight: 500;
  display: inline-block;
  transition: transform 0.3s;
}

.card-link:hover {
  transform: translateX(4px);
}
```

---

### Cas 4 : Formulaire de contact

**Maquette** :
```
┌──────────────────────┐
│ Nom: [___________]   │
│ Email: [_________]   │
│ Message:             │
│ [________________]   │
│ [________________]   │
│ [________________]   │
│     [Envoyer]        │
└──────────────────────┘
```

**HTML** :
```html
<section class="contact">
  <div class="container">
    <h2 class="section-title">Contactez-nous</h2>

    <form class="contact-form">
      <div class="form-group">
        <label for="name" class="form-label">Nom</label>
        <input
          type="text"
          id="name"
          name="name"
          class="form-input"
          required
        >
      </div>

      <div class="form-group">
        <label for="email" class="form-label">Email</label>
        <input
          type="email"
          id="email"
          name="email"
          class="form-input"
          required
        >
      </div>

      <div class="form-group">
        <label for="message" class="form-label">Message</label>
        <textarea
          id="message"
          name="message"
          class="form-textarea"
          rows="5"
          required
        ></textarea>
      </div>

      <button type="submit" class="btn btn-primary">Envoyer</button>
    </form>
  </div>
</section>
```

**CSS** :
```css
.contact-form {
  max-width: 600px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: var(--spacing-md);
}

.form-label {
  display: block;
  margin-bottom: var(--spacing-xs);
  font-weight: 500;
  color: var(--text-dark);
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 4px;
  font-family: inherit;
  font-size: 16px;
  transition: border-color 0.3s;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--primary-color);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
}

/* Bouton (composant réutilisable) */
.btn {
  display: inline-block;
  padding: 12px 32px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s;
  text-align: center;
}

.btn-primary {
  background: var(--primary-color);
  color: white;
}

.btn-primary:hover {
  background: #2980b9;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
```

---

## Étape 6 : Responsive Design

### 6.1 Analyse responsive de la maquette

**Si vous avez plusieurs maquettes** (mobile, tablette, desktop) :

1. **Comparez-les** : Quels éléments changent ?
2. **Identifiez les breakpoints** : À quels moments la mise en page change ?
3. **Planifiez les adaptations** : Menu hamburger, colonnes qui deviennent lignes, etc.

**Si vous n'avez qu'une maquette desktop** :

Anticipez comment les éléments doivent s'adapter :
- Navigation → Menu hamburger
- Grilles 3 colonnes → 2 colonnes → 1 colonne
- Textes grands → Textes adaptés
- Espacements réduits

### 6.2 Breakpoints recommandés

```css
/* Mobile first : styles de base pour mobile */

/* Tablettes */
@media (min-width: 768px) {
  /* Styles tablette */
}

/* Desktop */
@media (min-width: 1024px) {
  /* Styles desktop */
}

/* Grands écrans */
@media (min-width: 1440px) {
  /* Styles grands écrans */
}
```

### 6.3 Adaptation d'une grille

**Mobile** (base) :
```css
.cards-grid {
  display: grid;
  grid-template-columns: 1fr; /* 1 colonne sur mobile */
  gap: var(--spacing-sm);
}
```

**Tablette** :
```css
@media (min-width: 768px) {
  .cards-grid {
    grid-template-columns: repeat(2, 1fr); /* 2 colonnes */
    gap: var(--spacing-md);
  }
}
```

**Desktop** :
```css
@media (min-width: 1024px) {
  .cards-grid {
    grid-template-columns: repeat(3, 1fr); /* 3 colonnes */
  }
}
```

**Alternative avec auto-fit** (plus flexible) :
```css
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--spacing-md);
}
```

### 6.4 Menu responsive

**Desktop** : Menu horizontal
**Mobile** : Menu hamburger

```css
/* Navigation pour desktop */
.main-nav {
  display: block;
}

.nav-list {
  display: flex;
  gap: var(--spacing-md);
}

.mobile-menu-btn {
  display: none;
}

/* Mobile */
@media (max-width: 768px) {
  .mobile-menu-btn {
    display: block;
  }

  .main-nav {
    position: fixed;
    top: 60px;
    left: 0;
    right: 0;
    background: white;
    padding: var(--spacing-md);
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    transform: translateY(-100%);
    transition: transform 0.3s;
  }

  .main-nav.active {
    transform: translateY(0);
  }

  .nav-list {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
}
```

**JavaScript** :
```javascript
const menuBtn = document.querySelector('.mobile-menu-btn');
const mainNav = document.querySelector('.main-nav');

menuBtn.addEventListener('click', () => {
  mainNav.classList.toggle('active');
});
```

---

## Étape 7 : Refinements et détails

### 7.1 Espacements précis

**Comparez avec la maquette** :
- Utilisez les outils de mesure de Figma/XD
- Ajustez les marges et paddings pixel par pixel si nécessaire

**Astuce** : Activez les guides de Figma pour voir les espacements.

### 7.2 Typographie exacte

**Font-size** :
```css
/* Si la maquette indique 18px */
.text {
  font-size: 18px; /* ou 1.125rem si base = 16px */
}
```

**Line-height** :
```css
/* Généralement entre 1.4 et 1.8 pour la lisibilité */
p {
  line-height: 1.6;
}

h1, h2, h3 {
  line-height: 1.2;
}
```

**Letter-spacing** (si spécifié dans la maquette) :
```css
.title {
  letter-spacing: -0.02em; /* Rapproche les lettres */
}

.uppercase-text {
  letter-spacing: 0.1em; /* Écarte les lettres */
}
```

### 7.3 Ombres et effets

**Box shadows** :
```css
/* Ombre légère */
.card {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* Ombre prononcée */
.modal {
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
}

/* Ombre au survol */
.card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
}
```

**Text shadows** (rare, mais parfois nécessaire) :
```css
.hero-title {
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
}
```

### 7.4 Transitions et animations

**Ajoutez des transitions** pour les interactions :

```css
/* Sur tous les éléments interactifs */
a, button, .card {
  transition: all 0.3s ease;
}

/* Transitions spécifiques */
.nav-link {
  transition: color 0.3s ease;
}

.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
```

**Animations subtiles** :
```css
/* Fade in au chargement */
.fade-in {
  animation: fadeIn 0.6s ease;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* Slide up au scroll (avec JS pour trigger) */
.slide-up {
  animation: slideUp 0.6s ease;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

## Outils et techniques avancés

### 1. Mesurer précisément avec les DevTools

**Dans Chrome DevTools** :

1. Inspectez un élément
2. Dans l'onglet "Computed", voyez les dimensions exactes
3. Comparez avec la maquette
4. Ajustez si nécessaire

**Astuce** : Faites un screenshot de votre site et superposez-le avec la maquette dans Photoshop/Figma pour comparer pixel par pixel.

### 2. Extension Chrome : Pixel Perfect

**Pixel Perfect** permet de superposer votre maquette sur votre site pour vérifier l'alignement.

**Utilisation** :
1. Installez l'extension
2. Uploadez votre maquette (image)
3. Ajustez l'opacité
4. Vérifiez l'alignement

### 3. Figma → CSS

**Figma permet d'exporter le CSS** :

1. Sélectionnez un élément dans Figma
2. Panneau de droite → Section "Code"
3. Copiez le CSS généré

**⚠️ Attention** : Le CSS de Figma est parfois verbeux. Nettoyez-le et simplifiez-le.

### 4. Zeplin / Avocode

**Outils de collaboration designer-développeur** :

- **Zeplin** : Importe les designs et génère les specs
- **Avocode** : Similaire, avec export de code

**Avantages** :
- Mesures automatiques
- Export d'assets
- CSS généré
- Collaboration facilitée

---

## Workflow efficace

### Approche itérative recommandée

#### 1. HTML structurel (30 minutes)
- Toutes les balises sémantiques
- Contenu texte (même placeholder)
- Pas de classes CSS encore (ou minimales)

**Vérification** : La structure est logique sans CSS ?

#### 2. CSS Layout (1 heure)
- Positionnement des grandes sections
- Flexbox / Grid pour les layouts
- Responsive de base

**Vérification** : La structure tient debout sur mobile et desktop ?

#### 3. CSS Styling (2-3 heures)
- Couleurs
- Typographies
- Espacements
- Borders et ombres

**Vérification** : Ressemble à la maquette à 80% ?

#### 4. Détails et polish (1-2 heures)
- Ajustements fins
- Transitions
- Animations
- États hover/focus

**Vérification** : Ressemble à la maquette à 95%+ ?

#### 5. JavaScript (si nécessaire) (1-3 heures)
- Interactivité
- Animations au scroll
- Validation de formulaires
- Menu mobile

**Vérification** : Tout fonctionne comme attendu ?

#### 6. Tests et optimisation (1 heure)
- Tests navigateurs
- Tests responsive
- Validation HTML/CSS
- Optimisation des images

---

## Checklist de fidélité à la maquette

**Avant de considérer le travail terminé** :

### Général
- [ ] Toutes les sections sont présentes
- [ ] L'ordre des éléments correspond
- [ ] Les espacements sont respectés (+/- 5px)
- [ ] La hiérarchie visuelle est respectée

### Couleurs
- [ ] Couleurs principales exactes
- [ ] Couleurs de texte correctes
- [ ] Backgrounds corrects
- [ ] Hover states conformes

### Typographie
- [ ] Polices correctes et chargées
- [ ] Tailles de police respectées
- [ ] Poids de police (bold, regular) corrects
- [ ] Line-height approprié
- [ ] Letter-spacing si spécifié

### Images
- [ ] Toutes les images présentes
- [ ] Dimensions respectées
- [ ] Qualité suffisante (pas pixelisées)
- [ ] Attributs alt présents

### Interactions
- [ ] Liens fonctionnels
- [ ] Boutons avec états hover
- [ ] Transitions fluides
- [ ] Animations (si présentes dans la maquette)

### Responsive
- [ ] Mobile : tout s'affiche correctement
- [ ] Tablette : layout adapté
- [ ] Desktop : conforme à la maquette
- [ ] Pas de débordement horizontal

---

## Erreurs courantes et comment les éviter

### Erreur 1 : Vouloir coder en regardant la maquette

**❌ Mauvaise approche** :
- Ouvrir VS Code et Figma côte à côte
- Coder en regardant la maquette
- Allers-retours constants

**✅ Bonne approche** :
- Analyser la maquette d'abord (15-30 min)
- Prendre des notes (couleurs, espacements, etc.)
- Extraire les assets
- Puis coder avec les notes

### Erreur 2 : Coder le CSS avant la structure HTML

**❌** : Commencer par écrire les styles sans avoir fini le HTML

**✅** : Finir toute la structure HTML, puis commencer le CSS

**Pourquoi** : Le CSS dépend de la structure. Si vous changez le HTML après, vous devez réécrire beaucoup de CSS.

### Erreur 3 : Ne pas utiliser de classes réutilisables

**❌ Mauvais** :
```css
.hero button {
  background: blue;
  padding: 12px 24px;
  border-radius: 4px;
}

.contact button {
  background: blue;
  padding: 12px 24px;
  border-radius: 4px;
}
```

**✅ Bon** :
```css
.btn {
  background: blue;
  padding: 12px 24px;
  border-radius: 4px;
}
```

### Erreur 4 : Ignorer le responsive

**❌** : Coder en desktop uniquement, puis essayer d'adapter

**✅** : Approche mobile-first ou tester régulièrement le responsive

### Erreur 5 : Pixels fixes partout

**❌ Mauvais** :
```css
.container {
  width: 1200px; /* Déborde sur petit écran */
}
```

**✅ Bon** :
```css
.container {
  width: 100%;
  max-width: 1200px;
  padding: 0 20px;
}
```

### Erreur 6 : Copier-coller le CSS de Figma sans comprendre

**Figma génère parfois** :
```css
/* CSS généré par Figma - verbeux */
position: absolute;
width: 375px;
height: 812px;
left: 0px;
top: 0px;
background: linear-gradient(180deg, #667EEA 0%, #764BA2 100%);
```

**Ce qu'il faut vraiment** :
```css
/* CSS nettoyé et simplifié */
.hero {
  min-height: 100vh;
  background: linear-gradient(180deg, #667EEA 0%, #764BA2 100%);
}
```

---

## Ressources et outils

### Outils d'extraction de maquette

| Outil | Usage | Prix |
|-------|-------|------|
| **Figma** | Design et export | Gratuit (limité) |
| **Adobe XD** | Design et export | Gratuit |
| **Sketch** | Design (Mac only) | Payant |
| **Zeplin** | Collaboration designer-dev | Gratuit (limité) |
| **Avocode** | Export et collaboration | Payant |

### Extensions Chrome utiles

- **ColorZilla** : Color picker
- **Pixel Perfect** : Superposition de maquette
- **WhatFont** : Identifier les polices
- **Dimensions** : Mesurer les espacements

### Bibliothèques d'icônes

- **Font Awesome** : https://fontawesome.com/
- **Feather Icons** : https://feathericons.com/
- **Heroicons** : https://heroicons.com/
- **Material Icons** : https://fonts.google.com/icons

### Images gratuites

- **Unsplash** : https://unsplash.com/
- **Pexels** : https://www.pexels.com/
- **Pixabay** : https://pixabay.com/

---

## Conclusion

Passer de la maquette au code est une compétence qui s'améliore avec la pratique. Les clés du succès :

- ✅ **Analyser avant de coder** : Prenez le temps de comprendre la structure
- ✅ **Décomposer en petites tâches** : Section par section, composant par composant
- ✅ **Être méthodique** : HTML structure → CSS layout → CSS styling → JavaScript
- ✅ **Tester régulièrement** : Vérifiez le responsive et la compatibilité navigateurs
- ✅ **Être patient** : La perfection pixel-perfect prend du temps

**Au début**, il vous faudra peut-être 2-3 jours pour transformer une maquette simple en code.
**Avec l'expérience**, vous ferez la même chose en quelques heures.

**L'important** : Ne pas se décourager. Chaque projet vous rend plus rapide et efficace.

**Prochain objectif** : Pratiquez ! Prenez une maquette gratuite sur Figma Community ou Dribbble et transformez-la en code. C'est le meilleur moyen de progresser. 🚀

---


⏭️ [Git : notions avancées et collaboration](/07-debugging-et-outils-avances/04-workflow-developpement/03-git-avance.md)
