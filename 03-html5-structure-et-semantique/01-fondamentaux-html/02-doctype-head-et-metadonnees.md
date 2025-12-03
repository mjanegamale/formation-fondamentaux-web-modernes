🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.1.2 Doctype, balises head et métadonnées

## Introduction

Dans la section précédente, nous avons découvert la structure de base d'un document HTML5. Maintenant, nous allons approfondir deux éléments cruciaux mais souvent mal compris : le **DOCTYPE** et la section **`<head>`** avec ses métadonnées.

Ces éléments sont invisibles pour les visiteurs de votre site, mais ils sont **essentiels** pour :
- Les navigateurs (pour afficher correctement votre page)
- Les moteurs de recherche (pour indexer et référencer votre contenu)
- Les réseaux sociaux (pour créer de beaux aperçus de vos liens)
- Les technologies d'assistance (pour l'accessibilité)

## Le DOCTYPE en détail

### Qu'est-ce que le DOCTYPE ?

Le DOCTYPE (Document Type Declaration) est une **instruction** qui doit être placée **en tout début de fichier**, avant même la balise `<html>`. C'est une déclaration, pas une balise HTML.

```html
<!DOCTYPE html>
```

### À quoi sert-il vraiment ?

Le DOCTYPE indique au navigateur **quelle version de HTML** vous utilisez et **comment interpréter** le reste du document. C'est comme dire à quelqu'un dans quelle langue vous allez lui parler avant de commencer votre discours.

**Sans DOCTYPE**, le navigateur entre en "quirks mode" (mode bizarreries) :
- Il essaie de deviner comment afficher votre page
- Il peut utiliser d'anciens comportements de rendu
- Votre CSS peut ne pas fonctionner comme prévu
- Des bugs étranges peuvent apparaître

**Avec DOCTYPE**, le navigateur entre en "standards mode" (mode standards) :
- Il suit les spécifications modernes
- Votre code CSS et JavaScript se comporte de manière prévisible
- Tout fonctionne comme documenté

### L'évolution du DOCTYPE

#### Avant HTML5 (à titre informatif)

Les anciens DOCTYPE étaient **très longs** et **difficiles à mémoriser** :

```html
<!-- HTML 4.01 Strict (ne PLUS utiliser) -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 Strict (ne PLUS utiliser) -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

Personne ne pouvait se souvenir de ces lignes par cœur ! Les développeurs les copiaient-collaient.

#### Avec HTML5 (aujourd'hui)

HTML5 a simplifié tout cela :

```html
<!DOCTYPE html>
```

**C'est tout !** Simple, court, mémorisable. C'est l'une des grandes améliorations de HTML5.

### Règles importantes

1. **Toujours en premier** : Le DOCTYPE doit être la toute première ligne du fichier, sans espace ni caractère avant
2. **Insensible à la casse** : `<!DOCTYPE html>`, `<!doctype html>`, ou `<!DoCtYpE HtMl>` fonctionnent tous (mais par convention, on utilise les majuscules)
3. **Obligatoire** : Même si les navigateurs modernes sont tolérants, ne jamais l'omettre
4. **Pas une balise HTML** : C'est une instruction pour le navigateur, pas un élément HTML

### Exemples d'erreurs courantes

❌ **Mauvais : espaces ou texte avant le DOCTYPE**
```html
  <!DOCTYPE html>
```

❌ **Mauvais : commentaires avant le DOCTYPE**
```html
<!-- Mon super site -->
<!DOCTYPE html>
```

✅ **Bon : DOCTYPE en première ligne absolue**
```html
<!DOCTYPE html>
<html lang="fr">
```

## La section `<head>` approfondie

### Vue d'ensemble

La section `<head>` est le **centre de contrôle** de votre page. Elle contient toutes les informations **sur** la page, mais pas le contenu visible. Pensez-y comme aux réglages d'un appareil : invisibles pour l'utilisateur final, mais cruciaux pour le bon fonctionnement.

### Structure typique d'un `<head>` complet

Voici un exemple de `<head>` bien structuré pour un site moderne :

```html
<head>
    <!-- 1. Encodage (TOUJOURS EN PREMIER) -->
    <meta charset="UTF-8">

    <!-- 2. Compatibilité Internet Explorer (si nécessaire) -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <!-- 3. Viewport pour le responsive -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 4. Titre de la page -->
    <title>Ma page web professionnelle - Mon site</title>

    <!-- 5. Description pour les moteurs de recherche -->
    <meta name="description" content="Description concise de ma page (150-160 caractères)">

    <!-- 6. Mots-clés (optionnel, peu utilisé aujourd'hui) -->
    <meta name="keywords" content="mot1, mot2, mot3">

    <!-- 7. Auteur -->
    <meta name="author" content="Prénom Nom">

    <!-- 8. Favicon -->
    <link rel="icon" type="image/png" href="favicon.png">

    <!-- 9. Feuille de style CSS -->
    <link rel="stylesheet" href="styles.css">

    <!-- 10. Open Graph pour les réseaux sociaux (optionnel) -->
    <meta property="og:title" content="Titre pour Facebook">
    <meta property="og:description" content="Description pour Facebook">
    <meta property="og:image" content="image-preview.jpg">

    <!-- 11. Scripts JavaScript (généralement en fin de body, mais possibles ici) -->
    <!-- <script src="script.js" defer></script> -->
</head>
```

Nous allons maintenant détailler chaque élément.

## Les métadonnées essentielles

### 1. L'encodage des caractères (charset)

```html
<meta charset="UTF-8">
```

**Pourquoi c'est important :**

Sans cette balise, les caractères accentués et spéciaux peuvent s'afficher incorrectement :
- é devient Ã©
- à devient Ã
- € devient â‚¬

**UTF-8** est l'encodage universel qui supporte :
- Tous les alphabets du monde (latin, cyrillique, arabe, chinois, japonais, etc.)
- Tous les symboles et emojis
- Les caractères spéciaux (©, ®, ™, €, etc.)

**Règle d'or :** Cette balise doit être **dans les 1024 premiers octets** du fichier, idéalement juste après l'ouverture de `<head>`.

### 2. Le viewport (responsive design)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Cette balise est **indispensable** pour que votre site s'adapte correctement aux mobiles et tablettes.

**Décortiquons les paramètres :**

- **`width=device-width`** : La largeur de la page = la largeur de l'écran de l'appareil
  - Sans cela, le mobile afficherait une version "bureau" rétrécie

- **`initial-scale=1.0`** : Le zoom initial est à 100%
  - `1.0` signifie pas de zoom au chargement
  - L'utilisateur peut toujours zoomer manuellement

**Autres paramètres possibles (mais déconseillés) :**

```html
<!-- NE PAS FAIRE : empêche l'utilisateur de zoomer -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```

⚠️ **Attention :** Bloquer le zoom nuit à l'accessibilité et peut frustrer les utilisateurs malvoyants. C'est également pénalisé par les moteurs de recherche.

### 3. Le titre de la page (`<title>`)

```html
<title>Boulangerie Dupont - Pain artisanal à Lyon 3ème</title>
```

Le titre est **l'élément le plus important** du `<head>` pour plusieurs raisons :

**Où apparaît-il ?**
1. Dans l'onglet du navigateur
2. Dans les favoris/marque-pages
3. Dans les résultats de recherche Google (c'est le lien bleu cliquable)
4. Dans l'historique du navigateur
5. Quand on partage la page

**Bonnes pratiques pour le titre :**

✅ **Soyez descriptif et unique**
```html
<title>Recette de cookies au chocolat - Facile et rapide</title>
```

✅ **Incluez des mots-clés pertinents**
```html
<title>Formation développement web - HTML, CSS, JavaScript</title>
```

✅ **Mettez l'info importante en premier**
```html
<title>iPhone 15 Pro - Prix et caractéristiques | TechShop</title>
```

❌ **Évitez les titres trop génériques**
```html
<title>Accueil</title>  <!-- Trop vague -->
<title>Page 2</title>    <!-- Pas descriptif -->
```

❌ **Évitez les titres trop longs**
```html
<!-- Google tronquera après ~60 caractères -->
<title>Découvrez notre magnifique collection de produits artisanaux faits main avec amour et passion depuis 1985</title>
```

**Longueur optimale :** 50 à 60 caractères (environ 600 pixels dans les résultats Google).

### 4. La description (meta description)

```html
<meta name="description" content="Découvrez nos recettes de cookies faciles et rapides. Parfait pour les débutants en pâtisserie. Temps de préparation : 15 minutes.">
```

La meta description est un **résumé de votre page** qui apparaît sous le titre dans les résultats de recherche Google.

**Caractéristiques :**
- Longueur idéale : **150 à 160 caractères**
- Ne doit pas contenir de guillemets doubles (utilisez des apostrophes ou guillemets simples)
- Doit donner envie de cliquer (call-to-action)
- Doit être unique pour chaque page

**Impact SEO :**
La meta description n'affecte **pas directement** le classement dans Google, mais elle influence le **taux de clic** (CTR). Une bonne description = plus de visiteurs.

✅ **Bonne description**
```html
<meta name="description" content="Apprenez le HTML5 facilement avec nos tutoriels gratuits. Parfait pour débutants. 50+ exemples pratiques et explications claires.">
```

❌ **Mauvaise description**
```html
<meta name="description" content="Bienvenue sur notre site">
```

### 5. Les mots-clés (obsolète mais à connaître)

```html
<meta name="keywords" content="html, css, javascript, tutoriel, débutant">
```

⚠️ **Important :** Les moteurs de recherche modernes (Google, Bing) **ignorent** cette balise depuis des années en raison des abus (bourrage de mots-clés).

**Verdict :** Vous pouvez l'omettre complètement. Si vous l'incluez, soyez raisonnable (5-10 mots-clés maximum).

### 6. L'auteur

```html
<meta name="author" content="Marie Dubois">
```

Cette balise indique qui a créé la page. Utile pour :
- Les blogs personnels
- Les articles
- Les portfolios

Pas indispensable pour les sites d'entreprise ou e-commerce.

### 7. Compatibilité Internet Explorer

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```

Cette balise force Internet Explorer à utiliser son **moteur de rendu le plus récent**.

**Note :** Avec la fin d'Internet Explorer (remplacé par Edge basé sur Chromium), cette balise devient de moins en moins nécessaire. Elle ne fait pas de mal, mais n'est plus critique.

## Liens vers les ressources externes

### 1. Les feuilles de style (CSS)

```html
<link rel="stylesheet" href="styles.css">
```

**Anatomie de la balise :**
- **`rel="stylesheet"`** : Indique que c'est une feuille de style
- **`href="styles.css"`** : Le chemin vers le fichier CSS

**Plusieurs feuilles de style :**
```html
<link rel="stylesheet" href="css/reset.css">
<link rel="stylesheet" href="css/global.css">
<link rel="stylesheet" href="css/page-accueil.css">
```

L'ordre est important : les styles sont appliqués dans l'ordre de chargement.

**Feuilles de style externes vs. Google Fonts :**
```html
<!-- Police Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">

<!-- Votre CSS -->
<link rel="stylesheet" href="styles.css">
```

### 2. Le favicon

```html
<link rel="icon" type="image/png" href="favicon.png">
```

Le favicon est la **petite icône** qui apparaît :
- Dans l'onglet du navigateur
- Dans les favoris
- Dans la barre d'adresse

**Formats courants :**
```html
<!-- PNG (recommandé, largement supporté) -->
<link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">

<!-- ICO (ancien format, toujours supporté) -->
<link rel="icon" type="image/x-icon" href="favicon.ico">

<!-- SVG (moderne, vectoriel, idéal) -->
<link rel="icon" type="image/svg+xml" href="favicon.svg">
```

**Favicon pour Apple (iPhone/iPad) :**
```html
<link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
```

## Métadonnées pour les réseaux sociaux

### Open Graph (Facebook, LinkedIn, etc.)

Quand quelqu'un partage votre page sur Facebook ou LinkedIn, ces plateformes utilisent les balises **Open Graph** pour créer un aperçu attractif.

```html
<!-- Open Graph de base -->
<meta property="og:title" content="Le titre qui apparaît sur Facebook">
<meta property="og:description" content="La description qui apparaît sous le titre">
<meta property="og:image" content="https://www.monsite.com/images/preview.jpg">
<meta property="og:url" content="https://www.monsite.com/ma-page">
<meta property="og:type" content="website">
```

**Exemple complet pour un article de blog :**
```html
<meta property="og:title" content="10 astuces pour apprendre HTML rapidement">
<meta property="og:description" content="Découvrez comment maîtriser HTML5 en quelques semaines avec ces conseils pratiques et éprouvés.">
<meta property="og:image" content="https://www.monsite.com/images/html-tips.jpg">
<meta property="og:url" content="https://www.monsite.com/blog/astuces-html">
<meta property="og:type" content="article">
<meta property="og:locale" content="fr_FR">
<meta property="og:site_name" content="Mon Blog Tech">
```

**Points importants :**
- L'image doit être en **URL absolue** (avec https://)
- Dimensions recommandées pour l'image : **1200 x 630 pixels**
- Taille minimale : 600 x 315 pixels
- Format : JPG ou PNG

### Twitter Cards

Twitter utilise son propre système de métadonnées :

```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Titre pour Twitter">
<meta name="twitter:description" content="Description pour Twitter">
<meta name="twitter:image" content="https://www.monsite.com/images/preview.jpg">
<meta name="twitter:site" content="@moncompte">
```

**Types de cartes Twitter :**
- **`summary`** : petite carte avec image carrée
- **`summary_large_image`** : grande carte avec image rectangulaire (recommandé)
- **`app`** : pour les applications mobiles
- **`player`** : pour les contenus audio/vidéo

## Autres balises utiles

### Canonical (pour éviter le contenu dupliqué)

```html
<link rel="canonical" href="https://www.monsite.com/page-originale">
```

Cette balise indique aux moteurs de recherche quelle est la **version principale** d'une page si elle existe en plusieurs versions (avec/sans www, http/https, paramètres d'URL différents).

**Exemple d'utilisation :**
Si votre page est accessible via :
- `http://monsite.com/produit`
- `https://monsite.com/produit`
- `https://www.monsite.com/produit`

Vous mettez un canonical vers la version "officielle" :
```html
<link rel="canonical" href="https://www.monsite.com/produit">
```

### Balises robots (pour le référencement)

```html
<!-- Autoriser l'indexation et le suivi des liens -->
<meta name="robots" content="index, follow">

<!-- Interdire l'indexation (page privée) -->
<meta name="robots" content="noindex, nofollow">

<!-- Autoriser l'indexation mais pas le suivi des liens -->
<meta name="robots" content="index, nofollow">
```

**Quand utiliser noindex :**
- Pages de connexion/inscription
- Pages de résultats de recherche internes
- Pages temporaires ou en construction
- Pages confidentielles

### Refresh automatique (à utiliser avec modération)

```html
<!-- Rediriger vers une autre page après 5 secondes -->
<meta http-equiv="refresh" content="5; url=https://www.monsite.com/nouvelle-page">

<!-- Rafraîchir la page toutes les 30 secondes -->
<meta http-equiv="refresh" content="30">
```

⚠️ **Attention :** Le refresh automatique peut être frustrant pour les utilisateurs et nuire à l'accessibilité. Préférez JavaScript pour ce type de fonctionnalité.

## Organisation et ordre recommandé

Voici l'ordre logique optimal pour organiser votre `<head>` :

```html
<head>
    <!-- 1. ENCODAGE (obligatoire, en premier) -->
    <meta charset="UTF-8">

    <!-- 2. COMPATIBILITÉ (si nécessaire) -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <!-- 3. VIEWPORT (obligatoire pour responsive) -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 4. TITRE (obligatoire) -->
    <title>Titre de votre page</title>

    <!-- 5. MÉTADONNÉES SEO -->
    <meta name="description" content="Description de la page">
    <meta name="author" content="Votre nom">

    <!-- 6. CANONICAL (si nécessaire) -->
    <link rel="canonical" href="https://www.monsite.com/page">

    <!-- 7. OPEN GRAPH (réseaux sociaux) -->
    <meta property="og:title" content="Titre">
    <meta property="og:description" content="Description">
    <meta property="og:image" content="image.jpg">

    <!-- 8. TWITTER CARDS -->
    <meta name="twitter:card" content="summary_large_image">

    <!-- 9. FAVICON -->
    <link rel="icon" type="image/png" href="favicon.png">

    <!-- 10. POLICES EXTERNES (Google Fonts, etc.) -->
    <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">

    <!-- 11. CSS (vos styles en dernier) -->
    <link rel="stylesheet" href="styles.css">

    <!-- 12. SCRIPTS (optionnel, souvent en fin de body) -->
    <script src="script.js" defer></script>
</head>
```

## Exemple complet et commenté

Voici un `<head>` complet pour un site professionnel :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <!-- Encodage et compatibilité -->
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- Titre et description SEO -->
    <title>Boulangerie Dupont - Pain artisanal à Lyon 3ème</title>
    <meta name="description" content="Découvrez notre boulangerie artisanale à Lyon. Pain bio, viennoiseries maison, pâtisseries fraîches. Ouvert 7j/7 de 6h à 20h.">
    <meta name="author" content="Boulangerie Dupont">

    <!-- URL canonique -->
    <link rel="canonical" href="https://www.boulangerie-dupont.fr">

    <!-- Open Graph pour Facebook/LinkedIn -->
    <meta property="og:title" content="Boulangerie Dupont - Pain artisanal à Lyon">
    <meta property="og:description" content="Pain bio et viennoiseries maison depuis 1985">
    <meta property="og:image" content="https://www.boulangerie-dupont.fr/images/boulangerie-preview.jpg">
    <meta property="og:url" content="https://www.boulangerie-dupont.fr">
    <meta property="og:type" content="website">
    <meta property="og:locale" content="fr_FR">

    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="Boulangerie Dupont - Pain artisanal">
    <meta name="twitter:description" content="Pain bio et viennoiseries maison">
    <meta name="twitter:image" content="https://www.boulangerie-dupont.fr/images/boulangerie-preview.jpg">

    <!-- Favicon -->
    <link rel="icon" type="image/png" sizes="32x32" href="images/favicon-32x32.png">
    <link rel="apple-touch-icon" sizes="180x180" href="images/apple-touch-icon.png">

    <!-- Polices Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

    <!-- CSS -->
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <!-- Le contenu visible de la page ici -->
</body>
</html>
```

## Points clés à retenir

### Le DOCTYPE
- ✅ Toujours `<!DOCTYPE html>` en HTML5
- ✅ Première ligne absolue du fichier
- ✅ Active le "standards mode" du navigateur

### Le `<head>` essentiel
- ✅ `<meta charset="UTF-8">` en premier
- ✅ `<meta name="viewport">` pour le responsive
- ✅ `<title>` unique et descriptif (50-60 caractères)
- ✅ `<meta name="description">` pour le SEO (150-160 caractères)

### Ordre d'importance
1. **Obligatoire** : charset, viewport, title
2. **Fortement recommandé** : description, favicon, CSS
3. **Optionnel mais utile** : Open Graph, Twitter Cards, canonical
4. **Obsolète** : keywords

### Bonnes pratiques
- 📝 Commentez votre code pour vous y retrouver
- 🎯 Chaque page doit avoir un title et description uniques
- 🖼️ Préparez des images optimisées pour les réseaux sociaux (1200x630px)
- 🔍 Validez votre HTML avec le validateur W3C
- 📱 Testez toujours sur mobile

## Erreurs courantes à éviter

❌ **Oublier le charset**
→ Résultat : caractères bizarres (Ã©, Ã , etc.)

❌ **Oublier le viewport**
→ Résultat : site illisible sur mobile

❌ **Mettre du contenu visible dans le `<head>`**
→ Résultat : affichage imprévisible

❌ **Dupliquer le `<title>`**
→ Résultat : SEO médiocre, pages difficiles à différencier

❌ **Images Open Graph en chemin relatif**
→ Résultat : pas d'aperçu sur les réseaux sociaux

## Outils pour vérifier vos métadonnées

### Validation HTML
- **W3C Validator** : https://validator.w3.org/
- Vérifie que votre code HTML est valide

### Aperçu réseaux sociaux
- **Facebook Debugger** : https://developers.facebook.com/tools/debug/
- **Twitter Card Validator** : https://cards-dev.twitter.com/validator
- Testez comment votre page apparaît quand elle est partagée

### SEO
- **Google Search Console** : https://search.google.com/search-console
- Analysez comment Google voit votre page

### DevTools du navigateur
- Appuyez sur `F12` pour ouvrir les DevTools
- Onglet "Elements" pour inspecter le `<head>`
- Vérifiez que toutes vos balises sont présentes

## Conclusion

Le DOCTYPE et les métadonnées dans le `<head>` sont invisibles pour vos visiteurs, mais **cruciaux** pour :
- Le bon fonctionnement de votre site
- Votre référencement (SEO)
- L'apparence de vos liens partagés sur les réseaux sociaux
- L'accessibilité de votre contenu

Prenez le temps de bien configurer ces éléments : c'est un investissement qui portera ses fruits sur le long terme. Un bon `<head>` est le signe d'un développeur web professionnel et consciencieux.

Dans la prochaine section, nous verrons en détail l'encodage UTF-8 et l'attribut `lang`, deux éléments essentiels pour un web multilingue et accessible.

---

**Section suivante** : [3.1.3 Encodage UTF-8 et attribut lang](./03-encodage-utf8-et-attribut-lang.md)

⏭️ [Encodage UTF-8 et attribut lang](/03-html5-structure-et-semantique/01-fondamentaux-html/03-encodage-utf8-et-attribut-lang.md)
