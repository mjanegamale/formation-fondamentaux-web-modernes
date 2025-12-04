🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.3 - Accessibilité web (a11y)

## Introduction

Bienvenue dans cette section dédiée à l'**accessibilité web** (souvent abrégée **a11y**, car il y a 11 lettres entre le "a" et le "y" d'accessibility).

L'accessibilité web est la **pratique de rendre les sites et applications web utilisables par tous**, indépendamment de leurs capacités physiques, sensorielles ou cognitives. C'est un aspect fondamental du développement web moderne qui va bien au-delà d'une simple "bonne pratique" — c'est une **responsabilité professionnelle** et, dans de nombreux cas, une **obligation légale**.

---

## Pourquoi apprendre l'accessibilité dès le début ?

En tant que développeur web débutant, vous pourriez vous demander pourquoi l'accessibilité est incluse si tôt dans votre parcours d'apprentissage. Voici pourquoi c'est essentiel :

### 1. **C'est plus facile d'intégrer l'accessibilité dès le départ** 🏗️

Corriger l'accessibilité d'un site existant coûte **beaucoup plus cher** en temps et en ressources que de la concevoir dès le début. En apprenant les bonnes pratiques maintenant, vous les intégrerez naturellement dans votre façon de coder.

### 2. **C'est une compétence professionnelle recherchée** 💼

Les entreprises recherchent de plus en plus des développeurs qui comprennent l'accessibilité. C'est un **atout sur votre CV** et une compétence qui vous distinguera des autres candidats.

### 3. **Vous améliorerez l'expérience de TOUS vos utilisateurs** 🌟

Contrairement à une idée reçue, l'accessibilité ne profite pas qu'aux personnes handicapées. Un site accessible est :
- Plus facile à utiliser pour tout le monde
- Mieux référencé (SEO)
- Plus rapide et performant
- Plus robuste et maintenable

### 4. **C'est une question d'éthique et d'inclusion** ❤️

Le web a été créé pour être **universel et accessible à tous**. En tant que développeur, vous avez le pouvoir (et la responsabilité) de construire un web inclusif.

---

## Ce que vous allez apprendre dans cette section

Cette section couvre les **4 piliers fondamentaux** de l'accessibilité web que tout développeur doit maîtriser :

---

### 📚 [6.3.1 - Importance de l'accessibilité](./01-importance-accessibilite.md)

**Ce que vous découvrirez :**

Dans cette première partie, vous comprendrez :
- Ce qu'est concrètement l'accessibilité web
- **Qui est concerné** par l'accessibilité (vous serez surpris !)
- Les **raisons multiples** de rendre vos sites accessibles :
  - Humanité et inclusion
  - Obligations légales (lois et normes)
  - Avantages SEO
  - Bénéfices pour tous les utilisateurs
- Les **4 principes POUR** (Perceptible, Utilisable, Compréhensible, Robuste)
- Les technologies d'assistance courantes (lecteurs d'écran, navigation au clavier, etc.)
- Les idées reçues à déconstruire

**Pourquoi c'est important :** Cette section pose les bases et vous donnera une **compréhension globale** de l'enjeu. Vous comprendrez que l'accessibilité n'est pas une contrainte, mais une opportunité d'améliorer la qualité de votre travail.

---

### 🏷️ [6.3.2 - Attributs ARIA de base](./02-attributs-aria.md)

**Ce que vous découvrirez :**

Après avoir compris l'importance, vous apprendrez les outils techniques :
- Qu'est-ce qu'**ARIA** (Accessible Rich Internet Applications)
- La **règle d'or** : "Le meilleur ARIA, c'est pas d'ARIA"
- Les 3 catégories d'attributs ARIA :
  - **Roles** : définir le type d'un élément
  - **Properties** : caractéristiques d'un élément
  - **States** : états dynamiques
- Les attributs essentiels : `aria-label`, `aria-labelledby`, `aria-hidden`, `aria-expanded`, `aria-live`, etc.
- Des **exemples concrets** (accordéons, notifications, menus)
- Les erreurs courantes à éviter

**Pourquoi c'est important :** ARIA est l'outil qui permet d'enrichir l'accessibilité des applications web modernes. Vous apprendrez à **communiquer efficacement** avec les technologies d'assistance.

---

### ⌨️ [6.3.3 - Navigation au clavier](./03-navigation-clavier.md)

**Ce que vous découvrirez :**

La navigation au clavier est **l'un des aspects les plus critiques** de l'accessibilité :
- Les **touches essentielles** (Tab, Enter, Espace, Escape, flèches)
- Les éléments naturellement focusables vs non focusables
- L'attribut **`tabindex`** et ses 3 valeurs (-1, 0, 1+)
- L'**indicateur de focus** (`:focus` et `:focus-visible`)
- Comment rendre des éléments personnalisés accessibles au clavier
- L'**ordre de tabulation** et son importance
- Les **pièges à clavier** à éviter absolument
- Les **skip links** pour améliorer la navigation

**Pourquoi c'est important :** De nombreux utilisateurs dépendent **exclusivement** du clavier. Si votre site n'est pas navigable au clavier, il n'est tout simplement **pas accessible**. Cette section vous apprendra à tester et corriger ce point crucial.

---

### 🎨 [6.3.4 - Contraste et lisibilité](./04-contraste-lisibilite.md)

**Ce que vous découvrirez :**

La lisibilité visuelle est essentielle pour tous les utilisateurs :
- Les **normes WCAG** et les ratios de contraste (AA, AAA)
- Comment **calculer et vérifier** le contraste (outils en ligne, DevTools)
- Les **seuils minimums** à respecter (4.5:1 pour texte normal, 3:1 pour texte large)
- Au-delà du contraste :
  - Taille de police appropriée
  - Interligne (line-height)
  - Longueur de ligne optimale
  - Choix de polices lisibles
- Les cas particuliers :
  - Texte sur image
  - Daltonisme et utilisation de la couleur
  - Mode sombre (dark mode)
- Les **outils de vérification** du contraste
- Comment créer des **palettes accessibles**

**Pourquoi c'est important :** Un site peut avoir la meilleure structure HTML et les meilleurs attributs ARIA, mais si le texte n'est **pas lisible**, il n'est pas accessible. Cette section vous apprendra à créer des interfaces visuellement accessibles.

---

## Comment aborder cette section ?

### 📖 Lecture recommandée

Nous vous recommandons de suivre l'ordre des sections :

1. **Commencez par l'importance** pour comprendre le "pourquoi"
2. **Apprenez ARIA** pour comprendre les outils techniques
3. **Maîtrisez la navigation au clavier** pour l'interactivité
4. **Perfectionnez le visuel** avec le contraste et la lisibilité

### 🧪 Approche pratique

Pour chaque section :
1. **Lisez attentivement** les concepts et explications
2. **Testez les exemples de code** fournis
3. **Inspectez des sites existants** avec les DevTools
4. **Testez votre propre code** avec les outils recommandés
5. **Naviguez au clavier** sur vos projets
6. **Utilisez un lecteur d'écran** si possible (NVDA, VoiceOver)

### 🔧 Outils à avoir sous la main

Pour profiter pleinement de cette section, vous aurez besoin de :
- Un navigateur moderne (Chrome, Firefox, Safari)
- Les **DevTools** (déjà couverts en Section 2.4)
- Extension **WAVE** ou **axe DevTools**
- Un **lecteur d'écran** (optionnel mais recommandé) :
  - NVDA (Windows, gratuit)
  - VoiceOver (macOS/iOS, intégré)
  - TalkBack (Android, intégré)

---

## Points clés à retenir

Avant de commencer votre apprentissage de l'accessibilité, gardez en tête ces principes :

### ✅ L'accessibilité est pour TOUS

Ce n'est pas une fonctionnalité pour une minorité — c'est un **standard de qualité** qui améliore l'expérience de tous les utilisateurs.

### ✅ L'accessibilité commence dès la conception

N'attendez pas la fin du projet pour y penser. **Intégrez-la dès le début**, dans votre façon de coder.

### ✅ Le HTML sémantique est la base

Avant d'ajouter des attributs ARIA complexes, assurez-vous d'utiliser les **bonnes balises HTML**. Un `<button>` vaut mieux qu'une `<div>` avec `role="button"`.

### ✅ Testez, testez, testez

La meilleure façon de comprendre l'accessibilité est de **tester votre site** :
- Avec le clavier uniquement
- Avec un lecteur d'écran
- Avec les outils automatiques
- Avec de vrais utilisateurs en situation de handicap

### ✅ L'accessibilité est un processus continu

Il n'y a pas de moment où votre site sera "100% accessible pour toujours". C'est un **engagement permanent** d'amélioration et de maintenance.

---

## Les WCAG : votre référence

Les **WCAG (Web Content Accessibility Guidelines)** du W3C sont la référence mondiale en matière d'accessibilité web. Elles définissent 3 niveaux de conformité :

- **Niveau A** : Conformité minimale (éléments de base)
- **Niveau AA** : Conformité standard **(recommandé et souvent requis par la loi)**
- **Niveau AAA** : Conformité élevée (idéal mais parfois difficile à atteindre)

Dans cette formation, nous nous concentrons sur les pratiques qui vous permettront d'atteindre **le niveau AA**, qui est :
- Le niveau **exigé par la plupart des législations**
- Un **bon équilibre** entre accessibilité et faisabilité
- Ce que les **professionnels visent** en priorité

---

## Accessibilité et développement moderne

L'accessibilité n'est **pas en opposition** avec le développement moderne. Au contraire :

### 🆕 Les frameworks modernes facilitent l'accessibilité

- React, Vue, Angular ont des outils intégrés pour l'accessibilité
- Les composants modernes incluent souvent ARIA par défaut
- Les linters (ESLint) peuvent détecter les problèmes d'accessibilité

### 🆕 Les standards évoluent

- HTML5 a ajouté de nombreuses balises sémantiques
- CSS moderne facilite la création de designs accessibles
- Les DevTools intègrent des outils d'audit d'accessibilité

### 🆕 La communauté s'engage

- De plus en plus de ressources et de formations disponibles
- Des bibliothèques de composants accessibles (Reach UI, Radix UI)
- Une prise de conscience croissante dans l'industrie

**En apprenant l'accessibilité maintenant, vous êtes en phase avec l'évolution du web.**

---

## Votre engagement d'accessibilité

Avant de continuer, prenez un moment pour vous engager :

> **"En tant que développeur web, je m'engage à créer des sites et applications accessibles à tous, en intégrant l'accessibilité dès la conception de mes projets."**

Cet engagement fera de vous un **meilleur développeur** et contribuera à un **web plus inclusif**.

---

## Prêt à commencer ?

Vous avez maintenant une vue d'ensemble de ce qui vous attend dans cette section. L'accessibilité peut sembler intimidante au début, mais ne vous inquiétez pas :

- Les concepts sont **progressifs** et bien expliqués
- Les exemples sont **concrets** et testables
- Les bonnes pratiques sont **simples** à appliquer

**Commençons par comprendre pourquoi l'accessibilité est si importante.**

👉 **[Suivant : 6.3.1 - Importance de l'accessibilité](./01-importance-accessibilite.md)**

---

## Ressources générales sur l'accessibilité

Pour aller plus loin dans votre apprentissage de l'accessibilité :

### 📚 Documentation officielle
- [W3C - Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/)
- [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG21/)
- [MDN - Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)

### 🛠️ Outils essentiels
- [WAVE - Web Accessibility Evaluation Tool](https://wave.webaim.org/)
- [axe DevTools](https://www.deque.com/axe/devtools/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) (intégré à Chrome)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)

### 📖 Lectures recommandées
- [WebAIM](https://webaim.org/) - Ressources et articles sur l'accessibilité
- [A11y Project](https://www.a11yproject.com/) - Guide communautaire
- [Inclusive Components](https://inclusive-components.design/) - Patterns de composants accessibles

### 🇫🇷 Ressources en français
- [RGAA - Référentiel Général d'Amélioration de l'Accessibilité](https://www.numerique.gouv.fr/publications/rgaa-accessibilite/)
- [AcceDe Web](https://www.accede-web.com/) - Notices et ressources
- [Access42](https://access42.net/) - Blog et formations

---

**Bonne découverte de l'accessibilité web ! 🌍✨**

⏭️ [Importance de l'accessibilité](/06-integration-html-css-javascript/03-accessibilite-web/01-importance-accessibilite.md)
