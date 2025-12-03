🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.2.2 Paragraphes et listes (ul, ol, dl)

## Introduction

Après avoir structuré votre page avec des titres, il est temps de donner vie à votre contenu avec deux éléments fondamentaux : les **paragraphes** et les **listes**.

Ces éléments constituent le **corps du texte** de vos pages web. Pensez-y comme aux phrases et aux listes à puces d'un document Word, mais en version HTML.

**Dans cette section, vous apprendrez :**
- Comment créer des paragraphes de texte
- Les trois types de listes HTML
- Quand utiliser chaque type de liste
- Comment imbriquer des listes
- Les bonnes pratiques pour un contenu structuré

## Les paragraphes (`<p>`)

### Qu'est-ce qu'un paragraphe ?

La balise `<p>` (pour "paragraph") est utilisée pour créer un **bloc de texte**. C'est l'élément le plus courant pour afficher du contenu textuel.

**Syntaxe de base :**
```html
<p>Ceci est un paragraphe de texte.</p>
```

### Caractéristiques d'un paragraphe

**1. Espacement automatique**

Les navigateurs ajoutent automatiquement un **espace vertical** avant et après chaque paragraphe pour les séparer visuellement :

```html
<p>Premier paragraphe.</p>
<p>Deuxième paragraphe.</p>
<p>Troisième paragraphe.</p>
```

**Rendu :**
```
Premier paragraphe.

Deuxième paragraphe.

Troisième paragraphe.
```

**2. Retours à la ligne automatiques**

Le texte dans un paragraphe se **répartit automatiquement** sur plusieurs lignes selon la largeur de la fenêtre :

```html
<p>Ceci est un très long paragraphe qui va automatiquement passer à la ligne suivante quand il atteindra le bord de la fenêtre du navigateur. Vous n'avez pas besoin de vous soucier de la longueur des lignes.</p>
```

### Les retours à la ligne dans le code source

**Important :** Les retours à la ligne et espaces multiples dans votre **code HTML** sont ignorés par le navigateur.

**Exemple :**
```html
<p>Ce texte
   comporte plusieurs
        retours à la ligne
   et espaces
   dans le code source.</p>
```

**Affichage réel :**
```
Ce texte comporte plusieurs retours à la ligne et espaces dans le code source.
```

Tout est affiché sur une seule ligne avec des espaces simples !

### Comment forcer un retour à la ligne ?

Si vous voulez vraiment un retour à la ligne **à l'intérieur** d'un paragraphe, utilisez la balise `<br>` (pour "break") :

```html
<p>
    Première ligne<br>
    Deuxième ligne<br>
    Troisième ligne
</p>
```

**Important :** `<br>` est une balise **auto-fermante** (pas de `</br>`). Utilisez-la avec parcimonie : si vous avez besoin de plusieurs `<br>`, demandez-vous si vous ne devriez pas plutôt créer plusieurs paragraphes.

✅ **Bon usage de `<br>` :**
```html
<p>
    Jean Dupont<br>
    123 Rue de la Paix<br>
    75001 Paris
</p>
```

❌ **Mauvais usage (créez plutôt des paragraphes séparés) :**
```html
<p>
    Premier point important.<br>
    <br>
    <br>
    Deuxième point important.
</p>

<!-- Mieux : -->
<p>Premier point important.</p>
<p>Deuxième point important.</p>
```

### Paragraphes et sémantique

Un paragraphe représente une **unité de pensée** complète. Chaque nouvelle idée devrait idéalement être dans un nouveau paragraphe.

**Exemple d'article bien structuré :**
```html
<h1>Les bienfaits de la lecture</h1>

<p>La lecture est une activité bénéfique pour le cerveau à tout âge. Elle stimule l'imagination, enrichit le vocabulaire et améliore la concentration.</p>

<p>Des études scientifiques ont démontré que lire régulièrement réduit le stress et améliore la qualité du sommeil. Même quelques minutes par jour peuvent faire une différence significative.</p>

<p>Pour profiter pleinement de ces bienfaits, choisissez des livres qui vous passionnent vraiment. La lecture ne doit jamais être une corvée, mais un plaisir.</p>
```

Chaque paragraphe développe une idée distincte.

### Paragraphes vides

❌ **À éviter :** Ne créez jamais de paragraphes vides pour espacer le contenu.

```html
<!-- Mauvais : paragraphes vides pour l'espacement -->
<p>Premier paragraphe.</p>
<p></p>
<p></p>
<p>Deuxième paragraphe.</p>
```

✅ **Bon :** Utilisez CSS pour contrôler l'espacement.

```html
<p>Premier paragraphe.</p>
<p>Deuxième paragraphe.</p>

<!-- En CSS : -->
<style>
    p {
        margin-bottom: 20px;
    }
</style>
```

## Les listes non ordonnées (`<ul>`)

### Qu'est-ce qu'une liste non ordonnée ?

Une liste **non ordonnée** (unordered list) est utilisée quand l'**ordre des éléments n'est pas important**. C'est l'équivalent des listes à puces dans un document Word.

**Syntaxe :**
```html
<ul>
    <li>Premier élément</li>
    <li>Deuxième élément</li>
    <li>Troisième élément</li>
</ul>
```

**Rendu par défaut :**
```
• Premier élément
• Deuxième élément
• Troisième élément
```

### Anatomie d'une liste

- **`<ul>`** : La balise conteneur (UL = Unordered List)
- **`<li>`** : Chaque élément de la liste (LI = List Item)

**Règle importante :** Les balises `<li>` doivent **toujours** être des enfants directs de `<ul>`. Vous ne pouvez pas mettre autre chose directement dans `<ul>`.

✅ **Correct :**
```html
<ul>
    <li>Élément 1</li>
    <li>Élément 2</li>
</ul>
```

❌ **Incorrect :**
```html
<ul>
    Élément 1  <!-- ❌ Texte direct sans <li> -->
    <li>Élément 2</li>
</ul>
```

### Quand utiliser une liste non ordonnée ?

Utilisez `<ul>` quand l'ordre n'importe pas :

**✅ Bons exemples :**
```html
<!-- Liste de courses -->
<ul>
    <li>Pain</li>
    <li>Lait</li>
    <li>Œufs</li>
    <li>Fromage</li>
</ul>

<!-- Avantages d'un produit -->
<ul>
    <li>Facile à utiliser</li>
    <li>Prix compétitif</li>
    <li>Garantie 2 ans</li>
    <li>Livraison gratuite</li>
</ul>

<!-- Menu de navigation -->
<ul>
    <li>Accueil</li>
    <li>Services</li>
    <li>À propos</li>
    <li>Contact</li>
</ul>
```

**❌ Mauvais exemple (utilisez `<ol>` à la place) :**
```html
<!-- Recette de cuisine : l'ordre est important ! -->
<ul>
    <li>Préchauffer le four</li>
    <li>Mélanger les ingrédients</li>
    <li>Enfourner 30 minutes</li>
</ul>
```

### Personnalisation des puces

Par défaut, les navigateurs affichent des **disques pleins** (•). Vous pouvez changer cela avec CSS :

```html
<style>
    .liste-carree {
        list-style-type: square;  /* Carrés ■ */
    }

    .liste-cercle {
        list-style-type: circle;  /* Cercles ○ */
    }

    .liste-sans {
        list-style-type: none;    /* Pas de puce */
    }
</style>

<ul class="liste-carree">
    <li>Élément avec carré</li>
</ul>

<ul class="liste-sans">
    <li>Élément sans puce</li>
</ul>
```

## Les listes ordonnées (`<ol>`)

### Qu'est-ce qu'une liste ordonnée ?

Une liste **ordonnée** (ordered list) est utilisée quand l'**ordre des éléments est important**. Par défaut, les éléments sont numérotés.

**Syntaxe :**
```html
<ol>
    <li>Premier élément</li>
    <li>Deuxième élément</li>
    <li>Troisième élément</li>
</ol>
```

**Rendu par défaut :**
```
1. Premier élément
2. Deuxième élément
3. Troisième élément
```

### Quand utiliser une liste ordonnée ?

Utilisez `<ol>` quand l'**ordre est significatif** :

**✅ Bons exemples :**
```html
<!-- Instructions étape par étape -->
<ol>
    <li>Ouvrez le fichier</li>
    <li>Cliquez sur "Modifier"</li>
    <li>Apportez vos modifications</li>
    <li>Enregistrez le fichier</li>
</ol>

<!-- Classement -->
<ol>
    <li>Paris - 2,1 millions d'habitants</li>
    <li>Marseille - 870 000 habitants</li>
    <li>Lyon - 520 000 habitants</li>
</ol>

<!-- Recette de cuisine -->
<ol>
    <li>Préchauffer le four à 180°C</li>
    <li>Mélanger la farine et le sucre</li>
    <li>Ajouter les œufs un par un</li>
    <li>Verser dans un moule</li>
    <li>Enfourner 30 minutes</li>
</ol>
```

### Attributs de `<ol>`

#### 1. Commencer à un numéro différent

Utilisez l'attribut `start` pour commencer la numérotation à un nombre spécifique :

```html
<ol start="5">
    <li>Cinquième étape</li>
    <li>Sixième étape</li>
    <li>Septième étape</li>
</ol>
```

**Rendu :**
```
5. Cinquième étape
6. Sixième étape
7. Septième étape
```

#### 2. Changer le type de numérotation

L'attribut `type` change le style de numérotation :

```html
<!-- Chiffres arabes (par défaut) -->
<ol type="1">
    <li>Un</li>
    <li>Deux</li>
</ol>
<!-- Rendu : 1. Un / 2. Deux -->

<!-- Lettres majuscules -->
<ol type="A">
    <li>Point A</li>
    <li>Point B</li>
</ol>
<!-- Rendu : A. Point A / B. Point B -->

<!-- Lettres minuscules -->
<ol type="a">
    <li>Option a</li>
    <li>Option b</li>
</ol>
<!-- Rendu : a. Option a / b. Option b -->

<!-- Chiffres romains majuscules -->
<ol type="I">
    <li>Premier</li>
    <li>Deuxième</li>
</ol>
<!-- Rendu : I. Premier / II. Deuxième -->

<!-- Chiffres romains minuscules -->
<ol type="i">
    <li>Premier</li>
    <li>Deuxième</li>
</ol>
<!-- Rendu : i. Premier / ii. Deuxième -->
```

#### 3. Ordre inversé

L'attribut `reversed` inverse l'ordre de numérotation :

```html
<ol reversed>
    <li>Bronze</li>
    <li>Argent</li>
    <li>Or</li>
</ol>
```

**Rendu :**
```
3. Bronze
2. Argent
1. Or
```

**Cas d'usage :** Compte à rebours, classements inversés.

#### 4. Changer la valeur d'un élément spécifique

L'attribut `value` sur un `<li>` change sa numérotation (et affecte les suivants) :

```html
<ol>
    <li>Étape 1</li>
    <li>Étape 2</li>
    <li value="10">Étape 10</li>
    <li>Étape 11</li>
</ol>
```

**Rendu :**
```
1. Étape 1
2. Étape 2
10. Étape 10
11. Étape 11
```

## Les listes de définition (`<dl>`)

### Qu'est-ce qu'une liste de définition ?

La liste de **définition** (definition list) est utilisée pour afficher des paires **terme-définition**, comme dans un glossaire ou un dictionnaire.

**Syntaxe :**
```html
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language - Langage de balisage pour créer des pages web</dd>

    <dt>CSS</dt>
    <dd>Cascading Style Sheets - Langage de style pour la présentation des pages web</dd>

    <dt>JavaScript</dt>
    <dd>Langage de programmation pour rendre les pages web interactives</dd>
</dl>
```

### Anatomie d'une liste de définition

- **`<dl>`** : Le conteneur (DL = Definition List)
- **`<dt>`** : Le terme à définir (DT = Definition Term)
- **`<dd>`** : La définition du terme (DD = Definition Description)

**Rendu typique :**
```
HTML
    HyperText Markup Language - Langage de balisage...
CSS
    Cascading Style Sheets - Langage de style...
JavaScript
    Langage de programmation...
```

La définition est généralement **indentée** par rapport au terme.

### Relations multiples

**Un terme, plusieurs définitions :**
```html
<dl>
    <dt>Run</dt>
    <dd>Verbe : Se déplacer rapidement à pied</dd>
    <dd>Nom : Action de courir</dd>
    <dd>Nom : Série d'événements (un run de chance)</dd>
</dl>
```

**Plusieurs termes, une définition :**
```html
<dl>
    <dt>HTML</dt>
    <dt>HyperText Markup Language</dt>
    <dd>Le langage standard pour créer des pages web</dd>
</dl>
```

### Cas d'usage des listes de définition

**✅ Glossaire :**
```html
<h2>Glossaire du développement web</h2>
<dl>
    <dt>Frontend</dt>
    <dd>La partie visible d'un site web avec laquelle l'utilisateur interagit</dd>

    <dt>Backend</dt>
    <dd>La partie serveur d'un site web qui gère la logique et les données</dd>

    <dt>API</dt>
    <dd>Application Programming Interface - Interface permettant à des applications de communiquer entre elles</dd>
</dl>
```

**✅ FAQ (Foire Aux Questions) :**
```html
<h2>Questions fréquentes</h2>
<dl>
    <dt>Combien coûte le service ?</dt>
    <dd>Notre service de base est gratuit. Les fonctionnalités premium démarrent à 9,99€/mois.</dd>

    <dt>Puis-je annuler mon abonnement ?</dt>
    <dd>Oui, vous pouvez annuler à tout moment sans frais supplémentaires.</dd>
</dl>
```

**✅ Métadonnées / Informations produit :**
```html
<h2>Spécifications techniques</h2>
<dl>
    <dt>Poids</dt>
    <dd>250 grammes</dd>

    <dt>Dimensions</dt>
    <dd>15 x 10 x 5 cm</dd>

    <dt>Couleurs disponibles</dt>
    <dd>Noir, Blanc, Gris</dd>

    <dt>Garantie</dt>
    <dd>2 ans</dd>
</dl>
```

**✅ Définitions juridiques ou techniques :**
```html
<dl>
    <dt>RGPD</dt>
    <dd>Règlement Général sur la Protection des Données - Réglementation européenne sur la protection des données personnelles entrée en vigueur le 25 mai 2018.</dd>
</dl>
```

## Imbrication de listes

Vous pouvez **imbriquer** des listes les unes dans les autres pour créer une structure hiérarchique.

### Imbriquer des listes non ordonnées

```html
<h2>Menu du restaurant</h2>
<ul>
    <li>Entrées
        <ul>
            <li>Salade César</li>
            <li>Soupe du jour</li>
            <li>Bruschetta</li>
        </ul>
    </li>
    <li>Plats principaux
        <ul>
            <li>Poulet rôti</li>
            <li>Saumon grillé</li>
            <li>Pasta carbonara</li>
        </ul>
    </li>
    <li>Desserts
        <ul>
            <li>Tiramisu</li>
            <li>Tarte aux pommes</li>
            <li>Crème brûlée</li>
        </ul>
    </li>
</ul>
```

**Important :** La liste imbriquée doit être **à l'intérieur** d'un `<li>`, pas directement dans le `<ul>`.

✅ **Correct :**
```html
<ul>
    <li>Élément parent
        <ul>
            <li>Élément enfant</li>
        </ul>
    </li>
</ul>
```

❌ **Incorrect :**
```html
<ul>
    <li>Élément parent</li>
    <ul>  <!-- ❌ Ne peut pas être enfant direct de <ul> -->
        <li>Élément enfant</li>
    </ul>
</ul>
```

### Imbriquer des listes ordonnées

```html
<h2>Procédure d'installation</h2>
<ol>
    <li>Préparation
        <ol>
            <li>Télécharger le logiciel</li>
            <li>Vérifier les prérequis système</li>
            <li>Sauvegarder vos données</li>
        </ol>
    </li>
    <li>Installation
        <ol>
            <li>Lancer le programme d'installation</li>
            <li>Accepter les conditions</li>
            <li>Choisir le dossier d'installation</li>
        </ol>
    </li>
    <li>Configuration
        <ol>
            <li>Créer un compte utilisateur</li>
            <li>Configurer les préférences</li>
            <li>Redémarrer l'ordinateur</li>
        </ol>
    </li>
</ol>
```

**Rendu :**
```
1. Préparation
   1. Télécharger le logiciel
   2. Vérifier les prérequis système
   3. Sauvegarder vos données
2. Installation
   1. Lancer le programme d'installation
   2. Accepter les conditions
   3. Choisir le dossier d'installation
3. Configuration
   1. Créer un compte utilisateur
   2. Configurer les préférences
   3. Redémarrer l'ordinateur
```

### Mélanger les types de listes

Vous pouvez imbriquer différents types de listes :

```html
<h2>Plan de cours</h2>
<ol>
    <li>Introduction au HTML
        <ul>
            <li>Qu'est-ce que HTML ?</li>
            <li>Histoire et évolution</li>
            <li>Structure de base</li>
        </ul>
    </li>
    <li>Les balises essentielles
        <ul>
            <li>Titres et paragraphes</li>
            <li>Listes</li>
            <li>Liens et images</li>
        </ul>
    </li>
</ol>
```

## Listes et contenu enrichi

### Listes avec des liens

Les listes sont souvent utilisées pour créer des menus de navigation :

```html
<nav>
    <ul>
        <li><a href="index.html">Accueil</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="about.html">À propos</a></li>
        <li><a href="contact.html">Contact</a></li>
    </ul>
</nav>
```

### Listes avec du formatage

Vous pouvez inclure du **formatage** dans les éléments de liste :

```html
<ul>
    <li><strong>Important :</strong> Ne pas oublier de sauvegarder</li>
    <li><em>Conseil :</em> Utilisez un mot de passe fort</li>
    <li>Coût : <del>99€</del> <strong>49€</strong></li>
</ul>
```

### Listes avec plusieurs paragraphes

Un `<li>` peut contenir plusieurs paragraphes et autres éléments :

```html
<ol>
    <li>
        <h3>Première étape : Préparation</h3>
        <p>Rassemblez tous les ingrédients nécessaires.</p>
        <p>Assurez-vous que tout est à température ambiante.</p>
    </li>
    <li>
        <h3>Deuxième étape : Mélange</h3>
        <p>Combinez les ingrédients secs dans un bol.</p>
        <p>Dans un autre bol, mélangez les ingrédients liquides.</p>
    </li>
</ol>
```

## Accessibilité des listes

### Pourquoi les listes sont importantes pour l'accessibilité

Les **lecteurs d'écran** annoncent :
- Le type de liste (ordonnée ou non ordonnée)
- Le nombre total d'éléments
- La position actuelle dans la liste

**Exemple d'annonce :**
```
"Liste de 3 éléments"
"Élément 1 sur 3 : Premier élément"
"Élément 2 sur 3 : Deuxième élément"
"Élément 3 sur 3 : Troisième élément"
"Fin de la liste"
```

Cela aide les utilisateurs à **comprendre la structure** et à **naviguer efficacement**.

### Utiliser les vraies balises de liste

❌ **Mauvais (non accessible) :**
```html
<div>• Premier élément</div>
<div>• Deuxième élément</div>
<div>• Troisième élément</div>
```

✅ **Bon (accessible) :**
```html
<ul>
    <li>Premier élément</li>
    <li>Deuxième élément</li>
    <li>Troisième élément</li>
</ul>
```

### Listes de navigation

Pour les menus, combinez les listes avec la balise `<nav>` pour une meilleure sémantique :

```html
<nav aria-label="Navigation principale">
    <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services">Services</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

## Erreurs courantes à éviter

### Erreur 1 : Oublier la balise `<li>`

❌ **Mauvais :**
```html
<ul>
    Premier élément
    Deuxième élément
</ul>
```

✅ **Bon :**
```html
<ul>
    <li>Premier élément</li>
    <li>Deuxième élément</li>
</ul>
```

### Erreur 2 : Mettre autre chose que `<li>` directement dans `<ul>` ou `<ol>`

❌ **Mauvais :**
```html
<ul>
    <p>Ceci est un paragraphe</p>
    <li>Élément de liste</li>
</ul>
```

✅ **Bon :**
```html
<ul>
    <li>
        <p>Ceci est un paragraphe dans un élément de liste</p>
    </li>
    <li>Élément de liste</li>
</ul>
```

### Erreur 3 : Utiliser une liste pour de l'espacement

❌ **Mauvais (utilisation incorrecte) :**
```html
<ul>
    <li>Texte 1</li>
</ul>
<ul>
    <li>Texte 2</li>
</ul>
<!-- Créer plusieurs listes juste pour l'espacement -->
```

✅ **Bon :**
```html
<ul>
    <li>Texte 1</li>
    <li>Texte 2</li>
</ul>
<!-- Une seule liste, utilisez CSS pour l'espacement -->
```

### Erreur 4 : Mal imbriquer les listes

❌ **Mauvais :**
```html
<ul>
    <li>Élément parent</li>
    <ul>  <!-- ❌ Directement dans <ul> -->
        <li>Élément enfant</li>
    </ul>
</ul>
```

✅ **Bon :**
```html
<ul>
    <li>Élément parent
        <ul>  <!-- ✅ Dans le <li> -->
            <li>Élément enfant</li>
        </ul>
    </li>
</ul>
```

### Erreur 5 : Utiliser des listes pour ce qui n'est pas une liste

❌ **Mauvais (abus de liste) :**
```html
<ul>
    <li>Bienvenue sur notre site !</li>
</ul>
<!-- Un seul élément n'est pas vraiment une "liste" -->
```

✅ **Bon :**
```html
<p>Bienvenue sur notre site !</p>
<!-- C'est juste un paragraphe -->
```

### Erreur 6 : Confusion entre `<ol>` et `<ul>`

❌ **Mauvais (l'ordre importe) :**
```html
<ul>
    <li>Cassez les œufs</li>
    <li>Chauffez la poêle</li>
    <li>Versez les œufs</li>
</ul>
```

✅ **Bon :**
```html
<ol>
    <li>Chauffez la poêle</li>
    <li>Cassez les œufs</li>
    <li>Versez les œufs</li>
</ol>
```

## Exemples pratiques complets

### Exemple 1 : Article de blog avec listes mixtes

```html
<article>
    <h1>10 conseils pour mieux dormir</h1>

    <p>Le sommeil est essentiel à notre santé. Voici mes meilleurs conseils pour améliorer la qualité de votre sommeil.</p>

    <h2>Habitudes à adopter</h2>
    <ol>
        <li>Se coucher à heure fixe chaque soir</li>
        <li>Éviter les écrans 1h avant le coucher</li>
        <li>Maintenir une température fraîche dans la chambre (18-20°C)</li>
        <li>Pratiquer une activité relaxante (lecture, méditation)</li>
        <li>Éviter la caféine après 16h</li>
    </ol>

    <h2>Aliments favorisant le sommeil</h2>
    <ul>
        <li>Bananes (riches en magnésium)</li>
        <li>Tisanes (camomille, verveine)</li>
        <li>Amandes</li>
        <li>Lait chaud</li>
    </ul>

    <h2>Signes d'un bon sommeil</h2>
    <p>Voici comment savoir si vous dormez suffisamment :</p>
    <ul>
        <li>Vous vous réveillez naturellement sans réveil</li>
        <li>Vous vous sentez reposé au réveil</li>
        <li>Vous n'avez pas de coups de fatigue dans la journée</li>
        <li>Votre concentration est bonne</li>
    </ul>
</article>
```

### Exemple 2 : Page produit e-commerce

```html
<article>
    <h1>Ordinateur portable UltraBook Pro 15</h1>

    <h2>Caractéristiques principales</h2>
    <dl>
        <dt>Processeur</dt>
        <dd>Intel Core i7 12ème génération</dd>

        <dt>Mémoire RAM</dt>
        <dd>16 Go DDR5</dd>

        <dt>Stockage</dt>
        <dd>512 Go SSD NVMe</dd>

        <dt>Écran</dt>
        <dd>15,6 pouces Full HD (1920x1080)</dd>

        <dt>Système d'exploitation</dt>
        <dd>Windows 11 Pro</dd>

        <dt>Poids</dt>
        <dd>1,8 kg</dd>
    </dl>

    <h2>Points forts</h2>
    <ul>
        <li>Ultraléger et portable</li>
        <li>Autonomie jusqu'à 12 heures</li>
        <li>Charge rapide (80% en 30 minutes)</li>
        <li>Clavier rétroéclairé</li>
        <li>Reconnaissance faciale</li>
    </ul>

    <h2>Contenu de la boîte</h2>
    <ol>
        <li>Ordinateur portable UltraBook Pro 15</li>
        <li>Adaptateur secteur 65W</li>
        <li>Câble USB-C vers USB-C</li>
        <li>Guide de démarrage rapide</li>
        <li>Carte de garantie</li>
    </ol>
</article>
```

### Exemple 3 : Recette de cuisine

```html
<article>
    <h1>Cookies aux pépites de chocolat</h1>

    <p>Des cookies moelleux et délicieux, prêts en 30 minutes !</p>

    <h2>Ingrédients</h2>
    <p>Pour environ 20 cookies :</p>
    <ul>
        <li>200g de farine</li>
        <li>125g de beurre mou</li>
        <li>100g de sucre blanc</li>
        <li>50g de sucre roux</li>
        <li>1 œuf</li>
        <li>1 sachet de sucre vanillé</li>
        <li>1/2 sachet de levure chimique</li>
        <li>200g de pépites de chocolat</li>
        <li>1 pincée de sel</li>
    </ul>

    <h2>Préparation</h2>
    <ol>
        <li>
            <strong>Préchauffage</strong>
            <p>Préchauffez votre four à 180°C (thermostat 6).</p>
        </li>
        <li>
            <strong>Mélange des ingrédients</strong>
            <p>Dans un saladier, mélangez le beurre mou avec les deux sucres jusqu'à obtenir une texture crémeuse.</p>
        </li>
        <li>
            <strong>Ajout de l'œuf</strong>
            <p>Incorporez l'œuf et mélangez bien.</p>
        </li>
        <li>
            <strong>Ajout des ingrédients secs</strong>
            <p>Ajoutez progressivement la farine, la levure, le sucre vanillé et le sel.</p>
        </li>
        <li>
            <strong>Les pépites</strong>
            <p>Incorporez délicatement les pépites de chocolat.</p>
        </li>
        <li>
            <strong>Façonnage</strong>
            <p>Formez des boules de pâte et disposez-les sur une plaque recouverte de papier sulfurisé, en les espaçant bien.</p>
        </li>
        <li>
            <strong>Cuisson</strong>
            <p>Enfournez pour 10-12 minutes. Les cookies doivent être légèrement dorés sur les bords mais encore moelleux au centre.</p>
        </li>
        <li>
            <strong>Refroidissement</strong>
            <p>Laissez refroidir 5 minutes sur la plaque avant de les transférer sur une grille.</p>
        </li>
    </ol>

    <h2>Conseils</h2>
    <ul>
        <li>Ne pas trop cuire : ils durcissent en refroidissant</li>
        <li>Vous pouvez remplacer les pépites par des morceaux de chocolat coupés</li>
        <li>Conservation : 5 jours dans une boîte hermétique</li>
        <li>Possibilité de congeler la pâte en boules pour une cuisson ultérieure</li>
    </ul>
</article>
```

### Exemple 4 : Documentation technique

```html
<article>
    <h1>Guide d'installation de WordPress</h1>

    <h2>Prérequis</h2>
    <p>Avant de commencer, assurez-vous d'avoir :</p>
    <ul>
        <li>Un hébergement web compatible PHP 7.4 ou supérieur</li>
        <li>Une base de données MySQL 5.6 ou supérieur</li>
        <li>Un client FTP (FileZilla recommandé)</li>
        <li>Les identifiants de votre hébergement</li>
    </ul>

    <h2>Installation étape par étape</h2>
    <ol>
        <li>
            <strong>Téléchargement</strong>
            <ol type="a">
                <li>Rendez-vous sur wordpress.org</li>
                <li>Cliquez sur "Télécharger WordPress"</li>
                <li>Enregistrez le fichier ZIP sur votre ordinateur</li>
            </ol>
        </li>
        <li>
            <strong>Création de la base de données</strong>
            <ol type="a">
                <li>Connectez-vous à votre panneau d'hébergement</li>
                <li>Accédez à phpMyAdmin</li>
                <li>Créez une nouvelle base de données</li>
                <li>Notez le nom, l'utilisateur et le mot de passe</li>
            </ol>
        </li>
        <li>
            <strong>Upload des fichiers</strong>
            <ol type="a">
                <li>Décompressez le fichier WordPress</li>
                <li>Connectez-vous en FTP à votre serveur</li>
                <li>Uploadez tous les fichiers dans le dossier public_html</li>
                <li>Attendez la fin du transfert (peut prendre quelques minutes)</li>
            </ol>
        </li>
        <li>
            <strong>Configuration</strong>
            <ol type="a">
                <li>Accédez à votre nom de domaine dans un navigateur</li>
                <li>Sélectionnez votre langue</li>
                <li>Entrez les informations de la base de données</li>
                <li>Cliquez sur "Lancer l'installation"</li>
            </ol>
        </li>
        <li>
            <strong>Finalisation</strong>
            <ol type="a">
                <li>Choisissez un titre pour votre site</li>
                <li>Créez votre compte administrateur</li>
                <li>Entrez votre adresse email</li>
                <li>Cliquez sur "Installer WordPress"</li>
            </ol>
        </li>
    </ol>

    <h2>Problèmes courants</h2>
    <dl>
        <dt>Erreur de connexion à la base de données</dt>
        <dd>Vérifiez que les informations de connexion (nom, utilisateur, mot de passe) sont correctes dans le fichier wp-config.php</dd>

        <dt>Page blanche après installation</dt>
        <dd>Augmentez la limite de mémoire PHP dans le fichier wp-config.php en ajoutant : define('WP_MEMORY_LIMIT', '256M');</dd>

        <dt>Erreur 500</dt>
        <dd>Vérifiez les permissions des fichiers (644 pour les fichiers, 755 pour les dossiers) et le fichier .htaccess</dd>
    </dl>
</article>
```

## Bonnes pratiques récapitulatives

### Pour les paragraphes
- ✅ Un paragraphe = une idée
- ✅ Évitez les paragraphes trop longs (difficiles à lire)
- ✅ Utilisez des paragraphes courts sur mobile
- ❌ Pas de paragraphes vides pour l'espacement
- ❌ Limitez l'usage de `<br>` (utilisez des paragraphes séparés)

### Pour les listes
- ✅ `<ul>` quand l'ordre n'importe pas
- ✅ `<ol>` quand l'ordre est significatif
- ✅ `<dl>` pour les paires terme-définition
- ✅ Toujours utiliser `<li>` pour chaque élément
- ✅ Imbriquez correctement (liste dans un `<li>`)
- ❌ Ne pas mettre de contenu directement dans `<ul>` ou `<ol>`
- ❌ Ne pas utiliser de fausses listes (div avec puces en texte)

### Pour l'accessibilité
- ✅ Utilisez les vraies balises sémantiques
- ✅ Structure logique et cohérente
- ✅ Contenu descriptif et clair
- ✅ Testez avec un lecteur d'écran si possible

## Checklist avant publication

Avant de publier votre page avec des listes et paragraphes, vérifiez :

- [ ] Chaque paragraphe contient une idée distincte
- [ ] Aucun paragraphe vide utilisé pour l'espacement
- [ ] Le type de liste correspond au contenu (`<ul>` vs `<ol>` vs `<dl>`)
- [ ] Tous les éléments de liste sont dans des balises `<li>`
- [ ] Les listes imbriquées sont correctement structurées
- [ ] Pas de contenu orphelin (directement dans `<ul>` ou `<ol>`)
- [ ] Le code est validé avec le validateur W3C
- [ ] Le contenu est lisible et logique

## Conclusion

Les paragraphes et les listes sont les **éléments de base** pour structurer votre contenu textuel. Bien utilisés, ils rendent votre contenu :

- **Plus lisible** : Structure claire et aérée
- **Plus accessible** : Navigation facilitée pour tous
- **Mieux référencé** : Google comprend mieux votre structure
- **Plus maintenable** : Code propre et logique

**Points clés à retenir :**

**Paragraphes :**
- Utilisez `<p>` pour chaque bloc de texte
- Une idée = un paragraphe
- Évitez les `<br>` multiples

**Listes non ordonnées (`<ul>`) :**
- Quand l'ordre n'importe pas
- Puces par défaut
- Usage : menus, listes de courses, avantages

**Listes ordonnées (`<ol>`) :**
- Quand l'ordre est important
- Numérotation automatique
- Usage : instructions, classements, recettes

**Listes de définition (`<dl>`) :**
- Paires terme-définition
- Structure : `<dt>` + `<dd>`
- Usage : glossaires, FAQ, spécifications

Maîtriser ces éléments simples mais essentiels vous permet de créer du contenu web structuré et professionnel. Dans la prochaine section, nous découvrirons les éléments sémantiques HTML5 qui enrichissent encore plus la structure de vos pages.

---


**Section suivante** : [3.2.3 Éléments sémantiques HTML5](./03-elements-semantiques-html5.md)

⏭️ [Éléments sémantiques HTML5](/03-html5-structure-et-semantique/02-elements-structurants/03-elements-semantiques-html5.md)
