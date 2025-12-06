🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.12.2 Structure try...catch...finally

## Introduction

Maintenant que vous connaissez les différents types d'erreurs, apprenons à les **gérer** pour que votre programme ne s'arrête pas brutalement. La structure `try...catch...finally` est l'outil principal pour intercepter et gérer les erreurs en JavaScript.

> 💡 **Analogie** : Imaginez que vous apprenez à faire du vélo. Le bloc `try` c'est votre tentative de rouler, le bloc `catch` c'est le casque qui vous protège si vous tombez, et `finally` c'est le fait de ranger le vélo après, que vous soyez tombé ou non.

---

## Pourquoi gérer les erreurs ?

Sans gestion d'erreur, votre programme s'arrête complètement dès qu'une erreur survient :

```javascript
// ❌ Sans gestion d'erreur
console.log("Début du programme");
const utilisateur = null;
console.log(utilisateur.nom);  // ❌ ERREUR ! Le programme s'arrête ici
console.log("Cette ligne ne s'exécutera jamais");  // 😢
```

Avec la gestion d'erreur, votre programme peut continuer :

```javascript
// ✅ Avec gestion d'erreur
console.log("Début du programme");
const utilisateur = null;

try {
    console.log(utilisateur.nom);
} catch (erreur) {
    console.log("Une erreur s'est produite, mais le programme continue");
}

console.log("Cette ligne s'exécute normalement");  // ✅
```

---

## La structure de base : try...catch

### Syntaxe

```javascript
try {
    // Code susceptible de générer une erreur
} catch (erreur) {
    // Code à exécuter si une erreur se produit
}
```

### Le bloc try

Le bloc `try` contient le code que vous voulez **tester**. Si une erreur se produit dans ce bloc, JavaScript arrête immédiatement l'exécution du `try` et passe au bloc `catch`.

```javascript
try {
    console.log("Ligne 1 : OK");
    console.log("Ligne 2 : OK");
    const x = y;  // ❌ Erreur ici (y n'existe pas)
    console.log("Ligne 4 : Ne s'exécutera pas");
} catch (erreur) {
    console.log("Une erreur est survenue");
}
```

**Résultat :**
```
Ligne 1 : OK
Ligne 2 : OK
Une erreur est survenue
```

### Le bloc catch

Le bloc `catch` s'exécute **seulement si** une erreur se produit dans le `try`. Il reçoit automatiquement l'objet erreur en paramètre.

```javascript
try {
    const resultat = 10 / 0;  // Pas d'erreur en JavaScript (résultat = Infinity)
    console.log("Pas d'erreur");
} catch (erreur) {
    console.log("Ce code ne s'exécutera pas");  // Ne s'affichera pas
}
```

---

## L'objet erreur dans catch

L'objet erreur contient des informations utiles :

```javascript
try {
    const utilisateur = null;
    console.log(utilisateur.nom);
} catch (erreur) {
    console.log("Type d'erreur :", erreur.name);           // "TypeError"
    console.log("Message :", erreur.message);              // "Cannot read property 'nom' of null"
    console.log("Pile d'appels :", erreur.stack);         // Informations détaillées
}
```

### Propriétés principales de l'objet erreur

| Propriété | Description | Exemple |
|-----------|-------------|---------|
| `name` | Type d'erreur | "TypeError", "ReferenceError" |
| `message` | Description de l'erreur | "Cannot read property 'nom' of null" |
| `stack` | Pile d'appels complète | Informations de débogage |

---

## Exemples pratiques avec try...catch

### Exemple 1 : Validation de données utilisateur

```javascript
function calculerAge(anneeNaissance) {
    try {
        if (typeof anneeNaissance !== 'number') {
            throw new TypeError("L'année doit être un nombre");
        }

        const anneeActuelle = new Date().getFullYear();
        const age = anneeActuelle - anneeNaissance;

        return age;
    } catch (erreur) {
        console.error("Erreur lors du calcul :", erreur.message);
        return null;  // Valeur par défaut en cas d'erreur
    }
}

console.log(calculerAge(1990));      // ✅ 34 (ou l'âge actuel)
console.log(calculerAge("1990"));    // ❌ null + message d'erreur
```

### Exemple 2 : Parsing JSON

```javascript
function chargerConfiguration(jsonString) {
    try {
        const config = JSON.parse(jsonString);
        console.log("Configuration chargée avec succès");
        return config;
    } catch (erreur) {
        console.error("JSON invalide :", erreur.message);
        return { /* configuration par défaut */ };
    }
}

// ✅ JSON valide
const config1 = chargerConfiguration('{"theme": "dark"}');

// ❌ JSON invalide
const config2 = chargerConfiguration('{"theme": "dark"');  // Guillemet manquant
```

### Exemple 3 : Accès à des propriétés d'objets

```javascript
function afficherNomComplet(personne) {
    try {
        const nomComplet = personne.prenom + " " + personne.nom;
        console.log("Nom complet :", nomComplet);
    } catch (erreur) {
        console.log("Impossible d'afficher le nom :", erreur.message);
        console.log("Utilisation d'un nom par défaut : Utilisateur Anonyme");
    }
}

afficherNomComplet({ prenom: "Alice", nom: "Dupont" });  // ✅ OK
afficherNomComplet(null);                                 // ❌ Géré par catch
```

---

## Le bloc finally

Le bloc `finally` s'exécute **TOUJOURS**, qu'il y ait eu une erreur ou non. C'est utile pour le code de "nettoyage".

### Syntaxe complète

```javascript
try {
    // Code à tester
} catch (erreur) {
    // Gestion de l'erreur
} finally {
    // Code qui s'exécute TOUJOURS
}
```

### Exemple simple

```javascript
function exemple() {
    try {
        console.log("1. Dans try");
        return "Valeur de retour";
    } catch (erreur) {
        console.log("2. Dans catch");
    } finally {
        console.log("3. Dans finally - S'exécute TOUJOURS");
    }
}

exemple();
```

**Résultat :**
```
1. Dans try
3. Dans finally - S'exécute TOUJOURS
```

> ⚠️ **Important** : Le bloc `finally` s'exécute même si vous utilisez `return` dans `try` ou `catch` !

---

## Cas d'usage pratiques du finally

### 1. Fermeture de connexions

```javascript
function lireFichier(nomFichier) {
    let fichier = null;

    try {
        fichier = ouvrirFichier(nomFichier);  // Ouvre le fichier
        const contenu = fichier.lire();
        return contenu;
    } catch (erreur) {
        console.error("Erreur de lecture :", erreur.message);
        return null;
    } finally {
        if (fichier) {
            fichier.fermer();  // ✅ Ferme le fichier dans tous les cas
        }
        console.log("Nettoyage effectué");
    }
}
```

### 2. Affichage de loader/spinner

```javascript
function chargerDonnees() {
    afficherLoader();  // Affiche un indicateur de chargement

    try {
        const donnees = recupererDonneesServeur();
        afficherDonnees(donnees);
    } catch (erreur) {
        afficherMessageErreur("Impossible de charger les données");
    } finally {
        cacherLoader();  // ✅ Cache le loader dans tous les cas
    }
}
```

### 3. Réinitialisation d'état

```javascript
function traiterFormulaire() {
    const bouton = document.querySelector('#submitBtn');
    bouton.disabled = true;  // Désactive le bouton

    try {
        validerFormulaire();
        envoyerDonnees();
        afficherSucces();
    } catch (erreur) {
        afficherErreur(erreur.message);
    } finally {
        bouton.disabled = false;  // ✅ Réactive le bouton dans tous les cas
    }
}
```

---

## Combinaisons possibles

### try...catch (sans finally)

```javascript
try {
    // Code à tester
} catch (erreur) {
    // Gestion de l'erreur
}
// Le plus courant
```

### try...finally (sans catch)

```javascript
try {
    // Code à tester
} finally {
    // Nettoyage
}
// L'erreur se propagera après le finally
```

### try...catch...finally (complet)

```javascript
try {
    // Code à tester
} catch (erreur) {
    // Gestion de l'erreur
} finally {
    // Nettoyage
}
// La forme complète
```

---

## Ordre d'exécution

Voyons dans quel ordre les blocs s'exécutent :

```javascript
console.log("1. Avant try");

try {
    console.log("2. Dans try");
    throw new Error("Erreur volontaire");
    console.log("3. Après l'erreur - NE S'EXÉCUTE PAS");
} catch (erreur) {
    console.log("4. Dans catch");
} finally {
    console.log("5. Dans finally");
}

console.log("6. Après tout");
```

**Résultat :**
```
1. Avant try
2. Dans try
4. Dans catch
5. Dans finally
6. Après tout
```

---

## Attraper des erreurs spécifiques

Vous pouvez vérifier le type d'erreur dans le catch :

```javascript
try {
    // Code susceptible de générer différents types d'erreurs
} catch (erreur) {
    if (erreur instanceof TypeError) {
        console.log("Erreur de type");
    } else if (erreur instanceof ReferenceError) {
        console.log("Erreur de référence");
    } else {
        console.log("Autre type d'erreur");
    }
}
```

### Exemple pratique

```javascript
function diviser(a, b) {
    try {
        if (typeof a !== 'number' || typeof b !== 'number') {
            throw new TypeError("Les paramètres doivent être des nombres");
        }

        if (b === 0) {
            throw new Error("Division par zéro impossible");
        }

        return a / b;
    } catch (erreur) {
        if (erreur instanceof TypeError) {
            console.error("Erreur de type :", erreur.message);
            return NaN;
        } else {
            console.error("Erreur :", erreur.message);
            return Infinity;
        }
    }
}

console.log(diviser(10, 2));      // ✅ 5
console.log(diviser(10, "2"));    // ❌ NaN (TypeError)
console.log(diviser(10, 0));      // ❌ Infinity (Error)
```

---

## Try...catch imbriqués

Vous pouvez imbriquer des structures try...catch :

```javascript
try {
    console.log("Try externe");

    try {
        console.log("Try interne");
        throw new Error("Erreur interne");
    } catch (erreur) {
        console.log("Catch interne :", erreur.message);
        throw erreur;  // Relance l'erreur vers le catch externe
    }

} catch (erreur) {
    console.log("Catch externe :", erreur.message);
}
```

---

## Bonnes pratiques

### ✅ À faire

1. **Être spécifique dans les messages d'erreur**
```javascript
catch (erreur) {
    console.error("Erreur lors du chargement du profil utilisateur :", erreur.message);
}
```

2. **Utiliser finally pour le nettoyage**
```javascript
try {
    ouvrirConnexion();
    traiterDonnees();
} catch (erreur) {
    gererErreur(erreur);
} finally {
    fermerConnexion();  // ✅ Toujours exécuté
}
```

3. **Ne capturer que ce que vous pouvez gérer**
```javascript
try {
    const donnees = JSON.parse(jsonString);
    // Je sais gérer cette erreur
} catch (erreur) {
    afficherMessageUtilisateur("Format de données invalide");
}
```

### ❌ À éviter

1. **Try...catch vides**
```javascript
// ❌ Mauvais - cache les erreurs silencieusement
try {
    codeRisque();
} catch (erreur) {
    // Ne rien faire
}
```

2. **Try...catch trop larges**
```javascript
// ❌ Mauvais - tout le code est dans le try
try {
    const a = 1;
    const b = 2;
    const c = 3;
    // 100 lignes de code...
} catch (erreur) {
    console.log("Une erreur quelque part...");
}
```

3. **Capturer et relancer sans raison**
```javascript
// ❌ Inutile
try {
    faireQuelqueChose();
} catch (erreur) {
    throw erreur;  // Pourquoi capturer si on relance ?
}
```

---

## Quand utiliser try...catch ?

### ✅ Situations appropriées

- Parsing de JSON/XML
- Appels à des APIs externes
- Manipulation de données utilisateur
- Accès à des propriétés d'objets incertains
- Opérations de fichiers (Node.js)

### ❌ Situations inappropriées

- Contrôle de flux normal du programme
- Validation simple (utilisez des conditions `if`)
- Erreurs que vous pouvez éviter facilement

**Exemple - Préférez les conditions :**

```javascript
// ❌ Utiliser try...catch pour de la logique normale
try {
    const age = personne.age;
} catch (erreur) {
    const age = 0;
}

// ✅ Mieux : utiliser une condition
const age = personne && personne.age ? personne.age : 0;

// ✅ Encore mieux (ES2020+)
const age = personne?.age ?? 0;
```

---

## Récapitulatif

| Bloc | S'exécute quand ? | Usage principal |
|------|-------------------|-----------------|
| **try** | Toujours | Code à tester |
| **catch** | Si erreur dans try | Gérer l'erreur |
| **finally** | Toujours | Nettoyage/fermeture |

---

## Points clés à retenir

1. **try...catch permet de gérer les erreurs** sans arrêter le programme

2. **Le bloc catch reçoit l'objet erreur** avec des informations utiles (name, message, stack)

3. **finally s'exécute TOUJOURS**, même avec return ou throw

4. **Utilisez try...catch judicieusement** : pas pour tout, seulement pour les erreurs imprévisibles

5. **Soyez spécifique** dans vos messages d'erreur pour faciliter le débogage

6. **N'ignorez jamais les erreurs** : loggez-les au minimum

---

## Prochaines étapes

Dans les prochaines sections, vous apprendrez :
- Comment créer vos propres types d'erreurs personnalisées
- Comment utiliser `throw` pour générer des erreurs volontairement
- Les techniques de débogage avancées avec les DevTools

> 💡 **Conseil** : La gestion d'erreurs est comme une ceinture de sécurité : vous espérez ne jamais en avoir besoin, mais vous êtes content de l'avoir quand c'est nécessaire !

⏭️ [L'objet Error](/05-javascript-moderne-fondamentaux/12-gestion-erreurs/03-objet-error.md)
