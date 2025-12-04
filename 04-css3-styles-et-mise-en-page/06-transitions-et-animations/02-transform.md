🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.6.2 - Transform : translate, rotate, scale, skew

## Introduction

La propriété **transform** permet de modifier l'apparence visuelle d'un élément sans affecter le flux du document. Vous pouvez déplacer, faire pivoter, agrandir ou incliner un élément de façon fluide et performante.

**Transform est particulièrement puissant combiné avec les transitions** (vue dans la section précédente) pour créer des animations élégantes.

### Pourquoi transform est spécial ?

```css
/* ❌ Déplacer avec position (moins performant) */
.element {
    position: relative;
    left: 100px; /* Coûteux pour le navigateur */
}

/* ✅ Déplacer avec transform (très performant) */
.element {
    transform: translateX(100px); /* Optimisé par le GPU */
}
```

**Transform est géré par le GPU**, ce qui le rend extrêmement performant pour les animations !

## Syntaxe de base

```css
.element {
    transform: fonction(valeur);
}
```

**Exemples :**
```css
transform: translateX(50px);        /* Déplacement */
transform: rotate(45deg);           /* Rotation */
transform: scale(1.5);              /* Agrandissement */
transform: skew(10deg);             /* Inclinaison */
```

### Combiner plusieurs transformations

```css
.element {
    transform: translateX(50px) rotate(45deg) scale(1.2);
    /* Déplacement + rotation + agrandissement */
}
```

**⚠️ Ordre important :** L'ordre des fonctions affecte le résultat final !

## 1. translate : Déplacer un élément

**translate** déplace un élément dans le plan 2D (horizontal et/ou vertical).

### translate() - Déplacement 2D

```css
.element {
    transform: translate(x, y);
}
```

**Exemple :**
```css
.element {
    transform: translate(50px, 100px);
    /* Déplace de 50px à droite et 100px vers le bas */
}
```

### translateX() - Déplacement horizontal

```css
.element {
    transform: translateX(50px);
    /* Déplace de 50px à droite */
}

.element-left {
    transform: translateX(-50px);
    /* Déplace de 50px à gauche (valeur négative) */
}
```

**Valeurs positives :** déplacement vers la droite
**Valeurs négatives :** déplacement vers la gauche

### translateY() - Déplacement vertical

```css
.element {
    transform: translateY(100px);
    /* Déplace de 100px vers le bas */
}

.element-up {
    transform: translateY(-100px);
    /* Déplace de 100px vers le haut (valeur négative) */
}
```

**Valeurs positives :** déplacement vers le bas
**Valeurs négatives :** déplacement vers le haut

### Unités possibles

```css
/* Pixels */
transform: translate(50px, 100px);

/* Pourcentages (relatifs à la taille de l'élément) */
transform: translate(50%, 25%);

/* Em/Rem */
transform: translate(2em, 1.5rem);

/* Viewport units */
transform: translate(10vw, 5vh);
```

**💡 Astuce - Centrer avec translate :**

```css
.element {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    /* Centre parfaitement l'élément */
}
```

**Explication :** `top: 50%; left: 50%` positionne le coin supérieur gauche au centre. `translate(-50%, -50%)` décale ensuite l'élément de la moitié de sa propre taille pour un centrage parfait.

### Exemple pratique : Menu qui glisse

```html
<nav class="menu">
    <ul>
        <li>Accueil</li>
        <li>Services</li>
        <li>Contact</li>
    </ul>
</nav>
```

```css
.menu {
    transform: translateX(-100%); /* Caché à gauche */
    transition: transform 0.3s ease-out;
}

.menu.open {
    transform: translateX(0); /* Position normale */
}
```

**Résultat :** Menu qui glisse depuis la gauche !

### Exemple pratique : Bouton qui se soulève au survol

```css
.bouton {
    background: #3498db;
    color: white;
    padding: 15px 30px;
    border: none;
    border-radius: 5px;
    transform: translateY(0);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.bouton:hover {
    transform: translateY(-3px); /* Se soulève de 3px */
    box-shadow: 0 6px 12px rgba(0,0,0,0.15);
}

.bouton:active {
    transform: translateY(-1px); /* Légèrement enfoncé */
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

## 2. rotate : Faire pivoter un élément

**rotate** fait pivoter un élément autour d'un point (par défaut : son centre).

### Syntaxe

```css
.element {
    transform: rotate(angle);
}
```

**Angle en degrés (deg) :**
```css
transform: rotate(45deg);   /* 45° dans le sens horaire */
transform: rotate(-45deg);  /* 45° dans le sens anti-horaire */
transform: rotate(180deg);  /* Demi-tour */
transform: rotate(360deg);  /* Tour complet */
```

**Autres unités d'angle :**
```css
transform: rotate(0.5turn);  /* Demi-tour (équivaut à 180deg) */
transform: rotate(3.14rad);  /* Radians */
transform: rotate(100grad);  /* Gradians */
```

**💡 Pratique :** On utilise presque toujours les **degrés (deg)**.

### Sens de rotation

```
Valeurs positives : sens horaire (⟳)
Valeurs négatives : sens anti-horaire (⟲)
```

### Exemples visuels

```css
/* Légère inclinaison */
.element {
    transform: rotate(5deg);
}

/* Rotation 90° (quart de tour) */
.icon {
    transform: rotate(90deg);
}

/* Rotation 180° (retournement) */
.card-back {
    transform: rotate(180deg);
}

/* Rotation complète */
.loader {
    transform: rotate(360deg);
}
```

### Exemple pratique : Flèche qui tourne

```html
<button class="toggle">
    Menu <span class="arrow">▼</span>
</button>
<div class="dropdown">Contenu...</div>
```

```css
.arrow {
    display: inline-block;
    transform: rotate(0deg);
    transition: transform 0.3s ease;
}

.toggle.active .arrow {
    transform: rotate(180deg); /* Flèche qui pointe vers le haut */
}
```

### Exemple pratique : Logo qui tourne au survol

```css
.logo {
    transform: rotate(0deg);
    transition: transform 0.6s ease-in-out;
}

.logo:hover {
    transform: rotate(360deg); /* Tour complet */
}
```

### Exemple pratique : Loader qui tourne en continu

```html
<div class="loader"></div>
```

```css
.loader {
    width: 50px;
    height: 50px;
    border: 5px solid #f3f3f3;
    border-top: 5px solid #3498db;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}
```

**Note :** Cet exemple utilise `@keyframes` (que nous verrons en détail dans la section 4.6.3).

### Rotations 3D (aperçu)

Pour des rotations plus avancées :

```css
/* Rotation autour de l'axe X (effet bascule haut/bas) */
transform: rotateX(45deg);

/* Rotation autour de l'axe Y (effet flip gauche/droite) */
transform: rotateY(45deg);

/* Rotation autour de l'axe Z (comme rotate() standard) */
transform: rotateZ(45deg);
```

## 3. scale : Agrandir ou réduire un élément

**scale** modifie la taille d'un élément (zoom in/out).

### scale() - Échelle uniforme

```css
.element {
    transform: scale(facteur);
}
```

**Exemples :**
```css
transform: scale(1);     /* Taille normale (100%) */
transform: scale(1.5);   /* 150% de la taille (agrandi) */
transform: scale(0.5);   /* 50% de la taille (réduit) */
transform: scale(2);     /* 200% de la taille (doublé) */
```

**💡 Valeurs :**
- `scale(1)` = taille originale
- `scale(2)` = deux fois plus grand
- `scale(0.5)` = deux fois plus petit
- `scale(0)` = invisible (taille 0)

### scale(x, y) - Échelle différente sur chaque axe

```css
.element {
    transform: scale(largeur, hauteur);
}
```

**Exemples :**
```css
/* 150% de largeur, 200% de hauteur */
transform: scale(1.5, 2);

/* 200% de largeur, taille normale en hauteur */
transform: scale(2, 1);

/* Effet "écrasé" : largeur normale, hauteur réduite */
transform: scale(1, 0.5);
```

### scaleX() - Échelle horizontale uniquement

```css
.element {
    transform: scaleX(2); /* Deux fois plus large */
}

.mirror {
    transform: scaleX(-1); /* Effet miroir horizontal ! */
}
```

**💡 Astuce - Effet miroir :**
```css
.image-mirrored {
    transform: scaleX(-1); /* Inverse l'image horizontalement */
}
```

### scaleY() - Échelle verticale uniquement

```css
.element {
    transform: scaleY(1.5); /* 150% de hauteur */
}

.flip {
    transform: scaleY(-1); /* Effet miroir vertical ! */
}
```

### Exemple pratique : Image qui zoom au survol

```css
.image-container {
    overflow: hidden; /* Cache le débordement */
    border-radius: 8px;
}

.image-container img {
    width: 100%;
    transform: scale(1);
    transition: transform 0.3s ease-out;
}

.image-container:hover img {
    transform: scale(1.1); /* Zoom de 10% */
}
```

### Exemple pratique : Bouton qui pulse

```css
.bouton-pulse {
    transform: scale(1);
    animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
    0%, 100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.05); /* Légère expansion */
    }
}
```

### Exemple pratique : Cards responsive

```css
.card {
    transform: scale(1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.card:hover {
    transform: scale(1.05); /* Agrandit légèrement */
    box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}
```

**Résultat :** Card qui grossit légèrement au survol avec ombre plus forte !

### Combinaison avec translate pour effet zoom centré

```css
.element {
    transform: translate(-50%, -50%) scale(1);
    transition: transform 0.3s ease;
}

.element:hover {
    transform: translate(-50%, -50%) scale(1.2);
    /* Le zoom reste centré ! */
}
```

## 4. skew : Incliner un élément

**skew** incline un élément le long de l'axe X et/ou Y (effet de perspective).

### skew(x, y) - Inclinaison 2D

```css
.element {
    transform: skew(angleX, angleY);
}
```

**Exemples :**
```css
/* Inclinaison de 10° sur X, 5° sur Y */
transform: skew(10deg, 5deg);

/* Inclinaison uniquement sur X */
transform: skew(20deg, 0deg);
```

### skewX() - Inclinaison horizontale

```css
.element {
    transform: skewX(15deg); /* Incline vers la droite */
}

.element-left {
    transform: skewX(-15deg); /* Incline vers la gauche */
}
```

**Effet visuel :** L'élément semble "pencher" à gauche ou à droite.

### skewY() - Inclinaison verticale

```css
.element {
    transform: skewY(10deg); /* Incline vers le haut */
}

.element-down {
    transform: skewY(-10deg); /* Incline vers le bas */
}
```

**Effet visuel :** L'élément semble "basculer" vers le haut ou le bas.

### Exemples visuels

```css
/* Effet parallélogramme */
.shape {
    width: 200px;
    height: 100px;
    background: #3498db;
    transform: skewX(20deg);
}

/* Effet losange */
.diamond {
    width: 100px;
    height: 100px;
    background: #e74c3c;
    transform: rotate(45deg) skewX(15deg) skewY(15deg);
}
```

### Exemple pratique : Bouton style "moderne"

```css
.bouton-skew {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 15px 40px;
    border: none;
    transform: skewX(-10deg);
    transition: transform 0.3s ease;
}

.bouton-skew span {
    display: inline-block;
    transform: skewX(10deg); /* Rétablit le texte droit */
}

.bouton-skew:hover {
    transform: skewX(-10deg) translateY(-2px);
}
```

**HTML correspondant :**
```html
<button class="bouton-skew">
    <span>Cliquez ici</span>
</button>
```

### Exemple pratique : Effet carte perspective

```css
.card-skew {
    background: white;
    padding: 30px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    transform: perspective(1000px) rotateY(0deg);
    transition: transform 0.5s ease;
}

.card-skew:hover {
    transform: perspective(1000px) rotateY(10deg);
    /* Effet 3D léger */
}
```

### ⚠️ Attention avec skew

**Skew peut déformer le texte et rendre la lecture difficile.** Utilisez-le avec parcimonie !

```css
/* ❌ MAUVAIS - Texte illisible */
.texte {
    transform: skewX(30deg); /* Trop déformé */
}

/* ✅ BON - Effet subtil */
.fond {
    transform: skewX(5deg); /* Léger */
}

.fond .texte {
    transform: skewX(-5deg); /* Compense pour garder le texte droit */
}
```

## Combiner les transformations

### Ordre des transformations

L'ordre dans lequel vous appliquez les transformations **est important** !

```css
/* Ordre 1 : Déplace puis tourne */
.element {
    transform: translateX(100px) rotate(45deg);
}

/* Ordre 2 : Tourne puis déplace */
.element {
    transform: rotate(45deg) translateX(100px);
}
```

**Ces deux exemples donnent des résultats différents !**

**Explication :** Dans le premier cas, l'élément se déplace horizontalement puis tourne. Dans le second, l'élément tourne d'abord, ce qui change son système de coordonnées, puis se déplace selon ce nouveau système.

### Exemples de combinaisons

#### Déplacement + Rotation

```css
.element {
    transform: translateX(50px) rotate(45deg);
    /* Se déplace à droite ET tourne */
}
```

#### Rotation + Échelle

```css
.element {
    transform: rotate(15deg) scale(1.2);
    /* Tourne légèrement ET agrandit */
}
```

#### Combinaison complète

```css
.element {
    transform: translateX(50px) translateY(-20px) rotate(10deg) scale(1.1);
    /* Déplace à droite, monte, tourne légèrement, agrandit */
}
```

### Exemple pratique : Card avec effet complexe

```css
.card {
    transform: perspective(1000px) rotateY(0deg) translateZ(0);
    transition: transform 0.5s ease;
}

.card:hover {
    transform: perspective(1000px) rotateY(10deg) translateZ(20px) scale(1.05);
    /* Effet 3D + élévation + agrandissement */
}
```

### Exemple pratique : Animation d'apparition

```css
.element {
    opacity: 0;
    transform: translateY(50px) scale(0.8);
    transition: opacity 0.5s ease, transform 0.5s ease;
}

.element.visible {
    opacity: 1;
    transform: translateY(0) scale(1);
    /* Apparaît en montant et en grandissant */
}
```

## transform-origin : Point de référence

**transform-origin** définit le point autour duquel les transformations s'appliquent.

### Syntaxe

```css
.element {
    transform-origin: x y;
}
```

**Valeurs prédéfinies :**
```css
transform-origin: center;        /* Par défaut : centre de l'élément */
transform-origin: top left;      /* Coin supérieur gauche */
transform-origin: bottom right;  /* Coin inférieur droit */
transform-origin: center top;    /* Centre en haut */
```

**Valeurs personnalisées :**
```css
transform-origin: 50% 50%;       /* Centre (équivaut à center) */
transform-origin: 0 0;           /* Coin supérieur gauche */
transform-origin: 100px 50px;    /* Point précis en pixels */
```

### Impact sur les transformations

#### Rotation avec différents points d'origine

```css
/* Rotation autour du centre (défaut) */
.element {
    transform: rotate(45deg);
    transform-origin: center; /* Point central */
}

/* Rotation autour du coin supérieur gauche */
.element-corner {
    transform: rotate(45deg);
    transform-origin: top left; /* Pivote depuis le coin */
}

/* Rotation autour du bord gauche */
.element-left {
    transform: rotate(45deg);
    transform-origin: left center; /* Pivote depuis le bord */
}
```

#### Scale avec différents points d'origine

```css
/* Agrandissement depuis le centre (défaut) */
.element {
    transform: scale(1.5);
    transform-origin: center;
}

/* Agrandissement depuis le coin supérieur gauche */
.element-corner {
    transform: scale(1.5);
    transform-origin: top left;
    /* L'élément grandit vers le bas-droite */
}
```

### Exemple pratique : Menu qui se déploie

```css
.dropdown {
    opacity: 0;
    transform: scaleY(0);
    transform-origin: top; /* S'ouvre depuis le haut */
    transition: opacity 0.3s ease, transform 0.3s ease;
}

.dropdown.open {
    opacity: 1;
    transform: scaleY(1);
}
```

### Exemple pratique : Porte qui s'ouvre

```css
.door {
    width: 200px;
    height: 400px;
    background: brown;
    transform: rotateY(0deg);
    transform-origin: left center; /* Charnières à gauche */
    transition: transform 0.6s ease;
}

.door.open {
    transform: rotateY(-90deg); /* S'ouvre vers la gauche */
}
```

## Transformations 3D (Introduction)

Transform permet également des effets 3D avancés.

### translate3d()

```css
.element {
    transform: translate3d(x, y, z);
    /* z = profondeur (positif = vers l'avant, négatif = vers l'arrière) */
}
```

**Exemple :**
```css
transform: translate3d(50px, 100px, -50px);
/* Droite, bas, et en arrière-plan */
```

### rotate3d()

```css
/* Rotation autour d'un axe personnalisé */
transform: rotate3d(x, y, z, angle);
```

**Rotations sur axes principaux :**
```css
transform: rotateX(45deg); /* Bascule haut/bas */
transform: rotateY(45deg); /* Rotation gauche/droite */
transform: rotateZ(45deg); /* Rotation standard (équivaut à rotate()) */
```

### perspective

Pour des effets 3D réalistes, ajoutez une perspective :

```css
.conteneur {
    perspective: 1000px; /* Distance de vue */
}

.element {
    transform: rotateY(45deg);
    /* L'effet 3D est visible grâce à perspective sur le parent */
}
```

### Exemple pratique : Card flip (retournement)

```html
<div class="card-flip">
    <div class="card-front">Face avant</div>
    <div class="card-back">Face arrière</div>
</div>
```

```css
.card-flip {
    position: relative;
    width: 300px;
    height: 200px;
    perspective: 1000px;
}

.card-front,
.card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden; /* Cache la face arrière */
    transition: transform 0.6s ease;
}

.card-front {
    background: #3498db;
    transform: rotateY(0deg);
}

.card-back {
    background: #e74c3c;
    transform: rotateY(180deg);
}

.card-flip:hover .card-front {
    transform: rotateY(-180deg);
}

.card-flip:hover .card-back {
    transform: rotateY(0deg);
}
```

**Résultat :** Card qui se retourne au survol, révélant la face arrière !

## Exemples complets

### Exemple 1 : Bouton moderne avec multiples effets

```css
.btn-fancy {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 15px 40px;
    border: none;
    border-radius: 30px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    position: relative;
    overflow: hidden;

    transform: translateY(0) scale(1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
}

.btn-fancy::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    background: rgba(255,255,255,0.3);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: width 0.6s ease, height 0.6s ease;
}

.btn-fancy:hover {
    transform: translateY(-3px) scale(1.05);
    box-shadow: 0 8px 25px rgba(102, 126, 234, 0.6);
}

.btn-fancy:hover::before {
    width: 300px;
    height: 300px;
}

.btn-fancy:active {
    transform: translateY(-1px) scale(1.02);
}
```

### Exemple 2 : Galerie d'images avec hover effects

```css
.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
}

.gallery-item {
    position: relative;
    overflow: hidden;
    border-radius: 10px;
    cursor: pointer;
}

.gallery-item img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    transform: scale(1);
    transition: transform 0.5s ease;
}

.gallery-item:hover img {
    transform: scale(1.2) rotate(5deg);
}

.gallery-item .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(transparent, rgba(0,0,0,0.8));
    padding: 20px;
    color: white;
    transform: translateY(100%);
    transition: transform 0.4s ease;
}

.gallery-item:hover .overlay {
    transform: translateY(0);
}

.gallery-item .overlay h3 {
    transform: translateY(20px);
    opacity: 0;
    transition: transform 0.4s ease 0.1s, opacity 0.4s ease 0.1s;
}

.gallery-item:hover .overlay h3 {
    transform: translateY(0);
    opacity: 1;
}
```

### Exemple 3 : Menu hamburger animé

```html
<button class="menu-btn">
    <span class="line line-1"></span>
    <span class="line line-2"></span>
    <span class="line line-3"></span>
</button>
```

```css
.menu-btn {
    width: 50px;
    height: 50px;
    background: transparent;
    border: none;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 6px;
}

.line {
    width: 30px;
    height: 3px;
    background: #333;
    border-radius: 2px;
    transition: transform 0.3s ease, opacity 0.3s ease;
}

/* État ouvert */
.menu-btn.open .line-1 {
    transform: translateY(9px) rotate(45deg);
}

.menu-btn.open .line-2 {
    opacity: 0;
    transform: scaleX(0);
}

.menu-btn.open .line-3 {
    transform: translateY(-9px) rotate(-45deg);
}
```

**Résultat :** Menu burger qui se transforme en X !

### Exemple 4 : Loading spinner

```html
<div class="spinner">
    <div class="dot dot-1"></div>
    <div class="dot dot-2"></div>
    <div class="dot dot-3"></div>
</div>
```

```css
.spinner {
    display: flex;
    gap: 10px;
    padding: 20px;
}

.dot {
    width: 15px;
    height: 15px;
    background: #3498db;
    border-radius: 50%;
    animation: bounce 1.4s ease-in-out infinite;
}

.dot-1 {
    animation-delay: 0s;
}

.dot-2 {
    animation-delay: 0.2s;
}

.dot-3 {
    animation-delay: 0.4s;
}

@keyframes bounce {
    0%, 80%, 100% {
        transform: scale(1) translateY(0);
    }
    40% {
        transform: scale(1.3) translateY(-20px);
    }
}
```

## Bonnes pratiques

### ✅ À faire

**1. Utilisez transform pour les animations**
```css
/* ✅ BON - Performant */
.element {
    transform: translateX(100px);
    transition: transform 0.3s;
}
```

**2. Combinez avec transition**
```css
/* ✅ BON - Animation fluide */
.element {
    transform: scale(1);
    transition: transform 0.3s ease;
}

.element:hover {
    transform: scale(1.1);
}
```

**3. Restez subtil**
```css
/* ✅ BON - Effet discret et élégant */
.card:hover {
    transform: translateY(-5px) scale(1.02);
}
```

**4. Utilisez transform-origin quand nécessaire**
```css
/* ✅ BON - Contrôle précis */
.dropdown {
    transform: scaleY(0);
    transform-origin: top;
}
```

### ❌ À éviter

**1. Transformations excessives**
```css
/* ❌ MAUVAIS - Trop exagéré */
.element:hover {
    transform: scale(3) rotate(720deg);
    /* L'utilisateur est déboussolé ! */
}
```

**2. Déformer le texte**
```css
/* ❌ MAUVAIS - Texte illisible */
.texte {
    transform: skewX(45deg) scale(0.5);
}
```

**3. Oublier les transitions**
```css
/* ❌ MAUVAIS - Changement brutal */
.element:hover {
    transform: scale(1.5);
    /* Pas de transition = saccadé */
}
```

**4. Transformations qui cassent le layout**
```css
/* ❌ MAUVAIS - Déborde et chevauche */
.element {
    transform: scale(5);
    /* Trop grand, casse la mise en page */
}
```

## Performance

### Propriétés optimisées

**⚡ Transform est géré par le GPU = Très performant !**

```css
/* ✅ EXCELLENT pour les animations */
transform: translate();
transform: scale();
transform: rotate();
```

### Comparaison avec d'autres propriétés

```css
/* ❌ Coûteux (recalcul de layout) */
.element {
    left: 100px;
    width: 200px;
    height: 200px;
}

/* ✅ Performant (optimisé GPU) */
.element {
    transform: translateX(100px) scale(2);
}
```

### Activer l'accélération matérielle

```css
.element {
    transform: translateZ(0); /* Force l'accélération GPU */
    /* Ou */
    will-change: transform; /* Prévient le navigateur */
}
```

**⚠️ Attention :** N'abusez pas de `will-change` car cela consomme de la mémoire.

### Règle d'or

**Pour les animations fluides à 60 FPS, n'animez que :**
1. `transform`
2. `opacity`

**Évitez d'animer :**
- `width`, `height`
- `margin`, `padding`
- `top`, `left`, `right`, `bottom`

## Compatibilité navigateurs

Transform est **excellemment supporté** par tous les navigateurs modernes.

**Support :**
- ✅ Chrome (tous)
- ✅ Firefox (tous)
- ✅ Safari (tous)
- ✅ Edge (tous)
- ✅ Mobile (iOS, Android)

**Préfixes vendeur (obsolètes) :**
```css
/* Ancienne syntaxe (plus nécessaire) */
-webkit-transform: rotate(45deg);
-moz-transform: rotate(45deg);
-ms-transform: rotate(45deg);
transform: rotate(45deg);
```

**💡 Aujourd'hui :** Utilisez juste `transform` sans préfixe !

## Récapitulatif

**Transform** permet de modifier visuellement un élément sans affecter le flux du document.

**Les 4 fonctions principales :**

1. **translate(x, y)** : Déplace un élément
   ```css
   transform: translate(50px, 100px);
   transform: translateX(50px);
   transform: translateY(100px);
   ```

2. **rotate(angle)** : Fait pivoter un élément
   ```css
   transform: rotate(45deg);
   transform: rotate(-90deg);
   ```

3. **scale(factor)** : Agrandit ou réduit un élément
   ```css
   transform: scale(1.5);
   transform: scale(2, 0.5);
   transform: scaleX(2);
   ```

4. **skew(angle)** : Incline un élément
   ```css
   transform: skew(10deg, 5deg);
   transform: skewX(15deg);
   ```

**Combiner les transformations :**
```css
transform: translateX(50px) rotate(45deg) scale(1.2);
/* L'ordre compte ! */
```

**Point de référence :**
```css
transform-origin: center; /* Par défaut */
transform-origin: top left; /* Coin supérieur gauche */
```

**Performance :**
- ✅ Transform est géré par le GPU
- ✅ Parfait pour les animations fluides
- ✅ Combinez avec `transition` pour des effets élégants

---

**📚 Points à retenir :**

- **Transform** est très performant (GPU)
- Utilisez **translate** au lieu de position pour déplacer
- Utilisez **scale** au lieu de width/height pour redimensionner
- **rotate** pour faire pivoter (deg = degrés)
- **skew** avec parcimonie (peut déformer)
- Combinez avec **transition** pour des animations fluides
- **transform-origin** change le point de référence
- L'**ordre des transformations** est important !

**🔜 Prochaine étape :**
Dans la section suivante (4.6.3), nous découvrirons les **animations avec @keyframes** qui permettent de créer des animations complexes avec plusieurs étapes !

**💡 Astuce :**
Pour des animations performantes, utilisez uniquement `transform` et `opacity`. Votre site sera fluide même sur mobile ! 🚀

⏭️ [Animations avec @keyframes](/04-css3-styles-et-mise-en-page/06-transitions-et-animations/03-animations-keyframes.md)
