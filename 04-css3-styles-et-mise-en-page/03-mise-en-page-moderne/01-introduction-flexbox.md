🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.3.1 - Introduction à Flexbox

## Pourquoi Flexbox ?

Avant l'arrivée de Flexbox, créer des mises en page flexibles et alignées en CSS était souvent complexe et nécessitait des astuces peu intuitives (floats, positionnement, etc.). Flexbox (ou **Flexible Box Layout**) a été créé pour simplifier la création de layouts modernes et réactifs.

### Problèmes que Flexbox résout

- **Centrer verticalement** un élément (autrefois très difficile)
- **Répartir l'espace** entre plusieurs éléments de manière équitable
- **Aligner des éléments** de différentes tailles
- **Créer des layouts flexibles** qui s'adaptent à la taille de l'écran
- **Réorganiser l'ordre** des éléments sans modifier le HTML

## Qu'est-ce que Flexbox ?

Flexbox est un **modèle de mise en page unidimensionnel** qui permet d'organiser des éléments dans une direction : soit en ligne (horizontalement), soit en colonne (verticalement).

> **📌 Note importante** : Flexbox travaille dans **une seule dimension à la fois**. Pour des layouts en deux dimensions (lignes ET colonnes simultanément), on utilisera CSS Grid (vu plus tard).

## Les deux acteurs de Flexbox

Pour utiliser Flexbox, il faut comprendre qu'il y a toujours **deux types d'éléments** :

### 1. Le conteneur flex (Flex Container)

C'est l'élément parent auquel on applique `display: flex;`. Il devient alors un **conteneur flexible** qui contrôle la disposition de ses enfants.

```css
.conteneur {
  display: flex;
}
```

### 2. Les éléments flex (Flex Items)

Ce sont les **enfants directs** du conteneur flex. Ils seront automatiquement disposés selon les règles de Flexbox.

```html
<div class="conteneur">
  <!-- Ces trois div sont des éléments flex -->
  <div>Élément 1</div>
  <div>Élément 2</div>
  <div>Élément 3</div>
</div>
```

## Les deux axes de Flexbox

Flexbox fonctionne selon deux axes perpendiculaires :

### L'axe principal (Main Axis)

C'est la direction principale dans laquelle les éléments sont disposés :
- **Par défaut** : de gauche à droite (→)
- Contrôlé par la propriété `flex-direction`

### L'axe secondaire (Cross Axis)

C'est l'axe **perpendiculaire** à l'axe principal :
- Si l'axe principal est horizontal → l'axe secondaire est vertical
- Si l'axe principal est vertical → l'axe secondaire est horizontal

```
Axe principal (horizontal) →
┌─────────────────────────────────┐
│  [Item 1]  [Item 2]  [Item 3]   │
└─────────────────────────────────┘
        ↓ Axe secondaire (vertical)
```

## Activer Flexbox : `display: flex`

Pour transformer un élément en conteneur flex, il suffit d'une seule ligne de CSS :

```css
.conteneur {
  display: flex;
}
```

### Que se passe-t-il quand on applique `display: flex` ?

1. Tous les **enfants directs** deviennent automatiquement des éléments flex
2. Par défaut, les éléments se placent **en ligne** (côte à côte)
3. Les éléments s'adaptent pour tenir dans le conteneur
4. On peut ensuite contrôler leur disposition avec d'autres propriétés Flexbox

## Premier exemple simple

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Introduction Flexbox</title>
  <style>
    .conteneur {
      display: flex;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .item {
      background-color: #4CAF50;
      color: white;
      padding: 20px;
      margin: 10px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="conteneur">
    <div class="item">Item 1</div>
    <div class="item">Item 2</div>
    <div class="item">Item 3</div>
  </div>
</body>
</html>
```

### Résultat visuel

Les trois items s'affichent **côte à côte** (en ligne) au lieu de s'empiler verticalement comme ils le feraient normalement avec `display: block`.

```
┌────────────────────────────────────────┐
│  [Item 1]  [Item 2]  [Item 3]          │
└────────────────────────────────────────┘
```

## Flexbox vs disposition classique

### Sans Flexbox (comportement par défaut)

```css
/* Éléments div normaux (display: block) */
.item {
  background-color: lightblue;
  padding: 20px;
}
```

**Résultat** : Les éléments s'empilent verticalement (chacun prend toute la largeur)

```
┌────────────────────────────┐
│  Item 1                    │
├────────────────────────────┤
│  Item 2                    │
├────────────────────────────┤
│  Item 3                    │
└────────────────────────────┘
```

### Avec Flexbox

```css
.conteneur {
  display: flex;
}

.item {
  background-color: lightblue;
  padding: 20px;
}
```

**Résultat** : Les éléments se placent côte à côte

```
┌────────────────────────────────────────┐
│  [Item 1]  [Item 2]  [Item 3]          │
└────────────────────────────────────────┘
```

## Propriétés Flexbox : aperçu

Flexbox offre de nombreuses propriétés pour contrôler la disposition. Elles se divisent en deux catégories :

### Propriétés du conteneur flex

Ces propriétés s'appliquent sur le **parent** :
- `flex-direction` : direction des éléments (ligne ou colonne)
- `justify-content` : alignement sur l'axe principal
- `align-items` : alignement sur l'axe secondaire
- `flex-wrap` : passage à la ligne si nécessaire
- `gap` : espacement entre les éléments

### Propriétés des éléments flex

Ces propriétés s'appliquent sur les **enfants** :
- `flex-grow` : capacité à grandir
- `flex-shrink` : capacité à rétrécir
- `flex-basis` : taille de base
- `align-self` : alignement individuel

> **📚 Dans les prochaines leçons**, nous explorerons en détail chacune de ces propriétés avec des exemples pratiques.

## Cas d'usage courants de Flexbox

Flexbox est particulièrement adapté pour :

### 1. Barres de navigation

```css
nav {
  display: flex;
  justify-content: space-between;
}
```

### 2. Cartes disposées en ligne

```css
.carte-conteneur {
  display: flex;
  gap: 20px;
}
```

### 3. Centrer un élément (horizontal ET vertical)

```css
.conteneur {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

### 4. Footer qui reste en bas de page

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1; /* Prend tout l'espace disponible */
}
```

## Points clés à retenir

✅ **Flexbox est unidimensionnel** : il organise les éléments dans une seule direction à la fois

✅ **Deux acteurs** : le conteneur flex (`display: flex`) et ses enfants directs (éléments flex)

✅ **Deux axes** : l'axe principal (main axis) et l'axe secondaire (cross axis)

✅ **Simple à activer** : une seule ligne de CSS suffit (`display: flex`)

✅ **Très puissant** : résout facilement des problèmes de mise en page autrefois complexes

✅ **Support navigateur** : excellent support sur tous les navigateurs modernes

## Quand utiliser Flexbox ?

**✅ Utilisez Flexbox pour :**
- Aligner des éléments dans une direction (ligne ou colonne)
- Distribuer l'espace entre des éléments
- Centrer des éléments
- Créer des composants réactifs simples (navigation, cartes, etc.)

**❌ Préférez CSS Grid pour :**
- Des layouts complexes en 2D (lignes ET colonnes)
- Des grilles de mise en page complètes
- Nous verrons Grid dans les prochaines leçons !

## Conclusion

Flexbox est un outil **essentiel** du CSS moderne. Il simplifie radicalement la création de mises en page et est devenu la méthode standard pour organiser des éléments en ligne ou en colonne.

Dans les prochaines leçons, nous allons explorer en détail :
- Les propriétés du **conteneur flex** (flex-direction, justify-content, align-items...)
- Les propriétés des **éléments flex** (flex-grow, flex-shrink, flex-basis...)
- Des exemples pratiques et des patterns courants

---


⏭️ [Conteneur flex : flex-direction, justify-content, align-items](/04-css3-styles-et-mise-en-page/03-mise-en-page-moderne/02-conteneur-flex.md)
