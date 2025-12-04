🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.5.3 - Media queries et breakpoints

## Introduction

Les **media queries** sont l'outil principal qui permet d'adapter votre CSS en fonction des caractéristiques de l'appareil, principalement la largeur de l'écran. C'est grâce à elles que votre site peut afficher un menu horizontal sur desktop et un menu burger sur mobile, ou passer de 3 colonnes à 1 colonne sur petit écran.

Associées aux **breakpoints** (points de rupture), les media queries constituent le cœur technique du responsive design.

## Qu'est-ce qu'une media query ?

### Définition simple

Une **media query** est une instruction CSS qui dit : "Applique ces styles **uniquement si** certaines conditions sont remplies".

**Analogie :** C'est comme un interrupteur intelligent :
- "Si l'écran fait plus de 768px de large, alors applique ce style"
- "Si l'écran fait moins de 600px de large, alors applique cet autre style"

### Syntaxe de base

```css
@media (condition) {
    /* Styles à appliquer si la condition est vraie */
    .element {
        propriété: valeur;
    }
}
```

**Exemple concret :**

```css
/* Styles de base (pour tous les écrans) */
.titre {
    font-size: 24px;
    color: blue;
}

/* Styles uniquement si l'écran fait AU MOINS 768px */
@media (min-width: 768px) {
    .titre {
        font-size: 36px; /* Plus grand sur grand écran */
    }
}
```

## Anatomie d'une media query

### Structure détaillée

```css
@media type and (condition) {
    /* Règles CSS */
}
```

**Décomposition :**

| Partie | Description | Exemple |
|--------|-------------|---------|
| `@media` | Mot-clé qui débute la media query | `@media` |
| `type` | Type de média (optionnel) | `screen`, `print`, `all` |
| `and` | Opérateur logique | `and`, `or`, `not` |
| `(condition)` | Condition à tester | `(min-width: 768px)` |
| `{ }` | Bloc contenant les styles | `{ .menu { ... } }` |

### Les types de média

Dans la pratique moderne, on utilise presque toujours `screen` ou on l'omet complètement.

```css
/* Explicite */
@media screen and (min-width: 768px) {
    /* Styles pour écrans de 768px et plus */
}

/* Implicite (équivalent) - RECOMMANDÉ */
@media (min-width: 768px) {
    /* Styles pour écrans de 768px et plus */
}
```

**Autres types (rarement utilisés) :**

```css
/* Styles spécifiques à l'impression */
@media print {
    .bouton {
        display: none; /* Cacher les boutons à l'impression */
    }
}

/* Tous les médias */
@media all {
    /* Styles pour tous les types */
}
```

**💡 Conseil :** Pour le responsive design classique, vous pouvez omettre le type de média.

## Les conditions principales

### 1. min-width (le plus utilisé)

**Signification :** "À partir de cette largeur et au-delà"

```css
/* Styles appliqués quand l'écran fait AU MOINS 768px */
@media (min-width: 768px) {
    .conteneur {
        display: flex;
    }
}
```

**Quand ça s'applique :**
- ✅ Écran de 768px
- ✅ Écran de 800px
- ✅ Écran de 1920px
- ❌ Écran de 767px
- ❌ Écran de 500px

**Usage :** Approche **mobile-first** (on part du mobile et on enrichit pour les grands écrans)

### 2. max-width

**Signification :** "Jusqu'à cette largeur (incluse)"

```css
/* Styles appliqués quand l'écran fait AU MAXIMUM 767px */
@media (max-width: 767px) {
    .menu {
        display: none; /* Menu caché sur mobile */
    }
}
```

**Quand ça s'applique :**
- ✅ Écran de 767px
- ✅ Écran de 500px
- ✅ Écran de 320px
- ❌ Écran de 768px
- ❌ Écran de 1024px

**Usage :** Approche **desktop-first** (on part du desktop et on adapte pour les petits écrans)

### 3. Combiner min-width et max-width

**Pour cibler une plage de largeurs :**

```css
/* Styles appliqués UNIQUEMENT entre 768px et 1023px */
@media (min-width: 768px) and (max-width: 1023px) {
    .conteneur {
        width: 90%;
        /* Styles spécifiques aux tablettes */
    }
}
```

**Quand ça s'applique :**
- ✅ Écran de 768px
- ✅ Écran de 900px
- ✅ Écran de 1023px
- ❌ Écran de 767px (trop petit)
- ❌ Écran de 1024px (trop grand)

### 4. Autres conditions (moins courantes)

#### Hauteur de l'écran

```css
/* Pour les écrans très courts en hauteur */
@media (max-height: 600px) {
    .header {
        height: 60px; /* Header plus compact */
    }
}
```

#### Orientation

```css
/* Mode paysage (landscape) */
@media (orientation: landscape) {
    .image {
        max-width: 50%;
    }
}

/* Mode portrait */
@media (orientation: portrait) {
    .image {
        max-width: 100%;
    }
}
```

#### Résolution d'écran (pour écrans Retina)

```css
/* Écrans haute densité (Retina) */
@media (-webkit-min-device-pixel-ratio: 2),
       (min-resolution: 192dpi) {
    .logo {
        background-image: url('logo@2x.png');
    }
}
```

## Mobile-first vs Desktop-first

### Approche Mobile-first (RECOMMANDÉE) 🆕

**Principe :** On écrit d'abord les styles pour mobile, puis on ajoute des styles pour les écrans plus grands.

```css
/* Styles de BASE pour mobile (sans media query) */
.menu {
    display: block; /* Menu vertical */
    width: 100%;
}

.conteneur {
    padding: 15px;
}

/* Amélioration pour TABLETTE (768px et plus) */
@media (min-width: 768px) {
    .menu {
        display: flex; /* Menu horizontal */
        justify-content: space-between;
    }

    .conteneur {
        padding: 30px;
    }
}

/* Amélioration pour DESKTOP (1024px et plus) */
@media (min-width: 1024px) {
    .conteneur {
        max-width: 1200px;
        margin: 0 auto;
        padding: 40px;
    }
}
```

**Avantages :**
- ✅ Commence par l'essentiel (le mobile représente 60%+ du trafic)
- ✅ Meilleures performances sur mobile (moins de CSS à charger)
- ✅ On ajoute des fonctionnalités progressivement
- ✅ Encourage à penser "contenu d'abord"

**On utilise principalement `min-width`**

### Approche Desktop-first

**Principe :** On écrit d'abord les styles pour desktop, puis on adapte pour les petits écrans.

```css
/* Styles de BASE pour desktop (sans media query) */
.menu {
    display: flex; /* Menu horizontal */
    justify-content: space-between;
}

.conteneur {
    max-width: 1200px;
    margin: 0 auto;
    padding: 40px;
}

/* Adaptation pour TABLETTE (1023px et moins) */
@media (max-width: 1023px) {
    .conteneur {
        padding: 30px;
    }
}

/* Adaptation pour MOBILE (767px et moins) */
@media (max-width: 767px) {
    .menu {
        display: block; /* Menu vertical */
        width: 100%;
    }

    .conteneur {
        padding: 15px;
    }
}
```

**Inconvénients :**
- ❌ Plus complexe (on doit "retirer" des fonctionnalités)
- ❌ Moins performant sur mobile
- ❌ Approche moins naturelle avec les usages actuels

**On utilise principalement `max-width`**

**💡 Recommandation :** Privilégiez **l'approche mobile-first** pour tous vos nouveaux projets !

## Les breakpoints standards

### Qu'est-ce qu'un breakpoint ?

Un **breakpoint** (point de rupture) est une largeur d'écran spécifique à laquelle votre design "change" pour s'adapter.

**Analogie :** Comme un escalier où chaque marche représente une adaptation du design.

### Breakpoints courants (approche mobile-first)

Voici des valeurs standard, mais elles sont **indicatives** :

```css
/* MOBILE PORTRAIT (base) - 320px à 575px */
/* Styles de base, pas de media query */
body {
    font-size: 14px;
}

/* MOBILE PAYSAGE / GRANDS MOBILES - 576px et plus */
@media (min-width: 576px) {
    body {
        font-size: 15px;
    }
}

/* TABLETTE PORTRAIT - 768px et plus */
@media (min-width: 768px) {
    body {
        font-size: 16px;
    }
    .conteneur {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }
}

/* TABLETTE PAYSAGE / PETIT DESKTOP - 992px et plus */
@media (min-width: 992px) {
    .conteneur {
        grid-template-columns: repeat(3, 1fr);
    }
}

/* DESKTOP - 1200px et plus */
@media (min-width: 1200px) {
    body {
        font-size: 18px;
    }
    .conteneur {
        max-width: 1140px;
        margin: 0 auto;
    }
}

/* GRAND ÉCRAN - 1400px et plus */
@media (min-width: 1400px) {
    .conteneur {
        max-width: 1320px;
    }
}
```

### Tableau récapitulatif

| Appareil | Largeur | Breakpoint mobile-first | Breakpoint desktop-first |
|----------|---------|------------------------|-------------------------|
| 📱 Mobile S | 320px - 575px | Styles de base | `max-width: 575px` |
| 📱 Mobile L | 576px - 767px | `min-width: 576px` | `max-width: 767px` |
| 📱 Tablette | 768px - 991px | `min-width: 768px` | `max-width: 991px` |
| 💻 Desktop S | 992px - 1199px | `min-width: 992px` | `max-width: 1199px` |
| 💻 Desktop | 1200px - 1399px | `min-width: 1200px` | `max-width: 1399px` |
| 🖥️ Desktop XL | 1400px+ | `min-width: 1400px` | Styles de base |

**⚠️ Important :** Ces valeurs ne sont **pas gravées dans le marbre** ! Adaptez-les selon votre projet.

### Comment choisir vos breakpoints ?

**❌ Mauvaise approche :** Se baser sur des appareils spécifiques
```
"Je vais mettre un breakpoint à 375px pour l'iPhone X"
```

**✅ Bonne approche :** Se baser sur votre contenu
```
"Mon design se casse à 768px, je mets un breakpoint ici"
```

**Méthode recommandée :**

1. Commencez par designer pour mobile (320px - 375px)
2. Agrandissez progressivement votre navigateur
3. Quand le design commence à "se casser" ou semble bizarre, ajoutez un breakpoint
4. Continuez jusqu'aux grands écrans

**Exemple pratique :**
```css
/* Mobile : texte lisible, 1 colonne */
.grille {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
}

/* À 600px, j'ai assez de place pour 2 colonnes */
@media (min-width: 600px) {
    .grille {
        grid-template-columns: 1fr 1fr;
    }
}

/* À 900px, je peux passer à 3 colonnes */
@media (min-width: 900px) {
    .grille {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

## Opérateurs logiques

### L'opérateur AND

**Pour combiner plusieurs conditions :**

```css
/* Écran ENTRE 768px ET 1023px, ET en mode paysage */
@media (min-width: 768px) and (max-width: 1023px) and (orientation: landscape) {
    .conteneur {
        display: flex;
    }
}
```

**Toutes les conditions doivent être vraies.**

### L'opérateur OR (virgule)

**Pour appliquer les styles si AU MOINS une condition est vraie :**

```css
/* Petit mobile OU impression */
@media (max-width: 600px), print {
    .publicite {
        display: none;
    }
}
```

**L'une OU l'autre condition (ou les deux) doit être vraie.**

### L'opérateur NOT

**Pour inverser une condition :**

```css
/* Tout SAUF les écrans */
@media not screen {
    body {
        color: black;
    }
}
```

**Rarement utilisé en pratique.**

## Exemples concrets et complets

### Exemple 1 : Layout responsive simple

```css
/* MOBILE - 1 colonne */
.conteneur {
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 15px;
}

.carte {
    width: 100%;
    padding: 20px;
    background: white;
    border-radius: 8px;
}

/* TABLETTE - 2 colonnes */
@media (min-width: 768px) {
    .conteneur {
        flex-direction: row;
        flex-wrap: wrap;
        padding: 30px;
    }

    .carte {
        width: calc(50% - 10px); /* 2 colonnes avec gap */
    }
}

/* DESKTOP - 3 colonnes */
@media (min-width: 1024px) {
    .carte {
        width: calc(33.333% - 14px); /* 3 colonnes avec gap */
    }
}
```

### Exemple 2 : Navigation responsive

```css
/* MOBILE - Menu burger */
.nav-menu {
    display: none; /* Caché par défaut */
    position: fixed;
    top: 60px;
    left: 0;
    width: 100%;
    background: white;
    flex-direction: column;
}

.nav-menu.active {
    display: flex; /* Visible quand activé par JS */
}

.menu-toggle {
    display: block; /* Bouton burger visible */
    font-size: 24px;
}

/* TABLETTE/DESKTOP - Menu horizontal permanent */
@media (min-width: 768px) {
    .nav-menu {
        display: flex !important; /* Toujours visible */
        position: static;
        flex-direction: row;
        justify-content: space-between;
    }

    .menu-toggle {
        display: none; /* Bouton burger caché */
    }
}
```

### Exemple 3 : Typographie responsive

```css
/* MOBILE */
body {
    font-size: 16px;
    line-height: 1.5;
}

h1 {
    font-size: 28px;
    margin-bottom: 15px;
}

h2 {
    font-size: 22px;
    margin-bottom: 12px;
}

/* TABLETTE */
@media (min-width: 768px) {
    body {
        font-size: 17px;
        line-height: 1.6;
    }

    h1 {
        font-size: 36px;
        margin-bottom: 20px;
    }

    h2 {
        font-size: 28px;
        margin-bottom: 15px;
    }
}

/* DESKTOP */
@media (min-width: 1024px) {
    body {
        font-size: 18px;
        line-height: 1.7;
    }

    h1 {
        font-size: 48px;
        margin-bottom: 25px;
    }

    h2 {
        font-size: 36px;
        margin-bottom: 20px;
    }
}
```

## Organisation du code

### Structure recommandée

**Option 1 : Media queries à la fin du fichier**

```css
/* ===== STYLES DE BASE (MOBILE) ===== */
body { font-size: 16px; }
.conteneur { padding: 15px; }
.menu { display: block; }

/* ===== TABLETTE ===== */
@media (min-width: 768px) {
    body { font-size: 17px; }
    .conteneur { padding: 30px; }
    .menu { display: flex; }
}

/* ===== DESKTOP ===== */
@media (min-width: 1024px) {
    body { font-size: 18px; }
    .conteneur { padding: 40px; }
}
```

**Avantage :** Vue d'ensemble claire de la progression responsive.

**Option 2 : Media queries par composant**

```css
/* MENU */
.menu {
    display: block;
    /* Styles mobile */
}

@media (min-width: 768px) {
    .menu {
        display: flex;
        /* Styles tablette+ */
    }
}

/* CONTENEUR */
.conteneur {
    padding: 15px;
    /* Styles mobile */
}

@media (min-width: 768px) {
    .conteneur {
        padding: 30px;
        /* Styles tablette+ */
    }
}
```

**Avantage :** Tous les styles d'un composant regroupés ensemble.

**💡 Conseil :** Choisissez une approche et restez cohérent dans tout votre projet !

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier la balise viewport

```html
<!-- Sans cette balise, les media queries ne fonctionnent pas ! -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### ❌ Erreur 2 : Breakpoints qui se chevauchent

```css
/* MAUVAIS - Conflit à 768px */
@media (max-width: 768px) {
    .element { color: red; }
}

@media (min-width: 768px) {
    .element { color: blue; }
}

/* À 768px, quelle couleur ? Les deux s'appliquent ! */
```

**Solution :**
```css
/* BON - Pas de chevauchement */
@media (max-width: 767px) {
    .element { color: red; }
}

@media (min-width: 768px) {
    .element { color: blue; }
}
```

### ❌ Erreur 3 : Trop de breakpoints

```css
/* Trop complexe ! */
@media (min-width: 320px) { ... }
@media (min-width: 375px) { ... }
@media (min-width: 414px) { ... }
@media (min-width: 480px) { ... }
@media (min-width: 600px) { ... }
/* etc. */
```

**Solution :** 3 à 5 breakpoints suffisent généralement :
- Mobile (base)
- Tablette (768px)
- Desktop (1024px ou 1200px)
- Éventuellement un intermédiaire et un très grand écran

### ❌ Erreur 4 : Ordre incorrect (mobile-first)

```css
/* MAUVAIS ORDRE */
@media (min-width: 1024px) {
    .element { font-size: 20px; }
}

.element {
    font-size: 16px; /* Écrase le style ci-dessus ! */
}
```

**Solution :**
```css
/* BON ORDRE - Base d'abord, puis media queries */
.element {
    font-size: 16px; /* Mobile */
}

@media (min-width: 1024px) {
    .element {
        font-size: 20px; /* Desktop */
    }
}
```

### ❌ Erreur 5 : Utiliser des pixels partout

```css
/* Moins flexible */
@media (min-width: 768px) {
    .element {
        width: 600px; /* Fixe */
        padding: 30px;
    }
}
```

**Solution :**
```css
/* Plus flexible */
@media (min-width: 768px) {
    .element {
        width: 80%; /* Relatif */
        max-width: 600px;
        padding: 2rem; /* Relatif */
    }
}
```

## Tester vos media queries

### Dans le navigateur (DevTools)

1. **Ouvrir les DevTools** : F12 ou Clic droit > Inspecter
2. **Activer le mode responsive** : Icône smartphone/tablette ou Ctrl+Shift+M
3. **Changer la largeur** :
   - Avec les presets (iPhone, iPad, etc.)
   - Ou manuellement en faisant glisser
4. **Observer les changements** de style

### Astuce : Afficher les breakpoints actifs

Ajoutez temporairement ce code pour visualiser quel breakpoint est actif :

```css
body::before {
    content: 'Mobile';
    position: fixed;
    top: 0;
    left: 0;
    background: red;
    color: white;
    padding: 5px 10px;
    z-index: 9999;
}

@media (min-width: 576px) {
    body::before {
        content: 'Mobile L';
        background: orange;
    }
}

@media (min-width: 768px) {
    body::before {
        content: 'Tablette';
        background: green;
    }
}

@media (min-width: 1024px) {
    body::before {
        content: 'Desktop';
        background: blue;
    }
}
```

Un petit badge apparaîtra en haut à gauche vous indiquant le breakpoint actif !

## Récapitulatif

Les **media queries** permettent d'adapter vos styles CSS selon les caractéristiques de l'écran.

**Syntaxe de base :**
```css
@media (condition) {
    /* Styles */
}
```

**Conditions principales :**
- `min-width` : à partir de cette largeur (mobile-first ✅)
- `max-width` : jusqu'à cette largeur (desktop-first)
- Combinaison : `(min-width: X) and (max-width: Y)`

**Approche recommandée : Mobile-first** 🆕
- Styles de base pour mobile
- Ajout progressif avec `min-width`

**Breakpoints standards (indicatifs) :**
- 576px : Grands mobiles
- 768px : Tablette
- 992px ou 1024px : Desktop
- 1200px : Grand desktop

**Règles d'or :**
- ✅ Toujours ajouter la balise viewport
- ✅ Préférer mobile-first
- ✅ 3-5 breakpoints suffisent
- ✅ Baser les breakpoints sur le contenu, pas sur les appareils
- ✅ Tester sur de vrais appareils

---

**📚 Points à retenir :**

- Les media queries sont le **cœur** du responsive design
- `min-width` = mobile-first (recommandé)
- `max-width` = desktop-first
- Les breakpoints ne sont **pas** basés sur des appareils spécifiques
- **3 à 5 breakpoints** suffisent pour la plupart des projets
- Testez avec les **DevTools** du navigateur

**🔜 Prochaine étape :**
Dans la section suivante (4.5.4), nous allons découvrir les **unités relatives** (%, em, rem, vw, vh) qui rendent vos designs encore plus flexibles et responsive.

**💡 Astuce de pro :**
Créez un fichier CSS séparé pour vos media queries ou utilisez des variables CSS pour stocker vos breakpoints. Cela facilitera la maintenance !

⏭️ [Unités relatives : %, em, rem, vw, vh](/04-css3-styles-et-mise-en-page/05-responsive-design/04-unites-relatives.md)
