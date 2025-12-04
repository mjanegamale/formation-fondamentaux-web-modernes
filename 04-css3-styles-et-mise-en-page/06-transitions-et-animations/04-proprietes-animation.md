🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.6.4 - Propriétés d'animation

## Introduction

Dans la section précédente (4.6.3), nous avons vu comment créer des animations avec `@keyframes` et utilisé les propriétés de base. Dans cette section, nous allons **approfondir chaque propriété d'animation**, explorer des techniques avancées, et voir comment combiner ces propriétés pour créer des animations complexes et professionnelles.

Cette section est un guide de référence détaillé qui vous permettra de maîtriser complètement les animations CSS.

## Rappel : La syntaxe raccourcie

```css
.element {
    animation: name duration timing-function delay iteration-count direction fill-mode play-state;
}
```

**Ordre à retenir (mnémotechnique : "NDTDIDFP") :**
1. **N**ame (nom)
2. **D**uration (durée)
3. **T**iming-function (courbe)
4. **D**elay (délai)
5. **I**teration-count (répétitions)
6. **D**irection (sens)
7. **F**ill-mode (état avant/après)
8. **P**lay-state (état lecture)

**💡 Astuce :** Vous n'êtes pas obligé de tout spécifier. Les valeurs par défaut sont souvent suffisantes.

## 1. animation-name : Le nom de l'animation

### Syntaxe et règles

```css
.element {
    animation-name: slideIn;
}
```

**Règles de nommage :**
- ✅ Lettres, chiffres, tirets (-), underscores (_)
- ✅ Sensible à la casse : `fadeIn` ≠ `fadein`
- ❌ Pas d'espaces
- ❌ Ne peut pas commencer par un chiffre

**Exemples valides :**
```css
animation-name: slideIn;
animation-name: fade-in-left;
animation-name: bounce_effect;
animation-name: moveElement2;
```

**Exemples invalides :**
```css
animation-name: slide in;      /* ❌ Espace */
animation-name: 2bounce;       /* ❌ Commence par un chiffre */
animation-name: fade@effect;   /* ❌ Caractère spécial */
```

### Valeur spéciale : none

```css
.element {
    animation-name: none; /* Désactive l'animation */
}
```

**Usage :** Désactiver une animation dans certaines conditions :

```css
.element {
    animation-name: bounce;
}

@media (prefers-reduced-motion: reduce) {
    .element {
        animation-name: none; /* Pas d'animation pour ceux qui préfèrent */
    }
}
```

### Appliquer plusieurs animations

```css
.element {
    animation-name: fadeIn, slideUp, rotate;
    animation-duration: 1s, 0.5s, 2s;
    /* Chaque animation a sa propre durée */
}
```

**⚠️ Important :** Si vous spécifiez plusieurs animations, les autres propriétés doivent également être définies pour chacune (ou elles utiliseront les valeurs par défaut).

### Convention de nommage recommandée

**Style descriptif :**
```css
@keyframes fadeIn { }
@keyframes slideInLeft { }
@keyframes bounceOnce { }
@keyframes rotateClockwise { }
```

**Style avec préfixe (pour organisation) :**
```css
@keyframes anim-fade-in { }
@keyframes anim-slide-left { }
@keyframes effect-glow { }
@keyframes loader-spin { }
```

**💡 Conseil :** Choisissez une convention et restez cohérent dans tout votre projet.

## 2. animation-duration : La durée

### Syntaxe et unités

```css
.element {
    animation-duration: 2s;      /* Secondes */
    animation-duration: 500ms;   /* Millisecondes */
    animation-duration: 0.5s;    /* Équivaut à 500ms */
}
```

**Conversion :**
- `1s` = `1000ms`
- `0.5s` = `500ms`
- `0.3s` = `300ms`

### Durées par type d'effet

| Type d'animation | Durée recommandée | Exemple |
|------------------|-------------------|---------|
| **Micro-interaction** | 100-200ms | Checkbox check |
| **Fade simple** | 200-300ms | Apparition texte |
| **Slide/Move** | 300-500ms | Menu qui glisse |
| **Bounce/Spring** | 400-700ms | Effet rebond |
| **Rotation** | 500ms-1s | Logo qui tourne |
| **Animation complexe** | 1s-2s | Séquence élaborée |
| **Loader continu** | 1s-2s | Spinner |
| **Animation décorative** | 2s-5s | Particules flottantes |

### Exemples pratiques

#### Animation rapide (feedback utilisateur)

```css
@keyframes checkmark {
    0% {
        transform: scale(0);
    }
    50% {
        transform: scale(1.2);
    }
    100% {
        transform: scale(1);
    }
}

.checkbox:checked + .icon {
    animation-duration: 200ms; /* Rapide et réactif */
}
```

#### Animation normale (apparition d'élément)

```css
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.modal {
    animation-duration: 400ms; /* Ni trop rapide, ni trop lent */
}
```

#### Animation lente (effet spectaculaire)

```css
@keyframes floatUp {
    from {
        transform: translateY(100px);
        opacity: 0;
    }
    to {
        transform: translateY(0);
        opacity: 1;
    }
}

.hero-element {
    animation-duration: 1.5s; /* Lent et majestueux */
}
```

### Durée 0 pour désactiver

```css
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0s !important;
        /* Désactive toutes les animations */
    }
}
```

### Durées différentes pour plusieurs animations

```css
.element {
    animation-name: fadeIn, rotate, pulse;
    animation-duration: 0.5s, 2s, 1s;
    /*                  ↑     ↑    ↑
    /*               fadeIn rotate pulse
    */
}
```

## 3. animation-timing-function : La courbe d'accélération

### Les fonctions prédéfinies en détail

#### ease (par défaut)

```css
animation-timing-function: ease;
```

**Courbe :** Commence lentement, accélère rapidement, ralentit à la fin.

**Équivalent cubic-bezier :** `cubic-bezier(0.25, 0.1, 0.25, 1)`

**Idéal pour :** La plupart des animations. C'est la plus naturelle.

```css
.button {
    animation: slideIn 0.5s ease;
    /* Entrée douce et naturelle */
}
```

#### linear

```css
animation-timing-function: linear;
```

**Courbe :** Vitesse constante du début à la fin.

**Équivalent cubic-bezier :** `cubic-bezier(0, 0, 1, 1)`

**Idéal pour :** Rotations continues, déplacements mécaniques.

```css
.loader {
    animation: spin 1s linear infinite;
    /* Rotation à vitesse constante */
}
```

#### ease-in

```css
animation-timing-function: ease-in;
```

**Courbe :** Commence lentement, accélère progressivement.

**Équivalent cubic-bezier :** `cubic-bezier(0.42, 0, 1, 1)`

**Idéal pour :** Éléments qui disparaissent, tombent.

```css
.modal {
    animation: fadeOut 0.5s ease-in forwards;
    /* Disparaît en accélérant */
}
```

#### ease-out

```css
animation-timing-function: ease-out;
```

**Courbe :** Commence rapidement, ralentit progressivement.

**Équivalent cubic-bezier :** `cubic-bezier(0, 0, 0.58, 1)`

**Idéal pour :** Éléments qui apparaissent, se posent. **Très recommandé pour les apparitions !**

```css
.notification {
    animation: slideInRight 0.4s ease-out;
    /* Arrive rapidement puis se pose doucement */
}
```

#### ease-in-out

```css
animation-timing-function: ease-in-out;
```

**Courbe :** Commence lentement, accélère au milieu, ralentit à la fin.

**Équivalent cubic-bezier :** `cubic-bezier(0.42, 0, 0.58, 1)`

**Idéal pour :** Mouvements symétriques, va-et-vient.

```css
.pendulum {
    animation: swing 2s ease-in-out infinite alternate;
    /* Balancement naturel */
}
```

### cubic-bezier() : Courbes personnalisées

```css
animation-timing-function: cubic-bezier(x1, y1, x2, y2);
```

**Les 4 valeurs contrôlent deux points sur la courbe de Bézier.**

#### Courbes populaires

**Bounce (rebond) :**
```css
animation-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
```

**Easing rapide et fluide :**
```css
animation-timing-function: cubic-bezier(0.25, 0.46, 0.45, 0.94);
```

**Easing avec anticipation :**
```css
animation-timing-function: cubic-bezier(0.68, -0.6, 0.32, 1.6);
/* Recule légèrement avant d'avancer */
```

**Easing dramatique :**
```css
animation-timing-function: cubic-bezier(0.95, 0.05, 0.795, 0.035);
/* Très rapide au début, très lent à la fin */
```

#### Outil pour créer des courbes

**Utilisez [cubic-bezier.com](https://cubic-bezier.com/) ou [easings.net](https://easings.net/)** pour créer et tester vos courbes visuellement !

**Exemple d'utilisation :**

```css
@keyframes bounceIn {
    from {
        transform: scale(0);
        opacity: 0;
    }
    to {
        transform: scale(1);
        opacity: 1;
    }
}

.element {
    animation: bounceIn 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    /* Effet "pop" avec léger dépassement */
}
```

### steps() : Animation par étapes

```css
animation-timing-function: steps(nombre, position);
```

**Paramètres :**
- `nombre` : nombre d'étapes
- `position` : `start` ou `end` (optionnel)

**Usage :** Animations saccadées, sprite sheets, compteurs.

#### Exemple : Sprite animation

```css
@keyframes run {
    from {
        background-position-x: 0;
    }
    to {
        background-position-x: -800px; /* 8 frames × 100px */
    }
}

.character {
    width: 100px;
    height: 100px;
    background: url('sprite-run.png') no-repeat;
    animation: run 0.8s steps(8) infinite;
    /* 8 images dans le sprite */
}
```

#### Exemple : Compteur qui s'incrémente

```css
@keyframes count {
    from {
        content: "0";
    }
    to {
        content: "100";
    }
}

.counter::after {
    content: "0";
    animation: count 2s steps(100) forwards;
    /* Change de 1 en 1 */
}
```

#### step-start vs step-end

```css
/* Change immédiatement au début de chaque étape */
animation-timing-function: step-start;
/* Équivaut à steps(1, start) */

/* Change à la fin de chaque étape (défaut) */
animation-timing-function: step-end;
/* Équivaut à steps(1, end) */
```

### Timing-function par keyframe

Vous pouvez définir une timing-function différente pour chaque segment :

```css
@keyframes complex {
    0% {
        transform: translateX(0);
        animation-timing-function: ease-out; /* Pour 0% → 50% */
    }
    50% {
        transform: translateX(100px);
        animation-timing-function: ease-in; /* Pour 50% → 100% */
    }
    100% {
        transform: translateX(0);
    }
}
```

## 4. animation-delay : Le délai avant le début

### Syntaxe et usage

```css
.element {
    animation-delay: 0.5s; /* Attend 500ms avant de commencer */
}
```

### Délai positif (attente)

```css
.element {
    animation: fadeIn 1s;
    animation-delay: 1s; /* Démarre après 1 seconde */
}
```

**Usage :** Créer des séquences, effets de cascade.

#### Exemple : Cascade d'apparition

```css
.item-1 { animation-delay: 0s; }
.item-2 { animation-delay: 0.1s; }
.item-3 { animation-delay: 0.2s; }
.item-4 { animation-delay: 0.3s; }
.item-5 { animation-delay: 0.4s; }
```

#### Exemple : Animation en plusieurs phases

```css
.element {
    /* Phase 1 : Fade in (démarre immédiatement) */
    animation: fadeIn 0.5s;
}

.element::after {
    /* Phase 2 : Apparition du contenu (après fade in) */
    animation: slideIn 0.5s;
    animation-delay: 0.5s; /* Démarre quand fadeIn se termine */
}
```

### Délai négatif (démarrage avancé)

```css
.element {
    animation: spin 4s linear infinite;
    animation-delay: -2s; /* Démarre à mi-parcours de l'animation */
}
```

**Effet :** L'animation démarre comme si elle avait déjà tourné pendant 2 secondes.

**Usage :** Synchroniser plusieurs animations, éviter que toutes démarrent au même point.

#### Exemple : Loaders désynchronisés

```css
.dot-1 {
    animation: bounce 1.5s ease-in-out infinite;
    animation-delay: 0s;
}

.dot-2 {
    animation: bounce 1.5s ease-in-out infinite;
    animation-delay: -0.3s; /* Commence 0.3s "dans" l'animation */
}

.dot-3 {
    animation: bounce 1.5s ease-in-out infinite;
    animation-delay: -0.6s; /* Commence 0.6s "dans" l'animation */
}
```

**Résultat :** Les trois points ne sont jamais synchronisés, créant un mouvement fluide.

### Délais multiples

```css
.element {
    animation-name: fadeIn, rotate;
    animation-duration: 1s, 2s;
    animation-delay: 0s, 0.5s;
    /*               ↑    ↑
    /*            fadeIn  rotate
    /* fadeIn démarre immédiatement
    /* rotate démarre après 0.5s
    */
}
```

## 5. animation-iteration-count : Le nombre de répétitions

### Syntaxe et valeurs

```css
.element {
    animation-iteration-count: 3; /* Se répète 3 fois */
}
```

**Valeurs possibles :**
- Nombre entier : `1`, `2`, `3`, `10`, etc.
- Nombre décimal : `0.5`, `2.5`, `1.75`
- `infinite` : à l'infini

### Nombre entier

```css
@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
}

.button {
    animation: pulse 0.5s ease-in-out 3;
    /* Pulse 3 fois puis s'arrête */
}
```

**Usage :** Attirer l'attention temporairement.

### Nombre décimal

```css
.element {
    animation: rotate 2s linear 0.5;
    /* Tourne à moitié (180°) puis s'arrête */
}
```

**Usage :** Animation partielle, effet unique.

#### Exemple : Demi-rotation

```css
@keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

.element {
    animation: rotate 1s linear 0.5;
    /* Ne fait qu'un demi-tour (180°) */
}
```

### infinite : Animation continue

```css
.loader {
    animation: spin 1s linear infinite;
    /* Tourne indéfiniment */
}
```

**⚠️ Attention :** Utilisez `infinite` avec parcimonie :
- ✅ Loaders, spinners
- ✅ Animations de fond subtiles
- ❌ Animations distrayantes
- ❌ Éléments de contenu

#### Exemple : Loader classique

```css
@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

.spinner {
    width: 50px;
    height: 50px;
    border: 5px solid #f3f3f3;
    border-top-color: #3498db;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}
```

#### Exemple : Particules flottantes (background)

```css
@keyframes float {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    33% { transform: translateY(-20px) rotate(120deg); }
    66% { transform: translateY(-10px) rotate(240deg); }
}

.particle {
    animation: float 8s ease-in-out infinite;
    /* Flotte doucement à l'infini */
}
```

### Itérations multiples pour plusieurs animations

```css
.element {
    animation-name: fadeIn, pulse, rotate;
    animation-duration: 1s, 0.5s, 3s;
    animation-iteration-count: 1, 3, infinite;
    /*                         ↑  ↑  ↑
    /*                      fadeIn pulse rotate
    /* fadeIn: 1 fois
    /* pulse: 3 fois
    /* rotate: infini
    */
}
```

## 6. animation-direction : Le sens de l'animation

### Les 4 valeurs expliquées

#### normal (par défaut)

```css
animation-direction: normal;
```

**Comportement :** 0% → 100% → 0% → 100% (si répété)

**Schéma :**
```
Itération 1: 0% ────> 100%
Itération 2: 0% ────> 100%
Itération 3: 0% ────> 100%
```

#### reverse

```css
animation-direction: reverse;
```

**Comportement :** 100% → 0% → 100% → 0% (inverse)

**Schéma :**
```
Itération 1: 100% <──── 0%
Itération 2: 100% <──── 0%
Itération 3: 100% <──── 0%
```

**Usage :** Inverser une animation existante sans réécrire les keyframes.

```css
@keyframes slideInLeft {
    from { transform: translateX(-100px); }
    to { transform: translateX(0); }
}

.element-out {
    animation: slideInLeft 0.5s reverse;
    /* Utilise la même animation mais à l'envers = slideOutRight */
}
```

#### alternate ⭐ (le plus utile)

```css
animation-direction: alternate;
```

**Comportement :** 0% → 100% → 100% → 0% → 0% → 100% (va-et-vient)

**Schéma :**
```
Itération 1: 0% ────> 100%
Itération 2: 100% <──── 0%
Itération 3: 0% ────> 100%
```

**Usage :** Animations de va-et-vient, balancement, respiration.

**💡 C'est la valeur la plus utilisée avec `infinite` !**

```css
@keyframes breathe {
    from { transform: scale(1); }
    to { transform: scale(1.05); }
}

.element {
    animation: breathe 2s ease-in-out infinite alternate;
    /* Grandit puis rétrécit, grandit puis rétrécit... */
}
```

#### alternate-reverse

```css
animation-direction: alternate-reverse;
```

**Comportement :** 100% → 0% → 0% → 100% → 100% → 0% (va-et-vient inversé)

**Schéma :**
```
Itération 1: 100% <──── 0%
Itération 2: 0% ────> 100%
Itération 3: 100% <──── 0%
```

**Usage :** Commence par la fin puis alterne.

### Exemples pratiques

#### Balancier parfait

```css
@keyframes swing {
    from { transform: rotate(-15deg); }
    to { transform: rotate(15deg); }
}

.pendulum {
    transform-origin: top center;
    animation: swing 1s ease-in-out infinite alternate;
    /* Gauche → Droite → Gauche → Droite... */
}
```

#### Pulsation continue

```css
@keyframes pulse {
    from {
        transform: scale(1);
        opacity: 1;
    }
    to {
        transform: scale(1.1);
        opacity: 0.8;
    }
}

.notification-badge {
    animation: pulse 1.5s ease-in-out infinite alternate;
    /* Pulse en continu */
}
```

#### Slide in puis slide out

```css
@keyframes slide {
    from { transform: translateX(-100%); }
    to { transform: translateX(0); }
}

.notification {
    animation: slide 0.5s ease-out 2 alternate;
    /*                                ↑  ↑
    /*                            2 fois alternate
    /* Entre à gauche, ressort à gauche */
}
```

## 7. animation-fill-mode : L'état avant/après

### Comprendre le problème

Sans `fill-mode`, voici ce qui se passe :

```css
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.element {
    opacity: 1; /* État par défaut */
    animation: fadeIn 1s;
}
```

**Timeline :**
```
Avant animation: opacity: 1 (visible)
Pendant animation: opacity: 0 → 1
Après animation: opacity: 1 (retour à l'état par défaut)
```

**Problème :** L'élément est visible avant l'animation, disparaît au début de l'animation, puis réapparaît. Pas fluide !

### Les 4 valeurs expliquées

#### none (par défaut)

```css
animation-fill-mode: none;
```

**Comportement :**
- **Avant :** style par défaut de l'élément
- **Pendant :** styles de l'animation
- **Après :** retour au style par défaut

**Usage :** Rarement voulu pour les animations d'apparition/disparition.

#### forwards ⭐ (le plus important)

```css
animation-fill-mode: forwards;
```

**Comportement :**
- **Avant :** style par défaut de l'élément
- **Pendant :** styles de l'animation
- **Après :** **conserve le style du dernier keyframe**

**C'est la valeur la plus utilisée !**

```css
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.element {
    opacity: 0; /* Caché par défaut */
    animation: fadeIn 1s forwards;
    /* Reste visible après l'animation ✅ */
}
```

**Sans forwards :**
```
Avant: opacity: 0 (caché)
Pendant: opacity: 0 → 1 (apparaît)
Après: opacity: 0 (disparaît ❌)
```

**Avec forwards :**
```
Avant: opacity: 0 (caché)
Pendant: opacity: 0 → 1 (apparaît)
Après: opacity: 1 (reste visible ✅)
```

#### backwards

```css
animation-fill-mode: backwards;
```

**Comportement :**
- **Avant (avec delay) :** applique le style du **premier keyframe**
- **Pendant :** styles de l'animation
- **Après :** retour au style par défaut

**Usage :** Quand vous voulez que l'élément soit dans l'état initial pendant le délai.

```css
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.element {
    opacity: 1; /* Visible par défaut */
    animation: fadeIn 1s 2s backwards;
    /*                    ↑  ↑
    /*                durée délai
}
```

**Avec backwards :**
```
Avant le délai (2s): opacity: 0 (style du premier keyframe ✅)
Pendant délai: opacity: 0 (reste caché)
Pendant animation: opacity: 0 → 1
Après: opacity: 1 (retour au défaut)
```

**Sans backwards :**
```
Avant le délai (2s): opacity: 1 (visible ❌)
Pendant délai: opacity: 1 (visible)
Pendant animation: opacity: 0 → 1 (saut visible ❌)
Après: opacity: 1
```

#### both

```css
animation-fill-mode: both;
```

**Comportement :** Combine `forwards` et `backwards`.

**Usage :** Quand vous avez un délai ET que vous voulez conserver l'état final.

```css
.element {
    opacity: 1;
    animation: fadeIn 1s 2s both;
    /*                    ↑  ↑
    /*                durée délai
    /* Avant délai: opacity: 0 (backwards)
    /* Après animation: opacity: 1 (forwards)
    */
}
```

### Tableau récapitulatif

| fill-mode | Avant animation | Pendant délai | Après animation |
|-----------|----------------|---------------|-----------------|
| `none` | Style par défaut | Style par défaut | Style par défaut |
| `forwards` | Style par défaut | Style par défaut | **Dernier keyframe** ✅ |
| `backwards` | **Premier keyframe** ✅ | Premier keyframe | Style par défaut |
| `both` | **Premier keyframe** ✅ | Premier keyframe | **Dernier keyframe** ✅ |

### Cas d'usage pratiques

#### Apparition définitive (forwards)

```css
.modal {
    opacity: 0;
    transform: scale(0.8);
    animation: zoomIn 0.3s ease-out forwards;
    /* Reste visible après */
}
```

#### Disparition définitive (forwards)

```css
.notification {
    opacity: 1;
    animation: fadeOut 0.5s ease-in 3s forwards;
    /*                           ↑    ↑        ↑
    /*                        durée délai  reste caché
    /* Disparaît après 3 secondes et reste caché */
}
```

#### Animation avec délai (both)

```css
.element {
    opacity: 1;
    transform: translateY(0);
    animation: slideInDown 0.6s 1s both;
    /*                          ↑   ↑  ↑
    /*                       durée délai both
    /* Caché pendant le délai, reste visible après */
}
```

## 8. animation-play-state : Contrôler la lecture

### Syntaxe et valeurs

```css
.element {
    animation-play-state: running; /* En cours (défaut) */
    animation-play-state: paused;  /* En pause */
}
```

### Pause au survol

```css
.gallery-item {
    animation: rotate 10s linear infinite;
}

.gallery-item:hover {
    animation-play-state: paused;
    /* Pause l'animation au survol */
}
```

### Contrôle avec JavaScript

```html
<button id="pauseBtn">Pause</button>
<div class="animated-box"></div>
```

```css
.animated-box {
    animation: spin 2s linear infinite;
}

.animated-box.paused {
    animation-play-state: paused;
}
```

```javascript
const btn = document.getElementById('pauseBtn');
const box = document.querySelector('.animated-box');

btn.addEventListener('click', () => {
    box.classList.toggle('paused');
    btn.textContent = box.classList.contains('paused') ? 'Play' : 'Pause';
});
```

### Pause/Play automatique

```css
.carousel {
    animation: scroll 20s linear infinite;
}

/* Pause quand l'utilisateur survole */
.carousel:hover {
    animation-play-state: paused;
}

/* Pause quand la page n'est pas visible */
.carousel.page-hidden {
    animation-play-state: paused;
}
```

## Combiner toutes les propriétés

### Exemple complet : Notification élaborée

```css
@keyframes notificationSequence {
    0% {
        transform: translateX(400px);
        opacity: 0;
    }
    10% {
        transform: translateX(0);
        opacity: 1;
    }
    90% {
        transform: translateX(0);
        opacity: 1;
    }
    100% {
        transform: translateX(400px);
        opacity: 0;
    }
}

.notification {
    position: fixed;
    top: 20px;
    right: 20px;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);

    /* Configuration complète de l'animation */
    animation-name: notificationSequence;
    animation-duration: 5s;                    /* 5 secondes au total */
    animation-timing-function: ease-in-out;    /* Mouvement fluide */
    animation-delay: 0s;                       /* Démarre immédiatement */
    animation-iteration-count: 1;              /* Une seule fois */
    animation-direction: normal;               /* Sens normal */
    animation-fill-mode: forwards;             /* Reste cachée après */
    animation-play-state: running;             /* En cours */

    /* Ou en version raccourcie : */
    /* animation: notificationSequence 5s ease-in-out 0s 1 normal forwards running; */
}
```

### Exemple complet : Loader sophistiqué

```css
@keyframes loaderSpin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

@keyframes loaderPulse {
    0%, 100% { transform: scale(1); opacity: 1; }
    50% { transform: scale(1.1); opacity: 0.8; }
}

.loader {
    width: 50px;
    height: 50px;
    border: 5px solid #f3f3f3;
    border-top-color: #3498db;
    border-radius: 50%;

    /* Rotation continue */
    animation-name: loaderSpin, loaderPulse;
    animation-duration: 1s, 2s;
    animation-timing-function: linear, ease-in-out;
    animation-delay: 0s, 0s;
    animation-iteration-count: infinite, infinite;
    animation-direction: normal, alternate;
    animation-fill-mode: none, none;
    animation-play-state: running, running;

    /* Version raccourcie : */
    /* animation: loaderSpin 1s linear infinite,
                  loaderPulse 2s ease-in-out infinite alternate; */
}
```

## Techniques avancées

### 1. Animation en cascade avec calc()

```css
/* Génère des délais automatiquement */
.item:nth-child(1) { animation-delay: calc(0.1s * 1); }
.item:nth-child(2) { animation-delay: calc(0.1s * 2); }
.item:nth-child(3) { animation-delay: calc(0.1s * 3); }
/* ... */
.item:nth-child(10) { animation-delay: calc(0.1s * 10); }
```

**Avec SCSS/SASS (bonus) :**
```scss
@for $i from 1 through 10 {
    .item:nth-child(#{$i}) {
        animation-delay: 0.1s * $i;
    }
}
```

### 2. Animation progressive avec custom properties

```css
.element {
    --animation-duration: 1s;
    animation: fadeIn var(--animation-duration);
}

@media (prefers-reduced-motion: reduce) {
    .element {
        --animation-duration: 0.01s; /* Quasi instantané */
    }
}
```

### 3. Animation conditionnelle

```css
.element {
    animation: none; /* Pas d'animation par défaut */
}

.element.animate {
    animation: slideIn 0.5s ease-out;
}

@media (min-width: 768px) {
    .element {
        animation: slideIn 0.5s ease-out; /* Animation seulement sur desktop */
    }
}
```

### 4. Séquence d'animations

```css
.element {
    /* Animation 1 : Apparition */
    animation: fadeIn 0.5s ease-out forwards;
}

/* Après 0.5s, changer l'animation */
.element.step-2 {
    animation: moveRight 1s ease-in-out 0.5s forwards;
}

/* Avec JavaScript pour changer les étapes */
```

## Debugging et outils

### 1. DevTools du navigateur

**Chrome DevTools :**
1. Inspectez l'élément (F12)
2. Onglet "Styles"
3. Les animations apparaissent avec une icône de lecture
4. Cliquez dessus pour :
   - Voir la timeline
   - Ajuster la vitesse
   - Mettre en pause
   - Rejouer

### 2. Afficher les keyframes dans la console

```javascript
// Lister toutes les animations définies
const styleSheets = Array.from(document.styleSheets);
styleSheets.forEach(sheet => {
    const rules = Array.from(sheet.cssRules || []);
    rules.forEach(rule => {
        if (rule.type === CSSRule.KEYFRAMES_RULE) {
            console.log('Animation:', rule.name);
            console.log('Keyframes:', Array.from(rule.cssRules));
        }
    });
});
```

### 3. Tester avec classes temporaires

```javascript
// Ajouter temporairement une animation pour tester
element.classList.add('test-animation');

setTimeout(() => {
    element.classList.remove('test-animation');
}, 2000);
```

### 4. Visualiser avec will-change

```css
.element {
    will-change: transform, opacity;
    /* Aide à voir ce qui sera animé */
}
```

## Optimisation des performances

### Propriétés à privilégier

**⚡ Très performant (GPU) :**
```css
@keyframes optimized {
    from {
        transform: translateX(0);
        opacity: 1;
    }
    to {
        transform: translateX(100px);
        opacity: 0;
    }
}
```

**⚠️ Moins performant (CPU) :**
```css
@keyframes slow {
    from {
        left: 0;
        width: 100px;
    }
    to {
        left: 100px;
        width: 200px;
    }
}
```

### Optimisations

```css
.element {
    /* Prévenir le navigateur */
    will-change: transform, opacity;

    /* Forcer l'accélération GPU */
    transform: translateZ(0);

    /* Animation optimisée */
    animation: slide 1s ease-out;
}
```

### Limiter les animations sur mobile

```css
@media (max-width: 768px) {
    /* Désactiver les animations décoratives */
    .decorative {
        animation: none !important;
    }

    /* Réduire les durées */
    .animated {
        animation-duration: 0.3s !important;
    }
}
```

## Récapitulatif complet

### Les 8 propriétés

| Propriété | Valeurs courantes | Usage principal |
|-----------|------------------|-----------------|
| `animation-name` | nom, `none` | Quelle animation |
| `animation-duration` | `0.5s`, `1s`, `2s` | Combien de temps |
| `animation-timing-function` | `ease`, `linear`, `ease-out` | Comment (courbe) |
| `animation-delay` | `0s`, `0.5s`, `-1s` | Quand démarrer |
| `animation-iteration-count` | `1`, `3`, `infinite` | Combien de fois |
| `animation-direction` | `normal`, `alternate` | Quel sens |
| `animation-fill-mode` | `forwards`, `both` | État avant/après |
| `animation-play-state` | `running`, `paused` | Pause/lecture |

### Syntaxe raccourcie

```css
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
```

**Exemple complet :**
```css
.element {
    animation: slideIn 1s ease-out 0.5s 2 alternate both running;
}
```

**Version minimale (la plus courante) :**
```css
.element {
    animation: slideIn 1s;
    /* Suffit dans 80% des cas ! */
}
```

### Valeurs par défaut

Si vous ne spécifiez pas une propriété, voici les valeurs par défaut :

```css
animation-name: none;
animation-duration: 0s;
animation-timing-function: ease;
animation-delay: 0s;
animation-iteration-count: 1;
animation-direction: normal;
animation-fill-mode: none;
animation-play-state: running;
```

---

**📚 Points à retenir :**

- **animation-name** : donne le nom de votre @keyframes
- **animation-duration** : 0.3s-1s pour la plupart des cas
- **animation-timing-function** : `ease-out` pour apparitions, `alternate` avec `infinite` pour va-et-vient
- **animation-delay** : positif = attente, négatif = démarre avancé
- **animation-iteration-count** : `infinite` avec parcimonie
- **animation-direction** : `alternate` = va-et-vient
- **animation-fill-mode** : `forwards` = garde l'état final ⭐
- **animation-play-state** : `paused` au survol pour contrôler

**💡 Les plus importantes :**
1. **forwards** (fill-mode) : pour que l'animation reste après
2. **alternate** (direction) : pour les va-et-vient
3. **ease-out** (timing-function) : pour les apparitions naturelles

**🎯 Pour aller plus loin :**
Expérimentez avec [cubic-bezier.com](https://cubic-bezier.com/) pour créer vos propres courbes d'animation et donnez un style unique à vos animations !

Vous maîtrisez maintenant tous les aspects des animations CSS. Continuez à pratiquer et vous créerez des animations fluides et professionnelles ! 🚀

⏭️ [JavaScript Moderne - Fondamentaux (ES6+)](/05-javascript-moderne-fondamentaux/README.md)
