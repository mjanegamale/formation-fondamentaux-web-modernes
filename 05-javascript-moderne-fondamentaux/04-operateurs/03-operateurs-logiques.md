🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4.3 - Opérateurs logiques

## Introduction

Les **opérateurs logiques** permettent de combiner plusieurs conditions ou d'inverser une condition. Ils sont essentiels pour créer des tests complexes et prendre des décisions basées sur plusieurs critères.

JavaScript offre trois opérateurs logiques principaux :
- **`&&`** (ET logique) - Toutes les conditions doivent être vraies
- **`||`** (OU logique) - Au moins une condition doit être vraie
- **`!`** (NON logique) - Inverse une condition

Ces opérateurs retournent toujours une valeur **booléenne** : `true` ou `false`.

---

## Vue d'ensemble des opérateurs

| Opérateur | Nom | Description | Exemple |
|-----------|-----|-------------|---------|
| `&&` | ET logique (AND) | Vrai si **toutes** les conditions sont vraies | `a && b` |
| `\|\|` | OU logique (OR) | Vrai si **au moins une** condition est vraie | `a \|\| b` |
| `!` | NON logique (NOT) | Inverse la valeur booléenne | `!a` |

---

## && (ET logique) - Toutes les conditions

L'opérateur `&&` retourne `true` uniquement si **toutes** les conditions sont vraies.

### Syntaxe

```javascript
condition1 && condition2
```

### Table de vérité

| condition1 | condition2 | condition1 && condition2 |
|------------|------------|--------------------------|
| `true` | `true` | `true` ✅ |
| `true` | `false` | `false` |
| `false` | `true` | `false` |
| `false` | `false` | `false` |

**Règle simple** : Si **une seule** condition est fausse, le résultat est `false`.

### Exemples de base

```javascript
// Deux conditions vraies
console.log(true && true);    // true

// Au moins une condition fausse
console.log(true && false);   // false
console.log(false && true);   // false
console.log(false && false);  // false
```

### Avec des comparaisons

```javascript
const age = 25;
const permis = true;

// Les deux conditions doivent être vraies
console.log(age >= 18 && permis === true);  // true

// Si une condition est fausse
const age2 = 16;
console.log(age2 >= 18 && permis === true); // false
```

### Cas d'usage pratiques

#### 1. Validation d'accès

```javascript
const age = 20;
const aUnBillet = true;

if (age >= 18 && aUnBillet) {
    console.log("✅ Accès autorisé");
} else {
    console.log("❌ Accès refusé");
}
```

#### 2. Validation de formulaire

```javascript
const username = "alice";
const password = "secret123";
const accepteConditions = true;

if (username.length > 0 && password.length >= 8 && accepteConditions) {
    console.log("✅ Formulaire valide");
} else {
    console.log("❌ Veuillez remplir tous les champs correctement");
}
```

#### 3. Plage de valeurs

```javascript
const note = 15;

// Vérifier si la note est entre 10 et 20
if (note >= 10 && note <= 20) {
    console.log("✅ Note valide");
} else {
    console.log("❌ Note invalide");
}
```

#### 4. Vérification de disponibilité

```javascript
const stock = 5;
const prixAbordable = true;
const livraison = true;

if (stock > 0 && prixAbordable && livraison) {
    console.log("🛒 Produit disponible à l'achat");
}
```

#### 5. Authentification

```javascript
const estConnecte = true;
const role = "admin";

if (estConnecte && role === "admin") {
    console.log("🔓 Accès administration autorisé");
}
```

### Chaîner plusieurs conditions

Vous pouvez combiner plus de deux conditions :

```javascript
const a = 5;
const b = 10;
const c = 15;

// Toutes les conditions doivent être vraies
if (a < b && b < c && c < 20) {
    console.log("Toutes les conditions sont remplies");
}
```

---

## || (OU logique) - Au moins une condition

L'opérateur `||` retourne `true` si **au moins une** condition est vraie.

### Syntaxe

```javascript
condition1 || condition2
```

### Table de vérité

| condition1 | condition2 | condition1 \|\| condition2 |
|------------|------------|---------------------------|
| `true` | `true` | `true` ✅ |
| `true` | `false` | `true` ✅ |
| `false` | `true` | `true` ✅ |
| `false` | `false` | `false` |

**Règle simple** : Il suffit qu'**une seule** condition soit vraie pour que le résultat soit `true`.

### Exemples de base

```javascript
// Au moins une condition vraie
console.log(true || true);    // true
console.log(true || false);   // true
console.log(false || true);   // true

// Toutes les conditions fausses
console.log(false || false);  // false
```

### Avec des comparaisons

```javascript
const age = 70;
const estEtudiant = false;

// Au moins une condition doit être vraie
console.log(age < 18 || estEtudiant);  // false (les deux sont fausses)

const age2 = 15;
console.log(age2 < 18 || estEtudiant); // true (première condition vraie)
```

### Cas d'usage pratiques

#### 1. Accès avec plusieurs critères

```javascript
const age = 70;
const estVIP = false;

if (age >= 65 || estVIP) {
    console.log("✅ Réduction accordée");
}
```

#### 2. Validation flexible

```javascript
const paypalActif = false;
const carteActif = true;
const especes = false;

if (paypalActif || carteActif || especes) {
    console.log("✅ Au moins un moyen de paiement disponible");
}
```

#### 3. Conditions d'erreur

```javascript
const username = "";
const email = "";

if (username === "" || email === "") {
    console.log("❌ Veuillez remplir tous les champs obligatoires");
}
```

#### 4. Rôles multiples

```javascript
const role = "moderateur";

if (role === "admin" || role === "moderateur" || role === "editeur") {
    console.log("🔓 Accès autorisé");
}
```

#### 5. Jours de fermeture

```javascript
const jour = "dimanche";

if (jour === "dimanche" || jour === "lundi") {
    console.log("🔒 Le magasin est fermé");
}
```

### Chaîner plusieurs conditions

```javascript
const jour = "samedi";

// Le magasin est ouvert tous les jours sauf dimanche et lundi
if (jour === "mardi" || jour === "mercredi" || jour === "jeudi" ||
    jour === "vendredi" || jour === "samedi") {
    console.log("🏪 Ouvert aujourd'hui");
}
```

---

## ! (NON logique) - Inversion

L'opérateur `!` inverse une valeur booléenne : `true` devient `false` et vice-versa.

### Syntaxe

```javascript
!condition
```

### Table de vérité

| condition | !condition |
|-----------|------------|
| `true` | `false` |
| `false` | `true` |

### Exemples de base

```javascript
console.log(!true);     // false
console.log(!false);    // true

const estConnecte = true;
console.log(!estConnecte); // false

const estVide = false;
console.log(!estVide);     // true
```

### Avec des comparaisons

```javascript
const age = 25;

// Inverser une comparaison
console.log(!(age < 18));  // true (car age < 18 est false)
console.log(!(age >= 18)); // false (car age >= 18 est true)
```

### Cas d'usage pratiques

#### 1. Vérifier qu'une condition n'est PAS vraie

```javascript
const estConnecte = false;

if (!estConnecte) {
    console.log("Veuillez vous connecter");
}
```

#### 2. Inverser un booléen

```javascript
let modeNuit = false;

// Basculer le mode
modeNuit = !modeNuit;
console.log(modeNuit); // true

modeNuit = !modeNuit;
console.log(modeNuit); // false
```

#### 3. Vérifier l'absence

```javascript
const utilisateur = null;

if (!utilisateur) {
    console.log("❌ Aucun utilisateur trouvé");
}
```

#### 4. Validation négative

```javascript
const emailValide = false;

if (!emailValide) {
    console.log("⚠️ Veuillez entrer un email valide");
}
```

#### 5. Cacher/afficher un élément

```javascript
let menuVisible = true;

// Toggle (basculer)
function toggleMenu() {
    menuVisible = !menuVisible;
    console.log(menuVisible ? "Menu affiché" : "Menu caché");
}

toggleMenu(); // Menu caché
toggleMenu(); // Menu affiché
```

### Double négation !!

Le double `!` convertit une valeur en booléen :

```javascript
// Première négation : convertit en booléen inverse
// Deuxième négation : inverse à nouveau (retour au booléen correct)

console.log(!!"hello");   // true (string non-vide)
console.log(!!"");        // false (string vide)
console.log(!!0);         // false
console.log(!!5);         // true
console.log(!!null);      // false
console.log(!!undefined); // false
```

**Note** : En JavaScript moderne, préférez `Boolean(valeur)` :

```javascript
// ✅ Plus clair
console.log(Boolean("hello")); // true
console.log(Boolean(""));      // false
```

---

## Combiner les opérateurs logiques

Vous pouvez combiner `&&`, `||` et `!` pour créer des conditions complexes.

### Ordre de priorité

1. **`!`** (NON) - Priorité la plus haute
2. **`&&`** (ET) - Priorité moyenne
3. **`||`** (OU) - Priorité la plus basse

### Exemples de combinaison

#### ET puis OU

```javascript
const age = 20;
const estEtudiant = true;
const aCarteReduction = false;

// (âge entre 18 et 25 ET étudiant) OU carte de réduction
if ((age >= 18 && age <= 25 && estEtudiant) || aCarteReduction) {
    console.log("✅ Réduction accordée");
}
```

#### Condition complexe avec négation

```javascript
const estConnecte = true;
const estBanni = false;
const ageValide = true;

// Connecté ET (pas banni) ET âge valide
if (estConnecte && !estBanni && ageValide) {
    console.log("✅ Accès autorisé");
}
```

#### Validation de formulaire avancée

```javascript
const nom = "Alice";
const email = "alice@example.com";
const age = 25;
const accepteConditions = true;

const formulaireValide =
    nom.length > 0 &&
    email.includes("@") &&
    (age >= 18 || accepteConditions) &&
    accepteConditions;

if (formulaireValide) {
    console.log("✅ Formulaire complet");
}
```

### Utiliser des parenthèses pour la clarté

Les parenthèses rendent votre intention plus claire :

```javascript
// ❌ Difficile à lire
if (a && b || c && d || e) { }

// ✅ Plus clair avec parenthèses
if ((a && b) || (c && d) || e) { }
```

---

## Court-circuit (Short-circuit evaluation)

JavaScript utilise l'**évaluation en court-circuit** : il arrête d'évaluer dès que le résultat est connu.

### Avec && (ET)

Si la première condition est `false`, JavaScript n'évalue pas les suivantes :

```javascript
const resultat = false && faireQuelqueChose();
// faireQuelqueChose() n'est JAMAIS appelée

// Exemple pratique
const utilisateur = null;

// Vérifie d'abord si utilisateur existe
if (utilisateur && utilisateur.role === "admin") {
    console.log("Admin");
}
// Sans utilisateur, utilisateur.role ne sera jamais évaluée (pas d'erreur)
```

### Avec || (OU)

Si la première condition est `true`, JavaScript n'évalue pas les suivantes :

```javascript
const resultat = true || faireQuelqueChose();
// faireQuelqueChose() n'est JAMAIS appelée

// Exemple pratique : valeur par défaut
const nom = nomUtilisateur || "Invité";
// Si nomUtilisateur est vide/null/undefined, utilise "Invité"
```

### Cas d'usage pratiques du court-circuit

#### 1. Éviter les erreurs

```javascript
const utilisateur = null;

// ✅ Sécurisé grâce au court-circuit
if (utilisateur && utilisateur.age > 18) {
    console.log("Adulte");
}

// ❌ Sans court-circuit, ceci causerait une erreur
// if (utilisateur.age > 18) { } // TypeError!
```

#### 2. Valeurs par défaut

```javascript
function saluer(nom) {
    // Si nom est vide/null/undefined, utilise "Invité"
    const nomFinal = nom || "Invité";
    console.log(`Bonjour ${nomFinal}`);
}

saluer("Alice");  // Bonjour Alice
saluer("");       // Bonjour Invité
saluer(null);     // Bonjour Invité
```

#### 3. Exécution conditionnelle

```javascript
const estConnecte = true;
const utilisateur = { nom: "Alice" };

// Exécute la fonction seulement si connecté
estConnecte && afficherTableauDeBord(utilisateur);

// Équivalent à :
if (estConnecte) {
    afficherTableauDeBord(utilisateur);
}
```

#### 4. Chaîne de vérifications

```javascript
const config = {
    theme: {
        couleur: "bleu"
    }
};

// Accès sécurisé avec court-circuit
const couleur = config && config.theme && config.theme.couleur;
console.log(couleur); // "bleu"

// Si config.theme n'existait pas, pas d'erreur
```

---

## Valeurs "truthy" et "falsy"

En JavaScript, toutes les valeurs peuvent être évaluées en contexte booléen.

### Valeurs "falsy" (considérées comme false)

```javascript
// Ces 6 valeurs sont "falsy"
Boolean(false);      // false
Boolean(0);          // false
Boolean("");         // false (string vide)
Boolean(null);       // false
Boolean(undefined);  // false
Boolean(NaN);        // false
```

### Valeurs "truthy" (considérées comme true)

Toutes les autres valeurs sont "truthy" :

```javascript
Boolean(true);       // true
Boolean(1);          // true
Boolean(-1);         // true
Boolean("hello");    // true
Boolean("0");        // true (string non-vide)
Boolean(" ");        // true (espace)
Boolean([]);         // true (tableau vide)
Boolean({});         // true (objet vide)
Boolean(function(){}); // true
```

### Utilisation pratique

```javascript
const message = "";

// "message" est évalué comme false (string vide)
if (message) {
    console.log(message);
} else {
    console.log("Pas de message"); // S'exécute
}
```

### Attention aux pièges

```javascript
// ⚠️ Ces valeurs sont "truthy" !
console.log(Boolean("0"));      // true (pas 0 !)
console.log(Boolean("false"));  // true (string, pas booléen)
console.log(Boolean([]));       // true (tableau vide)
console.log(Boolean({}));       // true (objet vide)
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Confondre && et ||

```javascript
const age = 25;
const permis = false;

// ❌ Utilisation incorrecte de ||
if (age >= 18 || permis === true) {
    console.log("Peut conduire"); // S'exécute même sans permis !
}

// ✅ Il faut &&
if (age >= 18 && permis === true) {
    console.log("Peut conduire");
}
```

### ❌ Erreur 2 : Mauvais ordre d'évaluation

```javascript
const valeur = null;

// ❌ Erreur : vérifie la propriété avant l'objet
if (valeur.length > 0 && valeur !== null) {
    // TypeError: Cannot read property 'length' of null
}

// ✅ Vérifier l'objet d'abord (court-circuit)
if (valeur !== null && valeur.length > 0) {
    console.log("Valide");
}
```

### ❌ Erreur 3 : Trop de négations

```javascript
const estPasInvalide = true;

// ❌ Confus
if (!estPasInvalide) { }

// ✅ Plus clair avec variable positive
const estValide = true;
if (estValide) { }
```

### ❌ Erreur 4 : Oublier les parenthèses

```javascript
// ❌ Ambigu à cause de la priorité
if (a && b || c && d) { }

// ✅ Clair avec parenthèses
if ((a && b) || (c && d)) { }
```

### ❌ Erreur 5 : Comparaison avec booléens inutile

```javascript
const estConnecte = true;

// ❌ Redondant
if (estConnecte === true) { }

// ✅ Plus simple
if (estConnecte) { }

// ❌ Redondant
if (estConnecte === false) { }

// ✅ Plus simple
if (!estConnecte) { }
```

---

## Bonnes pratiques

### ✅ Utilisez des variables pour la lisibilité

```javascript
// ❌ Difficile à comprendre
if ((age >= 18 && age <= 65) && (salaire > 30000 || epargne > 50000) && !aBanqueroute) { }

// ✅ Beaucoup plus clair
const estEnAgeActif = age >= 18 && age <= 65;
const aCapaciteFinanciere = salaire > 30000 || epargne > 50000;
const estSolvable = !aBanqueroute;

if (estEnAgeActif && aCapaciteFinanciere && estSolvable) { }
```

### ✅ Évitez les doubles négations

```javascript
// ❌ Confus
if (!(!estActif)) { }

// ✅ Simple
if (estActif) { }
```

### ✅ Utilisez des noms de variables positifs

```javascript
// ❌ Nécessite souvent des négations
const nestPasValide = true;
if (!nestPasValide) { }

// ✅ Plus naturel
const estValide = false;
if (estValide) { }
```

### ✅ Ordonnez vos conditions logiquement

```javascript
// ✅ Vérifiez d'abord les conditions les plus "bloquantes"
if (estConnecte && !estBanni && aUnAbonnement) {
    // Si pas connecté, les autres ne sont pas vérifiées
}
```

### ✅ Utilisez le court-circuit intelligemment

```javascript
// ✅ Accès sécurisé aux propriétés
const nom = utilisateur && utilisateur.profil && utilisateur.profil.nom;

// ✅ Valeur par défaut
const langue = configUtilisateur.langue || "fr";
```

---

## Cas pratiques complets

### 1. Système de permissions

```javascript
function peutModifier(utilisateur, document) {
    // L'utilisateur peut modifier si :
    // - Il est l'auteur du document OU
    // - Il est admin OU
    // - Il est éditeur ET le document n'est pas verrouillé

    const estAuteur = utilisateur.id === document.auteurId;
    const estAdmin = utilisateur.role === "admin";
    const estEditeur = utilisateur.role === "editeur";
    const documentVerrouille = document.verrouille;

    return estAuteur || estAdmin || (estEditeur && !documentVerrouille);
}

const user = { id: 1, role: "editeur" };
const doc = { auteurId: 2, verrouille: false };

console.log(peutModifier(user, doc)); // true
```

### 2. Validation de commande

```javascript
function validerCommande(panier, utilisateur, paiement) {
    // Conditions nécessaires
    const panierNonVide = panier.articles.length > 0;
    const stockDisponible = panier.articles.every(a => a.stock > 0);
    const utilisateurConnecte = utilisateur && utilisateur.id;
    const adresseLivraison = utilisateur && utilisateur.adresse;
    const paiementValide = paiement && paiement.montant > 0;

    // Toutes les conditions doivent être remplies
    if (panierNonVide && stockDisponible && utilisateurConnecte &&
        adresseLivraison && paiementValide) {
        return "✅ Commande validée";
    }

    // Messages d'erreur spécifiques
    if (!panierNonVide) return "❌ Panier vide";
    if (!stockDisponible) return "❌ Certains articles sont en rupture";
    if (!utilisateurConnecte) return "❌ Veuillez vous connecter";
    if (!adresseLivraison) return "❌ Adresse de livraison manquante";
    if (!paiementValide) return "❌ Informations de paiement invalides";
}
```

### 3. Système de tarification

```javascript
function calculerPrix(age, estEtudiant, estSenior, weekend) {
    const PRIX_BASE = 15;
    let prix = PRIX_BASE;

    // Réductions cumulables
    const aReductionAge = age < 12 || age >= 65;
    const aReductionEtudiant = estEtudiant && age >= 18 && age <= 25;

    if (aReductionAge) {
        prix *= 0.5; // -50%
    }

    if (aReductionEtudiant) {
        prix *= 0.7; // -30%
    }

    // Supplément weekend (ne s'applique pas si réduction senior)
    if (weekend && !estSenior) {
        prix *= 1.2; // +20%
    }

    return prix.toFixed(2);
}

console.log(calculerPrix(10, false, false, true));  // Enfant
console.log(calculerPrix(20, true, false, false));  // Étudiant
console.log(calculerPrix(70, false, true, true));   // Senior
```

### 4. Filtre de recherche avancé

```javascript
function filtrerProduits(produits, filtres) {
    return produits.filter(produit => {
        // Prix dans la fourchette (si spécifié)
        const prixOK = !filtres.prixMax || produit.prix <= filtres.prixMax;

        // Catégorie correspond (si spécifiée)
        const categorieOK = !filtres.categorie ||
                           produit.categorie === filtres.categorie;

        // En stock (si requis)
        const stockOK = !filtres.enStockUniquement || produit.stock > 0;

        // Marque dans la liste (si spécifiée)
        const marqueOK = !filtres.marques ||
                        filtres.marques.includes(produit.marque);

        // Note minimale (si spécifiée)
        const noteOK = !filtres.noteMin || produit.note >= filtres.noteMin;

        // Toutes les conditions doivent être remplies
        return prixOK && categorieOK && stockOK && marqueOK && noteOK;
    });
}

const produits = [
    { nom: "Produit A", prix: 50, categorie: "tech", stock: 5, marque: "X", note: 4.5 },
    { nom: "Produit B", prix: 30, categorie: "tech", stock: 0, marque: "Y", note: 3.5 }
];

const filtres = {
    prixMax: 60,
    categorie: "tech",
    enStockUniquement: true,
    noteMin: 4
};

console.log(filtrerProduits(produits, filtres));
```

### 5. Détection de conditions d'alerte

```javascript
function verifierAlertes(systeme) {
    const alertes = [];

    // Température critique
    if (systeme.temperature > 80 || systeme.temperature < 0) {
        alertes.push("🔥 Alerte température");
    }

    // Mémoire saturée
    if (systeme.memoireUtilisee / systeme.memoireTotal > 0.9) {
        alertes.push("💾 Mémoire critique");
    }

    // Disque plein ET pas de backup récent
    const disquePlein = systeme.disqueUtilise / systeme.disqueTotal > 0.95;
    const backupAncien = systeme.dernierBackup > 7; // jours

    if (disquePlein && backupAncien) {
        alertes.push("⚠️ Disque saturé sans backup récent");
    }

    // CPU surchargé ET services critiques actifs
    if (systeme.cpuUtilisation > 90 && systeme.servicesCritiques) {
        alertes.push("⚡ CPU surchargé - services critiques affectés");
    }

    return alertes;
}

const systeme = {
    temperature: 85,
    memoireUtilisee: 7.5,
    memoireTotal: 8,
    disqueUtilise: 480,
    disqueTotal: 500,
    dernierBackup: 10,
    cpuUtilisation: 95,
    servicesCritiques: true
};

console.log(verifierAlertes(systeme));
// ["🔥 Alerte température", "⚠️ Disque saturé...", "⚡ CPU surchargé..."]
```

---

## Points clés à retenir

✅ **`&&` (ET)** - Toutes les conditions doivent être vraies

✅ **`||` (OU)** - Au moins une condition doit être vraie

✅ **`!` (NON)** - Inverse une valeur booléenne

✅ **Priorité** : `!` > `&&` > `||`

✅ **Court-circuit** : JavaScript arrête l'évaluation dès que le résultat est connu

✅ **Truthy/Falsy** : Toutes les valeurs peuvent être évaluées en contexte booléen

✅ **Utilisez des parenthèses** pour clarifier les conditions complexes

✅ **Variables intermédiaires** améliorent la lisibilité

✅ **Évitez les doubles négations** et les noms de variables négatifs

---

## Tableau récapitulatif

| Opérateur | Signification | Exemple | Résultat |
|-----------|---------------|---------|----------|
| `&&` | ET - Tous vrais | `true && true` | `true` |
| `&&` | ET - Un faux | `true && false` | `false` |
| `\|\|` | OU - Un vrai | `true \|\| false` | `true` |
| `\|\|` | OU - Tous faux | `false \|\| false` | `false` |
| `!` | NON - Inverse | `!true` | `false` |
| `!` | NON - Inverse | `!false` | `true` |

---

## Dans la prochaine section

Dans la section **5.4.4 - Opérateur ternaire**, nous découvrirons un raccourci élégant pour écrire des conditions simples sur une seule ligne : `condition ? siVrai : siFaux`.

---


⏭️ [Opérateur ternaire](/05-javascript-moderne-fondamentaux/04-operateurs/04-operateur-ternaire.md)
