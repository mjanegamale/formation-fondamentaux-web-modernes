🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.1 - Déclaration de fonction classique

## Introduction

Une **fonction** est un bloc de code réutilisable qui accomplit une tâche spécifique. Au lieu de répéter le même code plusieurs fois dans votre programme, vous pouvez l'écrire une seule fois dans une fonction et l'appeler chaque fois que vous en avez besoin.

Imaginez une fonction comme une recette de cuisine : vous écrivez les instructions une fois, puis vous pouvez les suivre autant de fois que nécessaire.

## Pourquoi utiliser des fonctions ?

Les fonctions permettent de :

- **Réutiliser du code** : Écrire une fois, utiliser plusieurs fois
- **Organiser le code** : Diviser un programme complexe en petites parties compréhensibles
- **Faciliter la maintenance** : Modifier le code à un seul endroit plutôt que partout
- **Rendre le code plus lisible** : Donner des noms significatifs aux blocs de code

## Syntaxe de base

La déclaration de fonction classique suit cette structure :

```javascript
function nomDeLaFonction() {
  // Code à exécuter
}
```

**Décortiquons cette syntaxe :**

1. **`function`** : Le mot-clé qui indique que vous déclarez une fonction
2. **`nomDeLaFonction`** : Le nom que vous donnez à votre fonction (suivez les règles de nommage JavaScript)
3. **`()`** : Les parenthèses qui contiendront les paramètres (pour l'instant vides)
4. **`{}`** : Les accolades qui délimitent le corps de la fonction (le code à exécuter)

## Premier exemple simple

Créons une fonction qui affiche un message de bienvenue :

```javascript
function direBonjour() {
  console.log("Bonjour ! Bienvenue dans le monde de JavaScript.");
}
```

### Appeler (exécuter) la fonction

Déclarer une fonction ne l'exécute pas automatiquement. Pour l'utiliser, vous devez **l'appeler** :

```javascript
direBonjour(); // Affiche : "Bonjour ! Bienvenue dans le monde de JavaScript."
```

Vous pouvez appeler la même fonction plusieurs fois :

```javascript
direBonjour();
direBonjour();
direBonjour();

// Résultat :
// Bonjour ! Bienvenue dans le monde de JavaScript.
// Bonjour ! Bienvenue dans le monde de JavaScript.
// Bonjour ! Bienvenue dans le monde de JavaScript.
```

## Fonctions avec paramètres

Les fonctions deviennent vraiment puissantes quand elles peuvent accepter des **paramètres** (aussi appelés **arguments**). Les paramètres sont des valeurs que vous passez à la fonction pour personnaliser son comportement.

### Syntaxe avec paramètres

```javascript
function nomDeLaFonction(parametre1, parametre2) {
  // Code utilisant les paramètres
}
```

### Exemple avec un paramètre

```javascript
function saluer(prenom) {
  console.log("Bonjour " + prenom + " !");
}

// Appels avec différents arguments
saluer("Alice");   // Affiche : "Bonjour Alice !"
saluer("Thomas");  // Affiche : "Bonjour Thomas !"
saluer("Sophie");  // Affiche : "Bonjour Sophie !"
```

Dans cet exemple :
- `prenom` est le **paramètre** (la variable dans la déclaration)
- `"Alice"`, `"Thomas"`, `"Sophie"` sont les **arguments** (les valeurs réelles passées lors de l'appel)

### Exemple avec plusieurs paramètres

```javascript
function presenter(prenom, age) {
  console.log("Je m'appelle " + prenom + " et j'ai " + age + " ans.");
}

presenter("Julie", 25);    // Affiche : "Je m'appelle Julie et j'ai 25 ans."
presenter("Marc", 32);     // Affiche : "Je m'appelle Marc et j'ai 32 ans."
```

**⚠️ Important :** L'ordre des arguments est crucial ! Le premier argument correspond au premier paramètre, le deuxième au deuxième, etc.

## Fonctions avec valeur de retour

Jusqu'ici, nos fonctions affichaient des messages. Mais les fonctions peuvent aussi **retourner** des valeurs qui peuvent être utilisées ailleurs dans le code.

### Le mot-clé `return`

```javascript
function additionner(a, b) {
  return a + b;
}

const resultat = additionner(5, 3);
console.log(resultat); // Affiche : 8
```

**Points importants sur `return` :**

1. `return` termine immédiatement l'exécution de la fonction
2. La valeur après `return` est renvoyée à l'endroit où la fonction a été appelée
3. Le code après `return` n'est jamais exécuté

```javascript
function exemplerReturn(x) {
  return x * 2;
  console.log("Ce message ne s'affichera jamais"); // Code mort !
}
```

### Exemple pratique : calculer une surface

```javascript
function calculerSurfaceRectangle(longueur, largeur) {
  const surface = longueur * largeur;
  return surface;
}

const surface1 = calculerSurfaceRectangle(10, 5);
console.log("La surface est : " + surface1 + " m²"); // Affiche : "La surface est : 50 m²"

const surface2 = calculerSurfaceRectangle(8, 3);
console.log("La surface est : " + surface2 + " m²"); // Affiche : "La surface est : 24 m²"
```

Ou de manière plus concise :

```javascript
function calculerSurfaceRectangle(longueur, largeur) {
  return longueur * largeur;
}
```

## Exemples pratiques complets

### Exemple 1 : Vérifier si un nombre est pair

```javascript
function estPair(nombre) {
  return nombre % 2 === 0;
}

console.log(estPair(4));   // Affiche : true
console.log(estPair(7));   // Affiche : false
console.log(estPair(10));  // Affiche : true
```

### Exemple 2 : Convertir des températures

```javascript
function celsiusVersFahrenheit(celsius) {
  const fahrenheit = (celsius * 9/5) + 32;
  return fahrenheit;
}

console.log(celsiusVersFahrenheit(0));    // Affiche : 32
console.log(celsiusVersFahrenheit(20));   // Affiche : 68
console.log(celsiusVersFahrenheit(100));  // Affiche : 212
```

### Exemple 3 : Créer un message personnalisé

```javascript
function creerMessage(nom, ville) {
  const message = "Bonjour " + nom + ", comment se passe la vie à " + ville + " ?";
  return message;
}

const msg1 = creerMessage("Alice", "Paris");
console.log(msg1); // Affiche : "Bonjour Alice, comment se passe la vie à Paris ?"

const msg2 = creerMessage("Bob", "Lyon");
console.log(msg2); // Affiche : "Bonjour Bob, comment se passe la vie à Lyon ?"
```

## Fonctions sans return

Une fonction qui ne retourne pas de valeur explicitement retourne automatiquement `undefined` :

```javascript
function afficherMessage(texte) {
  console.log(texte);
  // Pas de return
}

const resultat = afficherMessage("Hello");
console.log(resultat); // Affiche : undefined
```

## Nommage des fonctions : bonnes pratiques

### Règles à respecter

✅ **Utilisez des verbes d'action** : Les fonctions font des choses
```javascript
function calculer() { }       // Bon
function afficher() { }       // Bon
function envoyer() { }        // Bon
```

✅ **Soyez descriptif et précis**
```javascript
function calculerTotalPanier() { }              // Bon
function afficherMessageBienvenue() { }         // Bon
function verifierEmailValide() { }              // Bon
```

✅ **Utilisez le camelCase** : première lettre en minuscule, majuscules pour les mots suivants
```javascript
function calculerSurfaceCercle() { }   // Bon
function envoyerEmailConfirmation() { } // Bon
```

❌ **À éviter**
```javascript
function f() { }                  // Trop vague
function fonction1() { }          // Pas descriptif
function CalculerTotal() { }      // Ne pas commencer par une majuscule
function calculer_total() { }     // Évitez les underscores (style Python)
```

## Portée des variables dans les fonctions

Les variables déclarées à l'intérieur d'une fonction ne sont accessibles que dans cette fonction (portée locale) :

```javascript
function exemple() {
  const messageLocal = "Je suis local";
  console.log(messageLocal); // Fonctionne
}

exemple();
console.log(messageLocal); // ❌ Erreur : messageLocal n'est pas défini
```

Les variables déclarées en dehors sont accessibles partout (portée globale) :

```javascript
const messageGlobal = "Je suis global";

function exemple() {
  console.log(messageGlobal); // Fonctionne
}

exemple(); // Affiche : "Je suis global"
console.log(messageGlobal); // Fonctionne aussi
```

## Hoisting : Les fonctions remontent !

Une particularité des déclarations de fonctions classiques est le **hoisting** (remontée). JavaScript « remonte » les déclarations de fonctions au début du code, ce qui permet de les appeler avant leur déclaration :

```javascript
// Ceci fonctionne ! ✅
direBonjour();

function direBonjour() {
  console.log("Bonjour !");
}
```

**Note :** Bien que cela fonctionne, il est recommandé de déclarer vos fonctions avant de les utiliser pour une meilleure lisibilité du code.

## Différence : déclaration vs appel

Il est crucial de comprendre la différence :

```javascript
// DÉCLARATION : Créer la fonction
function additionner(a, b) {
  return a + b;
}

// APPEL : Utiliser la fonction
additionner(5, 3);  // ✅ Avec parenthèses et arguments

// Référence à la fonction (sans l'exécuter)
console.log(additionner);  // Affiche le code de la fonction
```

## Quand utiliser les fonctions ?

Créez une fonction quand :

- ✅ Vous répétez le même code plusieurs fois
- ✅ Un bloc de code accomplit une tâche claire et distincte
- ✅ Vous voulez rendre votre code plus lisible et organisé
- ✅ Vous devez tester ou déboguer une partie spécifique de votre code

## Points clés à retenir

1. **Une fonction est un bloc de code réutilisable** qui accomplit une tâche spécifique

2. **Syntaxe de base** :
   ```javascript
   function nomFonction(parametres) {
     // code
     return valeur;
   }
   ```

3. **Appeler une fonction** : utilisez son nom suivi de parenthèses `nomFonction()`

4. **Paramètres** : permettent de passer des informations à la fonction

5. **Return** : permet de renvoyer une valeur, termine l'exécution de la fonction

6. **Hoisting** : les déclarations de fonctions sont "remontées" au début du code

7. **Portée** : les variables dans une fonction sont locales à cette fonction

8. **Nommage** : utilisez des verbes d'action en camelCase

## Prochaines étapes

Maintenant que vous maîtrisez la déclaration classique de fonctions, vous êtes prêt à explorer :

- Les **expressions de fonction** (5.6.2)
- Les **fonctions fléchées** (arrow functions) - la syntaxe moderne ES6+ (5.6.3)
- Les **paramètres par défaut** (5.6.5)
- Et bien plus encore !

Les fonctions sont au cœur de JavaScript, et vous les utiliserez constamment dans vos projets. Prenez le temps de bien comprendre ces concepts fondamentaux avant d'avancer.

---

**Note :** Dans le développement moderne, vous rencontrerez également d'autres façons de déclarer des fonctions (expressions de fonction, arrow functions). La déclaration classique reste cependant fondamentale à comprendre et est toujours largement utilisée, notamment pour sa clarté et son hoisting.

⏭️ [Expression de fonction](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/02-expression-fonction.md)
