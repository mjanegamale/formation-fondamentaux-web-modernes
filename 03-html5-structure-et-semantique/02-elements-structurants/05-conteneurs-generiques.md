🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2.5 Conteneurs génériques : div et span

## Introduction

Après avoir découvert tous les éléments sémantiques HTML5 (`<header>`, `<nav>`, `<article>`, etc.), vous vous demandez peut-être : "Quand utiliser `<div>` et `<span>` ?" Ces deux balises sont des **conteneurs génériques** sans signification sémantique particulière.

**Règle d'or :** Utilisez toujours un élément sémantique quand c'est possible. `<div>` et `<span>` sont des **solutions de dernier recours** quand aucune balise sémantique ne convient.

**Dans cette section, vous apprendrez :**
- Ce que sont `<div>` et `<span>`
- La différence entre éléments de bloc et en ligne
- Quand utiliser ces conteneurs génériques
- Comment éviter l'abus de `<div>` et `<span>`
- Les bonnes pratiques d'utilisation

## `<div>` : Conteneur de bloc

### Qu'est-ce qu'un `<div>` ?

`<div>` (pour "division") est un **conteneur de bloc générique** sans signification sémantique. C'est comme une boîte vide que vous pouvez remplir avec du contenu et styliser avec CSS.

**Syntaxe de base :**
```html
<div>
    <!-- Contenu ici -->
</div>
```

### Caractéristiques d'un élément de bloc

Un `<div>` est un **élément de bloc**, ce qui signifie qu'il :

1. **Prend toute la largeur disponible** par défaut
2. **Commence sur une nouvelle ligne**
3. **Crée une nouvelle ligne après lui**
4. **Peut contenir d'autres éléments** (de bloc ou en ligne)

**Exemple visuel :**
```html
<div style="background: lightblue;">Div 1</div>
<div style="background: lightgreen;">Div 2</div>
<div style="background: lightyellow;">Div 3</div>
```

**Rendu :**
```
┌─────────────────────────┐
│ Div 1                   │  (prend toute la largeur)
└─────────────────────────┘
┌─────────────────────────┐
│ Div 2                   │  (nouvelle ligne)
└─────────────────────────┘
┌─────────────────────────┐
│ Div 3                   │  (nouvelle ligne)
└─────────────────────────┘
```

### Autres éléments de bloc (pour comparaison)

Voici d'autres exemples d'éléments de bloc que vous connaissez déjà :
- `<p>` (paragraphe)
- `<h1>` à `<h6>` (titres)
- `<ul>`, `<ol>`, `<li>` (listes)
- `<header>`, `<footer>`, `<main>`, `<section>`, `<article>`, etc.

**Important :** Ces éléments ont une **signification sémantique**, contrairement à `<div>`.

## `<span>` : Conteneur en ligne

### Qu'est-ce qu'un `<span>` ?

`<span>` est un **conteneur en ligne générique** sans signification sémantique. C'est utile pour cibler une partie spécifique de texte sans créer de nouvelle ligne.

**Syntaxe de base :**
```html
<p>Ceci est un <span>mot important</span> dans une phrase.</p>
```

### Caractéristiques d'un élément en ligne

Un `<span>` est un **élément en ligne**, ce qui signifie qu'il :

1. **Ne prend que la largeur nécessaire** à son contenu
2. **Ne crée pas de nouvelle ligne**
3. **S'insère dans le flux du texte**
4. **Ne peut contenir que d'autres éléments en ligne** (pas d'éléments de bloc)

**Exemple visuel :**
```html
<p>
    Voici un <span style="color: red;">mot en rouge</span> et
    un <span style="background: yellow;">mot surligné</span> dans une phrase.
</p>
```

**Rendu :**
```
Voici un mot en rouge et un mot surligné dans une phrase.
         └─rouge─┘       └──jaune──┘
```

### Autres éléments en ligne (pour comparaison)

Voici d'autres exemples d'éléments en ligne que vous connaissez :
- `<a>` (lien)
- `<strong>` (texte important)
- `<em>` (emphase)
- `<code>` (code informatique)
- `<img>` (image - techniquement "inline-block")

**Important :** Ces éléments ont une **signification sémantique**, contrairement à `<span>`.

## Différence entre `<div>` et `<span>`

### Comparaison visuelle

```html
<!-- <div> : élément de bloc -->
<div>Premier div</div>
<div>Deuxième div</div>

<!-- Résultat : chaque div sur sa propre ligne -->
```

```html
<!-- <span> : élément en ligne -->
<p>
    <span>Premier span</span>
    <span>Deuxième span</span>
</p>

<!-- Résultat : les spans côte à côte dans le paragraphe -->
```

### Tableau récapitulatif

| Caractéristique | `<div>` | `<span>` |
|----------------|---------|----------|
| Type | Bloc | En ligne |
| Nouvelle ligne | Oui | Non |
| Largeur par défaut | 100% | Selon le contenu |
| Peut contenir | Bloc + Inline | Inline uniquement |
| Usage typique | Structure, layout | Style sur texte |

### Règle importante

❌ **Invalide : `<span>` ne peut pas contenir de bloc**
```html
<span>
    <div>Ceci est invalide !</div>
</span>
```

✅ **Valide : `<div>` peut contenir des `<span>`**
```html
<div>
    <span>Ceci est valide</span>
</div>
```

## Quand utiliser `<div>` ?

### Cas d'usage légitimes

#### 1. Wrapper pour la mise en page CSS

Créer un conteneur pour appliquer du CSS (flexbox, grid, centrage, etc.) :

```html
<div class="container">
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
</div>
```

**En CSS :**
```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}
```

#### 2. Grilles et layouts

Créer des structures de mise en page :

```html
<div class="grid">
    <div class="grid-item">
        <h3>Produit 1</h3>
        <p>Description...</p>
    </div>
    <div class="grid-item">
        <h3>Produit 2</h3>
        <p>Description...</p>
    </div>
    <div class="grid-item">
        <h3>Produit 3</h3>
        <p>Description...</p>
    </div>
</div>
```

**En CSS :**
```css
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

#### 3. Cartes (cards) ou composants visuels

Créer des composants qui n'ont pas d'équivalent sémantique :

```html
<div class="card">
    <img src="photo.jpg" alt="Photo de produit">
    <h3>Titre du produit</h3>
    <p>Description courte...</p>
    <button>Acheter</button>
</div>
```

#### 4. Effets visuels ou décoratifs

Créer des éléments purement décoratifs :

```html
<div class="hero">
    <div class="hero-overlay"></div>
    <h1>Bienvenue sur notre site</h1>
</div>
```

**En CSS :**
```css
.hero {
    position: relative;
    background-image: url(hero.jpg);
}

.hero-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
}
```

#### 5. Groupement pour JavaScript

Cibler plusieurs éléments pour les manipuler ensemble :

```html
<div id="notification" class="hidden">
    <p>Message enregistré avec succès !</p>
    <button onclick="closeNotification()">Fermer</button>
</div>
```

**En JavaScript :**
```javascript
function showNotification() {
    document.getElementById('notification').classList.remove('hidden');
}
```

### Exemples pratiques avec `<div>`

**Exemple 1 : Layout de page**
```html
<body>
    <div class="wrapper">
        <header>
            <div class="container">
                <img src="logo.png" alt="Logo">
                <nav>...</nav>
            </div>
        </header>

        <main>
            <div class="container">
                <!-- Contenu principal -->
            </div>
        </main>

        <footer>
            <div class="container">
                <!-- Pied de page -->
            </div>
        </footer>
    </div>
</body>
```

**Exemple 2 : Grille de produits**
```html
<section>
    <h2>Nos produits</h2>

    <div class="products-grid">
        <div class="product-card">
            <img src="produit1.jpg" alt="Produit 1">
            <h3>Nom du produit</h3>
            <p class="price">99,99 €</p>
            <button>Ajouter au panier</button>
        </div>

        <div class="product-card">
            <img src="produit2.jpg" alt="Produit 2">
            <h3>Nom du produit</h3>
            <p class="price">149,99 €</p>
            <button>Ajouter au panier</button>
        </div>

        <!-- Plus de produits... -->
    </div>
</section>
```

## Quand utiliser `<span>` ?

### Cas d'usage légitimes

#### 1. Styliser une partie de texte

Appliquer du CSS à une portion spécifique de texte :

```html
<p>Le prix est de <span class="price">99,99 €</span> seulement.</p>
```

**En CSS :**
```css
.price {
    color: red;
    font-weight: bold;
    font-size: 1.2em;
}
```

#### 2. Mettre en évidence

Surligner ou mettre en valeur des mots :

```html
<p>Attention : les <span class="highlight">délais de livraison</span> peuvent varier.</p>
```

**En CSS :**
```css
.highlight {
    background-color: yellow;
    font-weight: bold;
}
```

#### 3. Icônes dans le texte

Insérer des icônes ou symboles :

```html
<button>
    <span class="icon">📧</span>
    Envoyer un email
</button>
```

#### 4. Manipulation JavaScript

Cibler un élément spécifique dans le texte :

```html
<p>Température actuelle : <span id="temperature">20</span>°C</p>
```

**En JavaScript :**
```javascript
document.getElementById('temperature').textContent = '25';
```

#### 5. Texte décoratif ou stylé

Créer des effets typographiques :

```html
<h1>
    <span class="text-gradient">Bienvenue</span>
</h1>
```

**En CSS :**
```css
.text-gradient {
    background: linear-gradient(45deg, #ff0000, #0000ff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}
```

### Exemples pratiques avec `<span>`

**Exemple 1 : Badge ou étiquette**
```html
<h2>
    Nouvelle formation
    <span class="badge">Nouveau</span>
</h2>
```

**Exemple 2 : Prix avec devise**
```html
<p class="product-price">
    <span class="amount">99</span>
    <span class="currency">€</span>
</p>
```

**Exemple 3 : Statut coloré**
```html
<p>
    Statut de votre commande :
    <span class="status status-success">Livrée</span>
</p>
```

**Exemple 4 : Texte avec tooltip**
```html
<p>
    Utilisez le
    <span class="tooltip" title="HyperText Markup Language">HTML</span>
    pour structurer vos pages.
</p>
```

## Quand NE PAS utiliser `<div>` et `<span>`

### Privilégier les éléments sémantiques

#### ❌ Mauvais : Divs pour tout

```html
<div class="header">
    <div class="nav">
        <div class="nav-item">Accueil</div>
        <div class="nav-item">Services</div>
    </div>
</div>
<div class="main">
    <div class="article">
        <div class="title">Titre de l'article</div>
        <div class="content">Contenu...</div>
    </div>
</div>
<div class="footer">
    <div class="copyright">© 2025</div>
</div>
```

#### ✅ Bon : Éléments sémantiques appropriés

```html
<header>
    <nav>
        <a href="/">Accueil</a>
        <a href="/services">Services</a>
    </nav>
</header>
<main>
    <article>
        <h2>Titre de l'article</h2>
        <p>Contenu...</p>
    </article>
</main>
<footer>
    <p>&copy; 2025</p>
</footer>
```

### Exemples de mauvaise utilisation

#### ❌ Utiliser `<div>` au lieu de `<p>`
```html
<div>Ceci est un paragraphe.</div>
```

✅ **Mieux :**
```html
<p>Ceci est un paragraphe.</p>
```

#### ❌ Utiliser `<span>` au lieu de `<strong>`
```html
<p>Ceci est <span style="font-weight: bold;">important</span>.</p>
```

✅ **Mieux :**
```html
<p>Ceci est <strong>important</strong>.</p>
```

#### ❌ Utiliser `<div>` au lieu de `<button>`
```html
<div onclick="submitForm()">Envoyer</div>
```

✅ **Mieux :**
```html
<button onclick="submitForm()">Envoyer</button>
```

#### ❌ Utiliser `<div>` au lieu de listes
```html
<div class="menu">
    <div>Accueil</div>
    <div>Services</div>
    <div>Contact</div>
</div>
```

✅ **Mieux :**
```html
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services">Services</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

## Le problème de "divitis" et "spanitis"

### Qu'est-ce que la "divitis" ?

La **"divitis"** est l'abus de balises `<div>` à outrance, créant un code verbeux et non sémantique.

**Symptômes :**
- Des `<div>` imbriqués sur 10 niveaux ou plus
- Des `<div>` utilisés même quand un élément sémantique existe
- Difficulté à comprendre la structure du code

#### ❌ Exemple de divitis sévère
```html
<div class="page">
    <div class="header-wrapper">
        <div class="header-container">
            <div class="header-content">
                <div class="logo-wrapper">
                    <div class="logo">
                        <img src="logo.png" alt="Logo">
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

#### ✅ Version simplifiée et sémantique
```html
<header>
    <div class="container">
        <img src="logo.png" alt="Logo" class="logo">
    </div>
</header>
```

### Qu'est-ce que la "spanitis" ?

La **"spanitis"** est l'abus de balises `<span>` là où des éléments sémantiques existent.

#### ❌ Exemple de spanitis
```html
<p>
    <span style="font-weight: bold;">Attention :</span>
    <span style="font-style: italic;">Ceci est important</span>
</p>
```

#### ✅ Version sémantique
```html
<p>
    <strong>Attention :</strong>
    <em>Ceci est important</em>
</p>
```

## Classes et IDs avec `<div>` et `<span>`

### Utilisation des classes

Les classes permettent de styliser et cibler plusieurs éléments :

```html
<div class="card">
    <h3>Produit 1</h3>
</div>

<div class="card">
    <h3>Produit 2</h3>
</div>

<div class="card highlight">
    <h3>Produit vedette</h3>
</div>
```

**En CSS :**
```css
.card {
    border: 1px solid #ddd;
    padding: 20px;
    margin-bottom: 10px;
}

.card.highlight {
    border-color: gold;
    background: lightyellow;
}
```

### Utilisation des IDs

Les IDs permettent de cibler un élément unique :

```html
<div id="notification">
    <span class="icon">✓</span>
    <span class="message">Message enregistré !</span>
</div>
```

**Rappel important :**
- **Classe** : Peut être utilisée sur **plusieurs éléments**
- **ID** : Doit être **unique** sur la page

### Nommage des classes

✅ **Bonnes pratiques de nommage :**
```html
<div class="product-card">
    <span class="product-price">99€</span>
    <span class="product-badge">Nouveau</span>
</div>
```

**Conventions courantes :**
- **kebab-case** : `product-card`, `main-content`, `user-profile`
- **camelCase** : `productCard`, `mainContent`, `userProfile`
- **BEM** : `block__element--modifier`

❌ **À éviter :**
```html
<div class="div1">  <!-- Pas descriptif -->
<span class="red">  <!-- Décrit le style, pas le contenu -->
<div class="DIV">   <!-- Tout en majuscules -->
```

## Accessibilité et `<div>`/`<span>`

### Le problème d'accessibilité

`<div>` et `<span>` n'ont **aucune signification** pour les technologies d'assistance :

- Pas de rôle ARIA implicite
- Pas d'indication sémantique
- Les lecteurs d'écran les ignorent (sauf leur contenu)

### Solutions

#### 1. Privilégier les éléments sémantiques

✅ **Bon :**
```html
<button>Cliquer ici</button>
```

❌ **Moins accessible :**
```html
<div onclick="handleClick()">Cliquer ici</div>
```

#### 2. Ajouter des rôles ARIA si nécessaire

Si vous **devez** utiliser `<div>` pour un composant interactif :

```html
<div role="button" tabindex="0" onclick="handleClick()" onkeypress="handleClick()">
    Cliquer ici
</div>
```

**Mais c'est mieux d'utiliser :**
```html
<button onclick="handleClick()">Cliquer ici</button>
```

#### 3. Utiliser des attributs ARIA

Pour améliorer la sémantique quand nécessaire :

```html
<div role="alert" aria-live="polite">
    <span class="icon">⚠️</span>
    <span>Message important</span>
</div>
```

## Exemples complets bien structurés

### Exemple 1 : Carte de produit

```html
<article class="product-card">
    <div class="product-image">
        <img src="produit.jpg" alt="Nom du produit">
        <span class="badge badge-new">Nouveau</span>
    </div>

    <div class="product-info">
        <h3>Nom du produit</h3>
        <p class="product-description">Description courte du produit...</p>

        <div class="product-footer">
            <span class="product-price">
                <span class="amount">99</span>
                <span class="currency">€</span>
            </span>
            <button class="btn btn-primary">Acheter</button>
        </div>
    </div>
</article>
```

**Points positifs :**
- Utilise `<article>` (sémantique)
- Les `<div>` servent uniquement au layout
- Les `<span>` stylisent des parties de texte
- Titre avec `<h3>` (sémantique)
- Bouton avec `<button>` (sémantique)

### Exemple 2 : Layout de page complète

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon site</title>
</head>
<body>
    <!-- Wrapper général pour contraindre la largeur -->
    <div class="site-wrapper">

        <!-- En-tête sémantique -->
        <header class="site-header">
            <div class="container">
                <img src="logo.png" alt="Logo" class="logo">

                <nav>
                    <ul class="nav-list">
                        <li><a href="/">Accueil</a></li>
                        <li><a href="/services">Services</a></li>
                        <li><a href="/contact">Contact</a></li>
                    </ul>
                </nav>
            </div>
        </header>

        <!-- Contenu principal -->
        <main class="site-main">
            <div class="container">

                <!-- Section hero avec div pour l'overlay -->
                <section class="hero">
                    <div class="hero-overlay"></div>
                    <div class="hero-content">
                        <h1>Bienvenue sur notre site</h1>
                        <p>Découvrez nos services</p>
                        <button class="btn btn-primary">En savoir plus</button>
                    </div>
                </section>

                <!-- Grille de services -->
                <section class="services">
                    <h2>Nos services</h2>

                    <div class="services-grid">
                        <div class="service-card">
                            <span class="service-icon">🎨</span>
                            <h3>Design</h3>
                            <p>Création graphique professionnelle</p>
                        </div>

                        <div class="service-card">
                            <span class="service-icon">💻</span>
                            <h3>Développement</h3>
                            <p>Sites web sur mesure</p>
                        </div>

                        <div class="service-card">
                            <span class="service-icon">📱</span>
                            <h3>Mobile</h3>
                            <p>Applications iOS et Android</p>
                        </div>
                    </div>
                </section>

            </div>
        </main>

        <!-- Pied de page sémantique -->
        <footer class="site-footer">
            <div class="container">
                <p>&copy; 2025 Mon Entreprise. Tous droits réservés.</p>

                <div class="footer-links">
                    <a href="/mentions-legales">Mentions légales</a>
                    <span class="separator">|</span>
                    <a href="/cgv">CGV</a>
                    <span class="separator">|</span>
                    <a href="/contact">Contact</a>
                </div>
            </div>
        </footer>

    </div>
</body>
</html>
```

**Analyse :**
- Éléments sémantiques (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`)
- `<div>` utilisés pour le layout et le positionnement (.container, .services-grid)
- `<span>` utilisés pour les icônes et séparateurs
- Hiérarchie de titres respectée (`<h1>`, `<h2>`, `<h3>`)
- Classes descriptives et bien nommées

### Exemple 3 : Notification/Alert

```html
<div class="notification notification-success" role="alert">
    <div class="notification-header">
        <span class="notification-icon">✓</span>
        <strong class="notification-title">Succès</strong>
        <button class="notification-close" aria-label="Fermer">&times;</button>
    </div>

    <div class="notification-body">
        <p>Votre message a été envoyé avec succès !</p>
    </div>
</div>
```

**Points positifs :**
- `role="alert"` pour l'accessibilité
- `<strong>` pour le titre (sémantique)
- `<button>` pour le bouton de fermeture
- `aria-label` pour le bouton sans texte
- `<p>` pour le texte (sémantique)

## Checklist des bonnes pratiques

Avant d'utiliser `<div>` ou `<span>`, demandez-vous :

### Pour `<div>`
- [ ] Ai-je vérifié qu'aucun élément sémantique ne convient ?
- [ ] Est-ce vraiment nécessaire pour le layout ou le style ?
- [ ] Ai-je une classe ou un ID descriptif ?
- [ ] Est-ce que j'évite la "divitis" (trop de divs imbriqués) ?
- [ ] Si c'est pour une interaction, ne devrais-je pas utiliser `<button>` ?

### Pour `<span>`
- [ ] Ai-je vérifié qu'aucun élément sémantique ne convient ?
- [ ] Est-ce pour styliser une partie de texte seulement ?
- [ ] Ne puis-je pas utiliser `<strong>`, `<em>`, ou une autre balise sémantique ?
- [ ] Ai-je une classe descriptive si nécessaire ?

### Règles générales
- [ ] Mon HTML reste lisible et compréhensible
- [ ] La structure a du sens même sans CSS
- [ ] Les éléments interactifs utilisent les bonnes balises
- [ ] Mon code est accessible (lecteurs d'écran, clavier)

## Résumé des principes

### Hiérarchie de choix

Quand vous devez structurer du contenu, suivez cet ordre de préférence :

1. **Éléments sémantiques HTML5** (`<header>`, `<article>`, `<nav>`, etc.)
2. **Éléments HTML classiques** (`<p>`, `<h1>-<h6>`, `<ul>`, `<button>`, etc.)
3. **`<div>` et `<span>`** (en dernier recours)

### Tableau de décision

| Si vous voulez... | N'utilisez PAS | Utilisez |
|-------------------|----------------|----------|
| Un paragraphe | `<div>` | `<p>` |
| Un titre | `<div>` ou `<span>` | `<h1>` à `<h6>` |
| Un bouton | `<div>` ou `<span>` | `<button>` |
| Un lien | `<div>` ou `<span>` | `<a>` |
| Emphase | `<span>` avec style | `<em>` ou `<strong>` |
| Citation | `<div>` ou `<span>` | `<blockquote>` |
| Code | `<span>` | `<code>` |
| Liste | `<div>` répétés | `<ul>` + `<li>` |
| Navigation | `<div>` | `<nav>` |
| Article | `<div>` | `<article>` |
| Layout/Wrapper | ... | `<div>` ✓ |
| Styliser du texte | ... | `<span>` ✓ |

## Erreurs courantes

### Erreur 1 : Tout mettre dans des `<div>`

❌ **Mauvais :**
```html
<div>
    <div>Titre principal</div>
    <div>Ceci est un paragraphe</div>
    <div>
        <div>Item 1</div>
        <div>Item 2</div>
    </div>
</div>
```

✅ **Bon :**
```html
<article>
    <h1>Titre principal</h1>
    <p>Ceci est un paragraphe</p>
    <ul>
        <li>Item 1</li>
        <li>Item 2</li>
    </ul>
</article>
```

### Erreur 2 : Utiliser `<div>` pour des boutons

❌ **Mauvais :**
```html
<div class="button" onclick="submit()">Envoyer</div>
```

✅ **Bon :**
```html
<button onclick="submit()">Envoyer</button>
```

### Erreur 3 : Noms de classes basés sur le style

❌ **Mauvais :**
```html
<div class="red-box">Attention</div>
<span class="bold">Important</span>
```

✅ **Bon :**
```html
<div class="alert alert-danger">Attention</div>
<strong>Important</strong>
```

### Erreur 4 : `<span>` contenant du bloc

❌ **Invalide :**
```html
<span>
    <div>Contenu</div>
</span>
```

✅ **Valide :**
```html
<div>
    <span>Contenu</span>
</div>
```

### Erreur 5 : Divs/spans sans raison

❌ **Inutile :**
```html
<div>
    <p>Un seul paragraphe</p>
</div>
```

✅ **Simplifié :**
```html
<p>Un seul paragraphe</p>
```

## Conclusion

`<div>` et `<span>` sont des outils **indispensables** mais doivent être utilisés avec **parcimonie** et **intelligence**.

**Points clés à retenir :**

| Élément | Type | Usage principal | Règle d'or |
|---------|------|----------------|------------|
| `<div>` | Bloc | Layout, structure CSS | Quand aucun élément sémantique ne convient |
| `<span>` | Inline | Style sur texte | Quand aucun élément inline sémantique ne convient |

**Les trois commandements :**

1. **Sémantique d'abord** : Utilisez toujours un élément sémantique si possible
2. **Divs avec raison** : Chaque `<div>` doit avoir une justification (layout, style, script)
3. **Classes descriptives** : Nommez vos classes selon leur **fonction**, pas leur **apparence**

**Pensez ainsi :**
- `<div>` = Conteneur neutre pour organiser visuellement
- `<span>` = Wrapper neutre pour styliser du texte
- Éléments sémantiques = Sens et structure du contenu

En maîtrisant quand et comment utiliser `<div>` et `<span>` en complément des éléments sémantiques, vous créez un HTML **propre**, **accessible** et **maintenable**.

Dans la prochaine section, nous découvrirons le contenu multimédia : images, vidéos et audio, des éléments essentiels pour enrichir vos pages web.

---


**Section suivante** : [3.3 Contenu multimédia](../03-contenu-multimedia/README.md)

⏭️ [Contenu multimédia](/03-html5-structure-et-semantique/03-contenu-multimedia/README.md)
