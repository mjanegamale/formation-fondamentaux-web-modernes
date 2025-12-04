🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.5.2 - Meta viewport

## Introduction

La balise **meta viewport** est une petite ligne de code HTML qui a un impact énorme sur l'affichage de votre site web sur mobile. Sans elle, votre site responsive ne fonctionnera tout simplement pas correctement sur smartphone et tablette.

C'est l'une des **premières choses à ajouter** dans tout projet web moderne !

## Qu'est-ce que le viewport ?

### Définition simple

Le **viewport** (littéralement "fenêtre de visualisation") est la zone visible de la page web dans votre navigateur.

**Analogie :** Imaginez que votre page web est une grande affiche et que le viewport est une fenêtre à travers laquelle vous la regardez. Sur un ordinateur, la fenêtre est grande. Sur un smartphone, elle est petite.

### Le problème historique

Avant l'ère des smartphones, les sites web étaient conçus pour des écrans d'ordinateur (environ 1000px de large). Quand les premiers smartphones sont apparus, ils avaient de petits écrans (320px de large par exemple).

**Le dilemme des navigateurs mobiles :**
- Si le site s'affiche à 320px, il sera illisible (texte minuscule)
- Solution trouvée : faire **semblant** que l'écran fait 980px de large, puis zoomer/dézoomer

**Résultat :** Les sites s'affichent en tout petit, et l'utilisateur doit zoomer manuellement. Pas idéal !

## La balise meta viewport : la solution

### Syntaxe de base (à connaître par cœur !)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon site responsive</title>
</head>
<body>
    <!-- Contenu du site -->
</body>
</html>
```

Cette balise **doit toujours être placée dans le `<head>`** de votre document HTML, idéalement juste après la balise `<meta charset>`.

### Décortiquons cette balise

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Décomposition :**

| Partie | Signification |
|--------|---------------|
| `<meta>` | Balise de métadonnées HTML |
| `name="viewport"` | Type de métadonnée : configuration du viewport |
| `content="..."` | Valeur de la configuration |
| `width=device-width` | La largeur du viewport = largeur de l'appareil |
| `initial-scale=1.0` | Le zoom initial est à 100% (1.0) |

## Comprendre chaque attribut

### 1. width=device-width

**Ce que ça fait :** Dit au navigateur que le viewport doit avoir la même largeur que l'appareil physique.

**Sans cette directive :**
```
Smartphone de 375px → Le navigateur fait semblant que l'écran fait 980px
```

**Avec cette directive :**
```
Smartphone de 375px → Le viewport fait effectivement 375px
```

**Exemples concrets :**
- iPhone SE : 375px de large → viewport de 375px
- iPad : 768px de large → viewport de 768px
- Desktop : 1920px de large → viewport de 1920px

### 2. initial-scale=1.0

**Ce que ça fait :** Définit le niveau de zoom initial quand la page se charge.

**Valeurs possibles :**
- `initial-scale=1.0` : 100% (taille normale) ✅ **Recommandé**
- `initial-scale=0.5` : 50% (page zoomée en arrière)
- `initial-scale=2.0` : 200% (page agrandie)

**Pourquoi 1.0 ?** C'est le plus naturel : l'utilisateur voit la page à sa taille normale et peut zoomer lui-même s'il le souhaite.

### 3. Autres attributs (optionnels)

Il existe d'autres attributs, mais ils sont rarement utilisés :

#### maximum-scale et minimum-scale

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0,
      maximum-scale=5.0, minimum-scale=0.5">
```

- `maximum-scale` : Zoom maximum autorisé
- `minimum-scale` : Zoom minimum autorisé

**⚠️ Attention :** Limiter le zoom peut nuire à l'accessibilité. Les personnes malvoyantes ont besoin de pouvoir zoomer !

#### user-scalable

```html
<!-- ❌ DÉCONSEILLÉ -->
<meta name="viewport" content="width=device-width, initial-scale=1.0,
      user-scalable=no">
```

- `user-scalable=no` : Désactive complètement le zoom

**❌ À éviter absolument !** Cela rend votre site inaccessible pour les personnes ayant des problèmes de vision. C'est une très mauvaise pratique et peut même pénaliser votre référencement.

## Comparaison visuelle : avec vs sans viewport

### Scénario 1 : Sans balise viewport ❌

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <!-- PAS de balise viewport ! -->
    <title>Mon site</title>
    <style>
        body {
            font-size: 16px;
            padding: 20px;
        }
        .contenu {
            max-width: 1200px;
            background: lightblue;
        }
    </style>
</head>
<body>
    <div class="contenu">
        <h1>Bienvenue sur mon site</h1>
        <p>Ceci est mon contenu...</p>
    </div>
</body>
</html>
```

**Résultat sur smartphone :**
- Le navigateur fait semblant que l'écran fait 980px de large
- Tout apparaît minuscule
- L'utilisateur doit zoomer manuellement
- Le texte de 16px est illisible
- Expérience utilisateur catastrophique 😢

### Scénario 2 : Avec balise viewport ✅

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon site</title>
    <style>
        body {
            font-size: 16px;
            padding: 20px;
        }
        .contenu {
            max-width: 1200px;
            background: lightblue;
        }
    </style>
</head>
<body>
    <div class="contenu">
        <h1>Bienvenue sur mon site</h1>
        <p>Ceci est mon contenu...</p>
    </div>
</body>
</html>
```

**Résultat sur smartphone :**
- Le viewport fait la vraie largeur de l'écran (375px par exemple)
- Le texte de 16px est parfaitement lisible
- Pas besoin de zoomer
- Les media queries CSS fonctionnent correctement
- Expérience utilisateur optimale 🎉

## Impact sur les media queries

La balise viewport est **essentielle** pour que vos media queries CSS fonctionnent !

### Avec viewport ✅

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

```css
/* CSS */
.menu {
    display: block; /* Menu vertical par défaut */
}

@media (min-width: 768px) {
    .menu {
        display: flex; /* Menu horizontal sur tablette/desktop */
    }
}
```

**Résultat :** Sur un smartphone de 375px, le menu reste vertical. Sur une tablette de 768px+, il devient horizontal. ✅

### Sans viewport ❌

```html
<!-- Pas de balise viewport -->
```

```css
/* Même CSS */
.menu {
    display: block;
}

@media (min-width: 768px) {
    .menu {
        display: flex;
    }
}
```

**Résultat :** Le navigateur mobile fait semblant que l'écran fait 980px, donc la media query `(min-width: 768px)` est **toujours activée**, même sur un petit smartphone. Le menu horizontal apparaît sur mobile, ce qui n'était pas voulu ! ❌

## Cas d'usage particuliers

### Sites non-responsive (héritage)

Si vous maintenez un **très vieux site non-responsive** (déconseillé), vous pourriez vouloir :

```html
<meta name="viewport" content="width=1024">
```

Cela fixe le viewport à 1024px. Le site apparaîtra zoomé en arrière sur mobile, mais au moins il sera entièrement visible.

**⚠️ Ceci n'est pas une bonne pratique !** Il vaut mieux rendre le site responsive.

### Applications web (PWA)

Pour les Progressive Web Apps, vous pourriez ajouter :

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0,
      viewport-fit=cover">
```

- `viewport-fit=cover` : Permet d'utiliser toute la surface de l'écran, même sur les iPhones avec encoche.

## Configuration recommandée (à utiliser systématiquement)

Pour **99% des projets web modernes**, utilisez cette configuration :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Description de votre site">
    <title>Titre de votre site</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Votre contenu -->
</body>
</html>
```

**C'est tout !** Simple, efficace, et suffisant pour la grande majorité des cas.

## Vérifier que ça fonctionne

### Méthode 1 : DevTools du navigateur

1. Ouvrez votre page dans Chrome ou Firefox
2. Ouvrez les DevTools (F12)
3. Activez le mode responsive (icône de smartphone/tablette)
4. Changez la taille de l'écran simulé

**Si la balise viewport est présente :**
- Le contenu s'adapte à la taille de l'écran simulé
- Les media queries fonctionnent correctement

**Si elle est absente :**
- Le site apparaît minuscule à 980px de large
- Les media queries ne fonctionnent pas comme prévu

### Méthode 2 : Test sur appareil réel

Le meilleur test reste de consulter votre site sur un vrai smartphone :

- Texte lisible sans zoomer ? ✅
- Pas de scroll horizontal ? ✅
- Éléments bien dimensionnés ? ✅

Si tout est bon, c'est que votre viewport est correctement configuré !

## Erreurs courantes

### ❌ Erreur 1 : Oublier la balise

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <!-- Oups, pas de viewport ! -->
    <title>Mon site</title>
</head>
```

**Conséquence :** Le site n'est pas responsive, même avec des media queries parfaites.

### ❌ Erreur 2 : Faute de frappe

```html
<!-- Mal écrit -->
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Attendez, celui-ci est en fait **correct** ! `initial-scale=1` équivaut à `initial-scale=1.0`.

Mais attention à :
```html
<!-- Vraie erreur -->
<meta name="viewport" content="width=devise-width, initial-scale=1.0">
<!-- "devise" au lieu de "device" -->
```

### ❌ Erreur 3 : Désactiver le zoom

```html
<!-- Mauvaise pratique -->
<meta name="viewport" content="width=device-width, initial-scale=1.0,
      user-scalable=no, maximum-scale=1.0">
```

**Problème :** Les personnes malvoyantes ne peuvent plus zoomer. C'est un problème d'accessibilité grave !

### ❌ Erreur 4 : Placer la balise au mauvais endroit

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mon site</title>
</head>
<body>
    <!-- ❌ Trop tard, ça doit être dans <head> ! -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</body>
</html>
```

La balise viewport **doit être dans `<head>`**, pas dans `<body>`.

## Compatibilité navigateurs

La balise meta viewport est supportée par **tous les navigateurs modernes** :

- ✅ Chrome (Android & Desktop)
- ✅ Safari (iOS & macOS)
- ✅ Firefox (Android & Desktop)
- ✅ Edge
- ✅ Opera
- ✅ Samsung Internet

**Même Internet Explorer 10+** la supporte (bien qu'IE ne soit plus maintenu).

## Récapitulatif

La balise **meta viewport** est **obligatoire** pour tout site responsive moderne.

**Configuration standard (à mémoriser) :**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Ce qu'elle fait :**
- Indique au navigateur mobile d'utiliser la vraie largeur de l'appareil
- Définit le zoom initial à 100%
- Permet aux media queries de fonctionner correctement

**Où la placer :**
- Dans le `<head>` du document HTML
- Idéalement après `<meta charset="UTF-8">`

**Ce qu'il ne faut PAS faire :**
- ❌ Oublier cette balise
- ❌ Désactiver le zoom (`user-scalable=no`)
- ❌ Limiter excessivement le zoom (problème d'accessibilité)

---

**📚 Points à retenir :**

- La balise viewport est **indispensable** pour le responsive design
- Sans elle, votre site apparaîtra minuscule sur mobile
- La configuration `width=device-width, initial-scale=1.0` convient à 99% des projets
- Ne **jamais** désactiver le zoom (accessibilité)
- Placez-la dans le `<head>`, avant vos CSS

**🔜 Prochaine étape :**
Maintenant que le viewport est configuré, nous allons voir en détail les **media queries** (section 4.5.3) pour adapter nos styles CSS selon la taille de l'écran.

**💡 Astuce de pro :**
Créez-vous un snippet (modèle de code) dans votre éditeur avec la structure HTML de base incluant la balise viewport. Vous gagnerez du temps sur chaque nouveau projet !

⏭️ [Media queries et breakpoints](/04-css3-styles-et-mise-en-page/05-responsive-design/03-media-queries-breakpoints.md)
