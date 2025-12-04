🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.1.1 Syntaxe : propriétés, valeurs, déclarations

## Introduction

Avant de pouvoir styliser vos pages web, il est essentiel de comprendre comment **écrire du CSS correctement**. La syntaxe CSS suit des règles précises qui, une fois maîtrisées, vous permettront de créer n'importe quel style imaginable.

Dans cette section, nous allons décortiquer la structure de base du CSS pour que vous compreniez chaque élément qui compose une règle de style.

---

## La structure d'une règle CSS

Une règle CSS complète se compose de plusieurs éléments. Observons cette règle simple :

```css
p {
  color: blue;
  font-size: 16px;
}
```

Cette règle se décompose ainsi :

```
sélecteur {
  propriété: valeur;
  propriété: valeur;
}
```

Décomposons chaque partie :

### 1. Le sélecteur

```css
p {
  /* ... */
}
```

Le **sélecteur** (`p` dans cet exemple) indique **à quels éléments HTML** appliquer les styles. Ici, tous les paragraphes `<p>` seront stylisés.

### 2. Les accolades `{ }`

```css
p { /* début du bloc */
  color: blue;
} /* fin du bloc */
```

Les **accolades** délimitent le bloc de déclarations. Tout ce qui se trouve entre les accolades sera appliqué aux éléments ciblés par le sélecteur.

### 3. Les déclarations

```css
p {
  color: blue;        /* première déclaration */
  font-size: 16px;    /* deuxième déclaration */
}
```

Une **déclaration** est l'association d'une propriété et d'une valeur. Elle définit **comment** l'élément doit être stylisé.

---

## Les propriétés CSS

### Qu'est-ce qu'une propriété ?

Une **propriété** est un aspect visuel ou comportemental que vous voulez modifier. C'est le "quoi" : **quoi modifier** sur l'élément.

**Exemples de propriétés courantes :**

```css
color          /* couleur du texte */
font-size      /* taille de la police */
background     /* couleur ou image de fond */
width          /* largeur */
height         /* hauteur */
margin         /* marge extérieure */
padding        /* marge intérieure */
border         /* bordure */
```

### Règles d'écriture des propriétés

- ✅ Toujours en **minuscules**
- ✅ Utiliser des **tirets** pour séparer les mots : `font-size` (pas `fontSize`)
- ✅ Suivies d'un **deux-points** `:` sans espace avant

**Exemples corrects :**
```css
color: red;
font-size: 16px;
background-color: yellow;
```

**❌ Erreurs courantes :**
```css
Color: red;              /* Majuscule - incorrect */
font_size: 16px;         /* Underscore - incorrect */
fontSize: 16px;          /* Camel case - incorrect (c'est du JavaScript) */
color : red;             /* Espace avant les deux-points - mauvaise pratique */
```

---

## Les valeurs CSS

### Qu'est-ce qu'une valeur ?

Une **valeur** définit **comment** la propriété doit se comporter. C'est le "comment" : **comment doit être modifiée** la propriété.

**Exemple :**
```css
color: blue;
      ^^^^
      valeur
```

### Types de valeurs

CSS accepte différents types de valeurs :

#### 1. **Mots-clés prédéfinis**

```css
color: red;              /* couleur par nom */
font-weight: bold;       /* texte en gras */
text-align: center;      /* alignement centré */
display: none;           /* élément caché */
```

#### 2. **Valeurs numériques avec unités**

```css
font-size: 16px;         /* pixels */
width: 50%;              /* pourcentage */
margin: 2em;             /* em (unité relative) */
padding: 1rem;           /* rem (unité relative) */
line-height: 1.5;        /* nombre sans unité */
```

**Les unités les plus courantes :**
- `px` : pixels (unité absolue)
- `%` : pourcentage (relatif au parent)
- `em` : relatif à la taille de police de l'élément
- `rem` : relatif à la taille de police racine
- `vh` / `vw` : relatif à la hauteur/largeur du viewport

#### 3. **Couleurs**

```css
/* Par nom */
color: red;

/* Hexadécimal */
color: #ff0000;

/* RGB */
color: rgb(255, 0, 0);

/* RGBA (avec transparence) */
color: rgba(255, 0, 0, 0.5);

/* HSL */
color: hsl(0, 100%, 50%);
```

#### 4. **Chaînes de caractères**

```css
font-family: "Arial", sans-serif;
content: "★";
```

#### 5. **Valeurs multiples**

Certaines propriétés acceptent plusieurs valeurs :

```css
/* Espacement : haut, droite, bas, gauche */
margin: 10px 20px 10px 20px;

/* Bordure : épaisseur, style, couleur */
border: 1px solid black;

/* Police : style, variante, poids, taille/hauteur, famille */
font: italic small-caps bold 16px/1.5 Arial, sans-serif;
```

---

## Les déclarations

### Structure d'une déclaration

Une **déclaration** complète associe une propriété et une valeur :

```css
propriété: valeur;
^         ^      ^
|         |      |
propriété |      point-virgule obligatoire (sauf dernière déclaration)
          deux-points
```

**Exemple :**
```css
p {
  color: blue;           /* déclaration complète */
  font-size: 16px;       /* autre déclaration */
}
```

### Le point-virgule `;`

Chaque déclaration doit se terminer par un **point-virgule** `;` (sauf la dernière, mais c'est une bonne pratique de toujours le mettre).

**✅ Bonne pratique :**
```css
p {
  color: blue;
  font-size: 16px;       /* point-virgule même sur la dernière ligne */
}
```

**⚠️ Fonctionne mais déconseillé :**
```css
p {
  color: blue;
  font-size: 16px        /* pas de point-virgule sur la dernière */
}
```

**❌ Erreur - ne fonctionnera pas :**
```css
p {
  color: blue
  font-size: 16px;       /* manque le point-virgule après blue */
}
```

### Plusieurs déclarations

Un sélecteur peut contenir autant de déclarations que nécessaire :

```css
h1 {
  color: navy;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
  text-transform: uppercase;
}
```

---

## Mise en forme et lisibilité

### Indentation et espaces

Le CSS est flexible sur la mise en forme, mais suivre des conventions améliore la lisibilité.

**✅ Style recommandé (une déclaration par ligne) :**
```css
p {
  color: blue;
  font-size: 16px;
  line-height: 1.5;
}
```

**⚠️ Fonctionne mais illisible :**
```css
p{color:blue;font-size:16px;line-height:1.5;}
```

**✅ Acceptable pour une seule déclaration courte :**
```css
.error { color: red; }
```

### Conventions de formatage

**1. Espacement autour des accolades :**
```css
/* Accolade ouvrante sur la même ligne */
p {
  color: blue;
}

/* Accolade fermante sur sa propre ligne */
```

**2. Indentation :**
```css
/* 2 ou 4 espaces (ou 1 tabulation) pour chaque niveau */
body {
  margin: 0;
  padding: 0;
}

  header {              /* imbrication logique (avec préprocesseurs) */
    background: gray;
  }
```

**3. Espacement autour des deux-points :**
```css
/* Un espace après les deux-points, pas avant */
color: blue;           /* ✅ correct */
color : blue;          /* ⚠️ fonctionne mais inhabituel */
color:blue;            /* ⚠️ fonctionne mais moins lisible */
```

---

## Les commentaires CSS

Les commentaires permettent d'expliquer votre code ou de désactiver temporairement des règles.

### Syntaxe des commentaires

```css
/* Ceci est un commentaire sur une ligne */

/*
   Ceci est un commentaire
   sur plusieurs lignes
   très pratique pour des explications longues
*/

p {
  color: blue;          /* commentaire en fin de ligne */
  /* font-size: 16px; */  /* déclaration désactivée */
}
```

**⚠️ Attention :** CSS utilise `/* */` uniquement. Les commentaires `//` (style JavaScript) ne fonctionnent pas en CSS pur.

```css
/* ✅ Correct */
// ❌ Ne fonctionne pas en CSS
```

### Bonnes pratiques pour les commentaires

**1. Documenter les sections :**
```css
/* ========================================
   HEADER STYLES
   ======================================== */

header {
  background: navy;
}

/* ========================================
   NAVIGATION
   ======================================== */

nav {
  margin: 20px 0;
}
```

**2. Expliquer les choix complexes :**
```css
.container {
  /* On utilise max-width au lieu de width pour la responsivité */
  max-width: 1200px;

  /* Centrage horizontal automatique */
  margin: 0 auto;
}
```

**3. Marquer les zones à réviser :**
```css
.button {
  background: blue;
  /* TODO: Vérifier l'accessibilité du contraste */
}
```

---

## Règles CSS complètes - Récapitulatif

Mettons tout ensemble pour comprendre une règle CSS complète :

```css
/* Sélecteur : cible les éléments <p> */
p {
  /* Déclaration 1 */
  color: #333333;              /* propriété: valeur; */

  /* Déclaration 2 */
  font-size: 16px;             /* propriété: valeur; */

  /* Déclaration 3 */
  line-height: 1.6;            /* propriété: valeur; */

  /* Déclaration 4 */
  margin-bottom: 15px;         /* propriété: valeur; */
}
```

**Anatomie complète :**
- **Sélecteur** : `p` → Quels éléments styliser
- **Bloc de déclarations** : `{ ... }` → Ensemble des styles
- **Déclarations** : `color: #333333;` → Chaque style individuel
- **Propriétés** : `color`, `font-size`, etc. → Quoi modifier
- **Valeurs** : `#333333`, `16px`, etc. → Comment modifier

---

## Plusieurs règles CSS

Un fichier CSS contient généralement de nombreuses règles :

```css
/* Styles pour le body */
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
  margin: 0;
  padding: 0;
}

/* Styles pour les titres h1 */
h1 {
  color: navy;
  font-size: 32px;
  margin-bottom: 20px;
}

/* Styles pour les paragraphes */
p {
  margin-bottom: 15px;
  text-align: justify;
}

/* Styles pour les liens */
a {
  color: blue;
  text-decoration: none;
}
```

**Note :** L'ordre des règles peut avoir de l'importance (nous verrons cela avec la cascade et la spécificité).

---

## Erreurs courantes et comment les éviter

### 1. Oublier le point-virgule

**❌ Erreur :**
```css
p {
  color: blue
  font-size: 16px;    /* Cette règle ne s'appliquera pas ! */
}
```

**✅ Correction :**
```css
p {
  color: blue;
  font-size: 16px;
}
```

### 2. Confondre les deux-points et le point-virgule

**❌ Erreur :**
```css
p {
  color; blue:        /* inversé ! */
}
```

**✅ Correct :**
```css
p {
  color: blue;
}
```

### 3. Utiliser des guillemets incorrects

**❌ Erreur :**
```css
font-family: 'Arial';    /* guillemets simples, fonctionne mais... */
font-family: "Arial';    /* mélange de guillemets - erreur ! */
```

**✅ Recommandé :**
```css
font-family: "Arial", sans-serif;    /* guillemets doubles */
```

### 4. Oublier l'unité pour les valeurs numériques

**❌ Erreur :**
```css
width: 300;              /* Manque l'unité ! */
```

**✅ Correct :**
```css
width: 300px;            /* avec px */
width: 50%;              /* ou % */
```

**Exception :** Certaines propriétés acceptent des nombres sans unité :
```css
line-height: 1.5;        /* ✅ valide sans unité */
opacity: 0.5;            /* ✅ valide sans unité */
z-index: 10;             /* ✅ valide sans unité */
```

### 5. Espaces dans les noms de propriétés

**❌ Erreur :**
```css
font size: 16px;         /* espace dans le nom */
```

**✅ Correct :**
```css
font-size: 16px;         /* tiret, pas d'espace */
```

---

## Validation du code CSS

Pour vérifier que votre syntaxe CSS est correcte, vous pouvez utiliser :

### 1. Les DevTools du navigateur

Ouvrez les DevTools (F12) :
- Les erreurs CSS apparaissent en rouge dans la console
- L'onglet "Elements" montre quels styles sont appliqués

### 2. Le validateur W3C

- URL : https://jigsaw.w3.org/css-validator/
- Permet de vérifier la validité de votre CSS
- Indique les erreurs de syntaxe

### 3. Extensions VS Code

- **CSS Lint** : détecte les erreurs en temps réel
- **Prettier** : formate automatiquement votre code

---

## Bonnes pratiques de syntaxe

Pour écrire du CSS propre et maintenable :

### ✅ À FAIRE

1. **Une déclaration par ligne**
```css
p {
  color: blue;
  font-size: 16px;
  line-height: 1.5;
}
```

2. **Indenter les déclarations**
```css
body {
  margin: 0;          /* indenté */
  padding: 0;         /* indenté */
}
```

3. **Toujours mettre le point-virgule final**
```css
p {
  color: blue;        /* point-virgule même sur la dernière */
}
```

4. **Grouper les propriétés par thème**
```css
.box {
  /* Positionnement */
  position: relative;
  top: 10px;

  /* Dimensions */
  width: 300px;
  height: 200px;

  /* Visuel */
  background: white;
  border: 1px solid gray;
}
```

5. **Utiliser des commentaires**
```css
/* Navigation principale */
nav {
  background: navy;
}
```

### ❌ À ÉVITER

1. **Tout sur une ligne (sauf règles très courtes)**
```css
/* ❌ Difficile à lire */
p { color: blue; font-size: 16px; line-height: 1.5; margin: 10px; }

/* ✅ Mieux */
p {
  color: blue;
  font-size: 16px;
  line-height: 1.5;
  margin: 10px;
}
```

2. **Mélanger les conventions**
```css
/* ❌ Inconsistant */
p{
    color:blue;
  font-size: 16px;
     line-height:1.5;
}

/* ✅ Cohérent */
p {
  color: blue;
  font-size: 16px;
  line-height: 1.5;
}
```

---

## Résumé

**Points clés à retenir :**

📌 **Structure de base :**
```css
sélecteur {
  propriété: valeur;
}
```

📌 **Les trois composants essentiels :**
- **Sélecteur** : quels éléments cibler
- **Propriété** : quoi modifier
- **Valeur** : comment modifier

📌 **Syntaxe stricte :**
- Propriétés en minuscules avec tirets
- Deux-points après la propriété
- Point-virgule après chaque déclaration
- Accolades pour délimiter le bloc

📌 **Commentaires :**
```css
/* Syntaxe des commentaires CSS */
```

📌 **Bonnes pratiques :**
- Une déclaration par ligne
- Indentation cohérente
- Commentaires explicatifs
- Point-virgule sur toutes les déclarations

---

## Exemple complet et commenté

Voici un exemple réel de CSS bien écrit :

```css
/* ========================================
   STYLES GLOBAUX
   ======================================== */

/* Réinitialisation et styles de base */
body {
  margin: 0;                          /* Supprime les marges par défaut */
  padding: 0;                         /* Supprime les paddings par défaut */
  font-family: Arial, sans-serif;     /* Police par défaut */
  font-size: 16px;                    /* Taille de base */
  line-height: 1.6;                   /* Hauteur de ligne confortable */
  color: #333;                        /* Couleur de texte (gris foncé) */
  background-color: #f4f4f4;          /* Fond gris clair */
}

/* ========================================
   TYPOGRAPHIE
   ======================================== */

/* Titre principal */
h1 {
  font-size: 2.5em;                   /* 2.5 fois la taille de base */
  color: navy;                        /* Bleu marine */
  margin-top: 0;                      /* Supprime la marge haute */
  margin-bottom: 20px;                /* Espace sous le titre */
  font-weight: bold;                  /* Texte en gras */
}

/* Paragraphes */
p {
  margin-bottom: 15px;                /* Espace entre les paragraphes */
  text-align: left;                   /* Alignement à gauche */
}

/* Liens */
a {
  color: #0066cc;                     /* Bleu pour les liens */
  text-decoration: none;              /* Supprime le soulignement */
  transition: color 0.3s ease;        /* Transition douce de couleur */
}

/* Liens au survol */
a:hover {
  color: #003366;                     /* Bleu plus foncé au survol */
  text-decoration: underline;         /* Soulignement au survol */
}
```

---

## Prochaine étape

Maintenant que vous maîtrisez la syntaxe de base du CSS, vous êtes prêt à découvrir les **méthodes d'intégration** du CSS dans vos pages HTML (section 4.1.2).

Vous apprendrez comment lier votre CSS à votre HTML de différentes manières, et quelle méthode privilégier selon les situations.

---

**Navigation :**

- ➡️ Section suivante : [4.1.2 Méthodes d'intégration](./02-methodes-integration.md)
- 🏠 Retour à la [Table des matières](../../SOMMAIRE.md)

⏭️ [Méthodes d'intégration : inline, interne, externe](/04-css3-styles-et-mise-en-page/01-syntaxe-et-selecteurs/02-methodes-integration.md)
