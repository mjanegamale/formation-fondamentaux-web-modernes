🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.13.1 - Closures (fermetures)

## Introduction

Les **closures** (ou fermetures en français) sont l'un des concepts les plus puissants de JavaScript, mais aussi l'un des plus difficiles à comprendre au début. Ne vous inquiétez pas si ce concept ne vous semble pas évident immédiatement : c'est normal ! Avec de la pratique, les closures deviendront une seconde nature.

> 💡 **En résumé** : Une closure, c'est quand une fonction "se souvient" des variables de son environnement d'origine, même après que cet environnement n'existe plus.

---

## Qu'est-ce qu'une Closure ?

### Définition simple

Une **closure** est une fonction qui a accès aux variables de sa fonction parente, même après que la fonction parente ait terminé son exécution.

### Analogie : La boîte à souvenirs

Imaginez que vous écrivez une lettre dans une boîte, puis vous fermez cette boîte et vous la donnez à quelqu'un. Cette personne peut ouvrir la boîte plus tard et lire la lettre, même si vous n'êtes plus là.

C'est exactement ce que fait une closure : elle "emballe" des variables dans une fonction et les garde accessibles, même après que le contexte initial soit terminé.

---

## Comprendre les bases : La portée lexicale

Avant de plonger dans les closures, revoyons rapidement la **portée lexicale** (lexical scope) :

```javascript
function fonctionExterne() {
  const message = "Bonjour depuis l'extérieur";

  function fonctionInterne() {
    console.log(message); // ✅ Peut accéder à "message"
  }

  fonctionInterne();
}

fonctionExterne();
// Affiche : "Bonjour depuis l'extérieur"
```

**Ce qui se passe ici :**
- `fonctionInterne` est définie à l'intérieur de `fonctionExterne`
- Elle peut accéder à la variable `message` de sa fonction parente
- C'est la portée lexicale : une fonction a accès aux variables de son parent

---

## Le vrai pouvoir des Closures

Maintenant, voici où ça devient intéressant : **la fonction interne continue d'avoir accès aux variables même après que la fonction externe soit terminée** !

### Exemple 1 : Une closure basique

```javascript
function creerSalutation(prenom) {
  // Cette variable sera "mémorisée" par la closure
  const message = `Bonjour ${prenom} !`;

  // On retourne une fonction
  return function() {
    console.log(message);
  };
}

// On crée une fonction de salutation pour Alice
const saluerAlice = creerSalutation("Alice");

// On l'exécute plus tard
saluerAlice(); // Affiche : "Bonjour Alice !"
```

**Ce qui se passe :**
1. `creerSalutation("Alice")` s'exécute et crée `message`
2. Une nouvelle fonction est retournée et stockée dans `saluerAlice`
3. `creerSalutation` a terminé son exécution
4. **Mais** quand on appelle `saluerAlice()`, elle a toujours accès à `message` !

C'est ça, une closure ! 🎉

---

## Exemples pratiques

### Exemple 2 : Compteur privé

Un des usages les plus courants des closures : créer des variables "privées".

```javascript
function creerCompteur() {
  let compteur = 0; // Variable "privée"

  return {
    incrementer: function() {
      compteur++;
      console.log(compteur);
    },
    decrementer: function() {
      compteur--;
      console.log(compteur);
    },
    obtenir: function() {
      return compteur;
    }
  };
}

const monCompteur = creerCompteur();

monCompteur.incrementer(); // 1
monCompteur.incrementer(); // 2
monCompteur.incrementer(); // 3
monCompteur.decrementer(); // 2

console.log(monCompteur.obtenir()); // 2

// ❌ On ne peut PAS accéder directement à compteur
console.log(monCompteur.compteur); // undefined
```

**Avantages :**
- La variable `compteur` est protégée
- On ne peut la modifier qu'à travers les méthodes fournies
- C'est le principe d'**encapsulation**

---

### Exemple 3 : Fonctions personnalisées

```javascript
function creerMultiplicateur(facteur) {
  return function(nombre) {
    return nombre * facteur;
  };
}

const doubler = creerMultiplicateur(2);
const tripler = creerMultiplicateur(3);

console.log(doubler(5));  // 10 (5 × 2)
console.log(tripler(5));  // 15 (5 × 3)
console.log(doubler(10)); // 20 (10 × 2)
```

**Explication :**
- Chaque appel à `creerMultiplicateur` crée une nouvelle closure
- Chaque closure "se souvient" de son propre `facteur`
- `doubler` se souvient que `facteur = 2`
- `tripler` se souvient que `facteur = 3`

---

### Exemple 4 : Gestionnaire d'événements

Les closures sont très utiles avec les événements :

```javascript
function attacherEvenement(elementId) {
  const compteur = { clics: 0 };

  document.getElementById(elementId).addEventListener('click', function() {
    compteur.clics++;
    console.log(`Cliqué ${compteur.clics} fois`);
  });
}

attacherEvenement('monBouton');
// Chaque clic incrémente le compteur grâce à la closure
```

---

## Piège classique : Closures dans une boucle

⚠️ **Attention** : Voici un piège courant avec les closures et les boucles.

### ❌ Code problématique (avec `var`)

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}

// Affiche : 4, 4, 4 (et non 1, 2, 3 !)
```

**Pourquoi ?** Parce que `var` a une portée de fonction, pas de bloc. Toutes les closures partagent la même variable `i`.

### ✅ Solution 1 : Utiliser `let`

```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}

// Affiche : 1, 2, 3 ✅
```

`let` a une portée de bloc, donc chaque itération crée une nouvelle variable.

### ✅ Solution 2 : Créer une closure explicite

```javascript
for (var i = 1; i <= 3; i++) {
  (function(index) {
    setTimeout(function() {
      console.log(index);
    }, 1000);
  })(i);
}

// Affiche : 1, 2, 3 ✅
```

On crée une fonction immédiatement exécutée (IIFE) qui capture la valeur de `i` à chaque itération.

---

## Cas d'usage pratiques

### 1. **Création de fonctions utilitaires**

```javascript
function creerValidateur(min, max) {
  return function(valeur) {
    return valeur >= min && valeur <= max;
  };
}

const validerAge = creerValidateur(18, 99);
const validerNote = creerValidateur(0, 20);

console.log(validerAge(25));  // true
console.log(validerAge(15));  // false
console.log(validerNote(15)); // true
```

### 2. **Mémorisation (memoization)**

```javascript
function memoize(fn) {
  const cache = {};

  return function(arg) {
    if (cache[arg]) {
      console.log('Résultat en cache');
      return cache[arg];
    }

    console.log('Calcul...');
    const resultat = fn(arg);
    cache[arg] = resultat;
    return resultat;
  };
}

function calculLourd(n) {
  return n * n;
}

const calculMemoize = memoize(calculLourd);

console.log(calculMemoize(5)); // Calcul... 25
console.log(calculMemoize(5)); // Résultat en cache 25
```

### 3. **Gestion d'état dans des applications**

```javascript
function creerGestionnaireUtilisateur() {
  let utilisateur = null;

  return {
    connexion: function(nom) {
      utilisateur = { nom, connecte: true };
      console.log(`${nom} connecté`);
    },

    deconnexion: function() {
      if (utilisateur) {
        console.log(`${utilisateur.nom} déconnecté`);
        utilisateur = null;
      }
    },

    obtenirUtilisateur: function() {
      return utilisateur;
    }
  };
}

const auth = creerGestionnaireUtilisateur();
auth.connexion('Alice');
console.log(auth.obtenirUtilisateur()); // { nom: 'Alice', connecte: true }
auth.deconnexion();
```

---

## Closures et Arrow Functions

Les closures fonctionnent exactement de la même manière avec les arrow functions :

```javascript
const creerSalutation = (prenom) => {
  const message = `Bonjour ${prenom}`;

  return () => console.log(message);
};

const saluerBob = creerSalutation("Bob");
saluerBob(); // "Bonjour Bob"
```

---

## Points clés à retenir

✅ **Une closure permet à une fonction de "se souvenir" de son environnement d'origine**

✅ **Les closures sont créées automatiquement chaque fois qu'une fonction est définie**

✅ **Elles permettent de créer des données privées (encapsulation)**

✅ **Très utiles pour :**
   - Créer des fonctions configurables
   - Gérer l'état de manière isolée
   - Créer des gestionnaires d'événements
   - Implémenter des patterns de conception

⚠️ **Attention aux boucles avec `var`** : préférez `let` ou créez une closure explicite

⚠️ **Les closures consomment de la mémoire** : les variables capturées restent en mémoire

---

## Visualiser une Closure

Voici une représentation mentale d'une closure :

```javascript
function externe() {
  const data = "données privées";

  return function interne() {
    console.log(data); // Closure : accès à "data"
  };
}

const maClosure = externe();

// À ce stade :
// - externe() a terminé
// - Mais la fonction interne() a toujours accès à "data"
// - "data" est "emprisonnée" dans la closure

maClosure(); // Affiche : "données privées"
```

---

## Conclusion

Les closures sont un concept fondamental en JavaScript. Même si elles peuvent sembler complexes au début, elles sont en réalité utilisées naturellement dans beaucoup de code JavaScript moderne.

**N'oubliez pas :**
- Une closure = une fonction + son environnement lexical
- Elles se créent automatiquement
- Elles sont puissantes pour créer des abstractions et gérer l'état

Avec la pratique, vous commencerez à reconnaître et à utiliser les closures sans même y penser ! 🚀

---

## Pour aller plus loin

Les closures sont la base de nombreux concepts avancés en JavaScript :
- Programmation fonctionnelle
- Décorateurs
- Currying
- Modules pattern
- Factory functions

Vous rencontrerez les closures partout dans le code JavaScript moderne, notamment dans les frameworks comme React (hooks), Vue.js, et bien d'autres !

⏭️ [IIFE vs Modules ES6](/05-javascript-moderne-fondamentaux/13-concepts-avances/02-iife-vs-modules.md)
