🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.6.1 - Transitions CSS : durée, délai, timing-function

## Introduction

Les **transitions CSS** permettent de créer des animations fluides et élégantes lorsqu'une propriété CSS change de valeur. Au lieu d'un changement brutal et instantané, la transition crée une progression douce et agréable à l'œil.

**Sans transition :**
```
Couleur bleue → [INSTANTANÉ] → Couleur rouge
```

**Avec transition :**
```
Couleur bleue → [PROGRESSION FLUIDE] → Couleur rouge
```

Les transitions améliorent considérablement l'expérience utilisateur en rendant votre site plus vivant et professionnel.

## Pourquoi utiliser des transitions ?

### Amélioration de l'expérience utilisateur

**Sans transitions :**
- Changements brusques et saccadés
- Interface qui semble "cheap" ou amateur
- Manque de feedback visuel

**Avec transitions :**
- Animations fluides et naturelles
- Interface moderne et professionnelle
- Feedback visuel clair pour l'utilisateur

### Exemples d'utilisation courante

```css
/* Bouton qui change de couleur au survol */
button:hover {
    background-color: blue;
    /* Avec transition = changement fluide */
}

/* Menu qui apparaît */
.menu {
    opacity: 0;
    /* Avec transition = fade-in élégant */
}

.menu.visible {
    opacity: 1;
}

/* Image qui grossit au survol */
img:hover {
    transform: scale(1.1);
    /* Avec transition = zoom progressif */
}
```

## Comparaison : avec et sans transition

### Exemple : bouton au survol

**Sans transition ❌**

```css
.bouton {
    background-color: #3498db;
    color: white;
    padding: 15px 30px;
    border: none;
    border-radius: 5px;
}

.bouton:hover {
    background-color: #2980b9; /* Changement BRUTAL */
}
```

**Résultat :** Le fond change instantanément. C'est fonctionnel mais pas élégant.

**Avec transition ✅**

```css
.bouton {
    background-color: #3498db;
    color: white;
    padding: 15px 30px;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s ease; /* MAGIE ! */
}

.bouton:hover {
    background-color: #2980b9; /* Changement FLUIDE */
}
```

**Résultat :** Le fond change progressivement en 0.3 seconde. C'est professionnel et agréable !

## La propriété transition

### Syntaxe de base

```css
.element {
    transition: propriété durée timing-function délai;
}
```

**Exemple :**
```css
.element {
    transition: background-color 0.3s ease 0s;
    /*          ↑              ↑    ↑    ↑
    /*          propriété      durée fonction délai
    */
}
```

### Version simplifiée (la plus courante)

```css
.element {
    transition: background-color 0.3s;
    /* Suffit dans 90% des cas ! */
}
```

## Les 4 sous-propriétés de transition

La propriété `transition` est en fait un raccourci pour 4 propriétés distinctes :

| Sous-propriété | Description | Exemple |
|----------------|-------------|---------|
| `transition-property` | Quelle propriété animer | `background-color` |
| `transition-duration` | Combien de temps | `0.3s` |
| `transition-timing-function` | Comment (courbe d'animation) | `ease` |
| `transition-delay` | Délai avant le début | `0.1s` |

Vous pouvez les écrire séparément ou utiliser le raccourci `transition`.

## 1. transition-property : Quoi animer ?

### Syntaxe

```css
.element {
    transition-property: background-color;
}
```

### Valeurs possibles

#### Propriété spécifique

```css
.element {
    transition-property: background-color; /* Anime uniquement le fond */
}

.element:hover {
    background-color: red;
    color: white;         /* Pas de transition sur color */
}
```

#### Plusieurs propriétés

```css
.element {
    transition-property: background-color, color, transform;
    /* Séparez par des virgules */
}
```

#### Toutes les propriétés (all)

```css
.element {
    transition-property: all; /* Anime TOUTES les propriétés qui changent */
}
```

**💡 Conseil :** `all` est pratique mais peut être moins performant. Préférez nommer les propriétés spécifiques quand possible.

### Propriétés qui peuvent être animées

**✅ Propriétés animables :**
- `color`, `background-color`
- `width`, `height`
- `opacity`
- `transform` (position, rotation, échelle)
- `padding`, `margin`
- `border-color`, `border-width`
- `font-size`
- `top`, `left`, `right`, `bottom` (avec position)

**❌ Propriétés NON animables :**
- `display` (ne peut pas être animé)
- `font-family`
- `position`
- `visibility` (on/off, pas de progression)

**Exemple de ce qui ne fonctionne PAS :**

```css
.element {
    display: none;
    transition: display 0.3s; /* ❌ N'a aucun effet ! */
}

.element.visible {
    display: block;
}
```

**Solution : utilisez `opacity` et `visibility` :**

```css
.element {
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.3s, visibility 0.3s;
}

.element.visible {
    opacity: 1;
    visibility: visible;
}
```

## 2. transition-duration : Combien de temps ?

### Syntaxe

```css
.element {
    transition-duration: 0.3s; /* 0.3 seconde = 300 millisecondes */
}
```

### Unités de temps

**Secondes (s) :**
```css
transition-duration: 0.3s;  /* 300 millisecondes */
transition-duration: 1s;    /* 1 seconde */
transition-duration: 2.5s;  /* 2.5 secondes */
```

**Millisecondes (ms) :**
```css
transition-duration: 300ms; /* Équivaut à 0.3s */
transition-duration: 1000ms; /* Équivaut à 1s */
```

**💡 Convention :** On utilise généralement les secondes (s) car c'est plus lisible.

### Durées recommandées selon le type d'animation

| Type d'animation | Durée recommandée | Exemple |
|------------------|-------------------|---------|
| **Changement de couleur** | 0.2s - 0.3s | Hover de bouton |
| **Déplacement léger** | 0.3s - 0.5s | Menu qui glisse |
| **Apparition/disparition** | 0.3s - 0.4s | Fade-in/fade-out |
| **Transformation complexe** | 0.4s - 0.6s | Rotation, zoom |
| **Animation longue** | 0.8s - 1.5s | Loader, effet spectaculaire |

**⚠️ Attention :** Des animations trop longues (> 1s) peuvent frustrer l'utilisateur !

### Exemples pratiques

#### Animation rapide (changement de couleur)

```css
.bouton {
    background-color: blue;
    transition-duration: 0.2s; /* Rapide et réactif */
}

.bouton:hover {
    background-color: darkblue;
}
```

#### Animation moyenne (apparition de menu)

```css
.menu {
    opacity: 0;
    transition-duration: 0.4s; /* Ni trop rapide, ni trop lent */
}

.menu.visible {
    opacity: 1;
}
```

#### Animation lente (effet spectaculaire)

```css
.logo {
    transform: scale(1);
    transition-duration: 1s; /* Animation longue pour effet "wow" */
}

.logo:hover {
    transform: scale(1.5) rotate(360deg);
}
```

### Durées différentes pour plusieurs propriétés

```css
.element {
    transition-property: background-color, transform;
    transition-duration: 0.3s, 0.6s;
    /*                   ↑     ↑
    /*                   background = 0.3s
    /*                   transform = 0.6s
    */
}
```

## 3. transition-timing-function : Comment animer ?

La **timing-function** contrôle la **courbe d'accélération** de l'animation. C'est ce qui donne le "feeling" de l'animation.

### Les valeurs prédéfinies

#### ease (par défaut)

```css
transition-timing-function: ease;
```

**Comportement :** Commence doucement, accélère au milieu, ralentit à la fin.

**Courbe :** Lent → Rapide → Lent

**Usage :** Animation naturelle et agréable. **C'est la valeur par défaut et la plus utilisée.**

```css
.bouton {
    background-color: blue;
    transition: background-color 0.3s ease;
}
```

#### linear

```css
transition-timing-function: linear;
```

**Comportement :** Vitesse constante du début à la fin.

**Courbe :** Constant

**Usage :** Rotations continues, animations mécaniques.

```css
.loader {
    transform: rotate(0deg);
    transition: transform 1s linear;
}

.loader.spinning {
    transform: rotate(360deg);
}
```

#### ease-in

```css
transition-timing-function: ease-in;
```

**Comportement :** Commence lentement, accélère progressivement.

**Courbe :** Lent → Rapide

**Usage :** Éléments qui "tombent" ou "accélèrent".

```css
.element {
    opacity: 1;
    transition: opacity 0.5s ease-in;
}

.element.hidden {
    opacity: 0; /* Disparaît en accélérant */
}
```

#### ease-out

```css
transition-timing-function: ease-out;
```

**Comportement :** Commence rapidement, ralentit progressivement.

**Courbe :** Rapide → Lent

**Usage :** Éléments qui "arrivent" ou "se posent". **Très naturel pour les apparitions.**

```css
.modal {
    opacity: 0;
    transform: translateY(-50px);
    transition: opacity 0.4s ease-out, transform 0.4s ease-out;
}

.modal.visible {
    opacity: 1;
    transform: translateY(0); /* Arrive en douceur */
}
```

#### ease-in-out

```css
transition-timing-function: ease-in-out;
```

**Comportement :** Commence lentement, accélère au milieu, ralentit à la fin (plus prononcé que `ease`).

**Courbe :** Lent → Rapide → Lent

**Usage :** Animations symétriques, va-et-vient.

```css
.element {
    transform: translateX(0);
    transition: transform 0.6s ease-in-out;
}

.element.moved {
    transform: translateX(100px);
}
```

### Tableau comparatif

| Timing Function | Début | Milieu | Fin | Usage typique |
|-----------------|-------|--------|-----|---------------|
| `ease` | Lent | Rapide | Lent | **Par défaut, la plus naturelle** |
| `linear` | Constant | Constant | Constant | Rotations, mouvements mécaniques |
| `ease-in` | Lent | → | Rapide | Éléments qui accélèrent |
| `ease-out` | Rapide | → | Lent | **Apparitions naturelles** |
| `ease-in-out` | Lent | Rapide | Lent | Mouvements symétriques |

### Visualiser les courbes

Imaginez une voiture qui démarre et s'arrête :

- **ease :** Démarrage tranquille, accélère, freine en douceur 🚗
- **linear :** Vitesse de croisière constante 🚗💨
- **ease-in :** Démarre doucement, accélère fort à la fin 🚗💨💨
- **ease-out :** Démarre fort, freine progressivement 🚗🛑
- **ease-in-out :** Comme ease mais plus prononcé

### cubic-bezier() : courbe personnalisée

Pour un contrôle total, utilisez `cubic-bezier()` :

```css
transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
```

**Exemple - effet "bounce" :**
```css
.element {
    transform: scale(1);
    transition: transform 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.element:hover {
    transform: scale(1.1); /* "Rebondit" légèrement */
}
```

**💡 Outil :** Utilisez [cubic-bezier.com](https://cubic-bezier.com/) pour créer et tester vos courbes !

### steps() : animation par étapes

Pour des animations "saccadées" (comme un sprite sheet) :

```css
transition-timing-function: steps(4); /* 4 étapes distinctes */
```

**Exemple :**
```css
.sprite {
    background-position: 0 0;
    transition: background-position 0.8s steps(8);
}

.sprite.animate {
    background-position: -800px 0; /* Saute de 100px en 100px (8 fois) */
}
```

## 4. transition-delay : Quand démarrer ?

Le **délai** définit combien de temps attendre **avant** de commencer l'animation.

### Syntaxe

```css
.element {
    transition-delay: 0.2s; /* Attend 200ms avant de commencer */
}
```

### Quand utiliser un délai ?

#### 1. Effet de cascade

```css
.item-1 { transition-delay: 0s; }
.item-2 { transition-delay: 0.1s; }
.item-3 { transition-delay: 0.2s; }
.item-4 { transition-delay: 0.3s; }

/* Les éléments apparaissent les uns après les autres */
```

**Résultat :** Animation en cascade élégante !

#### 2. Éviter les animations accidentelles

```css
.tooltip {
    opacity: 0;
    transition: opacity 0.3s;
    transition-delay: 0.5s; /* N'apparaît que si on reste 0.5s */
}

.bouton:hover .tooltip {
    opacity: 1;
}
```

**Résultat :** Le tooltip n'apparaît que si l'utilisateur survole vraiment (évite les apparitions accidentelles).

#### 3. Animation complexe en plusieurs étapes

```css
.element {
    /* Première étape : opacité change immédiatement */
    transition: opacity 0.3s 0s,
    /* Deuxième étape : position change après 0.3s */
                transform 0.3s 0.3s;
}
```

### Exemple pratique : menu qui apparaît

```html
<nav class="menu">
    <a href="#" class="item-1">Accueil</a>
    <a href="#" class="item-2">Services</a>
    <a href="#" class="item-3">Portfolio</a>
    <a href="#" class="item-4">Contact</a>
</nav>
```

```css
.menu a {
    opacity: 0;
    transform: translateY(-20px);
    transition: opacity 0.4s ease-out, transform 0.4s ease-out;
}

.menu.visible a {
    opacity: 1;
    transform: translateY(0);
}

/* Délais en cascade */
.menu .item-1 { transition-delay: 0s; }
.menu .item-2 { transition-delay: 0.1s; }
.menu .item-3 { transition-delay: 0.2s; }
.menu .item-4 { transition-delay: 0.3s; }
```

**Résultat :** Les liens apparaissent les uns après les autres. Magnifique !

## La propriété raccourcie transition

### Syntaxe complète

```css
.element {
    transition: propriété durée timing-function délai;
}
```

### Exemples d'utilisation

#### Version minimale (la plus courante)

```css
.element {
    transition: background-color 0.3s;
    /* propriété + durée */
}
```

#### Avec timing-function

```css
.element {
    transition: transform 0.5s ease-out;
    /* propriété + durée + timing */
}
```

#### Version complète

```css
.element {
    transition: opacity 0.4s ease-in 0.2s;
    /* propriété + durée + timing + délai */
}
```

#### Plusieurs propriétés

```css
.element {
    transition: background-color 0.3s ease,
                transform 0.5s ease-out,
                opacity 0.4s ease-in 0.2s;
    /* Virgules pour séparer */
}
```

#### Tout animer (all)

```css
.element {
    transition: all 0.3s ease;
    /* Anime toutes les propriétés qui changent */
}
```

**⚠️ Attention :** `all` peut affecter la performance. Utilisez-le avec parcimonie.

## Exemples complets et pratiques

### Exemple 1 : Bouton moderne

```html
<button class="btn">Cliquez-moi</button>
```

```css
.btn {
    background-color: #3498db;
    color: white;
    padding: 15px 30px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    transform: translateY(0);

    /* Transitions fluides */
    transition: background-color 0.3s ease,
                transform 0.2s ease,
                box-shadow 0.2s ease;
}

.btn:hover {
    background-color: #2980b9;
    transform: translateY(-2px); /* Légère élévation */
    box-shadow: 0 4px 8px rgba(0,0,0,0.3); /* Ombre plus forte */
}

.btn:active {
    transform: translateY(0); /* Retour position normale */
    box-shadow: 0 1px 3px rgba(0,0,0,0.2); /* Ombre réduite */
}
```

**Résultat :** Bouton qui s'élève au survol et s'enfonce au clic !

### Exemple 2 : Card avec effet hover

```html
<div class="card">
    <img src="photo.jpg" alt="Photo">
    <h3>Titre</h3>
    <p>Description de la carte...</p>
</div>
```

```css
.card {
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    overflow: hidden;
    transform: translateY(0) scale(1);
    transition: transform 0.3s ease-out,
                box-shadow 0.3s ease-out;
}

.card:hover {
    transform: translateY(-8px) scale(1.02);
    box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

.card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    transition: transform 0.3s ease-out;
}

.card:hover img {
    transform: scale(1.1); /* Image zoome légèrement */
}

.card h3 {
    padding: 15px;
    color: #333;
    transition: color 0.3s ease;
}

.card:hover h3 {
    color: #3498db;
}
```

### Exemple 3 : Menu navigation responsive

```html
<nav class="navbar">
    <ul>
        <li><a href="#">Accueil</a></li>
        <li><a href="#">Services</a></li>
        <li><a href="#">Portfolio</a></li>
        <li><a href="#">Contact</a></li>
    </ul>
</nav>
```

```css
.navbar a {
    color: #333;
    text-decoration: none;
    padding: 10px 20px;
    display: inline-block;
    position: relative;
    transition: color 0.3s ease;
}

/* Trait qui apparaît en dessous */
.navbar a::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 0;
    height: 2px;
    background-color: #3498db;
    transform: translateX(-50%);
    transition: width 0.3s ease-out;
}

.navbar a:hover {
    color: #3498db;
}

.navbar a:hover::after {
    width: 80%; /* Le trait s'étend */
}
```

### Exemple 4 : Image avec overlay

```html
<div class="image-container">
    <img src="photo.jpg" alt="Photo">
    <div class="overlay">
        <h3>Titre de l'image</h3>
        <p>Description courte</p>
    </div>
</div>
```

```css
.image-container {
    position: relative;
    overflow: hidden;
    border-radius: 8px;
}

.image-container img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    transition: transform 0.5s ease-out;
}

.overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(transparent, rgba(0,0,0,0.8));
    color: white;
    padding: 30px 20px;
    transform: translateY(100%); /* Caché en dessous */
    transition: transform 0.4s ease-out;
}

.image-container:hover img {
    transform: scale(1.1);
}

.image-container:hover .overlay {
    transform: translateY(0); /* Remonte au survol */
}

.overlay h3 {
    margin-bottom: 10px;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.4s ease-out 0.1s,
                transform 0.4s ease-out 0.1s;
}

.overlay p {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.4s ease-out 0.2s,
                transform 0.4s ease-out 0.2s;
}

.image-container:hover .overlay h3,
.image-container:hover .overlay p {
    opacity: 1;
    transform: translateY(0);
}
```

**Résultat :** Overlay qui glisse avec texte qui apparaît en cascade !

## Bonnes pratiques

### ✅ À faire

**1. Restez subtil**
```css
/* BON - Animation subtile */
transition: transform 0.3s ease;
```

**2. Durées appropriées**
```css
/* BON - Rapide pour interactions simples */
.bouton {
    transition: background-color 0.2s;
}
```

**3. Transitions performantes**
```css
/* BON - transform et opacity sont très performants */
transition: transform 0.3s, opacity 0.3s;
```

**4. Prévisibilité**
```css
/* BON - L'utilisateur comprend ce qui se passe */
.element:hover {
    transform: translateY(-5px);
    transition: transform 0.3s ease-out;
}
```

### ❌ À éviter

**1. Animations trop longues**
```css
/* MAUVAIS - Trop long, frustrant */
transition: all 3s;
```

**2. Trop de propriétés animées**
```css
/* MAUVAIS - Peut causer des saccades */
transition: all 0.3s; /* Anime TOUT, même ce qui n'a pas besoin */
```

**3. Propriétés gourmandes**
```css
/* MAUVAIS - Très coûteux en performance */
transition: width 0.3s, height 0.3s;

/* MEILLEUR - Utilisez transform à la place */
transition: transform 0.3s; /* scale() au lieu de width/height */
```

**4. Animations sans but**
```css
/* MAUVAIS - Animation gratuite qui ne sert à rien */
.texte {
    transition: color 2s; /* Pourquoi le texte changerait de couleur ? */
}
```

## Performance et optimisation

### Propriétés performantes vs coûteuses

**⚡ Très performantes (GPU) :**
- `transform` (translate, scale, rotate)
- `opacity`

**⚠️ Moyennement performantes :**
- `color`, `background-color`
- `box-shadow`

**❌ Coûteuses (éviter si possible) :**
- `width`, `height`
- `margin`, `padding`
- `top`, `left`, `right`, `bottom`

### Exemple d'optimisation

**❌ Version non optimisée :**
```css
.element {
    width: 100px;
    transition: width 0.3s;
}

.element:hover {
    width: 150px; /* Coûteux ! */
}
```

**✅ Version optimisée :**
```css
.element {
    width: 100px;
    transition: transform 0.3s;
}

.element:hover {
    transform: scaleX(1.5); /* Performant ! */
}
```

### Astuce : will-change

Pour des animations complexes, prévenez le navigateur :

```css
.element {
    will-change: transform, opacity;
    transition: transform 0.3s, opacity 0.3s;
}
```

**⚠️ Attention :** N'utilisez `will-change` que sur des éléments qui seront réellement animés souvent. L'abus peut dégrader les performances.

## Compatibilité navigateurs

Les transitions CSS sont **très bien supportées** par tous les navigateurs modernes depuis 2012.

**Support :**
- ✅ Chrome (toutes versions récentes)
- ✅ Firefox (toutes versions récentes)
- ✅ Safari (toutes versions récentes)
- ✅ Edge (toutes versions)
- ✅ Mobile (iOS Safari, Chrome Android)

**Préfixes vendeur (obsolètes) :**
```css
/* Ancienne syntaxe (ne devrait plus être nécessaire) */
-webkit-transition: all 0.3s;
-moz-transition: all 0.3s;
-o-transition: all 0.3s;
transition: all 0.3s;
```

**💡 Aujourd'hui :** Vous n'avez besoin QUE de `transition` sans préfixe !

## Récapitulatif

Les **transitions CSS** permettent de créer des animations fluides et professionnelles.

**Syntaxe de base :**
```css
transition: propriété durée timing-function délai;
```

**Les 4 composants :**
1. **property** : Ce qui est animé (`background-color`, `transform`, etc.)
2. **duration** : Combien de temps (0.2s à 0.5s généralement)
3. **timing-function** : Comment (`ease`, `ease-out`, `linear`, etc.)
4. **delay** : Délai avant le début (optionnel)

**Durées recommandées :**
- Changements simples : **0.2s - 0.3s**
- Mouvements : **0.3s - 0.5s**
- Effets complexes : **0.5s - 0.8s**

**Timing-functions populaires :**
- `ease` : naturel et équilibré (par défaut)
- `ease-out` : apparitions naturelles
- `ease-in-out` : mouvements symétriques

**Performance :**
- ✅ Préférez `transform` et `opacity`
- ❌ Évitez d'animer `width`, `height`, `margin`

**Bonnes pratiques :**
- Restez subtil (0.2s - 0.5s)
- Animations avec un but précis
- Testez sur différents appareils
- Préférez nommer les propriétés plutôt que `all`

---

**📚 Points à retenir :**

- Les transitions améliorent l'**expérience utilisateur**
- Syntaxe simple : `transition: propriété durée;`
- Durées courtes (0.2s-0.5s) pour la plupart des cas
- `ease` et `ease-out` sont les plus naturels
- `transform` et `opacity` sont très performants
- Soyez subtil, pas excessif !

**🔜 Prochaine étape :**
Dans la section suivante (4.6.2), nous découvrirons la propriété **transform** qui permet des transformations visuelles (déplacement, rotation, échelle) que nous pourrons animer avec les transitions !

**💡 Astuce :**
Ajoutez `transition: all 0.3s ease;` sur vos boutons et liens. C'est un moyen rapide de rendre votre site plus professionnel, même si ce n'est pas l'approche la plus optimisée !

⏭️ [Transform : translate, rotate, scale, skew](/04-css3-styles-et-mise-en-page/06-transitions-et-animations/02-transform.md)
