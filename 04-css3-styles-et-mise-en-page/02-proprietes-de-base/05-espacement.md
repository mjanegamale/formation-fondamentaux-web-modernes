🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.2.5 Espacement : margin, padding, border

## Introduction

Maintenant que vous comprenez le modèle de boîte, explorons en détail les trois propriétés qui contrôlent l'espacement et les bordures : **margin** (marge), **padding** (rembourrage) et **border** (bordure).

Ces propriétés sont essentielles pour créer des mises en page aérées, lisibles et professionnelles. Elles déterminent comment vos éléments s'espacent les uns des autres et comment ils sont structurés visuellement.

---

## Margin : L'espace extérieur

### Qu'est-ce que c'est ?

La **margin** (marge) crée un espace **transparent** autour de l'élément, à l'extérieur de sa bordure. Elle sépare les éléments entre eux.

### Propriétés individuelles

Vous pouvez contrôler chaque côté indépendamment :

```css
.box {
  margin-top: 20px;      /* Marge en haut */
  margin-right: 30px;    /* Marge à droite */
  margin-bottom: 20px;   /* Marge en bas */
  margin-left: 30px;     /* Marge à gauche */
}
```

### Propriété raccourcie

La propriété `margin` permet de définir les 4 côtés en une seule ligne :

#### 1 valeur : Tous les côtés

```css
.box {
  margin: 20px;
  /* Équivaut à :
     margin-top: 20px;
     margin-right: 20px;
     margin-bottom: 20px;
     margin-left: 20px;
  */
}
```

#### 2 valeurs : Vertical | Horizontal

```css
.box {
  margin: 20px 40px;
  /* Équivaut à :
     margin-top: 20px;
     margin-bottom: 20px;
     margin-left: 40px;
     margin-right: 40px;
  */
}
```

**Mnémotechnique** : Vertical (haut/bas) puis Horizontal (gauche/droite)

#### 3 valeurs : Haut | Horizontal | Bas

```css
.box {
  margin: 10px 20px 30px;
  /* Équivaut à :
     margin-top: 10px;
     margin-left: 20px;
     margin-right: 20px;
     margin-bottom: 30px;
  */
}
```

#### 4 valeurs : Haut | Droite | Bas | Gauche (sens horaire)

```css
.box {
  margin: 10px 20px 30px 40px;
  /* Équivaut à :
     margin-top: 10px;
     margin-right: 20px;
     margin-bottom: 30px;
     margin-left: 40px;
  */
}
```

**Mnémotechnique** : Sens des aiguilles d'une montre (Top → Right → Bottom → Left) ou "TRouBLe" 🕐

### Valeur auto

La valeur `auto` est particulièrement utile pour centrer des éléments :

```css
/* Centrer horizontalement un élément block avec une largeur fixe */
.center {
  width: 300px;
  margin-left: auto;
  margin-right: auto;
  /* Ou en raccourci : */
  margin: 0 auto;  /* 0 vertical, auto horizontal */
}
```

**Important** : Cela fonctionne uniquement pour :
- Les éléments de type **block**
- Avec une **largeur définie** (pas `width: auto`)
- Pour le centrage **horizontal** uniquement

### Marges négatives

Les marges peuvent être négatives pour superposer des éléments :

```css
.overlap {
  margin-top: -20px;  /* L'élément "remonte" de 20px */
}

.pull-left {
  margin-left: -10px;  /* L'élément "déborde" à gauche de 10px */
}
```

**Cas d'usage** :
- Créer des effets de superposition
- Ajuster finement la position des éléments
- Créer des layouts créatifs

**⚠️ Attention** : À utiliser avec parcimonie, peut créer des layouts fragiles.

### Unités courantes

```css
.box {
  margin: 20px;          /* Pixels - fixe */
  margin: 1.5rem;        /* REM - relatif à la taille de base */
  margin: 1em;           /* EM - relatif à la taille de police de l'élément */
  margin: 5%;            /* Pourcentage - relatif à la largeur du parent */
  margin: auto;          /* Automatique - pour centrer */
}
```

**Note** : Les pourcentages pour les marges sont toujours calculés par rapport à la **largeur** du parent, même pour `margin-top` et `margin-bottom`.

### Exemples pratiques

```css
/* Espacer les paragraphes */
p {
  margin-bottom: 1rem;
}

/* Centrer un conteneur */
.container {
  width: 1200px;
  margin: 0 auto;  /* Centré horizontalement */
  padding: 0 20px; /* Padding pour les petits écrans */
}

/* Espacer des cartes */
.card {
  margin: 20px;
}

/* Retirer la marge du premier élément */
.content > *:first-child {
  margin-top: 0;
}

/* Retirer la marge du dernier élément */
.content > *:last-child {
  margin-bottom: 0;
}
```

---

## Padding : L'espace intérieur

### Qu'est-ce que c'est ?

Le **padding** (rembourrage) crée un espace **transparent** à l'intérieur de l'élément, entre le contenu et la bordure. Le padding prend la couleur de fond de l'élément.

### Propriétés individuelles

```css
.box {
  padding-top: 20px;      /* Rembourrage en haut */
  padding-right: 30px;    /* Rembourrage à droite */
  padding-bottom: 20px;   /* Rembourrage en bas */
  padding-left: 30px;     /* Rembourrage à gauche */
}
```

### Propriété raccourcie

Exactement comme margin, padding utilise la même logique :

#### 1 valeur : Tous les côtés

```css
.box {
  padding: 20px;
  /* Les 4 côtés ont 20px de padding */
}
```

#### 2 valeurs : Vertical | Horizontal

```css
.box {
  padding: 20px 40px;
  /* 20px en haut/bas, 40px à gauche/droite */
}
```

#### 3 valeurs : Haut | Horizontal | Bas

```css
.box {
  padding: 10px 20px 30px;
  /* Haut: 10px, Gauche/Droite: 20px, Bas: 30px */
}
```

#### 4 valeurs : Haut | Droite | Bas | Gauche

```css
.box {
  padding: 10px 20px 30px 40px;
  /* Sens horaire : Top Right Bottom Left */
}
```

### Padding vs Margin : Quand utiliser quoi ?

| Situation | Utilisez | Pourquoi |
|-----------|----------|----------|
| Espace entre le texte et le bord d'un bouton | **padding** | Espace à l'intérieur du bouton |
| Espace entre deux paragraphes | **margin** | Espace entre éléments séparés |
| Espace entre le contenu et la bordure d'une carte | **padding** | Espace à l'intérieur de la carte |
| Centrer un élément horizontalement | **margin: 0 auto** | margin-auto centre les éléments |
| Espace cliquable autour du texte d'un lien | **padding** | Augmente la zone cliquable |
| Éloigner un élément du haut de page | **margin-top** | Espace externe |

### Important : Padding ne peut pas être négatif

```css
/* ✅ Valide */
.box {
  padding: 20px;
}

/* ❌ Invalide - ignoré par le navigateur */
.box {
  padding: -20px;  /* Le padding ne peut pas être négatif ! */
}
```

### Unités courantes

```css
.box {
  padding: 20px;         /* Pixels */
  padding: 1.5rem;       /* REM - recommandé */
  padding: 1em;          /* EM */
  padding: 5%;           /* Pourcentage de la largeur du parent */
}
```

### Exemples pratiques

```css
/* Bouton avec espace intérieur */
.button {
  padding: 12px 24px;     /* Vertical 12px, Horizontal 24px */
  border: none;
  background-color: #3498DB;
  color: white;
}

/* Carte avec contenu aéré */
.card {
  padding: 20px;
  background-color: white;
  border: 1px solid #ddd;
}

/* Navigation avec espacement */
.nav-link {
  padding: 10px 15px;     /* Augmente la zone cliquable */
  text-decoration: none;
}

/* Section avec espacement */
.section {
  padding: 60px 0;        /* Vertical 60px, Horizontal 0 */
}

/* Conteneur responsive */
.container {
  padding: 20px;
  /* Sur mobile, donne de l'air au contenu */
}

@media (min-width: 768px) {
  .container {
    padding: 40px;
    /* Plus d'espace sur écrans larges */
  }
}
```

---

## Border : La bordure

### Qu'est-ce que c'est ?

La **border** (bordure) est une ligne visible qui entoure le padding et le contenu. Elle se situe entre le padding et la margin.

### Les trois propriétés de base

Une bordure complète nécessite trois informations :

```css
.box {
  border-width: 2px;           /* Épaisseur */
  border-style: solid;         /* Style de ligne */
  border-color: black;         /* Couleur */
}
```

### border-width : Épaisseur de la bordure

```css
.box {
  border-width: 1px;           /* Fine */
  border-width: 2px;           /* Moyenne */
  border-width: 5px;           /* Épaisse */

  /* Mots-clés */
  border-width: thin;          /* Fin (~1px) */
  border-width: medium;        /* Moyen (~3px) - défaut */
  border-width: thick;         /* Épais (~5px) */

  /* Différents côtés */
  border-width: 1px 2px 3px 4px;  /* Top Right Bottom Left */
}
```

### border-style : Style de la bordure

Le `border-style` est **obligatoire** pour que la bordure apparaisse.

```css
.none { border-style: none; }        /* Pas de bordure (défaut) */
.solid { border-style: solid; }      /* Ligne continue */
.dashed { border-style: dashed; }    /* Tirets */
.dotted { border-style: dotted; }    /* Pointillés */
.double { border-style: double; }    /* Ligne double */
.groove { border-style: groove; }    /* Effet 3D enfoncé */
.ridge { border-style: ridge; }      /* Effet 3D en relief */
.inset { border-style: inset; }      /* Boîte enfoncée */
.outset { border-style: outset; }    /* Boîte en relief */
```

**Styles les plus utilisés** : `solid`, `dashed`, `dotted`

### border-color : Couleur de la bordure

```css
.box {
  border-color: black;
  border-color: #3498DB;
  border-color: rgb(52, 152, 219);
  border-color: transparent;      /* Bordure invisible */

  /* Différentes couleurs par côté */
  border-color: red blue green yellow;  /* Top Right Bottom Left */
}
```

**Par défaut** : La bordure prend la couleur du texte (`color`)

### Propriété raccourcie : border

La syntaxe la plus courante et pratique :

```css
.box {
  border: 2px solid black;
  /* width style color */
}
```

**Ordre** : `border: [width] [style] [color];`

L'ordre n'est pas strict, mais cette convention est la plus lisible.

### Exemples

```css
/* Bordure simple */
.simple {
  border: 1px solid #ddd;
}

/* Bordure épaisse et colorée */
.thick {
  border: 5px solid #3498DB;
}

/* Bordure pointillée */
.dotted {
  border: 2px dotted #E74C3C;
}

/* Bordure double */
.double {
  border: 3px double #2C3E50;
}

/* Bordure invisible (pour l'espacement) */
.invisible {
  border: 2px solid transparent;
}
```

### Bordures individuelles par côté

#### Propriétés complètes par côté

```css
.box {
  border-top: 2px solid red;
  border-right: 1px dashed blue;
  border-bottom: 3px dotted green;
  border-left: 2px solid yellow;
}
```

#### Propriétés détaillées par côté

```css
.box {
  border-top-width: 2px;
  border-top-style: solid;
  border-top-color: red;

  border-right-width: 1px;
  border-right-style: dashed;
  border-right-color: blue;

  /* etc. */
}
```

### Cas d'usage pratiques

```css
/* Bordure uniquement en bas (soulignement) */
.underline {
  border-bottom: 2px solid #3498DB;
}

/* Séparateur horizontal */
.divider {
  border: none;
  border-top: 1px solid #ddd;
  margin: 20px 0;
}

/* Carte avec bordure subtile */
.card {
  border: 1px solid rgba(0, 0, 0, 0.1);
  padding: 20px;
  background-color: white;
}

/* Bouton avec bordure */
.button-outline {
  border: 2px solid #3498DB;
  background-color: transparent;
  color: #3498DB;
  padding: 10px 20px;
}

.button-outline:hover {
  background-color: #3498DB;
  color: white;
}

/* Effet de focus sur input */
.input {
  border: 1px solid #ddd;
  padding: 10px;
}

.input:focus {
  border-color: #3498DB;
  outline: none;  /* Retire le contour par défaut */
}
```

---

## border-radius : Coins arrondis 🆕

### Qu'est-ce que c'est ?

La propriété `border-radius` permet d'arrondir les coins d'un élément.

### Syntaxe de base

```css
/* Tous les coins avec le même rayon */
.rounded {
  border-radius: 5px;
}

.very-rounded {
  border-radius: 20px;
}

/* Cercle parfait (pour un carré) */
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
```

### Coins individuels

```css
.box {
  border-top-left-radius: 10px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 30px;
  border-bottom-left-radius: 40px;
}
```

### Propriété raccourcie

#### 1 valeur : Tous les coins

```css
.box {
  border-radius: 10px;
  /* Les 4 coins à 10px */
}
```

#### 2 valeurs : Diagonales

```css
.box {
  border-radius: 10px 20px;
  /* 10px: top-left et bottom-right
     20px: top-right et bottom-left */
}
```

#### 3 valeurs

```css
.box {
  border-radius: 10px 20px 30px;
  /* 10px: top-left
     20px: top-right et bottom-left
     30px: bottom-right */
}
```

#### 4 valeurs : Sens horaire

```css
.box {
  border-radius: 10px 20px 30px 40px;
  /* top-left, top-right, bottom-right, bottom-left */
}
```

### Exemples pratiques

```css
/* Bouton arrondi */
.button {
  border-radius: 4px;
  padding: 10px 20px;
  background-color: #3498DB;
  color: white;
  border: none;
}

/* Bouton très arrondi (pilule) */
.button-pill {
  border-radius: 50px;  /* Grande valeur pour effet "pilule" */
  padding: 10px 30px;
}

/* Avatar circulaire */
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;  /* Pour les images */
}

/* Carte arrondie */
.card {
  border-radius: 8px;
  padding: 20px;
  border: 1px solid #ddd;
  background-color: white;
}

/* Badge arrondi */
.badge {
  border-radius: 12px;
  padding: 4px 12px;
  background-color: #E74C3C;
  color: white;
  display: inline-block;
}

/* Forme organique */
.blob {
  border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
  /* Syntaxe avancée pour formes organiques */
}
```

### Valeurs elliptiques

Vous pouvez créer des bordures elliptiques :

```css
.ellipse {
  border-radius: 50% / 30%;
  /* horizontal / vertical */
}
```

---

## Outline : Alternative à border

### Qu'est-ce que c'est ?

`outline` est similaire à `border`, mais ne prend **pas de place** dans le modèle de boîte. Il est dessiné au-dessus du contenu.

### Différences border vs outline

| Caractéristique | border | outline |
|-----------------|--------|---------|
| Prend de l'espace | ✅ Oui | ❌ Non |
| Affecte la taille | ✅ Oui | ❌ Non |
| Coins arrondis | ✅ Oui (border-radius) | ❌ Non |
| Côtés individuels | ✅ Oui | ❌ Non |
| Usage principal | Structure visuelle | Focus, debug |

### Syntaxe

```css
.element {
  outline: 2px solid red;
  /* width style color */

  outline-width: 2px;
  outline-style: solid;
  outline-color: red;
  outline-offset: 5px;  /* Distance entre l'élément et l'outline */
}
```

### Cas d'usage

```css
/* Indicateur de focus accessible */
.button:focus {
  outline: 2px solid #3498DB;
  outline-offset: 2px;
}

/* Debug (voir les limites d'un élément) */
.debug {
  outline: 1px solid red;  /* N'affecte pas le layout */
}

/* ❌ À éviter : retirer le focus sans alternative */
button:focus {
  outline: none;  /* Mauvais pour l'accessibilité */
}

/* ✅ Bon : remplacer par un style personnalisé */
button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.5);
}
```

---

## Combiner margin, padding et border

### Exemple : Bouton complet

```css
.button {
  /* Contenu et dimensions */
  display: inline-block;

  /* Texte */
  color: white;
  font-size: 1rem;
  font-weight: 600;
  text-decoration: none;
  text-align: center;

  /* Espacement intérieur */
  padding: 12px 24px;

  /* Bordure et fond */
  border: 2px solid #3498DB;
  border-radius: 4px;
  background-color: #3498DB;

  /* Espacement extérieur */
  margin: 10px 5px;

  /* Effets */
  cursor: pointer;
  transition: all 0.3s ease;
}

.button:hover {
  background-color: #2980B9;
  border-color: #2980B9;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
```

### Exemple : Carte complète

```css
.card {
  /* Structure */
  display: block;
  width: 100%;
  max-width: 400px;

  /* Espacement intérieur */
  padding: 24px;

  /* Bordure et fond */
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: white;

  /* Espacement extérieur */
  margin: 20px auto;

  /* Ombre */
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

  /* Transition */
  transition: all 0.3s ease;
}

.card:hover {
  border-color: #3498DB;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  transform: translateY(-4px);
}

.card-title {
  margin-top: 0;
  margin-bottom: 16px;
  font-size: 1.5rem;
  color: #2C3E50;
}

.card-content {
  margin-bottom: 20px;
  line-height: 1.6;
  color: #555;
}

.card-button {
  padding: 8px 16px;
  border: 1px solid #3498DB;
  border-radius: 4px;
  background-color: #3498DB;
  color: white;
  text-decoration: none;
}
```

---

## Techniques d'espacement modernes

### Reset des marges

```css
/* Retirer les marges par défaut */
* {
  margin: 0;
  padding: 0;
}

/* Ou plus sélectif */
h1, h2, h3, h4, h5, h6, p, ul, ol {
  margin: 0;
  padding: 0;
}
```

### Espacement unidirectionnel (Flow)

```css
/* Bonne pratique : espacer uniquement vers le bas */
.content > * {
  margin-bottom: 1rem;
}

.content > *:last-child {
  margin-bottom: 0;  /* Pas de marge après le dernier élément */
}
```

### Espacement avec variables CSS

```css
:root {
  --spacing-xs: 0.25rem;   /* 4px */
  --spacing-sm: 0.5rem;    /* 8px */
  --spacing-md: 1rem;      /* 16px */
  --spacing-lg: 1.5rem;    /* 24px */
  --spacing-xl: 2rem;      /* 32px */
  --spacing-2xl: 3rem;     /* 48px */
}

.card {
  padding: var(--spacing-lg);
  margin-bottom: var(--spacing-md);
}

.section {
  padding: var(--spacing-2xl) 0;
}
```

### Utilitaires d'espacement (approche Tailwind)

```css
/* Marges */
.m-0 { margin: 0; }
.m-1 { margin: 0.25rem; }
.m-2 { margin: 0.5rem; }
.m-3 { margin: 0.75rem; }
.m-4 { margin: 1rem; }
.m-5 { margin: 1.5rem; }

/* Padding */
.p-0 { padding: 0; }
.p-1 { padding: 0.25rem; }
.p-2 { padding: 0.5rem; }
.p-3 { padding: 0.75rem; }
.p-4 { padding: 1rem; }
.p-5 { padding: 1.5rem; }

/* Directions spécifiques */
.mt-4 { margin-top: 1rem; }
.mb-4 { margin-bottom: 1rem; }
.mx-auto { margin-left: auto; margin-right: auto; }
.py-4 { padding-top: 1rem; padding-bottom: 1rem; }
```

---

## Erreurs courantes et solutions

### Erreur 1 : Oublier border-style

```css
/* ❌ Ne fonctionne pas - pas de style défini */
.box {
  border-width: 2px;
  border-color: red;
  /* Aucune bordure visible ! */
}

/* ✅ Solution */
.box {
  border: 2px solid red;
}
```

### Erreur 2 : Padding négatif

```css
/* ❌ Invalide */
.box {
  padding: -10px;  /* Ignoré par le navigateur */
}

/* ✅ Utiliser margin négatif à la place */
.box {
  margin: -10px;
}
```

### Erreur 3 : Border-radius sans taille

```css
/* ❌ N'a aucun effet visible */
.circle {
  border-radius: 50%;
  /* Pas de width/height défini */
}

/* ✅ Solution */
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
```

### Erreur 4 : Marges qui fusionnent (collapse)

```css
/* ❌ Problème : margin collapse */
.box1 {
  margin-bottom: 20px;
}
.box2 {
  margin-top: 20px;
}
/* Espace réel entre box1 et box2 : 20px (pas 40px) */

/* ✅ Solution 1 : N'utiliser que margin-bottom */
.box1, .box2 {
  margin-bottom: 20px;
  margin-top: 0;
}

/* ✅ Solution 2 : Utiliser padding ou flexbox */
.container {
  display: flex;
  flex-direction: column;
  gap: 20px;  /* Pas de margin collapse avec gap */
}
```

### Erreur 5 : Centrage incorrect

```css
/* ❌ Ne centre pas */
.box {
  margin: auto;  /* Manque une width définie */
}

/* ✅ Solution */
.box {
  width: 300px;
  margin: 0 auto;  /* Centre horizontalement */
}
```

---

## Bonnes pratiques

### 1. Cohérence dans l'espacement

```css
/* ✅ Bon : utiliser une échelle cohérente */
:root {
  --spacing-unit: 8px;
}

.small { padding: calc(var(--spacing-unit) * 1); }    /* 8px */
.medium { padding: calc(var(--spacing-unit) * 2); }   /* 16px */
.large { padding: calc(var(--spacing-unit) * 3); }    /* 24px */
```

### 2. Espacement unidirectionnel

```css
/* ✅ Bon : marges dans une seule direction */
.content h2 {
  margin-top: 0;
  margin-bottom: 1.5rem;
}

/* ❌ Moins prévisible */
.content h2 {
  margin: 1rem 0;  /* Risque de margin collapse */
}
```

### 3. Reset intelligent

```css
/* ✅ Bon : reset ciblé */
h1, h2, h3, p {
  margin-top: 0;
}

/* ❌ Trop agressif */
* {
  margin: 0;
  padding: 0;
}
```

### 4. Utiliser box-sizing: border-box

```css
/* ✅ Toujours en début de CSS */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### 5. Responsive spacing

```css
/* ✅ Bon : espacement adaptatif */
.section {
  padding: 2rem 1rem;
}

@media (min-width: 768px) {
  .section {
    padding: 4rem 2rem;
  }
}
```

---

## Tableau récapitulatif

| Propriété | Zone | Transparent ? | Peut être négatif ? | Usage principal |
|-----------|------|---------------|---------------------|-----------------|
| **margin** | Extérieur | ✅ Oui | ✅ Oui | Espacer les éléments entre eux |
| **padding** | Intérieur | ⚠️ Prend la couleur de fond | ❌ Non | Espacer le contenu des bords |
| **border** | Entre padding et margin | ❌ Visible | ❌ Non | Créer des contours visuels |
| **outline** | Au-dessus | ❌ Visible | ❌ Non | Focus, debug (ne prend pas d'espace) |

---

## Résumé

### Points clés à retenir

1. **Margin** = espace **extérieur**, transparent, peut être négatif
2. **Padding** = espace **intérieur**, prend la couleur de fond
3. **Border** = contour visible entre padding et margin
4. **Syntaxe raccourcie** : 1 valeur, 2 valeurs, 3 valeurs, 4 valeurs (sens horaire)
5. **margin: 0 auto** = centrer horizontalement (avec width définie)
6. **border-radius** = arrondir les coins (50% pour un cercle)
7. **box-sizing: border-box** = inclure padding et border dans width/height

### Syntaxes essentielles

```css
/* Espacement complet */
.element {
  /* Margin (extérieur) */
  margin: 20px;              /* Tous les côtés */
  margin: 10px 20px;         /* Vertical | Horizontal */
  margin: 10px 20px 30px 40px;  /* Top Right Bottom Left */
  margin: 0 auto;            /* Centrer horizontalement */

  /* Padding (intérieur) */
  padding: 20px;
  padding: 10px 20px;

  /* Border (bordure) */
  border: 2px solid #333;
  border-radius: 8px;

  /* Configuration recommandée */
  box-sizing: border-box;
}
```

Maîtriser l'espacement est essentiel pour créer des interfaces claires, lisibles et professionnelles. Expérimentez avec ces propriétés pour trouver le bon équilibre visuel !

⏭️ [Propriété display : block, inline, inline-block, none](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/06-propriete-display.md)
