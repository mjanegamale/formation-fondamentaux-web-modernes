🔝 Retour au [Sommaire](/SOMMAIRE.md)

# HTML5 - Structure et Sémantique

## Introduction

Bienvenue dans le chapitre consacré à **HTML5**, le langage de balisage qui constitue la fondation de toutes les pages web modernes. HTML est l'acronyme de **HyperText Markup Language** (langage de balisage hypertexte), et la version 5 est la norme actuelle utilisée partout sur le web.

### Qu'est-ce que HTML5 ?

HTML5 n'est pas un langage de programmation, mais un **langage de balisage** : il permet de structurer et d'organiser le contenu d'une page web. Pensez à HTML comme au squelette d'un site web, définissant où se trouvent les titres, les paragraphes, les images, les liens, et tous les autres éléments de contenu.

Imaginez que vous rédigez un document texte : vous utilisez des titres, des sous-titres, des listes à puces, des paragraphes... HTML fait exactement la même chose, mais pour le web. Il dit au navigateur : "Ceci est un titre principal", "Ceci est un paragraphe", "Ceci est une image", etc.

### Pourquoi "5" ?

HTML5 est la cinquième révision majeure du langage HTML. Lancée officiellement en 2014, cette version a apporté de nombreuses améliorations par rapport aux versions précédentes :

- **Des éléments sémantiques** : des balises qui décrivent clairement leur contenu (comme `<header>`, `<nav>`, `<article>`)
- **Support multimédia natif** : intégration simple de vidéos et d'audio sans plugins externes
- **Formulaires améliorés** : nouveaux types de champs avec validation intégrée
- **APIs JavaScript** : nouvelles capacités pour créer des applications web riches
- **Meilleure accessibilité** : structure plus claire pour les technologies d'assistance

### La notion de sémantique

Un concept central de HTML5 est la **sémantique**. Mais qu'est-ce que cela signifie ?

La sémantique en HTML, c'est utiliser des balises qui ont du **sens**, qui décrivent clairement le rôle du contenu qu'elles encadrent. Par exemple :

- Plutôt que d'utiliser un simple `<div>` générique pour tout, on utilisera `<header>` pour l'en-tête de la page
- Plutôt qu'un autre `<div>`, on utilisera `<nav>` pour la navigation principale
- Au lieu d'un énième `<div>`, on utilisera `<article>` pour un article de blog

**Pourquoi est-ce important ?**

1. **Pour les moteurs de recherche** : ils comprennent mieux la structure de votre page et peuvent mieux indexer votre contenu
2. **Pour l'accessibilité** : les lecteurs d'écran utilisés par les personnes en situation de handicap peuvent naviguer plus facilement dans votre contenu
3. **Pour la maintenabilité** : votre code est plus lisible et compréhensible, même des mois après l'avoir écrit
4. **Pour les autres développeurs** : ils comprennent immédiatement la structure de votre page

### HTML : la base incontournable

Avant d'apprendre CSS pour styliser vos pages ou JavaScript pour les rendre interactives, il est **essentiel** de maîtriser HTML. C'est comme apprendre l'alphabet avant d'écrire des phrases : sans une base solide en HTML, tout le reste sera plus difficile.

Un bon code HTML, c'est :
- Une structure **logique** et **claire**
- Des balises **sémantiques** appropriées
- Un code **valide** (qui respecte les standards)
- Une base **accessible** à tous les utilisateurs

### Ce que vous allez apprendre dans ce chapitre

Ce chapitre est organisé en cinq grandes sections qui vous permettront de maîtriser HTML5 de manière progressive :

#### 1. **Fondamentaux HTML**
Vous apprendrez la structure de base d'un document HTML5, les métadonnées essentielles, l'encodage des caractères, et comment valider votre code.

#### 2. **Éléments structurants**
Découvrez les balises qui organisent votre contenu : titres, paragraphes, listes, liens, et les nouveaux éléments sémantiques HTML5 qui donnent du sens à votre structure.

#### 3. **Contenu multimédia**
Apprenez à intégrer et optimiser images, vidéos et sons dans vos pages web de manière moderne et performante.

#### 4. **Formulaires HTML5**
Maîtrisez la création de formulaires interactifs avec les nouveaux types de champs et la validation native, essentiels pour toute interaction utilisateur.

#### 5. **Tableaux**
Comprenez comment créer des tableaux de données accessibles et bien structurés, utiles pour présenter des informations tabulaires.

### Approche pédagogique

Dans tout ce chapitre, nous privilégions :

- **Les standards modernes** : vous apprendrez les meilleures pratiques actuelles
- **L'accessibilité** : chaque technique sera enseignée en pensant à tous les utilisateurs
- **La sémantique** : utiliser les bonnes balises au bon moment
- **La progressivité** : chaque concept s'appuie sur les précédents

### HTML en contexte

Rappelez-vous que HTML ne fonctionne jamais seul dans le développement web moderne :

```
HTML  → Structure et contenu (le squelette)
CSS   → Présentation et style (l'apparence)
JavaScript → Comportement et interactivité (la vie)
```

Pour l'instant, concentrez-vous sur HTML : c'est la fondation solide sur laquelle tout le reste reposera. Plus votre HTML sera bien structuré et sémantique, plus il sera facile d'ajouter du style avec CSS et de l'interactivité avec JavaScript.

### Conseils pour réussir

1. **Pratiquez régulièrement** : HTML s'apprend en l'écrivant, pas juste en le lisant
2. **Inspectez des sites web** : utilisez les outils de développement de votre navigateur (F12) pour voir comment les sites professionnels sont structurés
3. **Respectez la sémantique** : prenez le temps de choisir la bonne balise, même si plusieurs semblent fonctionner
4. **Validez votre code** : utilisez les validateurs en ligne pour vérifier que votre HTML est correct
5. **Pensez accessibilité** : dès le début, prenez les bonnes habitudes pour créer un web inclusif

### Ressources et outils

Tout au long de ce chapitre, vous utiliserez :

- **Votre éditeur de code** : Visual Studio Code (configuré dans le chapitre 2)
- **Un navigateur moderne** : Chrome, Firefox, Edge ou Safari
- **Les DevTools** : les outils de développement intégrés à votre navigateur
- **Le validateur W3C** : pour vérifier la conformité de votre code

### Prêt à commencer ?

HTML5 est un langage accessible et logique. Avec de la pratique et de la patience, vous serez bientôt capable de créer des pages web bien structurées et professionnelles. Chaque section de ce chapitre vous rapprochera de cet objectif.

N'oubliez pas : **tous les développeurs web, même les plus expérimentés, ont commencé exactement là où vous êtes maintenant**. La différence ? Ils ont persévéré et pratiqué régulièrement.

Alors, prêt à construire votre première page HTML5 ? Passons aux fondamentaux !

---

**Prochaine section** : 3.1 Fondamentaux HTML

⏭️ [Fondamentaux HTML](/03-html5-structure-et-semantique/01-fondamentaux-html/README.md)
