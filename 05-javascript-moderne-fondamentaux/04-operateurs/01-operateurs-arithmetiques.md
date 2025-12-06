🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4.1 - Opérateurs arithmétiques

## Introduction

Les **opérateurs arithmétiques** permettent d'effectuer des calculs mathématiques en JavaScript. Ils sont essentiels pour manipuler des nombres, calculer des totaux, des pourcentages, des moyennes, et bien plus encore.

JavaScript offre six opérateurs arithmétiques de base :
- **Addition** `+`
- **Soustraction** `-`
- **Multiplication** `*`
- **Division** `/`
- **Modulo (reste)** `%`
- **Exponentiation** `**` 🆕

Ces opérateurs fonctionnent de manière similaire aux calculs que vous faites avec une calculatrice.

---

## Addition `+`

L'opérateur `+` additionne deux nombres.

### Syntaxe

```javascript
resultat = nombre1 + nombre2;
```

### Exemples de base

```javascript
const a = 5 + 3;
console.log(a); // 8

const b = 10 + 25;
console.log(b); // 35

const c = 1.5 + 2.3;
console.log(c); // 3.8
```

### Avec des variables

```javascript
const prix1 = 15;
const prix2 = 23;
const total = prix1 + prix2;

console.log(total); // 38
```

### Additions multiples

```javascript
const somme = 5 + 10 + 15 + 20;
console.log(somme); // 50

// Avec des variables
const a = 10;
const b = 20;
const c = 30;
const total = a + b + c;
console.log(total); // 60
```

### Cas d'usage pratiques

#### Calcul de panier d'achat

```javascript
const prixProduit1 = 29.99;
const prixProduit2 = 15.50;
const prixProduit3 = 8.00;

const sousTotal = prixProduit1 + prixProduit2 + prixProduit3;
console.log(sousTotal); // 53.49
```

#### Calcul d'âge

```javascript
const anneeNaissance = 1990;
const anneeActuelle = 2025;
const age = anneeActuelle - anneeNaissance; // (on verra la soustraction juste après)
```

### ⚠️ Attention : Addition vs Concaténation

L'opérateur `+` a **deux rôles différents** selon le contexte :

```javascript
// Avec des nombres : ADDITION
console.log(5 + 3);      // 8

// Avec des strings : CONCATÉNATION
console.log("5" + "3");  // "53" (pas 8 !)

// Mélange nombre + string : CONCATÉNATION
console.log(5 + "3");    // "53" (le nombre devient une string)
console.log("Âge: " + 25); // "Âge: 25"
```

**Règle importante** : Si au moins un opérande est une string, l'opérateur `+` fait de la concaténation, pas de l'addition !

```javascript
const a = 10;
const b = 20;
const c = "30";

console.log(a + b);     // 30 (addition)
console.log(a + c);     // "1030" (concaténation)
console.log(a + b + c); // "3030" (10+20=30, puis "30"+"30")
```

---

## Soustraction `-`

L'opérateur `-` soustrait le second nombre du premier.

### Syntaxe

```javascript
resultat = nombre1 - nombre2;
```

### Exemples de base

```javascript
const a = 10 - 3;
console.log(a); // 7

const b = 50 - 25;
console.log(b); // 25

const c = 5.5 - 2.3;
console.log(c); // 3.2
```

### Résultats négatifs

```javascript
const a = 5 - 10;
console.log(a); // -5

const temperature = 15 - 20;
console.log(temperature); // -5 (degrés)
```

### Cas d'usage pratiques

#### Calcul de différence

```javascript
const prixInitial = 100;
const remise = 15;
const prixFinal = prixInitial - remise;

console.log(prixFinal); // 85
```

#### Calcul de temps restant

```javascript
const dureeFilm = 120; // minutes
const dejavu = 45;     // minutes
const tempsRestant = dureeFilm - dejavu;

console.log(tempsRestant); // 75 minutes
```

#### Calcul de différence d'âge

```javascript
const ageAlice = 28;
const ageBob = 25;
const difference = ageAlice - ageBob;

console.log(`Alice a ${difference} ans de plus que Bob`);
// Alice a 3 ans de plus que Bob
```

### ⚠️ Attention : Soustraction avec strings

Contrairement à `+`, l'opérateur `-` **ne fait jamais de concaténation** :

```javascript
console.log("10" - "3");  // 7 (conversion automatique en nombres)
console.log("10" - 3);    // 7
console.log(10 - "3");    // 7

// Mais attention aux strings non-numériques
console.log("abc" - 5);   // NaN (Not a Number)
```

---

## Multiplication `*`

L'opérateur `*` multiplie deux nombres.

### Syntaxe

```javascript
resultat = nombre1 * nombre2;
```

### Exemples de base

```javascript
const a = 5 * 3;
console.log(a); // 15

const b = 7 * 8;
console.log(b); // 56

const c = 2.5 * 4;
console.log(c); // 10
```

### Cas d'usage pratiques

#### Calcul de prix total

```javascript
const prixUnitaire = 15.99;
const quantite = 3;
const total = prixUnitaire * quantite;

console.log(total); // 47.97
```

#### Conversion d'unités

```javascript
const heures = 2;
const minutes = heures * 60;
console.log(minutes); // 120

const jours = 7;
const heuresParSemaine = jours * 24;
console.log(heuresParSemaine); // 168
```

#### Calcul de surface

```javascript
const longueur = 5;
const largeur = 3;
const surface = longueur * largeur;

console.log(`La surface est de ${surface} m²`);
// La surface est de 15 m²
```

#### Calcul de pourcentage

```javascript
const prix = 100;
const pourcentageRemise = 0.20; // 20%
const montantRemise = prix * pourcentageRemise;

console.log(montantRemise); // 20
```

---

## Division `/`

L'opérateur `/` divise le premier nombre par le second.

### Syntaxe

```javascript
resultat = nombre1 / nombre2;
```

### Exemples de base

```javascript
const a = 10 / 2;
console.log(a); // 5

const b = 15 / 3;
console.log(b); // 5

const c = 7 / 2;
console.log(c); // 3.5 (division avec décimales)
```

### Division avec décimales

JavaScript retourne automatiquement des nombres décimaux :

```javascript
console.log(10 / 3);  // 3.3333333333333335
console.log(7 / 2);   // 3.5
console.log(1 / 4);   // 0.25
```

### Cas d'usage pratiques

#### Calcul de moyenne

```javascript
const note1 = 15;
const note2 = 18;
const note3 = 12;
const total = note1 + note2 + note3;
const moyenne = total / 3;

console.log(moyenne); // 15
```

#### Calcul de prix unitaire

```javascript
const prixTotal = 50;
const quantite = 4;
const prixUnitaire = prixTotal / quantite;

console.log(prixUnitaire); // 12.5
```

#### Conversion d'unités

```javascript
const kilometres = 5;
const metres = kilometres * 1000;
console.log(metres); // 5000

const retourEnKm = metres / 1000;
console.log(retourEnKm); // 5
```

#### Partage équitable

```javascript
const montantTotal = 150;
const nombrePersonnes = 3;
const partParPersonne = montantTotal / nombrePersonnes;

console.log(`Chaque personne doit payer ${partParPersonne}€`);
// Chaque personne doit payer 50€
```

### ⚠️ Attention : Division par zéro

Diviser par zéro produit un résultat spécial :

```javascript
console.log(10 / 0);  // Infinity
console.log(-10 / 0); // -Infinity
console.log(0 / 0);   // NaN (Not a Number)
```

**Bonne pratique** : Vérifier avant de diviser :

```javascript
const dividende = 100;
const diviseur = 0;

if (diviseur !== 0) {
    const resultat = dividende / diviseur;
    console.log(resultat);
} else {
    console.log("Erreur : division par zéro impossible");
}
```

---

## Modulo `%` - Le reste de la division

L'opérateur `%` (modulo) retourne le **reste** d'une division entière.

### Syntaxe

```javascript
resultat = nombre1 % nombre2;
```

### Comprendre le modulo

Le modulo retourne ce qui reste après avoir divisé :

```javascript
console.log(10 % 3);  // 1  (10 ÷ 3 = 3 reste 1)
console.log(15 % 4);  // 3  (15 ÷ 4 = 3 reste 3)
console.log(20 % 5);  // 0  (20 ÷ 5 = 4 reste 0)
console.log(7 % 2);   // 1  (7 ÷ 2 = 3 reste 1)
```

**Explication détaillée** :
- `10 % 3` → 10 divisé par 3 = 3 (avec reste 1)
- 3 × 3 = 9, il reste 1 pour arriver à 10
- Donc `10 % 3 = 1`

### Cas d'usage pratiques

#### Vérifier si un nombre est pair ou impair

```javascript
const nombre = 7;

if (nombre % 2 === 0) {
    console.log(`${nombre} est pair`);
} else {
    console.log(`${nombre} est impair`);
}
// 7 est impair
```

**Astuce** : Un nombre pair a un reste de 0 quand on le divise par 2.

#### Cycle et répétition

```javascript
// Créer un cycle de 0 à 4 qui se répète
for (let i = 0; i < 15; i++) {
    console.log(i % 5);
}
// Affiche : 0, 1, 2, 3, 4, 0, 1, 2, 3, 4, 0, 1, 2, 3, 4
```

#### Alterner entre deux valeurs

```javascript
const items = ["A", "B", "C", "D", "E", "F"];

items.forEach((item, index) => {
    if (index % 2 === 0) {
        console.log(`${item} - Ligne paire`);
    } else {
        console.log(`${item} - Ligne impaire`);
    }
});
```

#### Diviser en groupes

```javascript
// Afficher 3 éléments par ligne
const nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9];

nombres.forEach((nombre, index) => {
    if (index % 3 === 0 && index !== 0) {
        console.log("--- Nouvelle ligne ---");
    }
    console.log(nombre);
});
```

#### Vérifier la divisibilité

```javascript
const nombre = 15;

if (nombre % 3 === 0) {
    console.log(`${nombre} est divisible par 3`);
}

if (nombre % 5 === 0) {
    console.log(`${nombre} est divisible par 5`);
}
// 15 est divisible par 3
// 15 est divisible par 5
```

---

## Exponentiation `**` - Puissance 🆕

L'opérateur `**` élève un nombre à une puissance (introduit en ES2016).

### Syntaxe

```javascript
resultat = base ** exposant;
```

### Exemples de base

```javascript
console.log(2 ** 3);   // 8  (2 × 2 × 2)
console.log(5 ** 2);   // 25 (5 × 5)
console.log(10 ** 3);  // 1000 (10 × 10 × 10)
console.log(3 ** 4);   // 81 (3 × 3 × 3 × 3)
```

### Puissances spéciales

```javascript
// Carré (puissance 2)
console.log(5 ** 2);   // 25

// Cube (puissance 3)
console.log(3 ** 3);   // 27

// Puissance 0 (toujours 1)
console.log(5 ** 0);   // 1
console.log(100 ** 0); // 1

// Puissance 1 (toujours le nombre lui-même)
console.log(7 ** 1);   // 7
```

### Puissances négatives et décimales

```javascript
// Puissance négative (inverse)
console.log(2 ** -2);  // 0.25 (1 / 2²)
console.log(10 ** -1); // 0.1 (1 / 10)

// Puissance décimale (racine)
console.log(9 ** 0.5);  // 3 (racine carrée de 9)
console.log(8 ** (1/3)); // 2 (racine cubique de 8)
```

### Cas d'usage pratiques

#### Calculs scientifiques

```javascript
// Notation scientifique
const vitesseLumiere = 3 * (10 ** 8); // 3 × 10⁸ m/s
console.log(vitesseLumiere); // 300000000
```

#### Calcul de surface et volume

```javascript
// Surface d'un carré
const cote = 5;
const surface = cote ** 2;
console.log(`Surface: ${surface} m²`); // 25 m²

// Volume d'un cube
const volume = cote ** 3;
console.log(`Volume: ${volume} m³`); // 125 m³
```

#### Calcul d'intérêts composés

```javascript
const capital = 1000;
const tauxAnnuel = 0.05; // 5%
const annees = 10;

const montantFinal = capital * ((1 + tauxAnnuel) ** annees);
console.log(montantFinal.toFixed(2)); // 1628.89
```

### ⚠️ Alternative : Math.pow()

Avant ES2016, on utilisait `Math.pow()` :

```javascript
// ⚠️ Ancienne méthode
console.log(Math.pow(2, 3)); // 8

// ✅ Méthode moderne
console.log(2 ** 3);         // 8
```

**Recommandation** : Utilisez `**` dans du nouveau code, c'est plus lisible.

---

## Ordre des opérations (priorité)

Comme en mathématiques, JavaScript suit un ordre de priorité des opérations.

### Règles de priorité

1. **Parenthèses** `( )` - Priorité absolue
2. **Exponentiation** `**`
3. **Multiplication** `*` et **Division** `/` et **Modulo** `%` (même niveau)
4. **Addition** `+` et **Soustraction** `-` (même niveau)

### Exemples sans parenthèses

```javascript
console.log(2 + 3 * 4);      // 14 (pas 20)
// Calcul : 3 * 4 = 12, puis 2 + 12 = 14

console.log(10 - 2 * 3);     // 4 (pas 24)
// Calcul : 2 * 3 = 6, puis 10 - 6 = 4

console.log(2 ** 3 * 2);     // 16
// Calcul : 2 ** 3 = 8, puis 8 * 2 = 16
```

### Utiliser les parenthèses

Les parenthèses forcent l'ordre d'exécution :

```javascript
console.log((2 + 3) * 4);    // 20
// Calcul : 2 + 3 = 5, puis 5 * 4 = 20

console.log((10 - 2) * 3);   // 24
// Calcul : 10 - 2 = 8, puis 8 * 3 = 24
```

### Exemples pratiques

#### Calcul de moyenne avec pondération

```javascript
const note1 = 15;
const note2 = 18;
const coef1 = 2;
const coef2 = 3;

// ❌ Sans parenthèses (incorrect)
const faux = note1 * coef1 + note2 * coef2 / coef1 + coef2;
console.log(faux); // Résultat incorrect

// ✅ Avec parenthèses (correct)
const moyenne = (note1 * coef1 + note2 * coef2) / (coef1 + coef2);
console.log(moyenne); // 16.8
```

#### Calcul de prix avec remise

```javascript
const prix = 100;
const quantite = 3;
const remisePourcentage = 10;

// ❌ Sans parenthèses
const total1 = prix * quantite - prix * quantite * remisePourcentage / 100;

// ✅ Avec parenthèses (plus clair)
const sousTotal = prix * quantite;
const remise = (sousTotal * remisePourcentage) / 100;
const total2 = sousTotal - remise;

console.log(total2); // 270
```

**Bonne pratique** : En cas de doute, **utilisez des parenthèses** pour rendre votre code plus clair !

---

## Opérateurs d'affectation composés

JavaScript offre des raccourcis pour combiner opération et affectation.

### Syntaxe de base

Au lieu de :
```javascript
variable = variable + valeur;
```

Vous pouvez écrire :
```javascript
variable += valeur;
```

### Addition et affectation `+=`

```javascript
let score = 10;
score += 5;  // Équivalent à : score = score + 5
console.log(score); // 15

score += 10;
console.log(score); // 25
```

### Soustraction et affectation `-=`

```javascript
let vies = 100;
vies -= 20;  // Équivalent à : vies = vies - 20
console.log(vies); // 80

vies -= 30;
console.log(vies); // 50
```

### Multiplication et affectation `*=`

```javascript
let points = 10;
points *= 2;  // Équivalent à : points = points * 2
console.log(points); // 20

points *= 3;
console.log(points); // 60
```

### Division et affectation `/=`

```javascript
let nombre = 100;
nombre /= 2;  // Équivalent à : nombre = nombre / 2
console.log(nombre); // 50

nombre /= 5;
console.log(nombre); // 10
```

### Modulo et affectation `%=`

```javascript
let valeur = 17;
valeur %= 5;  // Équivalent à : valeur = valeur % 5
console.log(valeur); // 2
```

### Exponentiation et affectation `**=`

```javascript
let base = 2;
base **= 3;  // Équivalent à : base = base ** 3
console.log(base); // 8
```

### Cas d'usage pratiques

#### Compteur de points

```javascript
let score = 0;

score += 10;  // +10 points
console.log(score); // 10

score += 25;  // +25 points
console.log(score); // 35

score -= 5;   // -5 points (pénalité)
console.log(score); // 30
```

#### Gestion d'inventaire

```javascript
let stock = 100;

stock -= 15;  // Vente de 15 articles
console.log(stock); // 85

stock += 50;  // Réapprovisionnement
console.log(stock); // 135
```

#### Multiplicateur de bonus

```javascript
let points = 100;

points *= 2;  // Double points
console.log(points); // 200

points *= 1.5;  // Bonus de 50%
console.log(points); // 300
```

---

## Incrémentation et décrémentation

JavaScript offre des opérateurs spéciaux pour ajouter ou soustraire 1.

### Incrémentation `++`

```javascript
let compteur = 5;

compteur++;  // Équivalent à : compteur = compteur + 1
console.log(compteur); // 6

compteur++;
console.log(compteur); // 7
```

### Décrémentation `--`

```javascript
let vies = 3;

vies--;  // Équivalent à : vies = vies - 1
console.log(vies); // 2

vies--;
console.log(vies); // 1
```

### Préfixe vs Postfixe

Il existe deux positions pour `++` et `--` :

#### Postfixe (variable++)

Utilise la valeur **puis** incrémente :

```javascript
let x = 5;
let y = x++;  // y prend la valeur de x (5), puis x devient 6

console.log(x); // 6
console.log(y); // 5
```

#### Préfixe (++variable)

Incrémente **puis** utilise la valeur :

```javascript
let x = 5;
let y = ++x;  // x devient 6, puis y prend la valeur de x (6)

console.log(x); // 6
console.log(y); // 6
```

**Conseil pour débutants** : Utilisez ces opérateurs sur des lignes séparées pour éviter la confusion :

```javascript
// ✅ Clair et simple
let compteur = 5;
compteur++;
console.log(compteur); // 6
```

---

## Conversion automatique de types (Coercition)

JavaScript convertit automatiquement les types lors des opérations arithmétiques.

### Strings vers nombres

```javascript
console.log("10" - 5);    // 5 (string converti en nombre)
console.log("10" * 2);    // 20
console.log("20" / 4);    // 5
console.log("15" % 4);    // 3
```

⚠️ **Exception** : Le `+` fait de la concaténation si une string est présente !

```javascript
console.log("10" + 5);    // "105" (concaténation)
console.log(10 + "5");    // "105"
```

### Strings non-numériques

```javascript
console.log("abc" * 5);   // NaN (Not a Number)
console.log("hello" - 3); // NaN
```

### Conversion explicite

Pour éviter les surprises, convertissez explicitement :

```javascript
const stringNombre = "42";

// Conversion explicite
const nombre = Number(stringNombre);
console.log(nombre + 10); // 52

// Ou avec parseInt/parseFloat
const entier = parseInt("42.7");
console.log(entier); // 42

const decimal = parseFloat("42.7");
console.log(decimal); // 42.7
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier la priorité des opérations

```javascript
// ❌ Calcul incorrect
const resultat = 10 + 5 * 2;
console.log(resultat); // 20 (pas 30)

// ✅ Utilisez des parenthèses
const correct = (10 + 5) * 2;
console.log(correct); // 30
```

### ❌ Erreur 2 : Confusion entre + arithmétique et + concaténation

```javascript
const a = 5;
const b = "10";

// ❌ Résultat inattendu
console.log(a + b); // "510" (concaténation)

// ✅ Convertir d'abord
console.log(a + Number(b)); // 15
```

### ❌ Erreur 3 : Division par zéro non vérifiée

```javascript
const total = 100;
const nombre = 0;

// ❌ Produit Infinity
const moyenne = total / nombre;
console.log(moyenne); // Infinity

// ✅ Vérifier avant
if (nombre !== 0) {
    const moyenne = total / nombre;
    console.log(moyenne);
} else {
    console.log("Division par zéro impossible");
}
```

### ❌ Erreur 4 : Précision des nombres décimaux

```javascript
// ❌ Problème de précision
console.log(0.1 + 0.2); // 0.30000000000000004 (pas 0.3)

// ✅ Arrondir si nécessaire
const resultat = (0.1 + 0.2).toFixed(1);
console.log(resultat); // "0.3"

// Ou multiplier par 10, calculer, puis diviser
const resultat2 = (1 + 2) / 10;
console.log(resultat2); // 0.3
```

---

## Bonnes pratiques

### ✅ Utilisez des noms de variables explicites

```javascript
// ❌ Peu clair
const x = 100;
const y = 0.2;
const z = x * y;

// ✅ Clair et explicite
const prix = 100;
const tauxRemise = 0.2;
const montantRemise = prix * tauxRemise;
```

### ✅ Décomposez les calculs complexes

```javascript
// ❌ Difficile à lire
const total = prix * quantite - prix * quantite * remise / 100 + fraisPort;

// ✅ Étapes claires
const sousTotal = prix * quantite;
const montantRemise = (sousTotal * remise) / 100;
const totalAvecRemise = sousTotal - montantRemise;
const total = totalAvecRemise + fraisPort;
```

### ✅ Commentez les formules complexes

```javascript
// Calcul des intérêts composés
// Formule : M = C × (1 + r)^n
const capital = 1000;           // Capital initial
const tauxAnnuel = 0.05;        // Taux d'intérêt (5%)
const nombreAnnees = 10;        // Durée

const montantFinal = capital * ((1 + tauxAnnuel) ** nombreAnnees);
```

### ✅ Utilisez des constantes pour les valeurs fixes

```javascript
const TVA = 0.20;               // 20%
const FRAIS_LIVRAISON = 5.99;

const prixHT = 100;
const prixTTC = prixHT * (1 + TVA);
const total = prixTTC + FRAIS_LIVRAISON;
```

---

## Cas pratiques complets

### 1. Calculatrice de panier

```javascript
// Produits
const prixOrdi = 899.99;
const prixSouris = 29.99;
const prixClavier = 79.99;

// Quantités
const qteOrdi = 1;
const qteSouris = 2;
const qteClavier = 1;

// Calculs
const sousTotal = (prixOrdi * qteOrdi) +
                  (prixSouris * qteSouris) +
                  (prixClavier * qteClavier);

const remisePourcentage = 10; // 10%
const montantRemise = (sousTotal * remisePourcentage) / 100;
const totalAvecRemise = sousTotal - montantRemise;

const TVA = 0.20; // 20%
const montantTVA = totalAvecRemise * TVA;
const totalTTC = totalAvecRemise + montantTVA;

console.log(`Sous-total: ${sousTotal.toFixed(2)}€`);
console.log(`Remise (${remisePourcentage}%): -${montantRemise.toFixed(2)}€`);
console.log(`TVA (20%): ${montantTVA.toFixed(2)}€`);
console.log(`Total TTC: ${totalTTC.toFixed(2)}€`);
```

### 2. Convertisseur de température

```javascript
// Celsius vers Fahrenheit
const celsius = 25;
const fahrenheit = (celsius * 9/5) + 32;
console.log(`${celsius}°C = ${fahrenheit}°F`);

// Fahrenheit vers Celsius
const fahrenheitTemp = 77;
const celsiusTemp = (fahrenheitTemp - 32) * 5/9;
console.log(`${fahrenheitTemp}°F = ${celsiusTemp.toFixed(1)}°C`);
```

### 3. Calculateur d'IMC

```javascript
const poids = 70;        // kg
const taille = 1.75;     // mètres

const imc = poids / (taille ** 2);
console.log(`Votre IMC est: ${imc.toFixed(1)}`);

if (imc < 18.5) {
    console.log("Insuffisance pondérale");
} else if (imc < 25) {
    console.log("Poids normal");
} else if (imc < 30) {
    console.log("Surpoids");
} else {
    console.log("Obésité");
}
```

---

## Points clés à retenir

✅ **Six opérateurs arithmétiques** : `+`, `-`, `*`, `/`, `%`, `**`

✅ **L'opérateur `+`** fait de la **concaténation** si une string est présente

✅ **Priorité des opérations** : parenthèses > exponentiation > × ÷ % > + -

✅ **Opérateurs composés** : `+=`, `-=`, `*=`, `/=`, `%=`, `**=`

✅ **Incrémentation** `++` et **décrémentation** `--`

✅ **Vérifier la division par zéro** avant de diviser

✅ **Le modulo `%`** retourne le reste d'une division

✅ **Utiliser des parenthèses** en cas de doute pour clarifier l'ordre

✅ **Attention à la précision** des nombres décimaux en JavaScript

---

## Dans la prochaine section

Dans la section **5.4.2 - Opérateurs de comparaison**, nous découvrirons comment comparer des valeurs en JavaScript, avec une attention particulière sur la différence cruciale entre `==` et `===`.

---


⏭️ [Opérateurs de comparaison (insister sur === vs ==)](/05-javascript-moderne-fondamentaux/04-operateurs/02-operateurs-comparaison.md)
