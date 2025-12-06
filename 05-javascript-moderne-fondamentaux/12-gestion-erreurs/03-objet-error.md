🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.12.3 L'objet Error

## Introduction

L'objet `Error` est l'objet JavaScript qui représente une erreur. Quand une erreur se produit, JavaScript crée automatiquement un objet Error. Mais vous pouvez aussi créer vos propres objets Error pour signaler des problèmes dans votre code.

> 💡 **Analogie** : Un objet Error est comme un rapport d'incident. Il contient toutes les informations importantes : ce qui s'est passé (le message), où ça s'est passé (la pile d'appels), et quel type d'incident c'est (le nom).

---

## Qu'est-ce que l'objet Error ?

L'objet `Error` est un objet JavaScript qui contient des informations sur une erreur qui s'est produite (ou pourrait se produire).

```javascript
// JavaScript crée automatiquement un objet Error quand une erreur survient
try {
    const x = y;  // ReferenceError
} catch (erreur) {
    console.log(erreur);  // Ceci est un objet Error
}
```

---

## Les propriétés de l'objet Error

### 1. name (nom)

Indique le type d'erreur.

```javascript
try {
    const utilisateur = null;
    console.log(utilisateur.nom);
} catch (erreur) {
    console.log(erreur.name);  // "TypeError"
}
```

**Types de name courants :**
- `"Error"` - Erreur générique
- `"TypeError"` - Erreur de type
- `"ReferenceError"` - Référence invalide
- `"SyntaxError"` - Erreur de syntaxe
- `"RangeError"` - Valeur hors limites

### 2. message (message)

Contient une description lisible de l'erreur.

```javascript
try {
    JSON.parse("texte invalide {");
} catch (erreur) {
    console.log(erreur.message);
    // "Unexpected token t in JSON at position 0"
}
```

### 3. stack (pile d'appels)

Affiche la trace complète de l'erreur : où elle s'est produite et comment on y est arrivé.

```javascript
function fonctionA() {
    fonctionB();
}

function fonctionB() {
    fonctionC();
}

function fonctionC() {
    throw new Error("Problème ici !");
}

try {
    fonctionA();
} catch (erreur) {
    console.log(erreur.stack);
}
```

**Résultat de stack :**
```
Error: Problème ici !
    at fonctionC (script.js:10)
    at fonctionB (script.js:6)
    at fonctionA (script.js:2)
    at <anonymous>:1:1
```

> 💡 **Important** : La stack trace se lit de bas en haut - elle montre le chemin suivi jusqu'à l'erreur.

---

## Créer ses propres objets Error

Vous pouvez créer manuellement des objets Error avec le constructeur `Error`.

### Syntaxe de base

```javascript
new Error(message)
```

### Exemples

```javascript
// Créer une erreur simple
const erreur1 = new Error("Quelque chose s'est mal passé");
console.log(erreur1.message);  // "Quelque chose s'est mal passé"
console.log(erreur1.name);     // "Error"

// Créer et lancer une erreur
const erreur2 = new Error("Fichier non trouvé");
throw erreur2;  // Lance l'erreur
```

### Note : `new` est optionnel

```javascript
// Ces deux lignes sont équivalentes
const erreur1 = new Error("Message");
const erreur2 = Error("Message");
```

---

## Les différents constructeurs d'erreurs natifs

JavaScript fournit plusieurs types d'erreurs prédéfinis.

### 1. Error (erreur générique)

Le type de base, utilisé quand aucun autre type ne convient.

```javascript
throw new Error("Erreur générique");
```

### 2. TypeError

Pour les erreurs de type de données.

```javascript
function multiplier(a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new TypeError("Les deux paramètres doivent être des nombres");
    }
    return a * b;
}

try {
    multiplier(5, "dix");
} catch (erreur) {
    console.log(erreur.name);     // "TypeError"
    console.log(erreur.message);  // "Les deux paramètres doivent être des nombres"
}
```

### 3. ReferenceError

Pour les erreurs de référence (variable inexistante).

```javascript
function verifierVariable(nomVariable) {
    if (typeof window[nomVariable] === 'undefined') {
        throw new ReferenceError(`La variable ${nomVariable} n'existe pas`);
    }
}
```

### 4. RangeError

Pour les valeurs hors limites.

```javascript
function creerTableau(taille) {
    if (taille < 0) {
        throw new RangeError("La taille ne peut pas être négative");
    }
    return new Array(taille);
}

try {
    creerTableau(-5);
} catch (erreur) {
    console.log(erreur.name);  // "RangeError"
}
```

### 5. SyntaxError

Généralement lancée automatiquement par JavaScript, mais vous pouvez aussi la créer.

```javascript
function analyserCommande(commande) {
    if (!commande.includes('=')) {
        throw new SyntaxError("Commande mal formée : symbole '=' manquant");
    }
}
```

### 6. URIError

Pour les erreurs liées aux URI.

```javascript
try {
    decodeURIComponent('%');
} catch (erreur) {
    console.log(erreur.name);  // "URIError"
}
```

---

## Utiliser throw pour lancer des erreurs

Le mot-clé `throw` permet de lancer une erreur manuellement.

### Syntaxe

```javascript
throw expression;
```

### Lancer un objet Error

```javascript
if (age < 0) {
    throw new Error("L'âge ne peut pas être négatif");
}
```

### Vous pouvez lancer n'importe quelle valeur

Bien que ce ne soit pas recommandé, vous pouvez techniquement lancer n'importe quoi :

```javascript
// ❌ Pas recommandé
throw "Erreur !";              // Lance une string
throw 42;                      // Lance un nombre
throw { erreur: "problème" };  // Lance un objet

// ✅ Recommandé : toujours lancer un objet Error
throw new Error("Description claire du problème");
```

### Pourquoi toujours utiliser Error ?

```javascript
try {
    throw "Juste une string";
} catch (erreur) {
    console.log(erreur.stack);  // undefined - pas de stack trace !
}

try {
    throw new Error("Avec Error");
} catch (erreur) {
    console.log(erreur.stack);  // ✅ Stack trace complète disponible
}
```

---

## Exemples pratiques

### Exemple 1 : Validation de formulaire

```javascript
function validerEmail(email) {
    if (!email) {
        throw new Error("L'email est obligatoire");
    }

    if (!email.includes('@')) {
        throw new TypeError("L'email doit contenir un @");
    }

    if (email.length < 5) {
        throw new RangeError("L'email est trop court");
    }

    return true;
}

try {
    validerEmail("abc");
} catch (erreur) {
    console.log(`${erreur.name}: ${erreur.message}`);
    // "TypeError: L'email doit contenir un @"
}
```

### Exemple 2 : Gestion de fichier

```javascript
function lireFichier(nomFichier) {
    if (!nomFichier) {
        throw new Error("Le nom du fichier est requis");
    }

    if (typeof nomFichier !== 'string') {
        throw new TypeError("Le nom du fichier doit être une chaîne de caractères");
    }

    if (!nomFichier.endsWith('.txt')) {
        throw new Error("Seuls les fichiers .txt sont supportés");
    }

    // Simulation de lecture
    return "Contenu du fichier";
}

try {
    const contenu = lireFichier("document.pdf");
} catch (erreur) {
    console.error(`Erreur: ${erreur.message}`);
    // "Erreur: Seuls les fichiers .txt sont supportés"
}
```

### Exemple 3 : Calculs mathématiques

```javascript
function diviser(a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new TypeError("Les deux paramètres doivent être des nombres");
    }

    if (b === 0) {
        throw new Error("Division par zéro impossible");
    }

    return a / b;
}

function calculer(operation) {
    try {
        const resultat = diviser(operation.a, operation.b);
        console.log(`Résultat: ${resultat}`);
    } catch (erreur) {
        if (erreur instanceof TypeError) {
            console.error("Erreur de type:", erreur.message);
        } else {
            console.error("Erreur:", erreur.message);
        }
    }
}

calculer({ a: 10, b: 2 });    // ✅ Résultat: 5
calculer({ a: 10, b: 0 });    // ❌ Erreur: Division par zéro impossible
calculer({ a: 10, b: "2" });  // ❌ Erreur de type: Les deux paramètres...
```

---

## Vérifier le type d'erreur avec instanceof

L'opérateur `instanceof` permet de vérifier le type exact d'une erreur.

```javascript
try {
    throw new TypeError("Erreur de type");
} catch (erreur) {
    if (erreur instanceof TypeError) {
        console.log("C'est une TypeError");
    } else if (erreur instanceof ReferenceError) {
        console.log("C'est une ReferenceError");
    } else if (erreur instanceof Error) {
        console.log("C'est une Error générique");
    }
}
```

### Hiérarchie des erreurs

Toutes les erreurs héritent de `Error` :

```javascript
const erreur = new TypeError("Test");

console.log(erreur instanceof TypeError);      // true
console.log(erreur instanceof Error);          // true (TypeError hérite de Error)
console.log(erreur instanceof ReferenceError); // false
```

---

## Créer des classes d'erreurs personnalisées

Pour des applications plus complexes, vous pouvez créer vos propres types d'erreurs.

### Syntaxe moderne (ES6)

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}

class DatabaseError extends Error {
    constructor(message, code) {
        super(message);
        this.name = "DatabaseError";
        this.code = code;
    }
}
```

### Utilisation

```javascript
function validerUtilisateur(utilisateur) {
    if (!utilisateur.nom) {
        throw new ValidationError("Le nom est requis");
    }

    if (!utilisateur.email) {
        throw new ValidationError("L'email est requis");
    }
}

try {
    validerUtilisateur({ nom: "Alice" });
} catch (erreur) {
    if (erreur instanceof ValidationError) {
        console.log("Erreur de validation:", erreur.message);
    } else {
        console.log("Autre erreur:", erreur.message);
    }
}
```

### Exemple plus complet

```javascript
class HTTPError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.name = "HTTPError";
        this.statusCode = statusCode;
    }
}

function requeteAPI(url) {
    // Simulation d'une réponse API
    const statusCode = 404;

    if (statusCode >= 400) {
        throw new HTTPError("Ressource non trouvée", statusCode);
    }
}

try {
    requeteAPI("https://api.example.com/users");
} catch (erreur) {
    if (erreur instanceof HTTPError) {
        console.log(`Erreur HTTP ${erreur.statusCode}: ${erreur.message}`);
        // "Erreur HTTP 404: Ressource non trouvée"
    }
}
```

---

## Bonnes pratiques avec les objets Error

### ✅ À faire

**1. Utilisez toujours new Error() avec throw**
```javascript
// ✅ Bon
throw new Error("Description claire");

// ❌ Éviter
throw "Une erreur";
```

**2. Fournissez des messages descriptifs**
```javascript
// ✅ Bon - message clair
throw new Error("Impossible de charger l'utilisateur ID: 42 - Serveur indisponible");

// ❌ Mauvais - message vague
throw new Error("Erreur");
```

**3. Choisissez le bon type d'erreur**
```javascript
// ✅ Bon - type approprié
if (typeof age !== 'number') {
    throw new TypeError("L'âge doit être un nombre");
}

// ❌ Moins bon - Error générique
if (typeof age !== 'number') {
    throw new Error("L'âge doit être un nombre");
}
```

**4. Incluez du contexte utile**
```javascript
// ✅ Bon - contexte inclus
function diviser(a, b) {
    if (b === 0) {
        throw new Error(`Division impossible: ${a} / ${b}`);
    }
    return a / b;
}
```

### ❌ À éviter

**1. Messages d'erreur vagues**
```javascript
// ❌ Mauvais
throw new Error("Erreur");
throw new Error("Problème");
throw new Error("Échec");
```

**2. Lancer des valeurs primitives**
```javascript
// ❌ Mauvais
throw "erreur";
throw 404;
throw true;
```

**3. Créer des erreurs sans les lancer**
```javascript
// ❌ Inutile - crée l'erreur mais ne la lance pas
if (erreurCondition) {
    new Error("Une erreur");  // Rien ne se passe !
}

// ✅ Correct
if (erreurCondition) {
    throw new Error("Une erreur");
}
```

---

## Inspecter les objets Error dans la console

### Afficher les propriétés

```javascript
try {
    throw new Error("Erreur de test");
} catch (erreur) {
    console.log("Name:", erreur.name);
    console.log("Message:", erreur.message);
    console.log("Stack:", erreur.stack);

    // Ou afficher tout l'objet
    console.log(erreur);
}
```

### Utiliser console.error

```javascript
try {
    throw new Error("Problème grave");
} catch (erreur) {
    console.error(erreur);  // Affiche en rouge dans la console
}
```

### Extraire des informations de la stack

```javascript
try {
    throw new Error("Test");
} catch (erreur) {
    const lignes = erreur.stack.split('\n');
    console.log("Première ligne:", lignes[0]);  // Nom et message
    console.log("Lieu de l'erreur:", lignes[1]); // Première fonction dans la stack
}
```

---

## Tableau récapitulatif des types d'erreurs

| Type | Utilisation | Exemple |
|------|-------------|---------|
| **Error** | Erreur générique | `new Error("Problème général")` |
| **TypeError** | Mauvais type de données | `new TypeError("Doit être un nombre")` |
| **ReferenceError** | Variable inexistante | `new ReferenceError("x n'existe pas")` |
| **RangeError** | Valeur hors limites | `new RangeError("Taille négative")` |
| **SyntaxError** | Syntaxe invalide | `new SyntaxError("Format invalide")` |
| **URIError** | Problème d'URI | Rarement utilisé manuellement |

---

## Points clés à retenir

1. **L'objet Error contient 3 propriétés principales** : name, message, et stack

2. **Utilisez toujours new Error()** quand vous lancez une erreur avec throw

3. **Choisissez le bon type d'erreur** (TypeError, RangeError, etc.) selon la situation

4. **Les messages doivent être clairs et descriptifs** pour faciliter le débogage

5. **instanceof permet de vérifier le type** d'une erreur dans un bloc catch

6. **Vous pouvez créer vos propres classes d'erreurs** en héritant de Error

7. **La stack trace est précieuse** pour trouver l'origine de l'erreur

---

## Prochaines étapes

Dans la prochaine section, vous apprendrez :
- Comment créer et lancer vos propres erreurs personnalisées
- Comment structurer la gestion d'erreurs dans une application
- Les patterns avancés de gestion d'erreurs

> 💡 **Conseil** : Prenez l'habitude de toujours regarder la stack trace dans la console quand une erreur survient. C'est votre meilleur allié pour comprendre ce qui s'est passé !

⏭️ [Throw et création d'erreurs personnalisées](/05-javascript-moderne-fondamentaux/12-gestion-erreurs/04-throw-erreurs-personnalisees.md)
