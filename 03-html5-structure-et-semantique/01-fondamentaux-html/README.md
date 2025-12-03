🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.1 Fondamentaux HTML

## Introduction

Bienvenue dans la section **Fondamentaux HTML** ! C'est ici que commence véritablement votre apprentissage du développement web. Cette section va vous enseigner les **bases essentielles** que vous utiliserez dans chaque page web que vous créerez.

Si HTML est le langage du web, alors cette section vous apprend son **alphabet et sa grammaire**. Sans ces fondamentaux, impossible d'aller plus loin !

## Qu'allez-vous apprendre ?

Cette section couvre **quatre piliers fondamentaux** :

### 1. La structure d'un document HTML5
Vous découvrirez le "squelette" de base que doit contenir **chaque page web** : le DOCTYPE, les balises `<html>`, `<head>`, et `<body>`. C'est comme apprendre la structure d'une lettre avant d'écrire son contenu.

### 2. Le DOCTYPE et les métadonnées
Vous comprendrez l'importance de ces éléments "invisibles" qui se trouvent dans le `<head>` : le titre de la page, la description pour les moteurs de recherche, le favicon, et tous ces petits détails qui font qu'un site est professionnel.

### 3. L'encodage UTF-8 et l'attribut lang
Vous apprendrez à gérer correctement les caractères spéciaux (accents, emojis, symboles) et à indiquer la langue de votre contenu pour l'accessibilité et le référencement.

### 4. La validation et l'inspection
Vous maîtriserez les outils pour vérifier que votre code est correct : le validateur W3C et les DevTools du navigateur. Ce sont vos compagnons de route au quotidien !

## Pourquoi ces fondamentaux sont-ils si importants ?

### Une base solide pour tout le reste

Imaginez que vous apprenez à construire une maison. Avant de parler de décoration, de peinture ou de meubles, il faut d'abord apprendre à poser des fondations solides. C'est exactement le rôle de cette section.

**Sans ces fondamentaux :**
- Vos pages peuvent s'afficher de manière imprévisible
- Les moteurs de recherche auront du mal à indexer votre contenu
- Les personnes utilisant des technologies d'assistance auront des difficultés
- Votre code sera difficile à maintenir et à déboguer

**Avec ces fondamentaux :**
- Vos pages fonctionnent de manière fiable dans tous les navigateurs
- Votre site est bien référencé sur Google
- Votre contenu est accessible à tous
- Votre code est professionnel et maintenable

### Des compétences que vous utiliserez toujours

Même les développeurs avec 10 ans d'expérience utilisent ces fondamentaux **tous les jours**. Ce ne sont pas des notions théoriques que vous oublierez : ce sont des **réflexes** que vous devez acquérir.

Chaque fois que vous créerez une nouvelle page web, vous :
1. Commencerez par la structure de base (DOCTYPE, html, head, body)
2. Ajouterez les métadonnées appropriées
3. Définirez l'encodage et la langue
4. Validerez votre code

**C'est le workflow de base de tout développeur web.**

## Ce qui rend cette section spéciale

### Une approche moderne

Cette section est basée sur **HTML5**, la version actuelle et moderne du langage. Vous n'apprendrez pas de techniques obsolètes : tout ce qui est enseigné ici est utilisé dans le développement web professionnel d'aujourd'hui.

### Focus sur les standards

Vous apprendrez à écrire du code qui **respecte les standards du W3C**. Cela signifie :
- Code valide et sans erreurs
- Compatibilité maximale entre navigateurs
- Respect des meilleures pratiques
- Code compréhensible par tous les développeurs

### Accessibilité dès le début

L'accessibilité n'est pas une option à ajouter "plus tard". Elle commence dès les fondamentaux :
- L'attribut `lang` pour les lecteurs d'écran
- L'encodage UTF-8 pour tous les caractères
- Une structure sémantique correcte
- Des métadonnées complètes

En apprenant les bonnes pratiques dès maintenant, vous créerez naturellement des sites accessibles.

## Comment aborder cette section ?

### 1. Suivez l'ordre des leçons

Les quatre sous-sections sont organisées dans un **ordre logique** :
- Chaque leçon s'appuie sur la précédente
- Les concepts deviennent progressivement plus avancés
- Tout est conçu pour une courbe d'apprentissage douce

**Conseil :** Ne sautez pas d'étapes, même si certains concepts vous semblent simples. Les détails sont importants.

### 2. Pratiquez au fur et à mesure

La théorie seule ne suffit pas. Pour chaque nouveau concept :
1. **Lisez** la section attentivement
2. **Testez** le code dans votre éditeur
3. **Observez** le résultat dans le navigateur
4. **Expérimentez** avec des variations
5. **Validez** votre code

**Important :** Créez vos propres fichiers HTML pendant que vous apprenez. La lecture passive ne suffit pas !

### 3. Utilisez vos outils

Vous aurez besoin de :
- **Visual Studio Code** (ou votre éditeur préféré)
- **Un navigateur moderne** (Chrome, Firefox, Edge, ou Safari)
- **Les DevTools** (intégrés au navigateur)
- **Une connexion Internet** (pour accéder au validateur W3C)

Si vous n'avez pas encore configuré votre environnement, retournez au **Chapitre 2 : Environnement de Développement**.

### 4. Ne cherchez pas la perfection immédiate

**C'est normal de faire des erreurs !** Tous les développeurs en font :
- Oublier de fermer une balise
- Mal orthographier un attribut
- Placer quelque chose au mauvais endroit

L'important est d'apprendre à :
- **Identifier** les erreurs (avec le validateur)
- **Comprendre** pourquoi c'est une erreur
- **Corriger** le problème
- **Ne pas refaire** la même erreur

Les erreurs font partie de l'apprentissage. Le validateur et les DevTools sont là pour vous aider, pas pour vous juger !

### 5. Prenez des notes

Gardez un document (papier ou numérique) où vous notez :
- Les concepts clés
- Les pièges à éviter
- Les raccourcis utiles
- Les questions que vous vous posez

Cela vous aidera à mémoriser et à revenir sur les points importants.

## La structure de base : un exemple

Avant de plonger dans les détails, voici un aperçu de ce que vous saurez créer après cette section :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Une description claire de ma page">
    <title>Ma première page HTML5 professionnelle</title>
    <link rel="icon" type="image/png" href="favicon.png">
</head>
<body>
    <!-- Votre contenu visible ici -->
    <h1>Bienvenue !</h1>
    <p>Voici ma première page HTML5 bien structurée.</p>
</body>
</html>
```

**Ce simple bout de code contient :**
- Une déclaration DOCTYPE HTML5
- Un attribut de langue pour l'accessibilité
- Un encodage UTF-8 pour tous les caractères
- Une configuration responsive pour les mobiles
- Des métadonnées pour le référencement
- Un titre unique et descriptif
- Un favicon pour l'identité visuelle
- Une structure body prête à recevoir du contenu

**À la fin de cette section, vous comprendrez chaque ligne de ce code** et saurez pourquoi chaque élément est important.

## Objectifs d'apprentissage

Après avoir terminé cette section, vous serez capable de :

- ✅ **Créer** la structure de base d'un document HTML5 valide de mémoire
- ✅ **Expliquer** le rôle de chaque élément (DOCTYPE, html, head, body)
- ✅ **Utiliser** correctement les métadonnées essentielles
- ✅ **Configurer** l'encodage UTF-8 et l'attribut lang
- ✅ **Valider** votre code HTML avec le validateur W3C
- ✅ **Inspecter** votre code avec les DevTools du navigateur
- ✅ **Identifier** et corriger les erreurs courantes
- ✅ **Comprendre** l'importance de ces fondamentaux pour la suite

## Le mindset du développeur web

Au-delà des connaissances techniques, cette section vous inculque un **état d'esprit** :

### 1. La rigueur
Le HTML est un langage de balisage précis. Une balise oubliée, un attribut mal orthographié, et le résultat peut être imprévisible. Apprenez à être **attentif aux détails**.

### 2. La validation systématique
Les développeurs professionnels valident leur code régulièrement. Ce n'est pas de la perfectionnisme, c'est de la **prévention**. Un bug détecté tôt est un bug facile à corriger.

### 3. La curiosité
Les DevTools sont une fenêtre sur le fonctionnement interne du web. Prenez l'habitude d'**inspecter les sites** que vous visitez pour voir comment ils sont construits.

### 4. L'apprentissage continu
Le web évolue. HTML5 est stable, mais de nouvelles fonctionnalités apparaissent. Restez **curieux** et continuez à apprendre même après cette formation.

### 5. Le respect des standards
Les standards existent pour une bonne raison : garantir que le web fonctionne pour tout le monde, partout. **Respecter les standards** n'est pas une contrainte, c'est une responsabilité.

## Connexion avec le reste du cours

Cette section **Fondamentaux HTML** est la première d'un parcours complet :

**Maintenant (Section 3.1) :** Fondamentaux
- La structure de base
- Les métadonnées
- La validation

**Ensuite (Section 3.2) :** Éléments structurants
- Titres et paragraphes
- Listes et liens
- Éléments sémantiques HTML5

**Puis (Sections 3.3 à 3.5) :** Contenu riche
- Images et multimédia
- Formulaires interactifs
- Tableaux de données

**Enfin (Chapitre 4) :** CSS pour la présentation
- Styles et couleurs
- Mise en page moderne
- Responsive design

Chaque étape s'appuie sur la précédente. Les fondamentaux que vous apprenez maintenant sont la **base de tout le reste**.

## Prêt à commencer ?

Vous avez maintenant une vue d'ensemble de ce qui vous attend dans cette section. Ne vous inquiétez pas si tout semble nouveau : c'est le but d'une formation !

**Rappelez-vous :**
- Allez à votre rythme
- Pratiquez régulièrement
- N'hésitez pas à relire si nécessaire
- Validez votre code systématiquement
- Les erreurs sont normales et utiles

Le HTML n'est pas difficile, il est **logique**. Avec un peu de pratique et de patience, tout deviendra naturel.

### Quelques encouragements

> "Tout expert a d'abord été un débutant."

Chaque développeur web professionnel que vous admirez a commencé exactement là où vous êtes maintenant. La seule différence ? Ils ont **persévéré** et **pratiqué**.

Le HTML que vous apprenez aujourd'hui est utilisé par des milliards de pages web. En maîtrisant ces fondamentaux, vous rejoignez la communauté mondiale des créateurs du web.

**C'est parti pour les fondamentaux HTML !**

Dans la première sous-section, nous allons découvrir en détail la structure d'un document HTML5, ligne par ligne, pour que vous compreniez parfaitement chaque élément.

---

**Première sous-section** : [3.1.1 Structure d'un document HTML5](./01-structure-document-html5.md)

## Plan détaillé de la section

1. **[Structure d'un document HTML5](./01-structure-document-html5.md)**
   - Le DOCTYPE
   - Les balises html, head et body
   - La hiérarchie du document
   - Exemples commentés

2. **[Doctype, balises head et métadonnées](./02-doctype-head-et-metadonnees.md)**
   - Le DOCTYPE en profondeur
   - Les métadonnées essentielles (charset, viewport, title)
   - Les métadonnées SEO (description, keywords)
   - Open Graph et réseaux sociaux

3. **[Encodage UTF-8 et attribut lang](./03-encodage-utf8-et-attribut-lang.md)**
   - Comprendre l'encodage des caractères
   - Pourquoi UTF-8 est le standard
   - L'attribut lang pour l'accessibilité
   - Gérer le contenu multilingue

4. **[Validation HTML et inspection avec DevTools](./04-validation-html-et-devtools.md)**
   - Le validateur W3C
   - Comprendre les erreurs courantes
   - Maîtriser les DevTools
   - Workflow de validation professionnel

⏭️ [Structure d'un document HTML5](/03-html5-structure-et-semantique/01-fondamentaux-html/01-structure-document-html5.md)
