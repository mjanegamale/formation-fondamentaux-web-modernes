🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.5.3 Cellules et attributs de fusion

## Introduction

Parfois, vous avez besoin qu'une cellule s'étende sur **plusieurs colonnes** ou **plusieurs lignes** pour créer des tableaux plus complexes et expressifs. HTML offre deux attributs puissants pour cela :

- **`colspan`** : Fusionne des cellules **horizontalement** (sur plusieurs colonnes)
- **`rowspan`** : Fusionne des cellules **verticalement** (sur plusieurs lignes)

Ces attributs permettent de créer des tableaux sophistiqués comme :
- Tableaux avec en-têtes groupés
- Plannings horaires
- Tableaux de comparaison
- Factures et devis
- Tableaux hiérarchiques

Dans ce chapitre, nous allons maîtriser ces deux attributs avec de nombreux exemples visuels pour comprendre leur fonctionnement.

---

## `colspan` - Fusion horizontale (colonnes)

### Qu'est-ce que colspan ?

L'attribut `colspan` (column span) permet à une cellule de **s'étendre sur plusieurs colonnes**.

**Syntaxe :**
```html
<td colspan="3">Cette cellule occupe 3 colonnes</td>
```

### Exemple simple

```html
<table border="1">
    <tr>
        <td colspan="3">Cellule qui s'étend sur 3 colonnes</td>
    </tr>
    <tr>
        <td>Colonne 1</td>
        <td>Colonne 2</td>
        <td>Colonne 3</td>
    </tr>
</table>
```

**Résultat visuel :**
```
┌─────────────────────────────────────┐
│  Cellule sur 3 colonnes             │
├───────────┬───────────┬─────────────┤
│ Colonne 1 │ Colonne 2 │ Colonne 3   │
└───────────┴───────────┴─────────────┘
```

### Comment ça fonctionne ?

Sans `colspan`, un tableau à 3 colonnes nécessite 3 cellules par ligne :

```html
<!-- Ligne normale : 3 cellules -->
<tr>
    <td>A</td>
    <td>B</td>
    <td>C</td>
</tr>
```

Avec `colspan="3"`, une seule cellule remplace les 3 :

```html
<!-- Ligne avec colspan : 1 cellule qui vaut 3 -->
<tr>
    <td colspan="3">ABC fusionnés</td>
</tr>
```

**Règle importante :** Le nombre total de colonnes doit rester constant dans tout le tableau.

### Exemple : En-tête de tableau groupé

```html
<table>
    <caption>Ventes trimestrielles 2024</caption>
    <thead>
        <tr>
            <th scope="col" rowspan="2">Région</th>
            <th scope="colgroup" colspan="3">Semestre 1</th>
            <th scope="colgroup" colspan="3">Semestre 2</th>
        </tr>
        <tr>
            <th scope="col">T1</th>
            <th scope="col">T2</th>
            <th scope="col">Total</th>
            <th scope="col">T3</th>
            <th scope="col">T4</th>
            <th scope="col">Total</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Paris</th>
            <td>120K€</td>
            <td>145K€</td>
            <td>265K€</td>
            <td>168K€</td>
            <td>195K€</td>
            <td>363K€</td>
        </tr>
    </tbody>
</table>
```

**Structure visuelle :**
```
┌────────┬─────────────────────────┬─────────────────────────┐
│ Région │    Semestre 1           │    Semestre 2           │
│        ├─────┬─────┬─────────────┼─────┬─────┬─────────────┤
│        │ T1  │ T2  │ Total       │ T3  │ T4  │ Total       │
├────────┼─────┼─────┼─────────────┼─────┼─────┼─────────────┤
│ Paris  │120K │145K │ 265K        │168K │195K │ 363K        │
└────────┴─────┴─────┴─────────────┴─────┴─────┴─────────────┘
```

**Explication :**
- "Semestre 1" s'étend sur 3 colonnes (`colspan="3"`)
- "Semestre 2" s'étend sur 3 colonnes (`colspan="3"`)
- La ligne suivante a 6 cellules individuelles (3 + 3)

### Cas d'usage courants de colspan

#### 1. Titres de sections dans un tableau

```html
<table>
    <thead>
        <tr>
            <th scope="col">Produit</th>
            <th scope="col">Quantité</th>
            <th scope="col">Prix</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th colspan="3" scope="colgroup">ÉLECTRONIQUE</th>
        </tr>
        <tr>
            <td>Ordinateur</td>
            <td>5</td>
            <td>899€</td>
        </tr>
        <tr>
            <td>Smartphone</td>
            <td>12</td>
            <td>699€</td>
        </tr>
        <tr>
            <th colspan="3" scope="colgroup">ACCESSOIRES</th>
        </tr>
        <tr>
            <td>Souris</td>
            <td>25</td>
            <td>29€</td>
        </tr>
    </tbody>
</table>
```

#### 2. Ligne de total

```html
<tfoot>
    <tr>
        <th colspan="2" scope="row">Total général</th>
        <td>1 527€</td>
    </tr>
</tfoot>
```

**Résultat :**
```
┌─────────────────────────┬─────────────┐
│ Total général           │   1 527€    │
└─────────────────────────┴─────────────┘
```

#### 3. Notes de bas de tableau

```html
<tfoot>
    <tr>
        <td colspan="5">
            * Prix TTC incluant 20% de TVA. Frais de port offerts dès 50€ d'achat.
        </td>
    </tr>
</tfoot>
```

---

## `rowspan` - Fusion verticale (lignes)

### Qu'est-ce que rowspan ?

L'attribut `rowspan` (row span) permet à une cellule de **s'étendre sur plusieurs lignes**.

**Syntaxe :**
```html
<td rowspan="3">Cette cellule occupe 3 lignes</td>
```

### Exemple simple

```html
<table border="1">
    <tr>
        <td rowspan="3">Cellule sur 3 lignes</td>
        <td>Ligne 1, Colonne 2</td>
    </tr>
    <tr>
        <td>Ligne 2, Colonne 2</td>
    </tr>
    <tr>
        <td>Ligne 3, Colonne 2</td>
    </tr>
</table>
```

**Résultat visuel :**
```
┌──────────────────┬──────────────────┐
│                  │ Ligne 1, Col 2   │
│  Cellule sur     ├──────────────────┤
│    3 lignes      │ Ligne 2, Col 2   │
│                  ├──────────────────┤
│                  │ Ligne 3, Col 2   │
└──────────────────┴──────────────────┘
```

### Comment ça fonctionne ?

Sans `rowspan`, chaque ligne a ses propres cellules :

```html
<tr>
    <td>A</td>
    <td>B</td>
</tr>
<tr>
    <td>C</td>
    <td>D</td>
</tr>
```

Avec `rowspan="2"`, la première cellule s'étend sur 2 lignes :

```html
<tr>
    <td rowspan="2">A+C fusionnés</td>
    <td>B</td>
</tr>
<tr>
    <!-- Pas de première cellule ici ! Elle vient de la ligne précédente -->
    <td>D</td>
</tr>
```

**⚠️ Point crucial :** Quand vous utilisez `rowspan`, les lignes suivantes ont **moins de cellules** car certaines sont "prises" par le rowspan.

### Exemple : Emploi du temps

```html
<table>
    <caption>Planning hebdomadaire</caption>
    <thead>
        <tr>
            <th scope="col">Jour</th>
            <th scope="col">Matin</th>
            <th scope="col">Après-midi</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row" rowspan="2">Lundi</th>
            <td>9h-12h : Mathématiques</td>
            <td>14h-16h : Sport</td>
        </tr>
        <tr>
            <!-- Pas de cellule "Jour" ici, elle vient de la ligne précédente -->
            <td colspan="2">16h-18h : Projet de groupe</td>
        </tr>
        <tr>
            <th scope="row">Mardi</th>
            <td>9h-12h : Français</td>
            <td>14h-17h : Sciences</td>
        </tr>
    </tbody>
</table>
```

**Structure visuelle :**
```
┌────────┬────────────────────┬─────────────────────┐
│  Jour  │      Matin         │    Après-midi       │
├────────┼────────────────────┼─────────────────────┤
│        │ 9h-12h : Maths     │ 14h-16h : Sport     │
│ Lundi  ├────────────────────┴─────────────────────┤
│        │ 16h-18h : Projet de groupe               │
├────────┼────────────────────┬─────────────────────┤
│ Mardi  │ 9h-12h : Français  │ 14h-17h : Sciences  │
└────────┴────────────────────┴─────────────────────┘
```

### Cas d'usage courants de rowspan

#### 1. Groupement par catégorie

```html
<table>
    <thead>
        <tr>
            <th scope="col">Catégorie</th>
            <th scope="col">Produit</th>
            <th scope="col">Prix</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="rowgroup" rowspan="3">Électronique</th>
            <td>Ordinateur</td>
            <td>899€</td>
        </tr>
        <tr>
            <td>Tablette</td>
            <td>449€</td>
        </tr>
        <tr>
            <td>Smartphone</td>
            <td>699€</td>
        </tr>
        <tr>
            <th scope="rowgroup" rowspan="2">Accessoires</th>
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

**Résultat :**
```
┌──────────────┬──────────────┬────────┐
│  Catégorie   │   Produit    │  Prix  │
├──────────────┼──────────────┼────────┤
│              │ Ordinateur   │  899€  │
│Électronique  ├──────────────┼────────┤
│              │ Tablette     │  449€  │
│              ├──────────────┼────────┤
│              │ Smartphone   │  699€  │
├──────────────┼──────────────┼────────┤
│              │ Souris       │   29€  │
│Accessoires   ├──────────────┼────────┤
│              │ Clavier      │   79€  │
└──────────────┴──────────────┴────────┘
```

#### 2. Informations qui s'appliquent à plusieurs lignes

```html
<table>
    <caption>Détails de commande</caption>
    <thead>
        <tr>
            <th scope="col">N° Commande</th>
            <th scope="col">Article</th>
            <th scope="col">Quantité</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="rowgroup" rowspan="3">CMD-2024-001</th>
            <td>Clavier mécanique</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Souris gamer</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Tapis de souris XXL</td>
            <td>1</td>
        </tr>
    </tbody>
</table>
```

---

## Combiner `colspan` et `rowspan`

La vraie puissance vient de la **combinaison** des deux attributs !

### Exemple 1 : Cellule qui s'étend en largeur ET en hauteur

```html
<table border="1">
    <tr>
        <td colspan="2" rowspan="2">Grande cellule<br>(2 colonnes × 2 lignes)</td>
        <td>A</td>
    </tr>
    <tr>
        <!-- 2 cellules manquantes à cause du colspan et rowspan -->
        <td>B</td>
    </tr>
    <tr>
        <td>C</td>
        <td>D</td>
        <td>E</td>
    </tr>
</table>
```

**Résultat visuel :**
```
┌─────────────────────────────┬─────┐
│                             │  A  │
│    Grande cellule           ├─────┤
│  (2 colonnes × 2 lignes)    │  B  │
├───────────┬─────────────────┼─────┤
│     C     │        D        │  E  │
└───────────┴─────────────────┴─────┘
```

### Exemple 2 : Planning complexe

```html
<table>
    <caption>Programme de la conférence</caption>
    <thead>
        <tr>
            <th scope="col">Horaire</th>
            <th scope="col">Salle A</th>
            <th scope="col">Salle B</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">9h - 10h</th>
            <td colspan="2" style="text-align: center; background-color: #e3f2fd;">
                <strong>Session plénière d'ouverture</strong>
            </td>
        </tr>
        <tr>
            <th scope="row">10h15 - 11h45</th>
            <td>Atelier JavaScript</td>
            <td>Atelier Python</td>
        </tr>
        <tr>
            <th scope="row">12h - 13h30</th>
            <td colspan="2" style="text-align: center; background-color: #fff3e0;">
                Déjeuner
            </td>
        </tr>
        <tr>
            <th scope="row">14h - 15h30</th>
            <td rowspan="2" style="vertical-align: middle; background-color: #f3e5f5;">
                <strong>Workshop DevOps</strong><br>
                <small>(Session de 3h)</small>
            </td>
            <td>Conférence : Cloud Computing</td>
        </tr>
        <tr>
            <th scope="row">15h45 - 17h15</th>
            <!-- Pas de cellule Salle A (rowspan de la cellule précédente) -->
            <td>Conférence : IA et ML</td>
        </tr>
    </tbody>
</table>
```

**Structure :**
```
┌──────────────┬──────────────────────┬──────────────────────┐
│   Horaire    │       Salle A        │       Salle B        │
├──────────────┼──────────────────────┴──────────────────────┤
│ 9h - 10h     │  Session plénière d'ouverture               │
├──────────────┼──────────────────────┬──────────────────────┤
│10h15 - 11h45 │ Atelier JavaScript   │ Atelier Python       │
├──────────────┼──────────────────────┴──────────────────────┤
│12h - 13h30   │          Déjeuner                           │
├──────────────┼──────────────────────┬──────────────────────┤
│14h - 15h30   │                      │ Cloud Computing      │
│              │  Workshop DevOps     ├──────────────────────┤
│15h45 - 17h15 │   (Session 3h)       │ IA et ML             │
└──────────────┴──────────────────────┴──────────────────────┘
```

---

## Calcul du nombre de cellules

### La règle d'or

**Chaque ligne doit avoir le même nombre total de "colonnes occupées".**

Formule : `Cellules normales + (colspan × cellules avec colspan) + (cellules de rowspan venant d'en haut) = Nombre total de colonnes`

### Exemple détaillé

Prenons un tableau à **4 colonnes** :

```html
<table border="1">
    <!-- Ligne 1 : 4 cellules normales = 4 colonnes ✓ -->
    <tr>
        <td>A</td>
        <td>B</td>
        <td>C</td>
        <td>D</td>
    </tr>

    <!-- Ligne 2 : 1 cellule (colspan 3) + 1 cellule normale = 3+1 = 4 colonnes ✓ -->
    <tr>
        <td colspan="3">E (3 colonnes)</td>
        <td>F</td>
    </tr>

    <!-- Ligne 3 : 1 cellule (rowspan 2) + 3 cellules = 1+3 = 4 colonnes ✓ -->
    <tr>
        <td rowspan="2">G (2 lignes)</td>
        <td>H</td>
        <td>I</td>
        <td>J</td>
    </tr>

    <!-- Ligne 4 : G continue + 3 cellules = 1+3 = 4 colonnes ✓ -->
    <tr>
        <!-- Pas de première cellule : G continue -->
        <td>K</td>
        <td>L</td>
        <td>M</td>
    </tr>
</table>
```

**Visualisation :**
```
┌───┬───┬───┬───┐
│ A │ B │ C │ D │  ← 4 cellules
├───┴───┴───┼───┤
│     E     │ F │  ← colspan="3" + 1 = 4
├───┬───┬───┼───┤
│   │ H │ I │ J │  ← rowspan commence
│ G ├───┼───┼───┤
│   │ K │ L │ M │  ← rowspan continue (pas de 1ère cellule)
└───┴───┴───┴───┘
```

### Erreurs fréquentes

#### ❌ Erreur 1 : Trop de cellules

```html
<!-- MAUVAIS : Tableau à 3 colonnes -->
<table border="1">
    <tr>
        <td>A</td>
        <td>B</td>
        <td>C</td>
    </tr>
    <tr>
        <td colspan="2">D-E</td>
        <td>F</td>
        <td>G</td>  <!-- ❌ 4ème cellule en trop ! -->
    </tr>
</table>
```

**Problème :** La ligne 2 a 2+1+1 = 4 colonnes au lieu de 3.

**Solution :**
```html
<!-- BON -->
<tr>
    <td colspan="2">D-E</td>
    <td>F</td>  <!-- 3 colonnes : OK ✓ -->
</tr>
```

#### ❌ Erreur 2 : Oublier le rowspan dans les lignes suivantes

```html
<!-- MAUVAIS -->
<table border="1">
    <tr>
        <td rowspan="2">A</td>
        <td>B</td>
    </tr>
    <tr>
        <td>C</td>  <!-- ❌ Devrait être la première cellule ! -->
        <td>D</td>
    </tr>
</table>
```

**Problème :** La ligne 2 a 3 colonnes (A continue + C + D) au lieu de 2.

**Solution :**
```html
<!-- BON -->
<tr>
    <td rowspan="2">A</td>
    <td>B</td>
</tr>
<tr>
    <!-- A continue, donc pas de première cellule -->
    <td>C</td>  <!-- C'est la 2ème colonne ✓ -->
</tr>
```

---

## Exemples pratiques complets

### Exemple 1 : Facture professionnelle

```html
<table>
    <caption>Facture N° 2024-12-001</caption>

    <thead>
        <tr>
            <th scope="col" colspan="4" style="text-align: left; background-color: #2c3e50; color: white; padding: 15px;">
                Mon Entreprise SARL<br>
                <small>123 Rue de la Paix, 75000 Paris</small>
            </th>
        </tr>
        <tr>
            <th scope="col">Désignation</th>
            <th scope="col">Quantité</th>
            <th scope="col">Prix unitaire</th>
            <th scope="col">Total</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <th colspan="4" scope="colgroup" style="background-color: #ecf0f1; text-align: left; padding: 8px;">
                Prestations de service
            </th>
        </tr>
        <tr>
            <td>Développement site web</td>
            <td>1</td>
            <td>3 500,00€</td>
            <td>3 500,00€</td>
        </tr>
        <tr>
            <td>Maintenance annuelle</td>
            <td>1</td>
            <td>500,00€</td>
            <td>500,00€</td>
        </tr>

        <tr>
            <th colspan="4" scope="colgroup" style="background-color: #ecf0f1; text-align: left; padding: 8px;">
                Licences logicielles
            </th>
        </tr>
        <tr>
            <td>Licence Premium (1 an)</td>
            <td>5</td>
            <td>99,00€</td>
            <td>495,00€</td>
        </tr>
    </tbody>

    <tfoot>
        <tr>
            <th colspan="3" scope="row" style="text-align: right; padding-right: 15px;">
                Sous-total HT
            </th>
            <td>4 495,00€</td>
        </tr>
        <tr>
            <th colspan="3" scope="row" style="text-align: right; padding-right: 15px;">
                TVA (20%)
            </th>
            <td>899,00€</td>
        </tr>
        <tr style="background-color: #2c3e50; color: white; font-size: 1.2em;">
            <th colspan="3" scope="row" style="text-align: right; padding-right: 15px;">
                Total TTC
            </th>
            <td><strong>5 394,00€</strong></td>
        </tr>
        <tr>
            <td colspan="4" style="padding: 15px; font-size: 0.9em;">
                <strong>Conditions de paiement :</strong> À réception, par virement bancaire<br>
                <strong>Date d'échéance :</strong> 03/01/2025
            </td>
        </tr>
    </tfoot>
</table>
```

### Exemple 2 : Tableau de comparaison de produits

```html
<table>
    <caption>Comparaison des forfaits mobiles</caption>

    <thead>
        <tr>
            <th scope="col">Caractéristique</th>
            <th scope="col">Basic</th>
            <th scope="col">Standard</th>
            <th scope="col">Premium</th>
        </tr>
    </thead>

    <tbody>
        <!-- Internet -->
        <tr>
            <th colspan="4" scope="colgroup" style="background-color: #3498db; color: white; padding: 10px;">
                Internet mobile
            </th>
        </tr>
        <tr>
            <th scope="row">Data 4G/5G</th>
            <td>5 Go</td>
            <td>50 Go</td>
            <td>Illimité</td>
        </tr>
        <tr>
            <th scope="row">Débit max</th>
            <td>4G</td>
            <td>4G+</td>
            <td>5G</td>
        </tr>

        <!-- Communication -->
        <tr>
            <th colspan="4" scope="colgroup" style="background-color: #3498db; color: white; padding: 10px;">
                Communication
            </th>
        </tr>
        <tr>
            <th scope="row">Appels</th>
            <td colspan="3" style="text-align: center;">Illimités France</td>
        </tr>
        <tr>
            <th scope="row">SMS/MMS</th>
            <td colspan="3" style="text-align: center;">Illimités</td>
        </tr>

        <!-- International -->
        <tr>
            <th colspan="4" scope="colgroup" style="background-color: #3498db; color: white; padding: 10px;">
                International
            </th>
        </tr>
        <tr>
            <th scope="row">Roaming Europe</th>
            <td>❌</td>
            <td>✅ Inclus</td>
            <td>✅ Inclus</td>
        </tr>
        <tr>
            <th scope="row">Destinations monde</th>
            <td>❌</td>
            <td>❌</td>
            <td>✅ 100 pays</td>
        </tr>
    </tbody>

    <tfoot>
        <tr style="background-color: #2c3e50; color: white; font-weight: bold; font-size: 1.1em;">
            <th scope="row">Prix mensuel</th>
            <td>9,99€</td>
            <td>19,99€</td>
            <td>29,99€</td>
        </tr>
        <tr>
            <td colspan="4" style="text-align: center; padding: 10px; font-size: 0.9em;">
                Sans engagement • Résiliable à tout moment
            </td>
        </tr>
    </tfoot>
</table>
```

### Exemple 3 : Calendrier mensuel

```html
<table>
    <caption>Décembre 2024</caption>

    <thead>
        <tr>
            <th scope="col">Lun</th>
            <th scope="col">Mar</th>
            <th scope="col">Mer</th>
            <th scope="col">Jeu</th>
            <th scope="col">Ven</th>
            <th scope="col" style="background-color: #e3f2fd;">Sam</th>
            <th scope="col" style="background-color: #e3f2fd;">Dim</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td colspan="5" style="background-color: #f5f5f5;"></td>
            <td style="background-color: #e3f2fd;">1</td>
            <td style="background-color: #e3f2fd;">2</td>
        </tr>
        <tr>
            <td>3</td>
            <td>4</td>
            <td>5</td>
            <td>6</td>
            <td>7</td>
            <td style="background-color: #e3f2fd;">8</td>
            <td style="background-color: #e3f2fd;">9</td>
        </tr>
        <tr>
            <td>10</td>
            <td>11</td>
            <td>12</td>
            <td>13</td>
            <td>14</td>
            <td style="background-color: #e3f2fd;">15</td>
            <td style="background-color: #e3f2fd;">16</td>
        </tr>
        <tr>
            <td>17</td>
            <td>18</td>
            <td>19</td>
            <td>20</td>
            <td>21</td>
            <td style="background-color: #e3f2fd;">22</td>
            <td style="background-color: #e3f2fd;">23</td>
        </tr>
        <tr>
            <td>24</td>
            <td style="background-color: #ffebee;">25<br><small>Noël</small></td>
            <td>26</td>
            <td>27</td>
            <td>28</td>
            <td style="background-color: #e3f2fd;">29</td>
            <td style="background-color: #e3f2fd;">30</td>
        </tr>
        <tr>
            <td>31</td>
            <td colspan="6" style="background-color: #f5f5f5;"></td>
        </tr>
    </tbody>
</table>
```

---

## Pièges courants et solutions

### Piège 1 : Compter les cellules

**Problème :** Oublier qu'un colspan ou rowspan "consomme" plusieurs emplacements.

**Solution :** Dessinez votre tableau sur papier avant de coder :

```
Tableau cible :
┌───┬───┬───┐
│ A │ B │ C │  Ligne 1 : 3 cellules
├───┴───┼───┤
│   D   │ E │  Ligne 2 : colspan 2 + 1 cellule
└───────┴───┘

Code :
<tr>
    <td>A</td>
    <td>B</td>
    <td>C</td>
</tr>
<tr>
    <td colspan="2">D</td>
    <td>E</td>
</tr>
```

### Piège 2 : Rowspan et lignes suivantes

**Problème :** Mettre le même nombre de cellules dans chaque ligne alors qu'un rowspan continue.

```html
<!-- ❌ MAUVAIS -->
<tr>
    <td rowspan="2">A</td>
    <td>B</td>
    <td>C</td>
</tr>
<tr>
    <td>D</td>  <!-- Première cellule -->
    <td>E</td>  <!-- Deuxième cellule -->
    <td>F</td>  <!-- ❌ Trop de cellules ! -->
</tr>
```

**Solution :** Les lignes avec rowspan actif ont moins de cellules :

```html
<!-- ✅ BON -->
<tr>
    <td rowspan="2">A</td>
    <td>B</td>
    <td>C</td>
</tr>
<tr>
    <!-- A continue, donc on commence directement -->
    <td>D</td>  <!-- Deuxième colonne -->
    <td>E</td>  <!-- Troisième colonne -->
</tr>
```

### Piège 3 : Mélanger colspan et rowspan

**Problème :** Ne pas visualiser l'espace occupé.

**Astuce :** Utilisez un tableur (Excel, Google Sheets) pour planifier :

1. Créez la grille
2. Fusionnez les cellules visuellement
3. Comptez les colonnes/lignes
4. Codez en HTML

### Piège 4 : Oublier scope avec colspan/rowspan

**Problème :** Les attributs colspan/rowspan sur des `<th>` sans adapter le scope.

```html
<!-- ❌ Moins précis -->
<th colspan="3">Groupe</th>

<!-- ✅ Meilleur pour l'accessibilité -->
<th scope="colgroup" colspan="3">Groupe</th>
```

**Valeurs de scope possibles :**
- `scope="col"` : En-tête d'une seule colonne
- `scope="row"` : En-tête d'une seule ligne
- `scope="colgroup"` : En-tête de **groupe de colonnes** (avec colspan)
- `scope="rowgroup"` : En-tête de **groupe de lignes** (avec rowspan)

---

## Accessibilité avec cellules fusionnées

### Associer les en-têtes aux données

Pour des tableaux complexes, utilisez `headers` et `id` :

```html
<table>
    <thead>
        <tr>
            <th id="region" scope="col">Région</th>
            <th id="sem1" scope="colgroup" colspan="2">Semestre 1</th>
        </tr>
        <tr>
            <th id="t1" scope="col">T1</th>
            <th id="t2" scope="col">T2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th id="paris" scope="row">Paris</th>
            <td headers="paris t1">120K€</td>
            <td headers="paris t2">145K€</td>
        </tr>
    </tbody>
</table>
```

**Lecteur d'écran annoncera :**
"Paris, T1 : 120 000 euros"

### Utiliser les bons scope

```html
<!-- En-tête de groupe de colonnes -->
<th scope="colgroup" colspan="3">Groupe</th>

<!-- En-tête de groupe de lignes -->
<th scope="rowgroup" rowspan="3">Catégorie</th>

<!-- En-tête simple -->
<th scope="col">Colonne</th>
<th scope="row">Ligne</th>
```

### Garder la structure logique

Même avec colspan/rowspan, la structure doit rester compréhensible :

```html
<!-- ✅ BON : Structure claire -->
<thead>
    <tr>
        <th scope="col" rowspan="2">Nom</th>
        <th scope="colgroup" colspan="2">Contact</th>
    </tr>
    <tr>
        <th scope="col">Email</th>
        <th scope="col">Téléphone</th>
    </tr>
</thead>
```

---

## Styling des cellules fusionnées

### Centrer verticalement le contenu

```css
/* Centrer dans les cellules avec rowspan */
td[rowspan],
th[rowspan] {
    vertical-align: middle;
}

/* Ou explicitement */
.centered-cell {
    vertical-align: middle;
    text-align: center;
}
```

### Différencier visuellement

```css
/* En-têtes de groupes */
th[colspan] {
    background-color: #3498db;
    color: white;
    font-weight: bold;
    text-align: center;
}

/* Cellules fusionnées verticalement */
th[rowspan] {
    background-color: #ecf0f1;
    font-weight: 600;
}
```

### Bordures spéciales

```css
/* Bordure épaisse pour groupes */
th[colspan] {
    border-bottom: 3px solid #2c3e50;
}

th[rowspan] {
    border-right: 3px solid #2c3e50;
}
```

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Dessiner le tableau d'abord**
```
Planifiez sur papier ou dans un tableur avant de coder
```

2. **Vérifier le nombre de colonnes par ligne**
```html
<!-- Tableau 4 colonnes -->
<tr>
    <td>A</td>
    <td>B</td>
    <td>C</td>
    <td>D</td>  <!-- 4 ✓ -->
</tr>
<tr>
    <td colspan="2">E</td>
    <td>F</td>
    <td>G</td>  <!-- 2+1+1 = 4 ✓ -->
</tr>
```

3. **Utiliser scope avec colspan/rowspan**
```html
<th scope="colgroup" colspan="3">Groupe de colonnes</th>
<th scope="rowgroup" rowspan="2">Groupe de lignes</th>
```

4. **Donner un sens visuel aux fusions**
```html
<!-- Fusion pour grouper des données liées -->
<th colspan="3" scope="colgroup">Informations de contact</th>
```

5. **Tester avec un lecteur d'écran**
```
Vérifiez que la structure reste compréhensible à l'écoute
```

### ❌ À ÉVITER

1. **Fusionner pour le style uniquement**
```html
<!-- ❌ MAUVAIS : fusion sans raison sémantique -->
<td colspan="3" style="background-color: blue;"></td>

<!-- ✅ BON : utilisez CSS pour le style -->
<td class="full-width"></td>
```

2. **Tableaux trop complexes**
```
Si vous avez besoin de dessiner un schéma pour comprendre,
votre tableau est peut-être trop complexe.
Envisagez de le simplifier ou de le diviser.
```

3. **Oublier les cellules dans les lignes avec rowspan**
```html
<!-- ❌ MAUVAIS -->
<tr>
    <td rowspan="2">A</td>
    <td>B</td>
</tr>
<tr>
    <td>C</td>
    <td>D</td>  <!-- ❌ Une cellule de trop -->
</tr>
```

4. **Colspan/rowspan avec des valeurs incorrectes**
```html
<!-- ❌ Éviter -->
<td colspan="0">...</td>  <!-- 0 est invalide -->
<td rowspan="-1">...</td>  <!-- Négatif invalide -->

<!-- ✅ Valeurs valides : entiers positifs -->
<td colspan="2">...</td>
<td rowspan="3">...</td>
```

5. **Imbriquer des tableaux pour simuler colspan/rowspan**
```html
<!-- ❌ TRÈS MAUVAIS : tableau dans tableau -->
<td>
    <table>
        <tr><td>Sous-tableau</td></tr>
    </table>
</td>

<!-- ✅ BON : utilisez colspan/rowspan -->
<td colspan="2">Contenu fusionné</td>
```

---

## Validation et débogage

### Outils de vérification

1. **Validateur W3C**
   - https://validator.w3.org/
   - Détecte les erreurs de structure

2. **Inspecteur de navigateur**
   - Clic droit → Inspecter
   - Visualisez la structure réelle

3. **Extension WAVE**
   - Vérifie l'accessibilité
   - Teste les associations en-têtes/données

### Checklist de débogage

Si votre tableau ne s'affiche pas correctement :

- [ ] Comptez les colonnes par ligne (doivent être égales)
- [ ] Vérifiez que les rowspan ne créent pas de cellules en trop
- [ ] Confirmez que les valeurs de colspan/rowspan sont positives
- [ ] Assurez-vous que tous les `<tr>` sont dans `<thead>`, `<tbody>` ou `<tfoot>`
- [ ] Vérifiez les balises fermantes
- [ ] Testez dans différents navigateurs

---

## Points clés à retenir

1. **`colspan`** fusionne des cellules **horizontalement** (colonnes)
2. **`rowspan`** fusionne des cellules **verticalement** (lignes)
3. **Comptez toujours** : chaque ligne doit avoir le même nombre total de colonnes
4. **Les rowspan "consomment" des emplacements** dans les lignes suivantes
5. **Utilisez `scope` approprié** : `colgroup` avec colspan, `rowgroup` avec rowspan
6. **Dessinez avant de coder** : planifiez la structure visuellement
7. **Valeurs valides** : entiers positifs uniquement (1, 2, 3...)
8. **Testez l'accessibilité** : le tableau doit rester compréhensible sans vision
9. **Simplicité avant tout** : si c'est trop complexe, divisez le tableau
10. **Combiner les deux** : colspan et rowspan peuvent coexister sur la même cellule

---

## Prochaine étape

Maintenant que vous maîtrisez colspan et rowspan pour créer des tableaux complexes, nous allons découvrir dans le prochain chapitre comment **rendre vos tableaux responsives** pour qu'ils s'adaptent parfaitement aux petits écrans (mobiles, tablettes) et améliorer leur **accessibilité avancée** avec les attributs ARIA et les techniques modernes.

⏭️ [CSS3 - Styles et Mise en Page](/04-css3-styles-et-mise-en-page/README.md)
