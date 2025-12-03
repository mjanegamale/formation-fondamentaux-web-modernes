🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2 Éléments structurants

## Introduction

Maintenant que vous maîtrisez les fondamentaux HTML (structure de base, métadonnées, encodage), il est temps de passer au cœur de votre contenu : les **éléments structurants**. Ce sont les briques qui donnent vie à vos pages web !

Si les fondamentaux étaient le squelette de votre page, les éléments structurants en sont **le corps et les organes**. Ils organisent, présentent et donnent du sens à votre contenu.

**Dans cette section, vous allez découvrir :**
- Comment structurer votre texte avec des titres hiérarchiques
- Comment organiser votre contenu en paragraphes et listes
- Les éléments sémantiques HTML5 qui révolutionnent la structure web
- Comment créer des liens et naviguer entre les pages
- Quand et comment utiliser les conteneurs génériques

## Qu'est-ce qu'un "élément structurant" ?

Un **élément structurant** est une balise HTML qui organise et donne du sens à votre contenu. Ces éléments :

- **Organisent** : Ils créent une hiérarchie claire (titres, sections, listes)
- **Donnent du sens** : Ils indiquent le rôle de chaque partie (navigation, article, en-tête)
- **Structurent visuellement** : Ils créent la mise en page de base (avant même le CSS)
- **Améliorent l'accessibilité** : Ils aident les technologies d'assistance à comprendre votre page
- **Optimisent le SEO** : Ils permettent aux moteurs de recherche d'indexer correctement

**Analogie :** Imaginez un journal papier :
- Les **titres** en gros caractères → balises `<h1>` à `<h6>`
- Les **paragraphes** de texte → balise `<p>`
- Les **listes à puces** → balise `<ul>` + `<li>`
- L'**en-tête** avec le logo → balise `<header>`
- Les **articles** → balise `<article>`
- La **navigation** / sommaire → balise `<nav>`
- Les **publicités** sur le côté → balise `<aside>`
- Le **pied de page** avec les mentions → balise `<footer>`

HTML vous permet de recréer cette structure logique pour le web.

## Pourquoi cette section est cruciale ?

### 1. C'est 80% de votre code HTML quotidien

Les éléments que vous allez apprendre dans cette section constituent la **majorité du code HTML** que vous écrirez dans votre carrière :
- Tous les sites ont des titres
- Tous les sites ont des paragraphes et des listes
- Tous les sites modernes utilisent les éléments sémantiques
- Tous les sites ont des liens

**Maîtriser ces éléments = maîtriser l'essentiel du HTML.**

### 2. La base de toute structure web moderne

Avant d'apprendre CSS ou JavaScript, vous devez savoir créer une **structure HTML solide**. C'est comme apprendre à construire les murs d'une maison avant de penser à la décoration ou à l'électricité.

### 3. L'accessibilité dès le départ

Une bonne structure HTML = un site accessible par défaut. Les éléments structurants sont la fondation de l'accessibilité web :
- Les lecteurs d'écran s'appuient sur la hiérarchie des titres
- Les listes permettent une navigation efficace
- Les éléments sémantiques indiquent clairement le rôle de chaque zone

### 4. Le SEO commence ici

Google et les autres moteurs de recherche analysent la **structure** de votre HTML pour comprendre et classer votre contenu :
- La hiérarchie des titres indique l'importance des sujets
- Les liens créent le maillage interne de votre site
- Les éléments sémantiques aident à identifier le contenu principal

## Vue d'ensemble de la section

Cette section est organisée en **cinq sous-sections** qui s'enchaînent logiquement :

### 3.2.1 Titres et hiérarchie sémantique

**Ce que vous apprendrez :**
- Les six niveaux de titres (h1 à h6)
- Comment créer une hiérarchie logique
- L'importance du H1 unique
- Les bonnes pratiques pour le SEO et l'accessibilité

**Pourquoi c'est important :**
Les titres sont la **colonne vertébrale** de votre contenu. Une bonne hiérarchie de titres rend votre page scandable, accessible et bien référencée.

**Temps estimé :** 20-30 minutes

### 3.2.2 Paragraphes et listes

**Ce que vous apprendrez :**
- Créer des paragraphes avec `<p>`
- Les listes non ordonnées (`<ul>`)
- Les listes ordonnées (`<ol>`)
- Les listes de définition (`<dl>`)
- L'imbrication de listes

**Pourquoi c'est important :**
Les paragraphes et listes sont les **éléments de base** pour présenter votre contenu textuel. Vous les utiliserez dans chaque page que vous créerez.

**Temps estimé :** 30-40 minutes

### 3.2.3 Éléments sémantiques HTML5

**Ce que vous apprendrez :**
- Les nouveaux éléments HTML5 (`<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`)
- La différence entre `<article>` et `<section>`
- Comment structurer une page moderne
- L'importance de la sémantique

**Pourquoi c'est important :**
HTML5 a révolutionné la façon de structurer les pages web. Ces éléments remplacent les `<div>` anonymes par des balises qui ont du **sens** et améliorent drastiquement l'accessibilité et le SEO.

**Temps estimé :** 40-50 minutes

### 3.2.4 Liens hypertextes et navigation

**Ce que vous apprendrez :**
- Créer des liens avec `<a>`
- Les différents types de liens (internes, externes, ancres)
- Les attributs importants (`href`, `target`, `rel`)
- Créer des menus de navigation
- Les bonnes pratiques d'accessibilité

**Pourquoi c'est important :**
Les liens sont **l'essence même du web**. Sans liens, Internet ne serait qu'une collection de pages isolées. Maîtriser les liens, c'est comprendre ce qui fait du web un réseau.

**Temps estimé :** 40-50 minutes

### 3.2.5 Conteneurs génériques : div et span

**Ce que vous apprendrez :**
- Quand utiliser `<div>` (conteneur de bloc)
- Quand utiliser `<span>` (conteneur en ligne)
- La différence entre éléments de bloc et en ligne
- Pourquoi privilégier les éléments sémantiques
- Éviter la "divitis"

**Pourquoi c'est important :**
Après avoir appris tous les éléments sémantiques, vous devez comprendre **quand** et **comment** utiliser les conteneurs génériques. Cette section vous évite de mauvaises habitudes courantes chez les débutants.

**Temps estimé :** 30-40 minutes

## Progression pédagogique

Cette section suit une logique d'apprentissage progressive :

**1. Les bases textuelles** (Titres, paragraphes, listes)
→ Les éléments fondamentaux pour présenter du contenu

**2. La structure sémantique** (Éléments HTML5)
→ Comment organiser ces éléments dans une page moderne

**3. La navigation** (Liens)
→ Comment connecter vos pages entre elles

**4. Les conteneurs** (Div et span)
→ Quand utiliser des éléments génériques (en dernier recours)

Chaque sous-section s'appuie sur les précédentes pour construire progressivement vos compétences.

## Ce que vous saurez faire après cette section

À la fin de cette section, vous serez capable de :

✅ **Créer une structure HTML complète** avec titres, paragraphes, listes et éléments sémantiques

✅ **Organiser votre contenu** de manière logique et hiérarchique

✅ **Utiliser les balises appropriées** pour chaque type de contenu (pas de divs partout !)

✅ **Créer des menus de navigation** et des liens efficaces

✅ **Comprendre la sémantique** et son impact sur l'accessibilité et le SEO

✅ **Structurer une page web moderne** selon les standards HTML5

✅ **Éviter les erreurs courantes** des débutants (divitis, mauvaise hiérarchie, etc.)

## Le principe de sémantique : fil rouge de cette section

Un concept traverse toute cette section : la **sémantique**. Mais qu'est-ce que cela signifie concrètement ?

### Définition simple

**La sémantique** en HTML signifie que chaque balise a un **sens** et décrit le **rôle** de son contenu, pas seulement son apparence.

### Exemple concret

❌ **Non sémantique (ancien style) :**
```html
<div class="titre-gros">Mon titre</div>
<div>Mon paragraphe</div>
<div class="menu">
    <div>Accueil</div>
    <div>Services</div>
</div>
```

✅ **Sémantique (moderne) :**
```html
<h1>Mon titre</h1>
<p>Mon paragraphe</p>
<nav>
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services">Services</a></li>
    </ul>
</nav>
```

**Pourquoi c'est mieux ?**
- **Accessible** : Les lecteurs d'écran comprennent la structure
- **SEO** : Google sait ce qui est important (le h1, la navigation)
- **Maintenable** : Vous comprenez instantanément le rôle de chaque élément
- **Flexible** : Le style peut changer (avec CSS) sans modifier le HTML

### Pensez "sens" avant "apparence"

Tout au long de cette section, rappelez-vous :
1. **Choisissez la balise selon son sens**, pas selon son apparence par défaut
2. **Le style viendra plus tard** avec CSS
3. **La structure HTML doit avoir du sens** même sans CSS

## Comment tirer le meilleur de cette section ?

### 1. Suivez l'ordre

Les sous-sections sont dans un ordre logique. Ne sautez pas d'étape, même si un sujet vous semble simple.

### 2. Pratiquez immédiatement

Après chaque nouvelle balise apprise, **testez-la** dans votre éditeur :
- Créez un fichier HTML
- Écrivez le code
- Ouvrez-le dans un navigateur
- Inspectez-le avec les DevTools

### 3. Pensez structure avant style

Ne vous préoccupez **pas encore** de l'apparence visuelle. Concentrez-vous sur la **structure logique** de votre contenu. Le CSS viendra plus tard (Chapitre 4).

### 4. Utilisez les outils

- **VS Code** : Pour écrire votre code
- **Navigateur** : Pour voir le résultat
- **DevTools** (F12) : Pour inspecter la structure
- **Validateur W3C** : Pour vérifier que votre code est correct

### 5. Prenez des notes

Gardez une trace des balises que vous apprenez :
- Quel est leur rôle ?
- Quand les utiliser ?
- Quelles sont leurs particularités ?

### 6. Construisez des exemples personnels

Au lieu de simplement copier les exemples, créez vos propres pages :
- Un CV en HTML
- La page d'accueil d'un site imaginaire
- Un article de blog
- Une recette de cuisine

Cela ancrera mieux vos connaissances.

## Les pièges à éviter

### Piège 1 : Choisir les balises pour leur apparence

❌ **Mauvais :**
"J'utilise h3 parce qu'il a la taille que je veux"

✅ **Bon :**
"J'utilise h3 parce que c'est un titre de niveau 3 dans ma hiérarchie"

### Piège 2 : Tout mettre dans des divs

❌ **Mauvais :**
```html
<div>Titre</div>
<div>Paragraphe</div>
```

✅ **Bon :**
```html
<h1>Titre</h1>
<p>Paragraphe</p>
```

### Piège 3 : Oublier l'accessibilité

Pensez toujours : "Est-ce que ma structure est compréhensible pour quelqu'un qui utilise un lecteur d'écran ?"

### Piège 4 : Négliger la hiérarchie

Respectez toujours l'ordre logique des titres : h1 → h2 → h3 (ne sautez pas de niveaux).

## Connexion avec le reste du cours

Cette section s'inscrit dans un parcours d'apprentissage cohérent :

**Vous venez de voir (Section 3.1) :**
- La structure de base d'un document HTML5
- Les métadonnées essentielles
- L'encodage et la validation

**Vous êtes ici (Section 3.2) :**
- Les éléments pour structurer votre contenu
- La sémantique HTML5
- La navigation et les liens

**Vous verrez ensuite (Section 3.3 à 3.5) :**
- Les images et contenus multimédia
- Les formulaires interactifs
- Les tableaux de données

**Puis (Chapitre 4) :**
- CSS pour styliser tout ce que vous avez structuré

Chaque étape construit sur la précédente. Les éléments structurants que vous apprenez maintenant seront les **fondations** sur lesquelles vous appliquerez du style (CSS) et de l'interactivité (JavaScript).

## Prêt à commencer ?

Vous allez maintenant apprendre les éléments HTML que vous utiliserez **tous les jours** dans votre pratique du développement web. Ces balises sont le vocabulaire de base du langage HTML.

**Quelques encouragements :**

✨ **C'est plus simple qu'il n'y paraît** : Chaque balise a un rôle clair et logique

✨ **C'est immédiatement utile** : Vous pouvez créer des pages complètes dès la fin de cette section

✨ **C'est la base de tout** : Même les sites les plus complexes utilisent ces mêmes éléments

✨ **Vous progressez vite** : HTML est un langage logique et cohérent

**Rappelez-vous :**
- Allez à votre rythme
- Testez chaque exemple dans votre navigateur
- N'hésitez pas à relire si nécessaire
- Créez vos propres exemples
- Validez votre code avec le validateur W3C

La maîtrise des éléments structurants est la **compétence fondamentale** de tout développeur web. C'est l'investissement en temps le plus rentable que vous puissiez faire dans votre apprentissage du web.

**Commençons par les titres, la colonne vertébrale de tout contenu web !**

---


**Première sous-section** : [3.2.1 Titres (h1-h6) et hiérarchie sémantique](./01-titres-et-hierarchie.md)

## Plan détaillé de la section

1. **[Titres (h1-h6) et hiérarchie sémantique](./01-titres-et-hierarchie.md)**
   - Les six niveaux de titres
   - Le H1 unique et son importance
   - Créer une hiérarchie logique
   - Impact sur le SEO et l'accessibilité

2. **[Paragraphes et listes (ul, ol, dl)](./02-paragraphes-et-listes.md)**
   - Les paragraphes avec `<p>`
   - Listes non ordonnées (`<ul>`)
   - Listes ordonnées (`<ol>`)
   - Listes de définition (`<dl>`)
   - Imbrication de listes

3. **[Éléments sémantiques HTML5](./03-elements-semantiques-html5.md)**
   - `<header>`, `<footer>`, `<nav>`
   - `<main>`, `<article>`, `<section>`
   - `<aside>`, `<figure>`, `<figcaption>`
   - Structurer une page moderne
   - Différence entre `<article>` et `<section>`

4. **[Liens hypertextes et navigation](./04-liens-hypertextes-et-navigation.md)**
   - La balise `<a>` et l'attribut `href`
   - Liens internes et externes
   - Ancres et navigation interne
   - Attributs `target`, `rel`, `download`
   - Créer des menus de navigation
   - Accessibilité des liens

5. **[Conteneurs génériques : div et span](./05-conteneurs-generiques.md)**
   - Quand utiliser `<div>` (bloc)
   - Quand utiliser `<span>` (inline)
   - Différence bloc vs inline
   - Éviter la "divitis"
   - Privilégier la sémantique

⏭️ [Titres (h1-h6) et hiérarchie sémantique](/03-html5-structure-et-semantique/02-elements-structurants/01-titres-et-hierarchie.md)
