🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.12.4 Throw et création d'erreurs personnalisées

## Introduction

Dans les sections précédentes, vous avez appris à **gérer** les erreurs avec `try...catch`. Maintenant, vous allez apprendre à **créer** et **lancer** vos propres erreurs de manière intentionnelle. C'est un outil puissant pour rendre votre code plus robuste et plus facile à déboguer.

> 💡 **Analogie** : Si `try...catch` est comme un filet de sécurité, `throw` est comme un signal d'alarme que vous déclenchez volontairement quand quelque chose ne va pas.

---

## Le mot-clé throw

### Qu'est-ce que throw ?

`throw` est un mot-clé JavaScript qui permet de **lancer une exception** (une erreur) de manière intentionnelle. Quand vous utilisez `throw`, l'exécution normale du code s'arrête immédiatement.

### Syntaxe de base

```javascript
throw expression;
```

### Premier exemple simple

```javascript
function verifierAge(age) {
    if (age < 0) {
        throw new Error("L'âge ne peut pas être négatif !");
    }
    console.log("Âge valide :", age);
}

verifierAge(25);   // ✅ Âge valide : 25
verifierAge(-5);   // ❌ Error: L'âge ne peut pas être négatif !
```

---

## Que peut-on lancer avec throw ?

Techniquement, vous pouvez lancer n'importe quelle valeur avec `throw`, mais ce n'est pas toujours recommandé.

### 1. Lancer une string (❌ déconseillé)

```javascript
throw "Une erreur s'est produite";
```

**Problème :** Pas de stack trace, difficile à déboguer.

### 2. Lancer un nombre (❌ déconseillé)

```javascript
throw 404;
```

**Problème :** Pas de contexte, peu informatif.

### 3. Lancer un objet simple (❌ déconseillé)

```javascript
throw { message: "Erreur", code: 500 };
```

**Problème :** Pas de stack trace automatique.

### 4. Lancer un objet Error (✅ recommandé)

```javascript
throw new Error("Description claire du problème");
```

**Avantages :**
- Stack trace automatique
- Propriétés `name` et `message`
- Compatibilité avec tous les outils de débogage
- Standard JavaScript

---

## Pourquoi toujours utiliser new Error() ?

Comparons les deux approches :

```javascript
// ❌ Lancer une string
try {
    throw "Fichier non trouvé";
} catch (erreur) {
    console.log(typeof erreur);      // "string"
    console.log(erreur.stack);       // undefined
    console.log(erreur.message);     // undefined
}

// ✅ Lancer un objet Error
try {
    throw new Error("Fichier non trouvé");
} catch (erreur) {
    console.log(typeof erreur);      // "object"
    console.log(erreur.stack);       // Stack trace complète ✅
    console.log(erreur.message);     // "Fichier non trouvé" ✅
    console.log(erreur.name);        // "Error" ✅
}
```

---

## Quand utiliser throw ?

### ✅ Situations appropriées

**1. Validation de paramètres**

```javascript
function calculerSurface(largeur, hauteur) {
    if (typeof largeur !== 'number' || typeof hauteur !== 'number') {
        throw new TypeError("Les dimensions doivent être des nombres");
    }

    if (largeur <= 0 || hauteur <= 0) {
        throw new RangeError("Les dimensions doivent être positives");
    }

    return largeur * hauteur;
}

try {
    console.log(calculerSurface(5, 10));    // ✅ 50
    console.log(calculerSurface(-5, 10));   // ❌ RangeError
} catch (erreur) {
    console.error(erreur.message);
}
```

**2. États invalides**

```javascript
function retirerArgent(montant, solde) {
    if (montant > solde) {
        throw new Error("Solde insuffisant");
    }
    return solde - montant;
}

try {
    const nouveauSolde = retirerArgent(100, 50);
} catch (erreur) {
    console.log("Transaction refusée :", erreur.message);
}
```

**3. Opérations impossibles**

```javascript
function diviser(a, b) {
    if (b === 0) {
        throw new Error("Division par zéro impossible");
    }
    return a / b;
}
```

**4. Données manquantes ou invalides**

```javascript
function creerUtilisateur(donnees) {
    if (!donnees.nom) {
        throw new Error("Le nom est obligatoire");
    }

    if (!donnees.email || !donnees.email.includes('@')) {
        throw new Error("Email invalide");
    }

    return {
        nom: donnees.nom,
        email: donnees.email,
        creeLe: new Date()
    };
}
```

---

## Choisir le bon type d'erreur

JavaScript fournit différents types d'erreurs pour différentes situations.

### Error - Erreur générique

Utilisez `Error` pour les erreurs générales.

```javascript
function chargerConfiguration() {
    const config = lireConfigDepuisFichier();
    if (!config) {
        throw new Error("Impossible de charger la configuration");
    }
    return config;
}
```

### TypeError - Erreur de type

Utilisez `TypeError` quand le type de données est incorrect.

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
    console.log(erreur.name);  // "TypeError"
}
```

### RangeError - Valeur hors limites

Utilisez `RangeError` quand une valeur est en dehors de la plage autorisée.

```javascript
function definirAge(age) {
    if (age < 0 || age > 150) {
        throw new RangeError("L'âge doit être entre 0 et 150");
    }
    return age;
}
```

### ReferenceError - Référence inexistante

Rarement utilisé manuellement (JavaScript le lance automatiquement).

```javascript
function accederVariable(nom) {
    if (!window.hasOwnProperty(nom)) {
        throw new ReferenceError(`La variable ${nom} n'existe pas`);
    }
}
```

---

## Créer des classes d'erreurs personnalisées

Pour des applications plus complexes, vous pouvez créer vos propres types d'erreurs.

### Syntaxe de base (ES6)

```javascript
class MonErreurPersonnalisee extends Error {
    constructor(message) {
        super(message);
        this.name = "MonErreurPersonnalisee";
    }
}
```

### Exemple pratique : Erreur de validation

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}

function validerEmail(email) {
    if (!email) {
        throw new ValidationError("L'email est requis");
    }

    if (!email.includes('@')) {
        throw new ValidationError("L'email doit contenir un @");
    }

    return true;
}

try {
    validerEmail("invalide");
} catch (erreur) {
    if (erreur instanceof ValidationError) {
        console.log("Erreur de validation :", erreur.message);
    }
}
```

### Exemple avancé : Erreur avec code et détails

```javascript
class DatabaseError extends Error {
    constructor(message, code, query) {
        super(message);
        this.name = "DatabaseError";
        this.code = code;
        this.query = query;
        this.timestamp = new Date();
    }
}

function executerRequete(sql) {
    // Simulation d'une erreur de base de données
    throw new DatabaseError(
        "Erreur de syntaxe SQL",
        1064,
        sql
    );
}

try {
    executerRequete("SELECT * FORM users");  // Faute de frappe volontaire
} catch (erreur) {
    if (erreur instanceof DatabaseError) {
        console.log(`Erreur DB [${erreur.code}]: ${erreur.message}`);
        console.log(`Requête: ${erreur.query}`);
        console.log(`Timestamp: ${erreur.timestamp}`);
    }
}
```

### Hiérarchie d'erreurs personnalisées

Vous pouvez créer une hiérarchie d'erreurs pour différents contextes.

```javascript
// Erreur de base pour l'application
class AppError extends Error {
    constructor(message) {
        super(message);
        this.name = "AppError";
    }
}

// Erreurs spécifiques qui héritent d'AppError
class AuthenticationError extends AppError {
    constructor(message) {
        super(message);
        this.name = "AuthenticationError";
    }
}

class PermissionError extends AppError {
    constructor(message, requiredRole) {
        super(message);
        this.name = "PermissionError";
        this.requiredRole = requiredRole;
    }
}

class NotFoundError extends AppError {
    constructor(resource) {
        super(`${resource} non trouvé`);
        this.name = "NotFoundError";
        this.resource = resource;
    }
}

// Utilisation
function accederRessource(utilisateur, ressource) {
    if (!utilisateur) {
        throw new AuthenticationError("Utilisateur non connecté");
    }

    if (utilisateur.role !== 'admin') {
        throw new PermissionError("Accès refusé", "admin");
    }

    if (!ressource.existe) {
        throw new NotFoundError("Ressource");
    }
}

try {
    accederRessource(null, { existe: true });
} catch (erreur) {
    if (erreur instanceof AuthenticationError) {
        console.log("Redirection vers la page de connexion");
    } else if (erreur instanceof PermissionError) {
        console.log(`Rôle requis: ${erreur.requiredRole}`);
    } else if (erreur instanceof NotFoundError) {
        console.log(`${erreur.resource} introuvable`);
    } else if (erreur instanceof AppError) {
        console.log("Erreur applicative:", erreur.message);
    }
}
```

---

## Relancer une erreur (re-throw)

Parfois, vous voulez capturer une erreur, faire quelque chose, puis la relancer.

### Syntaxe

```javascript
try {
    // Code risqué
} catch (erreur) {
    // Faire quelque chose (logger, nettoyer, etc.)
    console.log("Erreur capturée :", erreur.message);

    // Relancer l'erreur
    throw erreur;
}
```

### Exemple pratique

```javascript
function traiterDonnees(donnees) {
    try {
        return JSON.parse(donnees);
    } catch (erreur) {
        // Logger l'erreur pour le monitoring
        console.error("Erreur de parsing à", new Date());
        console.error("Données reçues:", donnees);

        // Relancer pour que l'appelant puisse aussi la gérer
        throw erreur;
    }
}

try {
    const resultat = traiterDonnees('{ invalide }');
} catch (erreur) {
    console.log("L'application a capturé l'erreur");
}
```

### Transformer et relancer

Vous pouvez aussi transformer l'erreur avant de la relancer :

```javascript
function chargerUtilisateur(id) {
    try {
        return appelAPI(`/users/${id}`);
    } catch (erreur) {
        // Transformer l'erreur technique en erreur métier
        throw new Error(`Impossible de charger l'utilisateur ${id}: ${erreur.message}`);
    }
}
```

---

## Patterns courants de gestion d'erreurs

### Pattern 1 : Validation en chaîne

```javascript
class FormValidator {
    constructor() {
        this.errors = [];
    }

    validateRequired(value, fieldName) {
        if (!value || value.trim() === '') {
            throw new ValidationError(`${fieldName} est requis`);
        }
        return this;
    }

    validateEmail(email) {
        if (!email.includes('@')) {
            throw new ValidationError("Email invalide");
        }
        return this;
    }

    validateLength(value, min, max, fieldName) {
        if (value.length < min || value.length > max) {
            throw new ValidationError(
                `${fieldName} doit contenir entre ${min} et ${max} caractères`
            );
        }
        return this;
    }
}

const validator = new FormValidator();

try {
    validator
        .validateRequired("Alice", "Nom")
        .validateEmail("alice@example.com")
        .validateLength("motdepasse123", 8, 20, "Mot de passe");

    console.log("Formulaire valide !");
} catch (erreur) {
    console.error("Validation échouée :", erreur.message);
}
```

### Pattern 2 : Early return avec throw

```javascript
function traiterCommande(commande) {
    if (!commande) {
        throw new Error("Commande manquante");
    }

    if (!commande.produits || commande.produits.length === 0) {
        throw new Error("Aucun produit dans la commande");
    }

    if (!commande.client) {
        throw new Error("Client non spécifié");
    }

    if (commande.total <= 0) {
        throw new RangeError("Le montant doit être positif");
    }

    // Si on arrive ici, tout est OK
    return traiterPaiement(commande);
}
```

### Pattern 3 : Factory avec gestion d'erreurs

```javascript
class UserFactory {
    static create(data) {
        if (!data.email) {
            throw new ValidationError("Email requis");
        }

        if (!data.password || data.password.length < 8) {
            throw new ValidationError("Mot de passe trop court");
        }

        return {
            id: generateId(),
            email: data.email,
            passwordHash: hash(data.password),
            createdAt: new Date()
        };
    }
}

try {
    const user = UserFactory.create({
        email: "user@example.com",
        password: "court"
    });
} catch (erreur) {
    if (erreur instanceof ValidationError) {
        console.log("Données invalides :", erreur.message);
    }
}
```

---

## Bonnes pratiques

### ✅ À faire

**1. Messages d'erreur descriptifs**

```javascript
// ✅ Bon - message clair avec contexte
throw new Error(`Impossible de charger l'utilisateur ${userId}: serveur indisponible`);

// ❌ Mauvais - message vague
throw new Error("Erreur");
```

**2. Utiliser le type d'erreur approprié**

```javascript
// ✅ Bon
if (typeof age !== 'number') {
    throw new TypeError("L'âge doit être un nombre");
}

// ❌ Moins bon
if (typeof age !== 'number') {
    throw new Error("L'âge doit être un nombre");
}
```

**3. Valider tôt (fail fast)**

```javascript
// ✅ Bon - validation au début
function processer(data) {
    if (!data) {
        throw new Error("Données manquantes");
    }

    // Traitement...
}

// ❌ Mauvais - validation tardive
function processer(data) {
    // 50 lignes de traitement...
    if (!data) {
        throw new Error("Données manquantes");
    }
}
```

**4. Documenter les erreurs possibles**

```javascript
/**
 * Calcule la surface d'un rectangle
 * @param {number} largeur - La largeur du rectangle
 * @param {number} hauteur - La hauteur du rectangle
 * @returns {number} La surface
 * @throws {TypeError} Si les paramètres ne sont pas des nombres
 * @throws {RangeError} Si les dimensions sont négatives ou nulles
 */
function calculerSurface(largeur, hauteur) {
    if (typeof largeur !== 'number' || typeof hauteur !== 'number') {
        throw new TypeError("Les dimensions doivent être des nombres");
    }

    if (largeur <= 0 || hauteur <= 0) {
        throw new RangeError("Les dimensions doivent être positives");
    }

    return largeur * hauteur;
}
```

### ❌ À éviter

**1. Lancer des erreurs pour le contrôle de flux normal**

```javascript
// ❌ Mauvais - utilise throw pour la logique normale
function trouverUtilisateur(id) {
    const user = users.find(u => u.id === id);
    if (!user) {
        throw new Error("Utilisateur non trouvé");
    }
    return user;
}

// ✅ Mieux - retourner null ou undefined
function trouverUtilisateur(id) {
    return users.find(u => u.id === id) || null;
}
```

**2. Lancer des erreurs sans contexte**

```javascript
// ❌ Mauvais
throw new Error("Erreur");

// ✅ Bon
throw new Error(`Échec de la validation du champ "${fieldName}": ${reason}`);
```

**3. Ignorer les erreurs capturées**

```javascript
// ❌ Très mauvais
try {
    operationRisquee();
} catch (erreur) {
    // Ne rien faire - l'erreur est perdue
}

// ✅ Bon - au minimum logger
try {
    operationRisquee();
} catch (erreur) {
    console.error("Erreur capturée:", erreur);
    // Potentiellement relancer ou gérer
}
```

---

## Exemple complet : Système de validation

Voici un exemple complet qui combine tous les concepts :

```javascript
// Définition des erreurs personnalisées
class ValidationError extends Error {
    constructor(field, message) {
        super(message);
        this.name = "ValidationError";
        this.field = field;
    }
}

class DatabaseError extends Error {
    constructor(message, operation) {
        super(message);
        this.name = "DatabaseError";
        this.operation = operation;
    }
}

// Classe de validation
class UserValidator {
    static validateEmail(email) {
        if (!email) {
            throw new ValidationError("email", "L'email est requis");
        }

        if (typeof email !== 'string') {
            throw new ValidationError("email", "L'email doit être une chaîne");
        }

        if (!email.includes('@')) {
            throw new ValidationError("email", "Format d'email invalide");
        }

        return true;
    }

    static validatePassword(password) {
        if (!password) {
            throw new ValidationError("password", "Le mot de passe est requis");
        }

        if (password.length < 8) {
            throw new ValidationError(
                "password",
                "Le mot de passe doit contenir au moins 8 caractères"
            );
        }

        return true;
    }

    static validateAge(age) {
        if (typeof age !== 'number') {
            throw new ValidationError("age", "L'âge doit être un nombre");
        }

        if (age < 0 || age > 150) {
            throw new ValidationError("age", "L'âge doit être entre 0 et 150");
        }

        return true;
    }
}

// Fonction d'inscription
function inscrireUtilisateur(userData) {
    try {
        // Validation
        UserValidator.validateEmail(userData.email);
        UserValidator.validatePassword(userData.password);
        UserValidator.validateAge(userData.age);

        // Simulation de sauvegarde
        const emailExiste = verifierEmailExiste(userData.email);
        if (emailExiste) {
            throw new DatabaseError(
                "Cet email est déjà utilisé",
                "create_user"
            );
        }

        // Création réussie
        return {
            success: true,
            message: "Utilisateur créé avec succès"
        };

    } catch (erreur) {
        if (erreur instanceof ValidationError) {
            return {
                success: false,
                field: erreur.field,
                message: erreur.message
            };
        } else if (erreur instanceof DatabaseError) {
            return {
                success: false,
                message: erreur.message,
                operation: erreur.operation
            };
        } else {
            // Erreur inattendue
            console.error("Erreur inattendue:", erreur);
            return {
                success: false,
                message: "Une erreur inattendue s'est produite"
            };
        }
    }
}

// Fonction helper
function verifierEmailExiste(email) {
    // Simulation
    return email === "existe@example.com";
}

// Utilisation
console.log(inscrireUtilisateur({
    email: "nouveau@example.com",
    password: "motdepasse123",
    age: 25
}));
// { success: true, message: "Utilisateur créé avec succès" }

console.log(inscrireUtilisateur({
    email: "invalide",
    password: "motdepasse123",
    age: 25
}));
// { success: false, field: "email", message: "Format d'email invalide" }

console.log(inscrireUtilisateur({
    email: "existe@example.com",
    password: "motdepasse123",
    age: 25
}));
// { success: false, message: "Cet email est déjà utilisé", operation: "create_user" }
```

---

## Points clés à retenir

1. **throw permet de lancer des erreurs intentionnellement** pour signaler un problème

2. **Utilisez toujours new Error()** (ou ses variantes) pour avoir une stack trace

3. **Choisissez le bon type d'erreur** : Error, TypeError, RangeError selon le contexte

4. **Créez des erreurs personnalisées** pour des besoins spécifiques de votre application

5. **Les messages doivent être descriptifs** et inclure du contexte

6. **Validez tôt** (fail fast) pour détecter les problèmes au plus vite

7. **Documentez les erreurs** que vos fonctions peuvent lancer

8. **throw n'est pas pour le contrôle de flux normal** - réservez-le aux situations exceptionnelles

---

## Prochaines étapes

Dans la prochaine section, vous apprendrez :
- Les techniques de debugging avancées
- Comment utiliser console.log, console.error et les autres méthodes de la console
- L'utilisation des breakpoints dans les DevTools

> 💡 **Conseil final** : Une bonne gestion des erreurs rend votre application plus robuste et plus facile à maintenir. Prenez le temps de bien nommer vos erreurs et de fournir des messages clairs !

⏭️ [Debugging : console.log, console.table, console.error](/05-javascript-moderne-fondamentaux/12-gestion-erreurs/05-debugging-console.md)
