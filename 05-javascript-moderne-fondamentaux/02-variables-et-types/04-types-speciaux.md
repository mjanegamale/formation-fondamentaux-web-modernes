🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.2.4 - Types spéciaux : undefined, null, Symbol

## Introduction

Dans la section précédente, nous avons découvert les trois types primitifs fondamentaux : `string`, `number` et `boolean`. JavaScript possède également **trois types spéciaux** qui représentent des concepts particuliers :

- ❓ **undefined** : "Je n'ai pas encore de valeur"
- ⭕ **null** : "Je n'ai volontairement pas de valeur"
- 🔐 **Symbol** : "Je suis un identifiant unique" (ES6+)

Ces types peuvent sembler abstraits au début, mais ils sont essentiels pour écrire du code JavaScript robuste et professionnel.

> 💡 **Note** : `undefined` et `null` sont très importants et vous les rencontrerez constamment. `Symbol` est plus avancé et moins utilisé au quotidien, mais bon à connaître.

## 1. undefined ❓

### Qu'est-ce que undefined ?

`undefined` signifie littéralement "**non défini**". C'est la valeur automatique donnée à une variable qui a été **déclarée mais pas encore initialisée**.

### Analogie

Imaginez une boîte étiquetée mais vide. Vous avez créé la boîte (déclaré la variable), mais vous n'avez encore rien mis dedans. Son contenu est donc "non défini".

### Quand obtient-on undefined ?

#### 1. Variable déclarée sans valeur

```javascript
let nom;
console.log(nom);  // undefined

let age;
console.log(age);  // undefined

let ville;
console.log(typeof ville);  // "undefined"
```

> ⚡ **Important** : Avec `const`, vous **devez** initialiser la variable, donc vous n'aurez jamais `undefined` de cette façon.

```javascript
const prenom;  // ❌ SyntaxError: Missing initializer in const declaration
```

#### 2. Propriété d'objet inexistante

```javascript
const personne = {
    nom: "Alice",
    age: 25
};

console.log(personne.nom);    // "Alice"
console.log(personne.ville);  // undefined (cette propriété n'existe pas)
```

#### 3. Fonction sans return

```javascript
function direBonjour() {
    console.log("Bonjour !");
    // Pas de return
}

const resultat = direBonjour();
console.log(resultat);  // undefined
```

#### 4. Paramètre de fonction non fourni

```javascript
function saluer(prenom) {
    console.log(`Bonjour ${prenom}`);
}

saluer();  // Bonjour undefined
// prenom n'a pas été fourni, donc il vaut undefined
```

#### 5. Élément de tableau inexistant

```javascript
const fruits = ["Pomme", "Banane"];
console.log(fruits[0]);  // "Pomme"
console.log(fruits[5]);  // undefined (cet index n'existe pas)
```

### Vérifier si une valeur est undefined

```javascript
let variable;

// Méthode 1 : Comparaison stricte (recommandée)
if (variable === undefined) {
    console.log("Variable non définie");
}

// Méthode 2 : Avec typeof (utile si la variable peut ne pas exister)
if (typeof variable === "undefined") {
    console.log("Variable non définie");
}

// ❌ Ne faites pas ça
if (variable == undefined) {  // Éviter == (non strict)
    // Ceci sera vrai aussi pour null !
}
```

### undefined est falsy

Dans un contexte booléen, `undefined` est considéré comme `false` :

```javascript
let nom;

if (nom) {
    console.log("nom a une valeur");
} else {
    console.log("nom est undefined");  // Ceci s'affiche
}
```

### Exemples pratiques avec undefined

```javascript
// Vérification avant utilisation
function afficherAge(personne) {
    if (personne.age === undefined) {
        console.log("Âge non renseigné");
    } else {
        console.log(`Âge : ${personne.age} ans`);
    }
}

const alice = { nom: "Alice", age: 25 };
const bob = { nom: "Bob" };  // Pas d'âge

afficherAge(alice);  // "Âge : 25 ans"
afficherAge(bob);    // "Âge non renseigné"

// Paramètre optionnel avec valeur par défaut
function saluer(nom = "Visiteur") {
    // Si nom est undefined, utilise "Visiteur"
    console.log(`Bonjour ${nom} !`);
}

saluer("Alice");   // "Bonjour Alice !"
saluer();          // "Bonjour Visiteur !"
```

## 2. null ⭕

### Qu'est-ce que null ?

`null` représente une **absence intentionnelle de valeur**. C'est le développeur qui assigne explicitement `null` pour dire "cette variable n'a volontairement aucune valeur".

### Analogie

Imaginez une boîte étiquetée avec un panneau "VIDE" à l'intérieur. La boîte existe, mais vous avez **volontairement** mis un marqueur indiquant qu'elle est vide.

### Différence avec undefined

| undefined | null |
|-----------|------|
| "Pas encore de valeur" | "Volontairement aucune valeur" |
| Automatique (JavaScript) | Intentionnel (développeur) |
| Variable déclarée non initialisée | Variable explicitement vidée |

```javascript
// undefined : JavaScript ne sait pas
let nom;
console.log(nom);  // undefined

// null : le développeur dit "pas de valeur"
let prenom = null;
console.log(prenom);  // null
```

### Quand utiliser null ?

#### 1. Initialiser une variable qui sera remplie plus tard

```javascript
// On sait qu'on aura un utilisateur plus tard
let utilisateurConnecte = null;

// Plus tard, après connexion...
utilisateurConnecte = {
    nom: "Alice",
    email: "alice@example.com"
};
```

#### 2. Réinitialiser une variable

```javascript
let selection = "Option A";
console.log(selection);  // "Option A"

// L'utilisateur annule sa sélection
selection = null;
console.log(selection);  // null
```

#### 3. Indiquer qu'une recherche n'a rien trouvé

```javascript
function rechercherUtilisateur(id) {
    // Simulation de recherche
    if (id === 1) {
        return { nom: "Alice", id: 1 };
    } else {
        return null;  // Pas trouvé
    }
}

const utilisateur = rechercherUtilisateur(999);
if (utilisateur === null) {
    console.log("Utilisateur introuvable");
}
```

### Vérifier si une valeur est null

```javascript
let valeur = null;

// Méthode recommandée : comparaison stricte
if (valeur === null) {
    console.log("La valeur est null");
}

// ❌ Éviter
if (valeur == null) {
    // Ceci sera vrai aussi pour undefined !
}
```

### null est falsy

Comme `undefined`, `null` est considéré comme `false` dans un contexte booléen :

```javascript
let utilisateur = null;

if (utilisateur) {
    console.log("Utilisateur connecté");
} else {
    console.log("Aucun utilisateur");  // Ceci s'affiche
}
```

### typeof null : une bizarrerie historique 🐛

```javascript
console.log(typeof null);  // "object" ⚠️

// ⚠️ C'est un BUG historique de JavaScript !
// null devrait retourner "null", pas "object"
```

C'est une erreur dans la conception initiale de JavaScript qui ne peut pas être corrigée (pour des raisons de rétrocompatibilité).

**Comment vérifier null correctement :**

```javascript
const valeur = null;

// ❌ Ne fonctionne pas correctement
if (typeof valeur === "null") {  // Jamais vrai !
    console.log("C'est null");
}

// ✅ Utilisez la comparaison stricte
if (valeur === null) {
    console.log("C'est null");
}
```

### Exemples pratiques avec null

```javascript
// Gestion d'un champ optionnel
let telephone = null;  // Pas de téléphone renseigné

function afficherContact(nom, telephone) {
    console.log(`Nom : ${nom}`);

    if (telephone === null) {
        console.log("Téléphone : non renseigné");
    } else {
        console.log(`Téléphone : ${telephone}`);
    }
}

afficherContact("Alice", "06 12 34 56 78");  // Affiche le téléphone
afficherContact("Bob", null);                // "non renseigné"

// Réinitialiser un état
let panierActif = { produits: ["Livre", "Stylo"] };
console.log(panierActif);  // { produits: [...] }

// Vider le panier
panierActif = null;
console.log(panierActif);  // null
```

## undefined vs null : Quand utiliser quoi ?

### Règles générales

#### Utilisez undefined pour :
- ✅ Laisser JavaScript gérer (ne pas initialiser une variable `let`)
- ✅ Indiquer qu'un paramètre n'a pas été fourni
- ✅ Représenter l'absence "naturelle" d'une valeur

#### Utilisez null pour :
- ✅ Indiquer **intentionnellement** l'absence de valeur
- ✅ Réinitialiser une variable qui avait une valeur
- ✅ Indiquer qu'une recherche n'a rien trouvé
- ✅ Représenter "aucune valeur" de façon explicite

### Comparaison pratique

```javascript
// undefined : naturel, automatique
let nom;  // JavaScript met undefined
function sanReturn() { }  // Retourne undefined automatiquement

// null : intentionnel, explicite
let prenom = null;  // Le développeur décide
function aucunResultat() { return null; }  // Retour explicite
```

### Vérifier les deux avec ==

Si vous voulez vérifier `undefined` **ou** `null`, utilisez `==` (un des rares cas où `==` est acceptable) :

```javascript
let valeur;  // undefined

// Vérifie undefined ET null
if (valeur == null) {
    console.log("Pas de valeur");  // S'affiche
}

// Équivalent à :
if (valeur === null || valeur === undefined) {
    console.log("Pas de valeur");
}
```

> 💡 **Astuce** : `variable == null` est vrai si la variable est `null` **OU** `undefined`. C'est pratique !

## 3. Symbol 🔐 (ES6+)

### Qu'est-ce qu'un Symbol ?

Un **Symbol** est un type primitif introduit en ES6 (2015) qui représente un **identifiant unique et immuable**. Chaque Symbol créé est **garanti d'être unique**, même si deux Symbols ont la même description.

### Pourquoi Symbol existe-t-il ?

Les Symbols ont été créés pour éviter les conflits de noms de propriétés dans les objets, particulièrement dans les bibliothèques et frameworks.

### Créer un Symbol

```javascript
// Créer un Symbol
const symbole1 = Symbol();
const symbole2 = Symbol();

// Même sans description, chaque Symbol est unique !
console.log(symbole1 === symbole2);  // false

// Avec une description (optionnelle, pour le debug)
const id = Symbol("identifiant");
const nom = Symbol("nom");

console.log(id);  // Symbol(identifiant)
```

### Unicité garantie

```javascript
// Même description, mais Symbols différents !
const sym1 = Symbol("test");
const sym2 = Symbol("test");

console.log(sym1 === sym2);  // false
console.log(sym1);  // Symbol(test)
console.log(sym2);  // Symbol(test)
```

### Utilisation principale : propriétés d'objets uniques

```javascript
// Créer des Symbols
const ID = Symbol("id");
const SECRET = Symbol("secret");

// Utiliser comme clés de propriétés
const utilisateur = {
    nom: "Alice",
    [ID]: 12345,        // Propriété Symbol
    [SECRET]: "xyz789"  // Propriété Symbol
};

console.log(utilisateur.nom);     // "Alice"
console.log(utilisateur[ID]);     // 12345
console.log(utilisateur[SECRET]); // "xyz789"

// Les Symbols ne sont pas énumérables
console.log(Object.keys(utilisateur));  // ["nom"] - pas les Symbols !
```

### Symbol.for() et Symbol.keyFor()

Pour créer des Symbols **globaux** réutilisables :

```javascript
// Créer ou récupérer un Symbol global
const sym1 = Symbol.for("app.id");
const sym2 = Symbol.for("app.id");

console.log(sym1 === sym2);  // true ! (même Symbol)

// Récupérer la clé d'un Symbol global
const cle = Symbol.keyFor(sym1);
console.log(cle);  // "app.id"
```

### Well-known Symbols (Symbols prédéfinis)

JavaScript définit des Symbols spéciaux pour personnaliser le comportement des objets :

```javascript
// Symbol.iterator : définit comment un objet est itéré
// Symbol.toStringTag : définit la représentation en string
// Symbol.hasInstance : définit comment instanceof fonctionne
// ... et d'autres

const tableau = [1, 2, 3];
console.log(tableau[Symbol.iterator]);  // function
```

### typeof Symbol

```javascript
const sym = Symbol("test");
console.log(typeof sym);  // "symbol"
```

### Quand utiliser Symbol ?

#### Cas d'usage courants :

1. **Éviter les conflits de propriétés**
   ```javascript
   const INTERNE_ID = Symbol("id");

   const objet = {
       id: 123,           // ID publique
       [INTERNE_ID]: 456  // ID interne, ne peut pas entrer en conflit
   };
   ```

2. **Créer des "constantes" uniques**
   ```javascript
   const STATUT_EN_COURS = Symbol("en_cours");
   const STATUT_TERMINE = Symbol("termine");
   const STATUT_ERREUR = Symbol("erreur");

   let statut = STATUT_EN_COURS;

   if (statut === STATUT_EN_COURS) {
       console.log("Tâche en cours...");
   }
   ```

3. **Métaprogrammation avancée**
   ```javascript
   // Personnaliser le comportement d'objets
   const monObjet = {
       [Symbol.toStringTag]: "MonObjetPersonnalise"
   };

   console.log(monObjet.toString());  // [object MonObjetPersonnalise]
   ```

### Symbol : à connaître mais rarement utilisé

> 💡 **Pour les débutants** : Vous n'utiliserez probablement pas beaucoup les Symbols dans vos premiers projets. C'est normal ! Ils sont plus utiles dans des cas avancés (bibliothèques, frameworks, métaprogrammation). L'important est de **savoir qu'ils existent**.

## Comparaison des types spéciaux

| Type | Description | Cas d'usage typique | typeof |
|------|-------------|---------------------|--------|
| **undefined** | Non défini (automatique) | Variable non initialisée | `"undefined"` |
| **null** | Vide (intentionnel) | Absence explicite de valeur | `"object"` ⚠️ |
| **Symbol** | Identifiant unique | Propriétés uniques, métaprogrammation | `"symbol"` |

## Vérifier les types spéciaux

### Méthode recommandée pour chaque type

```javascript
let a;
let b = null;
let c = Symbol("test");

// undefined
console.log(a === undefined);           // true
console.log(typeof a === "undefined");  // true

// null
console.log(b === null);                // true ✅
console.log(typeof b === "object");     // true (mais pas fiable !)

// Symbol
console.log(typeof c === "symbol");     // true
```

### Vérifier "pas de valeur" (undefined OU null)

```javascript
function aUneValeur(variable) {
    // Méthode 1 : Vérification explicite
    return variable !== null && variable !== undefined;

    // Méthode 2 : Plus courte (avec ==)
    return variable != null;

    // Méthode 3 : Avec truthy (attention aux autres valeurs falsy !)
    return !!variable;  // false si 0, "", false aussi !
}

console.log(aUneValeur("texte"));   // true
console.log(aUneValeur(undefined)); // false
console.log(aUneValeur(null));      // false
console.log(aUneValeur(0));         // Varie selon la méthode !
```

## Valeurs falsy : récapitulatif

Tous ces types spéciaux font partie des **valeurs falsy** :

```javascript
// 6 valeurs falsy en JavaScript
if (false) { }       // false
if (0) { }           // 0
if ("") { }          // String vide
if (null) { }        // null ⭕
if (undefined) { }   // undefined ❓
if (NaN) { }         // Not a Number

// Tout le reste est truthy !
```

## Exemples pratiques complets

### Exemple 1 : Gestion de profil utilisateur

```javascript
// Profil avec informations optionnelles
const profil = {
    nom: "Alice",
    age: 25,
    telephone: null,      // Non renseigné intentionnellement
    photo: undefined      // Pas encore défini
};

// Affichage
function afficherProfil(profil) {
    console.log(`Nom : ${profil.nom}`);
    console.log(`Âge : ${profil.age}`);

    if (profil.telephone === null) {
        console.log("Téléphone : non renseigné");
    } else {
        console.log(`Téléphone : ${profil.telephone}`);
    }

    if (profil.photo === undefined) {
        console.log("Photo : pas encore définie");
    } else {
        console.log(`Photo : ${profil.photo}`);
    }
}

afficherProfil(profil);
```

### Exemple 2 : Recherche avec résultat null

```javascript
const utilisateurs = [
    { id: 1, nom: "Alice" },
    { id: 2, nom: "Bob" },
    { id: 3, nom: "Charlie" }
];

function trouverUtilisateur(id) {
    const utilisateur = utilisateurs.find(u => u.id === id);

    if (utilisateur === undefined) {
        return null;  // Pas trouvé : retourner null explicitement
    }

    return utilisateur;
}

const user1 = trouverUtilisateur(2);
console.log(user1);  // { id: 2, nom: "Bob" }

const user2 = trouverUtilisateur(999);
console.log(user2);  // null

// Utilisation
if (user2 === null) {
    console.log("Utilisateur introuvable");
}
```

### Exemple 3 : Paramètres optionnels

```javascript
function creerUtilisateur(nom, email, telephone) {
    const utilisateur = {
        nom: nom,
        email: email
    };

    // telephone est optionnel
    if (telephone !== undefined) {
        utilisateur.telephone = telephone;
    }

    return utilisateur;
}

const user1 = creerUtilisateur("Alice", "alice@example.com", "0612345678");
console.log(user1);  // { nom, email, telephone }

const user2 = creerUtilisateur("Bob", "bob@example.com");
console.log(user2);  // { nom, email } - pas de telephone
```

### Exemple 4 : Utilisation de Symbol pour propriétés privées

```javascript
// "Simuler" des propriétés privées avec Symbol
const _balance = Symbol("balance");
const _historique = Symbol("historique");

class CompteBancaire {
    constructor(soldeInitial) {
        this[_balance] = soldeInitial;
        this[_historique] = [];
    }

    deposer(montant) {
        this[_balance] += montant;
        this[_historique].push(`+${montant}`);
    }

    getSolde() {
        return this[_balance];
    }
}

const compte = new CompteBancaire(1000);
compte.deposer(500);

console.log(compte.getSolde());  // 1500

// Les propriétés Symbol ne sont pas visibles
console.log(Object.keys(compte));  // [] - vide !
console.log(compte._balance);      // undefined - pas accessible directement
```

## Bonnes pratiques

### ✅ À faire

1. **Utilisez null intentionnellement**
   ```javascript
   let resultat = null;  // Pas encore de résultat
   ```

2. **Vérifiez avec === pour null et undefined**
   ```javascript
   if (valeur === null) { }
   if (valeur === undefined) { }
   ```

3. **Utilisez == null pour vérifier les deux**
   ```javascript
   if (valeur == null) {  // null OU undefined
       console.log("Pas de valeur");
   }
   ```

4. **Donnez des valeurs par défaut aux paramètres**
   ```javascript
   function saluer(nom = "Visiteur") {
       console.log(`Bonjour ${nom}`);
   }
   ```

5. **Utilisez Symbol pour des identifiants vraiment uniques**
   ```javascript
   const ID_INTERNE = Symbol("id");
   ```

### ❌ À éviter

1. **Ne vérifiez pas null avec typeof**
   ```javascript
   if (typeof valeur === "null") { }  // ❌ Ne fonctionne jamais !
   ```

2. **N'assignez pas undefined manuellement**
   ```javascript
   let nom = undefined;  // ❌ Utilisez null à la place
   let prenom = null;    // ✅ Mieux
   ```

3. **Ne comparez pas avec == sauf pour null/undefined**
   ```javascript
   if (valeur == true) { }  // ❌ Utilisez ===
   if (valeur == null) { }  // ✅ OK (cas spécial)
   ```

4. **N'utilisez pas Symbol partout**
   ```javascript
   // ❌ Inutilement complexe
   const NOM = Symbol("nom");
   const obj = { [NOM]: "Alice" };

   // ✅ Simple suffit
   const obj = { nom: "Alice" };
   ```

## En résumé

### Les 3 types spéciaux

#### undefined ❓
```javascript
let variable;
console.log(variable);  // undefined
```
- Valeur **automatique** des variables non initialisées
- "Pas encore de valeur"
- Type : `"undefined"`

#### null ⭕
```javascript
let variable = null;
console.log(variable);  // null
```
- Absence **intentionnelle** de valeur
- "Volontairement vide"
- Type : `"object"` (bug historique)

#### Symbol 🔐
```javascript
const id = Symbol("id");
console.log(typeof id);  // "symbol"
```
- Identifiant **unique et immuable**
- Utile pour propriétés uniques
- Type : `"symbol"`

### Quand utiliser quoi ?

| Situation | Type à utiliser |
|-----------|----------------|
| Variable non initialisée | Laisser `undefined` |
| Réinitialiser une variable | `null` |
| Recherche sans résultat | `null` |
| Propriété unique garantie | `Symbol` |
| Paramètre non fourni | `undefined` (automatique) |

> 🎯 **À retenir** : `undefined` = automatique, `null` = intentionnel, `Symbol` = unique. Comprenez bien la différence entre `undefined` et `null`, c'est essentiel !

## Prochaine étape

Maintenant que vous connaissez tous les types primitifs (string, number, boolean, undefined, null, Symbol), nous allons découvrir l'opérateur **typeof** en détail pour vérifier les types de nos variables.

---


💡 **Citation** : "null est une absence de valeur intentionnelle, undefined est une absence de valeur accidentelle" - comprendre cette différence vous évitera bien des bugs !

⏭️ [Opérateur typeof](/05-javascript-moderne-fondamentaux/02-variables-et-types/05-operateur-typeof.md)
