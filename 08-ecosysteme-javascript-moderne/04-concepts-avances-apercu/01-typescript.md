🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.4.1 TypeScript : JavaScript typé 🆕

## Introduction

**TypeScript** est un langage de programmation développé par Microsoft qui se base sur JavaScript en y ajoutant un système de **typage statique**. On peut le voir comme une version améliorée de JavaScript qui aide à détecter les erreurs avant même d'exécuter le code.

> 💡 **En résumé** : TypeScript = JavaScript + Types

TypeScript n'est pas un langage complètement différent : tout code JavaScript valide est aussi du code TypeScript valide. C'est un **sur-ensemble** (superset) de JavaScript.

---

## Pourquoi TypeScript existe-t-il ?

### Le problème avec JavaScript

JavaScript est un langage à **typage dynamique**, ce qui signifie que le type d'une variable peut changer pendant l'exécution :

```javascript
// JavaScript classique
let age = 25;        // age est un nombre
age = "vingt-cinq";  // maintenant age est une chaîne - pas d'erreur !
age = true;          // maintenant age est un booléen - toujours pas d'erreur !
```

Cette flexibilité peut causer des bugs difficiles à détecter :

```javascript
function calculerRemise(prix, pourcentage) {
  return prix * pourcentage / 100;
}

calculerRemise(100, "20");  // Fonctionne mais comportement inattendu
calculerRemise("100", 20);  // Fonctionne aussi...
calculerRemise(100);        // undefined ! Mais pas d'erreur
```

Ces erreurs ne sont découvertes qu'à l'exécution, parfois en production avec de vrais utilisateurs !

### La solution TypeScript

TypeScript détecte ces problèmes **avant l'exécution**, pendant que vous codez :

```typescript
function calculerRemise(prix: number, pourcentage: number): number {
  return prix * pourcentage / 100;
}

calculerRemise(100, "20");  // ❌ Erreur : "20" n'est pas un nombre
calculerRemise("100", 20);  // ❌ Erreur : "100" n'est pas un nombre
calculerRemise(100);        // ❌ Erreur : il manque le deuxième paramètre
```

---

## Les avantages de TypeScript

### 1. Détection précoce des erreurs

Les erreurs sont trouvées **pendant le développement**, pas en production :

```typescript
let utilisateur = {
  nom: "Alice",
  age: 30
};

console.log(utilisateur.prenom);  // ❌ Erreur : 'prenom' n'existe pas
```

### 2. Auto-complétion améliorée

Votre éditeur connaît les types et peut vous proposer des suggestions pertinentes :

```typescript
let message: string = "Bonjour";
message.  // Votre éditeur affiche : toUpperCase, toLowerCase, split, etc.
```

### 3. Documentation intégrée

Les types servent de documentation :

```typescript
// On comprend immédiatement ce que la fonction attend et retourne
function creerUtilisateur(nom: string, age: number, email: string): User {
  // ...
}
```

### 4. Refactoring plus sûr

Quand vous renommez une propriété, TypeScript trouve tous les endroits à modifier :

```typescript
interface Produit {
  nom: string;
  prix: number;
}

// Si vous renommez 'prix' en 'prixTTC', TypeScript vous indique
// tous les endroits où vous devez mettre à jour le code
```

---

## Les bases du typage en TypeScript

### Types primitifs

```typescript
let prenom: string = "Marie";
let age: number = 25;
let estActif: boolean = true;
let rien: null = null;
let pasDefini: undefined = undefined;
```

### Tableaux

```typescript
let nombres: number[] = [1, 2, 3, 4, 5];
let prenoms: string[] = ["Alice", "Bob", "Charlie"];

// Syntaxe alternative (moins courante)
let scores: Array<number> = [95, 87, 92];
```

### Objets avec interfaces

```typescript
// Définition de la structure d'un objet
interface Utilisateur {
  nom: string;
  age: number;
  email: string;
  estAdmin?: boolean;  // Le ? signifie "optionnel"
}

let user: Utilisateur = {
  nom: "Alice",
  age: 30,
  email: "alice@example.com"
  // estAdmin est optionnel, on peut l'omettre
};
```

### Fonctions

```typescript
// Type des paramètres et du retour
function additionner(a: number, b: number): number {
  return a + b;
}

// Fonction qui ne retourne rien
function afficherMessage(message: string): void {
  console.log(message);
}

// Arrow function
const multiplier = (a: number, b: number): number => a * b;
```

### Union de types

Une variable peut accepter plusieurs types :

```typescript
let identifiant: string | number;

identifiant = "ABC123";  // ✅ OK
identifiant = 456;       // ✅ OK aussi
identifiant = true;      // ❌ Erreur
```

### Type `any` (à éviter)

Le type `any` désactive les vérifications TypeScript :

```typescript
let nImporteQuoi: any = "texte";
nImporteQuoi = 123;      // ✅ OK
nImporteQuoi = true;     // ✅ OK
nImporteQuoi = [];       // ✅ OK

// ⚠️ À éviter : on perd tous les bénéfices de TypeScript !
```

---

## Comment TypeScript fonctionne-t-il ?

### Le processus de compilation

TypeScript ne peut pas être exécuté directement par les navigateurs. Il doit être **transpilé** (converti) en JavaScript :

```
Code TypeScript (.ts)  →  [Transpilation]  →  Code JavaScript (.js)
```

**Exemple :**

TypeScript (fichier `app.ts`) :
```typescript
function saluer(nom: string): string {
  return `Bonjour ${nom}`;
}

const message: string = saluer("Alice");
console.log(message);
```

JavaScript généré (fichier `app.js`) :
```javascript
function saluer(nom) {
  return `Bonjour ${nom}`;
}

const message = saluer("Alice");
console.log(message);
```

Les types disparaissent dans le JavaScript final : ils ne servent qu'au développement.

### Installation et utilisation basique

Pour utiliser TypeScript, il faut l'installer via npm :

```bash
# Installation globale
npm install -g typescript

# Compilation d'un fichier
tsc monFichier.ts
```

---

## TypeScript dans le développement moderne

### Adoption massive

TypeScript est devenu extrêmement populaire :

- **Frameworks** : Angular utilise TypeScript par défaut, React et Vue.js le supportent parfaitement
- **Entreprises** : Microsoft, Google, Airbnb, Slack utilisent TypeScript
- **Projets open-source** : De plus en plus de bibliothèques sont écrites en TypeScript

### TypeScript et VS Code

Visual Studio Code offre un excellent support de TypeScript :

- Auto-complétion intelligente
- Détection d'erreurs en temps réel
- Refactoring assisté
- Documentation au survol

---

## Quand utiliser TypeScript ?

### ✅ TypeScript est recommandé pour :

- **Projets de moyenne à grande taille** : plus il y a de code, plus TypeScript est utile
- **Travail en équipe** : les types servent de contrat entre développeurs
- **Applications complexes** : avec beaucoup de logique métier
- **Projets à long terme** : facilite la maintenance

### ⚠️ TypeScript peut être optionnel pour :

- **Petits scripts** : quelques dizaines de lignes
- **Prototypes rapides** : quand la vitesse de développement prime
- **Projets personnels simples** : si vous débutez, commencez par JavaScript

---

## Exemple comparatif

### Version JavaScript

```javascript
function creerProduit(nom, prix, enStock) {
  return {
    nom: nom,
    prix: prix,
    enStock: enStock,
    afficherInfo: function() {
      return `${this.nom} - ${this.prix}€`;
    }
  };
}

const produit = creerProduit("Laptop", 999);  // Oups, on a oublié enStock
console.log(produit.prix);  // undefined ? string ? number ? on ne sait pas
```

### Version TypeScript

```typescript
interface Produit {
  nom: string;
  prix: number;
  enStock: boolean;
  afficherInfo(): string;
}

function creerProduit(nom: string, prix: number, enStock: boolean): Produit {
  return {
    nom: nom,
    prix: prix,
    enStock: enStock,
    afficherInfo: function(): string {
      return `${this.nom} - ${this.prix}€`;
    }
  };
}

// ❌ Erreur détectée immédiatement
const produit = creerProduit("Laptop", 999);
// TypeScript dit : "Il manque le paramètre 'enStock'"

const produitCorrect = creerProduit("Laptop", 999, true);  // ✅ OK
console.log(produitCorrect.prix);  // TypeScript sait que c'est un number
```

---

## Points clés à retenir

1. **TypeScript = JavaScript + Types** : tout ce que vous savez en JavaScript reste valable
2. **Sécurité accrue** : les erreurs sont détectées avant l'exécution
3. **Meilleure expérience de développement** : auto-complétion, refactoring, documentation
4. **Transpilation nécessaire** : TypeScript doit être converti en JavaScript
5. **Adoption croissante** : de plus en plus utilisé dans l'industrie
6. **Courbe d'apprentissage douce** : on peut commencer progressivement

---

## Pour aller plus loin

Une fois les fondamentaux de JavaScript maîtrisés, TypeScript devient une évolution naturelle qui améliore votre productivité et la qualité de votre code. C'est un investissement qui vaut la peine, surtout si vous envisagez de travailler sur des projets professionnels.

### Ressources recommandées :

- **Documentation officielle** : [typescriptlang.org](https://www.typescriptlang.org/)
- **TypeScript Playground** : Testez TypeScript directement dans le navigateur
- **VS Code** : L'éditeur recommandé pour TypeScript

> 🎯 **Conseil** : Ne vous précipitez pas sur TypeScript si vous débutez en JavaScript. Maîtrisez d'abord les fondamentaux de JavaScript (ES6+), puis ajoutez TypeScript quand vous vous sentirez à l'aise.

⏭️ [APIs modernes : Fetch, Storage, Geolocation](/08-ecosysteme-javascript-moderne/04-concepts-avances-apercu/02-apis-modernes.md)
