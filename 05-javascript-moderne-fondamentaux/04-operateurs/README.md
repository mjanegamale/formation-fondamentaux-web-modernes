🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4 - Opérateurs

## Introduction

Bienvenue dans cette section dédiée aux **opérateurs** en JavaScript ! Les opérateurs sont les symboles et mots-clés qui permettent d'effectuer des opérations sur les valeurs : calculs mathématiques, comparaisons, tests logiques, et bien plus encore.

### Qu'est-ce qu'un opérateur ?

Un **opérateur** est un symbole ou un mot-clé qui effectue une opération sur une ou plusieurs valeurs (appelées **opérandes**) et produit un résultat.

```javascript
// Opérateur arithmétique
const somme = 5 + 3;        // + est l'opérateur, 5 et 3 sont les opérandes

// Opérateur de comparaison
const estMajeur = age >= 18; // >= est l'opérateur

// Opérateur logique
const peutVoter = estMajeur && estCitoyen; // && est l'opérateur
```

Les opérateurs sont les **outils de base** qui vous permettent de manipuler les données et de prendre des décisions dans votre code.

---

## Pourquoi cette section est cruciale ?

Les opérateurs sont omniprésents dans **tout** code JavaScript :
- 🧮 **Calculs** : prix totaux, moyennes, conversions d'unités
- ✅ **Validations** : vérifier l'âge, valider des formulaires, tester des conditions
- 🔀 **Décisions** : afficher un message selon le contexte, autoriser un accès
- 🔄 **Logique métier** : implémenter les règles de votre application
- 🎯 **Filtrage** : sélectionner des données selon des critères

**Impossible de programmer sans maîtriser les opérateurs** - c'est vraiment la base de la logique de programmation.

---

## Approche moderne : Les bonnes pratiques

Cette section met l'accent sur les **pratiques modernes** et les pièges à éviter absolument :

### ⚠️ Point critique : === vs ==

**LA règle la plus importante** : utilisez **TOUJOURS** `===` (égalité stricte) et **JAMAIS** `==` (égalité faible).

```javascript
// ❌ À ÉVITER : == fait des conversions bizarres
console.log(5 == "5");      // true (wtf?)
console.log(0 == false);    // true (wtf?)

// ✅ À UTILISER : === vérifie valeur ET type
console.log(5 === "5");     // false (correct)
console.log(5 === 5);       // true
```

Cette règle simple vous évitera d'innombrables bugs !

### 🆕 Opérateurs modernes ES2020+

Vous découvrirez aussi les opérateurs les plus récents qui rendent le code plus sûr et plus élégant :
- **`??`** (Nullish Coalescing) - Pour des valeurs par défaut intelligentes
- **`?.`** (Optional Chaining) - Pour accéder aux propriétés sans erreur

Ces opérateurs sont désormais **standards** et très largement utilisés.

---

## Ce que vous allez apprendre

Cette section couvre **5 chapitres** qui vous donneront une maîtrise complète des opérateurs en JavaScript :

### 1. Opérateurs arithmétiques
Les bases des mathématiques en JavaScript : addition, soustraction, multiplication, division, modulo et exponentiation.

### 2. Opérateurs de comparaison (=== vs ==)
Comparer des valeurs avec une attention particulière sur la différence CRUCIALE entre `===` et `==`.

### 3. Opérateurs logiques
Combiner des conditions avec ET (`&&`), OU (`||`) et NON (`!`) pour créer des tests complexes.

### 4. Opérateur ternaire
Un raccourci élégant pour écrire des conditions simples sur une seule ligne.

### 5. Opérateurs modernes 🆕
Les nouveaux opérateurs `??` et `?.` qui simplifient grandement la gestion de valeurs null et undefined.

---

## Prérequis

Pour suivre cette section, vous devez avoir compris :
- ✅ Les variables et types de données (Section 5.2)
- ✅ Les strings et leurs manipulations (Section 5.3)
- ✅ La différence entre `true` et `false`

Si ces concepts ne sont pas clairs, revenez aux sections précédentes.

---

## Concept clé : Les valeurs booléennes

Beaucoup d'opérateurs retournent des **valeurs booléennes** : `true` (vrai) ou `false` (faux).

```javascript
const age = 25;

// Opérateurs de comparaison retournent des booléens
console.log(age >= 18);      // true
console.log(age === 15);     // false

// Opérateurs logiques retournent des booléens
console.log(age > 18 && age < 30);  // true
```

Ces valeurs booléennes sont essentielles pour :
- Les conditions `if...else`
- Les boucles `while`
- Les ternaires `? :`
- Les filtres de tableaux

---

## Vue d'ensemble : Moderne vs Legacy

| Catégorie | ⚠️ Legacy (à éviter) | ✅ Moderne (recommandé) |
|-----------|---------------------|------------------------|
| **Égalité** | `==` (conversion auto) | `===` (stricte) |
| **Inégalité** | `!=` (conversion auto) | `!==` (stricte) |
| **Valeur par défaut** | `\|\|` (problèmes avec 0, "") | `??` (null/undefined only) |
| **Accès propriété** | `obj && obj.prop` | `obj?.prop` |

**Philosophie** : Privilégiez **toujours** les opérateurs modernes pour un code plus sûr et prévisible !

---

## Les catégories d'opérateurs

JavaScript propose plusieurs catégories d'opérateurs :

### 1. Opérateurs arithmétiques
Effectuent des calculs mathématiques.
```javascript
const somme = 10 + 5;        // 15
const produit = 10 * 5;      // 50
const reste = 10 % 3;        // 1
```

### 2. Opérateurs de comparaison
Comparent deux valeurs et retournent `true` ou `false`.
```javascript
console.log(10 > 5);         // true
console.log(10 === 5);       // false
```

### 3. Opérateurs logiques
Combinent ou inversent des conditions booléennes.
```javascript
const resultat = true && false;  // false
const inverse = !true;           // false
```

### 4. Opérateurs d'affectation
Assignent des valeurs aux variables.
```javascript
let x = 5;
x += 3;  // x = x + 3 → x vaut maintenant 8
```

### 5. Opérateurs spéciaux
Opérateurs modernes ou particuliers comme `??`, `?.`, l'opérateur ternaire, etc.

---

## Comment utiliser cette section ?

### Pour les débutants complets
Suivez les chapitres **dans l'ordre** du 5.4.1 au 5.4.5. Chaque chapitre construit sur le précédent.

**Parcours recommandé** :
1. Opérateurs arithmétiques (bases)
2. Opérateurs de comparaison (**CRUCIAL** : === vs ==)
3. Opérateurs logiques (combiner des conditions)
4. Opérateur ternaire (raccourci élégant)
5. Opérateurs modernes (outils puissants)

### Pour ceux qui ont des bases
Concentrez-vous sur :
- **5.4.2** (=== vs ==) - Même si vous connaissez, lisez cette partie !
- **5.4.5** (Opérateurs modernes) - Les nouveautés ES2020+

### Approche pratique
- 💻 **Testez TOUT** dans la console du navigateur
- 🔧 **Expérimentez** : changez les valeurs, voyez ce qui se passe
- 📝 **Notez** les pièges et erreurs courantes
- 🎯 **Pratiquez** avec les cas d'usage fournis

---

## Plan détaillé de la section

### 1. **[Opérateurs arithmétiques](./01-operateurs-arithmetiques.md)**
   - Les 6 opérateurs : `+`, `-`, `*`, `/`, `%`, `**`
   - Addition vs concaténation (piège du `+`)
   - Modulo : comprendre le reste de la division
   - Opérateurs composés : `+=`, `-=`, `*=`, etc.
   - Ordre des opérations et priorité

### 2. **[Opérateurs de comparaison](./02-operateurs-comparaison.md)** ⚠️ CRUCIAL
   - `===` et `!==` (stricte - À UTILISER)
   - `==` et `!=` (faible - À ÉVITER)
   - Pourquoi === est indispensable
   - `>`, `<`, `>=`, `<=`
   - Comparaison de strings
   - Erreurs courantes mortelles

### 3. **[Opérateurs logiques](./03-operateurs-logiques.md)**
   - `&&` (ET) - Toutes les conditions vraies
   - `||` (OU) - Au moins une condition vraie
   - `!` (NON) - Inversion
   - Court-circuit (short-circuit evaluation)
   - Valeurs truthy et falsy
   - Combiner les opérateurs

### 4. **[Opérateur ternaire](./04-operateur-ternaire.md)**
   - Syntaxe : `condition ? siVrai : siFaux`
   - Quand l'utiliser vs if...else
   - Ternaires imbriqués (avec précaution)
   - Dans les expressions et template literals
   - Cas d'usage élégants

### 5. **[Opérateurs modernes](./05-operateurs-modernes.md)** 🆕
   - `??` (Nullish Coalescing) - Valeurs par défaut intelligentes
   - `?.` (Optional Chaining) - Accès sécurisé
   - Différence `??` vs `||` (important !)
   - Combiner `??` et `?.`
   - Migration du code ancien vers moderne

---

## Conventions utilisées

Dans cette section, vous verrez ces symboles :

- 🆕 : Fonctionnalité moderne ES6+ (à privilégier)
- ⚠️ : Opérateur legacy ou piège dangereux
- ✅ : Bonne pratique recommandée
- ❌ : Erreur courante à éviter
- 💡 : Astuce importante
- 🔧 : Outil ou technique de debug

---

## Pièges majeurs à connaître

### ⚠️ Piège 1 : == vs ===
```javascript
// ❌ DANGER
if (age == "18") { } // true même si age est un nombre !

// ✅ SÛR
if (age === 18) { }  // false si age est une string
```

### ⚠️ Piège 2 : = vs === vs ==
```javascript
// = → affectation
let x = 5;

// == → égalité faible (À ÉVITER)
if (x == "5") { } // true

// === → égalité stricte (À UTILISER)
if (x === 5) { }  // true
```

### ⚠️ Piège 3 : Le + avec strings et nombres
```javascript
console.log(5 + 3);     // 8 (addition)
console.log("5" + 3);   // "53" (concaténation)
console.log(5 + "3");   // "53" (concaténation)
```

### ⚠️ Piège 4 : Division par zéro
```javascript
console.log(10 / 0);    // Infinity (pas d'erreur !)
console.log(0 / 0);     // NaN
```

---

## Testez vos connaissances

Au fur et à mesure, posez-vous ces questions :

- Quelle est la différence entre `==` et `===` ?
- Pourquoi `5 + "3"` donne `"53"` et pas `8` ?
- Comment vérifier si un nombre est pair ?
- Que retourne `true && false` ?
- Que retourne `true || false` ?
- Quand utiliser `??` plutôt que `||` ?
- Comment accéder à `user.profile.name` sans risque d'erreur ?

Si vous ne savez pas répondre maintenant, pas d'inquiétude ! Cette section va tout clarifier. 😊

---

## Les opérateurs dans le contexte

Les opérateurs ne sont pas isolés - ils sont utilisés partout :

### Dans les conditions
```javascript
if (age >= 18 && hasPermit) {
    console.log("Peut conduire");
}
```

### Dans les boucles
```javascript
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

### Dans les fonctions
```javascript
function calculerTotal(prix, quantite) {
    return prix * quantite;
}
```

### Dans les tableaux
```javascript
const adultes = utilisateurs.filter(u => u.age >= 18);
```

---

## Objectifs d'apprentissage

À la fin de cette section, vous serez capable de :

- ✅ Effectuer des calculs mathématiques en JavaScript
- ✅ Comparer des valeurs **correctement** (avec ===)
- ✅ Comprendre la différence mortelle entre == et ===
- ✅ Combiner plusieurs conditions avec &&, ||, !
- ✅ Écrire des conditions concises avec l'opérateur ternaire
- ✅ Utiliser les opérateurs modernes ?? et ?.
- ✅ Éviter les pièges courants qui causent des bugs
- ✅ Choisir le bon opérateur pour chaque situation

---

## Règles d'or à retenir

Avant de commencer, gravez ces règles dans votre esprit :

1. **TOUJOURS** utiliser `===` et `!==` (jamais `==` ou `!=`)
2. **Attention** au `+` qui peut faire addition OU concaténation
3. **Vérifier** avant de diviser par zéro
4. **Utiliser** `??` pour les valeurs par défaut (pas `||`)
5. **Utiliser** `?.` pour accéder aux propriétés en toute sécurité
6. **Tester** vos conditions dans la console pour bien comprendre

---

## Pourquoi tant insister sur === ?

Parce que `==` est **la source de bugs n°1** chez les débutants JavaScript !

```javascript
// Comportements surprenants de ==
console.log(0 == false);        // true (wtf?)
console.log("" == false);       // true (wtf?)
console.log(null == undefined); // true (wtf?)
console.log([] == false);       // true (wtf?)
```

**Solution simple** : n'utilisez JAMAIS `==`, toujours `===` !

```javascript
// Comportement prévisible de ===
console.log(0 === false);       // false (correct)
console.log("" === false);      // false (correct)
console.log(null === undefined); // false (correct)
```

---

## Progression recommandée

```
Jour 1-2 : Opérateurs arithmétiques
  → Maîtriser les calculs de base
  → Comprendre le modulo %

Jour 3-4 : Opérateurs de comparaison
  → === vs == (CRUCIAL !)
  → Pratiquer les comparaisons

Jour 5 : Opérateurs logiques
  → Combiner des conditions
  → Comprendre truthy/falsy

Jour 6 : Opérateur ternaire
  → Conditions sur une ligne

Jour 7 : Opérateurs modernes
  → ?? et ?.
  → Moderniser son code
```

---

## Ressources complémentaires

- **Console du navigateur** : Testez tous les exemples en direct
- **MDN Web Docs** : Documentation de référence
- **DevTools** : Inspectez les valeurs et leurs types
- **ESLint** : Configure des règles pour éviter == automatiquement

---

## Prêt à commencer ?

Les opérateurs sont les **outils fondamentaux** qui vous permettent de transformer des données statiques en programmes dynamiques et intelligents. Chaque opérateur résout un problème spécifique, et leur maîtrise est absolument essentielle.

**Point important** : Ne passez pas à la section suivante sans avoir compris la différence entre `===` et `==`. C'est vraiment critique !

Commençons par les bases avec les opérateurs arithmétiques !

---


⏭️ [Opérateurs arithmétiques](/05-javascript-moderne-fondamentaux/04-operateurs/01-operateurs-arithmetiques.md)
