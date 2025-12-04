🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.5.5 - Images responsives

## Introduction

Les images représentent souvent la plus grande part du poids d'une page web. Sur mobile, charger une image de 3000px de large prévue pour un écran 4K est un gaspillage de bande passante et de batterie. Les **images responsives** permettent d'afficher l'image appropriée selon l'appareil, la taille d'écran et la résolution.

Une image responsive, c'est :
- Une image qui s'adapte à la taille de son conteneur
- Qui charge la bonne résolution selon l'écran
- Qui ne déborde jamais et ne déforme pas

## La base : rendre une image flexible

### Le problème des images fixes

Sans CSS, une image garde sa taille d'origine :

```html
<img src="photo.jpg" alt="Photo de paysage">
<!-- Si photo.jpg fait 2000px de large, elle déborde sur mobile ! -->
```

**Résultat sur un smartphone de 375px de large :** L'image dépasse, crée un scroll horizontal → mauvaise expérience utilisateur.

### La solution simple et essentielle

```css
img {
    max-width: 100%; /* L'image ne dépasse jamais son conteneur */
    height: auto;    /* Conserve les proportions originales */
}
```

**Ce que ça fait :**
- `max-width: 100%` : L'image ne fera jamais plus large que son conteneur
- `height: auto` : La hauteur s'ajuste automatiquement pour garder les bonnes proportions

**Exemple :**
```html
<div class="conteneur" style="width: 300px;">
    <img src="photo.jpg" alt="Photo">
    <!-- Photo de 2000px affichée à 300px, sans déformation -->
</div>
```

### CSS recommandé pour toutes les images

```css
/* À mettre dans votre CSS de base */
img {
    max-width: 100%;
    height: auto;
    display: block; /* Évite l'espace blanc en dessous */
}
```

**💡 Conseil :** Ajoutez ce CSS au début de votre projet, toutes vos images seront automatiquement responsives !

## Comprendre le problème de performance

### Le gaspillage de bande passante

Imaginez cette situation :

```html
<img src="photo-4k.jpg" alt="Photo">
<!-- photo-4k.jpg : 3840px × 2160px, 2.5 Mo -->
```

**Sur un smartphone :**
- L'écran fait 375px de large
- L'utilisateur télécharge 2.5 Mo
- Mais l'image s'affiche à 375px de large
- Les 3465px restants sont inutiles !

**Conséquences :**
- ❌ Temps de chargement long
- ❌ Consommation de données mobiles
- ❌ Batterie drainée
- ❌ Mauvaise expérience utilisateur

### La solution : différentes versions d'images

L'idéal est d'avoir plusieurs versions de la même image :

```
photo-small.jpg   (500px de large, 80 Ko)   → Pour mobile
photo-medium.jpg  (1000px de large, 200 Ko) → Pour tablette
photo-large.jpg   (2000px de large, 500 Ko) → Pour desktop
photo-xlarge.jpg  (3000px de large, 1 Mo)   → Pour grands écrans
```

**Maintenant, comment dire au navigateur de charger la bonne version ?**

## L'attribut srcset (Résolution switching)

### Principe de base

**srcset** permet de fournir plusieurs versions d'une image et de laisser le navigateur choisir la meilleure.

```html
<img
    src="photo-small.jpg"
    srcset="photo-small.jpg 500w,
            photo-medium.jpg 1000w,
            photo-large.jpg 2000w"
    alt="Photo de paysage">
```

**Explication :**
- `src` : image par défaut (pour les vieux navigateurs)
- `srcset` : liste des images disponibles
- `500w`, `1000w`, `2000w` : largeur réelle de chaque image en pixels (le "w" signifie "width")

**Comment le navigateur choisit :**
- Sur mobile 375px : charge `photo-small.jpg` (500w)
- Sur tablette 768px : charge `photo-medium.jpg` (1000w)
- Sur desktop 1920px : charge `photo-large.jpg` (2000w)

### Avec densité de pixels (écrans Retina)

Les écrans modernes ont souvent une densité de pixels élevée (Retina, 2×, 3×).

```html
<img
    src="logo.png"
    srcset="logo.png 1x,
            logo@2x.png 2x,
            logo@3x.png 3x"
    alt="Logo">
```

**Explication :**
- `1x` : écrans normaux
- `2x` : écrans Retina (iPhone, MacBook Pro, etc.)
- `3x` : écrans haute densité (certains smartphones Android)

**Usage typique :** Pour les logos, icônes, petites images décoratives.

## L'attribut sizes

### Le problème

Avec `srcset` seul, le navigateur ne sait pas quelle taille l'image aura sur la page. Il devine, mais ce n'est pas optimal.

**Exemple :**
```html
<!-- Le navigateur ne sait pas que l'image ne fera que 50% de la largeur ! -->
<img srcset="photo-500.jpg 500w, photo-1000.jpg 1000w"
     style="width: 50%;">
```

### La solution : sizes

**sizes** dit au navigateur : "Voici la taille que l'image aura dans la page".

```html
<img
    src="photo-small.jpg"
    srcset="photo-small.jpg 500w,
            photo-medium.jpg 1000w,
            photo-large.jpg 2000w"
    sizes="(max-width: 768px) 100vw,
           (max-width: 1200px) 50vw,
           800px"
    alt="Photo">
```

**Explication :**

| Condition | Taille de l'image dans la page |
|-----------|-------------------------------|
| `(max-width: 768px)` | `100vw` (100% de la largeur du viewport) |
| `(max-width: 1200px)` | `50vw` (50% de la largeur du viewport) |
| Par défaut | `800px` (taille fixe) |

**Comment le navigateur choisit :**

1. Sur mobile (375px) :
   - Condition `max-width: 768px` est vraie
   - Taille = `100vw` = 375px
   - Charge l'image la plus proche : `photo-small.jpg` (500w)

2. Sur tablette (900px) :
   - Condition `max-width: 1200px` est vraie
   - Taille = `50vw` = 450px
   - Charge `photo-small.jpg` (500w)

3. Sur desktop (1920px) :
   - Aucune condition ne s'applique
   - Taille = `800px`
   - Charge `photo-medium.jpg` (1000w)

### Syntaxe sizes

```html
sizes="(condition-media-query) taille-image,
       (autre-condition) autre-taille,
       taille-par-defaut"
```

**Unités possibles :**
- `100vw` : 100% de la largeur du viewport
- `50vw` : 50% de la largeur du viewport
- `calc(100vw - 40px)` : 100% moins 40px de marges
- `800px` : taille fixe

### Exemple complet et pratique

```html
<!-- Image dans un conteneur qui fait 90% sur mobile, 50% sur desktop -->
<img
    src="photo-fallback.jpg"
    srcset="photo-400.jpg 400w,
            photo-800.jpg 800w,
            photo-1200.jpg 1200w,
            photo-1600.jpg 1600w"
    sizes="(max-width: 768px) 90vw,
           50vw"
    alt="Belle photo de paysage"
    loading="lazy">
```

**Ce qui se passe :**
- Mobile 375px : `90vw` = 338px → charge `photo-400.jpg`
- Tablette 768px : `50vw` = 384px → charge `photo-400.jpg`
- Desktop 1200px : `50vw` = 600px → charge `photo-800.jpg`
- Grand écran 1920px : `50vw` = 960px → charge `photo-1200.jpg`

## L'élément &lt;picture&gt; (Art Direction)

### Quand utiliser &lt;picture&gt; ?

L'élément `<picture>` est plus puissant que `srcset`. Utilisez-le quand vous voulez :

1. **Art direction** : afficher des images différentes (recadrées différemment) selon l'écran
2. **Formats modernes** : servir WebP aux navigateurs compatibles, JPEG en fallback
3. **Contrôle total** : vous choisissez exactement quelle image pour quelle condition

### Exemple 1 : Art direction

Sur mobile, on veut un gros plan. Sur desktop, on veut la vue complète.

```html
<picture>
    <!-- Sur mobile : image portrait recadrée -->
    <source media="(max-width: 768px)" srcset="portrait-mobile.jpg">

    <!-- Sur desktop : image paysage complète -->
    <source media="(min-width: 769px)" srcset="paysage-desktop.jpg">

    <!-- Fallback pour vieux navigateurs -->
    <img src="paysage-desktop.jpg" alt="Paysage magnifique">
</picture>
```

**Résultat :**
- Mobile : affiche `portrait-mobile.jpg` (image différente, recadrée pour mobile)
- Desktop : affiche `paysage-desktop.jpg`

### Exemple 2 : Formats modernes (WebP)

WebP est un format plus léger que JPEG, mais pas supporté par tous les navigateurs.

```html
<picture>
    <!-- Si le navigateur supporte WebP -->
    <source type="image/webp" srcset="photo.webp">

    <!-- Sinon, JPEG classique -->
    <source type="image/jpeg" srcset="photo.jpg">

    <!-- Fallback -->
    <img src="photo.jpg" alt="Photo">
</picture>
```

**Avantage :** WebP est 25-35% plus léger que JPEG à qualité égale !

### Exemple 3 : Combinaison complète

Art direction + formats modernes + srcset :

```html
<picture>
    <!-- Mobile : WebP -->
    <source
        media="(max-width: 768px)"
        type="image/webp"
        srcset="mobile-small.webp 400w, mobile-large.webp 800w"
        sizes="100vw">

    <!-- Mobile : JPEG fallback -->
    <source
        media="(max-width: 768px)"
        type="image/jpeg"
        srcset="mobile-small.jpg 400w, mobile-large.jpg 800w"
        sizes="100vw">

    <!-- Desktop : WebP -->
    <source
        media="(min-width: 769px)"
        type="image/webp"
        srcset="desktop-medium.webp 1000w, desktop-large.webp 2000w"
        sizes="50vw">

    <!-- Desktop : JPEG fallback -->
    <source
        media="(min-width: 769px)"
        type="image/jpeg"
        srcset="desktop-medium.jpg 1000w, desktop-large.jpg 2000w"
        sizes="50vw">

    <!-- Fallback final -->
    <img src="desktop-medium.jpg" alt="Photo">
</picture>
```

**C'est l'approche la plus optimale, mais aussi la plus complexe !**

## Lazy loading (chargement différé) 🆕

### Qu'est-ce que le lazy loading ?

Le **lazy loading** charge les images uniquement quand elles sont sur le point d'être visibles à l'écran.

**Sans lazy loading :**
- Toutes les images de la page se chargent au début
- Ralentit le chargement initial
- Gaspillage si l'utilisateur ne scrolle jamais en bas

**Avec lazy loading :**
- Les images hors écran ne se chargent pas
- Elles se chargent quand l'utilisateur scrolle vers elles
- Chargement initial plus rapide !

### Utilisation (très simple)

```html
<img src="photo.jpg" alt="Photo" loading="lazy">
```

**C'est tout !** L'attribut `loading="lazy"` suffit.

**Valeurs possibles :**
- `loading="lazy"` : chargement différé (recommandé)
- `loading="eager"` : chargement immédiat (par défaut)
- `loading="auto"` : le navigateur décide

### Où l'utiliser ?

```html
<!-- Images en haut de page : chargement normal -->
<img src="hero.jpg" alt="Hero">

<!-- Images plus bas : lazy loading -->
<img src="photo1.jpg" alt="Photo 1" loading="lazy">
<img src="photo2.jpg" alt="Photo 2" loading="lazy">
<img src="photo3.jpg" alt="Photo 3" loading="lazy">
```

**💡 Règle :** N'utilisez PAS `loading="lazy"` pour les images visibles immédiatement (au-dessus de la ligne de flottaison).

### Compatibilité

`loading="lazy"` est supporté par tous les navigateurs modernes (Chrome, Firefox, Safari, Edge). Pour les vieux navigateurs, ça ne fait rien (l'image se charge normalement).

## CSS : object-fit

### Le problème des images déformées

Quand vous imposez des dimensions à une image, elle peut se déformer :

```css
img {
    width: 300px;
    height: 200px; /* L'image risque d'être déformée ! */
}
```

### La solution : object-fit

**object-fit** contrôle comment l'image s'ajuste dans son conteneur.

```css
img {
    width: 300px;
    height: 200px;
    object-fit: cover; /* L'image couvre tout sans déformation */
}
```

### Les valeurs de object-fit

#### cover (le plus utilisé)

```css
.image {
    width: 400px;
    height: 300px;
    object-fit: cover;
}
```

**Comportement :** L'image couvre tout l'espace, quitte à être rognée. Les proportions sont conservées.

**Usage :** Vignettes, galeries photos, cards.

#### contain

```css
.image {
    width: 400px;
    height: 300px;
    object-fit: contain;
}
```

**Comportement :** L'image entière est visible, des bandes vides peuvent apparaître.

**Usage :** Logos, images dont on veut voir l'intégralité.

#### fill (par défaut)

```css
.image {
    width: 400px;
    height: 300px;
    object-fit: fill; /* Déforme l'image */
}
```

**Comportement :** L'image remplit tout l'espace, peut être déformée.

**Usage :** Rarement voulu.

#### none

```css
.image {
    width: 400px;
    height: 300px;
    object-fit: none;
}
```

**Comportement :** L'image garde sa taille originale, centrée.

#### scale-down

```css
.image {
    width: 400px;
    height: 300px;
    object-fit: scale-down;
}
```

**Comportement :** Comme `contain`, mais ne grossit jamais l'image.

### object-position

Contrôle où l'image est positionnée dans son conteneur :

```css
.image {
    width: 400px;
    height: 300px;
    object-fit: cover;
    object-position: top; /* Centre en haut */
}
```

**Valeurs possibles :**
- `center` (par défaut)
- `top`, `bottom`, `left`, `right`
- `top left`, `bottom right`, etc.
- `50% 50%` (personnalisé)

**Exemple pratique : portraits**

```css
.portrait {
    width: 200px;
    height: 300px;
    object-fit: cover;
    object-position: top; /* Garde la tête visible, coupe les pieds */
}
```

## Images de fond responsives (CSS)

### Background-size

Pour les images de fond CSS, utilisez `background-size` :

```css
.hero {
    background-image: url('hero.jpg');
    background-size: cover; /* Couvre tout */
    background-position: center;
    height: 500px;
}
```

**Valeurs de background-size :**

#### cover
```css
background-size: cover;
```
Couvre tout le conteneur, peut rogner l'image.

#### contain
```css
background-size: contain;
```
L'image entière est visible, peut laisser des espaces vides.

#### Dimensions personnalisées
```css
background-size: 50% auto;      /* 50% de largeur, hauteur auto */
background-size: 100% 100%;     /* Étire (déforme) */
background-size: 400px 300px;   /* Taille fixe */
```

### Media queries pour images de fond

```css
.hero {
    /* Image mobile (petite) */
    background-image: url('hero-mobile.jpg');
    background-size: cover;
    background-position: center;
    height: 300px;
}

@media (min-width: 768px) {
    .hero {
        /* Image tablette (moyenne) */
        background-image: url('hero-tablet.jpg');
        height: 400px;
    }
}

@media (min-width: 1024px) {
    .hero {
        /* Image desktop (grande) */
        background-image: url('hero-desktop.jpg');
        height: 600px;
    }
}
```

### image-set() pour images de fond 🆕

Équivalent de `srcset` pour les images CSS :

```css
.element {
    background-image: image-set(
        url('image.jpg') 1x,
        url('image@2x.jpg') 2x,
        url('image@3x.jpg') 3x
    );
}
```

**Avec formats modernes :**

```css
.element {
    background-image: image-set(
        url('image.webp') type('image/webp'),
        url('image.jpg') type('image/jpeg')
    );
}
```

**⚠️ Note :** Support encore partiel dans certains navigateurs, utilisez avec fallback.

## Formats d'images modernes

### Les formats à connaître

| Format | Usage | Avantages | Inconvénients |
|--------|-------|-----------|---------------|
| **JPEG** | Photos | Bonne compression | Pas de transparence |
| **PNG** | Logos, icônes | Transparence | Fichiers lourds |
| **WebP** 🆕 | Tous usages | Léger, qualité | Support partiel (ancien Safari) |
| **AVIF** 🆕 | Photos | Très léger | Support limité |
| **SVG** | Logos, icônes | Vectoriel, léger | Seulement pour graphiques |

### WebP : le meilleur compromis

WebP offre 25-35% de réduction de taille par rapport à JPEG, avec qualité identique.

**Utilisation avec fallback :**

```html
<picture>
    <source type="image/webp" srcset="photo.webp">
    <img src="photo.jpg" alt="Photo">
</picture>
```

### AVIF : le futur

AVIF est encore plus léger que WebP, mais moins supporté.

```html
<picture>
    <source type="image/avif" srcset="photo.avif">
    <source type="image/webp" srcset="photo.webp">
    <img src="photo.jpg" alt="Photo">
</picture>
```

**Support :** Chrome, Firefox récents. Safari depuis 2021.

## Optimisation des images

### 1. Compresser vos images

**Avant de les mettre sur votre site :**
- JPEG : qualité 70-85% (suffisant pour le web)
- PNG : utiliser des outils comme TinyPNG
- WebP : conversion depuis JPEG/PNG

**Outils en ligne :**
- TinyPNG / TinyJPG
- Squoosh (Google)
- ImageOptim (Mac)

### 2. Choisir la bonne taille

Ne téléchargez jamais une image plus grande que nécessaire :

```
Mobile : 500-800px de large max
Tablette : 1000-1200px de large max
Desktop : 1500-2000px de large max
```

### 3. Utiliser le bon format

**Règle simple :**
- Photo → JPEG (ou WebP)
- Logo/icône avec transparence → PNG (ou SVG si vectoriel)
- Illustration simple → SVG

### 4. Lazy loading

```html
<img src="photo.jpg" alt="Photo" loading="lazy">
```

### 5. Dimensionner dans le HTML

Indiquez toujours `width` et `height` pour éviter les sauts de page :

```html
<img src="photo.jpg" alt="Photo" width="800" height="600" loading="lazy">
```

**CSS associé :**
```css
img {
    max-width: 100%;
    height: auto;
}
```

Les attributs `width` et `height` définissent le **ratio**, pas la taille finale affichée !

## Exemples complets

### Exemple 1 : Image simple responsive

```html
<img
    src="photo-800.jpg"
    srcset="photo-400.jpg 400w,
            photo-800.jpg 800w,
            photo-1200.jpg 1200w"
    sizes="(max-width: 768px) 100vw, 800px"
    alt="Belle photo de paysage"
    width="800"
    height="600"
    loading="lazy">
```

```css
img {
    max-width: 100%;
    height: auto;
    display: block;
}
```

### Exemple 2 : Galerie de vignettes

```html
<div class="galerie">
    <img src="thumb1.jpg" alt="Photo 1" loading="lazy">
    <img src="thumb2.jpg" alt="Photo 2" loading="lazy">
    <img src="thumb3.jpg" alt="Photo 3" loading="lazy">
</div>
```

```css
.galerie {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
}

.galerie img {
    width: 100%;
    height: 200px;
    object-fit: cover; /* Toutes les images ont la même hauteur */
    border-radius: 8px;
}
```

### Exemple 3 : Hero section avec image de fond

```html
<section class="hero">
    <h1>Bienvenue</h1>
    <p>Sur mon site magnifique</p>
</section>
```

```css
.hero {
    /* Image mobile */
    background-image: url('hero-mobile.jpg');
    background-size: cover;
    background-position: center;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
    text-align: center;
}

@media (min-width: 768px) {
    .hero {
        /* Image tablette */
        background-image: url('hero-tablet.jpg');
        height: 500px;
    }
}

@media (min-width: 1024px) {
    .hero {
        /* Image desktop */
        background-image: url('hero-desktop.jpg');
        height: 600px;
    }
}
```

### Exemple 4 : Image avec formats modernes

```html
<picture>
    <!-- WebP pour navigateurs modernes -->
    <source
        type="image/webp"
        srcset="photo-400.webp 400w,
                photo-800.webp 800w,
                photo-1200.webp 1200w"
        sizes="(max-width: 768px) 100vw, 50vw">

    <!-- JPEG en fallback -->
    <source
        type="image/jpeg"
        srcset="photo-400.jpg 400w,
                photo-800.jpg 800w,
                photo-1200.jpg 1200w"
        sizes="(max-width: 768px) 100vw, 50vw">

    <!-- Fallback final -->
    <img
        src="photo-800.jpg"
        alt="Photo magnifique"
        width="800"
        height="600"
        loading="lazy">
</picture>
```

## Checklist : Images responsives

**✅ CSS de base :**
```css
img {
    max-width: 100%;
    height: auto;
    display: block;
}
```

**✅ Attributs HTML :**
```html
<img src="..." alt="..." width="..." height="..." loading="lazy">
```

**✅ Plusieurs résolutions (simple) :**
```html
<img srcset="small.jpg 500w, large.jpg 1000w" sizes="...">
```

**✅ Formats modernes (optimal) :**
```html
<picture>
    <source type="image/webp" srcset="photo.webp">
    <img src="photo.jpg" alt="...">
</picture>
```

**✅ Optimisation :**
- Images compressées
- Bonne résolution (pas trop grande)
- Lazy loading sur images hors écran

## Erreurs courantes

### ❌ Erreur 1 : Oublier max-width: 100%

```css
/* MAUVAIS - L'image peut déborder */
img {
    width: auto;
}

/* BON */
img {
    max-width: 100%;
    height: auto;
}
```

### ❌ Erreur 2 : Lazy loading partout

```html
<!-- MAUVAIS - Image hero visible immédiatement -->
<img src="hero.jpg" alt="Hero" loading="lazy">

<!-- BON - Pas de lazy loading pour images visibles -->
<img src="hero.jpg" alt="Hero">
```

### ❌ Erreur 3 : Oublier les attributs width et height

```html
<!-- MAUVAIS - Cause des sauts de page -->
<img src="photo.jpg" alt="Photo">

<!-- BON - Réserve l'espace -->
<img src="photo.jpg" alt="Photo" width="800" height="600">
```

### ❌ Erreur 4 : Images trop grandes

```html
<!-- MAUVAIS - 5 Mo pour une vignette ! -->
<img src="photo-original-5000px.jpg" alt="Vignette" style="width: 200px;">

<!-- BON - Version optimisée -->
<img src="photo-thumbnail-400px.jpg" alt="Vignette" style="max-width: 200px;">
```

## Récapitulatif

Les **images responsives** sont essentielles pour la performance et l'expérience utilisateur.

**Base indispensable (CSS) :**
```css
img {
    max-width: 100%;
    height: auto;
}
```

**Techniques principales :**
- **srcset** : plusieurs résolutions, le navigateur choisit
- **sizes** : indiquer la taille de l'image dans la page
- **&lt;picture&gt;** : art direction et formats modernes
- **loading="lazy"** : chargement différé
- **object-fit** : contrôler l'ajustement dans un conteneur

**Formats modernes :**
- WebP : 25-35% plus léger que JPEG ✅
- AVIF : encore plus léger, support croissant

**Optimisation :**
1. Compresser les images
2. Créer plusieurs résolutions
3. Utiliser WebP avec fallback
4. Ajouter lazy loading
5. Spécifier width et height

---

**📚 Points à retenir :**

- `max-width: 100%; height: auto;` sur toutes les images
- Utilisez **srcset** et **sizes** pour les images adaptatives
- **&lt;picture&gt;** pour art direction et formats modernes
- **loading="lazy"** pour images hors écran
- **WebP** offre le meilleur rapport qualité/poids
- Toujours spécifier **width** et **height**

**🔜 Prochaine étape :**
Dans la section suivante (4.5.6), nous découvrirons l'**approche mobile-first** en détail et comment structurer son CSS de manière moderne et efficace.

**💡 Astuce de pro :**
Utilisez des outils comme Squoosh (squoosh.app) pour optimiser et convertir vos images en WebP facilement. Gagnez 50-70% de poids sans perte de qualité visible !

⏭️ [Approche mobile-first](/04-css3-styles-et-mise-en-page/05-responsive-design/06-approche-mobile-first.md)
