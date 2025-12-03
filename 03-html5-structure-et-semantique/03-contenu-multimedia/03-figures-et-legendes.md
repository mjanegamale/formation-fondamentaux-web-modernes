🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.3.3 Figures et légendes (figure, figcaption)

## Introduction

HTML5 a introduit deux balises sémantiques très utiles pour structurer le contenu multimédia : `<figure>` et `<figcaption>`. Ensemble, elles permettent d'associer un contenu (image, vidéo, illustration, code, etc.) à une légende de manière sémantiquement correcte.

Avant HTML5, on utilisait souvent des `<div>` avec des classes personnalisées. Maintenant, nous avons des balises dédiées qui améliorent la structure, l'accessibilité et le référencement de nos pages.

---

## La balise `<figure>`

### Qu'est-ce qu'une figure ?

Une **figure** est un contenu auto-contenu qui :
- Illustre ou complète le contenu principal
- Peut être déplacé ailleurs dans le document sans perdre son sens
- Peut avoir une légende explicative

**Exemples de figures :**
- Une image avec sa description
- Un diagramme ou graphique
- Un extrait de code source
- Une vidéo avec son titre
- Une citation avec sa source
- Un tableau de données

### Syntaxe de base

```html
<figure>
    <!-- Contenu de la figure (image, vidéo, code, etc.) -->
</figure>
```

La balise `<figure>` est un **conteneur sémantique** qui enveloppe le contenu que vous souhaitez présenter comme une figure.

---

## La balise `<figcaption>`

### Qu'est-ce qu'une légende ?

`<figcaption>` (figure caption) représente la **légende** ou **description** de la figure. Elle fournit un contexte, une explication ou un titre pour le contenu de la figure.

### Syntaxe

```html
<figure>
    <img src="photo.jpg" alt="Description courte">
    <figcaption>Légende détaillée de l'image</figcaption>
</figure>
```

**Règles importantes :**

1. `<figcaption>` est **optionnel** (une figure peut exister sans légende)
2. `<figcaption>` doit être **enfant direct** de `<figure>`
3. Il ne peut y avoir **qu'un seul** `<figcaption>` par `<figure>`
4. `<figcaption>` peut être placé en **premier** ou en **dernier** dans la figure

```html
<!-- ✅ Légende en dernier (plus courant) -->
<figure>
    <img src="chat.jpg" alt="Chat">
    <figcaption>Mon chat Félix en train de dormir</figcaption>
</figure>

<!-- ✅ Légende en premier (aussi valide) -->
<figure>
    <figcaption>Résultats de l'expérience scientifique</figcaption>
    <img src="graphique.jpg" alt="Graphique des résultats">
</figure>
```

---

## Pourquoi utiliser `<figure>` et `<figcaption>` ?

### 1. Sémantique et structure

Ces balises donnent un **sens** au contenu :

```html
<!-- ❌ AVANT (pas sémantique) -->
<div class="image-container">
    <img src="photo.jpg" alt="Paysage">
    <p class="caption">Vue sur les Alpes françaises</p>
</div>

<!-- ✅ MAINTENANT (sémantique) -->
<figure>
    <img src="photo.jpg" alt="Paysage">
    <figcaption>Vue sur les Alpes françaises</figcaption>
</figure>
```

La seconde version indique clairement au navigateur, aux moteurs de recherche et aux technologies d'assistance qu'il s'agit d'une figure avec sa légende.

### 2. Accessibilité

Les lecteurs d'écran comprennent la relation entre le contenu et sa légende :

```html
<figure>
    <img src="diagramme.png" alt="Diagramme du processus">
    <figcaption>
        Figure 1 : Processus de fabrication en 5 étapes,
        de la matière première au produit fini
    </figcaption>
</figure>
```

Un lecteur d'écran annoncera : *"Figure, Diagramme du processus, Figure 1 : Processus de fabrication..."*

### 3. SEO (référencement)

Les moteurs de recherche comprennent mieux la structure et peuvent indexer les légendes comme contexte des images.

### 4. Styling CSS cohérent

Il est plus facile de styliser uniformément toutes vos figures :

```css
figure {
    margin: 2rem 0;
    border: 1px solid #ddd;
    padding: 1rem;
    background-color: #f9f9f9;
}

figcaption {
    font-style: italic;
    color: #666;
    margin-top: 0.5rem;
    text-align: center;
}
```

---

## Cas d'usage principaux

### 1. Images avec légende

C'est l'utilisation la plus courante :

```html
<article>
    <h2>Découverte d'une nouvelle espèce</h2>
    <p>Des biologistes ont découvert une nouvelle espèce de papillon...</p>

    <figure>
        <img src="papillon-rare.jpg"
             alt="Papillon aux ailes bleues et noires"
             width="600"
             height="400">
        <figcaption>
            Figure 1 : Le <em>Papilio novus</em>, découvert en Amazonie en 2024
        </figcaption>
    </figure>

    <p>Cette espèce se caractérise par...</p>
</article>
```

**Remarque** : L'attribut `alt` reste **obligatoire** ! Il fournit une description courte, tandis que `<figcaption>` donne un contexte ou des informations supplémentaires.

#### Différence entre `alt` et `<figcaption>`

```html
<figure>
    <!-- alt : description de CE QUI EST dans l'image -->
    <img src="conference.jpg"
         alt="Femme présentant devant un auditoire de 50 personnes">

    <!-- figcaption : contexte, où, quand, pourquoi -->
    <figcaption>
        Marie Dupont lors de sa conférence sur l'IA à Paris,
        le 15 novembre 2024
    </figcaption>
</figure>
```

### 2. Galeries d'images multiples

Vous pouvez mettre plusieurs images dans une seule figure :

```html
<figure>
    <img src="photo1.jpg" alt="Vue d'ensemble du bâtiment">
    <img src="photo2.jpg" alt="Détail de la façade">
    <img src="photo3.jpg" alt="Intérieur du hall">
    <figcaption>
        Figure 2 : Le nouveau musée d'art moderne,
        vues extérieures et intérieures
    </figcaption>
</figure>
```

Ou avec une structure plus détaillée :

```html
<figure>
    <div class="gallery">
        <img src="avant.jpg" alt="Maison avant rénovation">
        <img src="apres.jpg" alt="Maison après rénovation">
    </div>
    <figcaption>
        Comparaison avant/après de la rénovation écologique
    </figcaption>
</figure>
```

### 3. Vidéos avec légende

Parfait pour contextualiser des vidéos :

```html
<figure>
    <video controls width="800" height="450">
        <source src="tutoriel.mp4" type="video/mp4">
    </video>
    <figcaption>
        Vidéo 1 : Tutoriel complet sur la création d'un site responsive
        (durée : 15 minutes)
    </figcaption>
</figure>
```

### 4. Audio avec légende

```html
<figure>
    <audio controls>
        <source src="interview-expert.mp3" type="audio/mpeg">
    </audio>
    <figcaption>
        Interview du Dr. Martin sur les nouvelles technologies
        (Podcast #42, 12 décembre 2024)
    </figcaption>
</figure>
```

### 5. Extraits de code

Très utile dans les tutoriels et documentations techniques :

```html
<figure>
    <pre><code>
function saluer(nom) {
    return `Bonjour ${nom} !`;
}

console.log(saluer("Alice"));
// Affiche : Bonjour Alice !
    </code></pre>
    <figcaption>
        Listing 1 : Fonction JavaScript utilisant les template literals
    </figcaption>
</figure>
```

### 6. Citations (blockquotes)

Pour des citations importantes avec attribution :

```html
<figure>
    <blockquote>
        <p>
            Le web est plus qu'un outil, c'est un nouveau média qui
            transforme notre façon de communiquer et de penser.
        </p>
    </blockquote>
    <figcaption>
        — Tim Berners-Lee, inventeur du World Wide Web,
        <cite>Weaving the Web</cite> (1999)
    </figcaption>
</figure>
```

### 7. Tableaux de données

Pour des tableaux nécessitant un contexte explicatif :

```html
<figure>
    <table>
        <thead>
            <tr>
                <th>Trimestre</th>
                <th>Ventes (K€)</th>
                <th>Croissance</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>T1 2024</td>
                <td>120</td>
                <td>+15%</td>
            </tr>
            <tr>
                <td>T2 2024</td>
                <td>145</td>
                <td>+21%</td>
            </tr>
            <tr>
                <td>T3 2024</td>
                <td>168</td>
                <td>+16%</td>
            </tr>
        </tbody>
    </table>
    <figcaption>
        Tableau 1 : Évolution des ventes sur les trois premiers trimestres 2024
    </figcaption>
</figure>
```

### 8. Diagrammes et schémas SVG

```html
<figure>
    <svg width="300" height="200" viewBox="0 0 300 200">
        <rect x="50" y="50" width="100" height="80" fill="#3498db"/>
        <circle cx="200" cy="90" r="40" fill="#e74c3c"/>
        <line x1="150" y1="90" x2="160" y2="90" stroke="#000" stroke-width="2"/>
        <text x="100" y="95" text-anchor="middle" fill="white">Input</text>
        <text x="200" y="95" text-anchor="middle" fill="white">Output</text>
    </svg>
    <figcaption>
        Figure 3 : Schéma simplifié du flux de données dans l'application
    </figcaption>
</figure>
```

---

## Figures imbriquées (cas rare)

Il est possible (mais rare) d'imbriquer des figures :

```html
<figure>
    <figcaption>Série de photographies du projet Alpha</figcaption>

    <figure>
        <img src="alpha-phase1.jpg" alt="Phase 1 du projet">
        <figcaption>Phase 1 : Conception (janvier 2024)</figcaption>
    </figure>

    <figure>
        <img src="alpha-phase2.jpg" alt="Phase 2 du projet">
        <figcaption>Phase 2 : Développement (mars 2024)</figcaption>
    </figure>

    <figure>
        <img src="alpha-phase3.jpg" alt="Phase 3 du projet">
        <figcaption>Phase 3 : Lancement (juin 2024)</figcaption>
    </figure>
</figure>
```

⚠️ **Attention** : Gardez cette structure simple. Une imbrication complexe peut nuire à l'accessibilité.

---

## Styling CSS des figures

### Styles de base

```css
/* Style général des figures */
figure {
    margin: 2rem auto;
    max-width: 100%;
    text-align: center;
}

/* L'image dans la figure */
figure img {
    max-width: 100%;
    height: auto;
    display: block;
}

/* Style de la légende */
figcaption {
    margin-top: 0.75rem;
    font-size: 0.9rem;
    font-style: italic;
    color: #555;
    line-height: 1.5;
}
```

### Exemple de style "carte"

```css
figure {
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    margin: 2rem auto;
    max-width: 600px;
}

figure img {
    width: 100%;
    height: auto;
    display: block;
}

figcaption {
    padding: 1rem;
    background-color: #f8f9fa;
    border-top: 1px solid #dee2e6;
    font-size: 0.9rem;
    color: #495057;
    text-align: left;
}
```

**HTML correspondant :**
```html
<figure>
    <img src="produit.jpg" alt="Nouveau smartphone">
    <figcaption>
        <strong>Smartphone Pro X</strong> -
        Le dernier né de notre gamme premium,
        disponible en trois coloris
    </figcaption>
</figure>
```

### Numérotation automatique des figures

Vous pouvez numéroter automatiquement vos figures avec CSS :

```css
/* Compteur pour les figures */
body {
    counter-reset: figure-counter;
}

figure {
    counter-increment: figure-counter;
}

figcaption::before {
    content: "Figure " counter(figure-counter) " : ";
    font-weight: bold;
}
```

**Résultat :**
- Figure 1 : Première légende
- Figure 2 : Deuxième légende
- Figure 3 : Troisième légende

```html
<!-- HTML simple, la numérotation est automatique -->
<figure>
    <img src="image1.jpg" alt="Description">
    <figcaption>Paysage montagneux</figcaption>
</figure>

<figure>
    <img src="image2.jpg" alt="Description">
    <figcaption>Lac de montagne</figcaption>
</figure>
```

---

## Accessibilité et bonnes pratiques

### 1. L'attribut `alt` reste obligatoire

```html
<!-- ✅ BON : alt ET figcaption -->
<figure>
    <img src="graphique.png"
         alt="Graphique en barres montrant la croissance des ventes"
         width="600"
         height="400">
    <figcaption>
        Figure 1 : Croissance des ventes 2020-2024,
        avec une augmentation de 45%
    </figcaption>
</figure>

<!-- ❌ MAUVAIS : pas d'alt -->
<figure>
    <img src="graphique.png">
    <figcaption>Figure 1 : Croissance des ventes</figcaption>
</figure>
```

**Rappel :**
- `alt` = description courte de ce qui est dans l'image
- `figcaption` = contexte, explication, numéro de figure

### 2. Légendes significatives

```html
<!-- ❌ MAUVAIS : légende vague -->
<figure>
    <img src="photo.jpg" alt="Oiseau sur une branche">
    <figcaption>Photo d'oiseau</figcaption>
</figure>

<!-- ✅ BON : légende informative -->
<figure>
    <img src="photo.jpg" alt="Oiseau sur une branche">
    <figcaption>
        Rouge-gorge européen photographié dans le jardin botanique
        de Lyon, avril 2024
    </figcaption>
</figure>
```

### 3. Figures sans légende

Si une figure n'a pas besoin de légende, vous pouvez omettre `<figcaption>` :

```html
<!-- ✅ Valide : figure sans légende -->
<figure>
    <img src="logo.png" alt="Logo de l'entreprise">
</figure>
```

Mais dans ce cas, demandez-vous si `<figure>` est vraiment nécessaire. Si l'image n'a pas besoin de contexte supplémentaire, un simple `<img>` suffit.

### 4. Contenu riche dans les légendes

Les légendes peuvent contenir du HTML :

```html
<figure>
    <img src="manuscrit.jpg" alt="Page de manuscrit ancien">
    <figcaption>
        <strong>Figure 3.2</strong> : Manuscrit médiéval du
        <abbr title="treizième">XIII<sup>e</sup></abbr> siècle.
        Source : <cite>Bibliothèque Nationale de France</cite>.
        <a href="source-complete.html">Voir la notice complète</a>
    </figcaption>
</figure>
```

### 5. Figures et articles

Dans un article scientifique ou technique, référencez vos figures dans le texte :

```html
<article>
    <h2>Résultats de l'étude</h2>

    <p>
        Les données récoltées montrent une tendance claire
        (voir <a href="#fig-resultats">Figure 1</a>).
        On observe notamment une augmentation significative...
    </p>

    <figure id="fig-resultats">
        <img src="graphique-resultats.png"
             alt="Graphique des résultats expérimentaux">
        <figcaption>
            Figure 1 : Évolution des mesures sur 12 mois
        </figcaption>
    </figure>

    <p>
        Comme le montre la Figure 1, les valeurs ont augmenté de...
    </p>
</article>
```

---

## Quand NE PAS utiliser `<figure>` ?

### 1. Logo ou icône décorative

```html
<!-- ❌ PAS NÉCESSAIRE pour un logo simple -->
<figure>
    <img src="logo.png" alt="Logo entreprise">
</figure>

<!-- ✅ MIEUX : img simple suffit -->
<img src="logo.png" alt="Logo entreprise" class="site-logo">
```

### 2. Image purement décorative

```html
<!-- ❌ PAS NÉCESSAIRE pour décoration -->
<figure>
    <img src="decoration.png" alt="">
</figure>

<!-- ✅ MIEUX : img simple ou CSS background -->
<img src="decoration.png" alt="" class="decoration">
```

### 3. Image dans un lien sans contexte additionnel

```html
<!-- ❌ PAS VRAIMENT UTILE -->
<figure>
    <a href="produit.html">
        <img src="produit.jpg" alt="Voir le produit">
    </a>
</figure>

<!-- ✅ MIEUX : pas de figure si pas de légende nécessaire -->
<a href="produit.html">
    <img src="produit.jpg" alt="Voir le produit">
</a>
```

**Règle générale** : Si vous n'avez pas de légende significative à ajouter ou si l'image ne constitue pas une "figure" au sens d'un élément auto-contenu illustratif, `<figure>` n'est probablement pas nécessaire.

---

## Exemples complets et pratiques

### Exemple 1 : Article de blog avec images

```html
<article>
    <header>
        <h1>Voyage au Japon : Guide complet</h1>
        <p>Par Marie Dubois | 3 décembre 2024</p>
    </header>

    <p>
        Le Japon est une destination fascinante qui mélange
        tradition et modernité. Voici mon retour d'expérience...
    </p>

    <figure>
        <img src="tokyo-skyline.jpg"
             alt="Vue panoramique de Tokyo avec la tour Skytree"
             width="800"
             height="500">
        <figcaption>
            Tokyo au coucher du soleil, vue depuis le quartier de Shibuya
        </figcaption>
    </figure>

    <h2>Les incontournables</h2>

    <p>
        Parmi les lieux à ne pas manquer, Kyoto se distingue
        par ses temples traditionnels...
    </p>

    <figure>
        <img src="temple-kyoto.jpg"
             alt="Temple zen entouré de jardins japonais"
             width="800"
             height="600">
        <figcaption>
            Le temple Kinkaku-ji (Pavillon d'Or) à Kyoto,
            classé au patrimoine mondial de l'UNESCO
        </figcaption>
    </figure>
</article>
```

### Exemple 2 : Documentation technique

```html
<article>
    <h1>Installation de Node.js</h1>

    <p>
        Pour vérifier que Node.js est correctement installé,
        ouvrez votre terminal et exécutez la commande suivante :
    </p>

    <figure>
        <pre><code>node --version</code></pre>
        <figcaption>
            Commande pour vérifier la version de Node.js installée
        </figcaption>
    </figure>

    <p>
        Vous devriez voir s'afficher le numéro de version :
    </p>

    <figure>
        <pre><code>v20.10.0</code></pre>
        <figcaption>
            Exemple de sortie indiquant que Node.js v20.10.0 est installé
        </figcaption>
    </figure>
</article>
```

### Exemple 3 : Portfolio photographique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio Photo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
            background-color: #f5f5f5;
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        figure {
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
            margin: 0;
        }

        figure:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
        }

        figure img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            display: block;
        }

        figcaption {
            padding: 1rem;
            font-size: 0.9rem;
            color: #333;
            line-height: 1.5;
        }

        figcaption strong {
            display: block;
            margin-bottom: 0.25rem;
            color: #000;
            font-size: 1rem;
        }
    </style>
</head>
<body>
    <h1>Portfolio - Nature & Paysages</h1>

    <div class="gallery">
        <figure>
            <img src="montagne-1.jpg"
                 alt="Sommet enneigé au lever du soleil">
            <figcaption>
                <strong>L'aube sur le Mont Blanc</strong>
                Haute-Savoie, France - Février 2024
            </figcaption>
        </figure>

        <figure>
            <img src="foret-2.jpg"
                 alt="Chemin forestier couvert de feuilles d'automne">
            <figcaption>
                <strong>Promenade automnale</strong>
                Forêt de Fontainebleau - Octobre 2024
            </figcaption>
        </figure>

        <figure>
            <img src="lac-3.jpg"
                 alt="Lac de montagne avec reflets">
            <figcaption>
                <strong>Miroir naturel</strong>
                Lac d'Annecy au crépuscule - Juillet 2024
            </figcaption>
        </figure>

        <figure>
            <img src="cascade-4.jpg"
                 alt="Grande cascade dans la jungle">
            <figcaption>
                <strong>Force de la nature</strong>
                Cascade du Rouget, Alpes - Mai 2024
            </figcaption>
        </figure>
    </div>
</body>
</html>
```

### Exemple 4 : Rapport scientifique

```html
<article>
    <h1>Étude sur la biodiversité marine</h1>

    <section>
        <h2>Méthodologie</h2>
        <p>
            L'étude a été menée sur une période de 12 mois,
            avec des prélèvements hebdomadaires. La figure 1
            présente le site d'étude.
        </p>

        <figure id="fig1">
            <img src="carte-site.jpg"
                 alt="Carte géographique du site d'étude"
                 width="700"
                 height="500">
            <figcaption>
                <strong>Figure 1</strong> : Localisation du site d'étude
                dans la baie de Douarnenez, Bretagne.
                Les points rouges indiquent les zones de prélèvement.
            </figcaption>
        </figure>
    </section>

    <section>
        <h2>Résultats</h2>
        <p>
            Les résultats montrent une diversité importante
            (voir <a href="#fig2">Figure 2</a>).
        </p>

        <figure id="fig2">
            <img src="graphique-diversite.png"
                 alt="Graphique en barres de la diversité des espèces"
                 width="800"
                 height="500">
            <figcaption>
                <strong>Figure 2</strong> : Distribution des espèces
                recensées par famille. Les mollusques représentent 42%
                des observations (n=1247).
            </figcaption>
        </figure>

        <figure id="table1">
            <table>
                <caption>Tableau 1 : Nombre d'espèces par saison</caption>
                <thead>
                    <tr>
                        <th>Saison</th>
                        <th>Espèces observées</th>
                        <th>Nouvelles espèces</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Printemps</td>
                        <td>87</td>
                        <td>12</td>
                    </tr>
                    <tr>
                        <td>Été</td>
                        <td>103</td>
                        <td>8</td>
                    </tr>
                    <tr>
                        <td>Automne</td>
                        <td>95</td>
                        <td>5</td>
                    </tr>
                    <tr>
                        <td>Hiver</td>
                        <td>68</td>
                        <td>2</td>
                    </tr>
                </tbody>
            </table>
            <figcaption>
                Recensement saisonnier effectué entre janvier et
                décembre 2024. Les nouvelles espèces correspondent
                à des observations non répertoriées lors des études
                précédentes (2019-2023).
            </figcaption>
        </figure>
    </section>
</article>
```

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Utiliser `<figure>` pour du contenu auto-contenu** qui illustre le document
2. **Ajouter `<figcaption>`** quand une légende apporte une valeur
3. **Garder `alt` sur les images** même dans une figure
4. **Rendre les légendes informatives** et contextuelles
5. **Référencer les figures** dans le texte (Figure 1, voir ci-dessous, etc.)
6. **Utiliser pour divers contenus** : images, vidéos, code, tableaux, citations
7. **Soigner le style CSS** pour une présentation cohérente
8. **Permettre l'accessibilité** en combinant correctement `alt` et `figcaption`

### ❌ À ÉVITER

1. Utiliser `<figure>` pour toutes les images (uniquement celles qui le méritent)
2. Omettre l'attribut `alt` sous prétexte qu'il y a une légende
3. Légendes vagues ou redondantes avec `alt`
4. Utiliser `<figure>` pour des logos ou images purement décoratives
5. Imbriquer des figures de manière complexe sans raison
6. Oublier de référencer les figures importantes dans le texte
7. Mettre plusieurs `<figcaption>` dans une même `<figure>`

---

## Tableau récapitulatif

| Élément | Rôle | Obligatoire ? | Nombre par figure |
|---------|------|---------------|-------------------|
| `<figure>` | Conteneur sémantique | - | 1 par contenu |
| `<figcaption>` | Légende/description | Non | 0 ou 1 |
| `alt` (sur img) | Description de l'image | Oui | 1 |
| Contenu | Image, vidéo, code, etc. | Oui | 1 ou plusieurs |

---

## Points clés à retenir

1. **`<figure>` = conteneur sémantique** pour contenu illustratif auto-contenu
2. **`<figcaption>` = légende** optionnelle mais recommandée
3. **Une seule `<figcaption>` par `<figure>`**, en premier ou en dernier
4. **`alt` reste obligatoire** sur les images, même dans une figure
5. **Utilisable pour** : images, vidéos, audio, code, citations, tableaux, diagrammes
6. **Améliore** : sémantique, accessibilité, SEO, maintenance
7. **N'utilisez pas** pour logos, icônes, ou images sans contexte additionnel

---

## Ressources complémentaires

- **MDN - `<figure>`** : Documentation complète
- **MDN - `<figcaption>`** : Spécifications détaillées
- **W3C HTML5 Specification** : Définition officielle
- **WebAIM** : Guide d'accessibilité pour les figures

---

## Prochaine étape

Dans le prochain chapitre, nous aborderons les **formulaires HTML5**, un élément essentiel pour toute interaction utilisateur sur le web. Nous verrons comment créer des formulaires accessibles, sécurisés et modernes avec les nouveaux types d'inputs introduits par HTML5.

⏭️ [Formulaires HTML5](/03-html5-structure-et-semantique/04-formulaires-html5/README.md)
