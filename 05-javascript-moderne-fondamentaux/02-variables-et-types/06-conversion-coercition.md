🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.2.6 - Conversion et coercition de types

## Introduction

JavaScript est un langage **dynamiquement typé** : une variable peut changer de type au cours de l'exécution. Mais parfois, vous avez besoin de transformer explicitement un type en un autre (un string en number, par exemple), ou JavaScript le fait automatiquement pour vous.

Dans cette section, nous allons explorer :
- 🔄 **Conversion explicite** : quand VOUS convertissez un type (intentionnel)
- ⚡ **Coercition implicite** : quand JAVASCRIPT convertit automatiquement (automatique)

> 💡 **Pourquoi c'est important** : La conversion de types est source de nombreux bugs chez les débutants. Comprendre comment JavaScript gère les types vous évitera bien des surprises !

## Qu'est-ce que la conversion de types ?

### Définition simple

La **conversion de types** (ou **cast**) consiste à transformer une valeur d'un type vers un autre type.

### Exemple de la vie réelle

Imaginez que vous avez :
- Un nombre écrit sur papier : `"42"` (c'est du texte, un string)
- Vous voulez l'utiliser dans un calcul : `42` (c'est un nombre, un number)

Il faut "convertir" le texte en nombre.

## Conversion vs Coercition

### Conversion explicite (intentionnelle)

**Vous** décidez de convertir un type en un autre avec une fonction ou un opérateur.

```javascript
const texte = "42";
const nombre = Number(texte);  // Conversion explicite
console.log(nombre);  // 42 (number)
```

### Coercition implicite (automatique)

**JavaScript** convertit automatiquement les types quand c'est nécessaire.

```javascript
const texte = "42";
const resultat = texte * 2;  // JavaScript convertit "42" en 42 automatiquement
console.log(resultat);  // 84 (number)
```

### Analogie

- **Conversion** : Vous traduisez consciemment un texte d'une langue à une autre
- **Coercition** : Un traducteur automatique traduit pour vous (parfois avec des erreurs !)

## Conversion explicite vers String

### Méthode 1 : String()

La fonction `String()` convertit n'importe quelle valeur en string.

```javascript
// Number vers String
console.log(String(42));           // "42"
console.log(String(3.14));         // "3.14"
console.log(String(-10));          // "-10"

// Boolean vers String
console.log(String(true));         // "true"
console.log(String(false));        // "false"

// Undefined et Null vers String
console.log(String(undefined));    // "undefined"
console.log(String(null));         // "null"

// Avec des variables
const age = 25;
const ageString = String(age);
console.log(ageString);            // "25"
console.log(typeof ageString);     // "string"
```

### Méthode 2 : .toString()

Méthode disponible sur les nombres, booléens, etc.

```javascript
const nombre = 42;
console.log(nombre.toString());    // "42"

const vrai = true;
console.log(vrai.toString());      // "true"

// ⚠️ Ne fonctionne pas avec null et undefined
// null.toString();       // ❌ TypeError
// undefined.toString();  // ❌ TypeError
```

### Méthode 3 : Concaténation avec string vide

Astuce rapide : ajouter `""` à une valeur.

```javascript
const nombre = 42;
const texte = nombre + "";
console.log(texte);                // "42"
console.log(typeof texte);         // "string"

console.log(true + "");            // "true"
console.log(null + "");            // "null"
```

### Méthode 4 : Template literals

```javascript
const age = 25;
const ageString = `${age}`;
console.log(ageString);            // "25"
console.log(typeof ageString);     // "string"
```

### Comparaison des méthodes

| Méthode | Avantages | Inconvénients |
|---------|-----------|---------------|
| `String()` | ✅ Fonctionne avec tout | Verbeux |
| `.toString()` | ✅ Clair | ❌ Échoue avec null/undefined |
| `+ ""` | ✅ Court | Moins lisible |
| Template literals | ✅ Moderne | Overkill pour une simple conversion |

**Recommandation :** Utilisez `String()` pour la clarté et la sécurité.

## Conversion explicite vers Number

### Méthode 1 : Number()

La fonction `Number()` convertit une valeur en number.

```javascript
// String vers Number
console.log(Number("42"));         // 42
console.log(Number("3.14"));       // 3.14
console.log(Number("-10"));        // -10

// Boolean vers Number
console.log(Number(true));         // 1
console.log(Number(false));        // 0

// Cas particuliers
console.log(Number(""));           // 0 (string vide = 0)
console.log(Number("   "));        // 0 (espaces = 0)
console.log(Number(null));         // 0
console.log(Number(undefined));    // NaN

// Conversions invalides
console.log(Number("hello"));      // NaN
console.log(Number("42px"));       // NaN
console.log(Number("12.5.3"));     // NaN
```

### Méthode 2 : parseInt() - Entiers

Convertit un string en **entier** (nombre sans décimales).

```javascript
console.log(parseInt("42"));       // 42
console.log(parseInt("42.7"));     // 42 (ignore les décimales)
console.log(parseInt("-10"));      // -10

// Ignore ce qui suit le nombre
console.log(parseInt("42px"));     // 42
console.log(parseInt("100 euros")); // 100

// S'arrête au premier caractère non-numérique
console.log(parseInt("abc123"));   // NaN (commence par une lettre)

// Avec une base (optionnelle)
console.log(parseInt("1010", 2));  // 10 (binaire vers décimal)
console.log(parseInt("FF", 16));   // 255 (hexadécimal vers décimal)
```

> 💡 **Conseil** : Spécifiez toujours la base (radix) pour éviter les ambiguïtés : `parseInt("10", 10)`

### Méthode 3 : parseFloat() - Décimaux

Convertit un string en **nombre décimal**.

```javascript
console.log(parseFloat("42.7"));       // 42.7
console.log(parseFloat("3.14159"));    // 3.14159
console.log(parseFloat("0.5"));        // 0.5

// Ignore ce qui suit le nombre
console.log(parseFloat("42.5px"));     // 42.5
console.log(parseFloat("3.14 mètres"));// 3.14

// S'arrête au premier caractère invalide
console.log(parseFloat("abc"));        // NaN
```

### Méthode 4 : Opérateur + unaire

Astuce rapide : mettre `+` devant une valeur.

```javascript
console.log(+"42");                // 42
console.log(+"3.14");              // 3.14
console.log(+"-10");               // -10

const texte = "100";
const nombre = +texte;
console.log(nombre);               // 100
console.log(typeof nombre);        // "number"

// Avec boolean et autres
console.log(+true);                // 1
console.log(+false);               // 0
console.log(+"");                  // 0
console.log(+"hello");             // NaN
```

### Comparaison des méthodes

| Méthode | Usage | Exemple | Résultat |
|---------|-------|---------|----------|
| `Number()` | Conversion stricte | `Number("42px")` | `NaN` |
| `parseInt()` | Extraire un entier | `parseInt("42px")` | `42` |
| `parseFloat()` | Extraire un décimal | `parseFloat("3.14m")` | `3.14` |
| `+` unaire | Conversion rapide | `+"42"` | `42` |

**Recommandation :**
- `Number()` pour des valeurs "propres" (strings numériques purs)
- `parseInt()` ou `parseFloat()` pour extraire des nombres de strings mixtes

### Vérifier si la conversion a réussi

```javascript
function convertirEnNombre(valeur) {
    const nombre = Number(valeur);

    if (isNaN(nombre)) {
        console.log("Conversion échouée");
        return null;
    }

    return nombre;
}

console.log(convertirEnNombre("42"));      // 42
console.log(convertirEnNombre("hello"));   // null (+ message)
```

## Conversion explicite vers Boolean

### Méthode 1 : Boolean()

La fonction `Boolean()` convertit une valeur en boolean.

```javascript
// Valeurs falsy (deviennent false)
console.log(Boolean(false));       // false
console.log(Boolean(0));           // false
console.log(Boolean(""));          // false
console.log(Boolean(null));        // false
console.log(Boolean(undefined));   // false
console.log(Boolean(NaN));         // false

// Toutes les autres valeurs sont truthy (deviennent true)
console.log(Boolean(true));        // true
console.log(Boolean(1));           // true
console.log(Boolean(-1));          // true
console.log(Boolean("hello"));     // true
console.log(Boolean("0"));         // true ⚠️ (string non vide)
console.log(Boolean(" "));         // true ⚠️ (espace)
console.log(Boolean([]));          // true ⚠️ (tableau vide)
console.log(Boolean({}));          // true ⚠️ (objet vide)
```

### Méthode 2 : Double négation (!!)

Astuce rapide : utiliser `!!` (double NOT).

```javascript
console.log(!!"hello");            // true
console.log(!!42);                 // true
console.log(!!"");                 // false
console.log(!!0);                  // false

const nom = "Alice";
const aNom = !!nom;
console.log(aNom);                 // true
console.log(typeof aNom);          // "boolean"
```

**Comment ça marche :**
- `!` inverse la valeur et la convertit en boolean
- `!!` inverse deux fois, donc revient au boolean original

```javascript
const valeur = "hello";
console.log(!valeur);              // false (inverse et convertit)
console.log(!!valeur);             // true (inverse deux fois)
```

### Rappel : Valeurs falsy et truthy

**6 valeurs falsy (deviennent false) :**
```javascript
false, 0, "", null, undefined, NaN
```

**Tout le reste est truthy (devient true) :**
```javascript
true, 1, -1, "0", "false", " ", [], {}, function() {}, ...
```

### Pièges courants

```javascript
// ⚠️ Le string "0" est truthy !
console.log(Boolean("0"));         // true
console.log(Boolean(0));           // false

// ⚠️ Le string "false" est truthy !
console.log(Boolean("false"));     // true
console.log(Boolean(false));       // false

// ⚠️ Un tableau vide est truthy !
console.log(Boolean([]));          // true
console.log(Boolean([].length));   // false (0 est falsy)

// ⚠️ Un objet vide est truthy !
console.log(Boolean({}));          // true
```

## Coercition implicite (automatique)

JavaScript convertit automatiquement les types dans certaines situations.

### 1. Addition avec strings (concaténation)

Quand l'opérateur `+` est utilisé avec un string, **tout devient string**.

```javascript
// Number + String = String
console.log(5 + "3");              // "53" (string)
console.log("Hello" + 5);          // "Hello5" (string)

// Multiple additions
console.log(1 + 2 + "3");          // "33" (1+2=3, puis "3"+"3"="33")
console.log("1" + 2 + 3);          // "123" ("1"+"2"="12", puis "12"+"3"="123")

// Boolean + String = String
console.log(true + " story");      // "true story" (string)
console.log("Result: " + false);   // "Result: false" (string)

// Null/Undefined + String = String
console.log("Value: " + null);     // "Value: null" (string)
console.log(undefined + "!");      // "undefined!" (string)
```

> 🐛 **Piège fréquent** : L'addition peut créer des résultats inattendus !

```javascript
const a = 5;
const b = 10;
console.log("Total : " + a + b);   // "Total : 510" ⚠️ (pas 15 !)

// Solution : utiliser des parenthèses
console.log("Total : " + (a + b)); // "Total : 15" ✅
```

### 2. Autres opérateurs arithmétiques (-, *, /, %)

Avec `-`, `*`, `/`, `%`, JavaScript convertit en **number**.

```javascript
// String vers Number (automatique)
console.log("10" - 5);             // 5 (number)
console.log("10" * 2);             // 20 (number)
console.log("10" / 2);             // 5 (number)
console.log("10" % 3);             // 1 (number)

// Multiple opérations
console.log("20" - "5");           // 15 (number)
console.log("6" * "7");            // 42 (number)

// Conversions invalides
console.log("hello" - 5);          // NaN
console.log("10px" * 2);           // NaN
```

### 3. Comparaisons

#### Avec == (égalité non stricte)

`==` effectue une **conversion de type** avant de comparer.

```javascript
// Number et String
console.log(5 == "5");             // true ⚠️ (convertit "5" en 5)
console.log(0 == "");              // true ⚠️ (convertit "" en 0)

// Boolean et Number
console.log(true == 1);            // true ⚠️ (true devient 1)
console.log(false == 0);           // true ⚠️ (false devient 0)

// Null et Undefined
console.log(null == undefined);    // true ⚠️ (cas spécial)

// Cas bizarres
console.log("0" == false);         // true ⚠️ (les deux deviennent 0)
console.log("" == false);          // true ⚠️ (les deux deviennent 0)
```

#### Avec === (égalité stricte) ✅

`===` compare **sans conversion de type**.

```javascript
// Number et String
console.log(5 === "5");            // false ✅ (types différents)
console.log(0 === "");             // false ✅

// Boolean et Number
console.log(true === 1);           // false ✅
console.log(false === 0);          // false ✅

// Null et Undefined
console.log(null === undefined);   // false ✅

// Cas clairs
console.log("0" === false);        // false ✅
console.log("" === false);         // false ✅
```

> 🎯 **Règle d'or** : Utilisez **toujours** `===` et `!==` (égalité stricte) sauf cas très particulier.

### 4. Contexte booléen (if, while, etc.)

Dans les conditions, JavaScript convertit automatiquement en boolean.

```javascript
// Avec if
if ("hello") {
    console.log("String non vide est truthy");  // S'exécute
}

if (0) {
    console.log("Ne s'exécute pas");  // 0 est falsy
}

// Avec while
let i = 5;
while (i) {  // i est converti en boolean
    console.log(i);
    i--;
}
// Affiche : 5, 4, 3, 2, 1 (s'arrête à 0 qui est falsy)

// Avec opérateur ternaire
const age = 18;
const status = age ? "a un âge" : "pas d'âge";  // age converti en boolean
```

### 5. Opérateurs logiques (&&, ||)

Ces opérateurs ne retournent pas forcément un boolean !

#### ET logique (&&)

Retourne la **première valeur falsy** ou la **dernière valeur** si toutes sont truthy.

```javascript
console.log(true && "hello");      // "hello" (toutes truthy, retourne la dernière)
console.log("hello" && 42);        // 42
console.log("hello" && "world");   // "world"

console.log(false && "hello");     // false (première falsy)
console.log(0 && "hello");         // 0
console.log("" && "hello");        // ""
console.log(null && "hello");      // null
```

**Utilisation pratique :**
```javascript
const utilisateur = { nom: "Alice" };

// Accès conditionnel
const nom = utilisateur && utilisateur.nom;
console.log(nom);  // "Alice"

// Si utilisateur est null
const utilisateur2 = null;
const nom2 = utilisateur2 && utilisateur2.nom;
console.log(nom2);  // null (pas d'erreur)
```

#### OU logique (||)

Retourne la **première valeur truthy** ou la **dernière valeur** si toutes sont falsy.

```javascript
console.log(false || "hello");     // "hello" (première truthy)
console.log(0 || 42);              // 42
console.log("" || "default");      // "default"
console.log(null || "fallback");   // "fallback"

console.log("hello" || "world");   // "hello" (première truthy)
console.log(42 || 0);              // 42
```

**Utilisation pratique : valeurs par défaut**
```javascript
function saluer(nom) {
    nom = nom || "Visiteur";  // Si nom est falsy, utilise "Visiteur"
    console.log(`Bonjour ${nom} !`);
}

saluer("Alice");   // "Bonjour Alice !"
saluer();          // "Bonjour Visiteur !"
saluer("");        // "Bonjour Visiteur !" ⚠️ (string vide est falsy)
```

> 🆕 **Moderne** : En ES2020+, utilisez plutôt l'opérateur `??` (nullish coalescing) que nous verrons plus tard.

## Exemples de bugs courants liés à la coercition

### Bug 1 : Addition vs Concaténation

```javascript
// Bug
const a = "5";
const b = 10;
const total = a + b;
console.log(total);  // "510" ⚠️ (pas 15)

// Solution
const total2 = Number(a) + b;
console.log(total2);  // 15 ✅
```

### Bug 2 : Comparaison avec ==

```javascript
// Bug
if (valeur == true) {  // Piège !
    console.log("Vrai");
}

// Exemple surprenant
console.log("2" == true);   // false ⚠️
console.log("1" == true);   // true ⚠️
console.log("0" == false);  // true ⚠️

// Solution : utiliser === ou vérifier directement
if (valeur === true) { }  // ✅
if (valeur) { }           // ✅ (si on veut juste truthy/falsy)
```

### Bug 3 : String vide vs 0

```javascript
const input = "";

// Bug
if (input == 0) {
    console.log("C'est zéro");  // ⚠️ S'exécute (car "" == 0)
}

// Solution
if (input === 0) {
    console.log("C'est vraiment zéro");  // ✅ Ne s'exécute pas
}

// Ou vérifier le type
if (typeof input === "number" && input === 0) { }
```

### Bug 4 : Array/Object dans conditions

```javascript
const tableau = [];

// Piège
if (tableau) {
    console.log("Tableau existe");  // S'exécute (tableau vide est truthy)
}

// Solution : vérifier la longueur
if (tableau.length > 0) {
    console.log("Tableau non vide");  // ✅
}
```

## Tableaux récapitulatifs

### Conversion vers String

| Valeur | `String()` | `.toString()` | `+ ""` |
|--------|-----------|---------------|---------|
| `42` | `"42"` | `"42"` | `"42"` |
| `true` | `"true"` | `"true"` | `"true"` |
| `null` | `"null"` | ❌ Error | `"null"` |
| `undefined` | `"undefined"` | ❌ Error | `"undefined"` |

### Conversion vers Number

| Valeur | `Number()` | `parseInt()` | `parseFloat()` | `+` unaire |
|--------|-----------|--------------|----------------|-----------|
| `"42"` | `42` | `42` | `42` | `42` |
| `"42.7"` | `42.7` | `42` | `42.7` | `42.7` |
| `"42px"` | `NaN` | `42` | `42` | `NaN` |
| `""` | `0` | `NaN` | `NaN` | `0` |
| `true` | `1` | `NaN` | `NaN` | `1` |
| `false` | `0` | `NaN` | `NaN` | `0` |
| `null` | `0` | `NaN` | `NaN` | `0` |
| `undefined` | `NaN` | `NaN` | `NaN` | `NaN` |

### Conversion vers Boolean

| Valeur | `Boolean()` | `!!` | Résultat |
|--------|------------|------|----------|
| `false` | `false` | `false` | falsy |
| `0` | `false` | `false` | falsy |
| `""` | `false` | `false` | falsy |
| `null` | `false` | `false` | falsy |
| `undefined` | `false` | `false` | falsy |
| `NaN` | `false` | `false` | falsy |
| `"0"` | `true` | `true` | truthy ⚠️ |
| `[]` | `true` | `true` | truthy ⚠️ |
| `{}` | `true` | `true` | truthy ⚠️ |

## Bonnes pratiques

### ✅ À faire

1. **Convertissez explicitement quand nécessaire**
   ```javascript
   const texte = "42";
   const nombre = Number(texte);  // ✅ Clair et explicite
   ```

2. **Utilisez === au lieu de ==**
   ```javascript
   if (valeur === 5) { }  // ✅ Pas de conversion implicite
   ```

3. **Vérifiez les conversions avant de les utiliser**
   ```javascript
   const nombre = Number(input);
   if (!isNaN(nombre)) {
       // Utiliser nombre
   }
   ```

4. **Utilisez des parenthèses pour clarifier**
   ```javascript
   const resultat = "Total : " + (a + b);  // ✅ Clair
   ```

5. **Privilégiez les conversions explicites lisibles**
   ```javascript
   const nombre = Number(texte);  // ✅ Clair
   const nombre2 = +texte;        // ⚠️ Moins clair pour les débutants
   ```

### ❌ À éviter

1. **Compter sur la coercition implicite**
   ```javascript
   if (valeur == true) { }     // ❌ Imprévisible
   if (valeur === true) { }    // ✅ Clair
   ```

2. **Utiliser + pour convertir en string**
   ```javascript
   const texte = nombre + "";  // ❌ Peu clair
   const texte = String(nombre); // ✅ Explicite
   ```

3. **Oublier les parenthèses dans les calculs**
   ```javascript
   "Total: " + 5 + 10;         // ❌ "Total: 510"
   "Total: " + (5 + 10);       // ✅ "Total: 15"
   ```

4. **Supposer qu'un tableau/objet vide est falsy**
   ```javascript
   if ([]) { }                 // ⚠️ Toujours vrai
   if ([].length) { }          // ✅ Vérifie la longueur
   ```

## Exemples pratiques complets

### Exemple 1 : Calculatrice sécurisée

```javascript
function calculer(a, b, operation) {
    // Convertir les entrées en nombres
    const num1 = Number(a);
    const num2 = Number(b);

    // Vérifier que les conversions ont réussi
    if (isNaN(num1) || isNaN(num2)) {
        return "Erreur : entrées invalides";
    }

    // Calculer selon l'opération
    switch (operation) {
        case "+":
            return num1 + num2;
        case "-":
            return num1 - num2;
        case "*":
            return num1 * num2;
        case "/":
            if (num2 === 0) {
                return "Erreur : division par zéro";
            }
            return num1 / num2;
        default:
            return "Erreur : opération inconnue";
    }
}

console.log(calculer("10", "5", "+"));     // 15
console.log(calculer("10", "5", "*"));     // 50
console.log(calculer("hello", "5", "+"));  // "Erreur : entrées invalides"
console.log(calculer("10", "0", "/"));     // "Erreur : division par zéro"
```

### Exemple 2 : Validation de formulaire

```javascript
function validerAge(input) {
    // Convertir en nombre
    const age = Number(input);

    // Vérifier que c'est un nombre valide
    if (isNaN(age)) {
        return { valide: false, message: "L'âge doit être un nombre" };
    }

    // Vérifier que c'est un entier
    if (!Number.isInteger(age)) {
        return { valide: false, message: "L'âge doit être un nombre entier" };
    }

    // Vérifier la plage
    if (age < 0 || age > 150) {
        return { valide: false, message: "L'âge doit être entre 0 et 150" };
    }

    return { valide: true, age: age };
}

console.log(validerAge("25"));      // { valide: true, age: 25 }
console.log(validerAge("25.5"));    // { valide: false, message: "..." }
console.log(validerAge("abc"));     // { valide: false, message: "..." }
console.log(validerAge("-5"));      // { valide: false, message: "..." }
```

### Exemple 3 : Gestion de valeurs par défaut

```javascript
function creerUtilisateur(nom, age, ville) {
    // Conversion et valeurs par défaut
    return {
        nom: String(nom || "Anonyme"),
        age: Number(age) || 0,
        ville: String(ville || "Non renseigné")
    };
}

console.log(creerUtilisateur("Alice", 25, "Paris"));
// { nom: "Alice", age: 25, ville: "Paris" }

console.log(creerUtilisateur("", "", ""));
// { nom: "Anonyme", age: 0, ville: "Non renseigné" }

console.log(creerUtilisateur());
// { nom: "Anonyme", age: 0, ville: "Non renseigné" }
```

## En résumé

### Conversion explicite (vous contrôlez)

| Vers | Méthode recommandée | Exemple |
|------|-------------------|---------|
| **String** | `String()` | `String(42)` → `"42"` |
| **Number** | `Number()` | `Number("42")` → `42` |
| **Boolean** | `Boolean()` | `Boolean("hi")` → `true` |

### Coercition implicite (JavaScript décide)

| Contexte | Comportement |
|----------|-------------|
| **String + autre** | Tout devient string |
| **Nombre - / * / %** | Tout devient number |
| **Comparaison ==** | Conversion avant comparaison |
| **Comparaison ===** | ✅ Pas de conversion |
| **Condition (if)** | Conversion en boolean |

### Points clés

- ✅ **Préférez la conversion explicite** : plus claire et prévisible
- ✅ **Utilisez toujours ===** : évite les conversions implicites
- ✅ **Vérifiez les conversions** : utilisez `isNaN()` après `Number()`
- ⚠️ **Attention à +** : concatène avec strings, additionne avec numbers
- ⚠️ **Valeurs truthy/falsy** : apprenez les 6 valeurs falsy par cœur

> 🎯 **À retenir** : La coercition implicite peut créer des bugs subtils. Convertissez explicitement vos types quand c'est important, et utilisez toujours `===` pour les comparaisons !

## Prochaine étape

Félicitations ! Vous avez maintenant une solide compréhension des variables et des types en JavaScript. Dans la prochaine section, nous allons découvrir les **strings modernes** et toutes leurs puissantes méthodes !

---


💡 **Citation** : "Il y a deux types de bugs : les erreurs de syntaxe et les erreurs de type. Les erreurs de syntaxe sont faciles à trouver. Les erreurs de type... beaucoup moins !" - Comprendre la conversion de types vous évitera des heures de debugging !

⏭️ [Strings modernes](/05-javascript-moderne-fondamentaux/03-strings-modernes/README.md)
