🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.1.5 - Ordre de chargement des ressources

## Introduction

Imaginez que vous préparez un gâteau :

❌ **Mauvais ordre :**
1. Mélanger les ingrédients
2. Mettre au four
3. **Ensuite** chercher la farine et les œufs

Résultat : Échec total !

✅ **Bon ordre :**
1. Rassembler tous les ingrédients
2. Mélanger dans le bon ordre
3. Mettre au four

C'est exactement pareil avec un site web ! Le navigateur a besoin de charger les ressources (HTML, CSS, JavaScript, images) dans un **ordre logique** pour que tout fonctionne correctement et rapidement.

### Pourquoi l'ordre est crucial ?

**Performance :** Un mauvais ordre ralentit le chargement de la page

**Fonctionnalité :** JavaScript exécuté trop tôt peut ne pas trouver les éléments HTML

**Expérience utilisateur :** L'utilisateur voit une page qui "saute" pendant le chargement

---

## Le cycle de vie d'une page web

### Vue d'ensemble simplifiée

Quand vous accédez à une page web, voici ce qui se passe dans le navigateur :

```
1. 📥 Télécharger le HTML
2. 📖 Lire le HTML ligne par ligne (parsing)
3. 🔍 Découvrir les ressources (<link>, <script>, <img>)
4. 📥 Télécharger ces ressources
5. 🎨 Appliquer le CSS
6. ⚡ Exécuter le JavaScript
7. 🖼️ Afficher la page
```

### Détails étape par étape

#### Étape 1 : Téléchargement du HTML

```
Navigateur → Serveur : "Je veux index.html"
Serveur → Navigateur : "Voici le fichier"
```

#### Étape 2 : Parsing (lecture) du HTML

Le navigateur lit le HTML **de haut en bas**, ligne par ligne :

```html
<!DOCTYPE html>
<html>
<head>
    <!-- ← Le navigateur est ici -->
    <title>Ma page</title>
    <!-- ← Puis ici -->
    <link rel="stylesheet" href="style.css">
    <!-- ← Puis ici : découvre le CSS, commence à le télécharger -->
</head>
<body>
    <!-- ← Continue de lire -->
    <h1>Titre</h1>
    <!-- ← Encore plus bas -->
    <script src="script.js"></script>
    <!-- ← Ici : découvre le JS, doit l'attendre -->
</body>
</html>
```

#### Étape 3 : Construction du DOM

Au fur et à mesure de la lecture, le navigateur construit le **DOM** (Document Object Model) :

```
html
 ├── head
 │   ├── title
 │   └── link
 └── body
     ├── h1
     └── script
```

#### Étape 4 : Le problème du blocage

Certaines ressources **bloquent** le parsing :

```html
<head>
    <link rel="stylesheet" href="style.css">  <!-- ⏸️ Bloque le rendu -->
</head>
<body>
    <h1>Titre</h1>
    <script src="script.js"></script>  <!-- ⏸️ BLOQUE TOUT -->
    <p>Ce paragraphe attend que le script soit chargé et exécuté</p>
</body>
```

**Pourquoi c'est un problème ?**

Si `script.js` met 3 secondes à charger, l'utilisateur voit une page blanche pendant 3 secondes !

---

## Le problème des scripts bloquants

### Exemple concret du problème

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Problème de chargement</title>
</head>
<body>
    <h1>Bienvenue</h1>

    <!-- ❌ PROBLÈME : Le script bloque ici -->
    <script src="tres-gros-script.js"></script>
    <!-- Pendant que ce script se charge et s'exécute,
         le reste de la page ne s'affiche PAS -->

    <p>Ce texte n'apparaît qu'après le chargement du script</p>
    <img src="image.jpg" alt="Image">
    <footer>Footer</footer>
</body>
</html>
```

**Ce qui se passe :**

1. ✅ L'utilisateur voit `<h1>Bienvenue</h1>`
2. ⏸️ Le navigateur découvre `<script>`
3. ⏸️ **STOP** : il télécharge `tres-gros-script.js` (3 secondes)
4. ⏸️ **STOP** : il exécute le script (0.5 seconde)
5. ✅ Enfin, il continue et affiche le reste

**Résultat :** 3.5 secondes d'attente pour un script !

### Visualisation du blocage

```
Temps écoulé : ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
               0s        1s        2s        3s

HTML parsing : ████████⏸️⏸️⏸️⏸️⏸️⏸️⏸️⏸️⏸️⏸️████
               └─ h1    │                    └─ reste
                        └─ Bloqué par le script

Script :               📥📥📥📥📥📥⚡
                       └─ Téléchargement  └─ Exécution

Affichage :    ████████⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜████
               └─ h1    └─ PAGE BLANCHE    └─ reste
```

---

## Solutions : Où placer les scripts ?

### Solution 1 : À la fin du `<body>` (méthode traditionnelle)

**Principe :** Placer tous les scripts juste avant `</body>`

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Scripts en fin de body</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Tout le contenu HTML -->
    <header>
        <h1>Mon Site</h1>
        <nav>...</nav>
    </header>

    <main>
        <article>...</article>
    </main>

    <footer>...</footer>

    <!-- ✅ Scripts à la fin -->
    <script src="utils.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

**Avantages :**
- ✅ Le HTML est entièrement chargé avant les scripts
- ✅ L'utilisateur voit la page rapidement
- ✅ Le DOM est complet quand le JS s'exécute
- ✅ Fonctionne partout (vieux navigateurs compris)

**Inconvénients :**
- ❌ Les scripts bloquent quand même à la fin
- ❌ Si le script est gros, l'interactivité tarde

**Quand l'utiliser :**
- Projets simples
- Compatibilité avec vieux navigateurs
- Scripts qui ne sont pas critiques

### Solution 2 : Attribut `defer` (recommandé) 🌟

**Principe :** Le script est téléchargé en parallèle, mais exécuté seulement après le parsing du HTML

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Scripts avec defer</title>
    <link rel="stylesheet" href="style.css">

    <!-- ✅ Scripts dans le head avec defer -->
    <script defer src="utils.js"></script>
    <script defer src="app.js"></script>
</head>
<body>
    <h1>Mon Site</h1>
    <!-- Le HTML est parsé normalement -->
    <main>...</main>
</body>
</html>
```

**Comportement :**

```
HTML parsing :  ████████████████████████████
                └─ Pas bloqué !

Script téléch:  📥📥📥📥📥📥
                └─ En parallèle du HTML

Script exécution:                          ⚡
                                           └─ Après le parsing

Affichage :     ████████████████████████████
                └─ Rien n'est bloqué !
```

**Avantages :**
- ✅ **Ne bloque PAS** le parsing HTML
- ✅ Scripts téléchargés **en parallèle**
- ✅ Exécution **après** le parsing du DOM
- ✅ **Ordre d'exécution garanti** (dans l'ordre des balises)
- ✅ Parfait pour les scripts qui manipulent le DOM

**Inconvénients :**
- ❌ Ne fonctionne pas sur très vieux navigateurs (IE9 et avant)

**Quand l'utiliser :**
- ✅ **C'est la solution recommandée dans la plupart des cas**
- ✅ Pour vos scripts principaux
- ✅ Quand vous manipulez le DOM

### Solution 3 : Attribut `async`

**Principe :** Le script est téléchargé en parallèle ET exécuté **dès qu'il est prêt**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Scripts avec async</title>

    <!-- Scripts indépendants avec async -->
    <script async src="analytics.js"></script>
    <script async src="ads.js"></script>
</head>
<body>
    <h1>Mon Site</h1>
</body>
</html>
```

**Comportement :**

```
HTML parsing :  ████████⏸️██████████████
                        └─ Peut être interrompu !

Script téléch:  📥📥📥📥
                └─ En parallèle

Script exécution:       ⚡
                        └─ Dès que prêt (peut bloquer le HTML !)

Affichage :     ████████⬜████████████████
                        └─ Brève pause possible
```

**Avantages :**
- ✅ Téléchargement en parallèle
- ✅ Exécution au plus tôt
- ✅ Bon pour les scripts indépendants

**Inconvénients :**
- ❌ **Ordre d'exécution NON garanti**
- ❌ Peut s'exécuter **avant** que le DOM soit prêt
- ❌ Peut bloquer le parsing pendant l'exécution

**Quand l'utiliser :**
- ✅ Scripts **totalement indépendants** (analytics, publicités)
- ✅ Scripts qui n'ont **pas besoin** du DOM
- ✅ Quand l'ordre n'a **pas d'importance**

---

## Comparaison : defer vs async vs classique

### Tableau récapitulatif

| Critère | Sans attribut | `defer` | `async` |
|---------|--------------|---------|---------|
| **Téléchargement** | Bloque le parsing | Parallèle | Parallèle |
| **Exécution** | Immédiate (bloque) | Après parsing HTML | Dès que prêt |
| **Ordre garanti** | ✅ Oui | ✅ Oui | ❌ Non |
| **Bloque le parsing** | ✅ Oui | ❌ Non | ⚠️ Peut bloquer |
| **DOM disponible** | Dépend de la position | ✅ Toujours | ⚠️ Peut-être pas |
| **Utilisation** | Fin du body | Scripts principaux | Scripts indépendants |

### Visualisation comparative

```html
<!-- 1. Sans attribut (bloquant) -->
<script src="script.js"></script>

HTML: ████⏸️⏸️⏸️████
Script:    📥⚡

<!-- 2. Avec defer (recommandé) -->
<script defer src="script.js"></script>

HTML: ████████████
Script: 📥📥📥   ⚡

<!-- 3. Avec async -->
<script async src="script.js"></script>

HTML: ████⏸️██████
Script: 📥📥⚡
```

### Exemple avec plusieurs scripts

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Comparaison</title>

    <!-- ✅ Bibliothèque utilisée partout : defer -->
    <script defer src="jquery.js"></script>

    <!-- ✅ Script principal : defer -->
    <script defer src="app.js"></script>
    <!-- app.js sera exécuté APRÈS jquery.js -->

    <!-- ✅ Analytics indépendant : async -->
    <script async src="analytics.js"></script>
    <!-- Peut s'exécuter n'importe quand -->
</head>
<body>
    <h1>Ma Page</h1>
</body>
</html>
```

---

## Les modules JavaScript (type="module")

### Comportement par défaut

Les modules ont un comportement **similaire à `defer`** par défaut :

```html
<script type="module" src="app.js"></script>
```

**Équivalent à :**
```html
<script defer src="app.js"></script>
```

**Caractéristiques :**
- ✅ Téléchargement en parallèle
- ✅ Exécution après le parsing HTML
- ✅ Ordre d'exécution garanti
- ✅ Mode strict automatique

### Modules avec async

Vous pouvez aussi combiner module et async :

```html
<!-- Module exécuté dès que prêt -->
<script type="module" async src="analytics-module.js"></script>
```

---

## Le CSS et le chargement

### CSS bloque le rendu

Le CSS **bloque l'affichage** (render blocking) mais pas le parsing HTML :

```html
<head>
    <link rel="stylesheet" href="style.css">
    <!-- Le navigateur attend que le CSS soit chargé
         avant d'afficher quoi que ce soit -->
</head>
```

**Pourquoi ?**
Pour éviter le **FOUC** (Flash Of Unstyled Content) : la page qui apparaît sans style puis "saute" quand le CSS arrive.

### Ordre des CSS

L'ordre des fichiers CSS est important :

```html
<head>
    <!-- ✅ BON : Dans l'ordre logique -->
    <link rel="stylesheet" href="reset.css">      <!-- 1. Reset -->
    <link rel="stylesheet" href="base.css">       <!-- 2. Base -->
    <link rel="stylesheet" href="components.css"> <!-- 3. Composants -->
    <link rel="stylesheet" href="pages.css">      <!-- 4. Pages -->

    <!-- ❌ MAUVAIS : Ordre illogique -->
    <link rel="stylesheet" href="pages.css">
    <link rel="stylesheet" href="reset.css">
    <!-- Le reset écrase les styles de pages ! -->
</head>
```

### CSS critique inline

Pour les performances, on peut mettre le CSS critique directement dans le HTML :

```html
<head>
    <!-- CSS critique inline pour affichage immédiat -->
    <style>
        body { margin: 0; font-family: Arial; }
        .header { background: #333; color: white; }
        /* Uniquement le CSS pour le "above the fold" */
    </style>

    <!-- CSS complet chargé après -->
    <link rel="stylesheet" href="full-styles.css">
</head>
```

---

## Ordre complet recommandé

### Template HTML optimal

Voici la structure optimale pour de bonnes performances :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 1. Meta tags essentiels -->
    <meta name="description" content="Description de la page">
    <title>Titre de la page</title>

    <!-- 2. Preconnect pour les ressources externes -->
    <link rel="preconnect" href="https://fonts.googleapis.com">

    <!-- 3. CSS critique inline (optionnel) -->
    <style>
        /* Styles critiques pour l'affichage initial */
        body { margin: 0; font-family: system-ui; }
        .header { background: #333; }
    </style>

    <!-- 4. CSS externes dans l'ordre logique -->
    <link rel="stylesheet" href="assets/css/reset.css">
    <link rel="stylesheet" href="assets/css/base.css">
    <link rel="stylesheet" href="assets/css/components.css">

    <!-- 5. Polices web -->
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto">

    <!-- 6. Scripts avec defer (dans le head !) -->
    <script defer src="assets/js/utils.js"></script>
    <script defer src="assets/js/app.js"></script>

    <!-- 7. Scripts indépendants avec async -->
    <script async src="https://www.google-analytics.com/analytics.js"></script>

    <!-- 8. Modules ES6 -->
    <script type="module" src="assets/js/main.js"></script>
</head>
<body>
    <!-- Contenu de la page -->
    <header class="header">
        <h1>Mon Site</h1>
    </header>

    <main>
        <article>
            <h2>Article</h2>
            <p>Contenu...</p>
        </article>
    </main>

    <footer>
        <p>&copy; 2025</p>
    </footer>

    <!-- Pas de scripts ici si on utilise defer/async -->
</body>
</html>
```

### Explication de l'ordre

1. **Meta tags** : Toujours en premier pour l'encodage et le viewport
2. **Preconnect** : Établir les connexions tôt pour les ressources externes
3. **CSS inline critique** : Pour afficher rapidement le contenu visible
4. **CSS externes** : Dans l'ordre de spécificité (reset → base → composants → pages)
5. **Polices web** : Après le CSS de base
6. **Scripts avec defer** : Dans le `<head>` pour commencer le téléchargement tôt
7. **Scripts async** : Pour les scripts indépendants (analytics, etc.)
8. **Modules ES6** : Comportement defer par défaut

---

## Techniques avancées de chargement

### 1. Preload

**Dire au navigateur** : "Tu vas avoir besoin de ça, commence à le charger maintenant"

```html
<head>
    <!-- Précharger une police critique -->
    <link rel="preload" href="fonts/main.woff2" as="font" type="font/woff2" crossorigin>

    <!-- Précharger une image hero -->
    <link rel="preload" href="images/hero.jpg" as="image">

    <!-- Précharger un script important -->
    <link rel="preload" href="critical.js" as="script">
</head>
```

**Quand l'utiliser :**
- Ressources critiques utilisées rapidement
- Polices personnalisées
- Images "above the fold"

### 2. Prefetch

**Dire au navigateur** : "Tu auras probablement besoin de ça plus tard"

```html
<head>
    <!-- Précharger la page suivante probable -->
    <link rel="prefetch" href="next-page.html">

    <!-- Précharger des images de la galerie -->
    <link rel="prefetch" href="images/gallery-1.jpg">
</head>
```

**Quand l'utiliser :**
- Ressources de la page suivante
- Contenu que l'utilisateur consultera probablement
- En basse priorité (idle time)

### 3. Preconnect

**Établir la connexion** avec un domaine externe à l'avance :

```html
<head>
    <!-- Se connecter à Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

    <!-- Se connecter à une API -->
    <link rel="preconnect" href="https://api.example.com">
</head>
```

**Quand l'utiliser :**
- CDNs externes
- APIs tierces
- Services de polices

### 4. DNS-Prefetch

**Résoudre le DNS** à l'avance (version allégée de preconnect) :

```html
<head>
    <!-- Résoudre le DNS pour des ressources externes -->
    <link rel="dns-prefetch" href="https://www.google-analytics.com">
    <link rel="dns-prefetch" href="https://cdn.example.com">
</head>
```

### 5. Lazy Loading

**Charger les images uniquement** quand elles sont visibles :

```html
<!-- Images chargées à la demande -->
<img src="image1.jpg" alt="Visible" loading="eager">
<img src="image2.jpg" alt="En bas de page" loading="lazy">
<img src="image3.jpg" alt="En bas de page" loading="lazy">
```

**Attributs :**
- `loading="eager"` : Charge immédiatement (défaut)
- `loading="lazy"` : Charge quand l'image approche du viewport

---

## Problèmes courants et solutions

### Problème 1 : JavaScript ne trouve pas les éléments

**Symptôme :**
```javascript
const button = document.getElementById('myButton');
console.log(button); // null
```

**Cause :** Le script s'exécute avant que le HTML soit chargé

**Solutions :**

```html
<!-- Solution 1 : Script en fin de body -->
<body>
    <button id="myButton">Cliquer</button>
    <script src="app.js"></script>
</body>
```

```html
<!-- Solution 2 : Attribut defer -->
<head>
    <script defer src="app.js"></script>
</head>
<body>
    <button id="myButton">Cliquer</button>
</body>
```

```javascript
// Solution 3 : Attendre le DOMContentLoaded
document.addEventListener('DOMContentLoaded', () => {
    const button = document.getElementById('myButton');
    console.log(button); // ✅ Fonctionne
});
```

### Problème 2 : Scripts exécutés dans le mauvais ordre

**Symptôme :**
```javascript
// app.js essaie d'utiliser jQuery
$('.element').hide(); // Erreur : $ is not defined
```

**Cause :** `app.js` s'exécute avant `jquery.js`

**Solution avec defer :**
```html
<head>
    <!-- ✅ Ordre garanti avec defer -->
    <script defer src="jquery.js"></script>
    <script defer src="app.js"></script>
    <!-- app.js s'exécutera APRÈS jquery.js -->
</head>
```

**❌ Ne fonctionne PAS avec async :**
```html
<head>
    <!-- ❌ Ordre aléatoire avec async -->
    <script async src="jquery.js"></script>
    <script async src="app.js"></script>
    <!-- app.js peut s'exécuter avant jquery.js ! -->
</head>
```

### Problème 3 : Page blanche pendant le chargement

**Cause :** CSS ou scripts bloquants dans le `<head>`

**Solution :**
```html
<head>
    <!-- CSS critique inline -->
    <style>
        body { background: white; margin: 0; }
        .loader { /* Spinner de chargement */ }
    </style>

    <!-- Scripts avec defer -->
    <script defer src="app.js"></script>
</head>
<body>
    <!-- Affichage immédiat -->
    <div class="loader">Chargement...</div>
</body>
```

### Problème 4 : FOUC (Flash Of Unstyled Content)

**Symptôme :** La page apparaît sans style pendant une fraction de seconde

**Cause :** Le CSS charge trop lentement

**Solutions :**

```html
<!-- Solution 1 : CSS critique inline -->
<head>
    <style>
        /* Styles essentiels immédiatement disponibles */
        body { font-family: Arial; margin: 0; }
        .header { background: #333; }
    </style>
    <link rel="stylesheet" href="full-styles.css">
</head>
```

```html
<!-- Solution 2 : Masquer le contenu jusqu'au chargement -->
<head>
    <style>
        html { visibility: hidden; }
        html.loaded { visibility: visible; }
    </style>
    <script>
        window.addEventListener('load', () => {
            document.documentElement.classList.add('loaded');
        });
    </script>
</head>
```

---

## Mesurer les performances

### Outils de mesure

#### 1. DevTools → Network

**Ouvrez les DevTools** (F12) → Onglet **Network** :

- Voir la timeline de chargement
- Identifier les ressources bloquantes
- Mesurer les temps de chargement

**Colonnes importantes :**
- **Name** : Nom du fichier
- **Status** : Code HTTP (200 = OK)
- **Type** : Type de ressource (document, stylesheet, script)
- **Size** : Taille du fichier
- **Time** : Temps de chargement
- **Waterfall** : Timeline visuelle

#### 2. DevTools → Performance

Enregistrer une trace de performance :

1. Ouvrir DevTools → Performance
2. Cliquer sur ⚫ Record
3. Recharger la page
4. Arrêter l'enregistrement
5. Analyser la timeline

**À regarder :**
- **FCP** (First Contentful Paint) : Quand apparaît le premier contenu
- **LCP** (Largest Contentful Paint) : Quand le contenu principal apparaît
- **TTI** (Time To Interactive) : Quand la page devient interactive

#### 3. Lighthouse

Audit automatique de performance :

1. DevTools → Lighthouse
2. Sélectionner "Performance"
3. Cliquer "Generate report"

**Métriques :**
- Performance score (0-100)
- Suggestions d'amélioration
- Opportunités d'optimisation

### Objectifs de performance

**Seuils recommandés :**

| Métrique | Bon | À améliorer | Mauvais |
|----------|-----|-------------|---------|
| **FCP** | < 1.8s | 1.8s - 3s | > 3s |
| **LCP** | < 2.5s | 2.5s - 4s | > 4s |
| **TTI** | < 3.8s | 3.8s - 7.3s | > 7.3s |
| **Total page size** | < 1 MB | 1-3 MB | > 3 MB |

---

## Checklist de chargement optimal

### Pour chaque projet, vérifiez :

#### HTML
- [ ] Meta charset en premier
- [ ] Viewport meta tag présent
- [ ] Titre descriptif

#### CSS
- [ ] CSS critique inline (si nécessaire)
- [ ] CSS externes dans l'ordre logique
- [ ] Polices après le CSS de base
- [ ] Éviter les @import dans le CSS

#### JavaScript
- [ ] Scripts principaux avec `defer` dans le `<head>`
- [ ] Scripts indépendants avec `async`
- [ ] Modules ES6 avec `type="module"`
- [ ] Pas de scripts inline bloquants
- [ ] Code minifié en production

#### Optimisations
- [ ] Preconnect pour les domaines externes
- [ ] Lazy loading pour les images
- [ ] Compression des fichiers (gzip/brotli)
- [ ] Cache navigateur configuré

#### Tests
- [ ] Tester avec Network throttling (3G)
- [ ] Vérifier le score Lighthouse
- [ ] Tester sur mobile
- [ ] Vérifier le FOUC

---

## Exemple complet : Page optimisée

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <!-- 1. Essentiels -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Site performant et optimisé">
    <title>Mon Site Optimisé</title>

    <!-- 2. Preconnect pour ressources externes -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link rel="dns-prefetch" href="https://www.google-analytics.com">

    <!-- 3. Preload ressources critiques -->
    <link rel="preload" href="assets/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
    <link rel="preload" href="assets/images/hero.jpg" as="image">

    <!-- 4. CSS critique inline -->
    <style>
        /* Reset minimal */
        * { margin: 0; padding: 0; box-sizing: border-box; }

        /* Styles critiques pour affichage immédiat */
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            line-height: 1.6;
            color: #333;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 2rem;
            text-align: center;
        }

        .hero {
            background: url('assets/images/hero.jpg') center/cover;
            min-height: 60vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Loader pour le chargement */
        .loader {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 1.5rem;
            color: #667eea;
        }

        .loaded .loader { display: none; }
    </style>

    <!-- 5. CSS complets -->
    <link rel="stylesheet" href="assets/css/base.css">
    <link rel="stylesheet" href="assets/css/components.css">
    <link rel="stylesheet" href="assets/css/responsive.css">

    <!-- 6. Polices web -->
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">

    <!-- 7. Scripts avec defer (chargement optimal) -->
    <script defer src="assets/js/utils.js"></script>
    <script defer src="assets/js/components/slider.js"></script>
    <script defer src="assets/js/components/modal.js"></script>
    <script defer src="assets/js/app.js"></script>

    <!-- 8. Scripts indépendants avec async -->
    <script async src="https://www.google-analytics.com/analytics.js"></script>

    <!-- 9. Module principal -->
    <script type="module" src="assets/js/main.js"></script>

    <!-- 10. Script pour retirer le loader -->
    <script>
        window.addEventListener('load', () => {
            document.documentElement.classList.add('loaded');
        });
    </script>
</head>
<body>
    <!-- Loader initial -->
    <div class="loader" aria-label="Chargement en cours">
        Chargement...
    </div>

    <!-- Header visible immédiatement -->
    <header class="header">
        <h1>Bienvenue sur Mon Site</h1>
        <p>Optimisé pour les performances</p>
    </header>

    <!-- Hero section -->
    <section class="hero">
        <div class="hero__content">
            <h2>Chargement ultra-rapide</h2>
            <button class="btn btn--primary">En savoir plus</button>
        </div>
    </section>

    <!-- Contenu principal -->
    <main class="main">
        <article class="article">
            <h2>Notre approche</h2>
            <p>Nous utilisons les meilleures pratiques de chargement...</p>
        </article>

        <!-- Images avec lazy loading -->
        <section class="gallery">
            <h2>Galerie</h2>
            <!-- Première image eager (visible) -->
            <img src="assets/images/photo1.jpg" alt="Photo 1" loading="eager">

            <!-- Autres images lazy (bas de page) -->
            <img src="assets/images/photo2.jpg" alt="Photo 2" loading="lazy">
            <img src="assets/images/photo3.jpg" alt="Photo 3" loading="lazy">
            <img src="assets/images/photo4.jpg" alt="Photo 4" loading="lazy">
        </section>
    </main>

    <!-- Footer -->
    <footer class="footer">
        <p>&copy; 2025 Mon Site Optimisé</p>
    </footer>
</body>
</html>
```

### Ce qui rend cette page performante :

1. ✅ **CSS critique inline** → Affichage immédiat
2. ✅ **Scripts avec defer** → Pas de blocage
3. ✅ **Preconnect** → Connexions anticipées
4. ✅ **Preload** → Ressources critiques prioritaires
5. ✅ **Lazy loading** → Images chargées à la demande
6. ✅ **Loader** → Retour visuel pendant le chargement
7. ✅ **Ordre optimisé** → Chargement logique et rapide

---

## Résumé

### Les 3 règles d'or du chargement

1. **CSS dans le `<head>`**
   ```html
   <head>
       <link rel="stylesheet" href="style.css">
   </head>
   ```

2. **JavaScript avec `defer` dans le `<head>`**
   ```html
   <head>
       <script defer src="app.js"></script>
   </head>
   ```

3. **Scripts indépendants avec `async`**
   ```html
   <head>
       <script async src="analytics.js"></script>
   </head>
   ```

### Attributs de script : Quand utiliser quoi ?

| Situation | Solution |
|-----------|----------|
| Script qui manipule le DOM | `defer` |
| Scripts avec dépendances | `defer` (ordre garanti) |
| Scripts indépendants | `async` |
| Analytics, ads | `async` |
| Modules ES6 | `type="module"` (defer par défaut) |

### Ordre optimal dans le `<head>` :

```html
<head>
    1. Meta tags (charset, viewport)
    2. Title et description
    3. Preconnect / DNS-prefetch
    4. Preload ressources critiques
    5. CSS critique inline
    6. CSS externes
    7. Polices web
    8. Scripts avec defer
    9. Scripts avec async
    10. Modules ES6
</head>
```

### Métriques à viser :

- **FCP < 1.8s** : Premier contenu visible
- **LCP < 2.5s** : Contenu principal visible
- **TTI < 3.8s** : Page interactive
- **Lighthouse score > 90** : Bonne performance globale

---

## Pour aller plus loin

Vous maîtrisez maintenant l'architecture de projet moderne ! La section suivante abordera :
- **6.2** - Bonnes pratiques de développement pour un code propre et maintenable

L'ordre de chargement peut sembler complexe, mais retenez l'essentiel :
1. **CSS en premier** (dans le head)
2. **Scripts avec defer** (sauf indépendants → async)
3. **Testez et mesurez** avec les DevTools

Avec ces bases solides, vos sites seront rapides et efficaces ! ⚡🚀

⏭️ [Bonnes pratiques de développement](/06-integration-html-css-javascript/02-bonnes-pratiques/README.md)
