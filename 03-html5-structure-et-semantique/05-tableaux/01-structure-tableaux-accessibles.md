🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.5.1 Structure de tableaux accessibles

## Introduction

Les tableaux HTML sont conçus pour présenter des **données tabulaires** : des informations organisées en lignes et en colonnes où chaque cellule a une relation avec les autres. Ils sont essentiels pour afficher des données structurées de manière claire et compréhensible.

**Exemples de données tabulaires :**
- Horaires de train
- Résultats sportifs
- Listes de prix
- Comparaisons de produits
- Statistiques
- Calendriers
- Emplois du temps

HTML5 offre une structure sémantique riche pour créer des tableaux accessibles et professionnels. Dans ce chapitre, nous allons découvrir comment créer des tableaux correctement structurés qui fonctionnent pour tous les utilisateurs.

---

## Pourquoi l'accessibilité des tableaux est cruciale

### Qui utilise les tableaux différemment ?

**Personnes malvoyantes avec lecteurs d'écran :**
- Ne voient pas la structure visuelle
- Dépendent des balises sémantiques
- Ont besoin d'en-têtes explicites pour naviguer

**Personnes sur mobile :**
- Petits écrans rendent les tableaux difficiles à lire
- Ont besoin d'une structure claire pour comprendre

**Tous les utilisateurs :**
- Bénéficient de tableaux bien organisés
- Comprennent mieux les données structurées

### L'impact d'un tableau mal structuré

```html
<!-- ❌ MAUVAIS : Structure invisible pour les lecteurs d'écran -->
<table>
    <tr>
        <td>Produit</td>
        <td>Prix</td>
    </tr>
    <tr>
        <td>Ordinateur</td>
        <td>899€</td>
    </tr>
</table>
```

**Problème :** Un lecteur d'écran ne sait pas que "Produit" et "Prix" sont des en-têtes. Il lit simplement "Produit, Prix, Ordinateur, 899 euros" sans contexte.

```html
<!-- ✅ BON : Structure claire et accessible -->
<table>
    <thead>
        <tr>
            <th scope="col">Produit</th>
            <th scope="col">Prix</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Ordinateur</td>
            <td>899€</td>
        </tr>
    </tbody>
</table>
```

**Résultat :** Le lecteur d'écran annonce "Colonne Produit, Colonne Prix" puis "Produit : Ordinateur, Prix : 899 euros". Contexte clair !

---

## Quand utiliser (et ne pas utiliser) des tableaux

### ✅ Utilisez des tableaux pour :

**Données tabulaires réelles :**
```html
<!-- ✅ BON : Comparaison de produits -->
<table>
    <caption>Comparaison des forfaits mobile</caption>
    <thead>
        <tr>
            <th>Forfait</th>
            <th>Data</th>
            <th>Prix</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Basic</td>
            <td>5 Go</td>
            <td>9,99€/mois</td>
        </tr>
        <tr>
            <td>Premium</td>
            <td>50 Go</td>
            <td>19,99€/mois</td>
        </tr>
    </tbody>
</table>
```

**Autres exemples valides :**
- Horaires (trains, cours, événements)
- Statistiques et résultats
- Listes de prix
- Données financières
- Tableaux de bord analytiques

### ❌ N'utilisez PAS de tableaux pour :

**La mise en page :**
```html
<!-- ❌ TRÈS MAUVAIS : Tableau pour la mise en page -->
<table>
    <tr>
        <td>Menu</td>
        <td>Contenu principal</td>
        <td>Sidebar</td>
    </tr>
</table>
```

**Pourquoi c'est mauvais :**
- Non sémantique (ce n'est pas des données)
- Problèmes d'accessibilité majeurs
- Non responsive
- Difficile à maintenir
- Mauvais pour le SEO

**✅ Utilisez plutôt CSS (Flexbox ou Grid) pour la mise en page :**
```html
<!-- ✅ BON : Mise en page avec CSS -->
<div class="container">
    <nav class="menu">Menu</nav>
    <main class="content">Contenu principal</main>
    <aside class="sidebar">Sidebar</aside>
</div>
```

**Règle simple :** Si ce ne sont pas des données qui devraient être dans une feuille Excel, ce n'est probablement pas un tableau !

---

## Structure de base d'un tableau

### Les balises essentielles

Un tableau HTML est construit avec plusieurs balises qui ont chacune un rôle spécifique :

```html
<table>           <!-- Conteneur principal -->
    <caption>     <!-- Titre du tableau -->
    <thead>       <!-- En-tête du tableau -->
        <tr>      <!-- Ligne (Table Row) -->
            <th>  <!-- Cellule d'en-tête (Table Header) -->
    <tbody>       <!-- Corps du tableau -->
        <tr>      <!-- Ligne -->
            <td>  <!-- Cellule de données (Table Data) -->
    <tfoot>       <!-- Pied de tableau (optionnel) -->
</table>
```

### Tableau le plus simple

Voici le tableau le plus simple possible :

```html
<table>
    <tr>
        <td>Ligne 1, Cellule 1</td>
        <td>Ligne 1, Cellule 2</td>
    </tr>
    <tr>
        <td>Ligne 2, Cellule 1</td>
        <td>Ligne 2, Cellule 2</td>
    </tr>
</table>
```

**Structure :**
- `<table>` : Le conteneur
- `<tr>` : Une ligne (Table Row)
- `<td>` : Une cellule de données (Table Data)

**Résultat visuel :**
```
┌─────────────────────┬─────────────────────┐
│ Ligne 1, Cellule 1  │ Ligne 1, Cellule 2  │
├─────────────────────┼─────────────────────┤
│ Ligne 2, Cellule 1  │ Ligne 2, Cellule 2  │
└─────────────────────┴─────────────────────┘
```

---

## La balise `<table>`

C'est le conteneur principal qui englobe tout le tableau.

```html
<table>
    <!-- Tout le contenu du tableau ici -->
</table>
```

### Attributs courants (pour CSS)

```html
<!-- Avec ID pour ciblage CSS/JavaScript -->
<table id="tableau-produits">
    <!-- contenu -->
</table>

<!-- Avec classe pour style -->
<table class="table-striped table-bordered">
    <!-- contenu -->
</table>
```

**Note :** Les anciens attributs HTML comme `border`, `cellpadding`, `cellspacing` sont **obsolètes**. Utilisez CSS à la place.

```html
<!-- ❌ OBSOLÈTE : attributs HTML -->
<table border="1" cellpadding="10" cellspacing="0">

<!-- ✅ MODERNE : CSS -->
<table class="styled-table">
```

```css
.styled-table {
    border-collapse: collapse;
    border: 1px solid #ddd;
}

.styled-table td,
.styled-table th {
    padding: 10px;
    border: 1px solid #ddd;
}
```

---

## La balise `<caption>` - Titre du tableau

`<caption>` fournit un titre ou une description pour le tableau. **Fortement recommandé pour l'accessibilité.**

```html
<table>
    <caption>Liste des employés - Décembre 2024</caption>
    <tr>
        <th>Nom</th>
        <th>Poste</th>
    </tr>
    <tr>
        <td>Dupont</td>
        <td>Développeur</td>
    </tr>
</table>
```

### Position de `<caption>`

`<caption>` doit être le **premier élément** juste après `<table>` :

```html
<!-- ✅ BON : caption en premier -->
<table>
    <caption>Horaires des cours</caption>
    <!-- reste du tableau -->
</table>

<!-- ❌ MAUVAIS : caption mal placé -->
<table>
    <tr>...</tr>
    <caption>Titre</caption>
</table>
```

### Pourquoi utiliser `<caption>` ?

**Accessibilité :**
- Les lecteurs d'écran lisent le caption avant le tableau
- Donne le contexte immédiatement
- Aide à comprendre le but du tableau

**SEO :**
- Aide les moteurs de recherche à comprendre le contenu
- Améliore l'indexation

**Utilisabilité :**
- Titre visible pour tous les utilisateurs
- Particulièrement utile pour plusieurs tableaux sur une page

### Styliser le caption

```css
caption {
    font-weight: bold;
    font-size: 1.2em;
    margin-bottom: 0.5rem;
    text-align: left; /* Par défaut : center */
}
```

---

## Les lignes : `<tr>` (Table Row)

`<tr>` représente une **ligne** dans le tableau. C'est un conteneur pour les cellules.

```html
<table>
    <tr>
        <!-- Cellules de la ligne 1 -->
    </tr>
    <tr>
        <!-- Cellules de la ligne 2 -->
    </tr>
</table>
```

**Règle importante :** Toutes les lignes d'un tableau doivent avoir le **même nombre de cellules** (sauf si vous utilisez `colspan` ou `rowspan`, que nous verrons dans un chapitre ultérieur).

```html
<!-- ✅ BON : 3 cellules par ligne -->
<table>
    <tr>
        <td>A</td>
        <td>B</td>
        <td>C</td>
    </tr>
    <tr>
        <td>D</td>
        <td>E</td>
        <td>F</td>
    </tr>
</table>

<!-- ❌ MAUVAIS : nombre de cellules différent -->
<table>
    <tr>
        <td>A</td>
        <td>B</td>
        <td>C</td>
    </tr>
    <tr>
        <td>D</td>
        <td>E</td>
        <!-- Cellule manquante ! -->
    </tr>
</table>
```

---

## Les cellules d'en-tête : `<th>` (Table Header)

`<th>` représente une **cellule d'en-tête**. Elle indique que le contenu est un titre de colonne ou de ligne.

```html
<table>
    <tr>
        <th>Nom</th>
        <th>Âge</th>
        <th>Ville</th>
    </tr>
    <tr>
        <td>Alice</td>
        <td>25</td>
        <td>Paris</td>
    </tr>
</table>
```

### Différences entre `<th>` et `<td>`

| Caractéristique | `<th>` (header) | `<td>` (data) |
|-----------------|-----------------|---------------|
| **Usage** | En-têtes (titres) | Données |
| **Style par défaut** | Gras + centré | Normal + aligné à gauche |
| **Accessibilité** | Annoncé comme en-tête | Annoncé comme donnée |
| **Sémantique** | Décrit la colonne/ligne | Contient les données |

### Pourquoi `<th>` est crucial pour l'accessibilité

```html
<!-- ❌ MAUVAIS : tout en <td> -->
<table>
    <tr>
        <td><strong>Produit</strong></td>
        <td><strong>Prix</strong></td>
    </tr>
    <tr>
        <td>Ordinateur</td>
        <td>899€</td>
    </tr>
</table>
```

**Problème :** Les lecteurs d'écran ne savent pas que ce sont des en-têtes. Visuellement en gras, mais pas sémantiquement des en-têtes.

```html
<!-- ✅ BON : en-têtes avec <th> -->
<table>
    <tr>
        <th>Produit</th>
        <th>Prix</th>
    </tr>
    <tr>
        <td>Ordinateur</td>
        <td>899€</td>
    </tr>
</table>
```

**Résultat :** Les lecteurs d'écran comprennent la structure et peuvent annoncer "Produit : Ordinateur, Prix : 899 euros".

### L'attribut `scope` - ESSENTIEL pour l'accessibilité

L'attribut `scope` indique **ce que l'en-tête décrit** : une colonne, une ligne, ou un groupe.

#### `scope="col"` - En-tête de colonne

```html
<table>
    <tr>
        <th scope="col">Prénom</th>
        <th scope="col">Nom</th>
        <th scope="col">Email</th>
    </tr>
    <tr>
        <td>Jean</td>
        <td>Dupont</td>
        <td>jean@example.com</td>
    </tr>
</table>
```

**Signification :** Ces en-têtes décrivent les colonnes en dessous.

#### `scope="row"` - En-tête de ligne

```html
<table>
    <caption>Emploi du temps</caption>
    <tr>
        <th scope="row">Lundi</th>
        <td>Mathématiques</td>
        <td>Français</td>
    </tr>
    <tr>
        <th scope="row">Mardi</th>
        <td>Histoire</td>
        <td>Anglais</td>
    </tr>
</table>
```

**Signification :** "Lundi" et "Mardi" décrivent les lignes à leur droite.

#### Pourquoi `scope` est important ?

Sans `scope`, les lecteurs d'écran devinent la relation, mais peuvent se tromper. Avec `scope`, c'est **explicite et garanti**.

**Lecteur d'écran sans scope :**
"Jean, Dupont, jean@example.com"

**Lecteur d'écran avec scope :**
"Prénom : Jean, Nom : Dupont, Email : jean@example.com"

**La différence est énorme !**

---

## Les cellules de données : `<td>` (Table Data)

`<td>` représente une **cellule de données** ordinaire.

```html
<td>Contenu de la cellule</td>
```

### Contenu des cellules

Les cellules peuvent contenir :

**Texte simple :**
```html
<td>Bonjour</td>
```

**Nombres :**
```html
<td>123</td>
<td>99,99€</td>
```

**Liens :**
```html
<td>
    <a href="/produit/1">Voir le produit</a>
</td>
```

**Images :**
```html
<td>
    <img src="icon.png" alt="Disponible" width="20" height="20">
</td>
```

**Boutons :**
```html
<td>
    <button type="button">Modifier</button>
</td>
```

**Éléments de formulaire :**
```html
<td>
    <input type="checkbox" id="select-1">
</td>
```

**HTML complexe :**
```html
<td>
    <strong>Important :</strong>
    <span class="price">99,99€</span>
</td>
```

---

## Sections du tableau : `<thead>`, `<tbody>`, `<tfoot>`

Pour des tableaux bien structurés, divisez-les en trois sections logiques :

### Structure complète

```html
<table>
    <caption>Ventes trimestrielles 2024</caption>

    <!-- En-tête du tableau -->
    <thead>
        <tr>
            <th scope="col">Trimestre</th>
            <th scope="col">Ventes</th>
            <th scope="col">Objectif</th>
        </tr>
    </thead>

    <!-- Corps du tableau -->
    <tbody>
        <tr>
            <th scope="row">T1</th>
            <td>120 000€</td>
            <td>100 000€</td>
        </tr>
        <tr>
            <th scope="row">T2</th>
            <td>145 000€</td>
            <td>120 000€</td>
        </tr>
        <tr>
            <th scope="row">T3</th>
            <td>168 000€</td>
            <td>150 000€</td>
        </tr>
    </tbody>

    <!-- Pied du tableau -->
    <tfoot>
        <tr>
            <th scope="row">Total</th>
            <td>433 000€</td>
            <td>370 000€</td>
        </tr>
    </tfoot>
</table>
```

### `<thead>` - En-tête du tableau

**Usage :** Contient les en-têtes de colonnes.

**Avantages :**
- Sémantique claire
- Peut être répété en haut de chaque page à l'impression
- Peut rester fixe lors du scroll (avec CSS)
- Améliore l'accessibilité

```html
<thead>
    <tr>
        <th scope="col">Colonne 1</th>
        <th scope="col">Colonne 2</th>
    </tr>
</thead>
```

**Note :** `<thead>` n'est pas obligatoire, mais **fortement recommandé** pour les tableaux avec en-têtes.

### `<tbody>` - Corps du tableau

**Usage :** Contient les données principales du tableau.

**Avantages :**
- Sépare clairement les données des en-têtes
- Permet de styliser différemment le corps
- Peut contenir plusieurs sections de données

```html
<tbody>
    <tr>
        <td>Donnée 1</td>
        <td>Donnée 2</td>
    </tr>
    <!-- Autres lignes -->
</tbody>
```

**Note :** Si vous ne mettez pas de `<tbody>`, le navigateur en crée un automatiquement (implicit tbody).

### `<tfoot>` - Pied du tableau

**Usage :** Contient les totaux, résumés ou notes de bas de tableau.

**Placement :** Peut être placé AVANT ou APRÈS `<tbody>` dans le code, mais s'affichera toujours en bas visuellement.

```html
<!-- Option 1 : tfoot après tbody (logique) -->
<table>
    <thead>...</thead>
    <tbody>...</tbody>
    <tfoot>
        <tr>
            <th scope="row">Total</th>
            <td>999€</td>
        </tr>
    </tfoot>
</table>

<!-- Option 2 : tfoot avant tbody (HTML5 accepte les deux) -->
<table>
    <thead>...</thead>
    <tfoot>
        <tr>
            <th scope="row">Total</th>
            <td>999€</td>
        </tr>
    </tfoot>
    <tbody>...</tbody>
</table>
```

**Avantage :** En le plaçant avant `<tbody>`, le navigateur peut l'afficher avant de charger toutes les lignes de données (utile pour de très grands tableaux).

---

## Exemple de tableau complet et accessible

Voici un tableau professionnel qui applique toutes les bonnes pratiques :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tableau accessible</title>
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 2rem 0;
            font-family: Arial, sans-serif;
        }

        caption {
            font-size: 1.3em;
            font-weight: bold;
            margin-bottom: 0.75rem;
            text-align: left;
            color: #2c3e50;
        }

        thead {
            background-color: #3498db;
            color: white;
        }

        th, td {
            padding: 12px 15px;
            text-align: left;
            border: 1px solid #ddd;
        }

        th {
            font-weight: 600;
        }

        tbody tr:nth-child(even) {
            background-color: #f8f9fa;
        }

        tbody tr:hover {
            background-color: #e3f2fd;
        }

        tfoot {
            background-color: #ecf0f1;
            font-weight: bold;
        }

        tfoot th {
            color: #2c3e50;
        }
    </style>
</head>
<body>
    <h1>Rapport de ventes</h1>

    <table>
        <caption>
            Résultats des ventes par région - Année 2024
        </caption>

        <thead>
            <tr>
                <th scope="col">Région</th>
                <th scope="col">T1</th>
                <th scope="col">T2</th>
                <th scope="col">T3</th>
                <th scope="col">T4</th>
                <th scope="col">Total</th>
            </tr>
        </thead>

        <tbody>
            <tr>
                <th scope="row">Île-de-France</th>
                <td>45 000€</td>
                <td>52 000€</td>
                <td>48 000€</td>
                <td>55 000€</td>
                <td>200 000€</td>
            </tr>
            <tr>
                <th scope="row">Auvergne-Rhône-Alpes</th>
                <td>38 000€</td>
                <td>42 000€</td>
                <td>45 000€</td>
                <td>50 000€</td>
                <td>175 000€</td>
            </tr>
            <tr>
                <th scope="row">Provence-Alpes-Côte d'Azur</th>
                <td>32 000€</td>
                <td>35 000€</td>
                <td>40 000€</td>
                <td>43 000€</td>
                <td>150 000€</td>
            </tr>
            <tr>
                <th scope="row">Nouvelle-Aquitaine</th>
                <td>28 000€</td>
                <td>30 000€</td>
                <td>33 000€</td>
                <td>35 000€</td>
                <td>126 000€</td>
            </tr>
        </tbody>

        <tfoot>
            <tr>
                <th scope="row">Total national</th>
                <td>143 000€</td>
                <td>159 000€</td>
                <td>166 000€</td>
                <td>183 000€</td>
                <td>651 000€</td>
            </tr>
        </tfoot>
    </table>
</body>
</html>
```

**Ce tableau est accessible car :**

1. ✅ **`<caption>`** : Titre clair du tableau
2. ✅ **`<thead>`, `<tbody>`, `<tfoot>`** : Structure sémantique
3. ✅ **`<th>` avec `scope`** : En-têtes explicites
4. ✅ **Présentation visuelle claire** : Bordures, couleurs alternées
5. ✅ **Responsive** : S'adapte à différentes largeurs

---

## Tableaux avec en-têtes sur deux axes

Certains tableaux ont des en-têtes à la fois en colonnes ET en lignes :

```html
<table>
    <caption>Horaire hebdomadaire</caption>
    <thead>
        <tr>
            <th scope="col">Heure</th>
            <th scope="col">Lundi</th>
            <th scope="col">Mardi</th>
            <th scope="col">Mercredi</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">9h - 10h</th>
            <td>Mathématiques</td>
            <td>Français</td>
            <td>Histoire</td>
        </tr>
        <tr>
            <th scope="row">10h - 11h</th>
            <td>Anglais</td>
            <td>Sciences</td>
            <td>Sport</td>
        </tr>
    </tbody>
</table>
```

**Structure :**
- `scope="col"` pour les en-têtes de colonnes (jours)
- `scope="row"` pour les en-têtes de lignes (heures)
- Les données (cours) sont dans `<td>`

**Lecteur d'écran annoncera :**
"Lundi, 9h - 10h : Mathématiques"

Contexte clair sur deux axes !

---

## Styling de base avec CSS

### Bordures

```css
/* Fusionner les bordures */
table {
    border-collapse: collapse;
}

/* Bordures sur cellules */
th, td {
    border: 1px solid #ddd;
}

/* Bordure externe du tableau */
table {
    border: 2px solid #333;
}
```

### Espacement

```css
/* Padding dans les cellules */
th, td {
    padding: 10px 15px;
}

/* Espacement entre le tableau et le reste */
table {
    margin: 2rem 0;
}
```

### Largeur

```css
/* Largeur fixe */
table {
    width: 800px;
}

/* Largeur responsive */
table {
    width: 100%;
    max-width: 1200px;
}

/* Largeur de colonnes spécifiques */
th:first-child,
td:first-child {
    width: 200px;
}
```

### Alignement du texte

```css
/* Alignement général */
th, td {
    text-align: left;
}

/* Nombres alignés à droite */
td.number {
    text-align: right;
}

/* Centrage */
th {
    text-align: center;
}
```

### Couleurs alternées (zebra striping)

```css
/* Lignes alternées dans tbody */
tbody tr:nth-child(odd) {
    background-color: #f9f9f9;
}

tbody tr:nth-child(even) {
    background-color: #ffffff;
}

/* Survol */
tbody tr:hover {
    background-color: #e3f2fd;
}
```

### Style d'en-tête

```css
thead {
    background-color: #3498db;
    color: white;
}

thead th {
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}
```

---

## Exemples pratiques

### Exemple 1 : Liste de produits

```html
<table>
    <caption>Catalogue de produits</caption>
    <thead>
        <tr>
            <th scope="col">Produit</th>
            <th scope="col">Catégorie</th>
            <th scope="col">Prix</th>
            <th scope="col">Stock</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Ordinateur portable Dell XPS</td>
            <td>Informatique</td>
            <td>1 299€</td>
            <td>En stock</td>
        </tr>
        <tr>
            <td>iPhone 15 Pro</td>
            <td>Téléphonie</td>
            <td>1 229€</td>
            <td>En stock</td>
        </tr>
        <tr>
            <td>AirPods Pro 2</td>
            <td>Audio</td>
            <td>279€</td>
            <td>Rupture</td>
        </tr>
    </tbody>
</table>
```

### Exemple 2 : Résultats sportifs

```html
<table>
    <caption>Classement Ligue 1 - Saison 2024/2025</caption>
    <thead>
        <tr>
            <th scope="col">Position</th>
            <th scope="col">Équipe</th>
            <th scope="col">Points</th>
            <th scope="col">Victoires</th>
            <th scope="col">Nuls</th>
            <th scope="col">Défaites</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">1</th>
            <td>PSG</td>
            <td>38</td>
            <td>12</td>
            <td>2</td>
            <td>0</td>
        </tr>
        <tr>
            <th scope="row">2</th>
            <td>Marseille</td>
            <td>35</td>
            <td>11</td>
            <td>2</td>
            <td>1</td>
        </tr>
        <tr>
            <th scope="row">3</th>
            <td>Monaco</td>
            <td>32</td>
            <td>10</td>
            <td>2</td>
            <td>2</td>
        </tr>
    </tbody>
</table>
```

### Exemple 3 : Comparaison de forfaits

```html
<table>
    <caption>Comparaison des forfaits internet</caption>
    <thead>
        <tr>
            <th scope="col">Caractéristique</th>
            <th scope="col">Essentiel</th>
            <th scope="col">Confort</th>
            <th scope="col">Premium</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Débit descendant</th>
            <td>100 Mb/s</td>
            <td>500 Mb/s</td>
            <td>1 Gb/s</td>
        </tr>
        <tr>
            <th scope="row">Débit montant</th>
            <td>50 Mb/s</td>
            <td>200 Mb/s</td>
            <td>500 Mb/s</td>
        </tr>
        <tr>
            <th scope="row">Téléphonie fixe</th>
            <td>✓ Incluse</td>
            <td>✓ Incluse</td>
            <td>✓ Incluse</td>
        </tr>
        <tr>
            <th scope="row">TV</th>
            <td>✗ Non</td>
            <td>✓ 100 chaînes</td>
            <td>✓ 200 chaînes</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th scope="row">Prix mensuel</th>
            <td>19,99€</td>
            <td>29,99€</td>
            <td>39,99€</td>
        </tr>
    </tfoot>
</table>
```

### Exemple 4 : Statistiques financières

```html
<table>
    <caption>Bilan financier annuel</caption>
    <thead>
        <tr>
            <th scope="col">Catégorie</th>
            <th scope="col">2022</th>
            <th scope="col">2023</th>
            <th scope="col">2024</th>
            <th scope="col">Évolution</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Chiffre d'affaires</th>
            <td>1 500 000€</td>
            <td>1 750 000€</td>
            <td>2 000 000€</td>
            <td>+33%</td>
        </tr>
        <tr>
            <th scope="row">Charges</th>
            <td>900 000€</td>
            <td>1 000 000€</td>
            <td>1 150 000€</td>
            <td>+28%</td>
        </tr>
        <tr>
            <th scope="row">Résultat net</th>
            <td>600 000€</td>
            <td>750 000€</td>
            <td>850 000€</td>
            <td>+42%</td>
        </tr>
    </tbody>
</table>
```

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Toujours ajouter un `<caption>`**
```html
<table>
    <caption>Description claire du tableau</caption>
    <!-- ... -->
</table>
```

2. **Utiliser `<th>` pour les en-têtes**
```html
<th scope="col">En-tête de colonne</th>
<th scope="row">En-tête de ligne</th>
```

3. **Ajouter l'attribut `scope` sur tous les `<th>`**
```html
<th scope="col">Colonne</th>
<th scope="row">Ligne</th>
```

4. **Structurer avec `<thead>`, `<tbody>`, `<tfoot>`**
```html
<table>
    <thead><!-- en-têtes --></thead>
    <tbody><!-- données --></tbody>
    <tfoot><!-- totaux --></tfoot>
</table>
```

5. **Styliser avec CSS, pas avec attributs HTML**
```html
<!-- ✅ BON -->
<table class="styled-table">

<!-- ❌ OBSOLÈTE -->
<table border="1" cellpadding="10">
```

### ❌ À ÉVITER

1. **Utiliser des tableaux pour la mise en page**
```html
<!-- ❌ MAUVAIS : pas des données tabulaires -->
<table>
    <tr>
        <td>Menu</td>
        <td>Contenu</td>
    </tr>
</table>
```

2. **Oublier `<caption>`**
```html
<!-- ❌ Moins accessible -->
<table>
    <tr>...</tr>
</table>

<!-- ✅ Accessible -->
<table>
    <caption>Titre du tableau</caption>
    <tr>...</tr>
</table>
```

3. **Utiliser `<td>` pour les en-têtes**
```html
<!-- ❌ MAUVAIS -->
<tr>
    <td><strong>Nom</strong></td>
    <td><strong>Âge</strong></td>
</tr>

<!-- ✅ BON -->
<tr>
    <th scope="col">Nom</th>
    <th scope="col">Âge</th>
</tr>
```

4. **Oublier l'attribut `scope`**
```html
<!-- ❌ Moins précis -->
<th>Nom</th>

<!-- ✅ Explicite -->
<th scope="col">Nom</th>
```

5. **Lignes avec nombre de cellules différent**
```html
<!-- ❌ MAUVAIS : structure incohérente -->
<tr>
    <td>A</td>
    <td>B</td>
    <td>C</td>
</tr>
<tr>
    <td>D</td>
    <td>E</td>
    <!-- Cellule manquante ! -->
</tr>
```

---

## Checklist d'accessibilité

Avant de publier un tableau, vérifiez :

- [ ] Le tableau a un `<caption>` descriptif
- [ ] Les en-têtes utilisent `<th>`, pas `<td>`
- [ ] Tous les `<th>` ont un attribut `scope` (col ou row)
- [ ] Le tableau est structuré avec `<thead>`, `<tbody>`, éventuellement `<tfoot>`
- [ ] Toutes les lignes ont le même nombre de cellules
- [ ] Le tableau contient réellement des données tabulaires
- [ ] Le style est fait en CSS, pas avec des attributs HTML obsolètes
- [ ] Le tableau est lisible sans CSS (structure HTML solide)
- [ ] Testé avec un lecteur d'écran si possible

---

## Points clés à retenir

1. **Les tableaux sont pour les données tabulaires**, pas la mise en page
2. **`<caption>` est essentiel** pour l'accessibilité
3. **`<th>` pour les en-têtes**, `<td>` pour les données
4. **`scope="col"` ou `scope="row"`** sur tous les `<th>`
5. **Structure sémantique** : `<thead>`, `<tbody>`, `<tfoot>`
6. **Toutes les lignes** doivent avoir le même nombre de cellules
7. **Style avec CSS**, pas avec attributs HTML
8. **Tester l'accessibilité** : peut-on comprendre le tableau sans le voir ?

---

## Prochaine étape

Maintenant que vous maîtrisez la structure de base des tableaux accessibles, nous allons découvrir dans le prochain chapitre comment **organiser les en-têtes avec `<thead>`, `<tbody>` et `<tfoot>`** de manière plus avancée, et comment créer des tableaux complexes avec plusieurs niveaux d'en-têtes.

⏭️ [En-têtes et organisation : thead, tbody, tfoot](/03-html5-structure-et-semantique/05-tableaux/02-entetes-et-organisation.md)
