🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.5.2 En-têtes et organisation : thead, tbody, tfoot

## Introduction

Dans le chapitre précédent, nous avons découvert la structure de base des tableaux. Maintenant, nous allons approfondir l'organisation des tableaux avec les trois sections principales : `<thead>`, `<tbody>` et `<tfoot>`.

Ces balises ne sont pas juste des conteneurs visuels : elles apportent une **structure sémantique forte** qui améliore considérablement l'accessibilité, la maintenance et les possibilités de style de vos tableaux.

Dans ce chapitre, nous allons explorer :
- L'utilisation détaillée de chaque section
- Comment organiser des tableaux complexes
- Les en-têtes multiples et hiérarchiques
- Les cas d'usage avancés
- Les avantages pour l'impression et le scroll

---

## Rappel : Les trois sections d'un tableau

Un tableau bien structuré est divisé en trois zones logiques :

```html
<table>
    <thead>  <!-- En-tête : titres des colonnes -->
    <tbody>  <!-- Corps : données principales -->
    <tfoot>  <!-- Pied : totaux, résumés, notes -->
</table>
```

**Analogie avec un document :**
- `<thead>` = En-tête de page (titre, colonnes)
- `<tbody>` = Contenu principal (paragraphes, données)
- `<tfoot>` = Pied de page (notes, totaux, signature)

---

## `<thead>` - L'en-tête du tableau

### Rôle et usage

`<thead>` contient les **en-têtes de colonnes** du tableau. C'est la première chose qu'un utilisateur lit pour comprendre la structure des données.

```html
<table>
    <thead>
        <tr>
            <th scope="col">Nom</th>
            <th scope="col">Âge</th>
            <th scope="col">Ville</th>
        </tr>
    </thead>
    <!-- tbody avec les données -->
</table>
```

### Pourquoi utiliser `<thead>` ?

#### 1. Sémantique claire

Le navigateur et les lecteurs d'écran comprennent que ces lignes sont des en-têtes, pas des données.

```html
<!-- ❌ Sans thead : moins clair -->
<table>
    <tr>
        <th>Nom</th>
        <th>Âge</th>
    </tr>
    <tr>
        <td>Alice</td>
        <td>25</td>
    </tr>
</table>

<!-- ✅ Avec thead : structure explicite -->
<table>
    <thead>
        <tr>
            <th scope="col">Nom</th>
            <th scope="col">Âge</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Alice</td>
            <td>25</td>
        </tr>
    </tbody>
</table>
```

#### 2. Styling indépendant

Vous pouvez facilement styliser l'en-tête différemment du corps :

```css
thead {
    background-color: #2c3e50;
    color: white;
    font-weight: bold;
}

tbody {
    background-color: white;
}
```

#### 3. En-tête fixe lors du scroll

Avec CSS, vous pouvez fixer l'en-tête en haut pendant que le corps défile :

```css
thead {
    position: sticky;
    top: 0;
    background-color: #2c3e50;
    z-index: 10;
}

tbody {
    display: block;
    max-height: 400px;
    overflow-y: auto;
}
```

**Résultat :** Les en-têtes restent visibles lors du scroll, pratique pour de longs tableaux !

#### 4. Répétition automatique à l'impression

Les navigateurs peuvent automatiquement répéter le `<thead>` en haut de chaque page imprimée :

```css
@media print {
    thead {
        display: table-header-group; /* Répété sur chaque page */
    }
}
```

### En-têtes sur plusieurs lignes

Un `<thead>` peut contenir plusieurs `<tr>` pour des en-têtes complexes :

```html
<table>
    <caption>Résultats trimestriels 2024</caption>
    <thead>
        <!-- Ligne 1 : Catégories principales -->
        <tr>
            <th scope="col" rowspan="2">Région</th>
            <th scope="colgroup" colspan="3">Ventes (K€)</th>
            <th scope="colgroup" colspan="3">Objectifs (K€)</th>
        </tr>
        <!-- Ligne 2 : Sous-catégories -->
        <tr>
            <th scope="col">T1</th>
            <th scope="col">T2</th>
            <th scope="col">T3</th>
            <th scope="col">T1</th>
            <th scope="col">T2</th>
            <th scope="col">T3</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Paris</th>
            <td>120</td>
            <td>145</td>
            <td>168</td>
            <td>100</td>
            <td>130</td>
            <td>150</td>
        </tr>
    </tbody>
</table>
```

**Résultat visuel :**
```
┌────────┬─────────────────┬─────────────────┐
│ Région │   Ventes (K€)   │ Objectifs (K€)  │
│        ├─────┬─────┬─────┼─────┬─────┬─────┤
│        │ T1  │ T2  │ T3  │ T1  │ T2  │ T3  │
├────────┼─────┼─────┼─────┼─────┼─────┼─────┤
│ Paris  │ 120 │ 145 │ 168 │ 100 │ 130 │ 150 │
└────────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

*Note : `rowspan` et `colspan` seront détaillés dans le chapitre 3.5.3*

---

## `<tbody>` - Le corps du tableau

### Rôle et usage

`<tbody>` contient les **données principales** du tableau. C'est le cœur de votre tableau.

```html
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
        <tr>
            <td>Souris</td>
            <td>29€</td>
        </tr>
        <tr>
            <td>Clavier</td>
            <td>79€</td>
        </tr>
    </tbody>
</table>
```

### Tbody implicite

**Important :** Si vous ne mettez pas de balise `<tbody>`, le navigateur en créera une automatiquement !

```html
<!-- Code source -->
<table>
    <tr>
        <td>Données</td>
    </tr>
</table>

<!-- Ce que voit le navigateur -->
<table>
    <tbody>  <!-- Créé automatiquement -->
        <tr>
            <td>Données</td>
        </tr>
    </tbody>
</table>
```

**Recommandation :** Écrivez toujours `<tbody>` explicitement pour plus de clarté et de contrôle.

### Plusieurs tbody dans un tableau

Vous pouvez avoir **plusieurs `<tbody>`** dans un même tableau pour grouper des données :

```html
<table>
    <caption>Ventes par région et par mois</caption>
    <thead>
        <tr>
            <th scope="col">Mois</th>
            <th scope="col">Ventes</th>
        </tr>
    </thead>

    <!-- Groupe 1 : Région Nord -->
    <tbody>
        <tr>
            <th colspan="2" scope="colgroup">Région Nord</th>
        </tr>
        <tr>
            <th scope="row">Janvier</th>
            <td>45 000€</td>
        </tr>
        <tr>
            <th scope="row">Février</th>
            <td>52 000€</td>
        </tr>
    </tbody>

    <!-- Groupe 2 : Région Sud -->
    <tbody>
        <tr>
            <th colspan="2" scope="colgroup">Région Sud</th>
        </tr>
        <tr>
            <th scope="row">Janvier</th>
            <td>38 000€</td>
        </tr>
        <tr>
            <th scope="row">Février</th>
            <td>41 000€</td>
        </tr>
    </tbody>
</table>
```

**Avantages :**
- Groupement logique des données
- Styling distinct pour chaque groupe
- Meilleure lisibilité

```css
/* Style différent pour chaque tbody */
tbody:nth-of-type(1) {
    background-color: #e3f2fd;
}

tbody:nth-of-type(2) {
    background-color: #fff3e0;
}

/* Espacement entre les tbody */
tbody + tbody {
    border-top: 3px solid #333;
}
```

### Styling des lignes dans tbody

```css
/* Lignes alternées (zebra striping) */
tbody tr:nth-child(odd) {
    background-color: #f9f9f9;
}

tbody tr:nth-child(even) {
    background-color: #ffffff;
}

/* Survol */
tbody tr:hover {
    background-color: #e3f2fd;
    cursor: pointer;
}

/* Première ligne en gras */
tbody tr:first-child {
    font-weight: bold;
}

/* Dernière ligne avec bordure */
tbody tr:last-child {
    border-bottom: 2px solid #333;
}
```

---

## `<tfoot>` - Le pied du tableau

### Rôle et usage

`<tfoot>` contient les **totaux, résumés, moyennes** ou notes de bas de tableau.

```html
<table>
    <thead>
        <tr>
            <th scope="col">Produit</th>
            <th scope="col">Quantité</th>
            <th scope="col">Prix unitaire</th>
            <th scope="col">Total</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Ordinateur</td>
            <td>2</td>
            <td>899€</td>
            <td>1 798€</td>
        </tr>
        <tr>
            <td>Souris</td>
            <td>5</td>
            <td>29€</td>
            <td>145€</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th scope="row" colspan="3">Total général</th>
            <td>1 943€</td>
        </tr>
    </tfoot>
</table>
```

### Position dans le code HTML

**HTML5 accepte deux positions pour `<tfoot>` :**

#### Option 1 : Après `<tbody>` (logique et recommandée)

```html
<table>
    <thead>...</thead>
    <tbody>...</tbody>
    <tfoot>...</tfoot>  <!-- Après tbody -->
</table>
```

**Avantage :** L'ordre dans le code reflète l'ordre visuel.

#### Option 2 : Avant `<tbody>` (ancienne spécification)

```html
<table>
    <thead>...</thead>
    <tfoot>...</tfoot>  <!-- Avant tbody -->
    <tbody>...</tbody>
</table>
```

**Avantage :** Le navigateur peut afficher le pied avant de charger toutes les données (utile pour de très grands tableaux).

**⚠️ Important :** Quelle que soit sa position dans le code, `<tfoot>` s'affichera **toujours en bas** visuellement !

### Quand utiliser tfoot ?

**✅ Utilisez tfoot pour :**

**Totaux et sommes :**
```html
<tfoot>
    <tr>
        <th scope="row">Total</th>
        <td>1 250€</td>
    </tr>
</tfoot>
```

**Moyennes :**
```html
<tfoot>
    <tr>
        <th scope="row">Moyenne</th>
        <td>15.7/20</td>
    </tr>
</tfoot>
```

**Notes de bas de tableau :**
```html
<tfoot>
    <tr>
        <td colspan="3">
            * Prix TTC incluant 20% de TVA
        </td>
    </tr>
</tfoot>
```

**Résumé :**
```html
<tfoot>
    <tr>
        <th scope="row">Statistiques</th>
        <td colspan="2">42 entrées sur 3 pages</td>
    </tr>
</tfoot>
```

### ❌ N'utilisez pas tfoot pour :

- De simples lignes de données (utilisez tbody)
- Des informations qui ne résument pas le tableau
- Du contenu qui devrait être dans caption

### Styling de tfoot

```css
tfoot {
    background-color: #ecf0f1;
    font-weight: bold;
    border-top: 3px solid #34495e;
}

tfoot th {
    text-align: right;
    padding-right: 1rem;
}

tfoot td {
    font-size: 1.1em;
    color: #2c3e50;
}
```

---

## Organisation complète d'un tableau

Voici un exemple complet qui utilise toutes les sections :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tableau organisé</title>
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 2rem 0;
            font-family: Arial, sans-serif;
        }

        caption {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 1rem;
            text-align: left;
            color: #2c3e50;
        }

        thead {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        thead th {
            padding: 15px;
            text-align: left;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        tbody tr {
            border-bottom: 1px solid #ddd;
        }

        tbody tr:nth-child(odd) {
            background-color: #f8f9fa;
        }

        tbody tr:hover {
            background-color: #e3f2fd;
            transition: background-color 0.3s ease;
        }

        tbody td,
        tbody th {
            padding: 12px 15px;
        }

        tbody th {
            text-align: left;
            font-weight: 600;
            color: #495057;
        }

        tfoot {
            background-color: #2c3e50;
            color: white;
            font-weight: bold;
        }

        tfoot th,
        tfoot td {
            padding: 15px;
        }

        tfoot th {
            text-align: left;
        }

        tfoot td {
            font-size: 1.2em;
        }

        /* Alignement des nombres à droite */
        td.number {
            text-align: right;
            font-variant-numeric: tabular-nums;
        }
    </style>
</head>
<body>
    <table>
        <caption>
            Rapport de ventes mensuelles - Année 2024
        </caption>

        <!-- EN-TÊTE : Titres des colonnes -->
        <thead>
            <tr>
                <th scope="col">Mois</th>
                <th scope="col">Ventes (unités)</th>
                <th scope="col">Chiffre d'affaires</th>
                <th scope="col">Objectif</th>
                <th scope="col">Atteinte</th>
            </tr>
        </thead>

        <!-- CORPS : Données principales -->
        <tbody>
            <tr>
                <th scope="row">Janvier</th>
                <td class="number">1 250</td>
                <td class="number">45 000€</td>
                <td class="number">40 000€</td>
                <td class="number">112,5%</td>
            </tr>
            <tr>
                <th scope="row">Février</th>
                <td class="number">1 380</td>
                <td class="number">52 000€</td>
                <td class="number">45 000€</td>
                <td class="number">115,6%</td>
            </tr>
            <tr>
                <th scope="row">Mars</th>
                <td class="number">1 520</td>
                <td class="number">58 000€</td>
                <td class="number">50 000€</td>
                <td class="number">116,0%</td>
            </tr>
            <tr>
                <th scope="row">Avril</th>
                <td class="number">1 410</td>
                <td class="number">54 000€</td>
                <td class="number">48 000€</td>
                <td class="number">112,5%</td>
            </tr>
            <tr>
                <th scope="row">Mai</th>
                <td class="number">1 680</td>
                <td class="number">63 000€</td>
                <td class="number">55 000€</td>
                <td class="number">114,5%</td>
            </tr>
            <tr>
                <th scope="row">Juin</th>
                <td class="number">1 760</td>
                <td class="number">68 000€</td>
                <td class="number">60 000€</td>
                <td class="number">113,3%</td>
            </tr>
        </tbody>

        <!-- PIED : Totaux et moyennes -->
        <tfoot>
            <tr>
                <th scope="row">Total / Moyenne</th>
                <td class="number">9 000 unités</td>
                <td class="number">340 000€</td>
                <td class="number">298 000€</td>
                <td class="number">114,1%</td>
            </tr>
        </tfoot>
    </table>
</body>
</html>
```

**Ce tableau démontre :**
- ✅ Structure complète (caption, thead, tbody, tfoot)
- ✅ En-têtes de colonnes (`<th scope="col">`)
- ✅ En-têtes de lignes (`<th scope="row">`)
- ✅ Données alignées à droite pour les nombres
- ✅ Styling différencié pour chaque section
- ✅ Lignes alternées dans tbody
- ✅ Effet de survol
- ✅ Totaux dans tfoot

---

## Tableaux complexes avec sections multiples

### Exemple : Tableau avec sous-totaux

```html
<table>
    <caption>Ventes par catégorie de produits - T1 2024</caption>

    <thead>
        <tr>
            <th scope="col">Produit</th>
            <th scope="col">Quantité</th>
            <th scope="col">Prix unitaire</th>
            <th scope="col">Total</th>
        </tr>
    </thead>

    <!-- Catégorie 1 : Électronique -->
    <tbody>
        <tr>
            <th colspan="4" scope="colgroup">ÉLECTRONIQUE</th>
        </tr>
        <tr>
            <td>Ordinateur portable</td>
            <td>15</td>
            <td>899€</td>
            <td>13 485€</td>
        </tr>
        <tr>
            <td>Smartphone</td>
            <td>32</td>
            <td>699€</td>
            <td>22 368€</td>
        </tr>
        <tr>
            <td>Tablette</td>
            <td>18</td>
            <td>449€</td>
            <td>8 082€</td>
        </tr>
        <tr>
            <th colspan="3">Sous-total Électronique</th>
            <td><strong>43 935€</strong></td>
        </tr>
    </tbody>

    <!-- Catégorie 2 : Accessoires -->
    <tbody>
        <tr>
            <th colspan="4" scope="colgroup">ACCESSOIRES</th>
        </tr>
        <tr>
            <td>Souris sans fil</td>
            <td>45</td>
            <td>29€</td>
            <td>1 305€</td>
        </tr>
        <tr>
            <td>Clavier mécanique</td>
            <td>28</td>
            <td>79€</td>
            <td>2 212€</td>
        </tr>
        <tr>
            <td>Casque audio</td>
            <td>35</td>
            <td>99€</td>
            <td>3 465€</td>
        </tr>
        <tr>
            <th colspan="3">Sous-total Accessoires</th>
            <td><strong>6 982€</strong></td>
        </tr>
    </tbody>

    <!-- Total général -->
    <tfoot>
        <tr>
            <th colspan="3">TOTAL GÉNÉRAL</th>
            <td><strong>50 917€</strong></td>
        </tr>
    </tfoot>
</table>
```

**Avantages de cette structure :**
- Groupement clair par catégorie
- Sous-totaux intermédiaires
- Total général dans tfoot
- Facile à styliser différemment chaque section

```css
/* Titres de catégories */
tbody tr:first-child th {
    background-color: #34495e;
    color: white;
    padding: 10px;
    text-align: left;
}

/* Lignes de sous-totaux */
tbody tr:last-child {
    background-color: #ecf0f1;
    font-weight: bold;
    border-top: 2px solid #95a5a6;
}

/* Espacement entre les tbody */
tbody + tbody {
    border-top: 3px double #2c3e50;
}
```

---

## En-têtes avec hiérarchie

Pour des tableaux complexes avec plusieurs niveaux d'en-têtes :

```html
<table>
    <caption>Performance commerciale - 2024</caption>
    <thead>
        <!-- Niveau 1 : Grandes catégories -->
        <tr>
            <th scope="col" rowspan="2">Région</th>
            <th scope="colgroup" colspan="4">Semestre 1</th>
            <th scope="colgroup" colspan="4">Semestre 2</th>
            <th scope="col" rowspan="2">Total annuel</th>
        </tr>
        <!-- Niveau 2 : Détails par trimestre -->
        <tr>
            <th scope="col">T1</th>
            <th scope="col">T2</th>
            <th scope="col">Obj.</th>
            <th scope="col">%</th>
            <th scope="col">T3</th>
            <th scope="col">T4</th>
            <th scope="col">Obj.</th>
            <th scope="col">%</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Paris</th>
            <td>120K€</td>
            <td>145K€</td>
            <td>250K€</td>
            <td>106%</td>
            <td>168K€</td>
            <td>195K€</td>
            <td>300K€</td>
            <td>121%</td>
            <td>628K€</td>
        </tr>
        <tr>
            <th scope="row">Lyon</th>
            <td>95K€</td>
            <td>110K€</td>
            <td>200K€</td>
            <td>102%</td>
            <td>125K€</td>
            <td>142K€</td>
            <td>250K€</td>
            <td>107%</td>
            <td>472K€</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th scope="row">Total national</th>
            <td>215K€</td>
            <td>255K€</td>
            <td>450K€</td>
            <td>104%</td>
            <td>293K€</td>
            <td>337K€</td>
            <td>550K€</td>
            <td>115%</td>
            <td>1 100K€</td>
        </tr>
    </tfoot>
</table>
```

**Attributs importants :**
- `scope="colgroup"` : L'en-tête décrit un groupe de colonnes
- `rowspan="2"` : L'en-tête s'étend sur 2 lignes
- `colspan="4"` : L'en-tête s'étend sur 4 colonnes

*Note : Nous détaillerons colspan et rowspan dans le chapitre 3.5.3*

---

## Tableaux scrollables avec en-tête fixe

Pour de longs tableaux, vous pouvez fixer l'en-tête pendant le scroll :

```html
<div class="table-container">
    <table>
        <thead>
            <tr>
                <th>Colonne 1</th>
                <th>Colonne 2</th>
                <th>Colonne 3</th>
            </tr>
        </thead>
        <tbody>
            <!-- 50+ lignes de données -->
        </tbody>
    </table>
</div>
```

```css
.table-container {
    max-height: 400px;
    overflow-y: auto;
    position: relative;
}

table {
    width: 100%;
    border-collapse: collapse;
}

thead {
    position: sticky;
    top: 0;
    background-color: #2c3e50;
    color: white;
    z-index: 10;
}

thead th {
    padding: 15px;
    border-bottom: 2px solid #34495e;
}

tbody td {
    padding: 12px 15px;
    border-bottom: 1px solid #ddd;
}
```

**Résultat :** L'en-tête reste visible en haut même quand vous scrollez les données !

---

## Impression et pagination

### Répétition des en-têtes à l'impression

Les sections `<thead>` et `<tfoot>` peuvent être répétées sur chaque page imprimée :

```css
@media print {
    thead {
        display: table-header-group;
    }

    tfoot {
        display: table-footer-group;
    }

    tbody {
        display: table-row-group;
    }

    /* Éviter les coupures de page au milieu des lignes */
    tr {
        page-break-inside: avoid;
    }
}
```

**Comportement :**
- `<thead>` apparaît en haut de chaque page
- `<tfoot>` apparaît en bas de chaque page
- Les données (`<tbody>`) se répartissent entre les pages

---

## Exemples pratiques avancés

### Exemple 1 : Tableau financier complet

```html
<table>
    <caption>
        Bilan financier annuel - Société XYZ
        <small>Montants en milliers d'euros</small>
    </caption>

    <thead>
        <tr>
            <th scope="col">Poste</th>
            <th scope="col">2022</th>
            <th scope="col">2023</th>
            <th scope="col">2024</th>
            <th scope="col">Évolution 24/23</th>
        </tr>
    </thead>

    <!-- Actifs -->
    <tbody>
        <tr>
            <th colspan="5" scope="colgroup">ACTIF</th>
        </tr>
        <tr>
            <th scope="row">Immobilisations</th>
            <td>2 500</td>
            <td>2 800</td>
            <td>3 200</td>
            <td>+14,3%</td>
        </tr>
        <tr>
            <th scope="row">Stocks</th>
            <td>450</td>
            <td>520</td>
            <td>580</td>
            <td>+11,5%</td>
        </tr>
        <tr>
            <th scope="row">Créances clients</th>
            <td>680</td>
            <td>750</td>
            <td>820</td>
            <td>+9,3%</td>
        </tr>
        <tr>
            <th scope="row">Disponibilités</th>
            <td>370</td>
            <td>430</td>
            <td>500</td>
            <td>+16,3%</td>
        </tr>
        <tr class="subtotal">
            <th scope="row">Total Actif</th>
            <td>4 000</td>
            <td>4 500</td>
            <td>5 100</td>
            <td>+13,3%</td>
        </tr>
    </tbody>

    <!-- Passifs -->
    <tbody>
        <tr>
            <th colspan="5" scope="colgroup">PASSIF</th>
        </tr>
        <tr>
            <th scope="row">Capitaux propres</th>
            <td>2 200</td>
            <td>2 600</td>
            <td>3 100</td>
            <td>+19,2%</td>
        </tr>
        <tr>
            <th scope="row">Dettes long terme</th>
            <td>1 200</td>
            <td>1 300</td>
            <td>1 400</td>
            <td>+7,7%</td>
        </tr>
        <tr>
            <th scope="row">Dettes court terme</th>
            <td>600</td>
            <td>600</td>
            <td>600</td>
            <td>0%</td>
        </tr>
        <tr class="subtotal">
            <th scope="row">Total Passif</th>
            <td>4 000</td>
            <td>4 500</td>
            <td>5 100</td>
            <td>+13,3%</td>
        </tr>
    </tbody>

    <tfoot>
        <tr>
            <td colspan="5">
                <small>* Données auditées par cabinet comptable XYZ</small>
            </td>
        </tr>
    </tfoot>
</table>
```

### Exemple 2 : Planning horaire hebdomadaire

```html
<table>
    <caption>Emploi du temps - Classe de 3ème A</caption>

    <thead>
        <tr>
            <th scope="col">Horaire</th>
            <th scope="col">Lundi</th>
            <th scope="col">Mardi</th>
            <th scope="col">Mercredi</th>
            <th scope="col">Jeudi</th>
            <th scope="col">Vendredi</th>
        </tr>
    </thead>

    <!-- Matinée -->
    <tbody>
        <tr>
            <th colspan="6" scope="colgroup">MATINÉE</th>
        </tr>
        <tr>
            <th scope="row">8h - 9h</th>
            <td>Mathématiques<br><small>Salle 201</small></td>
            <td>Français<br><small>Salle 105</small></td>
            <td>Anglais<br><small>Salle 302</small></td>
            <td>Histoire-Géo<br><small>Salle 108</small></td>
            <td>Sciences<br><small>Lab 2</small></td>
        </tr>
        <tr>
            <th scope="row">9h - 10h</th>
            <td>Mathématiques<br><small>Salle 201</small></td>
            <td>EPS<br><small>Gymnase</small></td>
            <td>Français<br><small>Salle 105</small></td>
            <td>Anglais<br><small>Salle 302</small></td>
            <td>Arts plastiques<br><small>Salle 401</small></td>
        </tr>
        <tr>
            <th scope="row">10h15 - 11h15</th>
            <td>Physique-Chimie<br><small>Lab 1</small></td>
            <td>Mathématiques<br><small>Salle 201</small></td>
            <td>Étude</td>
            <td>Musique<br><small>Salle 501</small></td>
            <td>Technologie<br><small>Salle Tech</small></td>
        </tr>
    </tbody>

    <!-- Après-midi -->
    <tbody>
        <tr>
            <th colspan="6" scope="colgroup">APRÈS-MIDI</th>
        </tr>
        <tr>
            <th scope="row">13h30 - 14h30</th>
            <td>SVT<br><small>Lab 3</small></td>
            <td>Histoire-Géo<br><small>Salle 108</small></td>
            <td rowspan="2" style="vertical-align: middle; background-color: #e8f5e9;">
                <strong>Libre</strong>
            </td>
            <td>Français<br><small>Salle 105</small></td>
            <td>EPS<br><small>Gymnase</small></td>
        </tr>
        <tr>
            <th scope="row">14h30 - 15h30</th>
            <td>Espagnol<br><small>Salle 303</small></td>
            <td>Technologie<br><small>Salle Tech</small></td>
            <td>SVT<br><small>Lab 3</small></td>
            <td>EPS<br><small>Gymnase</small></td>
        </tr>
    </tbody>

    <tfoot>
        <tr>
            <td colspan="6">
                <small>Dernière mise à jour : 03/12/2024</small>
            </td>
        </tr>
    </tfoot>
</table>
```

---

## Accessibilité : Récapitulatif des bonnes pratiques

### Checklist pour thead, tbody, tfoot

- [ ] **Toujours utiliser `<thead>`** pour les en-têtes de colonnes
- [ ] **Toujours utiliser `<tbody>`** explicitement (même si implicite)
- [ ] **Utiliser `<tfoot>`** pour les totaux, résumés, notes
- [ ] **Tous les `<th>` ont un `scope`** approprié (col, row, colgroup)
- [ ] **Les en-têtes complexes** utilisent rowspan/colspan avec scope approprié
- [ ] **Caption présent** pour décrire le tableau
- [ ] **Structure logique** : thead → tbody → tfoot (ou thead → tfoot → tbody)

### Test d'accessibilité

**Questions à se poser :**

1. Si j'écoute ce tableau avec un lecteur d'écran, puis-je comprendre la structure ?
2. Les en-têtes sont-ils clairement identifiés ?
3. Puis-je comprendre à quoi correspond chaque donnée ?
4. Les totaux sont-ils clairement séparés des données ?

**Si la réponse est "non" à l'une de ces questions, revoyez votre structure !**

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Structure complète pour tableaux complexes**
```html
<table>
    <caption>Titre</caption>
    <thead><!-- En-têtes --></thead>
    <tbody><!-- Données --></tbody>
    <tfoot><!-- Totaux --></tfoot>
</table>
```

2. **Écrire tbody explicitement**
```html
<!-- ✅ BON : tbody explicite -->
<tbody>
    <tr>...</tr>
</tbody>

<!-- ⚠️ Éviter : tbody implicite -->
<table>
    <tr>...</tr>
</table>
```

3. **Utiliser plusieurs tbody pour grouper**
```html
<tbody><!-- Groupe 1 --></tbody>
<tbody><!-- Groupe 2 --></tbody>
```

4. **Placer tfoot logiquement**
```html
<!-- ✅ Recommandé : après tbody -->
<thead>...</thead>
<tbody>...</tbody>
<tfoot>...</tfoot>
```

5. **En-têtes hiérarchiques avec scope approprié**
```html
<th scope="colgroup" colspan="3">Groupe</th>
```

### ❌ À ÉVITER

1. **Oublier les sections pour tableaux complexes**
```html
<!-- ❌ MAUVAIS : tout mélangé -->
<table>
    <tr><th>En-tête</th></tr>
    <tr><td>Donnée</td></tr>
    <tr><th>Total</th></tr>
</table>
```

2. **Utiliser div ou span dans thead/tbody/tfoot**
```html
<!-- ❌ MAUVAIS : div inutile -->
<tbody>
    <div>
        <tr>...</tr>
    </div>
</tbody>

<!-- ✅ BON -->
<tbody>
    <tr>...</tr>
</tbody>
```

3. **Mélanger données et totaux dans le même tbody**
```html
<!-- ❌ Moins clair -->
<tbody>
    <tr><td>Donnée 1</td></tr>
    <tr><td>Donnée 2</td></tr>
    <tr><th>Total</th></tr>  <!-- Devrait être dans tfoot -->
</tbody>
```

4. **En-têtes sans scope**
```html
<!-- ❌ MAUVAIS -->
<thead>
    <tr>
        <th>Colonne</th>
    </tr>
</thead>

<!-- ✅ BON -->
<thead>
    <tr>
        <th scope="col">Colonne</th>
    </tr>
</thead>
```

---

## Points clés à retenir

1. **`<thead>` contient les en-têtes** de colonnes
2. **`<tbody>` contient les données** principales
3. **`<tfoot>` contient les totaux** et résumés
4. **Plusieurs `<tbody>` possibles** pour grouper les données
5. **`<tfoot>` s'affiche toujours en bas** quelle que soit sa position dans le code
6. **Structure sémantique forte** améliore accessibilité et SEO
7. **En-têtes fixes possibles** avec CSS position: sticky
8. **Répétition automatique** à l'impression avec display: table-header-group
9. **Tous les `<th>` doivent avoir `scope`** (col, row, colgroup)
10. **Organisation claire = tableau accessible**

---

## Prochaine étape

Maintenant que vous maîtrisez l'organisation des tableaux avec thead, tbody et tfoot, nous allons découvrir dans le prochain chapitre comment **fusionner des cellules** avec les attributs `colspan` et `rowspan`, et comment créer des tableaux encore plus complexes et expressifs.

⏭️ [Cellules et attributs de fusion](/03-html5-structure-et-semantique/05-tableaux/03-cellules-et-fusion.md)
