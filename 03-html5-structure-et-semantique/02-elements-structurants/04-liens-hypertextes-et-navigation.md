🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2.4 Liens hypertextes et navigation

## Introduction

Les **liens hypertextes** (ou simplement "liens") sont l'essence même du web. Le "H" de HTML signifie d'ailleurs "HyperText", qui désigne du texte contenant des liens vers d'autres documents. Sans les liens, Internet ne serait qu'une collection de pages isolées. Ce sont les liens qui créent le **réseau** (web en anglais) qui connecte des milliards de pages entre elles.

Dans cette section, nous allons découvrir :
- Comment créer des liens
- Les différents types de liens
- Comment créer des menus de navigation
- Les bonnes pratiques pour des liens accessibles et efficaces

**Symbole universel :** Sur le web, le texte souligné en bleu est devenu le symbole universel d'un lien cliquable (même si les designers modernes changent souvent ces couleurs).

## La balise `<a>` : créer un lien

### Syntaxe de base

La balise `<a>` (pour "anchor" = ancre) est utilisée pour créer des liens hypertextes.

```html
<a href="https://www.exemple.com">Cliquez ici</a>
```

**Anatomie d'un lien :**
- **`<a>`** : La balise ouvrante
- **`href="..."`** : L'attribut qui contient la destination du lien (obligatoire)
- **Texte du lien** : Le texte visible et cliquable
- **`</a>`** : La balise fermante

**Important :** `href` signifie "hypertext reference" (référence hypertexte).

### Exemple simple

```html
<p>Visitez notre <a href="https://www.exemple.com">site web</a> pour plus d'informations.</p>
```

**Rendu :**
Visitez notre [site web](lien souligné en bleu) pour plus d'informations.

### Le texte du lien

Le texte entre `<a>` et `</a>` est ce que l'utilisateur voit et peut cliquer. Il doit être :

✅ **Descriptif et clair**
```html
<a href="/contact">Contactez-nous</a>
<a href="/telecharger-guide.pdf">Télécharger le guide (PDF, 2 Mo)</a>
```

❌ **Évitez les textes vagues**
```html
<a href="/contact">Cliquez ici</a>  <!-- Trop vague -->
<a href="/page">En savoir plus</a>  <!-- Sur quoi ? -->
<a href="/doc.pdf">Télécharger</a>  <!-- Quoi ? Quel format ? -->
```

**Pourquoi ?**
- **Accessibilité** : Les lecteurs d'écran peuvent lister tous les liens. "Cliquez ici, cliquez ici, cliquez ici" ne dit rien !
- **SEO** : Google utilise le texte des liens pour comprendre le contenu de la page de destination
- **UX** : Les utilisateurs scannent la page et repèrent les liens pertinents

## Les différents types de liens

### 1. Liens externes (vers d'autres sites)

Les liens **externes** pointent vers des sites web différents du vôtre. Utilisez toujours l'**URL complète** (avec `https://`).

```html
<a href="https://www.google.com">Google</a>
<a href="https://www.wikipedia.org">Wikipédia</a>
<a href="https://developer.mozilla.org">MDN Web Docs</a>
```

**Structure d'une URL complète :**
```
https://www.exemple.com/page/sous-page.html
│      │               │                 │
│      │               │                 └─ Nom du fichier
│      │               └─────────────────── Chemin
│      └─────────────────────────────────── Nom de domaine
└────────────────────────────────────────── Protocole
```

**Important :** Utilisez toujours `https://` (sécurisé) plutôt que `http://` quand c'est possible.

### 2. Liens internes (vers d'autres pages de votre site)

Les liens **internes** pointent vers d'autres pages de votre propre site. Vous pouvez utiliser des **chemins relatifs**.

**Chemins relatifs (recommandé) :**
```html
<!-- Dans le même dossier -->
<a href="contact.html">Contact</a>
<a href="about.html">À propos</a>

<!-- Dans un sous-dossier -->
<a href="blog/article-1.html">Lire l'article</a>
<a href="produits/iphone.html">iPhone</a>

<!-- Dans un dossier parent -->
<a href="../index.html">Retour à l'accueil</a>
```

**Chemins absolus (possible mais moins flexible) :**
```html
<a href="https://www.monsite.com/contact.html">Contact</a>
```

**Avantages des chemins relatifs :**
- Fonctionnent en développement local (sur votre ordinateur)
- Pas de problème si vous changez de nom de domaine
- Plus courts et plus lisibles

**Structure de fichiers typique :**
```
mon-site/
├── index.html
├── contact.html
├── about.html
├── blog/
│   ├── article-1.html
│   └── article-2.html
└── images/
    └── logo.png
```

**Depuis `index.html` :**
```html
<a href="contact.html">Contact</a>
<a href="blog/article-1.html">Article 1</a>
```

**Depuis `blog/article-1.html` :**
```html
<a href="../index.html">Accueil</a>
<a href="../contact.html">Contact</a>
<a href="article-2.html">Article suivant</a>
```

### 3. Ancres (liens vers une section de la page)

Les **ancres** permettent de créer des liens vers une section **spécifique** de la même page (ou d'une autre page).

**Étape 1 : Créer une cible avec un ID**
```html
<h2 id="services">Nos services</h2>
```

**Étape 2 : Créer le lien vers cette ancre**
```html
<!-- Depuis la même page -->
<a href="#services">Aller à la section Services</a>

<!-- Depuis une autre page -->
<a href="about.html#services">Voir nos services</a>
```

**Exemple complet : Table des matières**
```html
<nav>
    <h2>Sommaire</h2>
    <ul>
        <li><a href="#introduction">Introduction</a></li>
        <li><a href="#chapitre1">Chapitre 1</a></li>
        <li><a href="#chapitre2">Chapitre 2</a></li>
        <li><a href="#conclusion">Conclusion</a></li>
    </ul>
</nav>

<section id="introduction">
    <h2>Introduction</h2>
    <p>Contenu de l'introduction...</p>
</section>

<section id="chapitre1">
    <h2>Chapitre 1</h2>
    <p>Contenu du chapitre 1...</p>
</section>

<section id="chapitre2">
    <h2>Chapitre 2</h2>
    <p>Contenu du chapitre 2...</p>
</section>

<section id="conclusion">
    <h2>Conclusion</h2>
    <p>Contenu de la conclusion...</p>
</section>
```

**Lien "Retour en haut" :**
```html
<!-- En haut de la page -->
<div id="top"></div>

<!-- En bas de la page -->
<a href="#top">↑ Retour en haut</a>
```

**Important :** Les ID doivent être **uniques** sur la page.

### 4. Liens de téléchargement

L'attribut `download` force le téléchargement d'un fichier au lieu de l'ouvrir dans le navigateur.

```html
<!-- Téléchargement avec nom original -->
<a href="documents/guide.pdf" download>Télécharger le guide</a>

<!-- Téléchargement avec nom personnalisé -->
<a href="doc.pdf" download="guide-complet-2025.pdf">Télécharger</a>
```

**Bonnes pratiques :**
- Indiquez le **format** et la **taille** du fichier
```html
<a href="rapport.pdf" download>Télécharger le rapport (PDF, 2,5 Mo)</a>
```

- Utilisez des icônes pour clarifier
```html
<a href="doc.pdf" download>📄 Télécharger le document (PDF, 1 Mo)</a>
<a href="photo.jpg" download>🖼️ Télécharger l'image (JPG, 500 Ko)</a>
```

### 5. Liens email (mailto)

Le protocole `mailto:` ouvre le client email par défaut de l'utilisateur.

**Simple :**
```html
<a href="mailto:contact@exemple.com">Envoyez-nous un email</a>
```

**Avec sujet et corps du message :**
```html
<a href="mailto:contact@exemple.com?subject=Demande d'information&body=Bonjour,%0AJe souhaite...">
    Nous contacter
</a>
```

**Paramètres disponibles :**
- `subject` : Sujet du message
- `body` : Corps du message
- `cc` : Copie carbone
- `bcc` : Copie carbone invisible

**Exemple complet :**
```html
<a href="mailto:support@exemple.com?subject=Support technique&cc=admin@exemple.com&body=Bonjour,%0A%0AJe rencontre un problème...">
    Contacter le support
</a>
```

**Note :** `%0A` représente un retour à la ligne dans l'URL.

**Alternative moderne :**
De nombreux sites préfèrent maintenant utiliser un formulaire de contact plutôt que `mailto:` pour éviter le spam et avoir plus de contrôle.

### 6. Liens téléphone (tel)

Le protocole `tel:` permet d'appeler directement sur mobile.

```html
<a href="tel:+33123456789">01 23 45 67 89</a>
<a href="tel:+33123456789">Appelez-nous</a>
```

**Format international :**
Utilisez toujours le format international avec le code pays (+33 pour la France).

```html
<!-- ✅ Bon : format international -->
<a href="tel:+33123456789">01 23 45 67 89</a>

<!-- ❌ Moins bon : format local -->
<a href="tel:0123456789">01 23 45 67 89</a>
```

### 7. Liens SMS

Le protocole `sms:` ouvre l'application de messagerie avec un numéro prérempli.

```html
<!-- Simple -->
<a href="sms:+33612345678">Envoyez un SMS</a>

<!-- Avec message prérempli (iOS uniquement) -->
<a href="sms:+33612345678&body=Bonjour">Envoyez-nous un message</a>
```

## Les attributs importants

### `target` : Contrôler l'ouverture du lien

L'attribut `target` définit **où** le lien s'ouvre.

**Valeurs possibles :**

**`target="_self"`** (par défaut)
```html
<a href="page.html" target="_self">Ouvrir dans l'onglet actuel</a>
```
Le lien s'ouvre dans le même onglet (comportement par défaut, pas besoin de le préciser).

**`target="_blank"`**
```html
<a href="https://www.exemple.com" target="_blank">Ouvrir dans un nouvel onglet</a>
```
Le lien s'ouvre dans un **nouvel onglet** (ou nouvelle fenêtre selon le navigateur).

**⚠️ Important pour la sécurité :**
Avec `target="_blank"`, ajoutez **toujours** `rel="noopener"` pour des raisons de sécurité :

```html
<a href="https://www.exemple.com" target="_blank" rel="noopener">
    Site externe
</a>
```

**Pourquoi ?** Sans `noopener`, la page externe peut potentiellement manipuler votre page d'origine (attaque de type "tabnabbing").

**Autres valeurs (moins courantes) :**
- `target="_parent"` : Ouvre dans le cadre parent
- `target="_top"` : Ouvre dans la fenêtre complète

### `rel` : Relation avec la page liée

L'attribut `rel` définit la **relation** entre la page actuelle et la page liée.

**`rel="noopener"` (sécurité)**
```html
<a href="https://externe.com" target="_blank" rel="noopener">
    Lien externe sûr
</a>
```
Empêche la page externe d'accéder à votre page.

**`rel="noreferrer"` (confidentialité)**
```html
<a href="https://externe.com" target="_blank" rel="noopener noreferrer">
    Lien anonyme
</a>
```
Ne transmet pas d'informations sur la page d'origine (pas de "Referrer" dans les statistiques du site externe).

**`rel="nofollow"` (SEO)**
```html
<a href="https://spam-site.com" rel="nofollow">
    Lien non approuvé
</a>
```
Indique aux moteurs de recherche de ne pas suivre ce lien (n'affecte pas le classement de la page liée). Utilisé pour :
- Les liens payants/publicités
- Les liens utilisateurs (commentaires, forums)
- Les liens vers des sites non fiables

**`rel="sponsored"` (SEO - liens payants)**
```html
<a href="https://partenaire.com" rel="sponsored">
    Lien sponsorisé
</a>
```
Indique que c'est un lien commercial/payant.

**`rel="ugc"` (SEO - contenu utilisateur)**
```html
<a href="https://site-utilisateur.com" rel="ugc">
    Site recommandé par un utilisateur
</a>
```
"User Generated Content" - pour les liens créés par les utilisateurs.

**Combinaison recommandée pour liens externes :**
```html
<a href="https://externe.com" target="_blank" rel="noopener noreferrer">
    Lien externe sécurisé
</a>
```

### `title` : Info-bulle

L'attribut `title` affiche une info-bulle au survol.

```html
<a href="contact.html" title="Envoyez-nous un message">Contact</a>
```

**⚠️ Attention :**
- L'info-bulle n'apparaît **pas sur mobile**
- Ne mettez **jamais** d'informations essentielles dans le `title`
- Les lecteurs d'écran peuvent ou non lire le `title`

**Utilisez `title` pour :**
- Des informations **supplémentaires** (non essentielles)
- Préciser la destination d'un lien court
```html
<a href="https://mdn.dev" title="Mozilla Developer Network">MDN</a>
```

### `hreflang` : Langue de la page cible

Indique la langue de la page de destination.

```html
<a href="/en/about" hreflang="en">About us</a>
<a href="/fr/a-propos" hreflang="fr">À propos</a>
<a href="/es/acerca-de" hreflang="es">Acerca de</a>
```

**Utilité :**
- Aide les moteurs de recherche
- Les navigateurs peuvent proposer la traduction
- Améliore l'accessibilité

## Créer des menus de navigation

### Menu horizontal simple

```html
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services">Services</a></li>
        <li><a href="/portfolio">Portfolio</a></li>
        <li><a href="/blog">Blog</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

**Avec CSS de base (aperçu) :**
```html
<style>
nav ul {
    list-style: none;
    display: flex;
    gap: 20px;
}
</style>
```

### Menu avec page active

Indiquez visuellement la page actuelle :

```html
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services" class="active">Services</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

Ou avec `aria-current` (meilleur pour l'accessibilité) :

```html
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services" aria-current="page">Services</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

### Menu avec sous-menu (dropdown)

```html
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li>
            <a href="/services">Services</a>
            <ul>
                <li><a href="/services/web">Développement web</a></li>
                <li><a href="/services/mobile">Applications mobiles</a></li>
                <li><a href="/services/seo">Référencement SEO</a></li>
            </ul>
        </li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

### Fil d'Ariane (Breadcrumb)

Le fil d'Ariane montre le chemin de navigation actuel :

```html
<nav aria-label="Fil d'Ariane">
    <ol>
        <li><a href="/">Accueil</a></li>
        <li><a href="/produits">Produits</a></li>
        <li><a href="/produits/ordinateurs">Ordinateurs</a></li>
        <li aria-current="page">MacBook Pro</li>
    </ol>
</nav>
```

**Avec séparateurs visuels (CSS) :**
```html
<nav aria-label="Fil d'Ariane">
    <ol>
        <li><a href="/">Accueil</a> &gt;</li>
        <li><a href="/produits">Produits</a> &gt;</li>
        <li><a href="/produits/ordinateurs">Ordinateurs</a> &gt;</li>
        <li>MacBook Pro</li>
    </ol>
</nav>
```

### Pagination

Navigation entre plusieurs pages de résultats :

```html
<nav aria-label="Pagination">
    <ul>
        <li><a href="/page/1" aria-label="Page précédente">« Précédent</a></li>
        <li><a href="/page/1">1</a></li>
        <li><a href="/page/2" aria-current="page">2</a></li>
        <li><a href="/page/3">3</a></li>
        <li><a href="/page/4">4</a></li>
        <li><a href="/page/5">5</a></li>
        <li><a href="/page/3" aria-label="Page suivante">Suivant »</a></li>
    </ul>
</nav>
```

## Styles de liens et états

### Les pseudo-classes CSS pour les liens

Les liens ont plusieurs **états** que vous pouvez styler avec CSS :

```css
/* Lien non visité */
a:link {
    color: blue;
}

/* Lien visité */
a:visited {
    color: purple;
}

/* Lien au survol */
a:hover {
    color: red;
    text-decoration: underline;
}

/* Lien actif (au moment du clic) */
a:active {
    color: orange;
}

/* Lien avec focus (navigation au clavier) */
a:focus {
    outline: 2px solid orange;
}
```

**Ordre important : LVHFA**
Mémorisez **LoVe HAte** (ou **L**ord **V**ader's **H**andle **A**ppeared **F**irst) :
1. **L**ink (`:link`)
2. **V**isited (`:visited`)
3. **H**over (`:hover`)
4. **F**ocus (`:focus`)
5. **A**ctive (`:active`)

### Retirer le soulignement

Par défaut, les liens sont soulignés. Vous pouvez le retirer avec CSS :

```css
a {
    text-decoration: none;
}

/* Mais ajoutez le soulignement au survol pour l'accessibilité */
a:hover {
    text-decoration: underline;
}
```

**⚠️ Attention :** Si vous retirez le soulignement, assurez-vous que les liens restent **visuellement distincts** du texte normal (couleur différente, par exemple).

## Accessibilité des liens

### Texte de lien descriptif

✅ **Bon - Descriptif hors contexte :**
```html
<a href="/guide.pdf">Télécharger le guide du débutant (PDF, 2 Mo)</a>
<a href="/inscription">S'inscrire à la newsletter</a>
<a href="/contact">Contactez notre équipe support</a>
```

❌ **Mauvais - Vague ou non descriptif :**
```html
<a href="/guide.pdf">Cliquez ici</a>
<a href="/inscription">Ici</a>
<a href="/contact">En savoir plus</a>
```

**Pourquoi c'est important ?**
Les utilisateurs de lecteurs d'écran peuvent naviguer de lien en lien. Si tous les liens disent "cliquez ici", c'est inutilisable !

### Liens d'images

Si une image est un lien, l'attribut `alt` devient le texte du lien :

```html
<a href="/">
    <img src="logo.png" alt="Retour à l'accueil">
</a>
```

**❌ Mauvais :**
```html
<a href="/">
    <img src="logo.png" alt="Logo">  <!-- Pas descriptif ! -->
</a>
```

### Liens qui s'ouvrent dans un nouvel onglet

Prévenez l'utilisateur quand un lien s'ouvre dans un nouvel onglet :

```html
<a href="https://externe.com" target="_blank" rel="noopener">
    Site externe <span aria-label="(s'ouvre dans un nouvel onglet)">(nouvel onglet)</span>
</a>
```

**Ou avec une icône :**
```html
<a href="https://externe.com" target="_blank" rel="noopener">
    Site externe <span aria-label="Lien externe s'ouvrant dans un nouvel onglet">🔗</span>
</a>
```

### Focus visible

Le contour de focus (outline) est **essentiel** pour la navigation au clavier. **Ne le supprimez jamais** sans le remplacer !

❌ **Très mauvais :**
```css
a:focus {
    outline: none;  /* Rend la navigation au clavier impossible ! */
}
```

✅ **Bon :**
```css
a:focus {
    outline: 3px solid orange;
    outline-offset: 2px;
}
```

### Éviter les liens ambigus

✅ **Bon :**
```html
<p>Pour plus d'informations sur nos services, <a href="/services">consultez notre page dédiée</a>.</p>
```

❌ **Ambigu :**
```html
<p>Pour plus d'informations, cliquez <a href="/services">ici</a>.</p>
```

## Bonnes pratiques SEO

### Texte d'ancrage (anchor text)

Le texte du lien est utilisé par Google pour comprendre le contenu de la page de destination.

✅ **Bon pour le SEO :**
```html
<a href="/formation-html-css">Formation complète HTML et CSS pour débutants</a>
```

❌ **Peu informatif :**
```html
<a href="/formation-html-css">Cliquez ici</a>
```

### Liens internes pour le maillage

Créez des liens entre vos propres pages (maillage interne) :

```html
<article>
    <h2>Introduction à HTML5</h2>
    <p>HTML5 apporte de nouvelles balises sémantiques. Pour en savoir plus sur les
    <a href="/article/balises-semantiques">balises sémantiques HTML5</a>, consultez notre
    guide complet.</p>

    <p>Une fois HTML maîtrisé, vous pourrez passer à
    <a href="/article/apprendre-css">l'apprentissage de CSS</a>.</p>
</article>
```

**Avantages :**
- Aide Google à comprendre la structure de votre site
- Améliore l'expérience utilisateur (navigation facilitée)
- Distribue le "jus de lien" (link juice) sur votre site

### Éviter les liens cassés

Les liens qui ne fonctionnent plus (erreur 404) nuisent au SEO et à l'expérience utilisateur.

**Vérifiez régulièrement :**
- Utilisez des outils comme "Dead Link Checker"
- Testez manuellement les liens importants
- Mettez à jour ou supprimez les liens obsolètes

## Erreurs courantes à éviter

### Erreur 1 : Oublier l'attribut `href`

❌ **Mauvais (pas un vrai lien) :**
```html
<a>Cliquez ici</a>
```

✅ **Bon :**
```html
<a href="/page">Cliquez ici</a>
```

### Erreur 2 : Utiliser `href="#"` sans raison

❌ **Mauvais (crée un comportement bizarre) :**
```html
<a href="#">Cliquez ici</a>
```

Si vous n'avez pas encore de destination, utilisez `href="#"` avec JavaScript pour empêcher le comportement par défaut, ou mieux, utilisez un `<button>`.

✅ **Bon :**
```html
<button onclick="faireQuelqueChose()">Cliquez ici</button>
```

### Erreur 3 : Imbriquer des liens

❌ **Invalide (on ne peut pas mettre un lien dans un lien) :**
```html
<a href="/page1">
    Ceci est un lien vers la page 1
    <a href="/page2">et ceci vers la page 2</a>
</a>
```

✅ **Bon (liens séparés) :**
```html
<a href="/page1">Lien vers la page 1</a>
<a href="/page2">Lien vers la page 2</a>
```

### Erreur 4 : Liens sans contenu

❌ **Mauvais (lien vide) :**
```html
<a href="/page"></a>
```

✅ **Bon (contenu descriptif) :**
```html
<a href="/page">Aller à la page</a>
```

### Erreur 5 : Utiliser `javascript:void(0)`

❌ **Mauvais (obsolète et non accessible) :**
```html
<a href="javascript:void(0)" onclick="faireQuelqueChose()">Action</a>
```

✅ **Bon (utilisez un bouton pour les actions) :**
```html
<button onclick="faireQuelqueChose()">Action</button>
```

**Règle :** Les liens (`<a>`) sont pour la **navigation**, les boutons (`<button>`) sont pour les **actions**.

### Erreur 6 : URLs mal formées

❌ **Mauvais :**
```html
<a href="www.exemple.com">Lien</a>  <!-- Manque le protocole -->
<a href="exemple.com">Lien</a>       <!-- Manque le protocole -->
```

✅ **Bon :**
```html
<a href="https://www.exemple.com">Lien</a>
```

## Exemples pratiques complets

### Exemple 1 : Menu de navigation complet

```html
<header>
    <nav aria-label="Navigation principale">
        <ul>
            <li><a href="/" aria-current="page">Accueil</a></li>
            <li>
                <a href="/services">Services</a>
                <ul>
                    <li><a href="/services/web">Développement web</a></li>
                    <li><a href="/services/mobile">Applications mobiles</a></li>
                    <li><a href="/services/consulting">Consulting</a></li>
                </ul>
            </li>
            <li><a href="/portfolio">Portfolio</a></li>
            <li><a href="/blog">Blog</a></li>
            <li><a href="/contact">Contact</a></li>
        </ul>
    </nav>
</header>
```

### Exemple 2 : Pied de page avec liens multiples

```html
<footer>
    <div class="footer-content">
        <section>
            <h3>Navigation</h3>
            <nav aria-label="Liens de bas de page">
                <ul>
                    <li><a href="/">Accueil</a></li>
                    <li><a href="/about">À propos</a></li>
                    <li><a href="/services">Services</a></li>
                    <li><a href="/contact">Contact</a></li>
                </ul>
            </nav>
        </section>

        <section>
            <h3>Légal</h3>
            <ul>
                <li><a href="/mentions-legales">Mentions légales</a></li>
                <li><a href="/politique-confidentialite">Politique de confidentialité</a></li>
                <li><a href="/cgv">CGV</a></li>
                <li><a href="/cookies">Gestion des cookies</a></li>
            </ul>
        </section>

        <section>
            <h3>Suivez-nous</h3>
            <ul>
                <li><a href="https://facebook.com/..." target="_blank" rel="noopener">Facebook</a></li>
                <li><a href="https://twitter.com/..." target="_blank" rel="noopener">Twitter</a></li>
                <li><a href="https://linkedin.com/..." target="_blank" rel="noopener">LinkedIn</a></li>
                <li><a href="https://instagram.com/..." target="_blank" rel="noopener">Instagram</a></li>
            </ul>
        </section>

        <section>
            <h3>Contact</h3>
            <ul>
                <li><a href="tel:+33123456789">01 23 45 67 89</a></li>
                <li><a href="mailto:contact@exemple.com">contact@exemple.com</a></li>
                <li><a href="/contact">Formulaire de contact</a></li>
            </ul>
        </section>
    </div>

    <p>&copy; 2025 Mon Entreprise. Tous droits réservés.</p>
</footer>
```

### Exemple 3 : Article de blog avec liens internes

```html
<article>
    <header>
        <h1>Guide complet du HTML5</h1>
        <p>Publié le <time datetime="2025-01-15">15 janvier 2025</time></p>
    </header>

    <!-- Table des matières -->
    <nav aria-label="Table des matières">
        <h2>Sommaire</h2>
        <ol>
            <li><a href="#introduction">Introduction</a></li>
            <li><a href="#structure">Structure de base</a></li>
            <li><a href="#elements">Éléments sémantiques</a></li>
            <li><a href="#formulaires">Formulaires</a></li>
            <li><a href="#conclusion">Conclusion</a></li>
        </ol>
    </nav>

    <section id="introduction">
        <h2>Introduction</h2>
        <p>HTML5 est la dernière version du langage HTML. Pour comprendre les bases,
        consultez notre <a href="/tutoriel/html-bases">tutoriel HTML pour débutants</a>.</p>
    </section>

    <section id="structure">
        <h2>Structure de base</h2>
        <p>Un document HTML5 commence toujours par un DOCTYPE. Si vous débutez,
        lisez d'abord notre article sur
        <a href="/article/structure-html">la structure d'un document HTML</a>.</p>
    </section>

    <section id="elements">
        <h2>Éléments sémantiques</h2>
        <p>HTML5 introduit de nouvelles balises comme &lt;header&gt;, &lt;nav&gt;, et &lt;article&gt;.
        Pour aller plus loin, consultez notre
        <a href="/guide/balises-semantiques">guide complet des balises sémantiques</a>.</p>
    </section>

    <section id="formulaires">
        <h2>Formulaires</h2>
        <p>Les formulaires HTML5 offrent de nouveaux types d'input. Découvrez comment les utiliser
        dans notre <a href="/tutoriel/formulaires-html5">tutoriel sur les formulaires</a>.</p>
    </section>

    <section id="conclusion">
        <h2>Conclusion</h2>
        <p>Une fois HTML5 maîtrisé, la prochaine étape est d'apprendre CSS pour styliser vos pages.
        Commencez avec notre <a href="/tutoriel/css-debutants">guide CSS pour débutants</a>.</p>

        <p><a href="#top">↑ Retour en haut</a></p>
    </section>

    <footer>
        <p>Articles connexes :</p>
        <ul>
            <li><a href="/article/css-bases">Les bases de CSS</a></li>
            <li><a href="/article/javascript-intro">Introduction à JavaScript</a></li>
            <li><a href="/article/responsive-design">Le responsive design</a></li>
        </ul>
    </footer>
</article>
```

### Exemple 4 : Page de contact

```html
<main>
    <h1>Contactez-nous</h1>

    <section>
        <h2>Plusieurs façons de nous joindre</h2>

        <div class="contact-methods">
            <div class="method">
                <h3>Par téléphone</h3>
                <p><a href="tel:+33123456789">01 23 45 67 89</a></p>
                <p>Du lundi au vendredi, 9h-18h</p>
            </div>

            <div class="method">
                <h3>Par email</h3>
                <p><a href="mailto:contact@exemple.com">contact@exemple.com</a></p>
                <p>Réponse sous 24h ouvrées</p>
            </div>

            <div class="method">
                <h3>Par courrier</h3>
                <address>
                    Mon Entreprise<br>
                    123 Rue de la Paix<br>
                    75001 Paris<br>
                    France
                </address>
                <p><a href="https://maps.google.com/?q=123+Rue+de+la+Paix+Paris"
                      target="_blank" rel="noopener">
                    Voir sur Google Maps 🗺️
                </a></p>
            </div>

            <div class="method">
                <h3>Par formulaire</h3>
                <p><a href="/formulaire-contact">Remplir le formulaire de contact</a></p>
                <p>Réponse garantie sous 48h</p>
            </div>
        </div>
    </section>

    <section>
        <h2>Support technique</h2>
        <p>Pour toute question technique, contactez notre équipe support :</p>
        <ul>
            <li>Email : <a href="mailto:support@exemple.com">support@exemple.com</a></li>
            <li>Téléphone : <a href="tel:+33123456790">01 23 45 67 90</a></li>
            <li><a href="/faq">Consultez notre FAQ</a></li>
            <li><a href="/documentation">Documentation technique</a></li>
        </ul>
    </section>

    <section>
        <h2>Réseaux sociaux</h2>
        <p>Suivez-nous et discutez avec notre communauté :</p>
        <ul>
            <li><a href="https://facebook.com/..." target="_blank" rel="noopener">Facebook</a></li>
            <li><a href="https://twitter.com/..." target="_blank" rel="noopener">Twitter</a></li>
            <li><a href="https://linkedin.com/..." target="_blank" rel="noopener">LinkedIn</a></li>
        </ul>
    </section>
</main>
```

## Checklist des bonnes pratiques

Avant de publier votre page, vérifiez :

### Qualité des liens
- [ ] Tous les liens ont un attribut `href` valide
- [ ] Le texte des liens est descriptif (pas de "cliquez ici")
- [ ] Les liens externes ont `target="_blank"` et `rel="noopener"` si nécessaire
- [ ] Les liens de téléchargement indiquent le format et la taille
- [ ] Les liens email et téléphone utilisent les bons protocoles

### Accessibilité
- [ ] Les liens sont visuellement distincts du texte
- [ ] Le focus est visible (outline présent)
- [ ] Les liens d'images ont un `alt` descriptif
- [ ] Les liens dans un nouvel onglet sont signalés
- [ ] Pas de liens vides ou sans texte

### SEO
- [ ] Les liens internes créent un bon maillage
- [ ] Le texte d'ancrage est pertinent
- [ ] Pas de liens cassés (404)
- [ ] Les liens externes non fiables ont `rel="nofollow"`

### Structure
- [ ] La navigation principale utilise `<nav>`
- [ ] Les menus sont dans des listes `<ul>` ou `<ol>`
- [ ] La page active est indiquée (`aria-current="page"`)
- [ ] Pas de liens imbriqués

## Conclusion

Les liens hypertextes sont **l'essence du web**. Ils transforment des pages isolées en un réseau interconnecté d'informations. Un bon usage des liens améliore :

- **L'expérience utilisateur** : Navigation fluide et intuitive
- **L'accessibilité** : Liens compréhensibles pour tous
- **Le SEO** : Meilleur référencement et indexation
- **La sécurité** : Protection contre les vulnérabilités

**Points clés à retenir :**

| Élément | Usage |
|---------|-------|
| `<a href="url">` | Créer un lien |
| `target="_blank"` | Ouvrir dans un nouvel onglet |
| `rel="noopener"` | Sécurité pour les liens externes |
| `href="#id"` | Lien vers une ancre |
| `download` | Forcer le téléchargement |
| `mailto:` | Lien email |
| `tel:` | Lien téléphone |

**Principes fondamentaux :**
1. **Texte descriptif** : Chaque lien doit être compréhensible hors contexte
2. **Sécurité** : Utilisez `rel="noopener"` avec `target="_blank"`
3. **Accessibilité** : Focus visible et navigation au clavier fonctionnelle
4. **SEO** : Maillage interne et textes d'ancrage pertinents

Maîtriser les liens, c'est maîtriser la navigation web. Avec ces connaissances, vous pouvez créer des sites web intuitifs, accessibles et bien référencés.

Dans la prochaine section, nous découvrirons les conteneurs génériques `<div>` et `<span>`, et comment les utiliser intelligemment en complément des éléments sémantiques.

---


**Section suivante** : [3.2.5 Conteneurs génériques : div et span](./05-conteneurs-generiques.md)

⏭️ [Conteneurs génériques : div et span](/03-html5-structure-et-semantique/02-elements-structurants/05-conteneurs-generiques.md)
