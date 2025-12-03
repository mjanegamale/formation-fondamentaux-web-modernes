🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2.3 Éléments sémantiques HTML5

## Introduction

HTML5 a introduit une révolution majeure dans la façon de structurer les pages web : les **éléments sémantiques**. Ces balises ont transformé le développement web en remplaçant les `<div>` anonymes par des éléments qui ont un **sens** et décrivent clairement leur contenu.

**Avant HTML5 :**
```html
<div id="header">...</div>
<div id="nav">...</div>
<div id="main">...</div>
<div id="footer">...</div>
```

**Avec HTML5 :**
```html
<header>...</header>
<nav>...</nav>
<main>...</main>
<footer>...</footer>
```

La différence peut sembler minime, mais l'impact est **énorme** pour l'accessibilité, le SEO et la maintenabilité de votre code.

## Qu'est-ce que la sémantique en HTML ?

### Définition

La **sémantique** en HTML signifie que chaque élément a une **signification** claire qui décrit son **rôle** dans la page, et pas seulement son apparence visuelle.

**Analogie :** Imaginez un journal papier :
- Le **titre principal** en haut → `<header>`
- Le **sommaire** → `<nav>`
- Les **articles** → `<article>`
- La **publicité** sur le côté → `<aside>`
- Les **informations légales** en bas → `<footer>`

Chaque section a un rôle spécifique et reconnaissable. HTML5 applique ce principe au web.

### Pourquoi c'est important ?

#### 1. Pour l'accessibilité ♿

Les **lecteurs d'écran** utilisent la sémantique pour :
- Identifier les différentes zones de la page
- Permettre une navigation rapide (sauter au contenu principal, à la navigation, etc.)
- Annoncer le type de contenu à l'utilisateur

**Exemple :** Un utilisateur aveugle peut dire "Va à la navigation principale" et le lecteur d'écran sautera directement à `<nav>`.

#### 2. Pour le référencement (SEO) 🔍

Google et les autres moteurs de recherche :
- Comprennent mieux la structure de votre page
- Identifient plus facilement le contenu principal
- Peuvent donner plus de poids au contenu dans `<article>` ou `<main>`
- Indexent plus efficacement votre site

#### 3. Pour la maintenabilité 🛠️

Un code sémantique est :
- Plus lisible (vous savez immédiatement ce que fait chaque section)
- Plus facile à modifier (vous trouvez rapidement ce que vous cherchez)
- Plus professionnel (c'est la norme moderne)

**Comparaison :**

❌ **Difficile à comprendre :**
```html
<div class="top">
    <div class="menu">...</div>
</div>
<div class="content">
    <div class="post">...</div>
</div>
```

✅ **Clair et évident :**
```html
<header>
    <nav>...</nav>
</header>
<main>
    <article>...</article>
</main>
```

## Les principaux éléments sémantiques HTML5

HTML5 a introduit plusieurs nouvelles balises sémantiques. Voici les plus importantes :

### Vue d'ensemble

| Élément | Rôle | Utilisation typique |
|---------|------|---------------------|
| `<header>` | En-tête | Logo, titre, navigation principale |
| `<nav>` | Navigation | Menu principal, fil d'ariane |
| `<main>` | Contenu principal | Contenu unique de la page |
| `<article>` | Article autonome | Article de blog, produit, commentaire |
| `<section>` | Section thématique | Chapitre, onglet, groupe de contenu |
| `<aside>` | Contenu annexe | Barre latérale, publicité, liens connexes |
| `<footer>` | Pied de page | Copyright, liens légaux, contact |
| `<figure>` | Illustration | Image avec légende |
| `<figcaption>` | Légende | Description d'une figure |

## `<header>` : L'en-tête

### Définition

`<header>` représente un **groupe de contenu introductif** ou de navigation. C'est typiquement l'en-tête de votre page ou d'une section.

### Où l'utiliser ?

**En-tête de page (le plus courant) :**
```html
<header>
    <img src="logo.png" alt="Logo de l'entreprise">
    <h1>Mon Site Web</h1>
    <nav>
        <ul>
            <li><a href="/">Accueil</a></li>
            <li><a href="/services">Services</a></li>
            <li><a href="/contact">Contact</a></li>
        </ul>
    </nav>
</header>
```

**En-tête d'article :**
```html
<article>
    <header>
        <h2>Titre de l'article</h2>
        <p>Publié le <time datetime="2025-01-15">15 janvier 2025</time></p>
        <p>Par Jean Dupont</p>
    </header>
    <p>Contenu de l'article...</p>
</article>
```

**En-tête de section :**
```html
<section>
    <header>
        <h2>Nos services</h2>
        <p>Découvrez notre gamme complète de solutions</p>
    </header>
    <!-- Contenu de la section -->
</section>
```

### Ce que peut contenir un `<header>`

- Logo de l'entreprise ou du site
- Titre principal (`<h1>`, `<h2>`, etc.)
- Navigation (`<nav>`)
- Slogan ou baseline
- Informations de publication (date, auteur)
- Barre de recherche

### Important

- Une page peut avoir **plusieurs `<header>`** (un pour la page, un par article, etc.)
- Ne confondez pas `<header>` avec `<head>` (les métadonnées)
- `<header>` ne peut pas être imbriqué dans un autre `<header>`, `<footer>` ou `<address>`

## `<nav>` : La navigation

### Définition

`<nav>` contient les **principaux liens de navigation** du site ou d'une section. C'est réservé aux **navigations majeures**, pas à tous les liens de la page.

### Où l'utiliser ?

**Menu principal du site :**
```html
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/produits">Produits</a></li>
        <li><a href="/a-propos">À propos</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

**Fil d'Ariane (breadcrumb) :**
```html
<nav aria-label="Fil d'Ariane">
    <ol>
        <li><a href="/">Accueil</a></li>
        <li><a href="/produits">Produits</a></li>
        <li><a href="/produits/ordinateurs">Ordinateurs</a></li>
        <li>MacBook Pro</li>
    </ol>
</nav>
```

**Table des matières d'un article :**
```html
<nav aria-label="Table des matières">
    <h2>Dans cet article</h2>
    <ol>
        <li><a href="#intro">Introduction</a></li>
        <li><a href="#methode">Méthodologie</a></li>
        <li><a href="#resultats">Résultats</a></li>
        <li><a href="#conclusion">Conclusion</a></li>
    </ol>
</nav>
```

**Pagination :**
```html
<nav aria-label="Pagination">
    <ul>
        <li><a href="/page/1">Page précédente</a></li>
        <li><a href="/page/1">1</a></li>
        <li><a href="/page/2">2</a></li>
        <li><a href="/page/3">3</a></li>
        <li><a href="/page/3">Page suivante</a></li>
    </ul>
</nav>
```

### Quand NE PAS utiliser `<nav>` ?

❌ **Pas pour tous les groupes de liens :**
```html
<!-- Mauvais : ce n'est pas une navigation principale -->
<nav>
    <a href="/mentions-legales">Mentions légales</a>
    <a href="/cgv">CGV</a>
</nav>

<!-- Mieux : utilisez simplement un <p> ou <div> -->
<p>
    <a href="/mentions-legales">Mentions légales</a>
    <a href="/cgv">CGV</a>
</p>
```

❌ **Pas pour les liens sociaux (généralement) :**
```html
<!-- Ces liens ne sont pas vraiment de la "navigation" -->
<div class="social-links">
    <a href="https://facebook.com/...">Facebook</a>
    <a href="https://twitter.com/...">Twitter</a>
</div>
```

### Bonnes pratiques

- Utilisez `aria-label` pour différencier plusieurs `<nav>` :
```html
<nav aria-label="Navigation principale">...</nav>
<nav aria-label="Liens de bas de page">...</nav>
```

- Limitez-vous aux navigations **vraiment importantes**
- Une page peut avoir plusieurs `<nav>`, mais restez raisonnable (2-3 maximum généralement)

## `<main>` : Le contenu principal

### Définition

`<main>` contient le **contenu principal unique** de la page. C'est le contenu qui change d'une page à l'autre, excluant les éléments répétés (en-tête, navigation, pied de page).

### Règles importantes

⚠️ **Il ne doit y avoir qu'UN SEUL `<main>` par page**

⚠️ **`<main>` ne doit PAS être un descendant de** `<article>`, `<aside>`, `<footer>`, `<header>` ou `<nav>`

### Exemple de structure

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <title>Mon site</title>
</head>
<body>
    <!-- En-tête répété sur toutes les pages -->
    <header>
        <h1>Mon Site</h1>
        <nav>...</nav>
    </header>

    <!-- Le contenu unique de CETTE page -->
    <main>
        <h2>Bienvenue sur notre page d'accueil</h2>
        <p>Contenu spécifique à cette page...</p>
    </main>

    <!-- Pied de page répété sur toutes les pages -->
    <footer>
        <p>&copy; 2025 Mon Site</p>
    </footer>
</body>
</html>
```

### Pourquoi c'est important ?

**Pour l'accessibilité :**
Les lecteurs d'écran peuvent proposer un raccourci "Aller au contenu principal" qui saute directement au `<main>`, évitant la navigation et l'en-tête.

**Pour le SEO :**
Google peut identifier plus facilement le contenu principal de la page et lui donner plus de poids dans le référencement.

### Exemple page article de blog

```html
<body>
    <header>
        <h1>Mon Blog</h1>
        <nav>
            <ul>
                <li><a href="/">Accueil</a></li>
                <li><a href="/blog">Articles</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <article>
            <h2>Titre de l'article</h2>
            <p>Contenu de l'article...</p>
        </article>

        <section id="commentaires">
            <h3>Commentaires</h3>
            <!-- Liste des commentaires -->
        </section>
    </main>

    <footer>
        <p>&copy; 2025 Mon Blog</p>
    </footer>
</body>
```

## `<article>` : Contenu autonome

### Définition

`<article>` représente un **contenu autonome** et **indépendant** qui pourrait être distribué ou réutilisé séparément (via RSS, réseaux sociaux, etc.).

### Test simple

**Question :** "Ce contenu aurait-il du sens s'il était extrait de la page et lu tout seul ?"

- **Oui** → Utilisez `<article>`
- **Non** → Utilisez `<section>` ou `<div>`

### Exemples d'utilisation

**Article de blog :**
```html
<article>
    <header>
        <h2>Les 10 meilleures pratiques HTML5</h2>
        <p>Publié le <time datetime="2025-01-15">15 janvier 2025</time></p>
        <p>Par Marie Durand</p>
    </header>

    <p>Introduction de l'article...</p>

    <h3>1. Utiliser les balises sémantiques</h3>
    <p>Explication...</p>

    <footer>
        <p>Tags : HTML, Web, Développement</p>
        <p>Partager : <a href="#">Facebook</a> | <a href="#">Twitter</a></p>
    </footer>
</article>
```

**Produit e-commerce :**
```html
<article>
    <h3>iPhone 15 Pro</h3>
    <img src="iphone.jpg" alt="iPhone 15 Pro">
    <p>Le smartphone le plus avancé.</p>
    <p class="prix">1 229 €</p>
    <button>Ajouter au panier</button>
</article>
```

**Commentaire d'utilisateur :**
```html
<article>
    <header>
        <h4>Jean Dupont</h4>
        <p><time datetime="2025-01-15T14:30">Il y a 2 heures</time></p>
    </header>
    <p>Super article, très instructif !</p>
    <footer>
        <button>Répondre</button>
        <button>Signaler</button>
    </footer>
</article>
```

**Widget ou gadget :**
```html
<article>
    <h3>Météo du jour</h3>
    <p>Paris : 12°C, Nuageux</p>
    <p>Prévisions pour demain : 15°C, Ensoleillé</p>
</article>
```

### Articles imbriqués

Un `<article>` peut contenir d'autres `<article>` :

```html
<article>
    <h2>Article principal sur les voyages</h2>
    <p>Contenu de l'article...</p>

    <section>
        <h3>Commentaires</h3>

        <article>
            <h4>Jean</h4>
            <p>Super article !</p>
        </article>

        <article>
            <h4>Marie</h4>
            <p>Très intéressant.</p>
        </article>
    </section>
</article>
```

## `<section>` : Section thématique

### Définition

`<section>` représente une **section générique** d'un document, typiquement avec un titre. C'est un regroupement thématique de contenu.

### Différence avec `<article>`

- **`<article>`** : Contenu autonome et réutilisable
- **`<section>`** : Partie d'un tout, dépendant du contexte

### Quand utiliser `<section>` ?

**Chapitres d'un document :**
```html
<article>
    <h1>Guide complet du HTML5</h1>

    <section>
        <h2>Introduction</h2>
        <p>Le HTML5 est...</p>
    </section>

    <section>
        <h2>Les bases</h2>
        <p>Pour commencer...</p>
    </section>

    <section>
        <h2>Techniques avancées</h2>
        <p>Une fois les bases maîtrisées...</p>
    </section>
</article>
```

**Onglets de contenu :**
```html
<section id="description">
    <h2>Description</h2>
    <p>Détails du produit...</p>
</section>

<section id="caracteristiques">
    <h2>Caractéristiques</h2>
    <ul>...</ul>
</section>

<section id="avis">
    <h2>Avis clients</h2>
    <p>Note moyenne : 4.5/5</p>
</section>
```

**Sections d'une page d'accueil :**
```html
<main>
    <section id="hero">
        <h2>Bienvenue chez nous</h2>
        <p>Slogan accrocheur...</p>
    </section>

    <section id="services">
        <h2>Nos services</h2>
        <div>...</div>
    </section>

    <section id="temoignages">
        <h2>Ce que disent nos clients</h2>
        <div>...</div>
    </section>
</main>
```

### Règle importante

⚠️ Une `<section>` devrait **toujours avoir un titre** (h1-h6). Si vous ne pouvez pas donner un titre logique à votre section, utilisez plutôt `<div>`.

❌ **Mauvais (pas de titre) :**
```html
<section>
    <p>Juste un paragraphe sans titre logique...</p>
</section>
```

✅ **Bon :**
```html
<section>
    <h2>À propos de nous</h2>
    <p>Nous sommes une entreprise...</p>
</section>

<!-- OU, si pas de titre logique, utilisez <div> -->
<div>
    <p>Juste un paragraphe...</p>
</div>
```

## `<aside>` : Contenu annexe

### Définition

`<aside>` représente du contenu **tangentiellement lié** au contenu principal, mais qui pourrait être séparé sans perdre le sens principal.

### Utilisations courantes

**Barre latérale (sidebar) :**
```html
<main>
    <article>
        <h1>Article principal</h1>
        <p>Contenu...</p>
    </article>
</main>

<aside>
    <h2>Articles connexes</h2>
    <ul>
        <li><a href="#">Article 1</a></li>
        <li><a href="#">Article 2</a></li>
    </ul>

    <h2>Publicité</h2>
    <div class="ad">...</div>
</aside>
```

**Encadré dans un article :**
```html
<article>
    <h1>L'histoire de l'Internet</h1>
    <p>L'Internet moderne a débuté dans les années 1960...</p>

    <aside>
        <h3>Le saviez-vous ?</h3>
        <p>Le premier message envoyé sur Internet était "LOGIN".</p>
    </aside>

    <p>Suite de l'article...</p>
</article>
```

**Citation ou définition :**
```html
<article>
    <p>Le concept de responsive design a révolutionné le web...</p>

    <aside>
        <h4>Définition</h4>
        <p><strong>Responsive design :</strong> Approche de conception qui permet aux sites web de s'adapter à différentes tailles d'écran.</p>
    </aside>

    <p>Continuons avec les techniques...</p>
</article>
```

**Widget :**
```html
<aside>
    <h3>Newsletter</h3>
    <form>
        <input type="email" placeholder="Votre email">
        <button>S'abonner</button>
    </form>
</aside>
```

### Ce que `<aside>` n'est PAS

❌ **Pas pour n'importe quel contenu secondaire :**
Si le contenu est essentiel à la compréhension du contenu principal, ce n'est pas un `<aside>`.

❌ **Pas automatiquement à mettre sur le côté visuellement :**
`<aside>` indique un sens sémantique, pas une position. Vous pouvez styler un `<aside>` pour qu'il apparaisse n'importe où avec CSS.

## `<footer>` : Pied de page

### Définition

`<footer>` représente le **pied de page** d'une section ou de la page entière. Il contient typiquement des informations sur l'auteur, le copyright, des liens légaux, etc.

### Pied de page du site

```html
<footer>
    <div class="footer-content">
        <section>
            <h3>À propos</h3>
            <p>Notre entreprise...</p>
        </section>

        <section>
            <h3>Liens utiles</h3>
            <ul>
                <li><a href="/mentions-legales">Mentions légales</a></li>
                <li><a href="/cgv">CGV</a></li>
                <li><a href="/politique-confidentialite">Confidentialité</a></li>
            </ul>
        </section>

        <section>
            <h3>Contact</h3>
            <p>Email : contact@exemple.com</p>
            <p>Tél : 01 23 45 67 89</p>
        </section>
    </div>

    <p>&copy; 2025 Mon Entreprise. Tous droits réservés.</p>
</footer>
```

### Pied de page d'article

```html
<article>
    <header>
        <h2>Titre de l'article</h2>
        <p>Par Jean Dupont</p>
    </header>

    <p>Contenu de l'article...</p>

    <footer>
        <p>Publié le <time datetime="2025-01-15">15 janvier 2025</time></p>
        <p>Catégories :
            <a href="/cat/tech">Technologie</a>,
            <a href="/cat/web">Web</a>
        </p>
        <p>Partager :
            <a href="#">Facebook</a> |
            <a href="#">Twitter</a> |
            <a href="#">LinkedIn</a>
        </p>
    </footer>
</article>
```

### Ce que peut contenir un `<footer>`

- Copyright et mentions légales
- Coordonnées de contact
- Liens de navigation secondaire
- Liens vers les réseaux sociaux
- Informations sur l'auteur
- Métadonnées (date, catégories, tags)

### Important

- Une page peut avoir plusieurs `<footer>` (un pour la page, un par article, etc.)
- Le footer peut contenir des `<section>`, des liens, etc.
- Ne confondez pas avec `<foot>` (qui n'existe pas en HTML !)

## `<figure>` et `<figcaption>` : Illustrations

### Définition

`<figure>` encapsule une **illustration** (image, diagramme, code, citation) avec sa **légende** optionnelle (`<figcaption>`).

### Structure de base

```html
<figure>
    <img src="photo.jpg" alt="Description de la photo">
    <figcaption>Légende de l'image</figcaption>
</figure>
```

### Exemples d'utilisation

**Image avec légende :**
```html
<figure>
    <img src="tour-eiffel.jpg" alt="La Tour Eiffel illuminée la nuit">
    <figcaption>
        La Tour Eiffel de nuit, photographiée depuis le Trocadéro.
        Photo : Jean Dupont, 2024
    </figcaption>
</figure>
```

**Plusieurs images (galerie) :**
```html
<figure>
    <img src="photo1.jpg" alt="Photo 1">
    <img src="photo2.jpg" alt="Photo 2">
    <img src="photo3.jpg" alt="Photo 3">
    <figcaption>Galerie de photos de vacances en Bretagne</figcaption>
</figure>
```

**Extrait de code :**
```html
<figure>
    <pre><code>
function hello() {
    console.log("Hello World!");
}
    </code></pre>
    <figcaption>Exemple de fonction JavaScript simple</figcaption>
</figure>
```

**Citation longue :**
```html
<figure>
    <blockquote>
        <p>Être ou ne pas être, telle est la question.</p>
    </blockquote>
    <figcaption>
        <cite>Hamlet</cite>, William Shakespeare
    </figcaption>
</figure>
```

**Vidéo :**
```html
<figure>
    <video controls>
        <source src="demo.mp4" type="video/mp4">
    </video>
    <figcaption>Démonstration du produit en action</figcaption>
</figure>
```

**Diagramme ou illustration :**
```html
<figure>
    <svg width="200" height="200">
        <!-- Code SVG du diagramme -->
    </svg>
    <figcaption>Diagramme circulaire des ventes par région</figcaption>
</figure>
```

### Position de `<figcaption>`

La légende peut être **avant ou après** le contenu :

```html
<!-- Légende après (le plus courant) -->
<figure>
    <img src="photo.jpg" alt="Photo">
    <figcaption>Légende</figcaption>
</figure>

<!-- Légende avant -->
<figure>
    <figcaption>Légende</figcaption>
    <img src="photo.jpg" alt="Photo">
</figure>
```

### Important

- `<figcaption>` est **optionnel** (vous pouvez avoir `<figure>` sans légende)
- Il ne peut y avoir qu'**un seul `<figcaption>`** par `<figure>`
- `<figcaption>` doit être le **premier ou dernier enfant** de `<figure>`

## `<div>` et `<span>` : Les conteneurs génériques

### Quand utiliser `<div>` et `<span>` ?

Après avoir vu tous ces éléments sémantiques, vous vous demandez peut-être : "Quand utiliser `<div>` et `<span>` ?"

**Réponse :** Utilisez-les **uniquement quand aucun élément sémantique ne convient**, généralement pour le style ou le scripting.

### `<div>` : Conteneur de bloc

`<div>` est un conteneur **de bloc** (prend toute la largeur, crée une nouvelle ligne) sans signification sémantique.

**Utilisation légitime :**
```html
<!-- Wrapper pour le style CSS -->
<div class="container">
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
</div>

<!-- Grille de mise en page -->
<div class="grid">
    <div class="grid-item">...</div>
    <div class="grid-item">...</div>
    <div class="grid-item">...</div>
</div>

<!-- Carte visuelle (card) -->
<div class="card">
    <h3>Titre de la carte</h3>
    <p>Contenu...</p>
</div>
```

### `<span>` : Conteneur en ligne

`<span>` est un conteneur **en ligne** (ne crée pas de nouvelle ligne) sans signification sémantique.

**Utilisation légitime :**
```html
<!-- Style sur une partie de texte -->
<p>Le mot <span class="highlight">important</span> est surligné.</p>

<!-- Icône dans un bouton -->
<button>
    <span class="icon">📧</span>
    Envoyer
</button>

<!-- Manipulation JavaScript -->
<p>Température actuelle : <span id="temp">20</span>°C</p>
```

### Privilégier le sémantique

✅ **Préférez les éléments sémantiques quand ils existent :**

```html
<!-- ❌ Mauvais -->
<div id="header">
    <div id="nav">...</div>
</div>

<!-- ✅ Bon -->
<header>
    <nav>...</nav>
</header>
```

```html
<!-- ❌ Mauvais -->
<div class="article">
    <div class="title">Titre</div>
</div>

<!-- ✅ Bon -->
<article>
    <h2>Titre</h2>
</article>
```

## Structure complète d'une page moderne

Voici un exemple de page HTML5 avec tous les éléments sémantiques :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog Tech - Article du jour</title>
</head>
<body>
    <!-- En-tête du site -->
    <header>
        <div class="container">
            <img src="logo.png" alt="Logo Blog Tech">
            <h1>Blog Tech</h1>

            <!-- Navigation principale -->
            <nav aria-label="Navigation principale">
                <ul>
                    <li><a href="/">Accueil</a></li>
                    <li><a href="/articles">Articles</a></li>
                    <li><a href="/tutoriels">Tutoriels</a></li>
                    <li><a href="/a-propos">À propos</a></li>
                    <li><a href="/contact">Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Contenu principal unique de cette page -->
    <main>
        <div class="container">
            <!-- Article principal -->
            <article>
                <header>
                    <h2>Les nouveautés HTML5 en 2025</h2>
                    <p>
                        Publié le <time datetime="2025-01-15">15 janvier 2025</time>
                        par <a href="/auteurs/marie">Marie Durand</a>
                    </p>
                </header>

                <figure>
                    <img src="html5-hero.jpg" alt="Logo HTML5">
                    <figcaption>Le logo officiel de HTML5</figcaption>
                </figure>

                <section>
                    <h3>Introduction</h3>
                    <p>HTML5 continue d'évoluer en 2025 avec de nouvelles fonctionnalités...</p>
                </section>

                <section>
                    <h3>Les éléments sémantiques</h3>
                    <p>Les balises sémantiques transforment la façon dont nous structurons nos pages...</p>

                    <aside>
                        <h4>Le saviez-vous ?</h4>
                        <p>Les éléments sémantiques ont été introduits en 2014.</p>
                    </aside>
                </section>

                <section>
                    <h3>Exemples pratiques</h3>
                    <figure>
                        <pre><code>&lt;header&gt;
    &lt;h1&gt;Mon site&lt;/h1&gt;
&lt;/header&gt;</code></pre>
                        <figcaption>Exemple de code HTML5</figcaption>
                    </figure>
                </section>

                <footer>
                    <p>
                        Catégories :
                        <a href="/cat/html">HTML</a>,
                        <a href="/cat/web">Développement Web</a>
                    </p>
                    <p>
                        Partager :
                        <a href="#">Facebook</a> |
                        <a href="#">Twitter</a> |
                        <a href="#">LinkedIn</a>
                    </p>
                </footer>
            </article>

            <!-- Section des commentaires -->
            <section id="commentaires">
                <h3>Commentaires (3)</h3>

                <article class="commentaire">
                    <header>
                        <h4>Jean Dupont</h4>
                        <p><time datetime="2025-01-15T10:30">Il y a 2 heures</time></p>
                    </header>
                    <p>Excellent article, très clair !</p>
                    <footer>
                        <button>Répondre</button>
                        <button>👍 5</button>
                    </footer>
                </article>

                <article class="commentaire">
                    <header>
                        <h4>Sophie Martin</h4>
                        <p><time datetime="2025-01-15T11:00">Il y a 1 heure</time></p>
                    </header>
                    <p>Merci pour ces explications détaillées.</p>
                    <footer>
                        <button>Répondre</button>
                        <button>👍 3</button>
                    </footer>
                </article>
            </section>
        </div>

        <!-- Barre latérale -->
        <aside>
            <section>
                <h3>Articles populaires</h3>
                <ul>
                    <li><a href="#">CSS Grid en 2025</a></li>
                    <li><a href="#">JavaScript ES2025</a></li>
                    <li><a href="#">Accessibilité web</a></li>
                </ul>
            </section>

            <section>
                <h3>Newsletter</h3>
                <form>
                    <input type="email" placeholder="Votre email">
                    <button>S'abonner</button>
                </form>
            </section>
        </aside>
    </main>

    <!-- Pied de page du site -->
    <footer>
        <div class="container">
            <section>
                <h3>À propos</h3>
                <p>Blog Tech est un site dédié au développement web moderne.</p>
            </section>

            <section>
                <h3>Liens</h3>
                <nav aria-label="Liens de bas de page">
                    <ul>
                        <li><a href="/mentions-legales">Mentions légales</a></li>
                        <li><a href="/politique-confidentialite">Confidentialité</a></li>
                        <li><a href="/cgv">CGV</a></li>
                        <li><a href="/plan-du-site">Plan du site</a></li>
                    </ul>
                </nav>
            </section>

            <section>
                <h3>Suivez-nous</h3>
                <div class="social">
                    <a href="#">Facebook</a>
                    <a href="#">Twitter</a>
                    <a href="#">LinkedIn</a>
                </div>
            </section>

            <p>&copy; 2025 Blog Tech. Tous droits réservés.</p>
        </div>
    </footer>
</body>
</html>
```

## Tableau récapitulatif des éléments sémantiques

| Élément | Peut être multiple ? | Peut contenir des titres ? | Usage principal |
|---------|---------------------|---------------------------|-----------------|
| `<header>` | ✅ Oui | ✅ Oui | En-tête de page/section |
| `<nav>` | ✅ Oui | ✅ Oui | Navigation importante |
| `<main>` | ❌ Un seul | ✅ Oui | Contenu principal unique |
| `<article>` | ✅ Oui | ✅ Oui | Contenu autonome |
| `<section>` | ✅ Oui | ✅ Oui (obligatoire) | Section thématique |
| `<aside>` | ✅ Oui | ✅ Oui | Contenu tangentiel |
| `<footer>` | ✅ Oui | ✅ Oui | Pied de page |
| `<figure>` | ✅ Oui | ❌ Non | Illustration avec légende |
| `<figcaption>` | ❌ Un par figure | ❌ Non | Légende d'une figure |

## Erreurs courantes à éviter

### Erreur 1 : Utiliser `<section>` sans titre

❌ **Mauvais :**
```html
<section>
    <p>Juste du contenu...</p>
</section>
```

✅ **Bon :**
```html
<section>
    <h2>Titre de la section</h2>
    <p>Contenu...</p>
</section>

<!-- Ou utilisez <div> si pas de titre logique -->
<div>
    <p>Juste du contenu...</p>
</div>
```

### Erreur 2 : Plusieurs `<main>` par page

❌ **Mauvais :**
```html
<main>
    <h1>Première partie</h1>
</main>
<main>
    <h1>Deuxième partie</h1>
</main>
```

✅ **Bon :**
```html
<main>
    <section>
        <h1>Première partie</h1>
    </section>
    <section>
        <h2>Deuxième partie</h2>
    </section>
</main>
```

### Erreur 3 : Confondre `<article>` et `<section>`

❌ **Mauvais :**
```html
<!-- Section d'une page qui n'a pas de sens toute seule -->
<article>
    <h2>Nos horaires d'ouverture</h2>
    <p>Lundi-Vendredi : 9h-18h</p>
</article>
```

✅ **Bon :**
```html
<section>
    <h2>Nos horaires d'ouverture</h2>
    <p>Lundi-Vendredi : 9h-18h</p>
</section>
```

### Erreur 4 : Utiliser `<nav>` pour tous les liens

❌ **Mauvais :**
```html
<nav>
    <a href="/mentions-legales">Mentions légales</a>
    <a href="/cgv">CGV</a>
</nav>
```

✅ **Bon :**
```html
<!-- Ce ne sont pas des liens de navigation principaux -->
<p>
    <a href="/mentions-legales">Mentions légales</a> |
    <a href="/cgv">CGV</a>
</p>
```

### Erreur 5 : Imbriquer mal les éléments

❌ **Mauvais :**
```html
<main>
    <header>
        <main>...</main>  <!-- main ne peut pas être dans header -->
    </header>
</main>
```

✅ **Bon :**
```html
<header>...</header>
<main>...</main>
```

### Erreur 6 : Ne pas utiliser les éléments sémantiques

❌ **Mauvais (style ancien, pré-HTML5) :**
```html
<div id="header">
    <div id="nav">...</div>
</div>
<div id="content">
    <div class="post">...</div>
</div>
<div id="sidebar">...</div>
<div id="footer">...</div>
```

✅ **Bon (HTML5 moderne) :**
```html
<header>
    <nav>...</nav>
</header>
<main>
    <article>...</article>
</main>
<aside>...</aside>
<footer>...</footer>
```

## Accessibilité et ARIA

### Rôles ARIA implicites

Les éléments sémantiques HTML5 ont des **rôles ARIA implicites** :

- `<header>` = `role="banner"` (quand enfant direct de `<body>`)
- `<nav>` = `role="navigation"`
- `<main>` = `role="main"`
- `<article>` = `role="article"`
- `<aside>` = `role="complementary"`
- `<footer>` = `role="contentinfo"` (quand enfant direct de `<body>`)

**Important :** N'ajoutez PAS ces rôles manuellement, ils sont automatiques !

❌ **Redondant (inutile) :**
```html
<nav role="navigation">...</nav>
```

✅ **Suffisant :**
```html
<nav>...</nav>
```

### Labels pour plusieurs éléments identiques

Utilisez `aria-label` ou `aria-labelledby` pour différencier plusieurs éléments du même type :

```html
<nav aria-label="Navigation principale">
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/blog">Blog</a></li>
    </ul>
</nav>

<nav aria-label="Liens de bas de page">
    <ul>
        <li><a href="/mentions">Mentions légales</a></li>
        <li><a href="/cgv">CGV</a></li>
    </ul>
</nav>
```

## Validation et vérification

### Validateur W3C

Vérifiez toujours votre HTML avec le validateur W3C : https://validator.w3.org/

Il détectera :
- Les erreurs de structure
- Les imbrications incorrectes
- Les éléments mal utilisés

### Extensions navigateur

- **HeadingsMap** : Affiche la structure des titres et sections
- **WAVE** : Évalue l'accessibilité
- **Accessibility Insights** : Teste l'accessibilité en profondeur

## Bonnes pratiques récapitulatives

### Checklist HTML sémantique

- [ ] J'utilise `<header>` pour les en-têtes
- [ ] J'utilise `<nav>` pour les navigations principales uniquement
- [ ] J'ai un seul `<main>` par page
- [ ] J'utilise `<article>` pour le contenu autonome
- [ ] Mes `<section>` ont toutes un titre
- [ ] J'utilise `<aside>` pour le contenu annexe
- [ ] J'utilise `<footer>` pour les pieds de page
- [ ] J'utilise `<figure>` et `<figcaption>` pour les illustrations
- [ ] Je n'abuse pas de `<div>` et `<span>`
- [ ] Ma structure est logique et cohérente

### Principes à retenir

1. **Sémantique avant style** : Choisissez les balises selon leur sens, pas leur apparence
2. **Spécificité** : Utilisez l'élément le plus spécifique possible
3. **Hiérarchie** : Respectez une structure logique
4. **Accessibilité** : Pensez aux lecteurs d'écran
5. **Validation** : Vérifiez toujours votre code

## Conclusion

Les éléments sémantiques HTML5 ne sont pas qu'une question de "beau code" : ils sont **essentiels** pour :

- **L'accessibilité** : Les technologies d'assistance comprennent mieux votre structure
- **Le SEO** : Les moteurs de recherche indexent mieux votre contenu
- **La maintenabilité** : Votre code est plus lisible et professionnel
- **Les standards** : Vous suivez les meilleures pratiques modernes

**Récapitulatif des éléments clés :**

| Élément | Utilisation |
|---------|-------------|
| `<header>` | En-tête (page ou section) |
| `<nav>` | Navigation principale |
| `<main>` | Contenu principal unique |
| `<article>` | Contenu autonome et réutilisable |
| `<section>` | Section thématique avec titre |
| `<aside>` | Contenu tangentiel |
| `<footer>` | Pied de page |
| `<figure>` + `<figcaption>` | Illustration avec légende |

En adoptant ces éléments sémantiques dès maintenant, vous créez des pages web modernes, accessibles et bien structurées. C'est une pratique professionnelle indispensable pour tout développeur web en 2025.

Dans la prochaine section, nous découvrirons les liens hypertextes et la navigation, éléments fondamentaux qui font du web ce qu'il est : un réseau interconnecté de pages.

---


**Section suivante** : [3.2.4 Liens hypertextes et navigation](./04-liens-hypertextes-et-navigation.md)

⏭️ [Liens hypertextes et navigation](/03-html5-structure-et-semantique/02-elements-structurants/04-liens-hypertextes-et-navigation.md)
