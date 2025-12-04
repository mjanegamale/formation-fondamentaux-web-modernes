🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.4.1 - Optimisation des images

## Pourquoi optimiser les images ?

Les images représentent souvent **la plus grande partie du poids** d'une page web. Selon HTTP Archive, les images constituent en moyenne **50 à 60%** du poids total d'un site web.

### L'impact des images non optimisées 📊

#### Sur la performance ⚡
- **Chargement lent** : des images lourdes ralentissent le chargement de la page
- **Consommation de bande passante** : coûteux pour les utilisateurs mobiles
- **Mauvaise expérience utilisateur** : les visiteurs quittent les sites trop lents

**Statistique importante** :
- 53% des utilisateurs abandonnent un site si le chargement dépasse 3 secondes
- Chaque seconde supplémentaire réduit les conversions de 7%

#### Sur le référencement (SEO) 🔍
- Google pénalise les sites lents dans ses résultats de recherche
- Les Core Web Vitals incluent la vitesse de chargement
- Un site rapide = meilleur classement

#### Sur les coûts 💰
- **Hébergement** : plus de bande passante = coûts plus élevés
- **CDN** : transfert de données facturé
- **Énergie** : impact environnemental

### Les bénéfices de l'optimisation ✅

En optimisant vos images, vous obtenez :
- ⚡ **Chargement jusqu'à 80% plus rapide**
- 💾 **Réduction de 50-90% du poids des images**
- 📈 **Meilleur référencement**
- 😊 **Expérience utilisateur améliorée**
- 🌍 **Réduction de l'empreinte carbone**

---

## Les formats d'images pour le web

Choisir le bon format d'image est la **première étape** de l'optimisation.

### JPEG (.jpg, .jpeg) 📸

**Meilleur pour** : Photos et images avec beaucoup de couleurs

#### Caractéristiques :
- **Compression avec perte** : réduit la taille en sacrifiant légèrement la qualité
- **Millions de couleurs** : idéal pour les photos réalistes
- **Pas de transparence** : fond toujours opaque
- **Compression ajustable** : vous contrôlez le compromis qualité/taille

#### ✅ Utilisez JPEG pour :
```html
<!-- Photos de produits -->
<img src="produit-smartphone.jpg" alt="Smartphone dernière génération">

<!-- Photos de personnes -->
<img src="equipe-photo.jpg" alt="Photo de l'équipe">

<!-- Paysages -->
<img src="paysage-montagne.jpg" alt="Vue des montagnes">

<!-- Images complexes avec dégradés -->
<img src="background-gradient.jpg" alt="">
```

#### ❌ N'utilisez PAS JPEG pour :
- Logos (utilisez PNG ou SVG)
- Icônes (utilisez SVG ou PNG)
- Texte dans l'image (utilisez PNG ou SVG)
- Images nécessitant de la transparence

#### Paramètres recommandés :
```
Qualité : 75-85% (bon équilibre qualité/taille)
Qualité < 70% : perte de qualité visible
Qualité > 90% : fichier trop lourd sans gain visible
```

---

### PNG (.png) 🎨

**Meilleur pour** : Images avec transparence, logos, icônes, captures d'écran

#### Caractéristiques :
- **Compression sans perte** : qualité préservée
- **Transparence** : canal alpha pour transparence
- **Deux versions** :
  - PNG-8 : 256 couleurs maximum (petits fichiers)
  - PNG-24 : Millions de couleurs (fichiers plus lourds)

#### ✅ Utilisez PNG pour :
```html
<!-- Logos avec transparence -->
<img src="logo.png" alt="Logo de l'entreprise">

<!-- Icônes -->
<img src="icon-checkmark.png" alt="">

<!-- Captures d'écran -->
<img src="screenshot-app.png" alt="Capture d'écran de l'application">

<!-- Graphiques avec texte -->
<img src="diagramme.png" alt="Diagramme des ventes">
```

#### ❌ N'utilisez PAS PNG pour :
- Photos (fichiers trop lourds, utilisez JPEG ou WebP)
- Images complexes avec beaucoup de couleurs

---

### WebP (.webp) 🆕

**Meilleur pour** : Tous types d'images (format moderne)

#### Caractéristiques :
- **Format moderne** développé par Google
- **Compression excellente** : 25-35% plus léger que JPEG/PNG
- **Supporte la transparence** comme PNG
- **Compression avec ou sans perte** au choix
- **Support navigateur** : Excellent (96%+ des navigateurs modernes)

#### ✅ Utilisez WebP pour :
```html
<!-- Photos -->
<img src="produit.webp" alt="Produit">

<!-- Logos avec transparence -->
<img src="logo.webp" alt="Logo">

<!-- Toute image où vous voulez optimiser le poids -->
```

#### Avec fallback pour anciens navigateurs :
```html
<picture>
  <!-- WebP pour navigateurs modernes -->
  <source srcset="image.webp" type="image/webp">
  <!-- JPEG pour anciens navigateurs -->
  <img src="image.jpg" alt="Description">
</picture>
```

---

### SVG (.svg) 📐

**Meilleur pour** : Logos, icônes, illustrations vectorielles

#### Caractéristiques :
- **Format vectoriel** : basé sur du code (XML)
- **Infiniment redimensionnable** : aucune perte de qualité
- **Très léger** : parfait pour icônes et logos simples
- **Modifiable** : couleurs, taille, animations en CSS/JS
- **Accessible** : peut contenir du texte réel

#### ✅ Utilisez SVG pour :
```html
<!-- Logos -->
<img src="logo.svg" alt="Logo de l'entreprise">

<!-- Icônes -->
<svg width="24" height="24" viewBox="0 0 24 24">
  <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>
</svg>

<!-- Illustrations simples -->
<img src="illustration.svg" alt="Illustration décorative">

<!-- Graphiques et diagrammes -->
<img src="chart.svg" alt="Graphique des statistiques">
```

#### ❌ N'utilisez PAS SVG pour :
- Photos (utilisez JPEG ou WebP)
- Images bitmap complexes

#### Optimisation SVG :
```html
<!-- ❌ SVG non optimisé : beaucoup de code inutile -->
<!-- Exporté directement d'Illustrator/Figma -->

<!-- ✅ SVG optimisé avec SVGO -->
<!-- Code nettoyé, métadonnées supprimées -->
```

**Outil recommandé** : [SVGOMG](https://jakearchibald.github.io/svgomg/) pour optimiser vos SVG en ligne.

---

### AVIF (.avif) 🌟

**Meilleur pour** : Images de nouvelle génération (très récent)

#### Caractéristiques :
- **Format ultra-moderne** (2019)
- **Compression exceptionnelle** : jusqu'à 50% plus léger que WebP
- **Supporte la transparence**
- **Support navigateur** : En croissance (Chrome, Firefox, Safari 16+)

#### ⚠️ Attention :
- Encore peu supporté (environ 85% des navigateurs en 2025)
- **Toujours fournir un fallback**

```html
<picture>
  <!-- AVIF pour navigateurs très modernes -->
  <source srcset="image.avif" type="image/avif">
  <!-- WebP pour navigateurs modernes -->
  <source srcset="image.webp" type="image/webp">
  <!-- JPEG pour tous les navigateurs -->
  <img src="image.jpg" alt="Description">
</picture>
```

---

### GIF (.gif) 🎬

**Meilleur pour** : Animations courtes (mais privilégiez les alternatives modernes)

#### Caractéristiques :
- **Animations** : séquence d'images
- **256 couleurs maximum** : palette limitée
- **Souvent très lourd** : peut atteindre plusieurs Mo

#### ⚠️ Problèmes avec GIF :
- Fichiers **très lourds** pour des animations
- Qualité **limitée** (256 couleurs)
- Pas de contrôle de lecture (pause, volume)

#### ✅ Alternatives modernes au GIF :
```html
<!-- ❌ GIF lourd : 5 MB -->
<img src="animation.gif" alt="Animation">

<!-- ✅ Vidéo MP4 légère : 500 KB (10x plus léère !) -->
<video autoplay loop muted playsinline>
  <source src="animation.mp4" type="video/mp4">
</video>
```

**Conseil** : Convertissez vos GIF en vidéo MP4 avec [Ezgif](https://ezgif.com/gif-to-mp4).

---

### Tableau récapitulatif des formats

| Format | Usage principal | Transparence | Compression | Poids moyen |
|--------|----------------|--------------|-------------|-------------|
| **JPEG** | Photos | ❌ Non | Avec perte | Moyen |
| **PNG** | Logos, icônes | ✅ Oui | Sans perte | Lourd |
| **WebP** | Tout type | ✅ Oui | Excellente | Léger |
| **AVIF** | Tout type (moderne) | ✅ Oui | Exceptionnelle | Très léger |
| **SVG** | Logos, icônes vectoriels | ✅ Oui | N/A (vectoriel) | Très léger |
| **GIF** | Animations (déprécié) | ⚠️ Limité | Mauvaise | Très lourd |

---

## Compression et qualité

### Comprendre la compression

Il existe deux types de compression :

#### 1. **Compression avec perte** (Lossy)
- Réduit la taille en **supprimant des données**
- Qualité légèrement dégradée (souvent imperceptible)
- **Formats** : JPEG, WebP (mode lossy), AVIF

```
Image originale : 5 MB
Après compression (80%) : 800 KB
Réduction : 84% → Qualité : Excellent
```

#### 2. **Compression sans perte** (Lossless)
- Réduit la taille **sans perte de qualité**
- Optimise le code/structure du fichier
- **Formats** : PNG, WebP (mode lossless), SVG

```
Image originale : 2 MB
Après compression : 1.2 MB
Réduction : 40% → Qualité : Identique
```

---

### Trouver le bon équilibre qualité/poids

#### Qualité JPEG recommandée :

```css
/* Guide des paramètres de qualité JPEG */

Qualité 100% : 2 MB    ❌ Inutile, trop lourd
Qualité 90%  : 800 KB  ⚠️ Qualité excellente mais lourd
Qualité 85%  : 400 KB  ✅ Qualité excellente, poids acceptable
Qualité 80%  : 300 KB  ✅ Idéal : bon compromis
Qualité 75%  : 220 KB  ✅ Très bon, légères pertes
Qualité 70%  : 180 KB  ⚠️ Acceptable, pertes visibles
Qualité 60%  : 150 KB  ❌ Mauvaise qualité visible
```

**Recommandation** :
- **Photos de héros** (hero images) : 85%
- **Photos de contenu** : 80%
- **Miniatures** : 75%

---

### Test visuel de qualité

Pour déterminer la qualité optimale :

1. **Créez plusieurs versions** (100%, 90%, 80%, 70%, 60%)
2. **Comparez visuellement** sur différents écrans
3. **Choisissez la qualité la plus basse** qui reste acceptable
4. **Testez sur mobile** aussi (écrans plus petits = moins de détails visibles)

---

## Dimensionner correctement les images

### Le problème des images surdimensionnées 📏

```html
<!-- ❌ Mauvais : image 4000x3000px affichée en 400x300px -->
<img src="photo-4000x3000.jpg" width="400" height="300" alt="Photo">
<!-- Le navigateur charge 4000x3000 mais affiche 400x300 = gaspillage ! -->

<!-- ✅ Bon : image déjà redimensionnée à la bonne taille -->
<img src="photo-400x300.jpg" width="400" height="300" alt="Photo">
<!-- Le navigateur charge exactement ce dont il a besoin -->
```

### Règle d'or : Dimensionnement

> **Ne servez jamais une image plus grande que sa taille d'affichage maximale.**

#### Exemple pratique :

Si votre design affiche une image à 800px de large maximum :
```
❌ Image originale : 4000 x 3000 px → 5 MB
✅ Image redimensionnée : 800 x 600 px → 150 KB

Économie : 97% de bande passante !
```

---

### Calcul de la taille d'affichage

Pour un affichage net sur les écrans haute résolution (Retina, etc.) :

```
Taille d'affichage × 2 = Taille de l'image

Exemple :
Affichage prévu : 400px
Image à fournir : 800px (pour Retina)
```

**Mais attention** :
- Ne dépassez pas 2x pour le web (3x est inutile et trop lourd)
- Pour les photos, 1.5x est souvent suffisant

---

## Images responsives

Les images responsives s'adaptent à la taille de l'écran et à la résolution.

### 1. Attribut `srcset` - Résolutions différentes

Pour servir différentes résolutions selon la densité d'écran :

```html
<img
  src="image-800w.jpg"
  srcset="
    image-400w.jpg 400w,
    image-800w.jpg 800w,
    image-1200w.jpg 1200w
  "
  sizes="(max-width: 600px) 400px,
         (max-width: 1200px) 800px,
         1200px"
  alt="Description"
>
```

**Comment ça marche ?**
1. Le navigateur connaît la taille de l'écran
2. Il choisit automatiquement l'image la plus appropriée
3. Sur mobile → petite image
4. Sur desktop → grande image

---

### 2. Élément `<picture>` - Recadrage artistique

Pour servir différentes versions d'une image selon le contexte :

```html
<picture>
  <!-- Image mobile (portrait) -->
  <source
    media="(max-width: 768px)"
    srcset="image-mobile-portrait.jpg"
  >

  <!-- Image tablette -->
  <source
    media="(max-width: 1200px)"
    srcset="image-tablet.jpg"
  >

  <!-- Image desktop (paysage) -->
  <img
    src="image-desktop-landscape.jpg"
    alt="Description"
  >
</picture>
```

**Cas d'usage** :
- Image de héros différente selon l'écran
- Recadrage différent (focus sur sujet principal)
- Format différent (portrait vs paysage)

---

### 3. Images responsives avec formats modernes

Combinez formats modernes et images responsives :

```html
<picture>
  <!-- WebP pour mobile -->
  <source
    media="(max-width: 768px)"
    srcset="image-mobile.webp"
    type="image/webp"
  >

  <!-- WebP pour desktop -->
  <source
    srcset="image-desktop.webp"
    type="image/webp"
  >

  <!-- JPEG fallback -->
  <img
    src="image-desktop.jpg"
    alt="Description"
  >
</picture>
```

---

## Lazy Loading (Chargement différé) ⏱️

Le lazy loading charge les images **uniquement quand elles deviennent visibles** à l'écran.

### Avantages du lazy loading :

- ⚡ **Chargement initial plus rapide**
- 💾 **Économie de bande passante** (images hors écran non chargées)
- 📱 **Meilleure expérience mobile**

---

### Lazy loading natif (moderne et simple)

```html
<!-- ✅ Lazy loading natif avec l'attribut loading -->
<img
  src="image.jpg"
  alt="Description"
  loading="lazy"
>
```

**C'est tout !** Le navigateur gère automatiquement :
- Les images "above the fold" (visibles) se chargent immédiatement
- Les images plus bas se chargent quand l'utilisateur scrolle

**Support navigateur** : Excellent (96%+ des navigateurs modernes)

---

### Bonnes pratiques lazy loading

#### ✅ Lazy loadez :
```html
<!-- Images en bas de page -->
<img src="image-footer.jpg" alt="..." loading="lazy">

<!-- Images dans une galerie -->
<img src="gallery-1.jpg" alt="..." loading="lazy">

<!-- Images de contenu long -->
<article>
  <img src="article-image.jpg" alt="..." loading="lazy">
</article>
```

#### ❌ Ne lazy loadez PAS :
```html
<!-- Images "above the fold" (visibles immédiatement) -->
<img src="hero-image.jpg" alt="..." loading="eager">

<!-- Logo -->
<img src="logo.png" alt="Logo" loading="eager">

<!-- Première image importante -->
<img src="main-image.jpg" alt="...">
```

**Règle** : Les 2-3 premières images de la page doivent charger normalement.

---

### Placeholder pendant le chargement

Pour améliorer l'expérience visuelle :

```html
<!-- Image avec couleur de fond placeholder -->
<img
  src="image.jpg"
  alt="Description"
  loading="lazy"
  style="background-color: #f0f0f0;"
>
```

Ou avec un effet de flou progressif (blur-up) :

```html
<div class="image-container">
  <!-- Version basse résolution (très légère, 1-2 KB) -->
  <img
    src="image-tiny.jpg"
    alt="Description"
    class="blur-placeholder"
  >

  <!-- Version haute résolution (chargement différé) -->
  <img
    src="image-full.jpg"
    alt="Description"
    loading="lazy"
    class="full-image"
  >
</div>
```

---

## Outils d'optimisation

### 1. Outils en ligne (gratuits) 🌐

#### TinyPNG / TinyJPG
- **URL** : https://tinypng.com
- Compresse PNG et JPEG jusqu'à 70%
- Qualité visuelle préservée
- Limite : 5 MB par fichier, 20 fichiers max

#### Squoosh
- **URL** : https://squoosh.app (par Google)
- Tous formats : JPEG, PNG, WebP, AVIF
- Comparaison visuelle avant/après
- Contrôle précis de la qualité
- **Recommandé** : Interface excellente

#### Compressor.io
- **URL** : https://compressor.io
- Compression jusqu'à 90%
- Supporte JPEG, PNG, SVG, GIF
- Limite : 10 MB par fichier

---

### 2. Outils de conversion de format 🔄

#### CloudConvert
- **URL** : https://cloudconvert.com
- Convertit vers WebP, AVIF, etc.
- Traitement par lots
- API disponible

#### Convertio
- **URL** : https://convertio.co/fr/
- Conversion entre tous formats
- Simple et rapide

---

### 3. Optimisation SVG 📐

#### SVGOMG
- **URL** : https://jakearchibald.github.io/svgomg/
- Interface graphique pour SVGO
- Nettoyage du code SVG
- Réduction de 50-90% du poids
- Prévisualisation en temps réel

---

### 4. Logiciels de traitement d'images 🖼️

#### Photoshop / GIMP
```
Exportation pour le web :
1. Fichier → Exporter → Enregistrer pour le web (legacy)
2. Choisir le format (JPEG, PNG-8, PNG-24)
3. Ajuster la qualité
4. Comparer les tailles
```

#### ImageOptim (Mac)
- Gratuit et open source
- Optimise PNG, JPEG, GIF, SVG
- Interface drag & drop simple

#### FileOptimizer (Windows)
- Gratuit
- Optimise tous formats d'images
- Traitement par lots

---

### 5. Build tools automatisés 🤖

Pour automatiser l'optimisation dans votre workflow :

#### gulp-imagemin (Node.js)
```javascript
// Exemple avec Gulp
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');

gulp.task('images', () =>
  gulp.src('src/images/*')
    .pipe(imagemin([
      imagemin.mozjpeg({quality: 80}),
      imagemin.optipng({optimizationLevel: 5})
    ]))
    .pipe(gulp.dest('dist/images'))
);
```

#### image-webpack-loader (Webpack)
```javascript
// Configuration Webpack
module: {
  rules: [{
    test: /\.(png|jpe?g|gif|svg)$/i,
    use: [
      'file-loader',
      {
        loader: 'image-webpack-loader',
        options: {
          mozjpeg: { quality: 80 },
          pngquant: { quality: [0.65, 0.90] }
        }
      }
    ]
  }]
}
```

---

## Bonnes pratiques d'optimisation

### Checklist complète ✅

#### Avant le développement

- [ ] **Choisir le bon format** selon le type d'image
  - Photos → JPEG ou WebP
  - Logos/icônes → SVG ou PNG
  - Animations → MP4 au lieu de GIF

- [ ] **Exporter aux bonnes dimensions**
  - Maximum 2x la taille d'affichage
  - Créer plusieurs versions pour responsive

- [ ] **Compresser les images**
  - JPEG : qualité 75-85%
  - PNG : optimisation sans perte
  - WebP : pour tous types

---

#### Pendant le développement

- [ ] **Utiliser des formats modernes**
  ```html
  <picture>
    <source srcset="image.webp" type="image/webp">
    <img src="image.jpg" alt="Description">
  </picture>
  ```

- [ ] **Implémenter le lazy loading**
  ```html
  <img src="image.jpg" alt="..." loading="lazy">
  ```

- [ ] **Rendre les images responsives**
  ```html
  <img
    srcset="small.jpg 400w, medium.jpg 800w, large.jpg 1200w"
    sizes="(max-width: 600px) 400px, 800px"
    src="medium.jpg"
    alt="..."
  >
  ```

- [ ] **Spécifier width et height**
  ```html
  <img src="image.jpg" width="800" height="600" alt="...">
  <!-- Évite les reflows pendant le chargement -->
  ```

- [ ] **Toujours ajouter un attribut alt**
  ```html
  <img src="image.jpg" alt="Description pertinente">
  ```

---

#### Après le développement

- [ ] **Tester la performance**
  - Lighthouse (Chrome DevTools)
  - PageSpeed Insights
  - WebPageTest

- [ ] **Vérifier les tailles de fichiers**
  - Onglet Network des DevTools
  - Identifier les images lourdes

- [ ] **Optimiser les images lourdes**
  - Compresser davantage
  - Redimensionner
  - Convertir en WebP

---

### Tailles cibles recommandées 📊

| Type d'image | Taille maximale recommandée |
|--------------|---------------------------|
| **Logo** | < 50 KB |
| **Icône** | < 10 KB |
| **Image de héros** (hero) | < 200 KB |
| **Photo de contenu** | < 150 KB |
| **Miniature** (thumbnail) | < 30 KB |
| **Image de fond** | < 100 KB |
| **Total de la page** | < 1-2 MB |

---

## Cas pratiques d'optimisation

### Exemple 1 : Photo de produit e-commerce

**Avant optimisation** :
```
photo-produit.jpg
Dimensions : 4000 x 3000 px
Poids : 6.2 MB
Format : JPEG 100%
```

**Après optimisation** :
```
photo-produit.webp
Dimensions : 800 x 600 px (taille d'affichage max)
Poids : 85 KB
Format : WebP 80%
Réduction : 98.6% !
```

**Code HTML** :
```html
<picture>
  <source srcset="photo-produit.webp" type="image/webp">
  <img
    src="photo-produit.jpg"
    width="800"
    height="600"
    alt="Nom du produit - vue principale"
    loading="lazy"
  >
</picture>
```

---

### Exemple 2 : Logo

**Avant optimisation** :
```
logo.png
Dimensions : 2000 x 500 px
Poids : 450 KB
Format : PNG-24
```

**Après optimisation** :
```
logo.svg
Vectoriel (redimensionnable)
Poids : 8 KB
Format : SVG optimisé
Réduction : 98.2% !
```

**Code HTML** :
```html
<img
  src="logo.svg"
  width="200"
  height="50"
  alt="Logo de l'entreprise"
>
```

---

### Exemple 3 : Galerie d'images responsive

```html
<div class="gallery">
  <picture>
    <!-- Mobile -->
    <source
      media="(max-width: 768px)"
      srcset="gallery-1-small.webp 400w"
      type="image/webp"
    >

    <!-- Desktop -->
    <source
      srcset="gallery-1-large.webp 1200w"
      type="image/webp"
    >

    <!-- Fallback -->
    <img
      src="gallery-1-large.jpg"
      alt="Photo de la galerie 1"
      loading="lazy"
      width="1200"
      height="800"
    >
  </picture>

  <!-- Répéter pour les autres images... -->
</div>
```

**Résultat** :
- Mobile : 50 KB par image
- Desktop : 180 KB par image
- Lazy loading : seules les images visibles chargent

---

## Tester et mesurer la performance

### 1. Lighthouse (Chrome DevTools) 💡

```
1. Ouvrir Chrome DevTools (F12)
2. Onglet "Lighthouse"
3. Cocher "Performance"
4. Cliquer sur "Analyze page load"
5. Consulter les recommandations images
```

**Métriques importantes** :
- Largest Contentful Paint (LCP) : < 2.5s
- Cumulative Layout Shift (CLS) : < 0.1
- Total Blocking Time (TBT) : < 300ms

---

### 2. PageSpeed Insights 📈

- **URL** : https://pagespeed.web.dev/
- Analyse votre page publique
- Suggestions d'optimisation spécifiques
- Score mobile et desktop

---

### 3. Onglet Network (DevTools) 🔍

```
1. Ouvrir DevTools (F12)
2. Onglet "Network"
3. Filtrer par "Img"
4. Recharger la page
5. Observer :
   - Taille de chaque image
   - Temps de chargement
   - Ordre de chargement
```

**À surveiller** :
- Images > 200 KB (à optimiser)
- Images qui bloquent le rendu
- Nombre total d'images

---

### 4. WebPageTest 🧪

- **URL** : https://www.webpagetest.org/
- Test de performance avancé
- Vue filmstrip (chargement visuel)
- Comparaison avant/après

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Images non compressées

```html
<!-- Image directement depuis l'appareil photo : 8 MB -->
<img src="IMG_1234.jpg" alt="Photo">
```

**Impact** : Temps de chargement de 10-30 secondes sur mobile.

---

### ❌ Erreur 2 : Même image pour mobile et desktop

```html
<!-- Image 4000px servie à un mobile 375px -->
<img src="huge-image.jpg" alt="Photo">
```

**Impact** : Gaspillage de 90% de la bande passante mobile.

---

### ❌ Erreur 3 : Pas de lazy loading

```html
<!-- 50 images chargent toutes immédiatement -->
<img src="image-1.jpg" alt="...">
<img src="image-2.jpg" alt="...">
<!-- ... 48 autres images ... -->
```

**Impact** : Chargement initial très lent, expérience utilisateur dégradée.

---

### ❌ Erreur 4 : Formats dépassés

```html
<!-- GIF animé de 15 MB -->
<img src="animation.gif" alt="Animation">
```

**Impact** : Fichier 30x plus lourd qu'une vidéo MP4 équivalente.

---

### ❌ Erreur 5 : Pas de dimensions spécifiées

```html
<!-- Pas de width/height : cause du layout shift -->
<img src="image.jpg" alt="...">
```

**Impact** : La page "saute" pendant le chargement (mauvais CLS).

---

## Récapitulatif : Workflow d'optimisation

### Étapes à suivre pour chaque image :

1. **Choisir le format approprié**
   - Photo → WebP ou JPEG
   - Logo → SVG ou PNG
   - Icône → SVG

2. **Redimensionner**
   - Maximum 2x la taille d'affichage
   - Créer versions mobile/desktop si nécessaire

3. **Compresser**
   - JPEG : 75-85% qualité
   - PNG : optimisation sans perte
   - WebP : conversion automatique

4. **Implémenter dans le code**
   - Utiliser `<picture>` si nécessaire
   - Ajouter `loading="lazy"`
   - Spécifier `width` et `height`
   - Toujours un `alt` descriptif

5. **Tester**
   - Lighthouse
   - Onglet Network
   - Test sur mobile réel

6. **Itérer**
   - Optimiser les images lourdes
   - Ajuster la qualité si nécessaire

---

## Conclusion

L'optimisation des images est **essentielle** pour créer des sites web performants et accessibles. En suivant les bonnes pratiques de cette section, vous pouvez :

- ⚡ **Réduire de 50-90%** le poids de vos images
- 🚀 **Accélérer le chargement** de vos pages
- 📱 **Améliorer l'expérience mobile** de vos utilisateurs
- 🔍 **Améliorer votre SEO** et votre classement
- 💰 **Réduire vos coûts** d'hébergement et de bande passante

**Points clés à retenir** :

1. Choisissez le **bon format** (WebP pour la plupart des cas)
2. **Redimensionnez** aux bonnes dimensions
3. **Compressez** avec le bon équilibre qualité/poids
4. Utilisez le **lazy loading** natif
5. Rendez vos images **responsives**
6. **Testez** régulièrement la performance

**L'optimisation des images n'est pas une tâche ponctuelle, c'est un réflexe à développer pour chaque projet.**

Dans la prochaine section, nous verrons comment optimiser le CSS et JavaScript pour améliorer encore davantage les performances de vos sites.

---

## Ressources complémentaires

### Outils d'optimisation
- [Squoosh](https://squoosh.app) - Compression et conversion d'images
- [TinyPNG](https://tinypng.com) - Compression PNG/JPEG
- [SVGOMG](https://jakearchibald.github.io/svgomg/) - Optimisation SVG
- [Ezgif](https://ezgif.com) - Conversion GIF vers MP4

### Tests de performance
- [PageSpeed Insights](https://pagespeed.web.dev/)
- [WebPageTest](https://www.webpagetest.org/)
- [GTmetrix](https://gtmetrix.com/)

### Documentation
- [MDN - Responsive Images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
- [Web.dev - Image Optimization](https://web.dev/fast/#optimize-your-images)
- [Can I Use - WebP](https://caniuse.com/webp)

⏭️ [Minification CSS/JS](/06-integration-html-css-javascript/04-performance-optimisation/02-minification.md)
