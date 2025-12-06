🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.5.2 - Switch et case

## Introduction

La structure `switch` est une alternative aux longues chaînes de `if...else if...else` lorsqu'on doit comparer une même variable à plusieurs valeurs différentes. Elle rend le code plus lisible et plus organisé dans certaines situations.

Imaginez un menu de restaurant : selon le numéro choisi, vous recevez un plat différent. Le `switch` fonctionne exactement comme ça !

---

## Pourquoi utiliser `switch` ?

### Avec `if...else if` (moins lisible)

```javascript
const jour = 3;

if (jour === 1) {
  console.log("Lundi");
} else if (jour === 2) {
  console.log("Mardi");
} else if (jour === 3) {
  console.log("Mercredi");
} else if (jour === 4) {
  console.log("Jeudi");
} else if (jour === 5) {
  console.log("Vendredi");
} else if (jour === 6) {
  console.log("Samedi");
} else if (jour === 7) {
  console.log("Dimanche");
}
```

### Avec `switch` (plus lisible)

```javascript
const jour = 3;

switch (jour) {
  case 1:
    console.log("Lundi");
    break;
  case 2:
    console.log("Mardi");
    break;
  case 3:
    console.log("Mercredi");
    break;
  case 4:
    console.log("Jeudi");
    break;
  case 5:
    console.log("Vendredi");
    break;
  case 6:
    console.log("Samedi");
    break;
  case 7:
    console.log("Dimanche");
    break;
}
// Affiche : "Mercredi"
```

**Avantage :** Avec `switch`, on écrit la variable une seule fois, et on liste clairement toutes les valeurs possibles.

---

## Syntaxe de base

```javascript
switch (expression) {
  case valeur1:
    // Code exécuté si expression === valeur1
    break;
  case valeur2:
    // Code exécuté si expression === valeur2
    break;
  case valeur3:
    // Code exécuté si expression === valeur3
    break;
  default:
    // Code exécuté si aucune valeur ne correspond
}
```

### Les éléments clés

1. **`switch (expression)`** : L'expression à évaluer (souvent une variable)
2. **`case valeur:`** : Chaque cas possible
3. **`break;`** : Arrête l'exécution et sort du switch
4. **`default:`** : Cas par défaut si aucune valeur ne correspond (optionnel)

---

## Premier exemple simple

```javascript
const fruit = "pomme";

switch (fruit) {
  case "pomme":
    console.log("🍎 C'est une pomme");
    break;
  case "banane":
    console.log("🍌 C'est une banane");
    break;
  case "orange":
    console.log("🍊 C'est une orange");
    break;
  default:
    console.log("❓ Fruit inconnu");
}
// Affiche : "🍎 C'est une pomme"
```

**Comment ça fonctionne :**
1. JavaScript évalue `fruit` (qui vaut "pomme")
2. Il compare avec chaque `case` en utilisant `===` (égalité stricte)
3. Quand il trouve `case "pomme":`, il exécute le code correspondant
4. Le `break` fait sortir du switch

---

## L'importance du `break`

⚠️ **Attention :** Si vous oubliez le `break`, JavaScript continue d'exécuter les cases suivants ! C'est ce qu'on appelle le **"fall-through"**.

### Exemple sans `break` (comportement inattendu)

```javascript
const note = "B";

switch (note) {
  case "A":
    console.log("Excellent !");
  case "B":
    console.log("Très bien !");
  case "C":
    console.log("Bien");
  case "D":
    console.log("Passable");
  default:
    console.log("Insuffisant");
}
```

**Résultat inattendu :**
```
Très bien !
Bien
Passable
Insuffisant
```

JavaScript exécute **tout** à partir de `case "B"` jusqu'à la fin car il n'y a pas de `break`.

### Exemple avec `break` (comportement correct)

```javascript
const note = "B";

switch (note) {
  case "A":
    console.log("Excellent !");
    break;
  case "B":
    console.log("Très bien !");
    break;
  case "C":
    console.log("Bien");
    break;
  case "D":
    console.log("Passable");
    break;
  default:
    console.log("Insuffisant");
}
// Affiche uniquement : "Très bien !"
```

---

## Le cas `default`

Le `default` est exécuté si aucun `case` ne correspond. C'est l'équivalent du `else` final dans un `if...else if`.

```javascript
const animal = "licorne";

switch (animal) {
  case "chat":
    console.log("🐱 Miaou");
    break;
  case "chien":
    console.log("🐶 Ouaf");
    break;
  case "oiseau":
    console.log("🐦 Cui-cui");
    break;
  default:
    console.log("❓ Animal inconnu");
}
// Affiche : "❓ Animal inconnu"
```

**Note :** Le `default` est optionnel, mais recommandé pour gérer les cas imprévus.

---

## Grouper plusieurs cases

Parfois, plusieurs valeurs doivent exécuter le même code. On peut les grouper en omettant volontairement le `break` :

### Exemple : jours de la semaine

```javascript
const jour = "samedi";

switch (jour) {
  case "lundi":
  case "mardi":
  case "mercredi":
  case "jeudi":
  case "vendredi":
    console.log("C'est un jour de semaine 💼");
    break;
  case "samedi":
  case "dimanche":
    console.log("C'est le week-end ! 🎉");
    break;
  default:
    console.log("Jour invalide");
}
// Affiche : "C'est le week-end ! 🎉"
```

**Explication :** Tous les jours de semaine "tombent" jusqu'au premier `break`, donc ils exécutent le même code.

### Exemple : calcul de saison

```javascript
const mois = 8; // Août

switch (mois) {
  case 12:
  case 1:
  case 2:
    console.log("❄️ Hiver");
    break;
  case 3:
  case 4:
  case 5:
    console.log("🌸 Printemps");
    break;
  case 6:
  case 7:
  case 8:
    console.log("☀️ Été");
    break;
  case 9:
  case 10:
  case 11:
    console.log("🍂 Automne");
    break;
  default:
    console.log("Mois invalide");
}
// Affiche : "☀️ Été"
```

---

## Switch avec des nombres

Le `switch` fonctionne aussi très bien avec des nombres.

```javascript
const choixMenu = 2;

switch (choixMenu) {
  case 1:
    console.log("🍕 Pizza Margherita - 12€");
    break;
  case 2:
    console.log("🍝 Pâtes Carbonara - 14€");
    break;
  case 3:
    console.log("🥗 Salade César - 10€");
    break;
  case 4:
    console.log("🍔 Burger Maison - 15€");
    break;
  default:
    console.log("❌ Choix invalide");
}
// Affiche : "🍝 Pâtes Carbonara - 14€"
```

---

## Comparaison stricte (===)

⚠️ **Important :** Le `switch` utilise la comparaison stricte `===`, pas `==`.

```javascript
const valeur = "3";

switch (valeur) {
  case 3:
    console.log("Le nombre 3");
    break;
  case "3":
    console.log("La chaîne '3'");
    break;
}
// Affiche : "La chaîne '3'"
```

**Explication :** `"3"` (string) n'est pas égal à `3` (number) avec `===`.

---

## Utilisation de variables et expressions

On peut utiliser des expressions plus complexes, mais c'est moins courant.

### Variables dans les cases

```javascript
const MAX_SCORE = 100;
const score = 100;

switch (score) {
  case 0:
    console.log("Aucun point");
    break;
  case MAX_SCORE:
    console.log("Score parfait ! 🏆");
    break;
  default:
    console.log(`Score : ${score}`);
}
// Affiche : "Score parfait ! 🏆"
```

### Attention avec les expressions

```javascript
const x = 5;

// ❌ Ceci ne fonctionne PAS comme prévu
switch (x) {
  case x > 10:
    console.log("Grand");
    break;
  case x > 0:
    console.log("Petit");
    break;
}
```

**Problème :** `x > 10` retourne `false`, et JavaScript compare `5 === false`, ce qui est faux.

**Solution :** Pour ce genre de comparaisons, utilisez `if...else if` à la place.

---

## Switch vs if...else : Quand utiliser quoi ?

### Utilisez `switch` quand :

- ✅ Vous comparez une seule variable à **plusieurs valeurs exactes**
- ✅ Vous avez **3 cas ou plus**
- ✅ Les valeurs sont **simples** (nombres, strings)

```javascript
// ✅ Bon usage de switch
switch (couleur) {
  case "rouge":
    // ...
    break;
  case "bleu":
    // ...
    break;
  case "vert":
    // ...
    break;
}
```

### Utilisez `if...else if` quand :

- ✅ Vous faites des **comparaisons complexes** (`>`, `<`, `>=`, etc.)
- ✅ Vous combinez **plusieurs conditions** (`&&`, `||`)
- ✅ Vous testez **différentes variables**

```javascript
// ✅ Bon usage de if...else
if (age >= 18 && pays === "France") {
  // ...
} else if (score > 100) {
  // ...
}
```

---

## Exemples pratiques

### Exemple 1 : Calculatrice simple

```javascript
const operation = "+";
const a = 10;
const b = 5;
let resultat;

switch (operation) {
  case "+":
    resultat = a + b;
    console.log(`${a} + ${b} = ${resultat}`);
    break;
  case "-":
    resultat = a - b;
    console.log(`${a} - ${b} = ${resultat}`);
    break;
  case "*":
    resultat = a * b;
    console.log(`${a} * ${b} = ${resultat}`);
    break;
  case "/":
    if (b !== 0) {
      resultat = a / b;
      console.log(`${a} / ${b} = ${resultat}`);
    } else {
      console.log("❌ Division par zéro impossible");
    }
    break;
  default:
    console.log("❌ Opération invalide");
}
// Affiche : "10 + 5 = 15"
```

### Exemple 2 : Système de tarification

```javascript
const typeClient = "etudiant";
const prixBase = 50;
let prixFinal;

switch (typeClient) {
  case "etudiant":
    prixFinal = prixBase * 0.5; // 50% de réduction
    console.log(`Prix étudiant : ${prixFinal}€`);
    break;
  case "senior":
    prixFinal = prixBase * 0.7; // 30% de réduction
    console.log(`Prix senior : ${prixFinal}€`);
    break;
  case "enfant":
    prixFinal = prixBase * 0.6; // 40% de réduction
    console.log(`Prix enfant : ${prixFinal}€`);
    break;
  case "adulte":
    prixFinal = prixBase;
    console.log(`Prix adulte : ${prixFinal}€`);
    break;
  default:
    console.log("❌ Type de client invalide");
    prixFinal = prixBase;
}
// Affiche : "Prix étudiant : 25€"
```

### Exemple 3 : Réponse HTTP

```javascript
const codeHTTP = 404;

switch (codeHTTP) {
  case 200:
    console.log("✅ OK - Requête réussie");
    break;
  case 201:
    console.log("✅ Created - Ressource créée");
    break;
  case 400:
    console.log("❌ Bad Request - Requête invalide");
    break;
  case 401:
    console.log("❌ Unauthorized - Non autorisé");
    break;
  case 404:
    console.log("❌ Not Found - Page non trouvée");
    break;
  case 500:
    console.log("❌ Internal Server Error - Erreur serveur");
    break;
  default:
    console.log(`Code HTTP : ${codeHTTP}`);
}
// Affiche : "❌ Not Found - Page non trouvée"
```

### Exemple 4 : Gestion de langues

```javascript
const langue = "fr";
let message;

switch (langue) {
  case "fr":
    message = "Bonjour !";
    break;
  case "en":
    message = "Hello!";
    break;
  case "es":
    message = "¡Hola!";
    break;
  case "de":
    message = "Guten Tag!";
    break;
  case "it":
    message = "Ciao!";
    break;
  default:
    message = "Hello!"; // Langue par défaut
    console.log("⚠️ Langue non supportée, utilisation de l'anglais");
}

console.log(message);
// Affiche : "Bonjour !"
```

---

## Retourner une valeur avec `switch`

On peut utiliser `switch` dans une fonction et retourner directement une valeur :

```javascript
function obtenirNomJour(numeroJour) {
  switch (numeroJour) {
    case 1:
      return "Lundi";
    case 2:
      return "Mardi";
    case 3:
      return "Mercredi";
    case 4:
      return "Jeudi";
    case 5:
      return "Vendredi";
    case 6:
      return "Samedi";
    case 7:
      return "Dimanche";
    default:
      return "Jour invalide";
  }
}

console.log(obtenirNomJour(3)); // "Mercredi"
console.log(obtenirNomJour(7)); // "Dimanche"
```

**Note :** Quand on utilise `return`, on n'a pas besoin de `break` car `return` sort automatiquement de la fonction.

---

## Switch avec des expressions régulières (avancé)

Pour les utilisateurs avancés, voici une astuce avec `true` :

```javascript
const score = 85;

switch (true) {
  case score >= 90:
    console.log("A - Excellent");
    break;
  case score >= 80:
    console.log("B - Très bien");
    break;
  case score >= 70:
    console.log("C - Bien");
    break;
  case score >= 60:
    console.log("D - Passable");
    break;
  default:
    console.log("F - Insuffisant");
}
// Affiche : "B - Très bien"
```

**Attention :** Cette technique fonctionne mais `if...else if` est plus naturel pour ce genre de cas.

---

## Bonnes pratiques

### ✅ Toujours utiliser `break` (sauf cas intentionnel)

```javascript
// ✅ Bon
switch (valeur) {
  case 1:
    console.log("Un");
    break;
  case 2:
    console.log("Deux");
    break;
}
```

### ✅ Toujours inclure un `default`

```javascript
// ✅ Bon
switch (choix) {
  case "A":
    // ...
    break;
  case "B":
    // ...
    break;
  default:
    console.log("Choix invalide");
}
```

### ✅ Indenter correctement

```javascript
// ✅ Lisible
switch (jour) {
  case "lundi":
    console.log("Début de semaine");
    break;
  case "vendredi":
    console.log("Fin de semaine");
    break;
  default:
    console.log("Autre jour");
}
```

### ✅ Commenter les fall-through intentionnels

```javascript
switch (niveau) {
  case "admin":
    console.log("Accès administration");
    // fall through - admin a aussi les droits utilisateur
  case "utilisateur":
    console.log("Accès utilisateur");
    break;
  default:
    console.log("Accès invité");
}
```

### ❌ Éviter les switch trop longs

Si votre `switch` dépasse 10 cas, envisagez d'utiliser un objet :

```javascript
// ❌ Switch trop long
switch (pays) {
  case "FR":
    return "France";
  case "ES":
    return "Espagne";
  case "IT":
    return "Italie";
  // ... 20 autres cas
}

// ✅ Objet (plus simple)
const nomsPays = {
  FR: "France",
  ES: "Espagne",
  IT: "Italie",
  // ...
};
return nomsPays[pays] || "Pays inconnu";
```

---

## Erreurs courantes

### ❌ Oublier le `break`

```javascript
// ❌ Erreur : tous les cas s'exécutent
switch (couleur) {
  case "rouge":
    console.log("Rouge");
  case "bleu":
    console.log("Bleu");
}
```

### ❌ Utiliser `==` au lieu de `===`

Le switch utilise automatiquement `===`, soyez conscient de la différence de types :

```javascript
const valeur = "5";

switch (valeur) {
  case 5:  // Ne correspondra PAS
    console.log("Nombre 5");
    break;
  case "5":  // Correspondra
    console.log("String 5");
    break;
}
```

### ❌ Oublier les accolades pour plusieurs instructions

```javascript
// ❌ Peut causer des erreurs
switch (type) {
  case "A":
    const x = 1;  // Erreur si 'const' est déjà déclaré
    console.log(x);
    break;
  case "B":
    const x = 2;  // Erreur : x déjà déclaré
    console.log(x);
    break;
}

// ✅ Solution : utiliser des accolades
switch (type) {
  case "A": {
    const x = 1;
    console.log(x);
    break;
  }
  case "B": {
    const x = 2;  // OK : nouveau scope
    console.log(x);
    break;
  }
}
```

---

## Résumé

- **`switch`** est idéal pour comparer une variable à plusieurs valeurs exactes
- Utilisez **`break`** après chaque case (sauf si vous voulez un fall-through intentionnel)
- Le **`default`** gère les cas non prévus (recommandé)
- On peut **grouper plusieurs cases** pour exécuter le même code
- Le switch utilise la **comparaison stricte** `===`
- Préférez `if...else if` pour les comparaisons complexes (`>`, `<`, `&&`, `||`)
- Utilisez un **objet** si vous avez trop de cas simples

Le `switch` est un outil puissant pour rendre votre code plus lisible et organisé quand vous devez gérer de nombreuses valeurs possibles pour une même variable ! 🎯

⏭️ [Boucle for classique](/05-javascript-moderne-fondamentaux/05-structures-controle/03-boucle-for-classique.md)
