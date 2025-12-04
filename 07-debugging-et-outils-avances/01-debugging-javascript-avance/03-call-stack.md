🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.1.3 Call Stack et Contexte d'Exécution

## Introduction

Vous savez maintenant mettre votre code en pause et surveiller des variables. Mais comment comprendre **comment on est arrivé là** ? Quelle fonction a appelé quelle fonction ? Dans quel ordre ?

C'est exactement ce que révèle le **Call Stack** (pile d'appels) : il vous montre le **chemin d'exécution** qui a mené votre code jusqu'au point actuel. Un outil indispensable pour comprendre le flux de votre programme !

---

## Qu'est-ce que le Call Stack ?

### Définition simple

Le **Call Stack** (ou pile d'appels en français) est une liste ordonnée qui montre :
- 📞 **Quelle fonction s'exécute actuellement**
- 📞 **Quelle fonction l'a appelée**
- 📞 **Quelle fonction a appelé celle d'avant**
- 📞 Et ainsi de suite jusqu'à la fonction initiale

C'est comme un historique de navigation, mais pour les fonctions de votre code.

### Analogie 1 : Les poupées russes

Imaginez des poupées russes (matriochkas) :
1. Vous ouvrez la plus grande (fonction A)
2. À l'intérieur, il y a une moyenne (fonction B)
3. À l'intérieur, il y a une petite (fonction C)

Le call stack vous montre que vous êtes actuellement dans la plus petite poupée (C), qui est dans la moyenne (B), qui est dans la grande (A).

### Analogie 2 : Un empilement d'assiettes

Le nom "stack" (pile) vient de cette image :
```
┌─────────────┐  ← Fonction actuelle (en haut)
│  fonction3  │
├─────────────┤
│  fonction2  │
├─────────────┤
│  fonction1  │
└─────────────┘  ← Première fonction appelée (en bas)
```

Comme des assiettes empilées :
- La dernière ajoutée est en haut (fonction actuelle)
- Pour atteindre celle du bas, il faut retirer toutes celles du dessus
- Quand une fonction finit, elle est retirée de la pile

---

## Pourquoi le Call Stack est-il important ?

### 1. Comprendre le flux d'exécution

Quand une erreur se produit, vous avez besoin de savoir :
- Dans quelle fonction ça s'est produit ?
- Qui a appelé cette fonction ?
- Avec quels paramètres ?
- Depuis où dans le code ?

Le call stack répond à toutes ces questions.

### 2. Débugger les fonctions imbriquées

Considérez ce code :

```javascript
function calculerTotal() {
  const sousTotal = calculerSousTotal();
  const taxes = calculerTaxes(sousTotal);
  return sousTotal + taxes;
}

function calculerSousTotal() {
  return calculerPrix() * getQuantite();
}

function calculerPrix() {
  // 🐛 Bug ici !
  return produit.prix; // produit est undefined !
}
```

**Sans call stack** : "Il y a une erreur dans `calculerPrix`"
**Avec call stack** : "L'erreur est dans `calculerPrix`, appelée par `calculerSousTotal`, elle-même appelée par `calculerTotal`"

Vous comprenez **le contexte complet** de l'erreur !

### 3. Identifier les boucles infinies

Si votre page freeze (se bloque), le call stack peut révéler une **récursion infinie** :

```
┌─────────────┐
│  maFonction │
├─────────────┤
│  maFonction │
├─────────────┤
│  maFonction │
├─────────────┤
│  maFonction │  ← Toujours la même fonction !
└─────────────┘
```

Vous voyez immédiatement que `maFonction` s'appelle elle-même sans fin.

---

## Comment utiliser le Call Stack dans les DevTools

### Accéder au Call Stack

#### Étape 1 : Mettre le code en pause

Le call stack n'est visible que **quand le code est en pause**. Utilisez :
- Un point d'arrêt (breakpoint)
- L'instruction `debugger;`
- Une erreur qui stoppe l'exécution

#### Étape 2 : Ouvrir les DevTools

- Appuyez sur **F12** (Windows/Linux) ou **Cmd+Option+I** (Mac)
- Allez dans l'onglet **Sources** (Chrome) ou **Debugger** (Firefox)

#### Étape 3 : Localiser le panneau Call Stack

Dans la colonne de droite, cherchez le panneau **"Call Stack"** :
- Il affiche la liste des fonctions empilées
- La fonction actuelle est en haut
- La fonction originelle est en bas

### Lecture du Call Stack

Exemple visuel dans DevTools :

```
Call Stack
┌─────────────────────────────┐
│ ▶ calculerPrix              │ ← Fonction actuelle (en haut)
│   script.js:15              │
├─────────────────────────────┤
│ ▶ calculerSousTotal         │ ← A appelé calculerPrix
│   script.js:11              │
├─────────────────────────────┤
│ ▶ calculerTotal             │ ← A appelé calculerSousTotal
│   script.js:6               │
├─────────────────────────────┤
│ ▶ afficherPanier            │ ← A appelé calculerTotal
│   script.js:2               │
├─────────────────────────────┤
│ ▶ (anonymous)               │ ← Code de départ (global)
│   script.js:20              │
└─────────────────────────────┘
```

**Lecture de bas en haut** :
1. Le code global démarre (ligne 20)
2. Il appelle `afficherPanier` (ligne 2)
3. Qui appelle `calculerTotal` (ligne 6)
4. Qui appelle `calculerSousTotal` (ligne 11)
5. Qui appelle `calculerPrix` (ligne 15) ← **on est ici actuellement**

---

## Naviguer dans le Call Stack

### Cliquer sur une fonction

Quand vous **cliquez sur une fonction** dans le call stack :

1. 📝 **Le code source** se positionne sur la ligne correspondante
2. 👀 **Le panneau Scope** montre les variables de cette fonction
3. 🔍 **Les watch expressions** sont évaluées dans ce contexte

**Exemple pratique** :

```javascript
function a() {
  const messageA = "Je suis dans A";
  b();
}

function b() {
  const messageB = "Je suis dans B";
  // 🔵 Point d'arrêt ici
  c();
}

function c() {
  const messageC = "Je suis dans C";
}
```

Quand le code s'arrête dans `b()` :

**Si vous cliquez sur `b` dans le call stack** :
- Vous voyez `messageB`
- Vous êtes dans le contexte de la fonction `b`

**Si vous cliquez sur `a` dans le call stack** :
- Vous voyez `messageA`
- Vous comprenez comment `b` a été appelée
- Vous êtes dans le contexte de la fonction `a`

### Flèches de navigation

Certains navigateurs affichent des flèches ↑↓ pour naviguer rapidement dans le call stack.

---

## Comprendre le Contexte d'Exécution

### Qu'est-ce qu'un contexte d'exécution ?

Chaque ligne du call stack représente un **contexte d'exécution** (execution context). C'est l'environnement dans lequel une fonction s'exécute.

Un contexte d'exécution contient :

1. 📦 **Les variables locales** de la fonction
2. 📥 **Les paramètres** reçus
3. 🔗 **Les références** aux variables externes (closure)
4. 🎯 **La valeur de `this`**

### Exemple détaillé

```javascript
function calculerRemise(prixOriginal, pourcentage) {
  const montantRemise = prixOriginal * (pourcentage / 100);
  const prixFinal = prixOriginal - montantRemise;

  // 🔵 Point d'arrêt ici

  return prixFinal;
}

const prix = 100;
calculerRemise(prix, 20);
```

Quand le code s'arrête dans `calculerRemise`, le **contexte d'exécution** contient :

```
Contexte de calculerRemise :
├─ prixOriginal: 100        (paramètre)
├─ pourcentage: 20          (paramètre)
├─ montantRemise: 20        (variable locale)
├─ prixFinal: 80            (variable locale)
└─ this: Window             (contexte global)
```

### Le panneau Scope

Le panneau **Scope** dans les DevTools montre exactement le contexte d'exécution :

```
Scope
├─ Local
│  ├─ prixOriginal: 100
│  ├─ pourcentage: 20
│  ├─ montantRemise: 20
│  └─ prixFinal: 80
├─ Closure (si applicable)
└─ Global
   └─ prix: 100
```

**Interprétation** :
- **Local** : Variables de la fonction actuelle
- **Closure** : Variables capturées d'une fonction parente
- **Global** : Variables globales accessibles partout

---

## Exemples pratiques

### Exemple 1 : Fonction simple avec appels imbriqués

```javascript
function etape1() {
  console.log("Étape 1 commence");
  etape2();
  console.log("Étape 1 termine");
}

function etape2() {
  console.log("Étape 2 commence");
  etape3();
  console.log("Étape 2 termine");
}

function etape3() {
  console.log("Étape 3 commence");
  // 🔵 Point d'arrêt ici
  console.log("Étape 3 termine");
}

etape1();
```

**Call Stack au point d'arrêt** :
```
etape3      ← Vous êtes ici
etape2      ← A appelé etape3
etape1      ← A appelé etape2
(anonymous) ← Code de départ
```

**Ordre d'exécution** :
1. `etape1` démarre
2. `etape1` appelle `etape2`
3. `etape2` appelle `etape3`
4. ⏸️ Pause dans `etape3`
5. `etape3` finira (sera retirée de la pile)
6. Retour dans `etape2` qui finira
7. Retour dans `etape1` qui finira

### Exemple 2 : Fonction avec paramètres

```javascript
function formaterNom(prenom, nom) {
  return afficherNomComplet(prenom, nom);
}

function afficherNomComplet(p, n) {
  const nomComplet = creerNomComplet(p, n);
  // 🔵 Point d'arrêt ici
  return nomComplet.toUpperCase();
}

function creerNomComplet(prenom, nom) {
  return `${prenom} ${nom}`;
}

formaterNom("Alice", "Dupont");
```

**Call Stack** :
```
afficherNomComplet   ← p: "Alice", n: "Dupont"
formaterNom          ← prenom: "Alice", nom: "Dupont"
(anonymous)
```

**Dans le Scope** :
- Dans `afficherNomComplet` : `p`, `n`, `nomComplet`
- Dans `formaterNom` : `prenom`, `nom`

Vous voyez comment les paramètres sont passés et renommés entre fonctions.

### Exemple 3 : Gestion d'erreur

```javascript
function traiterDonnees(data) {
  try {
    validerDonnees(data);
  } catch (error) {
    // 🔵 Point d'arrêt ici
    console.error("Erreur:", error.message);
  }
}

function validerDonnees(data) {
  if (!data.email) {
    lancerErreur("Email manquant");
  }
}

function lancerErreur(message) {
  throw new Error(message);
}

traiterDonnees({ nom: "Alice" }); // Pas d'email !
```

**Call Stack dans le catch** :
```
traiterDonnees ← Gère l'erreur
(anonymous)
```

**Call Stack au moment de l'erreur** (avant le catch) :
```
lancerErreur       ← Erreur lancée ici
validerDonnees     ← A appelé lancerErreur
traiterDonnees     ← A appelé validerDonnees
(anonymous)
```

Le call stack vous montre **tout le chemin** qu'a pris l'erreur !

### Exemple 4 : Récursion

```javascript
function factorielle(n) {
  // 🔵 Point d'arrêt ici
  if (n <= 1) {
    return 1;
  }
  return n * factorielle(n - 1);
}

factorielle(4);
```

**Call Stack pour n=1** (fin de la récursion) :
```
factorielle  ← n: 1 (cas de base)
factorielle  ← n: 2
factorielle  ← n: 3
factorielle  ← n: 4
(anonymous)
```

Vous voyez la **pile des appels récursifs** ! Chaque niveau a son propre `n`.

**Déroulement complet** :
1. `factorielle(4)` appelle `factorielle(3)`
2. `factorielle(3)` appelle `factorielle(2)`
3. `factorielle(2)` appelle `factorielle(1)`
4. `factorielle(1)` retourne `1` (cas de base)
5. Puis la pile se "dépile" : 2, 3, 4

### Exemple 5 : Callbacks et événements

```javascript
function initialiser() {
  document.getElementById('btn').addEventListener('click', gererClic);
}

function gererClic() {
  traiterClic();
}

function traiterClic() {
  // 🔵 Point d'arrêt ici
  console.log("Clic traité");
}

initialiser();
```

**Call Stack quand on clique** :
```
traiterClic           ← Fonction de traitement
gererClic             ← Handler de clic
(anonymous)           ← Code interne du navigateur
```

Le call stack montre comment l'événement du navigateur déclenche votre code.

---

## Astuces pour lire le Call Stack

### 1. Lire de bas en haut

Le call stack se lit comme un **historique chronologique** :
- 📕 **Bas** = Début de l'histoire (première fonction)
- 📗 **Milieu** = Étapes intermédiaires
- 📘 **Haut** = Situation actuelle (fonction en cours)

### 2. Repérer les motifs

**Récursion infinie** :
```
maFonction
maFonction
maFonction
maFonction
... (des centaines de fois)
```
→ La fonction s'appelle elle-même sans condition d'arrêt.

**Callbacks imbriqués** :
```
callback3
callback2
callback1
setTimeout
(anonymous)
```
→ Cascade de callbacks (peut indiquer un callback hell).

**Gestion d'erreur** :
```
gererErreur
try...catch
maFonction
```
→ Une erreur a été capturée et gérée.

### 3. Ignorer les fonctions système

Vous verrez parfois des fonctions du navigateur comme :
- `dispatchEvent`
- `invokeTask`
- `runTask`

Vous pouvez les **ignorer** : ce sont des mécanismes internes du navigateur. Concentrez-vous sur **vos fonctions** (celles de votre code).

### 4. Utiliser "Blackbox" pour masquer du code

Si une bibliothèque externe pollue votre call stack (comme jQuery ou React), vous pouvez la "blackboxer" :

1. Clic droit sur une ligne du call stack
2. Sélectionnez **"Blackbox script"**
3. Cette bibliothèque sera masquée du call stack

Utile pour se concentrer sur **votre code uniquement**.

---

## Le panneau Scope en détail

### Structure du Scope

Quand vous êtes en pause dans une fonction, le panneau Scope affiche trois sections :

#### 1. Local (Portée locale)

Toutes les variables de la **fonction actuelle** :
```javascript
function exemple(parametre) {
  const locale = 42;
  let autre = "test";
  // Scope Local contiendra : parametre, locale, autre
}
```

#### 2. Closure (Fermeture)

Variables capturées d'une **fonction parente** :
```javascript
function externe() {
  const valeurExterne = 100;

  function interne() {
    // 🔵 Point d'arrêt ici
    console.log(valeurExterne); // Closure !
  }

  interne();
}
```

Dans le Scope :
```
Local
  (vide)
Closure (externe)
  valeurExterne: 100
```

#### 3. Global (Portée globale)

Variables disponibles **partout** :
```javascript
const CONSTANTE_GLOBALE = 42;
let variableGlobale = "test";

function exemple() {
  // 🔵 Point d'arrêt ici
  // Scope Global contiendra : CONSTANTE_GLOBALE, variableGlobale
}
```

### Modifier des variables dans Scope

Astuce : vous pouvez **modifier des valeurs** directement dans le panneau Scope !

1. Double-cliquez sur une valeur
2. Modifiez-la
3. Appuyez sur **Entrée**

Utile pour **tester des hypothèses** : "Que se passerait-il si cette variable valait 0 ?"

---

## Débugger avec le Call Stack : Workflow

### Étape 1 : Identifier le problème

Une erreur se produit :
```
Uncaught TypeError: Cannot read property 'prix' of undefined
    at calculerPrix (script.js:15)
```

### Étape 2 : Mettre un point d'arrêt

Placez un breakpoint à la ligne de l'erreur (ligne 15).

### Étape 3 : Reproduire le bug

Exécutez l'action qui cause le bug.

### Étape 4 : Analyser le Call Stack

Quand le code s'arrête, regardez le call stack :
```
calculerPrix       ← Erreur ici (produit undefined)
calculerSousTotal  ← Qui a appelé ?
calculerTotal      ← Origine du problème ?
afficherPanier     ← Point de départ
```

### Étape 5 : Remonter la chaîne

Cliquez sur chaque fonction dans le call stack (de haut en bas) :

1. **Dans `calculerPrix`** : `produit` est `undefined` ✗
2. **Dans `calculerSousTotal`** : D'où vient `produit` ?
3. **Dans `calculerTotal`** : Ah ! `produit` n'est jamais défini ✓

Vous avez trouvé la **source du problème** !

### Étape 6 : Vérifier les variables

Dans chaque fonction, regardez le panneau **Scope** :
- Quelles variables existent ?
- Quelles valeurs ont-elles ?
- Laquelle est inattendue ?

### Étape 7 : Corriger

Maintenant que vous comprenez le flux, corrigez le bug :

```javascript
function calculerTotal(produit) { // ← Ajoutez le paramètre !
  const sousTotal = calculerSousTotal(produit); // ← Passez-le !
  // ...
}
```

---

## Cas pratiques avancés

### Cas 1 : Débugger une Promise

```javascript
function chargerDonnees() {
  fetch('/api/data')
    .then(response => response.json())
    .then(data => traiterDonnees(data))
    .catch(error => {
      // 🔵 Point d'arrêt ici
      console.error(error);
    });
}

function traiterDonnees(data) {
  // Erreur quelque part ici
}

chargerDonnees();
```

**Call Stack** :
```
(anonymous)        ← Catch de la Promise
Promise.then
traiterDonnees
(anonymous)
```

Vous voyez que l'erreur vient de `traiterDonnees`, appelée via une Promise.

### Cas 2 : Débugger async/await

```javascript
async function initialiser() {
  const utilisateur = await chargerUtilisateur();
  await afficherProfil(utilisateur);
}

async function chargerUtilisateur() {
  // 🔵 Point d'arrêt ici
  const response = await fetch('/api/user');
  return await response.json();
}

initialiser();
```

**Call Stack** :
```
chargerUtilisateur
initialiser
(anonymous)
```

Le call stack est plus **simple et lisible** qu'avec les Promises classiques !

### Cas 3 : Débugger des EventListeners

```javascript
document.getElementById('form').addEventListener('submit', function(e) {
  e.preventDefault();
  validerFormulaire();
});

function validerFormulaire() {
  const email = document.getElementById('email').value;
  // 🔵 Point d'arrêt ici
  if (!email.includes('@')) {
    afficherErreur('Email invalide');
  }
}

function afficherErreur(message) {
  console.error(message);
}
```

**Call Stack lors de la soumission** :
```
validerFormulaire
(anonymous)        ← Fonction fléchée du addEventListener
```

Vous voyez comment l'événement déclenche votre code.

---

## Erreurs courantes et solutions

### "Le Call Stack est vide"

**Cause** : Votre code n'est pas en pause.

**Solution** :
- Placez un point d'arrêt
- Utilisez `debugger;` dans votre code
- Attendez qu'une erreur se produise

### "Je vois plein de fonctions inconnues"

**Cause** : Code des bibliothèques externes (React, jQuery, etc.)

**Solutions** :
1. Utilisez le **Blackbox** pour les masquer
2. Cherchez **vos fonctions** dans la liste
3. Les fonctions de bibliothèques sont souvent entre parenthèses : `(anonymous)`

### "Le Call Stack est très long"

**Cause possible** : Récursion profonde ou callbacks imbriqués

**Solutions** :
1. Vérifiez qu'il n'y a pas de récursion infinie
2. Repérez les motifs répétitifs
3. Concentrez-vous sur les **premières et dernières** fonctions

### "Je ne comprends pas l'ordre"

**Rappel** : Le call stack se lit **de bas en haut** :
- **Bas** = Fonction appelée en premier (début)
- **Haut** = Fonction actuelle (maintenant)

---

## Call Stack vs Console

### Console

La console montre les **résultats** :
```javascript
console.log("Étape 1");
console.log("Étape 2");
console.log("Étape 3");
```

**Affiche** :
```
Étape 1
Étape 2
Étape 3
```

Vous voyez **quoi**, mais pas **comment**.

### Call Stack

Le call stack montre le **chemin** :
```
etape3
etape2
etape1
(anonymous)
```

Vous voyez **comment** on est arrivé là !

### Utilisation combinée

**Best practice** : Utilisez les deux ensemble :
1. **Console** : Pour voir les valeurs et l'avancement
2. **Call Stack** : Pour comprendre le flux et tracer les bugs

---

## Points clés à retenir

📚 **Call Stack = Historique des appels**
- Montre quelle fonction a appelé quelle fonction
- Se lit de bas (début) en haut (maintenant)
- Visible uniquement quand le code est en pause

🔍 **Contexte d'exécution = Environnement d'une fonction**
- Variables locales
- Paramètres
- Closures
- Valeur de `this`

🎯 **Panneau Scope = Variables disponibles**
- Local : Variables de la fonction actuelle
- Closure : Variables capturées
- Global : Variables globales

🛠️ **Utilisation pour débugger**
- Cliquez sur une fonction pour voir son contexte
- Remontez le call stack pour trouver l'origine d'un bug
- Identifiez les récursions infinies
- Comprenez les callbacks et événements

📊 **Navigation intelligente**
- Blackbox les bibliothèques externes
- Focalisez sur vos fonctions
- Utilisez le Scope pour voir les variables
- Modifiez les valeurs pour tester des hypothèses

---

## Pour aller plus loin

Le call stack est le **cœur du debugging**. Une fois que vous le maîtrisez, le debugging asynchrone (Promises, async/await) devient beaucoup plus simple.

Dans la prochaine section, nous verrons justement comment débugger du code asynchrone avec le call stack !

---

> 💡 **Astuce de pro** :
> Le call stack vous raconte une histoire. Apprenez à la lire, et vous comprendrez 80% de vos bugs deux fois plus vite !
>
> *"Le code ne ment jamais, mais il ne dit pas toujours toute la vérité. Le call stack, lui, révèle tout."* 🔍

⏭️ [Debugging asynchrone (Promises, async/await)](/07-debugging-et-outils-avances/01-debugging-javascript-avance/04-debugging-asynchrone.md)
