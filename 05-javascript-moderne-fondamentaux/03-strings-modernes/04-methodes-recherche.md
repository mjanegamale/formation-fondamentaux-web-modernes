🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.4 - Méthodes de recherche : indexOf, includes, startsWith, endsWith

## Introduction

Rechercher du texte dans une string est une opération extrêmement courante en programmation. JavaScript offre plusieurs méthodes pour effectuer ces recherches, des plus anciennes aux plus modernes.

Dans cette section, nous allons découvrir quatre méthodes principales :
- **`indexOf()`** : méthode classique qui retourne la position
- **`includes()`** 🆕 : méthode moderne qui retourne true/false
- **`startsWith()`** 🆕 : vérifie si la string commence par...
- **`endsWith()`** 🆕 : vérifie si la string se termine par...

---

## Vue d'ensemble des méthodes

| Méthode | Retourne | Usage moderne | Description |
|---------|----------|---------------|-------------|
| `indexOf()` | Nombre (index ou -1) | ⚠️ Legacy | Position de la première occurrence |
| `includes()` | Boolean (true/false) | ✅ Recommandée | Présence d'une sous-chaîne |
| `startsWith()` | Boolean (true/false) | ✅ Recommandée | Commence par... |
| `endsWith()` | Boolean (true/false) | ✅ Recommandée | Se termine par... |

**Conseil moderne** : Privilégiez `includes()`, `startsWith()` et `endsWith()` pour la lisibilité. Utilisez `indexOf()` uniquement si vous avez besoin de la position exacte.

---

## includes() - La méthode moderne 🆕

### Syntaxe

```javascript
string.includes(recherche, position)
```

- **`recherche`** : le texte à rechercher (obligatoire)
- **`position`** : position de départ (optionnel, par défaut 0)

### Retourne

`true` si la sous-chaîne est trouvée, `false` sinon.

### Utilisation de base

```javascript
const phrase = "JavaScript est un langage génial";

console.log(phrase.includes("JavaScript")); // true
console.log(phrase.includes("Python"));     // false
console.log(phrase.includes("langage"));    // true
console.log(phrase.includes("JAVASCRIPT")); // false (sensible à la casse)
```

### Pourquoi includes() est mieux ?

**Avant (avec indexOf) :**

```javascript
const texte = "Bonjour le monde";

// ❌ Moins lisible
if (texte.indexOf("monde") !== -1) {
    console.log("Le mot 'monde' est présent");
}
```

**Maintenant (avec includes) :**

```javascript
const texte = "Bonjour le monde";

// ✅ Beaucoup plus clair
if (texte.includes("monde")) {
    console.log("Le mot 'monde' est présent");
}
```

### Exemples pratiques

#### Vérifier un mot-clé dans un message

```javascript
const message = "Votre commande a été expédiée";

if (message.includes("expédiée")) {
    console.log("✅ La commande est en route");
}
```

#### Filtrer des résultats de recherche

```javascript
const produits = [
    "iPhone 15",
    "Samsung Galaxy S24",
    "iPad Pro",
    "MacBook Air"
];

const recherche = "iPhone";

const resultats = produits.filter(produit => produit.includes(recherche));
console.log(resultats); // ["iPhone 15"]
```

#### Validation d'email (simple)

```javascript
const email = "alice@example.com";

if (email.includes("@") && email.includes(".")) {
    console.log("Format d'email potentiellement valide");
} else {
    console.log("Email invalide");
}
```

### Paramètre position

Vous pouvez spécifier à partir de quelle position commencer la recherche :

```javascript
const texte = "chat chat chat";

console.log(texte.includes("chat"));      // true
console.log(texte.includes("chat", 0));   // true (commence à l'index 0)
console.log(texte.includes("chat", 5));   // true (trouve le 2ème "chat")
console.log(texte.includes("chat", 15));  // false (pas de "chat" après l'index 15)
```

### Sensibilité à la casse

`includes()` est **sensible à la casse** (majuscules/minuscules) :

```javascript
const texte = "JavaScript";

console.log(texte.includes("javascript")); // false
console.log(texte.includes("JavaScript")); // true
```

**Solution pour ignorer la casse :**

```javascript
const texte = "JavaScript est génial";
const recherche = "javascript";

// Convertir les deux en minuscules
if (texte.toLowerCase().includes(recherche.toLowerCase())) {
    console.log("Trouvé (peu importe la casse)");
}
```

---

## startsWith() - Commence par... 🆕

### Syntaxe

```javascript
string.startsWith(recherche, position)
```

- **`recherche`** : le texte à rechercher au début (obligatoire)
- **`position`** : position de départ (optionnel, par défaut 0)

### Retourne

`true` si la string commence par la sous-chaîne, `false` sinon.

### Utilisation de base

```javascript
const phrase = "JavaScript est génial";

console.log(phrase.startsWith("JavaScript")); // true
console.log(phrase.startsWith("Java"));       // true
console.log(phrase.startsWith("est"));        // false (ne commence pas par "est")
console.log(phrase.startsWith("javascript")); // false (sensible à la casse)
```

### Exemples pratiques

#### Vérifier un protocole URL

```javascript
const url = "https://www.example.com";

if (url.startsWith("https://")) {
    console.log("✅ Connexion sécurisée");
} else if (url.startsWith("http://")) {
    console.log("⚠️ Connexion non sécurisée");
}
```

#### Filtrer des fichiers par extension (avec position)

```javascript
const fichier = "document.pdf";

// Vérifier l'extension (à partir de la fin)
const extension = ".pdf";
const position = fichier.length - extension.length;

if (fichier.startsWith(extension, position)) {
    console.log("C'est un fichier PDF");
}
// Note : endsWith() serait plus approprié ici (voir ci-dessous)
```

#### Validation de numéro de téléphone français

```javascript
const telephone = "+33612345678";

if (telephone.startsWith("+33") || telephone.startsWith("0")) {
    console.log("Numéro français valide");
}
```

#### Système de commandes (chatbot)

```javascript
const commande = "/help";

if (commande.startsWith("/")) {
    console.log("C'est une commande");

    if (commande.startsWith("/help")) {
        console.log("Affichage de l'aide...");
    } else if (commande.startsWith("/start")) {
        console.log("Démarrage...");
    }
}
```

### Paramètre position

Commence la vérification à partir d'une position spécifique :

```javascript
const texte = "Bonjour le monde";

console.log(texte.startsWith("Bonjour"));     // true
console.log(texte.startsWith("le", 8));       // true (commence à l'index 8)
console.log(texte.startsWith("monde", 11));   // true (commence à l'index 11)
```

---

## endsWith() - Se termine par... 🆕

### Syntaxe

```javascript
string.endsWith(recherche, longueur)
```

- **`recherche`** : le texte à rechercher à la fin (obligatoire)
- **`longueur`** : longueur de la string à considérer (optionnel)

### Retourne

`true` si la string se termine par la sous-chaîne, `false` sinon.

### Utilisation de base

```javascript
const phrase = "JavaScript est génial";

console.log(phrase.endsWith("génial"));     // true
console.log(phrase.endsWith("génial !"));   // false (pas de "!")
console.log(phrase.endsWith("JavaScript")); // false (ne se termine pas par ça)
console.log(phrase.endsWith("GÉNIAL"));     // false (sensible à la casse)
```

### Exemples pratiques

#### Vérifier l'extension d'un fichier

```javascript
const fichier = "document.pdf";

if (fichier.endsWith(".pdf")) {
    console.log("C'est un fichier PDF");
} else if (fichier.endsWith(".jpg") || fichier.endsWith(".png")) {
    console.log("C'est une image");
} else if (fichier.endsWith(".txt")) {
    console.log("C'est un fichier texte");
}
```

#### Validation d'adresse email

```javascript
const email = "alice@example.com";

if (email.endsWith("@example.com")) {
    console.log("Email du domaine example.com");
}
```

#### Vérifier la ponctuation

```javascript
const phrase = "Êtes-vous d'accord ?";

if (phrase.endsWith("?")) {
    console.log("C'est une question");
} else if (phrase.endsWith("!")) {
    console.log("C'est une exclamation");
} else if (phrase.endsWith(".")) {
    console.log("C'est une affirmation");
}
```

#### Filtrer des URLs

```javascript
const urls = [
    "https://example.com/page.html",
    "https://example.com/image.jpg",
    "https://example.com/doc.pdf"
];

const pagesHTML = urls.filter(url => url.endsWith(".html"));
console.log(pagesHTML); // ["https://example.com/page.html"]
```

### Paramètre longueur

Considère seulement les premiers N caractères :

```javascript
const texte = "Bonjour le monde";

console.log(texte.endsWith("monde"));        // true
console.log(texte.endsWith("le", 10));       // true (ne considère que "Bonjour le")
console.log(texte.endsWith("Bonjour", 7));   // true (ne considère que "Bonjour")
```

---

## indexOf() - La méthode classique ⚠️

### Syntaxe

```javascript
string.indexOf(recherche, position)
```

- **`recherche`** : le texte à rechercher (obligatoire)
- **`position`** : position de départ (optionnel, par défaut 0)

### Retourne

L'**index** (position) de la première occurrence trouvée, ou **-1** si non trouvé.

### Utilisation de base

```javascript
const phrase = "JavaScript est un langage JavaScript";

console.log(phrase.indexOf("JavaScript")); // 0 (première occurrence)
console.log(phrase.indexOf("est"));        // 11
console.log(phrase.indexOf("Python"));     // -1 (non trouvé)
console.log(phrase.indexOf("javascript")); // -1 (sensible à la casse)
```

### Comprendre les indices

```javascript
const mot = "Bonjour";
//           0123456

console.log(mot.indexOf("B"));   // 0
console.log(mot.indexOf("o"));   // 1 (première occurrence)
console.log(mot.indexOf("j"));   // 3
console.log(mot.indexOf("our")); // 4
```

### Quand utiliser indexOf() ?

**✅ À utiliser** quand vous avez besoin de la **position exacte** :

```javascript
const texte = "Bonjour le monde";
const position = texte.indexOf("monde");

if (position !== -1) {
    console.log(`"monde" trouvé à la position ${position}`);
    // Affiche : "monde" trouvé à la position 11
}
```

**❌ À éviter** pour simplement vérifier la présence (utilisez `includes()`) :

```javascript
// ❌ Moins clair
if (texte.indexOf("monde") !== -1) { /* ... */ }

// ✅ Plus clair
if (texte.includes("monde")) { /* ... */ }
```

### Trouver toutes les occurrences

Avec une boucle, vous pouvez trouver toutes les positions d'une sous-chaîne :

```javascript
const texte = "JavaScript est JavaScript, j'aime JavaScript";
const recherche = "JavaScript";
let position = 0;

while ((position = texte.indexOf(recherche, position)) !== -1) {
    console.log(`Trouvé à la position ${position}`);
    position += recherche.length; // Continuer après cette occurrence
}
```

**Résultat :**
```
Trouvé à la position 0
Trouvé à la position 15
Trouvé à la position 35
```

### Paramètre position de départ

```javascript
const texte = "chat chat chat";

console.log(texte.indexOf("chat"));     // 0 (premier "chat")
console.log(texte.indexOf("chat", 1));  // 5 (deuxième "chat")
console.log(texte.indexOf("chat", 6));  // 10 (troisième "chat")
console.log(texte.indexOf("chat", 15)); // -1 (plus de "chat" après)
```

### Extraction de sous-chaîne avec indexOf()

```javascript
const email = "alice@example.com";
const positionArobase = email.indexOf("@");

if (positionArobase !== -1) {
    const utilisateur = email.substring(0, positionArobase);
    const domaine = email.substring(positionArobase + 1);

    console.log("Utilisateur :", utilisateur); // alice
    console.log("Domaine :", domaine);         // example.com
}
```

---

## Comparaison des méthodes

### Tableau récapitulatif

| Méthode | Retour | Sensible à la casse | Quand l'utiliser |
|---------|--------|---------------------|------------------|
| `includes()` | Boolean | Oui | ✅ Vérifier la présence (moderne) |
| `startsWith()` | Boolean | Oui | ✅ Vérifier le début (moderne) |
| `endsWith()` | Boolean | Oui | ✅ Vérifier la fin (moderne) |
| `indexOf()` | Number | Oui | ⚠️ Besoin de la position exacte |

### Exemple comparatif

```javascript
const phrase = "JavaScript est génial";

// Vérifier la présence
console.log(phrase.includes("est"));      // true (moderne)
console.log(phrase.indexOf("est") !== -1); // true (legacy)

// Vérifier le début
console.log(phrase.startsWith("Java"));   // true (moderne)
console.log(phrase.indexOf("Java") === 0); // true (legacy)

// Vérifier la fin
console.log(phrase.endsWith("génial"));   // true (moderne)
// Pas d'équivalent simple avec indexOf()
```

---

## Gestion de la casse (majuscules/minuscules)

Toutes ces méthodes sont **sensibles à la casse** par défaut.

### Solution : conversion en minuscules

```javascript
const texte = "JavaScript EST génial";
const recherche = "est";

// ❌ Ne trouve pas (casse différente)
console.log(texte.includes(recherche)); // false

// ✅ Conversion en minuscules
console.log(texte.toLowerCase().includes(recherche.toLowerCase())); // true
```

### Fonction utilitaire

```javascript
function includesIgnoreCase(string, recherche) {
    return string.toLowerCase().includes(recherche.toLowerCase());
}

const texte = "JavaScript";
console.log(includesIgnoreCase(texte, "JAVASCRIPT")); // true
console.log(includesIgnoreCase(texte, "javascript")); // true
console.log(includesIgnoreCase(texte, "JavaScript")); // true
```

---

## Cas d'usage avancés

### 1. Recherche multiple

Vérifier si la string contient l'un des mots-clés :

```javascript
const texte = "Apprenez JavaScript et Python";
const motsClés = ["JavaScript", "Java", "Python", "Ruby"];

const motsPresents = motsClés.filter(mot => texte.includes(mot));
console.log(motsPresents); // ["JavaScript", "Python"]

// Vérifier si au moins un mot est présent
const auMoinsUn = motsClés.some(mot => texte.includes(mot));
console.log(auMoinsUn); // true
```

### 2. Validation de format

```javascript
const codePostal = "75001";

// Vérifier le format (5 chiffres, commence par 75 pour Paris)
if (codePostal.startsWith("75") && codePostal.length === 5) {
    console.log("Code postal parisien valide");
}
```

### 3. Filtrage de contenu

```javascript
const commentaires = [
    "Super article !",
    "Contenu spam et inutile",
    "Merci pour cette information",
    "SPAM SPAM SPAM"
];

const motsInterdits = ["spam", "inutile"];

const commentairesValides = commentaires.filter(commentaire => {
    const commentaireLower = commentaire.toLowerCase();
    return !motsInterdits.some(mot => commentaireLower.includes(mot));
});

console.log(commentairesValides);
// ["Super article !", "Merci pour cette information"]
```

### 4. Détection de type de fichier

```javascript
function getTypeDefichier(nomFichier) {
    if (nomFichier.endsWith(".jpg") || nomFichier.endsWith(".png")) {
        return "image";
    } else if (nomFichier.endsWith(".pdf")) {
        return "document";
    } else if (nomFichier.endsWith(".mp4") || nomFichier.endsWith(".avi")) {
        return "vidéo";
    } else {
        return "inconnu";
    }
}

console.log(getTypeDefichier("photo.jpg"));     // "image"
console.log(getTypeDefichier("rapport.pdf"));   // "document"
console.log(getTypeDefichier("film.mp4"));      // "vidéo"
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier que c'est sensible à la casse

```javascript
const texte = "JavaScript";

// ❌ Ne trouve pas
console.log(texte.includes("javascript")); // false

// ✅ Solution
console.log(texte.toLowerCase().includes("javascript")); // true
```

### ❌ Erreur 2 : Utiliser indexOf() pour vérifier la présence

```javascript
// ❌ Moins lisible
if (string.indexOf("mot") !== -1) { }

// ✅ Plus clair et moderne
if (string.includes("mot")) { }
```

### ❌ Erreur 3 : Confondre la valeur de retour

```javascript
const texte = "Bonjour";

// ❌ indexOf() retourne 0 (qui est falsy)
if (texte.indexOf("Bonjour")) {
    // Ce bloc ne s'exécute PAS car 0 est falsy !
}

// ✅ Toujours comparer avec -1
if (texte.indexOf("Bonjour") !== -1) { }

// ✅ Ou utiliser includes()
if (texte.includes("Bonjour")) { }
```

### ❌ Erreur 4 : Oublier les espaces

```javascript
const texte = "Bonjour le monde";

console.log(texte.startsWith("Bonjourle")); // false
console.log(texte.startsWith("Bonjour "));  // true (avec espace)
```

---

## Points clés à retenir

✅ **`includes()`** : méthode moderne pour vérifier la présence (retourne true/false)

✅ **`startsWith()`** : vérifie si une string commence par une sous-chaîne

✅ **`endsWith()`** : vérifie si une string se termine par une sous-chaîne

✅ **`indexOf()`** : retourne la position (-1 si non trouvé), à utiliser uniquement si besoin de la position

✅ Toutes ces méthodes sont **sensibles à la casse**

✅ Pour ignorer la casse : utilisez `.toLowerCase()` sur les deux strings

✅ **Privilégiez les méthodes modernes** (`includes`, `startsWith`, `endsWith`) pour un code plus lisible

---

## Recommandations modernes

### Privilégiez la lisibilité

```javascript
// ✅ Clair et explicite
if (email.includes("@")) { }
if (url.startsWith("https://")) { }
if (fichier.endsWith(".pdf")) { }

// ❌ Moins évident
if (email.indexOf("@") !== -1) { }
if (url.indexOf("https://") === 0) { }
```

### Utilisez indexOf() seulement si nécessaire

```javascript
// ✅ Besoin de la position : indexOf() est approprié
const position = texte.indexOf("mot");
const sousChaine = texte.substring(position);

// ✅ Juste vérifier la présence : includes() est mieux
if (texte.includes("mot")) { }
```

---

## Dans la prochaine section

Dans la section **5.3.5 - Extraction : substring, slice**, nous découvrirons comment extraire des portions de strings pour créer de nouvelles sous-chaînes.

---


⏭️ [Extraction : substring, slice](/05-javascript-moderne-fondamentaux/03-strings-modernes/05-extraction-substring-slice.md)
