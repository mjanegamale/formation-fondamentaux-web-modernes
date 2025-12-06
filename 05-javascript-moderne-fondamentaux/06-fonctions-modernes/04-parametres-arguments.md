🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.4 - Paramètres et arguments

## Introduction

Lorsque vous créez des fonctions, il est essentiel de comprendre la différence entre **paramètres** et **arguments**, et comment les données sont transmises aux fonctions. Cette compréhension vous permettra d'écrire des fonctions flexibles et puissantes.

## Paramètres vs Arguments : quelle différence ?

Bien que souvent utilisés de manière interchangeable, ces termes ont des significations distinctes :

### Paramètres

Les **paramètres** sont les **variables** listées dans la **déclaration** de la fonction. Ce sont des "emplacements" qui attendent de recevoir des valeurs.

```javascript
function saluer(prenom, age) {
  //           ^^^^^^  ^^^
  //           Paramètres : variables dans la définition
  console.log("Bonjour " + prenom + ", vous avez " + age + " ans.");
}
```

### Arguments

Les **arguments** sont les **valeurs réelles** que vous passez à la fonction lors de son **appel**.

```javascript
saluer("Alice", 25);
//     ^^^^^^^  ^^
//     Arguments : valeurs réelles passées
```

### Analogie simple

Pensez à une fonction comme à une machine :
- Les **paramètres** sont les **bouches d'entrée** de la machine
- Les **arguments** sont les **ingrédients** que vous mettez dans ces entrées

```javascript
// La machine (fonction) a 2 entrées (paramètres)
function mixer(ingredient1, ingredient2) {
  return ingredient1 + " + " + ingredient2;
}

// Vous mettez des ingrédients réels (arguments) dans les entrées
mixer("fraise", "banane"); // Arguments
```

## Déclaration de paramètres

### Syntaxe

Les paramètres sont déclarés entre parenthèses, séparés par des virgules :

```javascript
// Aucun paramètre
function direBonjour() {
  console.log("Bonjour !");
}

// Un paramètre
function saluer(nom) {
  console.log("Bonjour " + nom);
}

// Deux paramètres
function additionner(a, b) {
  return a + b;
}

// Trois paramètres ou plus
function creerPersonne(prenom, nom, age, ville) {
  return prenom + " " + nom + ", " + age + " ans, habite à " + ville;
}
```

### Nommage des paramètres

Les paramètres suivent les mêmes règles que les variables :

✅ **Bonnes pratiques :**
```javascript
function calculerSurface(longueur, largeur) { }     // Descriptif
function creerUtilisateur(prenom, email) { }        // Clair
function convertir(montant, deviseSource, deviseCible) { }  // Explicite
```

❌ **À éviter :**
```javascript
function calculer(a, b) { }          // Trop vague
function faire(x, y, z) { }          // Pas descriptif
function fonction1(param1, param2) { } // Noms génériques
```

## Ordre des arguments

L'ordre dans lequel vous passez les arguments est **crucial** : chaque argument correspond au paramètre à la même position.

### Exemple de correspondance

```javascript
function presenter(prenom, nom, age, ville) {
  console.log(prenom + " " + nom + ", " + age + " ans, habite à " + ville);
}

presenter("Alice", "Martin", 28, "Paris");
//        ^^^^^^   ^^^^^^^^  ^^   ^^^^^^^
//        |        |         |    |
//        prenom   nom       age  ville
```

### Erreur d'ordre

```javascript
function calculerPrix(prixHT, tauxTVA) {
  return prixHT + (prixHT * tauxTVA / 100);
}

// ✅ Correct
calculerPrix(100, 20);  // 100€ HT, 20% TVA = 120€

// ❌ Inversé : résultat incorrect !
calculerPrix(20, 100);  // 20€ HT, 100% TVA = 40€
```

**Règle d'or :** Respectez toujours l'ordre défini dans la déclaration de la fonction.

## Nombre d'arguments

### Correspondance parfaite (idéal)

```javascript
function additionner(a, b) {
  return a + b;
}

additionner(5, 3); // ✅ 2 paramètres, 2 arguments = parfait
// Résultat : 8
```

### Moins d'arguments que de paramètres

Si vous passez **moins d'arguments** que de paramètres, les paramètres manquants valent `undefined` :

```javascript
function saluer(prenom, nom) {
  console.log("Bonjour " + prenom + " " + nom);
}

saluer("Alice");  // Seulement 1 argument au lieu de 2
// Affiche : "Bonjour Alice undefined"
```

#### Gérer les paramètres manquants

Vous pouvez vérifier si un paramètre est `undefined` :

```javascript
function saluer(prenom, nom) {
  if (nom === undefined) {
    console.log("Bonjour " + prenom);
  } else {
    console.log("Bonjour " + prenom + " " + nom);
  }
}

saluer("Alice");           // Affiche : "Bonjour Alice"
saluer("Alice", "Martin"); // Affiche : "Bonjour Alice Martin"
```

Ou utiliser l'opérateur `||` pour une valeur par défaut :

```javascript
function saluer(prenom, nom) {
  nom = nom || "Anonyme";
  console.log("Bonjour " + prenom + " " + nom);
}

saluer("Alice");           // Affiche : "Bonjour Alice Anonyme"
saluer("Alice", "Martin"); // Affiche : "Bonjour Alice Martin"
```

**Note :** Nous verrons une meilleure solution avec les **paramètres par défaut** dans la section suivante (5.6.5).

### Plus d'arguments que de paramètres

JavaScript **ignore** les arguments supplémentaires (mais ils ne causent pas d'erreur) :

```javascript
function additionner(a, b) {
  return a + b;
}

additionner(5, 3, 10, 20, 30); // Seulement 5 et 3 sont utilisés
// Résultat : 8 (les autres sont ignorés)
```

**Note :** Nous verrons comment capturer tous les arguments avec les **rest parameters** (`...args`) dans la section 5.6.6.

## Types de données en paramètres

Les fonctions peuvent accepter n'importe quel type de données comme arguments.

### Types primitifs

```javascript
function afficherInfos(texte, nombre, booleen) {
  console.log("Texte:", texte);       // String
  console.log("Nombre:", nombre);     // Number
  console.log("Booléen:", booleen);   // Boolean
}

afficherInfos("Bonjour", 42, true);
// Affiche :
// Texte: Bonjour
// Nombre: 42
// Booléen: true
```

### Tableaux

```javascript
function afficherPremier(tableau) {
  console.log("Premier élément:", tableau[0]);
}

afficherPremier([10, 20, 30]); // Affiche : "Premier élément: 10"
```

### Objets

```javascript
function afficherPersonne(personne) {
  console.log(personne.prenom + " " + personne.nom);
}

const utilisateur = { prenom: "Alice", nom: "Martin" };
afficherPersonne(utilisateur); // Affiche : "Alice Martin"
```

### Fonctions

Oui, même des fonctions peuvent être passées en arguments (callbacks) !

```javascript
function executerOperation(a, b, operation) {
  return operation(a, b);
}

const additionner = (x, y) => x + y;
const multiplier = (x, y) => x * y;

console.log(executerOperation(5, 3, additionner));  // Affiche : 8
console.log(executerOperation(5, 3, multiplier));   // Affiche : 15
```

## Passage par valeur vs passage par référence

C'est un concept important pour comprendre comment les données sont manipulées dans les fonctions.

### Types primitifs : passage par valeur

Les **types primitifs** (number, string, boolean, etc.) sont passés **par valeur**. Cela signifie qu'une **copie** de la valeur est créée.

```javascript
function doubler(nombre) {
  nombre = nombre * 2;
  console.log("Dans la fonction:", nombre);
  return nombre;
}

let x = 5;
const resultat = doubler(x);

console.log("Résultat:", resultat);  // Affiche : "Résultat: 10"
console.log("Variable x:", x);       // Affiche : "Variable x: 5"
//                                   // x n'a PAS changé !
```

**Explication :** La variable `x` à l'extérieur de la fonction n'est **pas modifiée** car la fonction travaille sur une copie.

### Objets et tableaux : passage par référence

Les **objets** et **tableaux** sont passés **par référence**. La fonction reçoit une référence vers l'objet original, pas une copie.

#### Avec un objet

```javascript
function changerNom(personne) {
  personne.nom = "Nouveau Nom";
}

const utilisateur = { nom: "Alice", age: 25 };
console.log("Avant:", utilisateur.nom);  // Affiche : "Avant: Alice"

changerNom(utilisateur);

console.log("Après:", utilisateur.nom);  // Affiche : "Après: Nouveau Nom"
//                                       // L'objet ORIGINAL a été modifié !
```

#### Avec un tableau

```javascript
function ajouterElement(tableau) {
  tableau.push("nouvel élément");
}

const liste = ["a", "b", "c"];
console.log("Avant:", liste);  // Affiche : "Avant: ["a", "b", "c"]"

ajouterElement(liste);

console.log("Après:", liste);  // Affiche : "Après: ["a", "b", "c", "nouvel élément"]"
//                             // Le tableau ORIGINAL a été modifié !
```

### Réassignation vs modification

Il y a une subtilité importante :

#### Réassigner le paramètre (n'affecte pas l'original)

```javascript
function changerTableau(tableau) {
  tableau = [1, 2, 3]; // Réassignation : nouvelle référence
}

const monTableau = [10, 20];
changerTableau(monTableau);
console.log(monTableau); // Affiche : [10, 20]
//                       // Pas de changement !
```

#### Modifier le contenu (affecte l'original)

```javascript
function modifierTableau(tableau) {
  tableau[0] = 999; // Modification du contenu
}

const monTableau = [10, 20];
modifierTableau(monTableau);
console.log(monTableau); // Affiche : [999, 20]
//                       // Le tableau a changé !
```

### Éviter les modifications involontaires

Pour éviter de modifier accidentellement un objet ou tableau passé en argument, créez une copie :

#### Copier un tableau

```javascript
function ajouterSansModifier(tableau, element) {
  const copie = [...tableau];  // Spread operator : crée une copie
  copie.push(element);
  return copie;
}

const original = [1, 2, 3];
const nouveau = ajouterSansModifier(original, 4);

console.log(original);  // Affiche : [1, 2, 3] (inchangé)
console.log(nouveau);   // Affiche : [1, 2, 3, 4]
```

#### Copier un objet

```javascript
function modifierSansImpact(personne, nouveauNom) {
  const copie = { ...personne };  // Spread operator : crée une copie
  copie.nom = nouveauNom;
  return copie;
}

const original = { nom: "Alice", age: 25 };
const modifie = modifierSansImpact(original, "Bob");

console.log(original.nom);  // Affiche : "Alice" (inchangé)
console.log(modifie.nom);   // Affiche : "Bob"
```

## Exemples pratiques complets

### Exemple 1 : Calculateur de prix

```javascript
const calculerTotal = (prixUnitaire, quantite, remise) => {
  const sousTotal = prixUnitaire * quantite;
  const montantRemise = sousTotal * (remise / 100);
  const total = sousTotal - montantRemise;
  return total;
};

console.log(calculerTotal(10, 5, 10));   // 10€ × 5 - 10% = 45€
console.log(calculerTotal(25, 3, 20));   // 25€ × 3 - 20% = 60€
```

### Exemple 2 : Formateur de nom complet

```javascript
const formaterNomComplet = (prenom, nom, titre) => {
  if (titre === undefined) {
    return prenom + " " + nom;
  }
  return titre + " " + prenom + " " + nom;
};

console.log(formaterNomComplet("Alice", "Martin"));
// Affiche : "Alice Martin"

console.log(formaterNomComplet("Alice", "Martin", "Dr."));
// Affiche : "Dr. Alice Martin"
```

### Exemple 3 : Traitement de tableau

```javascript
const calculerMoyenne = (notes) => {
  let somme = 0;
  for (let i = 0; i < notes.length; i++) {
    somme += notes[i];
  }
  return somme / notes.length;
};

const notesEleve = [15, 12, 18, 14, 16];
console.log("Moyenne:", calculerMoyenne(notesEleve));
// Affiche : "Moyenne: 15"
```

### Exemple 4 : Manipulation d'objet

```javascript
const afficherInfosProduit = (produit) => {
  console.log("Produit: " + produit.nom);
  console.log("Prix: " + produit.prix + "€");
  console.log("En stock: " + (produit.stock ? "Oui" : "Non"));
};

const ordinateur = {
  nom: "Laptop Pro",
  prix: 1200,
  stock: true
};

afficherInfosProduit(ordinateur);
// Affiche :
// Produit: Laptop Pro
// Prix: 1200€
// En stock: Oui
```

### Exemple 5 : Fonction avec callback

```javascript
const traiterNombres = (a, b, operation) => {
  return operation(a, b);
};

const addition = (x, y) => x + y;
const soustraction = (x, y) => x - y;
const multiplication = (x, y) => x * y;

console.log(traiterNombres(10, 5, addition));        // Affiche : 15
console.log(traiterNombres(10, 5, soustraction));    // Affiche : 5
console.log(traiterNombres(10, 5, multiplication));  // Affiche : 50
```

## Déstructuration de paramètres (aperçu)

Une technique moderne (ES6+) pour extraire directement des propriétés d'objets passés en arguments :

### Sans déstructuration

```javascript
const afficherPersonne = (personne) => {
  console.log(personne.nom + " - " + personne.age + " ans");
};

afficherPersonne({ nom: "Alice", age: 25 });
```

### Avec déstructuration

```javascript
const afficherPersonne = ({ nom, age }) => {
  console.log(nom + " - " + age + " ans");
};

afficherPersonne({ nom: "Alice", age: 25 });
```

**Plus lisible et plus court !** Nous approfondirons ce concept dans la section sur les objets (5.7.4).

## Bonnes pratiques

### 1. Nommez vos paramètres de manière descriptive

```javascript
// ❌ Vague
function calculer(a, b, c) {
  return a * b * c;
}

// ✅ Clair
function calculerVolume(longueur, largeur, hauteur) {
  return longueur * largeur * hauteur;
}
```

### 2. Limitez le nombre de paramètres

Si une fonction a plus de **3-4 paramètres**, envisagez d'utiliser un objet :

```javascript
// ❌ Trop de paramètres
function creerUtilisateur(prenom, nom, email, telephone, adresse, codePostal, ville) {
  // ...
}

// ✅ Utiliser un objet
function creerUtilisateur(infos) {
  console.log(infos.prenom);
  console.log(infos.email);
  // ...
}

creerUtilisateur({
  prenom: "Alice",
  nom: "Martin",
  email: "alice@example.com",
  telephone: "0123456789",
  adresse: "123 rue Example",
  codePostal: "75000",
  ville: "Paris"
});
```

### 3. Ordonnez les paramètres logiquement

```javascript
// Paramètres obligatoires d'abord, optionnels ensuite
function creerMessage(texte, destinataire, copie) {
  // texte et destinataire sont obligatoires
  // copie est optionnel
}
```

### 4. Documentez vos fonctions

```javascript
/**
 * Calcule le prix total avec remise
 * @param {number} prix - Prix unitaire
 * @param {number} quantite - Nombre d'articles
 * @param {number} remise - Pourcentage de remise (0-100)
 * @returns {number} Prix total après remise
 */
function calculerTotal(prix, quantite, remise) {
  return prix * quantite * (1 - remise / 100);
}
```

### 5. Validez les paramètres critiques

```javascript
function diviser(a, b) {
  if (b === 0) {
    console.error("Erreur: division par zéro !");
    return null;
  }
  return a / b;
}

console.log(diviser(10, 2));  // Affiche : 5
console.log(diviser(10, 0));  // Affiche erreur et retourne null
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Mauvais ordre des arguments

```javascript
function inscrire(nom, prenom, email) {
  console.log(nom + " " + prenom + " - " + email);
}

// ❌ Arguments dans le mauvais ordre
inscrire("alice@test.com", "Alice", "Martin");
// Affiche : "alice@test.com Alice - Martin" (incorrect !)

// ✅ Correct
inscrire("Martin", "Alice", "alice@test.com");
```

### ❌ Erreur 2 : Ne pas vérifier les paramètres undefined

```javascript
function saluer(nom) {
  // ❌ Crash si nom est undefined
  console.log("Bonjour " + nom.toUpperCase());
}

saluer(); // ❌ Erreur : Cannot read property 'toUpperCase' of undefined

// ✅ Avec vérification
function saluer(nom) {
  if (nom === undefined) {
    console.log("Bonjour visiteur !");
    return;
  }
  console.log("Bonjour " + nom.toUpperCase());
}
```

### ❌ Erreur 3 : Modifier un objet sans le vouloir

```javascript
function doublerNombres(tableau) {
  // ❌ Modifie le tableau original !
  for (let i = 0; i < tableau.length; i++) {
    tableau[i] = tableau[i] * 2;
  }
  return tableau;
}

const original = [1, 2, 3];
const double = doublerNombres(original);
console.log(original); // [2, 4, 6] - Oups, l'original a changé !

// ✅ Créer une copie
function doublerNombres(tableau) {
  const copie = [...tableau];
  for (let i = 0; i < copie.length; i++) {
    copie[i] = copie[i] * 2;
  }
  return copie;
}
```

## Points clés à retenir

1. **Paramètres** = variables dans la définition | **Arguments** = valeurs réelles passées

2. **L'ordre compte** : chaque argument correspond au paramètre à la même position

3. **Arguments manquants** : valent `undefined`

4. **Arguments supplémentaires** : sont ignorés (mais pas d'erreur)

5. **Types primitifs** : passés par valeur (copie)

6. **Objets/Tableaux** : passés par référence (modifications affectent l'original)

7. **Bonnes pratiques** :
   - Noms descriptifs
   - 3-4 paramètres maximum
   - Validation des entrées critiques
   - Documentation claire

## Prochaines étapes

Maintenant que vous comprenez les paramètres et arguments, vous êtes prêt pour :

- Les **paramètres par défaut** (5.6.5) - donner des valeurs par défaut aux paramètres
- Les **rest parameters** (`...args`) (5.6.6) - capturer un nombre variable d'arguments
- Les **callbacks** (5.6.10) - passer des fonctions en arguments

Ces concepts vous permettront de créer des fonctions encore plus flexibles et puissantes !

---

**Note :** La maîtrise des paramètres et arguments est fondamentale pour écrire des fonctions efficaces. Comprendre le passage par valeur vs par référence vous évitera de nombreux bugs difficiles à déboguer. Prenez le temps de bien assimiler ces concepts avant de continuer.

⏭️ [Paramètres par défaut (ES6)](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/05-parametres-par-defaut.md)
