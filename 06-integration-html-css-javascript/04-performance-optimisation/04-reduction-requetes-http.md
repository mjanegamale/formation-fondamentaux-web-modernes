🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.4.4 - Réduction des requêtes HTTP

## Qu'est-ce qu'une requête HTTP ?

Quand vous visitez un site web, votre navigateur doit **télécharger** tous les éléments de la page :
- Le fichier HTML
- Les fichiers CSS
- Les fichiers JavaScript
- Les images
- Les polices
- Les vidéos, etc.

Chaque téléchargement nécessite une **requête HTTP** (Hypertext Transfer Protocol).

### Visualisation d'une page web

```
Page web complète = 1 HTML + 3 CSS + 5 JS + 20 images + 2 polices
                  = 31 requêtes HTTP
```

**Plus vous avez de fichiers, plus vous avez de requêtes.**

---

## Pourquoi réduire les requêtes HTTP ?

### 1. **Le problème de la latence** ⏱️

Chaque requête HTTP a un **coût en temps**, même si le fichier est petit :

```
Temps pour une requête = Latence + Temps de téléchargement

Exemple pour un fichier de 5 KB :
- Latence (aller-retour serveur) : 100 ms
- Téléchargement du fichier : 5 ms
→ Total : 105 ms

Le temps de latence est souvent plus long que le téléchargement !
```

**Problème** : Si vous avez 50 requêtes, même pour de petits fichiers, la latence s'accumule !

---

### 2. **L'overhead HTTP** 📊

Chaque requête HTTP inclut :
- **Headers** (en-têtes) : ~500-800 octets par requête
- **Cookies** : peuvent ajouter 1-2 KB
- **Négociation SSL** (HTTPS) : ~2 KB

```
Exemple concret :
10 petites images de 2 KB chacune = 20 KB de données
+ Headers pour 10 requêtes = ~8 KB
+ Cookies = ~10 KB
→ Total transféré : 38 KB (90% de plus !)
```

---

### 3. **Limites de connexions simultanées** 🔌

Les navigateurs limitent le nombre de connexions simultanées par domaine :

```
HTTP/1.1 :
- 6 connexions simultanées maximum par domaine
- 100 fichiers = 100 ÷ 6 = ~17 vagues de téléchargements

HTTP/2 :
- Multiplexage : plusieurs fichiers par connexion
- Limite moins problématique, mais overhead reste présent
```

**Conséquence** : Plus de requêtes = chargement plus lent, même avec HTTP/2.

---

### 4. **Impact sur les performances** 📉

```
Site A : 150 requêtes HTTP
Temps de chargement : 8 secondes

Site B : 30 requêtes HTTP
Temps de chargement : 2 secondes

Amélioration : 75% plus rapide !
```

**Chaque requête économisée compte.**

---

## Mesurer vos requêtes HTTP

### Avec les DevTools (Network Tab) 🔍

```
1. Ouvrir Chrome DevTools (F12)
2. Onglet "Network"
3. Recharger la page (Ctrl/Cmd + R)
4. Observer :
   - Nombre total de requêtes (en bas)
   - Taille totale transférée
   - Temps de chargement total
```

**Exemple de résultat** :
```
147 requests
2.3 MB transferred
3.8 MB resources
Finish: 4.2s
DOMContentLoaded: 1.8s
Load: 3.5s
```

---

### Analyse par type de fichier

Dans Network, filtrez par type :
- **Doc** : HTML
- **CSS** : Feuilles de style
- **JS** : JavaScript
- **Img** : Images
- **Font** : Polices
- **Other** : Autres ressources

**Objectif** : Identifier les types de fichiers qui génèrent le plus de requêtes.

---

### Objectifs recommandés 🎯

| Métrique | Bon | Excellent |
|----------|-----|-----------|
| **Nombre de requêtes** | < 50 | < 25 |
| **Taille transférée** | < 1 MB | < 500 KB |
| **Temps de chargement** | < 3s | < 1.5s |

**Note** : Ces chiffres dépendent du type de site (blog vs application complexe).

---

## Techniques de réduction des requêtes

### 1. Concaténation de fichiers (Bundling) 📦

**Principe** : Regrouper plusieurs fichiers en un seul.

#### CSS - Avant optimisation ❌

```html
<!-- 5 requêtes CSS -->
<link rel="stylesheet" href="reset.css">
<link rel="stylesheet" href="typography.css">
<link rel="stylesheet" href="layout.css">
<link rel="stylesheet" href="components.css">
<link rel="stylesheet" href="responsive.css">
```

**Total** : 5 requêtes HTTP

---

#### CSS - Après optimisation ✅

```html
<!-- 1 seule requête CSS -->
<link rel="stylesheet" href="styles.bundle.css">
```

**Total** : 1 requête HTTP
**Économie** : 4 requêtes (80%)

---

#### JavaScript - Avant optimisation ❌

```html
<!-- 6 requêtes JavaScript -->
<script src="utils.js" defer></script>
<script src="helpers.js" defer></script>
<script src="validators.js" defer></script>
<script src="api.js" defer></script>
<script src="ui.js" defer></script>
<script src="main.js" defer></script>
```

**Total** : 6 requêtes HTTP

---

#### JavaScript - Après optimisation ✅

```html
<!-- 1 seule requête JavaScript -->
<script src="app.bundle.js" defer></script>
```

**Total** : 1 requête HTTP
**Économie** : 5 requêtes (83%)

---

#### Comment bundler ?

**Méthode manuelle** (petits projets) :
```bash
# Concaténer manuellement avec cat (Linux/Mac)
cat file1.css file2.css file3.css > bundle.css

# Ou avec copy (Windows)
copy file1.css + file2.css + file3.css bundle.css
```

**Méthode automatisée** (recommandée) :
- **Vite** (moderne, rapide)
- **Webpack** (populaire, complet)
- **Rollup** (pour bibliothèques)
- **Parcel** (zero-config)

**Exemple avec Vite** :
```bash
npm run build
# Génère automatiquement des bundles optimisés
```

---

### 2. Sprites CSS 🖼️

**Principe** : Combiner plusieurs petites images en une seule grande image.

#### Avant - Icônes séparées ❌

```html
<!-- 10 requêtes pour 10 icônes -->
<img src="icon-home.png" alt="Accueil">
<img src="icon-search.png" alt="Recherche">
<img src="icon-user.png" alt="Utilisateur">
<img src="icon-cart.png" alt="Panier">
<!-- ... 6 autres icônes ... -->
```

**Total** : 10 requêtes HTTP

---

#### Après - Sprite CSS ✅

```css
/* Une seule image contient toutes les icônes */
.icon {
  background-image: url('sprite.png');
  background-repeat: no-repeat;
  display: inline-block;
  width: 32px;
  height: 32px;
}

/* Position de chaque icône dans le sprite */
.icon-home { background-position: 0 0; }
.icon-search { background-position: -32px 0; }
.icon-user { background-position: -64px 0; }
.icon-cart { background-position: -96px 0; }
/* ... */
```

```html
<!-- 1 seule requête pour toutes les icônes -->
<span class="icon icon-home"></span>
<span class="icon icon-search"></span>
<span class="icon icon-user"></span>
<span class="icon icon-cart"></span>
```

**Total** : 1 requête HTTP
**Économie** : 9 requêtes (90%)

---

#### Outils pour créer des sprites

- **SpritePad** : https://wearekiss.com/spritepad
- **CSS Sprite Generator** : https://www.toptal.com/developers/css/sprite-generator
- **Spritesmith** (automatisé avec Gulp/Webpack)

---

### 3. SVG Sprites (moderne) 🎨

Pour les icônes, les **SVG sprites** sont une alternative moderne et supérieure.

#### Créer un sprite SVG

```html
<!-- sprite.svg - Un seul fichier SVG -->
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">

  <!-- Icône home -->
  <symbol id="icon-home" viewBox="0 0 24 24">
    <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
  </symbol>

  <!-- Icône search -->
  <symbol id="icon-search" viewBox="0 0 24 24">
    <path d="M15.5 14h-.79l-.28-.27A6.47 6.47 0 0016 9.5 6.5 6.5 0 109.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
  </symbol>

  <!-- Icône user -->
  <symbol id="icon-user" viewBox="0 0 24 24">
    <path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
  </symbol>

</svg>
```

#### Utilisation dans le HTML

```html
<!-- Inclure le sprite (inline ou externe) -->
<svg style="display: none;">
  <!-- Contenu du sprite ici ou chargé via AJAX -->
</svg>

<!-- Utiliser les icônes -->
<svg class="icon" width="24" height="24">
  <use href="#icon-home"></use>
</svg>

<svg class="icon" width="24" height="24">
  <use href="#icon-search"></use>
</svg>

<svg class="icon" width="24" height="24">
  <use href="#icon-user"></use>
</svg>
```

**Avantages des SVG sprites** :
- ✅ 1 seule requête HTTP
- ✅ Vectoriel (qualité parfaite à toute taille)
- ✅ Stylable en CSS (couleur, taille)
- ✅ Plus léger que PNG
- ✅ Accessible

---

### 4. Icon Fonts (alternative) 🔤

Les **icon fonts** (Font Awesome, Material Icons) regroupent des icônes dans une police.

```html
<!-- 1 requête pour la police -->
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">

<!-- Utilisation -->
<i class="material-icons">home</i>
<i class="material-icons">search</i>
<i class="material-icons">person</i>
```

**Avantages** :
- ✅ 1 seule requête
- ✅ Facile à utiliser
- ✅ Stylable en CSS

**Inconvénients** :
- ⚠️ Peut être lourd (toute la police téléchargée)
- ⚠️ Moins flexible que SVG
- ⚠️ Problèmes d'accessibilité possibles

**Recommandation** : Préférez les SVG sprites pour plus de contrôle.

---

### 5. Data URIs (Inline) 📎

**Principe** : Encoder une image en base64 directement dans le CSS/HTML.

#### Image externe (requête HTTP) ❌

```css
.logo {
  background-image: url('logo.png');
}
```

**Total** : 1 requête HTTP

---

#### Image inline avec Data URI ✅

```css
.logo {
  background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUA...');
  /* Image encodée en base64 */
}
```

**Total** : 0 requête HTTP (l'image est dans le CSS)

---

#### Quand utiliser les Data URIs ?

**✅ À utiliser pour** :
- Très petites images (< 2 KB)
- Icônes critiques
- Images qui ne changent jamais

**❌ À éviter pour** :
- Grandes images (> 10 KB)
- Images qui changent souvent
- Images utilisées sur plusieurs pages

**Pourquoi ?**
- Data URI augmente la taille du CSS de ~33% (base64 encoding)
- Le CSS ne peut pas être mis en cache séparément de l'image

---

#### Générer un Data URI

**Outil en ligne** :
- https://www.base64-image.de/

**Avec Node.js** :
```javascript
const fs = require('fs');
const imageBuffer = fs.readFileSync('icon.png');
const base64Image = imageBuffer.toString('base64');
const dataURI = `data:image/png;base64,${base64Image}`;
console.log(dataURI);
```

---

### 6. Inlining du CSS/JS critique 💉

**Principe** : Placer le CSS/JS critique directement dans le HTML (inline) pour éviter des requêtes supplémentaires.

#### CSS critique inline

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- CSS critique inline (pas de requête HTTP) -->
  <style>
    /* Styles nécessaires pour le contenu "above the fold" */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }

    .header {
      background: #333;
      color: white;
      padding: 1rem;
    }

    .hero {
      height: 400px;
      background: url('data:image/jpeg;base64,...') center/cover;
    }
  </style>

  <!-- CSS complet chargé après (non bloquant) -->
  <link rel="stylesheet" href="styles.css" media="print" onload="this.media='all'">
</head>
<body>
  <header class="header">
    <h1>Mon Site</h1>
  </header>

  <div class="hero">
    <!-- Contenu visible immédiatement -->
  </div>
</body>
</html>
```

**Avantage** : Le contenu "above the fold" s'affiche instantanément sans attendre le CSS externe.

---

#### JavaScript critique inline

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- Configuration critique inline -->
  <script>
    // Configuration nécessaire immédiatement
    window.APP_CONFIG = {
      apiUrl: 'https://api.example.com',
      version: '1.0.0'
    };

    // Appliquer le thème sauvegardé
    const theme = localStorage.getItem('theme') || 'light';
    document.documentElement.setAttribute('data-theme', theme);
  </script>

  <!-- JavaScript principal en defer -->
  <script src="app.js" defer></script>
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

---

#### ⚠️ Attention avec l'inlining

**À faire** :
- ✅ Inline uniquement le code critique (< 14 KB recommandé)
- ✅ Garder le reste en fichiers externes (pour le cache)

**À éviter** :
- ❌ Inline de gros CSS/JS complets
- ❌ Code inline dupliqué sur toutes les pages

---

### 7. Lazy Loading (Chargement différé) ⏱️

**Principe** : Ne charger les ressources que quand elles deviennent nécessaires.

#### Images (lazy loading natif)

```html
<!-- Images hors écran : chargées seulement au scroll -->
<img src="image1.jpg" alt="..." loading="lazy">
<img src="image2.jpg" alt="..." loading="lazy">
<img src="image3.jpg" alt="..." loading="lazy">
<!-- ... 50 autres images ... -->
```

**Économie** : Si l'utilisateur ne scrolle pas, les images ne sont jamais chargées !

**Avant** : 50 requêtes HTTP au chargement
**Après** : 5-10 requêtes (seulement les images visibles)

---

#### JavaScript (lazy loading)

```html
<!-- Script chargé uniquement quand nécessaire -->
<button id="open-modal">Ouvrir la modale</button>

<script>
  document.getElementById('open-modal').addEventListener('click', async () => {
    // Charge le script seulement au clic
    const { openModal } = await import('./modal.js');
    openModal();
  });
</script>
```

**Économie** : Le script modal.js n'est chargé que si l'utilisateur clique sur le bouton.

---

### 8. Utiliser du CSS au lieu d'images 🎨

**Principe** : Créer des effets visuels en pur CSS plutôt qu'avec des images.

#### Dégradés - Avant ❌

```html
<!-- Image de dégradé : 1 requête HTTP -->
<div style="background-image: url('gradient.png');"></div>
```

#### Dégradés - Après ✅

```html
<!-- Dégradé en CSS : 0 requête HTTP -->
<div style="background: linear-gradient(to right, #667eea 0%, #764ba2 100%);"></div>
```

---

#### Formes simples - CSS vs Images

**Triangles, cercles, carrés arrondis** :
```css
/* Triangle en CSS (0 requête) */
.triangle {
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid #007bff;
}

/* Cercle en CSS */
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: #007bff;
}
```

**Économie** : 0 requête vs 1 requête par forme.

---

#### Icônes simples en CSS

```css
/* Icône "hamburger" en CSS */
.menu-icon {
  width: 30px;
  height: 3px;
  background: black;
  position: relative;
}

.menu-icon::before,
.menu-icon::after {
  content: '';
  position: absolute;
  width: 30px;
  height: 3px;
  background: black;
}

.menu-icon::before { top: -10px; }
.menu-icon::after { top: 10px; }
```

**Économie** : 1 requête économisée.

---

### 9. Préchargement stratégique (Preload/Prefetch) 🔮

**Preload** : Charger une ressource critique en priorité.

```html
<head>
  <!-- Précharge la police critique -->
  <link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>

  <!-- Précharge l'image hero -->
  <link rel="preload" href="hero.jpg" as="image">

  <!-- Utilisation normale après -->
  <link rel="stylesheet" href="styles.css">
</head>
```

**Avantage** : Les ressources critiques commencent à charger plus tôt.

---

**Prefetch** : Charger une ressource qui sera probablement nécessaire.

```html
<head>
  <!-- Précharge la page suivante probable -->
  <link rel="prefetch" href="page2.html">

  <!-- Précharge des images qui seront vues plus tard -->
  <link rel="prefetch" href="gallery-image-1.jpg">
</head>
```

**Avantage** : Navigation plus rapide vers les pages suivantes.

---

### 10. CDN et domaines multiples 🌐

**Principe** : Utiliser des CDN pour distribuer la charge.

#### Sans CDN ❌

```html
<!-- Toutes les ressources sur votre domaine -->
<img src="https://monsite.com/images/photo1.jpg">
<img src="https://monsite.com/images/photo2.jpg">
<img src="https://monsite.com/images/photo3.jpg">
<!-- ... -->
```

**Limite** : 6 connexions simultanées vers monsite.com

---

#### Avec CDN ✅

```html
<!-- Images sur un CDN -->
<img src="https://cdn.monsite.com/images/photo1.jpg">
<img src="https://cdn.monsite.com/images/photo2.jpg">
<img src="https://cdn.monsite.com/images/photo3.jpg">
<!-- ... -->
```

**Avantage** :
- 6 connexions vers monsite.com
- 6 connexions vers cdn.monsite.com
- = 12 connexions simultanées au total

**CDN populaires** :
- Cloudflare
- Amazon CloudFront
- Google Cloud CDN
- Netlify/Vercel (automatique)

---

## HTTP/2 et son impact 🚀

### Différences HTTP/1.1 vs HTTP/2

#### HTTP/1.1 (ancien)
- 1 requête par connexion à la fois
- 6 connexions max par domaine
- Overhead important par requête

**Stratégie** : Minimiser au maximum les requêtes (bundling agressif).

---

#### HTTP/2 (moderne)
- **Multiplexing** : plusieurs requêtes simultanées par connexion
- **Compression des headers** : moins d'overhead
- **Server Push** : le serveur peut envoyer des ressources avant demande

**Stratégie** : Bundling moins critique, mais réduction des requêtes toujours bénéfique.

---

### HTTP/2 ne résout pas tout

Même avec HTTP/2, réduire les requêtes reste important :

**Raisons** :
1. **Overhead TLS** : chaque ressource a un coût
2. **Processing** : le navigateur doit traiter chaque fichier
3. **Cache** : plus de fichiers = gestion du cache plus complexe
4. **Mobile** : connexions moins stables

**Conclusion** : HTTP/2 réduit l'impact négatif, mais ne l'élimine pas.

---

## Stratégies par type de site

### Site vitrine / Blog 📝

**Objectif** : < 30 requêtes

**Stratégie** :
```
1. Bundle CSS (1 fichier)
2. Bundle JS (1 fichier)
3. Optimiser images (10-15 requêtes max)
4. SVG sprites pour icônes (1 requête)
5. Lazy loading pour images bas de page
```

**Résultat typique** : 20-25 requêtes

---

### E-commerce 🛒

**Objectif** : < 50 requêtes

**Stratégie** :
```
1. Bundle CSS/JS (2-3 bundles)
2. Lazy loading des images produits
3. CDN pour toutes les images
4. Préchargement des images de la première page
5. Sprites CSS pour icônes/badges
```

**Résultat typique** : 40-50 requêtes

---

### Application web (SPA) 💻

**Objectif** : < 40 requêtes (chargement initial)

**Stratégie** :
```
1. Code splitting (bundles par route)
2. Lazy loading des modules
3. CSS critique inline
4. Préchargement stratégique
5. Service Worker pour cache
```

**Résultat typique** : 25-40 requêtes initiales

---

## Outils et automatisation

### Build Tools automatiques 🤖

#### Vite (recommandé)

```javascript
// vite.config.js
export default {
  build: {
    rollupOptions: {
      output: {
        // Bundle automatique
        manualChunks: {
          vendor: ['react', 'react-dom'],
          utils: ['./src/utils']
        }
      }
    }
  }
}
```

**Commande** :
```bash
npm run build
# Génère automatiquement des bundles optimisés
```

---

#### Webpack

```javascript
// webpack.config.js
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        vendor: {
          test: /node_modules/,
          name: 'vendors'
        }
      }
    }
  }
}
```

---

### Plugins utiles

#### PostCSS avec autoprefixer
```bash
npm install --save-dev postcss autoprefixer
```

Optimise et préfixe automatiquement le CSS.

---

#### ImageMin (Gulp/Webpack)
```javascript
// Optimise toutes les images automatiquement
import imagemin from 'gulp-imagemin';

gulp.task('images', () =>
  gulp.src('src/images/*')
    .pipe(imagemin())
    .pipe(gulp.dest('dist/images'))
);
```

---

### Générateurs de sprites

#### Spritesmith (Gulp)
```javascript
const spritesmith = require('gulp.spritesmith');

gulp.task('sprite', () => {
  const spriteData = gulp.src('icons/*.png')
    .pipe(spritesmith({
      imgName: 'sprite.png',
      cssName: 'sprite.css'
    }));

  return spriteData.pipe(gulp.dest('dist/'));
});
```

---

## Bonnes pratiques récapitulatives

### ✅ À faire

1. **Bundler CSS et JavaScript**
   - 1-3 bundles au lieu de 20+ fichiers

2. **Utiliser des sprites**
   - CSS sprites ou SVG sprites pour icônes

3. **Optimiser les images**
   - Format WebP
   - Compression
   - Dimensions appropriées

4. **Lazy loading**
   - Images hors écran
   - Scripts non essentiels

5. **CSS au lieu d'images**
   - Dégradés, formes simples

6. **Minifier tous les fichiers**
   - CSS, JavaScript minifiés

7. **Utiliser un CDN**
   - Pour images et ressources statiques

8. **HTTP/2 sur votre serveur**
   - Activer la compression
   - Optimiser les headers

---

### ❌ À éviter

1. **20+ fichiers CSS/JS séparés**
   - Bundlez-les

2. **50+ petites icônes PNG**
   - Utilisez un sprite ou SVG

3. **Data URIs pour grandes images**
   - Uniquement pour < 2 KB

4. **Charger toutes les images immédiatement**
   - Lazy load les images hors écran

5. **CSS inline partout**
   - Uniquement pour le critique

6. **Images non optimisées**
   - Toujours optimiser

---

## Mesurer l'impact de vos optimisations

### Avant optimisation 📊

```
Network Tab :
- 147 requêtes HTTP
- 3.2 MB transférés
- 5.8 secondes de chargement

Lighthouse Score :
- Performance : 45/100
```

---

### Après optimisation 🎉

```
Network Tab :
- 28 requêtes HTTP (-81%)
- 850 KB transférés (-73%)
- 1.9 secondes de chargement (-67%)

Lighthouse Score :
- Performance : 92/100 (+104%)
```

---

### Tests comparatifs

**Utilisez WebPageTest** :
```
1. Tester la version non optimisée
2. Appliquer les optimisations
3. Tester la version optimisée
4. Comparer les résultats
```

---

## Cas pratique complet

### Site de départ (non optimisé)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- 5 fichiers CSS -->
  <link rel="stylesheet" href="reset.css">
  <link rel="stylesheet" href="typography.css">
  <link rel="stylesheet" href="layout.css">
  <link rel="stylesheet" href="components.css">
  <link rel="stylesheet" href="responsive.css">

  <!-- 8 fichiers JavaScript -->
  <script src="jquery.js"></script>
  <script src="utils.js"></script>
  <script src="validators.js"></script>
  <script src="api.js"></script>
  <script src="ui.js"></script>
  <script src="forms.js"></script>
  <script src="analytics.js"></script>
  <script src="main.js"></script>
</head>
<body>
  <header>
    <h1>Mon Site</h1>
    <nav>
      <!-- 10 icônes PNG séparées -->
      <img src="icon-home.png" alt="Accueil">
      <img src="icon-about.png" alt="À propos">
      <img src="icon-services.png" alt="Services">
      <img src="icon-portfolio.png" alt="Portfolio">
      <img src="icon-blog.png" alt="Blog">
      <img src="icon-contact.png" alt="Contact">
      <img src="icon-twitter.png" alt="Twitter">
      <img src="icon-facebook.png" alt="Facebook">
      <img src="icon-instagram.png" alt="Instagram">
      <img src="icon-linkedin.png" alt="LinkedIn">
    </nav>
  </header>

  <main>
    <!-- 30 images de galerie -->
    <img src="photo1.jpg" alt="Photo 1">
    <img src="photo2.jpg" alt="Photo 2">
    <!-- ... 28 autres ... -->
  </main>
</body>
</html>
```

**Total** : ~55 requêtes HTTP

---

### Site optimisé

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- CSS critique inline -->
  <style>
    /* Styles critiques pour above the fold */
    body { font-family: Arial, sans-serif; margin: 0; }
    .header { background: #333; color: white; padding: 1rem; }
    /* ... styles critiques ... */
  </style>

  <!-- 1 seul fichier CSS (bundlé et minifié) -->
  <link rel="stylesheet" href="styles.bundle.min.css">

  <!-- 1 seul fichier JavaScript (bundlé et minifié) -->
  <script src="app.bundle.min.js" defer></script>

  <!-- Analytics chargé en async (indépendant) -->
  <script src="analytics.min.js" async></script>

  <!-- Préchargement de la police critique -->
  <link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
</head>
<body>
  <!-- SVG sprite inline (0 requête supplémentaire) -->
  <svg style="display: none;">
    <symbol id="icon-home" viewBox="0 0 24 24">
      <!-- ... définition ... -->
    </symbol>
    <!-- ... autres icônes ... -->
  </svg>

  <header class="header">
    <h1>Mon Site</h1>
    <nav>
      <!-- Icônes SVG (0 requête HTTP) -->
      <svg class="icon"><use href="#icon-home"></use></svg>
      <svg class="icon"><use href="#icon-about"></use></svg>
      <svg class="icon"><use href="#icon-services"></use></svg>
      <svg class="icon"><use href="#icon-portfolio"></use></svg>
      <svg class="icon"><use href="#icon-blog"></use></svg>
      <svg class="icon"><use href="#icon-contact"></use></svg>
      <svg class="icon"><use href="#icon-twitter"></use></svg>
      <svg class="icon"><use href="#icon-facebook"></use></svg>
      <svg class="icon"><use href="#icon-instagram"></use></svg>
      <svg class="icon"><use href="#icon-linkedin"></use></svg>
    </nav>
  </header>

  <main>
    <!-- Images optimisées avec lazy loading -->
    <!-- Seules les 5-6 premières chargent immédiatement -->
    <img src="photo1.webp" alt="Photo 1" width="400" height="300">
    <img src="photo2.webp" alt="Photo 2" width="400" height="300" loading="lazy">
    <img src="photo3.webp" alt="Photo 3" width="400" height="300" loading="lazy">
    <!-- ... autres images avec loading="lazy" ... -->
  </main>
</body>
</html>
```

**Total** : ~10 requêtes HTTP initialement (les 25 autres images chargent au scroll)

**Amélioration** : 82% de requêtes en moins !

---

## Checklist d'optimisation ✅

### Audit des requêtes

- [ ] **Mesurer les requêtes actuelles** (Network Tab)
- [ ] **Identifier les gros consommateurs** (CSS, JS, images)
- [ ] **Définir un objectif** (< 30 requêtes idéalement)

### CSS

- [ ] **Bundler tous les CSS** en 1-2 fichiers
- [ ] **Minifier le CSS**
- [ ] **Inline le CSS critique** (< 14 KB)
- [ ] **Utiliser CSS au lieu d'images** quand possible

### JavaScript

- [ ] **Bundler tous les JS** en 1-3 fichiers
- [ ] **Minifier le JavaScript**
- [ ] **Utiliser defer/async** appropriément
- [ ] **Code splitting** pour les grosses apps
- [ ] **Lazy load** les scripts non essentiels

### Images

- [ ] **Optimiser toutes les images** (WebP, compression)
- [ ] **Lazy loading** pour images hors écran
- [ ] **Sprites CSS/SVG** pour icônes
- [ ] **Utiliser un CDN** pour les images

### Polices

- [ ] **Limiter à 2-3 polices**
- [ ] **Utiliser font-display: swap**
- [ ] **Précharger les polices critiques**

### Autres

- [ ] **HTTP/2 activé** sur le serveur
- [ ] **Compression Gzip/Brotli** activée
- [ ] **Cache headers** configurés
- [ ] **Service Worker** (PWA) pour cache avancé

---

## Conclusion

La réduction des requêtes HTTP est l'une des **optimisations les plus impactantes** que vous pouvez faire sur votre site web.

**Résumé des gains possibles** :
- 🚀 **50-80% de réduction** du nombre de requêtes
- ⚡ **40-70% de réduction** du temps de chargement
- 💾 **30-50% de réduction** de la bande passante
- 📈 **+30-50 points** Lighthouse score

**Les 3 techniques les plus efficaces** :
1. **Bundling CSS/JS** (bundler moderne)
2. **Lazy loading des images**
3. **SVG sprites pour les icônes**

**Commencez par** :
- Mesurer vos requêtes actuelles
- Bundler vos CSS et JS
- Lazy load vos images
- Mesurer à nouveau

**N'oubliez pas** : L'objectif n'est pas d'avoir 0 requête (impossible), mais de **minimiser intelligemment** pour un bon équilibre entre performance et maintenabilité.

---

## Ressources complémentaires

### Outils de mesure
- [Chrome DevTools - Network Tab](https://developer.chrome.com/docs/devtools/network/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [WebPageTest](https://www.webpagetest.org/)
- [GTmetrix](https://gtmetrix.com/)

### Build Tools
- [Vite](https://vitejs.dev/) - Bundler moderne
- [Webpack](https://webpack.js.org/) - Bundler populaire
- [Rollup](https://rollupjs.org/) - Bundler pour bibliothèques
- [Parcel](https://parceljs.org/) - Zero-config bundler

### Sprites et optimisation
- [SpritePad](https://wearekiss.com/spritepad)
- [CSS Sprite Generator](https://www.toptal.com/developers/css/sprite-generator)
- [IcoMoon](https://icomoon.io/) - SVG sprite generator
- [Squoosh](https://squoosh.app/) - Optimisation d'images

### Documentation
- [MDN - HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [Web.dev - Fast load times](https://web.dev/fast/)
- [HTTP/2 explained](https://http2-explained.haxx.se/)

⏭️ [Debugging et Outils Avancés](/07-debugging-et-outils-avances/README.md)
