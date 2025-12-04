🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.1.7 Spécificité et cascade CSS

## Introduction

Imaginez cette situation : vous écrivez deux règles CSS différentes qui ciblent le même élément avec des valeurs contradictoires. Quelle règle gagne ? C'est là qu'interviennent la **cascade** et la **spécificité**, deux concepts fondamentaux qui déterminent quelles règles CSS s'appliquent réellement.

Comprendre ces mécanismes est essentiel pour :
- **Éviter les conflits** entre vos règles CSS
- **Déboguer efficacement** quand les styles ne s'appliquent pas comme prévu
- **Écrire du CSS maintenable** et prévisible
- **Éviter l'abus de `!important`**

Dans cette section, nous allons explorer en détail comment CSS décide quelle règle appliquer quand plusieurs règles ciblent le même élément.

---

## Le "C" de CSS : Cascade (Cascade)

### Qu'est-ce que la cascade ?

Le mot **"Cascading"** dans CSS signifie que les styles peuvent "cascader" ou "se superposer" comme une cascade d'eau. Plusieurs règles peuvent s'appliquer au même élément, et CSS a un système pour déterminer laquelle a la priorité.

**Analogie simple :**
Imaginez que vous empilez plusieurs feuilles de calque transparent. Chaque feuille a des instructions de style. La feuille du dessus (la plus spécifique) masque partiellement ce qui est en dessous, mais vous pouvez voir à travers là où il n'y a rien d'écrit.

### Exemple de cascade

```html
<p class="intro" id="first">Quel style s'appliquera ?</p>
```

```css
/* Règle 1 : Sélecteur d'élément */
p {
  color: blue;
  font-size: 16px;
}

/* Règle 2 : Sélecteur de classe */
.intro {
  color: green;
  font-weight: bold;
}

/* Règle 3 : Sélecteur d'ID */
#first {
  color: red;
}
```

**Résultat :**
- **Couleur : rouge** (l'ID a la priorité la plus haute)
- **Taille : 16px** (héritée de la règle p)
- **Poids : bold** (héritée de la règle .intro)

Les styles ne s'annulent pas complètement, ils se **combinent**, avec priorité aux sélecteurs les plus spécifiques.

---

## La spécificité : le système de points

### Qu'est-ce que la spécificité ?

La **spécificité** est un système de calcul de points qui détermine quelle règle CSS est la plus "importante" ou la plus "précise". Plus un sélecteur est spécifique, plus il a de poids pour gagner en cas de conflit.

**Principe de base :** Un sélecteur qui cible précisément un élément l'emporte sur un sélecteur générique.

### Le système de notation : (a, b, c, d)

La spécificité se calcule selon quatre catégories, notées de gauche à droite par ordre d'importance :

```
(a, b, c, d)
 │  │  │  └─ d : Sélecteurs d'éléments et pseudo-éléments
 │  │  └──── c : Sélecteurs de classes, attributs et pseudo-classes
 │  └─────── b : Sélecteurs d'ID
 └────────── a : Styles inline
```

**Valeurs :**
- **a** : `1` pour les styles inline, `0` sinon
- **b** : Nombre d'IDs dans le sélecteur
- **c** : Nombre de classes, attributs et pseudo-classes
- **d** : Nombre d'éléments et pseudo-éléments

### Calcul de la spécificité - Exemples

**1. Sélecteur d'élément simple :**
```css
p { }
```
- Éléments : 1
- **Spécificité : (0, 0, 0, 1)**

**2. Sélecteur de classe :**
```css
.intro { }
```
- Classes : 1
- **Spécificité : (0, 0, 1, 0)**

**3. Sélecteur d'ID :**
```css
#header { }
```
- IDs : 1
- **Spécificité : (0, 1, 0, 0)**

**4. Style inline :**
```html
<p style="color: red;">Texte</p>
```
- Inline : 1
- **Spécificité : (1, 0, 0, 0)**

**5. Sélecteur composé :**
```css
div.container p { }
```
- Éléments : 2 (div, p)
- Classes : 1 (.container)
- **Spécificité : (0, 0, 1, 2)**

**6. Sélecteur avec ID et classe :**
```css
#sidebar .widget { }
```
- IDs : 1 (#sidebar)
- Classes : 1 (.widget)
- **Spécificité : (0, 1, 1, 0)**

**7. Sélecteur complexe :**
```css
nav#main-nav ul.menu li.active a { }
```
- IDs : 1 (#main-nav)
- Classes : 2 (.menu, .active)
- Éléments : 3 (nav, ul, li, a = 4, mais nav compte déjà avec l'ID)
- **Spécificité : (0, 1, 2, 3)**

### Tableau de calcul

| Sélecteur | a | b | c | d | Spécificité | Valeur |
|-----------|---|---|---|---|-------------|--------|
| `*` | 0 | 0 | 0 | 0 | (0,0,0,0) | 0 |
| `p` | 0 | 0 | 0 | 1 | (0,0,0,1) | 1 |
| `p.intro` | 0 | 0 | 1 | 1 | (0,0,1,1) | 11 |
| `div p` | 0 | 0 | 0 | 2 | (0,0,0,2) | 2 |
| `.intro` | 0 | 0 | 1 | 0 | (0,0,1,0) | 10 |
| `#header` | 0 | 1 | 0 | 0 | (0,1,0,0) | 100 |
| `style=""` | 1 | 0 | 0 | 0 | (1,0,0,0) | 1000 |

**Note :** Les valeurs ne sont pas décimales ! (0,0,1,0) n'est pas "10", c'est une notation qui signifie "0 inline, 0 ID, 1 classe, 0 élément".

---

## Règles de comparaison

### Comment comparer les spécificités ?

On compare les valeurs **de gauche à droite**, comme des nombres :

**Exemples :**

**1. (0, 1, 0, 0) vs (0, 0, 5, 3)**
- Compare a : 0 = 0 → Égalité
- Compare b : **1 > 0** → Le premier gagne
- **Résultat : (0, 1, 0, 0) gagne**

**Un seul ID bat n'importe quel nombre de classes !**

**2. (0, 0, 2, 1) vs (0, 0, 1, 5)**
- Compare a : 0 = 0 → Égalité
- Compare b : 0 = 0 → Égalité
- Compare c : **2 > 1** → Le premier gagne
- **Résultat : (0, 0, 2, 1) gagne**

**3. (0, 0, 1, 5) vs (0, 0, 1, 10)**
- Compare a : 0 = 0 → Égalité
- Compare b : 0 = 0 → Égalité
- Compare c : 1 = 1 → Égalité
- Compare d : **5 < 10** → Le second gagne
- **Résultat : (0, 0, 1, 10) gagne**

### Cas pratique de comparaison

```html
<div id="content" class="main">
  <p class="intro">Mon paragraphe</p>
</div>
```

```css
/* Règle 1 : (0, 0, 0, 1) */
p {
  color: blue;
}

/* Règle 2 : (0, 0, 1, 0) */
.intro {
  color: green;
}

/* Règle 3 : (0, 0, 1, 1) */
div.main p {
  color: orange;
}

/* Règle 4 : (0, 1, 0, 1) */
#content p {
  color: red;
}
```

**Analyse :**
- Règle 1 : (0, 0, 0, 1) - spécificité la plus basse
- Règle 2 : (0, 0, 1, 0) - bat la règle 1
- Règle 3 : (0, 0, 1, 1) - bat la règle 2
- Règle 4 : (0, 1, 0, 1) - **GAGNE** (l'ID fait toute la différence)

**Résultat : le texte sera rouge.**

---

## Sélecteurs spéciaux et spécificité

### 1. Le sélecteur universel `*`

Le sélecteur universel a une spécificité de **0**.

```css
* {
  margin: 0;
}
```
**Spécificité : (0, 0, 0, 0)**

### 2. Les combinateurs (` `, `>`, `+`, `~`)

Les combinateurs eux-mêmes **n'ajoutent pas de spécificité**, seuls les sélecteurs qu'ils relient comptent.

```css
/* Spécificité : (0, 0, 0, 2) - deux éléments */
div > p { }

/* Spécificité : (0, 0, 0, 2) - même chose */
div p { }
```

### 3. `:not()` - Exception importante

La pseudo-classe `:not()` elle-même n'ajoute **pas** de spécificité, mais son contenu **compte**.

```css
/* Spécificité : (0, 0, 1, 0) - la classe .intro compte */
p:not(.intro) { }

/* Spécificité : (0, 1, 0, 0) - l'ID compte */
p:not(#first) { }
```

### 4. `:where()` - Spécificité zéro (CSS moderne)

La pseudo-classe `:where()` a une spécificité de **0**, quel que soit son contenu.

```css
/* Spécificité : (0, 0, 0, 1) - seul le p compte */
:where(#content, .main) p { }
```

**Cas d'usage :** Créer des styles par défaut facilement surchargeables.

### 5. `:is()` - Prend la spécificité la plus haute

```css
/* Spécificité : (0, 1, 0, 1) - l'ID #content donne (0,1,0,0) + p donne (0,0,0,1) */
:is(#content, .main) p { }
```

---

## L'ordre des règles (en cas d'égalité)

Si deux règles ont **exactement la même spécificité**, c'est la **dernière déclarée** qui gagne.

### Exemple

```css
/* Règle 1 */
p {
  color: blue;
}

/* Règle 2 - Même spécificité */
p {
  color: red;
}
```

**Résultat : rouge** (la règle 2 est déclarée après)

### Ordre des fichiers CSS

L'ordre des fichiers compte aussi :

```html
<link rel="stylesheet" href="style1.css">
<link rel="stylesheet" href="style2.css">
```

Si les deux fichiers ont une règle de même spécificité, celle de `style2.css` gagne.

### Exemple pratique

```css
/* Dans style.css */
.button {
  background: blue;
  color: white;
}

/* Plus tard dans style.css */
.button {
  background: green;  /* Gagne - déclaré après */
}
```

**Résultat :**
- **Background : vert** (dernière règle)
- **Color : white** (pas de conflit, conservé)

---

## L'attribut `!important` - L'arme nucléaire

### Qu'est-ce que `!important` ?

Le mot-clé `!important` force une déclaration CSS à avoir la **priorité absolue**, quelle que soit la spécificité.

### Syntaxe

```css
sélecteur {
  propriété: valeur !important;
}
```

**⚠️ Important :** L'espace avant `!important` est facultatif mais recommandé.

### Exemple

```html
<p id="special" class="intro" style="color: blue;">Texte</p>
```

```css
/* Spécificité : (0, 0, 0, 1) */
p {
  color: red !important;
}

/* Spécificité : (0, 0, 1, 0) */
.intro {
  color: green;
}

/* Spécificité : (0, 1, 0, 0) */
#special {
  color: orange;
}

/* Style inline : (1, 0, 0, 0) */
/* Défini dans le HTML : color: blue; */
```

**Sans `!important` :** Le texte serait bleu (style inline gagne)
**Avec `!important` :** Le texte est rouge (l'important écrase tout)

### Hiérarchie complète avec `!important`

**Ordre de priorité (du plus fort au plus faible) :**

1. **`!important` utilisateur (navigateur)** - très rare
2. **`!important` auteur (votre CSS)**
3. Styles inline (`style=""`)
4. Sélecteurs par spécificité décroissante
5. Héritage du parent
6. Valeurs par défaut du navigateur

### Conflit entre plusieurs `!important`

Si plusieurs règles avec `!important` ciblent la même propriété, c'est la **spécificité** puis l'**ordre** qui départagent :

```css
/* Spécificité : (0, 0, 0, 1) */
p {
  color: blue !important;
}

/* Spécificité : (0, 0, 1, 0) - GAGNE */
.intro {
  color: red !important;
}
```

**Résultat : rouge** (même avec `!important`, la spécificité compte)

### ⚠️ Pourquoi éviter `!important` ?

**Problèmes causés par `!important` :**

1. **Casse la cascade naturelle**
```css
.button {
  background: blue !important;
}

/* Impossible de surcharger plus tard */
.button-special {
  background: red;  /* Ne fonctionnera PAS */
}
```

2. **Crée des guerres d'escalade**
```css
.button {
  color: blue !important;
}

/* Obligé d'utiliser !important aussi */
.button:hover {
  color: red !important;  /* Escalade ! */
}
```

3. **Rend le débogage difficile**
```css
/* Impossible de savoir pourquoi un style ne s'applique pas */
.element {
  color: green;  /* Pourquoi ça ne marche pas ? */
}

/* Ah, il y a un !important ailleurs... */
```

4. **Empêche les modifications dynamiques**
```javascript
// Très difficile de surcharger en JavaScript
element.style.color = "red";  // Ne fonctionnera pas si !important existe
```

### Cas d'usage légitime de `!important`

**✅ Rares situations acceptables :**

1. **Utilitaires qui doivent TOUJOURS s'appliquer :**
```css
.hidden {
  display: none !important;
}

.text-center {
  text-align: center !important;
}
```

2. **Surcharger des styles inline qu'on ne contrôle pas :**
```css
/* Plugin externe qui ajoute des styles inline */
.external-widget {
  background: blue !important;  /* Force notre style */
}
```

3. **Framework CSS (Bootstrap, Tailwind) :**
```css
/* Classes utilitaires */
.m-0 {
  margin: 0 !important;
}
```

---

## L'héritage CSS

### Qu'est-ce que l'héritage ?

Certaines propriétés CSS sont **héritées** des éléments parents vers les enfants, sans qu'il soit nécessaire de les redéfinir.

### Propriétés héritées

**Héritées par défaut :**
- Propriétés de texte : `color`, `font-family`, `font-size`, `font-weight`, `line-height`, `text-align`
- Propriétés de liste : `list-style`
- Visibilité : `visibility`
- Curseur : `cursor`

**NON héritées par défaut :**
- Modèle de boîte : `margin`, `padding`, `border`, `width`, `height`
- Positionnement : `position`, `top`, `left`
- Fond : `background`
- Display : `display`

### Exemple d'héritage

```html
<div style="color: blue; font-size: 16px;">
  <p>Ce texte hérite de la couleur et de la taille</p>
  <span>Celui-ci aussi</span>
</div>
```

Les enfants (`<p>` et `<span>`) hériteront automatiquement de `color: blue` et `font-size: 16px`.

### Forcer l'héritage : `inherit`

Vous pouvez forcer une propriété à hériter avec le mot-clé `inherit` :

```css
.child {
  border: inherit;  /* Hérite de la bordure du parent */
}
```

### Réinitialiser l'héritage : `initial` et `unset`

**`initial` :** Remet la valeur par défaut CSS (pas celle du navigateur)
```css
.element {
  color: initial;  /* Remet à la valeur initiale CSS (noir) */
}
```

**`unset` :**
- Si la propriété hérite normalement → se comporte comme `inherit`
- Si la propriété n'hérite pas → se comporte comme `initial`

```css
.element {
  color: unset;      /* Hérite (color hérite normalement) */
  margin: unset;     /* Initial (margin n'hérite pas) */
}
```

---

## Stratégies pour gérer la spécificité

### 1. Préférer les classes aux IDs

**❌ Mauvaise pratique :**
```css
#header { }
#nav { }
#content { }
```

**✅ Bonne pratique :**
```css
.header { }
.nav { }
.content { }
```

**Avantage :** Plus facile à surcharger, plus flexible.

### 2. Garder les sélecteurs simples

**❌ Trop spécifique :**
```css
body div.container section#main article.post p.text { }
```

**✅ Plus simple :**
```css
.post-text { }
```

### 3. Utiliser des classes de modification

**Pattern BEM (Block Element Modifier) :**
```css
/* Block */
.button { }

/* Modificateur */
.button--primary { }
.button--large { }
```

**HTML :**
```html
<button class="button button--primary button--large">Cliquez</button>
```

### 4. Éviter la sur-qualification

**❌ Sur-qualifié :**
```css
div.container { }      /* div n'est pas nécessaire */
ul.menu { }
```

**✅ Suffisant :**
```css
.container { }
.menu { }
```

### 5. Organiser le CSS par spécificité croissante

```css
/* 1. Reset / Normalisation */
* { margin: 0; padding: 0; }

/* 2. Éléments de base */
body { }
h1 { }
p { }

/* 3. Classes de layout */
.container { }
.row { }

/* 4. Composants */
.button { }
.card { }

/* 5. Modifications d'état */
.button:hover { }
.card.active { }

/* 6. Utilitaires (peuvent utiliser !important) */
.hidden { display: none !important; }
```

---

## Déboguer les problèmes de spécificité

### 1. Utiliser les DevTools du navigateur

**Comment voir la spécificité :**
1. Ouvrir les DevTools (F12)
2. Inspecter l'élément
3. Observer l'onglet "Styles"
4. Les règles barrées sont **écrasées**
5. Les règles actives sont **appliquées**

**Exemple dans DevTools :**
```
Styles
  element.style {
    color: blue;  ← Style inline (gagne)
  }

  #header .title {
    color: red;   ← Barré (écrasé par inline)
  }

  .title {
    color: green; ← Barré (écrasé par ID)
  }
```

### 2. Calculer la spécificité manuellement

**Outil mnémotechnique : "100-10-1"**
- ID = 100 points
- Classe = 10 points
- Élément = 1 point

(Ce n'est pas exact mathématiquement, mais ça aide à visualiser)

### 3. Vérifier l'ordre des fichiers CSS

```html
<!-- Le dernier chargé a priorité en cas d'égalité -->
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="theme.css">
<link rel="stylesheet" href="custom.css">  ← Gagne en cas d'égalité
```

### 4. Chercher les `!important`

Rechercher dans vos fichiers CSS :
```
Ctrl + F → "!important"
```

Souvent, c'est un `!important` oublié qui empêche vos styles de s'appliquer.

---

## Exemples pratiques complets

### Exemple 1 : Comprendre un conflit

**HTML :**
```html
<nav id="main-nav" class="navigation">
  <ul class="menu">
    <li class="menu-item active">
      <a href="#">Accueil</a>
    </li>
  </ul>
</nav>
```

**CSS :**
```css
/* Règle 1 : (0, 0, 0, 1) */
a {
  color: blue;
}

/* Règle 2 : (0, 0, 1, 1) */
.menu a {
  color: green;
}

/* Règle 3 : (0, 0, 2, 2) */
.menu .menu-item a {
  color: orange;
}

/* Règle 4 : (0, 1, 1, 2) */
#main-nav .menu-item a {
  color: red;
}

/* Règle 5 : (0, 0, 2, 1) */
.active a {
  color: purple;
}
```

**Question :** Quelle couleur pour le lien ?

**Analyse :**
- Règle 1 : (0, 0, 0, 1) = 1
- Règle 2 : (0, 0, 1, 1) = 11
- Règle 3 : (0, 0, 2, 2) = 22
- Règle 4 : (0, 1, 1, 2) = 112 ← **GAGNE**
- Règle 5 : (0, 0, 2, 1) = 21

**Réponse : rouge** (Règle 4 avec l'ID)

### Exemple 2 : Résoudre un problème sans !important

**Problème :**
```css
/* Bibliothèque CSS externe */
#content .widget {
  background: gray;
}

/* Votre CSS - ne fonctionne pas */
.widget-special {
  background: blue;  /* Écrasé par l'ID ci-dessus */
}
```

**❌ Mauvaise solution :**
```css
.widget-special {
  background: blue !important;  /* Éviter ! */
}
```

**✅ Bonnes solutions :**

**Solution 1 : Augmenter la spécificité**
```css
#content .widget-special {
  background: blue;  /* Même spécificité que la règle externe */
}
```

**Solution 2 : Utiliser un double classe (plus spécifique)**
```css
.widget.widget-special {
  background: blue;  /* Spécificité : (0, 0, 2, 0) */
}
```

**Solution 3 : Restructurer le HTML si possible**
```html
<!-- Sortir du #content si possible -->
<div class="widget-special">...</div>
```

### Exemple 3 : CSS organisé pour éviter les conflits

**Structure CSS bien organisée :**

```css
/* ==================================
   1. RESET & BASE
   ================================== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Spécificité : (0, 0, 0, 1) */
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
}

/* ==================================
   2. LAYOUT
   ================================== */
/* Spécificité : (0, 0, 1, 0) */
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.header,
.footer {
  padding: 20px;
}

/* ==================================
   3. COMPOSANTS
   ================================== */
/* Spécificité : (0, 0, 1, 0) */
.button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Spécificité : (0, 0, 2, 0) */
.button.button--primary {
  background: blue;
  color: white;
}

.button.button--secondary {
  background: gray;
  color: white;
}

/* ==================================
   4. ÉTATS
   ================================== */
/* Spécificité : (0, 0, 2, 0) */
.button.is-disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* ==================================
   5. UTILITAIRES (peuvent utiliser !important)
   ================================== */
.hidden {
  display: none !important;
}

.text-center {
  text-align: center !important;
}
```

**Avantages de cette organisation :**
- Spécificité croissante naturellement
- Facile à surcharger
- Prévisible
- Maintenable

---

## Résumé

### Points clés à retenir

- 📌 **La cascade détermine quelle règle s'applique** en cas de conflit
- 📌 **La spécificité se calcule en 4 catégories** : inline, ID, classe, élément
- 📌 **Plus le sélecteur est spécifique, plus il a de poids**
- 📌 **En cas d'égalité, la dernière règle gagne**
- 📌 **`!important` écrase tout** mais doit être évité
- 📌 **Certaines propriétés héritent** des parents aux enfants
- 📌 **Les IDs ont une spécificité très élevée** (préférer les classes)
- 📌 **Garder les sélecteurs simples** pour faciliter la maintenance

### Ordre de priorité complet

**Du plus fort au plus faible :**

1. Styles utilisateur avec `!important` (très rare)
2. **Vos styles avec `!important`** ⚠️
3. **Styles inline** `style="..."` (1,0,0,0)
4. **IDs** `#header` (0,1,0,0)
5. **Classes, attributs, pseudo-classes** `.class`, `[attr]`, `:hover` (0,0,1,0)
6. **Éléments, pseudo-éléments** `div`, `::before` (0,0,0,1)
7. **Sélecteur universel** `*` (0,0,0,0)
8. **Héritage** du parent
9. **Valeurs par défaut** du navigateur

### Formule de calcul rapide

```
Spécificité = (inline, IDs, classes/attributs/pseudo-classes, éléments/pseudo-éléments)

Exemples :
p                        → (0, 0, 0, 1)
.intro                   → (0, 0, 1, 0)
#header                  → (0, 1, 0, 0)
div.container p          → (0, 0, 1, 2)
#nav .menu a:hover       → (0, 1, 2, 1)
style="color: red;"      → (1, 0, 0, 0)
```

### Checklist de bonnes pratiques

- ✅ Privilégier les **classes** aux IDs pour le style
- ✅ Garder les sélecteurs **courts et simples**
- ✅ Éviter `!important` sauf pour les utilitaires
- ✅ Organiser le CSS par **spécificité croissante**
- ✅ Utiliser les **DevTools** pour déboguer
- ✅ Comprendre l'**héritage** des propriétés
- ✅ Tester les styles dans l'**inspecteur** avant de les écrire
- ✅ Documenter les cas où `!important` est nécessaire

---

## Outils et ressources

### Calculateurs de spécificité en ligne

- **Specificity Calculator** : https://specificity.keegan.st/
- **Polypane CSS Specificity Calculator** : https://polypane.app/css-specificity-calculator/

### Dans les DevTools

**Chrome / Edge / Firefox :**
- F12 → Onglet "Elements" / "Inspector"
- Cliquer sur un élément
- Observer l'onglet "Styles" / "Computed"
- Les règles barrées sont écrasées

---

## Prochaine étape

Vous maîtrisez maintenant la spécificité et la cascade CSS, deux concepts fondamentaux pour comprendre comment vos styles s'appliquent ! Vous savez désormais :
- Calculer la spécificité d'un sélecteur
- Résoudre les conflits entre règles CSS
- Organiser votre CSS pour éviter les problèmes
- Déboguer efficacement avec les DevTools

Dans la section suivante (4.2), nous allons découvrir les **propriétés de base CSS** : couleurs, typographie, espacements, et le modèle de boîte. C'est là que vous commencerez vraiment à styliser vos pages !

---

**Navigation :**

- ➡️ Section suivante : [4.2 Propriétés de base](../02-proprietes-de-base/README.md)
- 🏠 Retour à la [Table des matières](../../SOMMAIRE.md)

⏭️ [Propriétés de base](/04-css3-styles-et-mise-en-page/02-proprietes-de-base/README.md)
