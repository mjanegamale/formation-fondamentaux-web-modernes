🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.6 - Transformation : toLowerCase, toUpperCase, trim

## Introduction

Les méthodes de **transformation** permettent de modifier le contenu d'une string pour créer une nouvelle version transformée. Ces opérations sont essentielles pour :
- Normaliser les données utilisateur
- Comparer des strings sans tenir compte de la casse
- Nettoyer les entrées de formulaires
- Formater du texte

Dans cette section, nous allons découvrir trois méthodes fondamentales :
- **`toLowerCase()`** : convertir en minuscules
- **`toUpperCase()`** : convertir en majuscules
- **`trim()`** : supprimer les espaces en début et fin

**Rappel important** : Les strings sont immutables. Ces méthodes **créent une nouvelle string** et ne modifient pas l'originale.

---

## toLowerCase() - Conversion en minuscules

### Syntaxe

```javascript
string.toLowerCase()
```

### Retourne

Une **nouvelle string** avec tous les caractères alphabétiques en minuscules.

### Utilisation de base

```javascript
const texte = "BONJOUR";
const minuscules = texte.toLowerCase();

console.log(minuscules); // "bonjour"
console.log(texte);      // "BONJOUR" (inchangé)
```

### Exemples variés

```javascript
console.log("JAVASCRIPT".toLowerCase());           // "javascript"
console.log("Hello World".toLowerCase());          // "hello world"
console.log("ABC123xyz".toLowerCase());            // "abc123xyz"
console.log("École".toLowerCase());                // "école"
console.log("ÀÉÈÊËÏÔÙ".toLowerCase());             // "àéèêëïôù"
```

**Note** : Les chiffres et symboles ne sont pas affectés, seuls les caractères alphabétiques sont convertis.

### Cas d'usage pratiques

#### 1. Comparaison insensible à la casse

```javascript
const input1 = "JavaScript";
const input2 = "javascript";

// ❌ Comparaison directe (sensible à la casse)
console.log(input1 === input2); // false

// ✅ Comparaison insensible à la casse
console.log(input1.toLowerCase() === input2.toLowerCase()); // true
```

#### 2. Validation d'email

```javascript
const email = "Alice.Dupont@EXAMPLE.COM";
const emailNormalise = email.toLowerCase();

console.log(emailNormalise); // "alice.dupont@example.com"

// Sauvegarder en base de données en minuscules
```

#### 3. Recherche insensible à la casse

```javascript
const texte = "JavaScript est un langage génial";
const recherche = "JAVASCRIPT";

if (texte.toLowerCase().includes(recherche.toLowerCase())) {
    console.log("Trouvé !");
}
```

#### 4. Normalisation des tags

```javascript
const tags = ["JavaScript", "REACT", "Node.js", "vue"];
const tagsNormalises = tags.map(tag => tag.toLowerCase());

console.log(tagsNormalises);
// ["javascript", "react", "node.js", "vue"]
```

#### 5. Création d'identifiants (slugs)

```javascript
const titre = "Mon Article Important";
const slug = titre.toLowerCase().replace(/ /g, "-");

console.log(slug); // "mon-article-important"
```

---

## toUpperCase() - Conversion en majuscules

### Syntaxe

```javascript
string.toUpperCase()
```

### Retourne

Une **nouvelle string** avec tous les caractères alphabétiques en majuscules.

### Utilisation de base

```javascript
const texte = "bonjour";
const majuscules = texte.toUpperCase();

console.log(majuscules); // "BONJOUR"
console.log(texte);      // "bonjour" (inchangé)
```

### Exemples variés

```javascript
console.log("javascript".toUpperCase());           // "JAVASCRIPT"
console.log("Hello World".toUpperCase());          // "HELLO WORLD"
console.log("abc123xyz".toUpperCase());            // "ABC123XYZ"
console.log("école".toUpperCase());                // "ÉCOLE"
console.log("àéèêëïôù".toUpperCase());             // "ÀÉÈÊËÏÔÙ"
```

### Cas d'usage pratiques

#### 1. Affichage de titres ou en-têtes

```javascript
const titre = "bienvenue sur notre site";
const titreFormate = titre.toUpperCase();

console.log(titreFormate); // "BIENVENUE SUR NOTRE SITE"
```

#### 2. Codes de pays ou devises

```javascript
const pays = "france";
const codeISO = pays.slice(0, 2).toUpperCase();

console.log(codeISO); // "FR"

const devise = "eur";
console.log(devise.toUpperCase()); // "EUR"
```

#### 3. Abréviations et acronymes

```javascript
const mots = ["HyperText", "Markup", "Language"];
const acronyme = mots.map(mot => mot[0]).join("").toUpperCase();

console.log(acronyme); // "HTML"
```

#### 4. Messages d'alerte

```javascript
const message = "attention : erreur critique !";
const alerte = message.toUpperCase();

console.log(alerte); // "ATTENTION : ERREUR CRITIQUE !"
```

#### 5. Formatage de code postal ou immatriculation

```javascript
const immatriculation = "ab-123-cd";
const immatriculationFormatee = immatriculation.toUpperCase();

console.log(immatriculationFormatee); // "AB-123-CD"
```

---

## Capitalisation - Première lettre en majuscule

JavaScript n'a pas de méthode native pour capitaliser (première lettre en majuscule), mais on peut la créer facilement :

### Méthode simple

```javascript
const mot = "javascript";
const capitalise = mot[0].toUpperCase() + mot.slice(1);

console.log(capitalise); // "Javascript"
```

### Fonction réutilisable

```javascript
function capitaliser(string) {
    return string[0].toUpperCase() + string.slice(1).toLowerCase();
}

console.log(capitaliser("JAVASCRIPT")); // "Javascript"
console.log(capitaliser("bonjour"));    // "Bonjour"
console.log(capitaliser("hELLO"));      // "Hello"
```

### Capitaliser chaque mot (Title Case)

```javascript
function capitaliserMots(phrase) {
    return phrase
        .split(" ")
        .map(mot => mot[0].toUpperCase() + mot.slice(1).toLowerCase())
        .join(" ");
}

console.log(capitaliserMots("bonjour le monde"));
// "Bonjour Le Monde"

console.log(capitaliserMots("JAVASCRIPT EST GÉNIAL"));
// "Javascript Est Génial"
```

---

## trim() - Suppression des espaces

### Syntaxe

```javascript
string.trim()
```

### Retourne

Une **nouvelle string** sans les espaces (et autres caractères d'espacement) au début et à la fin.

### Caractères supprimés par trim()

`trim()` supprime :
- Les espaces normaux
- Les tabulations (`\t`)
- Les sauts de ligne (`\n`)
- Les retours chariot (`\r`)
- Et autres caractères d'espacement Unicode

### Utilisation de base

```javascript
const texte = "   Bonjour   ";
const nettoye = texte.trim();

console.log(texte);    // "   Bonjour   "
console.log(nettoye);  // "Bonjour"
console.log(texte.length);   // 13
console.log(nettoye.length); // 7
```

### Exemples variés

```javascript
console.log("   JavaScript   ".trim());     // "JavaScript"
console.log("\n\nBonjour\n\n".trim());      // "Bonjour"
console.log("\t\tCode\t\t".trim());         // "Code"
console.log("  Texte  mixte  ".trim());     // "Texte  mixte" (espaces internes conservés)
```

**Important** : `trim()` ne supprime que les espaces au **début** et à la **fin**, pas ceux au milieu !

### Cas d'usage pratiques

#### 1. Nettoyage d'entrées utilisateur (TRÈS IMPORTANT)

```javascript
const nomUtilisateur = "  alice  ";
const nomNettoye = nomUtilisateur.trim();

console.log(nomNettoye); // "alice"

// Évite des erreurs de connexion dues aux espaces !
```

#### 2. Validation de formulaire

```javascript
const champNom = "   ";

if (champNom.trim() === "") {
    console.log("Le champ nom est vide ou ne contient que des espaces");
}

// Meilleure validation
if (champNom.trim().length === 0) {
    console.log("Veuillez remplir le champ nom");
}
```

#### 3. Comparaison de données

```javascript
const input = "  JavaScript  ";
const reference = "JavaScript";

// ❌ Sans trim
console.log(input === reference); // false

// ✅ Avec trim
console.log(input.trim() === reference); // true
```

#### 4. Parsing de données CSV/texte

```javascript
const ligne = "  Alice,  25,  Paris  ";
const donnees = ligne.split(",").map(item => item.trim());

console.log(donnees);
// ["Alice", "25", "Paris"]
```

#### 5. Nettoyage de messages

```javascript
const message = `
    Bonjour,
    Ceci est un message
    avec plusieurs lignes
`;

const messagePropre = message.trim();
console.log(messagePropre);
// "Bonjour,
//     Ceci est un message
//     avec plusieurs lignes"
```

---

## trimStart() et trimEnd() - Versions ciblées 🆕

JavaScript moderne offre deux variantes pour un contrôle plus précis :

### trimStart() (ou trimLeft())

Supprime les espaces **uniquement au début** :

```javascript
const texte = "   Bonjour   ";

console.log(texte.trimStart());  // "Bonjour   "
console.log(texte.trimLeft());   // "Bonjour   " (alias)
```

### trimEnd() (ou trimRight())

Supprime les espaces **uniquement à la fin** :

```javascript
const texte = "   Bonjour   ";

console.log(texte.trimEnd());   // "   Bonjour"
console.log(texte.trimRight()); // "   Bonjour" (alias)
```

### Quand les utiliser ?

```javascript
// Exemple : formatage de code avec indentation
const code = "    console.log('Hello');";

// On veut garder l'indentation mais retirer les espaces de fin
const codeNettoye = code.trimEnd();
```

**Note** : `trimStart()` et `trimEnd()` sont les noms modernes recommandés. `trimLeft()` et `trimRight()` sont des alias plus anciens.

---

## Combiner les méthodes de transformation

Les méthodes de transformation peuvent être **chaînées** (appliquées successivement) :

### Exemples de chaînage

```javascript
const input = "  HELLO WORLD  ";

// Nettoyer puis convertir en minuscules
const resultat1 = input.trim().toLowerCase();
console.log(resultat1); // "hello world"

// Nettoyer puis convertir en majuscules
const resultat2 = input.trim().toUpperCase();
console.log(resultat2); // "HELLO WORLD"

// Combinaison complexe
const texte = "  javascript est GÉNIAL  ";
const resultat3 = texte.trim().toLowerCase();
console.log(resultat3); // "javascript est génial"
```

### Fonction de normalisation complète

```javascript
function normaliser(string) {
    return string.trim().toLowerCase();
}

console.log(normaliser("  JAVASCRIPT  ")); // "javascript"
console.log(normaliser("React  "));         // "react"
console.log(normaliser("  Node.js  "));     // "node.js"
```

### Validation d'email complète

```javascript
function validerEmail(email) {
    // 1. Nettoyer
    const emailNettoye = email.trim().toLowerCase();

    // 2. Vérifier le format basique
    if (!emailNettoye.includes("@") || !emailNettoye.includes(".")) {
        return false;
    }

    // 3. Vérifier qu'il n'est pas vide
    if (emailNettoye.length === 0) {
        return false;
    }

    return true;
}

console.log(validerEmail("  Alice@Example.COM  ")); // true
console.log(validerEmail("invalide"));              // false
```

### Préparation de recherche

```javascript
function preparerRecherche(texte, recherche) {
    const texteNormalise = texte.trim().toLowerCase();
    const rechercheNormalisee = recherche.trim().toLowerCase();

    return texteNormalise.includes(rechercheNormalisee);
}

console.log(preparerRecherche("  JavaScript est GÉNIAL  ", "  javascript  "));
// true
```

---

## Cas pratiques complets

### 1. Formulaire d'inscription

```javascript
const nom = "  Dupont  ";
const prenom = "  alice  ";
const email = "  ALICE.DUPONT@EXAMPLE.COM  ";

// Normalisation
const nomFinal = nom.trim();
const prenomFinal = prenom.trim()[0].toUpperCase() + prenom.trim().slice(1).toLowerCase();
const emailFinal = email.trim().toLowerCase();

console.log(nomFinal);    // "Dupont"
console.log(prenomFinal); // "Alice"
console.log(emailFinal);  // "alice.dupont@example.com"
```

### 2. Traitement de commentaires

```javascript
const commentaire = `
    Super article !
    Merci pour les explications
`;

// Nettoyer et normaliser
const commentaireNettoye = commentaire.trim();

// Vérifier la longueur minimale
if (commentaireNettoye.length < 10) {
    console.log("Commentaire trop court");
} else {
    console.log("Commentaire valide");
}
```

### 3. Création d'identifiant unique (slug)

```javascript
function creerSlug(titre) {
    return titre
        .trim()
        .toLowerCase()
        .replace(/[^a-z0-9]+/g, "-")  // Remplacer caractères spéciaux par -
        .replace(/^-+|-+$/g, "");     // Retirer - au début/fin
}

console.log(creerSlug("  Mon Super Article !  "));
// "mon-super-article"

console.log(creerSlug("JavaScript : Guide Complet"));
// "javascript-guide-complet"
```

### 4. Comparateur de mots de passe

```javascript
function comparerMotsDePasse(mdp1, mdp2) {
    // Les mots de passe sont sensibles à la casse et aux espaces
    // Mais on trim pour éviter les erreurs de saisie
    return mdp1.trim() === mdp2.trim();
}

const motDePasse = "MonMotDePasse123";
const confirmation = "MonMotDePasse123  "; // Espace accidentel

console.log(comparerMotsDePasse(motDePasse, confirmation)); // true
```

### 5. Parser une liste de tags

```javascript
const inputTags = "  JavaScript, REACT,   Vue.js , Node  ";

const tags = inputTags
    .split(",")
    .map(tag => tag.trim().toLowerCase())
    .filter(tag => tag.length > 0);

console.log(tags);
// ["javascript", "react", "vue.js", "node"]
```

---

## Immutabilité : rappel important

**Les strings sont immutables**. Les méthodes de transformation ne modifient jamais la string originale :

```javascript
let texte = "  JAVASCRIPT  ";

// ❌ Ceci ne modifie PAS texte
texte.trim();
texte.toLowerCase();

console.log(texte); // "  JAVASCRIPT  " (inchangé)

// ✅ Il faut réassigner
texte = texte.trim().toLowerCase();
console.log(texte); // "javascript"
```

### Chaînage et performance

Le chaînage est pratique mais crée des strings intermédiaires :

```javascript
const resultat = texte.trim().toLowerCase().slice(0, 10);

// Équivalent à :
// const etape1 = texte.trim();         // Nouvelle string
// const etape2 = etape1.toLowerCase(); // Nouvelle string
// const resultat = etape2.slice(0, 10); // Nouvelle string
```

**Note pour débutants** : Ne vous inquiétez pas pour les performances, JavaScript optimise très bien ces opérations. La lisibilité est plus importante !

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier d'assigner le résultat

```javascript
let email = "  ALICE@EXAMPLE.COM  ";

// ❌ Le résultat est perdu
email.trim().toLowerCase();
console.log(email); // "  ALICE@EXAMPLE.COM  " (inchangé)

// ✅ Réassigner la variable
email = email.trim().toLowerCase();
console.log(email); // "alice@example.com"
```

### ❌ Erreur 2 : Oublier les parenthèses

```javascript
const texte = "Bonjour";

// ❌ Oubli des parenthèses
console.log(texte.toLowerCase); // [Function: toLowerCase] (la fonction elle-même)

// ✅ Avec parenthèses
console.log(texte.toLowerCase()); // "bonjour"
```

### ❌ Erreur 3 : Trim() ne supprime pas les espaces internes

```javascript
const texte = "  Hello   World  ";

// ❌ Les espaces entre les mots restent
console.log(texte.trim()); // "Hello   World"

// ✅ Pour supprimer tous les espaces multiples
const sansTropEspaces = texte.trim().replace(/\s+/g, " ");
console.log(sansTropEspaces); // "Hello World"
```

### ❌ Erreur 4 : Comparaison sans normalisation

```javascript
const input = "  JavaScript  ";
const reference = "javascript";

// ❌ Comparaison incorrecte
if (input === reference) { } // false

// ✅ Normaliser avant de comparer
if (input.trim().toLowerCase() === reference) { } // true
```

---

## Méthodes obsolètes (à éviter)

JavaScript avait des méthodes plus anciennes qui sont maintenant déconseillées :

### ⚠️ toLocaleLowerCase() / toLocaleUpperCase()

Ces méthodes existent mais sont rarement nécessaires. Elles tiennent compte des règles linguistiques locales :

```javascript
const turc = "İstanbul"; // İ turc (avec point)

console.log(turc.toLowerCase());       // "i̇stanbul"
console.log(turc.toLocaleLowerCase("tr")); // "istanbul" (i sans point en turc)
```

**Conseil** : Utilisez simplement `toLowerCase()` et `toUpperCase()` dans 99% des cas.

---

## Bonnes pratiques

### 1. Toujours nettoyer les entrées utilisateur

```javascript
function traiterInput(input) {
    // 1. D'abord trim
    // 2. Puis autres transformations
    return input.trim().toLowerCase();
}
```

### 2. Normaliser avant de comparer

```javascript
function comparerStrings(str1, str2) {
    return str1.trim().toLowerCase() === str2.trim().toLowerCase();
}
```

### 3. Valider après transformation

```javascript
const input = "   ";

// ✅ Valider après trim
if (input.trim().length === 0) {
    console.log("Champ vide");
}

// Au lieu de
if (input.length === 0) { } // Ne détecte pas les espaces
```

### 4. Chaîner les méthodes pour la lisibilité

```javascript
// ✅ Clair et concis
const resultat = input.trim().toLowerCase().slice(0, 50);

// Au lieu de
const etape1 = input.trim();
const etape2 = etape1.toLowerCase();
const resultat = etape2.slice(0, 50);
```

---

## Tableau récapitulatif

| Méthode | Action | Retourne | Exemple |
|---------|--------|----------|---------|
| `toLowerCase()` | Convertit en minuscules | Nouvelle string | `"HELLO".toLowerCase()` → `"hello"` |
| `toUpperCase()` | Convertit en majuscules | Nouvelle string | `"hello".toUpperCase()` → `"HELLO"` |
| `trim()` | Supprime espaces début/fin | Nouvelle string | `" hi ".trim()` → `"hi"` |
| `trimStart()` 🆕 | Supprime espaces début | Nouvelle string | `" hi ".trimStart()` → `"hi "` |
| `trimEnd()` 🆕 | Supprime espaces fin | Nouvelle string | `" hi ".trimEnd()` → `" hi"` |

---

## Points clés à retenir

✅ **`toLowerCase()`** convertit tous les caractères en minuscules

✅ **`toUpperCase()`** convertit tous les caractères en majuscules

✅ **`trim()`** supprime les espaces au début et à la fin (pas au milieu)

✅ **Immutabilité** : ces méthodes créent une nouvelle string, elles ne modifient pas l'originale

✅ **Chaînage** : vous pouvez combiner plusieurs méthodes → `string.trim().toLowerCase()`

✅ **Toujours nettoyer** les entrées utilisateur avec `trim()` avant validation

✅ **Normaliser** avant de comparer des strings (trim + toLowerCase)

✅ **Ne pas oublier les parenthèses** : `toLowerCase()` pas `toLowerCase`

---

## Dans la prochaine section

Dans la section **5.3.7 - Méthodes split et join**, nous découvrirons comment convertir des strings en tableaux et vice-versa, une opération essentielle pour manipuler du texte structuré.

---


⏭️ [Méthodes split et join](/05-javascript-moderne-fondamentaux/03-strings-modernes/07-split-join.md)
