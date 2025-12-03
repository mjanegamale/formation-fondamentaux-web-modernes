🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.5 Tableaux HTML5

## Introduction à la section

Les **tableaux HTML** sont des éléments essentiels pour organiser et présenter des **données tabulaires** de manière structurée et accessible. Un tableau, c'est une grille composée de lignes et de colonnes qui permet d'afficher des informations où chaque cellule a une relation logique avec les autres.

Pensez à un tableau comme une feuille Excel simplifiée : vous avez des en-têtes qui décrivent le contenu des colonnes, et des lignes qui contiennent vos données. Cette structure est parfaite pour présenter des informations qui ont besoin d'être comparées ou analysées côte à côte.

**Exemples de données tabulaires dans la vie quotidienne :**
- Horaires de trains ou d'avions
- Résultats sportifs et classements
- Tableaux de prix et tarifs
- Comparaisons de produits
- Statistiques et données financières
- Emplois du temps scolaires
- Tableaux de bord et rapports
- Calendriers et plannings

Cette section est cruciale car les tableaux sont **omniprésents** sur le web professionnel. Que vous développiez un site e-commerce, une application de gestion, un site d'actualités sportives ou une plateforme analytique, vous rencontrerez des tableaux. Savoir les créer correctement fait partie des compétences de base de tout développeur web.

---

## Pourquoi les tableaux sont essentiels

### 1. Organisation visuelle des données

Les tableaux permettent de présenter des données complexes de manière **claire et structurée**. Sans tableaux, il serait extrêmement difficile de comparer plusieurs produits, de lire un horaire de transport, ou d'analyser des statistiques.

Imaginez devoir présenter les résultats d'un championnat de football avec 20 équipes, leurs points, victoires, défaites, et buts marqués. Sans tableau, ce serait un chaos de paragraphes illisibles. Avec un tableau bien structuré, toutes ces informations deviennent instantanément compréhensibles.

### 2. Accessibilité et inclusion

Les tableaux HTML, lorsqu'ils sont **correctement structurés avec les bonnes balises sémantiques**, sont parfaitement accessibles aux personnes utilisant des lecteurs d'écran. Ces technologies d'assistance peuvent annoncer les en-têtes de colonnes et de lignes, permettant aux personnes malvoyantes de naviguer et comprendre les données exactement comme tout le monde.

C'est là une différence fondamentale avec une simple mise en page visuelle : un tableau sémantique communique la **structure et les relations** entre les données, pas seulement leur apparence.

### 3. Référence et SEO

Les moteurs de recherche comprennent la structure des tableaux HTML et peuvent les indexer intelligemment. Des tableaux bien structurés améliorent votre SEO et peuvent même apparaître comme des "rich snippets" dans les résultats de recherche Google.

De plus, les utilisateurs peuvent copier-coller des tableaux HTML directement dans Excel ou Google Sheets, ce qui est extrêmement pratique pour l'analyse de données.

### 4. Maintenance et évolutivité

Un tableau HTML bien codé est facile à maintenir et à mettre à jour. Ajouter une ligne, modifier des données, ou changer le style devient simple car la structure est claire et logique. À l'inverse, des données présentées avec des divs et du CSS complexe deviennent rapidement ingérables.

---

## L'évolution des tableaux HTML

### Avant HTML5 : L'ère sombre des tableaux de mise en page

Dans les années 1990 et début 2000, avant que CSS ne soit largement supporté, les développeurs utilisaient des **tableaux pour créer la mise en page** des sites web. C'était la norme à l'époque : menu à gauche dans une cellule, contenu principal au centre, sidebar à droite.

**Exemple de l'ancienne méthode (à ne JAMAIS faire aujourd'hui) :**
```html
<!-- ❌ TRÈS MAUVAIS : Tableau pour la mise en page -->
<table>
    <tr>
        <td>Menu</td>
        <td>Contenu principal</td>
        <td>Publicités</td>
    </tr>
</table>
```

**Pourquoi c'était problématique :**
- Non sémantique : ce ne sont pas des données tabulaires
- Terrible pour l'accessibilité : les lecteurs d'écran annonçaient des "tableaux" partout
- Non responsive : impossible à adapter aux mobiles
- Difficile à maintenir : modifier la mise en page nécessitait de toucher au HTML
- Mauvais pour le SEO : structure confuse pour les moteurs de recherche
- Code lourd et complexe avec des tableaux imbriqués

Cette pratique a causé des années de mauvaises habitudes et a donné une mauvaise réputation aux tableaux en général.

### HTML5 et les bonnes pratiques modernes

Aujourd'hui, la règle est simple et claire : **les tableaux sont pour les données tabulaires, point final.**

Pour la mise en page, nous utilisons CSS avec Flexbox ou Grid. Pour les tableaux, nous utilisons les balises HTML appropriées avec une structure sémantique forte.

**HTML5 a apporté :**
- Une meilleure compréhension de la sémantique : quand utiliser des tableaux (données) vs. quand ne pas les utiliser (mise en page)
- Des attributs et balises clairement définis pour l'accessibilité
- Une structure standardisée avec `<thead>`, `<tbody>`, `<tfoot>`
- L'attribut `scope` pour clarifier les relations en-têtes/données
- Des recommandations claires du W3C sur les bonnes pratiques

**La révolution des mentalités :**
Le passage de "tableaux pour tout" à "tableaux uniquement pour les données" a été l'une des évolutions les plus importantes du développement web moderne. Cela a considérablement amélioré l'accessibilité, la maintenabilité et la qualité du web.

---

## Vue d'ensemble des chapitres

Cette section est structurée en plusieurs chapitres progressifs qui vous permettront de maîtriser complètement les tableaux HTML5, des bases à la création de tableaux complexes et responsives.

### 3.5.1 Structure de tableaux accessibles

Le premier chapitre pose les **fondations essentielles**. Vous découvrirez comment créer la structure de base d'un tableau avec les balises principales : `<table>`, `<tr>`, `<th>`, `<td>`, et `<caption>`.

L'accent est mis dès le début sur l'**accessibilité** : comment utiliser correctement les balises `<th>` pour les en-têtes, pourquoi l'attribut `scope` est crucial, et comment créer des tableaux que tout le monde peut comprendre, y compris les utilisateurs de lecteurs d'écran.

Vous apprendrez également la règle fondamentale : quand utiliser des tableaux (données tabulaires réelles) et quand ne PAS les utiliser (mise en page, listes, contenu qui n'est pas tabulaire).

### 3.5.2 En-têtes et organisation : thead, tbody, tfoot

Le deuxième chapitre approfondit l'**organisation structurelle** des tableaux. Vous découvrirez comment diviser vos tableaux en trois sections logiques : l'en-tête (`<thead>`), le corps (`<tbody>`), et le pied (`<tfoot>`).

Cette structure n'est pas qu'une question de style : elle apporte une sémantique forte qui améliore l'accessibilité, facilite le styling CSS, et permet des fonctionnalités avancées comme l'en-tête fixe lors du scroll ou la répétition automatique des en-têtes à l'impression.

Vous verrez comment organiser des tableaux complexes avec plusieurs groupes de données, comment utiliser plusieurs `<tbody>` pour séparer des sections, et comment créer des en-têtes hiérarchiques sur plusieurs niveaux.

### 3.5.3 Cellules et attributs de fusion

Le troisième chapitre explore les **attributs de fusion** `colspan` et `rowspan` qui permettent à une cellule de s'étendre sur plusieurs colonnes ou plusieurs lignes.

Ces attributs sont essentiels pour créer des tableaux sophistiqués : en-têtes groupés, plannings complexes, factures professionnelles, tableaux de comparaison, et bien plus encore.

Vous apprendrez à calculer correctement le nombre de cellules par ligne, à éviter les erreurs courantes de fusion, et à combiner `colspan` et `rowspan` pour créer des structures avancées tout en maintenant l'accessibilité.

### 3.5.4 Responsive et accessibilité avancée

Le quatrième chapitre aborde les **défis modernes** : comment rendre vos tableaux utilisables sur mobile alors qu'ils peuvent contenir beaucoup de colonnes ?

Vous découvrirez plusieurs techniques pour rendre vos tableaux responsives : scroll horizontal, transformation en cartes sur mobile, affichage sélectif des colonnes, et autres stratégies CSS et JavaScript.

Le chapitre couvre également l'accessibilité avancée avec les attributs ARIA, les techniques de navigation au clavier, et comment tester vos tableaux avec des lecteurs d'écran. Vous verrez aussi comment gérer les tableaux de données dynamiques et interactifs.

---

## Les trois piliers d'un bon tableau

### 1. Sémantique et structure

Un bon tableau utilise les **bonnes balises au bon endroit** :

**`<table>` : Le conteneur principal**
C'est la balise qui englobe tout le tableau. Elle doit contenir uniquement des éléments de tableau, jamais de contenu direct.

**`<caption>` : Le titre du tableau**
Toujours présent pour décrire le contenu du tableau. C'est le premier élément qu'un lecteur d'écran annonce.

**`<thead>`, `<tbody>`, `<tfoot>` : Les sections**
Divisent le tableau en zones logiques pour une meilleure organisation et accessibilité.

**`<tr>` : Les lignes (Table Row)**
Contiennent les cellules. Toutes les lignes d'un tableau doivent avoir le même nombre de colonnes (sauf avec colspan/rowspan).

**`<th>` : Les cellules d'en-tête (Table Header)**
Pour les titres de colonnes et de lignes. Toujours avec un attribut `scope` explicite.

**`<td>` : Les cellules de données (Table Data)**
Pour les données du tableau.

**Structure minimale d'un bon tableau :**
```html
<table>
    <caption>Titre descriptif du tableau</caption>
    <thead>
        <tr>
            <th scope="col">En-tête 1</th>
            <th scope="col">En-tête 2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Donnée 1</td>
            <td>Donnée 2</td>
        </tr>
    </tbody>
</table>
```

### 2. Accessibilité

L'accessibilité des tableaux repose sur plusieurs principes :

**En-têtes explicites avec `<th>` et `scope`**
Chaque en-tête doit clairement indiquer s'il décrit une colonne (`scope="col"`) ou une ligne (`scope="row"`). C'est ce qui permet aux lecteurs d'écran d'annoncer correctement les données : "Produit : Ordinateur, Prix : 899 euros".

**Caption toujours présent**
Le `<caption>` donne le contexte du tableau immédiatement. Sans lui, un utilisateur de lecteur d'écran ne sait pas de quoi parle le tableau avant de l'explorer.

**Structure logique**
L'ordre des éléments dans le code HTML doit refléter l'ordre logique de lecture. Ne comptez pas uniquement sur le CSS pour positionner les éléments.

**Contraste et taille**
Le texte dans les tableaux doit avoir un contraste suffisant (4.5:1 minimum) et une taille lisible (16px minimum recommandé).

**Navigation au clavier**
Les tableaux interactifs doivent être entièrement navigables au clavier avec Tab, flèches, et autres raccourcis standards.

### 3. Présentation et utilisabilité

Un bon tableau doit être **visuellement clair et agréable à lire** :

**Espacement adéquat**
Les cellules doivent avoir un padding suffisant (10-15px) pour que le contenu respire. Des cellules trop serrées rendent la lecture difficile.

**Bordures et séparations**
Les bordures aident à distinguer les cellules. Utilisez `border-collapse: collapse` pour des bordures nettes et `border: 1px solid #ddd` pour des séparations subtiles.

**Alternance de couleurs (zebra striping)**
Des lignes alternées en couleurs légèrement différentes améliorent considérablement la lisibilité, surtout pour les longs tableaux.

**En-têtes différenciés**
Le `<thead>` doit se démarquer visuellement avec une couleur de fond différente et/ou du texte en gras.

**Alignement du contenu**
- Texte : aligné à gauche
- Nombres : alignés à droite pour faciliter la comparaison
- En-têtes : selon le contexte (centré ou aligné au contenu)

**Survol interactif**
Un effet de survol (`:hover`) sur les lignes aide à suivre la ligne des yeux sur un large tableau.

---

## Tableaux vs. autres solutions

### Quand utiliser un tableau

**✅ Utilisez un tableau pour :**

**Données réellement tabulaires**
Si vous pouvez imaginer vos données dans Excel ou Google Sheets, c'est probablement un cas d'usage valide pour un tableau HTML.

**Exemples clairs :**
- Horaires et plannings
- Listes de prix et tarifs
- Résultats sportifs
- Statistiques et données financières
- Comparaisons de produits ou services
- Données scientifiques ou techniques
- Inventaires et catalogues

**Règle simple :** Si chaque ligne représente un "enregistrement" avec plusieurs "champs", et que vous avez plusieurs enregistrements similaires, c'est un tableau.

### Quand NE PAS utiliser un tableau

**❌ N'utilisez PAS de tableau pour :**

**La mise en page**
Jamais, au grand jamais. Utilisez CSS (Flexbox ou Grid) pour positionner des éléments sur la page.

**Des listes**
Si vous avez une simple liste d'éléments sans colonnes multiples, utilisez `<ul>` ou `<ol>`, pas un tableau à une colonne.

**Du contenu qui n'a pas de structure tabulaire**
Par exemple, une galerie d'images, une liste d'articles de blog, ou un menu de navigation.

**Pour forcer un alignement visuel**
Si vous voulez juste aligner des éléments visuellement, c'est un job pour CSS, pas pour un tableau.

### Alternatives aux tableaux

**Pour la mise en page : CSS Flexbox et Grid**
```css
.container {
    display: grid;
    grid-template-columns: 200px 1fr 300px;
    gap: 20px;
}
```

**Pour des listes : `<ul>` et `<ol>`**
```html
<ul>
    <li>Élément 1</li>
    <li>Élément 2</li>
</ul>
```

**Pour des cartes de données : `<article>` et CSS**
```html
<article class="product-card">
    <h3>Produit</h3>
    <p>Description</p>
    <span class="price">99€</span>
</article>
```

**Pour des définitions : `<dl>`, `<dt>`, `<dd>`**
```html
<dl>
    <dt>Terme</dt>
    <dd>Définition</dd>
</dl>
```

---

## Les erreurs courantes avec les tableaux

### 1. Utiliser des tableaux pour la mise en page

**Erreur majeure** qui persiste malheureusement encore aujourd'hui, surtout dans les emails HTML où le support CSS est limité (mais même là, il existe de meilleures solutions).

**Pourquoi c'est grave :**
- Désastre pour l'accessibilité
- Impossible à rendre responsive
- Mauvais pour le SEO
- Code complexe et difficile à maintenir

**Solution :** Apprenez CSS Flexbox et Grid. C'est un investissement en temps qui en vaut la peine.

### 2. Oublier le `<caption>`

Beaucoup de développeurs créent des tableaux sans caption, pensant qu'un titre `<h2>` au-dessus suffit. Ce n'est pas le cas.

**Problème :** Le caption est sémantiquement lié au tableau. Les lecteurs d'écran l'annoncent automatiquement avant le contenu du tableau, ce qui n'est pas le cas d'un titre séparé.

**Solution :** Toujours inclure un `<caption>` descriptif comme premier élément du tableau.

### 3. Utiliser `<td>` pour les en-têtes

Utiliser `<td>` avec du texte en gras pour simuler des en-têtes, au lieu d'utiliser `<th>`.

**Problème :** Les lecteurs d'écran ne reconnaissent pas ces cellules comme des en-têtes. La structure sémantique est perdue.

**Solution :** Toujours utiliser `<th>` pour les en-têtes, avec l'attribut `scope` approprié.

### 4. Oublier l'attribut `scope` sur les `<th>`

Créer des `<th>` sans préciser s'ils décrivent des colonnes ou des lignes.

**Problème :** Les lecteurs d'écran doivent deviner la relation entre en-têtes et données, ce qui peut mener à des interprétations incorrectes.

**Solution :** Toujours ajouter `scope="col"` ou `scope="row"` sur chaque `<th>`.

### 5. Ne pas structurer avec thead, tbody, tfoot

Mettre toutes les lignes directement dans `<table>` sans sections, même pour des tableaux complexes.

**Problème :** Perte de sémantique, impossible de fixer l'en-tête lors du scroll, difficile à styliser, répétition d'en-têtes à l'impression problématique.

**Solution :** Toujours utiliser `<thead>`, `<tbody>`, et `<tfoot>` si approprié, même si techniquement optionnel.

### 6. Nombre de colonnes incohérent

Avoir des lignes avec un nombre différent de cellules sans utiliser `colspan` ou `rowspan`.

**Problème :** Le tableau se déforme, la structure devient illisible.

**Solution :** Vérifiez que chaque ligne a le même nombre total de colonnes (en comptant les colspan).

### 7. Tableaux non responsives

Créer des tableaux larges sans stratégie pour les petits écrans.

**Problème :** Sur mobile, le tableau déborde, nécessite un scroll horizontal pénible, ou est carrément illisible.

**Solution :** Implémenter une stratégie responsive (que nous verrons dans le chapitre 3.5.4).

### 8. Styling avec attributs HTML obsolètes

Utiliser des attributs HTML comme `border`, `cellpadding`, `cellspacing`, `bgcolor`, etc.

**Problème :** Ces attributs sont obsolètes en HTML5, mélangent structure et présentation, et sont difficiles à maintenir.

**Solution :** Tout le styling doit être fait en CSS, pas avec des attributs HTML.

```html
<!-- ❌ OBSOLÈTE -->
<table border="1" cellpadding="10" cellspacing="0" bgcolor="#cccccc">

<!-- ✅ MODERNE -->
<table class="styled-table">
```

```css
.styled-table {
    border-collapse: collapse;
    background-color: #cccccc;
}

.styled-table td,
.styled-table th {
    padding: 10px;
    border: 1px solid #ddd;
}
```

---

## Ce que vous pourrez créer

Après avoir complété cette section sur les tableaux HTML5, vous serez capable de créer professionnellement :

### Tableaux de données commerciales

**Catalogues de produits**
Tableaux avec images, descriptions, prix, disponibilité, boutons d'achat, tout parfaitement organisé et accessible.

**Comparaisons de forfaits/services**
Tableaux de comparaison avec en-têtes groupés, cellules fusionnées pour les caractéristiques communes, mise en évidence des offres recommandées.

**Factures et devis**
Tableaux professionnels avec sections (produits, services, totaux), calculs automatiques, notes de bas de page, entièrement imprimables.

### Tableaux de planification

**Emplois du temps scolaires**
Planning hebdomadaire avec jours en colonnes, horaires en lignes, cellules fusionnées pour les cours longs, codes couleur par matière.

**Planning de conférences/événements**
Programmation avec plusieurs salles, sessions plénières sur toutes les salles, pauses, ateliers simultanés.

**Calendriers mensuels**
Calendrier classique 7 colonnes × 5-6 lignes, avec dates spéciales mise en évidence, événements dans les cellules.

### Tableaux statistiques et financiers

**Tableaux de bord analytiques**
Statistiques avec totaux, moyennes, pourcentages, évolutions, indicateurs visuels.

**Rapports financiers**
Bilans comptables avec actifs/passifs, comptes de résultats, flux de trésorerie, sous-totaux et totaux généraux.

**Résultats sportifs**
Classements avec positions, équipes, statistiques (points, victoires, défaites), évolutions par rapport à la semaine précédente.

### Tableaux interactifs

**Tableaux triables**
Tableaux où l'utilisateur peut cliquer sur les en-têtes pour trier par colonne (ascendant/descendant).

**Tableaux filtrables**
Recherche en temps réel qui filtre les lignes selon les critères de l'utilisateur.

**Tableaux avec pagination**
Grands ensembles de données divisés en pages, avec navigation et indication du nombre total d'entrées.

**Tableaux éditables**
Cellules éditables in-place, modification des données sans rechargement de page, validation en temps réel.

Tous ces tableaux seront non seulement fonctionnels et beaux visuellement, mais aussi **parfaitement accessibles** et **responsives** pour tous les appareils.

---

## Compatibilité navigateurs

La bonne nouvelle : les tableaux HTML sont l'une des fonctionnalités les **mieux supportées** du web. La structure de base des tableaux (`<table>`, `<tr>`, `<th>`, `<td>`) fonctionne dans **absolument tous les navigateurs**, même les très anciens.

### Support navigateurs modernes

**Structure HTML5 complète :** 100% supporté
- `<table>`, `<thead>`, `<tbody>`, `<tfoot>`
- `<tr>`, `<th>`, `<td>`, `<caption>`
- Attributs `scope`, `colspan`, `rowspan`
- Chrome, Firefox, Safari, Edge, Opera : support complet

**Attribut `headers` :** 99%+ supporté
Pour les tableaux complexes avec associations en-têtes/données via IDs.

**CSS avancé (position: sticky) :** 97%+ supporté
Pour les en-têtes fixes lors du scroll. Tous les navigateurs modernes depuis 2020.

### Points d'attention

**Internet Explorer 11** (encore présent dans certaines entreprises)
- Support de base : ✅ Complet
- position: sticky : ❌ Non supporté (fallback nécessaire)
- Solution : Détection et fallback JavaScript

**Anciens navigateurs mobiles** (< 2018)
- Structure HTML : ✅ Complet
- Tableaux responsives complexes : ⚠️ Tests nécessaires

**Impression**
- display: table-header-group pour répéter thead : support variable
- Toujours tester l'aperçu avant impression

### Stratégie de compatibilité

**Principe de dégradation gracieuse :**
Créez des tableaux avec une structure HTML solide. Même si CSS avancé ou JavaScript ne fonctionnent pas, le tableau reste **lisible et fonctionnel**.

**Progressive enhancement :**
Commencez par un tableau HTML sémantique de base, puis ajoutez des améliorations CSS et JavaScript pour les navigateurs qui les supportent.

**La structure HTML prime :**
Un tableau avec un HTML parfait mais un CSS basique sera toujours meilleur qu'un tableau avec un HTML approximatif mais un CSS sophistiqué.

---

## Outils et ressources

### Validateurs et testeurs

**W3C Markup Validator**
- https://validator.w3.org/
- Vérifie la validité HTML de vos tableaux
- Détecte les erreurs de structure

**WAVE Web Accessibility Evaluation Tool**
- Extension navigateur gratuite
- Teste l'accessibilité des tableaux
- Identifie les problèmes avec les en-têtes et scope

**Lighthouse (Chrome DevTools)**
- Audit automatique incluant l'accessibilité
- Score et recommandations concrètes

### Documentation de référence

**MDN Web Docs**
- https://developer.mozilla.org/fr/docs/Web/HTML/Element/table
- Documentation complète et exemples
- Meilleures pratiques actualisées

**W3C HTML Specification**
- Spécification officielle HTML
- Définitions précises des éléments et attributs

**WebAIM - Tables**
- https://webaim.org/techniques/tables/
- Guide complet sur l'accessibilité des tableaux
- Exemples détaillés

### Outils de développement

**Inspecteur de navigateur**
- Clic droit → Inspecter
- Visualisez la structure réelle du tableau
- Déboguez les problèmes de colspan/rowspan

**Lecteurs d'écran pour tests**
- NVDA (Windows, gratuit)
- JAWS (Windows, payant)
- VoiceOver (macOS/iOS, intégré)
- TalkBack (Android, intégré)

**Générateurs de tableaux**
- Tools online pour prototyper rapidement
- Attention : toujours vérifier et corriger le code généré

---

## Structure de cette section

Cette section est organisée de manière **progressive et pratique**. Chaque chapitre s'appuie sur les connaissances du précédent pour construire une compréhension complète et solide des tableaux HTML5.

**Chapitre 1** vous donne les fondations : structure de base, balises essentielles, accessibilité de base.

**Chapitre 2** approfondit l'organisation avec thead, tbody, tfoot pour des tableaux mieux structurés.

**Chapitre 3** ajoute la complexité avec colspan et rowspan pour des tableaux sophistiqués.

**Chapitre 4** aborde les défis modernes : responsive design et accessibilité avancée.

Chaque chapitre contient :
- Des explications claires adaptées aux débutants
- De nombreux exemples de code commentés
- Des visualisations pour comprendre la structure
- Des exemples pratiques réels et complets
- Des bonnes pratiques et erreurs à éviter
- Des points clés à retenir

**Pas d'exercices pratiques** comme demandé, mais les exemples fournis sont conçus pour être testés et modifiés directement. Nous encourageons l'expérimentation : copiez les exemples, modifiez-les, cassez-les, réparez-les. C'est en faisant qu'on apprend le mieux.

---

## Les trois règles d'or des tableaux

Avant de commencer cette section, gravez ces trois règles dans votre esprit :

### Règle 1 : Tableaux = Données tabulaires uniquement

Si ce ne sont pas des données qui devraient être dans Excel, ce n'est pas un tableau HTML. Utilisez CSS pour la mise en page, `<ul>` pour les listes, et d'autres éléments sémantiques appropriés.

### Règle 2 : Accessibilité d'abord, toujours

Chaque tableau doit avoir un `<caption>`, chaque en-tête doit être un `<th>` avec `scope`, et la structure doit être compréhensible sans voir le tableau. L'accessibilité n'est pas optionnelle, c'est une responsabilité.

### Règle 3 : Structure HTML solide avant tout

Un tableau avec un HTML parfait et un CSS basique sera toujours meilleur qu'un tableau avec un HTML approximatif et un CSS magnifique. La structure sémantique est la fondation sur laquelle tout le reste repose.

---

## Prochaine étape

Maintenant que vous comprenez l'importance des tableaux et leur place dans le développement web moderne, il est temps de plonger dans la pratique.

Le premier chapitre vous attend : **Structure de tableaux accessibles**. Vous y découvrirez comment créer vos premiers tableaux HTML avec une structure solide et accessible, en utilisant les bonnes balises au bon endroit.

Vous apprendrez à faire la distinction entre `<th>` et `<td>`, à utiliser l'attribut `scope` correctement, à ajouter un `<caption>` descriptif, et à styliser vos tableaux avec CSS moderne.

Prêt à créer des tableaux professionnels ? Allons-y ! 🚀

⏭️ [Structure de tableaux accessibles](/03-html5-structure-et-semantique/05-tableaux/01-structure-tableaux-accessibles.md)
