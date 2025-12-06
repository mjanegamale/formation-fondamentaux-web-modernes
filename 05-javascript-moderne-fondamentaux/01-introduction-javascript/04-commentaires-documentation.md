🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.1.4 - Commentaires et documentation du code

## Introduction

Les **commentaires** sont des lignes de texte dans votre code qui sont **ignorées par JavaScript** mais **lues par les humains** (vous et les autres développeurs). Ce sont des notes que vous laissez pour expliquer ce que fait votre code.

Écrire de bons commentaires est une compétence essentielle pour :
- 🧠 **Vous-même dans le futur** : Dans 6 mois, vous aurez oublié pourquoi vous avez écrit ce code
- 👥 **Vos collègues** : Ils doivent comprendre votre code
- 📚 **Faciliter la maintenance** : Un code bien commenté est plus facile à modifier
- 🎓 **Apprendre** : Commenter votre code vous aide à clarifier votre pensée

> 💡 **Citation célèbre** : "Le code explique COMMENT, les commentaires expliquent POURQUOI."

## Les deux types de commentaires en JavaScript

JavaScript propose deux syntaxes pour écrire des commentaires :

### 1. Commentaires sur une seule ligne (//)

Utilisez `//` pour commenter une seule ligne :

```javascript
// Ceci est un commentaire sur une ligne

// Déclarer une variable
let nom = 'Alice';

let age = 25;  // L'âge de l'utilisateur

// console.log('Ce code ne s'exécutera pas');
```

**Caractéristiques :**
- Commence par `//`
- Tout ce qui suit `//` sur la même ligne est ignoré
- Peut être placé en fin de ligne de code
- Parfait pour des notes courtes

### 2. Commentaires multi-lignes (/* */)

Utilisez `/* */` pour commenter plusieurs lignes :

```javascript
/*
Ceci est un commentaire
sur plusieurs lignes
Il peut contenir autant de lignes que nécessaire
*/

let prenom = 'Bob';

/*
Cette fonction calcule la moyenne de deux nombres.
Elle prend deux paramètres et retourne leur moyenne.
Auteur: Bob
Date: 2025-12-05
*/
function calculerMoyenne(a, b) {
    return (a + b) / 2;
}
```

**Caractéristiques :**
- Commence par `/*` et se termine par `*/`
- Peut s'étendre sur plusieurs lignes
- Parfait pour des explications longues ou des en-têtes de fichiers

> ⚡ **Important** : Les commentaires multi-lignes ne peuvent pas être imbriqués !

```javascript
/*
Début du commentaire
    /* Ceci ne fonctionne pas ! */
Fin du commentaire
*/
// ❌ Erreur de syntaxe !
```

## Pourquoi écrire des commentaires ?

### 1. Expliquer le "POURQUOI" 🤔

```javascript
// ❌ Mauvais : Le code dit déjà ce qu'il fait
let prix = 100;
prix = prix * 0.8;  // Multiplier le prix par 0.8

// ✅ Bon : Explique POURQUOI
let prix = 100;
prix = prix * 0.8;  // Appliquer une réduction de 20% pour les membres
```

### 2. Clarifier une logique complexe 🧩

```javascript
// Calculer le nombre de jours entre deux dates
// en tenant compte des années bissextiles
let jours = Math.floor((date2 - date1) / (1000 * 60 * 60 * 24));
```

### 3. Documenter des fonctions importantes 📚

```javascript
/**
 * Valide une adresse email
 * @param {string} email - L'email à valider
 * @returns {boolean} - true si valide, false sinon
 */
function validerEmail(email) {
    return email.includes('@') && email.includes('.');
}
```

### 4. Marquer des sections du code 🏷️

```javascript
// ============================================
// CONFIGURATION
// ============================================

const API_URL = 'https://api.example.com';
const TIMEOUT = 5000;

// ============================================
// FONCTIONS UTILITAIRES
// ============================================

function formaterDate(date) {
    // ...
}
```

### 5. Désactiver temporairement du code 🚧

```javascript
function tester() {
    console.log('Test 1');
    // console.log('Test 2 - temporairement désactivé');
    console.log('Test 3');
}
```

> ⚠️ **Attention** : Ne laissez pas de code commenté dans votre code final. Utilisez un système de contrôle de version (Git) pour gérer l'historique.

## Bonnes pratiques pour les commentaires

### ✅ Ce qu'il faut faire

#### 1. Expliquer le contexte et la raison

```javascript
// ✅ Bon
// On arrondit à 2 décimales pour éviter les erreurs de précision
// des nombres flottants (ex: 0.1 + 0.2 = 0.30000000000000004)
let total = Math.round(somme * 100) / 100;
```

#### 2. Documenter les cas particuliers

```javascript
// ✅ Bon
// Attention : cette API retourne null au lieu d'un tableau vide
// quand il n'y a pas de résultats
let resultats = api.rechercher() || [];
```

#### 3. Utiliser un langage clair et simple

```javascript
// ✅ Bon
// Vérifier si l'utilisateur est majeur
if (age >= 18) {
    // ...
}

// ❌ Mauvais : trop technique sans contexte
// Boolean check on numeric value with gte operator
if (age >= 18) {
    // ...
}
```

#### 4. Garder les commentaires à jour

```javascript
// ✅ Bon
// Calculer la TVA à 20%
let tva = montant * 0.20;

// ❌ Mauvais : commentaire obsolète
// Calculer la TVA à 19.6%
let tva = montant * 0.20;  // Le taux a changé mais pas le commentaire !
```

### ❌ Ce qu'il faut éviter

#### 1. Les commentaires évidents

```javascript
// ❌ Inutile : le code est déjà clair
let age = 25;  // Définir age à 25

// ❌ Inutile
i++;  // Incrémenter i

// ❌ Inutile
// Boucle for
for (let i = 0; i < 10; i++) {
    // ...
}
```

#### 2. Commenter du mauvais code au lieu de le réécrire

```javascript
// ❌ Mauvais : le code est confus et nécessite un commentaire
// x est le total, y est la quantité, z est le prix unitaire
let t = x / y * z;

// ✅ Bon : code auto-explicatif, pas besoin de commentaire
let prixMoyen = totalVentes / quantiteVendue * prixUnitaire;
```

#### 3. Les commentaires redondants

```javascript
// ❌ Redondant
function calculerSomme(a, b) {
    // Retourner la somme de a et b
    return a + b;
}

// ✅ Le nom de la fonction est suffisamment clair
function calculerSomme(a, b) {
    return a + b;
}
```

#### 4. Les commentaires périmés ou incorrects

```javascript
// ❌ Dangereux : commentaire faux !
// Cette fonction retourne toujours true
function verifierAge(age) {
    return age >= 18;  // Peut retourner false !
}
```

## JSDoc : Documentation professionnelle 📖

**JSDoc** est un format standard pour documenter les fonctions JavaScript. Il utilise des commentaires spéciaux qui peuvent être lus par des outils pour générer une documentation automatique.

### Syntaxe de base

```javascript
/**
 * Description de la fonction
 * @param {type} nomParametre - Description du paramètre
 * @returns {type} - Description de ce qui est retourné
 */
```

> 💡 **Note** : JSDoc commence par `/**` (avec deux étoiles) et non `/*`

### Exemple simple

```javascript
/**
 * Calcule l'aire d'un rectangle
 * @param {number} largeur - La largeur du rectangle
 * @param {number} hauteur - La hauteur du rectangle
 * @returns {number} L'aire du rectangle
 */
function calculerAire(largeur, hauteur) {
    return largeur * hauteur;
}
```

### Exemples plus avancés

```javascript
/**
 * Recherche un utilisateur par son ID
 * @param {number} id - L'identifiant de l'utilisateur
 * @returns {Object|null} L'objet utilisateur ou null si non trouvé
 * @example
 * const user = rechercherUtilisateur(42);
 * if (user) {
 *     console.log(user.nom);
 * }
 */
function rechercherUtilisateur(id) {
    // ...
}

/**
 * Filtre un tableau selon un critère
 * @param {Array} tableau - Le tableau à filtrer
 * @param {Function} callback - La fonction de filtrage
 * @returns {Array} Le tableau filtré
 */
function filtrer(tableau, callback) {
    // ...
}

/**
 * Configuration de l'application
 * @typedef {Object} Config
 * @property {string} apiUrl - L'URL de l'API
 * @property {number} timeout - Le délai d'expiration en ms
 * @property {boolean} debug - Mode debug activé ou non
 */

/**
 * Initialise l'application avec une configuration
 * @param {Config} config - La configuration de l'application
 */
function initialiser(config) {
    // ...
}
```

### Tags JSDoc courants

| Tag | Usage |
|-----|-------|
| `@param` | Décrit un paramètre de fonction |
| `@returns` | Décrit ce que retourne la fonction |
| `@example` | Donne un exemple d'utilisation |
| `@throws` | Décrit les erreurs possibles |
| `@deprecated` | Marque comme obsolète |
| `@since` | Indique depuis quelle version |
| `@author` | Indique l'auteur |
| `@see` | Fait référence à autre chose |

### Avantages de JSDoc

1. **Auto-complétion dans l'éditeur** 💡

Votre éditeur (VSCode) peut vous suggérer les paramètres et types !

2. **Documentation générée automatiquement** 📚

Des outils peuvent créer une documentation HTML à partir de vos commentaires JSDoc.

3. **Détection d'erreurs** 🐛

Les éditeurs peuvent détecter si vous passez de mauvais types de paramètres.

```javascript
/**
 * @param {number} age
 */
function verifierAge(age) {
    // ...
}

verifierAge('25');  // VSCode peut signaler que c'est un string, pas un number
```

## Commentaires spéciaux pour marquer des tâches 🏷️

### TODO - À faire

```javascript
// TODO: Ajouter la validation de l'email
function inscrireUtilisateur(email) {
    // Code actuel sans validation
}

// TODO: Optimiser cette boucle pour de meilleurs performances
for (let i = 0; i < data.length; i++) {
    // ...
}
```

### FIXME - À corriger

```javascript
// FIXME: Ce calcul ne fonctionne pas avec des nombres négatifs
function calculer(a, b) {
    return a / b;  // Que faire si b = 0 ?
}

// FIXME: La date n'est pas au bon format
let date = '2025/12/05';  // Devrait être ISO 8601
```

### HACK - Solution temporaire

```javascript
// HACK: Solution temporaire en attendant la vraie API
// Utilise des données mockées
const data = {
    users: ['Alice', 'Bob', 'Charlie']
};
```

### NOTE - Information importante

```javascript
// NOTE: Cette fonction modifie le tableau original !
function trierTableau(tableau) {
    return tableau.sort();
}
```

> 💡 **Astuce** : De nombreux éditeurs peuvent rechercher et lister tous vos TODO/FIXME automatiquement !

## Structure d'un fichier JavaScript bien commenté

Voici un exemple de structure professionnelle :

```javascript
/**
 * Gestionnaire de panier d'achat
 *
 * Ce module gère toutes les opérations liées au panier :
 * - Ajout/suppression de produits
 * - Calcul du total
 * - Sauvegarde en localStorage
 *
 * @author Alice Dupont
 * @version 1.2.0
 * @since 2025-01-15
 */

// ============================================
// CONSTANTES
// ============================================

const TVA = 0.20;  // Taux de TVA à 20%
const LIVRAISON_GRATUITE_SEUIL = 50;  // Livraison gratuite au-dessus de 50€

// ============================================
// ÉTAT GLOBAL
// ============================================

let panier = [];

// ============================================
// FONCTIONS PRINCIPALES
// ============================================

/**
 * Ajoute un produit au panier
 * @param {Object} produit - Le produit à ajouter
 * @param {number} produit.id - L'ID du produit
 * @param {string} produit.nom - Le nom du produit
 * @param {number} produit.prix - Le prix du produit
 * @param {number} quantite - La quantité à ajouter
 * @returns {boolean} true si ajouté avec succès
 */
function ajouterAuPanier(produit, quantite = 1) {
    // Vérifier si le produit existe déjà
    const index = panier.findIndex(item => item.id === produit.id);

    if (index !== -1) {
        // Produit déjà dans le panier : augmenter la quantité
        panier[index].quantite += quantite;
    } else {
        // Nouveau produit : l'ajouter au panier
        panier.push({
            ...produit,
            quantite
        });
    }

    // Sauvegarder dans localStorage
    sauvegarderPanier();

    return true;
}

/**
 * Calcule le total du panier TTC
 * @returns {number} Le montant total avec TVA
 */
function calculerTotal() {
    let sousTotal = 0;

    // Calculer le sous-total HT
    for (let item of panier) {
        sousTotal += item.prix * item.quantite;
    }

    // Ajouter la TVA
    let total = sousTotal * (1 + TVA);

    // Arrondir à 2 décimales
    return Math.round(total * 100) / 100;
}

// ============================================
// FONCTIONS UTILITAIRES
// ============================================

/**
 * Sauvegarde le panier dans localStorage
 * @private
 */
function sauvegarderPanier() {
    try {
        localStorage.setItem('panier', JSON.stringify(panier));
    } catch (error) {
        // NOTE: localStorage peut être désactivé ou plein
        console.error('Impossible de sauvegarder le panier:', error);
    }
}

// ============================================
// INITIALISATION
// ============================================

// Charger le panier depuis localStorage au démarrage
(function initialiser() {
    const panierSauvegarde = localStorage.getItem('panier');
    if (panierSauvegarde) {
        try {
            panier = JSON.parse(panierSauvegarde);
        } catch (error) {
            // Le panier sauvegardé est corrompu, on repart de zéro
            console.warn('Panier corrompu, réinitialisation');
            panier = [];
        }
    }
})();
```

## Commentaires et code propre 🧹

### Le meilleur commentaire est l'absence de commentaire

Un code bien écrit devrait être **auto-documenté** autant que possible :

```javascript
// ❌ Nécessite un commentaire
// Vérifier si l'utilisateur a plus de 18 ans et moins de 65 ans
if (u.a > 18 && u.a < 65) {
    // ...
}

// ✅ Auto-explicatif, pas besoin de commentaire
const AGE_MINIMUM = 18;
const AGE_MAXIMUM = 65;

if (utilisateur.age > AGE_MINIMUM && utilisateur.age < AGE_MAXIMUM) {
    // ...
}

// ✅ Encore mieux : fonction avec nom descriptif
function estAgeEligible(age) {
    return age > 18 && age < 65;
}

if (estAgeEligible(utilisateur.age)) {
    // ...
}
```

### Principe général

1. **Noms de variables/fonctions clairs** > Commentaires explicatifs
2. **Code simple et lisible** > Code complexe avec commentaires
3. **Fonctions courtes et ciblées** > Longues fonctions commentées

```javascript
// ❌ Mauvais code qui nécessite beaucoup de commentaires
function p(d) {
    // Calculer le nombre de jours
    let j = Math.floor(d / 86400000);
    // Calculer les heures restantes
    let h = Math.floor((d % 86400000) / 3600000);
    // Calculer les minutes restantes
    let m = Math.floor((d % 3600000) / 60000);
    // Retourner le résultat formaté
    return j + 'j ' + h + 'h ' + m + 'm';
}

// ✅ Bon code qui n'a presque pas besoin de commentaires
function formaterDuree(millisecondes) {
    const MILLISECONDES_PAR_JOUR = 86400000;
    const MILLISECONDES_PAR_HEURE = 3600000;
    const MILLISECONDES_PAR_MINUTE = 60000;

    const jours = Math.floor(millisecondes / MILLISECONDES_PAR_JOUR);
    const heures = Math.floor((millisecondes % MILLISECONDES_PAR_JOUR) / MILLISECONDES_PAR_HEURE);
    const minutes = Math.floor((millisecondes % MILLISECONDES_PAR_HEURE) / MILLISECONDES_PAR_MINUTE);

    return `${jours}j ${heures}h ${minutes}m`;
}
```

## Commentaires dans différents contextes

### 1. En apprentissage 🎓

Quand vous apprenez, commentez **abondamment** :

```javascript
// Je déclare une variable pour stocker le nom
let nom = 'Alice';

// J'utilise une boucle pour parcourir le tableau
for (let i = 0; i < tableau.length; i++) {
    // À chaque itération, j'affiche l'élément
    console.log(tableau[i]);
}
```

C'est normal et même recommandé ! Cela vous aide à comprendre.

### 2. En développement professionnel 💼

Commentez **seulement ce qui n'est pas évident** :

```javascript
// Configuration de l'API externe
const API_CONFIG = {
    url: 'https://api.example.com',
    // Timeout augmenté à cause de la latence du serveur de production
    timeout: 10000,
    retries: 3
};

function traiterCommande(commande) {
    // Note importante : cette API peut mettre jusqu'à 30 secondes à répondre
    // en période de forte affluence (soldes, Black Friday)
    return fetch(API_CONFIG.url, {
        // ...
    });
}
```

## Les commentaires et le travail en équipe 👥

### Conventions d'équipe

De nombreuses équipes définissent des conventions pour les commentaires :

```javascript
// Convention exemple :
// TODO(alice): Implémenter la validation
// FIXME(bob): Corriger le bug #1234
// HACK(charlie): Solution temporaire, sera refactorisé dans la v2.0
```

### Code reviews et commentaires

Les commentaires aident lors des revues de code :

```javascript
/**
 * IMPORTANT: Ne pas modifier cette fonction sans consulter l'équipe backend
 * Elle doit rester synchronisée avec l'API v2
 */
function synchroniserDonnees() {
    // ...
}
```

## En résumé

### Les 3 règles d'or des commentaires 🏆

1. **Expliquez le POURQUOI, pas le QUOI**
   - Le code montre ce qu'il fait
   - Les commentaires expliquent pourquoi il le fait ainsi

2. **Écrivez du code auto-documenté d'abord**
   - Noms de variables clairs
   - Fonctions courtes et ciblées
   - Logique simple

3. **Commentez ce qui n'est pas évident**
   - Algorithmes complexes
   - Décisions business
   - Cas particuliers
   - Limitations techniques

### Checklist des commentaires ✅

- [ ] Mes commentaires expliquent le "pourquoi" plutôt que le "quoi"
- [ ] Je n'ai pas de commentaires évidents ou redondants
- [ ] Mes fonctions importantes ont une documentation JSDoc
- [ ] Mes commentaires sont à jour avec le code
- [ ] J'ai marqué mes TODO/FIXME pour ne pas les oublier
- [ ] Mon code est lisible même sans les commentaires

> 🎯 **À retenir** : Un bon code a besoin de peu de commentaires. Un excellent code se lit comme un livre et les commentaires ne font qu'enrichir la compréhension.

## Prochaine étape

Maintenant que vous savez documenter votre code, nous allons découvrir le **mode strict et les modules ES6**, deux fonctionnalités essentielles du JavaScript moderne !

---


💡 **Citation bonus** : "Les programmes doivent être écrits pour que les gens les lisent, et seulement accessoirement pour que les machines les exécutent." - Harold Abelson

⏭️ [Strict mode et modules ES6](/05-javascript-moderne-fondamentaux/01-introduction-javascript/05-strict-mode-modules.md)
