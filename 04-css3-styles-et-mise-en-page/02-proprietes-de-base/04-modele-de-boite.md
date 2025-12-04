🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.4 Le modèle de boîte (box-model)

## Introduction

Le **modèle de boîte** (box-model en anglais) est l'un des concepts les plus importants à comprendre en CSS. Chaque élément HTML est considéré comme une boîte rectangulaire, et cette boîte est composée de plusieurs couches qui déterminent sa taille totale et son espacement.

Comprendre le modèle de boîte est essentiel pour maîtriser la mise en page et éviter les surprises lorsque vous dimensionnez vos éléments.

---

## Les quatre composants de la boîte

Chaque élément HTML est composé de quatre zones, de l'intérieur vers l'extérieur :

```
┌────────────────────────────────────────┐
│           MARGIN (marge)               │  ← Espace extérieur (transparent)
│   ┌────────────────────────────────┐   │
│   │     BORDER (bordure)           │   │  ← Bordure visible
│   │   ┌────────────────────────┐   │   │
│   │   │  PADDING (rembourrage) │   │  ← Espace intérieur
│   │   │   ┌─────────────┐      │   │   │
│   │   │   │   CONTENT   │      │   │   │  ← Contenu (texte, image, etc.)
│   │   │   │  (contenu)  │      │   │   │
│   │   │   └─────────────┘      │   │   │
│   │   └────────────────────────┘   │   │
│   └────────────────────────────────┘   │
└────────────────────────────────────────┘
```

### 1. Content (Contenu)

C'est la zone où apparaît le contenu réel : texte, images, etc.

```css
.box {
  width: 200px;     /* Largeur du contenu */
  height: 100px;    /* Hauteur du contenu */
}
```

### 2. Padding (Rembourrage)

C'est l'espace **transparent** entre le contenu et la bordure. Le padding "pousse" le contenu vers l'intérieur.

```css
.box {
  padding: 20px;    /* Espace intérieur de 20px */
}
```

**Caractéristiques** :
- Transparent, mais prend la couleur de fond de l'élément
- Augmente la taille visuelle de l'élément
- Ne peut pas être négatif

### 3. Border (Bordure)

C'est le contour visible (ou invisible) qui entoure le padding et le contenu.

```css
.box {
  border: 2px solid black;    /* Bordure visible */
}
```

**Caractéristiques** :
- Peut être visible ou invisible
- A une épaisseur, un style et une couleur
- Augmente la taille totale de l'élément

### 4. Margin (Marge)

C'est l'espace **transparent** à l'extérieur de la bordure. La margin crée de l'espace entre les éléments.

```css
.box {
  margin: 20px;    /* Espace extérieur de 20px */
}
```

**Caractéristiques** :
- Toujours transparent
- Sépare les éléments entre eux
- Peut être négatif (pour superposer des éléments)
- Les marges verticales peuvent fusionner (margin collapse)

---

## Visualiser le box-model dans les DevTools

Les outils de développement du navigateur affichent le modèle de boîte :

1. **Clic droit** sur un élément → **Inspecter**
2. Dans l'onglet **Elements**, regardez en bas
3. Vous verrez un diagramme coloré montrant :
   - **Bleu** = Contenu (content)
   - **Vert** = Padding
   - **Jaune/Beige** = Border
   - **Orange** = Margin

C'est un outil indispensable pour comprendre et déboguer vos mises en page !

---

## Calcul de la taille totale

### Comportement par défaut (content-box)

Par défaut, les propriétés `width` et `height` définissent **seulement la taille du contenu**. La taille totale est donc :

```
Largeur totale = width + padding-left + padding-right + border-left + border-right

Hauteur totale = height + padding-top + padding-bottom + border-top + border-bottom
```

**Note** : Les margins ne sont **pas** incluses dans la taille de l'élément, elles ajoutent de l'espace autour.

### Exemple concret

```css
.box {
  width: 200px;
  height: 100px;
  padding: 20px;
  border: 5px solid black;
  margin: 10px;
}
```

**Calcul de la largeur totale** :
- Contenu : 200px
- Padding gauche : 20px
- Padding droit : 20px
- Border gauche : 5px
- Border droit : 5px
- **Total : 250px** (sans compter la margin)

**Calcul de la hauteur totale** :
- Contenu : 100px
- Padding haut : 20px
- Padding bas : 20px
- Border haut : 5px
- Border bas : 5px
- **Total : 150px** (sans compter la margin)

**Espace occupé avec les margins** :
- Largeur avec margins : 250px + 10px + 10px = **270px**
- Hauteur avec margins : 150px + 10px + 10px = **170px**

### Illustration du problème

```css
/* Vous voulez une boîte de 300px de large */
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
}

/* Mais la largeur réelle sera :
   300px (content) + 40px (padding) + 4px (border) = 344px ! */
```

C'est souvent source de confusion pour les débutants ! 😕

---

## box-sizing : Contrôler le calcul de taille 🆕

### La propriété box-sizing

CSS3 introduit la propriété `box-sizing` qui change la façon dont `width` et `height` sont calculées.

```css
.box {
  box-sizing: content-box;  /* Valeur par défaut */
  box-sizing: border-box;   /* Méthode recommandée */
}
```

### content-box (défaut)

C'est le comportement par défaut que nous venons de voir :

```css
.box {
  box-sizing: content-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
/* Largeur totale = 250px */
```

`width` = largeur du **contenu seulement**

### border-box (RECOMMANDÉ) 🆕

Avec `border-box`, `width` et `height` incluent le padding et la border :

```css
.box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
/* Largeur totale = 200px (tout compris !) */
```

`width` = largeur **totale** (contenu + padding + border)

**Avantage** : Quand vous définissez `width: 200px`, l'élément fait vraiment 200px de large, peu importe le padding et la border !

### Comparaison visuelle

```css
/* SANS border-box */
.box-default {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* Largeur réelle : 250px */
}

/* AVEC border-box */
.box-better {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* Largeur réelle : 200px comme demandé ! */
}
```

---

## La règle universelle (Best Practice) 🆕

La pratique recommandée est d'appliquer `border-box` à **tous les éléments** :

```css
/* Méthode moderne recommandée */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

Ou en version plus performante :

```css
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}
```

**Pourquoi cette pratique ?**
1. Plus intuitif : `width: 300px` donne vraiment 300px
2. Facilite les calculs
3. Plus prévisible pour la mise en page
4. Standard dans tous les frameworks CSS modernes

**Important** : Mettez cette règle en haut de votre feuille de style CSS !

---

## Exemples pratiques

### Exemple 1 : Deux colonnes de 50%

**SANS border-box (problématique)** :

```css
.column {
  width: 50%;
  padding: 20px;
  border: 2px solid black;
  float: left;
}
/* Les colonnes ne rentrent pas ! 50% + padding + border > 100% */
```

**AVEC border-box (fonctionne)** :

```css
.column {
  box-sizing: border-box;
  width: 50%;
  padding: 20px;
  border: 2px solid black;
  float: left;
}
/* Les colonnes rentrent parfaitement, le padding et border sont inclus dans les 50% */
```

### Exemple 2 : Formulaire

```css
/* SANS border-box : largeurs incohérentes */
input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  /* L'input déborde de son conteneur ! */
}

/* AVEC border-box : largeur cohérente */
input {
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  /* L'input fait exactement 100% de son conteneur */
}
```

### Exemple 3 : Cartes (Cards)

```css
.card {
  box-sizing: border-box;
  width: 300px;              /* Largeur fixe */
  padding: 20px;             /* Espace intérieur */
  border: 1px solid #ddd;    /* Bordure */
  margin: 10px;              /* Espace entre les cartes */
}
/* La carte fait exactement 300px de large, facile à prévoir ! */
```

---

## Margin et Padding : Différences clés

### Padding (Rembourrage intérieur)

```css
.box {
  padding: 20px;
  background-color: lightblue;
}
```

- ✅ Fait partie de l'élément
- ✅ Prend la couleur de fond (`background-color`)
- ✅ La zone cliquable inclut le padding
- ✅ Augmente la taille visuelle de l'élément
- ❌ Ne peut pas être négatif

**Utilisez padding pour** : Créer de l'espace autour du contenu **à l'intérieur** d'un élément.

### Margin (Marge extérieure)

```css
.box {
  margin: 20px;
  background-color: lightblue;
}
```

- ✅ Espace à l'extérieur de l'élément
- ✅ Toujours transparent
- ✅ Crée de l'espace entre les éléments
- ✅ Peut être négatif (pour superposer)
- ⚠️ Les marges verticales peuvent fusionner (collapse)

**Utilisez margin pour** : Créer de l'espace **entre** les éléments.

### Exemple visuel

```css
/* Padding : espace DANS la boîte */
.with-padding {
  width: 200px;
  padding: 20px;
  background-color: lightblue;  /* Le fond couvre le padding */
}

/* Margin : espace AUTOUR de la boîte */
.with-margin {
  width: 200px;
  margin: 20px;
  background-color: lightblue;  /* Le fond ne couvre PAS la margin */
}
```

---

## Margin Collapse (Fusion des marges)

### Qu'est-ce que c'est ?

Les marges verticales (top/bottom) de deux éléments adjacents peuvent **fusionner** en une seule marge.

### Exemple

```html
<div class="box1">Boîte 1</div>
<div class="box2">Boîte 2</div>
```

```css
.box1 {
  margin-bottom: 30px;
}

.box2 {
  margin-top: 20px;
}
```

**Question** : Quel est l'espace entre les deux boîtes ?
- ❌ Pas 50px (30px + 20px)
- ✅ **30px** (la plus grande des deux marges)

**C'est le margin collapse !** Les marges fusionnent et seule la plus grande est appliquée.

### Quand le margin collapse se produit

**Se produit entre** :
- Éléments frères adjacents (l'un après l'autre)
- Parent et premier/dernier enfant (dans certains cas)

**Ne se produit PAS** :
- Avec les marges horizontales (left/right)
- Si un padding, border ou clearance sépare les éléments
- Avec les éléments en `position: absolute` ou `float`
- Avec Flexbox ou Grid

### Comment l'éviter (si besoin)

```css
/* Ajouter un padding ou border au parent */
.parent {
  padding-top: 1px;  /* Ou border-top: 1px solid transparent; */
}

/* Utiliser Flexbox */
.container {
  display: flex;
  flex-direction: column;
}

/* Utiliser un seul élément avec margin */
.box {
  margin-bottom: 30px;  /* Seulement bottom, pas top */
}
```

**Conseil** : Dans la plupart des cas, le margin collapse est voulu et utile. Ne le combattez que si nécessaire.

---

## width et height : Valeurs spéciales

### auto (défaut)

```css
.box {
  width: auto;   /* Prend toute la largeur disponible (pour un block) */
  height: auto;  /* S'adapte à la hauteur du contenu */
}
```

### Valeurs en pixels

```css
.box {
  width: 300px;
  height: 200px;
}
```

### Valeurs en pourcentage

```css
.box {
  width: 50%;    /* 50% de la largeur du parent */
  height: 100%;  /* 100% de la hauteur du parent */
}
```

**Note** : Pour que `height: 100%` fonctionne, le parent doit avoir une hauteur définie.

### min-width, max-width, min-height, max-height

```css
.responsive-box {
  width: 50%;
  min-width: 300px;   /* Largeur minimale */
  max-width: 800px;   /* Largeur maximale */
}
```

**Utilité** : Créer des layouts responsive qui s'adaptent mais restent dans des limites raisonnables.

---

## Propriétés inline vs block

Le modèle de boîte se comporte différemment selon le type d'élément.

### Éléments block

```css
div, p, h1, section, article {
  display: block;
}
```

- Prennent toute la largeur disponible
- **Respectent** width, height, margin (tous côtés), padding (tous côtés)
- Commencent sur une nouvelle ligne

### Éléments inline

```css
span, a, strong, em {
  display: inline;
}
```

- Prennent seulement la largeur du contenu
- **Ignorent** width et height
- **Respectent** margin-left/right, padding (tous côtés)
- **Ignorent partiellement** margin-top/bottom
- Restent sur la même ligne

### inline-block (meilleur des deux mondes)

```css
.element {
  display: inline-block;
}
```

- Reste sur la même ligne (comme inline)
- **Respecte** width, height, margin, padding (comme block)

**Exemple d'usage** :

```css
/* Boutons en ligne avec dimensions contrôlées */
.button {
  display: inline-block;
  width: 150px;
  padding: 10px 20px;
  margin: 0 5px;
}
```

---

## Exemple complet : Créer une carte

Mettons en pratique le modèle de boîte avec une carte stylisée :

```html
<div class="card">
  <h2 class="card-title">Titre de la carte</h2>
  <p class="card-content">Contenu de la carte avec du texte intéressant.</p>
  <button class="card-button">En savoir plus</button>
</div>
```

```css
/* Configuration globale recommandée */
* {
  box-sizing: border-box;
}

/* La carte */
.card {
  width: 300px;               /* Largeur fixe */
  padding: 20px;              /* Espace intérieur */
  margin: 20px;               /* Espace avec les autres cartes */
  border: 1px solid #ddd;     /* Bordure légère */
  border-radius: 8px;         /* Coins arrondis */
  background-color: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);  /* Ombre portée */
}

/* Le titre */
.card-title {
  margin-top: 0;              /* Pas de margin en haut */
  margin-bottom: 15px;        /* Espace sous le titre */
  font-size: 1.5rem;
  color: #2C3E50;
}

/* Le contenu */
.card-content {
  margin-bottom: 20px;        /* Espace avant le bouton */
  line-height: 1.6;
  color: #555;
}

/* Le bouton */
.card-button {
  display: inline-block;      /* Pour contrôler les dimensions */
  padding: 10px 20px;         /* Espace intérieur du bouton */
  border: none;
  border-radius: 4px;
  background-color: #3498DB;
  color: white;
  cursor: pointer;
}

/* Avec box-sizing: border-box, la carte fait exactement 300px
   même avec padding et border ! */
```

---

## Déboguer le box-model

### Technique 1 : Bordure temporaire

```css
/* Ajouter une bordure pour visualiser */
.element {
  border: 1px solid red;  /* À retirer après debug */
}
```

### Technique 2 : Background temporaire

```css
/* Ajouter une couleur de fond */
.element {
  background-color: rgba(255, 0, 0, 0.1);  /* Rouge transparent */
}
```

### Technique 3 : DevTools (MEILLEURE MÉTHODE) 🔧

1. Clic droit → Inspecter
2. Regardez le diagramme du box-model en bas
3. Survolez les valeurs pour voir les zones surbrillées
4. Modifiez les valeurs en direct pour tester

### Technique 4 : Outline (au lieu de border)

```css
/* Outline ne change pas la taille de l'élément */
.element {
  outline: 2px solid red;  /* Pour le debug, n'affecte pas le layout */
}
```

**Différence** : `outline` ne prend pas de place, contrairement à `border`.

---

## Erreurs courantes

### Erreur 1 : Oublier box-sizing

```css
/* ❌ Problème : débordement inattendu */
.container {
  width: 100%;
  padding: 20px;
  border: 2px solid black;
  /* Largeur réelle > 100% ! */
}

/* ✅ Solution */
.container {
  box-sizing: border-box;
  width: 100%;
  padding: 20px;
  border: 2px solid black;
  /* Largeur réelle = 100% */
}
```

### Erreur 2 : Confondre margin et padding

```css
/* ❌ Mauvais : utiliser margin pour l'espace intérieur */
.box {
  margin: 20px;  /* Crée de l'espace AUTOUR, pas dedans */
}

/* ✅ Bon : utiliser padding pour l'espace intérieur */
.box {
  padding: 20px;  /* Crée de l'espace À L'INTÉRIEUR */
}
```

### Erreur 3 : Utiliser height: 100% sans parent défini

```css
/* ❌ Ne fonctionne pas */
.child {
  height: 100%;  /* 100% de quoi ? Le parent n'a pas de hauteur ! */
}

/* ✅ Solution 1 : Définir la hauteur du parent */
.parent {
  height: 500px;
}
.child {
  height: 100%;  /* Maintenant ça fonctionne */
}

/* ✅ Solution 2 : Utiliser Flexbox */
.parent {
  display: flex;
  min-height: 500px;
}
.child {
  flex: 1;  /* Prend tout l'espace disponible */
}
```

### Erreur 4 : Width sur élément inline

```css
/* ❌ Ne fonctionne pas */
span {
  display: inline;
  width: 200px;  /* Ignoré ! */
}

/* ✅ Solution */
span {
  display: inline-block;  /* Ou block */
  width: 200px;
}
```

---

## Bonnes pratiques

### 1. Utilisez toujours box-sizing: border-box

```css
/* Au début de votre CSS */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### 2. Préférez les classes aux éléments

```css
/* ❌ Moins maintenable */
div {
  padding: 20px;
}

/* ✅ Plus spécifique et réutilisable */
.card {
  padding: 20px;
}
```

### 3. Utilisez des unités cohérentes

```css
/* ✅ Bon : tout en rem pour la cohérence */
.element {
  padding: 1rem;
  margin: 1.5rem;
}

/* ❌ Moins cohérent */
.element {
  padding: 16px;
  margin: 1.5rem;
}
```

### 4. Marges dans une seule direction

```css
/* ✅ Bon : margin-bottom seulement */
h1, h2, h3, p {
  margin-top: 0;
  margin-bottom: 1rem;
}

/* ❌ Plus compliqué à gérer */
h1 {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
```

**Pourquoi ?** Éviter le margin collapse imprévu et simplifier l'espacement.

### 5. Évitez les hauteurs fixes

```css
/* ❌ Mauvais : contenu peut déborder */
.box {
  height: 200px;
}

/* ✅ Bon : s'adapte au contenu */
.box {
  min-height: 200px;  /* Hauteur minimale */
}
```

---

## Résumé

### Le modèle de boîte en bref

```
┌─────────────────────────────────┐
│        MARGIN (extérieur)       │  ← Transparent, sépare les éléments
│  ┌───────────────────────────┐  │
│  │   BORDER (bordure)        │  │  ← Visible, contour de l'élément
│  │  ┌─────────────────────┐  │  │
│  │  │ PADDING (intérieur) │  │  ← Transparent, espace dans l'élément
│  │  │  ┌─────────────┐    │  │  │
│  │  │  │   CONTENT   │    │  │  │  ← Le contenu réel
│  │  │  └─────────────┘    │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

### Points clés

1. **4 composants** : Content, Padding, Border, Margin
2. **box-sizing: border-box** est recommandé pour tous les éléments
3. **Padding** = espace intérieur (prend la couleur de fond)
4. **Margin** = espace extérieur (toujours transparent)
5. **Margin collapse** = les marges verticales fusionnent
6. **DevTools** = votre meilleur ami pour visualiser le box-model

### Syntaxe de base

```css
.element {
  /* Modèle de boîte recommandé */
  box-sizing: border-box;

  /* Dimensions */
  width: 300px;
  height: 200px;

  /* Espacement intérieur */
  padding: 20px;

  /* Bordure */
  border: 2px solid #333;

  /* Espacement extérieur */
  margin: 10px;
}
```

Le modèle de boîte est la fondation de toute mise en page CSS. Prenez le temps de le maîtriser, et vous éviterez 90% des problèmes de layout !

⏭️ [Espacement : margin, padding, border](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/05-espacement.md)
