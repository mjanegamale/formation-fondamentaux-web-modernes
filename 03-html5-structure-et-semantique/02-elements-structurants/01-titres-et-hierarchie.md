🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2.1 Titres (h1-h6) et hiérarchie sémantique

## Introduction

Les titres sont les **panneaux indicateurs** de votre page web. Tout comme un livre a un titre principal, des chapitres, des sections et des sous-sections, votre page web doit avoir une structure hiérarchique claire grâce aux balises de titre.

HTML propose **six niveaux de titres** : de `<h1>` (le plus important) à `<h6>` (le moins important). Ces balises ne servent pas seulement à rendre le texte plus gros, elles indiquent l'**importance et l'organisation** de votre contenu.

**Pourquoi c'est crucial ?**
- **Pour vos visiteurs** : ils peuvent scanner rapidement votre page
- **Pour l'accessibilité** : les lecteurs d'écran utilisent les titres pour naviguer
- **Pour le SEO** : Google utilise les titres pour comprendre votre contenu
- **Pour la structure** : votre code est plus lisible et maintenable

## Les six niveaux de titres

### Présentation des balises

HTML propose six balises de titre, de la plus importante à la moins importante :

```html
<h1>Titre de niveau 1 - Le plus important</h1>
<h2>Titre de niveau 2</h2>
<h3>Titre de niveau 3</h3>
<h4>Titre de niveau 4</h4>
<h5>Titre de niveau 5</h5>
<h6>Titre de niveau 6 - Le moins important</h6>
```

### Rendu visuel par défaut

Par défaut, les navigateurs affichent les titres avec des tailles décroissantes :

- **`<h1>`** : Très grand (environ 2em ou 32px)
- **`<h2>`** : Grand (environ 1.5em ou 24px)
- **`<h3>`** : Moyen-grand (environ 1.17em ou 18.72px)
- **`<h4>`** : Normal (environ 1em ou 16px)
- **`<h5>`** : Petit (environ 0.83em ou 13.28px)
- **`<h6>`** : Très petit (environ 0.67em ou 10.72px)

**Important :** Ne choisissez JAMAIS un niveau de titre en fonction de sa taille visuelle ! La taille peut être modifiée avec CSS. Choisissez toujours en fonction de l'**importance sémantique** du contenu.

### Le "h" signifie "heading" (en-tête)

Le "h" dans `<h1>`, `<h2>`, etc. vient de l'anglais "heading" qui signifie "en-tête" ou "titre". Le chiffre indique le niveau d'importance dans la hiérarchie.

## La hiérarchie sémantique

### Qu'est-ce que la sémantique ?

La **sémantique** en HTML, c'est l'idée que chaque balise a un **sens**, une **signification**. Les balises de titre ne disent pas "affiche ce texte en gros", elles disent "ceci est un titre de niveau X d'importance".

**Analogie avec un livre :**

```
📖 Titre du livre           → <h1>
   📑 Chapitre 1            → <h2>
      📄 Section 1.1        → <h3>
         📋 Sous-section    → <h4>
   📑 Chapitre 2            → <h2>
      📄 Section 2.1        → <h3>
      📄 Section 2.2        → <h3>
```

Chaque niveau est imbriqué dans le niveau supérieur, créant une **structure logique**.

### La règle d'or : respecter la hiérarchie

**Règle fondamentale :** Les niveaux de titre doivent suivre un ordre logique, sans sauter de niveaux.

✅ **Bon exemple - Hiérarchie respectée :**
```html
<h1>Mon blog de cuisine</h1>
    <h2>Recettes sucrées</h2>
        <h3>Gâteaux</h3>
            <h4>Gâteau au chocolat</h4>
        <h3>Tartes</h3>
            <h4>Tarte aux pommes</h4>
    <h2>Recettes salées</h2>
        <h3>Plats principaux</h3>
```

❌ **Mauvais exemple - Hiérarchie cassée :**
```html
<h1>Mon blog de cuisine</h1>
    <h4>Recettes sucrées</h4>  <!-- ❌ On saute h2 et h3 ! -->
        <h2>Gâteaux</h2>       <!-- ❌ On revient en arrière ! -->
```

### Pourquoi c'est important ?

#### 1. Pour l'accessibilité

Les utilisateurs de **lecteurs d'écran** (personnes aveugles ou malvoyantes) naviguent souvent de titre en titre pour comprendre la structure de la page :
- Ils peuvent sauter directement à la section qui les intéresse
- Ils comprennent l'organisation du contenu
- Ils peuvent revenir en arrière dans la hiérarchie

Si vous sautez des niveaux, la navigation devient confuse et frustrante.

#### 2. Pour le référencement (SEO)

Google et les autres moteurs de recherche utilisent les titres pour :
- **Comprendre la structure** de votre page
- **Identifier les sujets principaux** (surtout le h1)
- **Évaluer la pertinence** du contenu
- **Créer des "featured snippets"** dans les résultats de recherche

Une bonne hiérarchie = meilleur référencement.

#### 3. Pour la maintenabilité

Un code avec une hiérarchie claire est plus facile à :
- Lire et comprendre
- Modifier et mettre à jour
- Déboguer en cas de problème

## Le titre H1 : le plus important

### Règle du H1 unique

**Règle importante :** Il ne doit y avoir **qu'un seul `<h1>` par page**.

Le `<h1>` est le **titre principal** de votre page. C'est comme le titre d'un livre ou d'un article : il résume le sujet principal.

✅ **Bon - Un seul H1 :**
```html
<body>
    <h1>Les bienfaits du sport sur la santé</h1>
    <p>Introduction...</p>

    <h2>Bienfaits physiques</h2>
    <p>Contenu...</p>

    <h2>Bienfaits mentaux</h2>
    <p>Contenu...</p>
</body>
```

❌ **Mauvais - Plusieurs H1 :**
```html
<body>
    <h1>Les bienfaits du sport</h1>
    <p>Introduction...</p>

    <h1>Bienfaits physiques</h1>  <!-- ❌ Deuxième H1 ! -->
    <p>Contenu...</p>
</body>
```

**Exception moderne :** Techniquement, HTML5 permet plusieurs `<h1>` dans différentes sections (avec `<article>`, `<section>`), mais en pratique, la plupart des développeurs et experts SEO recommandent toujours **un seul H1** par page pour éviter toute confusion.

### Que mettre dans le H1 ?

Le `<h1>` doit être :

**Descriptif et clair**
```html
✅ <h1>Comment créer son premier site web</h1>
❌ <h1>Bienvenue</h1>  <!-- Trop vague -->
```

**Unique pour chaque page**
```html
<!-- Page d'accueil -->
<h1>Agence Web Créative - Solutions digitales sur mesure</h1>

<!-- Page Services -->
<h1>Nos services de développement web</h1>

<!-- Page Contact -->
<h1>Contactez notre équipe</h1>
```

**Contenant des mots-clés pertinents** (pour le SEO)
```html
✅ <h1>Formation HTML5 et CSS3 pour débutants</h1>
❌ <h1>Notre formation</h1>  <!-- Pas assez spécifique -->
```

**Court et percutant** (50-60 caractères idéalement)
```html
✅ <h1>Recettes végétariennes faciles et rapides</h1>
❌ <h1>Découvrez toutes nos meilleures recettes végétariennes qui sont à la fois très faciles à réaliser et également très rapides à préparer</h1>  <!-- Trop long -->
```

### H1 vs Title : quelle différence ?

Beaucoup de débutants confondent le `<h1>` et le `<title>`. Voici la différence :

**`<title>`** (dans le `<head>`)
- Apparaît dans **l'onglet du navigateur**
- Apparaît dans les **résultats de recherche Google**
- Apparaît dans les **favoris**
- **N'est pas visible** dans le contenu de la page

**`<h1>`** (dans le `<body>`)
- Apparaît **dans le contenu visible** de la page
- Premier titre que l'utilisateur voit
- **Est visible** sur la page elle-même

**Exemple complet :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Recette de cookies - Blog Cuisine Facile</title>
    <!-- ↑ Apparaît dans l'onglet et Google -->
</head>
<body>
    <h1>Recette facile de cookies au chocolat</h1>
    <!-- ↑ Apparaît sur la page -->

    <p>Ces délicieux cookies sont prêts en 20 minutes...</p>
</body>
</html>
```

**Conseil :** Le `<title>` et le `<h1>` peuvent être similaires, mais pas nécessairement identiques. Le title peut être plus optimisé pour le SEO, tandis que le H1 est plus orienté vers l'utilisateur.

## Les titres H2 à H6

### H2 : Les sections principales

Le `<h2>` représente les **grandes sections** de votre page. Ce sont les chapitres de votre contenu.

```html
<h1>Guide complet du jardinage</h1>

<h2>Préparer son jardin</h2>
<p>Contenu sur la préparation...</p>

<h2>Choisir ses plantes</h2>
<p>Contenu sur le choix des plantes...</p>

<h2>Entretenir son jardin</h2>
<p>Contenu sur l'entretien...</p>
```

**Utilisation :** Vous pouvez avoir **plusieurs H2** sur une page. C'est normal et recommandé pour structurer votre contenu.

### H3 : Les sous-sections

Le `<h3>` divise les sections H2 en **sous-parties**.

```html
<h2>Choisir ses plantes</h2>

    <h3>Plantes pour débutants</h3>
    <p>Liste et conseils...</p>

    <h3>Plantes selon la saison</h3>
    <p>Calendrier de plantation...</p>

    <h3>Plantes d'intérieur vs extérieur</h3>
    <p>Différences et spécificités...</p>
```

### H4 à H6 : Les détails

Les niveaux `<h4>`, `<h5>` et `<h6>` sont pour des subdivisions encore plus fines. En pratique :

- **H4** : Assez courant pour des sous-sous-sections
- **H5** : Rare, mais utile dans de longs documents
- **H6** : Très rare, sauf dans des documentations très détaillées

```html
<h2>Choisir ses plantes</h2>
    <h3>Plantes pour débutants</h3>
        <h4>Plantes résistantes</h4>
            <h5>Cactus</h5>
                <h6>Espèces recommandées</h6>
                <p>Détails sur chaque espèce...</p>
```

**Conseil pratique :** La plupart des pages web utilisent principalement H1, H2, et H3. Il est rare d'avoir besoin d'aller jusqu'à H6, sauf pour des contenus très longs et complexes.

## Exemples pratiques

### Exemple 1 : Blog article

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>10 astuces pour améliorer son référencement</title>
</head>
<body>
    <h1>10 astuces pour améliorer son référencement naturel</h1>

    <p>Introduction au SEO et pourquoi c'est important...</p>

    <h2>1. Optimiser les balises de titre</h2>
    <p>Explication et conseils...</p>

    <h2>2. Créer du contenu de qualité</h2>
    <p>L'importance du contenu...</p>

        <h3>Qu'est-ce qu'un contenu de qualité ?</h3>
        <p>Définition et critères...</p>

        <h3>Fréquence de publication</h3>
        <p>À quelle fréquence publier...</p>

    <h2>3. Améliorer la vitesse de chargement</h2>
    <p>Techniques d'optimisation...</p>

    <!-- ... autres astuces ... -->
</body>
</html>
```

### Exemple 2 : Page d'accueil d'entreprise

```html
<body>
    <h1>Agence Web Innovante - Création de sites sur mesure</h1>

    <h2>Nos services</h2>
    <p>Nous proposons une gamme complète de services...</p>

        <h3>Création de sites web</h3>
        <p>Sites vitrines, e-commerce, applications web...</p>

        <h3>Référencement SEO</h3>
        <p>Optimisation pour les moteurs de recherche...</p>

        <h3>Maintenance et support</h3>
        <p>Assistance technique continue...</p>

    <h2>Notre approche</h2>
    <p>Méthodologie et processus de travail...</p>

        <h3>Phase de découverte</h3>
        <p>Analyse de vos besoins...</p>

        <h3>Conception et développement</h3>
        <p>Création de votre solution...</p>

        <h3>Lancement et suivi</h3>
        <p>Mise en ligne et accompagnement...</p>

    <h2>Nous contacter</h2>
    <p>Informations de contact...</p>
</body>
```

### Exemple 3 : Page produit e-commerce

```html
<body>
    <h1>iPhone 15 Pro - 256 Go - Titane Naturel</h1>

    <h2>Caractéristiques principales</h2>
    <ul>
        <li>Puce A17 Pro</li>
        <li>Écran Super Retina XDR 6,1 pouces</li>
        <li>Triple caméra 48 Mpx</li>
    </ul>

    <h2>Description détaillée</h2>

        <h3>Design et construction</h3>
        <p>Cadre en titane de qualité aérospatiale...</p>

        <h3>Performance</h3>
        <p>Le processeur A17 Pro offre...</p>

            <h4>Gaming</h4>
            <p>Des jeux console directement sur iPhone...</p>

            <h4>Photographie computationnelle</h4>
            <p>Traitement d'image ultra-rapide...</p>

        <h3>Autonomie</h3>
        <p>Jusqu'à 23 heures de lecture vidéo...</p>

    <h2>Contenu de la boîte</h2>
    <ul>
        <li>iPhone 15 Pro</li>
        <li>Câble USB-C</li>
        <li>Documentation</li>
    </ul>

    <h2>Avis clients</h2>
    <p>Note moyenne : 4.5/5...</p>
</body>
```

### Exemple 4 : Documentation technique

```html
<body>
    <h1>Guide d'utilisation de l'API</h1>

    <h2>Introduction</h2>
    <p>Cette API permet de...</p>

    <h2>Authentification</h2>

        <h3>Obtenir une clé API</h3>
        <p>Pour obtenir votre clé...</p>

        <h3>Utiliser la clé dans les requêtes</h3>
        <p>Ajoutez votre clé dans l'en-tête...</p>

    <h2>Endpoints disponibles</h2>

        <h3>GET /users</h3>
        <p>Récupère la liste des utilisateurs</p>

            <h4>Paramètres</h4>
            <p>Liste des paramètres acceptés...</p>

            <h4>Réponse</h4>
            <p>Format de la réponse JSON...</p>

            <h4>Codes d'erreur</h4>
            <p>200: Succès, 401: Non autorisé...</p>

        <h3>POST /users</h3>
        <p>Crée un nouvel utilisateur</p>
</body>
```

## Erreurs courantes à éviter

### Erreur 1 : Utiliser les titres pour le style

❌ **Mauvais :**
```html
<h3>Bienvenue sur mon site</h3>
<!-- Utilisé juste parce que h3 a la bonne taille -->
```

✅ **Bon :**
```html
<h1>Bienvenue sur mon site</h1>
<!-- Utilisé parce que c'est le titre principal -->
```

**Solution :** Utilisez CSS pour changer la taille, pas un mauvais niveau de titre.

### Erreur 2 : Sauter des niveaux

❌ **Mauvais :**
```html
<h1>Titre principal</h1>
<h4>Sous-titre</h4>  <!-- On saute h2 et h3 ! -->
```

✅ **Bon :**
```html
<h1>Titre principal</h1>
<h2>Sous-titre</h2>
```

### Erreur 3 : Plusieurs H1

❌ **Mauvais :**
```html
<h1>Mon site web</h1>
<h1>Section 1</h1>
<h1>Section 2</h1>
```

✅ **Bon :**
```html
<h1>Mon site web</h1>
<h2>Section 1</h2>
<h2>Section 2</h2>
```

### Erreur 4 : H1 vide ou non descriptif

❌ **Mauvais :**
```html
<h1>Bienvenue</h1>
<h1>Page d'accueil</h1>
<h1>&nbsp;</h1>  <!-- Vide ! -->
```

✅ **Bon :**
```html
<h1>Boulangerie Dupont - Pain artisanal à Lyon</h1>
```

### Erreur 5 : Utiliser des balises non-sémantiques

❌ **Mauvais :**
```html
<div style="font-size: 24px; font-weight: bold;">Mon titre</div>
<!-- Ce n'est pas un vrai titre sémantique ! -->
```

✅ **Bon :**
```html
<h2>Mon titre</h2>
<!-- Utilisez les vraies balises de titre -->
```

### Erreur 6 : Ordre illogique

❌ **Mauvais :**
```html
<h2>Introduction</h2>
<h1>Mon article</h1>  <!-- Le H1 devrait être en premier ! -->
```

✅ **Bon :**
```html
<h1>Mon article</h1>
<h2>Introduction</h2>
```

## Titres et accessibilité

### Navigation par titres

Les utilisateurs de lecteurs d'écran peuvent :
- **Lister tous les titres** pour avoir une vue d'ensemble
- **Sauter de titre en titre** pour naviguer rapidement
- **Comprendre la structure** sans lire tout le contenu

**Pour tester :**
1. Ouvrez les DevTools (F12)
2. Allez dans l'onglet "Accessibility" (Accessibilité)
3. Regardez l'arbre d'accessibilité de votre page

### Titres descriptifs

Chaque titre doit être **compréhensible hors contexte**.

❌ **Mauvais (pas assez descriptif) :**
```html
<h2>Introduction</h2>
<h2>Suite</h2>
<h2>Plus d'infos</h2>
```

✅ **Bon (descriptif et clair) :**
```html
<h2>Introduction au HTML</h2>
<h2>Les balises de titre en détail</h2>
<h2>Ressources et documentation supplémentaires</h2>
```

### Ordre logique de lecture

Le lecteur d'écran lit la page dans l'ordre du code HTML. Assurez-vous que l'ordre des titres est logique :

```html
<!-- Ordre logique -->
<h1>Article principal</h1>
<h2>Première partie</h2>
<h3>Sous-section A</h3>
<h3>Sous-section B</h3>
<h2>Deuxième partie</h2>
```

## Titres et SEO

### Google et les titres

Google utilise les titres pour :

1. **Comprendre le sujet** de la page (surtout le H1)
2. **Identifier les sections importantes**
3. **Créer des liens directs** vers les sections (featured snippets)
4. **Évaluer la qualité** du contenu (structure claire = bon signal)

### Optimisation SEO des titres

**Incluez des mots-clés pertinents**
```html
<h1>Formation HTML CSS JavaScript pour débutants</h1>
<!-- Contient les mots-clés "HTML", "CSS", "JavaScript", "débutants" -->
```

**Soyez descriptif et naturel**
```html
✅ <h2>Comment créer un formulaire de contact en HTML</h2>
❌ <h2>Formulaire contact HTML créer code exemple</h2>
<!-- Ne faites pas du bourrage de mots-clés ! -->
```

**Utilisez une structure logique**
- H1 = Sujet principal de la page
- H2 = Sections principales (sous-sujets)
- H3 = Détails sur les sections

### Les Featured Snippets de Google

Google peut afficher vos titres dans des encadrés spéciaux au-dessus des résultats de recherche. Pour maximiser vos chances :

```html
<h1>Guide complet du SEO en 2025</h1>

<h2>Qu'est-ce que le SEO ?</h2>
<p>Le SEO (Search Engine Optimization)...</p>

<h2>Comment fonctionne le SEO ?</h2>
<p>Les moteurs de recherche utilisent...</p>

<h2>Combien coûte le SEO ?</h2>
<p>Le coût du SEO varie selon...</p>
```

Les titres formulés en questions (Quoi, Comment, Pourquoi, Combien...) ont plus de chances d'apparaître en featured snippets.

## Bonnes pratiques récapitulatives

### Les commandements des titres HTML

1. ✅ **Un seul H1 par page** (le titre principal)
2. ✅ **Respecter la hiérarchie** (ne pas sauter de niveaux)
3. ✅ **Être descriptif** (pas de "Bienvenue" ou "Introduction" vagues)
4. ✅ **Utiliser pour la structure**, pas pour le style
5. ✅ **Inclure des mots-clés** (naturellement)
6. ✅ **Rendre accessibles** (compréhensibles hors contexte)
7. ✅ **Suivre un ordre logique** (de haut en bas)

### Checklist avant publication

Avant de publier votre page, vérifiez :

- [ ] J'ai un unique `<h1>` qui décrit bien ma page
- [ ] Mes titres suivent une hiérarchie logique (h1 → h2 → h3...)
- [ ] Je n'ai pas sauté de niveaux
- [ ] Chaque titre est descriptif et clair
- [ ] J'ai utilisé les titres pour la structure, pas pour le style
- [ ] Mes titres contiennent des mots-clés pertinents
- [ ] L'ordre de mes titres est logique
- [ ] Je peux comprendre la structure de ma page juste en lisant les titres

## Visualiser votre structure de titres

### Avec les DevTools

**Méthode 1 : Inspecteur**
1. Ouvrez les DevTools (F12)
2. Recherchez les balises h1, h2, h3... dans l'arbre HTML
3. Vérifiez visuellement la hiérarchie

**Méthode 2 : Console**
Collez ce code dans la console pour lister tous les titres :

```javascript
document.querySelectorAll('h1, h2, h3, h4, h5, h6').forEach(h => {
    console.log(h.tagName + ': ' + h.textContent);
});
```

**Résultat exemple :**
```
H1: Mon blog de cuisine
H2: Recettes sucrées
H3: Gâteaux
H3: Tartes
H2: Recettes salées
H3: Plats principaux
```

### Extensions navigateur utiles

- **HeadingsMap** (Firefox/Chrome) : Affiche l'arbre des titres
- **Web Developer** : Diverses fonctionnalités, dont l'affichage de la structure
- **WAVE** : Outil d'accessibilité qui vérifie les titres

## Exemple complet et commenté

Voici un exemple complet de page bien structurée :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Apprendre la photographie - Guide complet pour débutants</title>
</head>
<body>
    <!-- Titre principal unique de la page -->
    <h1>Guide complet de la photographie pour débutants</h1>

    <p>La photographie est un art accessible à tous. Ce guide vous accompagne dans vos premiers pas.</p>

    <!-- Première section principale -->
    <h2>Choisir son appareil photo</h2>
    <p>Le choix de l'appareil dépend de vos besoins et de votre budget...</p>

        <!-- Sous-section de "Choisir son appareil" -->
        <h3>Appareils pour débutants</h3>
        <p>Pour commencer, un appareil simple est recommandé...</p>

            <!-- Détail de "Appareils pour débutants" -->
            <h4>Smartphones</h4>
            <p>Votre téléphone est déjà un excellent appareil...</p>

            <h4>Appareils compacts</h4>
            <p>Petits et faciles à transporter...</p>

            <h4>Reflex d'entrée de gamme</h4>
            <p>Pour ceux qui veulent aller plus loin...</p>

        <!-- Autre sous-section au même niveau -->
        <h3>Budget à prévoir</h3>
        <p>Les prix varient considérablement...</p>

    <!-- Deuxième section principale -->
    <h2>Maîtriser les bases techniques</h2>
    <p>Trois paramètres fondamentaux contrôlent l'exposition...</p>

        <h3>L'ouverture du diaphragme</h3>
        <p>L'ouverture contrôle la quantité de lumière...</p>

        <h3>La vitesse d'obturation</h3>
        <p>La vitesse détermine le temps d'exposition...</p>

        <h3>La sensibilité ISO</h3>
        <p>L'ISO ajuste la sensibilité du capteur...</p>

    <!-- Troisième section principale -->
    <h2>Composer ses photos</h2>
    <p>La composition est l'art de disposer les éléments...</p>

        <h3>La règle des tiers</h3>
        <p>Divisez l'image en 9 parties égales...</p>

        <h3>Les lignes directrices</h3>
        <p>Utilisez les lignes naturelles pour guider l'œil...</p>

    <!-- Section finale -->
    <h2>Progresser et se former</h2>
    <p>La pratique régulière est essentielle...</p>

        <h3>Exercices quotidiens</h3>
        <p>Photographiez tous les jours, même 5 minutes...</p>

        <h3>Ressources en ligne</h3>
        <p>De nombreux sites proposent des tutoriels gratuits...</p>
</body>
</html>
```

**Points à noter dans cet exemple :**
- ✅ Un seul H1 qui résume le contenu
- ✅ Les H2 représentent les grandes sections
- ✅ Les H3 divisent logiquement les H2
- ✅ Les H4 apportent des précisions sur les H3
- ✅ Pas de saut de niveau
- ✅ Hiérarchie cohérente et logique
- ✅ Chaque titre est descriptif

## Conclusion

Les titres HTML sont bien plus que de simples outils de mise en forme : ils sont la **colonne vertébrale** de votre contenu web. Une bonne hiérarchie de titres :

- **Structure** votre contenu de manière logique
- **Améliore** l'expérience utilisateur (scanabilité)
- **Aide** les technologies d'assistance (accessibilité)
- **Booste** votre référencement (SEO)
- **Facilite** la maintenance de votre code

**Rappelez-vous :**
- H1 = Un seul par page, le plus important
- H2 à H6 = Hiérarchie décroissante, sans sauter de niveaux
- Choisissez selon le sens, pas selon la taille
- Soyez descriptif et cohérent

Prenez l'habitude de **penser structure avant style**. Une fois votre hiérarchie de titres bien définie, vous pourrez facilement les styler avec CSS pour qu'ils correspondent à votre design, tout en gardant une base sémantique solide.

Dans la prochaine section, nous découvrirons les paragraphes et les listes, d'autres éléments essentiels pour organiser votre contenu textuel.

---

**Section suivante** : [3.2.2 Paragraphes et listes](./02-paragraphes-et-listes.md)

⏭️ [Paragraphes et listes (ul, ol, dl)](/03-html5-structure-et-semantique/02-elements-structurants/02-paragraphes-et-listes.md)
