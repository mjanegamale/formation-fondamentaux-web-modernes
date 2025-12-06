🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.1 - Création et manipulation de strings

## Introduction

Les **strings** (chaînes de caractères) sont l'un des types de données les plus utilisés en JavaScript. Une string est simplement une séquence de caractères utilisée pour représenter du texte : des mots, des phrases, des messages, etc.

Dans cette section, nous allons découvrir comment créer et manipuler des strings en JavaScript.

---

## Qu'est-ce qu'une string ?

Une string est une donnée textuelle. Elle peut contenir :
- Des lettres : `"Bonjour"`
- Des chiffres (traités comme du texte) : `"12345"`
- Des symboles : `"@#$%"`
- Des espaces : `"Hello World"`
- Même des strings vides : `""`

**Important** : En JavaScript, les strings sont **immutables**, c'est-à-dire qu'une fois créées, elles ne peuvent pas être modifiées directement. Chaque manipulation crée une nouvelle string.

---

## Les trois façons de créer une string

En JavaScript moderne, il existe **trois façons** de créer des strings, chacune avec ses particularités.

### 1. Guillemets simples `' '`

```javascript
const prenom = 'Alice';
const message = 'Bonjour tout le monde !';
```

✅ **Utilisation courante** : C'est la notation la plus simple et rapide à taper.

### 2. Guillemets doubles `" "`

```javascript
const prenom = "Bob";
const message = "Bienvenue sur notre site";
```

✅ **Équivalent aux guillemets simples** : Il n'y a aucune différence fonctionnelle entre les deux.

### 3. Backticks (accent grave) `` ` ` `` - Template Literals

```javascript
const prenom = `Charlie`;
const message = `Ceci est une string moderne`;
```

✅ **Fonctionnalités avancées** : Les backticks permettent l'interpolation de variables et les strings sur plusieurs lignes (nous verrons cela en détail dans la section suivante 5.3.2).

---

## Quelle notation choisir ?

Pour l'instant, retenez simplement :
- **Guillemets simples** ou **doubles** : peu importe, choisissez-en un et restez cohérent dans votre code
- **Backticks** : nous les découvrirons en détail dans la prochaine section

**Conseil** : Beaucoup de développeurs utilisent les guillemets simples par défaut, car ils sont plus rapides à taper (pas besoin de la touche Shift).

---

## Échappement de caractères

Parfois, vous devez inclure des caractères spéciaux dans vos strings. C'est là qu'intervient l'**échappement** avec le backslash `\`.

### Guillemets à l'intérieur d'une string

Si vous utilisez des guillemets simples pour délimiter votre string, vous ne pouvez pas directement utiliser un guillemet simple à l'intérieur :

```javascript
// ❌ ERREUR : JavaScript pense que la string se termine au 2ème guillemet
const phrase = 'C'est une erreur';
```

**Solutions :**

**Option 1** : Échapper le guillemet avec `\`
```javascript
const phrase = 'C\'est correct maintenant';
console.log(phrase); // Affiche : C'est correct maintenant
```

**Option 2** : Utiliser des guillemets doubles à l'extérieur
```javascript
const phrase = "C'est plus simple ainsi";
console.log(phrase); // Affiche : C'est plus simple ainsi
```

**Option 3** : Utiliser des backticks
```javascript
const phrase = `C'est encore mieux`;
console.log(phrase); // Affiche : C'est encore mieux
```

### Caractères spéciaux courants

JavaScript reconnaît plusieurs séquences d'échappement :

| Séquence | Résultat | Description |
|----------|----------|-------------|
| `\n` | Saut de ligne | Crée une nouvelle ligne |
| `\t` | Tabulation | Crée une tabulation |
| `\\` | Backslash | Affiche un backslash |
| `\"` | Guillemet double | Affiche un guillemet double |
| `\'` | Guillemet simple | Affiche un guillemet simple |

**Exemples :**

```javascript
const avecSautDeLigne = "Première ligne\nDeuxième ligne";
console.log(avecSautDeLigne);
// Affiche :
// Première ligne
// Deuxième ligne

const avecTabulation = "Nom:\tAlice";
console.log(avecTabulation);
// Affiche : Nom:    Alice

const chemin = "C:\\Users\\Documents\\fichier.txt";
console.log(chemin);
// Affiche : C:\Users\Documents\fichier.txt
```

---

## Concaténation : assembler des strings

La **concaténation** consiste à assembler plusieurs strings pour en former une seule.

### Avec l'opérateur `+`

C'est la méthode classique pour combiner des strings :

```javascript
const prenom = "Alice";
const nom = "Dupont";

const nomComplet = prenom + " " + nom;
console.log(nomComplet); // Affiche : Alice Dupont
```

**Avec des variables et du texte :**

```javascript
const age = 25;
const message = "J'ai " + age + " ans";
console.log(message); // Affiche : J'ai 25 ans
```

### Concaténation avec `+=`

L'opérateur `+=` permet d'ajouter du contenu à une string existante :

```javascript
let phrase = "Bonjour";
phrase += " tout";
phrase += " le monde";
console.log(phrase); // Affiche : Bonjour tout le monde
```

**Note** : Bien que pratique, la concaténation avec `+` peut devenir difficile à lire avec beaucoup de variables. C'est pourquoi les **template literals** (section suivante) sont préférés en JavaScript moderne.

---

## Conversion en string

JavaScript peut automatiquement convertir d'autres types de données en strings lors de la concaténation :

```javascript
const nombre = 42;
const texte = "La réponse est " + nombre;
console.log(texte); // Affiche : La réponse est 42
console.log(typeof texte); // Affiche : string
```

### Conversion explicite avec `String()`

Vous pouvez également convertir explicitement une valeur en string :

```javascript
const nombre = 123;
const string = String(nombre);
console.log(string); // Affiche : "123"
console.log(typeof string); // Affiche : string

const booleen = true;
const texte = String(booleen);
console.log(texte); // Affiche : "true"
```

### Conversion avec `.toString()`

La plupart des types de données ont une méthode `.toString()` :

```javascript
const nombre = 456;
const texte = nombre.toString();
console.log(texte); // Affiche : "456"
```

---

## String vide

Une **string vide** est une string qui ne contient aucun caractère :

```javascript
const stringVide = "";
console.log(stringVide.length); // Affiche : 0
```

Les strings vides sont utiles pour :
- Initialiser une variable avant de la remplir
- Réinitialiser le contenu d'un champ de formulaire
- Vérifier si une string contient du texte

```javascript
let message = "";

if (message === "") {
    console.log("Le message est vide");
}
```

---

## Comparaison de strings

Vous pouvez comparer des strings avec les opérateurs de comparaison :

```javascript
const mot1 = "chat";
const mot2 = "chat";
const mot3 = "chien";

console.log(mot1 === mot2); // true (identiques)
console.log(mot1 === mot3); // false (différents)
console.log(mot1 !== mot3); // true (différents)
```

**Attention à la casse** : JavaScript distingue majuscules et minuscules :

```javascript
const mot1 = "Bonjour";
const mot2 = "bonjour";

console.log(mot1 === mot2); // false (la casse est différente)
```

---

## Accéder aux caractères individuels

Bien que nous verrons les propriétés des strings en détail plus tard, sachez qu'il est possible d'accéder à un caractère spécifique d'une string :

### Avec la notation entre crochets `[]`

```javascript
const mot = "Bonjour";

console.log(mot[0]); // Affiche : B (premier caractère)
console.log(mot[1]); // Affiche : o (deuxième caractère)
console.log(mot[6]); // Affiche : r (septième caractère)
```

**Important** : En JavaScript, l'indexation commence à **0** (zéro) :
- Le premier caractère est à l'index 0
- Le deuxième caractère est à l'index 1
- Et ainsi de suite...

---

## Points clés à retenir

✅ **Une string est une séquence de caractères** représentant du texte

✅ **Trois notations** : guillemets simples `' '`, doubles `" "`, ou backticks `` ` ` ``

✅ **Les strings sont immutables** : chaque manipulation crée une nouvelle string

✅ **Échappement** : utilisez `\` pour inclure des caractères spéciaux (`\'`, `\"`, `\n`, etc.)

✅ **Concaténation** : assemblez des strings avec l'opérateur `+`

✅ **Conversion** : JavaScript convertit automatiquement les nombres en strings lors de la concaténation

✅ **Comparaison** : utilisez `===` pour comparer des strings (attention à la casse !)

---

## Dans la prochaine section

Dans la section **5.3.2 - Template Literals**, nous découvrirons la syntaxe moderne des strings avec les backticks, qui permet d'intégrer facilement des variables et de créer des strings sur plusieurs lignes de façon élégante.

---


⏭️ [Template Literals (backticks) et interpolation \`${}\`](/05-javascript-moderne-fondamentaux/03-strings-modernes/02-template-literals.md)
