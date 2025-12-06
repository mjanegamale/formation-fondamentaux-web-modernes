🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4.4 - Opérateur ternaire

## Introduction

L'**opérateur ternaire** (aussi appelé opérateur conditionnel) est un raccourci élégant pour écrire des conditions simples sur **une seule ligne**. C'est l'unique opérateur JavaScript qui prend **trois opérandes**.

Il permet de remplacer une structure `if...else` simple par une expression concise et lisible.

**Nom** : Il s'appelle "ternaire" parce qu'il utilise trois parties (condition, valeur si vrai, valeur si faux).

---

## Syntaxe

```javascript
condition ? valeurSiVrai : valeurSiFaux
```

**Structure** :
- **`condition`** : une expression qui s'évalue à `true` ou `false`
- **`?`** : séparateur "si vrai alors..."
- **`valeurSiVrai`** : valeur retournée si la condition est vraie
- **`:`** : séparateur "sinon..."
- **`valeurSiFaux`** : valeur retournée si la condition est fausse

### Lecture de gauche à droite

On peut lire l'opérateur ternaire comme une phrase :
```
condition ? "si oui, ça" : "sinon, ça"
```

---

## Comparaison avec if...else

### Avec if...else (verbose)

```javascript
let message;

if (age >= 18) {
    message = "Vous êtes majeur";
} else {
    message = "Vous êtes mineur";
}
```

### Avec l'opérateur ternaire (concis)

```javascript
const message = age >= 18 ? "Vous êtes majeur" : "Vous êtes mineur";
```

**Avantages** :
- ✅ Plus court (1 ligne au lieu de 5)
- ✅ Plus lisible pour les conditions simples
- ✅ Peut être utilisé dans des expressions
- ✅ Permet l'utilisation de `const`

---

## Exemples de base

### Exemple 1 : Affectation conditionnelle

```javascript
const age = 20;
const statut = age >= 18 ? "adulte" : "enfant";

console.log(statut); // "adulte"
```

### Exemple 2 : Affichage conditionnel

```javascript
const score = 85;
console.log(score >= 50 ? "Réussi" : "Échoué"); // "Réussi"
```

### Exemple 3 : Calcul conditionnel

```javascript
const heuresTrail = 45;
const salaireHoraire = 15;

// Heures supplémentaires après 40h payées 1.5x
const salaire = heuresTrail <= 40
    ? heuresTrail * salaireHoraire
    : (40 * salaireHoraire) + ((heuresTrail - 40) * salaireHoraire * 1.5);

console.log(salaire); // 712.5
```

### Exemple 4 : Classe CSS conditionnelle

```javascript
const estActif = true;
const className = estActif ? "btn-active" : "btn-inactive";

console.log(className); // "btn-active"
```

---

## Cas d'usage pratiques

### 1. Messages utilisateur

```javascript
const nouveauxMessages = 5;
const texte = nouveauxMessages === 1
    ? "1 nouveau message"
    : `${nouveauxMessages} nouveaux messages`;

console.log(texte); // "5 nouveaux messages"
```

### 2. Affichage de prix

```javascript
const prix = 0;
const affichage = prix > 0 ? `${prix}€` : "Gratuit";

console.log(affichage); // "Gratuit"
```

### 3. Statut de connexion

```javascript
const utilisateur = { nom: "Alice", connecte: true };
const statut = utilisateur.connecte ? "En ligne" : "Hors ligne";

console.log(statut); // "En ligne"
```

### 4. Validation de formulaire

```javascript
const email = "alice@example.com";
const estValide = email.includes("@") && email.includes(".");
const message = estValide ? "✅ Email valide" : "❌ Email invalide";

console.log(message); // "✅ Email valide"
```

### 5. Calcul de réduction

```javascript
const montant = 150;
const estMembre = true;

const total = estMembre ? montant * 0.9 : montant;
console.log(total); // 135 (réduction de 10%)
```

### 6. Pluralisation

```javascript
const nbProduits = 3;
const texte = `${nbProduits} produit${nbProduits > 1 ? "s" : ""}`;

console.log(texte); // "3 produits"
```

### 7. Icône selon statut

```javascript
const temperature = 25;
const icone = temperature > 20 ? "☀️" : temperature > 10 ? "⛅" : "❄️";

console.log(icone); // "☀️"
```

### 8. Couleur selon score

```javascript
const score = 75;
const couleur = score >= 80 ? "vert" : score >= 50 ? "orange" : "rouge";

console.log(couleur); // "orange"
```

---

## Dans des expressions

L'avantage majeur du ternaire est qu'il peut être utilisé **partout où une expression est attendue**.

### Dans console.log()

```javascript
const age = 16;
console.log(`Vous ${age >= 18 ? "pouvez" : "ne pouvez pas"} voter`);
// "Vous ne pouvez pas voter"
```

### Dans des template literals

```javascript
const nom = "Alice";
const estAdmin = true;

const message = `Bonjour ${nom}, vous êtes ${estAdmin ? "administrateur" : "utilisateur"}`;
console.log(message);
// "Bonjour Alice, vous êtes administrateur"
```

### Dans return

```javascript
function obtenirStatut(age) {
    return age >= 18 ? "majeur" : "mineur";
}

console.log(obtenirStatut(20)); // "majeur"
```

### Dans un tableau

```javascript
const age = 25;
const permissions = [
    "lecture",
    age >= 18 ? "écriture" : null,
    age >= 21 ? "suppression" : null
].filter(p => p !== null);

console.log(permissions); // ["lecture", "écriture", "suppression"]
```

### Dans un objet

```javascript
const estConnecte = true;

const utilisateur = {
    nom: "Alice",
    statut: estConnecte ? "actif" : "inactif",
    badge: estConnecte ? "🟢" : "🔴"
};

console.log(utilisateur);
// { nom: "Alice", statut: "actif", badge: "🟢" }
```

---

## Ternaires imbriqués

Il est possible d'imbriquer des opérateurs ternaires, mais **attention à la lisibilité** !

### Exemple simple (acceptable)

```javascript
const note = 15;
const mention = note >= 16 ? "Très bien"
              : note >= 14 ? "Bien"
              : note >= 12 ? "Assez bien"
              : note >= 10 ? "Passable"
              : "Insuffisant";

console.log(mention); // "Bien"
```

### Formaté pour la lisibilité

```javascript
const age = 25;
const tarif = age < 12 ? 5      // Enfant
            : age < 18 ? 10     // Adolescent
            : age < 65 ? 15     // Adulte
            : 10;               // Senior

console.log(tarif); // 15
```

### ⚠️ Trop complexe (à éviter)

```javascript
// ❌ Difficile à lire
const resultat = condition1 ? valeur1 : condition2 ? valeur2 : condition3 ? valeur3 : condition4 ? valeur4 : valeur5;

// ✅ Utilisez if...else ou switch pour plus de 2-3 niveaux
let resultat;
if (condition1) {
    resultat = valeur1;
} else if (condition2) {
    resultat = valeur2;
} else if (condition3) {
    resultat = valeur3;
} else if (condition4) {
    resultat = valeur4;
} else {
    resultat = valeur5;
}
```

---

## Quand utiliser le ternaire ?

### ✅ À UTILISER quand :

#### 1. Affectation simple basée sur une condition

```javascript
const statut = estConnecte ? "En ligne" : "Hors ligne";
```

#### 2. Valeurs par défaut

```javascript
const nom = utilisateur.nom ? utilisateur.nom : "Invité";
// Ou mieux avec nullish coalescing (section suivante) :
// const nom = utilisateur.nom ?? "Invité";
```

#### 3. Affichage conditionnel court

```javascript
console.log(`Résultat: ${succes ? "✅" : "❌"}`);
```

#### 4. Propriétés d'objet conditionnelles

```javascript
const config = {
    theme: modeNuit ? "dark" : "light",
    taille: estMobile ? "small" : "large"
};
```

#### 5. Arguments de fonction conditionnels

```javascript
afficherMessage(
    estErreur ? "Erreur" : "Succès",
    estErreur ? "rouge" : "vert"
);
```

### ❌ À ÉVITER quand :

#### 1. La logique est complexe

```javascript
// ❌ Trop complexe
const prix = estMembre ? (anciennete > 5 ? montant * 0.8 : montant * 0.9) : (montant > 100 ? montant * 0.95 : montant);

// ✅ Utilisez if...else
let prix;
if (estMembre) {
    prix = anciennete > 5 ? montant * 0.8 : montant * 0.9;
} else {
    prix = montant > 100 ? montant * 0.95 : montant;
}
```

#### 2. Vous devez exécuter plusieurs instructions

```javascript
// ❌ Impossible avec ternaire
if (estConnecte) {
    afficherTableauDeBord();
    chargerDonnees();
    demarrerTimer();
} else {
    afficherPageConnexion();
    effacerCache();
}
```

#### 3. La condition est très longue

```javascript
// ❌ Difficile à lire
const resultat = (utilisateur.age >= 18 && utilisateur.paysResidence === "FR" && utilisateur.accepteConditions) ? "autorisé" : "refusé";

// ✅ Plus clair avec variable intermédiaire
const estAutorise = utilisateur.age >= 18 &&
                    utilisateur.paysResidence === "FR" &&
                    utilisateur.accepteConditions;
const resultat = estAutorise ? "autorisé" : "refusé";
```

---

## Ternaire vs if...else : Tableau comparatif

| Critère | Opérateur ternaire | if...else |
|---------|-------------------|-----------|
| **Concision** | ✅ 1 ligne | ⚠️ 3-5 lignes |
| **Lisibilité simple** | ✅ Excellent | ✅ Bon |
| **Lisibilité complexe** | ❌ Mauvais | ✅ Excellent |
| **Affectation const** | ✅ Possible | ❌ Nécessite let |
| **Multiple instructions** | ❌ Impossible | ✅ Possible |
| **Retour de fonction** | ✅ Direct | ⚠️ Nécessite return |
| **Expression** | ✅ Oui | ❌ Non (statement) |

---

## Avec des fonctions

### Appel de fonction conditionnel

```javascript
const mode = "clair";
const couleur = mode === "clair" ? obtenirCouleurClaire() : obtenirCouleurSombre();
```

### Retour direct

```javascript
function obtenirRemise(estMembre) {
    return estMembre ? 0.10 : 0;
}

// Peut même être une arrow function
const obtenirRemise = (estMembre) => estMembre ? 0.10 : 0;
```

### Dans des méthodes

```javascript
const utilisateur = {
    nom: "Alice",
    estAdmin: true,
    obtenirBadge() {
        return this.estAdmin ? "👑 Admin" : "👤 Utilisateur";
    }
};

console.log(utilisateur.obtenirBadge()); // "👑 Admin"
```

---

## Chaînage et combinaisons

### Avec opérateurs logiques

```javascript
const age = 25;
const permis = true;

const peutConduire = age >= 18 && permis ? "Oui" : "Non";
console.log(peutConduire); // "Oui"
```

### Avec nullish coalescing (aperçu)

```javascript
const nom = null;
const affichage = nom ?? "Invité"; // Voir section 5.4.5

// Équivalent avec ternaire
const affichage2 = nom !== null && nom !== undefined ? nom : "Invité";
```

### Dans map()

```javascript
const nombres = [1, 2, 3, 4, 5];
const descriptions = nombres.map(n => n % 2 === 0 ? "pair" : "impair");

console.log(descriptions);
// ["impair", "pair", "impair", "pair", "impair"]
```

### Dans filter()

```javascript
const produits = [
    { nom: "A", prix: 50, stock: 5 },
    { nom: "B", prix: 30, stock: 0 },
    { nom: "C", prix: 70, stock: 3 }
];

const disponibles = produits.filter(p => p.stock > 0 ? true : false);
// Note : ici le ternaire est inutile, on pourrait juste faire : p.stock > 0
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier les deux-points

```javascript
// ❌ Erreur de syntaxe
const statut = estActif ? "Actif"; // Manque : "Inactif"

// ✅ Correct
const statut = estActif ? "Actif" : "Inactif";
```

### ❌ Erreur 2 : Ternaire pour plusieurs instructions

```javascript
// ❌ Impossible
age >= 18 ? (console.log("Majeur"); afficherMenu()) : console.log("Mineur");

// ✅ Utilisez if...else
if (age >= 18) {
    console.log("Majeur");
    afficherMenu();
} else {
    console.log("Mineur");
}
```

### ❌ Erreur 3 : Trop d'imbrication

```javascript
// ❌ Illisible
const x = a ? b ? c ? d : e : f : g;

// ✅ Utilisez if...else if...else
let x;
if (a) {
    if (b) {
        x = c ? d : e;
    } else {
        x = f;
    }
} else {
    x = g;
}
```

### ❌ Erreur 4 : Ternaire inutile

```javascript
// ❌ Redondant
const estVrai = condition ? true : false;

// ✅ La condition est déjà un booléen
const estVrai = condition;

// ❌ Redondant
const estFaux = condition ? false : true;

// ✅ Utilisez la négation
const estFaux = !condition;
```

### ❌ Erreur 5 : Mauvais ordre de priorité

```javascript
// ❌ Peut causer des surprises
const resultat = a + b > 10 ? "grand" : "petit";

// ✅ Utilisez des parenthèses pour clarifier
const resultat = (a + b) > 10 ? "grand" : "petit";
```

---

## Bonnes pratiques

### ✅ 1. Une condition, une ligne (pour les cas simples)

```javascript
// ✅ Lisible
const statut = estConnecte ? "En ligne" : "Hors ligne";

// ✅ Ou formaté si long
const message = utilisateur.estPremium
    ? "Accès complet à toutes les fonctionnalités"
    : "Accès limité - Passez Premium";
```

### ✅ 2. Ternaires imbriqués : alignez verticalement

```javascript
// ✅ Facile à suivre
const note = score >= 90 ? "A"
           : score >= 80 ? "B"
           : score >= 70 ? "C"
           : score >= 60 ? "D"
           : "F";
```

### ✅ 3. Variables intermédiaires pour conditions complexes

```javascript
// ❌ Difficile à lire
const acces = user.age >= 18 && user.verified && !user.banned ? "autorisé" : "refusé";

// ✅ Plus clair
const estEligible = user.age >= 18 && user.verified && !user.banned;
const acces = estEligible ? "autorisé" : "refusé";
```

### ✅ 4. Commentez les ternaires complexes

```javascript
const tarif = age < 12 ? 5      // Tarif enfant
            : age < 65 ? 15     // Tarif adulte
            : 10;               // Tarif senior
```

### ✅ 5. Préférez const avec le ternaire

```javascript
// ✅ Immuable avec const
const resultat = condition ? valeur1 : valeur2;

// ⚠️ Moins bon avec let
let resultat;
if (condition) {
    resultat = valeur1;
} else {
    resultat = valeur2;
}
```

---

## Cas pratiques complets

### 1. Système de badges utilisateur

```javascript
function obtenirBadge(utilisateur) {
    const anneesMembre = new Date().getFullYear() - utilisateur.anneeInscription;

    return utilisateur.estAdmin ? "👑 Admin"
         : utilisateur.estModerateur ? "🛡️ Modérateur"
         : anneesMembre >= 5 ? "⭐ Membre VIP"
         : anneesMembre >= 1 ? "✨ Membre"
         : "🆕 Nouveau";
}

const user = {
    estAdmin: false,
    estModerateur: false,
    anneeInscription: 2020
};

console.log(obtenirBadge(user)); // "⭐ Membre VIP"
```

### 2. Formatage de devises

```javascript
function formaterPrix(prix, devise = "EUR") {
    const symbole = devise === "EUR" ? "€"
                  : devise === "USD" ? "$"
                  : devise === "GBP" ? "£"
                  : devise;

    const position = devise === "USD" ? "avant" : "apres";

    return position === "avant"
        ? `${symbole}${prix.toFixed(2)}`
        : `${prix.toFixed(2)}${symbole}`;
}

console.log(formaterPrix(42.5, "EUR")); // "42.50€"
console.log(formaterPrix(42.5, "USD")); // "$42.50"
```

### 3. Calculateur de statut de commande

```javascript
function obtenirStatutCommande(commande) {
    const maintenant = new Date();
    const dateCommande = new Date(commande.date);
    const joursEcoules = Math.floor((maintenant - dateCommande) / (1000 * 60 * 60 * 24));

    return commande.livree ? "✅ Livrée"
         : commande.expedie ? (joursEcoules > 7 ? "⚠️ Retard de livraison" : "🚚 En transit")
         : commande.preparee ? "📦 En préparation"
         : commande.paye ? "💳 Paiement accepté"
         : "⏳ En attente de paiement";
}

const commande = {
    date: "2025-12-01",
    paye: true,
    preparee: true,
    expedie: true,
    livree: false
};

console.log(obtenirStatutCommande(commande)); // "🚚 En transit"
```

### 4. Générateur de messages d'erreur

```javascript
function validerFormulaire(data) {
    const erreurs = [];

    erreurs.push(
        data.nom.length < 2
            ? "Le nom doit contenir au moins 2 caractères"
            : null
    );

    erreurs.push(
        !data.email.includes("@")
            ? "L'email est invalide"
            : null
    );

    erreurs.push(
        data.age < 18
            ? "Vous devez avoir au moins 18 ans"
            : null
    );

    erreurs.push(
        data.motDePasse.length < 8
            ? "Le mot de passe doit contenir au moins 8 caractères"
            : null
    );

    const erreursReelles = erreurs.filter(e => e !== null);

    return erreursReelles.length > 0
        ? { valide: false, erreurs: erreursReelles }
        : { valide: true, erreurs: [] };
}

const formulaire = {
    nom: "A",
    email: "alice@example.com",
    age: 25,
    motDePasse: "secret"
};

console.log(validerFormulaire(formulaire));
// { valide: false, erreurs: ["Le nom doit...", "Le mot de passe doit..."] }
```

### 5. Affichage de durées relatives

```javascript
function tempsRelatif(timestamp) {
    const maintenant = Date.now();
    const difference = maintenant - timestamp;
    const secondes = Math.floor(difference / 1000);
    const minutes = Math.floor(secondes / 60);
    const heures = Math.floor(minutes / 60);
    const jours = Math.floor(heures / 24);

    return secondes < 60 ? "À l'instant"
         : minutes < 60 ? `Il y a ${minutes} minute${minutes > 1 ? "s" : ""}`
         : heures < 24 ? `Il y a ${heures} heure${heures > 1 ? "s" : ""}`
         : jours < 7 ? `Il y a ${jours} jour${jours > 1 ? "s" : ""}`
         : "Il y a plus d'une semaine";
}

const timestamp = Date.now() - (2 * 60 * 60 * 1000); // Il y a 2 heures
console.log(tempsRelatif(timestamp)); // "Il y a 2 heures"
```

---

## Points clés à retenir

✅ **Syntaxe** : `condition ? valeurSiVrai : valeurSiFaux`

✅ **Parfait pour** : affectations simples conditionnelles

✅ **Peut être utilisé** : dans les expressions, return, template literals

✅ **Permet l'usage de const** : au lieu de let avec if...else

✅ **Limite** : une seule expression par branche

✅ **Lisibilité** : excellent pour 1-2 niveaux, mauvais au-delà

✅ **Alternative** : utilisez if...else pour la logique complexe

⚠️ **Évitez** : les imbrications excessives (> 2-3 niveaux)

⚠️ **Évitez** : le ternaire quand plusieurs instructions sont nécessaires

---

## Quand utiliser quoi ?

| Situation | Recommandation |
|-----------|----------------|
| Affectation simple | ✅ Ternaire |
| 2-3 niveaux de conditions | ✅ Ternaire (bien formaté) |
| 4+ niveaux de conditions | ✅ if...else if...else |
| Plusieurs instructions | ✅ if...else |
| Retour de fonction simple | ✅ Ternaire |
| Logique métier complexe | ✅ if...else ou switch |
| Affichage conditionnel court | ✅ Ternaire |

---

## Dans la prochaine section

Dans la section **5.4.5 - Opérateurs modernes : nullish coalescing (??) et optional chaining (?.),** nous découvrirons deux opérateurs ES2020 qui simplifient grandement la gestion des valeurs null et undefined.

---


⏭️ [Opérateurs modernes : nullish coalescing (??) et optional chaining (?.)](/05-javascript-moderne-fondamentaux/04-operateurs/05-operateurs-modernes.md)
