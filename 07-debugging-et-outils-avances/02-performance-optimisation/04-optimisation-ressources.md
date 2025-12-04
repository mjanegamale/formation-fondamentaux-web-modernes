🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.2.4 Optimisation des Images et Ressources

## Introduction

Vous avez analysé votre site avec Lighthouse et les DevTools. Vous savez maintenant **où** sont les problèmes. Mais comment les **corriger** concrètement ?

L'optimisation des images et ressources est souvent le **quick win #1** des performances web. C'est l'amélioration qui apporte le **plus de résultats avec le moins d'effort**. Une simple optimisation d'images peut transformer un site qui charge en 8 secondes en un site qui charge en 2 secondes !

Dans cette section, nous allons apprendre à optimiser **tout ce que votre site télécharge** : images, CSS, JavaScript, polices, et plus encore.

---

## Pourquoi optimiser ?

### L'impact des ressources non optimisées

**Statistiques réelles** :
- 📊 Les images représentent **50-70%** du poids d'une page web moyenne
- 🐌 Une page de 3 MB met **10 secondes** à charger en 3G
- 💰 Les utilisateurs mobiles paient pour chaque Mo téléchargé
- 📉 **+1 seconde** de chargement = -7% de conversions

### Exemple concret

**Avant optimisation** :
```
Page d'accueil :
├─ hero.jpg       2.5 MB  ← 🔴 Énorme !
├─ logo.png       800 KB  ← 🔴 Trop lourd
├─ style.css      250 KB  ← 🟠 Non minifié
├─ script.js      1.2 MB  ← 🔴 Non compressé
└─ fonts/         400 KB  ← 🟠 Toutes les variantes

Total: 5.15 MB
Temps de chargement (3G): 12 secondes
```

**Après optimisation** :
```
Page d'accueil :
├─ hero.webp      180 KB  ← ✅ Converti et compressé
├─ logo.svg       8 KB    ← ✅ Format vectoriel
├─ style.min.css  45 KB   ← ✅ Minifié
├─ script.min.js  350 KB  ← ✅ Minifié + tree-shaking
└─ fonts/         100 KB  ← ✅ Sous-ensemble

Total: 683 KB
Temps de chargement (3G): 2.5 secondes
```

**Résultat** : **87% de réduction** de poids, **80% plus rapide** !

---

## Optimisation des images

### Comprendre les formats d'images

Chaque format a ses forces et faiblesses :

#### JPEG (.jpg, .jpeg)

**Utilisation** : Photos, images complexes avec beaucoup de couleurs

**Avantages** :
- ✅ Excellente compression pour les photos
- ✅ Support universel (tous les navigateurs)
- ✅ Taille de fichier raisonnable

**Inconvénients** :
- ❌ Perte de qualité (compression avec perte)
- ❌ Pas de transparence
- ❌ Format ancien, moins efficace que WebP/AVIF

**Quand utiliser** :
- Photos de produits
- Images de héros
- Galeries photos
- Arrière-plans photographiques

**Exemple de compression** :
```
photo-originale.jpg   2.5 MB (qualité 100%)
photo-optimisée.jpg   250 KB (qualité 85%)  ← Différence visuelle minime !
```

#### PNG (.png)

**Utilisation** : Logos, icônes, illustrations, images avec transparence

**Avantages** :
- ✅ Sans perte de qualité
- ✅ Support de la transparence (alpha)
- ✅ Parfait pour les graphiques nets

**Inconvénients** :
- ❌ Fichiers très lourds pour les photos
- ❌ Moins efficace que WebP

**Quand utiliser** :
- Logos avec transparence
- Icônes
- Captures d'écran avec texte
- Graphiques et diagrammes

**Types de PNG** :
- **PNG-8** : 256 couleurs maximum (léger)
- **PNG-24** : Millions de couleurs (lourd)

#### WebP (.webp)

**Utilisation** : Tout ! Photos ET graphiques

**Avantages** :
- ✅ 25-35% plus léger que JPEG/PNG
- ✅ Support de la transparence
- ✅ Compression avec et sans perte
- ✅ Supporté par 96% des navigateurs (2025)

**Inconvénients** :
- ❌ Pas de support sur très vieux navigateurs (IE11)

**Comparaison** :
```
photo.jpg     250 KB
photo.webp    165 KB  ← 34% plus léger !

logo.png      80 KB
logo.webp     25 KB   ← 69% plus léger !
```

**Le format du futur** (presque du présent) !

#### AVIF (.avif)

**Utilisation** : Images de haute qualité

**Avantages** :
- ✅ 50% plus léger que JPEG
- ✅ Meilleure qualité que WebP
- ✅ Support de la transparence

**Inconvénients** :
- ❌ Support navigateur limité (88% en 2025)
- ❌ Encodage plus lent

**Quand utiliser** :
- Images critiques de haute qualité
- Toujours avec un fallback WebP/JPEG

#### SVG (.svg)

**Utilisation** : Logos, icônes, illustrations vectorielles

**Avantages** :
- ✅ Infiniment redimensionnable (vectoriel)
- ✅ Fichiers très légers
- ✅ Modifiable avec CSS
- ✅ Parfait pour le responsive

**Inconvénients** :
- ❌ Uniquement pour les graphiques vectoriels
- ❌ Pas pour les photos

**Exemple** :
```
logo.png    80 KB
logo.svg    8 KB   ← 90% plus léger !
```

**Toujours préférer SVG** pour les logos et icônes !

### Tableau comparatif

| Format | Type | Transparence | Taille | Usage principal |
|--------|------|--------------|--------|-----------------|
| **JPEG** | Raster | ❌ | Moyenne | Photos |
| **PNG** | Raster | ✅ | Lourde | Logos, transparence |
| **WebP** | Raster | ✅ | Légère | Tout (moderne) |
| **AVIF** | Raster | ✅ | Très légère | Haute qualité |
| **SVG** | Vectoriel | ✅ | Très légère | Logos, icônes |

---

## Techniques de compression

### Compression avec perte (Lossy)

**Principe** : Réduire la qualité légèrement pour gagner beaucoup en taille

**Pour JPEG/WebP** :

```
Qualité 100% : 2.5 MB  ← Inutilement lourd
Qualité 85%  : 250 KB  ← Sweet spot ! Différence invisible
Qualité 60%  : 120 KB  ← Différence visible
Qualité 30%  : 50 KB   ← Trop dégradé
```

**Recommandation** : Qualité 80-85% pour les photos

**Astuce** : L'œil humain ne voit pas la différence entre 100% et 85% !

### Compression sans perte (Lossless)

**Principe** : Optimiser sans changer l'apparence

**Pour PNG** :
- Supprime les métadonnées inutiles (EXIF, commentaires)
- Optimise la structure du fichier
- Réduit la palette de couleurs si possible

**Gains** : 10-30% de réduction sans perte visuelle

### Outils de compression

#### Outils en ligne (recommandés pour débuter)

**1. Squoosh (Google)**
- URL : https://squoosh.app
- ✅ Gratuit, open source
- ✅ Comparaison visuelle côte à côte
- ✅ Tous les formats (JPEG, PNG, WebP, AVIF)
- ✅ Contrôle précis de la qualité

**Utilisation** :
1. Glissez-déposez votre image
2. Choisissez le format de sortie (WebP recommandé)
3. Ajustez la qualité (80-85 pour photos)
4. Téléchargez le résultat

**2. TinyPNG / TinyJPG**
- URL : https://tinypng.com
- ✅ Super simple
- ✅ Traitement par lot (20 images max)
- ✅ Excellents résultats

**3. Compressor.io**
- URL : https://compressor.io
- ✅ 90% de compression
- ✅ Prévisualisation avant/après

#### Outils desktop

**1. ImageOptim (Mac)**
- Gratuit, open source
- Drag & drop
- Optimisation automatique

**2. FileOptimizer (Windows)**
- Gratuit
- Supporte 200+ formats
- Compression aggressive

**3. GIMP (Multi-plateforme)**
- Gratuit, open source
- Contrôle total
- Export optimisé

#### Outils en ligne de commande

**Pour automatisation/build** :

**ImageMagick** :
```bash
# Convertir en WebP avec qualité 85
convert photo.jpg -quality 85 photo.webp

# Redimensionner et compresser
convert photo.jpg -resize 800x600 -quality 85 photo-small.jpg
```

**cwebp (outil officiel WebP)** :
```bash
cwebp -q 85 photo.jpg -o photo.webp
```

**Sharp (Node.js)** :
```javascript
const sharp = require('sharp');

sharp('photo.jpg')
  .resize(800, 600)
  .webp({ quality: 85 })
  .toFile('photo.webp');
```

---

## Responsive Images (Images adaptatives)

### Le problème

**Scénario classique** :
```html
<img src="photo-4k.jpg" alt="Photo">
```

**Problèmes** :
- 📱 Mobile (360px) télécharge image 4K (3840px) → **gaspillage énorme**
- 🖥️ Desktop retina télécharge la même image que mobile non-retina → **pas optimisé**

### Solution 1 : srcset (tailles multiples)

**Principe** : Fournir plusieurs versions, le navigateur choisit

```html
<img
  src="photo-800.jpg"
  srcset="
    photo-400.jpg 400w,
    photo-800.jpg 800w,
    photo-1200.jpg 1200w,
    photo-1600.jpg 1600w
  "
  sizes="
    (max-width: 600px) 400px,
    (max-width: 1200px) 800px,
    1200px
  "
  alt="Description">
```

**Explication** :

**srcset** : Liste des images disponibles avec leurs largeurs
- `photo-400.jpg 400w` = Image de 400px de large
- `photo-800.jpg 800w` = Image de 800px de large

**sizes** : Indique au navigateur quelle taille d'image afficher selon la viewport
- "Sur mobile (<600px), affiche l'image à 400px"
- "Sur tablette (600-1200px), affiche à 800px"
- "Sur desktop (>1200px), affiche à 1200px"

**Résultat** :
- Mobile 📱 : Télécharge 400px (50 KB) au lieu de 1600px (500 KB)
- Tablette : Télécharge 800px (150 KB)
- Desktop : Télécharge 1200px (300 KB)

### Solution 2 : picture (formats multiples)

**Principe** : Fournir plusieurs formats avec fallback

```html
<picture>
  <!-- Format moderne (AVIF) pour navigateurs récents -->
  <source
    srcset="photo.avif"
    type="image/avif">

  <!-- Format moderne (WebP) pour navigateurs moyens -->
  <source
    srcset="photo.webp"
    type="image/webp">

  <!-- Fallback JPEG pour vieux navigateurs -->
  <img
    src="photo.jpg"
    alt="Description">
</picture>
```

**Fonctionnement** :
1. Navigateur récent : Charge AVIF (le plus léger)
2. Navigateur moyen : Charge WebP
3. Vieux navigateur : Charge JPEG (fallback)

**Gains** :
```
photo.jpg     250 KB  ← Vieux navigateurs
photo.webp    165 KB  ← La plupart des utilisateurs (-34%)
photo.avif    125 KB  ← Navigateurs récents (-50%)
```

### Solution 3 : Combiner srcset + picture

**Le meilleur des deux mondes** :

```html
<picture>
  <!-- AVIF responsive -->
  <source
    type="image/avif"
    srcset="photo-400.avif 400w,
            photo-800.avif 800w,
            photo-1200.avif 1200w"
    sizes="(max-width: 600px) 400px,
           (max-width: 1200px) 800px,
           1200px">

  <!-- WebP responsive -->
  <source
    type="image/webp"
    srcset="photo-400.webp 400w,
            photo-800.webp 800w,
            photo-1200.webp 1200w"
    sizes="(max-width: 600px) 400px,
           (max-width: 1200px) 800px,
           1200px">

  <!-- JPEG responsive (fallback) -->
  <img
    src="photo-800.jpg"
    srcset="photo-400.jpg 400w,
            photo-800.jpg 800w,
            photo-1200.jpg 1200w"
    sizes="(max-width: 600px) 400px,
           (max-width: 1200px) 800px,
           1200px"
    alt="Description">
</picture>
```

**Résultat** : Chaque utilisateur reçoit l'image **optimale** pour son appareil et navigateur !

---

## Lazy Loading (Chargement différé)

### Le problème

**Scénario** : Page avec 50 images, l'utilisateur ne voit que les 3 premières

**Sans lazy loading** :
- Télécharge les 50 images au chargement
- Gaspille de la bande passante
- Ralentit le chargement initial

### Solution native (loading="lazy")

```html
<!-- ❌ MAUVAIS : Charge immédiatement -->
<img src="photo.jpg" alt="Photo">

<!-- ✅ BON : Charge quand visible -->
<img src="photo.jpg" alt="Photo" loading="lazy">
```

**Fonctionnement** :
1. Image hors de l'écran : pas chargée
2. Utilisateur scroll vers l'image : chargement déclenché
3. Image apparaît progressivement

**Support** : 97% des navigateurs (2025)

### Exceptions importantes

**NE PAS lazy-load** :
- Images "above the fold" (visibles sans scroller)
- Logo
- Image hero
- Première image de galerie

```html
<!-- ✅ Image visible immédiatement : pas de lazy -->
<img src="hero.jpg" alt="Hero" class="hero-image">

<!-- ✅ Images en bas de page : lazy loading -->
<img src="gallery-1.jpg" alt="Photo 1" loading="lazy">
<img src="gallery-2.jpg" alt="Photo 2" loading="lazy">
```

### Placeholder pour éviter le layout shift

**Problème** :
```html
<!-- ❌ Pas de dimensions = layout shift -->
<img src="photo.jpg" loading="lazy">
```
→ L'image charge → La page "saute" → Mauvaise UX (CLS élevé)

**Solution** :
```html
<!-- ✅ Dimensions définies = espace réservé -->
<img
  src="photo.jpg"
  width="800"
  height="600"
  loading="lazy"
  alt="Photo">
```

**Avec CSS aspect-ratio** :
```css
img {
  width: 100%;
  height: auto;
  aspect-ratio: 16 / 9;
}
```

```html
<img
  src="photo.jpg"
  loading="lazy"
  style="aspect-ratio: 16/9"
  alt="Photo">
```

---

## Optimisation du CSS

### Problèmes courants

**1. CSS trop volumineux**
```css
/* style.css - 250 KB */
/* Beaucoup de règles non utilisées */
```

**2. CSS bloquant**
```html
<!-- Bloque l'affichage de la page -->
<link rel="stylesheet" href="style.css">
```

**3. CSS non minifié**
```css
/* Avec espaces et commentaires */
.button {
  background-color: blue;
  padding: 10px 20px;
}
```

### Solutions

#### 1. Minification

**Principe** : Supprimer espaces, commentaires, optimiser

**Avant minification** (10 KB) :
```css
/* Bouton principal */
.button {
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}
```

**Après minification** (6 KB) :
```css
.button{background-color:#3498db;color:#fff;padding:10px 20px;border-radius:5px}
```

**Gain** : 40% de réduction

**Outils** :
- **cssnano** : Plugin PostCSS
- **clean-css** : Ligne de commande
- **CSS Minifier** : En ligne (https://cssminifier.com)

**Build avec Webpack/Vite** :
```javascript
// Minification automatique en production
module.exports = {
  mode: 'production', // Active la minification
};
```

#### 2. Suppression du CSS non utilisé

**Problème** : Frameworks CSS (Bootstrap, Tailwind) incluent beaucoup de code non utilisé

**Exemple** :
```
bootstrap.css    150 KB  (toutes les classes)
Utilisation :    20 KB   (seulement 13% utilisé !)
```

**Solution avec PurgeCSS** :

```javascript
// Configuration PostCSS
module.exports = {
  plugins: [
    require('@fullhuman/postcss-purgecss')({
      content: ['./src/**/*.html', './src/**/*.js'],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || []
    })
  ]
}
```

**Résultat** :
```
Avant :  150 KB
Après :   20 KB  ← 87% de réduction !
```

#### 3. CSS critique inline

**Principe** : Inclure le CSS essentiel directement dans le HTML

```html
<!DOCTYPE html>
<html>
<head>
  <!-- CSS critique inline (above-the-fold) -->
  <style>
    body { margin: 0; font-family: sans-serif; }
    .hero { height: 100vh; background: blue; }
    .header { padding: 20px; }
  </style>

  <!-- Reste du CSS en async -->
  <link rel="stylesheet" href="style.css" media="print" onload="this.media='all'">
</head>
<body>
  <!-- Contenu -->
</body>
</html>
```

**Avantages** :
- Affichage immédiat (pas de requête)
- Pas de blocage
- Amélioration du FCP

**Outils** :
- **Critical** (npm package)
- **Critters** (Angular)
- Intégré dans Next.js, Gatsby

#### 4. Précharger les fonts

```html
<!-- ❌ MAUVAIS : Font charge tard -->
<link rel="stylesheet" href="fonts.css">

<!-- ✅ BON : Preload + font-display -->
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>

<style>
  @font-face {
    font-family: 'MyFont';
    src: url('font.woff2') format('woff2');
    font-display: swap; /* Affiche fallback puis swap */
  }
</style>
```

---

## Optimisation du JavaScript

### Problèmes courants

**1. Fichiers trop volumineux**
```
bundle.js    1.2 MB  ← Trop lourd !
```

**2. Code bloquant**
```html
<!-- Bloque l'affichage -->
<script src="script.js"></script>
```

**3. Code non utilisé**
```javascript
// Importe toute la bibliothèque
import _ from 'lodash'; // 70 KB
// Mais utilise seulement une fonction
_.uniq(array);
```

### Solutions

#### 1. Minification et compression

**Minification** :

**Avant** (20 KB) :
```javascript
function calculateTotal(items) {
  let total = 0;
  for (let item of items) {
    total += item.price * item.quantity;
  }
  return total;
}
```

**Après** (8 KB) :
```javascript
function calculateTotal(e){let t=0;for(let a of e)t+=a.price*a.quantity;return t}
```

**Outils** :
- **Terser** : Le standard (utilisé par Webpack, Vite)
- **UglifyJS** : Plus ancien mais efficace
- Automatique dans les bundlers modernes

#### 2. Tree Shaking

**Principe** : Supprimer le code non utilisé

```javascript
// ❌ MAUVAIS : Importe tout
import _ from 'lodash'; // 70 KB
const result = _.uniq(array);

// ✅ BON : Importe uniquement ce qui est utilisé
import uniq from 'lodash/uniq'; // 2 KB
const result = uniq(array);
```

**Configuration Webpack** :
```javascript
module.exports = {
  mode: 'production',
  optimization: {
    usedExports: true, // Active tree-shaking
  }
};
```

#### 3. Code Splitting

**Principe** : Diviser le code en petits morceaux chargés à la demande

**Avant** :
```
bundle.js    1.2 MB  ← Tout chargé d'un coup
```

**Après** :
```
main.js      200 KB  ← Charge au démarrage
admin.js     300 KB  ← Charge si page admin
chart.js     150 KB  ← Charge si graphique affiché
```

**Avec import dynamique** :
```javascript
// ❌ MAUVAIS : Charge toujours
import Chart from 'chart.js';
showChart(); // Utilise Chart

// ✅ BON : Charge à la demande
button.addEventListener('click', async () => {
  const Chart = await import('chart.js');
  showChart(Chart); // Charge seulement si bouton cliqué
});
```

#### 4. defer et async

**Sans attribut** :
```html
<!-- ❌ Bloque l'affichage -->
<script src="script.js"></script>
```
→ HTML parsing stoppé → Script téléchargé et exécuté → HTML parsing reprend

**Avec defer** :
```html
<!-- ✅ Télécharge en parallèle, exécute après parsing -->
<script src="script.js" defer></script>
```
→ HTML parsing continue → Script téléchargé en parallèle → Exécute après parsing complet

**Avec async** :
```html
<!-- ✅ Télécharge et exécute dès que prêt -->
<script src="analytics.js" async></script>
```
→ HTML parsing continue → Script exécuté dès téléchargé

**Quand utiliser quoi** :

| Attribut | Quand | Exemple |
|----------|-------|---------|
| **Aucun** | Scripts critiques (rare) | Polyfills essentiels |
| **defer** | Scripts qui manipulent le DOM | Script principal de l'app |
| **async** | Scripts indépendants | Analytics, publicité |

---

## Optimisation des polices (Fonts)

### Problèmes courants

**1. Trop de variantes**
```css
/* ❌ Charge 8 fichiers ! */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap');
```

**2. FOIT/FOUT**
- **FOIT** (Flash of Invisible Text) : Texte invisible pendant le chargement
- **FOUT** (Flash of Unstyled Text) : Texte en fallback puis swap brutal

### Solutions

#### 1. Limiter les variantes

```css
/* ❌ MAUVAIS : 6 variantes = 600 KB */
font-weight: 100, 300, 400, 500, 700, 900

/* ✅ BON : 2 variantes = 200 KB */
font-weight: 400, 700  /* Normal et gras suffisent */
```

#### 2. Utiliser font-display

```css
@font-face {
  font-family: 'MyFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* ← Important ! */
}
```

**Options font-display** :
- `swap` : Affiche fallback immédiatement, swap quand prêt (recommandé)
- `optional` : Utilise la font si charge rapidement, sinon fallback
- `block` : Attend 3s max, puis fallback (FOIT)
- `fallback` : Compromis entre swap et block

#### 3. Précharger les fonts

```html
<link
  rel="preload"
  href="font.woff2"
  as="font"
  type="font/woff2"
  crossorigin>
```

#### 4. Sous-ensemble (Subsetting)

**Principe** : Inclure uniquement les caractères utilisés

```
font-complete.woff2    120 KB  (tous les caractères)
font-latin.woff2        40 KB  (seulement latin)
font-custom.woff2       15 KB  (seulement les caractères de votre site)
```

**Outils** :
- **FontSquirrel Webfont Generator**
- **glyphhanger** (npm)

#### 5. Utiliser system fonts

**La plus rapide** : Pas de téléchargement !

```css
body {
  font-family:
    system-ui,
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI",
    Roboto,
    sans-serif;
}
```

**Avantages** :
- ⚡ Instantané (0 KB)
- 👁️ Familier pour l'utilisateur
- 📱 Optimisé pour chaque OS

---

## Optimisation des vidéos

### Problèmes

**Vidéo non optimisée** :
```html
<video src="video-4k.mp4"></video>
<!-- 500 MB à télécharger ! -->
```

### Solutions

#### 1. Compression

**Utiliser un codec moderne** :
- H.264 : Bon support (ancien)
- H.265 (HEVC) : 50% plus léger que H.264
- VP9 : Gratuit, bon (Google)
- AV1 : Futur, excellent (pas encore bien supporté)

**Outils** :
- **HandBrake** : Interface graphique
- **FFmpeg** : Ligne de commande

```bash
# Compresser avec FFmpeg
ffmpeg -i video.mp4 -c:v libx264 -crf 23 video-compressed.mp4
```

#### 2. Formats multiples

```html
<video controls>
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
  Votre navigateur ne supporte pas la vidéo.
</video>
```

#### 3. Lazy loading

```html
<video
  src="video.mp4"
  preload="none"  ← Ne charge pas automatiquement
  controls>
</video>
```

**Options preload** :
- `none` : Ne précharge rien (recommandé)
- `metadata` : Précharge seulement les métadonnées
- `auto` : Précharge la vidéo entière

#### 4. Alternative : Poster et lecture à la demande

```html
<video
  poster="thumbnail.jpg"  ← Image d'aperçu
  preload="none"
  controls>
  <source src="video.mp4">
</video>
```

#### 5. Considérer YouTube/Vimeo

**Pour vidéos lourdes** :
- Hébergement gratuit
- Optimisation automatique
- Streaming adaptatif
- CDN mondial

```html
<iframe
  src="https://www.youtube.com/embed/VIDEO_ID"
  loading="lazy"
  title="Titre de la vidéo">
</iframe>
```

---

## CDN (Content Delivery Network)

### Qu'est-ce qu'un CDN ?

**Principe** : Distribuer vos ressources sur des serveurs mondiaux

**Sans CDN** :
```
Utilisateur (Paris)  →  5000 km  →  Serveur (New York)
                        Latence : 150ms
```

**Avec CDN** :
```
Utilisateur (Paris)  →  50 km  →  Serveur CDN (Paris)
                        Latence : 10ms
```

### Avantages

- ⚡ **Latence réduite** : Serveur proche de l'utilisateur
- 🚀 **Bande passante** : Serveurs puissants
- 💾 **Cache** : Ressources mises en cache
- 🛡️ **Protection** : DDoS protection
- 📊 **Scalabilité** : Gère les pics de trafic

### CDN populaires

**Gratuits** :
- **Cloudflare** : Le plus populaire, excellent plan gratuit
- **jsDelivr** : Pour bibliothèques JavaScript/CSS
- **Vercel** : Hébergement + CDN gratuit

**Payants** :
- **AWS CloudFront** : Intégré AWS
- **Google Cloud CDN** : Intégré GCP
- **Fastly** : Ultra-rapide, premium

### Utilisation basique

**Au lieu de** :
```html
<script src="/js/script.js"></script>
<link rel="stylesheet" href="/css/style.css">
```

**Avec CDN** :
```html
<script src="https://cdn.example.com/js/script.js"></script>
<link rel="stylesheet" href="https://cdn.example.com/css/style.css">
```

**Pour bibliothèques** :
```html
<!-- ❌ Local -->
<script src="/node_modules/react/react.js"></script>

<!-- ✅ CDN -->
<script src="https://cdn.jsdelivr.net/npm/react@18/umd/react.production.min.js"></script>
```

---

## Cache navigateur

### Principe

**Sans cache** :
```
Visite 1 : Télécharge 2 MB
Visite 2 : Télécharge 2 MB  ← Tout retéléchargé !
Visite 3 : Télécharge 2 MB
```

**Avec cache** :
```
Visite 1 : Télécharge 2 MB
Visite 2 : Cache (0 MB)      ← Instantané !
Visite 3 : Cache (0 MB)
```

### Configuration

**Headers HTTP à configurer** :

```
Cache-Control: max-age=31536000, immutable
```

**Signification** :
- `max-age=31536000` : Cache pendant 1 an
- `immutable` : Ne jamais revalider

**Configuration Apache (.htaccess)** :
```apache
<IfModule mod_expires.c>
  ExpiresActive On

  # Images : 1 an
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/webp "access plus 1 year"

  # CSS/JS : 1 an
  ExpiresByType text/css "access plus 1 year"
  ExpiresByType application/javascript "access plus 1 year"

  # HTML : Pas de cache (contenu dynamique)
  ExpiresByType text/html "access plus 0 seconds"
</IfModule>
```

**Configuration Nginx** :
```nginx
location ~* \.(jpg|jpeg|png|webp|css|js)$ {
  expires 1y;
  add_header Cache-Control "public, immutable";
}

location ~* \.(html)$ {
  expires -1;
  add_header Cache-Control "no-cache, no-store, must-revalidate";
}
```

### Stratégie de cache

**Fichiers avec hash** :
```
style.a3f2c1.css    ← Hash change si fichier modifié
script.7b9e4d.js
```

**Avantage** : Cache agressif possible (1 an) sans risque

**Build avec Webpack** :
```javascript
output: {
  filename: '[name].[contenthash].js',
  // Génère : main.a3f2c1b4.js
}
```

---

## Checklist d'optimisation complète

### ✅ Images

- [ ] Converties en WebP (ou AVIF)
- [ ] Compressées (qualité 80-85%)
- [ ] Responsive (srcset + sizes)
- [ ] Lazy loading activé (sauf above-the-fold)
- [ ] Dimensions width/height définies
- [ ] Logos/icônes en SVG

### ✅ CSS

- [ ] Minifié en production
- [ ] CSS non utilisé supprimé (PurgeCSS)
- [ ] CSS critique inline
- [ ] Reste du CSS en async
- [ ] Fonts optimisées (font-display: swap)

### ✅ JavaScript

- [ ] Minifié en production
- [ ] Tree-shaking activé
- [ ] Code splitting utilisé
- [ ] Scripts avec defer/async
- [ ] Import dynamique pour code non critique

### ✅ Fonts

- [ ] Nombre de variantes limité (2-3 max)
- [ ] font-display: swap configuré
- [ ] Fonts préchargées (preload)
- [ ] Sous-ensemble si possible
- [ ] Ou system fonts considérées

### ✅ Vidéos

- [ ] Compressées
- [ ] Formats multiples (WebM + MP4)
- [ ] preload="none"
- [ ] Poster défini
- [ ] YouTube/Vimeo considéré pour grandes vidéos

### ✅ Infrastructure

- [ ] CDN configuré
- [ ] Cache navigateur activé
- [ ] Compression gzip/brotli activée
- [ ] HTTP/2 activé
- [ ] HTTPS activé

---

## Mesurer l'impact

### Avant optimisation

1. **Lighthouse** : Notez les scores
2. **Network** : Notez taille totale et temps
3. **Export HAR** : Sauvegardez pour comparaison

### Après optimisation

1. **Relancez Lighthouse** : Comparez les scores
2. **Vérifiez Network** : Vérifiez la réduction
3. **Testez en réel** : Sur vrai mobile en 3G

### Métriques à suivre

**Avant** :
```
Total : 5.2 MB
Temps : 12s (3G)
Performance Score : 45
```

**Après** :
```
Total : 680 KB (-87%)
Temps : 2.5s (-79%)
Performance Score : 92 (+47)
```

---

## Outils récapitulatifs

### Analyse

- **Lighthouse** : Audit global
- **PageSpeed Insights** : Lighthouse + données réelles
- **WebPageTest** : Test approfondi multi-locations

### Optimisation images

- **Squoosh** : Compression manuelle
- **TinyPNG** : Batch automatique
- **ImageOptim** : Desktop (Mac)
- **Sharp** : Automatisation (Node.js)

### Optimisation code

- **Webpack Bundle Analyzer** : Visualiser le bundle
- **PurgeCSS** : Supprimer CSS non utilisé
- **Terser** : Minifier JavaScript

### Fonts

- **FontSquirrel** : Webfont generator
- **Google Fonts** : Fonts gratuites optimisées
- **glyphhanger** : Subsetting automatique

---

## Points clés à retenir

🖼️ **Images = 50-70% du poids d'une page**
- Convertir en WebP/AVIF
- Compresser (qualité 80-85%)
- Responsive images (srcset)
- Lazy loading

📦 **Minifier tout**
- CSS : cssnano, clean-css
- JS : Terser, UglifyJS
- HTML : html-minifier

🎯 **Code splitting**
- Diviser le JavaScript
- Import dynamique
- Charger à la demande

🚀 **CDN = Latence réduite**
- Serveurs géographiquement proches
- Cache automatique
- Bande passante élevée

💾 **Cache navigateur**
- Configuration aggressive (1 an)
- Fichiers avec hash
- Headers Cache-Control

⚡ **Quick wins**
1. Compresser les images → -60%
2. Activer gzip → -70%
3. Lazy loading → Chargement initial -40%
4. Minifier CSS/JS → -40%

---

## Pour aller plus loin

L'optimisation est un processus continu, pas une tâche ponctuelle. Intégrez ces pratiques dans votre workflow de développement dès le début !

**Mantra** : "Un site rapide n'est pas un luxe, c'est un standard." 🚀

---

> 💡 **Citation de Steve Souders** (expert performance web) :
> *"80-90% of the end-user response time is spent on the frontend. Start there."*
>
> Et l'optimisation des images/ressources est le meilleur point de départ ! 🎯

⏭️ [Validation et qualité du code](/07-debugging-et-outils-avances/03-validation-qualite/README.md)
