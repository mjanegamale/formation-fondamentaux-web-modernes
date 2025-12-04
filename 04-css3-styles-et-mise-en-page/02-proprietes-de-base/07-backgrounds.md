🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.7 Backgrounds et images de fond

## Introduction

Les propriétés de **background** (arrière-plan) permettent de définir la couleur et les images de fond des éléments HTML. Elles sont essentielles pour créer des designs visuellement attractifs et des interfaces modernes.

CSS offre un contrôle très précis sur les arrière-plans :
- Couleurs unies ou dégradés
- Images de fond avec positionnement et dimensionnement
- Effets de parallaxe
- Arrière-plans multiples superposés

---

## background-color : Couleur de fond

### Qu'est-ce que c'est ?

La propriété `background-color` définit la couleur d'arrière-plan d'un élément.

### Syntaxe

```css
.element {
  background-color: blue;              /* Nom de couleur */
  background-color: #3498DB;           /* Hexadécimal */
  background-color: rgb(52, 152, 219); /* RGB */
  background-color: rgba(52, 152, 219, 0.5); /* RGBA avec transparence */
  background-color: hsl(204, 70%, 53%);      /* HSL */
  background-color: transparent;       /* Transparent (défaut) */
}
```

### Exemples pratiques

```css
/* Fond coloré simple */
.header {
  background-color: #2C3E50;
  color: white;
  padding: 20px;
}

/* Fond semi-transparent */
.overlay {
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 40px;
}

/* Fond blanc pour contraste */
.card {
  background-color: white;
  border: 1px solid #ddd;
  padding: 20px;
}

/* Fond coloré au survol */
.button {
  background-color: #3498DB;
  color: white;
  padding: 10px 20px;
  border: none;
}

.button:hover {
  background-color: #2980B9;
}
```

### Valeur par défaut

```css
/* Transparent par défaut */
.element {
  background-color: transparent;
  /* L'arrière-plan du parent est visible */
}
```

---

## background-image : Image de fond

### Qu'est-ce que c'est ?

La propriété `background-image` permet de définir une ou plusieurs images comme arrière-plan d'un élément.

### Syntaxe

```css
.element {
  background-image: url('chemin/vers/image.jpg');
}
```

**Important** : Le chemin peut être :
- **Relatif** : `url('images/photo.jpg')` ou `url('../images/photo.jpg')`
- **Absolu** : `url('/images/photo.jpg')`
- **URL complète** : `url('https://exemple.com/image.jpg')`

### Exemples pratiques

```css
/* Image de fond simple */
.hero {
  background-image: url('hero-image.jpg');
  height: 500px;
  color: white;
}

/* Image locale */
.section {
  background-image: url('../images/background.jpg');
}

/* Image externe */
.banner {
  background-image: url('https://exemple.com/banner.jpg');
}

/* Pas d'image (retirer l'image) */
.element {
  background-image: none;
}
```

### Important : Chemin des fichiers

```css
/* Si votre CSS est dans css/style.css
   et votre image dans images/photo.jpg */

/* ❌ Mauvais chemin */
.element {
  background-image: url('images/photo.jpg');
  /* Cherche dans css/images/photo.jpg */
}

/* ✅ Bon chemin */
.element {
  background-image: url('../images/photo.jpg');
  /* Remonte d'un niveau, puis va dans images/ */
}
```

---

## background-repeat : Répétition de l'image

### Qu'est-ce que c'est ?

Par défaut, une image de fond se répète pour remplir tout l'élément. `background-repeat` contrôle ce comportement.

### Valeurs

```css
/* Répète horizontalement et verticalement (défaut) */
.element {
  background-repeat: repeat;
}

/* Ne répète pas */
.element {
  background-repeat: no-repeat;
}

/* Répète horizontalement seulement */
.element {
  background-repeat: repeat-x;
}

/* Répète verticalement seulement */
.element {
  background-repeat: repeat-y;
}

/* Répète pour remplir sans couper les images */
.element {
  background-repeat: space;  /* Ajoute de l'espace entre les répétitions */
}

/* Répète et étire légèrement pour éviter les coupures */
.element {
  background-repeat: round;
}
```

### Visualisation

```css
/* repeat (défaut) */
.repeat {
  background-image: url('pattern.png');
  background-repeat: repeat;
}
/* Résultat : l'image se répète partout comme un motif */

/* no-repeat */
.no-repeat {
  background-image: url('logo.png');
  background-repeat: no-repeat;
}
/* Résultat : l'image apparaît une seule fois */

/* repeat-x */
.repeat-x {
  background-image: url('border.png');
  background-repeat: repeat-x;
}
/* Résultat : l'image se répète horizontalement seulement */
```

### Exemples pratiques

```css
/* Image de héros unique */
.hero {
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
  height: 600px;
}

/* Motif répétitif */
.pattern-bg {
  background-image: url('pattern.png');
  background-repeat: repeat;
}

/* Bordure en haut qui se répète */
.header-border {
  background-image: url('border-pattern.png');
  background-repeat: repeat-x;
  background-position: top;
}
```

---

## background-position : Position de l'image

### Qu'est-ce que c'est ?

`background-position` définit où l'image de fond est placée dans l'élément.

### Valeurs avec mots-clés

```css
/* Mots-clés horizontaux : left, center, right */
/* Mots-clés verticaux : top, center, bottom */

.element {
  background-position: left top;      /* Coin supérieur gauche (défaut) */
  background-position: center center; /* Centre */
  background-position: right bottom;  /* Coin inférieur droit */
  background-position: center top;    /* Centré en haut */
  background-position: left center;   /* Gauche et centré verticalement */
}

/* Syntaxe courte */
.element {
  background-position: center;  /* Équivaut à center center */
  background-position: top;     /* Équivaut à center top */
  background-position: right;   /* Équivaut à right center */
}
```

### Valeurs numériques

```css
/* Pixels */
.element {
  background-position: 20px 50px;  /* 20px de la gauche, 50px du haut */
}

/* Pourcentages */
.element {
  background-position: 50% 50%;    /* Centre parfait */
  background-position: 100% 100%;  /* Coin inférieur droit */
  background-position: 0% 0%;      /* Coin supérieur gauche */
}

/* Mélange */
.element {
  background-position: left 20px; /* Gauche, 20px du haut */
  background-position: center 80%; /* Centré horizontalement, 80% du haut */
}
```

### Comment fonctionnent les pourcentages ?

Les pourcentages sont calculés de façon particulière :

```css
.element {
  background-position: 50% 50%;
}
```

**Signification** :
- Le point à 50% de l'image est aligné avec le point à 50% de l'élément
- Résultat : l'image est parfaitement centrée

```css
.element {
  background-position: 100% 100%;
}
```

**Signification** :
- Le point à 100% de l'image (coin inférieur droit) est aligné avec le point à 100% de l'élément
- Résultat : l'image est en bas à droite

### Exemples pratiques

```css
/* Centrer une image de fond */
.banner {
  background-image: url('banner.jpg');
  background-repeat: no-repeat;
  background-position: center center;
  height: 400px;
}

/* Logo en haut à droite */
.header {
  background-image: url('logo.png');
  background-repeat: no-repeat;
  background-position: right top;
  padding-top: 60px; /* Laisser de l'espace pour le logo */
}

/* Image décalée légèrement */
.feature {
  background-image: url('icon.png');
  background-repeat: no-repeat;
  background-position: 20px center;
  padding-left: 80px; /* Laisser de l'espace pour l'icône */
}
```

---

## background-size : Taille de l'image

### Qu'est-ce que c'est ?

`background-size` contrôle les dimensions de l'image de fond.

### Valeurs avec mots-clés

```css
/* auto - Taille réelle de l'image (défaut) */
.element {
  background-size: auto;
}

/* cover - L'image couvre tout l'élément (peut être rognée) */
.element {
  background-size: cover;
}

/* contain - L'image est entièrement visible (peut laisser des espaces vides) */
.element {
  background-size: contain;
}
```

### Différence cover vs contain

#### cover (Usage le plus courant)

```css
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  background-position: center;
  height: 500px;
}
```

**Comportement** :
- L'image remplit **complètement** l'élément
- L'image peut être **rognée** sur les bords
- **Aucun espace vide** n'est visible
- Le ratio de l'image est préservé

**Usage** : Bannières, héros, sections plein écran

#### contain

```css
.logo-container {
  background-image: url('logo.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  height: 200px;
}
```

**Comportement** :
- L'image est **entièrement visible**
- L'image n'est **jamais rognée**
- Peut laisser des **espaces vides** autour
- Le ratio de l'image est préservé

**Usage** : Logos, icônes, quand l'image entière doit être visible

### Valeurs numériques

```css
/* Largeur fixe, hauteur auto */
.element {
  background-size: 200px auto;
}

/* Largeur et hauteur fixes */
.element {
  background-size: 300px 200px;
}

/* Pourcentages */
.element {
  background-size: 50% 50%;    /* 50% de la largeur/hauteur de l'élément */
  background-size: 100% auto;  /* Largeur 100%, hauteur proportionnelle */
}
```

### Exemples pratiques

```css
/* Section héros avec image plein écran */
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Carte avec image d'arrière-plan */
.card {
  background-image: url('card-bg.jpg');
  background-size: cover;
  background-position: center;
  padding: 40px;
  color: white;
  height: 300px;
}

/* Pattern de fond redimensionné */
.pattern {
  background-image: url('pattern.png');
  background-size: 50px 50px; /* Pattern de 50x50px */
  background-repeat: repeat;
}

/* Logo responsive */
.logo-bg {
  background-image: url('logo.svg');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  height: 100px;
}
```

---

## background-attachment : Comportement au scroll

### Qu'est-ce que c'est ?

`background-attachment` définit si l'image de fond défile avec le contenu ou reste fixe.

### Valeurs

```css
/* scroll - L'image défile avec l'élément (défaut) */
.element {
  background-attachment: scroll;
}

/* fixed - L'image reste fixe par rapport à la fenêtre */
.element {
  background-attachment: fixed;
}

/* local - L'image défile avec le contenu de l'élément */
.element {
  background-attachment: local;
}
```

### Effet parallaxe avec fixed

```css
/* Effet parallaxe classique */
.parallax {
  background-image: url('landscape.jpg');
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  height: 500px;
}
```

**Résultat** : L'image reste fixe pendant que vous scrollez, créant un effet de profondeur.

### Exemples pratiques

```css
/* Section avec effet parallaxe */
.hero-parallax {
  background-image: url('mountains.jpg');
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Plusieurs sections alternées */
.section-fixed {
  background-image: url('section-bg.jpg');
  background-attachment: fixed;
  background-size: cover;
  padding: 100px 0;
  color: white;
}

.section-normal {
  background-color: white;
  padding: 100px 0;
}
```

**⚠️ Note** : `background-attachment: fixed` peut causer des problèmes de performance sur mobile. Testez bien !

---

## background-origin et background-clip

### background-origin

Définit la zone de référence pour le positionnement de l'image :

```css
.element {
  background-origin: padding-box;  /* Défaut - depuis le padding */
  background-origin: border-box;   /* Depuis la bordure */
  background-origin: content-box;  /* Depuis le contenu */
}
```

### background-clip

Définit jusqu'où l'arrière-plan s'étend :

```css
.element {
  background-clip: border-box;   /* Défaut - jusqu'à la bordure */
  background-clip: padding-box;  /* Jusqu'au padding */
  background-clip: content-box;  /* Seulement le contenu */
  background-clip: text;         /* Clip sur le texte (effet spécial) */
}
```

### Exemple : Texte avec image de fond

```css
.gradient-text {
  background-image: linear-gradient(45deg, #f093fb, #f5576c);
  background-clip: text;
  -webkit-background-clip: text;  /* Pour Safari */
  color: transparent;
  font-size: 3rem;
  font-weight: bold;
}
```

---

## Propriété raccourcie : background

### Syntaxe

La propriété `background` permet de définir toutes les propriétés d'arrière-plan en une seule ligne :

```css
.element {
  background: color image repeat position / size attachment;
}
```

**Important** : L'ordre n'est pas strict, mais `position` et `size` doivent être séparés par `/`

### Exemples

```css
/* Simple : couleur uniquement */
.element {
  background: #3498DB;
}

/* Image avec propriétés */
.element {
  background: url('image.jpg') no-repeat center center;
}

/* Complet avec size */
.element {
  background: url('hero.jpg') no-repeat center center / cover;
}

/* Très complet */
.element {
  background: #2C3E50 url('bg.jpg') no-repeat center top / cover fixed;
}

/* Avec couleur de secours */
.element {
  background: #3498DB url('image.jpg') no-repeat center / cover;
  /* Si l'image ne charge pas, le fond reste bleu */
}
```

### Ordre recommandé (pour la lisibilité)

```css
.element {
  background:
    [color]
    url('image.jpg')
    [repeat]
    [position] / [size]
    [attachment];
}
```

### Exemples pratiques

```css
/* Héros simple */
.hero {
  background: url('hero.jpg') no-repeat center center / cover;
  height: 500px;
}

/* Avec couleur de fond et image */
.section {
  background: #2C3E50 url('pattern.png') repeat;
  padding: 60px 0;
  color: white;
}

/* Effet parallaxe en une ligne */
.parallax {
  background: url('mountains.jpg') no-repeat center center / cover fixed;
  height: 100vh;
}
```

---

## Arrière-plans multiples 🆕

CSS3 permet de superposer plusieurs arrière-plans :

### Syntaxe

```css
.element {
  background-image:
    url('image1.png'),
    url('image2.png'),
    url('image3.png');

  background-position:
    top right,
    bottom left,
    center center;

  background-repeat:
    no-repeat,
    no-repeat,
    repeat;
}
```

**Important** : Les images sont listées de la plus **visible** (dessus) à la moins visible (dessous).

### Exemple pratique

```css
/* Overlay + texture + image de fond */
.hero-complex {
  background-image:
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url('texture.png'),
    url('hero.jpg');

  background-position:
    center,
    top left,
    center;

  background-size:
    cover,
    auto,
    cover;

  background-repeat:
    no-repeat,
    repeat,
    no-repeat;
}
```

### Syntaxe raccourcie pour multiples backgrounds

```css
.element {
  background:
    url('overlay.png') no-repeat center / cover,
    url('pattern.png') repeat,
    url('main.jpg') no-repeat center / cover;
}
```

---

## Dégradés (Gradients) 🆕

Les dégradés sont des "images" générées par CSS.

### linear-gradient : Dégradé linéaire

```css
/* Dégradé vertical (par défaut) */
.element {
  background: linear-gradient(#3498DB, #2C3E50);
}

/* Dégradé horizontal */
.element {
  background: linear-gradient(to right, #3498DB, #2C3E50);
}

/* Dégradé diagonal */
.element {
  background: linear-gradient(to bottom right, #3498DB, #2C3E50);
}

/* Dégradé avec angle */
.element {
  background: linear-gradient(45deg, #3498DB, #2C3E50);
}

/* Dégradé avec plusieurs couleurs */
.element {
  background: linear-gradient(to right, #f093fb, #f5576c, #4facfe);
}

/* Dégradé avec positions */
.element {
  background: linear-gradient(
    to right,
    #3498DB 0%,
    #2C3E50 50%,
    #E74C3C 100%
  );
}
```

### Exemples de dégradés populaires

```css
/* Dégradé sunset */
.sunset {
  background: linear-gradient(to bottom, #ff6b6b, #feca57, #48dbfb);
}

/* Dégradé violet-rose */
.purple-pink {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Dégradé avec overlay */
.hero-gradient {
  background:
    linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.6)),
    url('hero.jpg') no-repeat center / cover;
}
```

### radial-gradient : Dégradé radial

```css
/* Dégradé circulaire (centre par défaut) */
.element {
  background: radial-gradient(circle, #3498DB, #2C3E50);
}

/* Dégradé elliptique */
.element {
  background: radial-gradient(ellipse, #3498DB, #2C3E50);
}

/* Dégradé avec position */
.element {
  background: radial-gradient(circle at top right, #3498DB, #2C3E50);
}

/* Dégradé avec taille */
.element {
  background: radial-gradient(
    circle 200px at center,
    #3498DB,
    #2C3E50
  );
}
```

### repeating-linear-gradient : Dégradé répété

```css
/* Rayures */
.stripes {
  background: repeating-linear-gradient(
    45deg,
    #3498DB,
    #3498DB 10px,
    #2C3E50 10px,
    #2C3E50 20px
  );
}

/* Effet de lignes */
.lines {
  background: repeating-linear-gradient(
    to bottom,
    transparent,
    transparent 10px,
    rgba(0, 0, 0, 0.1) 10px,
    rgba(0, 0, 0, 0.1) 11px
  );
}
```

---

## Exemples pratiques complets

### Exemple 1 : Section héros moderne

```css
.hero {
  /* Overlay sombre + image */
  background:
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.7)),
    url('hero.jpg') no-repeat center center / cover;

  /* Dimensions */
  min-height: 100vh;

  /* Centrage du contenu */
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;

  /* Texte */
  color: white;
}
```

### Exemple 2 : Carte avec image de fond

```css
.feature-card {
  /* Image + overlay dégradé */
  background:
    linear-gradient(to bottom, transparent, rgba(0, 0, 0, 0.8)),
    url('card-image.jpg') no-repeat center / cover;

  /* Dimensions et espacement */
  height: 300px;
  padding: 20px;
  border-radius: 8px;

  /* Positionnement du texte */
  display: flex;
  flex-direction: column;
  justify-content: flex-end;

  /* Texte */
  color: white;
}
```

### Exemple 3 : Bouton dégradé

```css
.button-gradient {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 15px 30px;
  border: none;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.button-gradient:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}
```

### Exemple 4 : Section alternée avec parallaxe

```css
/* Section avec fond fixe */
.parallax-section {
  background: url('background.jpg') no-repeat center center / cover fixed;
  padding: 100px 20px;
  color: white;
  text-align: center;
}

/* Section normale entre deux parallaxe */
.content-section {
  background-color: white;
  padding: 80px 20px;
}
```

### Exemple 5 : Pattern de fond subtil

```css
.pattern-bg {
  background:
    url('subtle-pattern.png') repeat,
    linear-gradient(to bottom, #f5f7fa, #c3cfe2);
  padding: 60px 20px;
}
```

---

## Images responsive

### Technique 1 : background-size: cover

```css
.responsive-bg {
  background-image: url('image.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  min-height: 400px;
}

/* S'adapte automatiquement à toutes les tailles */
```

### Technique 2 : Images différentes selon la taille

```css
/* Image mobile */
.hero {
  background-image: url('hero-mobile.jpg');
  background-size: cover;
  background-position: center;
  height: 300px;
}

/* Image desktop */
@media (min-width: 768px) {
  .hero {
    background-image: url('hero-desktop.jpg');
    height: 600px;
  }
}
```

### Technique 3 : image-set pour la résolution

```css
.element {
  background-image: image-set(
    url('image-1x.jpg') 1x,
    url('image-2x.jpg') 2x
  );
  /* Charge l'image appropriée selon la résolution de l'écran */
}
```

---

## Performance et optimisation

### 1. Optimiser les images

```css
/* ✅ Bon : image optimisée */
.hero {
  background-image: url('hero-optimized.jpg'); /* 200KB */
  background-size: cover;
}

/* ❌ Mauvais : image trop lourde */
.hero {
  background-image: url('hero-original.jpg'); /* 5MB */
}
```

**Conseils** :
- Compressez vos images (TinyPNG, ImageOptim)
- Utilisez le format approprié (JPG pour photos, PNG pour transparence, WebP pour le web)
- Redimensionnez aux dimensions réelles utilisées

### 2. Utiliser des images adaptées

```css
/* Pour un petit élément, utilisez une petite image */
.icon-bg {
  background-image: url('icon-small.png'); /* 50x50px */
  width: 50px;
  height: 50px;
}

/* Pas une image 2000x2000px ! */
```

### 3. Couleur de secours

```css
/* Toujours fournir une couleur de secours */
.element {
  background-color: #3498DB; /* Couleur de secours */
  background-image: url('image.jpg');
}
```

### 4. Lazy loading avec CSS (approche moderne)

```css
/* Charger l'image seulement quand nécessaire */
.lazy-bg {
  background-color: #f0f0f0; /* Placeholder */
}

.lazy-bg.loaded {
  background-image: url('image.jpg');
}
```

---

## Accessibilité

### Images décoratives vs informatives

```css
/* ❌ Mauvais : information importante seulement en background */
.announcement {
  background-image: url('important-info.png');
  height: 200px;
}
/* Les lecteurs d'écran ne verront pas cette information */

/* ✅ Bon : utiliser <img> pour contenu informatif */
```

**Règle** : Si l'image porte de l'information, utilisez `<img>` avec `alt`. Les backgrounds sont pour la décoration uniquement.

### Contraste suffisant

```css
/* ✅ Bon : overlay pour assurer le contraste */
.hero {
  background:
    linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.6)),
    url('hero.jpg') no-repeat center / cover;
  color: white;
}

/* ❌ Mauvais : texte peut être illisible selon l'image */
.hero {
  background: url('hero.jpg') no-repeat center / cover;
  color: white; /* Peut ne pas avoir assez de contraste */
}
```

---

## Erreurs courantes et solutions

### Erreur 1 : Image ne s'affiche pas

```css
/* ❌ Problème : chemin incorrect */
.element {
  background-image: url('image.jpg');
  /* Cherche dans le même dossier que le CSS */
}

/* ✅ Solution : vérifier le chemin */
.element {
  background-image: url('../images/image.jpg');
}
```

**Vérifications** :
1. Le chemin est-il correct ?
2. Le fichier existe-t-il ?
3. L'extension est-elle correcte (.jpg, .png) ?
4. Les guillemets sont-ils présents ?

### Erreur 2 : Image répétée non voulue

```css
/* ❌ Problème : image se répète */
.hero {
  background-image: url('hero.jpg');
  /* Se répète par défaut */
}

/* ✅ Solution */
.hero {
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}
```

### Erreur 3 : Image déformée

```css
/* ❌ Mauvais : étire l'image */
.element {
  background-size: 100% 100%;
  /* Ne respecte pas le ratio */
}

/* ✅ Bon : garde le ratio */
.element {
  background-size: cover;  /* Ou contain */
}
```

### Erreur 4 : Oublier height

```css
/* ❌ Problème : élément vide avec background */
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  /* Pas de hauteur = élément invisible */
}

/* ✅ Solution */
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  min-height: 500px;  /* Ou height, ou du contenu */
}
```

### Erreur 5 : background-attachment: fixed sur mobile

```css
/* ❌ Problème : performance sur mobile */
.parallax {
  background-attachment: fixed;
  /* Peut être très lent sur mobile */
}

/* ✅ Solution : désactiver sur mobile */
.parallax {
  background-attachment: scroll;
}

@media (min-width: 1024px) {
  .parallax {
    background-attachment: fixed;
  }
}
```

---

## Bonnes pratiques

### 1. Ordre recommandé des propriétés

```css
.element {
  /* Couleur de fond */
  background-color: #3498DB;

  /* Image */
  background-image: url('image.jpg');

  /* Positionnement et taille */
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;

  /* Comportement */
  background-attachment: fixed;
}
```

### 2. Toujours tester sans l'image

```css
/* Assurez-vous que le texte reste lisible si l'image ne charge pas */
.hero {
  background-color: #2C3E50; /* Couleur de secours */
  background-image: url('hero.jpg');
  color: white;
}
```

### 3. Utiliser des variables pour les chemins

```css
:root {
  --img-path: '../images/';
}

.hero {
  background-image: url(var(--img-path)hero.jpg);
}
```

### 4. Combiner avec object-fit pour <img>

Pour les images HTML (pas background), utilisez `object-fit` :

```css
/* Pour <img> tag */
img {
  width: 100%;
  height: 300px;
  object-fit: cover;  /* Similaire à background-size: cover */
  object-position: center; /* Similaire à background-position */
}
```

### 5. Nommer clairement les classes

```css
/* ✅ Bon : descriptif */
.hero-background { }
.pattern-background { }
.gradient-overlay { }

/* ❌ Moins clair */
.bg1 { }
.style2 { }
```

---

## Résumé

### Propriétés essentielles

| Propriété | Fonction | Valeur courante |
|-----------|----------|-----------------|
| **background-color** | Couleur de fond | `#3498DB`, `rgba(0,0,0,0.5)` |
| **background-image** | Image de fond | `url('image.jpg')` |
| **background-repeat** | Répétition | `no-repeat`, `repeat` |
| **background-position** | Position | `center`, `top right` |
| **background-size** | Taille | `cover`, `contain` |
| **background-attachment** | Scroll | `fixed`, `scroll` |
| **background** | Raccourci | `url('img.jpg') no-repeat center/cover` |

### Syntaxes essentielles

```css
/* Image de fond basique */
.element {
  background-image: url('image.jpg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

/* Version raccourcie */
.element {
  background: url('image.jpg') no-repeat center / cover;
}

/* Héros moderne avec overlay */
.hero {
  background:
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url('hero.jpg') no-repeat center / cover;
  min-height: 100vh;
}

/* Dégradé simple */
.gradient {
  background: linear-gradient(135deg, #667eea, #764ba2);
}
```

### Points clés à retenir

1. **`background-size: cover`** est le plus utilisé pour les images de fond
2. Toujours utiliser **`background-repeat: no-repeat`** pour les photos
3. **`background-position: center`** centre l'image
4. Les **dégradés** sont considérés comme des images
5. On peut **superposer plusieurs backgrounds**
6. Toujours fournir une **couleur de secours**
7. Optimiser les **images** pour le web

Les backgrounds sont essentiels pour créer des designs modernes et attractifs. Expérimentez avec les dégradés et les overlays pour des effets visuels sophistiqués !

⏭️ [Mise en page moderne](/04-css3-styles-et-mise-en-page/03-mise-en-page-moderne/README.md)
