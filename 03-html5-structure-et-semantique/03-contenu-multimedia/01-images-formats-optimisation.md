🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.3.1 Images : formats, optimisation et accessibilité

## Introduction

Les images sont des éléments essentiels du web moderne. Elles rendent vos pages plus attrayantes, aident à communiquer visuellement et améliorent l'expérience utilisateur. Cependant, mal utilisées, elles peuvent ralentir considérablement votre site et poser des problèmes d'accessibilité.

Dans ce chapitre, nous allons découvrir comment intégrer des images de manière professionnelle en HTML5.

---

## La balise `<img>`

### Syntaxe de base

La balise `<img>` est une **balise auto-fermante** (elle n'a pas de balise de fermeture). Voici sa forme la plus simple :

```html
<img src="chemin/vers/image.jpg" alt="Description de l'image">
```

### Attributs essentiels

#### 1. `src` (source) - **OBLIGATOIRE**

L'attribut `src` indique le chemin vers le fichier image. Ce chemin peut être :

**Relatif** (par rapport à votre fichier HTML) :
```html
<img src="images/photo.jpg" alt="Ma photo">
<img src="../images/logo.png" alt="Logo">
```

**Absolu** (URL complète) :
```html
<img src="https://exemple.com/images/photo.jpg" alt="Photo">
```

#### 2. `alt` (texte alternatif) - **OBLIGATOIRE**

L'attribut `alt` fournit une description textuelle de l'image. Il est **crucial pour l'accessibilité** :

```html
<img src="chat.jpg" alt="Un chat roux assis sur un canapé gris">
```

**Pourquoi l'attribut `alt` est-il si important ?**

- **Accessibilité** : Les lecteurs d'écran lisent ce texte aux personnes malvoyantes
- **SEO** : Les moteurs de recherche utilisent ce texte pour comprendre l'image
- **Fallback** : Si l'image ne charge pas, le texte alternatif s'affiche à la place
- **Contexte** : Aide à comprendre le contenu même sans voir l'image

**Bonnes pratiques pour le texte alternatif :**

```html
<!-- ✅ BON : description claire et concise -->
<img src="produit.jpg" alt="Smartphone noir avec écran 6 pouces">

<!-- ❌ MAUVAIS : trop vague -->
<img src="produit.jpg" alt="image">

<!-- ❌ MAUVAIS : redondant -->
<img src="produit.jpg" alt="Image d'un smartphone">

<!-- ✅ BON : image décorative (vide mais présent) -->
<img src="decoration.png" alt="">
```

**Note importante** : Si une image est purement décorative et n'apporte aucune information, utilisez `alt=""` (vide) plutôt que de supprimer l'attribut.

#### 3. `width` et `height` (dimensions)

Ces attributs définissent la largeur et la hauteur de l'image en pixels :

```html
<img src="logo.png" alt="Logo entreprise" width="200" height="100">
```

**Pourquoi spécifier les dimensions ?**

- **Performance** : Le navigateur réserve l'espace avant le chargement de l'image, évitant les sauts de mise en page
- **CLS** (Cumulative Layout Shift) : Améliore les Core Web Vitals de Google

```html
<!-- ✅ BON : dimensions spécifiées -->
<img src="photo.jpg" alt="Paysage" width="800" height="600">

<!-- ⚠️ À éviter : pas de dimensions (cause des sauts de page) -->
<img src="photo.jpg" alt="Paysage">
```

**Note** : Vous pouvez ensuite ajuster la taille avec CSS sans problème, les attributs HTML servent juste à indiquer les proportions.

#### 4. `title` (info-bulle)

L'attribut `title` affiche une info-bulle au survol de la souris :

```html
<img src="auteur.jpg" alt="Portrait de l'auteur" title="Photo prise en 2024">
```

⚠️ **Attention** : Ne remplacez jamais `alt` par `title`. Ce sont deux attributs différents avec des usages distincts.

---

## Les différents formats d'images

Choisir le bon format d'image est crucial pour l'optimisation de votre site. Voici les formats les plus courants :

### 1. JPEG / JPG (Joint Photographic Experts Group)

**Caractéristiques :**
- Format avec **compression destructive** (perte de qualité)
- Idéal pour les **photographies** et images avec beaucoup de couleurs
- Ne supporte **pas la transparence**
- Taille de fichier généralement petite

**Quand l'utiliser :**
- Photos de produits
- Images de paysages
- Portraits
- Toute image complexe avec dégradés de couleurs

```html
<img src="photo-vacances.jpg" alt="Plage au coucher du soleil" width="1200" height="800">
```

**Avantages :** Excellente compression, fichiers légers
**Inconvénients :** Perte de qualité, pas de transparence

---

### 2. PNG (Portable Network Graphics)

**Caractéristiques :**
- Format avec **compression sans perte** (qualité préservée)
- Supporte la **transparence** (canal alpha)
- Idéal pour les graphiques, logos, icônes
- Taille de fichier plus importante que JPEG

**Quand l'utiliser :**
- Logos avec transparence
- Icônes
- Captures d'écran
- Images avec texte
- Graphiques avec zones de couleurs unies

```html
<img src="logo.png" alt="Logo de l'entreprise" width="150" height="50">
```

**Avantages :** Qualité parfaite, transparence
**Inconvénients :** Fichiers plus lourds que JPEG

---

### 3. GIF (Graphics Interchange Format)

**Caractéristiques :**
- Format avec **palette limitée** (256 couleurs maximum)
- Supporte les **animations**
- Supporte la transparence (mais basique, pas de semi-transparence)
- Format ancien mais toujours utilisé pour les animations courtes

**Quand l'utiliser :**
- Animations simples
- Petites icônes animées
- Illustrations simples

```html
<img src="animation.gif" alt="Animation de chargement" width="50" height="50">
```

**Avantages :** Animations, compatible partout
**Inconvénients :** Qualité limitée, fichiers lourds pour les animations

⚠️ **Note moderne** : Pour les animations complexes, préférez les vidéos (format MP4) qui sont plus performantes.

---

### 4. WebP

**Caractéristiques :**
- Format **moderne** développé par Google
- Excellente compression (meilleure que JPEG et PNG)
- Supporte la **transparence** et les **animations**
- Qualité supérieure pour une taille de fichier réduite

**Quand l'utiliser :**
- Toutes les situations (photos, logos, graphiques)
- Quand la performance est prioritaire
- Sites modernes avec compatibilité récente

```html
<img src="photo.webp" alt="Image optimisée" width="800" height="600">
```

**Avantages :** Excellent compromis qualité/poids
**Inconvénients :** Support limité sur les très vieux navigateurs (mais maintenant largement supporté)

---

### 5. SVG (Scalable Vector Graphics)

**Caractéristiques :**
- Format **vectoriel** (pas de pixels, mais des formes mathématiques)
- **Évolutif sans perte de qualité** (zoom infini)
- Fichiers très légers
- Modifiable avec CSS et JavaScript
- Idéal pour logos, icônes, illustrations simples

**Quand l'utiliser :**
- Logos
- Icônes
- Graphiques simples
- Illustrations géométriques
- Tout ce qui doit s'adapter à différentes tailles

```html
<img src="icone.svg" alt="Icône de menu" width="24" height="24">
```

**Avantages :** Qualité parfaite à toute taille, très léger
**Inconvénients :** Ne convient pas aux photos, complexité limitée

---

### Tableau récapitulatif

| Format | Usage principal | Transparence | Animation | Taille fichier |
|--------|----------------|--------------|-----------|----------------|
| **JPEG** | Photos, images complexes | ❌ Non | ❌ Non | 🟢 Petite |
| **PNG** | Logos, graphiques, captures | ✅ Oui | ❌ Non | 🟡 Moyenne |
| **GIF** | Animations simples | ⚠️ Basique | ✅ Oui | 🔴 Grande |
| **WebP** | Tout (moderne) | ✅ Oui | ✅ Oui | 🟢 Petite |
| **SVG** | Logos, icônes, vectoriel | ✅ Oui | ✅ Oui | 🟢 Très petite |

---

## Optimisation des images

L'optimisation des images est **cruciale** pour la performance de votre site web. Des images mal optimisées peuvent considérablement ralentir le chargement de vos pages.

### Pourquoi optimiser ?

- **Vitesse de chargement** : Les images représentent souvent 50 à 70% du poids total d'une page web
- **Expérience utilisateur** : Un site rapide = des utilisateurs satisfaits
- **SEO** : Google favorise les sites rapides dans son classement
- **Données mobiles** : Économise la bande passante des utilisateurs mobile
- **Coûts d'hébergement** : Réduit la consommation de bande passante

### 1. Choisir les bonnes dimensions

**Règle d'or** : Ne chargez jamais une image plus grande que nécessaire.

```html
<!-- ❌ MAUVAIS : Image de 3000x2000px affichée en 300x200px -->
<img src="enorme-photo.jpg" alt="Photo" width="300" height="200">

<!-- ✅ BON : Image déjà redimensionnée à 300x200px -->
<img src="photo-optimisee.jpg" alt="Photo" width="300" height="200">
```

**Exemple concret :**
- Votre image s'affiche en 400px de large sur la page
- Préparez une image de 800px de large maximum (pour les écrans haute résolution)
- Ne servez pas une image de 3000px !

### 2. Compresser les images

La compression réduit la taille du fichier sans (trop) dégrader la qualité visible.

**Outils de compression recommandés :**

**En ligne (gratuits) :**
- **TinyPNG / TinyJPG** : https://tinypng.com (excellent pour PNG et JPEG)
- **Squoosh** : https://squoosh.app (par Google, très complet)
- **Compressor.io** : https://compressor.io

**Logiciels :**
- **ImageOptim** (Mac) : gratuit et excellent
- **RIOT** (Windows) : Radical Image Optimization Tool
- **Photoshop** : "Enregistrer pour le web"

**Exemple de gain :**
- Image originale : 2.5 Mo
- Après compression : 250 Ko (10 fois plus légère !)
- Différence de qualité : imperceptible à l'œil nu

### 3. Choisir le bon format

```html
<!-- Pour une photo -->
<img src="paysage.jpg" alt="Montagne">
<!-- Ou mieux en moderne -->
<img src="paysage.webp" alt="Montagne">

<!-- Pour un logo avec transparence -->
<img src="logo.png" alt="Logo">
<!-- Ou mieux -->
<img src="logo.svg" alt="Logo">
```

### 4. Lazy loading (chargement différé)

L'attribut `loading="lazy"` indique au navigateur de ne charger l'image que quand elle devient visible (proche du viewport).

```html
<img src="image.jpg" alt="Description" loading="lazy">
```

**Avantages :**
- Charge d'abord les images visibles
- Économise la bande passante
- Améliore la vitesse de chargement initial

**Quand l'utiliser :**
- Images en bas de page
- Galeries d'images
- Longues pages avec beaucoup de contenu

**Quand NE PAS l'utiliser :**
- Image principale visible immédiatement (hero image)
- Logo dans le header
- Les 2-3 premières images de la page

```html
<!-- ❌ Ne pas mettre lazy sur l'image principale -->
<img src="hero.jpg" alt="Bannière principale" width="1920" height="600">

<!-- ✅ Mettre lazy sur les images plus bas -->
<img src="photo1.jpg" alt="Photo 1" loading="lazy">
<img src="photo2.jpg" alt="Photo 2" loading="lazy">
```

---

## Accessibilité des images

Rendre vos images accessibles est une **obligation légale** dans de nombreux pays et surtout une question d'éthique et d'inclusivité.

### L'attribut `alt` : votre meilleur allié

Nous l'avons déjà vu, mais insistons sur son importance :

```html
<!-- ✅ Excellent : description précise et utile -->
<img src="graphique.png" alt="Graphique montrant une augmentation de 45% des ventes en 2024">

<!-- ✅ Bon : description concise -->
<img src="chat.jpg" alt="Chat tigré dormant sur un coussin">

<!-- ❌ Mauvais : trop vague -->
<img src="chat.jpg" alt="animal">

<!-- ❌ Mauvais : informations inutiles -->
<img src="chat.jpg" alt="IMG_5847.jpg">
```

### Cas particuliers

#### Images décoratives

Si l'image est purement décorative (ne véhicule aucune information) :

```html
<img src="bordure-decorative.png" alt="">
```

L'attribut `alt` doit être présent mais vide. Cela indique aux lecteurs d'écran d'ignorer l'image.

#### Images de texte

**À éviter absolument** : utiliser des images pour afficher du texte.

```html
<!-- ❌ MAUVAIS : texte en image -->
<img src="titre.png" alt="Bienvenue sur notre site">

<!-- ✅ BON : texte HTML stylé avec CSS -->
<h1>Bienvenue sur notre site</h1>
```

**Pourquoi ?**
- Le texte dans une image n'est pas sélectionnable
- Mauvais pour le SEO
- Problèmes d'accessibilité
- Ne s'adapte pas aux différentes tailles d'écran

**Exception** : Logos contenant du texte (mais l'`alt` doit contenir le texte).

#### Images complexes (graphiques, diagrammes)

Pour les images complexes, le texte alternatif court ne suffit pas :

```html
<!-- Option 1 : Description longue dans le texte -->
<figure>
  <img src="graphique-ventes.png" alt="Graphique des ventes 2024">
  <figcaption>
    Ce graphique montre l'évolution des ventes trimestrielles en 2024.
    T1: 120k€, T2: 145k€, T3: 168k€, T4: 195k€ (estimation).
  </figcaption>
</figure>

<!-- Option 2 : Lien vers description détaillée -->
<img src="schema-complexe.png" alt="Schéma du processus de fabrication">
<p><a href="description-schema.html">Description détaillée du schéma</a></p>
```

### Rapport de contraste

Assurez-vous que les images avec du texte intégré ont un contraste suffisant :

- **Minimum recommandé** : 4.5:1 pour le texte normal
- **Recommandé** : 7:1 pour une meilleure accessibilité

**Outil** : WebAIM Contrast Checker (https://webaim.org/resources/contrastchecker/)

---

## Attributs HTML5 modernes

### `srcset` et images responsives

L'attribut `srcset` permet de fournir plusieurs versions d'une image pour différentes résolutions d'écran :

```html
<img src="photo.jpg"
     srcset="photo-400.jpg 400w,
             photo-800.jpg 800w,
             photo-1200.jpg 1200w"
     alt="Paysage de montagne"
     sizes="(max-width: 600px) 100vw, 50vw">
```

**Explication :**
- Le navigateur choisit automatiquement l'image la plus appropriée
- `400w`, `800w`, `1200w` indiquent la largeur réelle des images
- `sizes` indique la taille d'affichage selon la largeur de l'écran

*Note : Ce concept sera approfondi dans le chapitre sur le Responsive Design (4.5.5).*

### `decoding`

L'attribut `decoding` indique au navigateur comment gérer le décodage de l'image :

```html
<!-- Décodage asynchrone (non-bloquant) -->
<img src="image.jpg" alt="Description" decoding="async">

<!-- Décodage synchrone (par défaut) -->
<img src="image.jpg" alt="Description" decoding="sync">
```

**Quand utiliser `decoding="async"` :**
- Images non critiques pour le rendu initial
- Images dans une galerie ou un carrousel

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Toujours** inclure l'attribut `alt`
2. Spécifier `width` et `height` pour éviter les sauts de mise en page
3. Optimiser et compresser les images avant upload
4. Choisir le format approprié (JPEG/photo, PNG/logo, WebP/moderne)
5. Utiliser `loading="lazy"` pour les images en bas de page
6. Nommer vos fichiers de façon descriptive (`logo-entreprise.png` plutôt que `img001.png`)
7. Tester vos images sur différents appareils et connexions

### ❌ À ÉVITER

1. Charger des images énormes et les redimensionner avec HTML/CSS
2. Utiliser des images pour du texte
3. Oublier l'attribut `alt`
4. Utiliser des noms de fichiers génériques ou cryptiques
5. Mettre `loading="lazy"` sur l'image principale de la page
6. Ignorer l'optimisation ("ça marche sur mon ordinateur")

---

## Exemple complet

Voici un exemple qui applique toutes les bonnes pratiques :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galerie d'images optimisées</title>
</head>
<body>
    <!-- Image principale (hero) : pas de lazy loading -->
    <img src="hero-paysage.jpg"
         alt="Vue panoramique des Alpes au lever du soleil"
         width="1920"
         height="600">

    <!-- Logo avec transparence -->
    <img src="logo.svg"
         alt="Logo Montagne Aventure"
         width="150"
         height="50">

    <!-- Images de galerie avec lazy loading -->
    <section>
        <h2>Notre galerie</h2>

        <img src="randonnee-1.webp"
             alt="Groupe de randonneurs sur un sentier de montagne"
             width="600"
             height="400"
             loading="lazy">

        <img src="randonnee-2.webp"
             alt="Vue depuis le sommet avec vallée en contrebas"
             width="600"
             height="400"
             loading="lazy">

        <!-- Image décorative -->
        <img src="separateur.svg"
             alt=""
             width="100"
             height="20">
    </section>
</body>
</html>
```

---

## Points clés à retenir

1. **L'attribut `alt` est obligatoire** et crucial pour l'accessibilité
2. **Optimisez toujours vos images** avant de les mettre en ligne
3. **Choisissez le bon format** : JPEG pour photos, PNG pour logos, WebP pour tout (moderne), SVG pour vectoriel
4. **Spécifiez les dimensions** (`width` et `height`) pour améliorer les performances
5. **Utilisez `loading="lazy"`** pour les images non critiques
6. **Nommez vos fichiers intelligemment** : `produit-chaussures-sport.jpg` > `IMG_2847.jpg`

---

## Ressources complémentaires

- **MDN - Images en HTML** : Documentation complète sur `<img>`
- **TinyPNG** : Outil de compression en ligne
- **Can I Use** : Vérifier la compatibilité navigateur des formats WebP, AVIF
- **WebAIM** : Guides d'accessibilité pour les images

---

## Prochaine étape

Dans le prochain chapitre, nous découvrirons les éléments HTML5 **audio et vidéo**, qui utilisent des concepts similaires mais avec leurs propres spécificités.

⏭️ [Éléments audio et vidéo HTML5](/03-html5-structure-et-semantique/03-contenu-multimedia/02-audio-et-video-html5.md)
