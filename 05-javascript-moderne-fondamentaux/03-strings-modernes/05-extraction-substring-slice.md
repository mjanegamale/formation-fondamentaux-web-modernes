🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.5 - Extraction : substring, slice

## Introduction

L'**extraction** consiste à récupérer une portion (sous-chaîne) d'une string existante pour créer une nouvelle string. C'est une opération très courante en programmation.

JavaScript offre deux méthodes principales pour extraire des sous-chaînes :
- **`slice()`** ✅ : méthode moderne et flexible (recommandée)
- **`substring()`** ⚠️ : méthode classique avec comportement moins intuitif

**Important** : Ces méthodes ne modifient pas la string originale (rappel : les strings sont immutables), elles créent et retournent une **nouvelle string**.

---

## Vue d'ensemble

| Méthode | Indices négatifs | Comportement | Recommandation |
|---------|------------------|--------------|----------------|
| `slice()` | ✅ Supportés | Intuitif et prévisible | ✅ **À privilégier** |
| `substring()` | ❌ Traités comme 0 | Comportement particulier | ⚠️ Legacy |

---

## slice() - La méthode moderne ✅

### Syntaxe

```javascript
string.slice(debut, fin)
```

- **`debut`** : index de début (inclus)
- **`fin`** : index de fin (exclus) - optionnel

### Retourne

Une **nouvelle string** contenant la portion extraite.

### Utilisation de base

```javascript
const texte = "JavaScript";
//             0123456789

console.log(texte.slice(0, 4));   // "Java"
console.log(texte.slice(4, 10));  // "Script"
console.log(texte.slice(4));      // "Script" (jusqu'à la fin)
```

**Rappel important** : L'index de **fin est exclus** !

```javascript
const mot = "Bonjour";
//           0123456

console.log(mot.slice(0, 3));  // "Bon" (caractères 0, 1, 2)
console.log(mot.slice(3, 7));  // "jour" (caractères 3, 4, 5, 6)
```

### Sans paramètre de fin

Si vous omettez le second paramètre, `slice()` extrait jusqu'à la fin de la string :

```javascript
const phrase = "Bonjour le monde";

console.log(phrase.slice(8));   // "le monde"
console.log(phrase.slice(0));   // "Bonjour le monde" (copie complète)
console.log(phrase.slice(11));  // "monde"
```

### Indices négatifs - Le grand avantage de slice() ✨

Les **indices négatifs** comptent depuis la fin de la string :
- `-1` = dernier caractère
- `-2` = avant-dernier caractère
- etc.

```javascript
const mot = "JavaScript";
//           0123456789
//          -10-9-8-7-6-5-4-3-2-1

console.log(mot.slice(-6));      // "Script" (6 derniers caractères)
console.log(mot.slice(-10));     // "JavaScript" (toute la string)
console.log(mot.slice(0, -6));   // "Java" (tout sauf les 6 derniers)
console.log(mot.slice(-6, -2));  // "Scri" (de -6 à -2 exclus)
console.log(mot.slice(-4, -1));  // "rip"
```

**Visualisation :**

```javascript
const texte = "Bonjour";
//  Positif:  0 1 2 3 4 5 6
//  Négatif: -7-6-5-4-3-2-1

console.log(texte.slice(-3));    // "our" (3 derniers)
console.log(texte.slice(-7, -4)); // "Bon"
```

### Exemples pratiques avec slice()

#### Extraire les premiers caractères

```javascript
const nom = "Alexandre";
const initiale = nom.slice(0, 1);
console.log(initiale); // "A"

const trigramme = nom.slice(0, 3);
console.log(trigramme); // "Ale"
```

#### Extraire les derniers caractères

```javascript
const fichier = "document.pdf";
const extension = fichier.slice(-4);
console.log(extension); // ".pdf"

const derniers = fichier.slice(-3);
console.log(derniers); // "pdf"
```

#### Retirer le premier et le dernier caractère

```javascript
const texte = '"Bonjour"';
const sanGuillemets = texte.slice(1, -1);
console.log(sanGuillemets); // "Bonjour"
```

#### Extraire le nom de domaine d'un email

```javascript
const email = "alice@example.com";
const positionArobase = email.indexOf("@");
const domaine = email.slice(positionArobase + 1);
console.log(domaine); // "example.com"
```

#### Tronquer un texte long

```javascript
const description = "Ceci est une très longue description qui doit être tronquée";
const maxLength = 30;

const apercu = description.slice(0, maxLength) + "...";
console.log(apercu);
// "Ceci est une très longue desc..."
```

---

## substring() - La méthode classique ⚠️

### Syntaxe

```javascript
string.substring(debut, fin)
```

- **`debut`** : index de début (inclus)
- **`fin`** : index de fin (exclus) - optionnel

### Retourne

Une **nouvelle string** contenant la portion extraite.

### Utilisation de base

```javascript
const texte = "JavaScript";

console.log(texte.substring(0, 4));   // "Java"
console.log(texte.substring(4, 10));  // "Script"
console.log(texte.substring(4));      // "Script" (jusqu'à la fin)
```

Jusqu'ici, c'est identique à `slice()`.

### Comportements particuliers de substring() ⚠️

#### 1. Les indices négatifs sont traités comme 0

```javascript
const mot = "Bonjour";

console.log(mot.substring(-3));    // "Bonjour" (traité comme substring(0))
console.log(mot.substring(0, -3)); // "" (traité comme substring(0, 0))
```

**Problème** : Ce comportement est contre-intuitif et source d'erreurs !

#### 2. Les paramètres sont automatiquement inversés

Si `debut > fin`, `substring()` inverse automatiquement les paramètres :

```javascript
const texte = "JavaScript";

// Ces deux appels donnent le même résultat !
console.log(texte.substring(4, 0));  // "Java"
console.log(texte.substring(0, 4));  // "Java"

// Avec slice(), pas d'inversion
console.log(texte.slice(4, 0));      // "" (chaîne vide)
console.log(texte.slice(0, 4));      // "Java"
```

**Problème** : Là encore, ce comportement peut masquer des erreurs de logique !

---

## Comparaison : slice() vs substring()

### Tableau comparatif

| Caractéristique | slice() | substring() |
|-----------------|---------|-------------|
| **Indices négatifs** | ✅ Supportés | ❌ Traités comme 0 |
| **Inversion auto** | ❌ Non | ✅ Oui |
| **Prévisibilité** | ✅ Intuitive | ⚠️ Surprenante |
| **Recommandation** | ✅ **À utiliser** | ⚠️ Legacy |

### Exemples comparatifs

#### Avec indices positifs (identiques)

```javascript
const texte = "JavaScript";

console.log(texte.slice(0, 4));      // "Java"
console.log(texte.substring(0, 4));  // "Java"
// ✅ Résultat identique
```

#### Avec indices négatifs (différents)

```javascript
const texte = "JavaScript";

console.log(texte.slice(-6));        // "Script" ✅
console.log(texte.substring(-6));    // "JavaScript" ⚠️ (traité comme 0)

console.log(texte.slice(0, -6));     // "Java" ✅
console.log(texte.substring(0, -6)); // "" ⚠️ (traité comme substring(0, 0))
```

#### Avec paramètres inversés (différents)

```javascript
const texte = "JavaScript";

console.log(texte.slice(4, 0));      // "" ✅ (logique : début après fin)
console.log(texte.substring(4, 0));  // "Java" ⚠️ (inversion automatique)
```

---

## Pourquoi utiliser slice() ? ✅

### 1. Comportement cohérent et prévisible

```javascript
const texte = "Bonjour le monde";

// ✅ slice() est logique
console.log(texte.slice(-5));    // "monde" (5 derniers caractères)
console.log(texte.slice(8, 10)); // "le"

// ⚠️ substring() a des surprises
console.log(texte.substring(-5));    // "Bonjour le monde" (wtf?)
console.log(texte.substring(10, 8)); // "le" (inversion silencieuse)
```

### 2. Support des indices négatifs

Les indices négatifs sont extrêmement utiles pour extraire depuis la fin :

```javascript
const url = "https://example.com/page.html";

// ✅ Facile avec slice()
const extension = url.slice(-5);      // ".html"
const sanExtension = url.slice(0, -5); // "https://example.com/page"

// ⚠️ Compliqué avec substring()
const extension2 = url.substring(url.length - 5); // ".html"
const sanExtension2 = url.substring(0, url.length - 5);
```

### 3. Cohérence avec Array.slice()

JavaScript utilise aussi `slice()` pour les tableaux, avec la même syntaxe :

```javascript
const tableau = [1, 2, 3, 4, 5];
console.log(tableau.slice(1, 3));  // [2, 3]
console.log(tableau.slice(-2));    // [4, 5]

const texte = "12345";
console.log(texte.slice(1, 3));    // "23"
console.log(texte.slice(-2));      // "45"
// Même logique ! 🎉
```

---

## Cas d'usage courants

### 1. Extraire des sous-parties structurées

#### Code postal et ville

```javascript
const adresse = "75001 Paris";
const codePostal = adresse.slice(0, 5);
const ville = adresse.slice(6);

console.log(codePostal); // "75001"
console.log(ville);      // "Paris"
```

#### Date formatée

```javascript
const dateISO = "2025-12-05";
const annee = dateISO.slice(0, 4);
const mois = dateISO.slice(5, 7);
const jour = dateISO.slice(8, 10);

console.log(`${jour}/${mois}/${annee}`); // "05/12/2025"
```

### 2. Formatage de numéro de téléphone

```javascript
const telephone = "0612345678";

const formate = telephone.slice(0, 2) + " " +
                telephone.slice(2, 4) + " " +
                telephone.slice(4, 6) + " " +
                telephone.slice(6, 8) + " " +
                telephone.slice(8);

console.log(formate); // "06 12 34 56 78"
```

### 3. Masquage de données sensibles

```javascript
const carteBancaire = "1234567890123456";

// Masquer les 12 premiers chiffres
const masque = "************" + carteBancaire.slice(-4);
console.log(masque); // "************3456"
```

### 4. Extraction de nom d'utilisateur et domaine (email)

```javascript
const email = "alice.dupont@example.com";
const arobase = email.indexOf("@");

const utilisateur = email.slice(0, arobase);
const domaine = email.slice(arobase + 1);

console.log("Utilisateur :", utilisateur); // "alice.dupont"
console.log("Domaine :", domaine);         // "example.com"
```

### 5. Tronquer avec ellipses

```javascript
function tronquer(texte, longueurMax) {
    if (texte.length <= longueurMax) {
        return texte;
    }
    return texte.slice(0, longueurMax - 3) + "...";
}

const titre = "Un titre de blog extrêmement long qui doit être tronqué";
console.log(tronquer(titre, 30));
// "Un titre de blog extrêmem..."
```

### 6. Retirer un préfixe ou suffixe

```javascript
const commande = "/help";

// Retirer le préfixe "/"
if (commande.startsWith("/")) {
    const sansPrefixe = commande.slice(1);
    console.log(sansPrefixe); // "help"
}

const fichier = "document.txt";

// Retirer l'extension
if (fichier.endsWith(".txt")) {
    const sansSuffixe = fichier.slice(0, -4);
    console.log(sansSuffixe); // "document"
}
```

---

## Indices hors limites

Que se passe-t-il si vous utilisez des indices hors des limites de la string ?

### Avec slice()

```javascript
const mot = "Bonjour"; // longueur 7

console.log(mot.slice(0, 100));   // "Bonjour" (s'arrête à la fin)
console.log(mot.slice(10));       // "" (vide si début après la fin)
console.log(mot.slice(-100));     // "Bonjour" (traité comme 0)
console.log(mot.slice(5, 3));     // "" (début après fin)
```

**Comportement** : Toujours cohérent et sans erreur.

### Avec substring()

```javascript
const mot = "Bonjour";

console.log(mot.substring(0, 100));   // "Bonjour" (s'arrête à la fin)
console.log(mot.substring(10));       // "" (vide)
console.log(mot.substring(-100));     // "Bonjour" (traité comme 0)
console.log(mot.substring(5, 3));     // "nj" (inversion automatique)
```

---

## Combiner avec d'autres méthodes

### Avec indexOf() pour extraire dynamiquement

```javascript
const phrase = "Nom: Alice, Age: 25";

// Extraire le nom
const debutNom = phrase.indexOf(": ") + 2;
const finNom = phrase.indexOf(",");
const nom = phrase.slice(debutNom, finNom);
console.log(nom); // "Alice"

// Extraire l'âge
const debutAge = phrase.lastIndexOf(": ") + 2;
const age = phrase.slice(debutAge);
console.log(age); // "25"
```

### Avec trim() pour nettoyer

```javascript
const texte = "   Bonjour le monde   ";
const extrait = texte.slice(3, -3).trim();
console.log(extrait); // "Bonjour le monde"
```

### Avec toUpperCase() / toLowerCase()

```javascript
const titre = "javascript est génial";

// Première lettre en majuscule
const premiereLettreCapitale = titre.slice(0, 1).toUpperCase() + titre.slice(1);
console.log(premiereLettreCapitale); // "Javascript est génial"
```

---

## Astuce : créer une copie de string

Pour créer une copie d'une string (bien que rarement nécessaire) :

```javascript
const original = "JavaScript";

// Méthode 1 : slice() sans paramètres
const copie1 = original.slice();

// Méthode 2 : slice(0)
const copie2 = original.slice(0);

console.log(copie1); // "JavaScript"
console.log(copie2); // "JavaScript"
```

**Note** : En pratique, ce n'est presque jamais nécessaire car les strings sont immutables.

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier que l'index de fin est exclus

```javascript
const mot = "Bonjour";
//           0123456

// ❌ Pour extraire "Bon", on pourrait penser faire :
console.log(mot.slice(0, 2)); // "Bo" (pas "Bon"!)

// ✅ Il faut aller jusqu'à l'index 3 (exclus)
console.log(mot.slice(0, 3)); // "Bon"
```

### ❌ Erreur 2 : Utiliser substring() par habitude

```javascript
// ❌ Comportement imprévisible
const texte = "JavaScript";
const derniers = texte.substring(-6); // "JavaScript" (wtf?)

// ✅ Utilisez slice()
const derniers2 = texte.slice(-6);    // "Script" (logique!)
```

### ❌ Erreur 3 : Modifier la string originale

```javascript
let mot = "Bonjour";

// ❌ Ceci NE modifie PAS mot
mot.slice(0, 3);
console.log(mot); // "Bonjour" (inchangé)

// ✅ Il faut assigner le résultat
mot = mot.slice(0, 3);
console.log(mot); // "Bon"
```

### ❌ Erreur 4 : Confondre les indices positifs et négatifs

```javascript
const texte = "JavaScript";

// ❌ slice(0, -0) ne fait rien de spécial
console.log(texte.slice(0, -0)); // "" (car -0 === 0)

// ✅ Pour tout extraire sauf le dernier caractère
console.log(texte.slice(0, -1)); // "JavaScrip"
```

---

## Mémo des indices négatifs

Pour maîtriser les indices négatifs avec `slice()` :

```javascript
const texte = "Bonjour";
//  Positif:  0  1  2  3  4  5  6
//            B  o  n  j  o  u  r
//  Négatif: -7 -6 -5 -4 -3 -2 -1

// Extraire depuis la fin
texte.slice(-1)      // "r"     (dernier)
texte.slice(-2)      // "ur"    (2 derniers)
texte.slice(-3)      // "our"   (3 derniers)

// Extraire sauf la fin
texte.slice(0, -1)   // "Bonjou" (tout sauf dernier)
texte.slice(0, -2)   // "Bonjo"  (tout sauf 2 derniers)

// Combiner les deux
texte.slice(-5, -2)  // "njo"   (de -5 à -2 exclus)
```

---

## Points clés à retenir

✅ **`slice()`** est la méthode moderne recommandée pour extraire des sous-chaînes

✅ **Syntaxe** : `string.slice(debut, fin)` où `fin` est **exclus**

✅ **Indices négatifs** : comptent depuis la fin (`-1` = dernier caractère)

✅ `slice()` sans second paramètre extrait **jusqu'à la fin**

✅ `slice(0)` ou `slice()` copie toute la string

✅ **`substring()`** est une méthode legacy avec comportement contre-intuitif

✅ Les strings étant **immutables**, ces méthodes **créent une nouvelle string**

✅ Toujours **assigner le résultat** à une variable pour le conserver

---

## Recommandations

### ✅ À FAIRE

```javascript
// Utilisez slice() avec indices négatifs
const derniers = texte.slice(-5);
const sansDerniers = texte.slice(0, -5);

// Combinez avec d'autres méthodes
const extrait = texte.slice(0, 10).toUpperCase();

// Assignez toujours le résultat
const nouveau = texte.slice(5);
```

### ❌ À ÉVITER

```javascript
// N'utilisez pas substring() (sauf code legacy)
const extrait = texte.substring(-5); // comportement imprévisible

// N'oubliez pas d'assigner
texte.slice(0, 5); // ❌ Le résultat est perdu
```

---

## Dans la prochaine section

Dans la section **5.3.6 - Transformation : toLowerCase, toUpperCase, trim**, nous découvrirons les méthodes pour transformer et nettoyer les strings.

---


⏭️ [Transformation : toLowerCase, toUpperCase, trim](/05-javascript-moderne-fondamentaux/03-strings-modernes/06-transformation.md)
