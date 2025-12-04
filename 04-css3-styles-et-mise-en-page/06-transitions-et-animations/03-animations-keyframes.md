🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.6.3 - Animations avec @keyframes

## Introduction

Les **animations CSS avec @keyframes** permettent de créer des animations complexes avec plusieurs étapes, qui se déclenchent automatiquement sans interaction de l'utilisateur. Contrairement aux transitions (vues en 4.6.1) qui nécessitent un événement déclencheur (comme `:hover`), les animations peuvent démarrer automatiquement au chargement de la page.

**Analogie :**
- **Transition** = interrupteur (on/off) : "Quand je survole le bouton, change sa couleur"
- **Animation** = lecteur vidéo : "Joue cette séquence d'actions automatiquement"

## Différence entre transition et animation

### Transition (vue en 4.6.1)

```css
.bouton {
    background: blue;
    transition: background 0.3s;
}

.bouton:hover {
    background: red; /* Nécessite un survol pour se déclencher */
}
```

**Caractéristiques :**
- ✅ Nécessite un événement déclencheur (`:hover`, `.class-active`, etc.)
- ✅ Va d'un état A à un état B
- ✅ Simple et rapide à mettre en place
- ❌ Limité à 2 états (début → fin)

### Animation @keyframes

```css
@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.1); }
    100% { transform: scale(1); }
}

.bouton {
    animation: pulse 2s infinite; /* Se déclenche automatiquement ! */
}
```

**Caractéristiques :**
- ✅ Se déclenche automatiquement (ou sur événement)
- ✅ Peut avoir de multiples étapes (0%, 25%, 50%, 75%, 100%)
- ✅ Peut se répéter à l'infini
- ✅ Plus de contrôle et de complexité
- ❌ Plus verbeux à écrire

### Quand utiliser quoi ?

| Situation | Utilisez |
|-----------|----------|
| Changement au survol | **Transition** |
| Changement au clic | **Transition** |
| Animation au chargement | **Animation** |
| Animation qui se répète | **Animation** |
| Animation en plusieurs étapes | **Animation** |
| Effet simple A → B | **Transition** |
| Effet complexe A → B → C → D | **Animation** |

## Syntaxe de @keyframes

### Structure de base

```css
@keyframes nom-animation {
    /* Étapes de l'animation */
    0% {
        /* CSS au début */
    }
    100% {
        /* CSS à la fin */
    }
}
```

### Appliquer l'animation à un élément

```css
.element {
    animation: nom-animation durée;
}
```

### Exemple minimal

```css
/* 1. Définir l'animation */
@keyframes fadeIn {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}

/* 2. Appliquer l'animation */
.element {
    animation: fadeIn 1s;
}
```

**Résultat :** L'élément apparaît progressivement en 1 seconde au chargement de la page.

## Les étapes d'animation (keyframes)

### Syntaxe avec pourcentages

```css
@keyframes slide {
    0% {
        transform: translateX(0);
    }
    25% {
        transform: translateX(100px);
    }
    50% {
        transform: translateX(200px);
    }
    75% {
        transform: translateX(100px);
    }
    100% {
        transform: translateX(0);
    }
}
```

**0%** = début de l'animation
**100%** = fin de l'animation
Les valeurs intermédiaires (25%, 50%, 75%) = étapes intermédiaires

### Syntaxe avec from / to

Pour les animations simples (2 étapes seulement) :

```css
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

/* Équivaut à : */
@keyframes fadeIn {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
```

**💡 Conseil :** Utilisez `from/to` pour les animations simples, les pourcentages pour les animations complexes.

### Regrouper plusieurs étapes

Si plusieurs étapes ont les mêmes propriétés :

```css
@keyframes bounce {
    0%, 100% {
        transform: translateY(0); /* Même valeur au début et à la fin */
    }
    50% {
        transform: translateY(-30px);
    }
}
```

### Exemple : Animation en 4 étapes

```css
@keyframes colorChange {
    0% {
        background: red;
    }
    33% {
        background: yellow;
    }
    66% {
        background: blue;
    }
    100% {
        background: green;
    }
}

.element {
    animation: colorChange 4s;
}
```

**Résultat :** Le fond passe progressivement du rouge au jaune, puis au bleu, puis au vert.

## La propriété animation (raccourci)

### Syntaxe complète

```css
.element {
    animation: name duration timing-function delay iteration-count direction fill-mode play-state;
}
```

**C'est beaucoup ! Mais on peut simplifier :**

### Syntaxe minimale (la plus courante)

```css
.element {
    animation: nom-animation durée;
}
```

**Exemple :**
```css
.element {
    animation: fadeIn 1s;
}
```

### Syntaxe détaillée

```css
.element {
    animation: fadeIn 2s ease-in 0.5s infinite alternate forwards running;
    /*         nom    durée timing délai répét. direction fill-mode état
    */
}
```

Décomposons chaque paramètre :

## Les sous-propriétés d'animation

### 1. animation-name

**Quel animation @keyframes utiliser ?**

```css
@keyframes slideIn {
    /* ... */
}

.element {
    animation-name: slideIn;
}
```

### 2. animation-duration

**Combien de temps dure l'animation ?**

```css
.element {
    animation-duration: 2s; /* 2 secondes */
}
```

**Unités :**
- `s` : secondes (2s, 0.5s, 1.5s)
- `ms` : millisecondes (2000ms = 2s)

**Durées recommandées :**
- Animation rapide : **0.3s - 0.5s**
- Animation normale : **0.5s - 1s**
- Animation lente : **1s - 2s**
- Animation très lente : **2s+** (effet spectaculaire)

### 3. animation-timing-function

**Comment l'animation progresse-t-elle ?**

```css
.element {
    animation-timing-function: ease;
}
```

**Valeurs (identiques aux transitions) :**
- `ease` : naturel (défaut)
- `linear` : vitesse constante
- `ease-in` : commence lentement
- `ease-out` : finit lentement
- `ease-in-out` : lent au début et à la fin
- `cubic-bezier()` : personnalisé

**Exemple comparatif :**

```css
/* Animation avec accélération naturelle */
.element-1 {
    animation: slideIn 1s ease;
}

/* Animation à vitesse constante */
.element-2 {
    animation: slideIn 1s linear;
}

/* Animation qui commence doucement */
.element-3 {
    animation: slideIn 1s ease-in;
}
```

### 4. animation-delay

**Délai avant le début de l'animation**

```css
.element {
    animation-delay: 0.5s; /* Attend 0.5s avant de commencer */
}
```

**Valeurs :**
- `0s` : démarre immédiatement (défaut)
- `1s` : attend 1 seconde
- `-1s` : démarre 1 seconde DANS l'animation (effet avancé)

**Exemple : effet de cascade**

```css
.element-1 {
    animation: fadeIn 1s;
    animation-delay: 0s; /* Démarre tout de suite */
}

.element-2 {
    animation: fadeIn 1s;
    animation-delay: 0.2s; /* Démarre après 0.2s */
}

.element-3 {
    animation: fadeIn 1s;
    animation-delay: 0.4s; /* Démarre après 0.4s */
}
```

**Résultat :** Les éléments apparaissent les uns après les autres !

### 5. animation-iteration-count

**Combien de fois l'animation se répète ?**

```css
.element {
    animation-iteration-count: 3; /* 3 fois */
}
```

**Valeurs :**
- `1` : une seule fois (défaut)
- `3` : trois fois
- `infinite` : à l'infini (⚠️ attention à ne pas abuser)

**Exemples :**

```css
/* Pulse une seule fois au chargement */
.logo {
    animation: pulse 0.5s 1;
}

/* Tourne en continu */
.loader {
    animation: spin 1s infinite;
}

/* Clignote 5 fois puis s'arrête */
.notification {
    animation: blink 0.5s 5;
}
```

### 6. animation-direction

**Dans quel sens l'animation joue-t-elle ?**

```css
.element {
    animation-direction: normal;
}
```

**Valeurs :**

#### normal (défaut)
```css
animation-direction: normal;
/* 0% → 100% → 0% → 100% (si répété) */
```

#### reverse
```css
animation-direction: reverse;
/* 100% → 0% → 100% → 0% (à l'envers) */
```

#### alternate
```css
animation-direction: alternate;
/* 0% → 100% → 100% → 0% → 0% → 100% (allers-retours) */
```

**C'est le plus utilisé pour les animations qui se répètent !**

#### alternate-reverse
```css
animation-direction: alternate-reverse;
/* 100% → 0% → 0% → 100% (allers-retours mais commence à l'envers) */
```

**Exemple pratique - balancier :**

```css
@keyframes swing {
    0% {
        transform: rotate(-10deg);
    }
    100% {
        transform: rotate(10deg);
    }
}

.pendule {
    animation: swing 1s ease-in-out infinite alternate;
    /*                                     ↑        ↑
    /*                                  infini  va-et-vient
    */
}
```

**Résultat :** Balancement naturel qui va dans un sens puis dans l'autre !

### 7. animation-fill-mode

**Quel style appliquer AVANT et APRÈS l'animation ?**

```css
.element {
    animation-fill-mode: forwards;
}
```

**Valeurs :**

#### none (défaut)
```css
animation-fill-mode: none;
```
**Comportement :** L'élément revient à son état initial après l'animation.

```css
/* Style de base */
.element {
    opacity: 1;
}

@keyframes fadeOut {
    to { opacity: 0; }
}

.element {
    animation: fadeOut 1s none;
    /* Après l'animation : retour à opacity: 1 */
}
```

#### forwards ⭐
```css
animation-fill-mode: forwards;
```
**Comportement :** L'élément **conserve** le style du dernier keyframe (100%).

**C'est le plus utile !**

```css
.element {
    opacity: 1;
    animation: fadeOut 1s forwards;
    /* Après l'animation : reste à opacity: 0 */
}
```

#### backwards
```css
animation-fill-mode: backwards;
```
**Comportement :** Applique le style du premier keyframe PENDANT le délai (si `animation-delay`).

#### both
```css
animation-fill-mode: both;
```
**Comportement :** Combine `forwards` et `backwards`.

**Exemple comparatif :**

```css
@keyframes slideIn {
    from {
        transform: translateX(-100px);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

/* Sans fill-mode : revient à son état initial */
.element-1 {
    animation: slideIn 1s;
    /* Après l'animation : peut "sauter" à sa position d'origine */
}

/* Avec forwards : garde l'état final */
.element-2 {
    animation: slideIn 1s forwards;
    /* Après l'animation : reste visible et en place ✅ */
}
```

### 8. animation-play-state

**L'animation est-elle en cours ou en pause ?**

```css
.element {
    animation-play-state: running; /* ou paused */
}
```

**Valeurs :**
- `running` : en cours (défaut)
- `paused` : en pause

**Utilisation typique : mettre en pause au survol**

```css
.element {
    animation: spin 2s linear infinite;
    animation-play-state: running;
}

.element:hover {
    animation-play-state: paused; /* Pause au survol */
}
```

## Exemples d'animations courantes

### 1. Fade In (apparition)

```css
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

.element {
    animation: fadeIn 1s ease-out;
}
```

### 2. Fade Out (disparition)

```css
@keyframes fadeOut {
    from {
        opacity: 1;
    }
    to {
        opacity: 0;
    }
}

.element {
    animation: fadeOut 1s ease-in forwards;
    /* forwards pour rester invisible après */
}
```

### 3. Slide In (glissement depuis la gauche)

```css
@keyframes slideInLeft {
    from {
        transform: translateX(-100px);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

.element {
    animation: slideInLeft 0.6s ease-out;
}
```

### 4. Slide In depuis le bas

```css
@keyframes slideInBottom {
    from {
        transform: translateY(50px);
        opacity: 0;
    }
    to {
        transform: translateY(0);
        opacity: 1;
    }
}

.element {
    animation: slideInBottom 0.5s ease-out;
}
```

### 5. Bounce (rebond)

```css
@keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
        transform: translateY(0);
    }
    40% {
        transform: translateY(-30px);
    }
    60% {
        transform: translateY(-15px);
    }
}

.element {
    animation: bounce 2s ease-in-out;
}
```

### 6. Shake (secousse)

```css
@keyframes shake {
    0%, 100% {
        transform: translateX(0);
    }
    10%, 30%, 50%, 70%, 90% {
        transform: translateX(-10px);
    }
    20%, 40%, 60%, 80% {
        transform: translateX(10px);
    }
}

.element {
    animation: shake 0.5s ease-in-out;
}
```

**Usage :** Attirer l'attention sur un élément ou signaler une erreur.

### 7. Pulse (pulsation)

```css
@keyframes pulse {
    0%, 100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.05);
    }
}

.bouton {
    animation: pulse 2s ease-in-out infinite;
}
```

### 8. Spin (rotation continue)

```css
@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

.loader {
    animation: spin 1s linear infinite;
}
```

**Usage :** Loading spinners, icônes de chargement.

### 9. Flip (retournement)

```css
@keyframes flip {
    from {
        transform: perspective(400px) rotateY(0);
    }
    to {
        transform: perspective(400px) rotateY(360deg);
    }
}

.card {
    animation: flip 1s ease-in-out;
}
```

### 10. Zoom In (apparition avec zoom)

```css
@keyframes zoomIn {
    from {
        transform: scale(0);
        opacity: 0;
    }
    to {
        transform: scale(1);
        opacity: 1;
    }
}

.modal {
    animation: zoomIn 0.3s ease-out;
}
```

## Exemples complets et pratiques

### Exemple 1 : Hero section avec animation au chargement

```html
<section class="hero">
    <h1 class="hero-title">Bienvenue sur mon site</h1>
    <p class="hero-subtitle">Créons quelque chose d'incroyable ensemble</p>
    <button class="hero-cta">Commencer</button>
</section>
```

```css
/* Titre qui slide depuis le haut */
@keyframes slideDown {
    from {
        transform: translateY(-50px);
        opacity: 0;
    }
    to {
        transform: translateY(0);
        opacity: 1;
    }
}

.hero-title {
    animation: slideDown 0.8s ease-out;
}

.hero-subtitle {
    opacity: 0;
    animation: slideDown 0.8s ease-out 0.3s forwards;
    /*                              ↑    ↑        ↑
    /*                           durée délai  reste visible
    */
}

.hero-cta {
    opacity: 0;
    animation: slideDown 0.8s ease-out 0.6s forwards;
}
```

**Résultat :** Les éléments apparaissent les uns après les autres !

### Exemple 2 : Notification animée

```html
<div class="notification">
    <span class="icon">✓</span>
    <span class="message">Enregistré avec succès !</span>
</div>
```

```css
/* L'animation de la notification */
@keyframes slideInRight {
    from {
        transform: translateX(400px);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

@keyframes slideOutRight {
    from {
        transform: translateX(0);
        opacity: 1;
    }
    to {
        transform: translateX(400px);
        opacity: 0;
    }
}

.notification {
    animation: slideInRight 0.5s ease-out,
               slideOutRight 0.5s ease-in 3s forwards;
    /*         Entre             Sort après 3s
    */
}

/* L'icône qui pulse */
@keyframes checkPulse {
    0%, 100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.2);
    }
}

.notification .icon {
    animation: checkPulse 0.5s ease-in-out 0.3s 2;
    /*                                     ↑    ↑
    /*                                  délai 2 fois
    */
}
```

**Résultat :** Notification qui entre, l'icône pulse 2 fois, puis la notification sort après 3 secondes !

### Exemple 3 : Cards qui apparaissent en cascade

```html
<div class="cards">
    <div class="card">Card 1</div>
    <div class="card">Card 2</div>
    <div class="card">Card 3</div>
    <div class="card">Card 4</div>
</div>
```

```css
@keyframes fadeInUp {
    from {
        transform: translateY(30px);
        opacity: 0;
    }
    to {
        transform: translateY(0);
        opacity: 1;
    }
}

.card {
    opacity: 0;
    animation: fadeInUp 0.6s ease-out forwards;
}

/* Délais en cascade */
.card:nth-child(1) { animation-delay: 0s; }
.card:nth-child(2) { animation-delay: 0.1s; }
.card:nth-child(3) { animation-delay: 0.2s; }
.card:nth-child(4) { animation-delay: 0.3s; }
```

### Exemple 4 : Loader élaboré (3 dots qui bounces)

```html
<div class="loader">
    <div class="dot"></div>
    <div class="dot"></div>
    <div class="dot"></div>
</div>
```

```css
@keyframes bounce {
    0%, 80%, 100% {
        transform: scale(0.8) translateY(0);
        opacity: 0.5;
    }
    40% {
        transform: scale(1) translateY(-20px);
        opacity: 1;
    }
}

.loader {
    display: flex;
    gap: 10px;
    justify-content: center;
    align-items: center;
}

.dot {
    width: 15px;
    height: 15px;
    background: #3498db;
    border-radius: 50%;
    animation: bounce 1.4s ease-in-out infinite;
}

.dot:nth-child(1) {
    animation-delay: 0s;
}

.dot:nth-child(2) {
    animation-delay: 0.2s;
}

.dot:nth-child(3) {
    animation-delay: 0.4s;
}
```

**Résultat :** Trois points qui rebondissent en décalé !

### Exemple 5 : Menu hamburger animé

```html
<button class="menu-btn">
    <span class="line"></span>
    <span class="line"></span>
    <span class="line"></span>
</button>
```

```css
/* Animation pour transformer en X */
@keyframes lineToX-top {
    0% {
        transform: translateY(0) rotate(0);
    }
    50% {
        transform: translateY(8px) rotate(0);
    }
    100% {
        transform: translateY(8px) rotate(45deg);
    }
}

@keyframes lineToX-bottom {
    0% {
        transform: translateY(0) rotate(0);
    }
    50% {
        transform: translateY(-8px) rotate(0);
    }
    100% {
        transform: translateY(-8px) rotate(-45deg);
    }
}

@keyframes lineToX-middle {
    0% {
        opacity: 1;
        transform: scaleX(1);
    }
    50% {
        opacity: 0;
        transform: scaleX(0.5);
    }
    100% {
        opacity: 0;
        transform: scaleX(0);
    }
}

.menu-btn {
    width: 40px;
    height: 40px;
    background: transparent;
    border: none;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 6px;
}

.line {
    width: 100%;
    height: 3px;
    background: #333;
    border-radius: 2px;
    transition: transform 0.3s;
}

/* Quand le menu est ouvert */
.menu-btn.open .line:nth-child(1) {
    animation: lineToX-top 0.3s forwards;
}

.menu-btn.open .line:nth-child(2) {
    animation: lineToX-middle 0.3s forwards;
}

.menu-btn.open .line:nth-child(3) {
    animation: lineToX-bottom 0.3s forwards;
}
```

### Exemple 6 : Typewriter effect (effet machine à écrire)

```html
<h1 class="typewriter">Bonjour, je suis développeur web</h1>
```

```css
@keyframes typing {
    from {
        width: 0;
    }
    to {
        width: 100%;
    }
}

@keyframes blink {
    50% {
        border-color: transparent;
    }
}

.typewriter {
    font-family: monospace;
    font-size: 24px;
    border-right: 3px solid;
    white-space: nowrap;
    overflow: hidden;
    width: 0;
    animation: typing 4s steps(40) 1s forwards,
               blink 0.75s step-end infinite;
}
```

**Résultat :** Le texte s'écrit lettre par lettre avec un curseur qui clignote !

## Combiner animations et transitions

Vous pouvez utiliser les deux ensemble !

```css
.element {
    /* Animation au chargement */
    animation: fadeIn 1s ease-out;

    /* Transition au hover */
    transition: transform 0.3s ease;
}

.element:hover {
    transform: scale(1.1);
}
```

**Résultat :** L'élément apparaît avec une animation, puis réagit au survol avec une transition !

## Déclencher une animation avec JavaScript

### Ajouter/retirer une classe

```html
<button id="btn">Lancer l'animation</button>
<div class="box"></div>
```

```css
@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-10px); }
    75% { transform: translateX(10px); }
}

.box.animate {
    animation: shake 0.5s ease-in-out;
}
```

```javascript
const btn = document.getElementById('btn');
const box = document.querySelector('.box');

btn.addEventListener('click', () => {
    box.classList.add('animate');

    // Retirer la classe après l'animation pour pouvoir la relancer
    setTimeout(() => {
        box.classList.remove('animate');
    }, 500);
});
```

### Écouter la fin d'une animation

```javascript
const element = document.querySelector('.element');

element.addEventListener('animationend', () => {
    console.log('Animation terminée !');
    // Faire quelque chose après l'animation
});
```

**Événements disponibles :**
- `animationstart` : début de l'animation
- `animationiteration` : fin d'une itération (si répétée)
- `animationend` : fin de l'animation

## Animations responsives

Vous pouvez adapter les animations selon la taille d'écran :

```css
/* Animation normale sur desktop */
.element {
    animation: slideIn 1s ease-out;
}

/* Animation plus rapide sur mobile */
@media (max-width: 768px) {
    .element {
        animation: slideIn 0.5s ease-out;
    }
}
```

### Désactiver les animations sur mobile

Pour les performances ou la préférence utilisateur :

```css
/* Désactiver sur petits écrans */
@media (max-width: 480px) {
    * {
        animation-duration: 0s !important;
        animation-delay: 0s !important;
    }
}

/* Respecter la préférence utilisateur */
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01s !important;
        animation-iteration-count: 1 !important;
    }
}
```

**💡 Important :** Respectez `prefers-reduced-motion` pour l'accessibilité !

## Bonnes pratiques

### ✅ À faire

**1. Animations subtiles et naturelles**
```css
/* ✅ BON - Subtil et élégant */
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}
```

**2. Durées appropriées**
```css
/* ✅ BON - Rapide et efficace */
.element {
    animation: slideIn 0.6s ease-out;
}
```

**3. Utiliser forwards quand nécessaire**
```css
/* ✅ BON - L'élément reste visible */
.modal {
    opacity: 0;
    animation: fadeIn 0.5s forwards;
}
```

**4. Animations performantes**
```css
/* ✅ BON - transform et opacity */
@keyframes move {
    to { transform: translateX(100px); }
}
```

**5. Respecter les préférences utilisateur**
```css
/* ✅ BON - Accessibilité */
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01s !important;
    }
}
```

### ❌ À éviter

**1. Animations trop longues**
```css
/* ❌ MAUVAIS - Trop long */
.element {
    animation: slideIn 5s;
}
```

**2. Trop d'animations simultanées**
```css
/* ❌ MAUVAIS - Distrayant */
.element {
    animation: spin 1s infinite,
               bounce 0.5s infinite,
               pulse 2s infinite,
               shake 3s infinite;
    /* C'est le chaos ! */
}
```

**3. Animations qui se répètent sans raison**
```css
/* ❌ MAUVAIS - Agaçant */
.texte {
    animation: blink 0.5s infinite;
    /* Le texte clignote sans arrêt = très agaçant */
}
```

**4. Propriétés coûteuses**
```css
/* ❌ MAUVAIS - Mauvaises performances */
@keyframes resize {
    to { width: 500px; height: 500px; }
}

/* ✅ MEILLEUR - Utilisez transform */
@keyframes scale {
    to { transform: scale(2); }
}
```

**5. Oublier le fallback**
```css
/* ❌ MAUVAIS - Élément invisible si animation échoue */
.element {
    opacity: 0;
    animation: fadeIn 1s;
}

/* ✅ BON - Avec forwards */
.element {
    opacity: 0;
    animation: fadeIn 1s forwards;
}
```

## Performance

### Propriétés performantes

**⚡ Optimisées (GPU) :**
- `transform`
- `opacity`

**⚠️ Moyennes :**
- `color`
- `background-color`

**❌ Coûteuses (éviter) :**
- `width`, `height`
- `margin`, `padding`
- `top`, `left`

### Conseil performance

```css
/* ❌ Coûteux */
@keyframes grow {
    to { width: 500px; height: 500px; }
}

/* ✅ Performant */
@keyframes grow {
    to { transform: scale(2); }
}
```

### Activer l'accélération GPU

```css
.element {
    animation: move 1s;
    will-change: transform; /* Prévient le navigateur */
}
```

**⚠️ Attention :** N'utilisez `will-change` que sur des éléments vraiment animés.

## Librairies d'animations

Pour aller plus vite, vous pouvez utiliser des librairies :

**Animate.css**
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">

<div class="animate__animated animate__bounce">
    Contenu qui bounce
</div>
```

**AOS (Animate On Scroll)**
```html
<div data-aos="fade-up">
    Apparaît au scroll
</div>
```

**💡 Mais :** Apprendre à créer vos propres animations vous donne plus de contrôle !

## Récapitulatif

Les **animations @keyframes** permettent de créer des animations complexes et automatiques.

**Structure de base :**
```css
/* 1. Définir l'animation */
@keyframes nom {
    0% { /* début */ }
    50% { /* milieu */ }
    100% { /* fin */ }
}

/* 2. Appliquer */
.element {
    animation: nom durée;
}
```

**Propriétés principales :**
- `animation-name` : nom de l'animation
- `animation-duration` : durée (0.5s, 1s, etc.)
- `animation-timing-function` : courbe (ease, linear, etc.)
- `animation-delay` : délai avant le début
- `animation-iteration-count` : nombre de répétitions (1, 3, infinite)
- `animation-direction` : sens (normal, reverse, alternate)
- `animation-fill-mode` : état avant/après (forwards, backwards, both)
- `animation-play-state` : état (running, paused)

**Différences avec transitions :**
- ✅ Animations : multiples étapes, automatiques
- ✅ Transitions : 2 états, nécessitent un déclencheur

**Bonnes pratiques :**
- Animations subtiles (0.3s - 1s)
- Utilisez `transform` et `opacity`
- Respectez `prefers-reduced-motion`
- N'abusez pas de `infinite`

---

**📚 Points à retenir :**

- **@keyframes** définit les étapes de l'animation
- Utilisez **from/to** pour les animations simples, **pourcentages** pour les complexes
- **forwards** pour garder l'état final
- **alternate** pour les va-et-vient
- **infinite** avec parcimonie
- Respectez les **préférences utilisateur** (reduced motion)
- Préférez **transform** et **opacity** pour la performance

**🔜 Prochaine étape :**
Dans la section suivante (4.6.4), nous approfondirons les propriétés d'animation et verrons des techniques avancées !

**💡 Astuce :**
Créez votre propre bibliothèque d'animations réutilisables ! Gardez un fichier avec vos @keyframes favoris (fadeIn, slideIn, bounce, etc.) pour les réutiliser dans tous vos projets 🎨

⏭️ [Propriétés d'animation](/04-css3-styles-et-mise-en-page/06-transitions-et-animations/04-proprietes-animation.md)
