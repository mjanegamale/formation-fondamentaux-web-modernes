🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.3 - Destructuring de tableaux 🆕

## Qu'est-ce que le destructuring ?

Le **destructuring** (ou déstructuration en français) est une syntaxe moderne introduite avec **ES6** qui permet d'extraire facilement des valeurs d'un tableau et de les assigner à des variables.

C'est une façon plus élégante et plus lisible d'accéder aux éléments d'un tableau.

---

## Le problème : méthode classique

Avant ES6, pour extraire plusieurs valeurs d'un tableau, il fallait faire :

```javascript
const fruits = ["pomme", "banane", "orange"];

const fruit1 = fruits[0];
const fruit2 = fruits[1];
const fruit3 = fruits[2];

console.log(fruit1);  // "pomme"
console.log(fruit2);  // "banane"
console.log(fruit3);  // "orange"
```

C'est **répétitif** et peu pratique, surtout avec beaucoup de variables.

---

## La solution moderne : destructuring

Avec le destructuring, vous pouvez extraire toutes les valeurs en une seule ligne :

```javascript
const fruits = ["pomme", "banane", "orange"];

const [fruit1, fruit2, fruit3] = fruits;

console.log(fruit1);  // "pomme"
console.log(fruit2);  // "banane"
console.log(fruit3);  // "orange"
```

### Comment ça fonctionne ?

Les crochets `[]` du côté gauche indiquent que vous voulez destructurer un tableau :

```javascript
const [variable1, variable2, variable3] = tableau;
```

JavaScript assigne automatiquement :
- `variable1` reçoit `tableau[0]`
- `variable2` reçoit `tableau[1]`
- `variable3` reçoit `tableau[2]`

---

## Syntaxe de base

### Extraire les premiers éléments

```javascript
const nombres = [10, 20, 30, 40, 50];

const [premier, deuxieme] = nombres;

console.log(premier);   // 10
console.log(deuxieme);  // 20
```

Vous n'êtes **pas obligé** d'extraire tous les éléments. Les autres restent dans le tableau original.

### Noms de variables personnalisés

Vous pouvez utiliser n'importe quel nom de variable :

```javascript
const coordonnees = [48.8566, 2.3522];

const [latitude, longitude] = coordonnees;

console.log(latitude);   // 48.8566
console.log(longitude);  // 2.3522
```

---

## Ignorer des éléments

Si vous ne voulez pas certains éléments, laissez simplement un espace vide avec une virgule :

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi"];

const [premier, , troisieme] = fruits;
//             ↑ virgule pour ignorer "banane"

console.log(premier);    // "pomme"
console.log(troisieme);  // "orange"
```

### Ignorer plusieurs éléments

```javascript
const nombres = [1, 2, 3, 4, 5];

const [premier, , , quatrieme] = nombres;
//             ↑  ↑ ignorer 2 et 3

console.log(premier);     // 1
console.log(quatrieme);   // 4
```

---

## Valeurs par défaut

Si un élément n'existe pas dans le tableau, vous pouvez définir une **valeur par défaut** :

```javascript
const couleurs = ["rouge", "vert"];

const [couleur1, couleur2, couleur3 = "bleu"] = couleurs;

console.log(couleur1);  // "rouge"
console.log(couleur2);  // "vert"
console.log(couleur3);  // "bleu" (valeur par défaut)
```

### Sans valeur par défaut

Si aucune valeur par défaut n'est fournie, la variable vaut `undefined` :

```javascript
const fruits = ["pomme"];

const [fruit1, fruit2] = fruits;

console.log(fruit1);  // "pomme"
console.log(fruit2);  // undefined
```

### Quand la valeur par défaut est utilisée

La valeur par défaut est utilisée **uniquement** si l'élément est `undefined` :

```javascript
const tab1 = [1, undefined, 3];
const [a, b = 10, c] = tab1;
console.log(b);  // 10 (valeur par défaut car undefined)

const tab2 = [1, null, 3];
const [x, y = 10, z] = tab2;
console.log(y);  // null (pas la valeur par défaut, car null ≠ undefined)
```

---

## Rest operator (...) dans le destructuring

Le **rest operator** (`...`) permet de capturer tous les éléments restants dans un nouveau tableau :

```javascript
const nombres = [1, 2, 3, 4, 5];

const [premier, deuxieme, ...autres] = nombres;

console.log(premier);   // 1
console.log(deuxieme);  // 2
console.log(autres);    // [3, 4, 5]
```

### Points importants

Le rest operator doit toujours être **en dernière position** :

```javascript
const nombres = [1, 2, 3, 4, 5];

// ✅ Correct
const [a, ...reste] = nombres;

// ❌ Erreur : rest doit être le dernier
const [...reste, dernier] = nombres;  // Syntaxe invalide !
```

### Capturer tout sauf le premier

```javascript
const fruits = ["pomme", "banane", "orange", "kiwi", "mangue"];

const [premierFruit, ...autresFruits] = fruits;

console.log(premierFruit);   // "pomme"
console.log(autresFruits);   // ["banane", "orange", "kiwi", "mangue"]
```

---

## Échange de variables (swap)

Le destructuring permet d'échanger facilement les valeurs de deux variables :

### Méthode classique (avant ES6)

```javascript
let a = 1;
let b = 2;

// Besoin d'une variable temporaire
let temp = a;
a = b;
b = temp;

console.log(a);  // 2
console.log(b);  // 1
```

### Méthode moderne avec destructuring

```javascript
let a = 1;
let b = 2;

[a, b] = [b, a];  // Échange en une ligne !

console.log(a);  // 2
console.log(b);  // 1
```

Pas besoin de variable temporaire ! 🎉

### Échanger plus de deux variables

```javascript
let x = 1, y = 2, z = 3;

[x, y, z] = [z, x, y];  // Rotation des valeurs

console.log(x, y, z);  // 3 1 2
```

---

## Destructuring de tableaux imbriqués

Vous pouvez destructurer des tableaux à plusieurs niveaux :

```javascript
const donnees = [1, [2, 3], 4];

const [a, [b, c], d] = donnees;

console.log(a);  // 1
console.log(b);  // 2
console.log(c);  // 3
console.log(d);  // 4
```

### Exemple avec une grille

```javascript
const grille = [
  [1, 2],
  [3, 4]
];

const [[a, b], [c, d]] = grille;

console.log(a);  // 1
console.log(b);  // 2
console.log(c);  // 3
console.log(d);  // 4
```

---

## Destructuring avec des fonctions

Le destructuring est particulièrement utile avec les valeurs retournées par des fonctions.

### Fonction retournant un tableau

```javascript
function getCoordonnees() {
  return [48.8566, 2.3522];
}

const [lat, long] = getCoordonnees();

console.log(lat);   // 48.8566
console.log(long);  // 2.3522
```

### Sans destructuring (moins lisible)

```javascript
function getCoordonnees() {
  return [48.8566, 2.3522];
}

const coords = getCoordonnees();
const lat = coords[0];
const long = coords[1];
```

---

## Exemples pratiques

### Exemple 1 : Résultat d'une opération

```javascript
function diviser(dividende, diviseur) {
  const quotient = Math.floor(dividende / diviseur);
  const reste = dividende % diviseur;
  return [quotient, reste];
}

const [quotient, reste] = diviser(17, 5);

console.log(`17 ÷ 5 = ${quotient} reste ${reste}`);
// "17 ÷ 5 = 3 reste 2"
```

### Exemple 2 : Premiers et derniers éléments

```javascript
const scores = [95, 87, 92, 88, 90];

const [meilleurScore, , , , plusBas] = scores;

console.log("Meilleur :", meilleurScore);  // 95
console.log("Plus bas :", plusBas);        // 90
```

### Exemple 3 : Séparation de données

```javascript
const utilisateur = ["Alice", 25, "Paris", "Développeuse"];

const [nom, age, ville, metier] = utilisateur;

console.log(`${nom}, ${age} ans, ${metier} à ${ville}`);
// "Alice, 25 ans, Développeuse à Paris"
```

### Exemple 4 : Parsing de chaîne avec split()

```javascript
const dateString = "2025-12-25";

const [annee, mois, jour] = dateString.split("-");

console.log("Année :", annee);   // "2025"
console.log("Mois :", mois);     // "12"
console.log("Jour :", jour);     // "25"
```

### Exemple 5 : Première valeur et le reste

```javascript
const taches = ["Réviser le code", "Écrire tests", "Déployer", "Documenter"];

const [tacheUrgente, ...autresTaches] = taches;

console.log("À faire en premier :", tacheUrgente);
// "Réviser le code"

console.log("Pour plus tard :", autresTaches);
// ["Écrire tests", "Déployer", "Documenter"]
```

---

## Comparaison : avec et sans destructuring

### Scénario : Extraction de données

**Sans destructuring** (méthode classique) :

```javascript
const reponseAPI = ["John Doe", "john@example.com", 30, "Développeur"];

const nom = reponseAPI[0];
const email = reponseAPI[1];
const age = reponseAPI[2];
const profession = reponseAPI[3];
```

**Avec destructuring** (moderne) :

```javascript
const reponseAPI = ["John Doe", "john@example.com", 30, "Développeur"];

const [nom, email, age, profession] = reponseAPI;
```

Plus court, plus lisible ! ✨

---

## Cas d'usage avancés

### Destructuring dans une boucle

```javascript
const coordonnees = [
  [48.8566, 2.3522],   // Paris
  [51.5074, -0.1278],  // Londres
  [40.7128, -74.0060]  // New York
];

for (const [lat, long] of coordonnees) {
  console.log(`Latitude: ${lat}, Longitude: ${long}`);
}
```

### Avec des paramètres de fonction

```javascript
function afficherPoint([x, y]) {
  console.log(`Point : (${x}, ${y})`);
}

afficherPoint([10, 20]);  // "Point : (10, 20)"
```

---

## Points clés à retenir

- ✅ Syntaxe moderne ES6+ pour extraire des valeurs d'un tableau
- ✅ Syntaxe : `const [var1, var2] = tableau`
- ✅ Plus lisible et concis que l'accès par index
- ✅ Ignorer des éléments avec des virgules vides
- ✅ Valeurs par défaut possibles : `[a = 10, b = 20] = tableau`
- ✅ Rest operator pour capturer les éléments restants : `[first, ...rest]`
- ✅ Permet d'échanger des variables facilement
- ✅ Fonctionne avec les tableaux imbriqués
- ✅ Très utile avec les fonctions qui retournent des tableaux

---

## Quand utiliser le destructuring ?

- ✅ **Utilisez-le** quand vous devez extraire plusieurs valeurs d'un tableau
- ✅ **Utilisez-le** pour échanger des variables
- ✅ **Utilisez-le** avec les valeurs de retour de fonctions
- ✅ **N'en abusez pas** si vous n'avez besoin que d'un seul élément (utilisez `tableau[0]`)

---

## Pour aller plus loin

Dans la prochaine section, vous découvrirez le **spread operator** qui permet de copier et fusionner des tableaux de manière élégante.

---


⏭️ [Spread operator pour les tableaux](/05-javascript-moderne-fondamentaux/08-tableaux-modernes/04-spread-operator-tableaux.md)
