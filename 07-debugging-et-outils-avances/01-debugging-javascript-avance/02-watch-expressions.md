🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.1.2 Watch Expressions

## Introduction

Vous savez maintenant utiliser les points d'arrêt conditionnels pour mettre votre code en pause au bon moment. Mais une fois le code en pause, comment suivre efficacement l'évolution de vos variables ?

C'est là qu'interviennent les **Watch Expressions** (expressions surveillées) : un outil puissant qui vous permet de **surveiller en temps réel** les valeurs qui vous intéressent pendant le debugging.

---

## Qu'est-ce qu'une Watch Expression ?

### Définition simple

Une **Watch Expression** est une expression JavaScript que vous demandez aux DevTools de **calculer et d'afficher** automatiquement chaque fois que votre code est en pause.

Au lieu de taper manuellement dans la console pour vérifier une valeur, vous configurez une fois votre "surveillance" et les DevTools vous montrent automatiquement le résultat à chaque arrêt.

### Analogie

Imaginez que vous êtes un scientifique qui observe une expérience :
- **Sans watch expressions** : Vous devez noter manuellement chaque mesure à chaque étape
- **Avec watch expressions** : Vous avez des instruments qui affichent automatiquement les mesures qui vous intéressent

---

## Le problème sans Watch Expressions

### Scénario typique

Vous débuggez ce code :

```javascript
function calculerPanier(articles) {
  let total = 0;
  let nombreArticles = 0;
  let articlesPremium = [];

  for (let article of articles) {
    // 🔵 Point d'arrêt ici
    total += article.prix * article.quantite;
    nombreArticles += article.quantite;

    if (article.premium) {
      articlesPremium.push(article);
    }
  }

  return { total, nombreArticles, articlesPremium };
}
```

### Sans Watch Expressions 😓

À chaque arrêt, vous devez taper dans la console :
```javascript
> total
> nombreArticles
> articlesPremium.length
> article.prix
> article.quantite
> article.prix * article.quantite
```

**Inconvénients** :
- 😫 Répétitif et fatigant
- 🐌 Lent (il faut tout retaper)
- 🤔 Risque d'oublier de vérifier quelque chose
- ❌ Difficile de comparer l'évolution des valeurs

### Avec Watch Expressions ✨

Vous configurez une fois vos expressions surveillées, et à chaque arrêt, les DevTools affichent automatiquement :
- `total` → 156.50
- `nombreArticles` → 5
- `articlesPremium.length` → 2
- `article.prix` → 25.00
- `article.quantite` → 3
- `article.prix * article.quantite` → 75.00

**Avantages** :
- ⚡ Instantané
- 👁️ Vision globale d'un coup d'œil
- 📊 Suivi de l'évolution facile
- 🎯 Aucune valeur oubliée

---

## Comment utiliser les Watch Expressions

### Ouvrir le panneau Watch

#### Étape 1 : Ouvrir les DevTools
- Appuyez sur **F12** (Windows/Linux) ou **Cmd+Option+I** (Mac)
- Allez dans l'onglet **Sources**

#### Étape 2 : Localiser le panneau Watch
Dans la colonne de droite, vous trouverez plusieurs panneaux. Cherchez **"Watch"** :
- Si vous le voyez, cliquez dessus pour le déplier
- Si vous ne le voyez pas, cliquez sur les **"︙"** (trois points) et activez-le

### Ajouter une Watch Expression

#### Méthode visuelle (recommandée)

1. Cliquez sur le **"+"** dans le panneau Watch
2. Une zone de texte apparaît
3. Tapez votre expression JavaScript
4. Appuyez sur **Entrée** pour valider

#### Méthode alternative

1. Clic droit dans le panneau Watch
2. Sélectionnez **"Add watch expression"**
3. Tapez votre expression
4. Validez avec **Entrée**

### Exemple pas à pas

Imaginons que vous débuggez une fonction de calcul de remise :

```javascript
function calculerRemise(prix, codePromo) {
  let remise = 0;
  let prixFinal = prix;

  // 🔵 Point d'arrêt ici

  if (codePromo === "PROMO10") {
    remise = prix * 0.10;
  } else if (codePromo === "PROMO20") {
    remise = prix * 0.20;
  }

  prixFinal = prix - remise;

  return prixFinal;
}
```

**Ajoutez ces watch expressions** :
1. Cliquez sur "+" et tapez `prix` → Entrée
2. Cliquez sur "+" et tapez `codePromo` → Entrée
3. Cliquez sur "+" et tapez `remise` → Entrée
4. Cliquez sur "+" et tapez `prixFinal` → Entrée
5. Cliquez sur "+" et tapez `prix - remise` → Entrée

Maintenant, quand votre code s'arrête, vous voyez tout d'un coup d'œil ! 👀

---

## Types d'expressions surveillées

### 1. Variables simples

Les plus courantes : surveillez simplement une variable.

```javascript
// Watch expressions :
nomUtilisateur
age
email
isConnecte
```

**Affichage dans Watch** :
```
nomUtilisateur: "Alice"
age: 25
email: "alice@example.com"
isConnecte: true
```

### 2. Propriétés d'objets

Accédez aux propriétés imbriquées.

```javascript
// Watch expressions :
user.nom
user.adresse.ville
user.preferences.theme
commande.articles.length
```

**Affichage dans Watch** :
```
user.nom: "Bob"
user.adresse.ville: "Paris"
user.preferences.theme: "dark"
commande.articles.length: 5
```

### 3. Calculs et expressions

Surveillez des calculs complexes.

```javascript
// Watch expressions :
prix * quantite
montantTotal - remise
articles.length * prixUnitaire
Math.round(moyenne * 100) / 100
```

**Affichage dans Watch** :
```
prix * quantite: 150.50
montantTotal - remise: 135.45
articles.length * prixUnitaire: 125.00
Math.round(moyenne * 100) / 100: 18.56
```

### 4. Conditions et comparaisons

Vérifiez des conditions booléennes.

```javascript
// Watch expressions :
age >= 18
prix > 100
articles.length === 0
nom.includes('Admin')
```

**Affichage dans Watch** :
```
age >= 18: true
prix > 100: false
articles.length === 0: false
nom.includes('Admin'): true
```

### 5. Méthodes de tableaux

Surveillez des transformations de données.

```javascript
// Watch expressions :
articles.map(a => a.prix)
nombres.filter(n => n > 10)
prices.reduce((sum, p) => sum + p, 0)
users.find(u => u.id === 5)
```

**Affichage dans Watch** :
```
articles.map(a => a.prix): [10, 20, 15, 30]
nombres.filter(n => n > 10): [15, 20, 25]
prices.reduce((sum, p) => sum + p, 0): 75
users.find(u => u.id === 5): {id: 5, nom: "Eve"}
```

### 6. Conversions de types

Vérifiez les types et conversions.

```javascript
// Watch expressions :
typeof valeur
valeur.toString()
Number(texte)
Boolean(donnee)
JSON.stringify(objet)
```

**Affichage dans Watch** :
```
typeof valeur: "string"
valeur.toString(): "42"
Number(texte): 123
Boolean(donnee): true
JSON.stringify(objet): '{"nom":"Alice","age":25}'
```

---

## Exemples pratiques par situation

### Situation 1 : Débugger une boucle

```javascript
function trouverMaximum(nombres) {
  let max = nombres[0];

  for (let i = 1; i < nombres.length; i++) {
    // 🔵 Point d'arrêt ici
    if (nombres[i] > max) {
      max = nombres[i];
    }
  }

  return max;
}
```

**Watch expressions recommandées** :
```javascript
i
nombres[i]
max
nombres.length
i < nombres.length
nombres[i] > max
```

**Utilité** : Vous voyez l'évolution de `i`, la valeur actuelle testée, et si elle devient le nouveau maximum.

### Situation 2 : Débugger un formulaire

```javascript
function validerFormulaire(donnees) {
  const errors = [];

  // 🔵 Point d'arrêt ici

  if (!donnees.email.includes('@')) {
    errors.push('Email invalide');
  }

  if (donnees.age < 18) {
    errors.push('Vous devez être majeur');
  }

  return errors;
}
```

**Watch expressions recommandées** :
```javascript
donnees.email
donnees.email.includes('@')
donnees.age
donnees.age >= 18
errors
errors.length
```

**Utilité** : Vérifiez les validations et voyez les erreurs s'accumuler.

### Situation 3 : Débugger un calcul de panier

```javascript
function calculerPanier(articles, codePromo) {
  let sousTotal = 0;

  // 🔵 Point d'arrêt ici

  for (let article of articles) {
    sousTotal += article.prix * article.quantite;
  }

  let remise = codePromo ? sousTotal * 0.10 : 0;
  let total = sousTotal - remise;
  let tva = total * 0.20;
  let totalTTC = total + tva;

  return totalTTC;
}
```

**Watch expressions recommandées** :
```javascript
articles.length
sousTotal
codePromo
remise
total
tva
totalTTC
sousTotal - remise
(sousTotal - remise) * 1.20
```

**Utilité** : Suivez chaque étape du calcul et vérifiez les montants intermédiaires.

### Situation 4 : Débugger des données asynchrones

```javascript
async function chargerUtilisateur(id) {
  let utilisateur = null;
  let erreur = null;

  try {
    // 🔵 Point d'arrêt ici
    const reponse = await fetch(`/api/users/${id}`);
    utilisateur = await reponse.json();
  } catch (e) {
    erreur = e.message;
  }

  return { utilisateur, erreur };
}
```

**Watch expressions recommandées** :
```javascript
id
utilisateur
erreur
utilisateur?.nom
utilisateur?.email
typeof utilisateur
```

**Utilité** : Vérifiez si les données sont chargées correctement et leur structure.

### Situation 5 : Débugger des transformations de données

```javascript
function traiterCommandes(commandes) {
  // 🔵 Point d'arrêt ici

  const commandesValides = commandes.filter(c => c.montant > 0);
  const montants = commandesValides.map(c => c.montant);
  const total = montants.reduce((sum, m) => sum + m, 0);
  const moyenne = total / commandesValides.length;

  return { total, moyenne };
}
```

**Watch expressions recommandées** :
```javascript
commandes.length
commandesValides.length
montants
total
moyenne
commandesValides.length === 0
```

**Utilité** : Suivez chaque transformation et détectez les cas limites (division par zéro).

---

## Fonctionnalités avancées

### Déplier les objets et tableaux

Quand vous surveillez un objet ou un tableau, vous pouvez le **déplier** dans le panneau Watch :

```javascript
// Watch expression :
user
```

**Affichage** :
```
▶ user: {nom: "Alice", age: 25, ...}
  // Cliquez sur ▶ pour déplier :
▼ user: Object
    nom: "Alice"
    age: 25
    email: "alice@example.com"
  ▶ adresse: Object
    isActif: true
```

Vous pouvez naviguer dans la structure complète sans écrire plusieurs watch expressions.

### Surveiller this

Dans un contexte d'objet ou de classe, surveillez `this` :

```javascript
class Compteur {
  constructor() {
    this.valeur = 0;
  }

  incrementer() {
    // 🔵 Point d'arrêt ici
    this.valeur++;
  }
}
```

**Watch expression** :
```javascript
this
this.valeur
```

### Expressions avec fonctions

Vous pouvez même appeler des fonctions :

```javascript
// Watch expressions :
Math.abs(nombre)
texte.toUpperCase()
date.toLocaleDateString()
array.slice(0, 3)
```

⚠️ **Attention** : Évitez les fonctions qui modifient l'état (effets de bord) !

### Opérateur de coalescence nulle (??)

Gérez les valeurs null/undefined :

```javascript
// Watch expressions :
donnees?.utilisateur
utilisateur?.adresse?.ville
config?.theme ?? "default"
```

Très utile pour éviter les erreurs "Cannot read property of undefined".

---

## Gérer vos Watch Expressions

### Modifier une expression

1. **Double-cliquez** sur l'expression dans le panneau Watch
2. Modifiez le texte
3. Appuyez sur **Entrée** pour valider

Ou :

1. **Clic droit** sur l'expression
2. Sélectionnez **"Edit watch expression"**
3. Modifiez et validez

### Supprimer une expression

**Méthode 1** : Cliquez sur le **"−"** (moins) à côté de l'expression

**Méthode 2** : Clic droit → **"Delete watch expression"**

### Supprimer toutes les expressions

**Clic droit** dans le panneau Watch → **"Delete all watch expressions"**

Pratique pour repartir de zéro sur un nouveau bug.

### Réorganiser l'ordre

Malheureusement, on ne peut pas réorganiser l'ordre directement. Solution :
1. Notez vos expressions quelque part
2. Supprimez tout
3. Recréez dans l'ordre souhaité

💡 **Astuce** : Mettez les expressions les plus importantes en premier !

---

## Quand une expression affiche "Not available"

### Pourquoi ce message ?

Vous voyez `<not available>` quand :

1. **La variable n'existe pas encore**
   ```javascript
   function exemple() {
     // 🔵 Point d'arrêt AVANT la déclaration
     let resultat = 42; // resultat n'existe pas encore
   }
   ```

2. **La variable est hors scope (portée)**
   ```javascript
   function a() {
     let x = 10;
   }

   function b() {
     // 🔵 Point d'arrêt ici
     // x n'est pas accessible ici
   }
   ```

3. **La propriété n'existe pas sur l'objet**
   ```javascript
   const user = { nom: "Alice" };
   // Watch : user.age → <not available> (la propriété n'existe pas)
   ```

### Solutions

**Utilisez l'opérateur optionnel** :
```javascript
// Au lieu de :
user.adresse.ville

// Utilisez :
user?.adresse?.ville
```

Si `adresse` n'existe pas, vous verrez `undefined` au lieu d'une erreur.

**Vérifiez l'existence** :
```javascript
// Watch expression :
typeof variable !== 'undefined' ? variable : "n/a"
```

---

## Astuces et bonnes pratiques

### ✅ À faire

1. **Nommez clairement vos expressions**
   ```javascript
   // ✅ BON - expressif
   user.nom
   articles.length
   prixTotal - remise

   // ❌ MOINS BON - on ne sait pas ce que c'est
   x
   val
   tmp
   ```

2. **Groupez logiquement**
   - Variables d'entrée en haut
   - Calculs intermédiaires au milieu
   - Résultats finaux en bas

3. **Surveillez les conditions de vos if**
   ```javascript
   if (age >= 18 && hasPermission) {
     // ...
   }

   // Watch expressions :
   age >= 18
   hasPermission
   age >= 18 && hasPermission
   ```

4. **Utilisez des expressions pour tester**
   ```javascript
   // Tester si un tableau contient une valeur :
   array.includes(valeurCherchee)

   // Tester si toutes les conditions sont remplies :
   condition1 && condition2 && condition3
   ```

5. **Surveillez la longueur des collections**
   ```javascript
   articles.length
   erreurs.length
   Object.keys(config).length
   ```

### ❌ À éviter

1. **Expressions avec effets de bord**
   ```javascript
   // ❌ MAUVAIS - modifie le tableau !
   array.push(item)

   // ❌ MAUVAIS - modifie le compteur !
   compteur++

   // ✅ BON - observe seulement
   array.length
   compteur
   ```

2. **Expressions trop complexes**
   ```javascript
   // ❌ DIFFICILE À LIRE
   users.filter(u => u.age > 18).map(u => u.orders).flat().reduce((s, o) => s + o.total, 0)

   // ✅ MIEUX - découpez
   usersAdultes = users.filter(u => u.age > 18)
   ordersAdultes = usersAdultes.map(u => u.orders).flat()
   totalOrders = ordersAdultes.reduce((s, o) => s + o.total, 0)
   ```

3. **Trop d'expressions**
   - Plus de 10-15 expressions deviennent difficiles à suivre
   - Supprimez celles qui ne sont plus utiles
   - Gardez uniquement les essentielles

4. **Expressions redondantes**
   ```javascript
   // ❌ Redondant
   user.nom
   user

   // ✅ Surveillez juste "user" et dépliez-le
   user
   ```

---

## Différences entre Watch et Console

### Console

**Utilisation** : Taper manuellement des commandes quand le code est en pause

**Avantages** :
- ✅ Exploratiion libre et flexible
- ✅ Peut exécuter n'importe quel code
- ✅ Historique des commandes

**Inconvénients** :
- ❌ Il faut tout retaper à chaque arrêt
- ❌ Difficile de suivre plusieurs valeurs
- ❌ Pas de persistance entre les sessions

### Watch Expressions

**Utilisation** : Configuration une fois, affichage automatique

**Avantages** :
- ✅ Affichage automatique à chaque arrêt
- ✅ Vue d'ensemble claire
- ✅ Suivi facile de l'évolution
- ✅ Configuration persistante

**Inconvénients** :
- ❌ Expressions fixes (pas d'exploration libre)
- ❌ Moins flexible que la console

### Quand utiliser quoi ?

| Situation | Outil recommandé |
|-----------|------------------|
| Explorer une structure de données complexe | **Console** |
| Suivre l'évolution de variables connues | **Watch** |
| Tester rapidement une hypothèse | **Console** |
| Débugger une boucle avec plusieurs variables | **Watch** |
| Exécuter une fonction de test | **Console** |
| Surveiller plusieurs calculs en parallèle | **Watch** |

**Meilleure pratique** : Utilisez les **deux ensemble** !
- **Watch** pour les valeurs que vous surveillez systématiquement
- **Console** pour l'exploration ponctuelle

---

## Cas d'usage avancés

### Débugger un algorithme de tri

```javascript
function triBulles(tableau) {
  let echanges = 0;

  for (let i = 0; i < tableau.length; i++) {
    for (let j = 0; j < tableau.length - 1 - i; j++) {
      // 🔵 Point d'arrêt ici
      if (tableau[j] > tableau[j + 1]) {
        [tableau[j], tableau[j + 1]] = [tableau[j + 1], tableau[j]];
        echanges++;
      }
    }
  }

  return echanges;
}
```

**Watch expressions** :
```javascript
i
j
tableau.length
tableau[j]
tableau[j + 1]
tableau[j] > tableau[j + 1]
echanges
tableau
```

### Débugger une récursion

```javascript
function factorielle(n) {
  // 🔵 Point d'arrêt ici
  if (n <= 1) {
    return 1;
  }
  return n * factorielle(n - 1);
}
```

**Watch expressions** :
```javascript
n
n <= 1
n - 1
```

Observez comment `n` diminue à chaque appel récursif !

### Débugger un state management

```javascript
function updateState(state, action) {
  // 🔵 Point d'arrêt ici
  const newState = { ...state };

  switch (action.type) {
    case 'INCREMENT':
      newState.count += action.payload;
      break;
    case 'DECREMENT':
      newState.count -= action.payload;
      break;
  }

  return newState;
}
```

**Watch expressions** :
```javascript
state
state.count
action.type
action.payload
newState.count
newState.count === state.count
```

---

## Workflow de debugging efficace

### 1. Préparez vos watch expressions

**AVANT** de lancer votre code :
1. Identifiez les variables importantes
2. Ajoutez-les dans Watch
3. Ajoutez les calculs critiques
4. Ajoutez les conditions de vos if/while

### 2. Placez vos points d'arrêt

Avec vos watch expressions configurées, placez vos breakpoints stratégiquement.

### 3. Exécutez et observez

Lancez votre code. À chaque arrêt :
1. 👀 Regardez le panneau Watch en premier
2. 🔍 Identifiez les valeurs anormales
3. 💭 Formulez des hypothèses
4. ⏭️ Avancez pas à pas (Step Over/Into)

### 4. Affinez vos expressions

Pendant le debugging :
- Ajoutez des expressions si vous remarquez quelque chose
- Supprimez celles qui ne sont plus utiles
- Modifiez celles qui ne sont pas assez précises

### 5. Utilisez la console en complément

Pour les explorations ponctuelles, utilisez la console sans polluer vos watch expressions.

---

## Raccourcis utiles

### Pendant le debugging

| Action | Raccourci (Windows/Linux) | Raccourci (Mac) |
|--------|---------------------------|-----------------|
| Continuer | **F8** | **F8** ou **Cmd+\\** |
| Step Over | **F10** | **F10** ou **Cmd+'** |
| Step Into | **F11** | **F11** ou **Cmd+;** |
| Step Out | **Shift+F11** | **Shift+F11** ou **Cmd+Shift+;** |

### Navigation

| Action | Comment |
|--------|---------|
| Ajouter watch | **Clic sur "+"** dans panneau Watch |
| Modifier watch | **Double-clic** sur l'expression |
| Supprimer watch | **Clic sur "−"** à côté de l'expression |
| Supprimer tout | **Clic droit** → "Delete all" |

---

## Dépannage

### "J'ai trop d'expressions, c'est illisible"

**Solutions** :
1. Supprimez les expressions obsolètes
2. Gardez maximum 10-15 expressions actives
3. Utilisez plutôt les objets dépliables :
   ```javascript
   // Au lieu de :
   user.nom
   user.email
   user.age

   // Utilisez :
   user  // puis dépliez
   ```

### "Mon expression affiche une erreur"

**Causes** :
1. Erreur de syntaxe JavaScript
2. Variable qui n'existe pas
3. Propriété inaccessible

**Solutions** :
1. Testez votre expression dans la console d'abord
2. Utilisez l'opérateur optionnel `?.`
3. Ajoutez des vérifications de type

### "Je ne vois pas mes watch expressions"

**Vérifications** :
1. Êtes-vous dans l'onglet **Sources** ?
2. Le panneau **Watch** est-il visible/déplié ?
3. Le code est-il actuellement en pause ?
4. Avez-vous bien ajouté des expressions ?

### "Les valeurs ne se mettent pas à jour"

**Cause probable** : Le code n'est pas en pause

**Solution** :
1. Placez un point d'arrêt
2. Exécutez votre code jusqu'à l'arrêt
3. Les watch expressions se mettent à jour automatiquement

---

## Différences entre navigateurs

### Chrome DevTools

- Panneau "Watch" très visible
- Interface claire et intuitive
- Icônes + et − bien placés
- Support complet ES6+

### Firefox Developer Tools

- Panneau "Watch expressions" dans la section Variables
- Légèrement différent visuellement
- Mêmes fonctionnalités de base
- Bon support ES6+

### Safari Web Inspector

- Similaire à Chrome
- Quelques différences d'UI
- Fonctionnalités identiques

**Recommandation** : Les concepts sont les mêmes partout. Apprenez sur un navigateur, utilisez sur tous !

---

## Points clés à retenir

🎯 **Watch = Surveillance automatique**
- Configurez une fois, affichez à chaque arrêt
- Gain de temps énorme sur les debuggings répétitifs

👁️ **Vue d'ensemble instantanée**
- Voyez plusieurs valeurs simultanément
- Identifiez rapidement les anomalies
- Suivez l'évolution des variables

✏️ **Types d'expressions**
- Variables simples : `nomVariable`
- Propriétés : `objet.propriete`
- Calculs : `a * b + c`
- Conditions : `x > 10 && y < 20`
- Méthodes : `array.filter(...)`, `typeof x`

🔧 **Complémentaire à la console**
- Watch = surveillance systématique
- Console = exploration ponctuelle
- Utilisez les deux ensemble !

⚠️ **Évitez les effets de bord**
- Ne modifiez jamais l'état dans une watch expression
- Observez, ne transformez pas

🎨 **Organisez vos expressions**
- Maximum 10-15 expressions actives
- Supprimez celles qui ne servent plus
- Les plus importantes en premier

---

## Pour aller plus loin

Les watch expressions sont la base de tout bon workflow de debugging. Une fois que vous les maîtrisez, vous êtes prêt à découvrir :

- **Call stack** : comprendre la pile d'appels de fonctions
- **Scope** : voir toutes les variables disponibles
- **Step debugging** : avancer pas à pas dans le code

---

> 💡 **Citation de Brian Kernighan** :
> *"Everyone knows that debugging is twice as hard as writing a program in the first place. So if you're as clever as you can be when you write it, how will you ever debug it?"*
>
> La réponse : avec de bons outils comme les Watch Expressions ! 🔍

⏭️ [Call stack et contexte d'exécution](/07-debugging-et-outils-avances/01-debugging-javascript-avance/03-call-stack.md)
